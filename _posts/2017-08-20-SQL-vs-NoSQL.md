---
layout: post
title: SQL vs NoSQL
---
Vengo a hablarles de algo muy feo. Es casi casi una historia de terror. Si tienen un negocio propio, o son freelancers, me van a entender. Les vengo a hablar de facturas. Más específicamente de cómo guardar facturas en una base de datos.

Trabajo en una [empresa de servicios financieros](http://resuelve.mx) y estoy encargado de llevar la parte tecnológica de una [línea de negocios que hace contabilidad para PyMEs](http://enconta.com). Una de las funcionalidades más importantes de la plataforma que tenemos es descargar las facturas de nuestros clientes, tanto las que emiten como las que les emitieron. Una vez descargadas, tenemos que guardar la información de las mismas en una base de datos para poder sacar estadísticas.

## Qué es una factura?
Una factura, por si usted no lo sabe, es un archivo XML que contiene la información de un intercambio de dinero por servicios o productos. Se escogió XML porque gobierno a huevo trabaja con cosas viejas y feas. La información básica que guarda la factura es:
* Datos de quien la emite y recibe
	* RFC
	* Dirección
* Tabla de conceptos
* Tabla de impuestos
	* IVA
	* Impuestos retenidos y trasladados
* Datos generales de la factura
	* Cuando se emitió
	* Dónde se emitió
	* Cómo se pagó
	* Identificadores únicos y sellos de comprobación

Cuando esta línea de negocio iba a empezar, la empresa contrató a unos consultores gringos para hacer la primera versión de la plataforma. El problema que surgió de esto es que, por muy fregones y bien intencionados que hayan sido esos gringos, no entendieron el desmadre que tiene el SAT.

## Cómo almacenar una factura
Si hoy viera la estructura básica de una factura, no dudaría en guardarla en una base de datos relacional, en una estructura de tablas algo como:

* Facturas
* Emisores
* Receptores
* Conceptos
* Impuestos

Y si su empresa sólo va a facturar cosas simples, esta estructura es ideal. Pero qué pasa si van a facturar otra cosa? Digamos que facturan nómina. La nómina a nivel del XML es otro nodo (completamente opcional). Este nodo contiene cosas que sólo vas a ver en facturas de nómina, como deducciones, percepciones, empleados, etc. Si sólo vas a facturar tus facturas de operación y las de la nómina, igual y modificas la base de datos anterior y agregas algunas tablas más para poder sacar los datos de la nómina:

* Nómina
* Percepciones
* Deducciones
* Empleados

Eso todavía está manejable. El problema con el que nos enfrentamos nosotros es que el SAT permite otros muchos tipos de factura, con más nodos y cosas que almacenar. Peor tantito, tenemos clientes que usan facturas de este tipo. Por ende, tenemos que almacenar tanto como se pueda de estas facturas.

Si quieres almacenar la información de facturas de todos tipos, igual y tu lista de tablas va a terminar siendo algo así:
* Facturas
* Emisores
* Receptores
* Conceptos
* Impuestos
* Nómina
* Percepciones
* Deducciones
* Empleados
* Datos Aduanales
* Impuestos Locales
* Datos INE
* …

Esto es una mala idea. La forma como nosotros lo habíamos resuelto es, “pues no guardo más información”. Llegó el punto en el que ya no queríamos guardar cada dato particular de las facturas raras, por lo que sólo guardamos las cosas que se pueden, lo demás se queda en el XML.

Cuando nos pedían un reporte de alguna de las tablas con tres cadenas de relación, nuestra base chillaba. En este momento teníamos al rededor de 5 millones de facturas, por lo que la base tampoco era chica. Si nada más hubiera cambiado, la plataforma habría aguantado. Obviamente eso no pasó, al SAT se le ocurrió hacer de las suyas.

Igual y han escuchado últimamente que hay un cambio de versión en las facturas. Pasamos de 3.2 a 3.3. Como hacienda no tiene la más remota idea de qué es Semver, 3.3 es un breaking change mamón.

Cosas que antes eran opcionales ahora son obligatorias, cosas que antes eran obligatorias ahora son opcionales. Casi todas las propiedades cambiaron de nombre, no me pregunten por qué. Hubo propiedades que (con nombre diferente) ahora están en otro nodo. Ahora un buen de cosas vienen de catálogos donde antes eran texto libre. En resumidas cuentas todo cambió.

Cómo lidias con eso? Podrías migrar tu base de datos a que ahora se ajuste al nuevo esquema. Pero, y tus facturas viejas? Tal vez alguien haría una base de datos nueva para las facturas 3.3 y se quedaría con la anterior para 3.2. No quiero ni pensar en lo que eso involucraría a nivel código para poder tener acceso a todo. Este fue el momento en el que nos dimos cuenta que nuestra solución no iba a funcionar y había que cambiar el sistema.

## Encontrando una mejor solución
Empezamos a investigar alternativas de base de datos y descubrimos varias cosas interesantes. Una, sabían que hay bases de datos específicamente hechas para XML? Sabían que están horribles? Que usan comandos de tipo XPATH para poder hacer queries?

No iba a ser viable que el equipo aprendiera (a regañadientes) un nuevo sistema de queries para poder tener acceso a las facturas. Iba a ser demasiado código que se tendría que cambiar. Tenía que haber una mejor solución.

Alguien dijo que igual y DBs basadas en documentos, y sonó bien. Le rascamos un poco y nos dimos cuenta de que había pocas opciones viables. Necesitábamos algo que llevara ya algunos años fuera, que pudiéramos montar en la nube, preferiblemente pagándole a alguien por administrar los servers y que supiéramos que iba a aguantar madrazos.

Las opciones que surgieron fueron DynamoDB, CouchDB y MongoDB.

### DynamoDB
DynamoDB la usamos en la empresa en otras líneas de negocio, y funciona bien. El equipo que la usa nos dijo que no nos lo recomendaba porque aún sienten la db muy ‘verde’ y para algo tan importante no creían que fuera a funcionar bien. Investigando un poco más, nos dimos cuenta que no hay un ORM para Ruby, que es lo que usamos para la aplicación. Finalmente, como estamos empezando a experimentar en tener nuestra infraestructura replicada en más de una nube, algo exclusivo de Amazon jamás iba a ser la mejor idea. La descartamos.

### CouchDB
CouchDB se me hizo increíble, pero no la mejor solución para nuestro problema. Teníamos que hacer el cambio rápidamente, y  con el querying siendo más complicado que SQL, que el equipo cambiara todo el código aprendiendo todo una nueva forma de hacer queries iba a ser una bronca. Nuestra aplicación cambia constantemente, y hacer queries complicadas de manera rápida es muy importante. Tanto como en algún momento quiero jugar con esta base de datos, no era la decisión correcta para esta vez.

### MongoDB
Con eso llegamos a Mongo. Yo había trabajado con Mongo en proyectos anteriores, pero ningún otro miembro del equipo lo había usado. Es una base de datos basada en documentos, hecha para escalar. Con 40GB de información de facturas para empezar, era sumamente importante que la base pudiera crecer y no alentarse. Hay un ORM para Ruby muy fregón, que hace que la gran mayoría de las queries se hagan casi igual.

La parte más de miedo iban a ser las queries complicadas. Para ciertos reportes financieros que nos piden, nuestras queries en SQL están tan chonchas que terminamos haciendo funciones de Postgres de cientos de líneas. MongoDB tiene una funcionalidad llamada Aggregate que nos resolvió esto en casi casi todas las veces. Para las otras, usamos MapReduce.

## Creando el schema
La parte más grande de la chamba era modelar las facturas. Para que fuera posible consumir los XMLs y pasarlos a JSON, hubo que hacer un parser. Un parser en el que el equipo de desarrolladores se lució y modeló completamente el CFDi. En cuestión de dos semanas, ya había quedado modelada la factura completa, en ambas versiones, con todo lo que eso implica.

Gracias a cómo lo armaron, y pueden joder a este joven si quieren más información al respecto. El modelado de los distintos complementos es mucho más fácil. Ya tenemos varios listos (los que nuestros clientes más usan) y tenemos agenda ir levantando más. Tan fregona quedó la librería de parsing que queremos extraer todo en una gema y hacerla pública. De nuevo, jodan a este joven si quieren que eso pase.

## Cómo lo migramos?
Con todo el código listo para recibir las facturas en la nueva base de datos, el tema se volvió, “cómo fregados hacemos la migración?”. La primera opción era apagar todo, correr una migración gigante y volver a prender. Por el volumen de facturas, esto hubiera tardado varias horas, y habría implicado quedarnos muy noche o venir en fin de semana. No sé ustedes pero yo odio quedarme tarde en la oficina. Me encanta mi trabajo, pero no soy de los que se emociona si son las 11pm y sigue en la oficina. Entonces, quería evitar esa opción a toda costa.

Nuestras facturas se descargan todos los días y a todo momento por un scraper. Este sistema entra al SAT a nombre de nuestros clientes y busca facturas, si ya las tenemos, se las brinca y si no las tenemos las agrega. Usualmente busca sólo las facturas del mes corriente, pero de repente lo ponemos a que busque facturas de periodos más viejos. Esto porque de repente tenemos clientes que cancelan o les cancelan facturas de hace meses y necesitamos que la base esté actualizada. Decidimos colgarnos de este sistema para nuestra migración.

Como sabíamos que iba a haber un tiempo en el que ambas bases de datos tendrían que convivir, decidimos hacer un proceso gradual. Le dijimos al scraper que conforme pasara por las facturas, fuera viendo si existían en ambas bases de datos, y si no, las agregara a la base o bases que hicieran falta. Para probar que tuviéramos la información completa, agregamos un proceso al método de ver una factura, en el que primero revisa si ya existe en Mongo, si sí, le da prioridad a esa, y si no, recae en la de Postgres.

Durante dos semanas corrió nuestro proceso normal, que sólo revisa el mes corriente, y no tuvimos problemas. De poco a poco los clientes empezaron a ver facturas cuya información sale de MongoDB y fuera de algunos campos que nos faltaron en la primera vuelta, nadie se dio cuenta.

De repente, nos dimos cuenta que había un error en el proceso de descarga y que estábamos duplicando (o triplicando) las facturas en Mongo. Yo, bien güey, no agregué un índice a la base de datos para prevenir esto. Como para cuando nos dimos cuenta ya había decenas de miles de facturas duplicadas, ya no se podía agregar el índice. Lo que terminamos haciendo fue un proceso que revisaba cliente por cliente si tenía facturas duplicadas. Gracias a que las queries de mongo corren en chinga, pudimos borrar las facturas duplicadas, de nuevo, sin que nadie se diera cuenta. Una vez limpia la base, agregamos el índice y con eso evitamos que el error siguiera pasando.

Así fue como poco a poco nuestros clientes empezaron a ver información traída desde una base de datos distinta de manera gradual. Después de cerca de un mes de darle rienda suelta al scraper, llegamos a paridad de facturas. Todavía no me animo a borrar la base de datos vieja porque soy un paranoico, pero ya todas las facturas que revisan nuestros clientes las ven desde la base de datos nueva.
