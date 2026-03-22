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

# ⚡ Continuação — AWS Lambda (Eventos, Async, ALB, Streams)

---

# 9️⃣ Lambda Asynchronous Invocations & DLQ ⚡

## 📌 Conceito

➡️ Execução em background (**não espera resposta**)

---

## 🔹 Características

* InvocationType = `Event`
* Retry automático (**até 2 vezes**)
* Pode configurar destino de falha

---

## ☠️ DLQ (Dead Letter Queue)

➡️ Para eventos que falharam

### 🔹 Suporta:

* SQS
* SNS

---

## 🎯 Destinations (mais moderno)

| Tipo       | Uso          |
| ---------- | ------------ |
| On Success | Após sucesso |
| On Failure | Após falha   |

---

## 🚨 Pegadinha

👉 Async tem retry automático
👉 Sync NÃO tem

---

# 🔟 Lambda + EventBridge ⚡

## 📌 O que é

➡️ EventBridge = **event bus (event-driven)**

---

## 🔹 Fluxo

```id="0x6m7o"
Evento → Rule → Lambda
```

---

## 🔹 Exemplos

* EC2 mudou estado
* CloudTrail detectou ação
* Scheduler (cron)

---

## 🧠 Características

* Invocação **assíncrona**
* Desacoplado
* Filtragem por regra

---

## 🚨 Pegadinha

👉 EventBridge = async SEMPRE

---

# 1️⃣1️⃣ Lambda + S3 Event Notifications 📦

## 📌 O que é

➡️ S3 dispara Lambda automaticamente

---

## 🔹 Eventos comuns

* ObjectCreated
* ObjectRemoved

---

## 🔹 Fluxo

```id="z6x4g7"
Upload no S3 → Evento → Lambda
```

---

## 🧠 Características

* Invocação **assíncrona**
* Muito usado pra:

  * Processar arquivos
  * Imagens
  * ETL

---

## 🚨 Pegadinha

👉 S3 → Lambda = async

---

# 1️⃣2️⃣ Lambda + ALB ⚖️

## 📌 O que é

➡️ ALB pode chamar Lambda como target

---

## 🔹 Características

* Invocação **síncrona**
* HTTP request/response
* Similar ao API Gateway

---

## 🧠 Quando usar

* Web apps simples
* Microservices HTTP

---

## 🚨 Pegadinha

👉 ALB = síncrono
👉 API Gateway = síncrono

---

# 1️⃣3️⃣ Shards, Batching & Lambda (🔥 MUITO IMPORTANTE)

## 📌 Onde aparece

* Kinesis Data Streams
* DynamoDB Streams

---

## 🧩 Shard (fragmento)

➡️ Partição de dados do stream

```id="z6bptu"
Stream
 ├── Shard 1
 ├── Shard 2
 └── Shard 3
```

---

## ⚡ Regra principal

👉 **1 shard → 1 execução concorrente de Lambda (default)**

---

## 📦 Batching (o que o diagrama mostrou)

➡️ Eventos são agrupados em **batches**

```id="kk1r1b"
Eventos → Batch → Lambda execução
```

---

## 🔹 Importante

👉 1 batch = 1 execução de Lambda

👉 Um shard pode gerar **vários batches**

---

## 🔍 Fluxo real

```id="7o7hl2"
Shard → Records → Batches → Lambda execuções
```

---

## ⚠️ Ordem dos dados

| Escopo          | Ordem       |
| --------------- | ----------- |
| Dentro do shard | ✅ Garantida |
| Entre shards    | ❌ Não       |

---

## 🚀 Paralelismo

### 🔹 Default

* 1 shard → 1 execução

### 🔹 Com Parallelization Factor

* Até **10 execuções por shard**

---

## 🚨 Pegadinhas

❗ Shard ≠ Lambda
❗ Lambda NÃO cria shard
❗ Mais shards = mais paralelismo

---

# 🧠 Resumo mental (DECORA)

👉 Shard = divide dados
👉 Batch = agrupa eventos
👉 Lambda = processa batch

---

# 🎯 Cenários de prova

## 📌 Stream de dados em tempo real

👉 Kinesis + Lambda

---

## 📌 Processar uploads

👉 S3 + Lambda

---

## 📌 Arquitetura event-driven

👉 EventBridge + Lambda

---

## 📌 API HTTP

👉 API Gateway / ALB + Lambda

---

# 🔥 Resumo final geral

👉 Sync → RequestResponse (API, ALB)
👉 Async → Event (S3, EventBridge, SNS)

👉 Shard controla paralelismo
👉 Batch controla execução

---


