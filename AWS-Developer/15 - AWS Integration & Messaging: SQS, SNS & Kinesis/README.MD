# 📬 AWS SQS — Messaging (DVA-C02)

## 1️⃣ O que é o SQS? 🤔

➡️ Serviço de **mensageria totalmente gerenciado (serverless)**
➡️ Permite **desacoplar aplicações**
➡️ Baseado em **filas (queues)**

💡 **Essência para prova:**

* Produtor envia mensagem → Fila → Consumidor processa
* Evita dependência direta entre serviços

---

## 2️⃣ Tipos de Filas 🧠

### 🔹 Standard Queue

* ⚡ Alta performance (quase ilimitada)
* ❗ **Ordem NÃO garantida**
* ❗ Possíveis duplicatas (at-least-once)

👉 Use quando:

* Alta escala
* Ordem não importa

---

### 🔹 FIFO Queue

* 🔒 Ordem garantida (First-In-First-Out)
* 🚫 Sem duplicação (exactly-once)
* ⚠️ Throughput limitado

👉 Use quando:

* Ordem importa (ex: transações financeiras)

💡 **Dica prova:**

* FIFO → nome termina com `.fifo`

---

## 3️⃣ Message Visibility Timeout 👻

➡️ Tempo em que a mensagem fica **invisível após ser consumida**

### Fluxo:

1. Consumer faz `ReceiveMessage`
2. Mensagem some da fila (temporariamente)
3. Se NÃO deletar → volta para fila

---

### 🔥 Pegadinha clássica:

* ❗ Se o tempo for curto → mensagem pode ser processada **duas vezes**
* ❗ Se for longo demais → atraso no retry

---

### 🧠 Ajustes importantes:

* `ChangeMessageVisibility` → altera dinamicamente
* Ideal: tempo > tempo de processamento

---

## 4️⃣ Dead Letter Queue (DLQ) ☠️

➡️ Fila para mensagens que falharam várias vezes

### Como funciona:

* Define:

  * `maxReceiveCount` (ex: 3)
* Se falhar 3x → vai para DLQ

---

### 💡 Para prova:

* Debug
* Evitar loop infinito
* Isolar mensagens problemáticas

---

## 5️⃣ Delay Queues ⏳

➡️ Atrasam entrega da mensagem

* Mensagem só fica visível após X segundos

### Configuração:

* Nível da fila OU mensagem

---

💡 **Use quando:**

* Retry controlado
* Processamento futuro

---

## 6️⃣ Access Policy 🔐

➡️ Controle de acesso via **IAM + Resource Policy**

Permite:

* Quem pode enviar (`SendMessage`)
* Quem pode consumir (`ReceiveMessage`)

---

💡 **Cross-account?**

* Usa **SQS Policy (resource-based)**

---

## 7️⃣ Long Polling vs Short Polling 🎣

### 🔹 Short Polling (default)

* Retorna imediatamente
* Pode não encontrar mensagens

---

### 🔹 Long Polling

* Espera até 20 segundos
* Reduz custo
* Melhor performance

---

💡 **Dica prova:**

* Sempre preferir **Long Polling**

---

## 8️⃣ Message Retention 🗂️

➡️ Tempo que mensagem fica na fila

* Default: **4 dias**
* Máx: **14 dias**

---

## 9️⃣ Batch Operations 📦

➡️ Enviar/receber múltiplas mensagens

* Até 10 por request

💡 Melhora performance e reduz custo

---

## 🔟 Integrações comuns 🔗

* Lambda (event source)
* SNS → fan-out
* S3 / DynamoDB (event-driven)

---

## 1️⃣1️⃣ SQS + Lambda ⚡

➡️ Lambda pode consumir automaticamente

### Importante:

* Batch size
* Retry automático
* DLQ integrado

---

💡 **Pegadinha:**

* Lambda NÃO deleta manualmente → AWS gerencia

---

## 1️⃣2️⃣ FIFO Avançado 🧠

### Message Group ID

➡️ Garante ordem dentro do grupo

* Paralelismo por grupo

---

### Deduplication ID

➡️ Evita duplicatas

* Automático ou manual

---

💡 **Regra de ouro:**

* Mesmo Group ID → ordem garantida
* Grupos diferentes → paralelo

---

## 🧪 Resumo de Prova (🔥 ESSENCIAL)

| Conceito           | Cai MUITO |
| ------------------ | --------- |
| Visibility Timeout | 🔥🔥🔥    |
| DLQ                | 🔥🔥🔥    |
| FIFO vs Standard   | 🔥🔥🔥    |
| Long Polling       | 🔥🔥      |
| Lambda + SQS       | 🔥🔥      |
| Delay Queue        | 🔥        |

---

## 🧠 Mnemonics (pra decorar)

* **SQS = Buffer entre serviços**
* **Visibility = “peguei mas ainda não terminei”**
* **DLQ = “desiste e joga pra análise”**
* **FIFO = ordem + sem duplicar**
* **Standard = rápido + pode duplicar**

---

Boa, **isso aqui é nível prova mesmo** — pouca gente estuda e a AWS adora cobrar 😈

Vou complementar teu README com a parte que faltou 👇

---

# ➕ 1️⃣3️⃣ SQS Extended Client (⚠️ Avançado e MUITO cobrado)

## 📦 Problema

➡️ SQS tem limite de mensagem:

* **256 KB (máximo)**

❗ E se precisar enviar arquivos maiores?

---

## 💡 Solução: SQS Extended Client

➡️ Biblioteca que usa **Amazon S3 + SQS juntos**

---

## ⚙️ Como funciona

1. Producer envia mensagem grande
2. Payload é armazenado no **S3**
3. SQS recebe **apenas uma referência (pointer)**

---

### 🔄 Fluxo:

```
Producer → S3 (payload)
         → SQS (referência)

Consumer → SQS → busca no S3
```

---

## 🧠 Para prova (ESSENCIAL)

### ✅ Vantagens:

* Permite mensagens **> 256 KB**
* Escala com S3
* Transparente para aplicação

---

### ❗ Pegadinhas:

* SQS NÃO armazena o payload grande
* Precisa gerenciar:

  * Bucket S3
  * Permissões IAM

---

### 🔐 Segurança

* Precisa de acesso:

  * SQS
  * S3

---

## 🚨 IMPORTANTE (cai em prova)

Se a questão disser:

> “Preciso enviar mensagens maiores que 256 KB no SQS”

👉 Resposta correta:

➡️ **Usar SQS Extended Client com S3**

---

## ⚠️ Limitações

* Aumenta latência (S3 + SQS)
* Mais complexo que SQS puro
* Custo adicional (S3)

---

## 🧪 Comparação rápida

| Cenário               | Solução                  |
| --------------------- | ------------------------ |
| Mensagem pequena      | SQS normal               |
| Mensagem grande       | SQS Extended Client + S3 |
| Arquivo grande direto | S3 + evento              |

---

## 🧠 Mnemonic

* **“Grande demais? Vai pro S3”**

---

## 🔥 EXTRA (nível hard de prova)

👉 Pode cair assim:

> “Aplicação usa SQS e precisa suportar payloads grandes sem mudar arquitetura”

✔️ Resposta:

* **SQS Extended Client**

---
Perfeito — isso cai MUITO na DVA (principalmente CLI/API + atributos) 😈
Vou te adicionar uma sessão no padrão README 👇

---

# ➕ 1️⃣4️⃣ SQS API — CreateQueue & Operações 🔧

## 1️⃣ CreateQueue 🏗️

➡️ Cria uma fila no **Amazon SQS**

---

### 📌 Exemplo (CLI)

```bash
aws sqs create-queue \
  --queue-name minha-fila \
  --attributes VisibilityTimeout=60
```

---

## 🧠 Atributos IMPORTANTES (Cai MUITO)

### 🔹 VisibilityTimeout

➡️ Tempo que mensagem fica invisível após consumo

* Default: **30s**
* Ajuste via:

  * CreateQueue
  * SetQueueAttributes

---

### 🔹 MessageRetentionPeriod

➡️ Tempo que mensagem fica na fila

* Min: 60s
* Max: 14 dias
* Default: 4 dias

---

### 🔹 DelaySeconds

➡️ Delay padrão da fila

* 0 a 900s (15 min)

---

### 🔹 ReceiveMessageWaitTimeSeconds

➡️ Ativa **Long Polling**

* 0 = short polling
* Até 20s = long polling ✅

---

### 🔹 MaximumMessageSize

➡️ Tamanho máximo da mensagem

* Default: 256 KB
* Não pode passar disso ❗

---

## 🔐 FIFO (CreateQueue)

Para criar FIFO:

```bash
aws sqs create-queue \
  --queue-name minha-fila.fifo \
  --attributes FifoQueue=true
```

---

### ⚠️ Regras FIFO (PEGADINHA)

* Nome DEVE terminar com `.fifo`
* Precisa de:

  * `MessageGroupId`
  * (Opcional) `MessageDeduplicationId`

---

## 2️⃣ SendMessage 📤

➡️ Envia mensagem para fila

```bash
aws sqs send-message \
  --queue-url URL \
  --message-body "Hello"
```

---

### FIFO extra:

```bash
--message-group-id "grupo-1"
```

---

## 3️⃣ ReceiveMessage 📥

➡️ Consome mensagens

```bash
aws sqs receive-message \
  --queue-url URL \
  --max-number-of-messages 10
```

---

💡 Pode retornar vazio (short polling)

---

## 4️⃣ DeleteMessage 🗑️

➡️ Remove mensagem da fila

```bash
aws sqs delete-message \
  --queue-url URL \
  --receipt-handle XYZ
```

---

⚠️ **SUPER IMPORTANTE**

* Se NÃO deletar → mensagem volta após visibility timeout

---

## 5️⃣ ChangeMessageVisibility 🔄

➡️ Altera visibility timeout de UMA mensagem

```bash
aws sqs change-message-visibility \
  --queue-url URL \
  --receipt-handle XYZ \
  --visibility-timeout 120
```

---

💡 Use quando:

* Processamento demora mais que o esperado

---

## 6️⃣ DeleteQueue ❌

➡️ Deleta fila

```bash
aws sqs delete-queue --queue-url URL
```

---

## 🔥 Pegadinhas de prova

### ❗ 1. CreateQueue é idempotente

➡️ Se já existir com mesmos atributos:

* Retorna a URL da fila
* NÃO cria outra

---

### ❗ 2. Não pode mudar tipo da fila

* Standard ↔ FIFO ❌
* Precisa recriar

---

### ❗ 3. Mensagem só “sai” com delete

* Receive ≠ Delete

---

### ❗ 4. Visibility não remove mensagem

* Só esconde temporariamente

---

### ❗ 5. Long polling reduz custo

* Menos chamadas vazias

---

## 🧠 Resumo rápido (Prova)

| Ação             | Função          |
| ---------------- | --------------- |
| CreateQueue      | Criar fila      |
| SendMessage      | Enviar          |
| ReceiveMessage   | Ler             |
| DeleteMessage    | Remover         |
| ChangeVisibility | Ajustar timeout |
| DeleteQueue      | Apagar fila     |

---

## 🧠 Mnemonic final

* **Create → Send → Receive → Delete**
* **Não deletou = volta**
* **FIFO = .fifo + ordem**
* **Visibility = invisível, não deletado**

---



