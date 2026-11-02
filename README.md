## 🦷 Agendamento Odontológico — API & CI/CD Pipeline
Projeto de implantação da API Spring Boot de Agendamento Odontológico, utilizando contêineres Docker, banco de dados MySQL hospedado na nuvem (Aiven), automação de testes e build via GitHub Actions e deploy contínuo no Render.

## 🚀 Tecnologias Utilizadas

Componente,Tecnologia,Descrição
Linguagem,Java 21,Linguagem principal do projeto
Framework,Spring Boot 3.x,Framework backend para APIs REST
Banco de Dados,MySQL 8 (Aiven),Instância MySQL em nuvem com conexão segura SSL
Migrations,Flyway,Gerenciamento e versionamento automatizado do banco
Containerização,Docker,Build multi-stage para otimização da imagem final
CI/CD,GitHub Actions,"Validação de código, testes de integração e validação da imagem"
Hospedagem,Render Web Service,Implantação e execução contínua do contêiner Docker

## ⚙️ Configuração de Variáveis de Ambiente
Para manter a segurança das credenciais e evitar a exposição de segredos no repositório, o arquivo application.properties utiliza variáveis de ambiente:

DB_URL: URL JDBC de conexão ao MySQL no Aiven (jdbc:mysql://...).

DB_USERNAME: Usuário de autenticação do banco de dados (avnadmin).

DB_PASSWORD: Senha de acesso ao banco de dados.

JWT_SECRET: Chave secreta de 256 bits para validação de tokens JWT.

PORT: Porta de execução (atribuída dinamicamente pelo Render ou 8080 localmente).

## Esteira de CI/CD (GitHub Actions)
A automação do fluxo de integração contínua foi estruturada no arquivo .github/workflows/agendamento-odontologico-cicd.yml. A cada commit ou pull request na branch main:

O runner Ubuntu baixa o código fonte do repositório.

É configurado o Java 21 (Temurin) com suporte a cache do Maven.

As credenciais cadastradas nos GitHub Secrets são injetadas no ambiente.

O comando mvn clean verify compila a aplicação, executa as migrações do Flyway e valida os testes de integração contra o banco no Aiven.

A imagem Docker da aplicação é construída e validada com a tag correspondente ao commit (${{ github.sha }}).

## 🩺 Health Check & Monitoramento
A saúde e a disponibilidade da aplicação no ar são monitoradas em tempo real através do Spring Boot Actuator:

URL Pública: https://agendamento-odontologico-entrega.onrender.com/actuator/health

Status do Serviço: UP

Probes Ativas: liveness e readiness

## 📸 Evidências de Funcionamento (Prints de Validação)
1. Construção e Validação da Imagem Docker Local
<img width="743" height="69" alt="image" src="https://github.com/user-attachments/assets/f1128319-132f-40fa-8e9a-75cfdd86f459" />

2. Banco de Dados MySQL Ativo no Aiven
<img width="1055" height="71" alt="image" src="https://github.com/user-attachments/assets/ff158d47-fabd-44f9-b0b4-6dda705c55ad" />

3. Implantação e Publicação no Render (Deploy Succeeded | Live)
<img width="1332" height="257" alt="image" src="https://github.com/user-attachments/assets/536284c3-be13-427a-9900-c578a39ce789" />

4. Endpoint de Health Check Ativo (/actuator/health)
<img width="1352" height="729" alt="image" src="https://github.com/user-attachments/assets/36ae204e-6b63-4744-956d-e939d79e2ff0" />


## 🛠️ Como Executar o Projeto Localmente
Pré-requisitos
Java 21 JDK instalado.

Docker Desktop configurado (com virtualização/SVM ativada na BIOS).

Maven ou IDE (IntelliJ IDEA / VS Code).

Execução Passo a Passo
Clone o repositório:

```Bash
git clone https://github.com/bielxcesar/agendamento-odontologico-entrega.git
cd agendamento-odontologico-entrega
```

Defina as variáveis de ambiente necessárias ou configure a execução na sua IDE:

```Bash
DB_URL=jdbc:mysql://SEU_HOST:PORTA/defaultdb?sslMode=REQUIRED
DB_USERNAME=avnadmin
DB_PASSWORD=SUA_SENHA
JWT_SECRET=SUA_CHAVE_SECRET
```
Execute a compilação e verificação de testes com o Maven:

```Bash
mvn clean verify
```
Crie e teste o contêiner Docker localmente:

```Bash
docker build -t agendamento-odontologico .
```
