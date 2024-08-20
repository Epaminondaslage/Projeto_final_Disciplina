# Descrição Técnica do Projeto: Medidor ultrassônico: Volume de Água em uma Caixa d'Água

## Objetivo do Projeto

Desenvolver um sistema baseado em Arduino Uno que mede o volume de água em uma caixa d'água utilizando um sensor de distância ultrassônico (HC-SR04). O sistema calcula o volume de água com base na distância medida entre o sensor e a superfície da água, exibindo o valor no display LCD. Este projeto é aplicável para monitorar o nível de água em reservatórios, tanques e caixas d'água.

## Componentes Principais

### 1. Arduino Uno

- **Função**: Microcontrolador principal do sistema, responsável por enviar e receber os sinais do sensor ultrassônico, calcular a distância e, consequentemente, o volume de água, exibindo o valor no display LCD.
- **Especificações**:
  - **Tensão de Operação**: 5V.
  - **Pinos Digitais**: 14 (6 PWM).
  - **Pinos Analógicos**: 6.
  - **Corrente por pino de I/O**: 40mA.

### 2. Sensor de Distância Ultrassônico (HC-SR04)

- **Função**: Medir a distância entre o sensor e a superfície da água na caixa d'água.
- **Especificações**:
  - **Faixa de Medição**: 2 cm a 400 cm.
  - **Precisão**: ±3 mm.
  - **Tensão de Operação**: 5V.
  - **Corrente de Operação**: 15 mA.
  - **Interfaces**:
    - **Trig**: Pino de entrada digital onde o Arduino envia um pulso de 10 µs para iniciar a medição.
    - **Echo**: Pino de saída digital que retorna um sinal correspondente ao tempo que o som levou para voltar ao sensor.

### 3. Display LCD (16x2)

- **Função**: Exibir o volume de água na caixa d'água em litros, baseado na distância medida pelo sensor ultrassônico.
- **Especificações**:
  - **Tensão de Operação**: 5V.
  - **Interface**: Paralela (pinos digitais) ou I2C com adaptador.
  - **Capacidade**: 32 caracteres (16 por linha).

## Funcionamento do Sistema

### 1. Medição da Distância

- **Princípio de Operação**:
  - O sensor HC-SR04 opera emitindo um pulso ultrassônico através do pino `Trig`. Este pulso é refletido de volta ao sensor se encontrar a superfície da água no caminho. O tempo que o pulso leva para retornar ao sensor é medido no pino `Echo`.
  - A distância é calculada com a fórmula:
    \[
    \text{Distância (cm)} = \frac{\text{Tempo (µs)} \times 0,0343}{2}
    \]
    - O fator 0,0343 é a velocidade do som em cm/µs.
    - O tempo é dividido por 2 porque o sinal viaja até a superfície da água e volta ao sensor.

### 2. Cálculo do Volume de Água

- **Cálculo da Altura do Nível de Água**:
  - A altura do nível de água na caixa é obtida subtraindo a distância medida pelo sensor (do topo da caixa até a superfície da água) da altura total da caixa d'água:
    \[
    \text{Altura da Água} = \text{Altura Total da Caixa} - \text{Distância Medida}
    \]

- **Cálculo do Volume de Água**:
  - Para caixas d'água de formato cúbico ou retangular, o volume de água é calculado como:
    \[
    \text{Volume (litros)} = \text{Comprimento} \times \text{Largura} \times \text{Altura da Água}
    \]
  - Para caixas d'água cilíndricas, o volume é calculado como:
    \[
    \text{Volume (litros)} = \pi \times \left(\frac{\text{Diâmetro}}{2}\right)^2 \times \text{Altura da Água}
    \]
  - O resultado é convertido para litros (1 cm³ = 0,001 litro).

### 3. Exibição no Display LCD

- **Formato de Exibição**:
  - O display LCD 16x2 exibe o volume de água em litros. A primeira linha pode exibir "Volume de Água:" e a segunda linha mostra o valor calculado, por exemplo, "500 L".
- **Interface**:
  - O LCD pode ser conectado diretamente aos pinos digitais do Arduino ou através de um módulo I2C, economizando pinos e facilitando a integração.

### Aplicações Típicas

#### 1. Monitoramento de Nível de Água em Residências

- **Função**: Fornecer uma leitura precisa do volume de água disponível em uma caixa d'água residencial, ajudando a gerenciar o consumo e evitar transbordamentos.

#### 2. Controle de Irrigação

- **Função**: Monitorar o volume de água disponível em tanques de irrigação, garantindo que haja água suficiente para os ciclos de irrigação planejados.

#### 3. Medição de Nível em Tanques Industriais

- **Função**: Monitorar o nível de líquidos em tanques industriais, facilitando o controle de processos que dependem da quantidade de líquido disponível.

### Considerações Técnicas

- **Precisão da Medição**: A precisão depende da instalação do sensor e da estabilidade da superfície da água. Ondulações ou turbulências podem afetar a medição.
- **Tempo de Resposta**: A frequência das leituras deve ser ajustada conforme a aplicação; medições muito frequentes podem ser desnecessárias para aplicações de monitoramento de nível.
- **Configuração Inicial**: O sistema deve ser configurado com as dimensões exatas da caixa d'água (altura, comprimento e largura ou diâmetro) para calcular corretamente o volume de água.

### Expansões Futuras

- **Alarme de Nível Crítico**: Adicionar um alarme sonoro ou visual que se ativa quando o nível de água está abaixo de um valor crítico.
- **Conexão com Sistemas de Controle Remoto**: Integrar o sistema com uma rede Wi-Fi para monitorar remotamente o volume de água via smartphone ou computador.
- **Ajuste Automático de Bombeamento**: Automatizar o acionamento de bombas de água com base no nível de água medido, para controle mais eficiente do uso de água.
