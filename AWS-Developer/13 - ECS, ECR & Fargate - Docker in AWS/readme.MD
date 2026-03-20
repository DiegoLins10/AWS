

# 📦 Seção 16: ECS, ECR & Fargate (Docker in AWS)

## 1️⃣ Docker Basics 🐳

* Container = aplicação + dependências
* Imagem = template imutável
* Container = instância da imagem
* Docker elimina problema de “funciona na minha máquina”

💡 **DVA Tip**

* Docker NÃO é AWS → AWS usa Docker via ECS/EKS

---

## 2️⃣ Amazon ECS (Elastic Container Service)

### 🔹 O que é?

* Orquestrador de containers (tipo Kubernetes, mas AWS-native)

### 🔹 Modos de execução:

| Modo    | Infra gerenciada por quem? |
| ------- | -------------------------- |
| EC2     | Você gerencia instâncias   |
| Fargate | AWS gerencia tudo          |

💡 **Prova:**

* Fargate = serverless containers
* EC2 = mais controle / mais responsabilidade

---

## 3️⃣ ECS Components 🧠

### 🔹 Cluster

* Grupo lógico de recursos (EC2 ou Fargate)

### 🔹 Task Definition

* “Blueprint” do container
* Define:

  * CPU / memória
  * imagem Docker
  * portas
  * variáveis de ambiente

### 🔹 Task

* Instância de uma Task Definition

### 🔹 Service

* Mantém número desejado de tasks rodando
* Suporta auto scaling + load balancer

---

## 4️⃣ ECS Auto Scaling 📈

* Baseado em:

  * CPU
  * memória
  * métricas customizadas

💡 **Cai muito:**

* Service Auto Scaling ≠ EC2 Auto Scaling
* Pode escalar tasks automaticamente

---

## 5️⃣ Rolling Updates 🔄

* Atualiza containers sem downtime
* Controlado pelo ECS Service

Parâmetros importantes:

* **Minimum healthy percent**
* **Maximum percent**

💡 **Prova:**

* Deploy seguro → rolling update
* Zero downtime → configurar corretamente %

---

## 6️⃣ Task Placement 🧩

Define ONDE os containers rodam

### Estratégias:

* **Binpack** → otimiza uso (menos custo 💰)
* **Random** → distribuição aleatória
* **Spread** → alta disponibilidade

💡 **DVA Tip**

* Alta disponibilidade → Spread
* Custo → Binpack

---

## 7️⃣ ECS + Load Balancer ⚖️

* Integra com **Application Load Balancer (ALB)**
* Distribui tráfego entre containers

💡 **Cai MUITO:**

* ECS Service + ALB = padrão de produção

---

## 8️⃣ Amazon ECR (Elastic Container Registry) 📦

### 🔹 O que é?

* Repositório de imagens Docker (tipo Docker Hub)

### 🔹 Características:

* Privado por padrão
* Integrado com IAM
* Alta performance dentro da AWS

💡 **Fluxo típico:**

1. Build imagem Docker
2. Push → ECR
3. ECS puxa imagem do ECR

---

## 9️⃣ ECS vs EKS ⚔️

| Feature      | ECS          | EKS        |
| ------------ | ------------ | ---------- |
| Complexidade | Baixa        | Alta       |
| Controle     | Médio        | Alto       |
| Kubernetes   | ❌            | ✅          |
| Ideal para   | Simplicidade | Padrão K8s |

💡 **Prova:**

* Quer Kubernetes → EKS
* Quer simplicidade → ECS

---

## 🔟 Fargate 🚀 (IMPORTANTÍSSIMO)

### 🔹 O que é?

* Serverless para containers

### 🔹 Você NÃO gerencia:

* EC2
* Scaling de infra
* Patch

### 🔹 Você gerencia:

* CPU / memória da task

💡 **Cai MUITO:**

* Fargate = melhor opção se:

  * não quer gerenciar servidores
  * workload simples

---

## 1️⃣1️⃣ Segurança 🔐

* IAM Roles para tasks
* Security Groups para containers
* Integração com VPC

💡 **Prova:**

* Task Role → acesso AWS (S3, DynamoDB etc.)
* NÃO usar credenciais hardcoded

---

## 1️⃣2️⃣ Arquiteturas comuns 🏗️

### 🔹 Web App escalável:

* ALB → ECS Service → Tasks (Fargate)

### 🔹 Microservices:

* Vários services ECS independentes

---

## 🚨 Pegadinhas de prova

* ❌ ECS ≠ serverless (só com Fargate)
* ❌ ECR NÃO roda containers (só armazena)
* ❌ Task ≠ Service
* ❌ EC2 mode precisa gerenciar instância

---

## 🧠 Resumo Final (decora isso)

* ECS = orquestrador
* Fargate = serverless containers
* ECR = repositório de imagens
* Task Definition = blueprint
* Service = mantém containers vivos
* ALB = distribui tráfego

---

