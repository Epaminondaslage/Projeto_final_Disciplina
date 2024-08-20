# Projeto: Jardim Automatizado

## Componentes Utilizados

- **Arduino Uno**
  - Controla todo o sistema, lendo dados do sensor de umidade e acionando a bomba de água através de um relé.
- **Sensor de Umidade do Solo**
  - Sensor analógico que mede a umidade do solo. Geralmente, a saída do sensor é uma tensão que varia de 0 a 5V, onde 0V representa solo seco e 5V representa solo muito úmido.
- **Bomba de Água**
  - Dispositivo elétrico responsável por bombear água para o jardim. Opera em corrente contínua ou alternada, dependendo do modelo.
- **Relé**
  - Interruptor eletrônico controlado pelo Arduino, que permite o acionamento da bomba de água. O relé isola o circuito de controle (Arduino) do circuito de potência (bomba).

## Descrição do Projeto

### 1. Monitoramento da Umidade do Solo

- **Funcionamento do Sensor**:
  - O sensor de umidade do solo possui duas sondas que são inseridas no solo. Ele mede a resistência elétrica entre as sondas, que varia com o conteúdo de água no solo. A leitura é convertida em um sinal analógico que o Arduino lê através de um dos pinos analógicos (A0, por exemplo).
  
- **Leitura e Processamento**:
  - O Arduino realiza leituras periódicas do sensor (usando `analogRead()`), obtendo um valor entre 0 e 1023. Esse valor é comparado com um limite pré-definido no código (por exemplo, 300 para solo seco). Se o valor lido for menor que o limite, significa que o solo está seco e a irrigação é necessária.

### 2. Decisão e Acionamento da Irrigação

- **Decisão de Acionamento**:
  - O Arduino, ao identificar que o solo está seco, envia um sinal digital a um pino de saída (por exemplo, pino 8) que está conectado ao módulo de relé. Este sinal é geralmente `HIGH` para ativar o relé.

- **Funcionamento do Relé**:
  - O relé, ao ser ativado, fecha o circuito de potência que alimenta a bomba de água. Este relé é projetado para controlar cargas de corrente mais alta, permitindo que o Arduino controle a bomba de forma segura.

### 3. Acionamento da Bomba de Água

- **Operação da Bomba**:
  - Quando o relé é ativado, a bomba de água começa a operar, bombeando água para o sistema de irrigação. O sistema pode ser configurado para operar por um tempo determinado ou até que a umidade do solo atinja o nível desejado.
  
- **Controle do Tempo de Irrigação**:
  - O tempo que a bomba permanece ligada pode ser controlado programaticamente, utilizando funções como `delay()` ou `millis()` no Arduino para determinar por quanto tempo a bomba deve operar após o acionamento.

### 4. Ciclo de Operação

- **Ciclo Repetitivo**:
  - O sistema continua a monitorar a umidade do solo em intervalos regulares. Quando a umidade cai abaixo do limite, o ciclo de irrigação é repetido. Isso garante que o solo permaneça sempre dentro de um nível ideal de umidade.

### 5. Sensores Utilizados no Projeto de Jardim Automatizado

## 5.1. Sensor de Umidade do Solo

### Descrição Geral
- **Tipo**: Sensor analógico de umidade do solo.
- **Modelo Comum**: YL-69 (sensor) com módulo conversor YL-38.
- **Função**: Mede a resistência elétrica do solo, que varia com o conteúdo de água, e converte essa medida em um sinal de tensão analógico que o Arduino pode ler.

### Especificações Técnicas
- **Faixa de Operação**: 3.3V a 5V (compatível com a maioria dos microcontroladores, incluindo o Arduino Uno).
- **Faixa de Medição**: 0-1023 em leitura analógica (0V a 5V).
- **Tensão de Saída**: 0V (solo seco) a 5V (solo muito úmido).
- **Consumo de Corrente**: < 20mA.

### Características
- **Princípio de Operação**: Baseia-se na variação de resistência do solo. A água no solo reduz a resistência, aumentando a condutividade entre as sondas. O módulo YL-38 converte esta variação de resistência em um sinal de tensão analógico.
- **Calibração**: Pode ser necessário ajustar o ponto de referência no código do Arduino para determinar o limite entre solo seco e úmido, dependendo do tipo de solo.

### Considerações de Uso
- **Oxidação**: As sondas de metal estão sujeitas a oxidação com o tempo, especialmente em solos úmidos. Sensores de melhor qualidade, como aqueles com revestimento de ouro ou aço inoxidável, são preferíveis para aumentar a durabilidade.
- **Posicionamento**: As sondas devem ser inseridas consistentemente na mesma profundidade para garantir leituras precisas. O sensor deve estar bem posicionado para evitar contato com pedras ou outros obstáculos que possam afetar a medição.

## 5.2. Sensor de Temperatura e Umidade (Opcional para Expansão)

### Descrição Geral
- **Tipo**: Sensor digital de temperatura e umidade.
- **Modelo Comum**: DHT11 ou DHT22.
- **Função**: Mede a temperatura e a umidade relativa do ar. Embora não seja essencial para o controle da irrigação, pode ser usado para monitorar o ambiente e ajustar o sistema de irrigação com base nas condições climáticas.

### Especificações Técnicas
- **DHT11**:
  - **Faixa de Temperatura**: 0°C a 50°C, com precisão de ±2°C.
  - **Faixa de Umidade**: 20% a 90% RH, com precisão de ±5%.
  - **Tensão de Operação**: 3V a 5.5V.
  - **Saída de Dados**: Sinal digital serial.
- **DHT22**:
  - **Faixa de Temperatura**: -40°C a 80°C, com precisão de ±0.5°C.
  - **Faixa de Umidade**: 0% a 100% RH, com precisão de ±2-5%.
  - **Tensão de Operação**: 3V a 5.5V.
  - **Saída de Dados**: Sinal digital serial.

### Características
- **Princípio de Operação**: Utiliza um termistor para medir a temperatura e um capacitor de polímero para medir a umidade do ar, ambos processados por um microcontrolador interno no sensor.
- **Calibração**: Não requer calibração adicional, pois os valores de temperatura e umidade são pré-calibrados na fábrica.

### Considerações de Uso
- **Precisão**: O DHT22 oferece maior precisão e faixa de operação mais ampla em comparação ao DHT11, sendo ideal para aplicações que requerem medições mais precisas.
- **Intervalo de Leitura**: Deve-se evitar leituras muito frequentes (geralmente, uma leitura a cada 2 segundos) para garantir a precisão dos dados.

## 5.3. Sensor de Luz (LDR) (Opcional para Expansão)

### Descrição Geral
- **Tipo**: Sensor analógico de luminosidade (LDR - Light Dependent Resistor).
- **Função**: Mede a intensidade da luz ambiente. Pode ser usado para ajustar o sistema de irrigação com base na quantidade de luz solar recebida pelo jardim.

### Especificações Técnicas
- **Faixa de Operação**: 3.3V a 5V.
- **Resistência**: Varia de alguns ohms (alta luminosidade) a alguns megaohms (baixa luminosidade).
- **Tensão de Saída**: Sinal analógico proporcional à intensidade da luz.

### Características
- **Princípio de Operação**: A resistência do LDR diminui à medida que a intensidade da luz aumenta, resultando em um aumento da tensão de saída lida pelo Arduino.
- **Aplicação**: Ideal para detectar a transição entre dia e noite, ou para medir a quantidade de luz solar direta que atinge o jardim.

### Considerações de Uso
- **Proteção Contra Água**: O LDR deve ser protegido contra umidade e exposição direta à água para garantir uma longa vida útil.
- **Posicionamento**: Deve ser colocado em um local que represente bem a iluminação geral do jardim para fornecer leituras precisas.
 sensores especificados fornecem uma base robusta para o monitoramento preciso das condições do jardim. O sensor de umidade do solo é essencial para o controle de irrigação, enquanto os sensores de temperatura, umidade e luz podem ser usados para expandir as capacidades do sistema, permitindo uma automação mais inteligente e responsiva às condições ambientais.

### 6. Aplicações Práticas

1. **Automação de Jardins Domésticos**:
   - Mantém o jardim sempre irrigado, sem necessidade de intervenção manual, especialmente útil para quem não pode regar as plantas regularmente.
  
2. **Eficiência no Uso de Água**:
   - A irrigação só é acionada quando realmente necessária, evitando o desperdício de água.

3. **Cultivo em Estufas**:
   - Em ambientes controlados, como estufas, o sistema garante que as plantas recebam a quantidade ideal de água, independentemente das condições externas.

4. **Agricultura de Precisão**:
   - Pode ser expandido para monitorar várias zonas de irrigação, otimizando o uso de recursos hídricos em pequenas fazendas.

### 7. Considerações Técnicas

- **Fonte de Alimentação**:
  - Certifique-se de que a bomba e o relé sejam alimentados por uma fonte de energia adequada. O Arduino pode não fornecer corrente suficiente para bombas maiores, necessitando de uma fonte externa.

- **Proteção do Sistema**:
  - Utilize diodos de proteção (flyback diodes) ao operar com relés e bombas para proteger o Arduino de picos de corrente induzidos pela carga da bomba.

- **Configuração de Histerese**:
  - Implementar histerese no código ajuda a evitar acionamentos desnecessários da bomba em casos onde o valor do sensor oscila em torno do limite.

