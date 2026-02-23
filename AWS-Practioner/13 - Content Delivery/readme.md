
# 📘 README – Seção 16: Content Delivery (AWS Cloud Practitioner)

---

## 1️⃣ Sobre Route 53

Amazon Route 53 é o serviço de DNS da AWS.

Função:

* Traduz nomes de domínio (ex: [www.site.com](http://www.site.com)) em endereços IP.
* Pode registrar domínios.
* Pode direcionar tráfego para recursos AWS ou externos.

Características:

* Alta disponibilidade
* Escalável
* Global

📌 Para a prova:
Route 53 = DNS gerenciado da AWS.

---

## 2️⃣ Route 53 Policies (Políticas de Roteamento)

As políticas definem como o tráfego será direcionado.

Principais tipos:

### 🔹 Simple Routing

Encaminha para um único recurso.

### 🔹 Weighted Routing

Distribui tráfego por porcentagem.
Ex: 80% para servidor A, 20% para servidor B.

### 🔹 Latency-Based Routing

Direciona para a região com menor latência.

### 🔹 Failover Routing

Redireciona para backup caso o principal falhe.

### 🔹 Geolocation Routing

Direciona baseado na localização do usuário.

📌 Muito cobrado:
Failover + Health Check.

---

## 3️⃣ Configurando Route 53

Para configurar:

1. Registrar ou usar um domínio.
2. Criar Hosted Zone.
3. Criar registros (A, AAAA, CNAME, etc.).
4. Escolher política de roteamento.
5. (Opcional) Configurar Health Checks.

Route 53 pode apontar para:

* EC2
* Load Balancer
* S3
* CloudFront
* Recursos externos

---

## 4️⃣ Sobre AWS CloudFront

CloudFront é o CDN (Content Delivery Network) da AWS.

Função:

* Distribuir conteúdo globalmente
* Reduzir latência
* Melhorar performance

Funciona com:

* Edge Locations espalhadas pelo mundo

Pode distribuir:

* Conteúdo estático (imagens, CSS, JS)
* Conteúdo dinâmico
* APIs

📌 Na prova:
CloudFront = reduzir latência e melhorar performance global.

---

## 5️⃣ S3 Transfer Acceleration

Acelera upload de arquivos para o S3.

Funciona usando:

* Infraestrutura global da AWS
* Edge Locations

Indicado quando:

* Uploads são feitos de locais distantes da região do bucket.

📌 Diferença importante:
CloudFront → entrega conteúdo
Transfer Acceleration → acelera upload para S3

---

## 6️⃣ AWS Global Accelerator

Melhora disponibilidade e performance de aplicações globais.

Funciona:

* Direcionando tráfego pela rede privada da AWS
* Usando Anycast IP fixo

Benefícios:

* Melhor performance
* Failover automático
* IP fixo global

📌 Diferença importante para prova:

| Serviço               | Função                          |
| --------------------- | ------------------------------- |
| Route 53              | DNS                             |
| CloudFront            | CDN                             |
| Transfer Acceleration | Upload rápido para S3           |
| Global Accelerator    | Acelerar aplicações com IP fixo |

---

# 🎯 O que mais cai na prova

* Diferença entre Route 53 e CloudFront
* Política de Failover
* Latency-based routing
* CloudFront reduz latência usando Edge Locations
* Global Accelerator melhora performance usando rede privada da AWS

---

# 📌 Resumo Final

* Route 53 → DNS e roteamento inteligente
* CloudFront → CDN global
* S3 Transfer Acceleration → upload mais rápido
* Global Accelerator → melhora performance e disponibilidade com IP fixo global

---
