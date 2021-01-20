---
title: "WiFi controlled waterproof LED string"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - english
tags:
  - AN001
  - WiFi
  - MONGOOSE OS
header:
     teaser: "/assets/images/MOS_WIFI_IOT_LIGHTS_TEASER.jpg"
---

Decorative lights suitable for Halloween, Christmas, parties, etc. Not only controlled over internet but, also completely reprogrammed 
wirelessly using OTA over WiFi. Waterproof, dustproof and sturdy. Ideal for indoor projects like interactive backgrounds for youtubers/streamers
controlled by their audience and for outdoor projects like advertizing signs in walls or vehicles.


<figure>
	<a href="/assets/images/MOS_WIFI_IOT_LIGHTS.jpg"> <img src="/assets/images/MOS_WIFI_IOT_LIGHTS_MEDIUM.jpg"> </a>
	<figcaption>Open enclosure showing internal components</figcaption>
</figure>

Key component: [WS2811 waterproof LED string.](https://s.click.aliexpress.com/e/_AFqDHl)
{: .notice--danger}


##### Concept:

With the advent of addressable LED like WS2812, WS2812b, WS2811, etc. is now possible for small microcontrollers to 
handle large amounts of LEDs with only one I/O pin. That advantage popularized this component and a lot of variants appeared: surface mount 
single leds, flexible strips, Christmas-like strings, etc. The last one will be used in this article due to its flexibility and strength and could adapt
easily to different project from Christmas ornaments to led matrix, without soldering or other electrical modifications.

The microcontroller chosen was an ESP8266, more exactly a development board known as "NODEMCU V3" which has all additional components necessary to start work on
programming the MCU with a computer. The onboard WiFi of the ESP8266 is not only possible to to change light sequences, but also download a totally different
firmware wirelessly (OTA), using a powerful combo: [Mongoose OS](https://mongoose-os.com/) and its remote device management dashboard [mDASH](https://mdash.net/).
Mongoose OS uses a scaled down version of JavaScript known as [mJS](https://github.com/cesanta/mjs). This is an attractive language for web developers whom already 
work with JS. Mongoose OS is built on top of Espressif's ESP-iDF, so it is possible to write functions in C, which is also attractive for more "traditional" embedded programmers.

The circuit is built using [TUSISTEMITA](https://github.com/galopago/TUSISTEMITA) hardware prototyping system, which provides different kinds of prebuilt modules which allows
to build an electronic project without soldering, but making it very robust and expandable. All the parts are enclosed in a dustproof and waterproof IP65 box. This enclosure gives an
"industrial look" to the project and also adds mechanical strength to withstand abuses. The external electrical connections (AC, and LEDs) were fitted with IP accessories to provide
a good seal.

#### Key features:
* Mongoose OS embedded operating system running on ESP8266.
* Dustproof, waterproof and wall mountable.
* Wireless remote firmware update, thanks to Mongoose OS management dashboard mDASH.
* Built with TUSISTEMITA hardware prototyping blocks
* 110/220V AC power

The circuit is composed of 4 elements well differentiated: Power source, CPU, logic level shifter and LEDs. Power source is switched type, 20W power, 5V output and 110/220V input, so
it could be used in any country of the world. ESP8266 was used as CPU (NODEMCU V3). This board can be powered by 3.3V directly to processor power pin or by 5V using the
onboard regulator. The high logic level output of ESP8266 is 3.3V, so a logic level shifter is needed for working with 5V sensors. WS2812 works with 5V logic levels so TUSISTEMITA D06
logic level board converter was used. This board is based on BSS138 MOSFET.

<figure>
	<a href="/assets/images/mos_wifi_iot_lights_blockdiag.png"> <img src="/assets/images/mos_wifi_iot_lights_blockdiag.png"> </a>
	<figcaption>Simplified block diagram</figcaption>
</figure>

Power source output current is around 3.8A max, and each WS2811 LED consumes 60 mA max, so at least 63 LED could be powered. To stay below absolute maximum only 50
LED is recommended. Any LED string that works with WS2811 compatible protocol could be used.

##### Mongoose OS:

Mongoose OS is an operating system for the Internet Of Things, it can run on ESP8266, ESP32 and others. Is a blend of easiness and robustness. Ideal for rapid prototyping
of IoT products because of its native built-in cloud connectivity (AWS, Google, Azure).
There are two characteristics that make Mongoose OS so versatile. One of them is the possibility to work "remote/local". Remote is the default option, and compiles
the code in the cloud, this is good for beginners because avoids the problems related to SDK installations. Local option is based on docker containers and is good for automatic builds
without internet connection.

Another important characteristic is the use of a scaled down version of JavaScript called mJS as programming language. Advanced functionalities could be written with
few lines of code compared to other languages (Assembler, C, Processing). However, nothing prevents to call functions written in C, especially for time sensitive device drivers.

##### Software:

Sample application presented here is composed of two tasks: Send color data for every LED in the string and listen to incoming data coming from the cloud.


To send data to each LED, the color code is randomly extracted from a predefined color table. Communication to the LED string is made using NEOPIXEL library bundled 
with Mongoose OS.

Para recibir los datos desde la nube, se realiza una conexion MQTT a un broker donde se escucha por un topico especifico. Una aplicacion cliente puede conectarse a este broker MQTT
y enviar un determinado dato al topico que se esta escuchando, y con esto se puede cambiar la paleta de colores que se esta usando para los LED. De esta forma
se presenta una aplicacion de ejemplo muy simple de como modificar la secuencia de forma remota a traves de internet. 

##### Ensamblaje:

El prototipo del sistema fue montado usando varios componentes de TUSISTEMITA, como la placa trasera para montaje, las tarjetas adaptadoras para la fuente y NODEMCU, tarjeta de 
conversion niveles logicos y borneras de tornillos para conexiones de salida. Una vez descargada la aplicacion por primera vez y comprobado que las conexiones electricas funcionan bien,
se puede pasar a la caja para montaje definitivo sin ningun traumatismo. Solamente hay que desconectar la alimentacion electrica de las borneras y la conexion
de salida a los leds, ajustar la placa a la caja y reconectar nuevamente.

<figure class="third">
	<a href="/assets/images/MOS_WIFI_LIGHTS_PARTS.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_PARTS_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_WIRED.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_WIRED_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_WORKING.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_WORKING_MEDIUM.jpg"> </a>
	<figcaption>Ensamblaje y cableado.</figcaption>
</figure>

Se recomienda cambiar los conectores originales de las tiras de led, por unos mucho mas robustos mecanicamente y a prueba de agua, para evitar problemas de oxido en caso
de estar expuestos a los elementos ambientales. Se aconseja el uso de termoencogible con pegamento para mayor proteccion en las uniones entre los cables
de la tira led y los conectores.

<figure class="third">
	<a href="/assets/images/MOS_WIFI_LIGHTS_CABLEGLAND.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_CABLEGLAND_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_CONNECTOR.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_CONNECTOR_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_FINISHED.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_FINISHED_MEDIUM.jpg"> </a>
	<figcaption>Conectores para proteccion de los cables</figcaption>
</figure>

Una vez la caja se encuentra cerrada, las actualizaciones de firmware se pueden hacer inalambricamente mediante OTA por medio del dashboard de Mongoose
OS mDash. 

#### Listado de materiales

| Componente         | Consigue el tuyo! | Hoja de caracteristicas
| -------- | ------ | ------------------------------------------------------------ |
| ESP8266 NodeMCU V3    | [💸](https://s.click.aliexpress.com/e/_AKwJKn)     | [NodeMCUV3.pdf](/assets/pdf/NodeMCUV3.pdf)           |
| Tira de LED WS2811 resistente al agua | [💸](https://s.click.aliexpress.com/e/_AFqDHl )  | [WS2811_WATERPROOF_LED_STRING.pdf](/assets/pdf/WS2811_WATERPROOF_LED_STRING.pdf)                               |
| Fuente de alimentacion conmutada 5V 3.8A 20W   | [💸](https://s.click.aliexpress.com/e/_A57h4j)     | [5V_4A_switching_power.pdf](/assets/pdf/5V_4A_switching_power.pdf)           |
| Caja estanca generica resistente al agua de 200x120x75mm (varias opciones: tapa transparente, salientes para montaje en pared)| [💸](https://s.click.aliexpress.com/e/_A2ZqFz)  | [g373_g269.pdf](/assets/pdf/g373_g269.pdf)           |
| Tornillo M2.6 autorroscante tipo B | [💸](https://s.click.aliexpress.com/e/_A6SvXp)  | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf)                           |
| Tornillo M3 cabeza avellanada en cruz | [💸](https://s.click.aliexpress.com/e/_AaJKaL)  | [M2-M10_Stainless_steel_304_countersunk_screw_flat_head_phillips.pdf](/assets/pdf/M2-M10_Stainless_steel_304_countersunk_screw_flat_head_phillips.pdf)                           |
| Tuerca M3 hexagonal con brida DIN6923 | [💸](https://s.click.aliexpress.com/e/_9AB0mF)  | [FLANGED_NUT_3MM_DIN6923.pdf](/assets/pdf/FLANGED_NUT_3MM_DIN6923.pdf)                           |
| Espaciador separador de nylon G228  | [💸](https://s.click.aliexpress.com/e/_AqHnWn)  | [G228.pdf](/assets/pdf/G228.pdf)                           |
| Conector glandula o prensa estopa PG7 o PG9 | [💸](https://s.click.aliexpress.com/e/_9AvHyT)  | [pg_7.pdf](/assets/pdf/pg_7.pdf) | 
| Conector resistente al agua para tira led  | [💸](https://s.click.aliexpress.com/e/_AMoPnv)  | [Waterproof_led_string_connector.pdf](/assets/pdf/Waterproof_led_string_connector.pdf)                           |
| Tubo termoencogible 3:1 con pegamento  | [💸](https://s.click.aliexpress.com/e/_AEtntV)  | [3_1_heatshrink_tube_glue.pdf](/assets/pdf/3_1_heatshrink_tube_glue.pdf)                           |
| Tubo termoencogible 2:1 multiples colores  | [💸](https://s.click.aliexpress.com/e/_Ar4Zmf)  | [2_1_heatshrink_tube_colors.pdf](/assets/pdf/2_1_heatshrink_tube_colors.pdf)                           |

#### Componentes TUSISTEMITA

| PCB    |  Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Placa trasera para montaje A02 para caja de 200x120x75mm | [A02](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)           |
| Placa adaptadora A05 con agujeros espaciados 10.16mm para fuente 5V 3.8A   | [A05](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)        |
| Tarjeta B01 para conexiones mediante terminales de tornillos 2x4 3.5mm | [B01](https://github.com/galopago/TUSISTEMITA/tree/master/B_SCREW_TERMINAL_WIRE_CONNECTORS)        |
| Tarjeta breakout C08 con salida a terminales de tornillos para NODEMCU V3  | [C08](https://github.com/galopago/TUSISTEMITA/tree/master/C_BREAKOUTS)        |
| Tarjeta D06 de conversion de niveles logicos  | [D06](https://github.com/galopago/TUSISTEMITA/tree/master/D_ELECTRONICS)        |


#### Software

| Software    | Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Firmware    | [MOS_IOT_ADDRESSABLE_LEDS](https://github.com/galopago/MOS_IOT_ADDRESSABLE_LEDS)           |

 

## Componentes opcionales:

| Componente         | Consigue el tuyo! | Datasheet                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| Juego de 3 brocas escalonadas 3-20 mm + centropunto  | [💸](https://s.click.aliexpress.com/e/_AalUrz)     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
| Broca escalonada de 8 pasos 10-45 mm    | [💸](https://s.click.aliexpress.com/e/_ATtnjt)     | [8_steps_10-45mm_incremental_drill_bit.pdf](/assets/pdf/8_steps_10-45mm_incremental_drill_bit.pdf)           |
