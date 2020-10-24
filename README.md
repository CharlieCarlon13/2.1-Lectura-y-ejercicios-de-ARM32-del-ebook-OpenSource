# 2.1-Lectura-y-ejercicios-de-ARM32-del-ebook-OpenSource
Resumen.

![](https://images.cooltext.com/5474871.png)


![](https://images.cooltext.com/5474803.png)

ARM es una arquitectura RISC (Reduced Instruction Set Computer=Ordenador con Conjunto Reducido de Instrucciones) de 32 bits, salvo la versión del core ARMv8-A que es mixta 32/64 bits (bus de 32 bits con registros de 64 bits). Se trata de una arquitectura licenciable, quiere decir que la empresa desarrolladora ARM Holdings diseña la arquitectura, pero son otras compañías las que fabrican y venden los chips, llevándose ARM Holdings un pequeño porcentaje por la licencia.

## Registros.
La arquitectura ARMv6 presenta un conjunto de 17 registros (16 principales más uno de estado) de 32 bits cada uno.

**Registros Generales.**
Su función es el almacenamiento temporal de datos. Son los 13 registros que van R0 hasta R12.

**Registros Especiales.**
Son los últimos 3 registros principales: R13, R14 y R15.
Como son de propósito especial, tienen nombres alternativos.
  * **SP/R13**. Stack Pointer ó Puntero de Pila. Sirve como puntero para almacenar variables locales y registros en llamadas a funciones.
  * **LR/R14**. Link Register ó Registro de Enlace. Almacena la dirección de
  retorno cuando una instrucción BL ó BLX ejecuta una llamada a una
  rutina.
  * **PC/R15**. Program Counter ó Contador de Programa. Es un registro que
  indica la posición donde está el procesador en su secuencia de instrucciones. Se incrementa de 4 en 4 cada vez que se ejecuta una instrucción,
  salvo que ésta provoque un salto.
  
**Registro CPSR.**
Almacena las banderas condicionales y los bits de control. Los
bits de control definen la habilitación de interrupciones normales (I), interrupciones rápidas (F), modo Thumb 1
(T) y el modo de operación de la CPU.

## Esquema de almacenamiento.

El procesador es Bi-Endian, quiere decir que es configurable entre Big Endian y
Little Endian. Aunque nuestro sistema operativo nos lo limita a Little Endian.
La dirección de un dato es la de su byte menos significativo. La memoria siempre se
referencia a nivel de byte, es decir si decimos la posición N nos estamos refiriendo
al byte N-ésimo, aunque se escriba media palabra, una palabra.

![](https://github.com/FernandoOliva18212205/2.1-Lectura-y-ejercicios-de-ARM32-del-ebook-OpenSource/blob/main/Imagenes/Imagen1Memoria.PNG)

![](https://images.cooltext.com/5474860.png)

El ensamblador es un lenguaje de bajo nivel que permite un control directo de
la CPU y todos los elementos asociados. Cada línea de un programa ensamblador
consta de una instrucción del procesador y la posición que ocupan los datos de esa
instrucción.

Desarrollar programas en lenguaje ensamblador es un proceso laborioso. El procedimiento es similar al de cualquier lenguaje compilado. Un conjunto de instrucciones
y/o datos forman un módulo fuente. Este módulo es la entrada del compilador, que
chequea la sintaxis y lo traduce a código máquina formando un módulo objeto. Finalmente, un enlazador (montador ó linker) traduce todas las referencias relativas a
direcciones absolutas y termina generando el ejecutable.

Generalmente, y dado que crear programas un poco extensos es laborioso, el
ensamblador se utiliza como apoyo a otros lenguajes de alto nivel para 3 tipos de
situaciones:
* Operaciones que se repitan un número elevado de veces.
* Cuando se requiera una gran velocidad de proceso.
* Para utilización y aprovechamiento de dispositivos y recursos del sistema.

![](https://images.cooltext.com/5474870.png)

Los pasos habituales para hacer un programa (en cualquier lenguaje) son los
siguientes: lo primero es escribir el programa en el lenguaje fuente mediante un editor de programas. El resultado es un fichero en un lenguaje que puede entender el
usuario, pero no la máquina. Para traducirlo a lenguaje máquina hay que utilizar
un programa traductor. Éste genera un fichero con la traducción de dicho programa,
pero todavía no es un programa ejecutable. Un fichero ejecutable contiene el programa traducido más una serie de códigos que debe tener todo programa que vaya a ser
ejecutado en una máquina determinada. Entre estos códigos comunes se encuentran
las librerías del lenguaje. El encargado de unir el código del programa con el código
de estas librerías es un programa llamado montador (linker) que genera el programa
ejecutable 

![](https://github.com/FernandoOliva18212205/2.1-Lectura-y-ejercicios-de-ARM32-del-ebook-OpenSource/blob/main/Imagenes/Imagen2Entorno.PNG)

## Aspecto de un programa en ensamblador

La principal característica de un módulo fuente en ensamblador es que existe
una clara separación entre las instrucciones y los datos. La estructura más general
de un módulo fuente es:

* Sección de datos. Viene identificada por la directiva .data. En esta zona se
definen todas las variables que utiliza el programa con el objeto de reservar
memoria para contener los valores asignados. Hay que tener especial cuidado
para que los datos estén alineados en palabras de 4 bytes, sobre todo después
de las cadenas. Alinear significa rellenar con ceros el final de un dato para que
el siguiente dato comience en una dirección múltiplo de 4 (con los dos bits
menos significativos a cero). Los datos son modificables.
* Sección de código. Se indica con la directiva .text, y sólo puede contener código
o datos no modificables. Como todas las instrucciones son de 32 bits no hay
que tener especial cuidado en que estén alineadas. Si tratamos de escribir en
esta zona el ensamblador nos mostrará un mensaje de error.

**Datos** 
Los datos se pueden representar de distintas maneras. Para representar números
tenemos 4 bases. La más habitual es en su forma decimal, la cual no lleva ningún
delimitador especial. 

**Simbolos**
Como las etiquetas se pueden ubicar tanto en la sección de datos como en la de
código, la versatilidad que nos dan las mismas es enorme. En la zona de datos, las
etiquetas pueden representar variables, constantes y cadenas. En la zona de código
podemos usar etiquetas de salto, funciones y punteros a zona de datos.

**Instrucciones**
* Instrucciones de transferencia de datos Mueven información entre registros
y posiciones de memoria. En la arquitectura ARMv6 no existen puertos ya
que la E/S está mapeada en memoria. Pertenecen a este grupo las siguientes
instrucciones: mov, ldr, str, ldm, stm, push, pop.
* Instrucciones aritméticas. Realizan operaciones aritméticas sobre números binarios o BCD. Son instrucciones de este grupo add, cmp, adc, sbc, mul.
* Instrucciones de manejo de bits. Realizan operaciones de desplazamiento, rotación y lógicas sobre registros o posiciones de memoria. Están en este grupo
las instrucciones: and, tst, eor, orr, LSL, LSR, ASR, ROR, RRX.
* Instrucciones de transferencia de control. Se utilizan para controlar el flujo de
ejecución de las instrucciones del programa. Tales como b, bl, bx, blx y sus
variantes condicionales.

**Directivas**
* Directivas de asignación: Se utilizan para dar valores a las constantes o reservar
posiciones de memoria para las variables (con un posible valor inicial).
* Directivas de control: .text y .data sirven para delimitar las distintas secciones de nuestro módulo.
* Directivas de operando: Se aplican a los datos en tiempo de compilación.

# Ejecucion QEMU.

![](https://github.com/FernandoOliva18212205/2.1-Lectura-y-ejercicios-de-ARM32-del-ebook-OpenSource/blob/main/Imagenes/correrraspian.PNG)
![](https://github.com/FernandoOliva18212205/2.1-Lectura-y-ejercicios-de-ARM32-del-ebook-OpenSource/blob/main/Imagenes/correrraspian2.PNG)
![](https://github.com/FernandoOliva18212205/2.1-Lectura-y-ejercicios-de-ARM32-del-ebook-OpenSource/blob/main/Imagenes/ComienzoQEMU.PNG)
![](https://github.com/FernandoOliva18212205/2.1-Lectura-y-ejercicios-de-ARM32-del-ebook-OpenSource/blob/main/Imagenes/ComienzoQEMU2.PNG)

![](https://images.cooltext.com/5474896.png)

## Modos de direccionamiento del ARM

En la arquitectura ARM los accesos a memoria se hacen mediante instrucciones
específicas ldr y str (luego veremos las variantes ldm, stm y las preprocesadas push
y pop). El resto de instrucciones toman operandos desde registros o valores inmediatos, sin excepciones. En este caso la arquitectura nos fuerza a que trabajemos de
un modo determinado: primero cargamos los registros desde memoria, luego procesamos el valor de estos registros con el amplio abanico de instrucciones del ARM,
para finalmente volcar los resultados desde registros a memoria.

**Direccionamiento inmediato.** El operando fuente es una constante, formando
parte de la instrucción.

**Direccionamiento inmediato con desplazamiento o rotación.** Es una variante del anterior en la cual se permiten operaciones intermedias sobre los registros.

# Tipos de datos

| ARM            | Tipo en C                                                        | bits           | Rango                                                                              |
|----------------|------------------------------------------------------------------|----------------|------------------------------------------------------------------------------------|
| .byte          | unsigned char  (signed) char                                     | 8  8           | 0 a 255  -128 a 127                                                                |
| .hword  .short | unsigned short int  (signed) short int                           | 16  16         | 0 a 65.535  -32.768 a 32767                                                        |
| .word  .int    | unsigned int  (signed) int  unsigned long int  (signed) long int | 32  32  32  32 | 0 a 4294967296  -2147483648 a 2147483647  0 a 4294967296  -2147483648 a 2147483647 |
| .quad          | unsigned long long  (signed) long long                           | 64  64         | 0 a 2^64  -2^63 a 2^63-1                                                           |



# Instrucciones de salto

Las instrucciones de salto pueden producir saltos incondicionales (b y bx) o
saltos condicionales. Cuando saltamos a una etiqueta empleamos b, mientras que
si queremos saltar a un registro lo hacemos con bx. La variante de registro bx la
solemos usar como instrucción de retorno de subrutina, raramente tiene otros usos.
En los saltos condicionales añadimos dos o tres letras a la (b/bx), mediante las
cuales condicionamos si se salta o no dependiendo del estado de los flags. Estas
condiciones se pueden añadir a cualquier otra instrucción, aunque la mayoría de las
veces lo que nos interesa es controlar el flujo del programa y así ejecutar o no un
grupo de instrucciones dependiendo del resultado de una operación (reflejado en los
flags).

# Estructuras de control de alto nivel

En este punto veremos cómo se traducen a ensamblador las estructuras de control
de alto nivel que definen un bucle (for, while, . . . ), así como las condicionales
(if-else).
Las estructuras for y while se pueden ejecutar un mínimo de 0 iteraciones (si
la primera vez no se cumple la condición).

Para programar en ensamblador estas estructuras se utilizan instrucciones de
salto condicional. Previo a la instrucción de salto es necesario evaluar la condición
del bucle o de la sentencia if, mediante instrucciones aritméticas o lógicas, con el
fin de actualizar los flags de estado. 

# Compilación a ensamblador

Normalmente los compiladores crean código compilado (archivos .o) en un único paso. En
el caso de gcc este proceso se hace en dos fases: en una primera se pasa de C a
ensamblador, y en una segunda de ensambladador a código compilado (código máquina). Lo interesante es que podemos interrumpir justo después de la compilación
y ver con un editor el aspecto que tiene el código ensamblador generado a partir del
código fuente en C.


<a href="http://cooltext.com" target="_top"><img src="https://cooltext.com/images/ct_pixel.gif" width="80" height="15" alt="Cool Text: Logo and Graphics Generator" border="0" /></a>
