# 🌐 AWS VPC – Internet Gateway & NAT Gateway (DVA)

## 1️⃣ Amazon VPC (Virtual Private Cloud)

A **VPC** é uma rede virtual isolada dentro da AWS onde você executa seus recursos.

Principais componentes:

* **Subnets (Public / Private)**
* **Route Tables**
* **Internet Gateway**
* **NAT Gateway / NAT Instance**
* **Security Groups**
* **Network ACLs**

📌 **Ponto importante para prova:**
A VPC **não tem acesso à internet por padrão**.

---

# 2️⃣ Subnets (Public vs Private)

Uma **Subnet** é uma divisão da VPC.

## 🔓 Public Subnet

Uma subnet é **pública quando possui rota para o Internet Gateway**.

Exemplo de rota:

```
0.0.0.0/0 → Internet Gateway
```

Recursos comuns:

* EC2 públicas
* Load Balancers
* NAT Gateway
* Bastion Host

📌 **Importante para prova**

Uma instância só é pública se:

1. Está em **public subnet**
2. Possui **public IP**

---

## 🔒 Private Subnet

Uma subnet é **privada quando não possui rota direta para o Internet Gateway**.

Recursos comuns:

* Application servers
* Databases
* Internal services

📌 **Boa prática de arquitetura**

```
Public Subnet → Load Balancer
Private Subnet → Application Servers
Private Subnet → Databases
```

---

# 3️⃣ Internet Gateway (IGW)

O **Internet Gateway** permite comunicação entre a **VPC e a internet**.

Funções:

* Permite **entrada e saída de tráfego**
* É **altamente disponível**
* É **gerenciado pela AWS**

Arquitetura:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
EC2
```

📌 **Regra importante para prova**

Sem **Internet Gateway + Route Table**, a subnet **não tem internet**.

---

# 4️⃣ NAT Gateway

O **NAT Gateway** permite que **instâncias em subnets privadas acessem a internet**.

Mas **não permite conexões iniciadas da internet**.

Ou seja:

```
Private EC2 → Internet ✔
Internet → Private EC2 ❌
```

📌 **Uso comum**

Instâncias privadas precisam:

* baixar updates
* acessar APIs
* instalar pacotes

---

## Arquitetura NAT Gateway

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
NAT Gateway
   │
Private Subnet
   │
EC2
```

Fluxo:

1. EC2 privada envia requisição
2. Tráfego vai para **NAT Gateway**
3. NAT usa **Internet Gateway**
4. Resposta retorna

---

# 5️⃣ NAT Gateway vs NAT Instance

| Feature                | NAT Gateway | NAT Instance |
| ---------------------- | ----------- | ------------ |
| Gerenciado pela AWS    | ✅           | ❌            |
| Alta disponibilidade   | ✅           | ❌            |
| Escala automaticamente | ✅           | ❌            |
| Precisa gerenciar EC2  | ❌           | ✅            |

📌 **Para prova**

AWS **recomenda NAT Gateway**.

---

# 6️⃣ Regra importante para NAT Gateway

O **NAT Gateway deve estar em uma Public Subnet**.

Porque ele precisa acessar:

```
Internet Gateway
```

Arquitetura correta:

```
Public Subnet
   └── NAT Gateway

Private Subnet
   └── EC2 → Route → NAT Gateway
```

---

# 7️⃣ Route Tables

Controlam **para onde o tráfego da subnet vai**.

### Route Table da Public Subnet

```
0.0.0.0/0 → Internet Gateway
```

---

### Route Table da Private Subnet

```
0.0.0.0/0 → NAT Gateway
```

---

# 8️⃣ Fluxo completo da arquitetura

Arquitetura clássica usada na AWS:

```
              Internet
                  │
            Internet Gateway
                  │
        ┌──────────────────┐
        │   Public Subnet  │
        │  NAT Gateway     │
        │  Load Balancer   │
        └──────────────────┘
                  │
        ┌──────────────────┐
        │  Private Subnet  │
        │   EC2 Instances  │
        └──────────────────┘
```

---

# 🎯 Pontos que mais caem na prova DVA

### 1️⃣ Internet Gateway

Permite **internet para subnets públicas**.

---

### 2️⃣ NAT Gateway

Permite **internet para subnets privadas**.

---

### 3️⃣ Subnet pública

Tem rota:

```
0.0.0.0/0 → Internet Gateway
```

---

### 4️⃣ Subnet privada

Tem rota:

```
0.0.0.0/0 → NAT Gateway
```

---

### 5️⃣ NAT Gateway

* fica em **public subnet**
* usado por **private subnet**

---

# 🧠 Forma fácil de lembrar (para prova)

```
Public Subnet → Internet Gateway
Private Subnet → NAT Gateway → Internet Gateway
```

---

![img](https://github.com/DiegoLins10/AWS/blob/main/AWS-Developer/07%20-%20VPC%20Fundamentos/vpc.png)

---

# 🔐 NACL, Security Groups & VPC Flow Logs (AWS DVA)

## 1️⃣ Security Groups (SG)

**Security Groups são firewalls no nível da instância.**

Eles controlam **tráfego que entra e sai da EC2**.

📌 Características importantes:

* Funcionam no **nível da instância**
* São **stateful**
* Suportam apenas **ALLOW rules**
* Avaliam **todas as regras antes de decidir**

---

### Stateful (ponto importante da prova)

Se você permitir entrada, a resposta **é automaticamente permitida**.

Exemplo:

```text
Allow: HTTP (80) inbound
```

Resposta da EC2:

```text
Outbound automaticamente permitido
```

📌 Não precisa criar regra de retorno.

---

### Exemplo de Security Group

| Type | Port | Source    |
| ---- | ---- | --------- |
| HTTP | 80   | 0.0.0.0/0 |
| SSH  | 22   | My IP     |

---

### Security Groups podem referenciar outros SG

Muito comum em arquitetura.

Exemplo:

```text
Load Balancer SG → permite tráfego para → EC2 SG
```

---

# 2️⃣ Network ACL (NACL)

**NACL é um firewall no nível da subnet.**

Ele controla **tráfego que entra e sai da subnet inteira**.

📌 Características importantes:

* Funcionam no **nível da subnet**
* São **stateless**
* Suportam **ALLOW e DENY**
* Regras são avaliadas **em ordem numérica**

---

### Stateless (ponto de prova)

Para permitir comunicação você precisa:

* regra **inbound**
* regra **outbound**

Exemplo:

```text
Inbound: Allow 80
Outbound: Allow ephemeral ports
```

---

### Ordem das regras

As regras são avaliadas **do menor número para o maior**.

Exemplo:

| Rule | Type       | Action |
| ---- | ---------- | ------ |
| 100  | Allow HTTP | ALLOW  |
| 200  | Deny All   | DENY   |

📌 A primeira regra que bate **é aplicada**.

---

# 3️⃣ Security Group vs NACL

Tabela clássica de prova:

| Feature     | Security Group | NACL           |
| ----------- | -------------- | -------------- |
| Nível       | Instância      | Subnet         |
| Stateful    | ✅              | ❌              |
| Allow rules | ✅              | ✅              |
| Deny rules  | ❌              | ✅              |
| Avaliação   | Todas regras   | Ordem numérica |

📌 **Resumo para lembrar na prova**

```text
Security Group → Instance Firewall
NACL → Subnet Firewall
```

---

# 4️⃣ VPC Flow Logs

O **VPC Flow Logs** captura informações de tráfego de rede.

Pode registrar tráfego de:

* **VPC**
* **Subnet**
* **Network Interface (ENI)**

---

### Para onde os logs vão

Os logs podem ser enviados para:

* **CloudWatch Logs**
* **S3**

---

### O que ele registra

Exemplos de dados registrados:

* IP origem
* IP destino
* Porta
* Protocolo
* ACCEPT / REJECT
* quantidade de bytes

---

### Exemplo de registro

```text
srcaddr=10.0.1.5
dstaddr=52.95.110.1
action=ACCEPT
protocol=TCP
```

---

# 5️⃣ Uso comum na prova

Flow Logs ajudam a:

* diagnosticar **problemas de rede**
* verificar **tráfego bloqueado**
* auditoria de segurança

Exemplo clássico:

```text
EC2 não consegue acessar internet
→ verificar VPC Flow Logs
```

---

# 🎯 Pontos que mais caem na prova DVA

### 1️⃣ Security Groups

* firewall de **instância**
* **stateful**
* **apenas allow**

---

### 2️⃣ NACL

* firewall de **subnet**
* **stateless**
* **allow e deny**

---

### 3️⃣ VPC Flow Logs

Usado para **analisar tráfego de rede**.

---

# 🧠 Forma rápida de lembrar

```text
Security Group → Instance → Stateful

NACL → Subnet → Stateless

VPC Flow Logs → Monitorar tráfego
```

---


# 🌐 VPC Peering, Endpoints, VPN & Direct Connect (AWS DVA)

## 1️⃣ VPC Peering

**VPC Peering conecta duas VPCs diretamente usando a rede da AWS.**

Permite que recursos em duas VPCs se comuniquem **como se estivessem na mesma rede**.

📌 Características:

* tráfego **privado**
* usa **rede interna da AWS**
* baixa latência
* alta performance

---

### Arquitetura

```text
VPC A  ───── VPC Peering ───── VPC B
10.0.0.0/16                  172.31.0.0/16
```

EC2 em uma VPC pode acessar EC2 na outra usando **IP privado**.

---

### Regras importantes para prova

#### CIDR não pode sobrepor

```text
10.0.0.0/16
10.0.1.0/24 ❌
```

CIDRs precisam ser **diferentes**.

---

#### Não é transitivo

Se:

```text
VPC A ↔ VPC B
VPC B ↔ VPC C
```

Então:

```text
VPC A ❌ NÃO acessa VPC C
```

📌 Muito cobrado em prova.

---

#### Route tables precisam ser atualizadas

Você precisa adicionar rota:

```text
CIDR da outra VPC → VPC Peering Connection
```

---

# 2️⃣ VPC Endpoints

Permitem acessar **serviços da AWS sem usar internet**.

Tráfego fica **dentro da rede AWS**.

---

## Tipos de VPC Endpoint

### 1️⃣ Gateway Endpoint

Usado apenas para:

* **S3**
* **DynamoDB**

📌 Características:

* **gratuito**
* funciona via **route table**

Exemplo:

```text
Private EC2 → Gateway Endpoint → S3
```

Sem:

* NAT Gateway
* Internet Gateway

---

### 2️⃣ Interface Endpoint (PrivateLink)

Cria uma **ENI privada dentro da subnet**.

Permite acessar:

* serviços AWS
* serviços de terceiros
* serviços entre VPCs

Exemplo:

```text
EC2 → Interface Endpoint → AWS Service
```

---

### Exemplo de uso

EC2 privada precisa acessar **S3**:

Solução:

```text
Gateway Endpoint
```

---

# 3️⃣ AWS PrivateLink

O **PrivateLink usa Interface Endpoints**.

Permite expor serviços **privadamente entre VPCs**.

Arquitetura:

```text
Consumer VPC
     │
Interface Endpoint
     │
PrivateLink
     │
Service VPC (NLB)
```

📌 Muito usado para:

* SaaS
* microservices
* serviços entre contas AWS

---

# 4️⃣ Site-to-Site VPN

Conecta **datacenter on-premises com AWS**.

Usa **internet pública**, mas com **túnel criptografado**.

---

### Arquitetura

```text
On-Premise
    │
Customer Gateway
    │
VPN Tunnel
    │
Virtual Private Gateway
    │
VPC
```

---

### Características

* criptografado
* rápido de configurar
* mais barato que Direct Connect

📌 Porém depende da **internet pública**.

---

# 5️⃣ AWS Direct Connect (DX)

Conexão **dedicada entre datacenter e AWS**.

Não usa internet pública.

---

### Arquitetura

```text
On-Premise
    │
Direct Connect
    │
AWS Direct Connect Location
    │
VPC
```

---

### Características

* conexão privada
* baixa latência
* alta banda
* mais estável

📌 Muito usado por:

* bancos
* empresas grandes
* workloads críticos

---

# 6️⃣ VPN vs Direct Connect

| Feature          | VPN         | Direct Connect |
| ---------------- | ----------- | -------------- |
| Usa internet     | ✅           | ❌              |
| Conexão dedicada | ❌           | ✅              |
| Latência         | maior       | menor          |
| Custo            | mais barato | mais caro      |
| Setup            | rápido      | demorado       |

📌 Pergunta clássica de prova.

---

# 🎯 Cenários que caem muito na DVA

### EC2 privada precisa acessar S3

Resposta:

```text
Gateway Endpoint
```

---

### Conectar duas VPCs

Resposta:

```text
VPC Peering
```

---

### Conectar datacenter com AWS rápido

Resposta:

```text
VPN
```

---

### Conexão dedicada empresa → AWS

Resposta:

```text
Direct Connect
```

---

# 🧠 Resumo mental rápido (prova)

```text
VPC Peering → conectar VPCs

Gateway Endpoint → S3 / DynamoDB

Interface Endpoint → PrivateLink

VPN → conexão segura pela internet

Direct Connect → conexão dedicada
```

---


