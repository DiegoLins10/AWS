# 📊 Seção 20: AWS Monitoring & Audit (CloudWatch, X-Ray, CloudTrail, EventBridge)

---

## 1️⃣ Visão Geral 🧠

➡️ Monitoramento = **CloudWatch + X-Ray**
➡️ Auditoria = **CloudTrail**
➡️ Automação/Eventos = **EventBridge**

💡 **DVA Tip**

* CloudWatch = métricas + logs + alarmes
* X-Ray = tracing (debug distribuído)
* CloudTrail = quem fez o quê na AWS
* EventBridge = reage a eventos

---

## 2️⃣ CloudWatch Metrics 📈

➡️ Métricas = dados numéricos ao longo do tempo

### 🔹 Exemplos

* CPUUtilization (EC2)
* RequestCount (ALB)
* Throttles (Lambda)

### 🔹 Características

* Namespace (AWS/EC2, AWS/Lambda…)
* Dimensions (InstanceId, FunctionName…)
* Período (1 min, 5 min…)

💡 **DVA Tip**

* Métricas padrão: 1 min ou 5 min
* Detailed Monitoring (EC2) = 1 min

---

## 3️⃣ CloudWatch Custom Metrics 🧩

➡️ Você envia suas próprias métricas

### 🔹 Usos

* Tempo de resposta custom
* Quantidade de pedidos
* Erros de negócio

### 🔹 Envio

* SDK / CLI → `PutMetricData`

💡 **DVA Tip**

* Por padrão: **granularidade mínima = 1 min**
* Pode usar **high resolution (1 sec)**

---

## 4️⃣ CloudWatch Logs 📜

➡️ Armazena logs de aplicações e serviços

### 🔹 Estrutura

* Log Group
* Log Stream

### 🔹 Fontes

* Lambda
* EC2 (via agent)
* API Gateway

---

## 5️⃣ CloudWatch Logs Insights 🔍

➡️ Query em logs (tipo SQL)

### 🔹 Exemplo

```
fields @timestamp, @message
| filter status = 500
| sort @timestamp desc
```

💡 **DVA Tip**

* Muito usado em debug de Lambda

---

## 6️⃣ CloudWatch Agent 🤖

➡️ Instala em EC2 para enviar:

* Logs
* Métricas custom (CPU, memória, disco)

💡 **Importante**

* EC2 não envia memória por padrão → precisa do Agent

---

## 7️⃣ Metric Filters 🎯

➡️ Converte logs em métricas

### 🔹 Exemplo

* Log contém "ERROR" → vira métrica

💡 **DVA Tip**

* Muito cobrado:
  👉 Logs → Metric Filter → Alarm

---

## 8️⃣ CloudWatch Alarms 🚨

➡️ Disparam ações com base em métricas

### 🔹 Ações

* SNS
* Auto Scaling
* Lambda

### 🔹 Tipos

* Static threshold
* Anomaly detection

💡 **DVA Tip**

* Estado: OK / ALARM / INSUFFICIENT_DATA

---

## 9️⃣ CloudWatch Synthetics 🧪

➡️ Testa endpoints automaticamente

### 🔹 Usa

* Canaries (scripts)

### 🔹 Exemplo

* Testar API a cada 5 min

💡 **Cai pouco**, mas bom saber:

* Simula usuário real

---

## 🔟 AWS X-Ray 🔍

➡️ Debug de aplicações distribuídas

### 🔹 Mostra:

* Latência
* Erros
* Dependências

### 🔹 Conceitos

* Trace
* Segment
* Subsegment

💡 **DVA Tip**

* Muito usado com:

  * Lambda
  * API Gateway
  * ECS

👉 Identifica gargalos (ex: DB lento)

---
# ⏱️ 6️⃣ CloudWatch Resolution (High vs Standard)

## 📌 O que é Resolution?

➡️ Define **a frequência dos dados das métricas**

👉 Quanto menor o intervalo → mais detalhado (mais caro)

---

## 🟢 Standard Resolution (Low Resolution)

➡️ **1 minuto (60s)**

### 🔹 Características

* Default do CloudWatch
* Menor custo
* Menos detalhado

### 🔹 Exemplo

* CPU de EC2 padrão
* Métricas da maioria dos serviços AWS

💡 **Resumo**
👉 Mais barato
👉 Menos granular

---

## 🔴 High Resolution

➡️ **1 segundo (1s)**

### 🔹 Características

* Muito mais detalhado
* Precisa ser **custom metric**
* Mais caro

### 🔹 Exemplo

* Monitoramento em tempo real
* Sistemas críticos / trading / streaming

💡 **Importante**
👉 Só funciona com **Custom Metrics**

---

## ⚔️ Comparação

| Feature   | Standard 🟢 | High 🔴    |
| --------- | ----------- | ---------- |
| Intervalo | 60s         | 1s         |
| Custo     | Baixo       | Alto       |
| Tipo      | Default     | Custom     |
| Uso       | Geral       | Tempo real |

---

## 🚨 Pegadinhas de prova

❗ EC2 Detailed Monitoring = **1 minuto (não é high resolution)**

❗ High resolution:

* Só com `PutMetricData`
* Precisa configurar explicitamente

---

## 🧠 Regra de ouro

👉 **Precisa de precisão alta (segundos)** → High Resolution
👉 **Monitoramento normal** → Standard

---

## 🔥 Resumo rápido (decoração)

👉 Standard = 1 min (default, barato)
👉 High = 1 sec (custom, caro)

---


## 1️⃣1️⃣ AWS CloudTrail 📜

➡️ Auditoria de chamadas na AWS

### 🔹 Registra

* Quem fez
* Quando
* Qual ação

### 🔹 Exemplo

* DeleteBucket
* CreateUser

### 🔹 Tipos

* Management Events
* Data Events (S3, Lambda)

💡 **DVA Tip**

* Vai para S3 (persistência)
* Usado para segurança/compliance

---

## 1️⃣2️⃣ Amazon EventBridge ⚡

➡️ Sistema de eventos (evolução do CloudWatch Events)

### 🔹 Funciona assim:

Evento → Regra → Target

### 🔹 Targets

* Lambda
* SNS
* SQS
* Step Functions

---

### 🔹 Exemplos

👉 EC2 mudou de estado → dispara Lambda
👉 CloudTrail detecta ação → dispara alerta

---

## 1️⃣3️⃣ EventBridge - Multi-Account 🏢

➡️ Centraliza eventos de várias contas

### 🔹 Uso

* Organização com várias contas AWS
* Conta central de monitoramento

💡 **DVA Tip**

* Muito comum em arquitetura enterprise

---

## 🧠 Resumo Final (Cai MUITO)

| Serviço     | Função Principal          |
| ----------- | ------------------------- |
| CloudWatch  | Métricas + Logs + Alarmes |
| X-Ray       | Tracing / Debug           |
| CloudTrail  | Auditoria                 |
| EventBridge | Automação por eventos     |

---

## ⚠️ Pegadinhas de Prova

### ❗ Logs vs Metrics

* Logs → texto
* Metrics → números

---

### ❗ CloudWatch vs CloudTrail

* CloudWatch → performance
* CloudTrail → auditoria

---

### ❗ Metric Filter Flow

👉 Logs → Filter → Metric → Alarm

---

### ❗ EC2 Monitoring

* CPU → automático
* Memória → precisa Agent

---

### ❗ EventBridge

* Baseado em eventos (event-driven)
* Substitui CloudWatch Events

---

# 🔍 Seção: AWS X-Ray & CloudTrail (Tracing vs Auditoria)

---

## 1️⃣ Visão Geral 🧠

| Serviço       | Função                                     |
| ------------- | ------------------------------------------ |
| X-Ray 🔍      | **Tracing (debug da aplicação)**           |
| CloudTrail 📜 | **Auditoria (ações de usuário / API AWS)** |

---

## 🚨 REGRA DE OURO (CAI NA PROVA)

👉 **X-Ray = tracing (fluxo da request)**
👉 **CloudTrail = ações de usuário (API AWS)**

---

# 🔍 2️⃣ AWS X-Ray (TRACING)

## 📌 O que é

➡️ Serviço de **distributed tracing**

👉 Analisa **requisições dentro da aplicação**

---

## 📊 O que ele mostra

* Latência
* Erros
* Fluxo entre serviços
* Gargalos

---

## 🔹 Exemplo de fluxo

Usuário → API Gateway → Lambda → DynamoDB

👉 X-Ray mostra:

* Tempo em cada etapa
* Onde falhou
* Dependências

---

## 🧱 Conceitos importantes

| Conceito   | Definição                         |
| ---------- | --------------------------------- |
| Trace      | Requisição completa               |
| Segment    | Serviço (Lambda, EC2…)            |
| Subsegment | Operação interna (DB call, HTTP…) |

---

## ⚙️ Instrumentação

➡️ Pode exigir código (SDK)
➡️ Pode ser automático em alguns serviços

### 🔹 Casos comuns:

* Lambda → só ativar X-Ray
* ECS → daemon + config
* EC2 → SDK/manual

---

## 🎯 Sampling Rules

➡️ Controla quantas requests serão rastreadas

💡 Evita custo alto

---

## 🔌 X-Ray APIs

* `PutTraceSegments`
* `PutTelemetryRecords`

💡 Pouco cobrado, mas bom saber

---

## 🐳 X-Ray com ECS / Beanstalk

➡️ Usa **X-Ray daemon**

* Sidecar container (ECS)
* Integrado no Beanstalk

---

## 🌐 AWS Distro for OpenTelemetry (ADOT)

➡️ Alternativa moderna ao X-Ray SDK

* Padrão open-source
* Integra com X-Ray

💡 **Trend atual da AWS**

---

## 🧠 Quando usar X-Ray

✔️ Debug de API
✔️ Analisar latência
✔️ Microservices
✔️ Serverless tracing

---

# 📜 3️⃣ AWS CloudTrail (AUDITORIA)

## 📌 O que é

➡️ Serviço de **auditoria de ações na AWS**

👉 Registra chamadas de API

---

## 🔍 O que ele registra

* Quem fez (IAM user/role)
* Qual ação (API)
* Quando
* De onde (IP)

---

## 🔹 Exemplos

* `CreateUser`
* `DeleteBucket`
* `RunInstances`

---

## 🧩 Tipos de eventos

| Tipo              | Descrição                   |
| ----------------- | --------------------------- |
| Management Events | Ações administrativas       |
| Data Events       | Ações em dados (S3, Lambda) |

---

## 📦 Armazenamento

➡️ Logs enviados para:

* S3
* CloudWatch Logs (opcional)

---

## ⚡ Integração com EventBridge

➡️ CloudTrail → EventBridge → ação automática

### 🔹 Exemplo

* DeleteBucket → dispara alerta (Lambda/SNS)

💡 Muito cobrado em prova

---

## 🧠 Quando usar CloudTrail

✔️ Saber quem fez algo
✔️ Auditoria / compliance
✔️ Segurança
✔️ Investigar incidentes

---

# ⚔️ 4️⃣ CloudTrail vs X-Ray vs CloudWatch

| Serviço       | Uso                        |
| ------------- | -------------------------- |
| CloudTrail 📜 | Ações de usuário (API AWS) |
| X-Ray 🔍      | Tracing da aplicação       |
| CloudWatch 📊 | Métricas + Logs            |

---

# 🔥 5️⃣ Cenários de Prova

## ❓ Quem deletou um bucket S3?

👉 ✅ CloudTrail

---

## ❓ API está lenta, onde está o problema?

👉 ✅ X-Ray

---

## ❓ Monitorar CPU de EC2?

👉 ✅ CloudWatch

---

## ❓ Detectar ação e disparar automação?

👉 ✅ CloudTrail + EventBridge

---

# ⚠️ Pegadinhas

❌ CloudTrail NÃO mostra latência
❌ X-Ray NÃO mostra usuário/API calls
❌ X-Ray NÃO substitui logs

---

# 🧠 Resumo Final

👉 **X-Ray = tracing (fluxo da request, debug)**
👉 **CloudTrail = ações de usuário (API AWS, auditoria)**

---



