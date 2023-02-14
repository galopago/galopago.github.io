---
title: "Pedal USB baseado em Rpi Pico"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - portugues
tags:
  - AN002
  - RPI PICO
  - CIRCUITPYTHON
header:
     teaser: "/assets/images/USB_PEDAL_RPI_PICO_TEASER.jpg"
---
Pedais USB (ou qualquer outro interruptor momentâneo) que imitam a pressão de uma tecla no teclado ou combinação de teclas. Prático para usar com software de edição de vídeo para pausar/reproduzir sem afastar as mãos do teclado ou mouse, também pode ser usado por software de videoconferência para silenciar rapidamente. Não é necessário baixar firmware especial ou configurar teclas (apenas um editor de texto simples é necessário). Funciona com quase qualquer sistema operacional, até mesmo com dispositivos Android usando um adaptador USB OTG.

<figure>
	<a href="/assets/images/USB_PEDAL_RPI_PICO.jpg"> <img src="/assets/images/USB_PEDAL_RPI_PICO_MEDIUM.jpg"> </a>
	<figcaption>Circuito do pedal USB instalado em uma caixa robusta.</figcaption>
</figure>

Componente chave: [Rpi Pico.](https://s.click.aliexpress.com/e/_AXStdl)
{: .notice--danger}


##### Conceito:

A grande maioria dos pedais programáveis USB disponíveis no mercado precisam que você instale um aplicativo para configuração. Normalmente, este aplicativo só está disponível para Windows e vem traduzido de maneira precária (se é que vem traduzido). Isso é um obstáculo para usuários de Linux ou Mac, que só têm duas opções: instalar uma máquina virtual Windows ou pedir ajuda a um usuário Windows para configurar o pedal.

Aqui entra em ação o [Raspberry Pi Pico](https://www.raspberrypi.org/products/raspberry-pi-pico/), por duas grandes razões: interface USB nativa, sem necessidade de programador ou hardware adicional para download de firmware, e o mais importante: suporte ao CircuitPython. A programação pode ser feita "ao vivo", sem necessidade de compilação e download durante a fase de depuração. Portanto, o Rpi Pico é o melhor candidato para um pedal DIY.

Outra vantagem adicional sobre os pedais USB comerciais, o próprio pedal pode ser substituído por um mais robusto, sem tocar no circuito. Outro tipo de interruptores pode ser usado, para que a operação com diferentes partes do corpo seja possível. A quantidade de interruptores a serem instalados é limitada apenas pelos pinos GPIO do Rpi Pico e pelo espaço disponível na caixa.

O circuito é construído usando o sistema de prototipagem de hardware [MISISTEMITA](https://github.com/galopago/misistemita), que fornece diferentes tipos de módulos pré-construídos que permitem construir um projeto eletrônico sem solda, mas tornando-o muito robusto e expansível. Todas as peças estão enclausuradas em uma caixa à prova de poeira e água IP65. Essa caixa confere um aspecto "industrial" ao projeto e também adiciona força mecânica para suportar abusos. As conexões elétricas externas (pedais e USB) foram equipadas com acessórios IP para fornecer uma boa vedação.

#### Recursos principais:

* Desenvolvido usando CircuitPython, amigável e fácil de aprender
* Compatível com os sistemas operacionais mais comuns
* Não é necessário instalar aplicativos para o download inicial de firmware
* Configuração de teclas feita em um arquivo de texto
* Resistente a respingos e à choques
* Pedais desmontáveis e substituíveis
* Construído usando sistema de prototipagem de hardware
* Alimentado por USB, sem necessidade de fonte de alimentação adicional

O hardware é bastante simples, apenas exige um Rpi Pico e interruptores conectados entre GPIO e terra. Resistores de pull-up internos utilizados. Alimentação e dados via cabo USB.


<figure>
	<a href="/assets/images/rpi_pico_usb_keyboard.png"> <img src="/assets/images/rpi_pico_usb_keyboard.png"> </a>
	<figcaption>Diagrama de blocos simplificado</figcaption>
</figure>


##### O que é CircuitPython?:
Na palavras da [Adafruit Industres](https://learn.adafruit.com/bienvenido-a-circuitpython-2/que-es-circuitpython), criadora do CircuitPython:
> CircuitPython é uma linguagem de programação projetada para simplificar a experimentação e o aprendizado de programação em placas de microcontroladores de baixo custo. Torna o início mais fácil do que nunca, sem downloads prévios necessários. Assim que você configurar sua placa, basta abrir qualquer editor de texto e começar a editar o código. É assim de simples.

Outras razões para usar o CircuitPython incluem:

* Você quer começar rapidamente. Crie um arquivo, edite seu código, salve o arquivo e ele será executado imediatamente. Não há compilação, nem download nem upload necessários.
* Você é novo em programação. O CircuitPython foi projetado pensando na educação. É fácil começar a aprender a programar e você recebe um feedback imediato da placa.
* Atualize facilmente seu código. Como o seu código fica armazenado no disco, você pode editá-lo sempre que quiser. Além disso, você pode manter vários arquivos para fácil experimentação.
* A console serial e o REPL. Eles permitem feedback ao vivo do seu código e programação interativa.
* Armazenamento de arquivos. O armazenamento interno do CircuitPython é ótimo para registro de dados, reprodução de áudio e interação com arquivos.
* Suporte sólido a hardware. Existem muitas bibliotecas e drivers para sensores, placas de expansão e outros componentes externos.
É Python! O Python é a linguagem de programação em mais rápido crescimento. É ensinado em escolas e universidades. O CircuitPython é quase completamente compatível com o Python. Ele simplesmente adiciona suporte ao hardware.

##### Software:

A aplicação de exemplo apresentada aqui é composta por duas tarefas: inicializar o GPIO de acordo com o arquivo de configuração e, em seguida, executar um loop interminável verificando o fechamento do interruptor para enviar seu respectivo código de tecla. Uma função de descancelamento de software foi usada para evitar pressionamentos falsos de tecla. A LED integrada ao Rpi Pico acende quando qualquer interruptor configurado é fechado.

A estrutura do arquivo de configuração é muito simples. A primeira linha é dos GPIOs a serem usados, a segunda linha é do código de tecla a ser enviado e a terceira linha é do código de tecla modificadora (como SHIFT, CONTROL, ALT). Se durante a inicialização o arquivo de configuração não for encontrado, o programa assumirá alguns valores padrão. Mais GPIOs podem ser adicionados ao arquivo de configuração, permitindo que sejam plugadas 3, 4 ou mais pedais.


##### Circuit assembly:

The circuit was built using components of TUSISTEMITA, like enclosure backplate, and Rpi Pico screw terminal breakboard.

Once the app is downloaded for the first time, and electrical connections verified, the backplate could be attached to the enclosure hassle free. Just unplug USB cable and debug switches' screw terminals, screw backplate to enclosure and reconnect cables again.

<figure class="third">
	<a href="/assets/images/USB_PEDAL_PICO_DEBUG.jpg"> <img src="/assets/images/USB_PEDAL_PICO_DEBUG_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_PARTS.jpg"> <img src="/assets/images/USB_PEDAL_PICO_PARTS_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_WIRED.jpg"> <img src="/assets/images/USB_PEDAL_PICO_WIRED_MEDIUM.jpg"> </a>
	<figcaption>Debug, wiring and assembly.</figcaption>
</figure>

USB printer connector (Type B) was chosen because is very robust and intuitive. This specific connector is designed for panel mounting and sports 4 metal pins (VCC,USB+,USB-,GND) that must be soldered to a Micro USB extension cable to plug to the Rpi Pico. Pedals use circular aviation connectors.


<figure class="third">
	<a href="/assets/images/USB_PEDAL_PICO_AVIATION.jpg"> <img src="/assets/images/USB_PEDAL_PICO_AVIATION_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_PANEL.jpg"> <img src="/assets/images/USB_PEDAL_PICO_PANEL_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_PRINTER.jpg"> <img src="/assets/images/USB_PEDAL_PICO_PRINTER_MEDIUM.jpg"> </a>
	<figcaption>Connectors for computer and pedals</figcaption>
</figure>

Once the enclosure is closed, firmware updates could be done modifying the CircuitPython file, or via interactive environment. For a CircuitPython re-installation or Rpi Pico "format", the enclosure must be open to access bootsel button.

#### Bill of materials

| Component         | Get yours! | Datasheet                                          |
| -------- | ------ | ------------------------------------------------------------ |
| M2.6 self-tapping B-type screw | [💸](https://s.click.aliexpress.com/e/_eOJ3Kd) | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf) |
| 2:1 Heatshrink tube multiple colors | [💸](https://s.click.aliexpress.com/e/_9ikkU7) | [2_1_heatshrink_tube_colors.pdf](/assets/pdf/2_1_heatshrink_tube_colors.pdf) |
| 115x90x55 mm enclosure box | [💸](https://s.click.aliexpress.com/e/_AFnqxL) | [KH-F3.pdf](/assets/pdf/KH-F3.pdf) |
| Raspberry Pi Pico | [💸](https://s.click.aliexpress.com/e/_AXStdl) | [pico-datasheet.pdf](/assets/pdf/pico-datasheet.pdf) |
| USB Type B IP68 panel connector | [💸](https://s.click.aliexpress.com/e/_AbHdB8) | [USB_TYPE_B_PANEL_MOUNT_CONNECTOR.pdf](/assets/pdf/USB_TYPE_B_PANEL_MOUNT_CONNECTOR.pdf) |
| 4 pin aviation connector | [💸](https://s.click.aliexpress.com/e/_9yPVWE) | [CIRCULAR_AVIATION_PANEL_CONNECTOR.pdf](/assets/pdf/CIRCULAR_AVIATION_PANEL_CONNECTOR.pdf) |
| Metal electric foot switch | [💸](https://s.click.aliexpress.com/e/_97Yt4m) | [METAL_MOMENTARY_ELECTRIC_FOOT_SWITCH.pdf](/assets/pdf/METAL_MOMENTARY_ELECTRIC_FOOT_SWITCH.pdf) |
| USB printer cable A type | [💸](https://s.click.aliexpress.com/e/_A1mCwQ) | [USB_PRINTER_CABLE.pdf](/assets/pdf/USB_PRINTER_CABLE.pdf) |
| Micro USB cable | [💸](https://s.click.aliexpress.com/e/_97vmPY) | [MICRO_USB_CABLE.pdf](/assets/pdf/MICRO_USB_CABLE.pdf) |


#### TUSISTEMITA blocks

| PCB    |  Source file                                          | 
| -------- | ------------------------------------------------------------ |
| A01 Backplate for 158x90x60mm enclosure| [A01](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)           |
| C11 screw terminal breakout board for Rpi Pico  | [C11](https://github.com/galopago/TUSISTEMITA/tree/master/C_BREAKOUTS)        |



#### Software

| Software    | Source file                                        | 
| -------- | ------------------------------------------------------------ |
| Firmware    | [PEDAL_USB_RPI_PICO](https://github.com/galopago/RPI_PICO_USB_FOOT_SWITCH)           |

 

## Optional components:

| Componente         | Consigue el tuyo! | Hoja de caracteristicas                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| 3 pc step drill bit 3-20 mm + centerpunch  | [💸](https://s.click.aliexpress.com/e/_9vxJV5)     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
| 8 Step drill bit 10-45 mm    | [💸](https://s.click.aliexpress.com/e/_9Ior51)     | [8_steps_10-45mm_incremental_drill_bit.pdf](/assets/pdf/8_steps_10-45mm_incremental_drill_bit.pdf)           |
