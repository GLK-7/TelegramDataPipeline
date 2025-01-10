# Pipeline de Dados do Telegram

Este projeto implementa um pipeline de dados para capturar, processar e analisar mensagens enviadas em grupos do **Telegram**. A arquitetura é dividida em duas partes: a **transacional**, que utiliza o **Telegram** como fonte de dados, e a **analítica**, baseada na **AWS** para armazenamento e processamento dos dados.

## Arquitetura do Pipeline

### 1. **Captura de Dados (Transacional)**
Um *bot* do Telegram é adicionado a um grupo para monitorar mensagens enviadas pelos usuários. As mensagens são redirecionadas via *webhook* para um *endpoint* exposto pelo **AWS API Gateway**, que dispara a execução de uma função **AWS Lambda**. A função armazena o conteúdo em arquivos JSON no **AWS S3**, particionados por dia.

### 2. **Processamento de Dados (ETL)**
Um *job* diário acionado pelo **AWS EventBridge** processa os arquivos JSON do dia anterior. Os dados são denormalizados e salvos no formato **Apache Parquet**, orientado a colunas, e armazenados no **AWS S3**, também particionados por dia.

### 3. **Análise de Dados (Apresentação)**
Uma tabela do **AWS Athena** é configurada para acessar os arquivos processados no **S3**. Isso permite que profissionais de dados realizem análises e extraiam *insights* utilizando consultas SQL, como:
- Horários de maior uso do *bot*;
- Dúvidas ou problemas mais frequentes;
- Eficácia do *bot* na resolução de problemas.

## Objetivos do Projeto
O projeto fornece uma solução escalável e automatizada para a análise de mensagens do Telegram, habilitando a geração de *insights* acionáveis a partir dos dados coletados.

## Tecnologias Utilizadas
- **Telegram Bot API**
- **AWS API Gateway**
- **AWS Lambda**
- **AWS S3**
- **AWS EventBridge**
- **AWS Athena**
- **Apache Parquet**
- **SQL**

## Documentação Adicional
Consulte a [documentação oficial do Telegram Bot API](https://core.telegram.org/bots/api) para mais detalhes sobre como integrar o *bot* com a plataforma.

---
