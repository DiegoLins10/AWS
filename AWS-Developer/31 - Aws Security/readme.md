
# 🔐 Encryption (AWS) – Server-side vs Client-side

## 1. 🎯 Por que usar criptografia?

* Proteger dados **em repouso (at rest)**
* Garantir **confidencialidade**
* Atender **compliance (LGPD, etc.)**
* Reduzir impacto de vazamento de dados

---

## 2. 🖥️ Server-Side Encryption (SSE)

### 📌 Conceito

* Dados são **criptografados pelo serviço AWS (ex: S3)**
* A criptografia acontece **depois que o dado chega no servidor**
* O serviço **descriptografa automaticamente na leitura**

---

### 🔁 Fluxo

1. Cliente envia dado via HTTPS
2. AWS recebe o dado
3. AWS criptografa usando uma **data key**
4. Dado é armazenado criptografado
5. Na leitura → AWS descriptografa e retorna

---

### 🔑 Chaves

* Gerenciadas pela AWS ou pelo usuário (via AWS Key Management Service)
* O **servidor precisa ter acesso à chave**

---

### 🧠 Tipos importantes (prova!)

* **SSE-S3** → chave gerenciada pela AWS
* **SSE-KMS** → usa KMS (controle + audit) ⭐
* **SSE-C** → chave fornecida pelo cliente

---

### ✅ Vantagens

* Simples de usar
* Integrado com serviços AWS
* Menos responsabilidade do dev

---

### ❗ Pegadinha de prova

* ⚠️ AWS **consegue descriptografar** (pois tem acesso à chave)

---

## 3. 💻 Client-Side Encryption (CSE)

### 📌 Conceito

* Dados são criptografados **ANTES de sair do cliente**
* AWS **NUNCA vê o dado em plaintext**

---

### 🔁 Fluxo

1. Cliente criptografa usando sua chave
2. Envia dado já criptografado
3. AWS apenas **armazena (não entende o conteúdo)**
4. Outro cliente baixa
5. Cliente descriptografa localmente

---

### 🔑 Chaves

* Totalmente sob controle do cliente
* AWS **não tem acesso**

---

### 🧠 Pode usar

* **Envelope Encryption** (data key + master key via KMS)

---

### ✅ Vantagens

* Segurança máxima 🔐
* AWS não consegue ler os dados

---

### ❗ Desvantagens

* Mais complexo
* Você gerencia tudo (keys, rotação, etc.)

---

### ❗ Pegadinha de prova

* ⚠️ AWS **NÃO consegue descriptografar**
* ⚠️ Descriptografia acontece **no cliente**, não no servidor

---

## 4. ⚔️ Comparação (EXAME!)

| Feature             | Server-Side     | Client-Side |
| ------------------- | --------------- | ----------- |
| Onde criptografa    | AWS             | Cliente     |
| Onde descriptografa | AWS             | Cliente     |
| AWS acessa dados?   | ✅ Sim           | ❌ Não       |
| Complexidade        | Baixa           | Alta        |
| Controle das chaves | AWS/KMS/Cliente | Cliente     |
| Segurança máxima    | Média           | Alta        |

---

## 5. 🧠 Macete de prova

* **"AWS faz tudo" → Server-Side**
* **"Cliente criptografa antes de enviar" → Client-Side**
* **"AWS não pode ver os dados" → Client-Side**
* **"Menos esforço operacional" → Server-Side**
* **"Controle total da chave" → Client-Side**

---

## 6. 🎯 Quando usar cada um

### 👉 Use Server-Side

* Quando quer **simplicidade**
* Uso padrão (S3, EBS, RDS)
* Quando KMS já resolve

### 👉 Use Client-Side

* Quando precisa de **máxima segurança**
* Dados extremamente sensíveis
* Compliance exige que nem AWS veja os dados

---

