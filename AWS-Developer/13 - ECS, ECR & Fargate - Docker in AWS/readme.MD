# 📦 Seção 16: ECS, ECR & Fargate (Docker in AWS) — **VERSÃO TURBINADA 🚀**

## 1️⃣ Docker Basics 🐳

* Container = aplicação + dependências
* Imagem = template imutável
* Container = instância da imagem

💡 **Mental Model (IMPORTANTE):**

```
Imagem → vira → Container → roda no ECS
```

💡 **DVA Tip**

* Docker NÃO é AWS
* ECS/EKS usam Docker por baixo

---

## 2️⃣ Amazon ECS (Elastic Container Service)

### 🔹 O que é?

* Orquestrador de containers (AWS-native)

💡 **Comparação rápida:**

| Serviço | Ideia                 |
| ------- | --------------------- |
| ECS     | Simples, AWS-native   |
| EKS     | Kubernetes (complexo) |

---

### 🔹 Modos de execução

| Modo    | Quem gerencia infra? | Quando usar             |
| ------- | -------------------- | ----------------------- |
| EC2     | Você                 | Mais controle           |
| Fargate | AWS                  | Simplicidade (PROVA ❤️) |

💡 **Decore:**

* Fargate = serverless containers
* EC2 = você gerencia servidor

---

## 3️⃣ ECS Components 🧠

### 🔹 Cluster

* Agrupa recursos (EC2 ou Fargate)

---

### 🔹 Task Definition (**SUPER IMPORTANTE**)

Blueprint do container:

* CPU / memória
* imagem Docker (ECR)
* portas
* env vars

💡 **Prova:**
➡️ “configuração do container” → Task Definition

---

### 🔹 Task

* Container rodando (instância)

---

### 🔹 Service (**CAI MUITO**)

* Mantém N tasks rodando
* Faz:

  * Auto Scaling
  * Load Balancing
  * Deploy (rolling update)

💡 **Resumo:**

```
Task Definition → Task → Service controla tudo
```

---

## 4️⃣ ECS Auto Scaling 📈

Dois níveis (PEGADINHA 🚨):

### 🔹 1. Service Auto Scaling

* Escala número de **tasks**
* Baseado em CPU/memória

### 🔹 2. EC2 Auto Scaling

* Escala **instâncias EC2**

💡 **Prova:**

* Quer escalar containers → Service Auto Scaling
* NÃO confundir com EC2 scaling

---

## 5️⃣ Rolling Updates 🔄 (**AGORA SIM CLARO**)

### 🔹 O que é?

Atualizar containers **sem downtime**

---

### 🔹 Como funciona (PASSO A PASSO 🧠)

Exemplo: você tem **4 tasks rodando**

1. ECS começa novas tasks (nova versão)
2. Só depois mata as antigas
3. Sempre mantém um mínimo saudável

---

### 🔹 Parâmetros IMPORTANTES

#### ✅ Minimum healthy percent

* % mínima de tasks que devem estar rodando

👉 Exemplo:

* 4 tasks
* 50% → pelo menos **2 precisam estar vivas**

---

#### ✅ Maximum percent

* % máximo de tasks rodando durante deploy

👉 Exemplo:

* 4 tasks
* 200% → pode subir até **8 tasks temporariamente**

---

### 🔹 Cenário clássico de prova 🎯

| Configuração | Resultado                         |
| ------------ | --------------------------------- |
| Min 100%     | NUNCA para nenhuma task           |
| Max 200%     | Cria novas antes de matar antigas |

💡 **Tradução prática:**

```
Deploy seguro = sobe novo → depois mata antigo
```

---

### 🔹 Regra de ouro pra prova

* Zero downtime → **Min ≥ 100%**
* Deploy rápido → aumentar Max %

---

💡 **PEGADINHA 🚨**

* Se Min for baixo → pode ter downtime
* Se Max for baixo → deploy lento

---

## 6️⃣ Task Placement 🧩

Define ONDE os containers rodam

| Estratégia | Objetivo                 |
| ---------- | ------------------------ |
| Binpack    | 💰 reduzir custo         |
| Random     | aleatório                |
| Spread     | 🛡️ alta disponibilidade |

💡 **Decore:**

* HA → Spread
* Custo → Binpack

---

## 7️⃣ ECS + Load Balancer ⚖️

* Usa **Application Load Balancer (ALB)**

💡 **Arquitetura padrão (CAI MUITO):**

```
User → ALB → ECS Service → Tasks
```

---

## 8️⃣ Amazon ECR 📦

### 🔹 O que é?

* “Docker Hub da AWS”

### 🔹 Fluxo clássico

```
Docker build → push ECR → ECS puxa imagem
```

💡 **PEGADINHA:**

* ❌ ECR NÃO executa containers
* ✅ Só armazena imagens

---

## 9️⃣ ECS vs EKS ⚔️

| Feature      | ECS          | EKS        |
| ------------ | ------------ | ---------- |
| Complexidade | Baixa        | Alta       |
| Kubernetes   | ❌            | ✅          |
| Ideal        | Simplicidade | K8s padrão |

💡 **Prova:**

* Kubernetes → EKS
* Simples → ECS

---

## 🔟 Fargate 🚀 (**TOP 3 MAIS COBRADO**)

### 🔹 O que é?

* Serverless containers

---

### 🔹 Você NÃO gerencia:

* EC2
* Scaling infra
* Patch

---

### 🔹 Você configura:

* CPU
* memória

---

💡 **Quando usar (PROVA):**

* Não quer gerenciar servidor
* Aplicação simples
* Deploy rápido

---

## 1️⃣1️⃣ Segurança 🔐

* IAM Role para Task
* Security Group para container
* VPC integration

💡 **Prova:**

* Acesso AWS → **Task Role**
* ❌ Nunca credencial hardcoded

---

## 1️⃣2️⃣ Arquiteturas comuns 🏗️

### 🔹 Web App

```
ALB → ECS Service → Fargate Tasks
```

---

### 🔹 Microservices

* Vários ECS Services independentes

---

## 🚨 Pegadinhas de prova (OURO 🔥)

* ❌ ECS ≠ serverless (só Fargate)
* ❌ ECR NÃO roda container
* ❌ Task ≠ Service
* ❌ EC2 mode → você gerencia infra
* ❌ Rolling mal configurado → downtime

---

## 🧠 RESUMO FINAL (DECORAR)

```
ECS = orquestrador
Fargate = serverless
ECR = imagens
Task Definition = blueprint
Task = container rodando
Service = mantém vivo + scaling + deploy
ALB = entrada de tráfego
```

---
