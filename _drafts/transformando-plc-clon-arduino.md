---
title: "Transformando PLC clon para usarlo con Arduino"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - espanol
tags:
  - AN007
  - STM32
  - PLC
header:
     teaser: "/assets/images/AN007/PLC_CLONE_ARDUINO_TEASER.jpg"
---

Es bastante comun encontrarse en las plataformas de venta en linea con este tipo de anuncio: "Tarjeta de control industrial, compatible con FX1N, FX2N, FX3U, y programable mediante software GX". El precio es muy conveniente, sin embargo, la documentacion es nula, y no se menciona su compatibilidad para ser programadas con otro tipo de herramientas como Arduino ni sistemas operativos diferentes a Windows. Este articulo presentara unas ideas claves sobre como resolver en cierto modo este problema

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_MEDIUM.jpg"> </a>
	<figcaption>Tarjeta de control industrial compatible con software de programacion PLC de determinado fabricante</figcaption>
</figure>

Componente clave: [Tarjeta de control industrial compatible con FX1N](https://s.click.aliexpress.com/e/_DDbOiuF)
{: .notice--danger}


##### El ataque de los clones

Estas tarjetas mencionan compatibilidad con el software GX, que es producido por una [empresa Japonesa que fabrica PLC y tambien automoviles.](https://mx.mitsubishielectric.com/fa/es/products/controllers/programmable-controllers-melsec) A simple vista se puede ver que la compatibilidad con dicha marca no es oficial, pues los dispositivos no tienen ningun tipo de marca ni documentacion. Su origen es bastante incierto, podria ser una copia simplificada basandose en planos y codigo fuente original, o que de alguna manera se realizo ingenieria inversa al formato binario nativo del PLC original y se [construyo un interpretador que traduce el codigo](https://github.com/KeyMove/STM32-PLC-FX1N). En su mayoria estas tarjetas incorporan microcontroladores STM32, y segun algunos articulos y videos, definitivamente [¡el software de programacion logra reconocerlas como PLC originales!](http://pdacontroles.com/instalacion-gx-works2-demo-para-programacion-plc-le3u-fk3u-lollette/)

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_DINRAIL.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_DINRAIL_MEDIUM.jpg"> </a>
	<figcaption>Carcasa plastica y compatible con montaje de riel DIN </figcaption>
</figure>

Por su bajo precio (Alrededor de $25 USD), y por disponer de reles de salida, entradas opto-acoplada, puerto RS232 y fuente de poder regulada, son ideales para realizar pequeños proyectos, siempre y cuando estas pudieran programarse con otro tipo de herramienta libre y multiplataforma como Arduino o la suite de STM. Adicional a lo anterior, se requeriria del esquematico para saber que pines de I/O del microcontrolador coinciden con los perifericos de la tarjeta!

##### Listado de materiales

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_PARTS.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_PARTS_MEDIUM.jpg"> </a>
	<figcaption>Partes usadas en el proceso</figcaption>
</figure>

| Componente                                          | Enlace de compra                                           | Hoja de datos
|-----------------------------------------------------|------------------------------------------------------------|---------------
| Tarjeta de control industrial compatible con FX1N   | [compralo aqui](https://s.click.aliexpress.com/e/_DDbOiuF) | [industrial-control-board-fx1n.pdf](https://github.com/galopago/logistic/blob/main/datasheet/industrial-control-board-fx1n.pdf)
| Fuente de poder 24 V 15 W  para montaje en riel DIN | [compralo aqui](https://s.click.aliexpress.com/e/_DdcNhEL) | [24v-din-rail-power-supply.pdf](https://github.com/galopago/logistic/blob/main/datasheet/24v-din-rail-power-supply.pdf)
| Convertidor USB a RS232                             | [compralo aqui](https://s.click.aliexpress.com/e/_DFlu2nD) | [usb-rs232-converter.pdf](https://github.com/galopago/logistic/blob/main/datasheet/usb-rs232-converter.pdf)
| Conector terminal DB9 no requiere soldar            | [compralo aqui](https://s.click.aliexpress.com/e/_Dl5STXV) | [db9-solderless-terminal-connector.pdf](https://github.com/galopago/logistic/blob/main/datasheet/db9-solderless-terminal-connector.pdf)
| Cable calibre 30 AWG tipo UL1423 PVDF               | [compralo aqui](https://s.click.aliexpress.com/e/_eMiimB)  | [UL1423.pdf](https://github.com/galopago/logistic/blob/main/datasheet/UL1423.pdf)
| Cables dupont jumper                                | [compralo aqui](https://s.click.aliexpress.com/e/_DmusOdH) | [dupont-jumper-cables.pdf](https://github.com/galopago/logistic/blob/main/datasheet/dupont-jumper-cables.pdf)
| Conector de hilera de pines macho 2.54mm            | [compralo aqui](https://s.click.aliexpress.com/e/_eMCUJv)  | [FHA3-S1XX.pdf](https://github.com/galopago/logistic/blob/main/datasheet/FHA3-S1XX.pdf)


| Mapa de pines para tarjetas de control industrial | repositorio 
| ------------------------------------------------- | ----------- 
| Tarjetas de control industrial basadas en STM32   | [stm32-industrial-control-boards](https://github.com/galopago/stm32-industrial-control-boards)

| Herramientas opcionales                       | Enlace de compra                                          | Hoja de datos 
| ----------------------------------------------|-----------------------------------------------------------|--------------- 
| Lentes dobles para relojeria                  | [compralo aqui](https://s.click.aliexpress.com/e/_DcZsrEF)| [magnifying-double-eye.pdf](https://github.com/galopago/logistic/blob/main/datasheet/magnifying-double-eye.pdf) 
| Microscopio digital USB                       | [compralo aqui](https://s.click.aliexpress.com/e/_Dl3rIxZ)| [microscope-camera-digital-usb.pdf](https://github.com/galopago/logistic/blob/main/datasheet/microscope-camera-digital-usb.pdf) 
| Multimetro digital alimentado por baterias AA | [compralo aqui](https://s.click.aliexpress.com/e/_DeAv3zv)| [digital-multimeter-powered-aa-batteries-ut139c.pdf](https://github.com/galopago/logistic/blob/main/datasheet/digital-multimeter-powered-aa-batteries-ut139c.pdf) 

##### Reprogramando

La tarjeta en cuestion, cuenta con un procesador STM32F103, por lo tanto, instintivamente se buscara una huella de header en el PCB con los pines para conectar un programador SWD

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_PROGHEADER.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_PROGHEADER_MEDIUM.jpg"> </a>
	<figcaption>Posible header para programacion en la derecha abajo del terminal de tornillos</figcaption>
</figure>

Despues de seguir las pistas de este header, se encontro que uno de los pines estaba conectado a 3.3 V el otro a GND, pero los restantes no estaban conectados a los pines SWD del microcontrolador, sino a los pines PC10 y PC11. Tampoco se encontraron pistas visibles saliendo de los pines SWD desde el procesador, ni tampoco de los pines USB, por lo tanto, la unica alternativa para lograr reprogramar el micro seria desde la UART1 usando el bootloader almacenado en la ROM.

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_UART1.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_UART1_MEDIUM.jpg"> </a>
	<figcaption>Componentes involucrados en el puerto serial</figcaption>
</figure>

Haciendo el seguimiento desde el conector DB9, las pistas llegan a un circuito integrado que tiene la referencia borrada, sin embargo, tratandose de un puerto serial, y por los condensadores cercanos, se puede deducir que es un MAX232 o similar. Siguiendo las pistas desde este integrado al procesador, efectivamente esta conectado a los pines PA9 y PA10 que corresponden a la UART1.

Afortunadamente, en esta tarjeta esta claramente marcada la resistencia que esta conectada al pin BOOT0, lo que sera necesario para ingresar al modo bootloader y poder iniciar a reprogramar la tarjeta. Para lograrlo se soldo un conector header macho al pad donde hay 3.3 V y mediante un cable Dupont, se conecta temporalmente el pin BOOT0 a 3.3 V mientras se aplica poder a la tarjeta.

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_BOOT0.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_BOOT0_MEDIUM.jpg"> </a>
	<figcaption>Metodo usado para entrar en modo bootloader</figcaption>
</figure>

Una vez ejecutandose el bootloader, se procedio a abrir [STM32CubeProg](https://www.st.com/en/development-tools/stm32cubeprog.html) y se constato la comunicacion con el microcontrolador. Se observo que este estaba en modo de proteccion de lectura, por lo que no se podria hacer un backup y dejar la tarjeta en su estado original. Se procedio a borrar toda la memoria flash del dispositivo.

Mediante el IDE de Arduino, se instalo el [STM32duino core](https://github.com/stm32duino/Arduino_Core_STM32) y se realizo una pequeña aplicacion de prueba que enviaba datos por el puerto serial. Se descargo el programa y se verifico que estos datos llegaban al computador. ¡Ahora empieza lo bueno!

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_USB232.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_USB232_MEDIUM.jpg"> </a>
	<figcaption>Convertidor USB a RS232 y conectores usados para la comunicacion entre el PC y la tarjeta</figcaption>
</figure>


##### Identificando los pines de I/O

Dado que no existe esquematico de la tarjeta, ni marcas en la serigrafia que indiquen cuales pines de I/O del microcontrolador van a que periferico, este trabajo se debera hacer manualmente, con paciencia siguiendo las pistas. Afortunadamente, la tarjeta es de solo 2 caras, asi,  haciendo uso de lentes de aumento y multimetro se inicia la aventura.

###### LED e interruptor

La tarjeta posee dos indicadores LED, uno etiquetado como RUN y el otro etiquetado como ERR. Tambien posee un interruptor que era usado por el antiguo firmware del PLC para detener la ejecucion del programa. Dado que estos perifericos tienen muy pocos elementos involucrados hasta llegar al microcontrolador, seran los mas faciles para iniciar.

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_SWITCHLEDS.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_SWITCHLEDS_MEDIUM.jpg"> </a>
	<figcaption>Pines de I/O para LED e interruptor identificados</figcaption>
</figure>

Los pines se encontraron mapeados de la siguiente manera:

|ELEMENTO              |PIN
|----------------------|-----
| LED RUN              | PB12
| LED ERR              | PB13
| INTERRUPTOR RUN/STOP | PC9

###### Entradas digitales

Las entradas son relativamente sencillas de encontrar, pues las pistas que salen del optoacoplador llegan directamente al microcontrolador. Solo unas pocas fueron problematicas, pues saltan a la otra cara y otras pasan debajo de componentes grandes.


<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_INPUTS.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_INPUTS_MEDIUM.jpg"> </a>
	<figcaption>Siguiendo las pistas de entrada</figcaption>
</figure>

Los pines se encontraron mapeados de la siguiente manera:

|ELEMENTO   |PIN
|-----------|-----
| X0        | PA0
| X1        | PA1
| X2        | PB9
| X3        | PA6
| X4        | PA7
| X5        | PB5
| X6        | PB4
| X7        | PD2

###### Salidas digitales

Las salidas tomaron la mayor cantidad de esfuerzo, pues estas van primero a un integrado UL2003 y de alli a cada uno de los reles, pasando por debajo de componentes e incluso cambiando de cara, aqui se uso el multimetro para poder seguir los caminos.

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_OUTPUTS.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_OUTPUTS_MEDIUM.jpg"> </a>
	<figcaption>Siguiendo las pistas de salida</figcaption>
</figure>

Los pines se encontraron mapeados de la siguiente manera:

|ELEMENTO   |PIN
|-----------|-----
| Y0        | PB8
| Y1        | PB1
| Y2        | PB10
| Y3        | PB0
| Y4        | PC5
| Y5        | PC4


###### Entradas analogas

Las entradas analogas tambien son relativamente faciles de encontrar, pues son pocas (3) y estan conectadas solamente mediante dos resistencias que conforman un divisor de voltaje (15 K/30 K) antes de ingresar al microcontrolador.

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_AINPUTS.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_AINPUTS_MEDIUM.jpg"> </a>
	<figcaption>Siguiendo las pistas de entradas analogas</figcaption>
</figure>

Los pines se encontraron mapeados de la siguiente manera:

|ELEMENTO   |PIN
|-----------|-----
| AD1       | PC1
| AD2       | PC2
| AD3       | PC0

##### Toques finales

En este momento ya se tienen mapeados todos los perifericos a los pines de I/O del microcontrolador, sin embargo, cada que se requiere programar, se debera hacer el puente entre los 3.3 V y el pin BOOT0. Lo que implica abrir la carcasa. Una solucion rapida seria cablear el interruptor que usaba el PLC para la funcion de RUN/STOP al pin BOOT0, de esta forma se podria activar/desactivar el bootloader de forma externa sin tener que quitar la tapa cada vez que se requiera reprogramarlo

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_BOOTSWITCH.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_BOOTSWITCH_MEDIUM.jpg"> </a>
	<figcaption>Interruptor para BOOT0 ahora accionable de forma externa</figcaption>
</figure>


##### Resumiendo

En este punto se tiene una tarjeta de bajo costo y con perifericos suficentes para realizar pequeños proyectos y experimentos sin requerir hardware adicional, y que puede ser programada mediante Arduino o la suite de STM. En caso de querer replicar esta experiencia con una tarjeta diferente (siempre y cuando se logre identificar la referencia de la CPU) se deberan seguir los siguientes pasos:

* Buscar la huella de un posible header de programacion SWD en la PCB (4 pines) y seguir las pistas para corroborar que si lo sea.
* Si el paso anterior falla, seguir los pines de la UART1 y agregar el hardware necesario para conectar al computador (convertidores de nivel, conectores, etc.)
* Buscar el pin BOOT0, generalmente va conectado a tierra mediante una resistencia, esta servira como "testpoint"
* Mediante STM32CubeProg borrar la memoria del microcontrolador. Si se usa la UART1 como medio de conexion, se debera ejecutar el Bootloader almacenado en la ROM poniendo el pin BOOT0 a 3.3 V cuando se conecta la alimentacion de la tarjeta.
* Mediante el IDE de Arduino o el de STM generar una pequeña aplicacion de transmision por puerto serial, para comprobar que la tarjeta puede ser programada.
* Seguir las pistas para encontrar los pines de I/O del microcontrolador conectados a los diversos perifericos
* Realizar una conexion entre el pin BOOT0 y el interruptor RUN/STOP para poder reprogramar con facilidad

##### Posibles mejoras

Crear una aplicacion esqueleto, sobre la que se escribiran todos los programas, esta aplicacion tendra algun tipo de mecanismo para verificar el estado del interruptor RUN/STOP cada vez que se inicia el programa, y saltar al bootloader que esta en la ROM para programacion o ejecutar el programa almacenado en la FLASH, de forma tal que no se requiera hacer la conexion electrica mediante cable que une el BOOT0 con el interruptor de RUN/STOP.

Otra alternativa, si no se quiere tener una aplicacion esqueleto con lineas de codigo adicionales, seria desarrollar un bootloader que use la UART1, similar al que hay almacenado en la ROM, pero almacenado en la FLASH, de forma tal que este sea lo primero que se ejecute siempre al alimentar el microcontrolador (sin requerir poner BOOT0 a 3.3 V), revise el estado del interruptor RUN/STOP, para descargar un nuevo programa, o para ejecutar el que ya hay almacenado.

