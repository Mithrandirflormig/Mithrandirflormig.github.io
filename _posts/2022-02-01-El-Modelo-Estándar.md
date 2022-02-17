---
layout: single
title: Un cálculo de conmutadores para el módelo estándar con espín extendido Parte 1
date: 2022-02-20
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

Hace algún tiempo tuve la fortuna de ayudar a una gran amiga con algunos cálculos que requería en una parte concreta de su trabajo de tésis. Aunque no sea un tema particularmente afín a todos (y ni hablar de lo complicada que se torna la física), es cierto que los cálculos son metódicos y repetitivos, por lo que sin problemas pueden programarse. La base fundamental de esos calculos es el [conmutador](), que puede entenderse a grandes rasgos como un tipo de operación que identifica cuando el orden de aplicación de ciertos operadores es irrelevante. Si no se tiene muy claro cuando y como se aplica, no se preocupen, ya que no es propósito de este post desentrañar el concepto matemático o físico que involucra, sino el de aplicar mediante un programa una forma de calcularlos que nos evite el tedioso camino de hacerlo manualmente. Por tanto, en esta ocasión el post estará dividido en dos partes: La parte "conceptual", en donde se explicará la forma de calcularlos y la parte práctica, en donde desarrollaremos el programa. ¡Vamos allá!.

### <span style="color:#b2e74c"> Contenido </span>

<ul>
    <li>
        <a href = "#cont">Un mini contexto...</a>
    </li>
    <li>
        <a href = "#prob">Planteando el problema</a>
    </li>
</ul>

***

<a id="cont"></a>
## <span style="color:#b2e74c">Un mini contexto...</span>

Antes que cualquier otra cosa me gustaría agradecer a [Rebeca Sanchez R.](https://www.fciencias.unam.mx/directorio/77614) por permitirme hablar un poco de su trabajo, por explicarme a detalle el motivo de su investigación y por la cuál tengo una enorme respeto, admiración y cariño ya que se perfila a ser una gran investigadora. También me gustaría agradecer al [Dr. Jaime Bresprosbany P.](https://www.fisica.unam.mx/es/personal.php?id=56&lang=), principal responsable de proponer una extensión del módelo estándar que generaliza el espín. Los siguientes parrafos son con el fin de dar un pequeño contexto al problema, sin darle justicia al enorme trabajo que lleva detrás, por lo que encontrarán diversos enlaces a lo largo del texto que les permitirán profundizar mas en cada concepto mencionado.

Desde muy temprana edad en el colegio se nos enseña que existen interacciones fundamentales que rígen el universo:

* [La gravitación]()
* [El electromagnetísmo]()
* [La interacción nuclear debil]()
* [La interacción nuclear fuerte]()

Estoy seguro de que habrán escuchado de ellas en alguna parte de su vida, y de hecho es muy probable que hayan estudiado un pequeño subconjunto de las dos primeras. Con la divulgación científica en su mayor aúge, seguramente sabrán que a escalas cosmológicas, es la primera interacción la que describe el movimiento de los astros y que es una teoría descrita extraordinariamente bien por la [relatividad general de Einstein](). Las últimas tres por otro lado, existen en un apartado cuya teoría lleva por nombre [el módelo estándar](), encargada de regír en los procesos sub-atómicos.

Entonces, el _módelo estándar_ se encarga de describir las características de las partículas fundamentales y sus interacciones, siendo una teoría perfectamente consistente, ya que varios de sus aspectos han sido comprobados experimentalmente. Entre los muchos aciertos que la teoría posee, uno en partícular es el de predecir los valores de la masa para los bosones [_W_ y _Z_](http://www.sciepub.com/reference/25123) en términos de parámetros electrodebiles através del [mecanismo de Higgs](https://www.sciencedirect.com/science/article/abs/pii/0031916364911369?via%3Dihub). Pero a la par de ese acierto, un desacierto es la asignación arbitraria de la masas fermiónicas que surgen teóricamente de términos lagrangianos que poco tiene que ver con la naturaleza bosónica. Gran parte del estudio electrodebil (y sobre todo los investigadores involucrados) consideran una posible conexión entre bosones y fermiones, dadas distintas características que sugieren que se puede escribir un boson en términos de fermiones, lo cual daría como resultado un origen en común que permitiría obtener una escala de energía común.

Abordar ese problema no para nada trivial y sin duda no es algo que podríamos describir en un simple post sin conocer los fundamentos fisicos y matemáticos que permiten realizar esa clase de suposiciones. Lo que resta decir respecto a ello, es que el trabajo del Dr. Besprosbany muestra este vinculo, además de varias propiedades mas que permiten una descripción mas precisa del problema. Si están interesados en profundizar mucho mas en el tema, pueden revisar el artículo [Heavy quarks within the electroweak multiplet](https://arxiv.org/abs/1701.01191), advirtiendoles que no es física para aficionados, y que sin conocimientos previos seguramente no será una lectura placentera, sin quitar mérito a lo interesante que puede ser.

<a id="cont"></a>
## <span style="color:#b2e74c">Planteando el problema</span>
