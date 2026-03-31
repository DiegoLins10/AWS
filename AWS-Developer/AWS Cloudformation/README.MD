# ☁️ CloudFormation — README (AWS Developer DVA)

## 1️⃣ O que é? 🤔

👉 AWS CloudFormation

➡️ Serviço de **Infraestrutura como Código (IaC)**
➡️ Você define recursos em **template (YAML/JSON)**
➡️ AWS cria tudo automaticamente

💡 **Resumo prova:**

> “Descreva sua infra → CloudFormation provisiona”

No AWS CloudFormation, o nome do Export deve ser único por conta e região, ou seja, não pode existir dois exports com o mesmo nome nesse escopo, mas o valor do export pode ser repetido entre diferentes stacks sem problema; além disso, se um valor exportado estiver sendo usado por outro stack via Fn::ImportValue, ele não pode ser alterado nem removido até que as dependências sejam removidas.
---

## 2️⃣ Conceitos principais 🧱

### 🔹 Stack

* Conjunto de recursos
* Unidade de deploy

---

### 🔹 Template

* Arquivo YAML/JSON
* Define infraestrutura

---

### 🔹 Change Set

* Preview das mudanças antes de aplicar

💡 **DVA tip:**
👉 Evita erro em produção

---

## 3️⃣ Estrutura do Template 📄

### 🔹 Resources ⭐ (OBRIGATÓRIO)

👉 Define os recursos AWS

```yaml
Resources:
  MyEC2:
    Type: AWS::EC2::Instance
```

---

### 🔹 Parameters

👉 Inputs dinâmicos

```yaml
Parameters:
  InstanceType:
    Type: String
```

✔️ Reutilização
✔️ Flexibilidade

---

### 🔹 Mappings

👉 Valores fixos (ex: região → AMI)

```yaml
Mappings:
  RegionMap:
```

---

### 🔹 Outputs

👉 Saída da stack

```yaml
Outputs:
  InstanceId:
```

✔️ Pode exportar valores

---

### 🔹 Conditions

👉 Criar recursos condicionalmente

```yaml
Conditions:
```

---

Perfeito — vou **só melhorar a seção de Intrinsic Functions com exemplos mais fortes (nível prova DVA)** 👇

---

## 4️⃣ Intrinsic Functions 🧠 (CAI MUITO)

👉 Funções internas do AWS CloudFormation
👉 Usadas para deixar o template **dinâmico**

---

### 🔹 1. `Ref` (referência simples)

👉 Retorna:

* Valor do parâmetro
  OU
* ID do recurso

```yaml
Parameters:
  InstanceType:
    Type: String

Resources:
  MyEC2:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: !Ref InstanceType
```

💡 **Cai em prova:**
👉 `Ref` = valor básico / ID

---

### 🔹 2. `Fn::GetAtt` (atributo de recurso)

👉 Pega atributos de recursos criados

```yaml
Resources:
  MyInstance:
    Type: AWS::EC2::Instance

Outputs:
  PublicIP:
    Value: !GetAtt MyInstance.PublicIp
```

💡 **Muito comum:**

* PublicIp
* DNSName
* Arn

---

### 🔹 3. `Fn::Sub` ⭐ (string dinâmica — MAIS IMPORTANTE)

👉 Substitui variáveis dentro de string

```yaml
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: !Sub "my-bucket-${AWS::Region}-${AWS::AccountId}"
```

💡 Resultado:

```
my-bucket-us-east-1-123456789
```

✔️ Mais usado na prova
✔️ Mais limpo que Join

---

### 🔹 4. `Fn::Join` (concatenação)

👉 Junta strings com separador

```yaml
Outputs:
  URL:
    Value:
      Fn::Join:
        - ""
        - - "http://"
          - !GetAtt MyInstance.PublicDnsName
```

💡 **Dica prova:**
👉 Hoje `Sub` é preferido

---

### 🔹 5. `Fn::If` (condicional)

👉 Retorna valor baseado em condição

```yaml
Conditions:
  IsProd: !Equals [!Ref Env, prod]

Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: !If [IsProd, t3.large, t3.micro]
```

💡 **Cai assim:**
👉 comportamento diferente por ambiente

---

### 🔹 6. `Fn::FindInMap` (Mappings)

👉 Busca valores em mappings

```yaml
Mappings:
  RegionMap:
    us-east-1:
      AMI: ami-123
    us-west-1:
      AMI: ami-456

Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: !FindInMap [RegionMap, !Ref "AWS::Region", AMI]
```

💡 **Muito usado para AMI por região**

---

### 🔹 7. `Fn::ImportValue` (cross-stack) ⭐

👉 Importa valores de outra stack

```yaml
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      SubnetId: !ImportValue MySubnetExport
```

💡 **Cai MUITO:**
👉 comunicação entre stacks

---

### 🔹 8. `Fn::Base64` (User Data EC2)

👉 Codifica script para EC2

```yaml
Properties:
  UserData:
    Fn::Base64: !Sub |
      #!/bin/bash
      yum install -y httpd
      systemctl start httpd
```

💡 **Clássico de prova:**
👉 EC2 + UserData

---

# 🧠 Resumo rápido (decorar)

| Função        | Uso              |
| ------------- | ---------------- |
| Ref           | Valor básico     |
| GetAtt        | Atributo recurso |
| Sub ⭐         | String dinâmica  |
| Join          | Concatenar       |
| If            | Condição         |
| FindInMap     | Lookup           |
| ImportValue ⭐ | Cross-stack      |
| Base64        | UserData         |

---

# 🚨 Pegadinhas

* `Sub` > `Join` (preferido)
* `ImportValue` = integração entre stacks
* `GetAtt` ≠ `Ref` (muito confundido)

---
💡 **DVA tip:**
👉 `Fn::Sub` é o mais usado

---

## 5️⃣ Stack Lifecycle 🔄

### 🔹 Create

* Cria recursos

---

### 🔹 Update

* Atualiza stack

---

### 🔹 Delete

* Remove tudo

---

### 🔹 Rollback ⭐

👉 Se falhar:

* CloudFormation **desfaz tudo automaticamente**

💡 **Muito importante:**
👉 Garante consistência

---

## 6️⃣ Rollbacks (CAI MUITO) 💥

👉 Se erro no deploy:

* Stack volta ao estado anterior

✔️ Segurança
✔️ Evita estado inconsistente

---

## 7️⃣ Capabilities ⚠️

👉 Permissões especiais

Ex:

* `CAPABILITY_IAM`
* `CAPABILITY_NAMED_IAM`

💡 **Pegadinha:**
👉 Necessário para criar recursos IAM

---

## 8️⃣ Service Role 🔐

👉 Role que CloudFormation usa

✔️ Permissões controladas
✔️ Segurança

---

## 9️⃣ Deletion Policy 🧹

👉 O que acontece ao deletar stack

* `Delete` (default)
* `Retain` ⭐
* `Snapshot`

💡 **DVA tip:**
👉 Muito usado com RDS / S3

---

## 🔟 Stack Policy 🔒

👉 Protege recursos específicos

✔️ Evita updates acidentais

---

## 1️⃣1️⃣ Termination Protection 🚫

👉 Impede deletar a stack

✔️ Segurança extra

---

## 1️⃣2️⃣ Custom Resources ⚙️

👉 Executa lógica customizada (via Lambda)

* AWS Lambda

💡 Quando usar:

* Algo que CF não suporta nativamente

---

## 1️⃣3️⃣ StackSets 🌍

👉 Deploy em múltiplas contas/regiões

✔️ Multi-account
✔️ Multi-region

💡 Muito usado em empresas grandes

---

## 1️⃣4️⃣ YAML vs JSON 📄

| YAML         | JSON         |
| ------------ | ------------ |
| Mais legível | Mais verboso |
| Mais usado   | Menos comum  |

💡 **Prova:**
👉 YAML é o padrão

---

## 1️⃣5️⃣ Fluxo completo 🧠

1. Cria template
2. Cria stack
3. CloudFormation provisiona recursos
4. Monitora estado
5. Rollback se falhar

---

# 🧠 Pegadinhas de prova 🚨

### ❗ “Rollback automático”

👉 CloudFormation

---

### ❗ “Criar infra declarativa”

👉 CloudFormation

---

### ❗ “Preview antes do deploy”

👉 Change Set

---

### ❗ “Criar IAM via template”

👉 Precisa de **Capabilities**

---

### ❗ “Manter recurso após delete”

👉 `Retain`

---

### ❗ “Executar lógica custom”

👉 Custom Resource + Lambda

---

### ❗ “Multi account deploy”

👉 StackSets

---

# 🧠 Resumo final (pra decorar)

* Template → define infra
* Stack → executa infra
* Resources → obrigatório
* Rollback → automático ⭐
* Capabilities → IAM
* DeletionPolicy → Retain/Snapshot
* StackSets → multi-conta

---

# ➕ 1️⃣6️⃣ Pseudo Parameters 🧠 (CAI MUITO)

👉 São variáveis **automáticas da AWS** no AWS CloudFormation
👉 Você NÃO precisa declarar — já existem no template

---

## 🎯 Principais Pseudo Parameters

---

### 🔹 `AWS::Region`

👉 Região atual da stack

```yaml
!Ref AWS::Region
```

💡 Ex:

* us-east-1
* sa-east-1

---

### 🔹 `AWS::AccountId`

👉 ID da conta AWS

```yaml
!Ref AWS::AccountId
```

💡 Ex:

* 123456789012

---

### 🔹 `AWS::StackName`

👉 Nome da stack

```yaml
!Ref AWS::StackName
```

---

### 🔹 `AWS::StackId`

👉 ID único da stack

```yaml
!Ref AWS::StackId
```

---

### 🔹 `AWS::Partition`

👉 Tipo de partição

💡 Ex:

* aws (normal)
* aws-cn (China)

---

### 🔹 `AWS::URLSuffix`

👉 Sufixo de domínio

💡 Ex:

* amazonaws.com

---

### 🔹 `AWS::NoValue` ⭐

👉 Remove propriedade condicionalmente

```yaml
Conditions:
  IsProd: !Equals [!Ref Env, prod]

Resources:
  MyBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: !If [IsProd, "prod-bucket", !Ref "AWS::NoValue"]
```

💡 **Muito importante:**
👉 Remove o campo se condição for falsa

---

## 🔥 Uso mais comum (Fn::Sub) ⭐

👉 Onde mais aparece na prova

```yaml
BucketName: !Sub "my-bucket-${AWS::Region}-${AWS::AccountId}"
```

✔️ Nome único global
✔️ Evita conflito

---

## 🧪 Exemplo completo (nível prova)

```yaml
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: !Sub "app-${AWS::StackName}-${AWS::Region}"
```

---

## ⚔️ Comparação importante

| Pseudo Parameter | Uso                 |
| ---------------- | ------------------- |
| AWS::Region      | Região              |
| AWS::AccountId   | Conta               |
| AWS::StackName   | Nome stack          |
| AWS::NoValue ⭐   | Remover propriedade |

---

## 🚨 Pegadinhas de prova

### ❗ “Valor automático da conta/região”

👉 Pseudo parameter

---

### ❗ “Gerar nome único global”

👉 `Sub + AWS::Region + AWS::AccountId`

---

### ❗ “Remover campo condicional”

👉 `AWS::NoValue`

---

### ❗ “Não precisa declarar no template”

👉 Pseudo parameters

---

# 🧠 Resumo pra decorar

* Não precisam ser definidos
* Usados com `Ref` ou `Sub`
* `NoValue` remove propriedades ⭐
* Muito usados pra naming dinâmico

---

