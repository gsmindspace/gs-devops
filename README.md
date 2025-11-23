# 🧠 MindSpace - Global Solution 2025

**Tema:** O Futuro do Trabalho - Saúde Mental e Bem-Estar Corporativo

O **MindSpace** é uma solução integrada de IoT, Mobile e Cloud Computing projetada para monitorar e melhorar a saúde mental de colaboradores em regime de trabalho híbrido. O sistema utiliza sensores (simulados) para detectar níveis de estresse e sugere pausas proativas através de um aplicativo móvel, com todos os dados persistidos de forma segura em nuvem.

---

## 👨‍💻 Integrantes do Grupo

* **Luann Noqueli** (RM560313) - DevOps Engineer & IoT Specialist
* **Henrique Marques** (RM560698) - Back-End Engineer (Java & .NET)
* **Lucas Higuti** (RM561120) - Database & QA Architect

---

## 🎥 Links e Repositórios do Projeto

Para facilitar a avaliação, o código-fonte da solução foi segmentado em repositórios específicos por disciplina:

* **📱 Front-End (Mobile) & Documentação Geral:**
    * [LINK DO SEU REPOSITÓRIO PRINCIPAL (2TDSPA-GS1-MINDSPACE)]
    * *Contém: App React Native, Documentação de DevOps e Arquitetura.*

* **☕ Back-End (API Java):**
    * https://github.com/Henrique-error404/MindSpace_API.git
    * *Contém: API Spring Boot, Configurações de Segurança e Data Seeder.*

* **🤖 IoT (Sensores & Gateway):**
    * https://github.com/gsmindspace/gs-IoT.git
    * *Contém: Código C++ (Wokwi) e Fluxo JSON (Node-RED).*

---

### 📺 Vídeos de Demonstração

* **Vídeo 1 - DevOps, Cloud & CRUD:** [INSIRA O LINK DO YOUTUBE AQUI]
    * *Demonstração da infraestrutura Azure, deploy da API e persistência de dados.*
* **Vídeo 2 - Solução IoT:** https://youtu.be/9l0gPTwwPfQ
    * *Demonstração do sensor, gateway Node-RED e integração com o Back-End.*

## ☁️ Arquitetura da Solução (Cloud & DevOps)

A infraestrutura foi implantada na **Microsoft Azure**, seguindo o requisito de separação de ambientes e sistemas operacionais distintos.

### 🏗️ Recursos Azure
* **Resource Group:** `RG-MindSpace-PROD` (Brazil South)
* **Rede Virtual (VNet):** `VNet-MindSpace` (Conectividade privada entre as VMs)
* **Segurança (NSG):** `NSG-MindSpace` (Firewall configurado com regras estritas)

### 🖥️ Servidores (Virtual Machines)

#### 1. VM Linux (Servidor de Aplicação / Back-End)
* **Função:** Hospeda a API RESTful (Spring Boot) que centraliza a lógica de negócio.
* **OS:** Ubuntu Server 20.04 LTS
* **Size:** `Standard_B2s` (2 vCPUs, 4 GiB RAM) - *Upgrade realizado para suportar a compilação Maven.*
* **Stack Instalada:**
    * OpenJDK 21 (Atualizado para compatibilidade com Spring Boot 3)
    * Maven 3.6+ (Build Tool)
    * Git (Versionamento)
* **Endpoint:** `http://<IP_PUBLICO>:8080/registros`

#### 2. VM Windows (Servidor Administrativo / Front-End)
* **Função:** Estação de gerenciamento, testes de banco de dados e hospedagem da API de RH (.NET).
* **OS:** Windows Server 2019 Datacenter
* **Size:** `Standard_B2s`
* **Stack Instalada:**
    * .NET SDK 8.0
    * Oracle SQL Developer (Para validação da persistência)
    * Git for Windows

---

## 🛡️ Configuração de Segurança (NSG)

O **Network Security Group** foi configurado para permitir apenas o tráfego necessário:

| Prioridade | Porta | Protocolo | Origem | Ação | Finalidade |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **100** | 22 | TCP | Qualquer | Allow | Acesso SSH administrativo (Linux) |
| **110** | 3389 | TCP | Qualquer | Allow | Acesso RDP administrativo (Windows) |
| **120** | 8080 | TCP | Qualquer | Allow | Tráfego HTTP da API (Mobile & IoT) |
| **65500** | * | * | * | Deny | Bloqueio padrão de todo o resto |

---

## 🚀 Guia de Deploy (Como rodar o projeto)

### Pré-requisitos
* Acesso SSH à VM Linux.
* As variáveis de ambiente do Banco de Dados Oracle devem estar configuradas no `application.properties` ou no ambiente.

### Passo 1: Deploy da API Java (Linux)
1.  Acesse a VM via SSH:
    ```bash
    ssh rm560313@<IP_PUBLICO_LINUX>
    ```
2.  Clone o repositório (ou atualize):
    ```bash
    git clone https://github.com/Henrique-error404/MindSpace_API.git
    cd MindSpace_API
    git pull
    ```
3.  Compile o projeto (Geração do .jar):
    ```bash
    mvn clean package -DskipTests
    ```
4.  Execute a API:
    ```bash
    java -jar target/mindspace-api-0.0.1-SNAPSHOT.jar
    ```
    *Aguarde a mensagem `Started MindSpaceApiApplication`.*

### Passo 2: Validação da Persistência (Windows)
1.  Acesse a VM Windows via RDP.
2.  Abra o **SQL Developer**.
3.  Conecte-se ao banco Oracle da FIAP.
4.  Execute a query para validar os dados inseridos pela API:
    ```sql
    SELECT * FROM SINAL_ESTRESSE ORDER BY DT_HORA DESC;
    ```

---

## 📱 Integração Mobile & IoT

### Mobile (React Native)
O aplicativo móvel consome a API hospedada na Azure para realizar o CRUD completo de registros de humor.
* **Configuração:** O IP da VM Linux deve ser atualizado em `src/services/api.ts`.

### IoT (Wokwi + Node-RED)
Um sensor simulado (ESP32) envia dados de estresse via MQTT para um Gateway Node-RED, que processa a lógica de alerta e envia para a API na Azure.
* **Fluxo:** Sensor -> MQTT Broker -> Node-RED -> HTTP POST (Porta 8080) -> API Java -> Oracle DB.

---

> **Nota:** Este projeto foi desenvolvido como parte da avaliação Global Solution da FIAP (2025).

