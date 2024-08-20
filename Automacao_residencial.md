# Projeto: Sistema de Automação Residencial

## Componentes Utilizados

- **Arduino Uno**
  - Microcontrolador responsável por gerenciar os sensores e acionar os relés.
- **Módulos de Relé**
  - Dispositivos que permitem ao Arduino controlar circuitos de alta potência, como lâmpadas, ventiladores, e outros aparelhos elétricos.
- **Sensores Diversos**
  - **Sensor de Temperatura**: Monitora a temperatura ambiente, possibilitando o controle de sistemas de aquecimento ou ar-condicionado.
  - **Sensor de Movimento (PIR)**: Detecta a presença de pessoas em um ambiente, permitindo o acionamento de luzes ou alarmes.
  - **Sensor de Luz (LDR)**: Monitora a intensidade da luz ambiente, possibilitando o controle automático de lâmpadas.
- **Interface de Controle**
  - **Smartphone**: Usado para controlar remotamente os dispositivos conectados, utilizando aplicativos ou interfaces web.
  - **Computador**: Pode ser utilizado como uma central de controle, permitindo monitoramento e controle dos dispositivos em tempo real.

## Descrição do Projeto

O Sistema de Automação Residencial é um projeto que visa proporcionar conforto, segurança e eficiência energética em residências. O sistema utiliza o Arduino Uno para monitorar diferentes parâmetros dentro da casa através de sensores e aciona dispositivos conectados a módulos de relé com base em condições pré-definidas ou comandos recebidos de um smartphone ou computador.

### Funcionamento

#### 1. Monitoramento de Parâmetros

- **Sensor de Temperatura**: O Arduino lê os dados do sensor de temperatura para monitorar o clima interno. Se a temperatura ultrapassar um limite pré-estabelecido, o sistema pode ligar automaticamente um ventilador ou ar-condicionado.
  
- **Sensor de Movimento (PIR)**: Este sensor detecta a presença de movimento em um cômodo. Quando o movimento é detectado, o Arduino pode acionar automaticamente as luzes do ambiente. Além disso, se nenhum movimento for detectado por um determinado período, as luzes podem ser apagadas para economizar energia.

- **Sensor de Luz (LDR)**: O sensor LDR permite que o Arduino meça a intensidade da luz ambiente. Se a luz natural for insuficiente, o Arduino pode acionar as luzes elétricas, mantendo o ambiente sempre bem iluminado.

#### 2. Controle de Dispositivos

- **Módulos de Relé**: O Arduino utiliza os módulos de relé para controlar dispositivos elétricos conectados, como lâmpadas, ventiladores, aquecedores, e outros aparelhos. Os relés funcionam como interruptores controlados eletronicamente, permitindo que o Arduino ligue ou desligue dispositivos com segurança.

#### 3. Controle Remoto

- **Interface com Smartphone**: O sistema pode ser controlado remotamente através de um smartphone. Utilizando aplicativos dedicados ou uma interface web, o usuário pode monitorar os parâmetros da casa e acionar ou desligar dispositivos conforme necessário, de qualquer lugar.
  
- **Interface com Computador**: Além do controle por smartphone, o sistema pode ser gerenciado através de um computador, que pode atuar como uma central de automação, exibindo dados em tempo real e permitindo o controle manual ou automático dos dispositivos.

## Interface com Smartphone e Computador utilizando MQTT

### 1. Comunicação via MQTT

O protocolo **MQTT (Message Queuing Telemetry Transport)** é uma solução leve para comunicação máquina-a-máquina (M2M) que é ideal para dispositivos de IoT, como o Arduino. Ele permite a troca de mensagens entre dispositivos através de um broker central, facilitando o controle remoto e o monitoramento em tempo real.

### 2. Interface com Smartphone

- **Aplicativo MQTT**: Para controlar o sistema de automação residencial, o usuário pode utilizar um aplicativo MQTT disponível para smartphones (como MQTT Dash ou IoT MQTT Panel). Esses aplicativos permitem a criação de botões, sliders, e outras interfaces gráficas que enviam comandos MQTT ao Arduino.
  
- **Funcionalidades**:
  - **Monitoramento em Tempo Real**: O smartphone pode receber dados dos sensores conectados ao Arduino, como temperatura, presença de movimento, ou nível de iluminação, através de tópicos MQTT específicos.
  - **Controle de Dispositivos**: Comandos para ligar ou desligar dispositivos conectados aos relés podem ser enviados diretamente do smartphone através de tópicos MQTT. Por exemplo, ao pressionar um botão no aplicativo, uma mensagem MQTT é publicada no tópico correspondente, e o Arduino, ao receber essa mensagem, aciona o relé apropriado.
  
- **Exemplo de Tópicos MQTT**:
  - `casa/sala/temperatura` - Publicação da temperatura medida na sala.
  - `casa/luzes/sala/comando` - Comando para ligar ou desligar as luzes da sala.

### 3. Interface com Computador

- **Software MQTT**: Para interface com o computador, podem ser utilizados softwares como MQTT.fx ou a integração com uma interface web personalizada utilizando frameworks como Node-RED ou diretamente em uma aplicação web criada com HTML, CSS e JavaScript.
  
- **Funcionalidades**:
  - **Dashboard de Controle**: O computador pode exibir um painel de controle com gráficos e indicadores dos dados recebidos dos sensores. Este painel pode ser atualizado em tempo real, refletindo as condições atuais da casa.
  - **Automatizações Avançadas**: A interface no computador pode incluir regras automáticas baseadas em dados dos sensores. Por exemplo, se a temperatura ultrapassar um determinado valor, o sistema pode enviar um comando para ligar o ar-condicionado automaticamente, sem intervenção manual.
  - **Controle Manual**: Assim como no smartphone, o usuário pode controlar manualmente os dispositivos conectados, enviando comandos MQTT diretamente do computador.

- **Exemplo de Tópicos MQTT**:
  - `casa/sala/temperatura` - Exibição da temperatura em um gráfico no dashboard.
  - `casa/luzes/sala/status` - Recebe e exibe o status atual das luzes da sala (ligadas/desligadas).
  - `casa/luzes/sala/comando` - Envia comandos para ligar ou desligar as luzes da sala.

### 4. Integração e Funcionamento

- **Broker MQTT**: Tanto o smartphone quanto o computador se conectam a um broker MQTT (como Mosquitto) que gerencia as mensagens enviadas e recebidas. O Arduino também se conecta a este broker para publicar dados dos sensores e receber comandos para os dispositivos.
  
- **Fluxo de Operação**:
  1. **Leitura de Sensores**: O Arduino lê os valores dos sensores (temperatura, movimento, luz) e publica esses dados nos tópicos MQTT correspondentes.
  2. **Envio de Comandos**: O usuário, através do smartphone ou computador, publica comandos nos tópicos MQTT para controlar os dispositivos conectados aos relés.
  3. **Recepção de Comandos**: O Arduino subscreve aos tópicos de controle e, ao receber um comando, aciona o relé correspondente para ligar ou desligar um dispositivo.

- **Vantagens**:
  - **Controle Remoto**: O sistema pode ser controlado de qualquer lugar com acesso à internet, oferecendo grande flexibilidade.
  - **Escalabilidade**: Novos dispositivos e sensores podem ser facilmente integrados ao sistema, bastando adicionar novos tópicos MQTT.
  - **Eficiência e Rapidez**: O protocolo MQTT é leve e eficiente, garantindo que os comandos sejam executados rapidamente e com baixo consumo de recursos.

Este sistema baseado em MQTT torna a automação residencial inteligente, permitindo o controle e monitoramento fácil e em tempo real de diversos dispositivos na casa.
# Montagem de um Broker MQTT com Mosquitto

### O que é Mosquitto?

**Mosquitto** é um broker MQTT (Message Queuing Telemetry Transport) de código aberto, amplamente utilizado para gerenciar a comunicação entre dispositivos IoT. O Mosquitto é responsável por receber, armazenar e enviar mensagens entre clientes conectados (publicadores e subscritores) através de tópicos específicos.


### Considerações Finais

Este Sistema de Automação Residencial pode ser expandido com a adição de mais sensores e dispositivos, como câmeras de segurança, sistemas de irrigação automática, entre outros. Além disso, a implementação de comunicação via Wi-Fi ou Bluetooth pode ampliar ainda mais as funcionalidades e a flexibilidade do sistema.

O projeto oferece uma solução prática e acessível para modernizar residências, proporcionando maior conforto, segurança e eficiência no uso da energia.
