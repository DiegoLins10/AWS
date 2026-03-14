# 📦 Amazon S3 – AWS Developer Associate (DVA)

## 1️⃣ S3 Overview

O **Amazon S3 (Simple Storage Service)** é um serviço de **armazenamento de objetos**.

Estrutura do S3:

```
Bucket
 └── Object
      ├── Key (nome do arquivo)
      └── Value (dados)
```

📌 Conceitos importantes:

| Conceito   | Descrição              |
| ---------- | ---------------------- |
| Bucket     | container de objetos   |
| Object     | arquivo armazenado     |
| Key        | nome/caminho do objeto |
| Version ID | versão do objeto       |

Exemplo de key:

```
images/profile.jpg
```

---

# 2️⃣ Segurança no S3

O acesso ao S3 pode ser controlado por:

1️⃣ **IAM Policies**
2️⃣ **Bucket Policies**
3️⃣ **ACLs (menos usadas hoje)**

📌 Regra da AWS:

```
Default = Deny
```

Ou seja:

```
Sem permissão explícita → acesso negado
```

---

# 3️⃣ Bucket Policy

A **Bucket Policy** é uma política JSON aplicada diretamente no bucket.

Ela controla:

* quem pode acessar
* quais ações podem ser feitas
* quais recursos podem ser acessados

Exemplo permitindo leitura pública:

```json
{
 "Effect": "Allow",
 "Principal": "*",
 "Action": "s3:GetObject",
 "Resource": "arn:aws:s3:::meu-bucket/*"
}
```

📌 Usos comuns:

* permitir acesso público
* permitir outra conta AWS
* restringir acesso por IP
* permitir acesso via CloudFront

---

# 4️⃣ S3 Static Website

O S3 pode hospedar **sites estáticos**.

Exemplos:

* HTML
* CSS
* JavaScript

Fluxo:

```
User
 ↓
S3 Static Website
 ↓
index.html
```

Para habilitar:

1️⃣ ativar **Static Website Hosting**
2️⃣ definir **index document**

Exemplo:

```
index.html
error.html
```

📌 Importante:

O bucket precisa permitir **acesso público**.

---

# 5️⃣ S3 Versioning

O **Versioning** permite manter **múltiplas versões de um objeto**.

Exemplo:

```
file.txt
 ├── v1
 ├── v2
 └── v3
```

Benefícios:

* recuperação de arquivos apagados
* rollback de versões
* proteção contra sobrescrita

📌 Estados possíveis:

| Estado    | Descrição           |
| --------- | ------------------- |
| Enabled   | versionamento ativo |
| Suspended | pausado             |

---

### Delete Marker

Quando você deleta um objeto:

```
DELETE
```

S3 cria um:

```
Delete Marker
```

Mas as versões antigas continuam existindo.

---

# 6️⃣ S3 Replication

A **replicação do S3** copia objetos automaticamente entre buckets.

Existem dois tipos:

| Tipo | Descrição                |
| ---- | ------------------------ |
| CRR  | Cross Region Replication |
| SRR  | Same Region Replication  |

---

### CRR

Replica objetos para **outra região AWS**.

Usos:

* disaster recovery
* compliance
* latência global

---

### SRR

Replica objetos **na mesma região**.

Usos:

* separar ambientes
* replicar logs
* analytics

---

### Requisitos para replicação

1️⃣ **Versioning ativado nos dois buckets**

2️⃣ **IAM Role para replicação**

3️⃣ bucket destino configurado

📌 Apenas **novos objetos são replicados**.

---

# 7️⃣ S3 Storage Classes

As **Storage Classes do S3** permitem otimizar **custo vs frequência de acesso**.

Regra geral:

```
dados acessados frequentemente → mais caro
dados raramente acessados → mais barato
```

---

## 📊 Comparação das Storage Classes

| Storage Class                          | 💰 Custo | Uso Principal                    | Frequência de Acesso | Latência        | Durabilidade  | Disponibilidade | Multi-AZ | Retenção mínima |
| -------------------------------------- | -------- | -------------------------------- | -------------------- | --------------- | ------------- | --------------- | -------- | --------------- |
| **S3 Standard**                        | 💲💲💲💲 | aplicações, sites, dados ativos  | frequente            | ms              | 99.999999999% | 99.99%          | ✔        | nenhuma         |
| **S3 Standard-IA (INFREQUENT ACCESS)** | 💲💲💲   | backups, DR, arquivos ocasionais | pouco frequente      | ms              | 99.999999999% | 99.9%           | ✔        | 30 dias         |
| **S3 One Zone-IA (INFREQUENT ACCESS)** | 💲💲     | backups secundários              | pouco frequente      | ms              | 99.999999999% | 99.5%           | ❌        | 30 dias         |
| **S3 Intelligent-Tiering**             | 💲💲💲   | acesso imprevisível              | variável             | ms              | 99.999999999% | 99.9%           | ✔        | nenhuma         |
| **S3 Glacier Instant Retrieval**       | 💲💲     | arquivamento com acesso rápido   | raro                 | ms              | 99.999999999% | 99.9%           | ✔        | 90 dias         |
| **S3 Glacier Flexible Retrieval**      | 💲       | arquivamento barato              | muito raro           | minutos / horas | 99.999999999% | 99.99%          | ✔        | 90 dias         |
| **S3 Glacier Deep Archive**            | 💲       | arquivamento de longo prazo      | quase nunca          | horas           | 99.999999999% | 99.99%          | ✔        | 180 dias        |

---

## 📌 Classes **INFREQUENT ACCESS**

Essas aparecem muito nas questões da prova.

| Classe             | Característica                             |
| ------------------ | ------------------------------------------ |
| **S3 Standard-IA** | Multi-AZ + taxa de leitura (retrieval fee) |
| **S3 One Zone-IA** | armazenado em **apenas 1 AZ**              |

---

# 🎯 Pontos que mais caem na prova DVA

### S3 Versioning

Protege contra:

```
overwrite
delete acidental
```

---

### Replication

Precisa:

```
Versioning enabled
```

---

### Static Website

Requer:

```
Bucket público
```

---

### Bucket Policy

Controla **acesso ao bucket**.

---

# 🧠 Resumo rápido para revisão

```
S3 = armazenamento de objetos
```

Segurança:

```
IAM
Bucket Policy
ACL
```

Recursos importantes:

```
Versioning → versões de arquivos
Replication → copiar objetos entre buckets
Static Website → hospedar site
Storage Classes → otimizar custo
```

---

✅ Esse conjunto de conceitos cobre **grande parte das perguntas de S3 na prova Developer Associate**.

---

Se quiser, posso também te montar **uma seção extra que cai MUITO na DVA mas ainda não está no seu README**, como:

* **S3 Lifecycle Policies**
* **Pre-Signed URLs**
* **S3 Encryption (SSE-S3, SSE-KMS, SSE-C)**

Esses **caem bastante em simulado e prova real**.
