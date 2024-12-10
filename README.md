# **Análise de Segurança do Servidor Web ESP32**

Este repositório contém um projeto de servidor web local rodando em um ESP32, com foco em identificar e explorar vulnerabilidades de segurança.

## **Conteúdo do Projeto**

- **Código do Servidor ESP32**: Código em C++ para criar um servidor web local com controle dos GPIOs 26 e 27.
- **Análise de Vulnerabilidades**: Descrição das vulnerabilidades identificadas no código.
- **Ataques Demonstrados**:  
  - **Cross-Site Scripting (XSS)**  
  - **Man-in-the-Middle (MITM)**
- **Relatório Técnico**: Detalhamento dos ataques, probabilidades, impactos e riscos.
- **Evidências**: Capturas de tela e fotos dos testes realizados.

## **Como Executar o Projeto**

1. **Requisitos**:
   - **ESP32**  
   - **Arduino IDE**  
   - **Biblioteca Wi-Fi** para ESP32

2. **Configuração**:
   - Substitua os valores de `ssid` e `password` no código pelo seu Wi-Fi:
     ```cpp
     const char* ssid = "Seu_SSID";
     const char* password = "Sua_Senha";
     ```

3. **Upload do Código**:
   - Carregue o código no ESP32 usando a **Arduino IDE**.

4. **Acesso ao Servidor**:
   - Abra o navegador e acesse o IP exibido no monitor serial, por exemplo:  
     ```
     http://xxx.xxx.xxx.xxx
     ```
