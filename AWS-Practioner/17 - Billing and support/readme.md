# 📘 README – Seção 20: Billing e Support (AWS Cloud Practitioner)

---

## 1️⃣ AWS Control Tower

AWS Control Tower é um serviço que ajuda a configurar e governar um ambiente multi-conta na AWS.

Ele automatiza:

* Criação de contas
* Configuração de segurança
* Aplicação de políticas
* Governança inicial

Baseado em:

* AWS Organizations
* Guardrails (regras de governança)

Uso comum:
Empresas que querem estruturar corretamente várias contas AWS desde o início.

📌 Na prova:
Control Tower = governança automatizada para múltiplas contas.

---

## 2️⃣ AWS Resource Access Manager (AWS RAM)

AWS RAM permite compartilhar recursos da AWS entre diferentes contas.

Exemplo de recursos que podem ser compartilhados:

* Subnets
* Transit Gateway
* Licenças
* Outras infraestruturas específicas

Benefício:
Evita duplicação de recursos entre contas.

📌 Na prova:
RAM = compartilhamento seguro de recursos entre contas AWS.

---

## 3️⃣ AWS Service Catalog

AWS Service Catalog permite criar e gerenciar um catálogo de serviços aprovados para uso interno.

Exemplo:
Empresa disponibiliza:

* Templates de EC2
* Ambientes padronizados
* Infraestrutura pré-aprovada

Objetivo:
Padronização e controle.

Benefícios:

* Governança
* Conformidade
* Controle de custos

📌 Na prova:
Service Catalog = catálogo de produtos AWS aprovados para organização.

---

## 4️⃣ AWS Trusted Advisor

Trusted Advisor analisa sua conta e fornece recomendações de boas práticas.

Áreas avaliadas:

* Custo
* Performance
* Segurança
* Tolerância a falhas
* Limites de serviço

Exemplos:

* Instâncias EC2 ociosas
* Buckets S3 públicos
* Recursos subutilizados

📌 Muito importante:
Ajuda a otimizar custo e segurança.

Alguns checks são gratuitos (Basic Support).
Checks completos exigem planos superiores.

---

# 🎯 Comparação Rápida

| Serviço         | Função                                 |
| --------------- | -------------------------------------- |
| Control Tower   | Governança multi-conta                 |
| RAM             | Compartilhar recursos entre contas     |
| Service Catalog | Catálogo interno de serviços aprovados |
| Trusted Advisor | Recomendações de boas práticas         |

---

# 🧠 O que mais cai na prova

* Diferença entre Organizations e Control Tower
* Trusted Advisor para otimização de custos
* RAM para compartilhamento entre contas
* Service Catalog para padronização corporativa

---

# 📌 Resumo Final

* Control Tower → Estrutura e governança multi-conta
* RAM → Compartilhar recursos entre contas
* Service Catalog → Padronização interna
* Trusted Advisor → Recomendações de otimização

Esses serviços ajudam na gestão, governança e controle dentro da AWS.

---
