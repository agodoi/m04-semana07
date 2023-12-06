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

https://portal.vidadesilicio.com.br/descobrindo-o-endereco-i2c/


## Protocolo I2C

O barramento I2C (Inter-Integrated Circuit) é um protocolo de comunicação serial que permite a interconexão de vários dispositivos em um mesmo barramento. 

No ESP32, o I2C é implementado por meio de hardware e software. Veja na Fig. 1, como se comporta fisicamente as conexões eletrônica no barramento I2C.


<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m04-semana08/blob/main/imgs/barramentoI2C.png">
   <img alt="Boucing" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m04-semana08/blob/main/imgs/barramentoI2C.png)">
</picture>


Note que o mesmo par de fios SDA e SCL é usado para conectar todos os sensores. Não pode haver inversão desses pinos. Se isso acontecer, toda a comunicação será interrompida. A função de cada pino é a seguinte:

- **SDA (Serial Data Line):** Pino para a linha de dados. Este pino é usado para enviar e receber dados.
- **SCL (Serial Clock Line):** Pino para a linha de clock. Este pino é usado para sincronizar a transferência de dados entre dispositivos.

Na figura a seguir, é possível entender melhor como um projeto prático pode ser montado:

<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m04-semana08/blob/main/imgs/projetoPraticoI2C.png">
   <img alt="Circuito I2C" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m04-semana08/blob/main/imgs/projetoPraticoI2C.png)">
</picture>

## Quantidade de Dispositivos Suportados

O barramento de endereçamento I2C possui 7 bits. Isso significa que a quantidade de dispositivos suportados é de ```N = 2^7 = 128```. A faixa de endereços é dada na base hexadecimal. Portanto, você deve usar o número hexadecimal de **00** até **7F**.

Contudo, alguns dispositivos I2C já possuem um endereço fixo entre 00 e 7F. Ao invés de tentar encontrar na sorte de qual endereço tal dispositivo está fixado, use esse código para você varrer os endereços. Esse código-fonte pergunta ao dispositivo, qual o endereço ele está respondendo. Note que a rotina de varredura conta de 0 a 127, mas o resultado impresso no monitor serial é convertido para hexadecimal:

```
#include <Wire.h>
 
void setup() {
  Wire.begin();
  Serial.begin(115200);
  Serial.println("\nScanner I2C");
    byte error, address;
  int nDevices;
  Serial.println("Varrendo...");
  nDevices = 0;
  for(address = 1; address < 127; address++ ) {
    Wire.beginTransmission(address);
    error = Wire.endTransmission();
    if (error == 0) {
      Serial.print("Dispositivo I2C encontrado no endereço 0x");
      if (address<16) {
        Serial.print("0");
      }
      Serial.println(address,HEX);
      nDevices++;
    }
    else if (error==4) {
      Serial.print("Erro desconhecido no endereço 0x");
      if (address<16) {
        Serial.print("0");
      }
      Serial.println(address,HEX);
    }    
  }
  if (nDevices == 0) {
    Serial.println("Nenhum dispositivo I2C encontrado\n");
  }
  else {
    Serial.println("pronto\n");
  }
  delay(5000);  
  Serial.print("Dispositivos I2C encontrados:");
  Serial.println(nDevices); 
}
 
void loop() {
      
}
```

### Configuração do Barramento I2C:

Para usar o I2C no ESP32, é necessário inicializar e configurar o barramento. A biblioteca mais usada para o I2C chama-se **Wire.h**.

```
#include <Wire.h>

void setup() {
  Wire.begin();          // Inicializa o barramento I2C
  Serial.begin(115200);  // Inicializa a comunicação UART, que nesse caso, ocorre pelo cabo USB.
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
