# Chatbot Solubio - Design da Arquitetura

## Visão Geral
A arquitetura proposta foi projetada para criar um chatbot com abordagem híbrida de IA que atenda aos requisitos de atendimento ao cliente da Solubio, mantendo-se dentro do limite de crédito AWS de $50. A solução enfatiza escalabilidade, segurança e tratamento eficiente das várias interações com clientes.

> Para detalhes completos sobre os modelos de IA, suas capacidades, métricas e custos, consulte [tech-ia.md](tech-ia.md)

## Componentes Principais

### 1. Camada de Interface do Usuário
- **Amazon API Gateway**
  - Gerencia todas as requisições recebidas de vários canais
  - Fornece endpoints REST API para a interface do chatbot
  - Habilita conexões WebSocket para chat em tempo real
  - Custo: ~$1/milhão de chamadas API
  - SLA: 99.95% de disponibilidade
  - Referências:
    * [API Gateway Documentation](https://docs.aws.amazon.com/apigateway/)
    * [API Gateway Pricing](https://aws.amazon.com/api-gateway/pricing/)
    * [WebSocket APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api.html)

### 2. Autenticação & Segurança
- **Amazon Cognito**
  - Gerencia autenticação e autorização de usuários
  - Trata o acesso seguro aos dados dos clientes
  - Fornece gestão de identidade para clientes e funcionários
  - Custo: Nível gratuito inclui 50.000 MAUs
  - SLA: 99.9% de disponibilidade
  - Referências:
    * [Cognito Documentation](https://docs.aws.amazon.com/cognito/)
    * [Cognito Pricing](https://aws.amazon.com/cognito/pricing/)
    * [Security Best Practices](https://docs.aws.amazon.com/cognito/latest/developerguide/security-best-practices.html)

### 3. Router Lambda (Componente Central)
- **Análise e Classificação**
  - Processamento inicial de todas as mensagens
  - Análise de keywords e padrões
  - Classificação de complexidade
  - Decisão de roteamento
  - SLA: 99.95% de disponibilidade
  - Referências:
    * [Lambda Documentation](https://docs.aws.amazon.com/lambda/)
    * [Lambda Pricing](https://aws.amazon.com/lambda/pricing/)
    * [Best Practices](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)

- **Regras de Negócio**
  - Armazenadas em DynamoDB
  - Atualizáveis em tempo real
  - Baseadas em métricas e feedback
  - Otimização contínua
  - Performance: < 10ms para decisões
  - Referências:
    * [DynamoDB Design Patterns](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html)

- **Sistema de Cache**
  - Cache de decisões frequentes
  - Otimização de performance
  - Redução de custos
  - Melhoria de latência
  - Hit rate esperado: > 60%
  - Referências:
    * [DynamoDB DAX](https://aws.amazon.com/dynamodb/dax/)
    * [Caching Best Practices](https://aws.amazon.com/caching/best-practices/)

- **Métricas e Ajustes**
  - Monitoramento de precisão
  - Ajuste automático de regras
  - Feedback loop contínuo
  - Otimização de custos
  - Referências:
    * [CloudWatch Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html)

### 4. Integração com IA
> Detalhes completos sobre modelos, performance e custos em [tech-ia.md](tech-ia.md)

- **Distribuição de Carga**
  - Claude 3.5 Sonnet: 70% das interações
  - Gemini 1.5 Pro: 25% das interações
  - GPT-4o: 5% das interações

### 5. Lógica de Negócios & Dados
- **Amazon DynamoDB**
  - Histórico de conversas
  - Regras de roteamento
  - Cache de decisões
  - Métricas e análises
  - Custo: Nível gratuito
  - SLA: 99.999% disponibilidade
  - Performance: < 10ms p99
  - Referências:
    * [DynamoDB Documentation](https://docs.aws.amazon.com/dynamodb/)
    * [DynamoDB Pricing](https://aws.amazon.com/dynamodb/pricing/)

### 6. Gestão de Conteúdo
- **Amazon S3**
  - Templates de resposta
  - Logs e análises
  - Cache de respostas
  - Documentos e mídia
  - Custo: Nível gratuito
  - SLA: 99.99% disponibilidade
  - Durabilidade: 99.999999999%
  - Referências:
    * [S3 Documentation](https://docs.aws.amazon.com/s3/)
    * [S3 Pricing](https://aws.amazon.com/s3/pricing/)

### 7. Monitoramento
- **Amazon CloudWatch**
  - Métricas do Router
  - Performance de IA
  - Logs e alertas
  - Dashboards
  - Custo: Nível gratuito
  - Retenção: 15 meses
  - Granularidade: 1 minuto
  - Referências:
    * [CloudWatch Documentation](https://docs.aws.amazon.com/cloudwatch/)
    * [CloudWatch Pricing](https://aws.amazon.com/cloudwatch/pricing/)

## Fluxo de Processamento

### 1. Análise Inicial (Router)
- **Processamento de Entrada**
  - Extração de keywords
  - Identificação de padrões
  - Análise de contexto
  - Verificação de cache
  - Latência: < 50ms
  - Precisão: > 95%

- **Classificação**
  - Avaliação de complexidade
  - Verificação de regras
  - Análise de histórico
  - Decisão de roteamento
  - Latência: < 100ms
  - Acurácia: > 90%

### 2. Distribuição de IA
> Detalhes de performance e casos de uso em [tech-ia.md](tech-ia.md)

- **Roteamento**
  - Baseado em complexidade
  - Otimizado por custo
  - Cache inteligente
  - Fallback automático

### 3. Otimização
- **Cache**
  - Respostas frequentes
  - Decisões comuns
  - Padrões identificados
  - Otimização de custos
  - Hit rate: > 60%
  - TTL: 24 horas

- **Feedback Loop**
  - Métricas de precisão
  - Ajuste de regras
  - Melhoria contínua
  - Aprendizado do sistema
  - Ciclo: 1 hora
  - Threshold: 5% variação

## Estimativa de Custos

### Custos Fixos (AWS)
- API Gateway: $1-2
- Lambda: Nível gratuito
- DynamoDB: Nível gratuito
- S3: Nível gratuito
- CloudWatch: Nível gratuito
- Cognito: Nível gratuito

### Custos de IA
> Detalhamento completo em [tech-ia.md](tech-ia.md)

**Total Mensal: $9-14**
(Dentro do limite de $50)

## Benefícios da Arquitetura

### 1. Eficiência
- Roteamento inteligente
  * Latência < 50ms
  * Precisão > 95%
- Cache otimizado
  * Hit rate > 60%
  * TTL configurável
- Distribuição adequada
  * Load balancing automático
  * Fallback entre modelos
- Baixa latência
  * P95 < 2s
  * P99 < 4s

### 2. Custo-Benefício
- Uso otimizado de IA
  * Roteamento inteligente
  * Cache efetivo
- Cache eficiente
  * Redução de 40% em custos
  * Melhoria de 60% em latência
- Free tier AWS
  * Máximo aproveitamento
  * Monitoramento de limites
- Controle de custos
  * Alertas automáticos
  * Otimização contínua

### 3. Qualidade
- Modelo apropriado por caso
  * Precisão otimizada
  * Custo-benefício
- Alta precisão
  * > 90% geral
  * > 95% casos críticos
- Respostas consistentes
  * Padronização
  * Versionamento
- Melhoria contínua
  * Feedback loop
  * Ajustes automáticos

### 4. Manutenibilidade
- Arquitetura modular
  * Componentes isolados
  * Baixo acoplamento
- Regras atualizáveis
  * Sem downtime
  * Versionamento
- Monitoramento completo
  * Métricas detalhadas
  * Alertas proativos
- Ajustes simplificados
  * Interface de configuração
  * Rollback automático

### 5. Escalabilidade
- Serverless
  * Auto-scaling
  * Pay-per-use
- Auto-scaling
  * Horizontal
  * Vertical
- Distribuição de carga
  * Load balancing
  * Rate limiting
- Redundância
  * Multi-região
  * Multi-modelo

## Links Úteis

### AWS Services
- [API Gateway](https://aws.amazon.com/api-gateway/)
- [Lambda](https://aws.amazon.com/lambda/)
- [DynamoDB](https://aws.amazon.com/dynamodb/)
- [S3](https://aws.amazon.com/s3/)
- [CloudWatch](https://aws.amazon.com/cloudwatch/)
- [Cognito](https://aws.amazon.com/cognito/)
- [Bedrock](https://aws.amazon.com/bedrock/)

### Best Practices
- [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/)
- [Serverless Best Practices](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)
- [Security Best Practices](https://docs.aws.amazon.com/security/)

## Pontos de Atenção para Diagramas

### 1. Diagrama de Arquitetura Geral
- **Componentes Principais**
  - Interface do Usuário (API Gateway + WebSocket)
  - Router Lambda (Componente Central)
  - Serviços de IA (Claude, Gemini, GPT-4)
  - Armazenamento (DynamoDB, S3)
  - Monitoramento (CloudWatch)
- **Fluxos de Dados**
  - Entrada de mensagens
  - Roteamento de IA
  - Cache e otimização
  - Monitoramento e logs

### 2. Diagrama de Fluxo de Roteamento
- **Análise Inicial**
  - Entrada da mensagem
  - Extração de características
  - Classificação de complexidade
  - Decisão de roteamento
- **Seleção de Modelo**
  - Gemini para casos simples (25%)
  - Claude para casos médios (70%)
  - GPT-4 para casos complexos (5%)
- **Fallback e Recuperação**
  - Detecção de falhas
  - Estratégia de retry
  - Mudança de modelo
  - Cache de respostas

### 3. Diagrama de Integração
- **Sistemas Internos**
  - Base de conhecimento
  - Sistema de cache
  - Logs e métricas
- **APIs Externas**
  - AWS Bedrock (Claude)
  - Google Cloud (Gemini)
  - Azure OpenAI (GPT-4)
- **Monitoramento**
  - Métricas por modelo
  - Alertas de custo
  - Performance tracking

### 4. Diagrama de Sequência
- **Fluxo Principal**
  1. Recebimento da mensagem
  2. Análise e classificação
  3. Seleção do modelo
  4. Processamento da resposta
  5. Entrega ao usuário
- **Fluxos Alternativos**
  - Cache hit
  - Fallback entre modelos
  - Escalonamento para humano
  - Tratamento de erros

### 5. Diagrama de Componentes
- **Router Lambda**
  - Analisador de mensagens
  - Classificador de complexidade
  - Seletor de modelo
  - Gerenciador de cache
- **Serviços de IA**
  - Interfaces de API
  - Gerenciadores de contexto
  - Otimizadores de prompt
  - Monitores de performance

## Jornada do Usuário
> Detalhes completos sobre interação com IA em [tech-ia.md](tech-ia.md)

### 1. Primeiro Contato
- **Canais de Entrada**
  - Website: Interface web responsiva
  - WhatsApp: API Business oficial
  - App: Aplicativo móvel nativo
  - Email: Integração SMTP

### 2. Identificação
- **Processos**
  - Login/Cadastro via Cognito
  - Verificação de identidade
  - Recuperação de histórico
  - Definição de preferências

### 3. Análise e Roteamento
- **Router Lambda**
  - Análise da mensagem
  - Classificação de complexidade
  - Seleção do modelo adequado
  - Preparação de contexto

### 4. Resolução
- **Processamento**
  - Resposta do modelo selecionado
  - Validação de qualidade
  - Enriquecimento de contexto
  - Formatação adequada
- **Feedback**
  - Coleta de satisfação
  - Ajustes de roteamento
  - Melhoria contínua
  - Métricas de qualidade
