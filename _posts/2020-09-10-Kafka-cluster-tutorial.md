---
layout:	post
title:	"Kafka Cluster tutorial"
date:	2020-09-10 22:40:00
category: [Programming]



---



# kafka-cluster-tutorial

Create simple kafka cluster easily!
</br>
</br>

### Download

[Apache Kafka](http://kafka.apache.org/downloads)

my version is  `2.12-2.3.0`

</br>
</br>

### Start Server

Before start **kafka**, we need to start zookeeper first.
</br>
</br>

### config files

```bash
#zookeeper / kafka config files
$ vi config/zookeeper.properties

$ vi config/server.properties
```

</br>
</br>

### start zookeeper & kafka

```bash
$ bin/zookeeper-server-start.sh
$ bin/kafka-server-start.sh
```

you can see messages

![image](https://user-images.githubusercontent.com/46887352/90518317-8f658200-e1a1-11ea-9935-8d7e8a870e4f.png)


</br>
</br>
</br>

### Multi broker cluster

**1. Create each properties**

```bash
$ cp config/server.properties config/server1.properties
$ cp config/server.properties config/server2.properties
```
</br>

**2. Modify each config files**

```bash
#server1
config/server1.properties:
	broker.id=1
	listeners=PLAINTEXT://:9094
	log.dirs=/tmp/kafka-logs-1

#server2
config/server2.properties:
	broker.id=2
	listeners=PLAINTEXT://:9095
	log.dirs=/tmp/kafka-logs-2
```
</br>

**3. Start Replicated nodes** 

```bash
$ bin/kafka-server-start.sh config/server1.properties &
$ bin/kafka-server-start.sh config/server2.properties &
```

</br>

**4. Create new topic** 

```bash
$ bin/kafka-topics.sh --create --bootstrap-server localhost:9093 --replication-factor 3 --partitions 1 --topic my-replicated-topic
```

`kafka-topics.sh` : topic execute file </br>
`replication-factor` : can decide replica count </br>
`partitions` : can decide partition count </br>


</br>


**5. Check topic** 

```bash
$ bin/kafka-topics.sh --describe --bootsrap-server localhost:9093 --topic my-replicated-topic
```

![image](https://user-images.githubusercontent.com/46887352/90518333-98565380-e1a1-11ea-8f01-4bde16f4c520.png)


`[broker.id](http://broker.id)` : cluster에서 각 노드의 식별 가능한 영구적인 id, broker가 여러개가 되면, leader node가 생성된다. 

`Replicas` :  구성된 node 목록

`Isr` : 현재 살아있는 node

`zookeeper port`  ⇒ 2182

</br>
</br>

Ref.

[Apache Kafka](https://kafka.apache.org/documentation/)

</br>
</br>

### Useful Commands

```bash
##stop server
$ bin/kafka-server-stop.sh config/server.properties
$ bin/kafka-server-stop.sh config/server1.properties
$ bin/kafka-server-stop.sh config/server2.properties
$ bin/zookeeper-server-stop.sh config/zookeeper.properties

##start server
##before start kafka, you should run zookeeper first
$ bin/zookeeper-server-start.sh config/zookeeper.properties &
$ bin/kafka-server-start.sh config/server.properties &

##search topic
$ ./bin/kafka-topics.sh --list --bootstrap-server localhost:9093

```
</br>
</br>

</br>