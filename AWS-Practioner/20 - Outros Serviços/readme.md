# 📘 README – Seção 23: Outros Serviços (AWS Cloud Practitioner)

---

## 1️⃣ Amazon Cognito

Serviço de autenticação e gerenciamento de usuários.

Permite:

* Login de usuários
* Autenticação com redes sociais (Google, Facebook, etc.)
* Controle de acesso para aplicações

Uso comum:

* Aplicações web e mobile

📌 Na prova:
Cognito = autenticação e gerenciamento de identidade para apps.

---

## 2️⃣ Amazon Security Token Service (STS)

Permite criar credenciais temporárias.

Usado para:

* Acesso temporário a recursos
* Assumir roles
* Delegação segura de permissões

📌 STS = credenciais temporárias seguras.

---

## 3️⃣ AWS Device Farm

Permite testar aplicações mobile em dispositivos reais.

Benefícios:

* Teste automatizado
* Vários modelos de dispositivos
* Ambiente real

📌 Device Farm = testar app mobile na nuvem.

---

## 4️⃣ AWS AppSync

Serviço para criar APIs GraphQL totalmente gerenciadas.

Permite:

* Sincronização de dados em tempo real
* Integração com DynamoDB, Lambda, etc.

📌 AppSync = API GraphQL gerenciada.

---

## 5️⃣ AWS Amplify

Plataforma para desenvolvimento de aplicações web e mobile.

Inclui:

* Backend serverless
* Autenticação
* Hospedagem
* Integração com serviços AWS

📌 Amplify = framework para criar apps full-stack na AWS.

---

## 6️⃣ AWS IoT Core

Permite conectar dispositivos IoT à AWS.

Funções:

* Comunicação segura
* Coleta de dados
* Processamento em tempo real

Uso comum:

* Sensores
* Dispositivos inteligentes
* Monitoramento industrial

📌 IoT Core = conectar dispositivos físicos à nuvem.

---

## 7️⃣ AWS Step Functions

Permite orquestrar fluxos de trabalho.

Coordena:

* Lambda
* ECS
* Outros serviços

Usado para:

* Automatizar processos
* Criar workflows

📌 Step Functions = orquestração de processos.

---

## 8️⃣ Amazon AppFlow

Automatiza integração de dados entre:

* Aplicações SaaS (ex: Salesforce)
* Serviços AWS (ex: S3)

Uso:

* Transferência automática de dados
* Integração empresarial

📌 AppFlow = integração de dados entre SaaS e AWS.

---

## 9️⃣ AWS Backup

Serviço centralizado de backup.

Permite:

* Backup automático
* Políticas centralizadas
* Gerenciar múltiplos serviços

Suporta:

* EBS
* RDS
* DynamoDB
* EFS

📌 Backup centralizado e automatizado.

---

## 🔟 AWS Disaster Recovery Strategy

Estratégias para recuperação em caso de falha.

Principais modelos:

* Backup and Restore
* Pilot Light
* Warm Standby
* Multi-Site (Active/Active)

Quanto maior disponibilidade → maior custo.

📌 Muito comum na prova: relação custo x recuperação.

---

## 1️⃣1️⃣ AWS WorkSpaces

Serviço de desktop virtual (DaaS – Desktop as a Service).

Permite:

* Usuários acessarem desktop remoto
* Ambiente corporativo seguro

📌 WorkSpaces = desktop virtual na nuvem.

---

## 1️⃣2️⃣ AWS AppStream 2.0

Streaming de aplicações.

Diferença:

* WorkSpaces → desktop completo
* AppStream → apenas aplicação via streaming

Uso:

* Softwares pesados
* Aplicações específicas

---

# 🎯 Comparação Rápida

| Serviço        | Função                     |
| -------------- | -------------------------- |
| Cognito        | Autenticação de usuários   |
| STS            | Credenciais temporárias    |
| Device Farm    | Teste de apps mobile       |
| AppSync        | API GraphQL                |
| Amplify        | Desenvolvimento full-stack |
| IoT Core       | Conectar dispositivos IoT  |
| Step Functions | Orquestrar workflows       |
| AppFlow        | Integração SaaS            |
| Backup         | Backup centralizado        |
| WorkSpaces     | Desktop virtual            |
| AppStream      | Streaming de aplicações    |

---

# 🧠 O que mais pode cair na prova

* Diferença WorkSpaces vs AppStream
* Estratégias de Disaster Recovery
* Cognito para login
* STS para credenciais temporárias
* Step Functions para orquestração
* IoT Core para dispositivos físicos

---

# 📌 Resumo Final

Essa seção reúne serviços complementares que resolvem problemas específicos:

* Autenticação → Cognito
* Integração → AppFlow
* IoT → IoT Core
* Orquestração → Step Functions
* Backup → AWS Backup
* DR → Estratégias de recuperação
* Desktop/Apps remotas → WorkSpaces e AppStream

Saber identificar **qual serviço resolve qual problema** é o principal para a Cloud Practitioner.

---

