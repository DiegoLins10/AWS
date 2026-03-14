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

![]()

