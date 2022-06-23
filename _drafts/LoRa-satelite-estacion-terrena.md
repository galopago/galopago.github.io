---
title: "Estacion terrena para recepcion de satelites LoRa"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - espanol
tags:
  - AN005
  - LoRa
  - ESP32
header:
     teaser: "/assets/images/LORA_GROUND_STATION_TEASER.jpg"
---

Los satelites que en la actualidad usan tecnologia [LoRa](https://en.wikipedia.org/wiki/LoRa) han logrado que personas con pocos conocimientos tecnicos y con un bajo presupuesto puedan recibir sus señales, algo que era imposible hace algunos años. Gracias a la iniciativa [TinyGS](https://tinygs.com) se ha construido una red abierta de estaciones terrenas distribuidas por todo el mundo y que pueden ser construidas facilmente para ampliar dicha cobertura. El proyecto aqui presentado es una implementacion razonalmente robusta a prueba de polvo y agua, basada en componentes comerciales listos para usar. Ideal para montajes en exteriores.

<figure>
	<a href="/assets/images/LORA_GROUND_STATION.jpg"> <img src="/assets/images/LORA_GROUND_STATION_MEDIUM.jpg"> </a>
	<figcaption>Caja de las luces destapada mostrando sus componentes internos</figcaption>
</figure>

Componente clave: [Tira de LED WS2811 a prueba de agua.](https://s.click.aliexpress.com/e/_AFqDHl)
{: .notice--danger}


##### El concepto:

Con la llegada de los LED direccionables como el WS2812, WS2812b, WS2811, etc. fue posible controlar individualmente grandes
cantidades de leds usando un solo pin de microcontrolador!. Dicha facilidad de uso contribuyo a popularizar estos componentes
y a que estos se vendieran en diferentes presentaciones: leds individuales para montaje superficial, series de luces en tiras flexibles, extensiones
de luces tipo "arbol de navidad" a prueba de agua, entre otras. Es precisamente estas ultimas las que seran usadas en este proyecto dado lo facil que
pueden adaptarse a distintos tipos de proyectos como matrices de leds hasta adornos navideños, sin tener que soldar ni hacer modificaciones electricas a las luces.

Como microcontrolador se uso un ESP8266, mas precisamente una tarjeta conocida como "NODEMCU V3" que incorpora ya todos los elementos adicionales para poder
realizar la programacion inicial desde un computador. Utilizando el WiFi incorporado del ESP8266, no solo es posible controlar las secuencias y colores de las luces desde
internet, sino que tambien es posible descargarle nuevos programas de forma remota (OTA) usando un combo poderoso: El sistema operativo [Mongoose OS](https://mongoose-os.com/) junto con
plataforma para gestion remota de dispositivos [mDASH](https://mdash.net/). Mongoose OS usa una version restringida de JavaScript conocida como [mJS](https://github.com/cesanta/mjs), lo que probablemente
resultara atractivo para programadores web que ya trabajan con este tipo de tecnologia. Mongoose OS esta construido sobre el ESP-IDF de Espressif, por lo tanto
pueden hacerse llamados a funciones escritas en C, lo que sin duda tambien resultara atractivo para programadores de microcontroladores "tradicionales" que han
trabajado con este lenguaje bastante maduro.

En cuanto al montaje fisico, se utilizo el sistema de prototipado de hardware [TUSISTEMITA](https://github.com/galopago/TUSISTEMITA) que proporciona una serie de  modulos y elementos preconstruido que
permiten realizar un proyecto electonico sin necesidad de soldaduras, haciendolo facilmente modificable y flexible, pero a la vez robusto. Todo el conjunto va
dentro de una caja a prueba de agua IP65, la cual le proporciona resistencia al polvo y al agua, ademas de darle un aspecto estetico "industrial"  tambien le otorga suficiente
robustez mecanica para soportar uno que otro abuso. Los cables de conexiones electricas externas de la caja, fueron complementadas con accesorios para garantizar
el sellamiento IP65.


#### Principales Caracteristicas:
* Sistema Operativo embebido Mongoose OS corriendo sobre ESP8266
* Resistente al agua y con pestaña para montaje en pared.
* Actualizacion remota del Firmware gracias a la plataforma de gestion Mongoose OS dashboard mDASH
* Montaje realizado mediante el sistema de prototipado robusto para hardware electronico TUSISTEMITA
* Alimentacion 110/220V AC.


El hardware esta compuesto por 4 elementos bien diferenciados: Fuente de alimentacion, CPU, adaptador de nivel logico y LEDS. La fuente de alimentacion es de
tipo comutada con 20W de potencia, 5 voltios de salida y entrada de 110V a 220V, por lo tanto puede ser usada practicamente en cualquier lugar del mundo. Como CPU
se uso un ESP8266 en una tarjeta NODEMCU V3. Esta tarjeta puede ser alimentada a 3.3V directamente al pin de alimentacion del procesador, o por 5V haciendo uso del regulador incorporado.
Las salidas logicas de la CPU tendran voltajes de 0 a 3.3V, lo que debera ser tenido en cuenta si se desea instalar sensores u otros perifericos que trabajen
a 5V. Es aqui donde entre cobra importancia el adaptador de nivel logico, pues los leds son alimentados a 5V y esperan una señal logica con esta misma amplitud. Como adaptador
de nivel logico se uso la tarjeta TUSISTEMITA D06 que internamente usa un MOSFET BSS138 para realizar dicho trabajo. 

<figure>
	<a href="/assets/images/mos_wifi_iot_lights_blockdiag.png"> <img src="/assets/images/mos_wifi_iot_lights_blockdiag.png"> </a>
	<figcaption>Diagrama simplificado de bloques</figcaption>
</figure>


La fuente de poder entrega aproximadamente 3.8 A y cada led WS2811 consume 60 mA como maximo, estando en capacidad de alimentar extensiones de hasta 63 leds. Para
tener cierto margen se ha decidido usar extensiones de maximo 50 leds. Cualquier tipo de tira de LED que use el mismo protocolo del WS2811 puede ser usada.

##### Que es Mongoose OS?:
Mongoose OS es un sistema operativo para Internet De las Cosas, compatible con ESP8266, ESP32 entre otros. Combina facilidad con robustez. Es ideal para
el prototipado rapido de productos IoT, pues trae incorporada la conectividad nativa con "nubes" publicas o privadas como AWS, Google, Azure, etc.
Hay dos caracteristicas muy importantes que lo hacen tan versatil. Una de ella es la posibilidad de usarlo "remoto/local". Remoto, que es la opcion por defecto, la compilacion
se realiza en la nube lo cual evita los problemas clasicos de instalacion de los SDK para desarrollo embebido. 
Tambien existe la posibilidad de instalarlo localmente mediante dockers, en cuyo caso se puede compilar sin tener una conexion a internet.

La otra caracteristica importante, es que usa como lenguaje de programacion un subconjuto de JavaScript llamado mJS (embedded javascript). Esto hace que se 
puedan crear muchas funcionalidades avanzadas, sin necesidad de escribir tanto codigo como en otros lenguajes usados en sistemas embebidos (Assembler, C, Processing). Sin embargo
nada impide que se puedan llamar funciones escritas en C puro para ganar desempeño, en especial al escribir controladores para sensores y perifericos que
requieren un manejo eficiente de los recursos.

##### El programa:

El firmware presentado en este proyecto realiza dos tareas: Encender cada uno de los leds con un color determinado y la otra se encarga de recibir datos
desde la nube.

Para enviar el dato de color a cada uno de los LED , este se extrae aleatoriamente de una tabla de colores predefinida. La comunicacion con los LED se realiza
mediante la biblioteca NEOPIXEL que incorpora Mongoose OS.

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

| Componente         | Consigue el tuyo! | Hoja de caracteristicas                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| Juego de 3 brocas escalonadas 3-20 mm + centropunto  | [💸](https://s.click.aliexpress.com/e/_AalUrz)     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
| Broca escalonada de 8 pasos 10-45 mm    | [💸](https://s.click.aliexpress.com/e/_ATtnjt)     | [8_steps_10-45mm_incremental_drill_bit.pdf](/assets/pdf/8_steps_10-45mm_incremental_drill_bit.pdf)           |
