# Atendimento do Professor

## Terças e quintas. Professor de horário parcial. Nesses 2 dias, podem contar comigo!

# Semana 07 - Transmissão de Sinal e Dashboard (Atividade Ponderada em Sala)

## Impactos no seu Projeto

* Investigação profissional da qualidade do sinal WiFi entre um IoT (ESP32) e o roteador local;
* Entendimento prático do efeito Gaiola de Faraday;
* Entendimento prático do que é um dBm.

# Problema:

#### Imagine que a conexão entre roteador e ESP32 não esteja estável, com falhas de autenticação ou excessos daqueles pontinhos no processo de conexão.

#### Como investigar e como resolver?


# Entendendo o dB e o dBm

O **dBm** é uma unidade de medida que expressa a potência de um sinal em **decibéis** (dB) em relação a **1 milivatt (mW)**. É uma medida logarítmica utilizada para avaliar a intensidade de um sinal de transmissão ou recepção, como o sinal de Wi-Fi em uma rede LAN.

- **dB** (decibéis) é uma medida relativa, usada para comparar níveis de potência.
- **dBm** é uma medida absoluta, referida a uma potência de 1 mW.

A fórmula para converter a potência em watts para dBm é:


![Formula](https://latex.codecogs.com/png.latex?\text{dBm}=10\cdot\log_{10}\left(\frac{P}{1\\text{mW}}\right))


Por exemplo:
- Se a potência P do sinal é de 1 mW, o valor em dBm será 0 dBm.
- Se a potência P é 10 mW, o valor será 10 dBm.

O nome decibel faz referência ao bel; um decibel equivale a um décimo de bel.

### (5.1) Importância do dBm na Medição de Sinal Wi-Fi e do ESP32

No contexto de redes LAN, particularmente para redes Wi-Fi, o **dBm** é importante para avaliar a **qualidade e a intensidade do sinal**. Ele indica o nível de potência que um dispositivo está recebendo do ponto de acesso (AP - Access Point). Como o sinal de Wi-Fi tende a se atenuar à medida que se distancia do roteador ou encontra obstáculos (como paredes), o valor de dBm ajuda a determinar a qualidade da conexão.

### (5.2) Interpretação dos Valores de dBm

Como o dBm é uma escala logarítmica, números mais negativos indicam sinais mais fracos. A escala abaixo é apenas orientativa: os resultados variam com ruído, interferência, equipamento e requisitos da aplicação. Um valor de RSSI não garante sozinho desempenho nem estabilidade:

- **0 a -30 dBm**: sinal excelente. Pode indicar sinal muito forte; isso, isoladamente, não garante velocidade ou estabilidade.
- **-31 a -50 dBm**: sinal muito bom. Ainda proporciona alta qualidade de conexão.
- **-51 a -60 dBm**: sinal bom. Em geral indica sinal bom, mas outros fatores influenciam a conexão.
- **-61 a -70 dBm**: sinal aceitável. Pode haver alguma queda na velocidade ou na estabilidade da conexão, especialmente em ambientes congestionados.
- **-71 a -80 dBm**: sinal fraco. A conexão pode ser instável, com quedas de velocidade ou interrupções.
- **-81 dBm ou mais fraco**: sinal muito fraco; a conectividade pode ser prejudicada e depende do ambiente e do dispositivo.

### (5.3) Por que Medir o dBm em Redes Wi-Fi?

- **Otimização de Cobertura**: medir o dBm permite identificar pontos "cegos" ou áreas de sinal fraco dentro de um ambiente, especialmente no local do seu projeto. Isso ajuda a otimizar a localização de roteadores ou pontos de acesso.
  
- **Diagnóstico de Problemas de Conexão**: se um dispositivo estiver experimentando problemas de conexão, medir o dBm pode ajudar a diagnosticar se o problema é causado por um sinal fraco.

- **Configuração de Redes Mesh**: em redes Wi-Fi que utilizam tecnologia Mesh, a medição de dBm ajuda a posicionar os nós de forma eficiente para maximizar a cobertura e minimizar a interferência.

- **Análise de Interferência**: variações de RSSI podem motivar uma investigação, mas não identificam a causa da interferência por si só. Para investigar ruído e canais, são necessárias outras medições e ferramentas apropriadas.


### (5.4) Qual a diferença entre dBm e dB?

A diferença entre **dBm** e **dB** está relacionada ao contexto de uso e à referência de medição:


### 5.4.1 dB (decibel)

- **Definição:** 
  - Uma medida logarítmica que expressa uma razão entre grandezas compatíveis, como duas potências.
  - É adimensional e não tem uma referência fixa.
    
- **Fórmula:**
  - Para potências:  

   ![Equação de Potências](https://latex.codecogs.com/png.latex?\text{dB}=10\cdot\log_{10}\left(\frac{P_1}{P_2}\right))

    Onde \(P_1\) e \(P_2\) são as potências comparadas.

   - Para amplitudes (como tensões ou correntes), ao comparar potências com impedâncias equivalentes:  

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

Em um exemplo matemático, considere uma potência de 10 dBm. Quanto isso vale na escala linear, em mW? Esse valor é ilustrativo e não representa uma leitura típica de RSSI nesta prática.

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

Nesta atividade, você investigará a intensidade do sinal Wi-Fi recebido por um ESP32 em diferentes locais do Inteli e apresentará os resultados em **dBm**. O ESP32 utiliza a rede IoT e publica a telemetria no broker local da sala. Seu grupo deverá visualizar o RSSI no Monitor Serial e desenvolver, na própria instância do **Node-RED**, um gráfico de RSSI em função do tempo.

O `inteli_broker.h` usado na turma **já adiciona o campo `rssi` à telemetria** a partir de `WiFi.RSSI()`. Portanto, não é necessário programar uma segunda publicação MQTT para esse mesmo valor. No sketch `.ino`, você também fará a leitura para mostrá-la no Monitor Serial.

**Configuração do Node-RED:** cabe aos alunos identificar o tópico de telemetria do próprio ESP32, tratar o payload e configurar o fluxo e o dashboard para exibir o campo `rssi` em dBm. Não há um fluxo pronto fornecido neste enunciado. O grupo deve utilizar a sua própria instância e os dados de acesso enviados pelo professor no canal privado.

O ESP32 se conecta à rede IoT do roteador da sala; o notebook acessa, preferencialmente, o Node-RED pela rede institucional. O ensaio investiga o sinal **da rede à qual o ESP32 está conectado**, e não o sinal de qualquer rede Wi-Fi disponível nos locais visitados.

### Atenção ao ensaio de deslocamento

O broker é local. Ao se afastar do roteador ou entrar no elevador, o ESP32 pode perder o Wi-Fi e, consequentemente, a conexão com o broker. Nesse período, o dashboard pode parar de atualizar. **Não interprete o último ponto do gráfico como uma leitura atual** e não considere `0 dBm` uma leitura de desconexão. Registre no vídeo e no relatório quando ocorrer uma desconexão, uma reconexão ou uma lacuna de dados.

Com o `inteli_broker.h` desta aula, não há garantia de armazenamento e reenvio posterior das leituras feitas fora de conexão; também não há um RSSI válido da conexão anterior após a desconexão. O teste no elevador é uma observação de atenuação ou perda de sinal em um ambiente com superfícies metálicas: o resultado, sozinho, não comprova uma gaiola de Faraday ideal. Faça os deslocamentos e o registro seguindo as condições permitidas no local.

## Barema

**SEM EVIDÊNCIAS [0%]**  
O projeto IoT não foi desenvolvido e não há evidências em vídeo, ou o vídeo está inacessível.

**INSUFICIENTE [25%]**  
O projeto possui um ESP32 conectado ao Wi-Fi e apresenta a medição do RSSI em dBm no Monitor Serial.

**BÁSICO [50%]**  
O ESP32 mede o RSSI e exibe os valores no Monitor Serial, mas não há evidência de publicação MQTT no broker local nem de visualização correspondente no Node-RED.

**INTERMEDIÁRIO [75%]**  
O ESP32 apresenta o RSSI no Monitor Serial, publica a telemetria no broker local e demonstra os dados no Node-RED, mas o vídeo não mostra o teste de bloqueio ou atenuação de sinal.

**AVANÇADO [100%]**  
O ESP32 apresenta o RSSI no Monitor Serial, publica a telemetria no broker local, demonstra os dados no Node-RED e mostra o teste de atenuação ou perda de sinal. Se ocorrer desconexão, ela deve ser registrada como resultado do teste, sem inventar dados para o período sem conexão.

# Exemplo de código: RSSI com o broker local

## Preparação

1. Use o arquivo **`inteli_broker.h` fornecido para sua turma** e mantenha-o na mesma pasta do sketch `.ino`. Não altere as configurações do cabeçalho.
2. Na Arduino IDE, instale o suporte à placa ESP32 e a biblioteca **PubSubClient, de Nick O’Leary**. A biblioteca `WiFi.h` acompanha o suporte ao ESP32.
3. Escolha um ID disponível dentro da faixa informada ao seu grupo. O ID `222` abaixo é apenas um exemplo da faixa do Grupo 3 da T29; troque-o pelo ID adequado. Não use o mesmo ID em duas placas conectadas ao mesmo tempo.
4. Abra o Monitor Serial em **115200 baud**. A preparação e a exibição no Node-RED são responsabilidade do grupo.

```cpp
#include "inteli_broker.h"  // Cabeçalho configurado pelo professor para a turma.

const int ID_DISPOSITIVO = 222; // Troque por um ID livre da faixa do grupo.
const unsigned long INTERVALO_SERIAL_MS = 5000;
unsigned long ultimaLeituraSerial = 0;

void setup() {
  Serial.begin(115200);
  InteliBroker.begin(ID_DISPOSITIVO);
}

void loop() {
  // Mantém a conexão e a publicação periódica da telemetria.
  InteliBroker.loop();

  // Exibe localmente o RSSI; não cria uma segunda publicação MQTT.
  if (millis() - ultimaLeituraSerial >= INTERVALO_SERIAL_MS) {
    ultimaLeituraSerial = millis();

    if (WiFi.status() == WL_CONNECTED) {
      int rssi = WiFi.RSSI();
      Serial.printf("RSSI do Wi-Fi: %d dBm\n", rssi);
    } else {
      Serial.println("Wi-Fi desconectado: RSSI indisponível.");
    }
  }
}
```

## Como o valor chega ao Node-RED?

O arquivo `inteli_broker.h` da turma lê o sinal por meio de `WiFi.RSSI()` e inclui esse valor como `rssi` na mensagem de telemetria. Com o cabeçalho usado na semana 05, o tópico segue o padrão `inteli/iot/<ID>/telemetria`. Para o ID 222, por exemplo:

```text
inteli/iot/222/telemetria
```

Exemplo ilustrativo de uma mensagem:

```json
{"device":222,"seq":3,"rssi":-65,"uptime_ms":15000,"reconnects":1}
```

O grupo deverá identificar e apresentar o campo **`rssi`**, com unidade **dBm**, em um gráfico de tempo por RSSI no Node-RED. Verifique o formato da mensagem e o tópico efetivamente recebido. O gráfico não é criado automaticamente pelo broker nem pelo `.ino`.

> O cabeçalho utilizado na semana 05 publica aproximadamente a cada 5 segundos enquanto a conexão estiver ativa. A impressão no Monitor Serial e a publicação têm temporizadores independentes: seus instantes e valores podem não ser exatamente iguais. Confira se o `.h` efetivamente fornecido à turma mantém o campo e o intervalo indicados. Durante a conexão inicial ou uma reconexão, o cabeçalho pode esperar ou reiniciar o ESP32, e as mensagens no Monitor Serial dependem da execução do `loop()`.

### Dicas de implementação

- Mantenha `InteliBroker.loop()` sendo executado frequentemente.
- Use `millis()` para controlar a impressão no Monitor Serial sem interromper o programa com esperas longas.
- A instância Node-RED e suas credenciais são do grupo. Não compartilhe a senha do editor em canais públicos nem em vídeos ou repositórios.
- Observe que o gráfico depende da configuração feita pelo grupo e da comunicação ativa entre ESP32, broker e Node-RED.

---

# Entregável e Regras do Ensaio do Mapa de Calor do WiFi

A) Mantenha o celular na horizontal e faça um vídeo CONTÍNUO (sem cortes) de até 10 minutos mostrando o gráfico do Node-RED, o Monitor Serial e o ESP32 no mesmo quadro. Organize a visualização de modo que o gráfico e o Monitor Serial possam ser acompanhados. Registre também eventuais desconexões ou interrupções no gráfico.

B) Visite os seguintes locais:

    1) sala de aula, monitore por 10s
    
    2) catraca da recepção (onde tem uma bancada com recepcionistas), monitore por 10s
    
    3) suba para o 1º andar, vá até o posto do IT Bar, monitore por 10s
    
    4) ainda no 1º andar, entre no elevador e fique por lá com a porta fechada por 20s e monitore
    
    5) suba até 2º andar, vá até laboratório do André Leal, monitore por 10s
    
    6) vá até o final do mesanino 2, na última salinha de reunião, monitore por 10s
    
    7) dessa pelo elevador novamente sem ficar lá dentro
    
    8) saia do Inteli pela catraca da recepção e vá até a quadra de areia e monitore por 10s.
    
    9) Encerre o vídeo lá.
    
C) Suba o vídeo no YouTube, deixe-o como **não listado**. Vídeos do Google Drive não serão aceitos.

D) Monte um relatório descrevendo como ficou o sinal em cada local e conclua as diferenças

E) Trave o seu relatório num PDF e adicione o link do YouTube e poste na Adalove

Prazo: começa na aula e fecha hoje até às 18h.


# Conclusão
- O monitoramento de dBm é fundamental para diagnosticar e otimizar conexões Wi-Fi em projetos IoT.
- O ESP32 publica o RSSI no broker local, e o Node-RED pode apresentar os dados em um dashboard configurado pelo grupo.
