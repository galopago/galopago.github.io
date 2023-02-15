---
title: "Câmera Wi-Fi com colheita solar"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - portugues
tags:
  - AN006
  - Solar
  - ESP32
header:
     teaser: "/assets/images/ENERGY_HARVESTING_CAMERA_TEASER.jpg"
---

Um módulo [ESP32-CAM](https://www.arducam.com/esp32-machine-vision-learning-guide/) é um dispositivo de baixo custo baseado no módulo ESP32-S, em um sensor de imagem [OV2640](https://www.ourpcb.com/ov2640.html) e em um slot de Micro SD. O módulo não foi projetado para baixo consumo de energia, no entanto, após algumas alterações, o consumo de energia pode ser reduzido a um nível que seja viável por períodos curtos, alimentado por energia solar. O projeto apresentado aqui é uma plataforma de experimentação robusta, resistente a poeira e à água, usando componentes comerciais de prateleira. Ideal para uso externo.

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_MEDIUM.jpg"> </a>
	<figcaption>A câmera Wi-Fi com coleta de energia solar está pronta para ser colocada ao ar livre.</figcaption>
</figure>

Componente chave: [ESP 32 CAM](https://s.click.aliexpress.com/e/_Dde4rkL)
{: .notice--danger}


<figure>
	<a href="/assets/images/solar_wificamera_wires.png"> <img src="/assets/images/solar_wificamera_wires.png"> </a>
	<figcaption>Diagrama simplificado</figcaption>
</figure>

##### Redução do consumo de energia

O ESP32-CAM não foi projetado para ser um dispositivo de baixo consumo de energia. Sem modificações, a corrente de sono profundo medida foi de 2,8 mA, deixando muito a desejar.

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_POWER.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_POWER_MEDIUM.jpg"> </a>
	<figcaption>Medição da corrente de sono profundo sem modificações. </figcaption>
</figure>

Algumas [pessoas já se aventuraram](https://brettbeeson.com.au/mini-battery-and-solar-powered-timelapse-camera/) nas seguintes modificações na Internet:

* Remover o regulador de tensão de 5 V para 3 V, a câmera será alimentada diretamente por uma bateria de 3,2 V LiFePO4.
* Quebrar a trilha que alimenta a câmera a partir de 3,3 V e ligá-la ao [MOSFET Q2](https://github.com/SeeedDocument/forum_doc/blob/master/reg/ESP32_CAM_V1.6.pdf), que liga os reguladores de tensão de 2,8 V e 1,2 V.
* Remover o led embarcado e ligar o GPIO33 ao pino de 5 V (este pino já está isolado após a remoção do regulador) para usá-lo externamente.

Essas modificações reduziram a corrente em modo de sono profundo para 0,8 mA, o que é escandaloso para um dispositivo de baixo consumo, no entanto, é uma melhoria substancial em relação aos 2,8 mA sem modificações.

<figure class="third">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_SWTICH.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_SWTICH_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_NOREGULATORLED.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_NOREGULATORLED_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_LOWPOWER.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_LOWPOWER_MEDIUM.jpg"> </a>
	<figcaption>Modificações e resultado final, fita de poliamida utilizada para proteger fios finos.</figcaption>
</figure>

##### Lista de materiais

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_PARTS.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_PARTS_MEDIUM.jpg"> </a>
	<figcaption>peças utilizadas </figcaption>
</figure>

Caixa à prova d'água para câmera esportiva SJ4000, módulo de colheita de energia BQ25504, painel solar, cartão Micro SD.

| Componente        | Ligação do compra | Folha de dados                                   |
| ----------------- | ----------------- | ----------------------------------------------- |
| ESP32-CAM         | [Compre aqui](https://s.click.aliexpress.com/e/_Dde4rkL) | [esp-32-cam.pdf](/assets/pdf/esp-32-cam.pdf) |
| Caixa à prova d'água para câmera esportiva SJ4000 | [Compre aqui](https://s.click.aliexpress.com/e/_DFtVPpl) | [sj-4000-sport-cam-waterproof-case.pdf](/assets/pdf/sj-4000-sport-cam-waterproof-case.pdf) |
| módulo de colheita de energia BQ25504 |[Compre aqui](https://s.click.aliexpress.com/e/_DDgPnXv)|[bq25504-energy-harvesting-module.pdf](/assets/pdf/bq25504-energy-harvesting-module.pdf)|
| painel solar 39.5x39.5 mm | [Compre aqui](https://s.click.aliexpress.com/e/_DCzYmzh) | [solar-panel-39-5x39-5.pdf](/assets/pdf/solar-panel-39-5x39-5.pdf)|
| painel solar 30x25 mm |[Compre aqui](https://s.click.aliexpress.com/e/_DFMaS0r)|[solar-panel-30x25.pdf](/assets/pdf/solar-panel-30x25.pdf)|
| painel solar 53x18 mm |[Compre aqui](https://s.click.aliexpress.com/e/_DCbT3Mb)|[solar-panel-53x18.pdf](/assets/pdf/solar-panel-53x18.pdf)|
| Bateria de 3,2 V LiFePO4 |[Compre aqui](https://s.click.aliexpress.com/e/_DCA8kGr) |[lifepo4-3-2v-10440-rechargeable-battery-aaa.pdf](/assets/pdf/lifepo4-3-2v-10440-rechargeable-battery-aaa.pdf) |
| cartão Micro SD|[Compre aqui](https://s.click.aliexpress.com/e/_De2Jybl)|[micro-sd-card.pdf](/assets/pdf/micro-sd-card.pdf)|
| Diode Schottky 1N5817  |[Compre aqui](https://s.click.aliexpress.com/e/_DewOC9v)|[1n5817.pdf](/assets/pdf/1n5817.pdf)|
| Single AAA battery clip for PCB |[Compre aqui](https://s.click.aliexpress.com/e/_DmApqEj)|[bh-411.pdf](/assets/pdf/bh-411.pdf)|
| resistor kit  SMD 0603 | [Compre aqui](https://s.click.aliexpress.com/e/_DF6FuyR) | [4250-pcs-0603-smd-resistor-kit.pdf](/assets/pdf/4250-pcs-0603-smd-resistor-kit.pdf) |
| Barra De Pinos Fêmea 2.54mm|[Compre aqui](https://s.click.aliexpress.com/e/_eNYVzN)|[FHA3-S1XX.pdf](/assets/pdf/FHA3-S1XX.pdf)|
| Barra De Pinos macho 2.54mm|[Compre aqui](https://s.click.aliexpress.com/e/_eMCUJv)|[PHA1-S3XX.pdf](/assets/pdf/PHA1-S3XX.pdf)|
| Jumper 2 pinos| [Compre aqui](https://s.click.aliexpress.com/e/_DCCHLqX) | [pin-header-jumper-block.pdf](/assets/pdf/pin-header-jumper-block.pdf)|
| Cabo de 30 AWG UL1423 PVDF alta temperatura| [Compre aqui](https://s.click.aliexpress.com/e/_eMiimB) | [UL1423.pdf](/assets/pdf/UL1423.pdf) |
| Fio de cobre esmaltado | [Compre aqui](https://s.click.aliexpress.com/e/_DEHlzoj) | [repair-copper-enamelled-wire.pdf](/assets/pdf/repair-copper-enamelled-wire.pdf) |
| Fita Térmica Poliamida |[Compre aqui](https://s.click.aliexpress.com/e/_Dkf4nOR)|[high-temperature-polyimide-insulation-tape.pdf](/assets/pdf/high-temperature-polyimide-insulation-tape.pdf)|

| Placas de circuito impressas (PCB) | Ligação do compra | Arquivos de origem  |
| --------------------------------- | ---------------- | ------------------------------- |
| Placa PCB protótipo para caixa à prova d'água para câmera esportiva  | [Compre aqui](https://www.pcbway.com/project/shareproject/ESP32_CAM_HOST_BOARD_THAT_FITS_INSIDE_WATERPROOF_SPORTSCAM_HOUSING_d06579a9.html) | [esp32cam-proto-sportcam](https://github.com/galopago/misistemote/tree/main/esp32cam-proto-sportcam) |

| Software | repositório |
| ----------------------- | ---------------- |
| Firmware de exemplo que tira fotos e as envia para um servidor usando HTTP POST. | [download](https://github.com/galopago/esp32cam-upload) |
| Exemplo de servidor em Golang para upload de imagens via HTTP POST. | [download](https://github.com/galopago/golang-upload-server) |

| Componentes opcionais | Ligação do compra | Arquivos de origem |
| ----------------------- | ---------------- | ------------------------------- |
| Conversor USB a TTL 3.3 V 5 V | [Compre aqui](https://s.click.aliexpress.com/e/_Dc9HbCx) | [usb-ttl-converter-3-3v-5v.pdf](/assets/pdf/usb-ttl-converter-3-3v-5v.pdf) |
| Medidor Lux digital LCD | [Compre aqui](https://s.click.aliexpress.com/e/_DkDfxFp) | [digital-lcd-lux-meter.pdf](/assets/pdf/digital-lcd-lux-meter.pdf) |

##### Montagem

A plataforma básica consiste de uma caixa estanque para câmera de esporte e uma placa de circuito impresso com o tamanho apropriado para caber no interio


<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_PLATFORM.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_PLATFORM_MEDIUM.jpg"> </a>
	<figcaption>Componentes da plataforma básica.</figcaption>
</figure>

A caixa proposta é bastante comum, fácil de encontrar e barata. Abre e fecha sem parafusos e possui um ponto de montagem onde diferentes acessórios de montagem podem ser instalados.

A placa de circuito impresso foi projetada para colocar o ESP32-CAM perto da janela onde a lente da câmera seria localizada. O módulo pode ser posicionado em duas orientações diferentes para maximizar a área, dependendo dos componentes selecionados.

Foi adicionado um clipe de bateria AAA, conectores fêmea para conectar/desconectar facilmente o módulo e barra de pinos para programação, porque a placa não possui tal circuito. Além disso, foi adicionado um LED vermelho para fins de depuração.

<figure class="third">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDFRONT.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDFRONT_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDBACK.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDBACK_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_WITHMODULE.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_WITHMODULE_MEDIUM.jpg"> </a>
	<figcaption>Placa com todos os componentes.</figcaption>
</figure>

##### Colhedor de energia

A câmera obtém energia de painéis solares instalados dentro da caixa, o que significa que a área disponível é pequena, por isso é necessário um meio de maximizar a eficiência. Foi usado um módulo coletor baseado no chip [BQ25504](https://www.lab4iot.com/2019/07/29/energy-harvesting-tutorial-with-the-ti-bq25570-part-1/). Este dispositivo aumenta a tensão do painel solar e é capaz de fazer isso com tensões de até 130 mV! Assim, é capaz de fornecer corrente para armazenamento na bateria, mesmo sem a luz direta atingir o painel.

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_HARVESTER.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_HARVESTER_MEDIUM.jpg"> </a>
	<figcaption>Módulo de colheita de energia fixado com fita dupla face.</figcaption>
</figure>

O módulo também funciona como um carregador de bateria com proteção contra sobretensão e subtensão. Para definir os [valores de tensão](https://github.com/galopago/electronic-modules-helper/tree/main/cjmcu-25504), alguns resistores devem ser modificados. O fabricante do módulo fornece uma [planilha](https://www.ti.com/product/BQ25504) para facilitar o processo.

Como o caixa é transparente, é possível colocar alguns painéis solares em vários locais dentro dele e conectá-los em paralelo ou em série. Talvez alguns [diodos](https://www.electronics-tutorials.ws/diode/bypass-diodes.html) sejam necessários para não perder muita eficiência quando alguns painéis estiverem sombreados.

Outra função importante do módulo de colheita de energia é a capacidade de fornecer um SINAL DE OK DE TENSÃO, para que o MCU possa ser mantido no estado de reset quando a tensão da bateria estiver muito baixa para operar.

<figure class="third">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_TWOPANELS.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_TWOPANELS_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDINSTALLED.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDINSTALLED_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BACKPANEL.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BACKPANEL_MEDIUM.jpg"> </a>
	<figcaption>Painéis solares e placa instalados no interior. Use um pedaço de espuma EVA para manter as coisas no lugar.</figcaption>
</figure>

##### Orçamento de energia

Aviso: Alguns dados e procedimentos serão simplificados para obter resultados mais simples e rápidos!
{: .notice--danger}

O ESP32 consome cerca de 200 mA a 3,3 V para enviar dados via Wi-Fi, o que é equivalente a 0,66 W. Um painel solar de 40x40 mm que cabe dentro do invólucro mencionado acima gera cerca de 65 mA a 2 V em pleno sol, o que equivale a 0,13 W.

Com esses dados, fica claro que não é possível usar o ESP32 enviando dados via Wi-Fi continuamente com esse painel, mesmo sob plena luz do sol.

Para lidar com esse problema, duas coisas são necessárias: um elemento de armazenamento e o uso do módulo ESP32 em modo não contínuo (ciclo de trabalho).

O módulo no modo de sono profundo consome cerca de 0,88 mA a 3,3 V, o que equivale a 0,003 W. Supondo 12 horas de luz solar, serão necessários em média 0,006 W por dia apenas para manter o módulo energizado em modo de sono. Se o par painel/coletor puder fornecer em média 4,6% da potência máxima do painel solar em pleno sol, será suficiente para manter o ESP32 energizado em modo de sono profundo por muito tempo (até a degradação da bateria!).

Assumindo 100.000 lux como sol pleno e 100% da potência do painel solar de 40x40 mm como 0,13 W, estima-se que a irradiância média necessária por dia para manter o ESP32 energizado em modo de sono profundo é de cerca de 4600 lux.

##### Quanta energia é necessária para tirar uma foto e enviá-la pela internet?

Depois de acordar de um deep sleep, leva cerca de 4 segundos para o ESP32 tirar uma foto, armazená-la no cartão SD e disponibilizá-la na internet. O consumo médio de energia desses 4 segundos é de 200 mA em 3,3 V. A corrente a ser acumulada por 12 horas é:

Ciclo ESP32:
200 mA x 4 s

É necessário:
? mA x 12 h
? mA x 12 (3600) s
? mA x 43200 s (Aproximando para 40000 para facilitar os cálculos)

fator = 4 S / 40000 S = 0,0001
200 mA * 0,0001 = 10 uA

É necessário uma média de 10 uA por 12 horas para tirar uma foto e enviá-la para um servidor, o que é perfeitamente viável ao ar livre, mesmo em dias nublados.

Encontrando a relação entre Lux e a saída de energia do painel solar de 40x40 mm e 0,13 W.

100.000 Lux => 0,13 W
0,77 Lux => 1 uW

10uA * 3,3V = 33 uW

(0,77 Lux / uW) 33 uW = 25,4 Lux (Aproximando para 26 Lux)

Será necessário uma média diária de 26 Lux para tirar uma foto e enviá-la por Wi-Fi.

Em resumo, para tirar pelo menos uma foto por dia e enviá-la por Wi-Fi, será necessário uma média diária de 4600 Lux + 26 Lux = 4626 Lux. Para duas fotos por dia, será necessário uma média diária de 4652 Lux, e assim por diante.

Se for usado um painel menor, como o de 30x25 mm na frente da câmera, cuja potência é cerca de um quarto do instalado na parte de trás, a irradiância deve ser 4 vezes mais forte.


<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_PANELCOMPARE.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_PANELCOMPARE_MEDIUM.jpg"> </a>
	<figcaption>Solar panel in the front vs. solar panel in the back</figcaption>
</figure>

To use the camera with such a small panel, a lot of light is required, especially direct light.

##### Firmware and Software

The firmware released here does the following things: take a picture and store in the Micro SD card, then send it over Wi-Fi to a server doing a multipart HTTP POST request and then, enters deep sleep for X amount of seconds before starting the cycle again. The code could serve as a starting point in the creation of a more robust application adapted to individual needs.

On the server side, there is a small app written in Golang, which listens HTTP POST requests and receives the images sent by the ESP32-CAM and stores them in a local folder. This app should run on a PC, or a Raspberry Pi in the same LAN of the ESP32-CAM. Due to being a basic starter example, there is no authentication method developed, so it is not recommended for deploying in a public server in the Internet.

To program the module, a USB to TTL serial converter is needed, because the module hasn’t an onboard chip for that task. In addition, GPIO0 should be tied to GND during programming.

GPIO33 was freed from the onboard LED and wired externally. The supplied firmware uses it for debugging, but it may be used for other purposes like:

* ADC for battery voltage measurement
* Set up as an RTC pin to wake up the MCU from deep sleep, i.e., PIR sensor
* Wire to a pushbutton to make local changes without a computer or Wi-Fi connectivity

##### Results

Image quality isn't great, which was expected due to the cost of the module. Quality could be improved, modifying several parameters of the chip depending on the specific lighting conditions. The image shown below was uploaded automatically by the module through Wi-Fi to a Raspberry Pi where the [Golang upload server](https://github.com/galopago/golang-upload-server) was running

<figure class="half">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_TESTRIG.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_TESTRIG_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_TESTPIC.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_TESTPIC_MEDIUM.jpg"> </a>
	<figcaption>Test rig and uploaded picture</figcaption>
</figure>

##### Possible improvements

Since firmware and upload server are very basic examples, there are some tasks proposed to the reader like:

* Wi-Fi manager to set up credentials without reprogramming.
* Implement some form of authentication when communicating with the server.
* A mechanism to change the deep sleep time, image settings, etc. from the server on every picture exchange.
* Develop an RTC-based scheduler to take pictures on specific dates.
* Use of a better Wi-Fi antenna (external to the module, but placed inside the enclosure), and place it in a place with less obstructions. Certain changes are needed in the components near the U.FL connector.
 
