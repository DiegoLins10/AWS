# 📘 API Gateway – Complete Guide (DVA-C02)

---

# 1️⃣ Overview

👉 **Amazon API Gateway** = serviço para criar, publicar, monitorar e proteger APIs

### Tipos de API:

* **REST API** → mais features (cai mais na prova)
* **HTTP API** → mais barato e simples
* **WebSocket API** → comunicação em tempo real

---

# 2️⃣ Stages & Deployment

## 📦 Deploy

* Cada mudança precisa de **deploy**
* Deploy cria uma versão da API

## 🌍 Stages

* Ex: `dev`, `test`, `prod`
* Cada stage aponta para um deployment

## ⚙️ Stage Config:

* Throttling
* Logging
* Cache
* Variables (tipo env vars)

---

# 3️⃣ Stage Variables (🔥 cai na prova)

👉 Permite mudar comportamento sem redeploy

Ex:

```
${stageVariables.lambdaAlias}
```

✅ Usos:

* Trocar Lambda (dev/prod)
* Configurar endpoints

---

# 4️⃣ Canary Deployment

👉 Deploy gradual

* Ex: 10% → nova versão
* 90% → versão antiga

✅ Usado para:

* Testar em produção
* Reduzir risco

⚠️ Cai na prova:

* Configurado **por stage**
* Pode promover depois

---

# 5️⃣ Integration Types

## 🔗 Tipos:

### 1. Lambda Proxy (🔥 MAIS IMPORTANTE)

* Passa request inteira para Lambda
* Simples e usado na prática

### 2. Lambda Non-Proxy

* Precisa mapping template

### 3. HTTP Integration

* Integra com backend HTTP

### 4. Mock Integration

* Retorna resposta fake

---

# 6️⃣ Mapping Templates (🔥 difícil mas cai)

👉 Usado em **Non-Proxy**

* Baseado em **VTL (Velocity Template Language)**

Ex:

```
$input.json('$.name')
```

✅ Usos:

* Transformar request/response
* Filtrar dados

---

# 7️⃣ OpenAPI (Swagger)

👉 Definir API via arquivo

* Importar/exportar API
* Infra as Code

⚠️ Cai na prova:

* Pode versionar API
* Facilita automação

---

# 8️⃣ Caching

👉 Cache no API Gateway

* Reduz chamadas ao backend
* TTL configurável

⚠️ Cai:

* Configurado por **stage**
* Pode invalidar cache

---

# 9️⃣ Usage Plans & API Keys

## 🔑 API Key

* Identifica cliente

## 📊 Usage Plan

* Throttle (rate limit)
* Quota (limite mensal)

⚠️ IMPORTANTE:

* ❌ NÃO é segurança
* Apenas controle de uso

---

# 🔟 Monitoring, Logging & Tracing

## 📊 CloudWatch

* Logs
* Metrics

## 🔍 X-Ray

* Tracing distribuído

⚠️ Cai:

* Debug de latência
* Identificar bottlenecks

---

# 1️⃣1️⃣ CORS

👉 Necessário para browser

Headers:

* `Access-Control-Allow-Origin`
* `Methods`
* `Headers`

⚠️ Cai:

* Precisa configurar OPTIONS

---

# 1️⃣2️⃣ Authentication & Authorization (🔥 MUITO COBRADO)

## 🔐 IAM

* Usuários/roles AWS
* Usa **SigV4**
* Sem JWT

---

## 🧩 Lambda Authorizer

* Valida token custom
* Retorna IAM Policy
* Pode cachear

---

## 👤 Cognito

* User pool
* JWT token
* Login social

---

# 🔥 COMPARAÇÃO (DECORAR)

| Feature      | IAM         | Lambda Authorizer | Cognito  |
| ------------ | ----------- | ----------------- | -------- |
| Uso          | Interno AWS | Custom auth       | Usuários |
| Token        | ❌           | ✅                 | ✅        |
| Complexidade | Baixa       | Alta              | Média    |
| Custo        | Baixo       | 💰                | Baixo    |

---

# 🧠 Dicas de Prova (OURO)

* 🔥 **Lambda Proxy = padrão real**
* 🔥 **API Key ≠ segurança**
* 🔥 **Cognito = JWT pronto**
* 🔥 **IAM = SigV4**
* 🔥 **Stage Variables evitam redeploy**
* 🔥 **Canary = rollout gradual**
* 🔥 **Caching = melhora performance**

---

# ⚠️ Pegadinhas clássicas

* ❌ API Gateway **não guarda estado**
* ❌ API Key não autentica usuário
* ❌ Lambda Authorizer pode aumentar latência
* ❌ Mapping template só no NON-proxy

---

# 🚀 Resumo final (pra decorar rápido)

👉 API Gateway = **porta de entrada + controle + segurança**

* Deploy → Stage
* Stage → Config + Cache + Canary
* Auth → IAM | Cognito | Lambda
* Performance → Cache + Throttle

---

Se quiser, posso te mandar agora:
✅ 10 questões nível prova DVA só de API Gateway
✅ ou um **simulado completo misturando tudo que você já estudou**

Esse tema aqui sozinho cai fácil **3–5 questões na prova** 🔥
