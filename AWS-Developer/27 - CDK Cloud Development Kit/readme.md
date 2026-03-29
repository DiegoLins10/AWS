# 📦 AWS CDK (Cloud Development Kit) — README DVA-C02

## 1️⃣ O que é o CDK

* AWS Cloud Development Kit = ferramenta de **Infrastructure as Code (IaC)** usando linguagens de programação
* Suporta: TypeScript, Python, Java, C#, etc.

👉 Você escreve código → ele gera:

* AWS CloudFormation

---

## 2️⃣ Conceito-chave (CAI NA PROVA)

> CDK **não substitui** CloudFormation
> CDK **USA** CloudFormation por baixo

✅ CDK = abstração
✅ CloudFormation = engine real

---

## 3️⃣ Estrutura do CDK

### 📁 Componentes principais

* **App** → ponto de entrada
* **Stack** → unidade de deploy (vira um stack do CloudFormation)
* **Construct** → blocos reutilizáveis

---

## 4️⃣ Constructs (MUITO COBRADO)

### 🔹 Níveis de Construct

| Nível | Nome       | Descrição                |
| ----- | ---------- | ------------------------ |
| L1    | Low-level  | 1:1 com CloudFormation   |
| L2    | High-level | Abstrações (mais usadas) |
| L3    | Patterns   | Arquiteturas prontas     |

---

### 💡 Exemplo mental

* L1 → `CfnBucket`
* L2 → `Bucket`
* L3 → API + Lambda + Dynamo já integrado

👉 Prova ama perguntar isso

---

## 5️⃣ Comandos principais (DECORAR)

```bash
cdk init      # inicia projeto
cdk synth     # gera CloudFormation
cdk deploy    # faz deploy
cdk diff      # mostra diferenças
cdk destroy   # remove stack
```

---

## 6️⃣ Bootstrapping (CAI)

```bash
cdk bootstrap
```

👉 Cria recursos na conta AWS (S3, roles, etc.)

📌 Necessário antes do primeiro deploy

---

## 7️⃣ Fluxo de execução

1. Escreve código CDK
2. `cdk synth`
3. Gera template do AWS CloudFormation
4. `cdk deploy`
5. AWS cria os recursos

---

## 8️⃣ CDK vs CloudFormation (clássico de prova)

| Característica | CDK    | CloudFormation |
| -------------- | ------ | -------------- |
| Linguagem      | Código | JSON/YAML      |
| Nível          | Alto   | Baixo          |
| Produtividade  | Alta   | Média          |
| Execução       | Usa CF | Nativo         |

---

## 9️⃣ CDK vs SAM (MUUUITO IMPORTANTE)

| Ferramenta | Uso         |
| ---------- | ----------- |
| CDK        | Infra geral |
| AWS SAM    | Serverless  |

👉 SAM é mais simples para Lambda/APIs
👉 CDK é mais flexível

---

## 🔟 Unit Testing (sim, pode cair)

* CDK permite testar infraestrutura
* Ex: verificar se um recurso foi criado

👉 Muito usado com Jest (TS)

---

## 1️⃣1️⃣ Quando usar CDK

✅ Infra complexa
✅ Reuso de código
✅ Times de dev (não só DevOps)

---

## 1️⃣2️⃣ Pegadinhas de prova ⚠️

* ❌ CDK não executa direto na AWS
* ❌ CDK não substitui CloudFormation
* ❌ CDK não é só pra serverless

✔️ Sempre passa pelo CloudFormation

---

## 🧠 Resumo final (pra revisão rápida)

* CDK = IaC com código
* Usa CloudFormation por baixo
* Constructs (L1, L2, L3) caem MUITO
* `cdk deploy`, `cdk synth`, `cdk bootstrap`
* Mais produtivo que CloudFormation

---


