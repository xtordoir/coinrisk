# Coinrisk

Crypto coins tracking for portfolio risk management

## 1. Docker images for services

Services are started using the docker-compose file in the `docker ` directory:

```
cd docker
docker-compose up
```

### Kafka

A `zookeeper` and a `kafka` container are started. Some tools are available in the `bin` directory to execute commands, e.g:

#### Topics

List topics:
```
bin/kafka-topics --zookeeper zookeeper:2181 --list
```

Create a topic named `test` (one partition, replication 1):

```
bin/kafka-topics --zookeeper zookeeper:2181 --partitions 1 --replication-factor 1 --topic test --create
```
See kafka documentation for options and usage.

#### Consumer

```
bin/kafka-console-consumer --bootstrap-server kafka:9092 --topic test
```

### Producer

```
bin/kafka-console-producer --broker-list kafka:9092 --topic test
```

### RiakTS? Cassandra? Postgresql?

## 2. Collector

A sample nodejs application is opening a subsrciption to a socket.io service provided by cryptocompare and logs the messages in stdout.

In its simplest form the collection consists is piping the node collector output to the `kafka-console-producer`, e.g.

```
node collectors/cryptocompare/stream.js | bin/kafka-console-producer --broker-list kafka:9092 --topic test
```
**TODO**: Are there other socket.io client implementations that would work? Or use a nodejs kafka library to publish directly?

## 3. Raw stream processing components

### Aggregator for current price

### Data dump to Time Series database

## 4. Raw streams Services

## 5. Raw streams dashboards

## 6. Derived streams/batch processing
