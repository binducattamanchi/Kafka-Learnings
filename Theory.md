# Kafka
Apache Kafka is a distributed publish-subscribe messaging system and a robust queue that can handle a high volume of data and enables you to pass messages from one end-point to another. Kafka is suitable for both offline and online message consumption. Kafka messages are persisted on the disk and replicated within the cluster to prevent data loss. Kafka is built on top of the ZooKeeper synchronization service. It integrates very well with Apache Storm and Spark for real-time streaming data analysis.

![image](https://user-images.githubusercontent.com/32897934/124020017-63449f80-da07-11eb-9ce0-2b9a1e6aa0f0.png)


# Core Components

* Event: An event records the fact that "something happened" in the world or in your business. It is also called record or message in the documentation. Conceptually, an event has a key, value, timestamp, and optional metadata headers. Here's an example event:
Event key: "Alice"
Event value: "Made a payment of $200 to Bob"
Event timestamp: "Jun. 25, 2020 at 2:06 p.m."

* Producer : An application that  sends messages  to kafka (json,xml,string,file ). But for Kafka it is an array of bytes. 
Each row as a message .

![image](https://user-images.githubusercontent.com/32897934/124016470-4efea380-da03-11eb-85c6-3154e9e62d1e.png)

* Consumer : An application that reads data from kafka.
We Need to create consumer application and need to request to Kafka server with permission.
Consumer will keep requesting for message  as long as new message are coming from the producer.
![image](https://user-images.githubusercontent.com/32897934/124016671-88371380-da03-11eb-909c-a4ffe704271d.png)


* Broker : Kafka server is same as a Kafka broker.
Name is suitable because all that Kafka does is act as message broker between producer and consumer.

* Cluster : A group of computer sharing workload for a common purpose, Since Kafka is distributed system cluster has same meaning for Kafka.
![image](https://user-images.githubusercontent.com/32897934/124016812-a69d0f00-da03-11eb-97ff-07fee92bee1f.png)



* Topic : Topic is a unique name that given to data set for Kafka stream
Every point of sale may have a producer. Each of them send order detail to the single topic name Global Orders. Subscriber can subscribe for same topic if it is interested.
![image](https://user-images.githubusercontent.com/32897934/124016932-c3394700-da03-11eb-9171-91abdbda541a.png)

Compact Topic 
![image](https://user-images.githubusercontent.com/32897934/124017339-393dae00-da04-11eb-9287-f03026ff78b5.png)


* Partitions : Within the Kafka cluster, topics are divided into partitions, and the partitions are replicated across brokers. From each partition, multiple consumers can read from a topic in parallel. It’s also possible to have producers add a key to a message—all messages with the same key will go to the same partition.
 ![image](https://user-images.githubusercontent.com/32897934/124017187-10b5b400-da04-11eb-8006-1f213b9265d9.png)

* Offset : A Sequence id given to messages  as they  arrive  in a partition 
This number assign as the message arrives into the partition and these number once assigned then never changed, The sequence means Kafka store  message  in order of message arrival within the partition. Offset are local to the partition 

* Consumer groups : A group  of consumers acting as  a single  logical unit. Many consumer form group for share the work. 
![image](https://user-images.githubusercontent.com/32897934/124017525-7013c400-da04-11eb-9cd6-a892939282cb.png)


* Zookeeper : Kafka broker uses ZooKeeper for the purpose of managing and coordinating
 Also, uses it to notify producer and consumer about the presence of any new broker in the Kafka system or failure of the broker in the Kafka system. 


