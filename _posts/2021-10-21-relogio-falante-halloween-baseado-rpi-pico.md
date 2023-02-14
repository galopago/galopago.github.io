---
title: "Relógio falante de Halloween baseado no Rpi Pico"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - portugues
tags:
  - AN003
  - RPI PICO  
  - C/C++ SDK
  - CIRCUITPHYTON
header:
     teaser: "/assets/images/HALLOWEEN_TALKING_CLOCK_TEASER.jpg"
---
Relógio falante de Halloween que toca sons a cada hora cheia. Apenas alguns componentes externos (fáceis de encontrar e soldar) são necessários. A placa de uma face pode ser fabricada em casa. Projeto altamente personalizável que envolve múltiplas áreas de conhecimento ([STEAM](https://en.wikipedia.org/wiki/STEAM_fields)): Eletrônica, programação, marcenaria, artes, etc.

<figure>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_MEDIUM.jpg"> </a>
	<figcaption>Relógio personalizado pendurado na parede.</figcaption>
</figure>

Componente chave: [Movimento de relógio de quartzo com gatilho](https://s.click.aliexpress.com/e/_AfCGIL)
{: .notice--danger}


##### Conceito:

Um grande número de relógios de parede musicais no mercado carecem da possibilidade de mudar os sons originais. Um relógio com essa capacidade pode ser construído com um sistema embarcado. Mas qual escolher? O Raspberry Pi Pico foi escolhido por 3 razões:

Não é necessário instalar software para o download inicial do firmware
A memória onboard de 2 MegaBytes de flash pode armazenar alguma quantidade de sons sem precisar de memória externa
Pode ser alimentado por 2 baterias AA sem componentes adicionais.

A Rpi Pico consome cerca de 1,6 mA no seu modo de consumo mais baixo (sono profundo). Pode parecer pouco, mas é alto demais para um circuito alimentado por bateria, pois elas se esgotarão em cerca de dois meses. Por esse motivo, um circuito de alimentação externo que pode desligar completamente a placa foi adicionado. Depois disso, o consumo de energia caiu para 70 uA, então as baterias durarão por um ano.

O Rpi Pico age como armazenador e tocador de som. Para exibir o tempo e gerar um sinal de "hora", foi usado um movimento de relógio de quartzo com gatilho. Ao combinar esses dois elementos, nasceu um relógio falante de som.


#### Recursos principais:

* Duas versões da mesma aplicação (quase): Uma desenvolvida em [CircuitPython](https://www.adafruit.com/circuitpython) e a outra no [C/C++ SDK](https://github.com/raspberrypi/pico-sdk).
* Compatível com os sistemas operacionais mais comuns.
* Não é necessário instalar aplicativos para o download inicial do firmware.
* Não é necessário recompilar o código (na aplicação desenvolvida em CircuitPython) para mudar os sons.
* Até 3 anos em modo de standby usando uma par de pilhas AA.
* Componentes fáceis de encontrar e soldar.


<figure>
	<a href="/assets/images/rpi_pico_sound_clock.png"> <img src="/assets/images/rpi_pico_sound_clock.png"> </a>
	<figcaption>Diagrama simplificado do circuito de energia</figcaption>
</figure>

##### Software:

Assim que ligado, o Rpi Pico coloca um nível baixo no GPIO que está conectado ao circuito de alimentação para mantê-lo ligado, então decide qual arquivo deve ser tocado e, após o som terminar, é colocado um nível alto no GPIO desligando o Pico. Além disso, é lida uma sensibilidade à luz para não tocar som quando estiver escuro (à noite).

Os arquivos de som são reproduzidos sequencialmente, um por um a cada ligada. Um ponteiro para o próximo arquivo é armazenado na memória não volátil, cuidado ao modificar o programa para manter a escrita mínima.

###### Peculiaridades da versão C/C++ SDK:

Os sons a serem reproduzidos devem ser convertidos primeiro para o formato WAV de 16 bits mono a 44100 Hz, em seguida convertidos para arrays C[] antes da compilação. A aplicação usa uma PWM via saída digital e interrupções para reproduzir sons.

O programa começa a ser executado logo após a ligação. A principal desvantagem do aplicativo por enquanto é que ele só suporta arquivos .WAV, que são grandes e não podem ser alterados sem recompilar o código.


###### Peculiaridades da versão CircuitPython:

Sons a serem tocados devem ser convertidos para o formato MP3 mono, o aplicativo usa módulos audiomp3 e audiopwmio para saída de áudio de um pino digital (PWM). Esses arquivos são armazenados no sistema de arquivos fornecido pelo CP, então a sua modificação é simples, basta arrastar e soltar.

Arquivos MP3 podem armazenar cerca de 10 vezes mais tempo de som do que WAV para o mesmo tamanho de arquivo, no entanto, a execução do tempo de execução do CircuitPython leva mais de um segundo após a ligar, então provavelmente não será uma coisa boa para qualquer tipo de aplicação final.


##### Hardware:
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

Para construir o relógio de parede, escolha uma placa ou disco feito de plástico ou madeira, com diâmetro suficiente para esconder o movimento do relógio e a placa de som. Fixe todos os componentes eletrônicos e, em seguida, acessórios decorativos, como luzes LED. Finalize com a pintura.

<figure class="third">
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK_MECHANISM.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_MECHANISM_MEDIUM.jpg"> </a>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK_COMPONENTS.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_COMPONENTS_MEDIUM.jpg"> </a>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK_BACK.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_BACK_MEDIUM.jpg"> </a>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK_FRONT.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_FRONT_MEDIUM.jpg"> </a>
	<figcaption>Movimento de relógio com contatos externos, elementos decorativos, verso finalizado e frente finalizada.</figcaption>
</figure>

Para ajustar a hora, retire todas as baterias e as mãos do relógio (hora, minuto, segundo). Gire lentamente a chave de ajuste do relógio até ouvir um som de "clique". Coloque todas as mãos do relógio apontando para 12 horas. Coloque as baterias. Os sons podem ser deslocados pressionando o interruptor de botão momentâneo na placa.


#### Lista de materiais

| Componente         | Ligação do compra! | Folha de dados                                        |
| -------- | ------ | ------------------------------------------------------------ |
| Barra de pinos fêmea  2.54mm | [Compre aqui](https://s.click.aliexpress.com/e/_eNNciZ) | [FHA3-S1XX.pdf](/assets/pdf/FHA3-S1XX.pdf) |
| barra de pinos macho 2.54mm | [Compre aqui](https://s.click.aliexpress.com/e/_eMCUJv) | [PHA1-S3XX.pdf](/assets/pdf/PHA1-S3XX.pdf) |
| 1/4W 1% TH Resistors | [Compre aqui](https://s.click.aliexpress.com/e/_eMCbH1) | [MGR-SERIES.pdf](/assets/pdf/MGR-SERIES.pdf) |
| Botão Microchave Push Button 6x6mm | [Compre aqui](https://s.click.aliexpress.com/e/_eKd4YV) | [TS-1301.pdf](/assets/pdf/TS-1301.pdf) |
| Raspberry Pi Pico | [Compre aqui](https://s.click.aliexpress.com/e/_AXStdl) | [pico-datasheet.pdf](/assets/pdf/pico-datasheet.pdf) |
| Suporte Caixa para 2 Pilhas AA para PCB | [Compre aqui](https://s.click.aliexpress.com/e/_AoI96B) | [Comfortable_Catalog.pdf](/assets/pdf/Comfortable_Catalog.pdf) |
| 8 Ohm Alto-falante 29 mm 0.25W | [Compre aqui](https://s.click.aliexpress.com/e/_ATihaX) | [DXP29W-A.pdf](/assets/pdf/DXP29W-A.pdf) |
| MOSFET 2N7000 | [Compre aqui](https://s.click.aliexpress.com/e/_9j8Bgx) | [NDS7002A-D.pdf](/assets/pdf/NDS7002A-D.pdf) |
| TRANSISTOR BIPOLAR NPN 2N2222A | [Compre aqui](https://s.click.aliexpress.com/e/_ANvtiX) | [P2N2222A-D.pdf](/assets/pdf/P2N2222A-D.pdf) |
| TH Capacitor eletrolítico radial | [Compre aqui](https://s.click.aliexpress.com/e/_9gn4vh) | [TS13DE-CD110X.pdf](/assets/pdf/TS13DE-CD110X.pdf) |
| TH Capacitor ceramico disco | [Compre aqui](https://s.click.aliexpress.com/e/_Apm6Pd) | [TS15.pdf](/assets/pdf/TS15.pdf) |
| movimento de relógio de quartzo com gatilho | [Compre aqui](https://s.click.aliexpress.com/e/_AfCGIL) | [12888SE_TRIGGER_CLOCK_MOVEMENT.pdf](/assets/pdf/12888SE_TRIGGER_CLOCK_MOVEMENT.pdf) |
| Wall Clock hooks DIY | [Compre aqui](https://s.click.aliexpress.com/e/_A0tg3V) | [wall_clock_hook.pdf](/assets/pdf/wall_clock_hook.pdf) |
| Fotodiodo de luz visível TEPT5700 | [Compre aqui](https://s.click.aliexpress.com/e/_AM6wDK) | [tept5700.pdf](/assets/pdf/tept5700.pdf) |
| Fio De Fada Led a bateria | [Compre aqui](https://s.click.aliexpress.com/e/_9vylbl) | [LED_Copper_Wire_Battery_Box.pdf](/assets/pdf/LED_Copper_Wire_Battery_Box.pdf) |


#### Placa de circuito impresso

| Placas de circuito impressas (PCB)    | Ligação do compra| Arquivos de origem             | 
| -------- | -----|------------------------------------------------------- |
|Placa de som (diretório de hardware) |[Compre aqui](https://www.pcbway.com/project/shareproject/Talking_wall_clock_board_for_Raspberry_Pi_Pico_399ca59f.html) |[SINSONTE](https://github.com/galopago/SINSONTE)           |



#### Software

| Software    | Source files                                         | 
| -------- | ------------------------------------------------------------ |
| Firmware CircuitPython & SDK C/C++ (diretório de software)   | [SINSONTE](https://github.com/galopago/SINSONTE)           |

 

## Componentes opcionais:

| Componente         | Ligação do compra | Folha de dados                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| Broca Escalonada bit 3 a 20 mm  | [shop now](https://s.click.aliexpress.com/e/_AalUrz)     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
