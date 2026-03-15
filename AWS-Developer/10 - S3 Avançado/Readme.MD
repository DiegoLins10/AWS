
# 📦 Advanced Amazon S3 – AWS Developer Associate (DVA)

## 1️⃣ S3 Lifecycle Rules

**Lifecycle Rules** permitem **mover ou deletar objetos automaticamente** para reduzir custos ao longo do tempo.

📌 Funcionam por **regras aplicadas ao bucket ou prefixo**.

Tipos de ações:

| Ação                    | Descrição                                 |
| ----------------------- | ----------------------------------------- |
| Transition              | mover objeto para **outra storage class** |
| Expiration              | **deletar objeto automaticamente**        |
| Noncurrent Version      | gerenciar versões antigas                 |
| Abort Incomplete Upload | cancelar uploads multipart incompletos    |

---

## 2️⃣ Lifecycle Transitions (mudança de storage class)

Permite mover objetos entre **classes de armazenamento** automaticamente.

Exemplo:

```
Day 0   → S3 Standard
Day 30  → S3 Standard-IA
Day 90  → S3 Glacier
Day 365 → Delete
```

Fluxo típico:

```
Upload → S3 Standard
        ↓
30 dias → Standard IA
        ↓
90 dias → Glacier
```

📌 Objetivo: **reduzir custo conforme o acesso diminui**.

---

## 3️⃣ Regras importantes para a prova

Algumas **restrições de transição**:

| Origem      | Pode ir para                     |
| ----------- | -------------------------------- |
| Standard    | IA, Intelligent Tiering, Glacier |
| Standard IA | Glacier                          |
| One Zone IA | Glacier                          |

📌 **Glacier classes são para arquivamento**.

---

## 4️⃣ S3 Event Notifications

Permitem que o **S3 envie eventos automaticamente** quando algo acontece no bucket.

Eventos comuns:

* `ObjectCreated`
* `ObjectRemoved`
* `ObjectRestore`
* `Replication`

Exemplo:

```
Upload file → trigger Lambda
```

Arquitetura:

```
S3
 ↓
Event Notification
 ↓
Lambda / SNS / SQS
```

📌 Destinos suportados:

| Destino |
| ------- |
| Lambda  |
| SNS     |
| SQS     |

---

## 5️⃣ S3 Events Filters

Você pode **filtrar eventos** por:

| Filtro | Exemplo   |
| ------ | --------- |
| Prefix | `images/` |
| Suffix | `.jpg`    |

Exemplo:

```
images/*.jpg → trigger Lambda
```

---

## 6️⃣ S3 Event Notifications vs EventBridge

O **S3 também pode enviar eventos para EventBridge**.

| Característica | S3 Events        | EventBridge   |
| -------------- | ---------------- | ------------- |
| Complexidade   | simples          | avançada      |
| Destinos       | Lambda, SNS, SQS | 200+ serviços |
| Filtros        | prefix/suffix    | JSON patterns |
| Uso comum      | trigger simples  | event routing |

📌 Regra para prova:

| Situação                 | Escolha     |
| ------------------------ | ----------- |
| Trigger simples          | S3 Event    |
| Arquitetura event-driven | EventBridge |
| Múltiplos destinos       | EventBridge |

---

## 7️⃣ S3 Performance

O S3 é **altamente escalável automaticamente**.

Performance padrão:

| Operação             | Limite por prefix |
| -------------------- | ----------------- |
| PUT/COPY/POST/DELETE | 3.500 req/s       |
| GET/HEAD             | 5.500 req/s       |

📌 Se precisar de mais performance:

➡ use **múltiplos prefixes**

Exemplo:

```
bucket/images/1/
bucket/images/2/
bucket/images/3/
```

---

## 8️⃣ Multipart Upload

Usado para **arquivos grandes**.

Recomendado quando:

* arquivos **> 100 MB**
* obrigatório quando **> 5 GB**

Fluxo:

```
Upload file
 ↓
Divide em partes
 ↓
Upload paralelo
 ↓
S3 monta o objeto final
```

📌 Benefícios:

* upload paralelo
* melhor performance
* retry de partes individuais

---

## 9️⃣ S3 Transfer Acceleration

Acelera uploads usando a **rede global da AWS (CloudFront Edge Locations)**.

Fluxo:

```
User
 ↓
Nearest Edge Location
 ↓
AWS Backbone Network
 ↓
S3 Bucket
```

📌 Ideal para:

* uploads **de longa distância**
* usuários globais

---

## 🔟 S3 Object Tags

Tags são **pares chave-valor associados a objetos**.

Exemplo:

```
Environment = Production
Project = Payments
```

Usos comuns:

* **Lifecycle rules**
* **Cost allocation**
* **segurança**
* **analytics**

Limite:

* até **10 tags por objeto**

---

## 1️⃣1️⃣ S3 Object Metadata

Metadata são **informações sobre o objeto**.

Tipos:

| Tipo            | Exemplo             |
| --------------- | ------------------- |
| System Metadata | size, last modified |
| User Metadata   | `x-amz-meta-author` |

Exemplo:

```
x-amz-meta-author: Diego
x-amz-meta-project: aws-study
```

📌 Metadata são armazenadas **junto com o objeto**.

---

# 🧠 Resumo para prova

| Feature               | Uso                        |
| --------------------- | -------------------------- |
| Lifecycle             | reduzir custo automático   |
| Event Notifications   | trigger Lambda/SQS/SNS     |
| EventBridge           | arquitetura event-driven   |
| Multipart Upload      | upload de arquivos grandes |
| Transfer Acceleration | upload global mais rápido  |
| Object Tags           | organização e billing      |
| Metadata              | informações do objeto      |

---

✅ **Dica de prova (muito comum)**

| Cenário                               | Resposta              |
| ------------------------------------- | --------------------- |
| processar arquivo após upload         | S3 Event Notification |
| mover dados para armazenamento barato | Lifecycle             |
| upload global lento                   | Transfer Acceleration |
| arquivo muito grande                  | Multipart Upload      |

---
