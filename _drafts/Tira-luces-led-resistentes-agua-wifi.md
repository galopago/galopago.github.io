---
title: "Tira de luces LED resistentes al agua controladas por WiFi"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - espanol
tags:
  - AN001
  - WiFi
  - MONGOOSE OS
header:
     teaser: "/assets/images/MOS_WIFI_IOT_LIGHTS_TEASER.jpg"
---

Luces apropiadas para decoraciones navideñas, halloween,etc. No solamente la secuencia puede ser manejadas por internet, sino que
tambien se pueden reprogramar completamente de forma inalambrica (OTA) mediante una conexion WiFi. Construccion robusta 
a prueba de polvo y agua. Ideal para montajes en interiores: como fondo para transmisiones de youtubers/streamers 
(manejadas en tiempo real por su audiencia),exteriores fijos como muros y avisos, o en exteriores moviles como carrozas de carnaval.

<figure>
	<a href="/assets/images/MOS_WIFI_IOT_LIGHTS.jpg"> <img src="/assets/images/MOS_WIFI_IOT_LIGHTS_MEDIUM.jpg"> </a>
	<figcaption>Caja de las luces destapada mostrando sus componentes internos</figcaption>
</figure>

Componente clave: [Tira de LED WS2811 a prueba de agua.](https://s.click.aliexpress.com/e/_AFqDHl)
{: .notice--danger}


Con la llegada de los LED direccionables como el WS2812, WS2812b, WS2811, etc. fue posible controlar individualmente grandes
cantidades de leds usando un solo pin de microcontrolador!. Esto contribuyo a que fuera cada vez mas facil encontrar estos dispositivos
y a que estos se vendieran en diferentes presentaciones: leds individuales para montaje superficial, series de luces en tiras flexibles, extensiones
de luces tipo "arbol de navidad" a prueba de agua, entre otras. Es precisamente estas ultimas las que seran usadas en este proyecto dado lo facil que
pueden adaptarse a distintos tipos de proyectos como matrices de leds hasta adornos navideños, sin tener que soldar ni hacer modificaciones electricas a las luces.

Como microcontrolador se uso un ESP8266, mas precisamente una tarjeta conocida como "NODE-MCU V" que incorpora ya todos los elementos adicionales para porder
realizar la programacion inicial desde un computador. Utilizando en WiFi incorporado del ESP, no solo es posible controlar las secuencias y colores de las luces desde
internet, sino que tambien es posible descargarle nuevos programas de forma remota (OTA) usando un combo poderoso: El sistema operativo Mongoose OS junto con
plataforma para gestion remota de dispositivos mDASH. Mongoose OS usa una version restringida de JavaScript conocida como mJS, lo que probablemente
resultara atractivo para programadores web que ya trabajan con este tipo de tecnologia. Mongoose OS esta construido por el ESP-IDF de Espressif, por lo tanto
pueden hacerse llamados a funciones escritas en C, lo que sin duda tambien resultara atractivo para programadores de microcontroladores "tradicionales" que han
trabajado con este lenguaje bastante maduro.

En cuanto al montaje fisico, se utilizo el sistema de prototipado de hardware TUSISTEMITA que proporciona una serie de  modulos y elementos preconstruido que
permiten realizar un proyecto electonico sin necesidad de soldaduras, haciendolo facilmente modificable y flexible, pero a la vez robusto. Todo el conjunto va
dentro de una caja a prueba de agua IP65, la cual le proporciona resistencia al polvo y al agua, ademas de darle no solo un aspecto estetico "industrial"  sino suficiente
entereza mecanica para soportar uno que otro abuso. Los cables de conexiones electricas externas de la caja, fueron complementadas con accesorios para garantizar
el sellamiento IP65.


#### Principales Caracteristicas:
* Sistema Operativo embebido [Mongoose OS](https://mongoose-os.com/) corriendo sobre ESP8266
* Resistente al agua y montable en pared.
* Actualizacion remota del Firmware gracias a la plataforma de gestion Mongoose OS [Dashboard](https://mdash.net/)
* Montaje realizado mediante el sistema de prototipado robusto para hardware electronico [TUSISTEMITA](https://github.com/galopago/TUSISTEMITA)
* Alimentacion 110/220V AC.

El hardware esta compuesto por 4 elementos bien diferenciados: Fuente de alimentacion, CPU, adaptador de nivel logico y LEDS. La fuente de alimentacion es de
tipo comutada con 20W de potencia, 5 voltios de salida y entrada de 110V a 220V, por lo tanto puede ser usada practicamente en cualquier lugar del mundo. Como CPU
se uso un ESP8266 en una tarjeta NODE MCU V3. Esta tarjeta puede ser alimentada a 3.3V directamente el procesador, o por 5V haciendo uso del regulador incorporado.
Las salidas logicas de la CPU tendran entonces voltages de 0 a 3.3V, lo que debera ser tenido en cuenta si se desean instalar sensores u otros perifericos que trabajen
a 5V. Es aqui donde entre cobra importancia el adaptador de nivel logico, pues los leds son alimentados a 5V y esperan una señal logica con esta misma amplitud. Como adaptador
de nivel logico se uso la tarjeta TUSISTEMITA D06 que internamente usa un MOSFET BSS138 para realizar dicho trabajo. 

<figure>
	<a href="/assets/images/mos_wifi_iot_lights_blockdiag.png"> <img src="/assets/images/mos_wifi_iot_lights_blockdiag.png"> </a>
	<figcaption>Diagrama simplificado de bloques</figcaption>
</figure>


La fuente de poder entrega aproximadamente 3.8 A y cada led WS2811 consume 60 mA como maximo, estando en capacidad de alimentar extensiones de hasta 63 leds. para
tener cierto margen se ha decidido usar extensiones de maximo 50 leds. Cualquier tipo de extension de LED que use el mismo protocolo del WS2811 puede ser usada.

Mongoose OS es un sistema operativo para Internet De las Cosas que es compatible con ESP8266, ESP32 entre otros. Combina facilidad con robustez. Es ideal para
el prototipado rapido de productos IoT, pues tiene incorporada la conectividad con "nubes" publicas o privadas como AWS,Google, Azure, etc de forma nativa.Hay
dos caracteristicas muy importantes que lo hacen tan versatil. Una de ella es la posibilidad de usarlo "online", que es la instalacion default, donde la compilacion
se realiza en la nube, por lo que se evita los problemas clasicos de instalacion de los SDK para desarrollo embebido, en general cuando se migra de un sistema operativo a 
a otro. Tambien existe la posibilidad de instalarlo localmente mediante dockers, en cuyo caso se puede trabajar en desarrollo sin tener una conexion a internet.

La otra caracteristica importante es que usa como lenguaje de programacion un subconjuto de JavaScript llamado mJS (embedded javascript). Esto hace que se 
puedan crear muchas funcionalidades, sin necesidad de escribir tanto codigo como en otros lenguaes usados en sistemas embebidos (Assembler, C, Processing). Sinembargo
nada impide que se puedan llamar funciones escritas en C puro para ganar desempeño, en especial al escribir controladores para sensores y perifericos que
requieren un manejo eficiente de los recursos.

El programa presentado en este proyecto realiza dos tareas: Encender cada uno de los leds con un color determinado y la otra es pendiente de recibir datos
desde la nube.

Se envia un dato de color a cada uno de los LED , este dato se extrae aleatoriamente de una tabla de colores predefinida. la comunicacion con los LED se realiza
mediante la biblioteca NEOPIXEL que incorpora mongoose os.

Otra tarea se encarga de realizar una conexion MQTT a un broker y escuchar por un topico especifico. Una aplicacion cliente puede conectarse a estre broker MQTT
y enviar un determinado dato al topico que se esta escuchando, y con esto se puede cambiar la paleta de colores que se esta usando para los LED. De esta forma
se presenta una aplicacion de ejemplo muy simple de como modificar la secuencia de forma remota a traves de internet. 

El prototipo del sistema fue montado usando varios componentes e TUSISTEMITA, como el bastidor, las tarjetas adaptadoras para la fuente y NODE MCU, tarjeta de 
niveles logicos y borneras para conexion de salida. Una vez descargada la aplicacion por primera vez y comprobado que las conexiones electricas funcionan bien,
se puede pasar a la caja para montaje definitivo sin ningun traumatismo. Solamente hay que desconectar la alimentacion electrica de las borneras y la conexion
de salida a los leds.

<figure class="third">
	<a href="/assets/images/MOS_WIFI_LIGHTS_PARTS.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_PARTS_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_WIRED.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_WIRED_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_WORKING.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_WORKING_MEDIUM.jpg"> </a>
	<figcaption>Nodo LoRa interruptor magnetico.</figcaption>
</figure>

Se recomienda cambiar los conectores originales de las tiras de led, por unos mucho mas robustos y a prueba de agua para evitar problemas de oxido en caso
de estar expuesto a los elementos ambientales. Se recomienda el uso de termoencogible con pegamento para mayor proteccion en las uniones entre los cables
de la tira led y los conectores.

<figure class="third">
	<a href="/assets/images/MOS_WIFI_LIGHTS_CABLEGLAND.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_CABLEGLAND_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_CONNECTOR.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_CONNECTOR_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_FINISHED.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_FINISHED_MEDIUM.jpg"> </a>
	<figcaption>Nodo LoRa interruptor magnetico.</figcaption>
</figure>

Una vez la caja se encuentra cerrada, las actualizaciones a la aplicacion se pueden hacer inalambricamente mediante OTA por medio del dashboard de mongoose
os mDash. 

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
| Doble fondo A02 para caja de 200x120x75mm | [A02](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)           |
| Doble fondo A05 con agujeros espaciados 10.16mm para fuente 5V 3.8A   | [A05](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)        |
| Tarjeta B01 de terminales de tornillos 2x4 3.5mm | [B01](https://github.com/galopago/TUSISTEMITA/tree/master/B_SCREW_TERMINAL_WIRE_CONNECTORS)        |
| Tarjeta breakout C08 con salida a borneras para NODEMCU V3  | [C08](https://github.com/galopago/TUSISTEMITA/tree/master/C_BREAKOUTS)        |
| Tarjeta D06 de cambio de niveles logicos  | [D06](https://github.com/galopago/TUSISTEMITA/tree/master/D_ELECTRONICS)        |


#### Software

| Software    | Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Firmware    | [MOS_IOT_ADDRESSABLE_LEDS](https://github.com/galopago/MOS_IOT_ADDRESSABLE_LEDS)           |

 

## Componentes opcionales:

| Component         | Get yours! | Datasheet                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| Juego de 3 brocas escalonadas 3-20 mm + centropunto  | [💸](https://s.click.aliexpress.com/e/_AalUrz)     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
| Broca escalonada de 8 pasos 10-45 mm    | [💸](https://s.click.aliexpress.com/e/_ATtnjt)     | [8_steps_10-45mm_incremental_drill_bit.pdf](/assets/pdf/8_steps_10-45mm_incremental_drill_bit.pdf)           |
