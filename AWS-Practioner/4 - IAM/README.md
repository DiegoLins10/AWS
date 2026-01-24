# 🛡️ AWS Cloud Practitioner (CLF-C02) - IAM Essentials

Este README contém um resumo sobre os principais conceitos de **IAM (Identity and Access Management)**, **IAM Identity Center**, **MFA** e **AWS Organizations** para a certificação **AWS Certified Cloud Practitioner CLF-C02**.

---

## 📌 IAM (Identity and Access Management)

O **IAM** permite gerenciar **usuários**, **grupos**, **funções (roles)** e **permissões** na conta AWS.

### ✅ Criar Usuários
- Um **usuário IAM** representa uma identidade com permissões definidas.
- Pode ser usado por uma pessoa ou um aplicativo.

### ✅ Criar Grupos de Usuários
- Um **grupo IAM** é um conjunto de usuários com permissões semelhantes.
- Permite aplicar políticas de maneira centralizada.

### ✅ Criar Roles (Funções)
- **Roles** são identidades com permissões atribuídas que **podem ser assumidas** por usuários, serviços AWS ou contas externas.

---

## 🔐 IAM Identity Center (Sucessor do AWS SSO)

- O **IAM Identity Center** é a nova abordagem recomendada para gerenciar **identidades e acessos centralizados**.
- Permite:
  - Criar usuários diretamente no console.
  - Conectar-se a diretórios externos (como Active Directory ou Okta).
  - Gerenciar permissões de múltiplas contas AWS de forma centralizada.

> ✅ **Recomendado** para novos projetos em vez de usuários IAM individuais.

---

## 🔒 MFA - Multi-Factor Authentication

- MFA adiciona uma camada extra de segurança.
- Exige **algo que o usuário sabe (senha)** + **algo que o usuário tem (token)**.

### Tipos de MFA:
- Aplicativos: **Google Authenticator**, **Authy**, **AWS Virtual MFA**.
- Dispositivos físicos: chaves U2F como **YubiKey**.

> ✅ **Boa prática:** Habilitar MFA para o usuário root e usuários com acesso privilegiado.

---

## 🏢 AWS Organizations

- O **AWS Organizations** permite **gerenciar múltiplas contas AWS** de forma centralizada.
- Cria-se uma **Organização** com contas-membro sob uma conta-mestre (gerenciamento centralizado).

### Principais benefícios:
- **Consolidação de cobrança (consolidated billing)**.
- Aplicação de **políticas de serviço (SCPs)** que controlam o que as contas podem fazer.
- Separação de ambientes por conta (ex: Produção, Desenvolvimento, Financeiro).

### Componentes importantes:
- **Organizational Units (OUs):** Agrupam contas com regras similares.
- **Service Control Policies (SCPs):** Impõem limites máximos de permissões.

> ✅ Ideal para ambientes corporativos com múltiplas equipes/unidades de negócio.

---

### 🧠 Quando usar: **Grupos**, **Roles**, e **Políticas** na AWS

| Recurso       | Quando Usar                                                                                                                                                                                                         |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Grupos**    | Quando você tem **vários usuários** que precisam das **mesmas permissões**. Ex: grupo "Desenvolvedores" com acesso ao S3 e EC2.                                                                                     |
| **Roles**     | Quando você quer conceder **acesso temporário** ou delegar permissões a **outros serviços AWS**, **contas externas** ou **usuários IAM/Identity Center**. Ex: uma função que permite uma Lambda acessar o DynamoDB. |
| **Políticas** | São os documentos JSON que definem **quais ações** são permitidas ou negadas. Elas são **anexadas a usuários, grupos ou roles**. Ex: política que permite `s3:GetObject` em um bucket específico.                   |

---

## Politica padrao de senha aws
Tamanho mínimo da senha
- 8 caracteres
- Intensidade da senha
- Inclua no mínimo três dos seguintes tipos de caracteres:

- Maiúsculas
- Minúsculas
- Números
- Caracteres não alfanuméricos

### Outros requisitos
- Nunca expirar senha
- Não deve ser idêntico ao nome ou endereço de e-mail da sua conta da AWS


## Cloudshell e CLI

Existem 3 formas para acessar e interagir com o aws services

1 - Console Web
2 - AWS CLI
3 - CloudShell

---

## ☁️ O que é o **AWS CloudShell**?

O **AWS CloudShell** é um terminal (shell) baseado na web que você acessa direto pelo navegador no console da AWS. Ele já vem configurado com as ferramentas da AWS, como o **AWS CLI**, além de outras como `Python`, `bash`, `git`, etc.

👉 Com ele, você pode rodar comandos sem precisar instalar nada na sua máquina.

---

## 💻 O que é a **AWS CLI**?

A **AWS CLI (Command Line Interface)** é uma ferramenta para você interagir com os serviços da AWS diretamente pelo terminal ou prompt de comando. Com ela, você pode:

* Criar recursos (como usuários, buckets S3, funções Lambda etc.)
* Gerenciar permissões
* Automatizar tarefas

Você pode usar a AWS CLI tanto no **CloudShell** quanto na sua máquina local (após instalar e configurar).

---

## 🛠️ Script para criar um usuário na AWS via CLI

Aqui vai um script para criar um usuário simples usando o **AWS CLI** ou **CloudShell**:

```bash

# Nome do usuário
USERNAME="usuario-teste"

# 1. Criar o usuário
aws iam create-user --user-name $USERNAME

# 2. Criar um grupo (se quiser adicionar o usuário a um grupo)
aws iam create-group --group-name grupo-teste

# 3. Adicionar o usuário ao grupo
aws iam add-user-to-group --user-name $USERNAME --group-name grupo-teste

# 4. (Opcional) Anexar uma política ao grupo, como acesso total ao S3
aws iam attach-group-policy --group-name grupo-teste --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess

# 5. Criar credenciais de acesso (Access Key e Secret) para o usuário
aws iam create-access-key --user-name $USERNAME

---

## Acess Key e SDK

---

## 🔑 **Access Key**

* Conjunto de **credenciais** (2 partes):

  * `AccessKeyId` (como um usuário)
  * `SecretAccessKey` (como a senha)
* Usadas para **acessar a AWS programaticamente** (ex: via CLI, SDKs, scripts).
* **Não são usadas para acessar o console web**.
* Devem ser guardadas com segurança — a **Secret Access Key só aparece uma vez**!

---

## 🧰 **SDK (Software Development Kit)**

* Conjunto de **bibliotecas** para você usar a AWS direto no seu código.
* Existem SDKs para várias linguagens: **Python (Boto3)**, **Java**, **JavaScript**, **.NET**, **Go**, etc.
* Com um SDK, você pode:

  * Criar buckets S3
  * Ler dados do DynamoDB
  * Invocar funções Lambda
  * Entre muitas outras ações, tudo via código

### Exemplo: SDK em Python com Boto3

```python
import boto3

# Criando cliente usando Access Key e Secret
client = boto3.client(
    's3',
    aws_access_key_id='SUA_ACCESS_KEY',
    aws_secret_access_key='SUA_SECRET_KEY',
    region_name='sa-east-1'
)

# Listando buckets
buckets = client.list_buckets()
print(buckets)
```

---

### 📌 Conexão entre eles

| Acess Key                              | SDK                                     |
| -------------------------------------- | --------------------------------------- |
| São as **credenciais**                 | É o **código/libraria** para usar a AWS |
| Usada com SDKs e CLI                   | Usa a Access Key por trás               |
| Não é uma ferramenta, é dado de acesso | É uma ferramenta de programação         |

---

## Reports
## Credential Report (Relatorio de credenciais)

Aqui é possivel baixar as informações sobre os usuarios, se tem MTF, ultima troca de senha, etc. Está localizado dentro do IAM.

## Acess advisor (Consultor de acesso)

Ele mostra de uma forma simples os serviços permitidos para o usuario. Está localizado dentro do usuario.


## Resumo - IAM

O AWS Identity and Access Management (IAM) é um serviço da AWS que ajuda a controlar quem está autenticado (assinado) e autorizado (tem permissões) para usar os recursos da AWS.

Aqui estão os principais pontos sobre o IAM:



1 - **Controle Granular de Acesso a AWS:** Com o IAM, você pode criar usuários, grupos, papéis e políticas de permissão para controlar o acesso aos serviços e recursos da AWS de uma maneira granular. Por exemplo, você pode permitir que um usuário tenha acesso somente leitura ao Amazon S3 e acesso total ao EC2.

2 - **Compartilhamento Seguro de Acesso:** O IAM permite compartilhar o acesso à sua conta AWS de maneira segura. Em vez de compartilhar suas credenciais de root, você pode criar vários usuários IAM, cada um com suas próprias credenciais e permissões.

3 - **Identidade Federada:** Com o IAM, você também pode permitir usuários que já tenham senhas em outros lugares, como na sua rede corporativa ou em um provedor de identidade baseado em SAML, a obter acesso temporário à sua conta AWS.

4 - **Compatível com Multi-Fator Authentication (MFA):** O IAM é compatível com a autenticação de vários fatores para fornecer uma camada adicional de proteção de segurança ao gerenciar o acesso aos serviços e recursos da AWS.

5 - **Integrado com AWS Services:** O IAM está integrado com todos os serviços da AWS, o que significa que você pode definir permissões para qualquer serviço que desejar.

6 - **Auditoria com AWS CloudTrail:** Com o AWS CloudTrail, você pode registrar todas as ações de usuários e APIs IAM para fins de auditoria.

7 - **Gratuito:** O IAM é um recurso gratuito da AWS; você só paga pelos outros recursos da AWS que seus usuários acessam.

Em suma, o AWS IAM é um serviço de segurança crítico que ajuda a proteger o acesso aos recursos da AWS, permitindo que você controle quem pode fazer o quê em sua conta AWS.


## Resumo MFA

A Autenticação Multifator (MFA) é um método de controle de acesso que exige que um usuário verifique sua identidade usando duas ou mais evidências (fatores) antes que o acesso seja concedido. Estes fatores podem ser algo que o usuário sabe (como uma senha), algo que o usuário tem (como um telefone celular ou um token de hardware) e algo que o usuário é (como uma impressão digital ou reconhecimento facial).

Aqui estão alguns pontos-chave sobre MFA:



1 - **Segurança Aprimorada:** O principal benefício da MFA é que ela aumenta significativamente a segurança, tornando muito mais difícil para os invasores ganharem acesso não autorizado a um sistema. Mesmo que um fator de autenticação seja comprometido (por exemplo, se uma senha for roubada), os outros fatores ainda protegem o sistema.

2 - **Diversos Métodos de Autenticação:** A MFA pode usar uma variedade de métodos de autenticação, como códigos de verificação por SMS, aplicativos de autenticação, tokens de hardware, impressões digitais, reconhecimento facial e muito mais.

3 - **Compatibilidade:** A MFA é compatível com muitos sistemas e serviços, incluindo a maioria das plataformas de nuvem (como AWS, Google Cloud e Azure), serviços de email, redes sociais, plataformas de pagamento online, entre outros.

4 - **AWS MFA:** A AWS suporta MFA e recomenda que os usuários a utilizem para proteger suas contas. Com a MFA ativada, quando um usuário se conecta à AWS, ele é solicitado a inserir seu nome de usuário e senha (primeiro fator) e um código de autenticação de um dispositivo MFA (segundo fator).

Resumindo, a Autenticação Multifator é uma medida de segurança essencial que protege os sistemas de acesso não autorizado, exigindo que os usuários verifiquem sua identidade com vários fatores de autenticação.

## Resumo Organizações

O AWS Organizations é um serviço da AWS que permite a você centralizar e gerenciar de forma unificada várias contas AWS. Com o AWS Organizations, você pode criar uma organização para administrar suas contas da AWS a partir de um único local.

Aqui estão algumas características principais do AWS Organizations:



1 - **Gerenciamento Centralizado de Contas:** O AWS Organizations permite agrupar e gerenciar todas as suas contas AWS de um único local centralizado. Isso facilita o gerenciamento de contas e recursos em uma organização.

2 - **Controle de Acesso Hierárquico:** Com o AWS Organizations, você pode criar uma estrutura hierárquica de Unidades Organizacionais (OUs) para agrupar suas contas. Isso ajuda a organizar suas contas em uma estrutura que melhor se alinhe com o uso dos recursos em sua organização.

3 - **Políticas de Controle de Serviço:** O AWS Organizations oferece políticas de controle de serviço (SCPs) que permitem que você controle as permissões para as contas em sua organização. Isso permite que você aplique regras de acesso uniformes em todas as suas contas.

4 - **Consolidação de Cobrança:** O AWS Organizations também oferece a capacidade de consolidar sua cobrança em todas as suas contas AWS, o que pode simplificar a gestão de custos e permitir um melhor rastreamento e controle dos gastos da AWS.

5 - **Automação:** Com o AWS Organizations, você pode automatizar a criação e o gerenciamento de contas por meio de APIs e integrações com outras ferramentas da AWS, como o AWS CloudFormation.

Em suma, o AWS Organizations é uma ferramenta poderosa para empresas e equipes que gerenciam várias contas da AWS, permitindo o gerenciamento centralizado de contas, a aplicação de políticas em todas as contas, a consolidação de cobranças e a automação de tarefas de gerenciamento de contas.

## 📚 Recomendações para a Prova CLF-C02

- Entenda a diferença entre **IAM** e **IAM Identity Center**.
- Saiba o papel das **roles**, **grupos**, e **políticas**.
- Saiba que **IAM é global**, **AWS Organizations** é multi-conta.
- Conheça o conceito de **SCPs** e **OU**.
- Lembre-se da importância de **MFA**.

---

📘 **Referências oficiais:**  
- [Documentação IAM AWS](https://docs.aws.amazon.com/iam/latest/UserGuide/introduction.html)  
- [IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html)  
- [AWS Organizations](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html)

---
