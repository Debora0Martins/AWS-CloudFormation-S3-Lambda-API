# Desafio DIO - AWS Lambda + DynamoDB com CloudFormation

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

## Como Executar
1. Acesse o AWS Console → CloudFormation  
2. Crie a Stack com o template desejado  
3. Configure a Lambda com variáveis de ambiente (`TABLE_NAME`)  
4. Teste a Lambda usando JSON de exemplo:  
```json

5. Verifique os logs no CloudWatch  
6. Confirme a inserção no DynamoDB  

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

## Codigo
index.js da Lambda (/src/lambda/index.js)

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

## Dynamodb

insertItem.js do DynamoDB (/src/dynamodb/insertItem.js)

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

---

## Recursos Úteis

### Documentação Oficial AWS
- [AWS CloudFormation](https://docs.aws.amazon.com/cloudformation/index.html) – Documentação completa para criar e gerenciar stacks.
- [AWS Lambda](https://docs.aws.amazon.com/lambda/index.html) – Guia de funções Lambda, triggers e integração com outros serviços.
- [AWS DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/) – Tutoriais e referências sobre tabelas, tipos de dados e operações.

### Material DIO
- [Formação AWS na DIO](https://digitalinnovation.one/) – Cursos e laboratórios oficiais.
- Laboratórios sobre Step Functions, Lambda e CloudFormation.

### GitHub
- [Guia do GitHub](https://docs.github.com/) – Como organizar repositórios, criar arquivos, commits e branches.
- [Markdown no GitHub](https://guides.github.com/features/mastering-markdown/) – Guia rápido para formatação de README.md.

### Extras
- [Node.js Documentation](https://nodejs.org/en/docs/) – Referência para JavaScript e Node.js.
- [Stack Overflow](https://stackoverflow.com/) – Comunidade para tirar dúvidas técnicas.

✍️ Autor: Débora Martins
📌 Repositório criado como parte do desafio DIO — 2025
📄 Licença: MIT
