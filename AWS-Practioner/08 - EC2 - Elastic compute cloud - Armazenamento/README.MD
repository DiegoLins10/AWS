# AWS Storage Services Overview

Este repositório contém uma visão geral dos principais serviços de armazenamento da Amazon Web Services (AWS): Amazon EBS, Amazon EFS e Amazon FSx. Cada um desses serviços é projetado para atender diferentes necessidades de armazenamento, desde blocos de dados de alta performance até sistemas de arquivos distribuídos e totalmente gerenciados.

---

## 📦 Amazon Elastic Block Store (EBS)

O **Amazon EBS** é um serviço de armazenamento em bloco de alto desempenho utilizado com instâncias do Amazon EC2. Ele é ideal para aplicações que exigem baixa latência de I/O, como bancos de dados.

### 🔹 Principais características:

- **Desempenho**: Oferece IOPS elevados e baixa latência, ideal para cargas de trabalho intensivas em leitura/escrita.
- **Durabilidade**: Volumes são replicados automaticamente dentro da zona de disponibilidade para alta disponibilidade.
- **Tipos de Volume**:
  - SSD: `gp2`, `gp3` (uso geral), `io1`, `io2` (alta performance)
  - HDD: `st1`, `sc1` (alto throughput)
- **Snapshots**: Backups armazenados no Amazon S3, podendo ser usados para restauração ou criação de novos volumes (ver seção abaixo).
- **Criptografia**: Suporte nativo via AWS KMS para volumes criptografados.
- **Integração AWS**: Compatível com IAM, CloudWatch, Snapshot Scheduler, entre outros.

---

## 📁 Amazon Elastic File System (EFS)

O **Amazon EFS** é um sistema de arquivos elástico, totalmente gerenciado, que permite o compartilhamento de arquivos entre múltiplas instâncias EC2.

### 🔹 Pontos principais:

- **Escalabilidade automática**: Ajusta-se dinamicamente de gigabytes a petabytes.
- **Alta disponibilidade e durabilidade**: Armazena arquivos em múltiplas zonas de disponibilidade.
- **Compartilhamento de arquivos**: Permite acesso simultâneo de diversas instâncias EC2.
- **Tipos de armazenamento**: 
  - `Standard`
  - `Infrequent Access (IA)` para otimização de custos.
- **Segurança**: Suporte à criptografia em trânsito e em repouso via AWS KMS.
- **Integração AWS**: Funciona com AWS Backup, IAM, CloudWatch, entre outros.

---

## 🗂️ Amazon FSx

O **Amazon FSx** fornece sistemas de arquivos completos e gerenciados para aplicações que exigem funcionalidades específicas de sistemas de arquivos tradicionais, como Windows File Server e Lustre.

### 🔹 Tipos disponíveis:

- **FSx para Windows File Server**:
  - Compatível nativamente com o Windows Server.
  - Suporte a SMB, NFS, deduplicação, ACLs e criptografia.
- **FSx para Lustre**:
  - Ideal para computação de alta performance (HPC), big data, machine learning e processamento de mídia.
  - Baixa latência e alta taxa de transferência.

### 🔹 Recursos adicionais:

- **Desempenho**: Otimizado para cargas exigentes.
- **Segurança**: Criptografia de dados, isolamento por VPC, suporte a ACLs.
- **Integração com AWS**: Compatível com IAM, CloudWatch, AWS Backup, entre outros.

---

## 📸 Snapshots na AWS

### 📌 O que são Snapshots?

**Snapshots** são cópias pontuais dos dados armazenados, usados como mecanismo de backup e recuperação.

### 🔹 Amazon EBS Snapshots

- Permitem criar uma cópia exata de um volume EBS.
- Armazenados no Amazon S3 de forma incremental (só armazenam as alterações desde o último snapshot).
- Podem ser usados para:
  - Criar novos volumes EBS.
  - Restaurar volumes corrompidos.
  - Clonar ambientes.
- Suporte a **Snapshot Lifecycle Policies** para automatizar backups.

### 🔹 Amazon EFS Snapshots

- Integrado com o **AWS Backup**, onde é possível agendar e gerenciar backups de sistemas de arquivos EFS.
- Os backups são armazenados separadamente do sistema de arquivos e podem ser restaurados conforme necessário.

### 🔹 Amazon FSx Snapshots

- Suporta snapshots manuais e automatizados para ambos os sistemas:
  - **FSx for Windows File Server**: snapshots são visíveis como pastas acessíveis dentro do sistema de arquivos.
  - **FSx for Lustre**: snapshots são usados principalmente para recuperação e replicação de dados.
- Integra-se com o **AWS Backup** para gerenciamento centralizado dos backups.

---

## ✅ Resumo

| Serviço | Tipo de Armazenamento | Ideal para | Compartilhamento | Snapshots | Escalável |
|--------|------------------------|------------|------------------|-----------|-----------|
| **EBS** | Bloco | Bancos de dados, apps de alta IOPS | ❌ | ✅ (Amazon S3) | Manual |
| **EFS** | Arquivo | Compartilhamento entre EC2, apps web | ✅ | ✅ (via AWS Backup) | Automático |
| **FSx** | Arquivo (Windows / Lustre) | Apps que dependem de sistemas de arquivos específicos | ✅ | ✅ | Manual / automático |

---

## 📚 Referências

- [Amazon EBS](https://aws.amazon.com/ebs/)
- [Amazon EFS](https://aws.amazon.com/efs/)
- [Amazon FSx](https://aws.amazon.com/fsx/)
- [AWS Backup](https://aws.amazon.com/backup/)
- [EBS Snapshots](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSSnapshots.html)
