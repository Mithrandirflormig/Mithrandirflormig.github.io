---
layout: single
title: Cálculo de conmutadores en el espacio de espín extendido Parte 1 - Conceptos
date: 2022-04-01
classes: wide
header:
  teaser: assets/images/png/Post_1/arbol.png
categories:
  - Python
tags:
  - Mecánica Cuántica
  - Conmutadores
  - Permutaciones
  - JSON
  - Intermedio/Avanzado
---

Hace algún tiempo tuve la fortuna de ayudar a una gran amiga con algunos cálculos que requería en una parte concreta de su trabajo de tesis. Aunque no sea un tema particularmente afín a todos (y ni hablar de lo complicada que se torna la física), es cierto que los cálculos son metódicos y repetitivos, por lo que sin problemas pueden programarse. La base fundamental de esos cálculos es el [conmutador](http://la-mecanica-cuantica.blogspot.com/2009/08/la-extrana-ecuacion-de-max-born.html), que puede entenderse a grandes rasgos como un tipo de operación que identifica cuando el orden de aplicación de ciertos operadores es irrelevante. Si no se tiene muy claro cuando y como se aplica, no se preocupen, ya que no es propósito de este post desentrañar el concepto matemático o físico que involucra, sino el de aplicar mediante un programa una forma de calcularlos que nos evite el tedioso camino de hacerlo manualmente. Por tanto, en esta ocasión el post estará dividido en dos partes: La parte "conceptual", en donde se explicará la forma de calcularlos y la parte práctica, en donde desarrollaremos el programa. ¡Vamos allá!.

### <span style="color:#b2e74c"> Contenido </span>

<ul>
    <li>
        <a href = "#cont">Un mini contexto...</a>
    </li>
    <li>
        <a href = "#calc">Abordando el cálculo del conmutador</a>
    </li>
</ul>

***

<a id="cont"></a>
## <span style="color:#b2e74c">Un mini contexto...</span>

Antes que cualquier otra cosa me gustaría agradecer a [Rebeca Sanchez R.](https://www.fciencias.unam.mx/directorio/77614) por permitirme hablar un poco de su trabajo, por explicarme a detalle el motivo de su investigación y porque le tengo una enorme respeto, admiración y cariño, ya que se perfila a ser una gran investigadora. También me gustaría agradecer al [Dr. Jaime Bresprosbany P.](https://www.fisica.unam.mx/es/personal.php?id=56&lang=), principal responsable de proponer una extensión del modelo estándar que generaliza el espín. Los siguientes párrafos son con el fin de dar un pequeño contexto al problema, sin darle justicia al enorme trabajo que lleva detrás, por lo que encontrarán diversos enlaces a lo largo del mismo que les permitirán profundizar en cada concepto mencionado.

Desde muy temprana edad en el colegio se nos enseña que existen interacciones fundamentales que rígen el universo:

* [La gravitación](http://www.scielo.org.mx/scielo.php?script=sci_arttext&pid=S1870-35422018000100087)
* [El electromagnetísmo](https://engineering.purdue.edu/wcchew/ece604f19/EMFTAll20191204.pdf)
* [La interacción nuclear debil](https://www.quimica.es/enciclopedia/Interacci%C3%B3n_d%C3%A9bil.html)
* [La interacción nuclear fuerte](https://www.quimica.es/enciclopedia/Interacci%C3%B3n_nuclear_fuerte.html)

Estoy seguro de que habrán escuchado de ellas en alguna parte de su vida, y de hecho es muy probable que hayan estudiado un pequeño subconjunto de las dos primeras. Con la divulgación científica en su mayor aúge, seguramente sabrán que a escalas cosmológicas, es la primera interacción la que describe el movimiento de los astros y que es una teoría descrita extraordinariamente bien por la [relatividad general de Einstein](http://www.damtp.cam.ac.uk/user/tong/gr/gr.pdf). Las últimas tres por otro lado, existen en un apartado cuya teoría lleva por nombre [el módelo estándar](https://www.damtp.cam.ac.uk/user/tong/particle.html), encargada de regír en los procesos sub-atómicos.

Entonces, el _módelo estándar_ se encarga de describir las características de las partículas fundamentales y sus interacciones, siendo una teoría perfectamente consistente, ya que varios de sus aspectos han sido comprobados experimentalmente. Entre los muchos aciertos que la teoría posee, uno en partícular es el de predecir los valores de la masa para los bosones [_W_ y _Z_](http://www.sciepub.com/reference/25123) en términos de parámetros electrodebiles através del [mecanismo de Higgs](https://www.sciencedirect.com/science/article/abs/pii/0031916364911369?via%3Dihub). Pero a la par de ese acierto, un desacierto es la asignación arbitraria de la masas fermiónicas que surgen teóricamente de términos lagrangianos que poco tiene que ver con la naturaleza bosónica. En gran parte del estudio electrodebil (y sobre todo los investigadores involucrados) se considera una posible conexión entre bosones y fermiones, dadas distintas características que sugieren que se puede escribir un boson en términos de fermiones, lo cual daría como resultado un origen en común que permitiría obtener una escala de energía común.

Abordar ese problema no es para nada trivial y sin duda no es algo que podríamos describir en un simple post sin conocer los fundamentos fisicos y matemáticos que permiten realizar esa clase de suposiciones, y por ello, lo que resta decir, es que el trabajo del Dr. Besprosbany muestra este vinculo, además de varias propiedades mas que permiten una descripción mas precisa del problema. Si están interesados en profundizar en el tema, pueden revisar el artículo [Heavy quarks within the electroweak multiplet](https://arxiv.org/abs/1701.01191), advirtiendoles que no es física para aficionados, y que sin conocimientos previos seguramente no será una lectura placentera, sin quitar mérito a lo interesante que puede ser.

<a id="calc"></a>
## <span style="color:#b2e74c">Abordando el cálculo del conmutador</span>

Comencemos estableciendo los operadores con los que trabajaremos a lo largo de este post. Dichos operadores están descritos en términos de los [quarks](http://hyperphysics.phy-astr.gsu.edu/hbase/Particles/quark.html) t(top) y b(bottom), dado que el espacio en el que se trabaja es el de espín extendido. Este espacio posee sus propias reglas y propiedades, aunque muchas de ellas serán conocidas para aquellos que hayan tomado con cierto grado de formalidad un curso de mecánica cuántica y para los que no, no se preocupen, que lejos de tratar de entender la física que involucran, nos concentraremos en la forma en la que operan. Los operadores entonces, son los siguientes: 

- <img src="/assets/images/svg/Post_3/Charge_Operator.svg" alt="Operador de Carga">
- <img src="/assets/images/svg/Post_3/Boson_Operator.svg" alt="Operador Boson W menos segunda componente">

Estos operadores son conocidos como: operador de carga _Q_ <img class = "svg" src="/assets/images/svg/Post_3/Charge_Symbol.svg">, y operador Bosón <img class = "svg" src="/assets/images/svg/Post_3/Boson_Wmenos.svg"> respectivamente. Como dije, están descritos mediante otros operadores que son los quarks, y estos a su vez también poseen ciertas propiedades y atributos. Conviene conocer un poco a que hacen referencia los índices y superíndices que aparecen en los sumandos de cada operador:

* <img class = "svg" src="/assets/images/svg/Post_3/Arrows.svg"> : Valores que puede tomar el espín (arriba o abajo).
* <img class = "svg" src="/assets/images/svg/Post_3/Left_Right.svg"> : Clasificación de estados fuera de la diagonal (Izquierda (L) y derecha (R)).
* <img class = "svg" src="/assets/images/svg/Post_3/Dagger.svg"> : Símbolo daga, que indica que el operador es Hermitiano.

Con ello, tendremos una serie de reglas para conmutar operadores que difieran o compartan ciertos índices y superíndices que abordaremos más adelante. Una última cosa a mencionar, es que un operador hermitiano _Op_ dentro del espacio de espín extendido, caracteriza un estado <img class = "svg" src="/assets/images/svg/Post_1/psi.svg"> con una regla de eigenvalor dada como:

- <img src="/assets/images/svg/Post_3/Eigenvalue.svg" alt="Regla de eigenvalor">

Si lo anterior suena un poco a chino, realmente lo que significa, es que al aplicar el conmutador entre los operadores anteriormente planteados, esperamos obtener el mismo estado con su respectivo eigenvalor asociado a la carga del mismo (es decir, un númerito que aparecerá a lado del operador). Esto será una garantía de que los cálculos fueron efectuados correctamente y no solo para la teoría, sino también para el programa.

Vamos entonces a realizar el cálculo introduciendo a los operadores dentro del conmutador de la siguiente forma:

<div class="pngdiv"><img src="/assets/images/png/Post_3/Conmutador_Operadores.png" width = 650 title = "Conmutador de dos operadores" alt = "Conmutador de Q y W"/></div>

donde expandiendo el término izquierdo podemos reescribir la expresión como sigue:

<div class="pngdiv"><img src="/assets/images/png/Post_3/Conmutador_2.png" width = 600 title = "Conmutador de dos operadores" alt = "Conmutador de Q y W"/></div>

En general, el cálculo de conmutadores no es directo, por lo que suelen utilizarse múltiples propiedades que reduzcan la expresión a algo más sencillo de evaluar. Aunque existen múltiples propiedades que obedecen los conmutadores, podemos utilizar la siguiente:

<div class="pngdiv"><img src="/assets/images/png/Post_3/Regla_conmutador.png" width = 500 title = "Regla de conmutación" alt = "Regla de conmutación"/></div>

Esta propiedad nos permitirá abrir la suma en distintos conmutadores (en lugar de tener la suma dentro de un solo conmutador), de forma que podremos eventualmente evaluar cada sumando de forma independiente (o es la idea). Entonces, aplicando la propiedad anterior tenemos que:

<div class="pngdiv"><img src="/assets/images/svg/Post_3/Conmutator_separate.svg" width = 750 title = "Conmutador de dos operadores" alt = "Conmutador de Q y W"/></div>

Ahora tenemos ocho sumandos, y en cada uno de ellos tenemos involucrados cuatro operadores (los t's y b's).
Para cada uno de estos sumandos (que son conmutadores) deberemos aplicar otra identidad que involucra otro tipo de operación conocida como el [anticonmutador](https://www.youtube.com/watch?v=_QB6uGFQp4g), y que se expresa de la siguiente forma:

<div class="pngdiv"><img src="/assets/images/png/Post_3/Anticonmutador.png" width = 600 title = "Indentidad anticonmutador" alt = "Identidad de anticonmutador"/></div>

El anticonmutador también posee diversas propiedades, pero la que nos interesa y que merece la pena conocer de ahorita es la siguiente:

<div class="pngdiv"><img src="/assets/images/svg/Post_3/Delta_anticonmutador.svg" width = 650 title = "Conmutador de dos operadores" alt = "Conmutador de Q y W"/></div>

Esa representación es una forma corta de describir el resultado de distintos escenarios para los operadores involucrados, puesto que aplicar el anticonmutador para dos operadores da como resultado un producto de [deltas de kronecker](https://es.wikipedia.org/wiki/Delta_de_Kronecker), que solo pueden tener como valor cero o uno.
Si no se está muy familiarizado con este tipo de expresiones, no hay que preocuparnos, ya que esto podemos interpretarlo de la siguiente forma:

_El Anticonmutador de dos operadores valdrá 1 **únicamente** en el caso en el que uno de los operadores sea hermitiano (que contenga el símbolo daga) y el otro no, y al mismo tiempo los subíndices sean los mismos, es decir, ambos operadores L o ambos R, ambos con espín arriba o espín abajo. En cualquier otro caso, y cualquier otra posible combinación que se nos ocurra será 0._

Esto nos permite reducir algunos cálculos cuando ya se tiene cierta experiencia desarrollando este tipo de expresiones, pero tengan en cuenta que introducir esa identidad para los 8 sumandos que tenemos en la expresión expandida del conmutador, dará como resultado una nueva expresión que contendrá 32 sumandos. Esto, como ven, puede resultar tedioso de escribir y calcular, a la par de errores de escritura y de interpretación. Pero como la idea es aplicar lo mismo para cada uno de los sumandos del conmutador, mostraré como aplicar esa identidad únicamente para el primer sumando, ya que para los demás será exactamente el mismo camino (y convenientemente es un buen ejercicio para comprobar el resultado que obtendremos).

Aplicando entonces la propiedad al primer sumando de la expresión [<img class = "svg" src="/assets/images/svg/Post_3/Charge_Symbol.svg">,<img class = "svg" src="/assets/images/svg/Post_3/Boson_Wmenos.svg">] tenemos que:

<div class="pngdiv"><img src="/assets/images/svg/Post_3/Conmutador_identidad.svg" width = 800 title = "Conmutador de dos operadores" alt = "Conmutador de Q y W"/></div>

donde se tomaron a los operadores en el orden en el que aparecen en la identidad. Ahora, lo único que nos interesa de esos sumandos son los valores que tomarán los anticonmutadores según la regla mencionada anteriormente, ya que varios de ellos se anularan.

- <img class = "svg" src="/assets/images/svg/Post_3/Primer_sumando.svg"> : Notamos que ambos son operadores t, que comparten los mismos índices; ambos con espín arriba y de tipo L. El problema es que ambos son operadores no hermitianos (ninguno tiene el símbolo de daga) y habíamos dicho que para que valgan 1, uno de ellos debe ser hermitiano (debe contener la daga). Por tanto, el resultado de este anticonmutador es **0**.
- <img class = "svg" src="/assets/images/svg/Post_3/Segundo_sumando.svg"> : Tenemos un operador b y un t. El primer operador tiene daga y el otro no, además de ser ambos de tipo L. El detalle es que el espín es distintos en ambos, por tanto, su valor es **0**.
- <img class = "svg" src="/assets/images/svg/Post_3/Tercer_sumando.svg"> : En este caso tenemos ambos operadores de tipo t. Ambos tienen los mismos subíndices, es decir, son de tipo L y espín arriba. Por otro lado, uno está dageado y el otro no, por lo que cumplen con los requisitos del enunciado anterior, así que el resultado de ese anticonmutador es **1**. Además, notemos que lo acompaña un coeficiente <img class = "svg" src="/assets/images/svg/Post_3/fraccion.svg">, por tanto, el resultado general es justamente eso, <img class = "svg" src="/assets/images/svg/Post_3/fraccion.svg">.
- <img class = "svg" src="/assets/images/svg/Post_3/Cuarto_sumando.svg"> : Tenemos un operador de tipo b y un t. Notamos que ambos son operadores dageados por lo que ya directamente sabemos que su valor es **0**.

Como pequeño resumen, los anticonmutadores para cada sumando son:

<div class="pngdiv"><img src="/assets/images/svg/Post_3/resumen_anticonmutador.svg" width = 180 title = "Conmutador de dos operadores" alt = "Conmutador de Q y W"/></div>

Finalmente, el primer sumando podemos reescribirlo como:

<div class="pngdiv"><img src="/assets/images/svg/Post_3/Resultado_primersumando.svg" width = 300 title = "Conmutador de dos operadores" alt = "Conmutador de Q y W"/></div>

El mismo proceso hay que realizar con los siete sumandos restantes aplicando la identidad y verificando el valor que toma el anticonmutador. Para ahorrar un poco de trabajo, únicamente pondré aquellos sumandos que arrojan un valor distinto de cero.

* El cuarto sumando

<div class="pngdiv"><img src="/assets/images/svg/Post_3/Resultado_cuartosumando.svg" width = 300 title = "Conmutador de dos operadores" alt = "Conmutador de Q y W"/></div>

* El sexto sumando

<div class="pngdiv"><img src="/assets/images/svg/Post_3/Resultado_sextosumando.svg" width = 300 title = "Conmutador de dos operadores" alt = "Conmutador de Q y W"/></div>

* Y septimo sumando

<div class="pngdiv"><img src="/assets/images/svg/Post_3/Resultado_septimosumando.svg" width = 300 title = "Conmutador de dos operadores" alt = "Conmutador de Q y W"/></div>

Como ven, únicamente sobrevivieron 4 términos de los 32 que tenemos al introducir la identidad de los anticonmutadores. Por tanto, podemos finalmente reescribir el conmutador original de la siguiente forma:

<div class="pngdiv"><img src="/assets/images/svg/Post_3/Resultado_conmutador.svg" width = 500 title = "Conmutador de dos operadores" alt = "Conmutador de Q y W"/></div>

¡Obtenemos el mismo operador con un coeficiente -1!. Esto significa que el cálculo fue realizado correctamente y por supuesto, se satisface la regla de eigenvalores que mencionamos previamente.