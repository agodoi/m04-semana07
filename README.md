# Sistema de disparo de atuadores

Neste encontro, será apresentado como ativar acionadores básicos (linha de força, motores, alarmes) a partir da resposta de sensores de forma a implementar regras de atuação. Adicionalmente, trataremos no detalhe, como funciona a comunicação I2C.

## Assuntos relacionados

- Atuadores

- Interfaces de comunicação

- Microcontroladores

## Perguntas que podem ajudar o seu projeto:

### (1) Quantos sensores I2C cabem no ESP32?

### (2) Quais ideias você aproveitar no seu projeto?

### (3) Qual a vantagem de se usar sensores I2C?

### (4) Quais os cuidados se você usar relés no seu projeto?


## Protocolo I2C

O barramento I2C (Inter-Integrated Circuit) é um protocolo de comunicação serial que permite a interconexão de vários dispositivos em um mesmo barramento. 

No ESP32, o I2C é implementado por meio de hardware e software. Veja na Fig. 1, como se comporta fisicamente as conexões eletrônica no barramento I2C.




Abaixo, vou explicar em detalhes técnicos como funciona a comunicação I2C no ESP32, incluindo a definição de endereços para dispositivos escravos.

### Hardware I2C no ESP32:

O ESP32 possui hardware dedicado para I2C, o que simplifica a implementação e melhora o desempenho. Existem dois pinos principais para I2C no ESP32:

- **SDA (Serial Data Line):** Pino para a linha de dados. Este pino é usado para enviar e receber dados.
- **SCL (Serial Clock Line):** Pino para a linha de clock. Este pino é usado para sincronizar a transferência de dados entre dispositivos.

### Configuração do Barramento I2C:

Para usar o I2C no ESP32, é necessário inicializar e configurar o barramento. Vou apresentar um exemplo usando a biblioteca Wire.h, que é comumente utilizada para manipular o I2C no Arduino e no ESP32.

```cpp
#include <Wire.h>

void setup() {
  Wire.begin();  // Inicializa o barramento I2C
  Serial.begin(115200);
}

void loop() {
  // Seu código aqui
}
```

### Comunicação I2C:

A comunicação I2C é iniciada pelo mestre (ESP32) e pode envolver um ou mais dispositivos escravos. A comunicação consiste em transferências de dados em bytes. O mestre envia um endereço de dispositivo seguido por dados ou recebe dados do dispositivo escravo.

#### Enviando dados para um dispositivo escravo:

```cpp
#include <Wire.h>

void setup() {
  Wire.begin();
  Serial.begin(115200);
}

void loop() {
  Wire.beginTransmission(8); // 8 é o endereço do dispositivo escravo
  Wire.write(42);            // Dado a ser enviado
  Wire.endTransmission();
  delay(500);
}
```

#### Recebendo dados de um dispositivo escravo:

```cpp
#include <Wire.h>

void setup() {
  Wire.begin();
  Serial.begin(115200);
}

void loop() {
  Wire.requestFrom(8, 6); // Solicita 6 bytes do dispositivo escravo com endereço 8
  while (Wire.available()) {
    char c = Wire.read(); // Lê os dados recebidos
    Serial.print(c);
  }
  delay(500);
}
```

### Definindo Endereços para Dispositivos Escravos:

Cada dispositivo escravo em um barramento I2C precisa ter um endereço único. O endereço padrão de 7 bits é frequentemente usado. No exemplo acima, o endereço do dispositivo escravo é definido como 8. Para definir um endereço diferente, você deve usar jumpers ou configurações específicas do dispositivo escravo.

Espero que estas informações tenham sido úteis para entender como funciona a comunicação I2C no ESP32. Se precisar de mais detalhes ou esclarecimentos, sinta-se à vontade para perguntar.
