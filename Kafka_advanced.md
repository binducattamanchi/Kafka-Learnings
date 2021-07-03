# Kafka Connect

![image](https://user-images.githubusercontent.com/32897934/124346431-68b70b00-dbfc-11eb-87a0-9603c8c34387.png)

Kafka Connect is a framework for connecting Kafka with external systems such as databases, key-value stores, search indexes, and file systems.
* Source Connector: A source connector collects data from a source system. Source systems can be entire databases, tables, or any message brokers. A source connector could also collect metrics from application servers into Kafka topics, making the data available for stream processing with low latency.
* Sink Connector: A sink connector reads data from Kafka topics into other systems, which might be indexed such as Elasticsearch, Hadoop or any other database.


# Kafka Replication Mechanism

Kafka-read-scalability-768x543.jpeg![Kafka-read-scalability-768x543](https://user-images.githubusercontent.com/32897934/124346422-5b018580-dbfc-11eb-8023-88d74364239b.jpeg)

The mechanism which brokers use to interact with each other in one cluster.
* Controller: The replica which is responsible for leader election
 - Kafka uses Zookeeper for replica management, when we set up a Kafka cluster, every node in the cluster requests an ephemeral node to zookeeper to be controller
 - the ephemeral node is a temporary node that exists until the session that created node is active.
 - The controller is responsible for leader election. When we setup cluster for the first time, leaders for every partition chosen by round robin algorithm. In this way, the load is balanced over all of the brokers.
 
* Leader: The replica that all requests from clients and other brokers of Kafka go to it. Each partition can only have one leader at a time.
* Follower: Other replicas that are not the leader.
* In-sync replica: replicas that frequently request for latest messages are considered in-sync.
