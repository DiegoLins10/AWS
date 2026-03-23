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


# 📘 DynamoDB — LSI (Local Secondary Index)

---

## 1️⃣ Ideia principal 🧠

```text
LSI = outro jeito de ordenar os dados
DENTRO da mesma Partition Key
```

👉 Tradução simples:

* Você **NÃO muda quem você está buscando**
* Você **só muda como os resultados são organizados**

---

👉 Ou seja:

 - Você ainda depende da Partition Key
 - Mas ganha outra Sort Key

## 2️⃣ Explicando “pra mula” 🐴

Imagina:

```text
userId = 123
```

👉 Esse é seu “grupo”

Agora você quer ver os dados desse usuário:

* Por data 📅
* Por score 🏆
* Por preço 💰

👉 O usuário é o mesmo
👉 Só muda a **ordem**

---

## 3️⃣ Sem LSI vs Com LSI 💡

### 🔹 Sem LSI

```text
PK: userId
SK: createdAt
```

👉 Só consegue:

* Buscar usuário
* Ordenar por data

---

### 🔹 Com LSI

```text
PK: userId (mesmo)
SK: score (novo)
```

👉 Agora consegue:

* Buscar usuário
* Ordenar por score

---

## 4️⃣ Regra de ouro ⚠️

```text
LSI NÃO muda a Partition Key
```

👉 Você ainda precisa dela sempre

---

## 5️⃣ Diferença pra GSI (ESSENCIAL) 💣

```text
LSI = ORDER BY
GSI = WHERE
```

| Tipo | O que muda      |
| ---- | --------------- |
| LSI  | Ordenação       |
| GSI  | Forma de buscar |

---

## 6️⃣ Limitações importantes 🚨

* ❌ Só pode criar **na criação da tabela**
* ❌ Não pode adicionar depois
* ❌ Máximo de **5 LSIs**
* ✅ Suporta **strongly consistent read**

---

## 7️⃣ Quando usar 🧠

👉 Quando você:

* Já tem a Partition Key
* Quer **outra forma de ordenar**

---

## 🧠 Resumo FINAL (pra prova)

```text
LSI:
→ mesma Partition Key
→ outra Sort Key
→ outro jeito de ordenar

GSI:
→ nova Partition Key
→ outro jeito de buscar
```

---

Se isso aparecer na prova:

> “preciso mudar a forma de ordenação dentro da mesma chave”

👉 **LSI**

> “preciso buscar por outro atributo”

👉 **GSI**

---

## 📘 Por que usar GSI e não LSI?
# 🧠 Resposta direta (nível prova)
 - GSI → quando você quer mudar COMO buscar
 - LSI → quando você quer mudar COMO ordenar

