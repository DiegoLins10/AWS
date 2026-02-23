# 📘 README – Seção 17: Containers (AWS Cloud Practitioner)

---

## 1️⃣ O que é Docker

Docker é uma plataforma que permite criar e executar aplicações dentro de containers.

### 📌 O que é um container?

Um container é:

* Um ambiente isolado
* Leve
* Portável
* Contém aplicação + dependências

Diferença principal:

* VM virtualiza sistema operacional
* Container compartilha o kernel do host (mais leve)

Benefícios:

* Portabilidade
* Consistência entre ambientes
* Inicialização rápida
* Menor consumo de recursos

📌 Para a prova:
Docker = tecnologia que empacota aplicação e dependências em containers.

---

## 2️⃣ Amazon Elastic Container Service (ECS)

Amazon ECS é o serviço gerenciado da AWS para rodar containers.

Ele permite:

* Executar containers Docker
* Orquestrar containers
* Escalar aplicações automaticamente

Pode rodar em:

### 🔹 EC2

Você gerencia as instâncias.

### 🔹 Fargate

Serverless (AWS gerencia infraestrutura).

📌 Muito importante:
Fargate elimina a necessidade de gerenciar servidores.

Uso comum:

* Microservices
* APIs
* Aplicações modernas

---

## 3️⃣ Amazon Elastic Kubernetes Service (EKS)

Amazon EKS é o serviço gerenciado da AWS para rodar Kubernetes.

Kubernetes é uma plataforma open-source para orquestração de containers.

O EKS:

* Gerencia o plano de controle do Kubernetes
* Permite rodar containers em EC2 ou Fargate

Diferença principal:

| Serviço | Característica                   |
| ------- | -------------------------------- |
| ECS     | Orquestrador proprietário da AWS |
| EKS     | Kubernetes gerenciado            |

📌 Para a prova:
EKS é usado quando a empresa quer Kubernetes.
ECS é solução nativa da AWS.

---

# 🎯 O que mais cai na prova

* Diferença entre VM e container
* O que é Docker
* Diferença entre ECS e EKS
* O que é Fargate
* Quando usar Kubernetes (EKS)

---

# 📌 Resumo Final

* Docker → Tecnologia de containers
* ECS → Orquestração de containers na AWS
* EKS → Kubernetes gerenciado
* Fargate → Rodar containers sem gerenciar servidores

---

