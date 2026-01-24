# 📘 README — IAM & AWS CLI (Resumo)

Este documento resume os principais conceitos de **IAM (Identity and Access Management)** e **AWS CLI**, abordados na seção do curso, com **dicas direcionadas para a prova AWS Developer (Associate)**.

---

## 🔐 1. Introdução ao IAM

O **IAM** é o serviço da AWS responsável por **gerenciar identidades e permissões**.

### Conceitos principais:

* **Users (Usuários)**: identidades individuais (pessoas ou aplicações).
* **Groups (Grupos)**: conjunto de usuários com permissões em comum.
* **Policies (Políticas)**: regras que definem o que pode ou não ser acessado.

👉 **Boa prática**
Nunca conceder permissões diretamente a usuários — usar **grupos ou roles**.

💡 **Dica de prova AWS Developer**

* IAM é sempre associado a **segurança**
* Se a questão fala em **controle de acesso**, **credenciais** ou **permissões**, a resposta quase sempre envolve IAM

---

## 👤 2. IAM Users & Groups (Hands On)

* Usuários representam **pessoas ou sistemas**
* Grupos facilitam o **gerenciamento de permissões**
* Um usuário pode pertencer a **vários grupos**

### Exemplo:

* Grupo `Admins` → permissões administrativas
* Grupo `Developers` → acesso limitado a serviços específicos

💡 **Dica de prova AWS Developer**

* **Usuários = pessoas**
* Aplicações **não deveriam usar IAM User**
* Se aparecer app + IAM User → **desconfie**

---

## 🌐 3. AWS Console – Simultaneous Sign-in

A AWS permite **login simultâneo** de vários usuários no Console.

### Importante:

* Cada usuário tem **credenciais próprias**
* Todas as ações ficam registradas no **CloudTrail**
* Facilita auditoria e segurança

💡 **Dica de prova AWS Developer**

* Console é acesso **humano**
* Auditoria e rastreabilidade → **CloudTrail**
* Perguntas sobre “quem fez o quê” → CloudTrail

---

## 📜 4. IAM Policies

As **policies** definem permissões usando JSON.

### Estrutura básica:

* **Effect**: Allow ou Deny
* **Action**: o que pode ser feito (ex: `s3:GetObject`)
* **Resource**: em quais recursos
* **Condition (opcional)**: regras adicionais

👉 **Regra de ouro**
Sempre aplicar o **Princípio do Menor Privilégio**.

💡 **Dica de prova AWS Developer**

* Alternativas com permissões amplas (`*`) quase sempre estão erradas
* Menor privilégio = resposta mais segura

---

## 🛠️ 5. IAM Policies (Hands On)

* Policies podem ser:

  * **AWS Managed** (prontas)
  * **Customer Managed** (criadas por você)
* Podem ser anexadas a:

  * usuários
  * grupos
  * roles

💡 **Dica de prova AWS Developer**

* AWS Managed = rapidez
* Customer Managed = controle
* Role + Policy = padrão para aplicações

---

## 🔑 6. IAM MFA (Multi-Factor Authentication)

O **MFA** adiciona uma camada extra de segurança.

### Como funciona:

* Algo que você **sabe** (senha)
* Algo que você **tem** (app autenticador)

👉 **Obrigatório para**:

* Usuário root
* Usuários com permissões elevadas

💡 **Dica de prova AWS Developer**

* Root sem MFA = **errado**
* Pergunta sobre aumentar segurança do Console → MFA

---

## 🔐 7. IAM MFA (Hands On)

* MFA pode ser configurado via:

  * Google Authenticator
  * Authy
  * Hardware MFA
* Reduz drasticamente o risco de acesso indevido

💡 **Dica de prova AWS Developer**

* MFA quase nunca é a resposta errada quando o foco é segurança

---

## 🔑 8. AWS Access Keys, CLI e SDK

### Access Keys

* Usadas para acesso **programático**
* Compostas por:

  * Access Key ID
  * Secret Access Key

⚠️ **Nunca** versionar ou expor essas chaves.

💡 **Dica de prova AWS Developer**

* Access Key no código ou Git = **errado**
* Sempre preferir **IAM Role**

---

### AWS CLI

Ferramenta de linha de comando para interagir com a AWS.

* Permite criar, listar e gerenciar recursos
* Usa as **Access Keys** configuradas localmente
* Ideal para automação e scripts

💡 **Dica de prova AWS Developer**

* CLI aparece em **automação e pipelines**
* Não caem comandos específicos

---

### AWS SDK

* Permite que aplicações se comuniquem com a AWS
* Disponível para:

  * Java
  * JavaScript
  * Python
  * entre outros

👉 **Boa prática**
Usar **IAM Roles** em vez de Access Keys hardcoded.

💡 **Dica de prova AWS Developer**

* SDK + IAM Role = padrão correto
* SDK + Access Key fixa = alternativa errada

---

## ✅ Boas Práticas Gerais

* Usar **IAM Roles** sempre que possível
* Evitar permissões amplas (`*`)
* Ativar **MFA**
* Seguir o **menor privilégio**
* Monitorar acessos com **CloudTrail**

💡 **Dica de prova AWS Developer**
Essas boas práticas aparecem **disfarçadas como requisitos da questão**.

---

📌 **Resumo final**
IAM garante **segurança**, **controle de acesso** e **auditoria** na AWS.
CLI e SDK permitem **automação e integração segura** com aplicações.


