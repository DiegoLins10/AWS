
# 🌱 Elastic Beanstalk — Visão Geral

## 1️⃣ O que é? 🤔

➡️ Serviço **PaaS (Platform as a Service)** da AWS
➡️ Você só envia o **código**, a AWS cuida da infra

💡 Em outras palavras:

* Você **não gerencia servidores diretamente**
* A AWS cria tudo automaticamente

---

## 2️⃣ O que ele provisiona por trás? ⚙️

Quando você faz deploy, ele cria automaticamente:

* Amazon EC2 → instâncias
* Elastic Load Balancing → balanceamento
* Auto Scaling → escala automática
* Amazon RDS → banco (opcional)
* Amazon S3 → armazenamento de artefatos

💡 **Resumo prova:**
👉 Beanstalk = "orquestrador" que cria esses serviços pra você

---

## 3️⃣ Fluxo de uso 🚀

1. Você sobe código (ZIP, Git, etc.)
2. Escolhe plataforma:

   * Java
   * Node.js
   * Python
   * .NET
   * Docker
3. Beanstalk:

   * Provisiona infra
   * Faz deploy
   * Monitora

---

## 4️⃣ Conceitos importantes 📦

### 🔹 Application

* Container lógico do app

### 🔹 Environment

* Ambiente rodando (DEV / PROD)

### 🔹 Version

* Versões do seu código

💡 Pode ter vários environments (ex: staging + prod)

---

## 5️⃣ Tipos de Environment 🌍

### 🟢 Web Server Environment

* Para apps web
* Usa Load Balancer

### 🟡 Worker Environment

* Para processamento assíncrono
* Usa fila (SQS)

---

Perfeito — vou deixar essa seção **completa nível prova DVA (com tudo que pode cair)** 👇

---

# 🔄 6️⃣ Deployment Strategies (Elastic Beanstalk)

## 1️⃣ All at once ⚡

👉 Atualiza **todas as instâncias de uma vez**

* ✅ Mais rápido
* ❌ **Downtime total**
* ❌ Sem rollback gradual

💡 **Quando usar:**

* Dev / teste
* Aplicações não críticas

---

## 2️⃣ Rolling 🔁

👉 Atualiza em **lotes (batches)**

* Parte das instâncias sai do ar por vez
* Outras continuam atendendo

✔️ Sem downtime total
❌ Pode degradar performance durante deploy

💡 **Risco:**

* Se der erro, parte do sistema já foi atualizada

---

## 3️⃣ Rolling with Additional Batch ➕

👉 Igual ao Rolling, mas cria **instâncias extras temporárias**

* Mantém capacidade total
* Mais seguro que Rolling

✔️ Menor impacto no usuário
❌ Custo temporariamente maior

💡 **DVA tip:**
👉 Muito usado quando não pode perder capacidade

---

## 4️⃣ Immutable ⭐

👉 Cria **novo Auto Scaling Group com novas instâncias**

* Não mexe nas instâncias antigas
* Só troca quando tudo estiver OK

✔️ **Zero downtime**
✔️ **Rollback fácil**
✔️ Mais seguro

❌ Mais caro (instâncias duplicadas temporariamente)

💡 **Regra de ouro:**
👉 **Mais seguro de todos**

---

## 5️⃣ Traffic Splitting 🚦

👉 Divide tráfego entre:

* versão antiga
* versão nova

Ex:

* 90% old
* 10% new

✔️ Teste gradual (canary)
✔️ Detecta problemas antes de impactar tudo

❌ Mais complexo

💡 Usa:

* Elastic Load Balancing

---

## 6️⃣ Blue/Green 🔵🟢

👉 Cria **ambiente totalmente novo**

* Blue = atual
* Green = novo

Depois:
👉 troca o tráfego (swap)

✔️ Zero downtime
✔️ Deploy seguro
✔️ Testes completos antes de ir pra produção

❌ Mais caro (2 ambientes rodando)

---

# ⚔️ Comparação geral (CAI MUITO)

| Strategy          | Downtime       | Segurança    | Custo           | Complexidade     |
| ----------------- | -------------- | ------------ | --------------- | ---------------- |
| All at once       | ❌ Alto         | ❌ Baixa      | 💰 Baixo        | 😀 Fácil         |
| Rolling           | ⚠️ Parcial     | ⚠️ Médio     | 💰 Médio        | 🙂 Médio         |
| Rolling + extra   | ⚠️ Muito baixo | 👍 Alto      | 💰💰 Médio/Alto | 🙂 Médio         |
| Immutable         | ✅ Zero         | ⭐ Muito alto | 💰💰 Alto       | 🙂 Médio         |
| Traffic Splitting | ✅ Zero         | ⭐ Alto       | 💰💰 Médio      | 😐 Mais complexo |
| Blue/Green        | ✅ Zero         | ⭐ Muito alto | 💰💰💰 Alto     | 😐 Mais complexo |

---

# 🧠 Pegadinhas de prova (IMPORTANTÍSSIMO)

### ❗ “Zero downtime + rollback fácil”

👉 **Immutable**

---

### ❗ “Testar nova versão com parte do tráfego”

👉 **Traffic Splitting**

---

### ❗ “Ambiente separado e troca completa”

👉 **Blue/Green**

---

### ❗ “Mais rápido possível”

👉 **All at once**

---

### ❗ “Atualização gradual”

👉 **Rolling**

---

# 🧠 Resumo pra decorar

* All at once → rápido 💀
* Rolling → gradual ⚖️
* Rolling + extra → seguro + capacidade
* Immutable → ⭐ padrão seguro
* Traffic splitting → canary 🧪
* Blue/Green → swap completo 🔄

---


## 7️⃣ Vantagens ✅

* Simples de usar
* Deploy rápido
* Auto scaling automático
* Integra com vários serviços

---

## 8️⃣ Desvantagens ❌

* Menos controle que EC2 puro
* Não é tão flexível quanto:

  * Amazon ECS
  * Amazon EKS

---

## 9️⃣ Comparação (🔥 Cai MUITO)

| Serviço   | Nível de controle | Complexidade |
| --------- | ----------------- | ------------ |
| EC2       | 🔥 Alto           | Difícil      |
| Beanstalk | ⚖️ Médio          | Fácil        |
| Lambda    | 🔽 Baixo          | Muito fácil  |

💡 **Regra mental:**

* Quer **controle total** → EC2
* Quer **facilidade** → Beanstalk
* Quer **serverless** → Lambda

---

## 🔟 Quando usar? 🎯

Use Beanstalk quando:

* Quer deploy rápido
* Não quer gerenciar infra
* App tradicional (web API, backend)

Evite quando:

* Precisa controle fino de arquitetura
* Usa microservices complexos → ECS/EKS

---

## 🧠 Resumo pra prova (memorização rápida)

* ✅ PaaS da AWS
* ✅ Deploy de código direto
* ✅ Cria EC2 + ELB + ASG automaticamente
* ✅ Suporta várias linguagens
* ✅ Tem strategies de deploy (Immutable ⭐)

---

