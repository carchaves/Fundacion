### Primera clase 18-08 (Introduccion a la Arquitectura y Organizacion de Computadores)
Alan Turing, Von Newmann, 
Charles Babbage Analitical Machine, series polinomicas, para calcular rutas maritimas, los engranajes tenian tanta precision que no la pudo armar, solo la planteo, fue el primero en hacer el programa almacenado.
Alan Turing, en el 36 enuncia un modelo teorico. Una cinta de lingitud infinita dividida en celdas contiguas, cualquier maquina que respondiera esa maquina era turing completa.
ENIAC, computadora de proposito general, primera. Era valvular, hacian de 70 a 80 grados de temperatura atras de la maquina.
EDVAC maquina turing completa. Publicada de 1945 despues de la guerra, antes no se publicaban porque eran maquinas de guerra.

Modelo Von MEWman tenian tres partes, tenia la posibilidad de incorporarle una memoria.
Von Meumann dejo un modelo de programa almacenado, Datos y programa en el mismo (unico) banco de memoria (variables y programa), maquina de estados perpetua.
Busqueda de instruccion, decodificación,  busqueda de operando, ejecuto, result. Al terminar busca otra instrucción y asi sucesivamente, un procesador no es inteligente en obediente.
Von Newmann, primero lo bardearon pero despues adoptaron su modelo, cuello de Von Newmann.
En un ciclo de reloj organizacion harvard, instruccion y variable almacenadas por memorias fisicamente distintas.

Hoy usamos organización von Newmann, pero incorporamos la memoria caché.

Segunda generación. Computadores transistorizados. Ventajas de menor consumo (no tan importante porque no habia tantas computadoras), menor espacio (eso estaba bueno porque se compactaron en los computadores), a largo plazo mejor desempeño.

1957 el primer compilador, FORTRAN (lo unico peor que windows).

La PDP 7 y 8 no eran compatibles, tenian distintos procesadores. Cuando hacen UNIX, estaban desarrollando un sistema multiusuario para General Electric, se hincharon las bolas y los dos tipos se dedicaron a hacer un arcade, de ahi salió lo que querían hacer y cuando lo presentaron le cuestionaron el hecho de haberlo programado en PDP 7 y que lo pasaran a la 9, como lo hicieron en assembly desarrollaron un compilador que se llamaba B y de ahi salió C.

Metieron UNIX en 16 kilobyte, no estaban para tirar manteca al techo. Tenian otras limitaciones en esa epoca

Biblioteca un conjunto de funciones

Las bibliotecas de C estan escritas en C, lo unico que no podes escribir en C es el encendido de la computadora, aproximadamente el 95% de lo que compila C esta escrito en C por lo que es muy transportable a otros sistemas. Actualmente todos los sistemas operativos estan escritos en C. Se están haciendo pruebas con RUST.

6800 motorola, 

IBM con materiales del supermercado armaron computadoras con el procesador de intel y otros perifericos, querian vender 250.000 computadoras, terminaron vendiendo 100 millones. Por como estaba armada y con el codigo del bios incluido cualquiera podia modificarla y programar en ella.

HALT and catch fire


Quien aca esta en situación de Windows. Bueno no se preocupen hay vacunas para eso.
Hay una raza muy especial de gente que son los usuarios.
No era ni siquiera binaria boludo.
C lo remplazó Python asi que la humanidad camina hacia su extinción.
Lo viejo funciona.
Actualmente los transistores llegan hasta 2 atomos, si seguimos a un atomo que queda después, medio atomo? dividir un atomo tiene sus consecuencias.
Alberto lo dijo, si se quieren suicidar aca tienen la formula, llego Opi y dijo bueno.

### Segunda Clase

el ensamblador es un programa que convierte el lenguaje ensamblador en unos y ceros, en el caso general, a veces no es uno a uno sino que crea una instruccion en varias.

el asembler no es un lenguaje generico cada maquina tiene su propio asembler en dependencia de la arquitectura.

es un bicho estupido que convierte el ensablador en unos y ceros.

lenguajes compilados, una sentencia no es una instruccion sino varias. Lo que hace el lenguaje de 

hace un tolkerizado, analisis sintactico, lo optimiza, toma el codigo y lo traduce a binario.

todo es texto plano

lo que va entre comillas es un puntero a caracteres

el return solo puede devolver una cosa de un tipo, puede no devolver nada.

char -> letra (1 byte)
int -> entero (4 byte)
int* -> puntero a 
char* -> string, null terminate letras de 1 bytes hasta encontrar un 0

printf no esta en el header

debuger 

los simbolos de debugin, informacion que esta en el codigo fuente. una linea esta escrito en un monton de instrucciones, el compilador hace que cada linea

gcc explorer

-start

### La Pila en os Procesadores IA-32 e Intel64

los procesadores de intel le dan mucha importancia a la pila, de forma que tiene un registro especifico que es el stack pointer.

Funcionamiento basico:
se expande hacia abajo, cuando sacamos algo el puntero incrementa y cuando agregamos algo decrementa. El elemento tiene un tamaño fijo, la pila de intel puede ser de 16 32 o 64
cuando la compu arranca la maquina es un procesador de 16. SP
cuando habilitas el modo 32 bits la pila tiene una palabra de 32. ESP
cuando habilitas el modo 64 bits la pila tiene una palabra de 64. RSP
lo determina el programador del sistema operativo

el pusheo no es una instruccion sencilla porque va a memoria

una vez que termine el proceso habría que vaciar la pila, pero hoy día el sistema operativo vacía la pila

la dirección con la que se inicia la pila tiene que estar en una posición multiplo de 8, alineada a su tamaño.

la pila se usa cuando llamamos a una subrutina y etc

cuando el hardware 
una interrupcion es algo que interrupe al procesador, es algo que tiene que ver con entrada y salida

call segment es un registro que te dice en que segmento estas
call near guarda el intruccion pointer
call far 

el tamaño de segmento es variable, las paginas tienen tamaño fijo.

las instrucciones son de tamaño variable entonces el instruccion pointer puede no estar alineado a 8.
cuando hace un call primero chequea cuanto mide la instruccion y le suma eso a la instruccion poniter, luego guarda eso en la pila



Interrupciones
llega cuando quiere, las interrupciones suelen generar una subrutina.




### Microarquitectura
menos de 50 años
Ley de moore
lighttography
ASML empresa holandesa con capitales estado unidense


### Clase práctica 28/08

gcc -Wall -pedantic -Wextra -Werror fizzbuzz

se pueden definir variables

CC = gcc
CFLAGS = -Wall -Wextra -pedantic
FILE = fizzbuzz.c
TARGET = fizzbuzz

all: $(TARGET) -> para ver que hay en las variables
	echo "Compilacion exitosa"
clean:
	rm  $(TARGET)
