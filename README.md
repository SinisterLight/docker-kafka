# docker-kafka
Docker for kafka

### Run Image

docker build -t sinisterlight/kafka .
docker run -p 2181:2181 -p 9092:9092 --env ADVERTISED_HOST=$(docker-machine ip default) --env ADVERTISED_PORT=9092 sinisterlight/kafka

### Using Kafka

#### Set Env
export DOCKER_IP=$(docker-machine ip default)
export KAFKA=$DOCKER_IP:9092
export ZOOKEEPER=$DOCKER_IP:2181

#### Create a test topic
kafka-topics.sh --create --zookeeper $ZOOKEEPER --replication-factor 1 --partitions 1 --topic test
kafka-console-producer.sh --broker-list $KAFKA --topic test

#### Consume Events
kafka-console-consumer.sh --zookeeper $ZOOKEEPER --topic test
