# 📘 README – Seção 13: Armazenamento S3 (AWS Cloud Practitioner)

---

# 1️⃣ Sobre o S3

O Amazon S3 (Simple Storage Service) é um serviço de armazenamento de objetos da AWS.

Ele permite armazenar:

* Arquivos
* Imagens
* Vídeos
* Backups
* Logs
* Dados estáticos

📌 Características principais:

* Armazenamento de objetos (não é bloco nem arquivo tradicional)
* Alta durabilidade (11 9’s – 99,999999999%)
* Escalabilidade automática
* Acesso via internet

Estrutura:

* Bucket → container de objetos
* Objeto → arquivo + metadados
* Key → nome/caminho do objeto

---

# 2️⃣ Criando uma Bucket

Bucket é o container onde os objetos ficam armazenados.

Regras importantes:

* Nome deve ser globalmente único
* Escolher a região ao criar
* Pode configurar:

  * Versionamento
  * Criptografia
  * Políticas de acesso
  * Bloqueio de acesso público

Boas práticas:

* Bloquear acesso público por padrão
* Definir políticas corretamente

---

# 3️⃣ Classes do S3

As classes definem custo e frequência de acesso.

## 🔹 S3 Standard

* Acesso frequente
* Alta disponibilidade

## 🔹 S3 Standard-IA

* Acesso infrequente
* Custo menor de armazenamento
* Custo por recuperação

## 🔹 S3 One Zone-IA

* Armazenado em uma única AZ
* Mais barato
* Menor resiliência

## 🔹 S3 Glacier

* Arquivamento
* Recuperação lenta
* Custo muito baixo

## 🔹 S3 Glacier Deep Archive

* Arquivamento de longo prazo
* Custo mais baixo
* Recuperação mais demorada

---

# 4️⃣ Valores do S3

A cobrança do S3 é baseada em:

* Armazenamento (GB por mês)
* Requisições (GET, PUT, etc.)
* Transferência de dados
* Recuperação (em classes IA/Glacier)

Modelo pay-as-you-go.

---

# 5️⃣ Hospedando um site em S3

O S3 pode hospedar sites estáticos (HTML, CSS, JS).

Requisitos:

* Habilitar Static Website Hosting
* Configurar arquivo index.html
* Ajustar permissões públicas (ou usar CloudFront)

Indicado para:

* Landing pages
* Portfólios
* Sites estáticos simples

---

# 6️⃣ Habilitando Versionamento

Versionamento permite manter múltiplas versões do mesmo objeto.

Benefícios:

* Recuperar arquivos apagados
* Proteger contra sobrescritas acidentais
* Suporte a replicação

Uma vez habilitado, não pode ser desativado (apenas suspenso).

---

# 7️⃣ Replicação de Buckets

Permite copiar objetos automaticamente para outro bucket.

Tipos:

* CRR (Cross-Region Replication) → entre regiões
* SRR (Same-Region Replication) → mesma região

Requisitos:

* Versionamento habilitado
* Permissões adequadas

Objetivo:

* Disaster recovery
* Compliance
* Baixa latência

---

# ️⃣ Sobre Criptografia S3

O S3 suporta criptografia em repouso:

## 🔹 SSE-S3

Criptografia gerenciada pela AWS.

## 🔹 SSE-KMS

Criptografia com AWS KMS (controle de chave).

## 🔹 SSE-C

Cliente fornece a chave.

Também suporta criptografia em trânsito via HTTPS.

---

# 9️⃣ Sobre Storage Gateway

AWS Storage Gateway conecta ambiente on-premise à AWS.

Permite:

* Backup na nuvem
* Integração híbrida
* Armazenamento local com sincronização no S3

Modos comuns:

* File Gateway
* Volume Gateway
* Tape Gateway

---

# 90️⃣ A família Snow da AWS

Serviços para transferir grandes volumes de dados fisicamente.

## 🔹 Snowcone

Pequeno e portátil.

## 🔹 Snowball

Transferência de grandes volumes.

## 🔹 Snowmobile

Transferência em escala extrema (petabytes/exabytes).

Usado quando:

* Internet é lenta
* Volume de dados é muito grande

---

# 🎯 Resumo Final

S3 é armazenamento de objetos altamente durável e escalável.

Principais pontos:

* Buckets armazenam objetos
* Possui múltiplas classes de armazenamento
* Suporta versionamento e replicação
* Permite hospedagem de site estático
* Possui criptografia integrada
* Integra com Storage Gateway
* Snow Family é usada para migração física de grandes dados

---

