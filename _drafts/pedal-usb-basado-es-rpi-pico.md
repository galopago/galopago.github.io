---
title: "Pedal USB basado en Rpi Pico"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - espanol
tags:
  - AN002
  - RPI PICO
  - CIRCUITPYTHON
header:
     teaser: "/assets/images/USB_PEDAL_RPI_PICO_TEASER.jpg"
---

Pedal USB que emula la pulsacion de teclas o combinaciones de teclas mediante pedales u cualquier otro interruptor momentaneo. Util para usar con aplicaciones de edicion de video/audio para detener/reproducir sin tener que quitar las manos del teclado ni del raton, tambien puede usarse con aplicaciones de video conferencia para hacer mute rapidamente. No se requiere ninguna aplicacion especial para descargar el firmware inicial, ni tampoco para configurar las teclas (un simple editor de texto bastara). Funciona practicamente con cualquier sistema operativo, incluso con dispositivos Android usando un adaptador USB OTG.

<figure>
	<a href="/assets/images/USB_PEDAL_RPI_PICO.jpg"> <img src="/assets/images/USB_PEDAL_RPI_PICO_MEDIUM.jpg"> </a>
	<figcaption>Pedal USB instalado en una caja robusta</figcaption>
</figure>

Componente clave: [Rpi Pico.](https://s.click.aliexpress.com/e/_9yrTG7)
{: .notice--danger}


##### El concepto:

La gran mayoria de los pedales programables USB que se encuentran en el mercado poseen la gran desventaja de requerir inicialmente instalar una aplicacion para poder ser configurados. Esta plicacion solo existe para Windows y generalmente viene traducida a pocos idiomas(a veces no viene traducida!) y es poco intuitiva. Esto supone que para usuarios de Linux o Mac, se requiera instalar una maquina virtual para poder configurar dicho pedal, o pedir el favor a algun usuario de windows que nos ayude con esta tarea. 

Es aqui donde cobra importancia el [Raspberry Pi Pico](https://www.raspberrypi.org/products/raspberry-pi-pico/), por 2 grandes razones: Tiene interfaz nativa USB, por lo que no se requiere de programador ni hardware adicional para descargar los programas y la mas importante aun es que soporta [CircuitPython](https://learn.adafruit.com/bienvenido-a-circuitpython-2/que-es-circuitpython), por lo que se puede programar "en caliente" sin necesidad de estar permanentemente compilando y descargando firmware durante el proceso de depuracion.

Otra ventaja adicional con respecto a los pedales USB comerciales, es que en este caso el pedal en si, puede ser reemplazado facilmente por uno de mejor calidad o resistencia. Tambien podria usarse otro tipo de interruptores diferentes para ser actuados con partes del cuerto diferentes a los pies. La cantidad de interruptores que se le pueden adicionar solo esta determinada por los GPIO disponibles del Rpi Pico y por el tamaño de la caja!

En cuanto al montaje fisico, se utilizo el sistema de prototipado de hardware [TUSISTEMITA](https://github.com/galopago/TUSISTEMITA) que proporciona una serie de  modulos y elementos preconstruido que permiten realizar un proyecto electonico sin necesidad de soldaduras, haciendolo facilmente modificable y flexible, pero a la vez robusto. Todo el conjunto va dentro de una caja a prueba de agua IP65, la cual le proporciona resistencia al polvo y al agua, ademas de darle un aspecto estetico "industrial"  tambien le otorga suficiente robustez mecanica para soportar uno que otro abuso. Los cables de conexiones electricas externas de la caja, fueron complementadas con accesorios para garantizar
el sellamiento IP65.


#### Principales Caracteristicas:

* Desarrollado mediante CircuitPython, amigable y facil de entender
* Compatible con con los sistemas operativos mas conocidos
* No se requiere instalar ninguna aplicacion para descargar el Firmware inicial
* La configuracion de las teclas se realiza mediante la edicion de un archivo de texto
* Resistente al agua y golpes.
* Pedales reemplazables
* Montaje realizado mediante el sistema de prototipado robusto para hardware electronico TUSISTEMITA
* Alimentacion mediante puerto USB, no requiere fuente adicional.

El hardware es bastante simple,solo se requiere el Rpi Pico y los interruptores conectados cada uno a un GPIO y a tierra. Se usan las resistencias de pull-up internas. La alimentacion y los datos llegan por el conector USB


<figure>
	<a href="/assets/images/rpi_pico_usb_keyboard.png"> <img src="/assets/images/rpi_pico_usb_keyboard.png"> </a>
	<figcaption>Diagrama simplificado de bloques</figcaption>
</figure>


##### Que es CircuitPython?:
Dicho en palabras de Industrias Adafruit, creadores de CircuitPython: 
> es un lenguaje de programación diseñado para simplificar la experimentación y aprendizaje de programar en microcontroladoras de bajo costo. Hace el iniciar más sencillo que nunca sin necesidad previa de descargar herramientas a la estación de trabajo. Una vez que tu tarjeta ha sido preparada, abres cualquier editor de texto, y puedes comenzar a escribir código. Es así de simple.

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
| Tornillo M2.6 autorroscante tipo B | [💸] (https://s.click.aliexpress.com/e/_esHHyb) | [M2.6x5-6-8-12mm.pdf] (/assets/pdf/M2.6x5-6-8-12mm.pdf) |
| Espaciador separador de nylon G228 | [💸] (https://s.click.aliexpress.com/e/_AqHnWn) | [G228.pdf] (/assets/pdf/G228.pdf) |
| Tubo termoencogible 2:1 multiples colores| [💸] (https://s.click.aliexpress.com/e/_Ar4Zmf) | [2_1_heatshrink_tube_colors.pdf] (/assets/pdf/2_1_heatshrink_tube_colors.pdf) |
| Caja estanca generica resistente al agua de 115x90x55 mm | [💸] (https://s.click.aliexpress.com/e/_9y9UWZ) | [KH-F3.pdf] (/assets/pdf/KH-F3.pdf) |
| Raspberry Pi Pico | [💸] (https://s.click.aliexpress.com/e/_9yrTG7) | [pico-datasheet.pdf] (/assets/pdf/pico-datasheet.pdf) |
| Conector USB Tipo B IP68 para panel | [💸] (https://s.click.aliexpress.com/e/_ATARh0) | [USB_TYPE_B_PANEL_MOUNT_CONNECTOR.pdf] (/assets/pdf/USB_TYPE_B_PANEL_MOUNT_CONNECTOR.pdf) |
| Conector de aviacion 4 pines | [💸] (https://s.click.aliexpress.com/e/_9IMuVU) | [CIRCULAR_AVIATION_PANEL_CONNECTOR.pdf] (/assets/pdf/CIRCULAR_AVIATION_PANEL_CONNECTOR.pdf) |
| Interruptor momentaneo de pedal Metalico  | [💸] (https://s.click.aliexpress.com/e/_AktOC6) | [METAL_MOMENTARY_ELECTRIC_FOOT_SWITCH.pdf] (/assets/pdf/METAL_MOMENTARY_ELECTRIC_FOOT_SWITCH.pdf) |
| Cable de impresora USB tipo A | [💸] (https://s.click.aliexpress.com/e/_A596l4) | [USB_PRINTER_CABLE.pdf] (/assets/pdf/USB_PRINTER_CABLE.pdf) |
| Cable Micro USB | [💸] (https://s.click.aliexpress.com/e/_AF0DcI) | [MICRO_USB_CABLE.pdf] (/assets/pdf/MICRO_USB_CABLE.pdf) |

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
