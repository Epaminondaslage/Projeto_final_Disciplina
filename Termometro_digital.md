# Descrição Técnica do Projeto: Termômetro Digital com Alerta

## Objetivo do Projeto

Desenvolver um sistema baseado em Arduino Uno capaz de monitorar a temperatura ambiente e, opcionalmente, a umidade relativa do ar. O sistema deve exibir esses valores em um display (7 segmentos, LCD, ou OLED) e acionar um alerta sonoro (buzina) quando a temperatura ou umidade ultrapassar um limite pré-definido.

## Componentes Principais

1. **Arduino Uno**
   - **Função**: Microcontrolador principal do sistema, responsável por ler os sensores, processar as informações, exibir os dados, e acionar a buzina.
   - **Especificações**: Opera a 5V, possui 14 pinos digitais (6 PWM) e 6 pinos analógicos. A corrente máxima por pino é de 40mA.

2. **Sensor de Temperatura LM35**
   - **Função**: Fornecer uma leitura analógica da temperatura ambiente, convertendo a temperatura em uma tensão proporcional (10mV por °C).
   - **Especificações**: Mede temperaturas de -55°C a +150°C com uma precisão de ±0.5°C a 25°C. Opera entre 4V e 30V.

3. **Sensor de Temperatura e Umidade DHT11/DHT22 (Opcional)**
   - **Função**: Fornecer leituras digitais de temperatura e umidade. O DHT11 é mais básico, enquanto o DHT22 oferece maior precisão e faixa de medição.
   - **Especificações**:
     - **DHT11**: Temperatura de 0°C a 50°C, umidade de 20% a 90% RH.
     - **DHT22**: Temperatura de -40°C a 80°C, umidade de 0% a 100% RH.
     - Ambos operam entre 3V e 5.5V e utilizam uma interface de comunicação digital.

4. **Display de 7 Segmentos, LCD ou OLED**
   - **Função**: Exibir a temperatura (e a umidade, se aplicável) de forma legível ao usuário.
   - **Especificações**:
     - **7 Segmentos**: Mostra dígitos de 0 a 9, ideal para leitura simples de temperatura.
     - **LCD 16x2**: Exibe 16 caracteres por linha em 2 linhas, podendo mostrar temperatura e umidade com mensagens adicionais.
     - **OLED 128x64**: Alta resolução gráfica, ideal para exibir dados com maior flexibilidade e contraste.

5. **Buzina**
   - **Função**: Emitir um som de alerta quando a temperatura ou umidade ultrapassa o limite definido.
   - **Especificações**: Buzina piezoelétrica ou eletromecânica, opera a 5V com consumo de corrente entre 20-30mA.

## Funcionamento do Sistema

1. **Leitura dos Sensores**
   - **LM35**: O Arduino lê a tensão de saída do LM35 através de um dos pinos analógicos. A tensão é convertida em um valor de temperatura utilizando a fórmula:
     \[
     \text{Temperatura (°C)} = \frac{\text{Leitura Analógica} \times 5.0 \, \text{V}}{1024} \times 100
     \]
   - **DHT11/DHT22**: O Arduino lê os dados de temperatura e umidade via comunicação digital, usando uma biblioteca específica como `DHT.h`. A leitura é periódica e pode ser ajustada para intervalos de tempo apropriados para a aplicação.

2. **Processamento dos Dados**
   - O Arduino processa os dados lidos dos sensores e os compara com limites pré-estabelecidos para temperatura e umidade. Esses limites são configurados no código do Arduino e podem ser ajustados conforme necessário.

3. **Exibição das Informações**
   - **7 Segmentos**: A temperatura é exibida em formato numérico. Se a temperatura exceder o limite, o display pode piscar para indicar a condição de alerta.
   - **LCD**: Exibe a temperatura e a umidade, além de mensagens como "ALERTA!" quando o limite é ultrapassado.
   - **OLED**: Mostra a temperatura e a umidade de forma gráfica, permitindo a exibição de gráficos de barras ou outros indicadores visuais.

4. **Acionamento da Buzina**
   - Se a temperatura ou umidade ultrapassar o limite pré-definido, o Arduino ativa a buzina enviando um sinal digital para o pino correspondente. A buzina continuará soando até que a condição de alerta seja resolvida ou o sistema seja resetado.

## Aplicações Típicas

- **Monitoramento de Ambientes Críticos**: Salas de servidores, laboratórios, estufas, ou qualquer ambiente onde o controle de temperatura e umidade seja crucial.
- **Segurança Eletrônica**: Proteção de dispositivos sensíveis ao calor e umidade, alertando sobre condições adversas.
- **Uso Doméstico**: Monitoramento em casa para alertar sobre falhas em sistemas de aquecimento ou refrigeração.

## Considerações Técnicas

- **Calibração dos Sensores**: Deve ser realizada para garantir a precisão das medições. O LM35 e o DHT22 são precisos, mas podem requerer ajustes finos dependendo do ambiente.
- **Escolha do Display**: Depende das necessidades de visibilidade e complexidade da informação a ser exibida. O OLED oferece a melhor legibilidade e flexibilidade.
- **Gerenciamento de Energia**: Se o sistema for alimentado por bateria, o consumo deve ser otimizado, especialmente se for utilizado um display OLED.

## Expansões Futuras

- **Integração com Sistemas de Alerta Remoto**: Usando módulos de comunicação (Wi-Fi, Bluetooth) para enviar alertas de temperatura e umidade a um smartphone ou servidor.
- **Adição de Controles**: Possibilidade de integrar relés para ativar sistemas de ventilação ou aquecimento com base nas leituras de temperatura.
- **Automatização Completa**: Com sensores adicionais (como luminosidade ou qualidade do ar), o sistema pode ser expandido para um controle ambiental completo.

