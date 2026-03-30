# 🔐 AWS KMS — README PARA PROVA DVA-C02

## 1️⃣ O que é o KMS?

* Serviço gerenciado da AWS para **criação e controle de chaves criptográficas**
* Integrado com vários serviços (S3, EBS, RDS, Lambda…)
* Usa conceito de **Envelope Encryption**

---

## 2️⃣ 🔑 Tipos de Chaves no KMS

### 🔹 Symmetric Key (MAIS IMPORTANTE NA PROVA)

* **1 única chave** para criptografar e descriptografar
* Nunca sai do KMS
* Usada em **99% dos casos**
* Suporta:

  * Encrypt / Decrypt
  * GenerateDataKey

📌 **Cai MUITO na prova**

---

### 🔹 Asymmetric Key

* Par de chaves:

  * **Public Key → criptografa**
  * **Private Key → descriptografa**
* Usado quando:

  * Integração externa (fora AWS)
  * Assinaturas digitais

📌 Não suporta `GenerateDataKey`

---

## 3️⃣ 🧠 Envelope Encryption (CAI CERTO)

Fluxo:

1. KMS cria uma **DEK (Data Encryption Key)**
2. Dados são criptografados com a DEK
3. DEK é criptografada com a **CMK (KMS Key)**

📌 Resultado:

* Dados criptografados + DEK criptografada

---

## 4️⃣ 📌 APIs IMPORTANTES (CAI NA PROVA)

### 🔹 Encrypt

* Criptografa **até 4 KB**
* Usa diretamente a KMS Key

👉 Use para dados pequenos

---

### 🔹 Decrypt

* Descriptografa dados (até 4 KB)
* Também descriptografa DEKs

---

### 🔹 GenerateDataKey ⭐ (MUUUITO COBRADO)

Retorna:

* ✅ DEK em plaintext
* ✅ DEK criptografada (com KMS Key)

👉 Usado em:

* S3 client-side encryption
* Envelope encryption

---

### 🔹 GenerateDataKeyWithoutPlaintext

Retorna:

* ❌ NÃO retorna plaintext
* ✅ Apenas DEK criptografada

👉 Quando:

* Quer gerar chave para uso futuro
* Segurança maior (não expõe a chave)

---

### 🔹 GenerateRandom

* Retorna bytes aleatórios
* Usado para seeds, tokens, etc

---

## 5️⃣ 🔐 CMK vs DEK (CONFUSÃO CLÁSSICA)

| Tipo          | Uso                  |
| ------------- | -------------------- |
| CMK (KMS Key) | Criptografa DEK      |
| DEK           | Criptografa os dados |

📌 Regra:
👉 **Nunca use CMK direto para dados grandes**

---

## 6️⃣ 🔥 Limites IMPORTANTES

* Encrypt/Decrypt → **até 4 KB**
* Para dados maiores → usar **Envelope Encryption**

---

## 7️⃣ 🧩 Server-side vs Client-side

### 🔹 Server-side (AWS faz tudo)

* S3 SSE-KMS
* Mais simples

### 🔹 Client-side

* Você chama `GenerateDataKey`
* Criptografa localmente

📌 Prova:
👉 Client-side = AWS NÃO vê seus dados

---

## 8️⃣ 🔐 Key Policies vs IAM (PEGADINHA)

| Controle   | Função                      |
| ---------- | --------------------------- |
| Key Policy | Controle principal da chave |
| IAM Policy | Controle adicional          |

📌 Precisa dos dois para acessar KMS

---

## 9️⃣ 🔄 Rotation

* Automática (1x por ano)
* Apenas para **symmetric keys**

---

## 🔟 🧠 Grants (CAI!)

* Permissões temporárias
* Usado por serviços AWS
* Evita mexer na key policy

---

## 1️⃣1️⃣ ⚡ Integrações importantes

* S3 (SSE-KMS)
* EBS
* RDS
* Lambda (env vars encryption)
* Secrets Manager

---

## 1️⃣2️⃣ 🧠 Pegadinhas clássicas da prova

❗ KMS NÃO armazena dados
❗ KMS NÃO criptografa arquivos grandes diretamente
❗ `GenerateDataKey` retorna DUAS chaves
❗ Asymmetric NÃO usa DataKey
❗ Client-side = mais seguro (AWS não vê dados)
❗ Encrypt limite 4 KB

---

## 1️⃣3️⃣ 🧪 Quando usar cada um (RESUMÃO)

| Cenário            | Solução                         |
| ------------------ | ------------------------------- |
| Pequeno payload    | Encrypt                         |
| Arquivo grande     | GenerateDataKey                 |
| Alta segurança     | GenerateDataKeyWithoutPlaintext |
| Integração externa | Asymmetric                      |
| AWS gerenciando    | SSE-KMS                         |

---

## 🧠 RESUMO FINAL (ESTILO PROVA)

* Symmetric → padrão
* Asymmetric → casos específicos
* Envelope Encryption → chave da prova
* GenerateDataKey → mais importante
* Limite → 4 KB
* CMK ≠ DEK

---

Boa, isso aí é **EXATAMENTE uma pegadinha clássica da prova** 👇
Vou melhorar teu README com esses detalhes mais “nível prova” 🔥

---

# 🔐 AWS KMS — README DVA (VERSÃO AVANÇADA)

## 1️⃣ 📌 Regra de OURO (CAI MUITO)

❌ `Encrypt` → até **4 KB**
✅ `GenerateDataKey` → permite criptografar **dados > 4 KB**

👉 **Por quê?**

* `Encrypt` usa direto a KMS Key → limitado
* `GenerateDataKey` → você criptografa localmente → **sem limite prático**

📌 **Resumo de prova:**

> Arquivo grande → SEMPRE `GenerateDataKey`

---

## 2️⃣ 🔥 Fluxo REAL do GenerateDataKey (CAI!)

1. Chama `GenerateDataKey`
2. Recebe:

   * DEK plaintext
   * DEK criptografada
3. Usa DEK plaintext pra criptografar o arquivo
4. Descarta a plaintext
5. Salva:

   * arquivo criptografado
   * DEK criptografada

👉 Para ler depois:

* chama `Decrypt` → recupera DEK → descriptografa dados

---

## 3️⃣ ⚠️ GenerateDataKeyWithoutPlaintext (PEGADINHA)

👉 Diferença chave:

| API                             | Retorna plaintext? | Uso          |
| ------------------------------- | ------------------ | ------------ |
| GenerateDataKey                 | ✅ SIM              | uso imediato |
| GenerateDataKeyWithoutPlaintext | ❌ NÃO              | uso futuro   |

📌 Cenário clássico:

* Você quer **armazenar chave segura**
* Outro serviço vai descriptografar depois

---

## 4️⃣ 🔐 Encryption Context (CAI MUITO!)

* Par chave-valor adicional na criptografia
* Funciona como **"AAD" (Additional Authenticated Data)**

👉 Precisa ser igual no Decrypt

```json
{
  "user": "123",
  "app": "payment"
}
```

📌 Se mudar → ❌ falha no decrypt

👉 Usado para:

* segurança extra
* evitar uso indevido

---

## 5️⃣ 🔥 Alias vs Key ID

| Tipo   | Exemplo        |
| ------ | -------------- |
| Key ID | `1234abcd-...` |
| Alias  | `alias/my-key` |

👉 Alias = mais fácil de gerenciar

📌 Prova gosta:

> Use alias para evitar hardcode de key id

---

## 6️⃣ 🔄 ReEncrypt (CAI!)

* Recriptografa dados **sem expor plaintext**

👉 Exemplo:

* trocar chave KMS
* mover dados entre contas

---

## 7️⃣ 🔐 KMS + IAM (PEGADINHA FORTE)

Para usar KMS precisa:

✅ IAM Policy
✅ Key Policy

📌 Se faltar um → ❌ acesso negado

---

## 8️⃣ ⚡ KMS vs CloudHSM

| Serviço  | Característica                     |
| -------- | ---------------------------------- |
| KMS      | gerenciado                         |
| CloudHSM | controle total (hardware dedicado) |

📌 Prova:

> Alta compliance → CloudHSM

---

## 9️⃣ 🔥 Tipos de KMS Keys

| Tipo             | Descrição       |
| ---------------- | --------------- |
| AWS Managed      | criado pela AWS |
| Customer Managed | você controla   |
| AWS Owned        | invisível       |

📌 Customer Managed = mais controle (rotação, policy)

---

## 🔟 🧠 Multi-Region Keys (CAI!)

* Replica chave em várias regiões
* Mesmo ID lógico

👉 Usado para:

* DR
* baixa latência

---

## 1️⃣1️⃣ 🔐 Grants (muito importante)

* Permissão temporária
* Muito usado por:

  * S3
  * Lambda

📌 Evita alterar Key Policy

---

## 1️⃣2️⃣ 🔥 Erros clássicos da prova

❗ “KMS criptografa arquivos grandes diretamente” → ❌
❗ “GenerateDataKey retorna só 1 chave” → ❌
❗ “Encryption context é opcional no decrypt” → ❌
❗ “Asymmetric suporta DataKey” → ❌

---

## 1️⃣3️⃣ 🧠 Cenários (DECORAR)

### 📦 Arquivo grande (S3, backup, etc)

👉 `GenerateDataKey`

---

### 🔒 Pequeno payload (<4KB)

👉 `Encrypt`

---

### 🔐 Segurança máxima (sem plaintext)

👉 `GenerateDataKeyWithoutPlaintext`

---

### 🌍 Integração externa

👉 Asymmetric Key

---

### 🔄 Trocar chave sem expor dados

👉 `ReEncrypt`

---

## 🧠 RESUMÃO FINAL (PROVA)

* 4 KB → limite do Encrypt
* > 4 KB → DataKey
* DataKey → coração do KMS
* CMK protege DEK
* Encryption Context → validação extra
* IAM + Key Policy → obrigatório

---

Perfeito — isso é **normal**, KMS confunde mesmo pelos nomes 😅
Vou te dar um **mapa mental + macete de prova** pra nunca mais errar 👇

---

# 🧠 🔐 KMS — COMO DECORAR (SEM CONFUNDIR)

## 1️⃣ 🎯 Regra simples (DECORA ISSO)

| Nome                            | O que faz                  | Dica mental                        |
| ------------------------------- | -------------------------- | ---------------------------------- |
| Encrypt                         | Criptografa direto (≤ 4KB) | **Simples e pequeno**              |
| Decrypt                         | Descriptografa             | **Reverter**                       |
| GenerateDataKey                 | Cria chave + plaintext     | **USAR AGORA**                     |
| GenerateDataKeyWithoutPlaintext | Só chave criptografada     | **USAR DEPOIS**                    |
| GenerateRandom                  | Bytes aleatórios           | **Nada a ver com crypto de dados** |

---

## 2️⃣ 🧠 MACETE QUE CAI NA PROVA

### 👉 “DATA KEY = arquivo grande”

Sempre que ver:

* arquivo grande
* S3 upload
* criptografia manual
* performance

💥 resposta: **GenerateDataKey**

---

### 👉 “WITHOUT PLAINTEXT = segurança máxima”

* não quer expor chave
* uso futuro
* outro serviço vai usar

💥 resposta: **GenerateDataKeyWithoutPlaintext**

---

### 👉 “Encrypt = pequeno e direto”

* payload pequeno
* token, senha curta

💥 resposta: **Encrypt**

---

## 3️⃣ 🔥 COMO DIFERENCIAR NA PROVA (RÁPIDO)

Pergunta fala:

### 📦 "arquivo grande"

👉 GenerateDataKey

---

### 🔒 "AWS não pode ver o dado"

👉 Client-side + GenerateDataKey

---

### 🕒 "usar chave depois"

👉 GenerateDataKeyWithoutPlaintext

---

### ⚡ "até 4KB"

👉 Encrypt

---

## 4️⃣ 🧠 HISTORINHA (FIXAÇÃO RÁPIDA)

Imagina:

👨‍💻 Você vai criptografar um arquivo grande:

1. Você pede pro KMS:
   👉 **GenerateDataKey**

2. Ele te dá:

* 🔓 chave aberta (usa agora)
* 🔒 chave fechada (guarda)

3. Você:

* criptografa o arquivo
* joga fora a chave aberta

📌 Isso é **Envelope Encryption**

---

## 5️⃣ ⚠️ PEGADINHAS QUE DERRUBAM

❗ “Encrypt arquivo grande” → ❌ errado
❗ “DataKey só retorna 1 chave” → ❌
❗ “WithoutPlaintext dá plaintext” → ❌

---

## 6️⃣ 🧠 RESUMO FINAL (DECORA ISSO)

```
≤ 4KB → Encrypt  
> 4KB → GenerateDataKey  
futuro → WithoutPlaintext  
```

---

Boa — isso **cai direto na prova** e tem pegadinha 👇

---

# 🔄 🔐 KMS Key Rotation (quando as chaves giram)

## 1️⃣ 📅 Automatic Rotation

* Acontece **automaticamente a cada 1 ano (365 dias)**
* Só para:
  ✅ **Symmetric Customer Managed Keys**

📌 NÃO funciona para:

* ❌ Asymmetric keys
* ❌ AWS Managed (você não controla)

---

## 2️⃣ 🎯 Importante (PEGADINHA)

👉 Quando a chave gira:

* ❌ **ID da chave NÃO muda**
* ❌ **ARN NÃO muda**
* ❌ **Alias NÃO muda**

✅ Apenas o **material criptográfico por trás muda**

---

## 3️⃣ 🧠 Impacto na prática

* Dados antigos continuam funcionando ✅
* KMS sabe qual versão da chave usar
* Não precisa recriptografar nada

---

## 4️⃣ 🔄 Rotation manual

Você pode:

👉 Criar uma nova chave + usar `ReEncrypt`

📌 Usado quando:

* compliance forte
* troca de chave urgente

---

## 5️⃣ 🔥 RESUMO DE PROVA

* Rotation automática → **1x por ano**
* Só → **symmetric CMK**
* Não muda → **ID / ARN / Alias**
* Transparente → **dados continuam acessíveis**

---

## 🧠 MACETE

> “KMS troca o motor, não troca o carro”

---


