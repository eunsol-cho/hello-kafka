# Hello Kafka 👋🏻

## [실전 카프카 개발부터 운영까지](https://www.yes24.com/Product/Goods/104410708?pid=123487&cosemkid=go16352122654963899&gad_source=1&gclid=CjwKCAiA8sauBhB3EiwAruTRJhbQsx-mucqyBEq-uZ1cB_K8sRnOMUfBEqSvoT64PKD1XEwG5lrxuBoCBe4QAvD_BwE)

💻 [Source code](https://github.com/eunsol-cho/hello-kafka/tree/main/basic) <br>
✏️ [Summary](https://golden-age-825.notion.site/b8cacd9d0db54901a67b736888465803?pvs=4) <br>

<details>
<summary>🪣 kafka 실습 환경구성</summary>
- 구성 : zookper(1) + kafaka(3) + kafdrop(1)
```yml
version: '3'
services:
  zookeeper:
    image: zookeeper:3.7
    hostname: zookeeper
    ports:
      - "2181:2181"
    environment:
      ZOO_MY_ID: 1
      ZOO_PORT: 2181
    volumes:
      - ./data/zookeeper/data:/data
      - ./data/zookeeper/datalog:/datalog
  kafka1:
    image: confluentinc/cp-kafka:7.0.0
    hostname: kafka1
    ports:
      - "9091:9091"
    environment:
      KAFKA_ADVERTISED_LISTENERS: LISTENER_DOCKER_INTERNAL://kafka1:19091,LISTENER_DOCKER_EXTERNAL://${DOCKER_HOST_IP:-127.0.0.1}:9091
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: LISTENER_DOCKER_INTERNAL:PLAINTEXT,LISTENER_DOCKER_EXTERNAL:PLAINTEXT
      KAFKA_INTER_BROKER_LISTENER_NAME: LISTENER_DOCKER_INTERNAL
      KAFKA_ZOOKEEPER_CONNECT: "zookeeper:2181"
      KAFKA_BROKER_ID: 1
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
    volumes:
      - ./data/kafka1/data:/tmp/kafka-logs
    depends_on:
      - zookeeper
  kafka2:
    image: confluentinc/cp-kafka:7.0.0
    hostname: kafka2
    ports:
      - "9092:9092"
    environment:
      KAFKA_ADVERTISED_LISTENERS: LISTENER_DOCKER_INTERNAL://kafka2:19092,LISTENER_DOCKER_EXTERNAL://${DOCKER_HOST_IP:-127.0.0.1}:9092
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: LISTENER_DOCKER_INTERNAL:PLAINTEXT,LISTENER_DOCKER_EXTERNAL:PLAINTEXT
      KAFKA_INTER_BROKER_LISTENER_NAME: LISTENER_DOCKER_INTERNAL
      KAFKA_ZOOKEEPER_CONNECT: "zookeeper:2181"
      KAFKA_BROKER_ID: 2
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
    volumes:
      - ./data/kafka2/data:/tmp/kafka-logs
    depends_on:
      - zookeeper
  kafka3:
    image: confluentinc/cp-kafka:7.0.0
    hostname: kafka3
    ports:
      - "9093:9093"
    environment:
      KAFKA_ADVERTISED_LISTENERS: LISTENER_DOCKER_INTERNAL://kafka3:19093,LISTENER_DOCKER_EXTERNAL://${DOCKER_HOST_IP:-127.0.0.1}:9093
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: LISTENER_DOCKER_INTERNAL:PLAINTEXT,LISTENER_DOCKER_EXTERNAL:PLAINTEXT
      KAFKA_INTER_BROKER_LISTENER_NAME: LISTENER_DOCKER_INTERNAL
      KAFKA_ZOOKEEPER_CONNECT: "zookeeper:2181"
      KAFKA_BROKER_ID: 3
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
    volumes:
      - ./data/kafka3/data:/tmp/kafka-logs
    depends_on:
      - zookeeper
  kafdrop:
    image: obsidiandynamics/kafdrop
    restart: "no"
    ports:
      - "9000:9000"
    environment:
      KAFKA_BROKER_CONNECT: "kafka1:19091"
    depends_on:
      - kafka1
      - kafka2
      - kafka3%
```
</details>

## [카프카 스트림즈와 ksqlDB 정복](https://m.yes24.com/Goods/Detail/115226495)

💻 [Source code](https://github.com/eunsol-cho/hello-kafka/tree/main/streams) <br>
✏️ [Summary](https://golden-age-825.notion.site/ksqlDB-a8eaa4f2668b453fb4dadf3c91c673c6?pvs=4) <br>