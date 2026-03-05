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

