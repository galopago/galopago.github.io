---
title: "Bicho falante ativado por movimento baseado no Rpi Pico"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - portugues
tags:
  - AN004
  - RPI PICO  
  - C/C++ SDK
  - CIRCUITPHYTON
header:
     teaser: "/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_TEASER.jpg"
---
Bicho de Halloween que toca sons quando é detectado movimento de pessoas. São necessários apenas alguns componentes externos (fáceis de encontrar e soldar). A placa de uma só face pode ser fabricada em casa. Projeto muito personalizável que envolve múltiplas áreas de conhecimento ([STEAM](https://en.wikipedia.org/wiki/STEAM_fields)): Eletrônica, programação, marcenaria, artes, etc.


<figure>
	<a href="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER.jpg"> <img src="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_MEDIUM.jpg"> </a>
	<figcaption>Bicho personalizado pendurado na parede</figcaption>
</figure>

Componente chave: [AM312 Mini IR Pyroelectric Infrared Sensor](https://s.click.aliexpress.com/e/_9wbM0t)
{: .notice--danger}


##### Conceito:

O projeto é uma pequena modificação do [relógio falante](https://galopago.github.io/portugues/relogio-falante-halloween-baseado-rpi-pico/) , mas neste caso, a energia é ativada por um sensor PIR. Quando uma pessoa se move perto do bicho, um som aleatório é tocado. O Raspberry Pi Pico foi escolhido pelas 3 seguintes razões:

* Não é necessário instalar software para o download inicial do firmware
* A memória onboard de 2 MegaBytes de flash pode armazenar alguma quantidade de sons sem exigir memória externa
* Pode ser alimentado por 2 baterias AA sem componentes adicionais

Rpi Pico consome cerca de 1,6 mA em seu modo de baixo consumo de energia (sono profundo). Parece pouco, mas é muito alto para um circuito alimentado por bateria, pois eles se esgotarão em cerca de dois meses. Por essa razão, um circuito de alimentação externo que pode desligar completamente a placa foi adicionado. Depois disso, o consumo de energia caiu para 70 uA, então as baterias durarão por um ano.

O Rpi Pico atua como armazenador e reproductor de som.

#### Recursos principais:

* Duas versões da mesma aplicação (quase): Uma desenvolvida em CircuitPython e a outra no C/C++ SDK.
* Compatível com os sistemas operacionais mais comuns.
* Não é necessário instalar aplicativos para o download inicial do firmware.
* Não é necessário recompilar o código (na aplicação desenvolvida em CircuitPython) para mudar os sons.
* Até 3 anos em modo de standby usando uma par de pilhas AA.
* Componentes fáceis de encontrar e soldar.


<figure>
	<a href="/assets/images/rpi_pico_sound_motion.png"> <img src="/assets/images/rpi_pico_sound_motion.png"> </a>
	<figcaption>Diagrama simplificado do circuito de energia</figcaption>
</figure>

##### Software:

Assim que ligado, o Rpi Pico coloca um nível baixo no GPIO que está conectado ao circuito de alimentação para mantê-lo ligado, então decide qual arquivo deve ser tocado e, após o som terminar, é colocado um nível alto no GPIO desligando o Pico. Além disso, é lida uma sensibilidade à luz para não tocar som quando estiver escuro (à noite).

Arquivos de som são reproduzidos aleatoriamente, um por um a cada ligação

###### Peculiaridades da versão C/C++ SDK

Os sons a serem reproduzidos devem ser convertidos primeiro para o formato WAV de 16 bits mono a 44100 Hz, em seguida convertidos para arrays C[] antes da compilação. A aplicação usa uma PWM via saída digital e interrupções para reproduzir sons.

O programa começa a ser executado logo após a ligação. A principal desvantagem do aplicativo por enquanto é que ele só suporta arquivos .WAV, que são grandes e não podem ser alterados sem recompilar o código.

###### Peculiaridades da versão CircuitPython:

Sons a serem tocados devem ser convertidos para o formato MP3 mono, o aplicativo usa módulos audiomp3 e audiopwmio para saída de áudio de um pino digital (PWM). Esses arquivos são armazenados no sistema de arquivos fornecido pelo CP, então a sua modificação é simples, basta arrastar e soltar.

Arquivos MP3 podem armazenar cerca de 10 vezes mais tempo de som do que WAV para o mesmo tamanho de arquivo, no entanto, a execução do tempo de execução do CircuitPython leva mais de um segundo após a ligar, então provavelmente não será uma coisa boa para qualquer tipo de aplicação final.

##### Hardware:
External components are part of one of the three different functionalities:

Componentes externos fazem parte de uma das três diferentes funcionalidades:

* __On/Off__ : O circuito é composto por um MOSFET, o terminal de dreno conectado a 3V3_EN e o terminal de fonte conectado a GND. Conectados à porta há 2 elementos: um capacitor para o solo e um resistor para V+. O circuito funciona da seguinte maneira:

* Passo 1: O capacitor é totalmente carregado, ligando o MOSFET e ligando 3V3_EN ao solo, desligando totalmente a placa Rpi Pico.

* Passo 2: O capacitor é rapidamente descarregado pelo breve fechamento dos contatos do movimento do relógio, desligando o MOSFET e ligando a Rpi Pico. A primeira coisa a fazer após a ligar é manter o capacitor descarregado com a ajuda de uma saída GPIO em nível baixo.

* Passo 3: Enquanto o som é reproduzido, o nível baixo na GPIO é mantido. Uma vez que o som termina, a saída GPIO é ligada em nível alto, fazendo com que o MOSFET ligue novamente, desligando a Rpi Pico até o próximo fechamento de Interruptor.

* __Amplificador de áudio__: amplificador de uma etapa, com um único transistor NPN alimenta um pequeno alto-falante de 8 Ohms. Há também um filtro RC passa-baixa de entrada para suavizar o ruído devido à saída PWM.

* __Detecção de dia/noite__: Sensor de luz visível para evitar a reprodução de sons à noite. Conectado a um pino ADC.


##### Montagem da placa:

A Rpi Pico, alto-falante, sensor de luz e contatos de relógio podem ser soldados diretamente à placa para obter um perfil de altura muito pequeno ou adicionar barra de pinos para uma opção mais flexível.

A placa de de camada única pode ser gravada em casa. Há algumas pad GPIO livres para experimentação e também furos de montagem perto das cantos.

<figure class="third">
	<a href="/assets/images/SINSONTE_BOARD_HOMEMADE.jpg"> <img src="/assets/images/SINSONTE_BOARD_HOMEMADE_MEDIUM.jpg"> </a>
	<a href="/assets/images/SINSONTE_BOARD_NOCONNECTOR.jpg"> <img src="/assets/images/SINSONTE_BOARD_NOCONNECTOR_MEDIUM.jpg"> </a>
	<a href="/assets/images/SINSONTE_BOARD_WITHCONNECTORS.jpg"> <img src="/assets/images/SINSONTE_BOARD_WITHCONNECTORS_MEDIUM.jpg"> </a>
	<figcaption>Placa impressa gravada em casa, exemplo de soldagem direta e finalizada com barra de pinos.</figcaption>
</figure>

Para construir o bicho, escolha uma placa ou disco feito de plástico ou madeira, com diâmetro suficiente para esconder o placa de som. Fixe todos os componentes eletrônicos e, em seguida, acessórios decorativos, como luzes LED. Finalize com a pintura.


<figure class="third">
	<a href="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_SENSOR.jpg"> <img src="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_SENSOR_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_COMPONENTS.jpg"> <img src="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_COMPONENTS_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_BACK.jpg"> <img src="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_FRONT.jpg"> <img src="/assets/images/MOTION_ACTIVATED_TALKING_CRITTER_FRONT_MEDIUM.jpg"> </a>
	<figcaption>Sensor PIR com transistor, forma de bicho em madeira, traseira e frente acaba</figcaption>
</figure>

Um transistor NPN foi adicionado ao sensor PIR para invertê-lo sinal para mantê-lo compatível com o circuito original.


#### Lista de materiais

| Componente         | Ligação do compra | Folha de dados                                          |
| -------- | ------ | ------------------------------------------------------------ |
| Barra de pinos fêmea 2.54mm | [Compre aqui](https://s.click.aliexpress.com/e/_eNNciZ) | [FHA3-S1XX.pdf](/assets/pdf/FHA3-S1XX.pdf) |
| Barra de pinos macho  2.54mm | [Compre aqui](https://s.click.aliexpress.com/e/_eMCUJv) | [PHA1-S3XX.pdf](/assets/pdf/PHA1-S3XX.pdf) |
| 1/4W 1% TH Resistors | [Compre aqui](https://s.click.aliexpress.com/e/_eMCbH1) | [MGR-SERIES.pdf](/assets/pdf/MGR-SERIES.pdf) |
| Botão Microchave Push Button 6x6mm | [Compre aqui](https://s.click.aliexpress.com/e/_eKd4YV) | [TS-1301.pdf](/assets/pdf/TS-1301.pdf) |
| Raspberry Pi Pico | [shop now](https://s.click.aliexpress.com/e/_AXStdl) | [pico-datasheet.pdf](/assets/pdf/pico-datasheet.pdf) |
| Suporte Caixa para 2 Pilhas AA para PCB | [Compre aqui](https://s.click.aliexpress.com/e/_AoI96B) | [Comfortable_Catalog.pdf](/assets/pdf/Comfortable_Catalog.pdf) |
| 8 Ohm Alto-falante 29 mm 0.25W | [Compre aqui](https://s.click.aliexpress.com/e/_ATihaX) | [DXP29W-A.pdf](/assets/pdf/DXP29W-A.pdf) |
| MOSFET 2N7000 | [shop now](https://s.click.aliexpress.com/e/_9j8Bgx) | [NDS7002A-D.pdf](/assets/pdf/NDS7002A-D.pdf) |
| TRANSISTOR BIPOLAR NPN 2N2222A | [Compre aqui](https://s.click.aliexpress.com/e/_ANvtiX) | [P2N2222A-D.pdf](/assets/pdf/P2N2222A-D.pdf) |
| TH Capacitor eletrolítico radial | [Compre aqui](https://s.click.aliexpress.com/e/_9gn4vh) | [TS13DE-CD110X.pdf](/assets/pdf/TS13DE-CD110X.pdf) |
| TH Capacitor ceramico disco | [Compre aqui](https://s.click.aliexpress.com/e/_Apm6Pd) | [TS15.pdf](/assets/pdf/TS15.pdf) |
| Fotodiodo de luz visível TEPT5700 | [Compre aqui](https://s.click.aliexpress.com/e/_AM6wDK) | [tept5700.pdf](/assets/pdf/tept5700.pdf) |
| AM312 Mini Pir Sensor De Movimento | [Compre aqui](https://s.click.aliexpress.com/e/_9wbM0t) | [AS312.pdf](/assets/pdf/AS312.pdf) |


#### Placa de circuito impresso

| Placas de circuito impressas (PCB)    | | Arquivos de origem                                        | 
| -------- | -----------|------------------------------------------------- |
| Placa de som (diretório de hardware) |[Compre aqui](https://www.pcbway.com/project/shareproject/Talking_wall_clock_board_for_Raspberry_Pi_Pico_399ca59f.html)| [SINSONTE](https://github.com/galopago/SINSONTE)           |



#### Software

| Software    | Arquivos de origem                                         | 
| -------- | ------------------------------------------------------------ |
| Firmware CircuitPython & SDK C/C++ (diretório de software)	   | [SINSONTE](https://github.com/galopago/SINSONTE)           |

 

## Componentes opcionais:

| Componente         | Ligação do compra | Folha de dados                                       | 
| -------- | ------ | ------------------------------------------------------------ |
| Broca Escalonada bit 3 a 20 mm  | [Compre aqui](https://s.click.aliexpress.com/e/_AalUrz)     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
