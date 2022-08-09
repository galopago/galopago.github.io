---
title: "Camara WiFi alimentada por energia solar"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - espanol
tags:
  - AN006
  - Solar
  - ESP32
header:
     teaser: "/assets/images/ENERGY_HARVESTING_CAMERA_TEASER.jpg"
---

El modulo ESP32-CAM es un dispositivo economico basado en el modulo ESP32-S,un sensor de imagen OV2640 y un conector para tarjeta MicroSD. Si bien este dispositivo no viene diseñado para un bajo consumo de energia, tras una serie de modificaciones se puede llegar a un nivel aceptable para que funcione de modo intermitente alimentado por energia solar. El proyecto aqui presentado es una plataforma para experimentacion razonablemente robusta, a prueba de polvo y agua, basada en componentes comerciales listos para usar. Ideal para montajes en exteriores.

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_MEDIUM.jpg"> </a>
	<figcaption>Camara WiFi alimentada por energia solar lista para ser ubicada en exteriores</figcaption>
</figure>

Componente clave: [ESP 32 CAM](https://s.click.aliexpress.com/e/_Dde4rkL)
{: .notice--danger}


<figure>
	<a href="/assets/images/solar_wificamera_wires.png"> <img src="/assets/images/solar_wificamera_wires.png"> </a>
	<figcaption>Diagrama simplificado del proyecto</figcaption>
</figure>

##### Reduciendo el consumo energetico

El ESP-32 CAM no esta diseñado para ser un dispositivo de bajo consumo, sin modificacion alguna, al poner el ESP32 en deep sleep, el consumo electrico medido es de 2.8 mA lo cual deja mucho que desear. 

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_POWER.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_POWER_MEDIUM.jpg"> </a>
	<figcaption>Medicion de consumo en deep sleep del modulo sin modificar</figcaption>
</figure>

Algunas personas en internet ya se han aventurado a hacer este tipo de modificaciones las cuales son las siguientes:

* Remover el regulador de voltaje de 5V a 3.3 V, la camara se alimentara directamente mediante bateria LiFePO4
* Cortar la pista que alimenta la camara a 3.3 V y conectarla al MOSFET que conmuta los reguladores de 2.8V y 1.2V
* Retirar el led y conectar el GPIO33 al pin de alimentacion de 5V para poder utilizar este GPIO de forma externa.

Estas modificaciones bajan el consumo en deep sleep hasta los 0.8 mA que es escandaloso para ser llamado bajo consumo, sinembargo es un avance sustancial sobre los 2.8 mA sin modificacion alguna.

<figure class="third">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_SWTICH.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_SWTICH_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_NOREGULATORLED.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_NOREGULATORLED_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_LOWPOWER.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_LOWPOWER_MEDIUM.jpg"> </a>
	<figcaption>Modificaciones y resultado final</figcaption>
</figure>

##### Listado de materiales

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_PARTS.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_PARTS_MEDIUM.jpg"> </a>
	<figcaption>Partes usadas en la construccion</figcaption>
</figure>

| Componente        | Enlace de compra | Hoja de datos                                   |
| ----------------- | ---------------- | ----------------------------------------------- |
| ESP 32-CAM        | [compralo aqui](https://s.click.aliexpress.com/e/_Dde4rkL) | [esp-32-cam.pdf](/assets/pdf/esp-32-cam.pdf) |

| Tarjeta de circuito impreso (PCB) | Enlace de compra | Repositorio con archivos fuente  |
| --------------------------------- | ---------------- | ------------------------------- |
| Tarjeta prototipo ESP32-CAM para caja de camara deportiva | [compralo aqui](https://www.pcbway.com/project/shareproject/ESP32_CAM_HOST_BOARD_THAT_FITS_INSIDE_WATERPROOF_SPORTSCAM_HOUSING_d06579a9.html) | [esp32cam-proto-sportcam](https://github.com/galopago/misistemote/tree/main/esp32cam-proto-sportcam) |

| Software | repositorio |
| ----------------------- | ---------------- |
| Firmware de ejemplo para envio de fotografias mediante HTTP POST | [descargalo aqui](https://github.com/galopago/esp32cam-upload) |
| Servidor para envio de imagenes mediante HTTP POST | [descargalo aqui](https://github.com/galopago/golang-upload-server) |

| Herramientas opcionales | Enlace de compra | Hoja de datos |
| ----------------------- | ---------------- | ------------------------------- |
| Taladro manual y juego de brocas de multiples diametros 0.5-3mm | [compralo aqui](https://s.click.aliexpress.com/e/_DBPw6on) | [Hand-drill-set-mini.pdf](/assets/pdf/Hand-drill-set-mini.pdf) |

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

La camara obtiene energia de paneles solares que van instalados dentro de la carcasa, esto significa que el area de dichos paneles sera pequeña y se requerira maximizar su eficiencia. Para ello se uso un modulo de cosecha de energia basado en el integrado BQ25504. Este modulo eleva la tension de los paneles solares y es capaz de hacerlo con valores de voltaje tan bajos como 130mV!. Por lo tanto es capaz de producir corriente que sera almacenada en la bateria incluso si los paneles no reciben luz directa. 
<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_HARVESTER.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_HARVESTER_MEDIUM.jpg"> </a>
	<figcaption>Circuito cosechador de energia adherido mediante cinta doble faz</figcaption>
</figure>

Este modulo tambien hace la funcion de cargador de bateria, pues se le configura un voltaje maximo de carga que nunca sera superado, ademas genera una señal en caso de bajo voltaje de bateria. La configuracion de estos parametros se hace mediante resistencias. El fabricante provee una hoja de calculo para facilitar dicho trabajo.

Dado que la carcasa es transparente es posible ubicar distintos paneles solares dentro de ella en diferentes sitios y conectarlos ya sea en serie o paralelo. Probalmenente sea necesario poner diodos de alta eficiencia al hacer dichas conexiones, para no perder tanta potencia en caso de obtener sombras muy fuertes sobre alguno de los paneles.

Otra funcion importante del modulo cosechador es generar una señal de NIVEL DE VOLTAJE OK, para que la MCU pueda ser operada cuando todo esta bajo control, o para que por el contrario se mantenga en modo RESET en caso que el nivel de la bateria sea demasiado bajo. 

<figure class="third">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_TWOPANELS.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_TWOPANELS_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDINSTALLED.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDINSTALLED_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BACKPANEL.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BACKPANEL_MEDIUM.jpg"> </a>
	<figcaption>Paneles y tarjeta instalados dentro</figcaption>
</figure>

##### Presupesto energetico

Advertencia: Se simplificaran aqui muchos datos para poder dar un resultado de forma simple y rapida!
{: .notice--danger}

El ESP32 requiere aproximadamente 200 mA a 3.3 V para enviar datos via WiFi, esto se traduce en 0.66 W. Un panel solar de 40x40mm que cabe dentro de la carcasa mencionada con anterioridad produce 65mA a 2 V a pleno sol, esto se traduce en 0.13 W. Con los anteriores datos es evidente que es imposible usar el esp32 en transmision WiFi continua con dicho panel, incluso a pleno sol. 

La solucion implica el uso de un elemento de almacenamiento de energia como una bateria y el uso del modulo esp 32 de forma intermitente, consumiendo la menor energia posible cuando se encuentre en "modo sueño".

El modulo en "sueño profundo" consume aproximadamente 0.88 mA a 3.3 V lo que se traduce en 0.003 W. Asumiendo 12 horas de luz al dia, se requeririan 0.006 W promedio en el dia solo para mantener el modulo dormido. Si el conjunto panel/cosechador puede al menos entregar promedio en el dia el 4.6% de la potencia maxima del panel solar a pleno sol, ya se puede mantener alimentado el esp 32 en modo sueño profundo por un tiempo muy largo (hasta que se desgaste la bateria!)

Asumiendo 100.000 Lux como pleno sol y 100% de potencia del panel de 40x40mm como 0.13 W, se estimaria que la iluminacion promedio que se requiere en un dia para que el esp 32 permanezca alimentado en modo sueño profundo seria de unos 4600 Lux.

##### Cuanta energia se requiere para tomar una fotografia y enviarla por internet

Al modulo esp 32, despues de despertar de sueño profundo le toma aproximadamente 4 segundos para tomar una fotografia y enviarla por internet. Durante esos cuatro segundos la corriente exigida a la bateria es en promedio 200 mA a 3.3 V. La corriente que sebera acumular durante 12 horas para lograr tomar una foto sera:

esp 32
200 mA x 4 S

se necesita:
X mA x 12 H
X ma x 12 (3600) S
X ma x 43200 S  (redondeando a 40000 para facilitar los calculos)

factor = 4 S / 40000 S = 0.0001

200 mA * 0.0001 = 10 uA (a 3.3 V)

Se requiere acumular un promedio de 10 uA durante doce horas para tomar una fotografia y enviarla via WiFi. Lo cual es perfectamente posible en exteriores incluso en dias nublados.

Haciendo un comparativo con Lux y el panel de 40x40mm y 0.13 W

100.000 Lux	=> 0.13 W
   0.77 Lux => 1 uW


10uA * 3.3V = 33 uW

(0.77 Lux /uW ) 33 uW = 25.4 Lux (redondeando a 26 Lux)

Se requeriran 26 Lux de promedio al dia para tomar una fotografia y enviarla por WiFi

Por lo tanto para tomar al menos una fotografia al dia y enviarla por WiFi se requerira 4600 Lux + 26 Lux = 4626 Lux. Para tomar y enviar dos fotografias al dia se requeriran 4652 Lux de promedio al dia y asi sucesivamente!.

##### Firmware y Software

Se presenta como ejemplo un firmware cuya funcion es la siguiente: tomar una fotografia y almacenarla en la memoria Micro SD, enviarla mediante WiFI haciendo una peticion HTTP POST multi-parte, luego de esto entrar en modo de sueño profundo por X tiempo  para luego despertar y repetir el proceso. El codigo puede ser usado para construir un firmware mucho mas robusto y flexible dependiendo de las necesidades individuales. 

Por el lado del servidor, se presenta una pequeña aplicacion escrita en Golang, cuya finalidad es eschuchar peticiones HTTP POST y recibir los datos de imagen enviados por el ESP32-CAM y guardarlos en el una carpeta local. Esta aplicacion debera estarse ejecutando en un PC, o en un Raspberry Pi dentro de la misma red local del ESP32-CAM. Puesto que es un ejemplo basico y no cuenta con ningun tipo de autenticacion, no se recomienda para su uso en un servidor publico en internet.

Para programar el modulo, es necesario una interfaz USB a TTL serial,  pues este modulo no incorpora dicho chip. Tambien sera necesario poner el GPIO a GND durante la programacion. 

El GPIO33 ha sido liberado del led que usaba la tarjeta internamente y alambrado externamente, el firmware lo usa para depuracion, pero podria ser utilizado con otros fines como:

* ADC para determinar el voltaje de la bateria.
* Configurado como pin de RTC podria ser usado para despertar la tarjeta del sueño profundo, por ejemplo con un sensor PIR.
* Conectar un pulsador para realizar algun tipo de configuracion local sin requerir computador ni conectividad.

##### Posibles mejoras

Tanto el firmware, como el servidor para carga de fotografias, tienen como funcion servir de esqueleto para producir aplicaciones mas robustas, por lo tanto algunas cosas se han obviado, queda a tarea del lector llevar a cabo algunas mejoras propuestas como:

* WiFi manager para poder cambiar los parametros de conexion sin requerir reconexion.
* Agreagar algun tipo de autenticacion al enviar datos al servidor
* Poder cambiar parametros como el intervalo de sueño profundo, calidad de las fotografias, etc, desde el servidor en cada envio de fotografias.
* Implementar algun tipo de scheduler mediante el RTC, para que el modulo tome fotografias en fechas y horas especificas.

