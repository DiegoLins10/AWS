# 📘 GSI (Global Secondary Index) — versão “sem enrolação”

## 1️⃣ O problema 🤯

No DynamoDB você só consegue buscar direto pela:

👉 **Primary Key (Partition Key + Sort Key)**

Mas e se quiser buscar por outro campo?

Ex:

```text
Tabela Users:
PK = userId

Mas quero buscar por email 🤡
```

👉 **Não dá direto**

---

## 2️⃣ A solução 🚀

👉 **GSI = um “índice alternativo”**

É tipo criar uma **nova forma de pesquisar a tabela**

---

## 3️⃣ Pensamento simples 🧠

```text
Tabela principal → busca por userId

GSI → busca por email
```

👉 É literalmente isso

---

## 4️⃣ Como funciona 🔧

Você cria um GSI com:

* Nova Partition Key (ex: email)
* (Opcional) Sort Key

A AWS cria uma “cópia indexada” dos dados

---

## 5️⃣ Exemplo 💡

### Tabela:

```text
PK: userId
```

### GSI:

```text
PK: email
```

Agora você pode:

* Buscar por userId ✅
* Buscar por email ✅

---

## 6️⃣ Características importantes ⚠️

* ✔ **Eventually consistent (por padrão)**
* ✔ Tem **RCU/WCU próprios**
* ✔ Pode ter **outra PK diferente da tabela**
* ✔ Pode ter **Sort Key diferente**
* ✔ Funciona com `Query` (não precisa Scan)

---

## 7️⃣ Diferença chave vs GSI 💣

| Tipo   | Pode mudar chave? | Uso                  |
| ------ | ----------------- | -------------------- |
| Tabela | ❌ Não             | Principal            |
| GSI    | ✅ Sim             | Consulta alternativa |

---

## 8️⃣ Pegadinha de prova ⚠️

Se a questão disser:

> “Preciso buscar por um atributo que NÃO é chave”

👉 Resposta quase sempre:

```text
Criar um GSI
```

---

## 9️⃣ Quando usar 🧠

* Buscar por **email**
* Buscar por **status**
* Buscar por **data**
* Qualquer coisa que **não seja PK**

---

## 🧠 Resumo nível prova

```text
GSI = nova forma de buscar dados

Permite:
→ Outra Partition Key
→ Outra Sort Key

Usado quando:
→ Query não funciona com chave atual
```

---
