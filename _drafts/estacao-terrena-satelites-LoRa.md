---
title: "Estação terrena para satélites LoRa"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - portugues
tags:
  - AN005
  - LoRa
  - ESP32
header:
     teaser: "/assets/images/LORA_GROUND_STATION_TEASER.jpg"
---
A chegada de [satélites miniaturizados](https://pt.wikipedia.org/wiki/Sat%C3%A9lite_miniaturizado) que usam [LoRa](https://pt.wikipedia.org/wiki/LoRa) para telemetria de dados significou que pessoas menos qualificadas tecnicamente, com orçamento muito baixo, podem receber suas transmissões. Graças ao TinyGS, agora há uma rede aberta de estações terrestres distribuídas, e mais estações podem ser construídas para aumentar sua cobertura. O projeto apresentado aqui é uma implementação razoavelmente robusta, resistente a poeira e à água do TinyGS ground station, usando componentes comerciais de prateleira. Ideal para uso ao ar livre.


<figure>
	<a href="/assets/images/LORA_GROUND_STATION.jpg"> <img src="/assets/images/LORA_GROUND_STATION_MEDIUM.jpg"> </a>
	<figcaption>Estação terrestre pronta para ser colocada ao ar livre</figcaption>
</figure>

Componente chave: [Heltec WiFi LoRa kit 32 v2 433mhz](https://s.click.aliexpress.com/e/_A0wUdR)
{: .notice--danger}


##### Por quê?

A ideia de usar o LoRa para comunicações por satélite se tornou óbvia para muitas pessoas por seguintes motivos:

* Usa a bandas de rádio [ISM](https://en.wikipedia.org/wiki/ISM_radio_band) não licenciada
* Disponibilidade de módulos eletrônicos prontos para usar, de baixo custo e fáceis de encontrar
* Comunicações de longo alcance e baixa potência
* Receptação possível com sinais de nível muito baixo, -120dBm

O último ponto é muito importante, pois muitas antenas comerciais podem ser usadas (também podem ser feitas em casa!), mesmo que não sejam muito eficientes, são suficientes para receber sinais. Isso era o ponto fraco das comunicações por satélite até agora.

#### O que é o projeto sobre?

Este projeto trata-se de uma ponte entre a Internet (WiFi) e LoRa @433Mhz, utilizando o máximo possível de componentes comerciais de prateleira ([COTS](https://en.wikipedia.org/wiki/Commercial_off-the-shelf)), o que significa que não é necessário muita experiência para a montagem. A chave final é fazer o download do [firmware TinyGS](https://github.com/G4lile0/tinyGS), que permite:

* Download de atualizações de firmware automáticas (OTA)
* O receptor irá sintonizar automaticamente o satélite mais próximo no céu
* Configuração de parâmetros usando a interface web local.

<figure>
	<a href="/assets/images/LORA_GROUND_STATION_TINYGS.png"> <img src="/assets/images/LORA_GROUND_STATION_TINYGS.png"> </a>
	<figcaption>Arquitetura da rede TinyGS (retirada do site TinyGS)</figcaption>
</figure>

#### Lista de materiais

<figure>
	<a href="/assets/images/LORA_GROUND_STATION_PARTS.jpg"> <img src="/assets/images/LORA_GROUND_STATION_PARTS_MEDIUM.jpg"> </a>
	<figcaption>Um pouco de arrumação dos objetos.</figcaption>
</figure>

| Componente        | 	Ligação do compra | Folha de dados                         |
| -------- | ------ | ------------------------------------------------------------ |
| Heltec Lora Kit 32 V2 433MHZ ESP32| [Compre aqui](https://s.click.aliexpress.com/e/_A0wUdR) | [WiFi-LoRa-32-V2-433-470-510.pdf](/assets/pdf/WiFi-LoRa-32-V2-433-470-510.pdf) |
| RP-SMA flange a U.FL pigtail | [Compre aqui](https://s.click.aliexpress.com/e/_9vbEjm) | [Catalog_SMA.pdf](/assets/pdf/Catalog_SMA.pdf) |
| 433 Mhz antenna SMA  | [Compre aqui](https://s.click.aliexpress.com/e/_AYvZau) | [433_MHZ_SMA_ANTENNA.pdf](/assets/pdf/433_MHZ_SMA_ANTENNA.pdf) |
| Caixa Ip66 Prova De "Água Sonoff" 100x68x50mm | [Compre aqui](https://s.click.aliexpress.com/e/_AtukwZ) | [SONOFF-IP66-waterproof-case.pdf](/assets/pdf/SONOFF-IP66-waterproof-case.pdf) |
| Parafuso cabeça chata M2.5 | [Compre aqui](https://s.click.aliexpress.com/e/_AEYxys) | [M2-5_COUNTERSUNK_SCREW.pdf](/assets/pdf/M2-5_COUNTERSUNK_SCREW.pdf) |
| Porca travante nylon M2.5  | [Compre aqui](https://s.click.aliexpress.com/e/_9RIfcu) | [M2-5_NYLON_LOCK_NUT.pdf](/assets/pdf/M2-5_NYLON_LOCK_NUT.pdf) |
| Parafuso auto-rostante tipo B M2.6 | [Compre aqui](https://s.click.aliexpress.com/e/_esHHyb) | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf) |
| Borne de parafuso 3.5mm kf350 (2,3 pinos) para PCB. | [Compre aqui](https://s.click.aliexpress.com/e/_eLjzKB) | [KF350.pdf](/assets/pdf/KF350.pdf) |
| Barra De Pinos Fêmea 2.54mm | [Compre aqui](https://s.click.aliexpress.com/e/_eNYVzN) | [FHA3-S1XX.pdf](/assets/pdf/FHA3-S1XX.pdf) |
| 30 AWG cabo wire wrap UL1423 PVDF | [Compre aqui](https://s.click.aliexpress.com/e/_eL2EYB) | [UL1423.pdf](/assets/pdf/UL1423.pdf) |
| PoE injetor 48V 0.5A  | [Compre aqui](https://s.click.aliexpress.com/e/_Dl1hpWX) | [PoE-injector-48V-05A.pdf](/assets/pdf/PoE-injector-48V-05A.pdf)|
| PoE separador D1398 modulo 5V 2A | [Compre aqui](https://s.click.aliexpress.com/e/_Al2dql) | [WC-PD13C050I.pdf](/assets/pdf/WC-PD13C050I.pdf)|
| Adaptadpr SMA Fêmea a RP SMA macho | [Compre aqui](https://s.click.aliexpress.com/e/_9JKRaz) | [SMA-Female-To-RP-SMA-Male-adapter.pdf](/assets/pdf/SMA-Female-To-RP-SMA-Male-adapter.pdf) |
| Silicone Neutro RTV | [Compre aqui](https://s.click.aliexpress.com/e/_ANKQnb) | [Neutral-cure-silicone.pdf](/assets/pdf/Neutral-cure-silicone.pdf) |
| Fita Isolante Auto Fusão | [Compre aqui](https://s.click.aliexpress.com/e/_DlbGSST) | [Waterproof-silicone-self-fusing-vulcanizing-tape.pdf](/assets/pdf/Waterproof-silicone-self-fusing-vulcanizing-tape.pdf) |


| Placas de circuito impressas (PCB) | Ligação do compra | Arquivos de origem |
| ---------------------------------- | ----------------- | ------------------------------- |
| Placa PCB protótipo para caixa de 100x68mm | [Compre aqui](https://www.pcbway.com/project/shareproject/mcu_proto_100x68mm_6ae31333.html) | [mcu-proto-100x68mm](https://github.com/galopago/misistemote/tree/main/mcu-proto-100x68mm) |

| Software | 	repositório|
| ----------------------- | ---------------- |
| TingyGS Firmware | [download it](https://github.com/G4lile0/tinyGS) |

|  Componentes opcionais  | Ligação do compra | Folha de dados  |
| ----------------------- | ---------------- | ------------------------------- |
| Mini Furadeira De Mão e brocas 0.5-3mm | [Compre aqui](https://s.click.aliexpress.com/e/_DBPw6on) | [Hand-drill-set-mini.pdf](/assets/pdf/Hand-drill-set-mini.pdf) |


##### Montagem:

Este artigo não pretende ser um guia de montagem passo a passo, ele tentará explicar brevemente o que fazer em seguida. Dependendo dos componentes obtidos, algumas instruções e sua sequência podem mudar ligeiramente.

###### Furações para conectores de antenas:

* Faça 4 furações com uma broca ligeiramente maior que 2,5 mm, é aí que as parafusos de fixação vão ir.

* Faça outra furação no meio com uma broca ligeiramente maior que 4 mm, é aí que o fio pigtail vai ir. O modelo de auxílio para furar pode ser encontrado [aqui](https://github.com/galopago/panel-mount-drill-layouts/tree/main/sma-flange-4-holes).


<figure class="third">
	<a href="/assets/images/SMA_FLANGE_TEMPLATE.jpg"> <img src="/assets/images/SMA_FLANGE_TEMPLATE_MEDIUM.jpg"> </a>
	<a href="/assets/images/SMA_FLANGE_FRONT.jpg"> <img src="/assets/images/SMA_FLANGE_FRONT_MEDIUM.jpg"> </a>
	<a href="/assets/images/SMA_FLANTE_DIAG.jpg"> <img src="/assets/images/SMA_FLANTE_DIAG_MEDIUM.jpg"> </a>
	<figcaption>furações para conectores de antenas</figcaption>
</figure>

###### Conectores e soldagem de fios

Existem duas opções para alimentar a estação: usando uma fonte de alimentação simples de 5V ou usando um adaptador PoE. A opção de energia 5V requer menos hardware, mas está limitada a alguns metros de cabo. No entanto, a versão PoE requer um injetor PoE, um divisor PoE dentro da caixa, mas pode ser colocada a até 100 metros de distância.

<figure>
	<a href="/assets/images/tinygs_power_wires_blockdiag.png"> <img src="/assets/images/tinygs_power_wires_blockdiag.png"> </a>
	<figcaption>Diagrama simplificado de fiação elétrica</figcaption>
</figure>

* Soldar os barra de pinos do módulo LoRa. Isso não é 100% necessário, pois o módulo poderia ser soldado diretamente na placa, mas o uso de barra de pinos permite desconectar o módulo a qualquer momento.

* Soldar o barra de pinos do módulo divisor PoE (se usado!).

* Soldar terminais de parafuso na placa para facilitar a conexão/desconexão do cabo de energia.

* Soldar os fios de energia debaixo da placa, usando cabo revestido de PVDF quando possível, entre os pads dos terminais de parafuso e os pads de energia PoE e, em seguida, para os pads de energia LoRa.

<figure class="third">
	<a href="/assets/images/PCB_BARE.jpg"> <img src="/assets/images/PCB_BARE_MEDIUM.jpg"> </a>
	<a href="/assets/images/PCB_CONNECTORS.jpg"> <img src="/assets/images/PCB_CONNECTORS_MEDIUM.jpg"> </a>
	<a href="/assets/images/PCB_POWER_WIRES.jpg"> <img src="/assets/images/PCB_POWER_WIRES_MEDIUM.jpg"> </a>
	<figcaption>Conectores e fios soldados</figcaption>
</figure>

######  Fixação do conector de antena, placa de circuito e cabo de energia.

* Fixe o conector de antena na caixa com os parafusos e porcas de nylon

* Passe o cabo de energia através do prensa cabo, deixando as porcas de ajuste um pouco desapertadas

* Colocar a placa de circuito dentro da caixa e fixá-la com os auto-parafusos

* Conecte o cabo de energia aos terminais de parafuso, cabo de antena ao módulo LoRa e aperte a porca do tampão de cabo. Alguma experimentação com a ordem dos passos mencionados acima será necessária para encontrar a maneira mais fácil de montar.

<figure class="third">
	<a href="/assets/images/TINYGS_ANT_CONNECTOR_FRONT.jpg"> <img src="/assets/images/TINYGS_ANT_CONNECTOR_FRONT_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_POWER_CABLES.jpg"> <img src="/assets/images/TINYGS_POWER_CABLES_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_PCB_FIXED.jpg"> <img src="/assets/images/TINYGS_PCB_FIXED_MEDIUM.jpg"> </a>
	<figcaption>Todos os componentes fixados dentro da caixa.</figcaption>
</figure>

######  Baixe o firmware.

Depois de verificar a conexão de energia (normalmente os módulos vêm com algum tipo de firmware de teste, então quando a energia é conectada, alguns dados aparecerão na tela), conecte o módulo LoRa a um computador usando um cabo USB e siga os passos da [wiki do TinyGS](https://github.com/G4lile0/tinyGS/wiki).

<figure>
	<a href="/assets/images/LORA_GROUND_STATION_FW.jpg"> <img src="/assets/images/LORA_GROUND_STATION_FW_MEDIUM.jpg"> </a>
	<figcaption>TinyGS firmware instalado!</figcaption>
</figure>

###### Colocação da antena.

A antena deve ser colocada onde há a visão mais clara do céu (no telhado ou em um poste longo) e longe de paredes ou estruturas metálicas. Em algumas casas, isso não é possível, então muitos testes nas janelas devem ser realizados para obter o melhor resultado.

Para instalação externa, selle a segunda prensa cabo com uma peça de borracha, envole algum fita auto fusão em torno das partes metálicas da antena e aplique um pouco de silicone selante de cura neutra sobre os parafusos. Evite usar silicone selante ácido (aquele que cheira a vinagre) pois ele oxida parafusos e partes metálicas.


###### Resultados

Devido às condições logísticas específicas deste teste, não foi possível acessar o telhado e não foi possível instalar estruturas permanentes fora das janelas, então foi testada a seguinte configuração: a caixa receptor seria colocada dentro e uma antena temporária com suporte magnético seria colocada fora.

A antena foi adquirida em uma loja local sem nenhuma otimização ou ajuste. O teste foi realizado em Cali, Colômbia, e a transmissão de maior alcance foi recebida do satélite [NORBY](https://tinygs.com/satellite/Norbi) sobre Arequipa, Peru. A distância é de cerca de 2265 Km em linha de vista, nada mal para um receptor de satélite montado em casa, com um orçamento de aproximadamente 40 EUR e sem necessidade de ajuste.


<figure class="third">
	<a href="/assets/images/TINYGS_WINDOW_SETUP.jpg"> <img src="/assets/images/TINYGS_WINDOW_SETUP_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_WINDOW_ANTENNA.jpg"> <img src="/assets/images/TINYGS_WINDOW_ANTENNA_MEDIUM.jpg"> </a>
	<a href="/assets/images/TYNYGS_ANTENNA_RECEPTION.jpg"> <img src="/assets/images/TYNYGS_ANTENNA_RECEPTION_MEDIUM.jpg"> </a>
	<figcaption>Estação terrena funcionando.</figcaption>
</figure>

###### Variants.

A portable version of the ground station has been developed, it uses a smaller enclosure and is powered by a battery. It was designed to be a temporary-mobile station which connects to a mobile phone via WiFi. It uses a 3.2v [LiFePo4](https://es.wikipedia.org/wiki/Bater%C3%ADa_de_litio-ferrofosfato) battery, therefore no voltage regulator was required, the battery is connected directly to the 3.3v power pin of the LoRa module

The same hardware (fixed or mobile versions) could be used for another type of projects, such as [aprs.fi](https://aprs.fi/), which is of particular interest to amateur radio operators. The hardware is 100% compatible and only requires a [firmware change](https://github.com/lora-aprs/LoRa_APRS_iGate)


<figure class="third">
	<a href="/assets/images/TINYGS_PORTABLE_PCB.jpg"> <img src="/assets/images/TINYGS_PORTABLE_PCB_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_PORTABLE_WIRED.jpg"> <img src="/assets/images/TINYGS_PORTABLE_WIRED_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_PORTABLE_FW.jpg"> <img src="/assets/images/TINYGS_PORTABLE_FW_MEDIUM.jpg"> </a>
	<figcaption>Detail of portable ground station</figcaption>
</figure>

| Optional components for mobile version| Buy link | Datasheet           |
| ------------ | ------ | ------------------------------------------------------------ |
| Generic 83x58x33mm waterproof enclosure box | [buy it](https://s.click.aliexpress.com/e/_Ad6Gxn) | [AK10019-A1.pdf](/assets/pdf/AK10019-A1.pdf) |
| AA Battery holder for PCB | [buy it](https://s.click.aliexpress.com/e/_A0wUdR) | [BH311.pdf](/assets/pdf/BH311.pdf) |
| LiFePo4 3.2V 14500 AA Rechargeable battery| [buy it](https://s.click.aliexpress.com/e/_Asl8pn) | [Lifepo4-3.2V-14500-Rechargeable-battery-AA.pdf](/assets/pdf/Lifepo4-3.2V-14500-Rechargeable-battery-AA.pdf) |


| Printed Circuit Board | Buy link | Source files repository  |
| --------------------------------- | ---------------- | ------------------------------- |
| Prototype circuit board for 83x58mm enclosure | [buy it](https://www.pcbway.com/project/shareproject/mcu_proto_83x58mm_16815998.html) | [mcu-proto-83x58mm](https://github.com/galopago/misistemote/tree/main/mcu-proto-83x58mm) |


