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

#### Montagem de hardware

A soldagem não será necessária* se os módulos a serem usados já tiverem sido construídos ou adquiridos antecipadamente. O primeiro passo é localizar as placas na placa de montagem removível, como boa prática, os [terminais borna com parafuso](https://github.com/galopago/misistemita/tree/main/b-screw-terminal-wire-connectors) devem ser colocados em algum lugar na borda da placa de montagem removível e o mais próximo possível do ponto de entrada do cabo.


<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTSPLACED.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTSPLACED_MEDIUM.jpg"> </a>
	<figcaption> Placas colocadas na placa de montagem removível </figcaption>
</figure>

O segundo passo é conectar os diferentes módulos dependendo do projeto originalmente proposto. Tanto cabos de cobre sólido quanto cabos de cobre multifilares podem ser usados. É recomendável baixar um firmware de teste mínimo para testar a conectividade dos componentes.


<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTSWIRED.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_PARTSWIRED_MEDIUM.jpg"> </a>
	<figcaption>Placas colocadas na placa de montagem removível e conectadas com fios</figcaption>
</figure>

O terceiro passo é remover as conexões externas, posicionar a placa de montagem removível na caixa e fixá-la com parafusos autoroscantes. Passe os cabos de alimentação pelos prensa cabos e reconecte-os à placa.


<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_BACKPLANEFIXED.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_BACKPLANEFIXED_MEDIUM.jpg"> </a>
	<figcaption>Placa de montagem removível fixada na caixa e cabos externos reconectados</figcaption>
</figure>

O último passo consiste em fechar a tampa, ajustar as prensa cabos e instalar na parede.

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_LIDCLOSED.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_LIDCLOSED_MEDIUM.jpg"> </a>
	<figcaption>Tampa fechada, pronta para instalação na parede</figcaption>
</figure>

#### Configuração de firmware

Os seguintes pontos não têm a intenção de ser um guia de instalação ou configuração abrangente. Para obter mais informações, consulte a documentação de cada plataforma utilizada ([Tasmota](https://tasmota.github.io/docs/) e [ESPHome](https://esphome.io/guides/)). Em resumo, algumas dicas sobre como o sensor foi criado em cada uma delas serão apresentadas.


##### Tasmota

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_TASMOTA.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_TASMOTA_MEDIUM.jpg"> </a>
	<figcaption>Firmware de sensor usando Tasmota</figcaption>
</figure>

A filosofia do Tasmota consiste em um firmware pré-compilado básico que é baixado no dispositivo e uma vez baixado, é personalizado usando templates. O instalador do Tasmota é baseado em um navegador da web, portanto, nenhum software adicional é necessário. Os seguintes parâmetros foram usados:

* Firmware Base: Display
* Configuração de template: Pinos da porta I2C, pino do sensor DS18B20
* Display mode: 0
* Display type: SSD1306
* Temperature visualization rule: rule 1 ON DS18B20#Temperature DO Displaytext[zs2y20] %value% C ENDON

##### ESPHome

<figure>
	<a href="/assets/images/AN008/WIFI_SENSOR_LOWCODE_ESPHOME.jpg"> <img src="/assets/images/AN008/WIFI_SENSOR_LOWCODE_ESPHOME_MEDIUM.jpg"> </a>
	<figcaption>Firmware de sensor usando ESPHome</figcaption>
</figure>

A filosofia do ESPHome consiste em compilar um firmware personalizado usando um arquivo de configuração YAML. Isso significa que o Home Assistant precisa ser instalado e, uma vez em funcionamento, o ESPHome deve ser instalado como um add-on. Após essas duas etapas, já é possível criar sensores. Uma parte do arquivo de configuração é mostrada aqui nas seções mais significativas.

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

##### resultado final

###### hardware:

A montagem do hardware, começando a partir de módulos pré-construídos, levou cerca de uma hora.

###### firmware:

Sensor firmware setup, using Tasmota, took approximately 10 minutes. Making a change to configuration like an I/O pin or visualization rule takes approximately 1 minute.

The same task, using ESPHome, took approximately 2 hours the first time, because Home Assistant needs to be installed (On a Raspberry Pi or other computer). Once ESPHome is installed Making a change in configuration takes around 5 to 10 minutes depending of the speed of the Rpi for code compilation.

On both platforms, the first setup is wired (ESP32 connected to a PC). After that all updates are done wirelessly (OTA).

The only "code" that was typed on both platforms was the minimum necessary to visualize temperature on the I2C display. Each platform has its own way to do that. In both cases, has been just a single line.



