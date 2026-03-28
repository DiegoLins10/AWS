
1 - Uma fila SQS pode receber um numero ilimitado de mensagens

# ⚡ RCU  DynamoDB = conta de 4 em 4 KB

👉 Ele divide o item em **blocos de 4 KB**
---
## 🧠 Como pensar sem arredondar pra mim cima... 
* 1–4 KB → **1 RCU**
* 5–8 KB → **2 RCUs**
* 9–12 KB → **3 RCUs**
---
## 📦 Exemplo
* 6 KB → ocupa:
  * 4 KB (1 bloco)
  * +2 KB (precisa de outro bloco)

👉 Total: **2 blocos = 2 RCUs**

10 leituras fortemente com 6kb de RCU. 

6kb = 2RCU, 8kb
10 * 2 rcu = 20 RCU para 10 leituras

---

## 🔥 Regra final (decora)

> **“Conta de 4 em 4 e sempre arredonda pra cima”**

Perfeito pra prova 👍

# ⚡ DynamoDB — PutItem vs UpdateItem (resumo)

* **PutItem** → cria ou **substitui tudo**
* **UpdateItem** → atualiza campos **ou cria (upsert)**

---

## 🧠 Regra de prova

> **Put = replace**
> **Update = patch + pode criar**

---

## ⚠️ Pegadinha

* Quer evitar criação no Update?
  👉 use `ConditionExpression` (`attribute_exists`)


--dry-run verifica se o usuário possui as permissões necessárias para executar a ação, sem realmente executar a operação. Se o usuário tiver permissão, a resposta será DryRunOperation; caso contrário, UnauthorizedOperation. Essa é a forma recomendada para testar permissões.

🧠 Hack pra decorar

gp2 → “3 por GB”

gp3 → “3 mil fixo”

io → “eu escolho”

🧠 Regra chave

gp2 = 3 IOPS por GB

👉 até um limite de:

16.000 IOPS

divide o limite de 16000 por 3
16000 / 3 ≈ 5334 GB

Aqui vai no estilo que você curte (README + prova 👇)

---

# 📘 EC2 – Detailed Monitoring (AWS CLI)

## 1. 🎯 O que é Detailed Monitoring?

* Por padrão, o Amazon EC2 envia métricas para o CloudWatch a cada **5 minutos**
* Com **Detailed Monitoring**, passa a enviar a cada **1 minuto**
* 🔥 Usado para:

  * Auto Scaling mais preciso
  * Troubleshooting fino
  * Métricas mais granulares

---

## 2. ⚙️ Habilitar em instância EXISTENTE

```bash
aws ec2 monitor-instances --instance-ids i-1234567890abcdef0
```

✅ Pontos importantes:

* `monitor-instances` → ação correta
* `--instance-ids` → **sempre no plural**
* Pode passar **várias instâncias**

---

## 3. 🆕 Habilitar ao CRIAR instância

```bash
aws ec2 run-instances \
  --image-id ami-xxxx \
  --monitoring Enabled=true
```

✅ Só funciona na criação

---

## 4. ❌ Pegadinhas de prova

| Erro comum                                    | Por que está errado                  |
| --------------------------------------------- | ------------------------------------ |
| `--instance-id`                               | ❌ Deve ser plural (`--instance-ids`) |
| `monitor-instances` com `--monitoring`        | ❌ Parâmetro não existe aqui          |
| `--monitoring State=enabled`                  | ❌ Sintaxe inválida                   |
| Usar `run-instances` para instância existente | ❌ Só criação                         |

---

## 5. 🔄 Desabilitar monitoring

```bash
aws ec2 unmonitor-instances --instance-ids i-1234567890abcdef0
```

---

## 6. 🧠 Resumo PROVA (⚡ decore isso)

* EXISTENTE → `monitor-instances`
* NOVA → `run-instances --monitoring Enabled=true`
* `instance-ids` → sempre plural

---

Se quiser, posso te fazer um **pacotão EC2 CLI (top 20 comandos + pegadinhas de prova)** que cai MUITO na DVA 👀


Boa — essa confusão é **clássica de prova** 😈
vou te explicar **bem direto e comparativo** (estilo AWS mesmo)

---

# 🧠 Diferença: Lambda Layer vs ARN de Alias

## 🧱 1. Lambda Layer (Camada do Lambda)

* Serviço: AWS Lambda

👉 **O que é:**

* Pacote com:

  * bibliotecas
  * dependências
  * código compartilhado

👉 **Função:**

* Reutilizar código entre funções

👉 **Importante:**

* ❌ NÃO executa função
* ❌ NÃO controla versão de deploy
* ❌ NÃO resolve problema de ARN

💡 Exemplo:

> colocar `numpy`, `aws-sdk`, libs comuns

---

## 🔗 2. ARN de Alias (Lambda Alias)

👉 **O que é:**

* Um **nome estável (ponteiro)** para uma versão da função

👉 **Função:**

* Controlar deploy/versionamento

👉 **Importante:**

* ✅ Aponta para uma versão específica
* ✅ Usado em integrações (SQS, API Gateway, etc)
* ✅ Evita trocar ARN toda hora

💡 Exemplo:

```bash
minha-funcao:prod → versão 3
```

---

## ⚔️ Comparação direta (nível prova)

| Conceito                 | Lambda Layer 🧱 | ARN de Alias 🔗 |
| ------------------------ | --------------- | --------------- |
| Serve pra deploy?        | ❌ Não           | ✅ Sim           |
| Executa função?          | ❌ Não           | ✅ Indiretamente |
| Gerencia versão?         | ❌ Não           | ✅ Sim           |
| Reutilização de código?  | ✅ Sim           | ❌ Não           |
| Resolve problema de ARN? | ❌ Não           | ✅ Sim           |

---

## 💀 Pegadinha clássica da prova

A questão mistura:

* “camada”
* “alias”
* “ARN”

👉 e tenta fazer você pensar que:

> layer ajuda no deploy

❌ ERRADO

---

## 🧠 Regra de ouro (grava isso)

> 🧱 **Layer = dependência**
> 🔗 **Alias = deploy/versionamento**

---

## 🎯 Tradução mental pra prova

Se a pergunta falar:

* “evitar atualizar ARN” → 👉 **Alias**
* “compartilhar código” → 👉 **Layer**

---

## 💬 Resumo simples

* Layer = **código extra**
* Alias = **controle de versão**

👉 funções totalmente diferentes

---

Perfeita essa — **nível DVA real mesmo** 😈
e aqui tem uma pegadinha MUITO clássica: **KMS = quase sempre simétrico**

---

# 🧠 O que a questão estava testando

Serviço: AWS Key Management Service

👉 Contexto:

* criptografia de dados (ex: DynamoDB, SDK de criptografia)
* uso de KMS por baixo

---

# ❌ Por que ASSIMÉTRICA está errada?

A frase chave:

> “SDK de criptografia… chave para cada item”

👉 Isso indica:

* criptografia de **dados em massa**
* uso interno de chaves

---

## 💀 Regra de prova

> 👉 **KMS para criptografia de dados = SIMÉTRICA**

---

## 🧠 Por quê?

* KMS usa:

  * **data keys (chaves de dados)**
* Essas chaves:

  * criptografam dados rapidamente
  * são geradas a partir de uma **KMS key simétrica**

---

## ⚠️ Assimétrica no KMS é usada pra:

* assinatura digital
* verificação
* criptografia com chave pública

👉 NÃO é padrão pra:

* criptografar banco
* criptografar volume grande de dados

---

# 🔥 Tradução da questão (o pulo do gato)

A questão basicamente disse:

> “criptografar itens de tabela com SDK + KMS”

👉 seu cérebro deve pensar:

> **SIMÉTRICA automaticamente**

---

# ⚔️ Comparação prática (AWS)

| Caso                                 | Tipo correto   |
| ------------------------------------ | -------------- |
| Criptografar dados (S3, Dynamo, EBS) | 🔵 Simétrica   |
| TLS / certificados                   | 🔴 Assimétrica |
| Assinatura digital                   | 🔴 Assimétrica |

---

# 🧠 Frase pra gravar

> 👉 **“KMS padrão = simétrica para dados”**

---

# 💬 Resumo direto

* Você escolheu assimétrica ❌
* Mas o cenário era:

  * dados
  * performance
  * SDK

👉 Logo:
✅ **Simétrica**

---

## 🚀 Dica nível aprovação

Se aparecer:

* “SDK de criptografia”
* “dados”
* “tabela”
* “alto volume”

👉 **marca simétrica sem pensar muito**

---



