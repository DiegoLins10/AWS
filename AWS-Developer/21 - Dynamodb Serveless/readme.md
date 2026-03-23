

# 📘 DynamoDB — Guia DVA (com comandos)

---

## 1️⃣ Partitioning 🧠

```text
PK define como os dados são distribuídos
```

✔ Alta cardinalidade
✔ Distribuição uniforme

❌ Evitar:

```text
status = "ativo"
data fixa
```

---

## 2️⃣ Conditional Writes ⚠️ (CAI MUITO)

### 🔹 Criar só se NÃO existir

```bash
aws dynamodb put-item \
  --table-name Users \
  --item '{ "id": {"S": "1"} }' \
  --condition-expression "attribute_not_exists(id)"
```

---

### 🔹 Atualizar só se existir

```bash
--condition-expression "attribute_exists(id)"
```

---

## 3️⃣ UpdateItem (atomic + seguro) ⚡

### 🔹 Incremento atômico

```bash
SET contador = contador + :inc
```

---

### 🔹 Adicionar atributo

```bash
SET nome = :nome
```

---

### 🔹 Remover atributo

```bash
REMOVE nome
```

---

## 4️⃣ Optimistic Locking 🔒

👉 Controle de versão

```text
version = 1 → 2 → 3
```

✔ Evita overwrite
✔ Usado com ConditionExpression

---

## 5️⃣ Transactions 🔄

### 🔹 Escrita

```bash
aws dynamodb transact-write-items --transact-items file://items.json
```

✔ ACID
✔ Tudo ou nada

⚠️

```text
Custo = ×2 WCU
```

---

### 🔹 Leitura

```bash
aws dynamodb transact-get-items --transact-items file://items.json
```

⚠️

```text
Custo = ×2 RCU
```

---

## 6️⃣ DAX 🚀

```text
Cache em memória (tipo Redis)
```

✔ Acelera leitura
❌ NÃO melhora escrita

---

## 7️⃣ Streams 🌊

👉 Captura mudanças

```text
INSERT
MODIFY
REMOVE
```

Usado com:

```text
Lambda trigger
```

---

## 8️⃣ TTL ⏳

👉 Expiração automática

```bash
ttl = timestamp (epoch)
```

✔ Remove item depois
✔ NÃO consome WCU

---

## 9️⃣ Query vs Scan 💣

### 🔹 Query (CORRETO)

```bash
aws dynamodb query \
  --table-name Users \
  --key-condition-expression "userId = :id"
```

✔ Rápido
✔ Econômico

---

### 🔹 Scan (EVITAR)

```bash
aws dynamodb scan --table-name Users
```

❌ Lento
❌ Caro
❌ Usa muito RCU

---

## 🔟 Streams + Lambda 🔥

```text
DynamoDB → Stream → Lambda
```

👉 Event-driven architecture

---

## 1️⃣1️⃣ Padrão com S3 ☁️

```text
DynamoDB → metadata
S3 → arquivo grande
```

❌ NÃO armazenar arquivos grandes no DynamoDB

---

## 1️⃣2️⃣ Concorrência ⚔️

| Tipo        | Como                 |
| ----------- | -------------------- |
| Conditional | condition-expression |
| Optimistic  | version              |
| Transaction | ACID                 |

---

## 1️⃣3️⃣ Operações principais 🔧

| Operação   | Comando       |
| ---------- | ------------- |
| PutItem    | `put-item`    |
| UpdateItem | `update-item` |
| GetItem    | `get-item`    |
| Query      | `query`       |
| Scan       | `scan`        |
| DeleteItem | `delete-item` |

---

## 💣 Pegadinhas da prova

* ❌ `Scan` quando deveria ser `Query`
* ❌ Esquecer `ConditionExpression`
* ❌ `PutItem` sobrescreve tudo
* ❌ DAX melhora escrita (NÃO)
* ❌ TTL consome WCU (NÃO)
* ❌ Transaction custa normal (NÃO → ×2)

---

## 🧠 Resumo FINAL (30s antes da prova)

```text
Query > Scan

PutItem = replace
UpdateItem = parcial

ConditionExpression = segurança

DAX = cache leitura
Streams = eventos
TTL = expiração

Transaction = ACID (×2)

GSI = nova busca
LSI = ordenação
```

---

