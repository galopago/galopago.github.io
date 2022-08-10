---
title: "Solar harvesting Wi-Fi camera"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - english
tags:
  - AN006
  - Solar
  - ESP32
header:
     teaser: "/assets/images/ENERGY_HARVESTING_CAMERA_TEASER.jpg"
---

An [ESP32-CAM](https://www.arducam.com/esp32-machine-vision-learning-guide/) module is a low-cost device based on ESP32-S module, an [OV2640](https://www.ourpcb.com/ov2640.html) image sensor and Micro SD slot. The module is not designed for low energy consumption, however, after some tweaks, the power consumption can be lowered to a level that is usable for short periods of time, powered by solar energy. The project presented here is a reasonably robust, dust-resistant and waterproof experimentation platform, using commercial off-the-shelf components. Ideal for outdoor usage.

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_MEDIUM.jpg"> </a>
	<figcaption>Solar harvesting Wi-Fi camera ready to be placed outside</figcaption>
</figure>

Key component: [ESP 32 CAM](https://s.click.aliexpress.com/e/_Dde4rkL)
{: .notice--danger}


<figure>
	<a href="/assets/images/solar_wificamera_wires.png"> <img src="/assets/images/solar_wificamera_wires.png"> </a>
	<figcaption>Simplified diagram</figcaption>
</figure>

##### Lowering power consumption

ESP32-CAM wasn't designed to be a low power device. Without modifications, deep sleep current measured was 2.8 mA, it leaves much to be desired.  

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_POWER.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_POWER_MEDIUM.jpg"> </a>
	<figcaption>Deep sleep current measurement without modifications </figcaption>
</figure>

Some [people on the Internet](https://brettbeeson.com.au/mini-battery-and-solar-powered-timelapse-camera/) already ventured in the following modifications:
* Removed 5 V to 3 V voltage regulator, the camera will be powered directly from a 3.2 V LiFePO4 battery.
* Break trace that powers the camera from 3.3 V and wire to [MOSFET Q2](https://github.com/SeeedDocument/forum_doc/blob/master/reg/ESP32_CAM_V1.6.pdf) who switches on 2.8 V and 1.2 V voltage regulators.
* Remove onboard led and wire GPIO33 to 5 V pin (this pin is already isolated after regulator removal) to use it externally.

These modifications lowered deep sleep current to 0.8 mA, which is scandalous for a low power device, however, is a substantial advance from the 2.8 mA without modifications.

<figure class="third">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_SWTICH.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_SWTICH_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_NOREGULATORLED.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_NOREGULATORLED_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_LOWPOWER.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_LOWPOWER_MEDIUM.jpg"> </a>
	<figcaption>Modifications and final result, Polyimide tape used to protect fine wire</figcaption>
</figure>

##### Bill of materials

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_PARTS.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_PARTS_MEDIUM.jpg"> </a>
	<figcaption>Parts usaded </figcaption>
</figure>

| Component        | Buy link | Datasheet                                   |
| ----------------- | ---------------- | ----------------------------------------------- |
| ESP32-CAM         | [buy it](https://s.click.aliexpress.com/e/_Dde4rkL) | [esp-32-cam.pdf](/assets/pdf/esp-32-cam.pdf) |
| Waterproof case for SJ4000 sport cam | [buy it](https://s.click.aliexpress.com/e/_DFtVPpl) | [sj-4000-sport-cam-waterproof-case.pdf](/assets/pdf/sj-4000-sport-cam-waterproof-case.pdf) |
| BQ25504 energy harvesting module |[buy it](https://s.click.aliexpress.com/e/_DDgPnXv)|[bq25504-energy-harvesting-module.pdf](/assets/pdf/bq25504-energy-harvesting-module.pdf)|
| 39.5x39.5 mm solar panel| [buy it](https://s.click.aliexpress.com/e/_DCzYmzh) | [solar-panel-39-5x39-5.pdf](/assets/pdf/solar-panel-39-5x39-5.pdf)|
| 30x25 mm solar panel |[buy it](https://s.click.aliexpress.com/e/_DFMaS0r)|[solar-panel-30x25.pdf](/assets/pdf/solar-panel-30x25.pdf)|
| 53x18 mm solar panel |[buy it](https://s.click.aliexpress.com/e/_DCbT3Mb)|[solar-panel-53x18.pdf](/assets/pdf/solar-panel-53x18.pdf)|
| 3.2V AAA 10440 LiFePO4 Battery  |[buy it](https://s.click.aliexpress.com/e/_DCA8kGr) |[lifepo4-3-2v-10440-rechargeable-battery-aaa.pdf](/assets/pdf/lifepo4-3-2v-10440-rechargeable-battery-aaa.pdf) |
| Micro SD Card|[buy it](https://s.click.aliexpress.com/e/_De2Jybl)|[micro-sd-card.pdf](/assets/pdf/micro-sd-card.pdf)|
| 1N5817 Diode Schottky |[buy it](https://s.click.aliexpress.com/e/_DewOC9v)|[1n5817.pdf](/assets/pdf/1n5817.pdf)|
| Single AAA battery clip for PCB |[buy it](https://s.click.aliexpress.com/e/_DmApqEj)|[bh-411.pdf](/assets/pdf/bh-411.pdf)|
| SMD 0603 resistor kit | [buy it](https://s.click.aliexpress.com/e/_DF6FuyR) | [4250-pcs-0603-smd-resistor-kit.pdf](/assets/pdf/4250-pcs-0603-smd-resistor-kit.pdf) |
| 2.54 mm female header|[buy it](https://s.click.aliexpress.com/e/_eNYVzN)|[FHA3-S1XX.pdf](/assets/pdf/FHA3-S1XX.pdf)|
| 2.54 mm male header|[buy it](https://s.click.aliexpress.com/e/_eMCUJv)|[PHA1-S3XX.pdf](/assets/pdf/PHA1-S3XX.pdf)|
| 2 pin jumper | [buy it](https://s.click.aliexpress.com/e/_DCCHLqX) | [pin-header-jumper-block.pdf](/assets/pdf/pin-header-jumper-block.pdf)|
| High temperature 30 AWG UL1423 PVDF wire| [buy it](https://s.click.aliexpress.com/e/_eMiimB) | [UL1423.pdf](/assets/pdf/UL1423.pdf) |
| Enamelled copper wire | [buy it](https://s.click.aliexpress.com/e/_DEHlzoj) | [repair-copper-enamelled-wire.pdf](/assets/pdf/repair-copper-enamelled-wire.pdf) |
| High temperature Polyimide insulation tape |[buy it](https://s.click.aliexpress.com/e/_Dkf4nOR)|[high-temperature-polyimide-insulation-tape.pdf](/assets/pdf/high-temperature-polyimide-insulation-tape.pdf)|

| Printed Circuit Board | Buy link | Source files repository  |
| --------------------------------- | ---------------- | ------------------------------- |
| ESP32-CAM prototyping board for sport cam enclosure | [buy it](https://www.pcbway.com/project/shareproject/ESP32_CAM_HOST_BOARD_THAT_FITS_INSIDE_WATERPROOF_SPORTSCAM_HOUSING_d06579a9.html) | [esp32cam-proto-sportcam](https://github.com/galopago/misistemote/tree/main/esp32cam-proto-sportcam) |

| Software | repository |
| ----------------------- | ---------------- |
| Sample Firmware takes photos and send them to a server using HTTP POST | [download it](https://github.com/galopago/esp32cam-upload) |
| Sample Golang server for image upload via HTTP POST | [download it](https://github.com/galopago/golang-upload-server) |

| Optional component | Buy link | Datasheet |
| ----------------------- | ---------------- | ------------------------------- |
| USB to TTL 3.3 V 5 V interface| [buy it](https://s.click.aliexpress.com/e/_Dc9HbCx) | [usb-ttl-converter-3-3v-5v.pdf](/assets/pdf/usb-ttl-converter-3-3v-5v.pdf) |
| Digital LCD Lux meter | [buy it](https://s.click.aliexpress.com/e/_DkDfxFp) | [digital-lcd-lux-meter.pdf](/assets/pdf/digital-lcd-lux-meter.pdf) |

##### Construccion de la plataforma

La plataforma consta de una carcasa a prueba de agua para una camara deportiva y una tarjeta de circuito impreso con las dimensiones adecuadas para ser ubicada adentro. 

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_PLATFORM.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_PLATFORM_MEDIUM.jpg"> </a>
	<figcaption>Componentes de la plataforma basica</figcaption>
</figure>

La carcasa usada es bastante comun, facil de conseguir y economica. Se abre y cierra sin necesidad de tornillos y posee un punto donde se le pueden agregar diferentes tipos de accesorios para ser montada. 

La tarjeta de circuito impreso fue diseñada para ubicar el modulo ESP32-CAM en la ventana que la carcasa dispone para la ubicacion del lente. El modulo puede ser montado en dos posiciones diferentes para maximizar el area dependiendo de los componentes a usar.

Se agrego un soporte para bateria AAA, conectores hembra para conectar/desconectar facilmente el modulo y pines en donde conectar el programador, pues esta tarjeta no cuenta con dicho circuito. Tambien se agrego un led a la tarjeta para depuracion.

<figure class="third">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDFRONT.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDFRONT_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDBACK.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDBACK_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_WITHMODULE.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_WITHMODULE_MEDIUM.jpg"> </a>
	<figcaption>Tarjeta con sus componentes</figcaption>
</figure>

##### Cosechador de energia

La camara obtiene energia de paneles solares que van instalados dentro de la carcasa, esto significa que el area de dichos paneles sera pequeña y se requerira maximizar su eficiencia. Para ello se uso un modulo de cosecha de energia basado en el integrado [BQ25504](https://www.lab4iot.com/2019/07/29/energy-harvesting-tutorial-with-the-ti-bq25570-part-1/). Este modulo eleva la tension de los paneles solares y es capaz de hacerlo con valores de voltaje tan bajos como 130 mV!. Por lo tanto, es capaz de producir corriente que sera almacenada en la bateria incluso si los paneles no reciben luz directa. 
<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_HARVESTER.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_HARVESTER_MEDIUM.jpg"> </a>
	<figcaption>Circuito cosechador de energia adherido mediante cinta doble faz</figcaption>
</figure>

Este modulo tambien realiza la funcion de cargador de bateria, pues se le configura un voltaje maximo de carga que nunca sera superado, ademas genera una señal en caso de bajo voltaje de bateria. La [configuracion de estos parametros](https://github.com/galopago/electronic-modules-helper/tree/main/cjmcu-25504) se hace mediante resistencias. El fabricante provee una [hoja de calculo](https://www.ti.com/product/BQ25504) para facilitar dicho trabajo.

Dado que la carcasa es transparente, es posible ubicar distintos paneles solares dentro de ella en diferentes sitios y conectarlos, ya sea en serie o paralelo. Probablemente, sea necesario poner [diodos de alta eficiencia al hacer dichas conexiones](https://www.dsisolar.com/info/pv-junction-box-s-bypass-diode-for-solar-panel-54221810.html), para no perder tanta potencia en caso de obtener sombras muy fuertes sobre alguno de los paneles.

Otra funcion importante del modulo cosechador es generar una señal de NIVEL DE VOLTAJE OK, para que la MCU pueda ser operada cuando todo esta bajo control, o para que, por el contrario, se mantenga en modo RESET en caso de que el nivel de la bateria sea demasiado bajo. 

<figure class="third">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_TWOPANELS.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_TWOPANELS_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDINSTALLED.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDINSTALLED_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BACKPANEL.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BACKPANEL_MEDIUM.jpg"> </a>
	<figcaption>Paneles y tarjeta instalados dentro. Usar un poco de espuma elastica para lograr el ajuste de las tarjetas</figcaption>
</figure>

##### Presupuesto energetico

Advertencia:¡Se simplificaran aqui muchos datos para poder dar un resultado de forma simple y rapida!
{: .notice--danger}

El ESP32 requiere aproximadamente 200 mA a 3.3 V para enviar datos via WiFi, esto se traduce en 0.66 W. Un panel solar de 40x40 mm que cabe dentro de la carcasa mencionada con anterioridad produce 65 mA a 2 V a pleno sol, esto se traduce en 0.13 W.  

Con los anteriores datos es evidente que es imposible usar el ESP32 en transmision WiFi continua con dicho panel, incluso a pleno sol. 

La solucion al anterior problema implica el uso de un elemento de almacenamiento de energia como una bateria y el uso del modulo ESP32 de forma intermitente, consumiendo la menor energia posible cuando se encuentre en modo sueño.

El modulo en sueño profundo consume aproximadamente 0.88 mA a 3.3 V lo que se traduce en 0.003 W. Asumiendo 12 horas de luz al dia, se requeririan 0.006 W promedio en el dia solo para mantener el modulo dormido. Si el conjunto panel/cosechador puede al menos entregar promedio en el dia el 4.6% de la potencia maxima del panel solar a pleno sol, ya se puede mantener alimentado el ESP32 en modo sueño profundo por un tiempo muy largo (hasta que se desgaste la bateria!)

Asumiendo 100.000 Lux como pleno sol y 100% de potencia del panel de 40x40 mm como 0.13 W, se estima que la iluminacion promedio que se requiere en un dia para que el ESP32 permanezca alimentado en modo sueño profundo seria de unos 4600 Lux.

##### Cuanta energia se requiere para tomar una fotografia y enviarla por internet

Al modulo ESP32, despues de despertar de sueño profundo le toma aproximadamente 4 segundos para tomar una fotografia, almacenarla en la tarjeta SD y enviarla por internet. Durante esos cuatro segundos la corriente exigida a la bateria es en promedio 200 mA a 3.3 V. La corriente que se debera acumular durante 12 horas para lograr tomar una foto sera:

Ciclo del ESP 32:  
200 mA x 4 S

se necesita:  
? mA x 12 H  
? ma x 12 (3600) S  
? ma x 43200 S  (redondeando a 40000 para facilitar los calculos)  

factor = 4 S / 40000 S = 0.0001  
200 mA * 0.0001 = 10 uA  

Se requiere acumular un promedio de 10 uA durante doce horas para tomar una fotografia y enviarla via WiFi. Lo cual es perfectamente posible en exteriores, incluso en dias nublados.

Hallando la relacion entre Lux y potencia para el panel de 40x40 mm y 0.13 W

100.000 Lux	=> 0.13 W  
0.77 Lux => 1 uW  

10uA * 3.3V = 33 uW

(0.77 Lux /uW ) 33 uW = 25.4 Lux (redondeando a 26 Lux)

Se requeriran 26 Lux de promedio al dia para tomar una fotografia y enviarla por WiFi

Por lo tanto, para tomar al menos una fotografia al dia y enviarla por WiFi se requerira un promedio diario de 4600 Lux + 26 Lux = 4626 Lux. ¡Para tomar y enviar dos fotografias al dia se requeriran 4652 Lux de promedio al dia y asi sucesivamente!.

En caso de usarse un panel mas pequeño como el que se encuentra en frente de la camara de 30x25 mm, cuya potencia es aproximadamente una cuarta parte del que esta instalado en la parte trasera, los requerimientos luminicos deberan ser de al menos cuatro veces mas.

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_PANELCOMPARE.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_PANELCOMPARE_MEDIUM.jpg"> </a>
	<figcaption>Comparacion entre panel solar trasero y delantero</figcaption>
</figure>

Para usar la camara con dicho panel se debera ubicarla en lugares con mucha iluminacion, especialmente luz directa.

##### Firmware y Software

Se presenta como ejemplo un firmware cuya funcion es la siguiente: tomar una fotografia y almacenarla en la memoria Micro SD, enviarla mediante WiFI haciendo una peticion HTTP POST multi-parte, luego de esto entrar en modo de sueño profundo por X tiempo  para luego despertar y repetir el proceso. El codigo puede ser usado para construir un firmware mucho mas robusto y flexible dependiendo de las necesidades individuales. 

Por el lado del servidor, se presenta una pequeña aplicacion escrita en Golang, cuya finalidad es eschuchar peticiones HTTP POST y recibir los datos de imagen enviados por el ESP32-CAM y guardarlos en una carpeta local. Esta aplicacion debera estarse ejecutando en un PC, o en un Raspberry Pi dentro de la misma red local del ESP32-CAM. Puesto que es un ejemplo basico y no cuenta con ningun tipo de autenticacion, no se recomienda para su uso en un servidor publico en internet.

Para programar el modulo, es necesario una interfaz USB a TTL serial,  pues este modulo no incorpora dicho chip. Tambien sera necesario poner el GPIO a GND durante la programacion. 

El GPIO33 ha sido liberado del led que usaba la tarjeta internamente y alambrado externamente, el firmware lo usa para depuracion, pero podria ser utilizado con otros fines como:

* ADC para determinar el voltaje de la bateria.
* Configurado como pin de RTC podria ser usado para despertar la tarjeta del sueño profundo, por ejemplo con un sensor PIR.
* Conectar un pulsador para realizar algun tipo de configuracion local sin requerir computador ni conectividad.

##### Resultados

La calidad de la imagen no es grandiosa, cosa que era de esperarse por el bajo precio del modulo. Jugando con los diferentes parametros de configuracion de la imagen podria mejorarse la calidad, dependiendo de las condiciones de iluminacion especificas. La imagen mostrada a continuacion ha sido almacenada de forma automatica via WiFi por el modulo, en un Raspberry Pi donde se ejectuaba la aplicacion de [servidor de carga de fotografias](https://github.com/galopago/golang-upload-server).

<figure class="half">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_TESTRIG.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_TESTRIG_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_TESTPIC.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_TESTPIC_MEDIUM.jpg"> </a>
	<figcaption>Montaje de prueba e imagen obtenida</figcaption>
</figure>

##### Posibles mejoras

Tanto el firmware, como el servidor para carga de fotografias, tienen como funcion servir de esqueleto para producir aplicaciones mas robustas, por lo tanto algunas cosas se han obviado, queda como tarea para el lector llevar a cabo algunas mejoras propuestas como:

* WiFi manager para poder cambiar los parametros de conexion sin requerir reconexion.
* Agregar algun tipo de autenticacion al enviar datos al servidor
* Poder cambiar parametros como el intervalo de sueño profundo, calidad de las fotografias, etc, desde el servidor en cada envio de fotografias.
* Implementar algun tipo de scheduler mediante el RTC, para que el modulo tome fotografias en fechas y horas especificas.
* Usar una mejor antena WiFI (externa al modulo pero ubicada dentro de la carcasa), y ponerla en un sitio con menos obstrucciones dentro de la carcasa, para ello hay que realizar algunos cambios en los componentes cercanos al conector U.FL 

