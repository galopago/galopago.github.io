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

A corrente de saída da fonte de alimentação é de cerca de 3,8A máximo, e cada LED WS2811 consome 60 mA no máximo, então pelo menos 63 LEDs poderiam ser alimentados. Para ficar abaixo do máximo absoluto, apenas 50 LED é recomendado. Qualquer corda de LED que funcione com o protocolo compatível com WS2811 pode ser usada.

##### Mongoose OS:

O Mongoose OS é um sistema operacional para a Internet das Coisas, que pode rodar no ESP8266, ESP32 e em outros dispositivos. É uma mistura de facilidade e robustez. Ideal para prototipagem rápida de produtos IoT devido à sua conectividade nativa com a nuvem (AWS, Google, Azure).

Existem duas características que tornam o Mongoose OS tão versátil. Uma delas é a possibilidade de trabalhar "remoto/local". A opção remota é a padrão e compila o código na nuvem, o que é bom para iniciantes, pois evita problemas relacionados à instalação de SDKs. A opção local é baseada em containers Docker e é boa para builds automáticos sem conexão à internet.

Outra característica importante é o uso de uma versão simplificada de JavaScript chamada mJS como linguagem de programação. Funcionalidades avançadas podem ser escritas com poucas linhas de código em comparação com outras linguagens (Assembler, C, Processing). No entanto, não há impedimento de chamar funções escritas em C, especialmente para controladores de dispositivos sensíveis ao tempo.

##### Software:

A amostra da aplicação apresentada aqui é composta por duas tarefas: Enviar dados de cor para cada LED na string e escutar dados de entrada vindos da nuvem.

Para enviar dados para cada LED, o código de cor é extraído aleatoriamente de uma tabela de cores predefinida. A comunicação com a corda de LED é feita usando a biblioteca NEOPIXEL que vem junto com o Mongoose OS.

Uma conexão MQTT é estabelecida com um corretor onde o aplicativo se inscreve em um tópico específico. Um aplicativo cliente de terceiros deve se conectar ao mesmo corretor MQTT e publicar dados no mesmo tópico para mudar a paleta de cores utilizada. Este é um jeito muito simples de mudar o padrão de luz na internet.

##### Montagem do circuito:

O circuito foi construído usando componentes da MISISTEMITA, como a placa de montagem removível, a placa de fonte de alimentação, a placa breakout NODEMCU, a placa de conversor de nível lógico e a placa borne de parafuso. Uma vez que o aplicativo é baixado pela primeira vez e as conexões elétricas são verificadas, a placa de montagem removível pode ser fixada ao caixa sem problemas. Basta desconectar os cabos externos dos terminais, fixar a placa de montagem removível ao caixa e reconectar os cabos novamente.

<figure class="third">
	<a href="/assets/images/MOS_WIFI_LIGHTS_PARTS.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_PARTS_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_WIRED.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_WIRED_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_WORKING.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_WORKING_MEDIUM.jpg"> </a>
	<figcaption>Montagem e fiação</figcaption>
</figure>

É recomendável trocar os conectores da fita LED por conectores mais robustos e à prova d'água. Deve-se usar tubo termoretrátil com cola (parede dupla) para proteger as soldas do tempo.

<figure class="third">
	<a href="/assets/images/MOS_WIFI_LIGHTS_CABLEGLAND.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_CABLEGLAND_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_CONNECTOR.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_CONNECTOR_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_FINISHED.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_FINISHED_MEDIUM.jpg"> </a>
	<figcaption>Conectores à prova d'água e prensa cabos</figcaption>
</figure>

Uma vez que a caixa está fechada, as atualizações de firmware podem ser feitas sem fio via OTA, usando o painel de gerenciamento de dispositivos mDASH do Mongoose OS.

#### Lista de materiais

| Componente | Ligação do compra | Folha de dados
| ------------------ | ----------------- | ----------------------------- |
| ESP8266 NodeMCU V3    | [Compre aqui](https://s.click.aliexpress.com/e/_As5zmb)| [NodeMCUV3.pdf](/assets/pdf/NodeMCUV3.pdf)           |
| Corda LED WS2811 à prova d'água | [Compre aqui](https://s.click.aliexpress.com/e/_AWaLpZ )| [WS2811_WATERPROOF_LED_STRING.pdf](/assets/pdf/WS2811_WATERPROOF_LED_STRING.pdf)                               |
| Fonte de alimentação comutada 5V 3.8A 20W   | [Compre aqui](https://s.click.aliexpress.com/e/_9gYBnH)     | [5V_4A_switching_power.pdf](/assets/pdf/5V_4A_switching_power.pdf)           |
| Caixa plástica à prova d'água 200x120x75mm (multiple options: transparent lid, wall mounting tabs)| [Compre aqui](https://s.click.aliexpress.com/e/_ASuE1N)  | [g373_g269.pdf](/assets/pdf/g373_g269.pdf)           |
| Parafuso auto-rostante tipo B M2.6 | [Compre aqui](https://s.click.aliexpress.com/e/_98ymAB)  | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf)                           |
| Parafuso cabeça chata Phillips M3 | [Compre aqui](https://s.click.aliexpress.com/e/_AoOvPz)  | [M2-M10_Stainless_steel_304_countersunk_screw_flat_head_phillips.pdf](/assets/pdf/M2-M10_Stainless_steel_304_countersunk_screw_flat_head_phillips.pdf)                           |
| Porca Flangeada M3 DIN6923 | [Compre aqui](https://s.click.aliexpress.com/e/_9g89th)  | [FLANGED_NUT_3MM_DIN6923.pdf](/assets/pdf/FLANGED_NUT_3MM_DIN6923.pdf)                           |
| Espaçador de Nylon de travamento reverso G228  | [Compre aqui](https://s.click.aliexpress.com/e/_A7PPYf)  | [G228.pdf](/assets/pdf/G228.pdf)                           |
| Prensa cabo PG7 or PG9 | [Compre aqui](https://s.click.aliexpress.com/e/_9z6Z4r )  | [pg_7.pdf](/assets/pdf/pg_7.pdf) | 
| Conector de cabo à prova d'água de 3 pinos para corda de LED.  | [Compre aqui](https://s.click.aliexpress.com/e/_AesJgr )  | [Waterproof_led_string_connector.pdf](/assets/pdf/Waterproof_led_string_connector.pdf)                           |
| 3:1 tubo termoretrátil com cola  | [Compre aqui](https://s.click.aliexpress.com/e/_AaW9bd)  | [3_1_heatshrink_tube_glue.pdf](/assets/pdf/3_1_heatshrink_tube_glue.pdf)                           |
| 2:1 Tubo termoretrátil em múltiplas cores  | [Compre aqui](https://s.click.aliexpress.com/e/_9ikkU7 )  | [2_1_heatshrink_tube_colors.pdf](/assets/pdf/2_1_heatshrink_tube_colors.pdf)                           |

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
