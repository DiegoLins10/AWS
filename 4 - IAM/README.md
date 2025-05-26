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
