# Título do Tutorial

**Descrição:** Neste tutorial, vamos construir um Monitor de Batimentos Cardíacos com Alerta via LED, um dispositivo que mede a frequência cardíaca em tempo real e utiliza LEDs para alertar sobre possíveis irregularidades. O objetivo principal do projeto é introduzir conceitos básicos de eletrônica, programação e uso de sensores biométricos, proporcionando uma experiência prática e educativa.

---

## Índice

1. [Introdução](#introdução)
2. [Requisitos](#requisitos)
3. [Configuração do Ambiente](#configuração-do-ambiente)
4. [Montagem do Circuito](#montagem-do-circuito)
5. [Programação](#programação)
6. [Teste e Validação](#teste-e-validação)
7. [Expansões e Melhorias](#expansões-e-melhorias)
8. [Referências](#referências)

---

## Introdução

Bem-vindo ao tutorial de construção de um Monitor de Batimentos Cardíacos com Alerta via LED! Neste guia passo a passo, você aprenderá a criar um dispositivo capaz de medir a frequência cardíaca em tempo real utilizando um sensor biométrico e um microcontrolador Arduino. O sistema aciona LEDs para fornecer alertas visuais: um LED verde indica frequência cardíaca normal, enquanto um LED vermelho sinaliza batimentos fora do intervalo ideal.

---

## Requisitos

### Hardware

- **Placa**: Arduino Uno R3
- **Sensores**: Pulse Sensor, Um sensor óptico simples e eficiente que utiliza luz para detectar alterações no fluxo sanguíneo.
- **Atuadores**: LEDs 
- **Outros componentes**: Resistores, Jumpers

### Software

- **Linguagens**: C/C++ para Arduino
- **IDE**: Arduino IDE
- **Bibliotecas**: PulseSensor Playground

---

## Configuração do Ambiente

### Passo 1: Instalação do Software

- **Arduino IDE**:
1. Acesse o site oficial do Arduino: https://www.arduino.cc
2. No menu, clique em Software e, em seguida, clique em Download.
3. Escolha a versão compatível com o seu sistema operacional (Windows, macOS ou Linux).![Captura de Tela (22)](https://github.com/user-attachments/assets/bc803399-03a8-449c-9f45-7cd45668e6d2)


### Passo 2: Configuração das Placas

- **Configuração no Arduino**:
1. Conecte seu Arduino ao computador via USB.
2. No Arduino IDE, vá para Ferramentas > Placa e escolha o modelo do seu Arduino (por exemplo, Arduino Uno).
3. Em Ferramentas > Porta, selecione a porta à qual o Arduino está conectado (por exemplo, COM3 no Windows ou /dev/ttyUSB0 no Linux).![IDE](https://github.com/user-attachments/assets/3987b794-df1a-41e2-8841-2b934e99729c)



---

## Montagem do Circuito

**Conectar o Sensor ao Arduino**
- VCC do sensor → 5V no Arduino.
- GND do sensor → GND no Arduino.
- Sinal do sensor → A0 no Arduino.

**Conectar os LEDs**
1. LED Verde:
    - Anodo (perna longa) → Pino digital D2 (via resistor de 330 Ω).
    - Catodo (perna curta) → GND.
2. LED Vermelho:
    - Anodo → Pino digital D3 (via resistor de 330 Ω).
    - Catodo → GND.
  
   ![Captura de Tela (21)](https://github.com/user-attachments/assets/ea032f68-d184-4153-80c0-631aac6a2dbb)

   Link do circuito no Tinkercad: https://www.tinkercad.com/things/diNXBp7jY2n-monitor-de-batimentos-cardiacos-com-alerta-via-led?sharecode=Eh0NAm455gc2cGZ-tbGXkeiGWD5VI6SkQIKg53SIBV0



---

## Programação

### Passo 1: Configuração dos Sensores e Atuadores

Para configurar nosso Monitor de Batimentos Cardíacos com Alerta via LED, utilizaremos o seguinte código:


```c
#include <PulseSensorPlayground.h>

#define SENSOR_PIN A0  // Pino para o sensor
#define GREEN_LED 2    // LED verde para BPM normal
#define RED_LED 3      // LED vermelho para BPM fora da faixa

PulseSensorPlayground pulseSensor;

void setup() {
  pinMode(GREEN_LED, OUTPUT);  // Define o LED verde como saída
  pinMode(RED_LED, OUTPUT);    // Define o LED vermelho como saída
  Serial.begin(9600);          // Inicializa a comunicação serial

  pulseSensor.analogInput(SENSOR_PIN);
  pulseSensor.begin();
}

void loop() {
  int bpm = pulseSensor.getBeatsPerMinute();  // Lê o BPM do sensor

  Serial.print("BPM: ");
  Serial.println(bpm);  // Exibe o BPM no Monitor Serial

  // Se o BPM estiver dentro da faixa normal
  if (bpm >= 60 && bpm <= 100) {
    digitalWrite(GREEN_LED, HIGH);  // Acende o LED verde
    digitalWrite(RED_LED, LOW);     // Desliga o LED vermelho
  } else {
    digitalWrite(GREEN_LED, LOW);   // Desliga o LED verde
    digitalWrite(RED_LED, HIGH);    // Acende o LED vermelho
  }

  delay(1000);  // Atualiza a cada segundo
}

```

**Na IDE do Tinkercad use:**

```c
#define SENSOR_PIN A0
#define GREEN_LED 2
#define RED_LED 3

void setup() {
  pinMode(SENSOR_PIN, INPUT);
  pinMode(GREEN_LED, OUTPUT);
  pinMode(RED_LED, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int signal = analogRead(SENSOR_PIN);
  int bpm = calculateBPM(signal); // Supondo que tenha uma função para calcular BPM

  Serial.print("BPM: ");
  Serial.println(bpm);

  if (bpm >= 60 && bpm <= 100) {
    digitalWrite(GREEN_LED, HIGH);
    digitalWrite(RED_LED, LOW);
  } else {
    digitalWrite(GREEN_LED, LOW);
    digitalWrite(RED_LED, HIGH);
  }

  delay(1000); // Atualização a cada segundo
}

int calculateBPM(int signal) {
  return random(50, 120); // Simula valores de BPM
}

```

### Passo 2: Processamento e Lógica de Alerta

**1. Processamento dos Dados do Sensor**
O sensor de batimentos cardíacos, como o PulseSensor, gera um sinal analógico que reflete a variação do ritmo cardíaco. Esse sinal precisa ser processado para calcular a frequência cardíaca (em batimentos por minuto, BPM).

**2. Lógica de Alerta**
A lógica de alerta depende dos valores de BPM obtidos. Geralmente, definimos intervalos de BPM que indicam normalidade ou anormalidade. Quando o valor de BPM cair dentro de uma faixa saudável, um alerta visual (LED verde) é ativado. Se o valor estiver fora dessa faixa (muito alto ou muito baixo), um alerta diferente (LED vermelho) é acionado.

## Teste e Validação

Descreva os testes para validar cada parte do projeto:

1. **Testando Sensores**: O valor de BPM deve estar mudando conforme o toque no sensor (evidência de que o sensor está funcionando).
2. **Validação dos Atuadores**: Quando o BPM estiver dentro da faixa normal (entre 60 e 100 BPM), o LED verde deve acender.
   Quando o BPM estiver fora da faixa normal, o LED vermelho deve acender.
4. **Monitoramento em Tempo Real**: O sistema deve exibir o valor de BPM no Monitor Serial em tempo real, com atualizações a cada segundo.

---

## Expansões e Melhorias

- Exibição de dados em Display, dispensa o uso do Monitor Serial e torna o dispositivo portátil e independente.
- Alerta sonoro, proporciona um alerta adicional para situações críticas.
- Detecção de anormalidades, expande o uso do projeto para monitoramento mais avançado.

---

## Referências
1. https://www.tinkercad.com/things/diNXBp7jY2n-monitor-de-batimentos-cardiacos-com-alerta-via-led?sharecode=Eh0NAm455gc2cGZ-tbGXkeiGWD5VI6SkQIKg53SIBV0
2. https://github.com/WorldFamousElectronics/PulseSensorPlayground
3. https://www.arduino.cc/en/software

---

