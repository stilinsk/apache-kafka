
mv server.properties server-0.properties

cp server -0.properties server-1.properties

cp server -0.properties server-2.properties


 
 
 
 zookeeper-server-start.sh -daemon zookeeper.properties

kafka-server-start.sh -daemon server-0.properties

 kafka-server-start.sh -daemon server-1.properties


kafka-server-start.sh -daemon server-2.properties


kafka-topics.sh --create --bootstrap-server localhost:9092 --topic first-topic --partitions 2 --replication-factor 3


kafka-console-producer.sh --broker-list localhost:9092,localhost:9093 --topic first-topic


kafka-console-consumer.sh --bootstrap-server localhost:9092,localhost:9093 --topic first-topic --from-beginning


kafka-server-stop.sh


zookeeper-server-stop.sh




