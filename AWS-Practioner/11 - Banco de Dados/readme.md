
# 📘 README – Seção 14: Bancos de Dados (AWS Cloud Practitioner)

---

## 1️⃣ Conceitos de Banco de Dados

Banco de dados é um sistema que armazena, organiza e permite consultar dados.

Na AWS existem dois grandes modelos:

### 🔹 Relacional (SQL)

* Estrutura em tabelas
* Esquema definido
* Usa SQL
* Ideal para dados estruturados
* Suporte a transações (ACID)

Exemplo de uso:

* Sistemas financeiros
* ERPs
* Sistemas corporativos

---

### 🔹 Não Relacional (NoSQL)

* Estrutura flexível
* Alta escalabilidade
* Pode ser:

  * Chave-valor
  * Documento
  * Grafo

Ideal para:

* Aplicações web escaláveis
* Aplicações serverless
* Alto volume de dados

---

## 2️⃣ Amazon RDS

O **Amazon RDS (Relational Database Service)** é um serviço gerenciado de banco relacional.

A AWS cuida de:

* Provisionamento
* Backup automático
* Atualizações (patching)
* Monitoramento
* Recuperação em caso de falha

### Engines suportadas:

* MySQL
* PostgreSQL
* MariaDB
* Oracle
* SQL Server
* Amazon Aurora

### Recursos importantes:

* Multi-AZ → Alta disponibilidade
* Read Replicas → Escala de leitura
* Backups automáticos

📌 Muito importante para a prova:
RDS é usado quando você quer banco relacional gerenciado sem administrar infraestrutura.

---

## 3️⃣ Amazon Aurora

Amazon Aurora é uma engine relacional desenvolvida pela AWS.

Compatível com:

* MySQL
* PostgreSQL

Diferenças principais:

* Melhor performance que MySQL/PostgreSQL padrão
* Armazenamento distribuído automaticamente em múltiplas AZs
* Escalabilidade automática de storage
* Alta disponibilidade nativa

Aurora é mais escalável e performático que RDS tradicional.

📌 Na prova:
Aurora = opção de alto desempenho para banco relacional.

---

## 4️⃣ Amazon DynamoDB

DynamoDB é um banco NoSQL totalmente gerenciado.

Características:

* Modelo chave-valor ou documento
* Escalabilidade automática
* Baixa latência (milissegundos)
* Serverless

Estrutura:

* Tabela
* Partition Key (obrigatória)
* Sort Key (opcional)

Ideal para:

* Aplicações serverless
* Aplicações com alto volume de requisições
* Jogos, IoT, e-commerce

📌 Na prova:
DynamoDB = NoSQL totalmente gerenciado e altamente escalável.

---

## 5️⃣ Amazon ElastiCache

Serviço de cache em memória.

Suporta:

* Redis
* Memcached

Usado para:

* Reduzir latência
* Diminuir carga no banco principal
* Melhorar performance de aplicações

📌 Não é banco principal.
É usado para acelerar aplicações.

---

## 6️⃣ Amazon Neptune

Banco de dados de grafos.

Usado para:

* Redes sociais
* Sistemas de recomendação
* Detecção de fraude
* Relações complexas

Estrutura:

* Nós (nodes)
* Relações (edges)

📌 Quando a pergunta envolver “relacionamentos complexos”, pense em Neptune.

---

## 7️⃣ AWS Glue

Serviço de ETL (Extract, Transform, Load).

Função:

* Extrair dados
* Transformar dados
* Carregar dados

Usado para:

* Data Lakes
* Integração entre bancos
* Processamento analítico

É serverless.

---

# 🎯 Comparação Rápida (Importante para Prova)

| Serviço     | Tipo       | Uso Principal                     |
| ----------- | ---------- | --------------------------------- |
| RDS         | Relacional | Banco SQL gerenciado              |
| Aurora      | Relacional | Alta performance e escalabilidade |
| DynamoDB    | NoSQL      | Escala massiva e baixa latência   |
| ElastiCache | Cache      | Melhorar performance              |
| Neptune     | Grafo      | Relacionamentos complexos         |
| Glue        | ETL        | Integração e preparação de dados  |

---

# 🧠 O que mais cai na prova sobre Databases

* Diferença entre SQL e NoSQL
* RDS vs DynamoDB
* Quando usar Aurora
* O que é Multi-AZ
* O que é Read Replica
* Banco para alta performance e baixa latência → DynamoDB
* Banco para relacionamentos complexos → Neptune
* Serviço para ETL → Glue

---

# 📌 Resumo Final

A AWS oferece múltiplos tipos de bancos para diferentes cenários:

* RDS → Banco relacional gerenciado
* Aurora → Relacional de alta performance
* DynamoDB → NoSQL escalável e serverless
* ElastiCache → Cache para acelerar aplicações
* Neptune → Banco de grafos
* Glue → Integração e transformação de dados

Entender quando usar cada um é o ponto principal para a Cloud Practitioner.

---


