# Prepared docker-compose file to deploy kafka dev-cluster with sasl, ssl and acl

1. Start "generate.sh" script

```shell
./generate.sh
```


2. Start compose

```shell
docker-compose up -d
```


3. Stop

```shell
docker-compose down
```

to stop and delete all volumes:

```shell
docker-compose down -v
```


4. UI

web-ui: [localhost:8080](localhost:8080) (admin/admin)
grafana: [localhost:3000](localhost:3000) (admin/admin)


5. Topic creation

```shell
# topic creation
docker exec -it kafka-0 kafka-topics.sh --bootstrap-server localhost:9091 --create --topic test-topic --partitions 3 --replication-factor 3 --command-config /opt/bitnami/kafka/admin.properties

# create ACL for topic test-topic
docker exec -it kafka-0 kafka-acls.sh --bootstrap-server localhost:9091 --add --allow-principal User:da --operation All --group '*' --topic test-topic --command-config /opt/bitnami/kafka/admin.properties

# checking ACLs
docker exec -it kafka-0 kafka-acls.sh --bootstrap-server localhost:9091 --list --topic test-topic --command-config /opt/bitnami/kafka/admin.properties
```
