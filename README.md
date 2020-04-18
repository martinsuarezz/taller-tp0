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
Se dejó un espacio innecesesario entre la línea de código y el punto y coma final.

### b. Errores de generación del ejecutable

`paso1_main.c:22:9: error: unknown type name 'wordscounter_t'`

`paso1_main.c:23:9: error: implicit declaration of function 'wordscounter_create' [-Wimplicit-function-declaration]`

`paso1_main.c:24:9: error: implicit declaration of function 'wordscounter_process' [-Wimplicit-function-declaration]`

`paso1_main.c:25:24: error: implicit declaration of function 'wordscounter_get_words' [-Wimplicit-function-declaration]`

`paso1_main.c:27:9: error: implicit declaration of function 'wordscounter_destroy' [-Wimplicit-function-declaration]`

Todos estos errores son de compilación. En paso1_main.c se llama a funciones no definidas y se utiliza el tipo de dato 'wordscounter_t' que tampoco fue definido con anterioridad.

### c. Reporte de WARNINGS

El sistema no reportó warnings. Esto se debe a que se le dio la instructiva al compilador `-Werror` para que todos los warnings se traten como errores.

## Paso 2

### a. Correcciones con respecto al paso 1

Básicamente se corrigieron todos los errores de estilo dejando la funcionalidad intacta. El strcpy() fue reemplazado con memcpy().

### b. Ejecución correcta de la verificación de normas de programación

s

### c. Errores de generación del ejecutable

`paso2_wordscounter.h:7:5: error: unknown type name 'size_t'`

`paso2_wordscounter.h:20:1: error: unknown type name 'size_t'`

`paso2_wordscounter.h:25:49: error: unknown type name 'FILE'`

Estos dos errores se deben a que no se declaro el tipo 'size_t' y 'FILE' en el programa. Son errores de compilación.

`paso2_wordscounter.c:17:8: error: conflicting types for 'wordscounter_get_words'`

`paso2_wordscounter.h:20:8: note: previous declaration of 'wordscounter_get_words' was here size_t wordscounter_get_words(wordscounter_t *self);`

En este contexto asumo que este error se da porque no se definió de manera correcta wordscounter_get_words al no existir el tipo 'size_t' (por los errores anteriores).

`paso2_wordscounter.c:30:25: error: implicit declaration of function 'malloc' [-Wimplicit-function-declaration]`

`paso2_wordscounter.c:30:25: error: incompatible implicit declaration of built-in function 'malloc' [-Werror]`

La función 'malloc' nunca fue declarada.

Todos estos son errores de tiempo de compilación.

## Paso 3

### a. Correcciones con respecto al paso 2

Básicamente se incluyeron las librerías stdlib.h, string.h y stdio.h solucionando los errores del paso anterior.

### b. Errores de generación del ejecutable

`paso3_main.c:27: undefined reference to 'wordscounter_destroy'`

La función 'wordscounter_destroy' fue declarada pero nunca fue definida.

## Paso 4

### a. Correcciones con respecto al paso 3

El único cambio es que se le definió una funcionalidad a función 'wordscounter_destroy' (en este caso no hace nada).

### b. Ejecución de Valgrind en la prueba 'TDA'

    ==00:00:00:00.585 3882== 344 bytes in 1 blocks are still reachable in loss record 1 of 2
    ==00:00:00:00.585 3882==    at 0x402D17C: malloc (in /usr/lib/valgrind/vgpreload_memcheck-x86-linux.so)
    ==00:00:00:00.585 3882==    by 0x409C279: __fopen_internal (iofopen.c:69)
    ==00:00:00:00.585 3882==    by 0x409C33D: fopen@@GLIBC_2.1 (iofopen.c:97)
    ==00:00:00:00.585 3882==    by 0x8048517: main (paso4_main.c:14)

Este error hace referencia a que en la linea 14 de paso4_main.c se abre el archivo recibido por el programa pero nunca se lo cierra.

    ==00:00:00:00.585 3882== 1,505 bytes in 215 blocks are definitely lost in loss record 2 of 2
    ==00:00:00:00.585 3882==    at 0x402D17C: malloc (in /usr/lib/valgrind/vgpreload_memcheck-x86-linux.so)
    ==00:00:00:00.585 3882==    by 0x8048685: wordscounter_next_state (paso4_wordscounter.c:35)
    ==00:00:00:00.585 3882==    by 0x8048755: wordscounter_process (paso4_wordscounter.c:30)
    ==00:00:00:00.585 3882==    by 0x8048535: main (paso4_main.c:24)

La memoria que es pedida por el 'malloc' de la línea 35 de paso4_wordscounter.c nunca es liberada por el programa.

### c. Ejecución de Valgrind en la prueba 'Long Filename'

    *00:00:00:00.509 3843** memcpy_chk: buffer overflow detected: program terminated
    ==00:00:00:00.509 3843==    at 0x402FD97: ??? (in /usr/lib/valgrind/vgpreload_memcheck-x86-linux.so)
    ==00:00:00:00.509 3843==    by 0x40346EB: __memcpy_chk (in /usr/lib/valgrind/vgpreload_memcheck-x86-linux.so)
    ==00:00:00:00.509 3843==    by 0x804850A: memcpy (string3.h:53)
    ==00:00:00:00.509 3843==    by 0x804850A: main (paso4_main.c:13)

Este error ocurre porque el programa utiliza en su función 'main' un buffer de 30 caracteres de largo para el nomnbre del archivo de entrada. En esta prueba se ingresa un archivo que tiene 33 caracteres de largo, superando el tamaño del buffer y haciendo que 'memcpy' lanze un error.

### d. Uso de strncpy

Strncpy sería una función más indicada para esta situación ya que se esta trabajando con strings. Sin embargo, lo lógico sería que el tamaño de caracteres a copiar sea definido por el tamaño del array de destino.
La prueba si sólo se cambia la función memcpy por strncpy probablemente hubiera fallado de igual manera.

### e. Segmentation fault y buffer overflow

Segmentation fault es un error que sucede cuando un programa intenta acceder a una porción de memoria que no le pertence. El sistema operativo por seguridad termina el programa.
Buffer overflow es un problema que sucede cuando se accede a una posición que sobrepasa los límites de cierta estructura. Por ejemplo, si declaro un array de 10 lugares y luego procedo a acceder a la posición 15. Probablemente no haya un segmentation fault ya que estoy accediendo a una posición de memoria que posee mi programa. Sin embargo, esta información probablemente pertenezca a otras partes del programa y su modificación puede conducir a errores de funcionamiento.

## Paso 5

### a. Correcciones con respecto al paso 4

En el código se quitaron dos casos en los que se utilizaba memoria dinámica. En cambio esa información se almaceno simplemente dentro de variables en las funciones.

### b. Pruebas 'Invalid File' y 'Single Word'

La prueba 'Invalid File' falla ya que espera que el programa devuelva un 1 (ya que no se le entrego un archivo válido). El programa en este caso está devolviendo un 255. Esto sucede porque se determinó que en caso de error el programa devuelva -1. Probablemente al comparar errores se realiza un casteo a unsigned char llevando el -1 a 255. El SERCOM advierte de esta situación: `Se esperaba terminar con un código de retorno 1 pero se obtuvo 255.`.

La prueba 'Single Word' falla ya que se espera que el programa devuelva 1, sin embargo está devolviendo 0. En el SERCOM se puede observar esto dentro de la pestaña de diferencias.

### c. Hexdump

### d. Ejecución con gdb

## Paso 6

### a. Correcciones con respecto al paso 3

Se cambió el codigo de error de -1 a 1. Los caracterés demilitadores de palabras se movieron a un 'define'.
Por otro lado, se modificó levemente la lógica del conteo de palabras dentro de 'wordscounter_next_state'. De esta manera, se le da la chance al programa de poder contar cuando solo hay una palabra. Anteriormente al llegar al end of file (EOF) esta función simplemente marcaba la finalización del texto mediante el estado 'STATE_FINISHED' sin aumentar el contador si hubo una palabra.

### b. Entregas realizadas

### c. Ejecución de la prueba 'Single Word' en forma local

