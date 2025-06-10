# AWS EC2 (Elastic Compute Cloud)

## 📘 Visão Geral

O **Amazon EC2 (Elastic Compute Cloud)** é um serviço da AWS que fornece capacidade de computação segura e redimensionável na nuvem. Ele permite a criação e execução de servidores virtuais, chamados de **instâncias**, para hospedar aplicações, sites, bancos de dados e outros serviços de backend.

---

## 🚀 Benefícios do EC2

- **Escalabilidade**: Fácil ajuste de capacidade para lidar com mudanças de demanda.
- **Controle Total**: Acesso root à instância e escolha total do sistema operacional e software.
- **Diversidade de Instâncias**: Tipos otimizados para memória, computação, armazenamento, entre outros.
- **Integração com outros serviços AWS**: Como S3, RDS, ELB, IAM, etc.
- **Pagamento por uso**: Faturamento com base no tempo em que as instâncias estão ativas.

---

## ⚙️ Principais Conceitos

| Conceito | Descrição |
|---------|-----------|
| **Instância** | Um servidor virtual em execução. |
| **AMI (Amazon Machine Image)** | Imagem que contém o SO e softwares necessários para iniciar uma instância. |
| **Tipos de Instância** | Define a configuração de CPU, memória, armazenamento e rede. Exemplos: `t2.micro`, `m5.large`. |
| **Chave SSH (Key Pair)** | Usada para autenticação segura ao acessar a instância via SSH. |
| **Security Groups** | Conjunto de regras de firewall para controlar o tráfego de entrada e saída. |
| **Elastic IP** | IP público fixo para sua instância EC2. |
| **Volumes EBS** | Discos persistentes usados como armazenamento para as instâncias. |

---

## 💰 Modelos de Aquisição

A AWS oferece diferentes **modelos de aquisição de instâncias EC2**, permitindo escolher o melhor custo-benefício conforme o uso:

| Modelo | Descrição | Indicado para |
|--------|-----------|---------------|
| **Sob Demanda (On-Demand)** | Pague por hora ou segundo de uso, sem compromisso a longo prazo. | Ambientes de teste, desenvolvimento ou cargas imprevisíveis. |
| **Instâncias Reservadas (Reserved Instances)** | Contrato de 1 ou 3 anos com desconto significativo (até 75%) comparado ao On-Demand. | Aplicações estáveis e com uso constante. |
| **Instâncias Spot** | Oferece capacidade ociosa da AWS com até 90% de desconto, mas pode ser interrompida a qualquer momento. | Processos tolerantes a falhas, como análise de dados e jobs em batch. |
| **Instâncias Savings Plans** | Compromisso de uso (em dólar/hora) por 1 ou 3 anos, aplicável a diferentes tipos de instância. | Flexibilidade com economia similar às reservadas. |
| **Instâncias Dedicadas (Dedicated Hosts)** | Servidor físico exclusivo para o cliente. Ideal para compliance e licenciamento. | Necessidades regulatórias específicas ou de isolamento físico. |

---

## ☁️ Exemplos de Uso

- Hospedagem de aplicações web e APIs.
- Execução de servidores de banco de dados.
- Ambientes de desenvolvimento e testes.
- Processamento em lote e tarefas automatizadas.
- Hospedagem de jogos e servidores de backend.

---

## 🧭 Passo a Passo para Criar uma Instância EC2

1. Acesse o [console da AWS](https://console.aws.amazon.com/)
2. Vá até o serviço **EC2**.
3. Clique em **Executar Instância**.
4. Escolha uma **AMI** (ex: Amazon Linux, Ubuntu, etc).
5. Escolha um **Tipo de Instância** (ex: `t2.micro` - elegível ao free tier).
6. Configure o armazenamento (EBS).
7. Configure o grupo de segurança (libere portas como 22/80/443).
8. Escolha ou crie um par de chaves (para acesso SSH).
9. Lance a instância.

---

## 🛡️ Boas Práticas

- Utilize **IAM Roles** para limitar permissões da instância.
- Ative **monitoramento com CloudWatch** para verificar uso de CPU, memória e disco.
- **Crie snapshots** regulares dos volumes EBS.
- Mantenha o sistema operacional e os pacotes atualizados.
- Utilize **Auto Scaling Groups** para alta disponibilidade.
- **Nunca exponha a porta SSH ao mundo (0.0.0.0/0)** sem necessidade.

---

## 📚 Links Úteis

- [Documentação Oficial do Amazon EC2](https://docs.aws.amazon.com/ec2/)
- [AWS Free Tier](https://aws.amazon.com/free/)
- [Preços do Amazon EC2](https://aws.amazon.com/ec2/pricing/)
- [Amazon EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)
- [Savings Plans vs Reserved Instances](https://aws.amazon.com/savingsplans/)

---

## 📌 Observações

Este README tem o objetivo de fornecer uma introdução prática e conceitual sobre o Amazon EC2. Para projetos reais, recomenda-se estudar tópicos mais avançados como **Elastic Load Balancer (ELB)**, **VPC**, **Auto Scaling**, **CloudWatch** e **AWS Systems Manager**.
