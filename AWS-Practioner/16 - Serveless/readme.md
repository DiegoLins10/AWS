
# 📘 README – Seção 19: Computação e Serverless (AWS Cloud Practitioner)

---

## 1️⃣ AWS Batch

AWS Batch é um serviço para executar jobs em lote (batch processing).

Ele permite:

* Rodar grandes volumes de processamento
* Executar tarefas agendadas
* Processar dados em segundo plano

A AWS:

* Provisiona automaticamente recursos (EC2 ou Fargate)
* Escala conforme necessidade

Uso comum:

* Processamento de dados científicos
* Renderização
* Análise em lote

📌 Na prova:
Batch = processamento em lote automatizado.

---

## 2️⃣ AWS Lightsail

Lightsail é uma forma simplificada de usar infraestrutura na AWS.

Indicado para:

* Pequenos projetos
* Sites simples
* Aplicações pequenas
* WordPress

Características:

* Preço fixo mensal
* Configuração simplificada
* Inclui VM, storage e rede

📌 Na prova:
Lightsail = solução simples e previsível para aplicações pequenas.

---

## 3️⃣ AWS Lambda

Lambda é o principal serviço serverless da AWS.

Permite:

* Executar código sem gerenciar servidores
* Rodar funções sob demanda

Modelo:
Event-driven (executa quando um evento ocorre).

Exemplos de gatilhos:

* Upload no S3
* Mensagem no SQS
* Requisição via API Gateway

Características:

* Escalabilidade automática
* Paga apenas pelo tempo de execução
* Sem gerenciamento de infraestrutura

📌 Na prova:
Lambda = computação serverless baseada em eventos.

---

## 4️⃣ AWS Fargate

Fargate é uma opção serverless para containers.

Usado com:

* ECS
* EKS

Diferença:
Você não precisa gerenciar servidores EC2.

A AWS cuida:

* Infraestrutura
* Provisionamento
* Escalabilidade

📌 Na prova:
Fargate = rodar containers sem gerenciar instâncias.

---

# 🎯 Comparação Rápida

| Serviço   | Uso Principal                |
| --------- | ---------------------------- |
| Batch     | Processamento em lote        |
| Lightsail | Infra simples com preço fixo |
| Lambda    | Funções serverless           |
| Fargate   | Containers serverless        |

---

# 🧠 O que mais cai na prova

* Diferença entre EC2 e Lambda
* O que é serverless
* Quando usar Fargate
* Lightsail para aplicações simples
* Batch para processamento em massa

---

# 📌 Resumo Final

* Batch → Jobs em lote automatizados
* Lightsail → Solução simples e barata
* Lambda → Executar código sem servidor
* Fargate → Containers sem gerenciar EC2

Esses serviços representam diferentes formas de computação na AWS, desde infraestrutura simplificada até modelo totalmente serverless.

---

