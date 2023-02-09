---
title: "Reprojetando um CLP clone para uso com Arduino"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - portugues
tags:
  - AN007
  - STM32
  - CLP
header:
     teaser: "/assets/images/AN007/PLC_CLONE_ARDUINO_TEASER.jpg"
---

É bastante comum encontrar em páginas de compras online, publicidades como esta: "Placa de controle industrial compatível com FX1N, FX2N, FX3U e programável com software GX". O preço é atraente, no entanto, a documentação é inexistente e não há menção de como programá-la com outras ferramentas, como Arduino em sistemas operacionais diferentes do Windows. Este artigo introduzirá alguns conceitos-chave para ajudar a resolver este problema.

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_MEDIUM.jpg"> </a>
	<figcaption>Placa de controle industrial compatível com o software de programação CLP de um fabricante específico.</figcaption>
</figure>

Componente chave: [Placa de controle industrial compatível com FX1N.](https://s.click.aliexpress.com/e/_DDbOiuF)
{: .notice--danger}


##### Ataque dos clones.

Essas placas mencionam a compatibilidade com o software GX, que é fabricado por uma empresa [Japonesa que faz CLP e também carros.](https://www.mitsubishielectric.com/fa/products/cnt/plc/index.html) À primeira vista, a compatibilidade não é oficial, pois não há marca registrada impressa. Sua origem é desconhecida, talvez sejam cópias simplificadas baseadas em esquemas originais e código fonte, ou de alguma forma o formato binário nativo do CLP foi feito engenharia reversa  e um [interpretador tenha sido construído e execute no microcontrolador traduzindo o código.](https://github.com/KeyMove/STM32-PLC-FX1N) A maioria das placas é baseada em microcontroladores STM32 e, de acordo com alguns artigos e vídeos, o [software de programação original realmente os reconhece como um CLP original!](http://pdacontrolen.com/installation-gx-works2-demo-for-programming-plc-le3u-fk3u-lollette/)


<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_DINRAIL.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_DINRAIL_MEDIUM.jpg"> </a>
	<figcaption>Caixa de plástico, instalação em trilho DIN. </figcaption>
</figure>

Devido ao seu baixo custo (cerca de $25 USD), e por suas saídas de relé isoladas, entradas optocamente isoladas, porta serial RS232 e fonte de alimentação regulada, são ótimos candidatos para projetos pequenos desde que possam ser programados com uma ferramenta multi-plataforma gratuita como o Arduino ou o conjunto STM. Além disso, é necessário um diagrama esquemático para descobrir qual I/O do microcontrolador vai para qual periférico na placa!

##### Lista de materiais.

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_PARTS.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_PARTS_MEDIUM.jpg"> </a>
	<figcaption>Partes usadas. </figcaption>
</figure>

| Componente                                          | Ligação do compra                                          | Folha de dados
|-----------------------------------------------------|------------------------------------------------------------|---------------
| Placa de controle industrial compatível com FX1N    | [Compre aqui](https://s.click.aliexpress.com/e/_DDbOiuF) | [industrial-control-board-fx1n.pdf](https://github.com/galopago/logistic/blob/main/datasheet/industrial-control-board-fx1n.pdf)
| Fonte de alimentação montada em trilho DIN de 24 V 15 W. | [Compre aqui](https://s.click.aliexpress.com/e/_DdcNhEL) | [24v-din-rail-power-supply.pdf](https://github.com/galopago/logistic/blob/main/datasheet/24v-din-rail-power-supply.pdf)
| Conversor USB para RS232.                             | [Compre aqui](https://s.click.aliexpress.com/e/_DFlu2nD) | [usb-rs232-converter.pdf](https://github.com/galopago/logistic/blob/main/datasheet/usb-rs232-converter.pdf)
| Conector de terminal sem solda DB9.           | [Compre aqui](https://s.click.aliexpress.com/e/_Dl5STXV) | [db9-solderless-terminal-connector.pdf](https://github.com/galopago/logistic/blob/main/datasheet/db9-solderless-terminal-connector.pdf)
| Fio tipo PVDF UL1423 de 30 AWG.              | [Compre aqui](https://s.click.aliexpress.com/e/_eMiimB)  | [UL1423.pdf](https://github.com/galopago/logistic/blob/main/datasheet/UL1423.pdf)
| Cabos de ligação Dupont jumper                                | [Compre aqui](https://s.click.aliexpress.com/e/_DmusOdH) | [dupont-jumper-cables.pdf](https://github.com/galopago/logistic/blob/main/datasheet/dupont-jumper-cables.pdf)
| Conector Berg masculino de linha única de 2,54 mm.             | [Compre aqui](https://s.click.aliexpress.com/e/_eMCUJv)  | [FHA3-S1XX.pdf](https://github.com/galopago/logistic/blob/main/datasheet/FHA3-S1XX.pdf)


| Pinagem para placas de controle industrial        | repositório 
| ------------------------------------------------- | ----------- 
| Placas de controle industrial baseadas no STM32   | [stm32-industrial-control-boards](https://github.com/galopago/stm32-industrial-control-boards)

| Componente opcional                           | Ligação do compra                                         | Folha de dados.
| ----------------------------------------------|-----------------------------------------------------------|--------------- 
| Lupa dupla olho para jóias                    | [Compre aqui](https://s.click.aliexpress.com/e/_DcZsrEF)| [magnifying-double-eye.pdf](https://github.com/galopago/logistic/blob/main/datasheet/magnifying-double-eye.pdf) 
| Câmera de microscópio digital USB             | [Compre aqui](https://s.click.aliexpress.com/e/_Dl3rIxZ)| [microscope-camera-digital-usb.pdf](https://github.com/galopago/logistic/blob/main/datasheet/microscope-camera-digital-usb.pdf) 
| Multímetro digital alimentado por baterias AA.| [Compre aqui](https://s.click.aliexpress.com/e/_DeAv3zv)| [digital-multimeter-powered-aa-batteries-ut139c.pdf](https://github.com/galopago/logistic/blob/main/datasheet/digital-multimeter-powered-aa-batteries-ut139c.pdf) 

##### Reprogramação

O mencionado placa, possui um microcontrolador STM32F103, então, instintivamente, deve-se procurar por uma trilha para um cabeçalho de programação SWD.


<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_PROGHEADER.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_PROGHEADER_MEDIUM.jpg"> </a>
	<figcaption>Impressão de cabeçalho de programação possível no canto inferior direito</figcaption>
</figure>

Depois de seguir as trilhas desse cabeçalho, um pino foi encontrado conectado a 3,3 V, outro a GND, mas os outros dois pinos não estavam conectados aos pinos SWD no microcontrolador, mas sim aos pinos PC10 e PC11. Começando a pesquisa a partir do microcontrolador, não há trilhas dos pinos SWD ou USB, então a única alternativa disponível para reprogramação é através do UART1 usando o bootloader armazenado na ROM.


<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_UART1.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_UART1_MEDIUM.jpg"> </a>
	<figcaption>Componentes relacionados à porta serial</figcaption>
</figure>

Seguindo as trilhas saindo do conector DB9, elas terminam em um chip sem marcação, no entanto, devido aos capacitores próximos, provavelmente é um MAX232 ou equivalente. Seguindo as trilhas saindo deste chip, elas terminam nos pinos PA9 e PA10 do microcontrolador, que são os pinos UART1.

Felizmente, nesta placa, o resistor conectado ao pino BOOT0 está claramente marcado na tela de seda. Para iniciar no modo de inicialização, um cpnector foi soldado no pad de 3,3 V e, usando um jumper cabo Dupont, uma conexão temporária entre BOOT0 e 3,3 V é feita enquanto a placa é alimentada.


<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_BOOT0.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_BOOT0_MEDIUM.jpg"> </a>
	<figcaption>Método utilizado para a ativação do bootloader</figcaption>
</figure>

Uma vez que o bootloader estava em execução, o [STM32CubeProg](https://www.st.com/en/development-tools/stm32cubeprog.html) foi iniciado e a comunicação com o microcontrolador foi verificada. O chip estava no modo de proteção de leitura, então não havia maneira de fazer backup do firmware para reverter a placa para o seu estado original. Toda a memória FLASH foi apagada.

Usando o Arduino IDE, procedeu-se à instalação do [STM32duino core](https://github.com/stm32duino/Arduino_Core_STM32) e à criação de uma pequena aplicação de teste que envia dados através da porta serial para o PC. O aplicativo foi baixado e os dados de entrada foram verificados. Agora a aventura começa!


<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_USB232.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_USB232_MEDIUM.jpg"> </a>
	<figcaption>Conversor USB para RS232 e conectores utilizados para verificação de comunicação entre PC e placa</figcaption>
</figure>

##### Identificando os pinos de E/S

Devido à falta de um diagrama esquemático ou marcas na tela de seda mostrando quais pinos de E/S do microcontrolador vão para qual periférico, esse trabalho deve ser feito manualmente, com muita paciência para seguir as trilhas. Felizmente, a placa tem apenas 2 camadas, então é possível começar apenas com uma lupa de duplo olho para jóias e um multímetro.

###### LED e interruptor

A placa tem dois indicadores LED, um rotulado como RUN e o outro rotulado como ERR. Além disso, há um interruptor que era usado pelo antigo firmware PLC para interromper a execução do programa. Devido a esses periféricos terem alguns elementos entre eles e o microcontrolador, eles são muito fáceis de começar.

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_SWITCHLEDS.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_SWITCHLEDS_MEDIUM.jpg"> </a>
	<figcaption>Pinos de E/S do microcontrolador conectados a indicadores LED e interruptor identificado</figcaption>
</figure>

Os pinos foram encontrados mapeados da seguinte maneira:


|ELEMENTO              |PIN
|----------------------|-----
| LED RUN              | PB12
| LED ERR              | PB13
| RUN/STOP SWITCH      | PC9

###### Entradas digitais

As entradas digitais foram relativamente fáceis de encontrar, porque as trilhas que saem dos optocopladores vão diretamente para o microcontrolador. Apenas algumas delas eram difíceis porque saltavam para a camada oposta ou viajavam por baixo de um componente grande.


<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_INPUTS.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_INPUTS_MEDIUM.jpg"> </a>
	<figcaption>Seguindo trilhos de entrada</figcaption>
</figure>

Os pinos foram encontrados mapeados da seguinte maneira:

|ELEMENTO   |PIN
|-----------|-----
| X0        | PA0
| X1        | PA1
| X2        | PB9
| X3        | PA6
| X4        | PA7
| X5        | PB5
| X6        | PB4
| X7        | PD2

###### Saídas digitais

As saídas digitais exigiram mais esforço, porque as trilhas foram primeiro para um chip UL2003 e, a partir daí, para cada relé, viajando sob componentes ou saltando para a camada oposta. O multímetro foi crucial para seguir as trilhas.


<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_OUTPUTS.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_OUTPUTS_MEDIUM.jpg"> </a>
	<figcaption>Seguindo trilhos de saída</figcaption>
</figure>

Os pinos foram encontrados mapeados da seguinte maneira:

|ELEMENTO   |PIN
|-----------|-----
| Y0        | PB8
| Y1        | PB1
| Y2        | PB10
| Y3        | PB0
| Y4        | PC5
| Y5        | PC4

###### Entradas analógicas

As entradas analógicas foram relativamente fáceis de encontrar, porque são apenas 3 e estão conectadas apenas a um divisor de resistência de tensão (15 K / 30 K) entre elas e o microcontrolador.


<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_AINPUTS.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_AINPUTS_MEDIUM.jpg"> </a>
	<figcaption>Seguindo trilhos de entrada analógica.</figcaption>
</figure>

Os pinos foram encontrados mapeados da seguinte maneira:

|ELEMENT    |PIN
|-----------|-----
| AD1       | PC1
| AD2       | PC2
| AD3       | PC0

##### Toques finais

Neste ponto, todos os periféricos estão mapeados nos pinos de E/S do microcontrolador, no entanto, sempre que a placa precisar ser reprogramada, o BOOT0 precisará ser definido para 3,3 V usando um jumper de cabo temporal, o que implica abrir a caixa. Uma solução rápida será conectar um cabo do pino BOOT0 ao interruptor RUN / STOP usado pelo antigo firmware PLC, dessa forma, o bootloader ROM poderia ser iniciado externamente sem abrir o caso para reprogramação.

<figure>
	<a href="/assets/images/AN007/PLC_CLONE_ARDUINO_BOOTSWITCH.jpg"> <img src="/assets/images/AN007/PLC_CLONE_ARDUINO_BOOTSWITCH_MEDIUM.jpg"> </a>
	<figcaption>Interruptor externo agora conectado ao pino BOOT0.</figcaption>
</figure>

##### Em resumo 

nesta etapa, você tem uma placa de baixo custo com periféricos suficientes para pequenos experimentos sem precisar de hardware adicional e pode ser programada usando o Arduino IDE ou o conjunto STM. Para replicar este experimento com uma placa diferente (desde que o CPU tenha sido identificado), siga os seguintes passos:

* Procure o pinos SWD na PCB (4 pads) e siga os trilhos até o microcontrolador para garantir que os pinos sejam os corretos.

* Se o passo anterior falhar, siga os trilhos dos pinos UART1 do microcontrolador e adicione o hardware adicional (conversor de nível, conectores) para a comunicação com o PC

* Procure o pino BOOT0, geralmente está conectado ao chão através de um resistor, que servirá como um "ponto de teste".

* Usando o STM32CubeProg, apague a memória FLASH do microcontrolador. Se o UART1 foi usado como meio de conexão, o bootloader ROM deve ser iniciado, configurando o BOOT0 para 3,3 V enquanto liga a placa.

* Usando o Arduino IDE ou o STM suite, faça uma pequena aplicação de teste, que envia caracteres para a porta serial, para saber se a placa pode ser programada.

* Siga os trilhos dos periféricos até o microcontrolador, para mapear os pinos de E/S.

* Faça uma conexão de cabo do BOOT0 para o interruptor RUN/STOP para programar facilmente a placa.

##### Melhorias possíveis:

Crie uma aplicação esqueleto como ponto de partida para cada programa para a placa, essa aplicação deve ter algum tipo de mecanismo que verifica a condição do interruptor RUN/STOP para decidir se vai para o bootloader ROM ou começar a executar o programa armazenado na FLASH, Isso elimina a necessidade de uma conexão elétrica entre BOOT0 e o interruptor.

Outra opção, se uma aplicação esqueleto não for desejada, é criar um bootloader armazenado na FLASH que usa o UART1 para comunicação, similar ao armazenado na ROM, mas esse verifica a condição do interruptor RUN/STOP para decidir se baixa um novo programa ou executa o programa armazenado na FLASH.
