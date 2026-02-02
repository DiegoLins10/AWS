# 📘 README — EC2 Fundamentals (AWS Developer Associate)

Este documento resume os conceitos fundamentais de **Amazon EC2**, cobrindo criação de instâncias, tipos, segurança, acesso SSH, roles e modelos de cobrança — exatamente no nível exigido na **certificação AWS Developer**.

---

## 1️⃣ AWS Budget Setup

### 📌 O que é

* Serviço para **monitorar custos**
* Permite criar **alertas** por:

  * valor gasto
  * uso de serviço
  * previsão de custo

### ⚠️ Dica de prova

* **Budgets ≠ bloquear recursos**
* Ele **alerta**, mas **não impede gastos**

---

## 2️⃣ EC2 Basics

### 📌 Conceitos principais

* EC2 = **máquina virtual na AWS**
* Componentes básicos:

  * AMI (imagem)
  * Instance Type
  * Security Group
  * Key Pair
  * Storage (EBS)

### ⚠️ Dica de prova

* EC2 é **IaaS**
* Você gerencia:

  * SO
  * patches
  * aplicação

---

## 3️⃣ EC2 com User Data (Hands On)

### 📌 User Data

* Script executado **na primeira inicialização**
* Muito usado para:

  * instalar pacotes
  * subir app
  * configurar servidor web

Exemplo típico:

```bash
#!/bin/bash
yum install httpd -y
systemctl start httpd
```

### ⚠️ Dica de prova

* User Data roda **uma vez**, no boot inicial
* Para automação contínua → **AMI ou Auto Scaling**

---

## 4️⃣ EC2 Instance Types Basics

### 📌 Famílias principais

* **t / t3 / t4g** → uso geral (burst)
* **m** → balanceado
* **c** → compute
* **r / x** → memória
* **g / p** → GPU

### ⚠️ Dica de prova

* `t` usa **CPU burst**
* Créditos de CPU importam ⚠️

---

## 5️⃣ Security Groups & Portas Clássicas

### 📌 O que são

* Firewall **stateful**
* Controla **inbound** e **outbound**

### 🔐 Portas mais cobradas

| Porta | Serviço    |
| ----- | ---------- |
| 22    | SSH        |
| 80    | HTTP       |
| 443   | HTTPS      |
| 3306  | MySQL      |
| 5432  | PostgreSQL |

### ⚠️ Dica de prova

* Security Group:

  * **permite** regras
  * **não bloqueia explicitamente**
* Stateful: resposta automática liberada

---

Boa — esse ponto é **muito cobrado em prova**, então vamos deixar **redondinho** 👌
Segue o trecho **completado**, já no formato de README pra você colar direto.

---

## 6️⃣ Security Groups (Hands On)

### 📌 Pontos importantes

* Associado à **instância** (ou ENI)
* Pode ser reutilizado em várias instâncias
* Regras podem referenciar **outros Security Groups**
* Atua como **firewall stateful** (se entrou, a resposta sai automaticamente)

---

### 🔽 Inbound Rules (Entrada)

👉 **Define o que PODE ENTRAR na instância**

Exemplos comuns:

* Porta **22** → SSH (admin)
* Porta **80** → HTTP
* Porta **443** → HTTPS
* Porta **3306** → MySQL

📌 Você controla:

* Porta
* Protocolo
* Origem (IP, range CIDR ou outro SG)

---

### 🔼 Outbound Rules (Saída)

👉 **Define para onde a instância PODE SAIR**

Padrão AWS:

* **All traffic → 0.0.0.0/0** (libera tudo)

Usado para:

* Acessar internet
* Chamar APIs
* Conectar em banco, S3, outros serviços

---

### ⚠️ Pontos IMPORTANTES pra prova

* Security Group:

  * ❌ **Não bloqueia** explicitamente
  * ✅ Só permite tráfego
* Se **inbound** permitir, o **retorno é automático** (stateful)
* Se não tem regra inbound → **nada entra**
* **Outbound bloqueado** pode quebrar app sem erro óbvio

---

### 🧠 Frase pra decorar

> **Inbound = quem entra**
> **Outbound = para onde sai**
> **SG é stateful e só permite**

---

## 7️⃣ SSH Overview

### 📌 Conceito

* Protocolo para acesso remoto seguro
* Usa **par de chaves**

  * pública (AWS)
  * privada (local)

### ⚠️ Dica de prova

* Perdeu a chave privada?

  * Não dá pra baixar de novo ❌

---

## 8️⃣ SSH usando Linux ou Mac

### 📌 Comando padrão

```bash
ssh -i chave.pem ec2-user@IP_PUBLICO
```

### ⚠️ Dica de prova

* Permissão da chave:

```bash
chmod 400 chave.pem
```

---

## 9️⃣ SSH usando Windows

### 📌 Opções

* PuTTY
* OpenSSH (Windows 10+)

### ⚠️ Dica de prova

* PuTTY usa `.ppk`
* AWS fornece `.pem`

---

## 🔟 SSH no Windows 10

### 📌 Vantagem

* SSH nativo no terminal
* Mesmo comando do Linux/Mac

### ⚠️ Dica de prova

* Menos conversão de chave
* Mais simples hoje em dia

---

## 1️⃣1️⃣ SSH Troubleshooting

### ❌ Problemas comuns

* Porta 22 bloqueada no SG
* IP errado
* Usuário errado (`ec2-user`, `ubuntu`)
* Permissão da chave incorreta

### ⚠️ Dica de prova

* **90% dos erros = Security Group**

---

## 1️⃣2️⃣ EC2 Instance Connect

### 📌 O que é

* Acesso SSH via **console AWS**
* Injeta chave temporária

### ⚠️ Limitações

* Precisa:

  * porta 22 aberta
  * instância compatível
* Não funciona em todos os cenários

---

## 1️⃣3️⃣ EC2 Instance Roles (Demo)

### 📌 Conceito CRÍTICO

* Role = **permissão IAM para EC2**
* Evita usar:

  * Access Key
  * Secret Key

### ⚠️ Dica de prova 🔥🔥🔥

> **Nunca** usar credenciais hardcoded
> **Sempre** usar **IAM Role**

---

## 1️⃣4️⃣ EC2 Purchasing Options

### 📌 Tipos

* **On-Demand** → flexível, caro
* **Reserved Instance** → contrato (1 ou 3 anos)
* **Savings Plans** → mais flexível que RI
* **Spot** → barato, pode ser interrompido
* **Dedicated Host / Instance** → compliance

### ⚠️ Dica de prova

* Trabalho crítico → On-Demand
* Batch / tolera interrupção → Spot
* Licença por core → Dedicated Host

---

## 🧠 RESUMO FINAL PRA PROVA

* EC2 = IaaS
* Security Group é **stateful**
* SSH = porta 22
* User Data roda no **primeiro boot**
* **IAM Role > Access Key**
* Spot pode ser interrompido
* Budget **alerta**, não bloqueia

---

Se quiser, no próximo passo eu posso:

* 🔥 Criar **questões estilo prova** só desse conteúdo
* 🧠 Fazer um **mapa mental**
* 📄 Juntar isso com **ECS / IAM / DynamoDB** num README único pra revisão final
