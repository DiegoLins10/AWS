# AWS

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
- **Privada** → Segura, personalizável, mas mais cara.  
- **Híbrida** → Mistura das duas, combinando segurança e custo.
