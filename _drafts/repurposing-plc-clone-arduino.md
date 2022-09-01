---
title: "Repurposing a PLC clone for use with Arduino"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - english
tags:
  - AN007
  - STM32
  - PLC
header:
     teaser: "/assets/images/AN007/PLC_CLONE_ARDUINO_TEASER.jpg"
---

It is fairly common to find in online shopping pages, advertising like this: "Industrial control board compatible with FX1N, FX2N, FX3U and programmable with GX software". The price is attractive, however, the documentation is non-existent, and there is no mention of how to program it with other tools like Arduino in other operating systems different from Windows. This article will introduce a few key concepts to help solve this problem.

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_MEDIUM.jpg"> </a>
	<figcaption>Industrial control board compatible with PLC programming software of a specific manufacturer</figcaption>
</figure>

Key component: [Industrial control board compatible with FX1N](https://s.click.aliexpress.com/e/_DDbOiuF)
{: .notice--danger}


##### Attack of the clones

These boards mention compatibility with GX software, which is manufactured by a [Japanese company that makes PLC and also cars.](https://www.mitsubishielectric.com/fa/products/cnt/plc/index.html) At first sight, the compatibility is not official, as no trademark is printed. Their origin is unknown, maybe they were simplified copies based on original schematics and source code, or somehow the native binary format of the PLC was reverse engineered and an [interpreter was built and runs in the microcontroller translating the code.](https://github.com/KeyMove/STM32-PLC-FX1N) Most of the cards are based on STM32 microcontrollers, and according to some articles and videos, [the original programming software actually recognizes them as an original PLC!](http://pdacontrolen.com/installation-gx-works2-demo-for-programming-plc-le3u-fk3u-lollette/)


<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_DINRAIL.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_DINRAIL_MEDIUM.jpg"> </a>
	<figcaption>Plastic enclosure, DIN rail installation </figcaption>
</figure>

Due to their low cost (around $25 USD), and for their relay isolated outputs, optically isolated inputs, RS232 serial port and regulated power supply, are great candidates for small projects as long as they can be programmed with a free multi-platform tool like Arduino or STM suite. In addition, a schematic diagram is needed to find out which I/O of the microcontroller goes to which peripheral in the board!

##### Bill of materials

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_PARTS.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_PARTS_MEDIUM.jpg"> </a>
	<figcaption>Parts used </figcaption>
</figure>

| Component                                           | Buy link                                          | Datasheet
|-----------------------------------------------------|------------------------------------------------------------|---------------
| Industrial control board compatible with FX1N   | [buy it](https://s.click.aliexpress.com/e/_DDbOiuF) | [industrial-control-board-fx1n.pdf](https://github.com/galopago/logistic/blob/main/datasheet/industrial-control-board-fx1n.pdf)
| 24 V 15 W  DIN rail mount power supply | [buy it](https://s.click.aliexpress.com/e/_DdcNhEL) | [24v-din-rail-power-supply.pdf](https://github.com/galopago/logistic/blob/main/datasheet/24v-din-rail-power-supply.pdf)
| USB to RS232 converter                             | [buy it](https://s.click.aliexpress.com/e/_DFlu2nD) | [usb-rs232-converter.pdf](https://github.com/galopago/logistic/blob/main/datasheet/usb-rs232-converter.pdf)
| DB9 solderless terminal connector            | [buy it](https://s.click.aliexpress.com/e/_Dl5STXV) | [db9-solderless-terminal-connector.pdf](https://github.com/galopago/logistic/blob/main/datasheet/db9-solderless-terminal-connector.pdf)
| 30 AWG UL1423 type PVDF wire               | [buy it](https://s.click.aliexpress.com/e/_eMiimB)  | [UL1423.pdf](https://github.com/galopago/logistic/blob/main/datasheet/UL1423.pdf)
| Dupont cable jumper                                | [buy it](https://s.click.aliexpress.com/e/_DmusOdH) | [dupont-jumper-cables.pdf](https://github.com/galopago/logistic/blob/main/datasheet/dupont-jumper-cables.pdf)
| Single line male header 2.54mm            | [buy it](https://s.click.aliexpress.com/e/_eMCUJv)  | [FHA3-S1XX.pdf](https://github.com/galopago/logistic/blob/main/datasheet/FHA3-S1XX.pdf)


| Pinout for industrial control boards              | repository 
| ------------------------------------------------- | ----------- 
| Industrial control boards based on STM32   | [stm32-industrial-control-boards](https://github.com/galopago/stm32-industrial-control-boards)

| Optional component                       | Buy link                                         | Datasheet 
| ----------------------------------------------|-----------------------------------------------------------|--------------- 
| Magnifying double eye for jewelry                  | [buy it](https://s.click.aliexpress.com/e/_DcZsrEF)| [magnifying-double-eye.pdf](https://github.com/galopago/logistic/blob/main/datasheet/magnifying-double-eye.pdf) 
| USB digital microscope camera                       | [buy it](https://s.click.aliexpress.com/e/_Dl3rIxZ)| [microscope-camera-digital-usb.pdf](https://github.com/galopago/logistic/blob/main/datasheet/microscope-camera-digital-usb.pdf) 
| Digital multimeter powered by AA batteries | [buy it](https://s.click.aliexpress.com/e/_DeAv3zv)| [digital-multimeter-powered-aa-batteries-ut139c.pdf](https://github.com/galopago/logistic/blob/main/datasheet/digital-multimeter-powered-aa-batteries-ut139c.pdf) 

##### Reprograming

The aforementioned board, sports a STM32F103 microcontroller, so instinctively a footprint for a SWD programming header should be looked for.


<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_PROGHEADER.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_PROGHEADER_MEDIUM.jpg"> </a>
	<figcaption>Possible programming header footprint at lower right</figcaption>
</figure>

After following the tracks of this header, one pin was found connected to 3.3 V, another one to GND, but the other two pins were not connected to SWD pins on the microcontroller but to PC10 and PC11 pins. Starting the search from the microcontroller, there are no tracks from SWD or USB pins, so the only alternative available for reprogramming is through UART1 using the bootloader stored in ROM


<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_UART1.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_UART1_MEDIUM.jpg"> </a>
	<figcaption>Serial port related components</figcaption>
</figure>

Following the tracks leaving from the DB9 connector, they end in an unmarked chip, however, due to the nearby capacitors it is probably a MAX232 or equivalent. Following the tracks leaving from this chip they end in PA9 and PA10 pins of the microcontroller which are the UART1 pins.

Luckily in this board, the resistor which is connected to the BOOT0 pin is clearly marked on the silkscreen. To start in bootloader mode, a male header was soldered to the 3.3 V pad, and using a Dupont wire jumper, a temporary connection between BOOT0 and 3.3 V is made while the board is powered up


<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_BOOT0.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_BOOT0_MEDIUM.jpg"> </a>
	<figcaption>Method used for bootloader activation</figcaption>
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
| X6        | PB4
| X7        | PD2


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

