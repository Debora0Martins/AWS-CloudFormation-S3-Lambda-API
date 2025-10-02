# DIO - AWS Lambda + DynamoDB

Aplicação serverless AWS Lambda, DynamoDB e CloudFormation criando uma função Lambda que insere itens em uma tabela DynamoDB e registra logs no CloudWatch.

## Serviços usados:

AWS Lambda: Serviço de computação sem servidor que executa código em resposta a eventos.

DynamoDB: Banco de dados NoSQL da AWS para armazenamento rápido e escalável de dados.

CloudFormation: Serviço de infraestrutura como código, que permite criar e gerenciar recursos da AWS de forma automatizada.

CloudWatch: Serviço de monitoramento e logs da AWS.

O que fizemos no projeto:

Criamos uma função Lambda que é responsável por processar dados de entrada.

A função Lambda insere itens em uma tabela do DynamoDB, armazenando informações de forma estruturada e escalável.

Registramos logs no CloudWatch, permitindo monitorar a execução da função, identificar erros e acompanhar o desempenho.

Automatizamos a criação da infraestrutura usando CloudFormation, garantindo que a função Lambda, a tabela DynamoDB e as permissões necessárias fossem criadas de forma organizada e reproduzível.

## Passos
1. Acesse o AWS Console → CloudFormation  
2. Crie a Stack com o template desejado  
3. Configure a Lambda com variáveis de ambiente (`TABLE_NAME`)  
4. Teste a Lambda usando JSON de exemplo:
json
{
  "produto": "Caneta",
  "preco": "2",
  "quantidade": "30"
}

5.	Verifique os logs no CloudWatch
	6.	Confirme a inserção no DynamoDB

Funcionalidades
	•	Recebe dados de produto via JSON
	•	Insere itens no DynamoDB
	•	Loga erros e sucesso no CloudWatch
	•	Permite variáveis de ambiente configuráveis
	•	Estrutura modular para expandir funcionalidades

## Aprendizado Pessoal

Durante este desafio, aprendi a integrar Lambda com DynamoDB usando Node.js, lidar com variáveis de ambiente e configurar stacks CloudFormation.
Identifiquei desafios em tipos de dados do DynamoDB e na configuração de permissões IAM, melhorando minha prática em AWS e automação de tarefas.

## Imagens

Todos os prints estão na pasta /images

Código

## index.js da Lambda (/src/lambda/index.js)

const { DynamoDBClient, PutItemCommand } = require("@aws-sdk/client-dynamodb");

const client = new DynamoDBClient({ region: "us-east-1" });
const TABLE_NAME = process.env.TABLE_NAME || "MinhaTabelaDemo";

exports.handler = async (event) => {
    const produto = event.produto || "ProdutoDemo";
    const preco = event.preco || "0";
    const quantidade = event.quantidade || "0";

    const item = {
        id: { S: Date.now().toString() },
        produto: { S: produto },
        preco: { N: preco.toString() },
        quantidade: { N: quantidade.toString() }
    };

    const command = new PutItemCommand({ TableName: TABLE_NAME, Item: item });

    try {
        await client.send(command);
        console.log("Item inserido:", item);
        return { statusCode: 200, body: JSON.stringify({ message: "Item inserido!", item }) };
    } catch (err) {
        console.error("Erro:", err);
        return { statusCode: 500, body: JSON.stringify({ message: "Erro ao inserir", error: err.message }) };
    }
};

## insertItem.js do DynamoDB (/src/dynamodb/insertItem.js)

const { DynamoDBClient, PutItemCommand } = require("@aws-sdk/client-dynamodb");

const client = new DynamoDBClient({ region: "us-east-1" });
const TABLE_NAME = process.env.TABLE_NAME || "MinhaTabelaDemo";

exports.insertItem = async (produto, preco, quantidade) => {
    const item = {
        id: { S: Date.now().toString() },
        produto: { S: produto },
        preco: { N: preco.toString() },
        quantidade: { N: quantidade.toString() }
    };

    const command = new PutItemCommand({ TableName: TABLE_NAME, Item: item });

    try {
        await client.send(command);
        console.log("Item inserido:", item);
    } catch (err) {
        console.error("Erro ao inserir item:", err);
    }
};

## Recursos Úteis

Documentação Oficial AWS
	•	AWS CloudFormation
	•	AWS Lambda
	•	AWS DynamoDB

## Material DIO
	•	Formação AWS na DIO

## GitHub
	•	Guia do GitHub
	•	Markdown no GitHub

## Extras
	•	Node.js Documentation
	•	Stack Overflow

✍️ Autor: Débora Martins
📌 Repositório criado como parte do desafio DIO — 2025
📄 Licença: MIT
