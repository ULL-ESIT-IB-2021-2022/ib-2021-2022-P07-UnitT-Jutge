# Práctica 7. Introducción a los tests unitarios. La plataforma Jutge.

# Factor de ponderación: 6

### Objetivos
Los objetivos de esta práctica son que el alumnado:
* Desarrolle con mayor fluidez programas sencillos en C++.
* Profundice en el uso de funciones en sus programas.
* Conozca los fundamentos del desarrollo de tests unitarios.
* Comience a utilizar la plataforma Jutge para autoevaluar la corrección de sus programas.

### Rúbrica de evaluacion de esta práctica
Se señalan a continuación los aspectos más relevantes (la lista no es exhaustiva)
que se tendrán en cuenta a la hora de evaluar esta práctica.
El alumnado ha de acreditar que:

* Conoce los conceptos expuestos en el material de referencia de esta práctica.
* Ha realizado todos los ejercicios propuestos, así como que es capaz de desarrollar otros de complejidad similar.
* Sus programas se compilan correctamente utilizando la utilidad `make` y un fichero `Makefile`.
* Todo el código que haya escrito cumple los estándares definidos en la 
  [Guía de Estilo de Google para C++](https://google.github.io/styleguide/cppguide.html).
* Todos los identificadores que utilice en su programa (constantes, variables, etc.) deberán ser
  siempre significativos. No utilice nunca identificadores de una única letra, tal vez con la excepción de las
  variables que utilice para iterar en un bucle.
* Dispone de una cuenta en la plataforma [Jutge](https://jutge.org/) y es capaz de auto-evaluar un programa en esa plataforma.


### La plataforma de testing de Google
Tal como recoge la
[Wikipedia](https://es.wikipedia.org/wiki/Desarrollo_guiado_por_pruebas),
El desarrollo dirigido por tests (TDD, *Test Driven Development* por sus siglas en inglés) es una práctica de 
ingeniería de software que involucra otras dos técnicas: 
escribir las pruebas primero (Test First Development) y 
[Refactorización](https://es.wikipedia.org/wiki/Refactorizaci%C3%B3n)
(Refactoring) o reestructuración del código.
Para escribir las pruebas generalmente se utilizan las pruebas unitarias (unit test en inglés). 

El TDD se basa en la repetición de un ciclo de desarrollo muy corto que
involucra la repetición de tres pasos:
1. En primer lugar el desarrollador escribe un caso de prueba (test) que falla (a propósito) y que define una mejora deseada (habitualmente una nueva función o método)
2. A continuación se desarrolla el código (de la función) que hace que la prueba pase satisfactoriamente 
3. Finalmente refactoriza el nuevo código hasta obtener un resultado satisfactorio

Esta imagen representa este ciclo repetitivo característico del TDD.

![TDD cycle](https://raw.githubusercontent.com/ULL-ESIT-IB-2020-2021/IB-P12-Classes-GTests-Exercism/master/red-green-refactor.png "Red-Green-Refactor")

El propósito del desarrollo guiado por pruebas es lograr un código limpio que funcione correctamente.
La idea es que los requisitos sean traducidos a pruebas (tests), y de este modo, cuando las pruebas pasen 
se garantizará que el software cumple con los requisitos que se han establecido.


Las "unidades" de código para las que se realizan tests habitualmente son clases, funciones o grupos ellas. 
Supongamos por ejemplo que se está implementando una función (unidad de código) que calcula la suma de dos números enteros.
Una prueba (test unitario) es un código que valida la corrección de esa función: se podría comprobar que lo
que reciba la función sean realmente dos parámetros, y que esos dos parámetros sean números, y que lo que
devuelva la función sea otro número, y que ese número corresponda realmente con la suma. 
Todas estas podrían ser posibles pruebas unitarias que se realicen sobre la función.
Las pruebas unitarias  se suelen realizar utilizando entornos de pruebas (testing) especializados.

Existen diversas plataformas para el desarrollo de tests unitarios en C++.
Algunas de las de uso más extendido son
[Boost.Test](https://www.boost.org/doc/libs/1_49_0/libs/test/doc/html/index.html),
[CppUnit](https://sourceforge.net/projects/cppunit/),
[Cute](https://cute-test.com/)
aunque hay
[muchas otras](https://en.wikipedia.org/wiki/List_of_unit_testing_frameworks#C++)

En esta práctica se propone utilizar el framework 
[Google Test](https://en.wikipedia.org/wiki/Google_Test),
(también conocido como gtest) que es una librería de pruebas unitarias (*unit tests*) para C++.
El entorno permite que los tests se ejecuten de una en uno o todos a la vez. 
Google Tests puede ser utilizado en 
[Visual Studio Code](https://docs.microsoft.com/es-es/visualstudio/test/how-to-use-google-test-for-cpp?view=vs-2019), 
aunque en este documento se propone un uso de la plataforma de modo independiente de VSC.

El primer paso para usar gtest es su instalación. 
Siga para ello los siguientes pasos:

```
$ git clone https://github.com/google/googletest.git -b release-1.10.0
$ cd googletest/
$ mkdir build
$ cd build/
$ cmake .. -DBUILD_GMOCK=OFF
$ make
$ sudo make install
```
que se explican en el documento 
[Standalone CMake Project](https://github.com/google/googletest/blob/master/googletest/README.md#standalone-cmake-project).
El comando `sudo make install` (obsérvese que se ejecuta con privilegios de *root*) 
instalará gtest en el directorio `/usr/local/` del sistema , de modo que en los directorios
```
/usr/local/include
/usr/local/lib
```
se alojan los ficheros de cabecera (`*.h`) y las librerías (`*.a`) necesarios para usar gtest.
Una vez instalada la librería puede eliminar el directorio `googletest` en el que copió el repositorio.

El repositorio de esta práctica contiene un directorio `gtests` con el siguiente contenido:
```
gtests
  ├── CMakeLists.txt
  ├── src
  │   ├── addition.cc
  │   ├── addition.h
  │   ├── date.cc
  │   ├── date_client_program.cc
  │   ├── date.h
  │   ├── factorial.cc
  │   ├── factorial.h
  │   ├── formula.cc
  │   ├── formula.h
  │   ├── main_program.cc
  │   ├── multiply.cc
  │   ├── multiply.h
  │   ├── sample2.cc
  │   ├── sample2.h
  │   ├── square_root.cc
  │   └── square_root.h
  └── test
      ├── gtest_main.cc
      ├── sample2_unittest.cc
      ├── test_addition.cc
      ├── test_date.cc
      ├── test_factorial.cc
      ├── test_formula.cc
      ├── test_multiply.cc
      └── test_square_root.cc
```
Siguiendo la costumbre habitual, el subdirectorio `src` contiene el código fuente del proyecto, que en este
caso es un proyecto ficticio que se usa para ilustrar el uso de tests unitarios.
A modo de ejemplo, el programa principal del proyecto `main_program.cc` (véase su código fuente)
invoca a diferentes funciones de carácter matemático que han sido
desarrolladas por el usuario (ficheros `src/*.cc` y `src/*.h`).

Compile el proyecto cuya configuración viene especificada en el fichero `CMakeLists.txt` ejecutando en el directorio
`gtests`:
```
$ mkdir build
$ cd build
$ cmake ..
$ make
```
Esta secuencia de comandos creará en el subdirectorio `build` sendos programas ejecutables: `user_program` y `runTests`.
El primero de ellos corresponde con el programa principal del usuario.
Pruebe a ejecutarlo y revise el código de las diferentes funciones que utiliza ese programa.

Por otra parte, el programa `runTests` ejecuta todos los tests unitarios que se han desarrollado para comprobar el correcto
funcionamiento de las diferentes funciones que intervienen en el programa del usuario.
Pruebe asimismo a ejecutarlo.
Ambos programas se pueden compilar de forma independiente ejecutando en el diectorio `build`:

```
$ make user_program
```
o bien:
```
$ make runTests
```

Estudie el contenido del fichero `CMakeLists.txt` y observe en el mismo (comandos `add_executable(runTests ...)`
y `add_executable(user_program)`) los ficheros que están involucrados en cada uno de los dos programas
anteriores.

Lo que más interesa estudiar a continuación es el contenido del directorio `tests`.
En ese directorio, el programa `gtest_main.cc` invoca la ejecución de todos los tests mientras que los
diferentes ficheros `test_*.cc` contienen los tests correspondientes a las diferentes funciones del usuario
que utiliza el programa `main_program.cc`.

Todos los ficheros del directorio `tests` contienen la línea
```
include <gtest/gtest.h>
```

de inclusión del fichero de cabecera donde se definen las macros y funciones de la librería de testing de
Google que se enlaza (*link*) con el programa.
Cada uno de esos ficheros contiene uno o más tests que tienen la siguiente estructura:
```
TEST(TestSuiteName, TestName) {
  ... test body ...
}
```
El primer parámetro de la macro TEST (`TestSuiteName`) es el nombre que se le da a un conjunto de tests
relacionados mientras que el segundo parámetro es el nombre que se le ha dado al test.

El test del fichero `test_date` es un ejemplo que comprueba métodos de una clase definida por el
usuario.
En este caso el test comprueba un par de métodos de la clase `Date`.

Los ficheros `test/sample2_unittest.cc` y  `src/sample2.*` están tomados de
[Googletest Samples](https://github.com/google/googletest/blob/master/googletest/docs/samples.md) 
donde se pueden hallar ejemplos adicionales de tests.

Estudie los tests que figuran en el directorio `gtests/test` para las diferentes funciones del ejemplo,
conjuntamente con la documentación del 
[Googletest Primer](https://github.com/google/googletest/blob/master/googletest/docs/primer.md)
para aprender sobre los diferentes tipos de 
[aserciones](https://es.wikipedia.org/wiki/Aserci%C3%B3n_(inform%C3%A1tica))
y comparaciones que soporta la plataforma para realizar sus tests.

En todos los programas C++ que desarrolle de ahora en adelante, utilice siempre gtests para comprobar la
corrección de todas sus funciones y métodos.
El enfoque (TDD) le ayudará a hallar los bugs de forma temprana de modo que podrá solucionarlos con un menor
coste en tiempo y esfuerzo.
La técnica de *testing* es fundamental para detectar cuanto antes potenciales errores.
Las funciones que han sido comprobadas mediante tests unitarios son siempre más fiables.
Para cada función que escriba de ahora en adelante, comience siempre por escribir antes que el código de la
función, al menos dos tests: uno para las situaciones "normales" y otro para situaciones "extremas".

La regla a seguir de ahora en adelante es **Convierta en un hábito la escritura de tests para sus programas**.
Desarrolle siempre sus funciones iterando el famoso ciclo TDD que ya se ha expuesto en este documento:
* Escriba un test que falle y que define una mejora deseada o una nueva función
* Escirba el código (función, método) que haga que la prueba pase satisfactoriamente 
* Finalmente refactoriza el nuevo código hasta obtener un resultado satisfactorio

Es fácil encontrar en la web mucha documentación sobre TDD. 
A modo de ejemplo e introducción se recomienda el estudio de
[Mejorar la calidad del código mediante la prueba unitaria](https://www.mql5.com/es/articles/1579).

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
