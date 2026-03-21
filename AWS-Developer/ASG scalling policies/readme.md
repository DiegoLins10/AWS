# 📊 Seção: Auto Scaling + CloudWatch (Scaling Policies)

## 1️⃣ Tipos de Scaling no ASG ⚙️

O Auto Scaling Group (ASG) suporta **3 tipos principais**:

---

### ⭐ 1. Target Tracking Scaling

👉 Mantém uma métrica em um valor alvo

**Exemplos de métricas:**

* CPUUtilization
* RequestCountPerTarget (ALB)

✔️ Totalmente automático
✔️ Mais usado na prova

---

### 📈 2. Step Scaling

👉 Escala baseado em **faixas (thresholds)**

Ex:

* CPU > 60% → +1 instância
* CPU > 80% → +2 instâncias

✔️ Mais controle
❗ Precisa configurar alarmes no Amazon CloudWatch

---

### ⚠️ 3. Simple Scaling (LEGADO)

👉 Baseado em 1 alarme + cooldown

❌ Menos eficiente
❌ Pode atrasar scaling

---

## 2️⃣ Métricas importantes (CAI MUITO) 📊

### 🖥️ EC2

* CPUUtilization
* NetworkIn / NetworkOut

---

### 🌐 Load Balancer (ALB)

* RequestCountPerTarget ⭐
* TargetResponseTime

---

### 📦 SQS

* ApproximateNumberOfMessagesVisible

---

## 3️⃣ Target Tracking na prática 🧠

👉 Exemplo clássico de prova:

“Manter **100 requests por instância**”

✔️ Usa:

* ALB + RequestCountPerTarget
* Target Tracking

---

### 📐 Fórmula mental

\text{Instâncias} = \frac{\text{Requests Totais}}{\text{Requests por Instância}}

---

## 4️⃣ Quando usar cada tipo 🎯

| Cenário                       | Melhor escolha  |
| ----------------------------- | --------------- |
| Manter CPU estável            | Target Tracking |
| Manter requests por instância | Target Tracking |
| Regras específicas de scaling | Step Scaling    |
| Sistema legado                | Simple Scaling  |

---

## 5️⃣ Integração com serviços 🔗

### ASG funciona com:

* Amazon EC2
* Elastic Load Balancing
* Amazon CloudWatch

💡 CloudWatch fornece métricas → ASG toma decisão

---

## 6️⃣ Pegadinhas de prova 🚨

### ❗ 1. “Manter valor automaticamente”

👉 Target Tracking

---

### ❗ 2. “Diferentes níveis de ação”

👉 Step Scaling

---

### ❗ 3. Requests por instância

👉 Só com **ALB + Target Tracking**

---

### ❗ 4. Cooldown manual

👉 Simple Scaling

---

## 7️⃣ Resumo final (pra decorar) 🧠

* Target Tracking = automático ⭐
* Step Scaling = controle fino
* Simple = legado

💡 Regra de ouro:

> “Se a questão fala manter métrica → Target Tracking”

---
