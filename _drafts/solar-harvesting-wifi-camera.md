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
	<figcaption>Parts used </figcaption>
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

##### Assembly

The basic platform consists of a waterproof enclosure for sport cam and a printed circuit board with the appropriate size to fit inside.

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_PLATFORM.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_PLATFORM_MEDIUM.jpg"> </a>
	<figcaption>Basic platform components</figcaption>
</figure>

The proposed enclosure is pretty common, easy to find and inexpensive. Opens and closes without screws and has a mounting point where different mounting accessories can be installed.

The printed circuit board was designed to place ESP32-CAM near the window where the camera lens was to be located. The module can be positioned in two different orientations to maximize area, depending on the selected components.

AAA battery clip added, female connectors to plug/unplug module easily and header pins for programming, because the board does not have such circuitry. Also, a red LED for debugging purposes was added.

<figure class="third">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDFRONT.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDFRONT_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDBACK.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDBACK_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_WITHMODULE.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_WITHMODULE_MEDIUM.jpg"> </a>
	<figcaption>Board with all components</figcaption>
</figure>

##### Energy harvester

The camera gets its energy from solar panels installed inside the enclosure, which means that the area available is small, so a way to maximize its efficiency is needed. A harvesting module based on [BQ25504](https://www.lab4iot.com/2019/07/29/energy-harvesting-tutorial-with-the-ti-bq25570-part-1/) chip was used. This device boosts solar panel voltage and is able to do that with voltages down to 130 mV!, is therefore able to supply current for storage in the battery, even without direct light hitting the panel.

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_HARVESTER.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_HARVESTER_MEDIUM.jpg"> </a>
	<figcaption>Energy harvesting module attached with double sided-tape</figcaption>
</figure>

The module also works as a battery charger with over voltage and under voltage protection. In order to [set voltage values](https://github.com/galopago/electronic-modules-helper/tree/main/cjmcu-25504), some resistors must be modified. The module's manufacturer provides a [spreadsheet](https://www.ti.com/product/BQ25504) to make the process easier.

Because the enclosure is transparent, it is possible to put a few solar panels in various places inside, and wire them in parallel or series. Maybe some [diodes](https://www.electronics-tutorials.ws/diode/bypass-diodes.html) will be required to not lose a lot of efficiency when some panels are shaded.

Another important function of the energy harvesting module is the ability to output a VOLTAGE OK SIGNAL, so the MCU could be kept in reset state when the battery voltage is too low to operate. 

<figure class="third">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_TWOPANELS.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_TWOPANELS_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDINSTALLED.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDINSTALLED_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BACKPANEL.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BACKPANEL_MEDIUM.jpg"> </a>
	<figcaption>Solar panels and board installed in the interior. Use a piece of EVA foam to keep things in place</figcaption>
</figure>

##### Energy budget

Warning: Some data and procedures will be simplified to yield simpler and faster results!
{: .notice--danger}

ESP32 draws about 200 mA at 3.3 V to send data over Wi-Fi, which is equivalent to 0.66 W. A 40x40 mm solar panel that fits inside the aforementioned enclosure yields around 65 mA at 2 V at full sun, which is equivalent to 0.13 W.

With this data, it is clear that it is not possible to use ESP32 sending data over Wi-Fi continuously with that panel, even in full sunlight.

To deal with this problem, two things are needed: a storage element, and the use of the ESP32 module in non continuous (duty cycled) mode.

The module in deep sleep mode draws about 0.88 mA at 3.3 V, which is equivalent to 0.003 W. Assuming 12 hours of daylight, it will take an average of 0.006 W average per day, just to keep the module energized up in sleep mode. If the pair panel/harvester can yield an average of 4.6% of the maximum power of the solar panel at full sun, it is enough to keep energized the ESP32 in deep sleep mode for a very long time (until battery degradation!).

Assuming 100.000 Lux as a full sun and 100% of the 40x40 mm solar panel power as 0.13 W, it is estimated that the average irradiance required per day to keep the ESP32 energized in deep sleep is around 4600 Lux. 

##### How much energy is required to take a picture and upload it over the internet?

After waking up from a deep sleep, it takes about 4 seconds for the ESP32 to take a picture, store it in the SD card, and bring it online. The average power consumption of these 4 seconds is 200 mA at 3.3 V. The current to be accumulated for 12 hours to is:

ESP 32 Cycle:  
200 mA x 4 S

It is needed:  
? mA x 12 H  
? ma x 12 (3600) S  
? ma x 43200 S  (Approximating to 40000 to make calculations easier)  

factor = 4 S / 40000 S = 0.0001  
200 mA * 0.0001 = 10 uA  

It is required an average of 10 uA for 12 hours to take a picture and send it to a server, which is perfectly feasible in the outdoors, even on cloudy days.

Finding the relation between Lux and output power of the 40x40 mm and 0.13 W solar panel.

100.000 Lux	=> 0.13 W  
0.77 Lux => 1 uW  

10uA * 3.3V = 33 uW

(0.77 Lux /uW ) 33 uW = 25.4 Lux (Approximating to 26 Lux)

It will take an average of 26 Lux per day to take a photo and send it over Wi-Fi

In short, to take at least one photo a day and send it over Wi-Fi, it will take a daily average of 4600 Lux + 26 Lux = 4626 Lux. For two pictures a day it will take a daily average of 4652 Lux, and so on.

If a smaller panel is used, such as the 30x25 mm in the front of the camera, whose power is about a quarter of that installed on the back, the irradiance should be 4 times stronger.


<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_PANELCOMPARE.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_PANELCOMPARE_MEDIUM.jpg"> </a>
	<figcaption>Solar panel in the front vs. solar panel in the back</figcaption>
</figure>

To use the camera with such a small panel, a lot of light is required, especially direct light.

##### Firmware and Software

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

