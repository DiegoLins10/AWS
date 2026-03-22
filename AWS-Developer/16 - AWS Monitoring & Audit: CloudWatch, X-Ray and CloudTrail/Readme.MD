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


