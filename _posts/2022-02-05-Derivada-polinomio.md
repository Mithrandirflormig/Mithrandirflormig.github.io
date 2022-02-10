---
layout: single
title: Calculando la derivada de un Polinomio de grado n
date: 2022-02-25
classes: wide
header:
  teaser: /assets/images/slae32.png
categories:
  - Python
tags:
  - Derivada
  - Polinomio
---

Hoy día existen diversos programas que nos permiten realizar calculos matemáticos de todo tipo, desde una sencilla suma hasta una integral complicada. [Wolfram alpha](https://www.wolframalpha.com/), es sin duda uno de los softwares mas poderosos actualmente con los que podemos realizar este tipo de calculos, usando procesamiento de lenguaje natural. Sin embargo, como un buen ejercicio de programación podemos realizar una implementación que derive un polinomio de grado n (determinado por el usuario) en bruto, es decir, sin la ayuda de módulos extra que realicen el calculo por nosotros. ¡Vamos allá!.

### <span style="color:#b2e74c">  Contenido </span>

- [Descomposición de expresión en elementos](#desc)
- [Separación de coeficientes y exponentes](#sep)
- [Producto de coeficientes y exponentes](#pro)
- [Construcción de la derivada](#cons)
- [Extra: Pruebas Unitarias](#prue)

***

<a id="desc"></a>
## <span style="color:#b2e74c"> Descomposición de expresión en elementos </span>

Derivar un polinomio no es particularmente complicado, por lo que esa explicación no la abordaré con demasiados detalles y me concetraré en la implementación. No obstante si por lo que sea necesitas recordar como se implementa, puedes revisar el siguiente [enlace](https://www.universoformulas.com/matematicas/analisis/derivada-polinomio/) y posteriormente regresar para entender completamente el proceso que llevaremos a cabo a continuación.