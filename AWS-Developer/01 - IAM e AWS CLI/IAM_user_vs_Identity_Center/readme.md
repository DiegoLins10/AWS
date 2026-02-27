# 📘 README — IAM User vs IAM Role vs Identity Center

---

# 1️⃣ 🔐 AWS Identity and Access Management — IAM User

## 📌 O que é?

Usuário criado **dentro de uma conta AWS**.

## 👤 Usado para:

* Acesso humano simples
* Scripts externos
* Integrações que exigem Access Key

## 🔑 Credenciais:

* Password (console)
* Access Key (permanente)

## ⚠️ Problema:

* Chave fixa
* Pode vazar
* Rotação manual
* Não escala bem em multi-conta

## 🎯 Mentalidade de prova:

Se falar **"criar access key manual"** → IAM User

---

# 2️⃣ 🎭 IAM Role

## 📌 O que é?

Uma identidade **assumível**, não tem usuário fixo.

## 👤 Usado para:

* EC2 acessar S3
* Lambda acessar DynamoDB
* Cross-account access
* STS temporary credentials

## 🔑 Credenciais:

* Sempre temporárias
* Geradas pelo STS
* Não existe Access Key permanente

## 🧠 Regra importante:

Role **não tem login nem senha**

## 🎯 Mentalidade de prova:

Se falar **"serviço acessando outro serviço"** → Role

---

# 3️⃣ 🏢 AWS IAM Identity Center (antigo AWS SSO)

## 📌 O que é?

Sistema de login centralizado para humanos.

## 👤 Usado para:

* Empresas
* Muitas contas AWS
* Governança corporativa
* Login via SSO

## 🔑 Credenciais:

* Temporárias
* Baseadas em Role
* Expiram automaticamente
* Não cria IAM User

## 🏗 Por trás funciona assim:

```
Usuário corporativo
      ↓
Permission Set
      ↓
Role criada na conta
      ↓
STS gera credencial temporária
```

## 🎯 Mentalidade de prova:

Se falar:

* Multi-conta
* Acesso corporativo
* Evitar credenciais permanentes

→ Identity Center

---

# 🔥 Comparação Direta

| Característica           | IAM User | IAM Role         | Identity Center |
| ------------------------ | -------- | ---------------- | --------------- |
| Usuário fixo             | ✅        | ❌                | ❌               |
| Access Key permanente    | ✅        | ❌                | ❌               |
| Credenciais temporárias  | Opcional | ✅                | ✅               |
| Multi-conta nativo       | ❌        | ⚠️ (manual)      | ✅               |
| Recomendado para empresa | ❌        | Parte da solução | ✅               |

---

# 🧠 Resumo mental definitivo

IAM User = 🔑 Chave fixa
IAM Role = 🎭 Permissão assumida
Identity Center = 🏢 Login corporativo moderno

---

# 💥 Regra de Ouro AWS (moderna)

* 👤 Humano em empresa → Identity Center
* 🤖 Serviço AWS → Role
* 🔧 Script externo simples → IAM User (com cuidado)

---

# 🎯 Frase para nunca mais confundir

> Identity Center usa Roles por trás.
> Roles usam STS.
> STS gera credenciais temporárias.
> Só IAM User gera chave permanente.

---
