
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

Vou manter o **mesmo padrão de README que você está usando para estudar a DVA**, com **numeração contínua, comparações e foco em prova**.

---

# 🌐 Route 53 – Routing Policies (AWS DVA)

## 1️⃣ Simple Routing Policy

### 📌 Conceito

A **Simple Routing Policy** é o roteamento mais básico do **Amazon Web Services Route 53**.

Ela retorna **um único recurso** para o cliente.

### ⚙️ Características

* 1 domínio → 1 recurso
* Sem lógica de distribuição
* Sem controle de tráfego

### 📊 Exemplo

```
api.example.com → EC2
```

### ⚠️ Limitações (cai em prova)

* ❌ Não suporta **Health Checks**
* ❌ Não controla porcentagem de tráfego
* ❌ Não faz roteamento inteligente

### 🎯 Quando usar

* Aplicações simples
* Apenas um endpoint

---

# 2️⃣ Weighted Routing Policy

### 📌 Conceito

A **Weighted Routing Policy** distribui tráfego **com base em pesos**.

Você define quanto tráfego cada recurso recebe.

### ⚙️ Funcionamento

Exemplo:

| Endpoint | Peso |
| -------- | ---- |
| EC2-A    | 80   |
| EC2-B    | 20   |

Distribuição aproximada:

```
80% → EC2-A
20% → EC2-B
```

### 💡 Usos comuns

#### Canary Deployment

```
versão antiga → 90
nova versão → 10
```

#### A/B Testing

```
versão A → 50
versão B → 50
```

#### Migração gradual

Mover tráfego aos poucos.

### ❤️ Health Checks

Se habilitado:

```
endpoint com falha → removido do DNS
```

### 🎯 Quando usar

* Deploy gradual
* A/B testing
* Canary releases

---

# 3️⃣ Latency Routing Policy

### 📌 Conceito

A **Latency Routing Policy** envia o usuário para a **região AWS com menor latência**.

⚠️ Não é baseado em localização, e sim em **latência da rede**.

### ⚙️ Funcionamento

O Route 53 mede latência entre:

```
Usuário ↔ Região AWS
```

E escolhe a mais rápida.

### 📊 Exemplo

Infraestrutura:

```
us-east-1
eu-west-1
ap-southeast-1
```

Usuário no Brasil:

```
→ us-east-1
```

Usuário na Europa:

```
→ eu-west-1
```

### 🎯 Quando usar

* Aplicações globais
* SaaS multi-região
* Melhor experiência para usuários

---

# 4️⃣ Failover Routing Policy

### 📌 Conceito

A **Failover Routing Policy** implementa **alta disponibilidade (HA)**.

Existem dois endpoints:

```
Primary
Secondary (backup)
```

### ⚙️ Funcionamento

```
Usuário → Primary
```

Se falhar:

```
Usuário → Secondary
```

### ❤️ Health Checks (obrigatório)

O **Route 53 monitora o Primary**.

Se o health check falhar:

```
tráfego → Secondary
```

### 📊 Exemplo

```
Primary → ALB (us-east-1)
Secondary → ALB (us-west-2)
```

### 🎯 Quando usar

* Disaster recovery
* Alta disponibilidade
* Backup de infraestrutura

---

# 5️⃣ Geolocation Routing Policy

### 📌 Conceito

A **Geolocation Routing Policy** roteia tráfego **com base na localização do usuário**.

Baseado em:

* continente
* país
* estado

### ⚙️ Funcionamento

Exemplo:

```
Usuários do Brasil → servidor BR
Usuários da Europa → servidor EU
Usuários dos EUA → servidor US
```

### 📊 Exemplo

```
app.example.com
 → BR endpoint
 → EU endpoint
 → US endpoint
```

### ⚠️ Importante

Se nenhuma regra corresponder:

```
usar Default record
```

### 🎯 Quando usar

* Conteúdo regional
* Regras legais por país
* Sites multilíngues

---

# 6️⃣ Geoproximity Routing Policy

### 📌 Conceito

A **Geoproximity Routing Policy** roteia usuários **com base na proximidade geográfica** de um recurso.

Ela permite **expandir ou reduzir o alcance de uma região**.

⚠️ Requer **Traffic Flow**.

### ⚙️ Funcionamento

Exemplo:

```
Recurso em São Paulo
Recurso em Singapura
```

Usuários mais próximos da America do sul → SP
Usuários mais próximos da Asia → singapura

### 🔧 Bias (cai em prova)

Você pode ajustar **bias** para expandir área.

```
Bias positivo → aumenta área
Bias negativo → reduz área
```

![img](https://github.com/DiegoLins10/AWS/blob/main/AWS-Developer/06%20-%20Route%2053/geoproximity_map.png)

### 🎯 Quando usar

* Controle fino de distribuição geográfica
* Balanceamento global

---

# 7️⃣ Multi-Value Answer Routing Policy

### 📌 Conceito

Permite retornar **vários IPs saudáveis** para o cliente.

Funciona como **DNS-based load balancing simples**.

### ⚙️ Funcionamento

Route 53 retorna **até 8 registros saudáveis**.

Exemplo:

```
api.example.com
 → EC2-A
 → EC2-B
 → EC2-C
```

Se um falhar:

```
não aparece na resposta DNS
```

### ❤️ Health Checks

Cada endpoint pode ter **health check**. Apenas em endpoint publico é possivel utilizar o seja um alb.

### 🎯 Quando usar

* Load balancing simples
* Alta disponibilidade básica

⚠️ Não substitui **Elastic Load Balancer**.

---

# 📊 Comparação (MUITO cobrado)

| Policy       | Baseado em              | Uso                |
| ------------ | ----------------------- | ------------------ |
| Simple       | nenhum                  | DNS simples        |
| Weighted     | peso (%)                | deploy gradual     |
| Latency      | latência                | apps globais       |
| Failover     | health check            | disaster recovery  |
| Geolocation  | localização do usuário  | conteúdo regional  |
| Geoproximity | proximidade geográfica  | controle avançado  |
| Multi Value  | múltiplos IPs saudáveis | load balancing DNS |

---

# 🧠 Dica rápida para prova

| Se a questão falar em        | Resposta     |
| ---------------------------- | ------------ |
| Distribuir % de tráfego      | Weighted     |
| Região mais rápida           | Latency      |
| Backup automático            | Failover     |
| Conteúdo por país            | Geolocation  |
| Controle geográfico avançado | Geoproximity |
| Vários IPs com health check  | Multi Value  |

---

💡 **Resumo mental para prova**

```
Simple → 1 destino
Weighted → porcentagem
Latency → menor latência
Failover → backup
Geolocation → país
Geoproximity → proximidade
Multi Value → vários IPs
```

---


# 🌍 Route 53 + ALB + Health Checks (Arquitetura Multi-Region)

## 1️⃣ Limitação do Load Balancer

O **Application Load Balancer** é **regional**.

Ou seja:

```
ALB → funciona apenas dentro de uma região AWS
```

Exemplo:

```
ALB (us-east-1)
 → EC2
 → EC2
 → EC2
```

O ALB **balanceia tráfego apenas dentro da região**.

---

# 2️⃣ Papel do Route 53

O **Amazon Route 53** fica **acima das regiões** e decide **para qual região enviar o usuário**.

Arquitetura típica:

```
User
  ↓
Route53
  ↓
ALB us-east-1
ALB eu-west-1
```

### Regra importante

```
Route53 → escolhe a região
ALB → balanceia dentro da região
```

---

# 3️⃣ Health Checks (Diferença importante)

### Health Check do ALB

O ALB verifica **instâncias individuais**.

```
ALB
 ├ EC2 (healthy)
 ├ EC2 (unhealthy)
 └ EC2 (healthy)
```

Se uma falhar:

```
ALB para de enviar tráfego para ela
```

👉 Geralmente **não precisa de Route53 health check** nesse caso.

---

### Health Check do Route 53

O Route 53 verifica **o endpoint inteiro**.

Exemplo:

```
Route53
 ├ ALB us-east-1
 └ ALB eu-west-1
```

Se uma região falhar:

```
Route53 remove esse endpoint do DNS
```

---

# 4️⃣ Quando usar Health Check do Route 53

Use principalmente em:

### 🌎 Multi-Region Failover

```
Primary → ALB us-east-1
Secondary → ALB eu-west-1
```

Se a região primária falhar:

```
Route53 redireciona tráfego
```

---

# 5️⃣ Resumo para prova (DVA)

| Serviço              | Responsabilidade     |
| -------------------- | -------------------- |
| Route53              | escolhe região       |
| ALB                  | balanceia instâncias |
| Health check ALB     | verifica EC2         |
| Health check Route53 | verifica região      |

---

# 🧠 Regra mental para certificação

```
ALB → balanceamento regional
Route53 → balanceamento global
```

---



