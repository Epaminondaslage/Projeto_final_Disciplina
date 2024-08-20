# Projeto: Robô Seguidor de Linha

## Componentes Utilizados

- **Arduino Uno**
- **Motores DC** (2 unidades)
- **Driver de Motor (L298N)**
- **Sensores de Linha Infravermelhos** (2 ou mais unidades)
- **Rodas** (2 unidades)
- **Chassi** (para montar os componentes)
- **Fonte de Alimentação** (bateria para os motores e o Arduino)

## Descrição do Projeto

O Robô Seguidor de Linha é um projeto clássico de robótica onde um robô é programado para seguir uma linha preta desenhada no chão. O robô utiliza sensores infravermelhos para detectar a linha e ajusta os motores para garantir que o robô permaneça sobre a linha enquanto se move.

### Funcionamento

## Funcionamento do Robô Seguidor de Linha

O Robô Seguidor de Linha opera utilizando sensores infravermelhos para detectar uma linha no chão e controlar os motores para seguir essa linha. Abaixo está um detalhamento de como o robô funciona:

### 1. Detecção da Linha

- **Sensores Infravermelhos**: O robô utiliza sensores infravermelhos montados na parte inferior para detectar a linha preta. Esses sensores emitem luz infravermelha e medem a quantidade de luz refletida de volta.
  - Quando o sensor está sobre uma superfície clara (como o chão branco), a luz infravermelha é refletida de volta para o sensor.
  - Quando o sensor está sobre a linha preta, menos luz é refletida de volta, pois a linha preta absorve a luz infravermelha.
- **Leitura dos Sensores**: O Arduino lê o valor de cada sensor. Um valor baixo indica que o sensor está sobre a linha preta, enquanto um valor alto indica que o sensor está sobre a superfície clara.

### 2. Decisão do Movimento

Com base nos valores lidos dos sensores, o Arduino decide como controlar os motores para manter o robô na linha:

- **Seguir em Frente**: Se ambos os sensores detectam a linha preta (ou estão sobre a borda da linha), o robô avança em linha reta.
- **Virar à Esquerda**: Se o sensor esquerdo sai da linha (detectando a superfície clara), o Arduino ajusta os motores para virar o robô à esquerda até que o sensor volte a detectar a linha preta.
- **Virar à Direita**: Se o sensor direito sai da linha, o Arduino ajusta os motores para virar o robô à direita até que o sensor detecte novamente a linha.

### 3. Controle dos Motores

- **Driver de Motor (L298N)**: O L298N é usado para controlar a direção e a velocidade dos motores DC. O Arduino envia sinais ao driver de motor para controlar os dois motores de forma independente.
  - **Motores para Frente**: Ambos os motores giram para a frente quando o robô deve seguir em linha reta.
  - **Motores para Curva**: Um motor gira mais rápido ou desacelera enquanto o outro desacelera ou para, permitindo que o robô faça curvas suaves ou acentuadas.

### 4. Ajuste Dinâmico

- **Correções Contínuas**: À medida que o robô se move, ele faz ajustes contínuos para permanecer sobre a linha preta. Pequenas variações na leitura dos sensores resultam em correções rápidas, garantindo que o robô siga a linha de maneira eficiente.
- **Curvas e Interseções**: Dependendo da complexidade do trajeto, o robô pode precisar lidar com curvas acentuadas e interseções. O código pode ser aprimorado para lidar com esses desafios, como diminuir a velocidade em curvas ou tomar decisões em bifurcações.

### 5. Considerações Adicionais

- **Sensibilidade dos Sensores**: A sensibilidade dos sensores infravermelhos pode ser ajustada para melhorar o desempenho do robô em diferentes condições de iluminação e em diferentes tipos de superfícies.
- **Velocidade dos Motores**: A velocidade dos motores deve ser ajustada para garantir que o robô tenha tempo de corrigir sua direção antes de sair completamente da linha.

Este processo de decisão e controle é o que permite ao robô seguir a linha de forma autônoma, corrigindo seu curso continuamente para permanecer na trajetória desejada.
