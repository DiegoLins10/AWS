
# 🌐 Route 53 — DNS e Registros (DVA)

## 1️⃣ O que é DNS?

**DNS (Domain Name System)** traduz **nomes de domínio em endereços IP**.

Exemplo:

```
www.example.com → 142.250.184.78
```

Fluxo simplificado:

```
User request
↓
DNS resolve domain
↓
IP address returned
↓
Client connects to server
```

Sem DNS precisaríamos acessar sites usando IPs.

---

# 2️⃣ Amazon Route 53

O **Amazon Route 53** é o serviço de DNS da AWS.

Principais funções:

* 🌍 **DNS management**
* 🧭 **Domain registration**
* ❤️ **Health checks**
* ⚖️ **Traffic routing policies**

Ele permite controlar **como o tráfego é direcionado para seus recursos AWS**.

---

# 3️⃣ Registrar um domínio

Com Route 53 você pode:

* registrar domínios
* gerenciar DNS

Exemplo:

```
example.com
```

Após registrar, você cria uma **Hosted Zone**.

Dentro da Hosted Zone ficam os **DNS records**.

---

# 4️⃣ DNS Records

Records definem **para onde o domínio aponta**.

Exemplo:

```
example.com → IP
```

Tipos importantes para a prova:

* **A Record**
* **CNAME**
* **Alias (AWS)**

---

# 5️⃣ A Record

O **A record** aponta **diretamente para um endereço IP**.

Exemplo:

```
example.com → 54.210.100.10
```

DNS record:

```
example.com   A   54.210.100.10
```

Características:

✔ DNS padrão
✔ usado para servidores com IP fixo

---

# 6️⃣ CNAME Record

**CNAME (Canonical Name)** aponta **um domínio para outro domínio**.

Não aponta para IP.

Exemplo:

```
api.example.com → myapi.otherdomain.com
```

DNS:

```
api.example.com   CNAME   myapi.otherdomain.com
```

Fluxo:

```
api.example.com
↓
myapi.otherdomain.com
↓
IP address
```

⚠️ Limitação importante:

CNAME **não pode ser usado no root domain**.

Exemplo inválido:

```
example.com → CNAME → cloudfront.net
```

---

# 7️⃣ Alias Record (AWS)

**Alias record** é uma **extensão do Route 53**.

Ele permite apontar diretamente para **recursos AWS**.

Exemplos de serviços suportados:

* **Amazon CloudFront**
* **Elastic Load Balancing**
* **Amazon S3**
* **Amazon API Gateway**

Exemplo:

```
example.com → Alias → CloudFront
```

---

# 8️⃣ Por que Alias aparece como tipo A?

No Route 53 você verá:

```
Type: A
Alias: Yes
```

Isso acontece porque:

* Alias **retorna IPs como um A record**
* mas resolve automaticamente recursos AWS

Fluxo:

```
example.com
↓
Alias → CloudFront
↓
Route 53 resolve IPs
↓
Client recebe IP
```

Ou seja:

👉 **Alias funciona como um A record inteligente da AWS**.

---

# 9️⃣ TTL (Time To Live)

**TTL define quanto tempo um DNS record fica em cache**.

Exemplo:

```
TTL = 300 seconds
```

Durante esse tempo:

```
DNS result cached
```

Benefícios:

* menos consultas DNS
* melhor performance

Mas TTL alto pode causar:

* propagação lenta de mudanças.

---

# 🔟 Comparação rápida (muito cobrado na prova)

| Tipo  | Aponta para   | Root domain? | Uso                   |
| ----- | ------------- | ------------ | --------------------- |
| A     | IP            | ✔            | servidor com IP       |
| CNAME | outro domínio | ❌            | subdomínios           |
| Alias | recurso AWS   | ✔            | CloudFront / ELB / S3 |

---

# 🎯 Pegadinha comum da prova DVA

Pergunta típica:

> Você quer apontar **example.com** para uma distribuição **CloudFront**.

Opções:

A) CNAME
B) A record (Alias)
C) TXT
D) MX

Resposta correta:

👉 **A record (Alias)**

Motivos:

* CNAME **não funciona no root domain**
* Alias foi feito para **integração com serviços AWS**

---

# 🧠 Regra mental para a prova

Memorize:

```
A Record → IP
CNAME → outro domínio
Alias → recurso AWS
```

---

