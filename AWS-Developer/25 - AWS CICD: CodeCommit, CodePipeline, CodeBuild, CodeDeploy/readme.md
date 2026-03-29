Aqui vai um **README estilo prova DVA-C02 (AWS Developer Associate)** focado em **CI/CD na AWS**, bem direto, estruturado e com pegadinhas de prova 👇

---

# 🚀 AWS CI/CD - README (DVA-C02)

## 1. 🧠 Conceito de CI/CD

* **CI (Continuous Integration)** → integrar código frequentemente + testes automáticos
* **CD (Continuous Delivery/Deployment)** → entrega automatizada até produção

💡 Objetivo:

* Deploy rápido
* Menos erro humano
* Pipeline automatizado

---

## 2. 🏗️ Visão Geral dos Serviços

| Serviço      | Função                        |
| ------------ | ----------------------------- |
| CodeCommit   | Repositório Git (privado)     |
| CodeBuild    | Build + testes                |
| CodeDeploy   | Deploy automático             |
| CodePipeline | Orquestra tudo                |
| CodeArtifact | Gerenciamento de dependências |
| CodeGuru     | Análise de código (ML)        |

---

## 3. 📦 AWS CodeCommit

### 🔹 O que é

* Repositório Git gerenciado pela AWS

### 🔹 Features importantes

* Privado por padrão
* Integrado com IAM
* Criptografia automática (KMS)

### 🔹 Autenticação

* HTTPS (Git credentials IAM)
* SSH

### ⚠️ Pegadinhas de prova

* ❌ Não é GitHub → é AWS nativo
* ❌ Não faz CI/CD sozinho
* ✅ Pode triggerar CodePipeline

---

## 4. 🔨 AWS CodeBuild

### 🔹 O que faz

* Compila código
* Executa testes
* Gera artefatos

### 🔹 Arquivo importante

* `buildspec.yml`

```yaml
version: 0.2
phases:
  install:
    commands: npm install
  build:
    commands: npm run build
```

### 🔹 Características

* Serverless (sem gerenciar infra)
* Escala automaticamente
* Suporta Docker

### ⚠️ Pegadinhas

* ✅ Cobrado por tempo de build
* ❌ Não faz deploy

---

## 5. 🚀 AWS CodeDeploy

### 🔹 O que faz

* Automatiza deploy em:

  * EC2
  * Lambda
  * On-premises

### 🔹 Estratégias de deploy

* In-place
* Blue/Green

### 🔹 Arquivo importante

* `appspec.yml`

### 🔹 Integrações

* Auto Scaling Group (ASG)
* Load Balancer

### ⚠️ Pegadinhas

* ✅ Pode fazer rollback automático
* ✅ Usa lifecycle hooks
* ❌ Não builda código

---

## 6. 🔄 AWS CodePipeline

### 🔹 O cérebro do CI/CD

### 🔹 Fluxo

1. Source (CodeCommit/GitHub/S3)
2. Build (CodeBuild)
3. Deploy (CodeDeploy)

### 🔹 Características

* Orquestra pipeline
* Visual (stages)
* Pode ter aprovação manual

### ⚠️ Pegadinhas

* ✅ Pode integrar serviços externos
* ✅ Dispara automaticamente (commit)
* ❌ Não executa build diretamente

---

## 7. 📚 AWS CodeArtifact

### 🔹 O que é

* Repositório de dependências (packages)

### 🔹 Suporte

* npm
* Maven
* pip
* NuGet

### 🔹 Benefícios

* Cache de dependências externas
* Segurança (controle de acesso IAM)

### ⚠️ Pegadinhas

* ❌ Não é S3
* ❌ Não armazena código fonte
* ✅ Usado no build (CodeBuild)

---

## 8. 🧠 AWS CodeGuru

### 🔹 Tipos

* Reviewer → análise de código
* Profiler → performance em runtime

### 🔹 Base

* Machine Learning

### ⚠️ Pegadinhas

* ❌ Não substitui testes
* ✅ Sugere melhorias e otimizações

---

## 9. 🔗 Pipeline Completo (Resumo)

```text
Dev → CodeCommit → CodePipeline → CodeBuild → CodeDeploy → Produção
```

---

## 10. 🧩 Integrações Importantes (PROVA)

| Cenário                 | Serviço      |
| ----------------------- | ------------ |
| Deploy EC2              | CodeDeploy   |
| Build Docker            | CodeBuild    |
| Orquestrar pipeline     | CodePipeline |
| Guardar libs            | CodeArtifact |
| Code review inteligente | CodeGuru     |

---

## 11. ⚠️ Pegadinhas Clássicas da Prova

### 🔸 1. “Quem faz o quê?”

* Build → CodeBuild
* Deploy → CodeDeploy
* Orquestra → CodePipeline

---

### 🔸 2. Arquivos importantes

* buildspec.yml → CodeBuild
* appspec.yml → CodeDeploy

---

### 🔸 3. Blue/Green

* Zero downtime
* Suportado no CodeDeploy

---

### 🔸 4. Trigger automático

* Commit no CodeCommit → dispara pipeline

---

### 🔸 5. Serverless

* CodeBuild é serverless
* CodePipeline também

---

## 12. 🧠 Dicas de Prova (nível hard)

* Se falar em **pipeline completo → CodePipeline**
* Se falar em **compilar/testar → CodeBuild**
* Se falar em **deploy EC2/Lambda → CodeDeploy**
* Se falar em **repositório privado AWS → CodeCommit**
* Se falar em **dependências → CodeArtifact**

---

## 13. 🧪 Exemplo de Cenário (cara de prova)

👉 “Aplicação precisa:

* Build automático
* Testes
* Deploy em EC2 com rollback”

✅ Resposta:

* CodePipeline + CodeBuild + CodeDeploy

---


# 🚀 AWS CI/CD - README (DVA-C02)

## 14. ⚡ Triggers (Disparos do Pipeline)

### 🔹 Formas de disparar o CodePipeline

| Trigger     | Como funciona             |
| ----------- | ------------------------- |
| Commit      | Push no CodeCommit/GitHub |
| EventBridge | Eventos AWS               |
| Manual      | Start pipeline            |
| Schedule    | Agendamento               |

---

### 🔹 Trigger via Commit (mais comum na prova)

* Commit no CodeCommit → dispara pipeline automaticamente

💡 Também funciona com:

* GitHub (webhook)
* S3 (upload de arquivo)

---

### 🔹 EventBridge (EX CloudWatch Events)

* Permite automação baseada em eventos

Exemplo:

* Novo commit → dispara pipeline
* Mudança em recurso AWS → trigger ação

---

## 15. 📩 Notificações (Email / Alertas)

### 🔹 Serviço principal: SNS (Simple Notification Service)

### 🔹 Fluxo clássico:

```text
Pipeline/Evento → SNS → Email
```

---

### 🔹 Como funciona

1. Evento ocorre (ex: build falhou)
2. SNS é acionado
3. SNS envia:

   * Email
   * SMS
   * HTTP endpoint

---

### 🔹 Integração com CI/CD

| Serviço      | Evento        |
| ------------ | ------------- |
| CodePipeline | Falha/sucesso |
| CodeBuild    | Build failed  |
| CodeDeploy   | Deploy status |

---

## 16. 🔔 CodeStar Notifications (IMPORTANTE PRA PROVA)

### 🔹 O que é

* Serviço para notificações de CI/CD

### 🔹 Integra com:

* CodePipeline
* CodeBuild
* CodeCommit
* CodeDeploy

---

### 🔹 Destinos

* SNS (email)
* Chat (Slack via AWS Chatbot)

---

### 🔹 Exemplo

* Pipeline falhou → envia email automaticamente

---

### ⚠️ Pegadinhas

* ❌ SNS não "escuta" sozinho → precisa de trigger
* ✅ CodeStar Notifications simplifica tudo
* ✅ Pode filtrar eventos (ex: só falha)

---

## 17. 💬 AWS Chatbot (extra prova)

### 🔹 Integração

* SNS → Chatbot → Slack / Chime

💡 Usado para alertas em tempo real no time

---

## 18. 🔄 Exemplo Completo (com notificação)

```text
Dev commit → CodeCommit
        ↓
CodePipeline inicia
        ↓
CodeBuild (build/test)
        ↓
CodeDeploy (deploy)
        ↓
Falhou?
   ↓
CodeStar Notification → SNS → Email/Slack
```

---

## 19. 🧠 Cenários de Prova (MUITO COBRADOS)

### 🔸 Cenário 1

👉 “Notificar time quando build falhar”

✅ SNS + CodeBuild
ou
✅ CodeStar Notifications

---

### 🔸 Cenário 2

👉 “Disparar pipeline ao subir arquivo no S3”

✅ S3 + EventBridge → CodePipeline

---

### 🔸 Cenário 3

👉 “Enviar alerta para Slack”

✅ SNS + AWS Chatbot

---

### 🔸 Cenário 4

👉 “Filtrar apenas falhas”

✅ CodeStar Notifications (event filtering)

---

## 20. ⚠️ Pegadinhas Clássicas (Triggers & Alerts)

* Commit → trigger automático (não precisa Lambda)
* SNS precisa de publisher (não age sozinho)
* EventBridge = engine de eventos
* CodeStar = mais simples que configurar SNS manualmente

---

## 21. 🧠 Dica de Ouro (PROVA)

Se a questão falar:

| Situação                    | Resposta               |
| --------------------------- | ---------------------- |
| “Notificar por email”       | SNS                    |
| “Automação por evento”      | EventBridge            |
| “CI/CD notifications fácil” | CodeStar Notifications |
| “Chat (Slack)”              | AWS Chatbot            |

---

