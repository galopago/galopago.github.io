---
title: "Sensor Wi-Fi sin soldar y sin programar*"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - espanol
tags:
  - AN008
  - ESP32
  - Prototipado
header:
     teaser: "/assets/images/AN008/WIFI_SENSOR_LOWCODE_TEASER.jpg"
---

Las plataformas para desarrollo de software no-code/low-code permiten crear aplicaciones escribiendo muy poco codigo y en algunos casos, ningun codigo, de forma tal que reducen el tiempo de desarrollo para poner en produccion aplicaciones en muy poco tiempo. Este proyecto combina dos ideas: plataforma de software no-code/low-code, con un sistema de prototipado rapido y robusto que no requiere soldar!. De esta forma en un par de horas se puede pasar de una idea, a un dispositivo operando en condiones reales.

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_MEDIUM.jpg"> </a>
	<figcaption>Sensor Wi-Fi desarrollado mediante herramientas de prototipado rapido de HW y SW en operacion en condiciones reales</figcaption>
</figure>

Componente clave: [ESP 32 D1 MINI](https://s.click.aliexpress.com/e/_DlJju2n)
{: .notice--danger}


### Prototipado rapido robusto hardware-software

Se realizara una aplicacion de ejemplo: un termometro WiFi basado en ESP32, sensor de temperatura DS18B20, e indicador local. Todo esto dentro de una caja a prueba de agua para montaje en pared. Lo anterior se realizara mediante los siguientes proyectos:

* HARDWARE: Sistema de prototipado rapido robusto, [MISISTEMITA](https://github.com/galopago/misistemita)

* SOFTWARE: Se realizaran pruebas tanto con [TASMOTA](https://tasmota.github.io) como con [ESPHome](https://esphome.io).


##### Listado de materiales

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTS.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTS_MEDIUM.jpg"> </a>
	<figcaption>Partes usadas en la construccion</figcaption>
</figure>

##### Partes discretas necesarias

| Componente        | Enlace de compra | Hoja de datos                                   |
| ----------------- | ---------------- | ----------------------------------------------- |
| ESP32 D1 MINI     | [compralo aqui](https://s.click.aliexpress.com/e/_DlJju2n) | [esp32-d1-mini.pdf](/assets/pdf/esp32-d1-mini.pdf) |
| Pantalla OLED 0.96 I2C | [compralo aqui](https://s.click.aliexpress.com/e/_DBmZwu3) | [096-i2c-oled-display.pdf](/assets/pdf/096-i2c-oled-display.pdf) |
| Sensor de temperatura DS18B20 a prueba de agua |[compralo aqui](https://s.click.aliexpress.com/e/_DCzX5Mn)|[ds18b20-waterproof.pdf](/assets/pdf/ds18b20-waterproof.pdf)|
| Caja generica a prueba de agua “Sonoff” 100x68x50mm | [compralo aqui](https://s.click.aliexpress.com/e/_AtukwZ) | [SONOFF-IP66-waterproof-case.pdf](/assets/pdf/SONOFF-IP66-waterproof-case.pdf)|

##### Componentes necesarios para los modulos misistemita requeridos

| Componente        | Enlace de compra | Hoja de datos                                   |
| ----------------- | ---------------- | ----------------------------------------------- |
| Espaciador separador de nylon de bloqueo inverso |[compralo aqui](https://s.click.aliexpress.com/e/_DCFVOtz)|[G228.pdf](/assets/pdf/G228.pdf)|
| Tornillo M2.6 autorroscante tipo B |[compralo aqui](https://s.click.aliexpress.com/e/_esHHyb)|[M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf)|
| Terminal de tornillo para PCB kf350 3.5mm 2 y 3 pines |[compralo aqui](https://s.click.aliexpress.com/e/_eLjzKB)|[KF350.pdf](/assets/pdf/KF350.pdf)|
| Conector tipo header hembra 2.54mm |[compralo aqui](https://s.click.aliexpress.com/e/_eNYVzN)|[FHA3-S1XX.pdf](/assets/pdf/FHA3-S1XX.pdf)|


##### Tarjetas de circuito impreso necesarias para los modulos misistemita requeridos

| Tarjeta de circuito impreso (PCB) | Enlace de compra | Repositorio con archivos fuente  |
| --------------------------------- | ---------------- | ------------------------------- |
| Bastidor para caja generica a prueba de agua de 100 x 68 x 52 mm  | [compralo aqui](https://www.pcbway.com/project/shareproject/ESP32_CAM_HOST_BOARD_THAT_FITS_INSIDE_WATERPROOF_SPORTSCAM_HOUSING_d06579a9.html) | [a06 backplate](https://github.com/galopago/misistemita/tree/main/a-backplates/a06) |
| Bornera de conexiones 2x7 de terminal de tornillo 3.5mm  | [compralo aqui](https://www.pcbway.com/project/shareproject/ESP32_CAM_HOST_BOARD_THAT_FITS_INSIDE_WATERPROOF_SPORTSCAM_HOUSING_d06579a9.html) | [b02 Bornera de conexiones](https://github.com/galopago/misistemita/tree/main/b-screw-terminal-wire-connectors/b02) |
| Tarjeta breakout para ESP32 D1 MINI de terminales de tornillo 3.5mm  | [compralo aqui](https://www.pcbway.com/project/shareproject/ESP32_CAM_HOST_BOARD_THAT_FITS_INSIDE_WATERPROOF_SPORTSCAM_HOUSING_d06579a9.html) | [c12 Breakout](https://github.com/galopago/misistemita/tree/main/c-breakouts/c12) |
| Tarjeta breakout para pantalla I2C de terminales de tornillo 3.5mm | [compralo aqui](https://www.pcbway.com/project/shareproject/ESP32_CAM_HOST_BOARD_THAT_FITS_INSIDE_WATERPROOF_SPORTSCAM_HOUSING_d06579a9.html) | [c10 Breakout](https://github.com/galopago/misistemita/tree/main/c-breakouts/c10) |


| Software | repositorio |
| ----------------------- | ---------------- |
| ESPHome | [descargalo aqui](https://esphome.io/) |
| TASMOTA | [descargalo aqui](https://tasmota.github.io/docs/) |

##### Construccion de la plataforma

La plataforma consta de una carcasa a prueba de agua para una camara deportiva y una tarjeta de circuito impreso con las dimensiones adecuadas para ser ubicada adentro. 

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_PARTS.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_PARTS_MEDIUM.jpg"> </a>
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

El ESP32 requiere aproximadamente 200 mA a 3.3 V para enviar datos via Wi-Fi, esto se traduce en 0.66 W. Un panel solar de 40x40 mm que cabe dentro de la carcasa mencionada con anterioridad produce 65 mA a 2 V a pleno sol, esto se traduce en 0.13 W.  

Con los anteriores datos es evidente que es imposible usar el ESP32 en transmision Wi-Fi continua con dicho panel, incluso a pleno sol. 

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
? ma x 43200 S  (aproximando a 40000 para facilitar los calculos)  

factor = 4 S / 40000 S = 0.0001  
200 mA * 0.0001 = 10 uA  

Se requiere acumular un promedio de 10 uA durante doce horas para tomar una fotografia y enviarla via Wi-Fi. Lo cual es perfectamente posible en exteriores, incluso en dias nublados.

Hallando la relacion entre Lux y potencia para el panel de 40x40 mm y 0.13 W

100.000 Lux	=> 0.13 W  
0.77 Lux => 1 uW  

10uA * 3.3V = 33 uW

(0.77 Lux /uW ) 33 uW = 25.4 Lux (aproximando a 26 Lux)

Se requeriran 26 Lux de promedio al dia para tomar una fotografia y enviarla por Wi-Fi

Por lo tanto, para tomar al menos una fotografia al dia y enviarla por Wi-Fi se requerira un promedio diario de 4600 Lux + 26 Lux = 4626 Lux. ¡Para tomar y enviar dos fotografias al dia se requeriran 4652 Lux de promedio al dia y asi sucesivamente!.

En caso de usarse un panel mas pequeño como el que se encuentra en frente de la camara de 30x25 mm, cuya potencia es aproximadamente una cuarta parte del que esta instalado en la parte trasera, los requerimientos luminicos deberan ser de al menos cuatro veces mas.

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_PANELCOMPARE.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_PANELCOMPARE_MEDIUM.jpg"> </a>
	<figcaption>Comparacion entre panel solar trasero y delantero</figcaption>
</figure>

Para usar la camara con dicho panel se debera ubicarla en lugares con mucha iluminacion, especialmente luz directa.

##### Firmware y Software

Se presenta como ejemplo un firmware cuya funcion es la siguiente: tomar una fotografia y almacenarla en la memoria Micro SD, enviarla mediante Wi-Fi haciendo una peticion HTTP POST multi-parte, luego de esto entrar en modo de sueño profundo por X tiempo  para luego despertar y repetir el proceso. El codigo puede ser usado para construir un firmware mucho mas robusto y flexible dependiendo de las necesidades individuales. 

Por el lado del servidor, se presenta una pequeña aplicacion escrita en Golang, cuya finalidad es eschuchar peticiones HTTP POST y recibir los datos de imagen enviados por el ESP32-CAM y guardarlos en una carpeta local. Esta aplicacion debera estarse ejecutando en un PC, o en un Raspberry Pi dentro de la misma red local del ESP32-CAM. Puesto que es un ejemplo basico y no cuenta con ningun tipo de autenticacion, no se recomienda para su uso en un servidor publico en internet.

Para programar el modulo, es necesario una interfaz USB a TTL serial,  pues este modulo no incorpora dicho chip. Tambien sera necesario poner el GPIO0 a GND durante la programacion. 

El GPIO33 ha sido liberado del led que usaba la tarjeta internamente y alambrado externamente, el firmware lo usa para depuracion, pero podria ser utilizado con otros fines como:

* ADC para determinar el voltaje de la bateria.
* Configurado como pin de RTC podria ser usado para despertar la tarjeta del sueño profundo, por ejemplo con un sensor PIR.
* Conectar un pulsador para realizar algun tipo de configuracion local sin requerir computador ni conectividad.

##### Resultados

La calidad de la imagen no es grandiosa, cosa que era de esperarse por el bajo precio del modulo. Jugando con los diferentes parametros de configuracion de la imagen podria mejorarse la calidad, dependiendo de las condiciones de iluminacion especificas. La imagen mostrada a continuacion ha sido almacenada de forma automatica via Wi-Fi por el modulo, en un Raspberry Pi donde se ejectuaba la aplicacion de [servidor de carga de fotografias](https://github.com/galopago/golang-upload-server).

<figure class="half">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_TESTRIG.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_TESTRIG_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_TESTPIC.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_TESTPIC_MEDIUM.jpg"> </a>
	<figcaption>Montaje de prueba e imagen obtenida</figcaption>
</figure>

##### Posibles mejoras

Tanto el firmware, como el servidor para carga de fotografias, tienen como funcion servir de esqueleto para producir aplicaciones mas robustas, por lo tanto algunas cosas se han obviado, queda como tarea para el lector llevar a cabo algunas mejoras propuestas como:

* Wi-Fi manager para poder cambiar los parametros de conexion sin requerir reconexion.
* Agregar algun tipo de autenticacion al enviar datos al servidor
* Poder cambiar parametros como el intervalo de sueño profundo, calidad de las fotografias, etc, desde el servidor en cada envio de fotografias.
* Implementar algun tipo de scheduler mediante el RTC, para que el modulo tome fotografias en fechas y horas especificas.
* Usar una mejor antena Wi-FI (externa al modulo pero ubicada dentro de la carcasa), y ponerla en un sitio con menos obstrucciones dentro de la carcasa, para ello hay que realizar algunos cambios en los componentes cercanos al conector U.FL 

