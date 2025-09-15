oi# Desafio DIO - AWS Lambda + DynamoDB com CloudFormation

## Objetivo
Consolidar o aprendizado sobre AWS CloudFormation criando uma Stack completa, integrando funções Lambda com DynamoDB, configurando variáveis de ambiente e documentando todo o processo.

## O que foi feito
- Criação de uma Stack no CloudFormation
- Implementação de uma Lambda API
- Integração da Lambda com DynamoDB para inserção de itens
- Configuração de variáveis de ambiente
- Teste da Lambda usando JSON de entrada
- Registro de prints e logs do CloudWatch

## Resultados
- Lambda executando corretamente e inserindo itens no DynamoDB
- Logs confirmando as operações
- Documentação completa com prints e anotações
- Estrutura pronta para estudo e referência futura

## Tecnologias Utilizadas
- AWS CloudFormation
- AWS Lambda
- AWS DynamoDB
- Node.js (JavaScript)
- GitHub (versionamento e documentação)

## Como Executar## 

1. Acesse o AWS Console → CloudFormation
2. Crie a Stack com o template desejado
3. Configure a Lambda com variáveis de ambiente (TABLE_NAME)
4. Teste a Lambda usando JSON de exemplo:
```json
{
  "produto": "Caneta",
  "preco": "2",
  "quantidade": "30"
}

- Verifique os logs no CloudWatch  
- Confirme a inserção no DynamoDB  

## Funcionalidades
- Recebe dados de produto via JSON
- Insere itens no DynamoDB
- Loga erros e sucesso no CloudWatch
- Permite variáveis de ambiente configuráveis
- Estrutura modular para expandir funcionalidades

## Aprendizado Pessoal
Durante este desafio, aprendi a integrar Lambda com DynamoDB usando Node.js, lidar com variáveis de ambiente e configurar stacks CloudFormation.  
Identifiquei desafios em tipos de dados do DynamoDB e na configuração de permissões IAM, melhorando minha prática em AWS e automação de tarefas.

## Imagens
Todos os prints estão na pasta `/images`

  Recursos Úteis

Documentação Oficial AWS
	•	AWS CloudFormation – Documentação completa para criar e gerenciar stacks.
	•	AWS Lambda – Guia de funções Lambda, triggers e integração com outros serviços.
	•	AWS DynamoDB – Tutoriais e referências sobre tabelas, tipos de dados e operações.

Material DIO
	•	Formação AWS na DIO – Cursos e laboratórios oficiais.

GitHub
	•	Guia do GitHub – Como organizar repositórios, criar arquivos, commits e branches.
	•	Markdown no GitHub – Guia rápido para formatação de README.md.

Extras
	•	Node.js Documentation – Referência para JavaScript e Node.js.
	•	Stack Overflow – Comunidade para tirar dúvidas técnicas.

✍️ Autor: Débora Martins
📌 Repositório criado como parte do desafio DIO — 2025
📄 Licença: MIT

