Aqui vai um **README estilo prova DVA-C02** (bem direto, comparativo e focado no que cai):

---

# 📘 API Gateway – Security (DVA-C02)

## 1️⃣ IAM Authorization

👉 **Quando usar:** acesso interno (users/roles AWS)

* Usa **Signature V4 (SigV4)**
* Autenticação + autorização via IAM
* Pode usar **Resource Policies** (cross-account)

✅ **Use quando:**

* Backend interno AWS
* Comunicação service-to-service

⚠️ **Cai na prova:**

* IAM = **não usa token JWT**
* Precisa **assinar request (SigV4)**

---

## 2️⃣ Lambda Authorizer (Custom Authorizer)

👉 **Quando usar:** tokens externos (OAuth, JWT custom, etc.)

* Executa uma **Lambda**
* Valida token manualmente
* Retorna uma **IAM Policy**
* Pode ser **cached**

💰 Custo: **por invocação da Lambda**

✅ **Use quando:**

* Precisa lógica custom
* Integração com auth externo

⚠️ **Cai na prova:**

* Flexível, mas **mais caro/complexo**
* Pode gerar **latência**
* Cache reduz custo

---

## 3️⃣ Cognito User Pool Authorizer

👉 **Quando usar:** autenticação gerenciada (login de usuário)

* Integra direto com **Cognito**
* Suporte a login social (Google, Facebook, etc.)
* Usa **JWT Token**
* Sem necessidade de Lambda

✅ **Use quando:**

* App com usuários finais (login/signup)
* Quer solução pronta

⚠️ **Cai na prova:**

* API Gateway **só valida o token**
* Autorização fina → backend

---

# 🔥 Comparação Rápida (MUUUUITO COBRADA)

| Feature       | IAM          | Lambda Authorizer | Cognito           |
| ------------- | ------------ | ----------------- | ----------------- |
| Tipo          | AWS internal | Custom            | User login        |
| Token         | ❌            | ✅                 | ✅ (JWT)           |
| Complexidade  | Baixa        | Alta              | Média             |
| Custo         | Baixo        | 💰 Lambda         | Baixo             |
| Flexibilidade | Baixa        | 🔥 Alta           | Média             |
| Melhor uso    | Serviços AWS | Auth externo      | Apps com usuários |

---

# 🧠 Dicas de Prova

* 🔐 **IAM → interno AWS**
* 🧩 **Lambda Authorizer → custom logic**
* 👤 **Cognito → usuários + login**

---

# ⚠️ Pegadinhas clássicas

* ❌ IAM **não usa JWT**
* ❌ Cognito **não faz autorização complexa sozinho**
* ❌ Lambda Authorizer **aumenta latência**
* ✅ Cache do Authorizer → **melhora performance**

---

# 🚀 Extras que podem cair

## API Keys + Usage Plans

* Controle de **throttling + quota**
* ❌ **NÃO é segurança**
* Apenas controle de uso

---

## CORS

* Necessário para frontend (browser)
* Headers:

  * `Access-Control-Allow-Origin`
  * `Methods`
  * `Headers`

---

## Monitoring

* **CloudWatch Logs**
* **X-Ray (tracing)**

---

## Caching

* Cache no API Gateway
* Reduz chamadas backend
* TTL configurável

---

# 🧩 Resumo final (pra decorar rápido)

👉 **IAM = AWS interno**
👉 **Lambda Authorizer = lógica custom**
👉 **Cognito = usuários + JWT**

---

Se quiser, te mando **5 questões estilo prova DVA só disso aqui** (esse tema cai MUITO).
