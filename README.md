# MindSpace – Global Solution (DevOps)

O MindSpace é um assistente digital de bem-estar voltado para ambientes de trabalho híbridos. Ele identifica sinais de estresse, sugere pausas inteligentes, exercícios mentais rápidos e recomendações personalizadas para ajudar colaboradores a manterem equilíbrio emocional durante a rotina. A solução foi implementada na Azure utilizando duas VMs: uma VM Linux (Ubuntu Server 20.04) responsável pela API em Spring Boot, e uma VM Windows Server 2019 que hospeda o Dashboard/Admin desenvolvido em .NET. O banco de dados utilizado é o Oracle (instância ORCL da FIAP), acessado pela API via JDBC. A comunicação entre as máquinas ocorre via HTTP/HTTPS, com segurança controlada pelo NSG configurado na VNet.

**Integrantes:**  
Henrique Marques Sladkevicius – RM560698  
Luann Noqueli Klochko – RM560313  
Lucas Higuti Fontanezi – RM561120  

**Tecnologias utilizadas:**  
Backend (API): Java 17, Spring Boot 3, Maven, Oracle JDBC, JPA/Hibernate  
Frontend (Dashboard): .NET SDK 8.0, C#  
Banco: Oracle FIAP (ORCL), SQL Developer  

## Como rodar Backend (API):

Para rodar o backend do MindSpace, siga os passos abaixo:

```bash
git clone https://github.com/gsmindspace/gs-devops.git
cd gs-devops/backend
mvn clean package
java -jar target/mindspace-api.jar

```
## Como rodar Frontend (Dashboard .NET)

O frontend do MindSpace é um dashboard web desenvolvido em .NET, responsável por permitir que gestores e equipes de RH visualizem os dados consolidados de bem-estar dos colaboradores. A partir desse painel, é possível acompanhar indicadores gerados pela API (como sessões de trabalho, registros de humor e sinais de estresse) e utilizar essas informações como apoio às decisões de People Analytics.

O projeto foi construído utilizando **.NET SDK 8.0** e C#, seguindo a arquitetura web padrão da plataforma. O dashboard se comunica com a API do MindSpace via HTTP/HTTPS, consumindo os endpoints expostos pela aplicação em Spring Boot hospedada na VM Linux. Dessa forma, o frontend funciona como a camada de apresentação da solução, exibindo de forma amigável os dados armazenados no banco Oracle da FIAP.

Para executar o frontend localmente, após clonar o repositório, utilize:

```bash
cd gs-devops/frontend
dotnet restore
dotnet run

