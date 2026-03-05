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

