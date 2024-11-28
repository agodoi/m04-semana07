# Atendimento do Professor

## Terças e quintas. Professor de horário parcial. Nesses 2 dias, podem contar comigo!

# Semama 07 - Transmissão de Sinal e Dashboard (Atividade Ponderada em Sala)

## Impactos no seu Projeto

* Investigação profissional da qualidade do sinal WiFi entre um IoT (ESP32) e o roteador local;
* Entendimento prático do efeito Gaiola de Faraday;
* Entendimento prático do que é um dBm.

# Problema:

#### Imagine que a conexão entre roteador e ESP32 não esteja estável, com falhas de autenticação ou excessos daqueles pontinhos no processo de conexão.

#### Como investigar e como resolver?


# Entendendo o dB e o dBm

O **dBm** é uma unidade de medida que expressa a potência de um sinal em **decibéis** (dB) em relação a **1 milivatt (mW)**. É uma medida logarítmica utilizada para avaliar a intensidade de um sinal de transmissão ou recepção, como o sinal de Wi-Fi em uma rede LAN. Foi criado pelo Graham Bell como forma de medir sua invensão, o sinal do telefone nas casas dos clientes.

- **dB** (decibéis) é uma medida relativa, usada para comparar níveis de potência.
- **dBm** é uma medida absoluta, referida a uma potência de 1 mW.

A fórmula para converter a potência em watts para dBm é:


![Formula](https://latex.codecogs.com/png.latex?\text{dBm}=10\cdot\log_{10}\left(\frac{P}{1\\text{mW}}\right))


Por exemplo:
- Se a potência P do sinal é de 1 mW, o valor em dBm será 0 dBm.
- Se a potência P é 10 mW, o valor será 10 dBm.

Curiosidade: a presença do 10 na fórmula apelidou de 10 Bells ou Decibel.

### (5.1) Importância do dBm na Medição de Sinal Wi-Fi e do ESP32

No contexto de redes LAN, particularmente para redes Wi-Fi, o **dBm** é importante para avaliar a **qualidade e a intensidade do sinal**. Ele indica o nível de potência que um dispositivo está recebendo do ponto de acesso (AP - Access Point). Como o sinal de Wi-Fi tende a se atenuar à medida que se distancia do roteador ou encontra obstáculos (como paredes), o valor de dBm ajuda a determinar a qualidade da conexão.

### (5.2) Interpretação dos Valores de dBm

Como o dBm é uma escala logarítmica, números mais negativos indicam sinais mais fracos. Veja uma escala de interpretação comum para redes Wi-Fi:

- **0 a -30 dBm**: sinal excelente. O dispositivo está muito próximo ao roteador, e a conexão será muito rápida e estável.
- **-31 a -50 dBm**: sinal muito bom. Ainda proporciona alta qualidade de conexão.
- **-51 a -60 dBm**: sinal bom. A maioria das aplicações funcionará sem problemas.
- **-61 a -70 dBm**: sinal aceitável. Pode haver alguma queda na velocidade ou na estabilidade da conexão, especialmente em ambientes congestionados.
- **-71 a -80 dBm**: sinal fraco. A conexão pode ser instável, com quedas de velocidade ou interrupções.
- **-81 dBm ou mais fraco**: sinal muito fraco ou inexistente. Provavelmente, o dispositivo não conseguirá se conectar.

### (5.3) Por que Medir o dBm em Redes Wi-Fi?

- **Otimização de Cobertura**: medir o dBm permite identificar pontos "cegos" ou áreas de sinal fraco dentro de um ambiente, especialmente no local do seu projeto. Isso ajuda a otimizar a localização de roteadores ou pontos de acesso.
  
- **Diagnóstico de Problemas de Conexão**: se um dispositivo estiver experimentando problemas de conexão, medir o dBm pode ajudar a diagnosticar se o problema é causado por um sinal fraco.

- **Configuração de Redes Mesh**: em redes Wi-Fi que utilizam tecnologia Mesh, a medição de dBm ajuda a posicionar os nós de forma eficiente para maximizar a cobertura e minimizar a interferência.

- **Análise de Interferência**: o dBm também pode ser utilizado para detectar interferências de outros dispositivos que operam na mesma frequência, como micro-ondas ou telefones sem fio, permitindo ajustes no canal de operação do Wi-Fi.


### (5.4) Qual a diferença entre dBm e dB?

A diferença entre **dBm** e **dB** está relacionada ao contexto de uso e à referência de medição:


### 5.4.1 dB (decibel)

- **Definição:** 
  - Uma unidade de medida relativa, que expressa a razão entre duas potências, intensidades ou amplitudes.
  - É adimensional e não tem uma referência fixa.
    
- **Fórmula:**
  - Para potências:  

   ![Equação de Potências](https://latex.codecogs.com/png.latex?\text{dB}=10\cdot\log_{10}\left(\frac{P_1}{P_2}\right))

    Onde \(P_1\) e \(P_2\) são as potências comparadas.

   - Para amplitudes (como tensões ou correntes):  

   ![Equação de Amplitudes](https://latex.codecogs.com/png.latex?\text{dB}=20\cdot\log_{10}\left(\frac{A_1}{A_2}\right))


    Onde \(A_1\) e \(A_2\) são as amplitudes comparadas.

- **Uso:**  
  - Medir ganhos, perdas ou relações relativas, como o ganho de um amplificador ou a atenuação de um sinal.
  - Não especifica valores absolutos; é sempre uma relação.

---

### 5.4.2 dBm (decibel-miliwatts)

- **Definição:**  
  - Uma unidade de medida **absoluta** que expressa a potência de um sinal **em relação a 1 miliwatt (mW)**.

- **Fórmula:**

 ![Equação dBm](https://latex.codecogs.com/png.latex?\text{dBm}=10\cdot\log_{10}\left(\frac{P}{1\\text{mW}}\right))

  Onde \(P\) é a potência medida em miliwatts.

- **Uso:**  
  - Medir a potência absoluta de sinais em sistemas de telecomunicações, rádio e redes.
  - Compara diretamente a potência a 1 mW, tornando-o útil para escalas absolutas.

---

### **Diferenças-chave**
| Característica      | dB                                | dBm                                  |
|---------------------|-----------------------------------|---------------------------------------|
| **Tipo de medida**  | Relativa (razão entre duas grandezas) | Absoluta (potência em relação a 1 mW) |
| **Referência fixa** | Não tem                          | 1 mW                                 |
| **Unidade associada** | Nenhuma (é adimensional)        | mW (potência absoluta)               |
| **Uso principal**   | Ganhos/perdas em amplificadores ou sinais | Potência absoluta em sistemas de RF e telecom |

---

### Exemplo Prático:
1. **dB (relativo):** Um amplificador aumenta a potência de um sinal de 10 mW para 100 mW. O ganho é:

   ![Equação de Ganho](https://latex.codecogs.com/png.latex?\text{Ganho%20(dB)}=10\cdot\log_{10}\left(\frac{100}{10}\right)=10\\text{dB})

2. **dBm (absoluto):** Se um sinal tem 50 mW de potência, sua medida em dBm é:

   ![Equação de Potencia](https://latex.codecogs.com/png.latex?\text{Potencia%20(dBm)}=10\cdot\log_{10}\left(\frac{50}{1}\right)=16,99\\text{dBm})
   

### (5.4) Exercícios teóricos

**a)** Calcule o ganho em dB de um amplificador que excitado com 1W de sinal na entrada fornece 10W na saída:

Solução:
G = 10 . log(10/1)
G = 10 . log(10)
G = 10 . 1
G = 10dB

Ao calcular o ganho, não colocamos o W na frente do dBW.
o dBW vai aparecer quando vc disser que a PTX ou PRX é de tanto X [dBW]


**b)** Calcule o ganho em dB de um amplificador que excitado com 2W de sinal na entrada fornece 30W na saída:

**c)** Calcule o perda em dB de um amplificador que excitado com 1W de sinal na entrada fornece 0,5W na saída:


### Exemplos práticos

Um sinal WiFi está com 10dBm na entrada da antena do ESP32. Quanto isso vale na escala linear comparado com 1mW?

X 		= 10 . log (Pd / 1mW)

10dBm 	= 10. log (Pd / 1mW)

10dBm = 10. log (Pd / 1mW)		→ você pode cancelar os milis envolvidos

10/10 =     log (Pd)

1     =     log (Pd)

10^1  =	         Pd

Pd = 10mW	→ lembre-se que estava em mW no enunciado, então vc corta o mili nas contas, mas retorne ele no resultado.

#### Agora tente resolver esses valores

a) Converta 13dBm para escala linear

b) Converta 17dBm para escala linear

c) Converta -41dBm para escala linear

d) Converta -35dBm para escala linear

---

# Resumo

1. **O que é dBm?**
   - Unidade logarítmica para medir potência relativa ao referencial.
   - Conversão entre dBm e escala linear (potência em mW).

2. **Importância do dBm no ESP32**
   - Medição da qualidade de sinal Wi-Fi.
   - Relevância em projetos de IoT para otimizar conectividade e eficiência energética.

3. **Vantagens e Desvantagens**
   - **Vantagens**:
     - Monitoramento em tempo real da intensidade de sinal.
     - Diagnóstico de problemas de conectividade.
   - **Desvantagens**:
     - Valores negativos podem ser difíceis de interpretar.
     - Necessidade de calibrar equipamentos para medições precisas.


# Ponderada

Este projeto é composto de uma coleta de potência do sinal WiFi em dBm de uma rede WiFi usando um ESP32 e a publicação destes valores em uma dashboard de uma plataforma online. O projeto IoT deve posssuir um ESP32 conectado a um Wifi, medindo o sinal de radiofrequência e imprimindo os dados em dBm na porta serial da Arduino IDE, além de publicar tais valores para a plataforma. Elabore um código MQTT capaz de transferir o valor de dBm de cada instante para a plataforma online. Nesta plataforma online, configure um gráfico contínuo de valores do dBm (gráfico tempo x dBm), e realize testes em cenários distintos. No final, vá até o elevador do Inteli para simular a gaiola de Faraday. Mais detalhes, vá até o final dessa aula.

## Barema

SEM EVIDÊNCIAS [0%]
O projeto IoT não foi desenvolvido e não há evidências (vídeo) a ser entregue, ou o vídeo não está acessível.

INSUFICIENTE [25%]
O projeto IoT posssui um ESP conectado ao WiFi e mede o sinal de RF na porta serial da IDE.

BÁSICO [50%]
O projeto IoT posssui um ESP conectado ao WiFi, medindo o sinal de RF e imprimindo os dados em dBm na porta serial da IDE, mas NÃO roda um código-fonte MQTT e NEM nota-se a reação da plataforma online.

INTERMEDIÁRIO [75%]
O projeto IoT posssui um ESP conectado ao WiFi, medindo o sinal de RF e imprimindo os dados em dBm na porta serial da IDE, e rodando um código-fonte MQTT nota-se a reação da plataforma online, mas não mostra o teste do bloqueio de sinal.

AVANÇADO [100%]
O projeto IoT posssui um ESP conectado ao WiFi, medindo o sinal de RF e imprimindo os dados em dBm na porta serial da IDE, e rodando um código-fonte MQTT nota-se a reação da plataforma online, e o vídeo também mostra o teste do bloqueio de sinal.

# Exemplo de Código

### (1) Clássico Código Envia Dados ao Broker [Ubidots]

#### Esse código está atualizado e funcionando. Alterem as variáveis com const char para as suas credenciais.

Se você não mexeu com o Ubidots até agora, [BAIXE AS BIBLIOTECAS AQUI](https://help.ubidots.com/en/articles/748067-connect-an-esp32-devkitc-to-ubidots-over-mqtt)

```
#include "UbidotsEsp32Mqtt.h"

/****************************************
 * Define Constants
 ****************************************/

const char *WIFI_SSID = ""; // Put here your Wi-Fi SSID
const char *WIFI_PASS = ""; // Put here your Wi-Fi password

const char *UBIDOTS_TOKEN = "PEGAR O TOKEN INDIVIDUAL QUE CHEGOU NO SLACK DO SEU GRUPO"; //PROCURE PELO SEU TOKEN COM O SEU PROFESSOR DE PROG.
const char *DEVICE_LABEL = "coloque um nome sem caracteres especiais"; // Coloque o nome do dispositivo que você deseja apelidar
const char *VARIABLE_LABEL1 = "potenciometro"; // Coloque o nome da variável que deseja publicar
const char *VARIABLE_LABEL2 = "botao"; // Outra variável que será publicada
const char *CLIENT_ID = "godoi"; //PULO DO GATO! Coloque um nome qualquer para te identificar no Ubidots de 5 a 20 caracteres e que seja diferente dos demais integrantes
//esse cliente_id é apenas para não sobrepor os tópicos dentro da conta do Ubidots. Ele é importante aqui no código, mas não vai aparecer na sua dashboard do Ubidots.



Ubidots ubidots(UBIDOTS_TOKEN, CLIENT_ID); //essa linha é novidade

const int PUBLISH_FREQUENCY = 3000; // Update rate in milliseconds
unsigned long timer;
uint8_t pinPotenciometro = 34;
uint8_t pinBotao = 33;
uint8_t pinLED = 2;
bool statusLED = false;

/****************************************
 * Auxiliar Functions
 ****************************************/

void callback(char *topic, byte *payload, unsigned int length)
{
  Serial.print("Message arrived [");
  Serial.print(topic);
  Serial.print("] ");
  for (int i = 0; i < length; i++)
  {
    Serial.print((char)payload[i]);
  }
  Serial.println();
}

/****************************************
 * Main Functions
 ****************************************/

void setup()
{
  // put your setup code here, to run once:
  Serial.begin(115200);
  ubidots.setDebug(true);  // uncomment this to make debug messages available
  ubidots.connectToWifi(WIFI_SSID, WIFI_PASS);
  ubidots.setCallback(callback);
  ubidots.setup();
  ubidots.reconnect();
  pinMode(pinBotao, INPUT_PULLUP);
  pinMode(pinPotenciometro, INPUT);
  pinMode(pinLED, OUTPUT);

  timer = millis();
}

void loop()
{
  // put your main code here, to run repeatedly:
  if (!ubidots.connected())
  {
    ubidots.reconnect();
  }
  if (millis() - timer > PUBLISH_FREQUENCY) // triggers the routine every X seconds
  {
    float value1 = analogRead(pinPotenciometro);
    bool value2 = digitalRead(pinBotao);
    Serial.println(value1);
    Serial.println(value2);
    
    ubidots.add(VARIABLE_LABEL1, value1); // Insert your variable Labels and the value to be sent
    ubidots.add(VARIABLE_LABEL2, value2); // Insert your variable Labels and the value to be sent
    ubidots.publish(DEVICE_LABEL); //pode usar um único publish para várias variáveis
    timer = millis();
  }
  ubidots.loop();
}
```

### (2) Clássico Código de Rastreamento do dBm [ESP32]

```
void loop() {
  if (WiFi.status() == WL_CONNECTED) {
    int32_t dBm = WiFi.RSSI(); // RSSI fornece o valor em dBm
    Serial.printf("Nível de Sinal Wi-Fi: %d dBm\n", dBm);

    // Publicação no Ubidots
    if (millis() - last_publish > PUBLISH_INTERVAL) {
      ubidots.add(VARIABLE_LABEL, dBm);
      ubidots.publish(DEVICE_LABEL);
      last_publish = millis();
    }
  } else {
    Serial.println("Wi-Fi desconectado! Tentando reconectar...");
    WiFi.begin(SSID, PASSWORD);
  }
}
```

---

### Dicas de Implementação
- **Evite usar `delay()` maiores que 500ms** no loop para não prejudicar a sincronização de dados.
- Use o método `millis()` para controlar os intervalos de publicação.
- Ajustes as variáveis entre os dois códigos que funciona.
---

# Entregável e Regras do Ensaio do Mapa de Calor do WiFi

A) Faça um vídeo de até 7min monstrando o gráfico do Ubidots, o seu monitor Serial e o ESP32. Tudo no mesmo quadro. Tente dividir a tela compartilhando o Ubidots e o seu monitor Serial.

B) Visite os seguintes locais:

    1) sala de aula, monitore por 10s
    
    2) catraca principal, monitore por 10s
    
    3) suba para o 1º andar, vá até o posto do IT Bar, monitore por 10s
    
    4) ainda no 1º andar, entre no elevador e fique por lá com a porta fechada por 20s e monitore
    
    5) suba até 2º andar, vá até laboratório do André Leal, monitore por 10s
    
    6) vá até o final do mesanino 2, na última salinha de reunião, monitore por 10s
    
    7) dessa pelo elevador novamente sem ficar lá dentro
    
    8) saia do Inteli pela catraca principal e vá até o outro lado da rua, monitore por 10s.
    
    9) Encerre o vídeo lá.
    
C) Suba o vídeo no YouTube, deixe-o como não listado

D) Monte um relatório descrevendo como ficou o sinal em cada local e conclua as diferenças

E) Trave o seu relatório num PDF e adicione o link do YouTube e poste na Adalove

Prazo: começa na aula e fecha hoje até às 16h.


# Conclusão
- O monitoramento de dBm é fundamental para diagnosticar e otimizar conexões Wi-Fi em projetos IoT.
- O ESP32, aliado ao Ubidots, permite uma análise em tempo real e com interface amigável para dashboards.
