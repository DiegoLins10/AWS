# 📘 README COMPLETO — ELB + ASG (AWS Developer Associate - DVA-C02)

---

# 1️⃣ High Availability & Scalability

## 🔹 High Availability (HA)

Alta disponibilidade significa:

* Aplicação distribuída em **múltiplas Availability Zones**
* Sem Single Point of Failure
* Balanceamento automático
* Substituição automática de instâncias

Arquitetura base:

```
Users
  ↓
ALB (Multi-AZ)
  ↓
ASG (Multi-AZ)
  ↓
EC2
```

Se:

* Instância falha → ASG substitui
* AZ falha → outra AZ assume
* Tráfego aumenta → escala horizontal

---

## 🔹 Escalabilidade

### Vertical Scaling

* Muda tipo da instância
* Limitado
* Pode gerar downtime

### Horizontal Scaling (preferido)

* Adiciona instâncias
* Usa ASG
* Sem downtime

---

# 2️⃣ Elastic Load Balancer (ELB)

Distribui tráfego e monitora saúde das instâncias.

Principais funções:

* Health check
* SSL termination
* Cross-zone load balancing
* Sticky sessions
* Integração com ASG

---

# 3️⃣ Tipos de Load Balancer

## 🔹 Application Load Balancer (ALB)

Application Load Balancer

### Camada

Layer 7 (HTTP/HTTPS)

### Recursos importantes

* Path-based routing
* Host-based routing
* Redirect HTTP → HTTPS
* Weighted target groups
* WebSocket support
* Lambda integration
* ECS integration

### Target types

* EC2
* IP
* Lambda

### Health Check

* Baseado em path (/health)
* Código HTTP 200

---

## 🔹 Network Load Balancer (NLB)

Network Load Balancer

Layer 4 (TCP/UDP)

Características:

* Alta performance
* Baixa latência
* IP estático
* TLS support
* Não suporta path-based routing

---

## 🔹 Gateway Load Balancer (GWLB)

Gateway Load Balancer

* Para appliances de segurança
* Firewall / IDS
* Transparente

---

## 🔹 Classic Load Balancer

Legado — evitar.

---

# 4️⃣ Cross-Zone Load Balancing

Distribui tráfego igualmente entre instâncias em AZs diferentes.

| Tipo | Cross-Zone   |
| ---- | ------------ |
| ALB  | Sempre ativo |
| NLB  | Opcional     |
| CLB  | Opcional     |

Sem cross-zone:
Tráfego pode ficar desbalanceado entre AZs.

---

# 5️⃣ Sticky Sessions

Mantém usuário na mesma instância via cookie.

Problemas:

* Desbalanceamento
* Anti-pattern para arquitetura stateless

Melhor prática:
Usar cache distribuído (ex: Redis) ao invés de sticky.

---

# 6️⃣ SSL Termination

Load Balancer pode terminar HTTPS usando:

AWS Certificate Manager

Fluxo:
Cliente → HTTPS → LB → HTTP interno

Benefícios:

* Reduz CPU nas EC2
* Centraliza certificados
* Facilita renovação

---

# 7️⃣ Health Checks

ELB verifica:

* Intervalo
* Timeout
* Threshold
* Código HTTP

Instância unhealthy:

* Removida do target group
* ASG pode substituir

Importante:
Running ≠ Healthy

---

# 8️⃣ Connection Draining (Deregistration Delay)

Quando instância sai:

* Espera requisições ativas terminarem
* Evita erro 502

Muito importante para:

* Scale in
* Deploy
* Instance refresh

---

# 9️⃣ Auto Scaling Groups (ASG)

Gerencia EC2 automaticamente.

Componentes:

* Launch Template
* Min size
* Max size
* Desired capacity
* Multi-AZ

---

# 🔟 Scaling Policies (Deep Dive)

ASG usa métricas do:

Amazon CloudWatch

---

## 🔹 1️⃣ Target Tracking (🔥 MAIS COBRADO)

Você define um alvo.

Ex:

* CPU 50%
* RequestCountPerTarget 1000

ASG calcula automaticamente quantas instâncias precisa adicionar ou remover.

Características:

* Cria alarm automaticamente
* Proporcional
* Recomendado pela AWS
* Menos configuração manual

Mentalidade:
"Mantenha em X%"

Melhor para:
Tráfego imprevisível

---

## 🔹 2️⃣ Step Scaling

Baseado em faixas.

Você define:

* Alarm manual
* Quantidade exata de instâncias para cada faixa

Ex:

| CPU  | Ação |
| ---- | ---- |
| >60% | +1   |
| >75% | +2   |
| >90% | +4   |

Controle total.

Mentalidade:
"Se passar de X, adiciona Y"

Melhor para:
Picos agressivos
Controle fino

---

## 🔹 3️⃣ Simple Scaling (Legacy)

* Um alarm
* Uma ação
* Cooldown longo

Não recomendado.
Quase não usado.

---

## 🔹 4️⃣ Scheduled Scaling

Escala baseado em horário.

Ex:

* 9h → 10 instâncias
* 18h → 2 instâncias

Usado quando:

* Tráfego previsível
* Eventos programados

---

# 1️⃣1️⃣ Cooldown & Warm-Up

## Cooldown

Tempo que ASG espera antes de nova ação de escala.

Evita:
Oscilação constante (scale in/out repetido)

---

## Instance Warm-Up

Tempo para instância estabilizar antes de considerar métrica.

Muito importante com:
Target Tracking

---

# 1️⃣2️⃣ Métricas Comuns

* CPUUtilization
* ALBRequestCountPerTarget
* NetworkIn
* Métricas customizadas

ALBRequestCountPerTarget é muito usada com Target Tracking.

---

# 1️⃣3️⃣ Instance Refresh

Permite:

* Atualizar AMI
* Rolling update
* Zero downtime

Muito cobrado em contexto CI/CD.

---

# 1️⃣4️⃣ Lifecycle Hooks

Permite executar ação quando:

* Instância inicia
* Instância termina

Ex:

* Rodar script bootstrap
* Backup antes de desligar

---

# 1️⃣5️⃣ Cenários Clássicos de Prova

### Tráfego imprevisível

→ ALB + ASG + Target Tracking

### Escalar agressivamente em picos

→ Step Scaling

### Atualizar AMI sem downtime

→ Instance Refresh

### Baixa latência TCP

→ NLB

### Aplicação stateful

→ Cache distribuído (não sticky)

---

# 🧠 Resumo Mental Final

ALB → HTTP inteligente (Layer 7)
NLB → TCP rápido (Layer 4)
Cross-zone → entre AZs
ASG → escala automático
Target Tracking → mantém métrica em alvo
Step Scaling → você define quanto escalar
Scheduled → horário fixo
Instance Refresh → rolling update
Connection Draining → evita erro ao remover instância

---

Se você quiser agora eu posso:

* 🔥 Criar um mini simulado só de arquitetura com pegadinhas
* 🧠 Misturar ELB + ASG + IAM (nível difícil DVA)
* 📘 Montar mapa mental textual conectando tudo


