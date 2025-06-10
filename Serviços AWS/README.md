## Serviços importantes aws 

- AWS ATHENA: É uma ide de consulta sql, serveless, Serviço utilizado parar criar estruturas de dados para realizar queries diretamente nos arquivos que estão no S3 e executá-las sem servidor.

- AWS AWS Certificate Manager: O AWS Certificate Manager permite a criação e gerenciamento de certificados digitais que são utilizados para criptografar os dados entre os usuários e os servidores com base no protocolo https tornando o tráfego de dados seguro.

- AWS COGNITO: O AWS Cognito é o serviço  utilizado para controlar acessos em aplicações web e mobile, ofertando diversas funcionalidades para esse fim.

- AWS KMS: O AWS KMS é o serviço utilizado para criar chaves de criptografia para uso em diversos serviços da AWS, geralmente para dados, arquivos no S3.

- Amazon OpenSearch: O Amazon OpenSearch é um conjunto distribuído de pesquisa e análise de código 100% aberto usado para uma ampla variedade de casos de uso, como monitoramento de aplicações em tempo real, análise de logs e pesquisa de sites.

- AWS GLUE: O AWS Glue é um serviço de ETL (Extração, Transformação e Carga) gerenciado que automatiza a preparação e transformação de dados para análises. Ele pode ser usado para converter arquivos que trafegam entre sistemas, como transformar dados brutos em formatos prontos para análise.

- AWS DataSync: O AWS DataSync é utilizado para realizar a sincronização automática de dados entre a infraestrutura on-premises e a AWS. Ele facilita a transferência eficiente e segura de grandes volumes de dados, automatizando tarefas de cópia, replicação e sincronização, garantindo que os dados estejam sempre atualizados entre os ambientes.

- AWS DMS: O AWS DMS (Database Migration Service) é o serviço utilizado para realizar a migração de bancos de dados na AWS. Ele facilita a migração de bancos de dados relacionais, não relacionais e de data warehouses para a AWS com mínimo tempo de inatividade, suportando migrações homogêneas e heterogêneas.

- Amazon EMR: O EMR (Elastic MapReduce) é a plataforma de Big Data da AWS, projetada para processar grandes volumes de dados utilizando frameworks como Apache Hadoop, Spark e Presto.

- Amazon CloudSearch: O CloudSearch oferece um serviço gerenciado de busca e localização que pode ser facilmente implementado em seu website.

- AWS CloudWatch: Para acompanhar o percentual de utilização de processamento e memória em seus servidores durante um período específico do dia, a empresa pode utilizar o Amazon CloudWatch. Este serviço permite monitorar métricas de desempenho, configurar alarmes e visualizar logs, facilitando o acompanhamento e a análise do uso de recursos como a memória dos servidores.

AWS CloudTrail: O CloudTrail pode ser utilizado para realizar logs de eventos relacionados a api de serviços. Com o AWS CloudTrail, é possível identificar ações manuais de desligamento de recursos ao registrar todas as atividades na conta AWS. Utilize o CloudTrail Event History ou exporte logs para Amazon Athena para filtrar eventos de desligamento, como `StopInstances` e `TerminateInstances`. Configure CloudWatch Alarms para monitorar e notificar sobre essas ações em tempo real.

Read replicas: Read Replicas (réplicas de leitura) na AWS são cópias somente leitura de um banco de dados primário (master), usadas para escalar a leitura, melhorar desempenho e aliviar a carga do banco principal.

S3  Lifecycle (Ciclo de Vida): Configurar a expiração dos objetos no Amazon S3 permite que eles sejam automaticamente excluídos quando atingirem uma data de validade.

S3 Glacier: O Amazon S3 Glacier oferece uma opção econômica para o armazenamento de dados, embora com um tempo de recuperação mais lento.

S3 Infrequent Access: O S3 Standard-IA é indicado para dados acessados com menos frequência, mas que exigem acesso rápido quando necessários. O custo é maior que o Glacier.

Amazon SQS: A função do SQS é armazenar e transmitir mensagens entre serviços, enquanto o AWS EventBridge gerencia a distribuição e o roteamento dos eventos entre diferentes sistemas e aplicações.

Amazon EventBridge: O EventBridge é um barramento de eventos sem servidor que torna mais fácil a criação de aplicações orientadas por eventos em escala usando eventos gerados com base em suas aplicações, aplicações integradas de software como serviço (SaaS) e serviços da AWS.

Elastic File System (EFS): O EFS pode ser anexado a suas instâncias EC2 permitindo o uso de sistemas de arquivo.


Amazon DynamoDB: É o banco de dados mais adequado para armazenar dados não estruturados, onde cada item pode ter diferentes atributos.

Simple Storage Service (S3): A funcionalidade de site estático do Amazon S3 permite hospedar sites estáticos diretamente em um bucket S3.

Elastic File System (EFS): O EFS - Elastic File System é um serviço utilizado para implementar um serviço de arquivos na sua arquitetura associado a instâncias EC2. Apesar de servir para armazenar arquivos estáticos não é o mais fácil e barato de implementar.

AWS Data Exchange : O AWS Data Exchange foi projetado para permitir que organizações descubram, acessem e compartilhem conjuntos de dados prontos para uso na nuvem. Sua função principal é facilitar a aquisição de dados de terceiros, como informações de mercado, financeiras ou de pesquisa

ordem de deploy: CodeCommit, CodeBuild, CodeDeploy.


AWS IQ: O AWS IQ permite que os clientes encontrem, contratem e paguem rapidamente especialistas terceirizados certificados pela AWS para trabalhos sob demanda em um projeto. O AWS IQ também facilita o uso de suas AWS Certifications para ajudar os clientes da AWS.


Amazon Comprehend: O Amazon Comprehend utiliza machine learning e processamento de linguagem natural (NLP) para analisar textos de forma avançada. Ele pode identificar o idioma do texto, extrair frases principais, e reconhecer entidades como lugares, pessoas, marcas e eventos.

Amazon Polly: O Amazon Polly é um serviço de nuvem que converte texto em fala realista indicado para desenvolver aplicações que aumentam o envolvimento e a acessibilidade.

AWS Fargate: O AWS Fargate é um serviço de computação sem servidor que facilita a execução de containers. Ele permite aos desenvolvedores concentrarem-se na criação e implantação de aplicações, enquanto a AWS gerencia a infraestrutura subjacente.

Amazon Neptune: O Amazon Neptune é um serviço de banco de dados de grafo gerenciado pela AWS. Ele é otimizado para armazenar e consultar dados altamente conectados, como redes sociais e recomendações

AWS Marketplace: O AWS Marketplace oferece uma vasta gama de aplicações e soluções de negócios prontas para uso imediato.

AWS Inspector: O AWS Inspector é um serviço de segurança automatizado da AWS que avalia a exposição a vulnerabilidades e ameaças em instâncias EC2 e aplicações.

AWS X-Ray: O AWS X-Ray é um serviço de análise de desempenho e depuração que permite rastrear e entender o comportamento de aplicações distribuídas.

AWS Budgets: O AWS Budgets é o serviço utilizado para definir orçamentos desejáveis para a uso e incluir alertas para notificação de alertas sobre uso acima do esperado.

AWS CostExplorer: Com o AWS Cost Explorer é possível consultar detalhes dos custos da sua infraestrutura a todo momento.

AWS Batch: O AWS Batch possibilita a execução de modo fácil e eficiente de centenas de milhares de tarefas de computação em lote na AWS.

AWS Wavelength: O AWS Wavelength é uma região geográfica especializada da AWS que fornece infraestrutura de computação na borda das redes de telecomunicações, próxima aos clientes.

 Amazon Route 53: Criar um novo domínio no Amazon Route 53.