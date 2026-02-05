
# 📘 AWS Developer Associate — EC2 Instance Storage (Seção 6)

Este documento reúne anotações e conceitos essenciais sobre **armazenamento em instâncias EC2**, com foco na prova **AWS Certified Developer – Associate**.

---

## 📌 1. Amazon EBS (Elastic Block Store) — Overview

O **Amazon EBS** fornece **volumes de armazenamento em bloco** para instâncias EC2.

### 🔹 Características principais

* Armazenamento **persistente**
* Dados **sobrevivem ao stop/start da instância**
* Vinculado a **uma AZ**
* Pode ser **anexado/desanexado** de instâncias
* Ideal para:

  * Bancos de dados
  * Sistemas de arquivos
  * Aplicações stateful

### 🔹 Conceitos importantes

* **Volume ≠ Instância**
* Pode ser usado como **root volume**
* Performance depende do **tipo do volume**

---

## 🛠️ 2. EBS — Hands On (Prática)

### Operações comuns:

* Criar volume EBS
* Anexar a uma instância EC2
* Montar no sistema operacional (`/dev/xvdf`, `/mnt/data`)
* Formatá-lo (`mkfs`)
* Persistir montagem no `/etc/fstab`

💡 **Na prova**: saber que EBS **não monta automaticamente**, isso é responsabilidade do SO.

---

## 📸 3. EBS Snapshots

Snapshots são **backups incrementais** de volumes EBS.

### 🔹 Características

* Armazenados no **Amazon S3 (gerenciado pela AWS)**
* Incrementais após o primeiro snapshot
* Podem ser usados para:

  * Criar novos volumes
  * Criar AMIs
* Podem ser **copiados entre regiões**

### 🔹 Segurança

* Suportam **criptografia**
* Snapshots criptografados → volumes criptografados

---

## 🛠️ 4. EBS Snapshots — Hands On

### Fluxo típico:

1. Criar snapshot de um volume
2. Criar novo volume a partir do snapshot
3. Anexar o volume a outra instância

💡 **Pegadinha de prova**: snapshot **não é em tempo real**, pode haver inconsistência se o volume estiver em uso (ideal parar ou usar flush).

---

## 🖼️ 5. AMI (Amazon Machine Image) — Overview

Uma **AMI** é um template para criar instâncias EC2.

### Contém:

* Sistema operacional
* Aplicações
* Configurações
* Volumes EBS (via snapshot)

### Tipos:

* AMIs públicas
* AMIs privadas
* AMIs do Marketplace

💡 Criar uma AMI = criar snapshots automaticamente.

---

## 🛠️ 6. AMI — Hands On

### Usos comuns:

* Escalar aplicações
* Padronizar ambientes
* Deploy rápido

💡 **Na prova**:
Para **replicar uma instância com tudo configurado**, a resposta geralmente é **AMI**, não snapshot manual.

---

## 💽 7. EC2 Instance Store

Armazenamento **temporário**, fisicamente conectado ao host.

### 🔹 Características

* Altíssima performance
* **Dados são perdidos** quando:

  * Instância é parada
  * Instância é encerrada
* Não pode ser desacoplado

### Casos de uso:

* Cache
* Buffer temporário
* Dados descartáveis

💡 **Nunca usar para dados críticos**.

---

## 🧱 8. Tipos de Volumes EBS

| Tipo      | Uso principal                   |
| --------- | ------------------------------- |
| gp3       | Uso geral (default recomendado) |
| gp2       | Uso geral (mais antigo)         |
| io1 / io2 | Alto IOPS (banco de dados)      |
| st1       | Throughput (big data, logs)     |
| sc1       | Baixo custo (dados frios)       |

💡 **Na prova**:

* Banco de dados → `io2`
* Uso geral → `gp3`

---

## 🔗 9. EBS Multi-Attach

Permite **anexar um volume EBS a múltiplas instâncias**.

### Restrições:

* Apenas volumes `io1` ou `io2`
* Todas as instâncias devem estar na **mesma AZ**
* Requer sistema de arquivos cluster-aware

💡 **Pegadinha**: Não funciona com `gp2/gp3`.

---

## 📂 10. Amazon EFS (Elastic File System)

Sistema de arquivos **NFS gerenciado**, compartilhado.

### 🔹 Características

* Pode ser montado em **múltiplas instâncias EC2**
* Multi-AZ
* Escala automaticamente
* Ideal para:

  * Containers
  * Microserviços
  * Conteúdo compartilhado

💡 **EFS ≠ EBS**

* EBS → bloco
* EFS → arquivo

---

## 🛠️ 11. Amazon EFS — Hands On

### Passos comuns:

1. Criar EFS
2. Criar mount targets
3. Ajustar Security Groups
4. Montar via NFS (`mount -t nfs4`)

💡 **Na prova**:
Aplicação compartilhando arquivos entre instâncias → **EFS**.

---

## ⚖️ 12. EFS vs EBS

| Característica  | EBS                     | EFS                    |
| --------------- | ----------------------- | ---------------------- |
| Tipo            | Block                   | File                   |
| Multi-instância | ❌ (exceto Multi-Attach) | ✅                      |
| Performance     | Alta                    | Variável               |
| AZ              | Única                   | Multi-AZ               |
| Caso de uso     | DB, SO                  | Conteúdo compartilhado |

---

## 🧹 13. Limpeza (Cleanup)

Boas práticas:

* Excluir volumes não usados
* Apagar snapshots antigos
* Remover AMIs obsoletas
* Evitar custos desnecessários 💸

---

## 🎯 Dicas finais para a prova

✔ EBS é **persistente**
✔ Instance Store é **efêmero**
✔ Snapshot ≠ Backup em tempo real
✔ AMI = snapshot + metadata
✔ EFS = compartilhamento entre EC2
✔ Multi-Attach é raro e limitado

---
