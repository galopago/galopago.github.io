---
title: "Halloween talking clock based on Rpi Pico"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - english
tags:
  - AN003
  - RPI PICO  
  - C/C++ SDK
  - CIRCUITPHYTON
header:
     teaser: "/assets/images/HALLOWEEN_TALKING_CLOCK_TEASER.jpg.jpg"
---
Halloween talking clock that plays sounds every O'clock hour. Only a few external components (easy to source and solder) needed. The single side board could be manufactured in home. Very customizable project than involves multiple knowlede areas ([STEAM](https://en.wikipedia.org/wiki/STEAM_fields)): Electronics, programming, woodworking, arts, etc.

<figure>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_MEDIUM.jpg"> </a>
	<figcaption>Customized clock hanging on a wall</figcaption>
</figure>

Key component: [Quartz clock movement with trigger](https://s.click.aliexpress.com/e/_AfCGIL)
{: .notice--danger}


##### Concepto:

A lot of musical wall clocks on the market lacks the possibility of change original sounds. A clock with that capability can be built with an embedded system. But wich one to choose? Raspberry Pi Pico was choose for the 3 following reasons: 

* There's no need to install software for initial firmware dowload
* Onboard memory 2 MegaBytes of flash can store some amount of sounds withour requiring external memory
* Can be powered by 2xAA batteries without additional components

Rpi Pico draws about 1.6 mA in it's lowest power mode (deep sleep). Seems not much, but is too high for a battery powered circuit, because they will eshaust in around two months. For that reason an external power circuit that can shut off the board completely was added. After that power compsumpion lowered to 70 uA, so batteries will last for a year.

The Rpi Pico acts as as sound storage and player. To show the time and generate an O'clock signal, a quartz clock movement with trigger was used. Combining this 2 elements a talking sound clock was born

#### Key features:

* Two versions of the (almost) same application: One developed in [CircuitPython](https://www.adafruit.com/circuitpython) and the other in [C/C++ SDK](https://github.com/raspberrypi/pico-sdk).
* Compatible with the most common operating systems.
* No need to install apps for initial firmware download
* There's no need to recompile code (in the app developed in CircuitPython) to change sounds
* Up to 3 years in standby mode using a pair of AA batteries.
* Easy to source, and easy to solder components.

<figure>
	<a href="/assets/images/rpi_pico_sound_clock.png"> <img src="/assets/images/rpi_pico_sound_clock.png"> </a>
	<figcaption>Simplified diagram of power circuit</figcaption>
</figure>

##### El programa:

Al encenderse el Rpi Pico lo primero que este hace es poner en nivel bajo el GPIO que esta conectado al circuito de encendido para mantenerlo enganchado, luego determina cual debe ser el archivo a reproducir y al final de la reproducion pone el GPIO del circuito de encendido en nivel alto con lo que hace que el sistema se apague totalmente. Adicionalmente se cuenta con un sensor de luz conectado a una entrada analoga para determinar si es de noche y no reproducir sonidos.

Los archivos se reproducen en forma secuencial, uno a uno con cada encendido de la tarjeta, y para poder guardar la informacion del proximo archivo a reproducir se usa la memoria no volatil, asi que se debera ser cuidadoso al modificar el programa para evitar desgastes acelerados!

###### PARTICULARIDADES DE LA VERSION EN SDK C/C++:

Los sonidos a reproducir deberan ser convertidos a formato .WAV 16 bit monofonicos a 44100 Hz. Una vez hecho esto, se deberan procesar para generar archivos .h que contendran arrays[] de C e incluirlos en el codigo antes de compilar. El programa usa una salida digital mediante PWM e interrupciones para la reproduccion de los sonidos. 

La principal virtud es que la ejecucion es inmediata al encender la tarjeta. La principal desventaja es que por ahora solo reproduce archivos .WAV que consumen bastante memoria, y para cambiarlos se requiere recompilar el programa.

###### PARTICULARIDADES DE LA VERSION EN CIRCUITPYTHON:

Los sonidos a reproducir deberan ser convertidos a formato .MP3 monofonicos. El programa usa los modulos audiopwmio y audiomp3 para la reproduccion de los archivos, que son leidos desde el sistema de archivos que viene incorporado. simplemente descargarlos al Rpi Pico y listo! 

La principal virtud es la facilidad para cambiar los archivos de sonido: solo hay que arrastrar los nuevos archivos y reemplazar los actuales, ademas por ser en formato MP3 se puede almacenar unas 10 veces mas tiempo de sonido que en formato WAV. La principal desventaja es que la tarjeta toma algo mas de un segundo en ejecutar el codigo despues de encenderse, esto podria ser inadmisible en algunas aplicaciones.

##### El circuito:
Los componentes externos adicionales al Rpi Pico componen tres diferentes funcionalidades:

* __Encendido/Apagado__: El circuito esta compuesto principalmente por un MOSFET, el Drain se conecta a la señal 3V3_EN y el source a GND. En la compuerta hay 2 elementos un capacitor conectado a tierra y una resistencia conectada a V+. Este circuito funciona en 3 pasos que se repiten ciclicamente:

  * Paso 1: El condensador esta totalmente cargado, haciendo que el MOSFET entre en conduccion, llevando la señal 3V3_EN a tierra y apagando completamente la tarjeta.

  * Paso 2: El condensador se descarga rapidamente mediante un pulsador o señal de contacto proveniente de la maquinaria del reloj, haciendo que momentaneamente el MOSFET entre en estado de no conduccion y se encienda la tarjeta. Al encenderse la tarjeta, lo primero que hace el programa es mantener dicho condensador descargado mediante un GPIO que pone en nivel bajo
  
  * paso 3: La tarjeta mantendra el nivel bajo del GPIO durante la ejecucion del sonido. Al finalizar pondra dicho GPIO en nivel alto, haciendo que el condensador se cargue rapidamente y que el MOSFET entre en conducion y se apague la tarjeta. La tarjeta quedara apagada totalmente hasta una nueva pulsacion.

* __Amplificador de audio__: Consta de una sola etapa, mediante un unico transistor NPN conectado a una bocina de 8 Ohm. Posee una etapa previa de filtrado mediante condensador y resistencia, para evitar posible ruido de la salida digital PWM

* __Deteccion dia/noche__: Sensor de luz para determinar si los sonidos deben reproducirse ( en el dia ) o no se deben reproducir ( noche ), esto para evitar ruidos molestor a la madrugada!


##### Ensamblaje:

El Rpi Pico puede ser soldado directamente a la tarjeta de circuito impreso, con lo cual se obtendra un conjunto de poca altura, o se podran soldar pines tipo header al Rpi Pico y conector hembra en la PCB para lograr un sistema flexible donde se puede extraer el Pico a voluntad. Todos los demas componentes no representan mucho problema, pues son de montaje Thru-hole. Finalmente la bocina, el sensor de luz y el interruptor de reloj podrian montarse mediante conectores para poder removerlos a voluntad, o directamente los cables al PCB para mayor ahorro de espacio.

El diseño de la tarjeta es de una sola capa y puede hacerse de forma casera en caso de ser necesario. Se han dejado pads libres para conexion a la mayoria de los GPIO del Rpi Pico, con lo cual se puede expandir sin mucho esfuerzo.

La tarjeta cuenta con 4 orificios para montaje, donde puede ser sujetada a la parte trasera del reloj de pared


<figure class="third">
	<a href="/assets/images/SINSONTE_BOARD_HOMEMADE.jpg"> <img src="/assets/images/SINSONTE_BOARD_HOMEMADE_MEDIUM.jpg"> </a>
	<a href="/assets/images/SINSONTE_BOARD_NOCONNECTOR.jpg"> <img src="/assets/images/SINSONTE_BOARD_NOCONNECTOR_MEDIUM.jpg"> </a>
	<a href="/assets/images/SINSONTE_BOARD_WITHCONNECTORS.jpg"> <img src="/assets/images/SINSONTE_BOARD_WITHCONNECTORS_MEDIUM.jpg"> </a>
	<figcaption>Tarjeta casera, ejemplo de montaje directo y finalizada con conectores.</figcaption>
</figure>


Para la construccion del reloj se debe escoger un disco, o plato, que puede ser de madera o plastico lo suficientemente grande para que pueda ubicarse la maquinaria del reloj y la tarjeta reproductora de los sonidos. Se debera realizar la fijacion de los elementos electronicos, seguido a esto se pueden agregar algunos accesorios como luces led y finalmente se realiza el trabajo artistico.


<figure class="third">
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK_MECHANISM.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_MECHANISM_MEDIUM.jpg"> </a>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK_COMPONENTS.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_COMPONENTS_MEDIUM.jpg"> </a>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK_BACK.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_BACK_MEDIUM.jpg"> </a>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK_FRONT.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_FRONT_MEDIUM.jpg"> </a>
	<figcaption>Mecanismo con salida externa, elementos decorativos, finalizado por atras y finalizado de frente</figcaption>
</figure>

Para ajustar la hora, se deben retirar las baterias y todas las manecillas (horario, minutero y segundero). Girar muy lentamente la perilla de ajuste del mecanismo de reloj hasta escuchar un "click". En ese momento poner todas las manecillas apuntando a las 12. Poner las baterias. Al presionar el interruptor pulsador de la tarjeta se puede "avanzar" sonidos una hora con cada pulsacion.


#### Listado de materiales

| Component         | Get yours! | Datasheet                                          |
| -------- | ------ | ------------------------------------------------------------ |
| Female header 2.54mm | [shop now](https://s.click.aliexpress.com/e/_eNNciZ) | [FHA3-S1XX.pdf](/assets/pdf/FHA3-S1XX.pdf) |
| Male pin header 2.54mm | [shop now](https://s.click.aliexpress.com/e/_eMCUJv) | [PHA1-S3XX.pdf](/assets/pdf/PHA1-S3XX.pdf) |
| 1/4W 1% TH Resistors | [shop now](https://s.click.aliexpress.com/e/_eMCbH1) | [MGR-SERIES.pdf](/assets/pdf/MGR-SERIES.pdf) |
| Push button 6x6mm | [shop now](https://s.click.aliexpress.com/e/_eKd4YV) | [TS-1301.pdf](/assets/pdf/TS-1301.pdf) |
| Raspberry Pi Pico | [shop now](https://s.click.aliexpress.com/e/_AXStdl) | [pico-datasheet.pdf](/assets/pdf/pico-datasheet.pdf) |
| 2xAA battery holder for PCB | [shop now](https://s.click.aliexpress.com/e/_AoI96B) | [Comfortable_Catalog.pdf](/assets/pdf/Comfortable_Catalog.pdf) |
| 8 Ohm speaker 29 mm 0.25W | [shop now](https://s.click.aliexpress.com/e/_ATihaX) | [DXP29W-A.pdf](/assets/pdf/DXP29W-A.pdf) |
| MOSFET 2N7000 | [shop now](https://s.click.aliexpress.com/e/_9j8Bgx) | [NDS7002A-D.pdf](/assets/pdf/NDS7002A-D.pdf) |
| NPN BIPOLAR TRANSISTOR 2N2222A | [shop now](https://s.click.aliexpress.com/e/_ANvtiX) | [P2N2222A-D.pdf](/assets/pdf/P2N2222A-D.pdf) |
| TH Radial Electrolytic Capacitor | [shop now](https://s.click.aliexpress.com/e/_9gn4vh) | [TS13DE-CD110X.pdf](/assets/pdf/TS13DE-CD110X.pdf) |
| TH Ceramic Disc Capacitor | [shop now](https://s.click.aliexpress.com/e/_Apm6Pd) | [TS15.pdf](/assets/pdf/TS15.pdf) |
| Quartz clock movement with trigger | [shop now](https://s.click.aliexpress.com/e/_AfCGIL) | [12888SE_TRIGGER_CLOCK_MOVEMENT.pdf](/assets/pdf/12888SE_TRIGGER_CLOCK_MOVEMENT.pdf) |
| Wall Clock hooks DIY | [shop now](https://s.click.aliexpress.com/e/_A0tg3V) | [wall_clock_hook.pdf](/assets/pdf/wall_clock_hook.pdf) |
| TEPT5700 visible light photodiode | [shop now](https://s.click.aliexpress.com/e/_AM6wDK) | [tept5700.pdf](/assets/pdf/tept5700.pdf) |
| LED Copper Wire with battery box | [shop now](https://s.click.aliexpress.com/e/_9vylbl) | [LED_Copper_Wire_Battery_Box.pdf](/assets/pdf/LED_Copper_Wire_Battery_Box.pdf) |


#### Circuito impreso

| PCB    |  Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Tarjeta de reproduccion de sonido (carpeta hardware) | [SINSONTE](https://github.com/galopago/SINSONTE)           |



#### Software

| Software    | Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Firmware en CircuitPython & SDK C/C++ (carpeta software)   | [SINSONTE](https://github.com/galopago/SINSONTE)           |

 

## Componentes opcionales:

| Componente         | Consigue el tuyo! | Hoja de caracteristicas                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| Juego de 3 brocas escalonadas 3-20 mm + centropunto  | [compralo aqui](https://s.click.aliexpress.com/e/_AalUrz)     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
