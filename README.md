# 💪 Challenge Inter Java Developer 

## 🏁 Getting Started

### Description!


Neste Labs vamos implantar uma aplicação escrita em Java/Kotlin no serviço    &nbsp;
Elastic Kubernetes Service da Amazon. A aplicação é um exemplo de padrão CQRS &nbsp;
que contempla dois serviços Quarkus que se comunicam através de um barramento &nbsp;
assíncrono usando o Kafka. Você vai aprender a criar manifestos do Kubernetes &nbsp;
para a implantação no EKS e quais configurações são necessárias para ter o    &nbsp; 
ambiente rodando em produção. 

## Deploying the external services

```
docker-compose up -d --build

```

Ele implantará quatro contêineres docker em seu ambiente com MongoDB, PostgreSQL, &nbsp;
Kafka e Zookepper (exigido por Kafka)

Depois de implantar o Kafka, você precisará criar o tópico no cluster Kafka. &nbsp;

Por exemplo:

```
docker exec -it bankaccount-kafka \
  ./bin/kafka-topics.sh --create \
  --topic transactions \
  --zookeeper bankaccount-zookeeper:2181 \
  --replication-factor 1 \
  --partitions 1
```

## Testing the application

# Executar uma solicitação CURL para criar uma transação

```
curl -X POST -H "Content-Type: application/json" -d @income-transaction.json http://localhost:8080/transactions
```

# Solicitação CURL em execução para uma busca balanceada

```
curl http://localhost:8081/balance\?accountId\=wesley | json_pp
``` 

# Executando o teste de desempenho simples do k6's

```
k6 run --vus 10 --duration 60s performance-tests/income.js
k6 run --vus 10 --duration 60s performance-tests/expense.js
```