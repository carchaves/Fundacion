#Computación/AyOC 
###### Útiles
Officedaytime.com/simid512e
# Video 1 Preliminares
VIDEO 1 (29.18)
![](https://youtu.be/y0rVgqAMg0I?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
## Preliminares
Clase de ejercicios preliminares. (Repaso)
![[Compilador]]

![[Lenguaje Ensamblador]]

![[Linker]]
## Endianess
![[Endianess]]

...

# Video 2
VIDEO 2 (68)
![](https://youtu.be/ZRsl7k5mxC4?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
Cómo hacer un programa en ensamblador que imprima "Hola Mundo".

Un programa en su archivo objeto esta separado en secciones, estas contienen distintos tipos de datos que son utilizados por el sistema operativo para poder ser ejecutados.
Secciones:
- .data: Donde declarar variables globales inicializadas (DB, DW, DD y DQ).
- .rodata: Donde declarar constantes globales inicializadas.
- .bss: Donde declarar variables globales no inicializadas (RESB, RESW, RESD y RESQ).
- .text: Es donde se escribe el código.

 Etiquetas y símbolos:
 - global: Modificador que define un símbolo que va a ser visto externamente.
 - _ start: Símbolo Utilizando como punto de entrada de un programa.

Comandos e instrucciones para el ensamblador
- DB, DW, DD, DQ, RESB, RESW, RESD y RESQ
- expresión $, se evalúa en la posición en memoria al principio de la línea que contiene la expresión.
- comando EQU, para definir constantes que después no quedan en el archivo objeto.
- comando INCBIN, incluye un binario en un archivo assembler.
- prefijo TIMES, repite una cantidad de veces la instrucción que le sigue.

Llamadas al sistema operativo (syscalls).
como no tenemos acceso directo a la pantalla, llamamos al sistema operativo para que este intermedie la operación e imprima en pantalla. Para hacerlo se debe llamar al mismo mediante interrupciones (syscalls), mecanismo que provee el procesador para acceder al sistema operativo.
Para acceder a las syscalls hay que seguir los siguientes pasos.
![[Pasted image 20240916210148.png]]

Syscalls:
- sys_write (mostrar por pantalla)
	- Función 4
	- Parámetros:
		1.  dónde (1=stdout)
		2.  Dirección de memoria del mensaje
		3. Longitud del mensaje (en bytes)
- Terminar programa (exit)
	- Función 1
	- Parámetros:
		1. código de retorno ( 0= sin error)



# Video 3
VIDEO 3 (51)

![](https://www.youtube.com/watch?v=RFE2JPGhPRw&list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs&index=3)
13.00
# Pila y Convención C
1. Estructura y uso de la pila
2. Convención C 
   - Cómo funciona el Stack Frame y la Conservación de Registros
   - y el Pasaje de parámetros entre funciones
3. Cómo ensamblar, compilar y linkear código en C y ASM
## Estructura y uso de la pila
### Estructura de la pila
La estructura de la pila es un área de memoria asignada por el sistema operativo cuando carga un programa. Cuando cargamos un programa el sistema operativo asigna un área en la memoria para la pila de ese programa y asigna un Stack Pointer al tope de la pila en esa área.

Se grafica de la siguiente forma
![[Pasted image 20240921160729.png | 300]]
ESP o RESP es el puntero tope de la pila, las direcciones **==válidas==** se considerarán como las direcciones más grandes que la del puntero tope de la pila.

La pila tiene un ancho determinado que refiere a la alineación de la pila, es decir cuántos bits tiene cada entrada de la pila

EBP o REBP apunta a la base de la pila

![[Pasted image 20240921161605.png | 350]]
### Estructura de la pila particularmente en 32 bits
Cada entrada de la pila va a tener 4 bytes.
Las instrucciones para escribir en la pila son PUSH y POP, se podría usar instrucciones para mover a memoria, pero estas instrucciones no solo mueven a memoria sino que tambien modifican el tamaño de la pila cambiando el puntero tope de la pila
![[Pasted image 20240921162919.png | 350]]
### Estructura de la pila particularmente en 64 bits
El manejo es igual que en la pila de 32 bits salvo que los registros ahora son RSP y RBP y la alineación ahora es de 8 bytes.
Por otro lado la diferencia importante que tiene, es que a la hora de llamar a funciones debe estar alineada a 16 bytes, es decir dos posiciones de memoria.
![[Pasted image 20240921163416.png | 350]]
#### PUSH
![[Pasted image 20240921163731.png|350]]
#### POP
![[Pasted image 20240921163610.png|350]]

### Uso de la pila
Se usa para guardar información local de una función. Se guardan registros, variables locales, parámetros, etc. Que la función necesita para ser ejecutada.
Sirve tambien para guardar contexto como las direcciones de retorno entre funciones.

## Convención C
Qué es la convención C, cómo funciona para el llamado de funciones y para la preservación de registros.

Los llamados a subrutinas en C se codifican de manera estática, esto es porque únicamente depende de la firma de la función (que parámetros hay que pasarle a la función) para ser llamada.
Esto permite implementar bibliotecas de funciones externas al programa que luego pueden ser importadas al código y ser ejecutadas sin importar como fueron implementadas, únicamente se tendría que conocer los parámetros que toma dicha función y como debe ser llamada.

La convención define:
- Cómo las funciones reciben parámetros
- Cómo las funciones retornan el resultado
- Qué registros se deben preservar en una función, es decir qué registros debemos conservar pues es lo que asume la función llamadora.

Las convenciones dependen del sistema operativo y de la arquitectura del procesador.
En la materia se usan las dos siguientes:
![[Pasted image 20240921175331.png|500]]
### Stack frame
Es el área de memoria entre el puntero al tope de pila y el puntero a base de la pila. En esta área se pueden encontrar la dirección de retorno, el conjunto de registros preservados, las variables locales y los parámetros pasados por pila.

### Caso 32 bits preservación y retorno de registros
Se deben preservar los registros EBX, ESI, EDI y EBP
(Se deben preservar SOLO los registros en caso de que se modifiquen).


Se debe retornar a través de los registros de EAX o EDX (si EAX ocupa 64 bits)

Preservar la consistencia de la pila

Los parámetros se pasan por la pila,

La pila debe estar alineada a 4 bytes antes de un llamado a función

# Video 4
VIDEO 4 (30.38)
![](https://youtu.be/gDe8_2Ecmts?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 5 (53)
![](https://youtu.be/eLDZ9jOfsRM?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 6 (32)
![](https://youtu.be/JC6c_reOukY?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 7 (110)
![](https://youtu.be/F2tsrtlQujs?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 8 (99)
![](https://youtu.be/enTZMwGqOhs?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 9 (60)
![](https://youtu.be/wo04AbFeqhw?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 10 (68)
![](https://youtu.be/ynQuwACSgTM?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 11 (37)
![](https://youtu.be/BZYlufTzmTQ?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 12 (39)
![](https://youtu.be/OzbCzYTpNNA?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 13 (35)
![](https://youtu.be/p3pUUVU08x0?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 14 (40)
![](https://youtu.be/Zfnt7V-ASNE?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 15 (19)
![](https://youtu.be/CZjg8jjdUoM?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 16 (41)
![](https://youtu.be/attq7hBRejM?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 17 (31)
![](https://youtu.be/J5Bd_rXKNhc?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
VIDEO 18 (24)
![](https://youtu.be/i2MLpqRrKRs?list=PLJg8TnncNzeLDbEMkR18I8_6XWuu5htHs)
