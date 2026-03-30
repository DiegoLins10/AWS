# 🔐 IAM Policy Evaluation + Inline vs Managed (DVA)

---

## 1️⃣ 🧠 Como a AWS decide (REGRA MAIS IMPORTANTE)

👉 Ordem de avaliação:

1. ❌ **Explicit DENY → ganha SEMPRE**
2. ✅ Se tiver ALLOW → permite
3. ❌ Senão → DENY (default)

---

## 🔥 Frase de prova

👉 **“Explicit Deny overrides any Allow”**

---

## 2️⃣ 🧩 IAM Policy + S3 Bucket Policy

👉 A AWS avalia **TUDO junto (UNION)**

✔️ IAM Policy (user/role)
➕ S3 Bucket Policy

👉 Resultado final = combinação das duas

---

### 💥 Regra importante:

* Se QUALQUER uma tiver **DENY → acabou**
* Se tiver ALLOW em alguma → pode permitir

---

## 3️⃣ 🧠 Dynamic Policies (cai bastante)

👉 Problema:

* 1 policy por usuário ❌ (não escala)

👉 Solução:

* Usar variável:

```id="fwe2h3"
${aws:username}
```

---

### 📌 Exemplo mental:

```id="3klf92"
arn:aws:s3:::meu-bucket/home/${aws:username}/*
```

👉 Cada usuário acessa só sua pasta

---

## 4️⃣ 🔐 Inline vs Managed (reforçando com a imagem)

### 🔸 AWS Managed

* Mantida pela Amazon Web Services
* Atualiza automaticamente
* Muito permissiva às vezes ⚠️

---

### 🔸 Customer Managed (🔥 MELHOR PRÁTICA)

* Criada por você
* Reutilizável
* Versionamento + rollback

👉 💥 **Resposta padrão da prova**

---

### 🔸 Inline Policy

* 1:1 com user/role
* Não reutilizável
* Apaga junto com o recurso

👉 ❗ Não escala

---

## 5️⃣ 🧠 Tabela mental rápida

| Tipo             | Quando usar         |
| ---------------- | ------------------- |
| AWS Managed      | Rápido / admin      |
| Customer Managed | ✅ padrão / produção |
| Inline           | Casos específicos   |

---

## 6️⃣ ⚠️ Pegadinhas (CAI MUITO)

❌ “Bucket policy substitui IAM policy” → ERRADO
✔️ Elas são combinadas

---

❌ “Se IAM permite e bucket nega → permite” → ERRADO
✔️ **DENY ganha sempre**

---

❌ “Inline é melhor prática” → ERRADO
✔️ Customer Managed é melhor

---

❌ “Uma policy por usuário é ok” → ERRADO
✔️ Use variável `${aws:username}`

---

## 7️⃣ 🧠 RESUMÃO FINAL (decora isso)

👉 Evaluation:

* DENY > ALLOW > default DENY

👉 Policies:

* IAM + Resource Policy = juntas

👉 Best practice:

* Customer Managed Policy

👉 Escala:

* Use `${aws:username}`

---
