## 📘 README — Amazon CloudFront (AWS Certified Developer – DVA)

Resumo **direto para prova AWS Developer** sobre CloudFront baseado nos tópicos da seção que você estudou.
Foquei nas **coisas que realmente aparecem em questão de prova**.

---

# 1️⃣ O que é CloudFront

**CloudFront = CDN (Content Delivery Network)** da Amazon Web Services.

Ele **cacheia conteúdo em Edge Locations** próximas ao usuário.

### Fluxo

```
Client → CloudFront Edge → Origin
```

Se tiver no cache:

```
Client ← CloudFront (Cache Hit)
```

Se não tiver:

```
Client → CloudFront → Origin → CloudFront → Client
```

### Benefícios

* menor latência
* menos carga no backend
* melhor performance global
* proteção contra tráfego direto ao origin

---

# 2️⃣ Edge Locations

Edge locations são **datacenters distribuídos globalmente** onde o cache fica armazenado.

Usuário sempre conecta na **edge mais próxima**.

---

# 3️⃣ Origins

**Origin = servidor que possui o conteúdo original.**

Pode ser:

* Amazon S3
* Amazon EC2
* Elastic Load Balancing
* Amazon API Gateway
* servidor HTTP externo

---

# 4️⃣ Cache Behavior

Define **como CloudFront trata requisições**.

Cada behavior define:

* origin
* cache policy
* allowed HTTP methods
* viewer protocol policy
* TTL

Exemplo:

```
/images/* → S3 origin
/api/* → API Gateway origin
```

---

# 5️⃣ Cache Policy

Define **o que entra na cache key**.

Ou seja:

> **quais partes da requisição determinam objetos diferentes no cache**

Pode incluir:

* headers
* cookies
* query strings

### Exemplo

Se incluir query string:

```
/image.jpg?size=small
/image.jpg?size=large
```

CloudFront cria **dois objetos diferentes no cache**.

---

# 6️⃣ Cache Key

**Cache Key = identificador do objeto no cache.**

Se duas requisições tiverem a **mesma cache key**:

➡️ CloudFront retorna do cache.

Se forem diferentes:

➡️ CloudFront busca no origin.

---

# 7️⃣ Origin Request Policy

Define **o que CloudFront envia para o origin**.

Pode encaminhar:

* headers
* cookies
* query strings

⚠️ Importante para prova:

| Policy                | Função                     |
| --------------------- | -------------------------- |
| Cache Policy          | define cache key           |
| Origin Request Policy | define o que vai ao origin |

---

# 8️⃣ TTL (Time To Live)

Controla quanto tempo um objeto fica no cache.

Tipos:

| TTL         | Função       |
| ----------- | ------------ |
| Minimum TTL | tempo mínimo |
| Default TTL | tempo padrão |
| Maximum TTL | tempo máximo |

Após expirar → CloudFront consulta o origin novamente.

---

# 9️⃣ Cache Invalidation

Remove objetos do cache **antes do TTL expirar**.

Exemplo:

```
/index.html
/images/*
```

Pode ser feito via:

* console
* CLI
* SDK
* API

⚠️ prova DVA:

AWS recomenda **versioned object names** em vez de invalidations frequentes.

Exemplo:

```
app.v1.js
app.v2.js
```

---

# 🔟 ALB / EC2 como Origin

CloudFront pode usar backend dinâmico:

* Application Load Balancer
* Amazon EC2

Arquitetura comum:

```
Client
 ↓
CloudFront
 ↓
ALB
 ↓
EC2
```

---

# 1️⃣1️⃣ Geo Restriction

Permite **bloquear ou permitir acesso por país**.

Tipos:

* allowlist
* blocklist

Exemplo:

```
permitir apenas Brasil e EUA
```

---

# 1️⃣2️⃣ Signed URLs e Signed Cookies

Usados para **controlar acesso a conteúdo privado**.

### Signed URL

URL com assinatura criptográfica.

Exemplo:

```
https://cdn.site.com/video.mp4?signature=xyz
```

Usado para:

* downloads
* conteúdo premium
* arquivos privados

---

### Signed Cookies

Permitem acessar **múltiplos arquivos protegidos**.

Usado quando:

* usuário acessa vários arquivos
* streaming
* conteúdo de site privado

---

# 1️⃣3️⃣ Key Groups

Key Groups são usados para **verificar assinaturas das URLs ou cookies**.

Eles usam **public keys** para validar as assinaturas.

---

# 1️⃣4️⃣ Real-Time Logs

Permite visualizar logs do CloudFront **em tempo quase real**.

Podem ser enviados para:

* Amazon Kinesis Data Streams
* ferramentas de análise

Usado para:

* monitoramento
* debugging
* analytics

---

# 🧠 Arquiteturas que caem na prova

### Static website

```
Client
 ↓
CloudFront
 ↓
S3
```

---

### API global

```
Client
 ↓
CloudFront
 ↓
API Gateway
 ↓
Lambda
```

---

### Web app

```
Client
 ↓
CloudFront
 ↓
ALB
 ↓
EC2
```

---

# ⚠️ Pegadinhas clássicas da prova

### 1️⃣ Melhor forma de atualizar conteúdo frequentemente

Resposta:

✅ **Versioned object names**

não:

❌ invalidation constante

---

### 2️⃣ CloudFront envia resposta para quem?

Resposta:

✅ **Client**

mesmo quando busca do origin.

---

### 3️⃣ Cache Policy vs Origin Request Policy

| Política              | Função                           |
| --------------------- | -------------------------------- |
| Cache Policy          | controla cache key               |
| Origin Request Policy | controla o que vai para o origin |

---

# 🎯 Resumo final (para revisão rápida)

| Conceito              | Definição                   |
| --------------------- | --------------------------- |
| CloudFront            | CDN da AWS                  |
| Edge Location         | local onde cache fica       |
| Origin                | servidor do conteúdo        |
| Cache Key             | identifica objeto no cache  |
| Cache Policy          | define cache key            |
| Origin Request Policy | define o que vai ao origin  |
| TTL                   | tempo de cache              |
| Invalidation          | remover cache antes do TTL  |
| Signed URL            | acesso temporário a arquivo |
| Signed Cookies        | acesso a múltiplos arquivos |
| Geo Restriction       | bloqueio por país           |

---

