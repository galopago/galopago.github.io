---
title: "Fio de LED à prova d'água controlado por WiFi"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - portugues
tags:
  - AN001
  - WiFi
  - MONGOOSE OS
header:
     teaser: "/assets/images/MOS_WIFI_IOT_LIGHTS_TEASER.jpg"
---

Luzes decorativas adequadas para Halloween, Natal, festas, etc. Não apenas controladas na internet, mas também completamente reprogramadas sem fio usando OTA sobre WiFi. à prova d'água, à prova de poeira e resistentes. Ideal para projetos internos como planos de fundo interativos para youtubers / streamers controlados por sua audiência e para projetos externos como sinais de publicidade em paredes ou veículos.


<figure>
	<a href="/assets/images/MOS_WIFI_IOT_LIGHTS.jpg"> <img src="/assets/images/MOS_WIFI_IOT_LIGHTS_MEDIUM.jpg"> </a>
	<figcaption>Abertura da caixa mostrando componentes internos</figcaption>
</figure>

Componente chave: [WS2811 waterproof LED string.](https://s.click.aliexpress.com/e/_AWaLpZ)
{: .notice--danger}


##### Conceito:

Com o advento de LEDs endereçáveis, como WS2812, WS2812b, WS2811, etc., agora é possível para microcontroladores pequenos lidarem com grandes quantidades de LEDs com apenas um pino de E/S. Essa vantagem popularizou esse componente e muitas variantes surgiram: LED único montado na superfície, fitas flexíveis, cordas como as de Natal, etc. A última será usada neste artigo devido à sua flexibilidade e força e pode ser facilmente adaptada a projetos diferentes, desde enfeites de Natal até matrizes de LED, sem soldar ou outras modificações elétricas.

O microcontrolador escolhido foi o ESP8266, mais especificamente uma placa de desenvolvimento conhecida como "NODEMCU V3", que possui todos os componentes adicionais necessários para começar a trabalhar na programação do MCU com um computador. O WiFi onboard do ESP8266 permite não apenas mudar as sequências de luz, mas também baixar um firmware totalmente diferente sem fio (OTA), usando uma combinação poderosa: [Mongoose OS](https://mongoose-os.com/) e sua central de gerenciamento de dispositivos remotos [mDASH](https://mdash.net/). O Mongoose OS usa uma versão reduzida do JavaScript conhecida como [mJS](https://github.com/cesanta/mjs). Este é um idioma atraente para desenvolvedores web que já trabalham com JS. O Mongoose OS é construído em cima do ESP-iDF do Espressif, então é possível escrever funções em C, o que também é atraente para programadores embarcados mais "tradicionais".

O circuito é construído usando o sistema de prototipagem de hardware [MISISTEMITA](https://github.com/galopago/misistemita), que fornece diferentes tipos de módulos pré-construídos, permitindo construir um projeto eletrônico sem solda, mas tornando-o muito robusto e expansível. Todas as peças estão encerradas em uma caixa à prova de poeira e à prova d'água IP65. Esta caixa dá um "aspecto industrial" ao projeto e também adiciona força mecânica para suportar abusos. As conexões elétricas externas (CA e LED) foram equipadas com acessórios IP para fornecer uma boa vedação.

#### Recursos Chave:
* Sistema operacional embarcado Mongoose OS executando no ESP8266.
Proteção contra poeira, água e pode ser montado na parede.
* Atualização remota de firmware sem fio, graças ao painel de gerenciamento mDASH do Mongoose OS.
* Construído com blocos de prototipagem de hardware MISISTEMITA
Alimentação AC de 110/220V

O circuito é composto por 4 elementos bem diferenciados: fonte de alimentação, CPU, conversor de nível lógico e LEDs. A fonte de alimentação é do tipo comutado, com potência de 20W, saída de 5V e entrada de 110/220V, de forma a ser utilizado em qualquer país do mundo. O ESP8266 foi usado como CPU (NODEMCU V3). Esta placa pode ser alimentada com 3,3V diretamente no pino de alimentação do processador ou com 5V usando o regulador embarcado. O nível lógico alto de saída do ESP8266 é de 3,3V, portanto, é necessário um conversor de nível lógico para trabalhar com sensores de 5V. O WS2812 funciona com níveis lógicos de 5V, então foi usado o conversor de nível lógico MISISTEMITA D06. Esta placa é baseada no MOSFET BSS138.


<figure>
	<a href="/assets/images/mos_wifi_iot_lights_blockdiag.png"> <img src="/assets/images/mos_wifi_iot_lights_blockdiag.png"> </a>
	<figcaption>Diagrama de blocos simplificado</figcaption>
</figure>

Power source output current is around 3.8A max, and each WS2811 LED consumes 60 mA max, so at least 63 LED could be powered. To stay below absolute maximum only 50
LED is recommended. Any LED string that works with WS2811 compatible protocol could be used.

##### Mongoose OS:

Mongoose OS is an operating system for the Internet Of Things, it can run on ESP8266, ESP32 and others. Is a blend of easiness and robustness. Ideal for rapid prototyping
of IoT products because of its native built-in cloud connectivity (AWS, Google, Azure).
There are two characteristics that make Mongoose OS so versatile. One of them is the possibility to work "remote/local". Remote is the default option, and compiles
the code in the cloud, this is good for beginners because avoids the problems related to SDK installations. Local option is based on docker containers and is good for automatic builds
without internet connection.

Another important characteristic is the use of a scaled down version of JavaScript called mJS as programming language. Advanced functionalities could be written with
few lines of code compared to other languages (Assembler, C, Processing). However, nothing prevents to call functions written in C, especially for time sensitive device drivers.

##### Software:

Sample application presented here is composed of two tasks: Send color data for every LED in the string and listen to incoming data coming from the cloud.

To send data to each LED, the color code is randomly extracted from a predefined color table. Communication to the LED string is made using NEOPIXEL library bundled 
with Mongoose OS.

An MQTT connection is established to a broker where the app subscribes to a specific topic. A third party client application must connect to the same MQTT broker and publish
data to the same topic to change the color palette used. This is a very simple way to change the light pattern over the internet.

##### Circuit assembly:

The circuit was built using components of TUSISTEMITA, like enclosure backplate, power source backplate, NODEMCU breakboard, logic level shifter board and screw
 terminal board. Once the app is downloaded for the first time, and electrical connections verified, the backplate could be attached to the enclosure hassle free. Just unplug
external cables from terminals, screw backplate to enclosure and reconnect cables again.

<figure class="third">
	<a href="/assets/images/MOS_WIFI_LIGHTS_PARTS.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_PARTS_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_WIRED.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_WIRED_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_WORKING.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_WORKING_MEDIUM.jpg"> </a>
	<figcaption>Assembly and wiring.</figcaption>
</figure>

It is recommended to change the connectors of the LED strip, for a more robust and waterproof connectors. Heatshrink tube with glue (double wall) should 
be used to protect solder joints from the elements.

<figure class="third">
	<a href="/assets/images/MOS_WIFI_LIGHTS_CABLEGLAND.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_CABLEGLAND_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_CONNECTOR.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_CONNECTOR_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_FINISHED.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_FINISHED_MEDIUM.jpg"> </a>
	<figcaption>Cable glands and waterproof connectors</figcaption>
</figure>

Once the enclosure is closed, firmware updates could be done via wirelessly via OTA, using Mongoose OS device management dashboard mDASH.

#### Bill of materials

| Component         | Get yours! | Datasheet
| -------- | ------ | ------------------------------------------------------------ |
| ESP8266 NodeMCU V3    | [💸](https://s.click.aliexpress.com/e/_As5zmb)     | [NodeMCUV3.pdf](/assets/pdf/NodeMCUV3.pdf)           |
| WS2811 waterproof LED string | [💸](https://s.click.aliexpress.com/e/_AWaLpZ )  | [WS2811_WATERPROOF_LED_STRING.pdf](/assets/pdf/WS2811_WATERPROOF_LED_STRING.pdf)                               |
| Switched power supply 5V 3.8A 20W   | [💸](https://s.click.aliexpress.com/e/_9gYBnH)     | [5V_4A_switching_power.pdf](/assets/pdf/5V_4A_switching_power.pdf)           |
| Waterproof plastic enclosure 200x120x75mm (multiple options: transparent lid, wall mounting tabs)| [💸](https://s.click.aliexpress.com/e/_ASuE1N)  | [g373_g269.pdf](/assets/pdf/g373_g269.pdf)           |
| M2.6 self-tapping B type screw | [💸](https://s.click.aliexpress.com/e/_98ymAB)  | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf)                           |
| M3 countersunk phillips screw | [💸](https://s.click.aliexpress.com/e/_AoOvPz)  | [M2-M10_Stainless_steel_304_countersunk_screw_flat_head_phillips.pdf](/assets/pdf/M2-M10_Stainless_steel_304_countersunk_screw_flat_head_phillips.pdf)                           |
| M3 hex flanged nut DIN6923 | [💸](https://s.click.aliexpress.com/e/_9g89th)  | [FLANGED_NUT_3MM_DIN6923.pdf](/assets/pdf/FLANGED_NUT_3MM_DIN6923.pdf)                           |
| Nylon spacer G228  | [💸](https://s.click.aliexpress.com/e/_A7PPYf)  | [G228.pdf](/assets/pdf/G228.pdf)                           |
| Cable gland PG7 or PG9 | [💸](https://s.click.aliexpress.com/e/_9z6Z4r )  | [pg_7.pdf](/assets/pdf/pg_7.pdf) | 
| 3 pin waterproof cable connector for LED string  | [💸](https://s.click.aliexpress.com/e/_AesJgr )  | [Waterproof_led_string_connector.pdf](/assets/pdf/Waterproof_led_string_connector.pdf)                           |
| 3:1 Heatshrink tube with glue  | [💸](https://s.click.aliexpress.com/e/_AaW9bd)  | [3_1_heatshrink_tube_glue.pdf](/assets/pdf/3_1_heatshrink_tube_glue.pdf)                           |
| 2:1 Heatshrink tube multiple colors  | [💸](https://s.click.aliexpress.com/e/_9ikkU7 )  | [2_1_heatshrink_tube_colors.pdf](/assets/pdf/2_1_heatshrink_tube_colors.pdf)                           |

#### TUSISTEMITA blocks

| PCB    |  Source file                                          | 
| -------- | ------------------------------------------------------------ |
| A02 Backplate for 200x120x75mm enclosure | [A02](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)           |
| A05 adapterboard 10.16mm pitch for 5V 3.8A PSU  | [A05](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)        |
| B01 2x4 3.5mm screw terminal board | [B01](https://github.com/galopago/TUSISTEMITA/tree/master/B_SCREW_TERMINAL_WIRE_CONNECTORS)        |
| C08 screw terminal breakout board for NODEMCU V3  | [C08](https://github.com/galopago/TUSISTEMITA/tree/master/C_BREAKOUTS)        |
| D06 logic level shifter board  | [D06](https://github.com/galopago/TUSISTEMITA/tree/master/D_ELECTRONICS)        |


#### Software

| Software    | Source file                                          | 
| -------- | ------------------------------------------------------------ |
| Firmware    | [MOS_IOT_ADDRESSABLE_LEDS](https://github.com/galopago/MOS_IOT_ADDRESSABLE_LEDS)           |

 

## Componentes opcionales:

| Component         | Get yours! | Datasheet                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| 3 pc step drill bit 3-20 mm + centerpunch | [💸](https://s.click.aliexpress.com/e/_9vxJV5 )     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
| 8 Step drill bit 10-45 mm    | [💸](https://s.click.aliexpress.com/e/_9Ior51)     | [8_steps_10-45mm_incremental_drill_bit.pdf](/assets/pdf/8_steps_10-45mm_incremental_drill_bit.pdf)           |
