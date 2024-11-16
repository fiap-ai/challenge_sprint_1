# Análise de Custos - Chatbot Solubio

> Para detalhes de custos e performance dos modelos de IA, consulte [tech-ia.md](tech-ia.md)

## 1. Serviços AWS e Limites

### 1.1 Serviços com Nível Gratuito (Free Tier)

#### Amazon API Gateway
- **Limites Gratuitos**
  - 1 milhão de chamadas API por mês
  - Primeiros 12 meses
  - [Free Tier Details](https://aws.amazon.com/free/)
- **Após Free Tier**
  - $1.00 por milhão de chamadas
  - $0.09 por GB de transferência
  - [API Gateway Pricing](https://aws.amazon.com/api-gateway/pricing/)
- **Performance**
  - Latência < 50ms
  - Disponibilidade 99.95%
  - [SLA Details](https://aws.amazon.com/api-gateway/sla/)

#### AWS Lambda
- **Limites Gratuitos**
  - 1 milhão de solicitações por mês
  - 400.000 GB-segundos de computação
  - Permanente (não expira)
  - [Lambda Free Tier](https://aws.amazon.com/lambda/pricing/)
- **Após Free Tier**
  - $0.20 por milhão de solicitações
  - $0.0000166667 por GB-segundo
  - [Detailed Pricing](https://aws.amazon.com/lambda/pricing/)
- **Limites de Serviço**
  - 1000 execuções concorrentes
  - 15 minutos por execução
  - [Service Quotas](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-limits.html)

#### Amazon DynamoDB
- **Limites Gratuitos**
  - 25 GB de armazenamento
  - 25 unidades de capacidade de gravação
  - 25 unidades de capacidade de leitura
  - Permanente (não expira)
  - [DynamoDB Free Tier](https://aws.amazon.com/dynamodb/pricing/provisioned/)
- **Após Free Tier**
  - $0.25 por GB/mês
  - $0.25 por WCU/mês
  - $0.05 por RCU/mês
  - [Pricing Details](https://aws.amazon.com/dynamodb/pricing/)
- **Performance**
  - Latência < 10ms
  - Disponibilidade 99.999%
  - [Performance Details](https://aws.amazon.com/dynamodb/performance/)

#### Amazon S3
- **Limites Gratuitos**
  - 5 GB de armazenamento Standard
  - 20.000 solicitações GET
  - 2.000 solicitações PUT
  - Primeiros 12 meses
  - [S3 Free Tier](https://aws.amazon.com/s3/pricing/)
- **Após Free Tier**
  - $0.023 por GB/mês
  - $0.005 por 1.000 solicitações GET
  - $0.004 por 1.000 solicitações PUT
  - [Detailed Pricing](https://aws.amazon.com/s3/pricing/)
- **Durabilidade**
  - 99.999999999% (11 noves)
  - [Reliability](https://aws.amazon.com/s3/reliability/)

#### Amazon CloudWatch
- **Limites Gratuitos**
  - 10 métricas personalizadas
  - 1 milhão de requisições API
  - 5 GB de ingestão de logs
  - Primeiros 12 meses
  - [CloudWatch Free Tier](https://aws.amazon.com/cloudwatch/pricing/)
- **Após Free Tier**
  - $0.30 por métrica/mês
  - $0.01 por 1.000 métricas API
  - $0.50 por GB de ingestão de logs
  - [Pricing Details](https://aws.amazon.com/cloudwatch/pricing/)
- **Retenção**
  - Métricas: 15 meses
  - Logs: Configurável
  - [Retention Details](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html)

#### Amazon Cognito
- **Limites Gratuitos**
  - 50.000 MAUs (usuários ativos mensais)
  - Permanente (não expira)
  - [Cognito Free Tier](https://aws.amazon.com/cognito/pricing/)
- **Após Free Tier**
  - $0.0055 por MAU
  - [Pricing Calculator](https://calculator.aws/#/addService/Cognito)
- **Performance**
  - Disponibilidade 99.9%
  - [SLA Details](https://aws.amazon.com/cognito/sla/)

## 2. Análise de Custos por Cenário

### 2.1 Cenário de Uso Mínimo
- API Gateway: Gratuito (< 1M chamadas)
- Lambda: Gratuito (< 1M execuções)
- DynamoDB: Gratuito (< 25GB)
- S3: Gratuito (< 5GB)
- CloudWatch: Gratuito (básico)
- Cognito: Gratuito (< 50K MAUs)
- IA Total: $6/mês (ver detalhes em [tech-ia.md](tech-ia.md))
**Total Mínimo: $6/mês**

### 2.2 Cenário de Uso Médio
- API Gateway: $1/mês (1.5M chamadas)
- Lambda: Gratuito
- DynamoDB: Gratuito
- S3: Gratuito
- CloudWatch: Gratuito
- Cognito: Gratuito
- IA Total: $9/mês (ver detalhes em [tech-ia.md](tech-ia.md))
**Total Médio: $10/mês**

### 2.3 Cenário de Uso Alto
- API Gateway: $2/mês (2M chamadas)
- Lambda: $0.40/mês
- DynamoDB: Gratuito
- S3: $0.50/mês
- CloudWatch: Gratuito
- Cognito: Gratuito
- IA Total: $12/mês (ver detalhes em [tech-ia.md](tech-ia.md))
**Total Alto: $14.90/mês**

## 3. Estratégias de Otimização de Custos

### 3.1 Otimização de IA
> Para detalhes completos sobre estratégias de otimização de IA, consulte [tech-ia.md](tech-ia.md#4-estratégia-de-cache)

### 3.2 Curto Prazo
- Maximizar uso do Free Tier
- Implementar cache
- Otimizar consultas
- Compressão de dados
- [AWS Cost Optimization Pillar](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html)

### 3.3 Médio Prazo
- Análise de padrões
- Ajuste de recursos
- Automação de scaling
- Limpeza de dados
- [AWS Cost Intelligence](https://aws.amazon.com/aws-cost-management/aws-cost-intelligence/)

### 3.4 Longo Prazo
- Reserved Instances
- Savings Plans
- Otimização arquitetural
- Análise de ROI
- [AWS Cost Optimization Resources](https://aws.amazon.com/pricing/cost-optimization/)

## 4. Monitoramento de Custos

### 4.1 Ferramentas
- AWS Cost Explorer ([Docs](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/))
- Google Cloud Billing ([Docs](https://cloud.google.com/billing/docs))
- Azure Cost Management ([Docs](https://azure.microsoft.com/products/cost-management))
- CloudWatch Alarms ([Docs](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html))
- Cost Allocation Tags ([Docs](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html))

### 4.2 Alertas
- Limite mensal total: $45 (90% do crédito)
- Limite IA total: $30
- Picos inesperados: +20% do normal
- Alertas por modelo de IA
- [AWS Budgets](https://aws.amazon.com/aws-cost-management/aws-budgets/)

## 5. Conclusões

### 5.1 Viabilidade
- Projeto viável dentro do limite de $50
- Abordagem híbrida otimiza custos
- Custos previsíveis e controláveis
- ROI positivo esperado
- [AWS Pricing Overview](https://aws.amazon.com/pricing/)

### 5.2 Recomendações
- Implementar monitoramento multi-cloud
- Revisar custos semanalmente
- Manter reserva para testes
- Otimizar continuamente o roteamento de IA
- [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/)
