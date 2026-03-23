# 📘 DynamoDB — Cálculo de RCU & WCU

---

## 1️⃣ Regras base 📏

### 🔹 Leitura (RCU)

* **1 RCU = 1 leitura fortemente consistente de até 4 KB / segundo**
* **Eventually consistent** → usa **½ RCU**
* **Transactional read** → usa **2x RCU**
* Leitura fortemente consistentente:  16 Itens * (12kb por item/4kb RCU) = 16 * 3  = 48 RCUs

if transacional 48 * 2
if eventualmente consistente 48 / 02
if fortemente consistente 48 RCU

---

### 🔹 Escrita (WCU)

* **1 WCU = 1 escrita de até 1 KB / segundo**
* **Transactional write** → usa **2x WCU**

---

## 2️⃣ Fórmulas 🧠

### 🔹 RCU (Leitura)

```text
RCU = (Tamanho do item em KB / 4) → arredonda pra cima
```

Depois:

```text
× número de leituras por segundo
```

Ajustes:

* Eventual → divide por 2
* Transacional → multiplica por 2

---

### 🔹 WCU (Escrita)

```text
WCU = (Tamanho do item em KB / 1) → arredonda pra cima
```

Depois:

```text
× número de escritas por segundo
```

Ajuste:

* Transacional → multiplica por 2

---

## 3️⃣ Regra MAIS IMPORTANTE da prova ⚠️

👉 **SEMPRE arredonda pra cima**

Ex:

* 4.1 KB → 5 KB
* 2.5 KB → 3 KB

---

## 4️⃣ Exemplos rápidos 🚀

### 🔹 Exemplo 1 — RCU (Strong)

* Item: 12 KB
* Leituras: 5/s

```text
12 / 4 = 3
3 × 5 = 15 RCU
```

---

### 🔹 Exemplo 2 — RCU (Eventual)

```text
15 / 2 = 7.5 → 8 RCU
```

---

### 🔹 Exemplo 3 — WCU

* Item: 2.5 KB
* Escritas: 4/s

```text
2.5 → 3
3 × 4 = 12 WCU
```

---

### 🔹 Exemplo 4 — WCU (Transacional)

```text
12 × 2 = 24 WCU
```

---

## 5️⃣ Tabela resumo ⚡

| Tipo                | Unidade base | Ajuste |
| ------------------- | ------------ | ------ |
| RCU (Strong)        | 4 KB         | normal |
| RCU (Eventual)      | 4 KB         | ÷2     |
| RCU (Transactional) | 4 KB         | ×2     |
| WCU                 | 1 KB         | normal |
| WCU (Transactional) | 1 KB         | ×2     |

---

## 6️⃣ Pegadinhas de prova 💣

* ❌ Escrever também NÃO divide por 2
* ❌ Consistência eventual NÃO existe pra escrita
* ❌ Esquecem de arredondar
* ❌ Confundem 4 KB (read) com 1 KB (write)
* ❌ Ignoram “por segundo”

---

## 🧠 Resumo final (decora isso)

```text
READ → 4 KB
WRITE → 1 KB

Eventual → /2
Transacional → ×2

SEMPRE arredonda pra cima
```

---

Se quiser, posso te mandar um **flashcard estilo revisão de 30 segundos** pra decorar isso antes da prova 👀
