# 📘 README – Seção 18: Integrações Cloud (AWS Cloud Practitioner)

---

## 1️⃣ AWS Kinesis

Amazon Kinesis é um serviço para processamento de dados em tempo real (streaming).

Ele permite:

* Coletar
* Processar
* Analisar dados em tempo real

Exemplos de uso:

* Logs de aplicação
* Dados de IoT
* Monitoramento
* Clickstream (cliques de usuários)

📌 Característica principal:
Processamento contínuo de grandes volumes de dados.

Na prova:
Kinesis = streaming de dados em tempo real.

---

## 2️⃣ AWS SQS (Simple Queue Service)

Amazon SQS é um serviço de fila de mensagens.

Função:
Permite que sistemas se comuniquem de forma desacoplada.

Exemplo:

* Aplicação envia mensagem para fila
* Outro serviço processa depois

Benefícios:

* Desacoplamento
* Escalabilidade
* Tolerância a falhas

Tipos de fila:

### 🔹 Standard

* Alta taxa de transferência
* Entrega pelo menos uma vez
* Pode ter duplicidade

### 🔹 FIFO

* Ordem garantida
* Sem duplicidade
* Throughput menor

📌 Muito cobrado:
SQS = comunicação assíncrona entre sistemas.

---

## 3️⃣ AWS SNS (Simple Notification Service)

Amazon SNS é um serviço de notificação.

Modelo:
Pub/Sub (publicador e múltiplos assinantes)

Pode enviar mensagens para:

* Email
* SMS
* SQS
* Lambda
* HTTP endpoints

Diferença principal:

| Serviço | Modelo                                    |
| ------- | ----------------------------------------- |
| SQS     | Fila (1 consumidor processa mensagem)     |
| SNS     | Publicação (envia para vários assinantes) |

📌 Na prova:
SNS = notificação para múltiplos destinos.
SQS = fila para processamento assíncrono.

---

# 🎯 Comparação Importante

| Serviço | Uso Principal                          |
| ------- | -------------------------------------- |
| Kinesis | Processamento de dados em tempo real   |
| SQS     | Fila de mensagens (desacoplamento)     |
| SNS     | Notificações para múltiplos assinantes |

---

# 🧠 O que mais cai na prova

* Diferença entre SQS e SNS
* Conceito de desacoplamento
* Processamento em tempo real → Kinesis
* Comunicação assíncrona → SQS
* Envio para múltiplos destinos → SNS

---

# 📌 Resumo Final

* Kinesis → Streaming em tempo real
* SQS → Fila de mensagens
* SNS → Serviço de notificações (Pub/Sub)

Esses serviços são usados para integrar aplicações de forma escalável e desacoplada.

---

