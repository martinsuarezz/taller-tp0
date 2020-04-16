# Informe TP0

## Paso 0

### a. Capturas de pantallas de ejecución del aplicativo

s

### b. Valgrind

Valgrind es una apliccación de debuggeo que permite, entre otras cosas, analizar problemas de pérdida de memoria (memory leaks) del programa debuggeado.
Algunos comandos típicos son:

* `--leak-check=yes`: brinda un análisis más detallado sobre la pérdida de memoria del programa.
* `--show-reachable=yes`: muestra segmentos de memoria que podrían ser liberados por el programa, sin embargo el sistema operativo se encargó de ello. Por defecto estos casos no son errores para Valgrind.
* `--track-origins=yes`: ayuda a obtener información sobre variables a las cuales no se les asignó un valor y luego se utilizan en el programa.

### c. sizeof()

El operador sizeof() en C y C++ devuelve un entero positivo que representa el tamaño del tipo de datos que se le pasa. Por convención sizeof(char) siempre devuelve 1. Por otro lado, sizeof(int) como cualquier otro sizeof() puede devolver cualquier número ya que depende totalmente de la arquitectura del procesador. Generalmente, en un procesador de 32 bits, un entero se representa con 4 bytes por lo que sizeof(int) devolvería 4.

### d. sizeof() con structs

No necesariamente el sizeof() de una struct de C es igual a la suma del sizeof() de cada uno de sus elementos. Esto depende de cómo el procesador maneje el alineamiento de memoria.

    struct Vector{
        char X;
        int Y;
    }vector;

En este ejemplo, corriéndolo en mi computadora sizeof(char) devuelve 1 y sizeof(int) devuelve 4. Sin embargo, sizeof(vector) devuelve 8. Esto ocurre porque luego del espacio de memoria para X, se dejan 3 bytes de padding.

### e. STDIN, STDOUT y STDERR

STDIN, STDOUT y STDERR son los archivos estándar de entrada y salida de información.
STDIN es el archivo de entrada estándar y por default está asignado a la entrada de teclado.
STDOUT es el archivo de salida de datos y por default está asignado a la consola.
STDERR es el archivo de salida de errores y por default tambien está asignado a la consola.

El proceso de redirección (utilizando los caracteres > y <) consiste en redirigir la salida de un programa a un archivo o obtener la entrada de un programa de un archivo.

`app1 > output.txt`: Este comando ejecuta app1 y guarda su salida en output.txt.

`app1 < input.txt`: Este comando ejecuta app1 obteniendo su entrada del archivo input.txt.

El proceso de pipeline (utilizando el caracter |) se basa en redirigir la salida de un programa a la entrada de otro.

`app1 | app2`: este comando va a ejecutar primero app1, tomar su salida estándar y utilizarlo como entrada estándar para app2.

## Paso 1

### a. Problemas de estilo

`./paso1_main.c:12:  Almost always, snprintf is better than strcpy  [runtime/printf] [4]`
sprintf tiene más funcionalidades que strcpy, además de tener que indicar el tamaño de caracteres a copiar evitando overflow del buffer.

`./paso1_main.c:15:  An else should appear on the same line as the preceding }  [whitespace/newline] [4]`
`./paso1_main.c:15:  If an else has a brace on one side, it should have it on both  [readability/braces] [5]`
Los else y else if de un condicional deben ir en la misma línea que termina el bloque anterior del condicional.

`./paso1_wordscounter.h:5:  Lines should be <= 80 characters long  [whitespace/line_length] [2]`
El comentario colocado en la línea 5 tiene más de 80 caracteres de largo, se debería dividir en dos líneas.

`./paso1_wordscounter.c:27:  Missing space before ( in while(  [whitespace/parens] [5]`
Entre el 'while' y el parentesis que abarca la condición debe haber un espacio.

`./paso1_wordscounter.c:41:  Mismatching spaces inside () in if  [whitespace/parens] [5]`
Dentro de un parentesis debe haber la misma cantidad de espacios entre los parentesis y la condición tanto a izquierda como a derecha.

`./paso1_wordscounter.c:41:  Should have zero or one spaces inside ( and ) in if  [whitespace/parens] [5]`
Dentro de un parentesis solo puede haber 0 o 1 espacio de separación entre los mismos y la condición.

`./paso1_wordscounter.c:47:  An else should appear on the same line as the preceding }  [whitespace/newline] [4]`
`./paso1_wordscounter.c:47:  If an else has a brace on one side, it should have it on both  [readability/braces] [5]`
Los else y else if de un condicional deben ir en la misma línea que termina el bloque anterior del condicional.

`./paso1_wordscounter.c:48:  Missing space before ( in if(  [whitespace/parens] [5]`
Entre el 'if' y el parentesis que abarca la condición debe haber un espacio.

`./paso1_wordscounter.c:53:  Extra space before last semicolon. If this should be an empty statement, use {} instead.  [whitespace/semicolon] [5]`
Se dejo un espacio innecesesario entre la línea de código y el ';'.

### b. Errores de generación del ejecutable

### c. Reporte de WARNINGS

## Paso 2

### a. Correciones realizadas

Básicamente se corrigieron todos los errores de estilo dejando la funcionalidad intacta. El strcpy() fue reemplazado con memcpy().
