---
title: "DIY Sensor Wi-Fi, sem programação, sem solda necessária*"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - portugues
tags:
  - AN008
  - ESP32
  - Prototyping
header:
     teaser: "/assets/images/AN008/WIFI_SENSOR_LOWCODE_TEASER.jpg"
---

Plataformas de software no-code/low-code tornaram possível criar aplicações, escrevendo apenas algumas linhas de código e, em alguns casos, sem código algum! Isso reduz o esforço de desenvolvimento e o tempo de implantação.

Este projeto combina duas ideias: plataforma de software no-code/low-code e um sistema de prototipagem rápida e robusto que não requer soldagem. Nesse sentido, é possível passar de uma ideia para um dispositivo materializado que funcione em um ambiente real em poucas horas.

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_MEDIUM.jpg"> </a>
	<figcaption>Sensor Wi-Fi desenvolvido usando ferramentas de prototipagem rápida tanto para software quanto para hardware, operando em condições do mundo real..</figcaption>
</figure>

Componente chave: [ESP 32 D1 MINI](https://s.click.aliexpress.com/e/_DlJju2n)
{: .notice--danger}

### Prototipagem rápida de hardware-software

A seguinte aplicação será construída como exemplo: um termômetro WiFi baseado em ESP32, sensor de temperatura DS18B20 e indicador local I2C. Tudo isso será fechado em uma caixa à prova d'água, montável na parede e alimentado por 5V. Isso será alcançado usando os seguintes projetos:

HARDWARE: Sistema de prototipagem rápida, de código aberto e robusto: [MISISTEMITA](https://github.com/galopago/misistemita)

SOFTWARE: Testado [TASMOTA](https://tasmota.github.io) e também [ESPHome](https://esphome.io).


##### Lista de materiais

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTS.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTS_MEDIUM.jpg"> </a>
	<figcaption>Peças usadas no projeto.</figcaption>
</figure>

##### Peças discretas necessárias

| Componente        | Ligação do compra  | Folha de dados                                   |
| ----------------- | ------------------ | ----------------------------------------------- |
| ESP32 D1 MINI     | [Compre aqui](https://s.click.aliexpress.com/e/_DlJju2n) | [esp32-d1-mini.pdf](/assets/pdf/esp32-d1-mini.pdf) |
| Display OLED 0.96 I2C | [Compre aqui](https://s.click.aliexpress.com/e/_DBmZwu3) | [096-i2c-oled-display.pdf](/assets/pdf/096-i2c-oled-display.pdf) |
| Sensor temperatura prova dágua DS18B20 |[Compre aqui](https://s.click.aliexpress.com/e/_DCzX5Mn)|[ds18b20-waterproof.pdf](/assets/pdf/ds18b20-waterproof.pdf)|
| Resistor 1/4W 1% TH  |[Compre aqui](https://s.click.aliexpress.com/e/_etm4gJ)|[MGR-SERIES.pdf](/assets/pdf/MGR-SERIES.pdf)|
| Caixa plástica à prova d’água “Sonoff” 100x68x50mm | [Compre aqui](https://s.click.aliexpress.com/e/_AtukwZ) | [SONOFF-IP66-waterproof-case.pdf](/assets/pdf/SONOFF-IP66-waterproof-case.pdf)|

##### Componentes necessários para construir os módulos necessários de misistemita

| Componente        | Ligação do compra   | Folha de dados                                      |
| ----------------- | ------------------- | ----------------------------------------------- |
| Espaçador de Nylon de travamento reverso |[Compre aqui](https://s.click.aliexpress.com/e/_DCFVOtz)|[G228.pdf](/assets/pdf/G228.pdf)|
| Parafuso auto-rostante tipo B M2.6 |[Compre aqui](https://s.click.aliexpress.com/e/_esHHyb)|[M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf)|
| Borne de parafuso 3.5mm kf350 (2,3 pinos) para PCB.   |[Compre aqui](https://s.click.aliexpress.com/e/_eLjzKB)|[KF350.pdf](/assets/pdf/KF350.pdf)|
| Barra De Pinos Fêmea 2.54mm |[Compre aqui](https://s.click.aliexpress.com/e/_eNYVzN)|[FHA3-S1XX.pdf](/assets/pdf/FHA3-S1XX.pdf)|


##### Placas de circuito impressas necessárias para construir os módulos necessários do MISISTEMITA

| Placas de circuito impressas (PCB)  | Ligação do compra  | Arquivos de origem         |
| ----------------------------------- | ------------------ | ------------------------------- |
| A06 placa de montagem removível para o caixa de 100 x 68 x 52 mm | [Compre aqui](https://www.pcbway.com/project/shareproject/BACKPLATE_FOR_GENERIC_100x68_mm_WATERPROOF_ENCLOSURE_MISISTEMITA_A06_BACKPLATE_64582f71.html) | [a06 backplate](https://github.com/galopago/misistemita/tree/main/a-backplates/a06) |
| B02 3.5mm 2x7 placa borne de parafuso  | [Compre aqui](https://www.pcbway.com/project/shareproject/2x7_3_5_mm_SCREW_TERMINAL_BOARD_TUSISTEMITA_B02_SCREW_TERMINALS_98bfe5fa.html) | [b02 Screw terminal](https://github.com/galopago/misistemita/tree/main/b-screw-terminal-wire-connectors/b02) |
| C12 Placa Borne De Expansão para ESP32 D1 MINI  | [Compre aqui](https://www.pcbway.com/project/shareproject/Breakout_ESP8266_D1_MINI_ESP32_CAM_and_ESP32_D1_MINI_ce1e3011.html) | [c12 Breakout](https://github.com/galopago/misistemita/tree/main/c-breakouts/c12) |
| C10 Placa Borne De Expansão para display I2C  | [Compre aqui](https://www.pcbway.com/project/shareproject/Breakout_for_I2C_0_96_OLED_Display_MISISTEMITA_C10_BREAKOUT_abf0ab6f.html) | [c10 Breakout](https://github.com/galopago/misistemita/tree/main/c-breakouts/c10) |


| Software | repositorio   |
| ----------------------- | ---------------- |
| ESPHome | [download](https://esphome.io/) |
| TASMOTA | [download](https://tasmota.github.io/docs/) |

#### Hardware assembly

Soldering will not be required* if the modules to be used have been built or acquired beforehand. The first step is to locate the boards in the backplate, as good practice, the [screw terminal wire connection boards](https://github.com/galopago/misistemita/tree/main/b-screw-terminal-wire-connectors) should be placed somewhere on the edge of the backplate and as close as possible to the cable entry point.


<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTSPLACED.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTSPLACED_MEDIUM.jpg"> </a>
	<figcaption>Boards placed on the backplate</figcaption>
</figure>

The second step is to wire the different modules depending on the originally proposed project. Both solid copper cable and multi-stranded copper cable can be used. Downloading a minimum test firmware is recommended to test the connectivity of the components.

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTSWIRED.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTSWIRED_MEDIUM.jpg"> </a>
	<figcaption>Boards placed on the backplate and wired</figcaption>
</figure>

The third step is to remove the external connections, locating the backplate in the enclosure and securing it with self-tapping screws. Pass the power cables through the cable glands and reconnect them to the board.


<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_BACKPLANEFIXED.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_BACKPLANEFIXED_MEDIUM.jpg"> </a>
	<figcaption>Backplate fixed to the enclosure and external cables connected again</figcaption>
</figure>

The final step consists of closing the cover, adjusting the cable glands, and installing on the wall.

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_LIDCLOSED.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_LIDCLOSED_MEDIUM.jpg"> </a>
	<figcaption>Lid closed, ready for wall installation</figcaption>
</figure>

#### Firmware setup

The following points are not intended to be a comprehensive installation or configuration guide. For more information, refer to the documentation of each platform used, ([Tasmota](https://tasmota.github.io/docs/) and [ESPHome](https://esphome.io/guides/)). Briefly, some hints about how the sensor was created on each of them will be presented.


##### Tasmota

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_TASMOTA.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_TASMOTA_MEDIUM.jpg"> </a>
	<figcaption>Sensor Firmware using Tasmota</figcaption>
</figure>

The philosophy of Tasmota consists of a basic pre-compiled firmware that is downloaded to the device and once downloaded it is customized using templates. The Tasmota installer is based on a web browser, so no additional software is required. The following parameters were used:

* Base Firmware: Display
* Template setup: I2C port pins, DS18B20 sensor pin
* Display mode: 0
* Display type: SSD1306
* Temperature visualization rule: rule 1 ON DS18B20#Temperature DO Displaytext[zs2y20] %value% C ENDON

##### ESPHome

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_ESPHOME.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_ESPHOME_MEDIUM.jpg"> </a>
	<figcaption>Sensor Firmware using ESPHome</figcaption>
</figure>

The philosophy of ESPHome consists of compiling a custom firmware using a YAML configuration file. This means that Home Assistant needs to be installed, and once it's up and running, ESPHome should be installed as an add-on. After these two steps, it's already possible to create sensors. A part of the configuration file is shown here in the most significant sections.

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

##### End result

###### hardware:

The assembly of the hardware, starting from pre-built modules, took approximately one hour.

###### firmware:

Sensor firmware setup, using Tasmota, took approximately 10 minutes. Making a change to configuration like an I/O pin or visualization rule takes approximately 1 minute.

The same task, using ESPHome, took approximately 2 hours the first time, because Home Assistant needs to be installed (On a Raspberry Pi or other computer). Once ESPHome is installed Making a change in configuration takes around 5 to 10 minutes depending of the speed of the Rpi for code compilation.

On both platforms, the first setup is wired (ESP32 connected to a PC). After that all updates are done wirelessly (OTA).

The only "code" that was typed on both platforms was the minimum necessary to visualize temperature on the I2C display. Each platform has its own way to do that. In both cases, has been just a single line.



