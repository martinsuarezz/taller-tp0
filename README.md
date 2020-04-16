# Informe TP0

## Paso 0

### a. Capturas de pantallas de ejecución del aplicativo

s

### b. Valgrind

Valgrind es una apliccación de debuggeo que permite, entre otras cosas, analizar problemas de pérdida de memoria (memory leaks) del programa debuggeado.
Algunos comandos típicos son:

* `--leak-check=yes`: brinda un análisis más detallado sobre la pérdida de memoria del programa.
* `--show-reachable=yes`: muestra segmentos de memoria que podrían ser liberados por el programa, sin embargo el sistema operativo se encargó de ello. Por defecto estos no son errores para Valgrind.
* `--track-origins=yes`: ayuda a obtener información sobre variables a las cuales no se les asignó un valor y luego se utilizan en el programa.

### c. sizeof()

El operador sizeof() en C y C++ devuelve un entero positivo que representa el tamaño del tipo de datos que se le pasa. Por convención sizeof(char) siempre devuelve 1. Por otro lado, sizeof(int) como cualquier otro sizeof() puede devolver cualquier número ya que depende totalmente de la arquitectura del procesador. Generalmente, en un procesador de 32 bits, un entero se representa con 4 bytes por lo que sizeof(int) devolvería 4.

### d. sizeof() con structs

No necesariamente el sizeof() de una struct de C es igual a la suma del sizeof() de cada uno de sus elementos. Esto depende de cómo el procesador maneje el alineamiento de memoria.

    struct Vector{
        char X;
        int Y;
    }vector;