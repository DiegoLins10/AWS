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

Aqui vai um **README estilo prova DVA-C02** focado nessa arquitetura 👇

---

# 📘 API Gateway – Architecture (DVA-C02)

---

# 1️⃣ Conceito Principal

👉 **API Gateway = Single Entry Point (porta única)** para todos os seus serviços

📌 Ele atua como:

* 🔀 **Router** (direciona requisições)
* 🔐 **Security layer**
* ⚙️ **Transformador de requests/responses**

---

# 2️⃣ Arquitetura Geral

👉 Fluxo típico:

```
Client → API Gateway → Backend Services
```

Backends podem ser:

* Lambda
* EC2
* ECS
* S3
* ELB

---

# 3️⃣ Microservices Pattern (🔥 MUITO COBRADO)

👉 API Gateway expõe **uma única API**
👉 Internamente chama vários serviços

Exemplo:

```
/service1 → ECS (via ELB)
/service2 → EC2 (Auto Scaling)
/docs → S3
```

✅ Benefícios:

* Abstrai complexidade
* Centraliza acesso
* Facilita versionamento

---

# 4️⃣ Integrações possíveis

## 🔗 Com Load Balancer (ELB)

* Usado com:

  * EC2
  * ECS

👉 API Gateway → ELB → serviços

---

## 🐳 ECS (Containers)

* Microservices em containers
* Escala automaticamente

---

## 💻 EC2 + Auto Scaling

* Apps tradicionais
* Escala com demanda

---

## 🪣 S3

* Conteúdo estático
* Ex: `/docs`

---

# 5️⃣ Custom Domain + Route 53

👉 Você pode usar domínio customizado:

Ex:

```
api.meusite.com
```

Usando:

* **Route 53** (DNS)
* Certificado SSL (HTTPS)

---

# 6️⃣ Transformações no API Gateway (🔥 cai)

👉 Pode modificar:

### Request

* Headers
* Body
* Query params

### Response

* Status codes
* Payload

📌 Usando:

* Mapping Templates
* Integration Response

---

# 7️⃣ Vantagens (IMPORTANTE PRA PROVA)

✅ Centralização
✅ Segurança unificada
✅ Controle de tráfego
✅ Observabilidade
✅ Desacoplamento

---

# 8️⃣ Comparação mental (DECORAR)

| Sem API Gateway               | Com API Gateway          |
| ----------------------------- | ------------------------ |
| Cliente chama vários serviços | Cliente chama 1 endpoint |
| Complexidade alta             | Simples                  |
| Segurança distribuída         | Centralizada             |

---

# 9️⃣ Pegadinhas de prova

* 🔥 API Gateway **não executa lógica pesada**
* 🔥 Ele é **proxy + controle**, não backend
* 🔥 Pode integrar com **múltiplos serviços diferentes**
* 🔥 Suporta **transformação de request/response**
* 🔥 Trabalha bem com arquitetura de **microservices**

---

# 🔟 Exemplo real (cai muito)

👉 Um app com:

* `/users` → Lambda
* `/orders` → ECS
* `/static` → S3

➡️ Tudo exposto via **um único endpoint**

---

# 🧠 Resumo final (pra decorar rápido)

👉 API Gateway = **entrada única + roteamento + segurança**

* Cliente → API Gateway
* Gateway → múltiplos backends
* Pode usar:

  * ELB
  * ECS
  * EC2
  * S3

---

Se quiser, posso te mandar:
✅ 5 questões estilo prova DVA só de arquitetura
✅ ou um mapa mental juntando API Gateway + Lambda + DynamoDB (cai MUITO junto)

## 🌐 WebSocket no API Gateway (DVA-C02)

👉 **WebSocket API** no API Gateway permite comunicação **bidirecional em tempo real** entre cliente e servidor.

---

## 🧠 Conceito rápido

👉 Diferente do HTTP:

* HTTP = request → response (curto, stateless)
* WebSocket = conexão **persistente (aberta)**

📌 Ou seja:

* Cliente conecta uma vez
* Depois **ambos podem enviar mensagens a qualquer momento**

---

## ⚙️ Como funciona no AWS

### 🔌 Conexão

1. Cliente conecta via WebSocket
2. API Gateway cria um **connectionId**
3. Essa conexão fica ativa

---

### 🧩 Rotas (Routes)

Você define rotas baseadas em eventos:

* `$connect` → quando conecta
* `$disconnect` → quando desconecta
* `$default` → fallback
* Rotas custom (ex: `sendMessage`)

---

### 🔗 Integração

Normalmente com:

* **Lambda** (mais comum)
* DynamoDB (guardar conexões)
* Outros serviços AWS

---

## 🔥 Exemplo de fluxo

1. Cliente conecta (`$connect`)
2. Salva `connectionId` no DynamoDB
3. Cliente envia mensagem
4. Lambda processa
5. Lambda responde usando:

   ```
   @connections API
   ```

---

## 📡 Enviar mensagem de volta

👉 Usa endpoint especial do API Gateway:

```
POST /@connections/{connectionId}
```

---

## 🧠 Casos de uso (cai na prova)

* Chat em tempo real 💬
* Notificações instantâneas 🔔
* Jogos online 🎮
* Dashboards live 📊

---

## ⚠️ Diferença HTTP vs WebSocket (DECORAR)

| Feature     | HTTP API         | WebSocket API           |
| ----------- | ---------------- | ----------------------- |
| Comunicação | Request/Response | Bidirecional            |
| Conexão     | Curta            | Persistente             |
| Tempo real  | ❌                | ✅                       |
| Estado      | Stateless        | Stateful (connectionId) |

---

## ⚠️ Pegadinhas de prova

* 🔥 WebSocket mantém conexão aberta
* 🔥 Usa `connectionId`
* 🔥 Pode enviar mensagem **sem novo request do cliente**
* 🔥 Precisa gerenciar conexões (ex: DynamoDB)

---

## 🚀 Resumo final

👉 WebSocket API = **tempo real + conexão persistente**

* Conecta → ganha `connectionId`
* Rotas: `$connect`, `$disconnect`, `$default`
* Backend (Lambda) pode enviar mensagens de volta

---

Se quiser, posso te mandar:
👉 3 questões estilo prova só sobre WebSocket (esse tema às vezes aparece como pegadinha)

