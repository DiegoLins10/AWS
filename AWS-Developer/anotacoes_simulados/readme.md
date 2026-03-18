
1 - Uma fila SQS pode receber um numero ilimitado de mensagens

# ⚡ RCU  DynamoDB = conta de 4 em 4 KB

👉 Ele divide o item em **blocos de 4 KB**
---
## 🧠 Como pensar sem arredondar pra mim cima... 
* 1–4 KB → **1 RCU**
* 5–8 KB → **2 RCUs**
* 9–12 KB → **3 RCUs**
---
## 📦 Exemplo
* 6 KB → ocupa:
  * 4 KB (1 bloco)
  * +2 KB (precisa de outro bloco)

👉 Total: **2 blocos = 2 RCUs**

10 leituras fortemente com 6kb de RCU. 

6kb = 2RCU, 8kb
10 * 2 rcu = 20 RCU para 10 leituras

---

## 🔥 Regra final (decora)

> **“Conta de 4 em 4 e sempre arredonda pra cima”**

Perfeito pra prova 👍

