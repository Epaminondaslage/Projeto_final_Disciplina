# Controle de Iluminação Automática

## Componentes Necessários:

1. **Arduino Uno**: Controlador principal que processa a leitura do sensor LDR e controla o acionamento do relé.
   
2. **Sensor de Luz (LDR - Light Dependent Resistor)**:
   - **Função**: Detecta a quantidade de luz ambiente. A resistência do LDR varia conforme a intensidade da luz, sendo alta em ambientes escuros e baixa em ambientes iluminados.
   - **Conexões**: Conectado a um pino analógico do Arduino (exemplo: A0) para ler a variação de resistência, com um divisor de tensão configurado.

3. **Relé**:
   - **Função**: Atua como um interruptor controlado eletronicamente pelo Arduino, permitindo ligar ou desligar a lâmpada com segurança.
   - **Conexões**: O sinal de controle do relé é conectado a um pino digital do Arduino (exemplo: D7). A alimentação do relé é conectada ao 5V e GND.

4. **Lâmpada**:
   - **Função**: A lâmpada é o dispositivo de saída que será controlado pelo relé, acendendo ou apagando conforme a quantidade de luz ambiente detectada.
   - **Conexões**: A lâmpada é conectada ao circuito de potência do relé, permitindo que o relé atue como um interruptor.

## Descrição do Funcionamento:

1. **Leitura da Luz Ambiente**:
   - O LDR é utilizado para medir a intensidade da luz no ambiente. O Arduino lê o valor analógico fornecido pelo LDR e o converte em um valor digital que representa a quantidade de luz detectada.

2. **Processamento no Arduino**:
   - Com base no valor lido do LDR, o Arduino decide se deve acionar ou desativar o relé. Por exemplo, se a luz ambiente estiver abaixo de um certo nível (indicando que está escuro), o Arduino acionará o relé para ligar a lâmpada.

3. **Controle da Lâmpada via Relé**:
   - Quando o relé é acionado pelo Arduino, a lâmpada é ligada, iluminando o ambiente. Quando a luz ambiente aumenta além do nível configurado, o relé é desativado, apagando a lâmpada.

## Circuito Eletrônico:

- **LDR**: Conectado ao pino A0 do Arduino, formando um divisor de tensão com um resistor fixo (geralmente 10kΩ). O ponto médio do divisor de tensão é lido pelo Arduino.

- **Relé**: O pino de sinal do relé é conectado ao pino D7 do Arduino. O relé é alimentado pelo pino 5V e GND do Arduino. A lâmpada é conectada ao circuito de comutação do relé.

- **Lâmpada**: Conectada ao circuito de potência do relé, que por sua vez é controlado pelo Arduino.

## Expansões Possíveis:

- **Ajuste de Sensibilidade**: A sensibilidade do sistema pode ser ajustada alterando o valor do resistor no divisor de tensão ou programando limites diferentes no código do Arduino.

- **Controle via Aplicativo**: Adicionando um módulo Wi-Fi ou Bluetooth, o sistema pode ser controlado remotamente por um aplicativo em smartphone, permitindo ligar ou desligar a lâmpada manualmente ou ajustar os parâmetros de controle.

- **Integração com Outros Sensores**: O sistema pode ser expandido para considerar outros fatores, como a presença de movimento, integrando um sensor PIR para ligar a lâmpada apenas quando há alguém no ambiente.

- **Registro de Dados**: Adicionando um módulo de cartão SD, o sistema pode registrar os níveis de luz ao longo do tempo para análise de padrões de iluminação no ambiente.

- **Integração com Aplicativos de Smartphones** 

## Componentes Adicionais Necessários:

- **Módulo Wi-Fi (ESP8266 ou ESP32)**:
  - **Função**: Permite ao Arduino se conectar a uma rede Wi-Fi para comunicação com um servidor web ou diretamente com um aplicativo de smartphone.
  - **Conexões**: O módulo ESP8266, por exemplo, pode ser conectado aos pinos RX e TX do Arduino para comunicação serial. O ESP32 pode ser utilizado diretamente no lugar do Arduino Uno, integrando todas as funcionalidades.

- **Aplicativo de Smartphone**:
  - **Função**: Interface de usuário para monitorar a intensidade da luz ambiente e controlar a lâmpada remotamente. Pode ser desenvolvido usando plataformas como Blynk, App Inventor, ou aplicativos personalizados.
  - **Conexões**: Comunicação com o Arduino via Wi-Fi, utilizando um servidor local ou uma plataforma de nuvem.

## Descrição do Funcionamento:

- **Configuração da Conexão Wi-Fi**:
  - O Arduino, equipado com um módulo Wi-Fi, conecta-se a uma rede Wi-Fi configurada previamente. Essa conexão permite que o Arduino se comunique com um servidor web, plataforma em nuvem ou diretamente com o aplicativo de smartphone.

- **Criação de um Servidor Web no Arduino**:
  - O Arduino pode hospedar um servidor web simples que responde a comandos enviados pelo aplicativo de smartphone. O servidor web pode apresentar uma página HTML com botões para ligar ou desligar a lâmpada, além de exibir o valor da leitura do sensor LDR.

- **Comunicação com o Aplicativo**:
  - **Via HTTP**: O aplicativo de smartphone pode enviar requisições HTTP (GET ou POST) ao servidor web no Arduino para realizar ações como ligar ou desligar a lâmpada. O Arduino processa essas requisições e aciona o relé conforme necessário.
  - **Via MQTT**: Alternativamente, o Arduino pode publicar e subscrever tópicos MQTT, permitindo uma comunicação mais robusta e escalável com o aplicativo. Isso é útil para integrar com plataformas como Home Assistant, Node-RED, ou outros sistemas de automação residencial.

- **Desenvolvimento do Aplicativo**:
  - O aplicativo pode ser desenvolvido utilizando plataformas como Blynk, que oferece uma interface de arrastar e soltar para criar controles como botões, sliders e displays. O aplicativo se conecta ao Arduino via Wi-Fi, permitindo o controle da iluminação diretamente do smartphone.
  - Alternativamente, pode-se usar o **MIT App Inventor** para criar um aplicativo personalizado. O App Inventor permite a criação de um aplicativo que se comunica com o Arduino via HTTP ou MQTT, fornecendo controle total sobre a interface e as funcionalidades.

- **Monitoramento e Controle Remoto**:
  - O aplicativo de smartphone pode exibir a leitura atual do sensor de luz, permitindo ao usuário verificar a condição de iluminação do ambiente em tempo real.
  - O usuário pode manualmente ligar ou desligar a lâmpada, ignorando o controle automático, se necessário.
  - Configurações como limites de ativação do relé com base na leitura do LDR podem ser ajustadas diretamente no aplicativo, oferecendo maior flexibilidade e personalização.
