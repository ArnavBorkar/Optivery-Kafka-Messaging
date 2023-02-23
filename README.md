# Optivery - Kafka based Communication Backend


- A real time communication backend for cabs booking system using containerized Kafka Messaging broker managed by a Zookeeper container
      
-  App ’generator’ simulates cab bookings and ’detector’ manages bookings and fraud ride detection

-  Communication between these python applications takes place over a docker network.



## Usage

- This project is fully containerised. You will need Docker and Docker Compose in order to run it.

- Create a Docker network called kafka-network to enable communication between the Kafka cluster and the apps:

```
$ docker network create kafka-network
```



### Commands
- To start the single node Kafka cluster
```
$ docker-compose -f docker-compose.kafka.yml up -d
```
Check if the cluster is running
```
$ docker-compose -f docker-compose.kafka.yml logs -f broker 
```
- Start the python apps,
generator simulates the cab bookings and detector manages booking
```
$ docker-compose up -d
```

- Show a stream of transactions in the topic T
```
$ docker-compose -f docker-compose.kafka.yml exec broker kafka-console-consumer --bootstrap-server localhost:9092 --topic T
```
Available topics
```
- `queuing.transactions`: All cab booking requests
- `streaming.transactions.legit`: Genuine and accepted bookings
- `streaming.transactions.fraud`: Rejected/fraud bookings
```
- To stop both python apps
```
$ docker-compose down
```
- To stop Kafka cluster
```
$ docker-compose -f docker-compose.kafka.yml stop
```


## Built With

* [Apache Kafka](https://kafka.apache.org/) - The message broker
* [Apache Zookeeper](https://zookeeper.apache.org/) - Management service
* [Docker-Compose](https://docs.docker.com/compose/) - To run multi-container Docker apps



