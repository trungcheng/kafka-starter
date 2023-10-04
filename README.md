# General

1. Là 1 streaming platform
2. Là 1 nền tảng điều phối message trong các hệ thống phân tán
3. Có khả năng chịu lỗi cao, commit log, horizontally-scalable

# Components

1. Producer: Gửi message đến broker.
2. Consumer: Nhận message từ broker.
3. Broker: Vai trò môi giới, vận chuyển message từ producer đến consumer.
4. Cluster: cụm của 1 hoặc nhiều broker, ZooKeeper là công cụ điều hành cluster, đưa ra chỉ định broker thay thế khi có 1 broker bị lỗi.
5. Topic: chủ đề (unique name) trong hệ thống Kafka Cluster, dùng để phân nhóm message theo chủ đề, có thể có nhiều các partitions nhỏ.
6. Partitions: các vùng nhỏ trong hệ thống kafka topic.
7. Offset: ô thứ tự trong 1 cụm partition.
8. Consumer groups: nhóm các consumer để lấy thông tin khi có 1 lượng lớn data được gửi từ nhiều producer.

# Commands:

1. Start ZooKeeper: 
bin/zookeeper-server-start.sh config/zookeeper.properties

2. Start Kafka Broker: 
bin/kafka-server-start.sh config/server.properties

3. Get list of the active broker ids: 
bin/zookeeper-shell.sh localhost:2181 ls /brokers/ids

4. Get information the broker by id: 
bin/zookeeper-shell.sh localhost:2181 get /brokers/ids/0

5. Create topic: 
bin/kafka-topics.sh --create --topic ${topic_name} --bootstrap-server localhost:9092

6. Describe topic: 
bin/kafka-topics.sh --describe --topic ${topic_name} --bootstrap-server localhost:9092

7. Send message by producer: 
bin/kafka-console-producer.sh --topic ${topic_name} --bootstrap-server localhost:9092

8. Read message by consumer: 
bin/kafka-console-consumer.sh --topic ${topic_name} --from-beginning --bootstrap-server localhost:9092

9. Create topic with partition number: 
bin/kafka-topics.sh --create --zookeeper localhost:9092 --replication-factor 1 --partitions 3 --topic ${topic_name}

10. Describe offset in Kafka topic and create consumer group: 
bin/kafka-console-consumer.sh --topic ${topic_name} --bootstrap-server localhost:9092 --from-beginning --group ${group_name}

11. Show topic and offset of partition: 
bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group ${group_name} --describe

12. Read message in the partition by offset: 
bin/kafka-console-consumer.sh --topic ${topic_name} --bootstrap-server localhost:9092 --partition 1 --offset 2

# Document: https://kafka.apache.org/quickstart
