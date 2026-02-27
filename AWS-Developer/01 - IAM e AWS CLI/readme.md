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

---

## 22. AWS CLI — Hands On

### O que é

A **AWS CLI** permite gerenciar recursos da AWS via terminal usando comandos (`aws ec2`, `aws iam`, etc.).

### Pontos-chave

* Usa **Access Key ID** + **Secret Access Key**
* Configuração via:

  ```bash
  aws configure
  ```
* Pode usar **profiles** (`--profile dev`)

### 💡 Dicas de prova

* **CLI ≠ Console** → CLI é programática
* Se a pergunta falar em **automação**, **scripts**, **CI/CD**, pense em **AWS CLI**
* CLI **não é recomendada em produção em EC2** → prefira **IAM Role**

---

## 23. AWS CloudShell

### O que é

Terminal **direto no console da AWS**, já autenticado, sem precisar configurar credenciais.

### Pontos-chave

* Não precisa de Access Keys
* Ideal para comandos rápidos
* Ambiente temporário

### 💡 Dicas de prova

* Pergunta falou **“sem instalar nada”** → **CloudShell**
* CloudShell **não substitui** EC2 ou Cloud9
* Ótimo para troubleshooting rápido

---

## 24. IAM Roles for AWS Services

### O que é

**IAM Role** permite que **serviços da AWS assumam permissões** temporárias.

### Exemplos clássicos

* EC2 acessando S3
* Lambda acessando DynamoDB
* ECS puxando imagem do ECR

### Pontos-chave

* **Não usa Access Keys**
* Usa **credenciais temporárias**
* Associada a **serviços**, não usuários

### 💡 Dicas de prova (MUITO IMPORTANTE)

* ❌ Nunca use Access Key dentro do código
* ✅ Sempre usar **IAM Role**
* Se a pergunta falar em **EC2 acessando outro serviço**, a resposta quase sempre é **IAM Role**

---

## 25. IAM Roles — Hands On

### O que acontece na prática

1. Cria a Role
2. Define **Trust Policy** (quem pode assumir)
3. Anexa **Permission Policy**
4. Associa ao serviço (EC2, Lambda, etc.)

### 💡 Dicas de prova

* **Trust Policy ≠ Permission Policy**
* Trust Policy define **QUEM assume**
* Permission Policy define **O QUE pode fazer**

---

## 26. IAM Security Tools

### Principais ferramentas

* **IAM Credentials Report**
* **IAM Access Advisor**
* **Password Policy**

### O que fazem

* Detectam chaves antigas
* Mostram permissões não usadas
* Ajudam em auditoria

### 💡 Dicas de prova

* Auditoria de usuários → **Credentials Report**
* Ver permissões usadas → **Access Advisor**

---

## 27. IAM Security Tools — Hands On

### Na prática

* Geração de relatórios
* Análise de risco
* Limpeza de permissões excessivas

### 💡 Dica de prova

* Pergunta sobre **revisão de permissões** → ferramentas de segurança IAM

---

## 28. IAM Best Practices

### Boas práticas (DECORAR)

* ❌ Não usar root
* ✅ MFA no root
* ❌ Não usar Access Key em EC2
* ✅ Usar Roles
* ✅ Princípio do menor privilégio
* ✅ Rotação de credenciais

### 💡 Dicas de prova

* **Root User** → só setup inicial
* Qualquer cenário seguro → **Least Privilege**
* MFA sempre aparece como resposta correta

---

## 29. Shared Responsibility Model for IAM

### Quem é responsável por quê

| AWS            | Cliente            |
| -------------- | ------------------ |
| Infraestrutura | Usuários IAM       |
| Datacenters    | Policies           |
| Hardware       | MFA                |
| Software base  | Controle de acesso |

### 💡 Dicas de prova

* IAM é **responsabilidade do cliente**
* AWS **não gerencia permissões do seu usuário**

---

## 30. IAM Summary (Resumo Final)

### Conceitos que mais caem

* IAM User vs Role
* Policies (JSON)
* Least Privilege
* Roles para serviços
* Security Tools
* Shared Responsibility

---


# 🧠 RESUMÃO DE PROVA (COLA FINAL)

* EC2 acessando S3 → **IAM Role**
* Código com Access Key → ❌ errado
* Auditoria de usuários → **Credentials Report**
* Permissões excessivas → **Least Privilege**
* CLI em produção → **Role**
* Sem instalar nada → **CloudShell**
* Segurança → **MFA**

---


