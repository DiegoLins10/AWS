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

# 🧠 README — AWS SAM (Parte 2)

---

## 1️⃣ 🔐 SAM Policy Templates

### 🧠 O que é?

* Templates prontos de permissões IAM no SAM
* Evita escrever policies complexas manualmente

---

### 🔥 Exemplo

```yaml
Policies:
  - S3ReadPolicy:
      BucketName: meu-bucket
```

---

### ✅ Vantagens

* Simples
* Rápido
* Menos erro

---

### ⚠️ Pegadinha de prova

> ❗ Policy Templates ≠ IAM Roles completas
> 👉 São **atalhos**, não substituem tudo

---

### 🧾 Exemplos comuns (CAI)

* `S3ReadPolicy`
* `DynamoDBCrudPolicy`
* `SQSPollerPolicy`

---

## 2️⃣ 🚀 SAM + CodeDeploy

### 🧠 O que é?

Integração do SAM com **AWS CodeDeploy** para deploy seguro

---

### 🔥 Objetivo

* Evitar downtime
* Fazer deploy gradual

---

### 📊 Tipos de deploy

| Tipo      | Descrição              |
| --------- | ---------------------- |
| AllAtOnce | Tudo de uma vez        |
| Canary    | Parte → espera → resto |
| Linear    | Incremental            |

---

### 🔥 Exemplo

```yaml
DeploymentPreference:
  Type: Canary10Percent5Minutes
```

---

### 🧠 Como funciona?

* Cria versões da Lambda
* Usa alias
* Direciona tráfego gradualmente

---

### ⚠️ Pegadinhas de prova

* ❗ Precisa de **versions + alias**
* ❗ Usa CodeDeploy por baixo
* ❗ Permite rollback automático

---

## 3️⃣ 🧪 SAM Local Capabilities

### 🧠 O que é?

Executar e testar localmente com Docker

---

### 🔥 Comandos

```bash
sam local invoke
```

```bash
sam local start-api
```

```bash
sam local start-lambda
```

---

### 🧠 O que simula?

* Lambda runtime
* API Gateway

---

### ⚠️ Limitações (CAI)

* ❗ Não simula 100% AWS
* ❗ IAM real não é aplicado
* ❗ Latência pode ser diferente

---

### 🧠 Quando usar?

* Desenvolvimento rápido
* Teste antes do deploy

---

## 4️⃣ 🌍 SAM — Multiple Environments

### 🧠 Problema

Ter:

* dev
* staging
* prod

---

### ✅ Solução SAM

Usar:

* Parâmetros
* `samconfig.toml`

---

### 🔥 Exemplo de parâmetros

```yaml
Parameters:
  Environment:
    Type: String
```

---

### 🔥 Deploy por ambiente

```bash
sam deploy --config-env dev
sam deploy --config-env prod
```

---

### 🧠 `samconfig.toml`

Define configs por ambiente:

```toml
[dev.deploy.parameters]
stack_name = "app-dev"

[prod.deploy.parameters]
stack_name = "app-prod"
```

---

### ⚠️ Pegadinhas de prova

* ❗ SAM suporta multi-env nativamente
* ❗ Usa `samconfig.toml`
* ❗ Não precisa duplicar template

---

## 🧠 RESUMO FINAL (RETA FINAL PROVA)

### 🔐 Policy Templates

* Atalhos de IAM
* Simples e rápidos

---

### 🚀 CodeDeploy

* Deploy seguro (Canary / Linear)
* Usa alias + version
* Rollback automático

---

### 🧪 Local

* `sam local`
* Teste com Docker
* Não 100% igual AWS

---

### 🌍 Multi-env

* `samconfig.toml`
* `--config-env`
* Um template, vários ambientes

---

## 🧠 DICA DE PROVA (IMPORTANTE)

Se a questão disser:

* “deploy gradual Lambda”
  👉 **CodeDeploy + SAM**

---

* “testar localmente Lambda/API”
  👉 **sam local**

---

* “gerenciar ambientes”
  👉 **samconfig.toml**

---


