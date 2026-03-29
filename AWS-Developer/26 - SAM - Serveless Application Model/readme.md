# 🧠 README — AWS SAM (Serverless Application Model)

---

## 1️⃣ O que é o AWS SAM

* Framework para **build, deploy e gerenciamento de aplicações serverless**
* Baseado em **AWS CloudFormation**
* Usa um template simplificado (`template.yaml`)

✅ Foco:

* Lambda
* API Gateway
* DynamoDB
* Event sources

---

## 2️⃣ 🏗️ Estrutura do SAM

```yaml
Resources:
  MinhaLambda:
    Type: AWS::Serverless::Function
    Properties:
      Handler: app.handler
      Runtime: nodejs18.x
      CodeUri: .
```

### 🔥 Tipos principais

* `AWS::Serverless::Function`
* `AWS::Serverless::Api`
* `AWS::Serverless::SimpleTable`

---

## 3️⃣ ⚙️ Fluxo padrão SAM

```bash
sam build → sam deploy
```

### 🧱 Etapas:

1. `sam build`

   * Compila código
   * Resolve dependências
   * Gera `.aws-sam`

2. `sam deploy`

   * Cria/atualiza stack no CloudFormation

---

## 4️⃣ 🚀 Comandos principais (CAI NA PROVA)

### 🔹 Inicializar projeto

```bash
sam init
```

---

### 🔹 Build

```bash
sam build
```

---

### 🔹 Deploy (guiado)

```bash
sam deploy --guided
```

👉 Cria:

* Stack
* Bucket S3 (artefatos)
* Parâmetros salvos (`samconfig.toml`)

---

### 🔹 Deploy direto

```bash
sam deploy
```

---

## 5️⃣ ⚡ SAM Accelerate (🔥 MUITO IMPORTANTE)

👉 Comando chave:

```bash
sam sync --code
```

### 🧠 O que é?

* Atualiza **somente o código**
* **SEM redeploy completo**
* Muito mais rápido que `sam deploy`

---

### 🆚 Comparação

| Comando           | O que faz      |
| ----------------- | -------------- |
| `sam deploy`      | Infra + código |
| `sam sync`        | Incremental    |
| `sam sync --code` | 🔥 Só código   |

---

### 🔥 Exemplo:

```bash
sam sync --code
```

👉 Atualiza:

* Lambda code direto
* Sem passar pelo CloudFormation completo

---

## 6️⃣ 🧪 Testes locais

### Rodar Lambda local

```bash
sam local invoke
```

---

### Rodar API local

```bash
sam local start-api
```

👉 Simula:

* API Gateway
* Lambda

---

## 7️⃣ 📦 Packaging (importante pra prova)

SAM usa:

* S3 para armazenar artefatos
* CloudFormation para deploy

Fluxo interno:

```id="1w2"
Code → zip → upload S3 → deploy stack
```

---

## 8️⃣ 🔐 Integrações comuns

SAM suporta eventos:

* API Gateway
* S3
* DynamoDB Streams
* EventBridge
* SNS / SQS

---

## 9️⃣ 🧠 SAM vs Terraform vs Serverless Framework

| Feature       | SAM            | Terraform   |
| ------------- | -------------- | ----------- |
| Base          | CloudFormation | Próprio     |
| Foco          | Serverless     | Infra geral |
| Deploy rápido | ✅ (`sam sync`) | ❌           |
| Drift control | CloudFormation | State       |

---

## 🔟 ⚠️ Pegadinhas de prova

### ❗ 1. SAM usa o quê por baixo?

👉 **CloudFormation**

---

### ❗ 2. Comando mais rápido para atualizar código?

👉 `sam sync --code`

---

### ❗ 3. Precisa de S3?

👉 ✅ Sim (artefatos)

---

### ❗ 4. SAM é só para Lambda?

👉 ❌ Não (API, eventos, etc)

---

### ❗ 5. `sam deploy` vs `sam sync`

* Deploy → completo
* Sync → incremental

---

## 1️⃣1️⃣ 🧠 Dica de ouro (nível prova)

> 🚨 Se a questão falar:

* “deploy rápido”
* “feedback loop rápido”
* “não recriar stack”

👉 Resposta = **SAM Accelerate (`sam sync`)**

---

## 1️⃣2️⃣ 🏁 Resumo final (pra revisar rápido)

* SAM = Serverless + CloudFormation
* `sam build` → prepara
* `sam deploy` → deploy completo
* `sam sync --code` → 🔥 deploy rápido
* Usa S3 + CloudFormation por trás
* Permite testes locais (`sam local`)

---
