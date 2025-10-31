# Laboratório AWS – Lambda Function e Amazon S3

## 📌 Objetivo

O objetivo deste laboratório é **consolidar conhecimentos em tarefas automatizadas** utilizando **AWS Lambda** e **Amazon S3**, praticando conceitos de **serverless** e **automação de processos** na nuvem.

Neste laboratório, você aprenderá a:

* Criar **Lambda Functions** para execução automática de tarefas
* Integrar **Lambda** com o **S3**, disparando funções a partir de eventos de buckets
* Automatizar **processamento de arquivos**, como logs, uploads ou transformação de dados
* Monitorar e verificar execução de funções via **CloudWatch Logs**

---

## 📚 Conceitos Aprendidos

* **AWS Lambda:** serviço serverless que executa código sem precisar gerenciar servidores.
* **Amazon S3:** armazenamento de objetos na nuvem, usado como fonte ou destino de dados.
* **Eventos do S3:** gatilhos que disparam Lambda quando arquivos são criados, modificados ou deletados.
* **IAM Roles e Policies:** permissões necessárias para Lambda acessar S3, CloudWatch e outros serviços.
* **CloudWatch Logs:** monitoramento de execuções e erros das funções Lambda.

---

## 🛠️ Serviços e Ferramentas Utilizadas

* **AWS Lambda:** criação e execução de funções serverless
* **Amazon S3:** armazenamento e eventos para disparo de funções
* **AWS IAM:** criação de roles e policies para permissões da Lambda
* **AWS CloudWatch:** monitoramento e logs de execução
* **AWS CLI / Console:** deploy, configuração e testes das funções

---

## 📝 Passo a Passo da Implementação

1. **Criação do Bucket no S3**

   * Crie um bucket novo no S3.
   * Ative eventos para notificar o Lambda quando arquivos forem adicionados.

2. **Criação da Role IAM**

   * Criar uma **IAM Role** com permissão para acessar S3 e CloudWatch.

3. **Criação da Lambda Function**

   * Criar função Lambda (Node.js, Python ou outra linguagem suportada).
   * Associar a **IAM Role** criada.
   * Configurar **gatilho do S3** apontando para o bucket criado.

4. **Exemplo de Função Lambda**

   ```python
   import json
   import boto3

   def lambda_handler(event, context):
       s3 = boto3.client('s3')
       for record in event['Records']:
           bucket = record['s3']['bucket']['name']
           key = record['s3']['object']['key']
           print(f"Arquivo {key} enviado para o bucket {bucket}")
       return {
           'statusCode': 200,
           'body': json.dumps('Processamento concluído!')
       }
   ```

5. **Testes**

   * Faça upload de arquivos no bucket S3.
   * Verifique se a Lambda é disparada automaticamente.
   * Analise logs no **CloudWatch** para conferir execução e mensagens.

6. **Automação e monitoramento**

   * Ajuste triggers, timeout, memória e monitoramento conforme necessidade.
   * Use **CloudWatch Alarms** para notificações em caso de falhas.

---

## 💡 Insights e Boas Práticas

* **Serverless simplifica infraestrutura:** sem necessidade de gerenciar servidores físicos ou virtuais.
* **IAM Roles são essenciais:** sempre conceda apenas permissões mínimas necessárias (princípio do menor privilégio).
* **Eventos do S3 são poderosos:** permitem automatizar pipelines de dados ou processamento de arquivos.
* **CloudWatch Logs é fundamental:** monitoramento em tempo real ajuda a identificar e corrigir problemas.
* **Testes em ambiente controlado:** sempre testar funções com arquivos de teste antes de colocar em produção.

---

## 📂 Estrutura do Repositório

```
aws-lambda-s3-lab/
│
├── README.md                 # Este arquivo
├── lambda_function.py        # Código da Lambda
└── notas-de-estudo.md        # Anotações e insights do laboratório
