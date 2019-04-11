---
layout: post
title: Por qué sigo usando Ruby?
---

Qué te hizo aprender a programar? A mí siempre me gustaron las computadoras, y en algún punto descubrí que aprender a programar me iba a dejar hacer aún más de lo que ya podía. Lo que me hizo aprender a programar fue encontrarle una utilidad. Cuando identifiqué un problema que sólo se podía resolver a través de esa habilidad, fue cuando me di a la tarea de aprender.

Siempre he visto la programación como algo práctico. Una herramienta dentro de mi arsenal que me permite hacer muchas cosas. A diferencia de algunos programadores, yo nunca he podido decir que me *encanta* programar*.* Amo los resultados. Me encanta que sé explicarle a una computadora cómo hacer algo y así ya no lo tengo que hacer yo. Cabe resaltar que soy un huevón, entonces entre más puedo automatizar, menos tengo que hacer yo y la vida es más bonita.

Después de haber agarrado, para cosas súper básicas, lenguajes como BASIC, C y hasta, *gulp*, un poco de FORTRAN, debo confesar que el primer lenguaje que agarré bien bien fue PHP. Por si eso no fuera suficientemente penoso, aprendí PHP para poder hacer cosas de WordPress. Yo lo sé, es un pasado del que no me enorgullezco, pero ahí está. PHP era un leguaje fácil de agarrar como principiante; su documentación era y sigue siendo increíble. Abrí mi primer negocio haciendo PHP y lo usé hasta que [mi socio][1] un día agarró y decidió que teníamos que usar Ruby, que porqué "estaba más chido". Me caga decirlo, pero tenía la boca atascada de razón.

Aprender Ruby después de usar otro lenguaje menos amigable es increíble. Es como la primera vez que le enseñas macOS a alguien que toda su vida sólo ha usado Windows. Son muchos momentos de "ah, no mames, es así de fácil?" No me queda duda que Ruby está diseñado para mejorar la vida del programador.

Ruby está construido para seguir [una filosofía][2] que muchos de nosotros deberíamos seguir también. Es muy simple, pero tiene mucha complejidad adentro para lograr esa simplicidad. A nosotros como usuarios nos da una interfaz súper limpia para poder hacer cosas tan complicadas como queramos. Deberíamos preocuparnos más por hacer lo mismo con nuestros usuarios, diseñar interfaces súper limpias pero aún dejando hacer cosas muy complicadas. Es bien difícil lograr eso.

# Qué me gusta de Ruby?

## Es fácil de entender

Es ultra legible. Básicamente, si sabes leer inglés, y el programa está bien escrito (algo clave), sabes leer Ruby. Las primeras semanas que usé Ruby, me encontré más de una vez diciendo "me pregunto cómo se llamará en Ruby algo que equivalente a x ó y en PHP?" y la primer cosa que se me ocurría, era tal cual como se llamaba. Quieres hacer algo 5 veces? Ah, pos usa `5.times`. Quieres el primer elemento de un array? ah, pues usa `.first`.

Esto se vuelve increíblemente útil cuando le quieres explicar un concepto de programación a alguien que no sabe programar. La mayoría de la gente no técnica, ve esto de la programada como algo mágico. Me toca seguido explicarle a la banda que la computadora no piensa, sólo hace tal cual lo que nosotros le decimos que haga. Para tratar de matar esta idea de la magia, no hay nada como enseñar código.

Me encanta esta idea de que [si no sabes explicarle algo a un niño de 6 años significa que realmente no lo comprendes][3]. Para mí, esa idea traducida al código implica que **si un programador junior no puede entender tu código con sólo leerlo, probablemente puedes mejorar tu código**. Recordemos que los lenguajes de programación no tienen el objetivo de que la máquina entienda mejor tu programa, sino que el siguiente programador que lo vea (que puedes ser tú en unos meses) lo entienda. De otra manera, mejor todos escribamos en algún lenguaje súper low-level y a la fregada, no?  

Una manera fácil de identificar a un programador junior es cuando ves código escrito en una línea que debió haber sido escrito en 10 para que fuera legible.  No hay pedo si tu función tiene más líneas si eso realmente lo hace más legible. La marca de un desarrollador fregón es cuando sabe encontrar el punto medio entre escribir algo súper corto pero difícil de leer y algo súper largo que nomás desperdicia espacio. Qué tanto del código que escribes todos los días lo podría entender cualquier programador?  Qué tal alguien que sabe programar pero no conoce el lenguaje que tú usas? Si no te dieron miedo esas preguntas, felicidades! Suenas como alguien que me gustaría contratar.

Ahora, qué pasa si incluyes a la gente que no sabe programar en esa frase? Te sigues sintiendo con la misma confianza? En eso siento que muchos lenguajes ponen la barrera de entrada muy difícil, y primero tienes que entender conceptos complicados y sintaxis horrible antes de poder leer un programa. En Ruby, eso no me da miedo. Es una de las razones por las que lo considero una herramienta súper poderosa.

## La comunidad es increíble

Pero un lenguaje no es sólo su sintaxis, también es su comunidad. Ruby tiene una de las mejores comunidades de programación. Creo que a todos nos ha pasado el que de repente te trabas con algo y nomás no ves para dónde hacerle. Le rascas y le rascas y nada. Empiezas a cuestionar tus habilidades. Llegas al punto en el que no sabes por qué alguien te paga por hacer estas mamadas. Google no ayuda. StackOverflow no ayuda. Se te ocurre escribirle al güey que escribió la librería, o el framework, y te contesta! No sólo eso, te contesta de buena manera y te ayuda a darte cuenta de dónde está tu error pendejo.

La comunidad de Ruby tiene este acrónimo, [MINASWAN][4]. Salió a raíz de que el creador de Ruby, Yukihiro Matsumoto (mejor conocido como Matz), es un güey re buen pedo. Todos deberíamos ser tan buen pedo como Matz. En la comunidad, este asunto se lo toman muy en serio. Es algo que muchas otras comunidades no tienen. Cometiste un error menso y pediste ayuda? "Ah pos que n00b!" "No eres un programador real!" "Por qué no lo haces en node?" Huevos. Si sólo se llevan una cosa de esto, por favor que sea que hay que ser pacientes, tolerantes y buen pedo con los demás. Llévense la buenavibrez de la comunidad de Ruby y contágienla a las demás comunidades en las que participan.

# Qué no está tan chido en Ruby?

## Es lento

La queja principal de la *comunidá* es que es lento. Sí, si lo comparas con otros lenguajes, es re lento. Pero qué significa eso? Qué tanto te va a afectar? Si tu aplicación llega a un tamaño en el que Ruby no es una buena opción, qué envidia me das.

GitHub, Twitter, Shopify y Airbnb son sólo algunos ejemplos de empresas que empezaron siendo simples aplicaciones de Rails. Es más, de esas, GitHub y Shopify siguen siendo aplicaciones (gigantes) de Rails. Airbnb todavía tiene mucho código de producción en Ruby. Gracias a la simplicidad de Ruby (y lo fregón que es Rails) la primer versión de Twitter se hizo en un fin de semana. Así que a menos de que tu aplicación o negocio sea de una escala que compita o supere a esas, para mí no es una excusa válida el que Ruby sea "lento".

## "Ya pasó de moda"

Esa es otra de las cosas negativas que escucho recurrentemente. Yo lo siento como un pro más que un contra. Me dice que los problemas grandes del lenguaje ya fueron resueltos. Chingos de veces. Está cañón que encuentres un problema nuevo en Ruby. Ya casi todo tiene una gema, o un artículo en Medium, o una respuesta en StackOverflow pa que sepas cómo hacerle. Los rubyistas seguimos siendo una comunidad fuerte e influyente. Tanto así que ya hay mucha banda que se fue de Ruby y empezó a meterle mano a otros lenguajes y les mejoraron cosas. JavaScript ya tiene un chingo de cosas que sacaron de Ruby. Elixir es Erlang disfrazado de Ruby. Esto está de huevos, quiere decir que cuando la gente me manda sus coding challenges en Elixir los puedo revisar! Esto también quiere decir que si aprendiste un lenguaje y quieres aprender el otro, te va a costar menos trabajo! El que Ruby ya sea un lenguaje maduro sólo quiere decir que te puedes sentir en completa confianza de correrlo en producción. Dejen de fregar con que ya pasó de moda.

# Deberías hacer todo en Ruby?

*Nel*. Ruby no es el *one true language* ni la respuesta a todos tus problmeas. Nada lo es. A mí me puede encantar, pero esa no es la idea que te vengo a vender. Hay cosas para las cuales no usaría, o de plano no se puede usar Ruby. Vas a procesar un chingo de archivos? Chance bash es la respuesta. Necesitas algo multi-threaded y a prueba de fallas? Igual investiga Go ó Elixir. Trabajas en front-end? Apuesto a que vas a usar JavaScript.  

Como recomendación general, no aprendas sólo un lenguaje. Puedes hacer muchas cosas en Ruby, pero no deberías de quedarte ahí. Siempre es bueno ver y aprender otras cosas. Es peligroso que tu única herramienta sea un martillo, porque entonces a todo le ves cara de clavo. Cada lenguaje, herramienta y comunidad tiene ideas diferentes. Es súper importante por lo menos estar al tanto de qué hacen y cómo hacen las cosas en otros lados, así uno hace las cosas mejor.

# Ya pa' acabar

Me encanta este lenguaje. Llevo usándolo casi 10 años. Hoy ya casi no programo profesionalmente. Cuando sí tengo que programar, usualmente lo hago en Ruby. Por qué? Porque se lo puedo enseñar a gente que no sabe programar y lo puedo explicar sin mayor problema. Porque si en algo me trabo, puedo encontrar la respuesta en friega. Porque aún si me encuentro con un problema nuevo, la comunidad es súper buen pedo y me ayudan. Porque aunque conozco más lenguajes, la mayoría de las veces es la manera más rápida que tengo de sacar algo de mi cabeza y ponerla en algo ejecutable. Finalmente, porque lo usamos en [Enconta][5].

[1]: https://twitter.com/unRob
[2]: https://www.ruby-lang.org/en/about/
[3]: https://www.goodreads.com/quotes/19421-if-you-can-t-explain-it-to-a-six-year-old
[4]: https://en.wiktionary.org/wiki/MINASWAN
[5]: https://enconta.com
