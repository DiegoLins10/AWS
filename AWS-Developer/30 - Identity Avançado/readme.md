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

Perfeito — essas duas sessões caem SIM na DVA, principalmente **PassRole** (clássico de prova).
Vou montar no estilo README direto pra revisão 👇

---

# 🔐 1️⃣ Granting Permissions to Pass a Role (iam:PassRole)

## 🧠 O que é

👉 Permissão que permite um usuário/serviço **passar uma IAM Role para um serviço AWS**

---

## 🔥 Cenário clássico

* Você cria uma Lambda
* E quer associar uma Role a ela

👉 Para isso, você precisa de:

✔️ Permissão:

```json
"iam:PassRole"
```

---

## 💥 Regra importante

👉 **Criar recurso ≠ poder passar role**

Você precisa de DUAS coisas:

1. Permissão para criar o recurso
2. Permissão para passar a role (`iam:PassRole`)

---

## 📌 Exemplo de prova

👉 Usuário consegue criar Lambda, mas falha ao associar Role

✔️ Motivo:

* Falta `iam:PassRole`

---

## ⚠️ Pegadinhas

❌ “Se pode criar EC2, pode anexar role automaticamente” → ERRADO
✔️ Precisa de `iam:PassRole`

---

❌ “PassRole dá permissão da role” → ERRADO
✔️ Só permite **ASSOCIAR**, não usar diretamente

---

## 🧠 Frase de prova

👉 **“iam:PassRole permite associar uma role a um serviço AWS”**

---

# 🧠 Quando isso aparece na prova

* Lambda execution role
* EC2 instance profile
* ECS task role
* Step Functions

---

# 🏢 2️⃣ AWS Directory Services

## 🧠 O que é

👉 Serviço gerenciado para integrar AWS com diretórios tipo:

* Microsoft AD
* LDAP

---

## 🔥 Tipos principais

---

### 1️⃣ AWS Managed Microsoft AD

👉 AD completo gerenciado pela AWS

✔️ Uso:

* Empresas que já usam AD
* Integração com Windows

---

### 2️⃣ AD Connector

👉 Proxy para seu AD on-premise

✔️ Não armazena dados na AWS
✔️ Só encaminha autenticação

---

### 3️⃣ Simple AD

👉 Versão básica (menos comum na prova)

---

## 🧩 Quando usar (cenários de prova)

| Situação                | Serviço              |
| ----------------------- | -------------------- |
| Quer AD completo na AWS | Managed Microsoft AD |
| Já tem AD on-premise    | AD Connector         |
| Caso simples/teste      | Simple AD            |

---

## 🔥 Casos clássicos

* EC2 Windows domain-joined
* Login corporativo integrado
* Aplicações empresariais

---

## ⚠️ Pegadinhas

❌ “AD Connector armazena usuários” → ERRADO
✔️ Só faz proxy

---

❌ “Simple AD é produção enterprise” → ERRADO
✔️ Limitado

---

## 🧠 Frase de prova

👉 **“AD Connector apenas encaminha autenticação para o AD on-premise”**

---

# 🎯 RESUMÃO FINAL

### 🔐 PassRole

* Necessário para associar roles
* Muito cobrado
* Sempre lembrar: **criar ≠ passar role**

---

### 🏢 Directory Service

* Managed AD → completo
* AD Connector → proxy
* Simple AD → básico

---


