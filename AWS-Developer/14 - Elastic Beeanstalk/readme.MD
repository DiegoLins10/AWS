
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

## 6️⃣ Deployment Strategies 🔄 (Cai em prova)

* **All at once** → rápido, downtime 😬
* **Rolling** → atualiza em batches
* **Rolling with additional batch** → mais seguro
* **Immutable** ⭐ → cria novas instâncias (mais seguro)

💡 **DVA tip:**
👉 Immutable = zero downtime + rollback fácil

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

