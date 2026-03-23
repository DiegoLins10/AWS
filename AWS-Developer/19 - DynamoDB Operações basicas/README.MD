Perfeito — esse é **um dos tópicos que MAIS confunde na DVA** (principalmente `PutItem` vs `UpdateItem` vs `Query` vs `Scan`) 👀

Vou deixar no formato **README direto pra prova**:

---

# 📘 DynamoDB — Operações Básicas (DVA)

---

## 1️⃣ Escrita de itens ✍️

### 🔹 `PutItem`

👉 **Cria OU substitui um item inteiro**

* Se **não existe** → cria
* Se **já existe** → **sobrescreve tudo**

⚠️ **Perigo de prova:**

* Pode apagar atributos sem querer

🧠 **Resumo:**

```text
PutItem = INSERT ou REPLACE (tudo)
```

---

### 🔹 `UpdateItem`

👉 **Atualiza atributos específicos**

* Pode:

  * Adicionar atributo
  * Alterar valor
  * Remover atributo

* NÃO substitui o item inteiro

🧠 **Resumo:**

```text
UpdateItem = UPDATE parcial
```

---

### 🔹 `DeleteItem`

👉 **Remove um item**

* Baseado na **Primary Key**

🧠

```text
DeleteItem = DELETE
```

---

## 2️⃣ Leitura de itens 🔍

### 🔹 `GetItem`

👉 Busca **1 item específico**

* Precisa da:

  * Partition Key
  * (+ Sort Key se existir)

✔️ Muito eficiente

🧠

```text
GetItem = busca direta (1 item)
```

---

### 🔹 `BatchGetItem`

👉 Busca **vários itens específicos**

* Até **100 itens por vez**
* Baseado em keys

🧠

```text
BatchGetItem = vários GetItem
```

---

## 3️⃣ Query vs Scan ⚔️ (MAIS IMPORTANTE)

---

### 🔹 `Query` ✅ (USE SEMPRE QUE POSSÍVEL)

👉 Busca usando **Partition Key**

* Pode usar:

  * Sort Key (opcional)
  * Filtros

✔️ Rápido
✔️ Econômico

🧠

```text
Query = busca inteligente (por chave)
```

---

### 🔹 `Scan` ❌ (EVITAR)

👉 Varre a tabela inteira

* Lê TODOS os dados
* Depois filtra

❌ Lento
❌ Caro
❌ Usa MUITO RCU

🧠

```text
Scan = FULL TABLE SCAN (ruim)
```

---

## 4️⃣ Filtros e condições 🧠

### 🔹 FilterExpression

* Aplicado **DEPOIS** da leitura
* Ainda consome RCU

⚠️ Pegadinha:

```text
Filter NÃO economiza RCU
```

---

### 🔹 KeyConditionExpression

* Usado no `Query`
* Filtra pela chave

✔️ Econômico

---

## 5️⃣ Operações condicionais ⚠️

👉 Evita sobrescrever dados sem querer

Exemplo:

* Só escreve se **não existir**

🧠

```text
ConditionExpression
```

💣 Cai MUITO na prova:

* Evitar overwrite acidental

---

## 6️⃣ Operações em lote 📦

### 🔹 `BatchWriteItem`

* Put + Delete em lote
* Até **25 itens**

⚠️ Não suporta update

---

## 7️⃣ Operações transacionais 🔒

### 🔹 `TransactWriteItems`

* Várias operações ACID
* Tudo ou nada

👉 Custa **2x WCU**

---

### 🔹 `TransactGetItems`

* Leitura consistente

👉 Custa **2x RCU**

---

## 8️⃣ Tabela resumo ⚡

| Operação       | O que faz        | Pegadinha      |
| -------------- | ---------------- | -------------- |
| PutItem        | Cria/substitui   | Apaga tudo     |
| UpdateItem     | Atualiza parcial | Mais seguro    |
| GetItem        | 1 item           | Precisa da key |
| BatchGetItem   | Vários itens     | Até 100        |
| Query          | Por chave        | Rápido         |
| Scan           | Tudo             | Lento/caro     |
| DeleteItem     | Remove item      | —              |
| BatchWriteItem | Lote             | Sem update     |
| TransactWrite  | ACID             | 2x custo       |

---

## 9️⃣ Pegadinhas de prova 💣

* ❌ `Scan` quando deveria ser `Query`
* ❌ `PutItem` sobrescrevendo dados
* ❌ `FilterExpression` achando que economiza RCU
* ❌ Esquecer que `BatchWrite` não faz update
* ❌ Não usar `ConditionExpression`

---

## 🧠 Resumo FINAL (decora isso)

```text
PutItem = replace
UpdateItem = update parcial

GetItem = 1 item
Query = por chave (bom)
Scan = tudo (ruim)

Filter ≠ economiza RCU

Transacional = ×2 custo
```

---

