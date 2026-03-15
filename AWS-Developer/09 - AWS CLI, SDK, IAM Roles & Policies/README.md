# 📘 AWS CLI, SDK, IAM Roles & Policies — AWS Developer Associate (DVA-C02)

Guia resumido dos tópicos que mais aparecem na prova envolvendo **CLI, SDK, credenciais e autenticação na AWS**.

---

# 1️⃣ Instance Metadata (EC2 Metadata)

O **Instance Metadata Service (IMDS)** permite que uma instância **Amazon EC2** obtenha **informações sobre si mesma**.

Essas informações ficam disponíveis **dentro da instância**, sem precisar de internet.

### Endpoint

```
http://169.254.169.254
```

### Exemplos

Obter instance id:

```bash
curl http://169.254.169.254/latest/meta-data/instance-id
```

Listar metadata:

```bash
curl http://169.254.169.254/latest/meta-data/
```

### Informações disponíveis

| Informação           | Exemplo                 |
| -------------------- | ----------------------- |
| Instance ID          | i-abc123                |
| Security Groups      | sg-xxxx                 |
| IP privado           | 10.0.1.5                |
| AMI ID               | ami-xxxx                |
| IAM Role credentials | credenciais temporárias |

---

# 2️⃣ Instance Metadata para IAM Roles

Quando uma EC2 tem uma **AWS Identity and Access Management Role**, ela recebe **credenciais temporárias automaticamente**.

Aplicações podem obter essas credenciais via metadata.

Exemplo:

```
http://169.254.169.254/latest/meta-data/iam/security-credentials/
```

### Benefício

❌ Não armazenar Access Keys no código
✔ Credenciais rotacionadas automaticamente
✔ Mais seguro

---

# 3️⃣ IMDSv1 vs IMDSv2

| Versão | Característica      |
| ------ | ------------------- |
| IMDSv1 | acesso direto       |
| IMDSv2 | usa token de sessão |

AWS recomenda **IMDSv2** porque protege contra **SSRF attacks**.

Fluxo IMDSv2:

1. Solicitar token
2. Usar token para acessar metadata

---

# 4️⃣ AWS CLI Profiles

A **AWS Command Line Interface** permite configurar **múltiplos perfis de credenciais**.

### Criar perfil

```
aws configure
```

Informações configuradas:

```
Access Key
Secret Key
Region
Output format
```

Arquivos usados:

```
~/.aws/credentials
~/.aws/config
```

---

### Usar perfil específico

```
aws s3 ls --profile dev
```

---

# 5️⃣ AWS CLI com MFA

MFA pode ser usado com CLI para aumentar segurança.

Fluxo:

1️⃣ Usuário autentica
2️⃣ Fornece código MFA
3️⃣ Recebe **temporary credentials**

Comando comum:

```
aws sts get-session-token
```

Serviço usado:

➡️ **AWS Security Token Service**

---

# 6️⃣ AWS SDK Overview

O **AWS SDK** permite que aplicações acessem serviços AWS programaticamente.

Suporta várias linguagens:

* Python (boto3)
* Java
* JavaScript
* Go
* .NET

Exemplo usando Python:

```python
import boto3

s3 = boto3.client('s3')
response = s3.list_buckets()
```

Serviços comuns usados via SDK:

* **Amazon S3**
* **Amazon DynamoDB**
* **Amazon SQS**
* **AWS Lambda**

---

# 7️⃣ Exponential Backoff & Retry

AWS SDK implementa **retry automático** quando ocorre erro temporário.

Exemplo de erros:

* **Throttling**
* **Rate exceeded**
* **Service unavailable**

### Estratégia usada

➡️ **Exponential Backoff**

Tempo de espera aumenta progressivamente:

```
1s
2s
4s
8s
16s
```

Objetivo:

✔ reduzir overload na AWS
✔ evitar retry agressivo

---

# 8️⃣ Credential Provider Chain

O AWS SDK procura credenciais em uma **ordem específica**.

### Ordem de busca

| Ordem | Fonte                 |
| ----- | --------------------- |
| 1     | Environment Variables |
| 2     | CLI credentials file  |
| 3     | CLI config file       |
| 4     | Container credentials |
| 5     | EC2 Instance Metadata |

---

### Exemplo (variáveis de ambiente)

```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
```

---

# 9️⃣ AWS Signature Version 4 (SigV4)

Toda requisição para AWS é **assinada criptograficamente**.

Esse processo chama-se **Signature Version 4**.

Objetivo:

✔ autenticar o request
✔ garantir integridade
✔ evitar tampering

Componentes usados na assinatura:

| Elemento     | Função              |
| ------------ | ------------------- |
| Access Key   | identifica usuário  |
| Secret Key   | gera assinatura     |
| Timestamp    | evita replay attack |
| Request hash | garante integridade |

---

### Processo simplificado

1️⃣ Criar canonical request
2️⃣ Criar string to sign
3️⃣ Gerar assinatura com Secret Key
4️⃣ Enviar assinatura no header

---

# 🔟 Resumo para prova

| Conceito          | O que lembrar             |
| ----------------- | ------------------------- |
| Instance Metadata | endpoint 169.254.169.254  |
| IAM Role EC2      | credenciais temporárias   |
| IMDSv2            | usa token                 |
| CLI Profiles      | múltiplas credenciais     |
| MFA CLI           | usa STS                   |
| SDK               | acesso programático AWS   |
| Retry             | exponential backoff       |
| Credential Chain  | ordem de busca            |
| SigV4             | assinatura de requisições |

---

# 🎯 Pegadinhas comuns na prova

| Situação                       | Resposta correta          |
| ------------------------------ | ------------------------- |
| EC2 precisa acessar S3         | IAM Role                  |
| App em EC2 precisa credenciais | Instance Metadata         |
| Erro de throttling             | exponential backoff       |
| SDK não encontra credenciais   | credential provider chain |
| Requisições AWS autenticadas   | SigV4                     |

---

✅ **Dica final para AWS Developer**

Esse bloco de conteúdos geralmente aparece em questões sobre:

* **SDK authentication**
* **EC2 IAM Roles**
* **Retry strategies**
* **Security / signing requests**

Eles aparecem principalmente junto com:

* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon S3**

---

Se quiser, posso também te mandar **um SUPER README de 1 página com tudo de autenticação da AWS que cai na prova Developer** (IAM + STS + Roles + Policies + SigV4). Isso elimina várias pegadinhas do exame.
