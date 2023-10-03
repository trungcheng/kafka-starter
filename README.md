1. General
    - Là 1 streaming platform
    - Là 1 nền tảng điều phối message trong các hệ thống phân tán
    - Có khả năng chịu lỗi cao, commit log, horizontally-scalable

2. Components
    - Producer: Gửi message đến broker.
    - Consumer: Nhận message từ broker.
    - Broker: Vai trò môi giới, vận chuyển message từ producer đến consumer.
    - Cluster: cụm của 1 hoặc nhiều broker, Zoo Keeper là công cụ điều hành cluster, đưa ra chỉ định broker thay thế khi có 1 broker bị lỗi.
    - Topic: chủ đề (unique name) trong hệ thống Kafka Cluster, dùng để phân nhóm message theo chủ đề, có thể có nhiều các partitions nhỏ.
    - Partitions: các vùng nhỏ trong hệ thống kafka topic.
    - Offset: ô thứ tự trong 1 cụm partition.
    - Consumer groups: nhóm các consumer để lấy thông tin khi có 1 lượng lớn data được gửi từ nhiều producer.

3. Document: https://kafka.apache.org/quickstart

4. Commands:
    - Start ZooKeeper: bin/zookeeper-server-start.sh config/zookeeper.properties
    - Start Kafka Broker: bin/kafka-server-start.sh config/server.properties
    - Lấy danh sách ID các broker đang active: bin/zookeeper-shell.sh localhost:2181 ls /brokers/ids
    - Lấy ra thông tin của 1 broker bởi id: bin/zookeeper-shell.sh localhost:2181 get /brokers/ids/0
    - Tạo topic: bin/kafka-topics.sh --create --topic ${topic_name} --bootstrap-server localhost:9092
    - Mô tả topic: bin/kafka-topics.sh --describe --topic ${topic_name} --bootstrap-server localhost:9092
    - Gửi message bằng producer: bin/kafka-console-producer.sh --topic ${topic_name} --bootstrap-server localhost:9092
    - Đọc message bằng consumer: bin/kafka-console-consumer.sh --topic ${topic_name} --from-beginning --bootstrap-server localhost:9092
    - Tạo topic với số lượng partitions: bin/kafka-topics.sh --create --zookeeper localhost:9092 --replication-factor 1 --partitions 3 --topic ${topic_name}
    - Mô tả offset trong Kafka topic và tạo consumer group: bin/kafka-console-consumer.sh --topic ${topic_name} --bootstrap-server localhost:9092 --from-beginning --group ${group_name}
    - Show topic và offset của partition: bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group ${group_name} --describe
    - Đọc message trong partition bằng offset: bin/kafka-console-consumer.sh --topic ${topic_name} --bootstrap-server localhost:9092 --partition 1 --offset 2
