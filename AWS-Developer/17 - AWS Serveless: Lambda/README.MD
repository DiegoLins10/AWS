# ⚡ AWS Lambda — Invocations & Integration (DVA-C02)

---

## 1️⃣ Visão Geral 🧠

➡️ AWS Lambda = **compute serverless**

* Executa código sem gerenciar servidor
* Escala automaticamente
* Paga por execução

---

## 2️⃣ Serverless Basics ☁️

➡️ Você NÃO gerencia:

* Servidores
* Scaling
* Infraestrutura

👉 Só envia código

💡 Exemplos serverless:

* Lambda
* DynamoDB
* S3
* Fargate

---

## 3️⃣ Lambda Invocation Types ⚡

## 🔹 Tipos

| Tipo       | Nome            | Comportamento   |
| ---------- | --------------- | --------------- |
| Síncrono   | RequestResponse | Espera resposta |
| Assíncrono | Event           | Fire-and-forget |

---

# 4️⃣ Synchronous Invocation (MUITO COBRADO)

## 📌 Como funciona

➡️ Cliente espera resposta da Lambda

---

## 🔹 Exemplos

* API Gateway
* Application Load Balancer (ALB)

---

## 🔹 Código / CLI

```bash
aws lambda invoke \
  --function-name minha-funcao \
  --invocation-type RequestResponse \
  response.json
```

---

## 🔹 IMPORTANTE (sua dúvida)

👉 Se NÃO definir `InvocationType`:

✅ **Default = RequestResponse (SÍNCRONO)**

---

## 🔹 Características

* Retorna resultado imediatamente
* Sem retry automático
* Cliente lida com erro

---

# 5️⃣ Lambda + Application Load Balancer ⚖️

➡️ ALB pode invocar Lambda

### 🔹 Características

* Sempre **síncrono**
* Suporta HTTP (como API Gateway)
* Pode retornar HTML/JSON

💡 Uso:

* Web apps simples
* Microservices

---

# 6️⃣ Asynchronous Invocation ⚡

## 📌 Como funciona

➡️ Lambda recebe evento e processa em background

👉 Cliente NÃO espera resposta

---

## 🔹 Como invocar

```bash
aws lambda invoke \
  --function-name minha-funcao \
  --invocation-type Event \
  response.json
```

---

## 🔹 SDK

```javascript
InvocationType: "Event"
```

---

## 🔹 Serviços que usam async

* S3
* SNS
* EventBridge
* CloudWatch Events

---

# 7️⃣ Async Behavior (CAI NA PROVA)

## 🔁 Retry automático

* Até **2 tentativas**

---

## ☠️ DLQ (Dead Letter Queue)

➡️ Se falhar:

Pode enviar para:

* SQS
* SNS

---

## 🎯 Destinations (mais moderno)

➡️ Define:

* On Success
* On Failure

---

# 8️⃣ Synchronous vs Asynchronous ⚔️

| Feature          | Síncrono | Assíncrono |
| ---------------- | -------- | ---------- |
| Espera resposta  | ✅        | ❌          |
| Retry automático | ❌        | ✅          |
| DLQ              | ❌        | ✅          |
| Uso comum        | API      | Eventos    |

---

# 🚨 Pegadinhas de prova

## ❗ Default Invocation

👉 Não definiu → **SÍNCRONO**

---

## ❗ API Gateway

👉 Sempre **síncrono**

---

## ❗ S3 / SNS / EventBridge

👉 Sempre **assíncrono**

---

## ❗ “Processamento em background”

👉 Assíncrono

---

## ❗ “Resposta imediata ao usuário”

👉 Síncrono

---

# 🧠 Regra de ouro

👉 RequestResponse → síncrono
👉 Event → assíncrono

---

# 🔥 Cenários clássicos (DVA)

## 📌 Upload de arquivo no S3

👉 S3 → Lambda → async

---

## 📌 API REST

👉 API Gateway → Lambda → sync

---

## 📌 Processamento pesado

👉 EventBridge/SQS → Lambda → async

---

# 🎯 Resumo final

👉 Default = síncrono
👉 Async precisa explícito (`Event`)
👉 Async = retry + DLQ
👉 Sync = resposta imediata

---

