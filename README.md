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


<a href="http://cooltext.com" target="_top"><img src="https://cooltext.com/images/ct_pixel.gif" width="80" height="15" alt="Cool Text: Logo and Graphics Generator" border="0" /></a>
