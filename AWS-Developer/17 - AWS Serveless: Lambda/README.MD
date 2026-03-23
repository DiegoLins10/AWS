# ⚡ AWS Lambda — Invocations & Integration (DVA-C02)

---

## 1️⃣ Visão Geral 🧠

➡️ AWS Lambda = **compute serverless**

* Executa código sem gerenciar servidor
* Escala automaticamente
* Paga por execução

---

## 2️⃣ Serverless Basics ☁️

➡️ Você NÃO gerencia:

* Servidores
* Scaling
* Infraestrutura

👉 Só envia código

💡 Exemplos serverless:

* Lambda
* DynamoDB
* S3
* Fargate

---

## 3️⃣ Lambda Invocation Types ⚡

## 🔹 Tipos

| Tipo       | Nome            | Comportamento   |
| ---------- | --------------- | --------------- |
| Síncrono   | RequestResponse | Espera resposta |
| Assíncrono | Event           | Fire-and-forget |

---

# 4️⃣ Synchronous Invocation (MUITO COBRADO)

## 📌 Como funciona

➡️ Cliente espera resposta da Lambda

---

## 🔹 Exemplos

* API Gateway
* Application Load Balancer (ALB)

---

## 🔹 Código / CLI

```bash
aws lambda invoke \
  --function-name minha-funcao \
  --invocation-type RequestResponse \
  response.json
```

---

## 🔹 IMPORTANTE (sua dúvida)

👉 Se NÃO definir `InvocationType`:

✅ **Default = RequestResponse (SÍNCRONO)**

---

## 🔹 Características

* Retorna resultado imediatamente
* Sem retry automático
* Cliente lida com erro

---

# 5️⃣ Lambda + Application Load Balancer ⚖️

➡️ ALB pode invocar Lambda

### 🔹 Características

* Sempre **síncrono**
* Suporta HTTP (como API Gateway)
* Pode retornar HTML/JSON

💡 Uso:

* Web apps simples
* Microservices

---

# 6️⃣ Asynchronous Invocation ⚡

## 📌 Como funciona

➡️ Lambda recebe evento e processa em background

👉 Cliente NÃO espera resposta

---

## 🔹 Como invocar

```bash
aws lambda invoke \
  --function-name minha-funcao \
  --invocation-type Event \
  response.json
```

---

## 🔹 SDK

```javascript
InvocationType: "Event"
```

---

## 🔹 Serviços que usam async

* S3
* SNS
* EventBridge
* CloudWatch Events

---

# 7️⃣ Async Behavior (CAI NA PROVA)

## 🔁 Retry automático

* Até **2 tentativas**

---

## ☠️ DLQ (Dead Letter Queue)

➡️ Se falhar:

Pode enviar para:

* SQS
* SNS

---

## 🎯 Destinations (mais moderno)

➡️ Define:

* On Success
* On Failure

---

# 8️⃣ Synchronous vs Asynchronous ⚔️

| Feature          | Síncrono | Assíncrono |
| ---------------- | -------- | ---------- |
| Espera resposta  | ✅        | ❌          |
| Retry automático | ❌        | ✅          |
| DLQ              | ❌        | ✅          |
| Uso comum        | API      | Eventos    |

---

# 🚨 Pegadinhas de prova

## ❗ Default Invocation

👉 Não definiu → **SÍNCRONO**

---

## ❗ API Gateway

👉 Sempre **síncrono**

---

## ❗ S3 / SNS / EventBridge

👉 Sempre **assíncrono**

---

## ❗ “Processamento em background”

👉 Assíncrono

---

## ❗ “Resposta imediata ao usuário”

👉 Síncrono

---

# 🧠 Regra de ouro

👉 RequestResponse → síncrono
👉 Event → assíncrono

---

# 🔥 Cenários clássicos (DVA)

## 📌 Upload de arquivo no S3

👉 S3 → Lambda → async

---

## 📌 API REST

👉 API Gateway → Lambda → sync

---

## 📌 Processamento pesado

👉 EventBridge/SQS → Lambda → async

---

# 🎯 Resumo final

👉 Default = síncrono
👉 Async precisa explícito (`Event`)
👉 Async = retry + DLQ
👉 Sync = resposta imediata

---

# ⚡ Continuação — AWS Lambda (Eventos, Async, ALB, Streams)

---

# 9️⃣ Lambda Asynchronous Invocations & DLQ ⚡

## 📌 Conceito

➡️ Execução em background (**não espera resposta**)

---

## 🔹 Características

* InvocationType = `Event`
* Retry automático (**até 2 vezes**)
* Pode configurar destino de falha

---

## ☠️ DLQ (Dead Letter Queue)

➡️ Para eventos que falharam

### 🔹 Suporta:

* SQS
* SNS

---

## 🎯 Destinations (mais moderno)

| Tipo       | Uso          |
| ---------- | ------------ |
| On Success | Após sucesso |
| On Failure | Após falha   |

---

## 🚨 Pegadinha

👉 Async tem retry automático
👉 Sync NÃO tem

---

# 🔟 Lambda + EventBridge ⚡

## 📌 O que é

➡️ EventBridge = **event bus (event-driven)**

---

## 🔹 Fluxo

```id="0x6m7o"
Evento → Rule → Lambda
```

---

## 🔹 Exemplos

* EC2 mudou estado
* CloudTrail detectou ação
* Scheduler (cron)

---

## 🧠 Características

* Invocação **assíncrona**
* Desacoplado
* Filtragem por regra

---

## 🚨 Pegadinha

👉 EventBridge = async SEMPRE

---

# 1️⃣1️⃣ Lambda + S3 Event Notifications 📦

## 📌 O que é

➡️ S3 dispara Lambda automaticamente

---

## 🔹 Eventos comuns

* ObjectCreated
* ObjectRemoved

---

## 🔹 Fluxo

```id="z6x4g7"
Upload no S3 → Evento → Lambda
```

---

## 🧠 Características

* Invocação **assíncrona**
* Muito usado pra:

  * Processar arquivos
  * Imagens
  * ETL

---

## 🚨 Pegadinha

👉 S3 → Lambda = async

---

# 1️⃣2️⃣ Lambda + ALB ⚖️

## 📌 O que é

➡️ ALB pode chamar Lambda como target

---

## 🔹 Características

* Invocação **síncrona**
* HTTP request/response
* Similar ao API Gateway

---

## 🧠 Quando usar

* Web apps simples
* Microservices HTTP

---

## 🚨 Pegadinha

👉 ALB = síncrono
👉 API Gateway = síncrono

---

# 1️⃣3️⃣ Shards, Batching & Lambda (🔥 MUITO IMPORTANTE)

## 📌 Onde aparece

* Kinesis Data Streams
* DynamoDB Streams

---

## 🧩 Shard (fragmento)

➡️ Partição de dados do stream

```id="z6bptu"
Stream
 ├── Shard 1
 ├── Shard 2
 └── Shard 3
```

---

## ⚡ Regra principal

👉 **1 shard → 1 execução concorrente de Lambda (default)**

---

## 📦 Batching (o que o diagrama mostrou)

➡️ Eventos são agrupados em **batches**

```id="kk1r1b"
Eventos → Batch → Lambda execução
```

---

## 🔹 Importante

👉 1 batch = 1 execução de Lambda

👉 Um shard pode gerar **vários batches**

---

## 🔍 Fluxo real

```id="7o7hl2"
Shard → Records → Batches → Lambda execuções
```

---

## ⚠️ Ordem dos dados

| Escopo          | Ordem       |
| --------------- | ----------- |
| Dentro do shard | ✅ Garantida |
| Entre shards    | ❌ Não       |

---

## 🚀 Paralelismo

### 🔹 Default

* 1 shard → 1 execução

### 🔹 Com Parallelization Factor

* Até **10 execuções por shard**

---

## 🚨 Pegadinhas

❗ Shard ≠ Lambda
❗ Lambda NÃO cria shard
❗ Mais shards = mais paralelismo

---

# 🧠 Resumo mental (DECORA)

👉 Shard = divide dados
👉 Batch = agrupa eventos
👉 Lambda = processa batch

---

# 🎯 Cenários de prova

## 📌 Stream de dados em tempo real

👉 Kinesis + Lambda

---

## 📌 Processar uploads

👉 S3 + Lambda

---

## 📌 Arquitetura event-driven

👉 EventBridge + Lambda

---

## 📌 API HTTP

👉 API Gateway / ALB + Lambda

---

# 🔥 Resumo final geral

👉 Sync → RequestResponse (API, ALB)
👉 Async → Event (S3, EventBridge, SNS)

👉 Shard controla paralelismo
👉 Batch controla execução

---

# 1️⃣4️⃣ Lambda Event Source Mapping 🔗

---

## 📌 O que é

➡️ Configuração que conecta **Lambda a uma fonte de eventos de polling**

👉 A AWS cria um **poller automático**

---

## 🔹 Serviços que usam Event Source Mapping

* SQS
* Kinesis Data Streams
* DynamoDB Streams

---

## 🧠 Diferença IMPORTANTE (CAI NA PROVA)

| Tipo                        | Como funciona        |
| --------------------------- | -------------------- |
| Push (S3, SNS, EventBridge) | Serviço envia evento |
| Polling (ESM)               | Lambda busca evento  |

👉 Event Source Mapping = **polling**

---

# ⚡ 1️⃣5️⃣ Como funciona por baixo dos panos

```id="q3r7n9"
Event Source → Poller → Batch → Lambda
```

---

## 🔹 Componentes

* Poller (AWS gerenciado)
* Batcher
* Invoker (Lambda)

---

# 📦 1️⃣6️⃣ Batching (MUITO IMPORTANTE)

➡️ Eventos são agrupados antes de invocar Lambda

---

## 🔹 Configurações

* Batch size (quantidade de mensagens)
* Batch window (tempo de espera)

---

## 🔹 Regra

👉 **1 batch = 1 execução de Lambda**

---

# ⚔️ 1️⃣7️⃣ Comportamento por serviço

---

## 🟢 SQS

### 🔹 Características

* Pull model
* Sem ordem (Standard queue)
* Com ordem (FIFO)

---

### 🔹 Batch

* Até **10 mensagens por batch**

---

### 🔹 Escala (IMPORTANTE)

👉 Começa com:

* **5 execuções concorrentes**

👉 Pode escalar até:

* **+60 execuções por minuto**

👉 Máximo:

* **1000 execuções concorrentes**

---

### 🔹 Retry

* Mensagem volta pra fila se falhar
* Controlado pelo visibility timeout

---

### 🚨 Pegadinhas

❗ Lambda NÃO remove mensagem manualmente
❗ SQS gerencia retry

---

## 🔵 Kinesis Data Streams

### 🔹 Características

* Baseado em shards
* Ordem garantida por shard

---

### 🔹 Batch

* Até **10.000 registros**
* Máx **6 MB por batch**

---

### 🔹 Escala

👉 **1 shard = 1 execução concorrente**

---

### 🔹 Throughput por shard

* **1 MB/s write**
* **2 MB/s read**
* **1000 records/s**

---

### 🔹 Retry

* Retry até expirar (24h default retention)

---

### 🚨 Pegadinhas

❗ Paralelismo depende de shards
❗ Ordem só dentro do shard

---

## 🟣 DynamoDB Streams

### 🔹 Características

* Similar ao Kinesis
* Trigger baseado em mudanças na tabela

---

### 🔹 Batch

* Até **1000 registros**
* Máx **6 MB**

---

### 🔹 Escala

👉 Igual Kinesis:

* **1 shard = 1 execução**

---

### 🔹 Retry

* Até expirar (24h)

---

---

# 🚀 1️⃣8️⃣ Parallelization Factor

➡️ Aumenta paralelismo por shard

---

## 🔹 Valor

* Até **10**

---

## 🔹 Exemplo

```id="pb2v6j"
1 shard + factor 2 → 2 execuções paralelas
```

---

## 🚨 Pegadinha

👉 Pode quebrar ordem lógica (cuidado)

---

# ⏱️ 1️⃣9️⃣ Tempo e controle

---

## 🔹 Batch Window

➡️ Tempo máximo pra formar batch

* Até **5 minutos**

---

## 🔹 Iterator Age (Kinesis/Dynamo)

➡️ Mede atraso no processamento

💡 Muito cobrado

---

# ⚠️ 2️⃣0️⃣ Erros e Retry

---

## 🔹 SQS

* Retry via visibility timeout
* DLQ configurável

---

## 🔹 Kinesis/Dynamo

* Retry até expirar
* Pode bloquear shard

---

## 🔹 Bisect Batch (🔥 importante)

➡️ Divide batch em caso de erro

---

# ⚔️ 2️⃣1️⃣ Comparação geral

| Feature   | SQS      | Kinesis   | DynamoDB  |
| --------- | -------- | --------- | --------- |
| Tipo      | Queue    | Stream    | Stream    |
| Ordem     | Opcional | Por shard | Por shard |
| Batch max | 10       | 10.000    | 1000      |
| Escala    | Alta     | Shards    | Shards    |

---

# 🚨 Pegadinhas de prova

## ❗ SQS escala automaticamente

👉 Não depende de shard

---

## ❗ Kinesis depende de shard

👉 Quer mais escala → mais shards

---

## ❗ Batch = 1 execução

👉 Sempre

---

## ❗ Polling vs Push

👉 SQS/Kinesis/Dynamo → polling
👉 S3/SNS/EventBridge → push

---

# 🧠 Regra de ouro

👉 Event Source Mapping = polling
👉 Batch = execução
👉 Shard = paralelismo

---

# 🎯 Resumo final (DECORA)

👉 SQS:

* Até 10 mensagens
* Escala até 1000 concorrência

👉 Kinesis:

* 1 shard = 1 Lambda
* 1000 records/s

👉 DynamoDB Streams:

* Igual Kinesis

---


# 2️⃣2️⃣ Lambda Event & Context Objects 📦

## 📌 Event

➡️ Contém os dados de entrada da Lambda

### 🔹 Exemplos

* S3 → info do bucket/objeto
* API Gateway → HTTP request
* SQS → mensagens

---

## 📌 Context

➡️ Metadados da execução

### 🔹 Contém

* `awsRequestId`
* `functionName`
* `remainingTimeInMillis`

---

## 🧠 Uso comum

👉 Timeout handling
👉 Logging
👉 Debug

---

## 🚨 Pegadinha

👉 Event = input
👉 Context = metadata

---

# 2️⃣3️⃣ Lambda Destinations 🎯

## 📌 O que é

➡️ Define o destino após execução async

---

## 🔹 Tipos

| Tipo       | Quando          |
| ---------- | --------------- |
| On Success | Execução OK     |
| On Failure | Execução falhou |

---

## 🔹 Destinos

* Lambda
* SNS
* SQS
* EventBridge

---

## ⚠️ Diferença importante

👉 **DLQ ≠ Destination**

| Feature        | DLQ | Destination |
| -------------- | --- | ----------- |
| Só erro        | ✅   | ❌           |
| Sucesso também | ❌   | ✅           |

---

## 🚨 Pegadinha

👉 Destinations = async only

---

# 2️⃣4️⃣ Lambda Permissions 🔐

## 📌 Dois tipos

---

## 🔹 1. IAM Role (Execution Role)

➡️ O que a Lambda **PODE FAZER**

### 🔹 Exemplo

* Ler S3
* Escrever DynamoDB

---

## 🔹 2. Resource-based Policy

➡️ Quem pode **invocar a Lambda**

### 🔹 Exemplo

* S3 invocar Lambda
* EventBridge invocar

---

## ⚔️ Resumo

| Tipo            | Controle     |
| --------------- | ------------ |
| IAM Role        | Lambda → AWS |
| Resource Policy | AWS → Lambda |

---

## 🚨 Pegadinha

👉 “Permitir S3 chamar Lambda”

❌ IAM Role
✅ Resource-based policy

---

# 2️⃣5️⃣ Lambda Environment Variables 🌱

## 📌 O que é

➡️ Configuração dinâmica da função

---

## 🔹 Usos

* URLs
* API keys
* Config flags

---

## 🔐 Segurança

👉 Pode usar:

* KMS encryption

---

## 🚨 Pegadinha

👉 NÃO guardar secrets sensíveis direto
👉 Use **Secrets Manager / SSM Parameter Store**

---

# 2️⃣6️⃣ Lambda Monitoring & X-Ray 📊

## 📌 CloudWatch

➡️ Logs + métricas

---

## 🔹 Métricas importantes

* Invocations
* Errors
* Duration
* Throttles

---

## 📌 X-Ray

➡️ **Tracing distribuído**

* Latência
* Fluxo
* Gargalos

---

## 🚨 Pegadinha

👉 CloudWatch = métricas/logs
👉 X-Ray = tracing

---

# 2️⃣7️⃣ Lambda@Edge & CloudFront Functions 🌍

## 📌 Lambda@Edge

➡️ Executa código no edge (CloudFront)

---

## 🔹 Características

* Mais pesado
* Pode acessar recursos AWS
* Maior latência que CF Functions

---

## 📌 CloudFront Functions

➡️ Mais leve e rápido

---

## 🔹 Características

* Ultra low latency
* Apenas manipulação HTTP simples
* Sem acesso a rede externa

---

## ⚔️ Comparação

| Feature      | Lambda@Edge     | CF Functions        |
| ------------ | --------------- | ------------------- |
| Complexidade | Alta            | Baixa               |
| Latência     | Média           | Muito baixa         |
| Uso          | Lógica complexa | Headers / redirects |

---

## 🚨 Pegadinha

👉 Precisa lógica complexa → Lambda@Edge
👉 Precisa ultra rápido → CF Functions

---

# 2️⃣8️⃣ Lambda in VPC 🌐

## 📌 O que é

➡️ Lambda dentro de uma VPC

---

## 🔹 Quando usar

* Acessar RDS
* Acessar recursos privados

---

## ⚠️ Problema clássico

👉 Lambda perde acesso à internet

---

## 🔹 Solução

* NAT Gateway (para internet)
* VPC endpoints (melhor opção)

---

## 🧠 Características

* Mais lenta (cold start maior)
* Mais complexa

---

## 🚨 Pegadinhas

❗ Lambda na VPC NÃO tem internet por padrão
❗ Precisa NAT ou endpoint

---

# 🎯 Resumo Final (Última Revisão)

👉 Event = input
👉 Context = metadata

👉 IAM Role = o que Lambda faz
👉 Resource Policy = quem chama Lambda

👉 Destinations = async flow
👉 DLQ = só erro

👉 CloudWatch = logs
👉 X-Ray = tracing

👉 Lambda@Edge vs CF Functions = complexidade vs performance

👉 Lambda VPC = acesso privado (com custo de rede)

---

# ⚡ AWS Lambda — Performance, Layers & Concurrency (DVA-C02)

---

# 1️⃣ Lambda Performance 🚀

## 📌 Fatores que impactam performance

### 🔹 1. Memória (MUITO IMPORTANTE)

➡️ Aumentar memória → aumenta CPU automaticamente

💡 Ex:

* 128 MB → pouca CPU
* 1024 MB → muito mais CPU

---

## 🔹 2. Duration

➡️ Tempo de execução

👉 Custo = **memória × tempo**

---

## 🔹 3. Cold Start ❄️

➡️ Tempo para inicializar Lambda

### 🔹 Impactado por:

* VPC (mais lento)
* Linguagem (Java mais lento)
* Tamanho do código

---

## 🧠 Otimizações

✔️ Aumentar memória
✔️ Reutilizar conexões (fora handler)
✔️ Evitar VPC se não precisar

---

## 🚨 Pegadinha

👉 Mais memória = mais caro?
👉 Nem sempre (pode reduzir duration)

---

# 2️⃣ Lambda Layers 📦

## 📌 O que é

➡️ Forma de **compartilhar código/dependências**

---

## 🔹 Exemplos

* Bibliotecas (numpy, requests)
* SDKs
* Código comum

---

## 🔹 Benefícios

✔️ Reuso
✔️ Deploy menor
✔️ Separação de responsabilidades

---

## 🔹 Limites

* Até **5 layers por função**

---

## 🚨 Pegadinha

👉 Layers NÃO melhoram performance diretamente
👉 Servem para organização/reuso

---

# 3️⃣ Lambda File System Mounting (EFS) 💾

## 📌 O que é

➡️ Lambda pode montar **Amazon EFS**

---

## 🔹 Uso

* Arquivos grandes
* ML models
* Dados compartilhados

---

## 🔹 Características

✔️ Persistente
✔️ Compartilhado entre Lambdas

---

## ⚠️ Importante

👉 Requer Lambda dentro da VPC

---

## 🚨 Pegadinha

👉 EFS ≠ S3
👉 EFS é filesystem, S3 é object storage

---

# 4️⃣ Lambda Concurrency ⚡

## 📌 O que é

➡️ Número de execuções simultâneas

---

## 🔹 Default (MUITO COBRADO)

👉 **1000 por conta por região**

---

## 🔹 Tipos

### 🟢 Unreserved

* Pool compartilhado

---

### 🔵 Reserved Concurrency

➡️ Garante capacidade para função

✔️ Isola
✔️ Evita competição

---

### 🟣 Provisioned Concurrency

➡️ Evita cold start

✔️ Instâncias pré-aquecidas

---

## ⚠️ Regra importante

👉 Sempre **100 unreserved mínimo**

---

## 🚨 Pegadinhas

❗ Throttling = limite atingido
❗ Reserved protege função crítica

---

# 5️⃣ Scaling Behavior 📈

## 🔹 Lambda escala automaticamente

👉 Baseado em eventos

---

## 🔹 Exemplos

* SQS → escala com fila
* Kinesis → baseado em shards
* API Gateway → requisições

---

## 🚨 Pegadinha

👉 Lambda escala rápido, mas não infinito
👉 Limitado por concurrency

---

# 6️⃣ Lambda External Dependencies 📦

## 📌 O que é

➡️ Bibliotecas externas usadas na função

---

## 🔹 Formas de incluir

### 🟢 Diretamente no deployment

* Zip com dependências

---

### 🔵 Lambda Layers

* Reutilizável

---

### 🟣 Container Image

* Até 10 GB

---

## 🔹 Boas práticas

✔️ Reduzir tamanho do pacote
✔️ Evitar dependências desnecessárias
✔️ Usar layers para libs comuns

---

## 🚨 Pegadinha

👉 Pacote grande = cold start maior

---

# ⚔️ Comparação rápida

| Feature   | Uso                 |
| --------- | ------------------- |
| Layers    | Reuso               |
| EFS       | Storage persistente |
| S3        | Storage de objetos  |
| Container | Apps grandes        |

---

# 🧠 Regras de ouro (DVA)

👉 Memória ↑ → CPU ↑
👉 Layers = organização
👉 EFS = arquivos persistentes
👉 Concurrency = limite de escala
👉 Provisioned = evita cold start

---

# 🎯 Cenários de prova

## 📌 App lento

👉 Aumentar memória

---

## 📌 Evitar cold start

👉 Provisioned concurrency

---

## 📌 Compartilhar libs

👉 Layers

---

## 📌 Arquivos grandes

👉 EFS

---

## 📌 Throttling

👉 Ajustar concurrency

---

# 🔥 Resumo final

👉 Performance = memória + cold start
👉 Layers = dependências compartilhadas
👉 EFS = filesystem persistente
👉 Concurrency = escala da Lambda

---




