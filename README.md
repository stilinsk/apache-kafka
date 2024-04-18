
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


openssl req -new -x509 -keyout ca-key -out ca-cert -days 3650


keytool -keystore kafka.zookeeper-client.truststore.jks -alias ca-cert -import -file ca-cert


keytool -keystore kafka.zookeeper-client.keystore.jks -alias zookeeper-client -validity 3650 -genkey -keyalg RSA -ext SAN=dns:localhost


keytool -keystore kafka.zookeeper-client.keystore.jks -alias zookeeper-client -certreq -file ca-request-zookeeper-client


openssl x509 -req -CA ca-cert -CAkey ca-key -in ca-request-zookeeper-client -out ca-signed-zookeeper-client -days 3650 -CAcreateserial


keytool -keystore kafka.zookeeper-client.keystore.jks -alias ca-cert -import -file ca-cert

keytool -keystore kafka.zookeeper-client.keystore.jks -alias zookeeper-client -import -file ca-signed-zookeeper-client



