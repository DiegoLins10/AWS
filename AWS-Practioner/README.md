# AWS cloud practioner CLF-C02

TOPICOS:

✅ 4. Foque nos tópicos que realmente caem
Evite estudar tudo em profundidade. Foque nos tópicos da prova, como:

Modelo de responsabilidade compartilhada.

Conceitos de regiões, zonas de disponibilidade.

Pricing models (On-demand, Reserved, Spot).

Ferramentas de suporte (Support plans, Trusted Advisor).

Segurança (IAM, MFA, CloudTrail, etc.).

Well-Architected Framework (pelo menos saber os pilares).

## LOCALIZACAO DEFAULT AWS 
- Norte da virginia 
Aqui temos todos as funcionalidades disponivel no aws sem restrição

## AWS Free tier

O **AWS Free Tier** é um programa da Amazon Web Services que permite aos usuários explorar e experimentar os serviços da AWS gratuitamente, dentro de certos limites. Ele se divide em três categorias principais:

1. **Gratuito por 12 meses** – Serviços disponíveis sem custo por um ano após a criação da conta, como:  
   - **EC2**: 750 horas por mês de instâncias t2.micro ou t3.micro  
   - **S3**: 5 GB de armazenamento padrão  
   - **RDS**: 750 horas em instâncias db.t2.micro ou db.t3.micro (MySQL, PostgreSQL, etc.)  
   - **Lambda**: 1 milhão de chamadas gratuitas por mês  

2. **Sempre gratuito** – Serviços que continuam gratuitos enquanto dentro dos limites, como:  
   - **AWS Lambda**: 1 milhão de execuções por mês  
   - **DynamoDB**: 25 GB de armazenamento e até 25 unidades de leitura/escrita  
   - **CloudWatch**: 10 métricas e 1 milhão de requisições gratuitas  

3. **Testes gratuitos por tempo limitado** – Alguns serviços oferecem períodos de teste específicos, como **Amazon Redshift** (2 meses com 750 horas/mês).

O **AWS Free Tier** é ideal para aprendizado, desenvolvimento e testes, mas é importante monitorar o uso para evitar cobranças ao ultrapassar os limites.

https://aws.amazon.com/pt/free

## Criando alerta de custo AWS
1. Entrar nas configurações da conta
2. Preferencias de faturamento
3. Ativar alertas de faturamento do cloudwatch em preferencias de alerta
4. Entrar no cloudwatch e acessar todos os alarmes
5. Criar alarme
6. selecionar a metrica(Billing) Total Estimated Charge e colocar o valor
7. Criar um novo topico e colocar seu email
8. Configurar serviços de SNS Ativar email

## Tipos de cloud

Esses três termos são modelos de serviço na **computação em nuvem**:  

### ☁️ **IaaS (Infrastructure as a Service)** – **Infraestrutura como Serviço**  
👉 **Fornece servidores, rede e armazenamento na nuvem**. Você gerencia o sistema operacional, aplicativos e configurações.  
✅ Exemplo: **AWS EC2, Google Compute Engine, Azure Virtual Machines**  
🔹 **Pense como:** Alugar um computador virtual na nuvem e configurar tudo do zero.  

### ☁️ **PaaS (Platform as a Service)** – **Plataforma como Serviço**  
👉 **Fornece um ambiente pronto para desenvolver, testar e rodar aplicativos**. Você só se preocupa com o código, sem gerenciar servidores.  
✅ Exemplo: **AWS Elastic Beanstalk, Google App Engine, Heroku**  
🔹 **Pense como:** Um serviço onde você só coloca seu código e ele roda sem precisar configurar servidores.  

### ☁️ **SaaS (Software as a Service)** – **Software como Serviço**  
👉 **Fornece um software pronto para uso na nuvem**, sem precisar instalar nada. Você só acessa e usa.  
✅ Exemplo: **Gmail, Google Drive, Dropbox, Microsoft 365**  
🔹 **Pense como:** Um site ou app que você usa sem precisar instalar ou configurar nada.  

💡 **Resumo fácil:**  
- **IaaS** → Infraestrutura bruta (você gerencia servidores).  
- **PaaS** → Plataforma pronta para rodar aplicativos (você só desenvolve).  
- **SaaS** → Software pronto para uso (você só usa).

  Esses termos se referem a **diferentes tipos de implantação de computação em nuvem**.  

### ☁️ **Nuvem Pública**  
👉 A infraestrutura é **compartilhada** entre vários usuários e gerenciada por um provedor de nuvem.  
✅ **Exemplo**: AWS, Google Cloud, Microsoft Azure.  
🔹 **Vantagens**: Menor custo, escalabilidade, manutenção feita pelo provedor.  
🔸 **Desvantagem**: Menos controle sobre segurança e personalização.  

### 🏢 **Nuvem Privada**  
👉 A infraestrutura é usada **exclusivamente** por uma única empresa ou organização. Pode estar dentro da empresa (on-premises) ou ser gerenciada por terceiros.  
✅ **Exemplo**: Nuvem interna de um banco ou governo.  
🔹 **Vantagens**: Maior segurança, controle total sobre dados e configurações.  
🔸 **Desvantagem**: Mais caro, exige equipe especializada para gerenciar.  

### 🔄 **Nuvem Híbrida**  
👉 Combina **nuvem pública + nuvem privada**, permitindo mais flexibilidade.  
✅ **Exemplo**: Uma empresa pode armazenar dados sigilosos em nuvem privada e usar nuvem pública para aplicativos escaláveis.  
🔹 **Vantagens**: Equilíbrio entre segurança e custo, otimização de recursos.  
🔸 **Desvantagem**: Mais complexa de gerenciar.  

💡 **Resumo fácil:**  
- **Pública** → Barata, escalável, mas menos controle (ex: AWS, Google Cloud).  
- **Privada** → Segura, personalizável, mas mais cara. Um servidor que não é compartilhado com ninguem, pode ser dentro da AWS, mais utilizado por bancos, governo, financeiro  
- **Híbrida** → Mistura das duas, combinando segurança e custo.

  ## AWS SUPPORT PLANS

  A AWS oferece **quatro planos de suporte**, dependendo das suas necessidades e orçamento:  

### 🆓 **1. Basic (Gratuito)**  
✅ Inclui:  
- Suporte apenas para **problemas gerais da conta e cobrança**.  
- Documentação, FAQs e fóruns.  
❌ **Sem suporte técnico direto**.  

### 💼 **2. Developer ($29/mês ou 3% do uso)**  
✅ Inclui:  
- Suporte técnico apenas por **e-mail**, com tempo de resposta em até **24 horas**.  
- Melhor para **testes e desenvolvimento**.  
❌ **Sem suporte por telefone ou análise de arquitetura**.  

### 🚀 **3. Business ($100/mês ou 10% do uso)**  
✅ Inclui:  
- Suporte técnico **24/7 por chat, e-mail e telefone**.  
- Tempo de resposta prioritário: **1 hora para problemas críticos**.  
- **Guias de arquitetura e recomendações de boas práticas**.  
💡 Ideal para **empresas que usam AWS em produção**.


### 🚀 **Enterprise On-Ramp ($5.500/mês ou 10% do uso)**  
✅ Inclui:  
- **Suporte 24/7 por e-mail, chat e telefone**.  
- **Tempo de resposta de 30 minutos para problemas críticos**.  
- **Consultas sobre arquitetura da AWS**.  
- **Gerente técnico designado para ajudar na conta (TAM)**.  
💡 **Ideal para empresas que precisam de suporte avançado, mas não querem pagar o preço do Enterprise completo.**  

Ou seja, ele é mais robusto que o **Business**, mas não tão caro e exclusivo quanto o **Enterprise**.

### 🏢 **4. Enterprise (Personalizado, $$$15.000)**  
✅ Inclui:  
- **Gerente de conta tecnico dedicado (TAM)**.  
- **Suporte 24/7 com tempo de resposta de 15 minutos para incidentes críticos**.  
- **Análise e otimização da arquitetura AWS**.  
💡 Indicado para **grandes empresas com uso crítico da AWS**.

Kkkkk clássico! Os **pilares do Well-Architected Framework** são tipo a parte mais teórica e menos usada no dia a dia — muita gente pula mesmo. Mas é uma das coisas que **caem direto na prova**, então vale decorar o básico.

---

### ✅ São 6 pilares (fácil de lembrar com a sigla “SCORE-O”):

| Pilar                         | O que significa?                                                                 |
| ----------------------------- | -------------------------------------------------------------------------------- |
| **S**ecurity                  | Segurança — controle de acesso, criptografia, IAM, logs, etc.                    |
| **C**ost Optimization         | Otimização de custos — pagar só pelo que usa, reservar instâncias, monitorar.    |
| **O**perational Excellence    | Excelência operacional — monitorar, responder a eventos, melhorar continuamente. |
| **R**eliability               | Confiabilidade — tolerância a falhas, recuperação rápida, backups.               |
| **E**fficiency (Performance)  | Eficiência de performance — usar o tipo certo de recurso (EC2, Lambda, etc).     |
| **O**rganizational Governance | (Novo, desde a versão 2 da prova: *Sustainability*) — uso sustentável da nuvem.  |

---

### 💡 Dica pra decorar:

**"SCORE-O"** → *imagina um placar de arquitetura bem-feita na AWS kkk*

---

### 🎯 O que você precisa saber de cada um pra passar:

#### 1. **Security**

* Princípio de menor privilégio (least privilege).
* MFA, IAM roles, logs com CloudTrail.
* Proteção de dados (S3 encryption, KMS).

#### 2. **Cost Optimization**

* Evitar recursos ociosos.
* Escolher instâncias reservadas quando faz sentido.
* Usar o Cost Explorer.

#### 3. **Operational Excellence**

* Automatizar implantações (CodePipeline, CloudFormation).
* Monitorar (CloudWatch).
* Aprender com falhas.

#### 4. **Reliability**

* Design tolerante a falhas.
* Multi-AZ / Multi-region.
* Backups, failover.

#### 5. **Performance Efficiency**

* Escolher os serviços certos (EC2 x Lambda x Fargate).
* Escalar horizontalmente.
* Monitorar uso de CPU/memória.

#### 6. **Sustainability (desde a versão nova da prova)**

* Usar recursos com eficiência.
* Desligar recursos não usados.
* Escolher regiões mais sustentáveis.


**Resumo rápido:**  
- **Basic** → Grátis, sem suporte técnico.  
- **Developer** → E-mail, até 24h de resposta.  
- **Business** → 24/7, suporte rápido, ideal para produção.  
- **Enterprise** → Suporte premium para grandes empresas.
