---
title: 'Display OLED 0,96" para montagem em painel com bornes de parafuso'
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - portugues
tags:
  - AN009
  - Prototyping
header:
  teaser: "/assets/images/AN009/PANEL_MOUNT_OLED_DISPLAY_TEASER.jpg"
---

Módulos OLED pequenos parecem intercambiáveis, mas furos de montagem e o recorte do painel necessário para que o mostrador apareça raramente coincidem entre fornecedores. Uma instalação limpa em painel costuma exigir uma janela quadrada precisa mais quatro furos para parafusos. Essas medidas mudam de um módulo para outro.

<figure>
  <a href="/assets/images/AN009/FIG_P0001_1.jpg">
    <img src="/assets/images/AN009/FIG_P0001_1_MEDIUM.jpg">
  </a>
  <figcaption>Diferenças sutis nas distâncias entre mostradores de fabricantes diferentes</figcaption>
</figure>

Este projeto integra um display OLED I2C de 0,96″ bare screen sem módulo de processamento intermediário em uma carcaça de montagem em painel 48×29 mm com [bornes de parafuso](https://dicasdeinstrumentacao.com/montagem-eletricas-com-uso-de-bornes). Monta-se uma única vez entre protótipos sem soldar de novo nem crimpar cabos específicos.

##### Conceito
Instrumentos de painel no formato 48×29 mm compartilham um semi-padrão útil: um recorte retangular, clipes internos e um bisel frontal que esconde bordas imperfeitas. A inspiração veio de medidores DC baratos, incluindo o popular “9 em 1” de tensão/corrente/potência, que já usam duas placas internas.

<figure>
  <a href="/assets/images/AN009/FIG_P0003_1.jpg">
    <img src="/assets/images/AN009/FIG_P0003_1_MEDIUM.jpg">
  </a>
  <figcaption>Voltímetro digital para montagem em painel</figcaption>
</figure>

Depois de procurar um produto pronto que combinasse montagem em painel, display I2C «burro» e bornes robustos, nada apareceu em quantidades de hobby. Como referência usou-se o medidor múltiplo «9 em 1» de tensão, corrente e potência em DC, em carcaça de painel 48×29 mm.

<figure class="third">
  <a href="/assets/images/AN009/FIG_P0004_1.jpg">
    <img src="/assets/images/AN009/FIG_P0004_1_MEDIUM.jpg">
  </a>
  <a href="/assets/images/AN009/FIG_P0004_2.jpg">
    <img src="/assets/images/AN009/FIG_P0004_2_MEDIUM.jpg">
  </a>
  <a href="/assets/images/AN009/FIG_P0004_3.jpg">
    <img src="/assets/images/AN009/FIG_P0004_3_MEDIUM.jpg">
  </a>
  <figcaption>Como é por dentro o medidor 9 em 1</figcaption>
</figure>

Componente chave: [0,96″ OLED 128x64 bare screen I2C.](https://s.click.aliexpress.com/e/_c4oPdlbb?SearchText=0.96%20i2c%20128x64%20oled%20display%20bare%20screen)
{: .notice--danger}

<figure>
  <a href="/assets/images/AN009/PANEL_MOUNT_OLED_DISPLAY.jpg">
    <img src="/assets/images/AN009/PANEL_MOUNT_OLED_DISPLAY_MEDIUM.jpg">
  </a>
  <figcaption>Módulo OLED para montagem em painel montado em carcaça 48x29 mm</figcaption>
</figure>

#### Características principais:
* Hardware open source: [fontes KiCad e Gerbers no GitHub](https://github.com/galopago/panel-mount-oled-display)
* Interface I2C direta (sem MCU na placa)
* Bisel 48×29 mm tolerante a recorte impreciso
* Seis LEDs indicadores 0805 com terminais de ânodo e cátodo independentes
* Bornes de parafuso 3,5 mm de duplo nível para fio rígido, multifilar ou Dupont
* Duas placas empilhadas: soldar uma vez, cabear muitas vezes

#### Lista de materiais

| Componente | Comprar | Datasheet |
| ---------- | ------- | --------- |
| Kit capacitores SMD (0805) | [Comprar](https://s.click.aliexpress.com/e/_c3bMZUIN?SearchText=smd%200805%20capacitor%20kit) | [smd-capacitors.pdf](/assets/pdf/smd-capacitors.pdf) |
| LED SMD (0805) | [Comprar](https://s.click.aliexpress.com/e/_c2vg3QZ7?SearchText=led%20smd%200805) | [smd-led-0805.pdf](/assets/pdf/smd-led-0805.pdf) |
| Diodo SMD 1N4148 | [Comprar](https://s.click.aliexpress.com/e/_c4T1PYI9?SearchText=smd%20led%201n4148%20melf) | [smd-diode-1n4148-melf.pdf](/assets/pdf/smd-diode-1n4148-melf.pdf) |
| Kit resistores SMD (0805) | [Comprar](https://s.click.aliexpress.com/e/_c4T1PYI9?SearchText=smd%200805%20resistor%20kit) | [smd-resistors.pdf](/assets/pdf/smd-resistors.pdf) |
| Header macho 1x8 2,54 mm | [Comprar](https://s.click.aliexpress.com/e/_c3fLPpqv?SearchText=single%20row%20pin%20header%202.54) | [single-row-male-header-2-54-pitch.pdf](/assets/pdf/single-row-male-header-2-54-pitch.pdf) |
| Borne parafuso PCB duplo nível 3,5 mm (2x8) | [Comprar](https://s.click.aliexpress.com/e/_c2vg3QZ7?SearchText=KF128A-3.5) | [pcb-screw-terminal-double-level-3-5.pdf](/assets/pdf/pcb-screw-terminal-double-level-3-5.pdf) |
| Display OLED 0,96″ 128x64 bare screen I2C | [Comprar](https://s.click.aliexpress.com/e/_c4oPdlbb?SearchText=0.96%20i2c%20128x64%20oled%20display%20bare%20screen) | [oled-0-96-i2c-128x64-bare-screen.pdf](/assets/pdf/oled-0-96-i2c-128x64-bare-screen.pdf) |
| Regulador LDO XC6206 3,3 V (SOT-23) | [Comprar](https://s.click.aliexpress.com/e/_c3bMZUIN?SearchText=XC6206P332%20sot%2023) | [xc6206.pdf](/assets/pdf/xc6206.pdf) |

#### Circuitos impressos

| PCB | Arquivos fonte |
| --- | -------------- |
| Placa display (OLED, regulador, LEDs) | [panel-mount-oled-display/display-board](https://github.com/galopago/panel-mount-oled-display/tree/main/display-board) |
| Placa conector (bornes de parafuso) | [panel-mount-oled-display/connector-board](https://github.com/galopago/panel-mount-oled-display/tree/main/connector-board) |

#### Design elétrico
O projeto divide a função entre duas placas ligadas por um header 1×8. Na placa display vão o regulador XC6206 a 3,3 V, a rede de auto-reset do OLED, o acoplamento I2C, alguns capacitores usados pelo conversor interno DC/DC do mostrador e seis LEDs com terminais independentes. A placa conector só encaminha aos bornes de parafuso de duplo nível. Os esquemáticos completos e as notas de projeto estão no [repositório GitHub](https://github.com/galopago/panel-mount-oled-display).

<figure>
  <a href="/assets/images/AN009/SCHEMATIC.png">
    <img src="/assets/images/AN009/SCHEMATIC.png">
  </a>
  <figcaption>Esquemático (placas display e conector)</figcaption>
</figure>

#### Montagem
A montagem manual segue o esquema de duas placas dos medidores “9 em 1”: primeiro soldam-se os componentes SMD nas duas PCBs. Na placa display vão o OLED de cabo flex (0,7 mm, 30 pinos), o XC6206, o auto-reset e os seis LEDs; na placa conector, os bornes de parafuso de duplo nível. O passo mais delicado é soldar o flex da tela com ponta de ferro em T; o resto é solda SMD comum.

<figure class="third">
  <a href="/assets/images/AN009/ASSEMBLY_1.jpg">
    <img src="/assets/images/AN009/ASSEMBLY_1_MEDIUM.jpg">
  </a>
  <a href="/assets/images/AN009/FIG_P0006_2.jpg">
    <img src="/assets/images/AN009/FIG_P0006_2_MEDIUM.jpg">
  </a>
  <a href="/assets/images/AN009/FIG_P0006_3.jpg">
    <img src="/assets/images/AN009/FIG_P0006_3_MEDIUM.jpg">
  </a>
  <figcaption>Montagem de componentes nas duas placas</figcaption>
</figure>

As duas placas unem-se com headers 1×8 e um espaçador entre elas, deixando os bornes acessíveis por um lado.

<figure>
  <a href="/assets/images/AN009/ASSEMBLY_2.jpg">
    <img src="/assets/images/AN009/ASSEMBLY_2_MEDIUM.jpg">
  </a>
  <figcaption>Placas display e conector empilhadas com conectores header e espaçadores</figcaption>
</figure>

A carcaça vem de um medidor de painel 48×29 mm (o mais barato que achar): retira-se a eletrônica original e reaproveita-se o frontal, inclusive o acrílico se servir, ou uma lente nova escura e translúcida de até 1 mm. O conjunto de placas encaixa na carcaça; as abas internas seguram o módulo sem parafusos extras no painel.

<figure>
  <a href="/assets/images/AN009/ASSEMBLY_3.jpg">
    <img src="/assets/images/AN009/ASSEMBLY_3_MEDIUM.jpg">
  </a>
  <figcaption>Conjunto de placas instalado dentro da carcaça</figcaption>
</figure>

#### Software
O módulo não inclui firmware. Qualquer host com I2C (Arduino, RPi Pico, ESP32, etc.) pode controlar o display compatível com SSD1306 e os seis LEDs pelos bornes de parafuso.

### Personalização
O projeto pode ser adaptado em alimentação e no uso dos LEDs indicadores. Também há um resistor que pode ser trocado de posição para escolher entre duas orientações possíveis do barramento I2C.

##### Fonte de alimentação
O XC6206 na placa gera 3,3 V para o OLED a partir dos bornes VCC/GND. Alimentar dentro das especificações do regulador e do display (tipicamente 3,3-5 V na entrada, conforme a variante de XC6206 montada).

##### Expansão
Seis LEDs 0805 têm terminais de ânodo e cátodo independentes, permitindo indicadores em circuitos ou terras diferentes. A fileira inferior de bornes é mais apertada para conectores Dupont, mas fica firme depois de encaixada.

<figure>
  <a href="/assets/images/AN009/FIG_P0012_1.jpg">
    <img src="/assets/images/AN009/FIG_P0012_1_MEDIUM.jpg">
  </a>
  <figcaption>Dois LEDs acesos: esquerda na posição central e direita na posição inferior</figcaption>
</figure>

##### Aplicação de exemplo
Montar o módulo em um painel ou caixa de instrumentação e ligar I2C (SCL, SDA, VCC, GND) do microcontrolador aos bornes de parafuso. Conectar um ou mais pares de LEDs a sinais de status (alimentação, alarme, modo, etc.) com retornos independentes se necessário. Ao encerrar o projeto, desparafusar os cabos e reutilizar o mesmo conjunto no próximo protótipo.

<figure class="third">
  <a href="/assets/images/AN009/SAMPLE_1.jpg">
    <img src="/assets/images/AN009/SAMPLE_1_MEDIUM.jpg">
  </a>
  <a href="/assets/images/AN009/SAMPLE_2.jpg">
    <img src="/assets/images/AN009/SAMPLE_2_MEDIUM.jpg">
  </a>
  <a href="/assets/images/AN009/SAMPLE_3.jpg">
    <img src="/assets/images/AN009/SAMPLE_3_MEDIUM.jpg">
  </a>
  <figcaption>Detalhe do recorte quadrado para montagem do mostrador</figcaption>
</figure>

## Componentes opcionais:

| Componente | Comprar | Datasheet |
| ---------- | ------- | --------- |
| Medidor de painel 48x29 mm (carcaça doadora) | [Comprar](https://s.click.aliexpress.com/e/_c3bMZUIN?SearchText=panel%20digital%20voltmeter) | [48x29mm-digital-voltmeter.pdf](/assets/pdf/48x29mm-digital-voltmeter.pdf) |
| Ponta de solda em T (cabo flex) | [Comprar](https://s.click.aliexpress.com/e/_c3bMZUIN?SearchText=Soldering%20Iron%20T%20Tip%20T-head%20Copper%20T-Tips%20%2B%20Rubber) | [t-type-soldering-tip-60w.pdf](/assets/pdf/t-type-soldering-tip-60w.pdf) |
| Chapa acrílica translúcida 1 mm | [Comprar](https://s.click.aliexpress.com/e/_c3fLPpqv?SearchText=Translucent%20%20Acrylic%20Plexiglass%201mm) | [translucent-acrylic-plexiglass-1mm.pdf](/assets/pdf/translucent-acrylic-plexiglass-1mm.pdf) |

## Notas práticas:
No fim das contas, a ideia era simples: soldar a tela uma vez e poder mover o módulo de um protótipo para outro sem voltar ao alicate de crimpagem nem ao ferro de solda. Aperta os fios, solta, pronto. Se você muda o cabeamento com frequência na bancada ou dentro de uma caixa de instrumentação, essa praticidade compensa.

O que mais consome tempo não é a eletrônica, e sim a carcaça. Achar uma carcaça vazia 48×29 mm em quantidade de hobby é quase impossível. O caminho usual é comprar o medidor mais barato que aparecer e esvaziá-lo. Para a janela frontal, provou-se de tudo: a lâmina vermelha do voltímetro original escurece demais o OLED; verdes e azuis também não ajudaram. Ficamos com a lâmina cinza translúcida do multímetro doador (ou acrílico escuro de até 1 mm se você cortar a sua).

Um detalhe que acalma: o furo no painel não precisa sair perfeito. O bisel esconde cantos irregulares e as abas internas seguram o módulo sem parafusos extras. Na fileira inferior dos terminais os Dupont entram justos (não é a fileira mais confortável), mas, depois de encaixados, aguentam se puxar o cabo.
