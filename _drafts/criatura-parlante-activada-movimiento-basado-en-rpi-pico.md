---
title: "Criatura parlante activada por movimiento basado en Rpi Pico"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - espanol
tags:
  - AN004
  - RPI PICO  
  - C/C++ SDK
  - CIRCUITPHYTON
header:
     teaser: "/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_TEASER.jpg"
---

Figura con sonidos de halloween que son reproducidos al percibir movimientos. Requiere pocos componentes externos, los cuales son faciles de conseguir y de soldar. La tarjeta de circuito impreso es de una sola cara y puede hacerse de forma casera. Proyecto bastante personalizable y que involucra multiples areas ([STEAM](https://es.wikipedia.org/wiki/STEAM)):Montaje electronico, programacion, carpinteria, arte, manualidades, etc.

<figure>
	<a href="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER.jpg"> <img src="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_MEDIUM.jpg"> </a>
	<figcaption>Figura de halloween personalizada instalada en la pared</figcaption>
</figure>

Componente clave: [Mini sensor infrarojo pasivo (PIR) AM312](https://s.click.aliexpress.com/e/_Aa5UHj)
{: .notice--danger}


##### El concepto:

Este proyecto nacio como modificacion del [reloj parlante](https://galopago.github.io/espanol/reloj-sonidos-halloween-basado-en-rpi-pico/), pero en este caso, el encendido es activado por un sensor de movimiento PIR. Al aproximarse una persona se repoducira un sonido de forma aleatoria. Como la idea del proyecto es hacer que sea lo mas facil posible modificar los sonidos, el proyecto se decanto por el Raspberry Pi Pico por 3 razones principalmente: 

* No se requiere instalar **ninguna** aplicacion ni driver para descargar el firmware. 
* La tarjeta cuenta con 2 MegaBytes de memoria flash, por lo tanto se podrian grabar algunos sonidos en dicha memoria sin necesitar hardware adicional como memorias SPI o Micro SD.
* La alimentacion se puede hacer mediante dos baterias AA directamente sin requerir componentes adicionales!

La tarjeta Raspberry Pi Pico, tiene un consumo aproximado de 1.6 mA en su rango mas bajo (en modo sueño profundo). Aunque parece poco, es demasiado alto para un circuito alimentado con baterias AA, pues estas se descargarian aproximadamente en 2 meses. Por esta razon fue necesario agregar un circuito externo que apagara totalmente la tarjeta, cayendo el consumo a 70 uA aproximadamente, lo cual le otorgaria una autonomia de un año mas o menos.

La funcionalidad principal del Raspberry Pi Pico es almacenar archivos de sonido y reproducirlos.

#### Principales Caracteristicas:

* Se han desarrollado 2 versiones que hacen practicamente lo mismo: una en [CircuitPython](https://learn.adafruit.com/bienvenido-a-circuitpython-2/que-es-circuitpython) y la otra en el [SDK de C/C++](https://github.com/raspberrypi/pico-sdk).
* Compatible con los sistemas operativos mas conocidos.
* No se requiere instalar ninguna aplicacion para descargar el Firmware inicial.
* La modificacion de los sonidos (en la version CircuitPython) no requiere recompilar codigo.
* Hasta 3 años de duracion de las baterias AA en modo espera.
* Componentes muy faciles de conseguir y ensamblar.

<figure>
	<a href="/assets/images/rpi_pico_sound_motion.png"> <img src="/assets/images/rpi_pico_sound_motion.png"> </a>
	<figcaption>Diagrama simplificado del sistema encendido/apagado mediante sensor de movimiento</figcaption>
</figure>

##### El programa:

Al encenderse el Rpi Pico lo primero que este hace es poner en nivel bajo el GPIO que esta conectado al circuito de encendido para mantenerlo enganchado, luego determina cual debe ser el archivo a reproducir y al final de la reproducion pone el GPIO del circuito de encendido en nivel alto con lo que hace que el sistema se apague totalmente. Adicionalmente se cuenta con un sensor de luz conectado a una entrada analoga para determinar si es de noche y no reproducir sonidos.

Los archivos se reproducen en forma aleatoria, uno con cada encendido de la tarjeta.

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

  * Paso 2: El condensador se descarga rapidamente mediante la señal de proveniente del sensor de movimiento PIR, haciendo que momentaneamente el MOSFET entre en estado de no conduccion y se encienda la tarjeta. Al encenderse la tarjeta, lo primero que hace el programa es mantener dicho condensador descargado mediante un GPIO que pone en nivel bajo
  
  * paso 3: La tarjeta mantendra el nivel bajo del GPIO durante la ejecucion del sonido. Al finalizar pondra dicho GPIO en nivel alto, haciendo que el condensador se cargue rapidamente y que el MOSFET entre en conducion y se apague la tarjeta. La tarjeta quedara apagada totalmente hasta una nueva pulsacion.

* __Amplificador de audio__: Consta de una sola etapa, mediante un unico transistor NPN conectado a una bocina de 8 Ohm. Posee una etapa previa de filtrado mediante condensador y resistencia, para evitar posible ruido de la salida digital PWM

* __Deteccion dia/noche__: Sensor de luz para determinar si los sonidos deben reproducirse ( en el dia ) o no se deben reproducir ( noche ), esto para evitar ruidos molestor a la madrugada!


##### Ensamblaje:

El Rpi Pico puede ser soldado directamente a la tarjeta de circuito impreso, con lo cual se obtendra un conjunto de poca altura, o se podran soldar pines tipo header al Rpi Pico y conector hembra en la PCB para lograr un sistema flexible donde se puede extraer el Pico a voluntad. Todos los demas componentes no representan mucho problema, pues son de montaje Thru-hole. Finalmente la bocina, el sensor de luz y el sensor PIR podrian montarse mediante conectores para poder removerlos a voluntad, o directamente los cables al PCB para mayor ahorro de espacio.

El diseño de la tarjeta es de una sola capa y puede hacerse de forma casera en caso de ser necesario. Se han dejado pads libres para conexion a la mayoria de los GPIO del Rpi Pico, con lo cual se puede expandir sin mucho esfuerzo.

La tarjeta cuenta con 4 orificios para montaje, donde puede ser sujetada a la parte trasera de la figura


<figure class="third">
	<a href="/assets/images/SINSONTE_BOARD_HOMEMADE.jpg"> <img src="/assets/images/SINSONTE_BOARD_HOMEMADE_MEDIUM.jpg"> </a>
	<a href="/assets/images/SINSONTE_BOARD_NOCONNECTOR.jpg"> <img src="/assets/images/SINSONTE_BOARD_NOCONNECTOR_MEDIUM.jpg"> </a>
	<a href="/assets/images/SINSONTE_BOARD_WITHCONNECTORS.jpg"> <img src="/assets/images/SINSONTE_BOARD_WITHCONNECTORS_MEDIUM.jpg"> </a>
	<figcaption>Tarjeta casera, ejemplo de montaje directo y finalizada con conectores.</figcaption>
</figure>


Para la construccion de la figura se debe escoger un trozo de madera o plastico lo suficientemente grande para que pueda ubicarse la tarjeta reproductora de los sonidos. Se debera realizar la fijacion de los elementos electronicos, seguido a esto se pueden agregar algunos accesorios como luces led y finalmente se realiza el trabajo artistico.


<figure class="third">
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK_MECHANISM.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_MECHANISM_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_COMPONENTS.jpg"> <img src="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_COMPONENTS_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_BACK.jpg"> <img src="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_FRONT.jpg"> <img src="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_FRONT_MEDIUM.jpg"> </a>
	<figcaption>Sensor PIR con transistor para negacion de señal, tabla de madera contorno figura, finalizado por atras y finalizado de frente</figcaption>
</figure>

Al sensor de movimiento PIR se le ha agregado un transistor NPN para invertir la señal, de forma tal que sea compatible con el circuito original.


#### Listado de materiales

| Componente         | Consigue el tuyo! | Hoja de caracteristicas                                          |
| -------- | ------ | ------------------------------------------------------------ |
| Conector de hilera de pines hembra 2.54mm | [lo quiero comprar](https://s.click.aliexpress.com/e/_eNYVzN) | [FHA3-S1XX.pdf](/assets/pdf/FHA3-S1XX.pdf) |
| Conector de hilera de pines macho 2.54mm | [lo quiero comprar](https://s.click.aliexpress.com/e/_eP34IL) | [PHA1-S3XX.pdf](/assets/pdf/PHA1-S3XX.pdf) |
| Resistencias TH 1/4W 1% | [lo quiero comprar](https://s.click.aliexpress.com/e/_etm4gJ) | [MGR-SERIES.pdf](/assets/pdf/MGR-SERIES.pdf) |
| Interruptor momentaneo pulsador 6x6mm | [lo quiero comprar](https://s.click.aliexpress.com/e/_etiG5l) | [TS-1301.pdf](/assets/pdf/TS-1301.pdf) |
| Raspberry Pi Pico | [lo quiero comprar](https://s.click.aliexpress.com/e/_9yrTG7) | [pico-datasheet.pdf](/assets/pdf/pico-datasheet.pdf) |
| Soporte para bateria AA para montaje en PCB | [lo quiero comprar]( https://s.click.aliexpress.com/e/_Anq4sJ) | [Comfortable_Catalog.pdf](/assets/pdf/Comfortable_Catalog.pdf) |
| Bocina 8 Ohm 29 mm 0.25W | [lo quiero comprar](https://s.click.aliexpress.com/e/_A4pgQL) | [DXP29W-A.pdf](/assets/pdf/DXP29W-A.pdf) |
| MOSFET 2N7000 | [lo quiero comprar](https://s.click.aliexpress.com/e/_9h3XmP) | [NDS7002A-D.pdf](/assets/pdf/NDS7002A-D.pdf) |
| Transistor bipolar NPN 2N2222A | [lo quiero comprar](https://s.click.aliexpress.com/e/_A1K2OF) | [P2N2222A-D.pdf](/assets/pdf/P2N2222A-D.pdf) |
| Capacitor TH electrolitico | [lo quiero comprar](https://s.click.aliexpress.com/e/_9J9jbZ) | [TS13DE-CD110X.pdf](/assets/pdf/TS13DE-CD110X.pdf) |
| Capacitor TH Ceramico de disco | [lo quiero comprar](https://s.click.aliexpress.com/e/_9wCjd9) | [TS15.pdf](/assets/pdf/TS15.pdf) |
| Fotodiodo de luz visible TEPT5700 | [lo quiero comprar](https://s.click.aliexpress.com/e/_AKnaIM) | [tept5700.pdf](/assets/pdf/tept5700.pdf) |
| Mini sensor infrarojo pasivo (PIR) AM312 | [lo quiero comprar](https://s.click.aliexpress.com/e/_Aa5UHj) | [AS312.pdf](/assets/pdf/AS312.pdf) |


#### Circuito impreso

| PCB    |  Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Tarjeta de reproduccion de sonido (carpeta hardware) | [SINSONTE](https://github.com/galopago/SINSONTE)           |



#### Software

| Software    | Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Firmware en CircuitPython & SDK C/C++ (carpeta software app random)   | [SINSONTE](https://github.com/galopago/SINSONTE)           |

 

## Componentes opcionales:

| Componente         | Consigue el tuyo! | Hoja de caracteristicas                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| Juego de 3 brocas escalonadas 3-20 mm + centropunto  | [compralo aqui](https://s.click.aliexpress.com/e/_AalUrz)     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
