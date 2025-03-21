Planilha de Recursos Otimizada - E-commerce AWS
============================================================

1. Infraestrutura Front-End
---------------------------

| Componente | Serviço AWS | Dimensionamento Reduzido | Custo Mensal Estimado (USD) |
| --- | --- | --- | --- |
| CloudFront | CloudFront | 8 TB de transferência mensal | $720 |
| Static Frontend | S3 + CloudFront | 30GB de armazenamento | $1 (S3) + já incluído acima |
| **Subtotal Front-End** |  |  | **$721** |

2. Camada de Aplicação
----------------------

| Componente | Serviço AWS | Dimensionamento Reduzido | Custo Mensal Estimado (USD) |
| --- | --- | --- | --- |
| E-Commerce App | ECS/Fargate | 10 containers (2vCPU, 4GB RAM) com Auto Scaling | $1,050 |
| SQS para Messaging | SQS | 20 milhões de mensagens mensais | $70 |
| SNS para Notificações | SNS | 5 milhões de notificações | $50 |
| API Gateway | API Gateway | 50 milhões de solicitações mensais | $175 |
| **Subtotal Camada de Aplicação** |  |  | **$1,345** |

3. Camada de Dados
------------------

| Componente | Serviço AWS | Dimensionamento Reduzido | Custo Mensal Estimado (USD) |
| --- | --- | --- | --- |
| Customers DB | RDS (PostgreSQL) | db.r6g.large (2vCPU, 16GB RAM) Multi-AZ | $395 |
| Orders DB | RDS (PostgreSQL) | db.r6g.large (2vCPU, 16GB RAM) Multi-AZ | $395 |
| Catalog DB | RDS (PostgreSQL) | db.r6g.large (2vCPU, 16GB RAM) Multi-AZ | $395 |
| Pricing DB | Aurora Serverless v2 | 16-32 ACUs, escalonável | $250 |
| RabbitMQ / MQ | Amazon MQ | mq.m5.large (1 instância) | $240 |
| ElastiCache (Redis) | ElastiCache | cache.t3.medium (2 nós) | $140 |
| **Subtotal Camada de Dados** |  |  | **$1,815** |

4. Monitoramento e Operações
----------------------------

| Componente | Serviço AWS | Dimensionamento Reduzido | Custo Mensal Estimado (USD) |
| --- | --- | --- | --- |
| CloudWatch | CloudWatch | Monitoramento básico + 50GB de logs | $125 |
| X-Ray | X-Ray | Uso seletivo e amostragem | $30 |
| Route 53 | Route 53 | Zona hospedada + health checks básicos | $10 |
| **Subtotal Monitoramento** |  |  | **$165** |

5. Segurança e Rede
-------------------

| Componente | Serviço AWS | Dimensionamento Reduzido | Custo Mensal Estimado (USD) |
| --- | --- | --- | --- |
| WAF | AWS WAF | Regras básicas, 50 milhões de solicitações | $450 |
| Shield | AWS Shield Standard | Proteção DDoS básica | $0 (incluído) |
| VPC | VPC + NAT Gateway | 2 AZs com NAT Gateways compartilhados | $180 |
| **Subtotal Segurança e Rede** |  |  | **$630** |

6. Custos de Transferência de Dados
-----------------------------------

| Tipo | Volume Estimado Reduzido | Custo Mensal Estimado (USD) |
| --- | --- | --- |
| Saída de dados (além do CloudFront) | 3 TB | $270 |
| Transferência entre AZs | 5 TB | $50 |
| **Subtotal Transferência** |  | **$320** |

7. Custos de Suporte
--------------------

| Plano | Cobertura | Custo Mensal Estimado (USD) |
| --- | --- | --- |
| AWS Developer Support | Suporte básico em horário comercial | $100 |
| **Subtotal Suporte** |  | **$100** |

8. Savings Plans e Otimizações
------------------------------

| Estratégia | Aplicação | Economia Mensal Estimada (USD) |
| --- | --- | --- |
| Savings Plans Compute | Compromisso de 1 ano para EC2/Fargate | -$300 |
| Instâncias Reservadas RDS | Compromisso de 1 ano para RDS | -$350 |
| **Subtotal Economia** |  | **-$650** |

Resumo de Custos
----------------

| Categoria | Custo Mensal Estimado (USD) |
| --- | --- |
| Front-End | $721 |
| Camada de Aplicação | $1,345 |
| Camada de Dados | $1,815 |
| Monitoramento e Operações | $165 |
| Segurança e Rede | $630 |
| Transferência de Dados | $320 |
| Suporte | $100 |
| Subtotal | $5,096 |
| Savings Plans e RIs | -$650 |
| **Total Mensal Estimado** | **$4,446** |
| **Reserva para Contingências (30%)** | **$1,334** |
| **Reserva para Escala em Picos (40%)** | **$1,778** |
| **Total Mensal com Reservas** | **$7,558** |
| **Total Anual Estimado** | **$90,696** |

Limitações e Considerações deste Orçamento
------------------------------------------

1.  **Capacidade reduzida**: Suporta aproximadamente 3-5 milhões de visitantes mensais e 200-300 mil transações
2.  **Menor redundância**: 2 zonas de disponibilidade em vez de 3, o que ainda garante boa disponibilidade
3.  **Capacidade de escala**: Orçamento inclui margem para picos de tráfego (40% reservado)
4.  **Segurança simplificada**: Shield Standard em vez de Advanced, mas com WAF mantido
5.  **Suporte Developer em vez de Business**: Tempos de resposta mais longos para incidentes

![image](https://github.com/user-attachments/assets/7fe6bba7-fd61-46cb-9374-323c2a44c89b)
