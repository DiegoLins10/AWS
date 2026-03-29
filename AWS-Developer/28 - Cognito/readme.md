# 📘 README — AWS Cognito (DVA-C02)

## 1️⃣ 🔐 Visão Geral do Cognito

O **Amazon Cognito** é usado para **autenticação + autorização de usuários** em aplicações.

👉 Ele tem **DOIS componentes principais**:

* 👤 **User Pools → Autenticação (login)**
* 🔑 **Identity Pools → Autorização (acesso AWS)**

---

## 2️⃣ 👤 Cognito User Pools (Autenticação)

👉 Serve para **gerenciar usuários da aplicação**

### ✅ Funcionalidades:

* Cadastro (Sign up)
* Login (Sign in)
* MFA (Multi-Factor Authentication)
* Reset de senha
* Login social (Google, Facebook, etc.)

### 📌 O que gera:

* Tokens JWT:

  * ID Token
  * Access Token
  * Refresh Token

### 🧠 DICA DE PROVA:

> Se a questão fala de **login de usuário → User Pool**

---

## 3️⃣ 🔑 Cognito Identity Pools (Autorização AWS)

👉 Permite dar acesso a recursos AWS

### ✅ Funcionalidades:

* Gera **credenciais temporárias da AWS**
* Integra com:

  * Cognito User Pools
  * Login social
  * SAML / OIDC

### 📌 Permite:

* Acesso ao S3
* Acesso ao DynamoDB
* Acesso a outros serviços AWS

### 🧠 DICA DE PROVA:

> Se a questão fala de **acesso a recursos AWS → Identity Pool**

---

## 4️⃣ 🔄 User Pools vs Identity Pools

| Feature         | User Pool 👤 | Identity Pool 🔑 |
| --------------- | ------------ | ---------------- |
| Função          | Autenticação | Autorização      |
| Login usuário   | ✅            | ❌                |
| Acesso AWS      | ❌            | ✅                |
| Tokens JWT      | ✅            | ❌                |
| Credenciais AWS | ❌            | ✅                |

### 🧠 RESUMO PROVA:

> **User Pool = QUEM É O USUÁRIO**
> **Identity Pool = O QUE ELE PODE ACESSAR**

---

## 5️⃣ 🔗 Integração entre eles

👉 Fluxo comum:

1. Usuário faz login no **User Pool**
2. Recebe token JWT
3. Token é passado para o **Identity Pool**
4. Identity Pool retorna **credenciais AWS temporárias**

---

## 6️⃣ 🌐 Cognito + ALB (Application Load Balancer)

👉 O **Application Load Balancer (ALB)** pode autenticar usuários usando Cognito

### ✅ Fluxo:

1. Usuário acessa aplicação
2. ALB redireciona para Cognito
3. Usuário faz login
4. ALB libera acesso

### 📌 Vantagem:

* Não precisa implementar autenticação no backend

### 🧠 DICA DE PROVA:

> ALB + autenticação → **Cognito User Pools**

---

## 7️⃣ 🔐 Cognito Sync (⚠️ LEGADO)

👉 Antigo serviço para sincronizar dados de usuário entre dispositivos

### ❗ Importante:

* Está **deprecated/legado**
* Substituído por:

  * AppSync
  * DynamoDB

### 🧠 DICA DE PROVA:

> Se aparecer Cognito Sync → provavelmente **não é a melhor resposta**

---

## 8️⃣ ⚙️ Hands-On / Conceitos importantes

### 🔹 User Pools:

* Hosted UI (login pronto)
* Triggers com Lambda (ex: pós-login)
* Custom authentication flows

### 🔹 Identity Pools:

* Roles IAM associadas
* Usuários autenticados vs não autenticados (guest access)

---

## 9️⃣ 🧠 Pegadinhas de prova

### ⚠️ 1. Confundir autenticação vs autorização

* Login → User Pool
* Acesso AWS → Identity Pool

---

### ⚠️ 2. “Usuário acessa S3 diretamente”

👉 Precisa de:

* Identity Pool + IAM Role

---

### ⚠️ 3. “Login social”

👉 Pode usar:

* User Pool (federation)
* Identity Pool (mais comum pra acesso AWS)

---

### ⚠️ 4. “Credenciais temporárias AWS”

👉 SEMPRE:

* Identity Pool

---

## 🔟 🎯 Resumo final (modo revisão rápida)

* 👤 User Pool → Login (AuthN)
* 🔑 Identity Pool → Permissão AWS (AuthZ)
* 🔗 Usados juntos na maioria dos casos
* 🌐 ALB pode autenticar com Cognito
* ⚠️ Cognito Sync é legado

---


