---
title: "Reloj sonoro para halloween basado en Rpi Pico"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - espanol
tags:
  - AN003
  - RPI PICO  
  - C/C++ SDK
header:
     teaser: "/assets/images/HALLOWEEN_TALKING_CLOCK_TEASER.jpg.jpg"
---

Reloj con sonidos de halloween que son reproducidos cada hora en punto. Requiere pocos componentes externos, los cuales son faciles de conseguir y de soldar. La tarjeta de circuito impreso es de una sola cara y puede hacerse de forma casera. Proyecto bastante personalizable y que invulucra multiples areas ([STEAM](https://es.wikipedia.org/wiki/STEAM)):Montaje electronico, programacion, carpinteria, arte, manualidades, etc.

<figure>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_MEDIUM.jpg"> </a>
	<figcaption>Reloj personalizado instalado en la pared</figcaption>
</figure>

Componente clave: [Maquinaria para reloj de pared con contacto externo](https://s.click.aliexpress.com/e/_ABHS4B)
{: .notice--danger}


##### El concepto:

La gran mayoria de los relojes de pared musicales que se encuentran en el mercado vienen con sonidos que no pueden ser cambiados ni modificados. Esto podria solucionarse con infinidad de microcontroladores y/o sistemas embebidos que hay actualmente en el mercado. Como la idea del proyecto es hacer que sea lo mas facil posible para cualquier persona realizar la personalizacion de los sonidos sin necesitar muchos conocimientos informaticos, el proyecto se decanto por el Raspberry Pi Pico por 3 razones principalmente: Primera, no se requiere instalar **ninguna** aplicacion ni driver para descargar el firmware, segunda la tarjeta cuenta con 2 MegaBytes de memoria flash, por lo tanto se podrian grabar algunos sonidos en dicha memoria sin necesitar harware adicional como memorias SPI o Micro SD y por ultimo la alimentacion se puede hacer mediante dos baterias AA directamente sin requerir componentes adicionales!

La tarjeta Raspberry Pi Pico, tiene un consumo aproximado de 1.6 mA en su rango mas bajo (en modo sueño profundo). Aunque parece poco, es demasiado alto para un circuito alimentado con baterias AA, pues estas se descargarian aproximadamente en 2 meses. Por esta razon fue necesario agregar un circuito externo que apagara totalmente la tarjeta, cayendo el consumo a 70 uA aproximadamente, lo cual le otorgaria una autonomia de un año mas o menos.

La funcionalidad principal del Raspberry Pi Pico es almacenar archivos de sonido y reproducirlos. Para mostrar las horas y generar una señal cada hora en punto, se usa una maquinaria de reloj de pared que tiene una salida de contacto. Combinando estos 2 elementos se obtiene el reloj que reproduce sonidos cada hora en punto!



#### Principales Caracteristicas:

* Se han desarrollado 2 versiones que hacen practicamente lo mismo una en [CircuitPython](https://learn.adafruit.com/bienvenido-a-circuitpython-2/que-es-circuitpython) y la otra en el SDK de C/C++.
* Compatible con los sistemas operativos mas conocidos.
* No se requiere instalar ninguna aplicacion para descargar el Firmware inicial.
* La modificacion de los sonidos (en la version CircuitPython) no requiere recompilar codigo.
* Hasta 3 años de duracion de las baterias AA en modo espera.
* Componentes muy faciles de conseguir y ensamblar.

Los componentes externos que forman el amplificador de audio y circuito de encendido/apagado son pocos, faciles de conseguir y faciles de soldar. La tarjeta de circuito impreso puede hacerse de forma casera en una sola capa.


<figure>
	<a href="/assets/images/rpi_pico_sound_clock.png"> <img src="/assets/images/rpi_pico_sound_clock.png"> </a>
	<figcaption>Diagrama simplificado del sistema encendido/apagado</figcaption>
</figure>

##### El programa:

###### SDK C/C++:

Al encenderse el Rpi Pico lo primero que este hace es poner en nivel alto el GPIO que esta conectado al circuito de encendido para mantenerlo enganchado, luego determina cual debe ser el archivo a reproducir y al final de la reproducion pone el GPIO del circuito de encendido en nivel bajo con lo que hace que el sistema se apague totalmente. Adicionalmente se cuenta con un sensor de luz conectado a una entrada analoga para determinar si es de noche y no reproducir sonidos.

Los sonidos a reproducir deberan ser convertidos a formato .WAV 16 bit monofonicos a 44100 Hz. Una vez hecho esto, se deberan procesar para generar archivos .h que contendran arrays[] de C e incluirlos en el codigo antes de compilar. El programa usa una salida digital mediante PWM e interrupciones para la reproduccion de los sonidos. 

Los archivos se reproducen en forma secuencial, uno a uno con cada encendido de la tarjeta, y para poder guardar la informacion del proximo archivo a reproducir se usa la memoria no volatil, asi que se debera ser cuidadoso al modificar el programa para evitar desgastes acelerados!

La principal virtud del codigo generado mediante el SDK es que la ejecucion es inmediata al enceder la tarjeta. La principal desventaja es que por ahora solo reproduce archivos .WAV que consumen bastante memoria, y para cambiarlos se requiere recompilar el programa.

###### CircuitPython:

Al encenderse el Rpi Pico lo primero que este hace es poner en nivel alto el GPIO que esta conectado al circuito de encendido para mantenerlo enganchado, luego determina cual debe ser el archivo a reproducir y al final de la reproducion pone el GPIO del circuito de encendido en nivel bajo con lo que hace que el sistema se apague totalmente. Adicionalmente se cuenta con un sensor de luz conectado a una entrada analoga para determinar si es de noche y no reproducir sonidos.

Los sonidos a reproducir deberan ser convertidos a formato .MP3 monofonicos. El programa usa los modulos audiopwmio y audiomp3 para la reproduccion de los archivos, que son leidos desde el sistema de archivos que viene incorporado. simplemente descargarlos al Rpi Pico y listo! 

Los archivos se reproducen en forma secuencial, uno a uno con cada encendido de la tarjeta, y para poder guardar la informacion del proximo archivo a reproducir se usa la memoria no volatil, asi que se debera ser cuidadoso al modificar el programa para evitar desgastes acelerados!

La principal virtud del codigo generado mediante CircuiTpython es la facilidad para cambiar los archivos de sonido: solo hay que arrastrar los nuevos archivos y reemplazar los actuales, ademas por ser en formato MP3 se puede almacenar unas 10 veces mas tiempo de sonido que en formato WAV. La principal desventaja es que la tarjeta toma algo mas de un segundo en ejecutar el codigo despues de encenderse, esto podria ser inadmisible en algunas aplicaciones.

##### Circuito:
Los componentes externos adicionales al Rpi Pico componen tres diferentes funcionalidades: encendido/Apagado, amplificador de audio y deteccion dia/noche

* __Encendido/Apagado__: Un MOSFET se encarga de poner a tierra la señal 3V3_EN controlando el apagado/encendido total de la tarjeta. En la compuerta de dicho mosfet se encuentra un condensador que se carga mediante una resistencia grande, de forma tal que en condiciones normales el MOSFET esta en estado de conduccion apagando la tarjeta. en paralelo a este condensador hay un interruptor normalmente abierto que viene del reloj, el cual se cierra momentaneamente en cada hora en punto. Al cerrarse momentaneamente este interruptor, se descarga el condensador, el MOSFET deja de conducir y la tarjeta se enciente. Una vez el programa arranca, mediante un GPIO aplica un nivel bajo y mantiene el condensador descargado mientras transcurre la reproduccion del sonido. Una vez finalizado el sonido el GPIO aplica un nivel alto al condensador, este se carga, habilitando nuevamente el MOSFET y apagando la tarjeta hasta la proxima pulsacion del interruptor.

* __Amplificador de audio__: Consta de una sola etapa, mediante un unico transistor NPN conectado a una bocina de 8 Ohm. Posee una etapa previa de filtrado mediante condensador y resistencia, para evitar posible ruido de la salida digital PWM

* __Deteccion dia/noche__: Sensor de luz para determinar si los sonidos deben reproducirse ( en el dia ) o no se deben reproducir ( noche ), esto para evitar ruidos molestor a la madrugada!


##### Ensamblaje:

El Rpi Pico puede ser soldado directamente a la tarjeta de circuito impreso, con lo cual se obtendra una conjunto de poca altura, o se podra soldar pines header al Rpi Pico y conector hembra en la PCB para lograr un sistema flexible donde se puede extraer el Pico a voluntad. todos los demas componenter no representan mucho problema, pues son de montaje Thru-hole. finalmente la bocina, el sensor de luz y el interruptor de reloj podrian montarse mediante conectores para poder removerlos a voluntad, o directamente los cables al PCB para mayor ahorro de espacio.

El diseño de la tarjeta es de una sola capa y puede hacerse de forma casera en caso de ser necesario.Se han dejado pads libres para conexion a la mayoria de los GPIO del Rpi Pico, con lo cual se puede expandir sin mucho esfuerzo.

La tarjeta cuenta con 4 orificios para montaje, donde puede ser sujetada a la parte trasera del reloj de pared


<figure class="third">
	<a href="/assets/SINSONTE_BOARD_HOMEMADE.jpg"> <img src="/assets/images/SINSONTE_BOARD_HOMEMADE_MEDIUM.jpg"> </a>
	<a href="/assets/images/SINSONTE_BOARD_NOCONNECTOR.jpg"> <img src="/assets/images/SINSONTE_BOARD_NOCONNECTOR_MEDIUM.jpg"> </a>
	<a href="/assets/images/SINSONTE_BOARD_WITHCONNECTORS.jpg"> <img src="/assets/images/SINSONTE_BOARD_WITHCONNECTORS_MEDIUM.jpg"> </a>
	<figcaption>Tarjeta casera, ejemplo de montaje directo y finalizada con conectores.</figcaption>
</figure>


Se escogio un conector USB tipo impresora, por ser uno de los mas robustos e intuitivos. El conector usado es del tipo para montaje en panel y
tiene 4 pines para soldar los cables (VCC,USB+,USB-,GND). Este conector se soldo a una extension Micro USB que conectara al Rpi Pico. Los pedales usan conectores tipo aviacion

<figure class="third">
	<a href="/assets/images/USB_PEDAL_PICO_AVIATION.jpg"> <img src="/assets/images/USB_PEDAL_PICO_AVIATION_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_PANEL.jpg"> <img src="/assets/images/USB_PEDAL_PICO_PANEL_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_PRINTER.jpg"> <img src="/assets/images/USB_PEDAL_PICO_PRINTER_MEDIUM.jpg"> </a>
	<figcaption>Conectores para pedales y computador</figcaption>
</figure>

Una vez cerrada la caja, las actualizaciones al programa pueden hacerse modificando el archivo de CircuitPython, o usando la interfaz interactiva. Si se requiere hacer una reinstalacion de CircuitPython o "formatear" el Rpi Pico, debera abrirse la caja para tener acceso al boton bootsel.

#### Listado de materiales

| Componente         | Consigue el tuyo! | Hoja de caracteristicas
| -------- | ------ | ------------------------------------------------------------ |
| Tornillo M2.6 autorroscante tipo B | [💸](https://s.click.aliexpress.com/e/_esHHyb) | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf) |
| Espaciador separador de nylon G228 | [💸](https://s.click.aliexpress.com/e/_AqHnWn) | [G228.pdf](/assets/pdf/G228.pdf) |
| Tubo termoencogible 2:1 multiples colores| [💸](https://s.click.aliexpress.com/e/_Ar4Zmf) | [2_1_heatshrink_tube_colors.pdf](/assets/pdf/2_1_heatshrink_tube_colors.pdf) |
| Caja estanca generica resistente al agua de 115x90x55 mm | [💸](https://s.click.aliexpress.com/e/_9y9UWZ) | [KH-F2.pdf](/assets/pdf/KH-F2.pdf) |
| Raspberry Pi Pico | [💸](https://s.click.aliexpress.com/e/_9yrTG7) | [pico-datasheet.pdf](/assets/pdf/pico-datasheet.pdf) |
| Conector USB Tipo B IP68 para panel | [💸](https://s.click.aliexpress.com/e/_ATARh0) | [USB_TYPE_B_PANEL_MOUNT_CONNECTOR.pdf](/assets/pdf/USB_TYPE_B_PANEL_MOUNT_CONNECTOR.pdf) |
| Conector de aviacion 4 pines | [💸](https://s.click.aliexpress.com/e/_9IMuVU) | [CIRCULAR_AVIATION_PANEL_CONNECTOR.pdf](/assets/pdf/CIRCULAR_AVIATION_PANEL_CONNECTOR.pdf) |
| Interruptor momentaneo de pedal Metalico  | [💸](https://s.click.aliexpress.com/e/_AktOC6) | [METAL_MOMENTARY_ELECTRIC_FOOT_SWITCH.pdf](/assets/pdf/METAL_MOMENTARY_ELECTRIC_FOOT_SWITCH.pdf) |
| Cable de impresora USB tipo A | [💸](https://s.click.aliexpress.com/e/_A596l4) | [USB_PRINTER_CABLE.pdf](/assets/pdf/USB_PRINTER_CABLE.pdf) |
| Cable Micro USB | [💸](https://s.click.aliexpress.com/e/_AF0DcI) | [MICRO_USB_CABLE.pdf](/assets/pdf/MICRO_USB_CABLE.pdf) |

#### Componentes TUSISTEMITA

| PCB    |  Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Placa trasera para montaje A01 para caja de 158x90x60mm | [A01](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)           |
| Tarjeta breakout C11 con salida a terminales de tornillos para Rpi Pico  | [C11](https://github.com/galopago/TUSISTEMITA/tree/master/C_BREAKOUTS)        |



#### Software

| Software    | Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Firmware    | [PEDAL_USB_RPI_PICO](https://github.com/galopago/RPI_PICO_USB_FOOT_SWITCH)           |

 

## Componentes opcionales:

| Componente         | Consigue el tuyo! | Hoja de caracteristicas                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| Juego de 3 brocas escalonadas 3-20 mm + centropunto  | [💸](https://s.click.aliexpress.com/e/_AalUrz)     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
| Broca escalonada de 8 pasos 10-45 mm    | [💸](https://s.click.aliexpress.com/e/_ATtnjt)     | [8_steps_10-45mm_incremental_drill_bit.pdf](/assets/pdf/8_steps_10-45mm_incremental_drill_bit.pdf)           |
