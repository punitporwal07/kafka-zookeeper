#  kafka-zookeeper
## kafka repository with ZooKeeper on K8s
### Replace Pod name

KAFKA TESTING -
```
export POD_NAME=$(kubectl get pods --namespace kafka -l "app.kubernetes.io/name=kafka,app.kubernetes.io/instance=kafka,app.kubernetes.io/component=kafka" -o jsonpath="{.items[0].metadata.name}")
```
CREATING A TOPIC 
```
kubectl --namespace kafka exec -it pod/kafka-broker0-9cd6dd669-l4qcc -- kafka-topics.sh --create --zookeeper zoo1:2181 --replication-factor 1 --partitions 1 --topic mytopic
```
STARTING MSG CONSUMER 
```
kubectl --namespace kafka exec -it pod/kafka-broker0-9cd6dd669-l4qcc -- kafka-console-consumer.sh --bootstrap-server kafka-service:9092 --topic mytopic --consumer.config /opt/kafka/config/consumer.properties &
```
STARTING MSG PRODUCER
```
kubectl --namespace kafka exec -it pod/kafka-broker0-9cd6dd669-l4qcc -- kafka-console-producer.sh --broker-list kafka-service:9092 --topic mytopic --producer.config /opt/kafka/config/producer.properties
```
