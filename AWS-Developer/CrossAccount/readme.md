
# 📘 Cross-Account Lambda → DynamoDB (STS AssumeRole)

## 🧠 🎯 Objetivo

Permitir que uma **Lambda na Conta B** acesse o **DynamoDB na Conta A** usando **STS AssumeRole**

---

# 🧱 1. Criar Lambda (Conta B)

* Criar função Lambda normalmente
* Associar uma **execution role (IAM Role)**

---

# 🔐 2. Execution Role da Lambda (Conta B)

👉 NÃO é resource policy
👉 É a **IAM Role da Lambda**

✔ Essa role executa a função
✔ Vai precisar assumir role da Conta A

---

# 🛡️ 3. Criar Role na Conta A (Trust Policy) Onde está o recurso que vou acessar

👉 Essa role será assumida pela Lambda

### Trust Policy (Conta A):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::CONTA_B_ID:role/NOME_DA_EXECUTION_ROLE"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

✔ Aqui você permite que a Conta B assuma essa role

---

# 🔑 4. Permissão na Conta B (Execution Role)

👉 Adicionar policy inline:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "sts:AssumeRole",
      "Resource": "arn:aws:iam::CONTA_A_ID:role/NOME_DA_ROLE"
    }
  ]
}
```

✔ Isso permite que a Lambda execute o AssumeRole

---

# 🗄️ 5. Permissões na Role (Conta A)

👉 Adicionar acesso ao DynamoDB:

```json
{
  "Effect": "Allow",
  "Action": "dynamodb:*",
  "Resource": "*"
}
```

✔ Aqui define o que a Lambda poderá fazer

---

# 💻 6. Código da Lambda (Python)

```python
import boto3

def lambda_handler(event, context):

    sts = boto3.client('sts')

    response = sts.assume_role(
        RoleArn='arn:aws:iam::CONTA_A_ID:role/NOME_DA_ROLE',
        RoleSessionName='lambda-session'
    )

    creds = response['Credentials']

    dynamodb = boto3.resource(
        'dynamodb',
        region_name='us-east-1',
        aws_access_key_id=creds['AccessKeyId'],
        aws_secret_access_key=creds['SecretAccessKey'],
        aws_session_token=creds['SessionToken']
    )

    table = dynamodb.Table('cadastro-pokemon')

    response = table.scan()

    for item in response['Items']:
        print(item)

    return response['Items']
```

---

# 🔥 🔁 Fluxo completo

```text
Lambda (Conta B)
→ Execution Role
→ sts:AssumeRole
→ Role (Conta A)
→ DynamoDB
```

---

# ⚠️ Pegadinhas de prova

* ❌ Não usar resource policy
* ❌ Não usar ARN da Lambda
* ✔ Usar ARN da **execution role**
* ✔ Sempre usar `sts:AssumeRole` em cross-account

---

# 🧠 Resumo final

* Conta B → executa
* Conta A → autoriza
* STS → conecta

---

