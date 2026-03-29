# 📬 AWS SQS — Messaging (DVA-C02)

## 1️⃣ O que é o SQS? 🤔

➡️ Serviço de **mensageria totalmente gerenciado (serverless)** 
➡️ Permite **desacoplar aplicações** 
➡️ Baseado em **filas (queues)** 
➡️ Tamanho maximo de mensagem 256kb** 

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


# ➕ 1️⃣5️⃣ Amazon SNS — Pub/Sub & Fan-Out 📢

## 1️⃣ O que é o SNS? 🤔

➡️ O **Amazon SNS** é um serviço de:

### 👉 **Pub/Sub (Publish/Subscribe)**

* 1 produtor → vários consumidores

---

## 🧠 Tradução simples

* SNS = **disparador de mensagens**
* Ele NÃO armazena (como SQS)
* Ele **entrega imediatamente**

---

## 2️⃣ Como funciona 📬

### 📌 Fluxo:

```id="sns-flow"
Publisher → SNS Topic → Subscribers
```

---

### Componentes:

* **Publisher** → envia mensagem
* **Topic** → canal
* **Subscribers** → recebem

---

## 3️⃣ Tipos de Subscribers 👀

SNS pode enviar para:

* SQS ✅ (mais comum)
* Lambda
* HTTP/HTTPS
* Email
* SMS

---

💡 **Para prova:**

* Integração mais importante = **SNS + SQS**

---

## 4️⃣ Fan-Out Pattern 📡 (🔥 MUITO IMPORTANTE)

➡️ Um evento → múltiplos destinos

---

### 📌 Exemplo:

```id="fanout"
App → SNS → SQS1
          → SQS2
          → Lambda
```

---

💡 Cada consumidor recebe **sua própria cópia**

---

## 🧠 Vantagem

* Desacoplamento total
* Escala independente
* Paralelismo

---

## 5️⃣ SNS vs SQS 🧠

| SNS              | SQS              |
| ---------------- | ---------------- |
| Push             | Pull             |
| Entrega imediata | Consumidor busca |
| Não armazena     | Armazena         |
| Fan-out          | Processamento    |

---

💡 **Resumo:**

* SNS = distribuir
* SQS = processar

---

## 6️⃣ SNS + SQS (🔥 Arquitetura clássica)

➡️ Melhor dos dois mundos:

* SNS → distribui
* SQS → garante processamento

---

### Benefícios:

* Retry automático
* Buffer
* Resiliência

---

## 7️⃣ Message Filtering 🎯

➡️ Subscriber recebe só mensagens específicas

---

### Exemplo:

* Mensagem: `{ tipo: "pedido" }`
* Filtro: só `pedido`

---

💡 Evita processamento desnecessário

---

## 8️⃣ FIFO SNS ⚠️

➡️ SNS também suporta FIFO

---

### Regras:

* Topic termina com `.fifo`
* Compatível com SQS FIFO
* Mantém ordem

---

💡 Pegadinha:

* Só funciona com endpoints compatíveis (ex: SQS FIFO)

---

## 9️⃣ Delivery & Retry 🔄

➡️ SNS tenta entregar automaticamente

* Retry configurável
* Pode usar DLQ

---

## 🔟 Segurança 🔐

* IAM policies
* Resource policies (cross-account)
* Encryption (KMS)

---

## 🔥 Pegadinhas de prova

### ❗ 1. SNS NÃO armazena mensagens

* Se subscriber falhar → pode perder (sem SQS)

---

### ❗ 2. Fan-out = múltiplos destinos

* Não confundir com fila

---

### ❗ 3. SNS + SQS = padrão recomendado

* Alta confiabilidade

---

### ❗ 4. Filtering evita custo

* Muito cobrado

---

### ❗ 5. Push vs Pull

* SNS → push
* SQS → pull

---

## 🧠 Mnemonics

* **SNS = megafone 📢**
* **Fan-out = espalhar mensagem**
* **SNS entrega / SQS segura**

---

## 🧪 Resumo de Prova

| Conceito     | Cai MUITO |
| ------------ | --------- |
| Fan-out      | 🔥🔥🔥    |
| SNS vs SQS   | 🔥🔥🔥    |
| Filtering    | 🔥🔥      |
| SNS + SQS    | 🔥🔥🔥    |
| Push vs Pull | 🔥🔥      |

---

# ➕ 1️⃣6️⃣ Kinesis Data Streams vs Firehose 🔥🌊

## 1️⃣ Visão geral 🤔

### 🌊 **Amazon Kinesis Data Streams**

➡️ Serviço de **streaming real-time com controle total**

---

### 🔥 **Amazon Kinesis Data Firehose**

➡️ Serviço para **entregar dados automaticamente para destinos**

---

## 2️⃣ Diferença principal (ESSÊNCIA DA PROVA) 🧠

| Kinesis Data Streams | Firehose          |
| -------------------- | ----------------- |
| Você PROCESSA dados  | AWS ENTREGA dados |
| Precisa de consumer  | Não precisa       |
| Real-time            | Near real-time    |
| Armazena dados       | Não armazena      |
| Replay possível      | ❌ Não tem replay  |

---

💡 **Resumo de ouro:**

* **KDS = você controla**
* **Firehose = AWS faz tudo**

---

## 3️⃣ Kinesis Data Streams 🌊

### Características:

* Real-time
* Usa **shards**
* Retention até **365 dias**
* Permite **reprocessar (replay)**

---

### Você precisa implementar:

* Producer
* Consumer
* Processamento

---

💡 Use quando:

* Precisa de lógica customizada
* Precisa replay
* Processamento em tempo real

---

## 4️⃣ Firehose 🔥

### Características:

* Fully managed ✅
* Auto scaling ✅
* Entrega para:

  * S3
  * Redshift
  * OpenSearch
  * HTTP endpoint

---

### NÃO precisa:

* Consumer
* Gerenciar shard
* Escalar

---

💡 Use quando:

* Só quer **entregar dados**
* ETL simples
* Logs → S3

---

## 5️⃣ Fluxo mental 🧠

### Kinesis Data Streams:

```id="kds-flow"
App → Kinesis → Consumer (Lambda/EC2)
```

---

### Firehose:

```id="firehose-flow"
App → Firehose → S3 / Redshift / etc
```

---

## 6️⃣ Replay (🔥 MUITO COBRADO)

| Serviço              | Replay |
| -------------------- | ------ |
| Kinesis Data Streams | ✅      |
| Firehose             | ❌      |

---

💡 Pegadinha clássica:

> “Precisa reprocessar dados”

👉 Resposta:

* **Kinesis Data Streams**

---

## 7️⃣ Latência ⏱️

| Serviço  | Latência                |
| -------- | ----------------------- |
| Kinesis  | Real-time               |
| Firehose | Near real-time (buffer) |

---

💡 Firehose usa buffer:

* Tempo ou tamanho

---

## 8️⃣ Escalabilidade 📈

| Serviço  | Escala          |
| -------- | --------------- |
| Kinesis  | Manual (shards) |
| Firehose | Automático      |

---

💡 Pegadinha:

* “Não quer gerenciar capacidade” → Firehose

---

## 9️⃣ Armazenamento 🗂️

| Serviço  | Armazena |
| -------- | -------- |
| Kinesis  | ✅        |
| Firehose | ❌        |

---

💡 Firehose = só entrega

---

## 🔟 Casos de uso 🎯

### Kinesis:

* Analytics real-time
* Processamento customizado
* Machine learning streaming

---

### Firehose:

* Logs → S3
* ETL simples
* Data lake ingestion

---

## 🔥 Pegadinhas de prova

### ❗ 1. Firehose NÃO permite replay

---

### ❗ 2. Kinesis precisa de consumer

---

### ❗ 3. Firehose NÃO armazena dados

---

### ❗ 4. Firehose é quase sempre resposta quando:

* “Menor esforço operacional”
* “Fully managed”
* “Enviar para S3/Redshift”

---

### ❗ 5. Kinesis quando:

* “Precisa processar”
* “Precisa replay”
* “Real-time estrito”

---

## 🧠 Mnemonics

* **Kinesis = controle total**
* **Firehose = entrega automática**
* **Replay? → Kinesis**
* **Zero esforço? → Firehose**

---

## 🧪 Resumo final (PROVA)

| Cenário             | Escolha  |
| ------------------- | -------- |
| Processar streaming | Kinesis  |
| Enviar para S3      | Firehose |
| Replay necessário   | Kinesis  |
| Sem gerenciamento   | Firehose |
| Tempo real absoluto | Kinesis  |

---

# ➕ 1️⃣7️⃣ Kinesis Data Streams + Firehose juntos 🤝

## 1️⃣ Pode usar os dois?

👉 **SIM, e é muito comum**

Você usa:

* 🌊 **Amazon Kinesis Data Streams** → processar
* 🔥 **Amazon Kinesis Data Firehose** → entregar

---

## 🧠 Ideia principal

* Kinesis = cérebro 🧠 (processa)
* Firehose = caminhão 🚚 (entrega)

---

## 2️⃣ Arquitetura típica (🔥 CAI NA PROVA)

```id="combo-flow"
Producers → Kinesis Data Streams → Firehose → S3 / Redshift
```

---

## 3️⃣ Quando usar os dois?

👉 Quando você quer:

### ✅ Processar + armazenar

Exemplo:

1. Dados chegam (logs, eventos)
2. Você processa em tempo real (Lambda / analytics)
3. Depois salva no S3

---

## 4️⃣ Cenário real (estilo prova)

> “Aplicação precisa processar eventos em tempo real e armazenar no data lake”

👉 Arquitetura correta:

* Kinesis Data Streams → processamento
* Firehose → entrega no S3

---

## 5️⃣ Por que não usar só Firehose?

Porque Firehose:

* ❌ Não permite lógica complexa
* ❌ Não tem replay
* ❌ Não é totalmente real-time

---

## 6️⃣ Por que não usar só Kinesis?

Porque Kinesis:

* ❌ Você precisa construir entrega
* ❌ Mais complexo
* ❌ Mais código

---

## 7️⃣ Comparação rápida 🧠

| Cenário               | Solução                |
| --------------------- | ---------------------- |
| Só enviar para S3     | Firehose               |
| Processar streaming   | Kinesis                |
| Processar + armazenar | **Kinesis + Firehose** |

---

## 🔥 Pegadinha de prova

### ❗ Cenário híbrido

> “Processar dados E enviar para S3 com baixo esforço”

👉 Melhor resposta:

* **Kinesis Data Streams + Firehose**

---

### ❗ “Menor esforço operacional”

👉 Firehose direto (sem Kinesis)

---

### ❗ “Replay necessário”

👉 Precisa de Kinesis (Firehose não serve)

---

## 🧠 Mnemonic

* **Streams = pensar**
* **Firehose = enviar**
* **Juntos = pipeline completo**

---

## ⚡ Resumo final (PROVA)

* Pode usar juntos ✅
* Streams processa
* Firehose entrega
* Arquitetura comum e recomendada

---
Perfeito — esse aqui é mais “low frequency” na prova, mas quando cai… derruba 😈
Vou te deixar no formato DVA direto 👇

---

# ➕ 1️⃣8️⃣ Amazon Managed Service for Apache Flink 🌊⚡

## 1️⃣ O que é? 🤔

➡️ O **Amazon Managed Service for Apache Flink** é um serviço para:

### 👉 **processar dados em streaming com lógica complexa**

---

## 🧠 Tradução simples

* Kinesis = recebe dados
* Flink = **processa dados em tempo real com inteligência**

---

💡 Pense assim:

* SQS = fila
* Kinesis = stream
* Flink = **cérebro do streaming**

---

## 2️⃣ Como funciona 📊

```id="flink-flow"
Kinesis → Flink → Output (S3 / DB / etc)
```

---

### Entrada:

* Kinesis Data Streams
* Kinesis Firehose

---

### Saída:

* S3
* Redshift
* OpenSearch
* Outros serviços

---

## 3️⃣ O que ele faz? 🧠

* Transformações
* Filtros
* Agregações
* Enriquecimento de dados

---

💡 Exemplo:

* Contar cliques por minuto
* Detectar fraude em tempo real

---

## 4️⃣ Por que usar Flink?

➡️ Quando precisa de:

* Processamento **stateful**
* Cálculos contínuos
* Baixa latência
* Lógica complexa

---

## 5️⃣ Linguagens 👨‍💻

* Java
* SQL (Flink SQL) ✅ (muito cobrado)

---

💡 Pegadinha:

* AWS gosta de citar **SQL streaming**

---

## 6️⃣ Flink vs Kinesis Data Streams 🧠

| Kinesis          | Flink          |
| ---------------- | -------------- |
| Transporta dados | Processa dados |
| Não transforma   | Transforma     |
| Simples          | Avançado       |

---

## 7️⃣ Flink vs Lambda ⚡

| Lambda       | Flink              |
| ------------ | ------------------ |
| Stateless    | Stateful           |
| Simples      | Complexo           |
| Event-driven | Streaming contínuo |

---

💡 **Resumo:**

* Lambda = eventos simples
* Flink = streaming complexo

---

## 8️⃣ Casos de uso 🎯

* Fraud detection
* Analytics em tempo real
* Monitoramento
* IoT

---

## 🔥 Pegadinhas de prova

### ❗ 1. Flink é para processamento avançado

---

### ❗ 2. NÃO é para simples ETL

👉 Use Firehose nesse caso

---

### ❗ 3. Usa Kinesis como fonte

---

### ❗ 4. Suporta SQL streaming

👉 Cai bastante

---

## 🧠 Mnemonics

* **Kinesis = fluxo**
* **Flink = inteligência**
* **Firehose = entrega**

---

## 🧪 Resumo de prova

| Cenário               | Serviço  |
| --------------------- | -------- |
| Processamento simples | Lambda   |
| Streaming avançado    | Flink    |
| Só entrega            | Firehose |
| Streaming básico      | Kinesis  |

---








