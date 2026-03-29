# 🧠📘 README — Step Functions & AppSync (DVA-C02)

---

# 🚀 1. AWS Step Functions Overview

## 🔹 O que é

* Serviço de **orquestração serverless**
* Cria **workflows (state machines)**

## 🔹 Usos

* Microservices orchestration
* ETL workflows
* Processamento assíncrono

---

# 🧱 2. Conceitos principais

## 🔹 State Machine

* Definida em **JSON (Amazon States Language)**

## 🔹 States tipos principais

| Tipo         | Função                          |
| ------------ | ------------------------------- |
| Task         | Executa ação (Lambda, API, etc) |
| Choice       | If/Else                         |
| Wait         | Delay                           |
| Parallel     | Execução paralela               |
| Map          | Loop / lista                    |
| Pass         | Debug / transformação           |
| Fail/Succeed | Finalização                     |

---

# ⚡ 3. Invoke Lambda

Integração direta com:

* AWS Lambda

👉 Pode:

* passar input/output JSON
* manipular dados entre estados

---

# ❌ 4. Error Handling (CAI MUITO)

## 🔹 Retry

```json
{
  "Retry": [{
    "ErrorEquals": ["States.ALL"],
    "IntervalSeconds": 2,
    "MaxAttempts": 3
  }]
}
```

## 🔹 Catch

```json
{
  "Catch": [{
    "ErrorEquals": ["States.ALL"],
    "Next": "FallbackState"
  }]
}
```

---

## 🧠 Regra de prova

👉 Retry = tenta de novo
👉 Catch = trata erro (fallback)

---

# ⏳ 5. Wait for Task Token

## 🔹 O que é

* Step Functions **pausa execução**
* Espera resposta externa

## 🔹 Usos

* Aprovação manual
* Processos humanos
* Integrações externas

---

# 🧩 6. Activity Tasks

## 🔹 O que é

* Worker externo faz polling

👉 usado quando:

* não dá pra usar Lambda
* precisa de processamento externo

---

# ⚖️ 7. Standard vs Express (CAI MUITO)

| Feature  | Standard           | Express          |
| -------- | ------------------ | ---------------- |
| Duração  | Longa              | Curta            |
| Execução | Exatamente uma vez | Alta escala      |
| Use case | Workflow crítico   | Eventos massivos |
| Custo    | Por transição      | Por execução     |

---

## 🧠 Regra de prova

* 💼 Processo crítico → **Standard**
* ⚡ Alta escala → **Express**

---

# 🔗 8. AWS AppSync Overview

## 🔹 O que é

* Serviço **GraphQL gerenciado**

## 🔹 Permite:

* Query
* Mutation
* Subscription (real-time)

---

## 🔹 Integrações

* Amazon DynamoDB
* AWS Lambda
* Amazon RDS

---

# ⚡ 9. AppSync Hands On (ponto de prova)

## 🔹 Resolver

* Define como buscar dados

## 🔹 VTL (Velocity Template Language)

* Mapeia request → backend

---

# 🔐 10. Segurança AppSync

* IAM
* Cognito
* API Key

---

# 📱 11. AWS Amplify

## 🔹 O que é

* Plataforma para:

  * Frontend
  * Mobile
  * Fullstack apps

---

## 🔹 Integra com:

* AppSync
* Cognito
* S3
* Lambda

---

## 🔹 Features

* Hosting
* CI/CD
* Auth fácil
* APIs prontas

---

# 🧠 12. Quando usar cada um (PROVA)

| Cenário              | Serviço        |
| -------------------- | -------------- |
| Orquestrar workflow  | Step Functions |
| API GraphQL          | AppSync        |
| App fullstack rápido | Amplify        |

---

# 🔥 TL;DR FINAL

* Step Functions → **orquestra fluxo**
* AppSync → **GraphQL API**
* Amplify → **frontend + integração rápida**

---


