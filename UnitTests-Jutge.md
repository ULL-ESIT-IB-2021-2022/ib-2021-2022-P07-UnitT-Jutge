# Práctica 7. Introducción a los tests unitarios. La plataforma Jutge.

# Factor de ponderación: 6

### Objetivos
Los objetivos de esta práctica son que el alumnado:
* Desarrolle con mayor fluidez programas sencillos en C++.
* Profundice en el uso de funciones en sus programas.
* Conozca los conceptos básicos del desarrollo de pruebas unitarias de código y escriba a mano pruebas unitarias para sus programas.
* Comience a utilizar la plataforma Jutge para autoevaluar la corrección de sus programas.

### Rúbrica de evaluacion de esta práctica
En esta práctica y las siguientes ya no será admisible la presentación de un programa que, al margen de su funcionamiento,
pudiera tener deficiencias en cuanto a reglas de estilo y formato. 
Ante tal situación la práctica se calificará como suspendida.
Todo el código que se presente a evaluación ha de cumplir los estándares definidos en la 
[Guía de Estilo de Google para C++](https://google.github.io/styleguide/cppguide.html).

Se señalan a continuación otros aspectos (la lista no es exhaustiva) que se tendrán en cuenta a la hora de evaluar esta práctica.
El alumnado ha de acreditar que:

* Conoce los conceptos expuestos en el material de referencia de esta práctica.
* Ha realizado todos los ejercicios propuestos, así como que es capaz de desarrollar otros de complejidad similar.
* Sus programas se compilan correctamente utilizando la utilidad `make` y un fichero `Makefile`.
* Todos los identificadores que utilice en su programa (constantes, variables, etc.) deberán ser
  siempre significativos. No utilice nunca identificadores de una única letra, tal vez con la excepción de las
  variables que utilice para iterar en un bucle.
* Dispone de una cuenta en la plataforma [Jutge](https://jutge.org/) y es capaz de auto-evaluar un programa en esa plataforma.

### Pruebas Unitarias
Las pruebas unitarias (unit tests en inglés), son pruebas que se utilizan para comprobar el correcto funcionamiento de
componentes individuales de un programa.
Se llaman "unidades de código" a aquellas partes de un programa cuyo funcionamiento se comprueba mediante tests 
y habitualmente son clases, funciones o grupos ellas, e incluso todo un programa.

Las pruebas consisten en suministrar al código un conjunto de entradas y determinar si  el conjunto de salida es el esperado. 
Es decir, comprobar si los valores devueltos son correctos o no, y gestionar los fallos, en caso de que la salida no sea la esperada.
El propósito de este tipo de pruebas, es el garantizar que cada componente funcione aisladamente y que todo funciona como se espera que funcione.

Por lo general, la propia programadora que escribe el código es quien tiene que escribir 
los test unitarios para probar su código, aunque lo deseable sería que el código y los tests los escriban
equipos diferentes, puesto que quien escribe el código suele ser menos exigente a la hora de escribir
los tests.
Por otra parte conviene siempre escribir las pruebas **antes** de escribir el código que se va a probar.

A la hora de escribir tests conviene centrar la atención en aquellas entradas del programa (o unidad de código)
que son más proclives a producir errores.
Supongamos por ejemplo que se está desarrollando una función (unidad de código) que calcula la suma de dos números enteros.
Tests unitarios que validen la corrección de esa función podrían: 
* Comprobar que lo que reciba la función sean realmente dos parámetros
* Que esos dos parámetros sean números
* Que lo que devuelva la función sea otro número
* Que ese número corresponda realmente con la suma
* Que la suma se calcule correctamente para cualquier combinación de números con valores negativos, positivos o con valor cero.
Todas estas podrían ser posibles pruebas unitarias que se realicen sobre la función.
Las pruebas unitarias  se suelen realizar utilizando entornos de pruebas especializados que estudiaremos en el futuro
pero por ahora el propósito en la asignatura es que antes de escribir un programa se escriban a mano un conjunto de pruebas
que sirvan para, una vez finalizado el programa, acreditar la corrección del mismo al menos para un cierto número de situaciones.
La regla a seguir de ahora en adelante es **Convierta en un hábito la escritura de tests para sus programas**.

### La plataforma Jutge
[Jutge](https://jutge.org/) es una plataforma que ha sido desarrollada en la
[UPC](https://www.upc.edu/en) para uso docente en asignaturas de programación.
La plataforma ofrece una gran cantidad de problemas que los estudiantes han
de resolver y el Jutge (juez en catalán) asigna un 
[veredicto](https://jutge.org/documentation/verdicts) 
a cada solución que se suba a la plataforma.

Jutge solo evalúa los programas desde el punto de vista de la corrección del resultado que ofrecen, 
no evalúa la calidad del código en cuanto a otros aspectos: diseño, estilo, formato, etc.
Para determinar si un programa es correcto o no, Jutge aplica varios tests al programa (tests unitarios)
que tratan de acreditar la bondad de la solución, que podría ser parcialmente correcta.
Algunos de esos tests son públicos y la programadora debiera encargarse de asegurar que su programa pasa
esos tests públicos (ofrece los resultados esperados) antes de enviar el programa al juez.

[Estas transparencias](https://docs.google.com/presentation/d/14UvZPw4OJvogp6afLeouOAODcBNo5JhgePBQfkiAkic/edit?usp=sharing)
contienen información algo más detallada sobre el uso de la plataforma Jutge. 
Estúdielas antes de comenzar a trabajar con la misma.

Una vez que tenga su cuenta en Jutge, realice cuantos ejercicios sea capaz de programar y súbalos para su evaluación
por el juez, hasta obtener un veredicto de AC (Accepted).
Cuantos más problemas resuelva, más incrementará sus capacidades como programadora.

### Ejercicios
1. 

### Referencias
* [Desarrollo dirigido por Tests](https://es.wikipedia.org/wiki/Desarrollo_guiado_por_pruebas)
* [Google Test](https://en.wikipedia.org/wiki/Google_Test)
* [Cómo usar Google Test para C++ en VSC](https://docs.microsoft.com/es-es/visualstudio/test/how-to-use-google-test-for-cpp?view=vs-2019), 
* [Google Tests build instructions](https://github.com/google/googletest/blob/master/googletest/README.md#standalone-cmake-project)
* [Googletest Primer](https://github.com/google/googletest/blob/master/googletest/docs/primer.md)
* [Mejorar la calidad del código mediante la prueba unitaria](https://www.mql5.com/es/articles/1579).
* [Google Test + gcover. Una lista de recetas](https://usingstdcpp.files.wordpress.com/2016/11/gtest.pdf)
* [Exercism](https://exercism.io/)
* [Exercism en genbeta](https://www.genbeta.com/desarrollo/exercism-fitness-para-nuestras-habilidades-programadoras)
* [¿Qué es Ubuntu `snap`?](https://blogubuntu.com/que-es-ubuntu-snap) 
* [snap quickstart guide](https://snapcraft.io/docs/getting-started)
* [Números complejos](https://es.wikipedia.org/wiki/N%C3%BAmero_complejo)
*	[Class code and header files](https://www.learncpp.com/cpp-tutorial/89-class-code-and-header-files/)
* [Header guards](https://www.learncpp.com/cpp-tutorial/header-guards/)
* [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)
