# **Relatório Técnico: Análise de Vulnerabilidades e Ataques no Servidor Web ESP32**

## **1. Análise Estática do Código com Descrição das Vulnerabilidades**

### **Vulnerabilidade 1: Entrada HTTP não Sanitizada**

- **Descrição**:  
  O servidor ESP32 processa requisições HTTP sem validar ou sanitizar as entradas recebidas. Isso permite que dados maliciosos sejam manipulados e interpretados diretamente pelo navegador.
  
- **Impacto**:  
  Torna o sistema vulnerável a ataques de **Cross-Site Scripting (XSS)**, onde um atacante pode injetar scripts maliciosos.

### **Vulnerabilidade 2: Conexão HTTP Insegura**

- **Descrição**:  
  O servidor utiliza o protocolo **HTTP** em vez de **HTTPS**, resultando em dados transmitidos sem criptografia.

- **Impacto**:  
  Facilita ataques de **Man-in-the-Middle (MITM)**, onde um atacante pode interceptar e modificar as comunicações entre o cliente e o servidor.

## **2. Análise Estática com Descrição dos Possíveis Ataques**

### **Ataque 1: Cross-Site Scripting (XSS)**

- **Descrição**:  
  Explorando a falta de sanitização das entradas, um atacante pode injetar scripts maliciosos que são executados no navegador do usuário.

### **Ataque 2: Man-in-the-Middle (MITM)**

- **Descrição**:  
  Aproveitando a falta de criptografia no HTTP, um atacante pode interceptar os dados transmitidos e modificar comandos ou informações enviadas entre o cliente e o ESP32.

## **3. Passo-a-Passo dos Dois Ataques**

### **Passo-a-Passo: Cross-Site Scripting (XSS)**

- **Preparar o Ambiente**:  
   - Carregar o código no ESP32.  
   - Conectar o ESP32 à rede Wi-Fi e verificar o endereço IP no monitor serial.

- **Injetar o Script**:  
   - Enviar a seguinte requisição pelo navegador:  
     ```
     http://<IP_DO_SEU_ESP32>/26/on<script>alert('XSS')</script>
     ```

- **Resultado Esperado**:  
   - Um alerta `XSS` aparecerá no navegador indicando que o script foi executado com sucesso.

### **Passo-a-Passo: Man-in-the-Middle (MITM)**

- **Captura do Tráfego**:  
   - Usar uma ferramenta como **Wireshark** para monitorar o tráfego na rede local.

- **Interceptação dos Pacotes**:  
   - Observar os comandos enviados ao ESP32, como `GET /26/on`.

- **Modificação dos Pacotes**:  
   - Injetar pacotes modificados para alterar o estado dos GPIOs sem autorização.

- **Resultado Esperado**:  
   - Controle indevido dos pinos GPIO do ESP32.

## **4. Probabilidade, Impacto e Risco dos Ataques**

| **Ataque**                   | **Probabilidade** | **Impacto**       | **Risco**        | **Justificativa**                                                                 |
|-------------------------------|------------------|-------------------|------------------|-----------------------------------------------------------------------------------|
| **Man-in-the-Middle (MITM)** | Alta             | Alto              | Alto             | HTTP sem criptografia torna a interceptação fácil em redes não seguras.           |
| **Cross-Site Scripting (XSS)**| Média/Alta       | Médio             | Médio            | Falta de sanitização permite injeção de scripts, afetando usuários e a interface. |

## **5. Tabela Consolidada dos Ataques**

| **Título do Ataque**          | **Probabilidade** | **Impacto** | **Risco** |  
|-------------------------------|------------------|-------------|-----------|  
| **Man-in-the-Middle (MITM)** | Alta             | Alto        | Alto      |  
| **Cross-Site Scripting (XSS)**| Média/Alta       | Médio       | Médio     |  

## **6. Análise Dinâmica com Teste de Ataque no ESP32**

### **Montagem e Teste do XSS**

- **Montagem em Protoboard**:  
   - Conectar o ESP32 a uma protoboard e configurar os pinos GPIO 26 e 27 com LEDs para visualizar os comandos.

- **Requisição Maliciosa**:  
   - Enviar a URL com o script malicioso:  
     ```
     http://<IP_DO_SEU_ESP32>/26/on<script>alert('XSS')</script>
     ```

- **Resultado**:  
   - O navegador exibiu um alerta `XSS`, confirmando a vulnerabilidade.

- **Evidências**:  
   - Captura de vídeo do alerta `XSS`.  
   - Foto da montagem do ESP32 em funcionamento.

### **Montagem e Teste do MITM**

- **Captura com Wireshark**:  
   - Interceptar comandos `GET` e visualizar os dados em texto claro.

- **Modificação dos Dados**:  
   - Alterar os pacotes interceptados para enviar comandos indesejados.

- **Resultado**:  
   - Os LEDs nos pinos GPIO mudaram de estado conforme os comandos manipulados.
