# 📚 AWS DVA – RDS, Multi-AZ e Read Replicas

## 1️⃣ Amazon RDS – Visão Geral

**Amazon RDS (Relational Database Service)** é um serviço gerenciado para bancos de dados relacionais.

Ele cuida automaticamente de:

* Provisionamento
* Backup
* Patch de segurança
* Monitoramento
* Failover
* Replicação

📌 **Você gerencia apenas o banco**, não o servidor.

### Engines suportadas

* MySQL
* PostgreSQL
* MariaDB
* Oracle
* SQL Server
* Amazon Aurora

---

## 2️⃣ Características importantes do RDS

| Feature             | Descrição                       |
| ------------------- | ------------------------------- |
| Backup automático   | Backup diário + logs            |
| Snapshots           | Backup manual                   |
| Multi-AZ            | Alta disponibilidade            |
| Read Replicas       | Escalar leitura                 |
| Storage autoscaling | Aumenta storage automaticamente |
| Encryption          | KMS                             |

---

# 3️⃣ Multi-AZ (High Availability)

**Multi-AZ = Alta disponibilidade / Disaster Recovery**

Quando ativado, o RDS cria **uma réplica standby em outra Availability Zone**.

### Como funciona

1. Primary DB recebe escrita
2. Dados replicados **sincronamente**
3. Existe uma **standby instance**
4. Se a AZ cair → **failover automático**

### Arquitetura

```
AZ-a
Primary DB
   │
   │ synchronous replication
   │
AZ-b
Standby DB
```

### Características

| Feature    | Multi-AZ             |
| ---------- | -------------------- |
| Objetivo   | Alta disponibilidade |
| Replicação | Síncrona             |
| Leitura    | ❌ Não                |
| Failover   | ✅ Automático         |
| AZ         | Sempre outra AZ      |

📌 **Aplicação continua usando o mesmo endpoint** após failover.

---

# 4️⃣ Read Replicas (Read Scaling)

**Read Replicas são usadas para escalar leitura.**

Elas criam **cópias do banco para consultas SELECT**.

### Como funciona

1. Primary DB recebe escrita
2. Dados replicados **assincronamente**
3. Aplicação envia consultas de leitura para replicas

### Arquitetura

```
Primary DB
   │
   ├── Read Replica
   ├── Read Replica
   └── Read Replica
```

### Características

| Feature             | Read Replica    |
| ------------------- | --------------- |
| Objetivo            | Escalar leitura |
| Replicação          | Assíncrona      |
| Leitura             | ✅ Sim           |
| Failover automático | ❌ Não           |
| Promover a primário | ✅ Manual        |

📌 Pode existir **até 15 Read Replicas** dependendo da engine.

---

# 5️⃣ Localização das Read Replicas

Read Replicas podem estar:

* mesma AZ
* outra AZ
* outra região (**Cross-Region Read Replica**)

📌 Muito usado para **disaster recovery entre regiões** ou **latência global**.

---

# 6️⃣ Multi-AZ vs Read Replicas

| Característica      | Multi-AZ             | Read Replica                 |
| ------------------- | -------------------- | ---------------------------- |
| Objetivo            | Alta disponibilidade | Escalar leitura              |
| Replicação          | Síncrona             | Assíncrona                   |
| Leitura             | ❌                    | ✅                            |
| Failover automático | ✅                    | ❌                            |
| Promover primário   | Automático           | Manual                       |
| Localização         | Outra AZ             | Mesma AZ, outra AZ ou região |

---

# 7️⃣ Arquitetura combinada (muito comum)

Você pode usar **Multi-AZ + Read Replicas juntos**.

```
                Read Replica
                     │
                     │
Primary DB ─── Read Replica
     │
     │ synchronous
     │
Standby DB (Multi-AZ)
```

* Multi-AZ → **alta disponibilidade**
* Read Replicas → **performance de leitura**

---

# 8️⃣ Pegadinhas comuns na prova (DVA)

### 🔹 Precisa escalar leitura

➡️ **Use Read Replicas**

---

### 🔹 Precisa alta disponibilidade automática

➡️ **Use Multi-AZ**

---

### 🔹 Precisa de Disaster Recovery entre regiões

➡️ **Cross-Region Read Replica**

---

### 🔹 Precisa performance + HA

➡️ **Multi-AZ + Read Replicas**

---

# 9️⃣ Resumo para lembrar rápido (prova)

🧠 **Multi-AZ**

* Alta disponibilidade
* Replicação síncrona
* Failover automático
* Não serve para leitura

🧠 **Read Replica**

* Escalar leitura
* Replicação assíncrona
* Pode estar em outra região
* Promoção manual

---

✅ **Regra de ouro da AWS**

```
Multi-AZ = High Availability
Read Replica = Read Scaling
```

---

# 🐬 Amazon Aurora – AWS Developer Associate (DVA) Study Notes

## 1️⃣ O que é o Amazon Aurora

O **Amazon Aurora** é um banco de dados relacional totalmente gerenciado pela AWS, compatível com **MySQL** e **PostgreSQL**, projetado para oferecer **alta performance, alta disponibilidade e escalabilidade automática**.

Ele faz parte do ecossistema do **Amazon RDS**, mas possui uma **arquitetura diferente e otimizada**.

Principais características:

* Até **5x mais rápido que MySQL**
* Até **3x mais rápido que PostgreSQL**
* Alta disponibilidade nativa
* Replicação automática entre AZs
* Escala leitura com várias replicas
* Storage que cresce automaticamente

---

# 2️⃣ Arquitetura do Aurora

Aurora separa **compute** e **storage**, diferente do RDS tradicional.

```
Aurora Cluster
│
├── Writer Instance (Primary)
├── Reader Instance (Replica)
├── Reader Instance (Replica)
│
└── Shared Storage Layer
```

O storage é **compartilhado entre todas as instâncias**.

Isso permite:

* failover muito rápido
* replicas sem replicação pesada
* escalabilidade maior

---

# 3️⃣ Replicação do Storage (Importante para prova)

Aurora replica automaticamente os dados:

* **6 cópias dos dados**
* distribuídas em **3 Availability Zones**

Distribuição:

```
AZ-1 → 2 cópias
AZ-2 → 2 cópias
AZ-3 → 2 cópias
```

Isso garante:

* tolerância a falha de **até 2 cópias**
* alta durabilidade
* failover rápido

---

# 4️⃣ Aurora Cluster

Um **Aurora Cluster** é composto por:

| Componente       | Função                                 |
| ---------------- | -------------------------------------- |
| Writer Instance  | instância principal que aceita escrita |
| Reader Instances | replicas usadas para leitura           |
| Shared Storage   | storage distribuído entre AZs          |

Endpoints importantes:

| Endpoint          | Função                              |
| ----------------- | ----------------------------------- |
| Cluster Endpoint  | conecta na instância writer         |
| Reader Endpoint   | balanceia consultas entre replicas  |
| Instance Endpoint | conecta em uma instância específica |

---

# 5️⃣ Quantas instâncias podem existir

Um cluster Aurora pode ter:

| Tipo            | Quantidade |
| --------------- | ---------- |
| Writer          | 1          |
| Reader Replicas | até **15** |

Total possível:

```
1 Writer + 15 Readers
```

---

# 6️⃣ Aurora Replicas

Aurora replicas são usadas para **escalar leitura**.

Características:

* compartilham o mesmo storage
* replicação **muito rápida (ms)**
* podem ser promovidas a **Writer**

Benefícios:

* escala leitura
* failover rápido
* balanceamento de consultas

---

# 7️⃣ Failover no Aurora

Se a instância **Writer falhar**:

1. Aurora promove automaticamente uma **Reader Replica**
2. Ela vira a nova **Writer**
3. O endpoint do cluster continua o mesmo

Tempo típico de failover:

```
~30 segundos
```

Mais rápido que **RDS Multi-AZ tradicional**.

---

# 8️⃣ Auto Scaling de Replicas

Aurora permite **Auto Scaling de Read Replicas**.

Baseado em:

* CPU
* número de conexões
* métricas do CloudWatch

Fluxo:

```
alta carga de leitura
↓
Aurora cria novas replicas
↓
Reader Endpoint distribui queries
```

---

# 9️⃣ Storage do Aurora

Aurora usa storage distribuído.

Características:

* cresce automaticamente
* até **128 TB**
* não precisa provisionar previamente

Escala automaticamente conforme dados aumentam.

---

# 🔟 Aurora vs RDS (diferença importante)

| Característica | RDS         | Aurora              |
| -------------- | ----------- | ------------------- |
| Replicação     | Multi-AZ    | Storage distribuído |
| Replicas       | até 5       | até 15              |
| Storage        | limitado    | até 128 TB          |
| Failover       | mais lento  | mais rápido         |
| Arquitetura    | tradicional | cluster             |

---

# 1️⃣1️⃣ Aurora Serverless

Aurora possui modo **Serverless**.

Nesse modo:

* não precisa gerenciar instâncias
* capacidade escala automaticamente
* cobrança por uso

Ideal para:

* workloads variáveis
* aplicações event-driven
* ambientes de desenvolvimento

---

# 1️⃣2️⃣ Integrações importantes

Aurora integra facilmente com:

* AWS Lambda
* AWS DMS
* CloudWatch
* IAM
* Secrets Manager

Muito usado em arquiteturas **serverless e microservices**.

---

# 1️⃣3️⃣ Pegadinhas comuns na prova DVA

### Alta disponibilidade + leitura escalável

Use:

```
Aurora + Aurora Replicas
```

---

### Banco relacional com alta performance

Resposta geralmente:

```
Amazon Aurora
```

---

### Replicação automática entre AZs

Aurora já possui isso **nativamente**.

---

### Aplicação precisa escalar leitura

Use:

```
Reader Endpoint
```

---

# 1️⃣4️⃣ Resumo rápido para revisão

Aurora:

* 6 cópias de dados
* 3 AZs
* até **15 replicas**
* storage até **128 TB**
* failover automático
* reader endpoint para leitura

Arquitetura:

```
1 Writer
+ até 15 Readers
+ storage distribuído
```

---

# 🧠 Regra rápida para prova

```
Aurora = banco relacional
        + alta performance
        + replicação automática
        + escalabilidade
```

---

# 🔐 RDS & Aurora Security – AWS Developer Associate (DVA)

Segurança em **Amazon RDS** e **Amazon Aurora** envolve principalmente:

* Controle de acesso
* Criptografia
* Segurança de rede
* Gerenciamento de credenciais

Esses pontos aparecem frequentemente na prova **AWS Developer Associate**.

---

# 1️⃣ Segurança de Rede (VPC)

RDS e Aurora são executados dentro de uma **VPC**.

Controle de acesso acontece através de:

| Componente      | Função                        |
| --------------- | ----------------------------- |
| Security Groups | controlam acesso ao banco     |
| Subnets         | definem onde a instância roda |
| NACLs           | camada adicional de segurança |

📌 Regra importante para prova:

Banco normalmente deve estar em **subnets privadas**.

Arquitetura típica:

```id="vns8u4"
VPC
│
├── Public Subnet
│      └─ Application / Load Balancer
│
└── Private Subnet
       └─ RDS / Aurora
```

---

# 2️⃣ Security Groups

Security Groups controlam **quem pode conectar no banco**.

Exemplo:

| Porta | Banco                |
| ----- | -------------------- |
| 3306  | MySQL / Aurora MySQL |
| 5432  | PostgreSQL           |
| 1433  | SQL Server           |
| 1521  | Oracle               |

Regra comum:

```id="4frygo"
Allow inbound
source = Security Group da aplicação
port = database port
```

📌 Boa prática: **não liberar acesso público ao banco**.

---

# 3️⃣ IAM Database Authentication

RDS e Aurora podem usar **IAM Authentication**.

Isso permite conectar no banco usando **credenciais IAM ao invés de senha estática**.

Fluxo:

```id="osx97g"
Application
   │
   │ IAM token
   │
IAM Authentication
   │
   │
RDS / Aurora
```

Benefícios:

* não precisa armazenar senha
* autenticação temporária
* integração com IAM

Muito usado com:

* Lambda
* aplicações serverless

---

# 4️⃣ Encryption at Rest

RDS e Aurora suportam **criptografia em repouso**.

Usa:

```id="4rtjng"
AWS KMS
```

Criptografia cobre:

* storage
* snapshots
* read replicas
* backups

📌 Importante para prova:

Se o banco estiver criptografado:

* **read replicas também serão criptografadas**

---

# 5️⃣ Encryption in Transit

Dados podem ser criptografados **durante a comunicação**.

Usa:

```id="rbgup0"
SSL / TLS
```

Fluxo seguro:

```id="rd1vdi"
Application
   │
   │ TLS
   │
RDS / Aurora
```

Isso protege contra:

* sniffing de rede
* interceptação de dados

---

# 6️⃣ Gerenciamento de Senhas

Credenciais do banco podem ser armazenadas no:

| Serviço                             | Uso                  |
| ----------------------------------- | -------------------- |
| AWS Secrets Manager                 | armazenamento seguro |
| AWS Systems Manager Parameter Store | alternativa          |

Secrets Manager permite:

* rotação automática de senha
* integração com aplicações

Fluxo:

```id="khv72c"
Application
   │
   │ request secret
   │
Secrets Manager
   │
   │
RDS / Aurora
```

---

# 7️⃣ Auditoria e Monitoramento

Atividades do banco podem ser monitoradas usando:

| Serviço             | Função                    |
| ------------------- | ------------------------- |
| CloudWatch          | métricas e logs           |
| CloudTrail          | auditoria de chamadas API |
| Enhanced Monitoring | métricas detalhadas       |

Isso permite detectar:

* conexões suspeitas
* mudanças de configuração
* acessos administrativos

---

# 8️⃣ Database Activity Streams (Aurora)

Aurora possui recurso chamado:

```id="6q1l9x"
Database Activity Streams
```

Ele permite monitorar **atividades do banco em tempo real**.

Captura:

* queries
* logins
* operações de dados

Muito usado para **compliance e auditoria**.

---

# 9️⃣ Melhores práticas de segurança

Boas práticas recomendadas:

* usar **subnets privadas**
* restringir acesso via **Security Groups**
* habilitar **encryption at rest**
* usar **TLS**
* armazenar credenciais no **Secrets Manager**
* usar **IAM Authentication quando possível**

---

# 🔟 Pegadinhas comuns na prova DVA

### Aplicação não deve armazenar senha do banco

Use:

```id="t3s42x"
AWS Secrets Manager
```

---

### Banco precisa ser criptografado

Use:

```id="kklw5s"
KMS encryption
```

---

### Conexão segura com banco

Use:

```id="n0csap"
TLS / SSL
```

---

### Controle de acesso ao banco

Use:

```id="r3yv0c"
Security Groups
```

---

# 🧠 Resumo rápido para prova

Segurança em RDS / Aurora envolve:

* Security Groups
* KMS encryption
* TLS
* IAM Authentication
* Secrets Manager
* CloudWatch / CloudTrail

Arquitetura segura:

```id="yfrn8e"
Application
   │
   │ TLS
   │
Security Group
   │
   │
RDS / Aurora
(encrypted with KMS)
```

---

