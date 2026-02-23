
# 📘 README – Seção 15: Rede (AWS Cloud Practitioner)

---

## 1️⃣ Sobre VPC

VPC (Virtual Private Cloud) é uma rede virtual isolada dentro da AWS.

Ela permite que você:

* Crie sua própria rede
* Defina IPs
* Configure subnets
* Controle tráfego de entrada e saída

📌 Pense na VPC como seu “data center virtual” dentro da AWS.

---

## 2️⃣ Criando uma VPC

Ao criar uma VPC você define:

* Bloco CIDR (ex: 10.0.0.0/16)
* Subnets
* Tabelas de rotas
* Internet Gateway (se quiser acesso à internet)

Tipos de Subnets:

* **Pública** → possui rota para Internet Gateway
* **Privada** → não tem acesso direto à internet

Boa prática:
Separar recursos públicos (ex: Load Balancer) de privados (ex: banco de dados).

---

## 3️⃣ Iniciando uma Instância com Elastic IP

Elastic IP é um IP público fixo.

Por padrão:

* Instâncias EC2 recebem IP público dinâmico

Com Elastic IP:

* O IP permanece o mesmo mesmo se a instância for parada e iniciada

Uso comum:

* Servidores que precisam manter IP fixo

⚠️ A AWS cobra se o Elastic IP não estiver associado a uma instância.

---

## 4️⃣ Sobre ACL (Network ACL)

ACL (Access Control List) é uma camada de segurança da VPC.

Características:

* Atua no nível da subnet
* É stateless (não guarda estado da conexão)
* Permite ou nega tráfego

Diferença importante:
Security Group é stateful
ACL é stateless

📌 Na prova isso é muito cobrado.

---

## 5️⃣ VPC Peering

VPC Peering conecta duas VPCs para que elas se comuniquem.

Regras:

* Comunicação privada
* Pode ser entre regiões
* Não é transitivo (A ↔ B e B ↔ C não conecta A ↔ C)

Uso comum:
Conectar ambientes diferentes dentro da AWS.

---

## 6️⃣ VPC Endpoints

Permite que sua VPC acesse serviços da AWS sem usar internet pública.

Exemplo:
Acessar S3 sem passar pela internet.

Benefícios:

* Mais segurança
* Tráfego permanece na rede da AWS

Tipos:

* Gateway Endpoint
* Interface Endpoint

📌 Muito cobrado em questões de segurança.

---

## 7️⃣ VPC Flow Logs

Captura informações sobre tráfego de rede na VPC.

Pode monitorar:

* Interface de rede
* Subnet
* VPC inteira

Usado para:

* Auditoria
* Troubleshooting
* Segurança

---

## 8️⃣ Client VPN e Site-to-Site VPN

### Client VPN

Permite que usuários individuais se conectem à VPC.

Exemplo:
Funcionário remoto acessando recursos internos.

---

### Site-to-Site VPN

Conecta:

* Data center on-premise
* VPC na AWS

Usa conexão criptografada pela internet.

---

## 9️⃣ AWS PrivateLink

Permite acesso privado a serviços da AWS ou serviços de terceiros.

Tráfego:

* Não passa pela internet
* Fica dentro da rede da AWS

Muito usado para:

* Comunicação segura entre serviços

---

## 🔟 AWS Direct Connect

Conexão dedicada física entre:

* Data center da empresa
* AWS

Vantagens:

* Menor latência
* Conexão estável
* Maior segurança

Usado por empresas que precisam de alta performance e tráfego constante.

---

## 1️⃣1️⃣ AWS Transit Gateway

Conecta múltiplas VPCs e redes on-premise de forma centralizada.

Funciona como um “hub” de rede.

Resolve problema de:

* Muitas conexões de peering
* Complexidade de rede

---

# 🎯 Comparação Rápida (Importante para Prova)

| Serviço         | Função                        |
| --------------- | ----------------------------- |
| VPC             | Rede virtual isolada          |
| Security Group  | Firewall stateful             |
| ACL             | Firewall stateless            |
| VPC Peering     | Conectar duas VPCs            |
| Transit Gateway | Conectar várias VPCs          |
| VPN             | Conexão segura via internet   |
| Direct Connect  | Conexão dedicada física       |
| PrivateLink     | Acesso privado a serviços     |
| VPC Endpoint    | Acesso privado a serviços AWS |

---

# 🧠 O que mais cai na prova

* Diferença entre Security Group e ACL
* Quando usar Direct Connect vs VPN
* O que é VPC
* Conceito de subnet pública vs privada
* O que é VPC Endpoint
* Transit Gateway para múltiplas VPCs

---

# 📌 Resumo Final

A VPC é a base de rede da AWS.

Principais pontos:

* Controle de IP, subnets e rotas
* Segurança com Security Groups e ACL
* Conexões com VPN, Direct Connect e Peering
* Acesso privado com PrivateLink e Endpoints
* Monitoramento com Flow Logs

---
