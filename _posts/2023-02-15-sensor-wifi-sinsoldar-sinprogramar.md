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

Las plataformas para desarrollo de software no-code/low-code permiten crear aplicaciones escribiendo muy poco codigo y en algunos casos, ningun codigo, de forma tal que reducen el tiempo de desarrollo para poner en produccion aplicaciones en muy poco tiempo. 

Este proyecto combina dos ideas: plataforma de software no-code/low-code, con un sistema de prototipado rapido y robusto que no requiere soldar. De esta forma en un par de horas se puede pasar de una idea, a un dispositivo operando en condiciones reales.

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_MEDIUM.jpg"> </a>
	<figcaption>Sensor Wi-Fi desarrollado mediante herramientas de prototipado rapido de SW y HW, en operacion en condiciones reales</figcaption>
</figure>

Componente clave: [ESP 32 D1 MINI](https://s.click.aliexpress.com/e/_DlJju2n)
{: .notice--danger}


### Prototipado rapido robusto hardware-software

Se construira la siguiente aplicacion como ejemplo: un termometro WiFi basado en ESP32, sensor de temperatura DS18B20, e indicador local I2C. Todo esto dentro de una caja a prueba de agua para montaje en pared y alimentado a 5V. Lo anterior se realizara usando los siguientes proyectos:

* HARDWARE: Sistema de prototipado rapido robusto, [MISISTEMITA](https://github.com/galopago/misistemita)

* SOFTWARE: Se realizaran pruebas tanto con [TASMOTA](https://tasmota.github.io) como con [ESPHome](https://esphome.io).


##### Listado de materiales

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTS.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTS_MEDIUM.jpg"> </a>
	<figcaption>Componentes usados en el proyecto</figcaption>
</figure>

##### Partes discretas necesarias

| Componente        | Enlace de compra | Hoja de datos                                   |
| ----------------- | ---------------- | ----------------------------------------------- |
| ESP32 D1 MINI     | [compralo aqui](https://s.click.aliexpress.com/e/_DlJju2n) | [esp32-d1-mini.pdf](/assets/pdf/esp32-d1-mini.pdf) |
| Pantalla OLED 0.96 I2C | [compralo aqui](https://s.click.aliexpress.com/e/_DBmZwu3) | [096-i2c-oled-display.pdf](/assets/pdf/096-i2c-oled-display.pdf) |
| Sensor de temperatura DS18B20 a prueba de agua |[compralo aqui](https://s.click.aliexpress.com/e/_DCzX5Mn)|[ds18b20-waterproof.pdf](/assets/pdf/ds18b20-waterproof.pdf)|
| Resistencias TH 1/4W 1% |[compralo aqui](https://s.click.aliexpress.com/e/_etm4gJ)|[MGR-SERIES.pdf](/assets/pdf/MGR-SERIES.pdf)|
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
| Bastidor para caja generica a prueba de agua de 100 x 68 x 52 mm  | [compralo aqui](https://www.pcbway.com/project/shareproject/BACKPLATE_FOR_GENERIC_100x68_mm_WATERPROOF_ENCLOSURE_MISISTEMITA_A06_BACKPLATE_64582f71.html) | [a06 backplate](https://github.com/galopago/misistemita/tree/main/a-backplates/a06) |
| Bornera de conexiones 2x7 de terminal de tornillo 3.5mm  | [compralo aqui](https://www.pcbway.com/project/shareproject/2x7_3_5_mm_SCREW_TERMINAL_BOARD_TUSISTEMITA_B02_SCREW_TERMINALS_98bfe5fa.html) | [b02 Bornera de conexiones](https://github.com/galopago/misistemita/tree/main/b-screw-terminal-wire-connectors/b02) |
| Tarjeta breakout para ESP32 D1 MINI de terminales de tornillo 3.5mm  | [compralo aqui](https://www.pcbway.com/project/shareproject/Breakout_ESP8266_D1_MINI_ESP32_CAM_and_ESP32_D1_MINI_ce1e3011.html) | [c12 Breakout](https://github.com/galopago/misistemita/tree/main/c-breakouts/c12) |
| Tarjeta breakout para pantalla I2C de terminales de tornillo 3.5mm | [compralo aqui](https://www.pcbway.com/project/shareproject/Breakout_for_I2C_0_96_OLED_Display_MISISTEMITA_C10_BREAKOUT_abf0ab6f.html) | [c10 Breakout](https://github.com/galopago/misistemita/tree/main/c-breakouts/c10) |


| Software | repositorio |
| ----------------------- | ---------------- |
| ESPHome | [descargalo aqui](https://esphome.io/) |
| TASMOTA | [descargalo aqui](https://tasmota.github.io/docs/) |

#### Ensamblaje del hardware

No se requerira soldadura si los modulos a usar han sido construidos o adquiridos con anterioridad. El primer paso consiste en ubicar las tarjetas en el bastidor, como buena practica las [tarjetas de puentes mediante borneras de tornillos](https://github.com/galopago/misistemita/tree/main/b-screw-terminal-wire-connectors) deberan ponerse algun lugar en el borde del bastidor y lo mas cerca posible del sitio del ingreso de los cables.


<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTSPLACED.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTSPLACED_MEDIUM.jpg"> </a>
	<figcaption>Componentes ubicados en el bastidor</figcaption>
</figure>

El segundo paso consiste en cablear los diferentes modulos dependiendo del proyecto originalmente planteado. Puede usarse tanto cable de cobre solido como cable de cobre de multiples hilos. Se recomienda cargar un firmware minimo de prueba para probar la conectividad de los componentes.

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTSWIRED.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTSWIRED_MEDIUM.jpg"> </a>
	<figcaption>Componentes ubicados en el bastidor e interconectados mediante cable</figcaption>
</figure>

El tercer paso consiste en retirar las conexiones externas, ubicar el bastidor en la carcasa y fijarlo mediante tornillos autorroscantes. Introducir los cables de alimentacion por medio de los pasacables y conectarlos nuevamente a la tarjeta. 

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_BACKPLANEFIXED.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_BACKPLANEFIXED_MEDIUM.jpg"> </a>
	<figcaption>Bastidor fijado en la caja y cables de alimentacion externos conectados</figcaption>
</figure>

El paso final consiste en cerrar la tapa, ajustar los pasacables e instalar en muro

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_LIDCLOSED.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_LIDCLOSED_MEDIUM.jpg"> </a>
	<figcaption>Caja cerrada, lista para instalar en muro</figcaption>
</figure>

#### Configuracion del Firmware

Los siguientes puntos no pretenden ser una guia completa de instalacion ni configuracion, para mayor informacion referirse a la documentacion de cada una de las plataformas usadas([Tasmota](https://tasmota.github.io/docs/), [ESPHome](https://esphome.io/guides/)). Se presentara brevemente algunas pistas acerca de como se creo el sensor en cada una de ellas:

##### Tasmota

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_TASMOTA.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_TASMOTA_MEDIUM.jpg"> </a>
	<figcaption>Firmware del sensor usando Tasmota</figcaption>
</figure>


La filosofia de tasmota consiste en un firmware basico pre-compilado que se descarga al dispositivo y una vez descargado se personaliza mediante templates. El instalador de Tasmota esta basado en navegador Web, por lo tanto no se requiere instalar software adicional. Los parametros que se usaron fueron los siguientes:

* Firmware usado como base: Display
* Configuracion del template: Pines del puerto I2C, pin del sensor DS18B20 
* Modo del display: 0
* Tipo del display: SSD1306
* Regla para visualizacion de temperatura: rule 1 ON DS18B20#Temperature DO Displaytext[zs2y20] %value% C ENDON

##### ESPHome

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_ESPHOME.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_ESPHOME_MEDIUM.jpg"> </a>
	<figcaption>Firmware del sensor usando ESPHome</figcaption>
</figure>

La filosofia de ESPHome consiste en compilar un firmware personalizado, usando archivo de configuracion YAML. Esto significa que se requiere tener instalado [Home Assistant](https://www.home-assistant.io/), y una vez se tiene este en funcionamiento, ESPHome se debera instalara como un add-on. Una vez realizados estos dos pasos, ya es posible crear sensores. Se muestra aqui una parte del archivo de configuracion en las secciones mas significativas:


```
# GPIO setup
dallas:
  - pin: 26
i2c:
  sda: 21
  scl: 22

# Sensor setup
sensor:
  - platform: dallas
    address: 0x8c01131b44162184
    id: outside_temperature
    name: "External temperature"
font:  
  # gfonts://family[@weight]
  - file: "gfonts://Roboto"
    id: roboto
    size: 20
display:
  - platform: ssd1306_i2c
    model: "SSD1306 128x64"
    address: 0x3c
    lambda: |-
      it.printf(90, 35, id(roboto), TextAlign::BASELINE_RIGHT , "%.1f °C", id(outside_temperature).state);           
```

##### Resultados

###### hardware:

El ensamblaje del hardware, partiendo de modulos pre-construidos tomo aproximadamente una hora.

###### firmware:

La configuracion del sensor mediante Tasmota tomo aproximadamente 10 minutos. Realizar algun tipo de cambio como configuracion de algun pin o regla de visualizacion toma aproximadamente 1 minuto.

La misma tarea mediante ESPHome tomo aproximadamente 2 horas la primera vez, pues se requiere instalar Home Assistant (En un Raspberry Pi o en otro computador independiente). Una vez esta instalado ESPHome, realizar algun tipo de cambio puede tomar de 5 a 10 minutos dependiendo de la velocidad del Rpi para compilar el codigo.

Con ambas plataformas, las actualizaciones se hacen de manera inalambrica (OTA) despues de la programacion inicial que debe realizarse conectando el ESP32 a un PC

El unico "codigo" que debio digitarse en ambas plataformas fue el necesario para visualizar la temperatura en el display I2C. Cada plataforma tiene su propio lenguaje para realizar esto. En ambos casos fue cuestion de una sola linea

