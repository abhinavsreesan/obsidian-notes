[[Kafka]]

REF: [Kafka Basics and Core concepts](https://medium.com/inspiredbrilliance/kafka-basics-and-core-concepts-5fd7a68c3193)

## Message

- A message is the **atomic unit** of data for Kafka.

- You can push String, Integer, a JSON of different schema, and everything else, but we generally push different types of messages into different topics.

- Messages might have an associated “Key” which is nothing but some metadata, which is used to determine the destination partition.

## Topic

- Topics, as the name suggests, are the **logical categories of messages in Kafka**, a stream of the same type of data. 
- It allows us to have logical segregation between messages, sort of like having different tables for holding different types of data.

## Partitions

- Partition is analogous to [shard](https://blog.yugabyte.com/how-data-sharding-works-in-a-distributed-sql-database) in the database and is the core concept behind Kafka’s scaling capabilities. 

- When we split data of a topic into multiple streams, we call all of those smaller streams the “Partition” of that topic.

![](https://miro.medium.com/max/700/1*pG3veZFlunxKRl9LlFhu-g.png)

Source: Kafka The Definitive Guide

This image depicts the idea of partitions, where a single topic has 4 partitions, and all of them hold a different set of data. The blocks you see here are the different messages in that partition. Let’s imagine the topic to be an array, now due to memory constraint we have split the single array into 4 different smaller arrays. And when we write a new message to a topic, the relevant partition is selected and then that message is added at the end of the array.

An offset for a message is the index of the array for that message. The numbers on the blocks in this picture denote the **Offset,** the first block is at the 0th offset and the last block would on the (n-1)th offset. The performance of the system also depends on the ways you set up partitions, we will look into that later in the article. 

## Producer

A producer is the Kafka client that **publishes messages to a Kafka topic**. Also one of the core responsibilities of the Producer is to decide which partition to send the messages to. Depending on various configuration and parameters, the producer decides the destination partition, let’s look a bit more into this.

1.  **No Key specified =>** When no key is specified in the message the producer will randomly decide partition and would try to balance the total number of messages on all partitions.
2.  **Key Specified =>** When a key is specified with the message, then the producer uses [Consistent Hashing](https://www.toptal.com/big-data/consistent-hashing) to map the key to a partition. Don’t worry if you don’t know what consistent hashing is, in short, it’s a hashing mechanism where for the same key same hash is generated always, and it minimizes the redistribution of keys on a re-hashing scenario like a node add or a node removal to the cluster. So let’s say in our logging system we use source node ID as the key, then the logs for the same node will always go to the same partition. This is very relevant for the order guarantees of messages in Kafka, we will shortly see how.
3.  **Partition Specified =>** You can hardcode the destination partition as well.
4.  **Custom Partitioning logic =>** We can write some rules depending on which the partition can be decided.

## Consumer

- So far we have produced messages, to **read those messages we use Kafka consumer**. A consumer reads messages from partitions, in an ordered fashion. So if 1, 2, 3, 4 was inserted into a topic, the consumer will read it in the same order. 

- Since every message has an offset, every time a consumer reads a message it stores the offset value onto Kafka or Zookeeper, denoting that it is the last message that the consumer read. So in case, a consumer node goes down, it can come back and resume from the last read position. Also if at any point in time a consumer needs to go back in time and read older messages, it can do so by just resetting the offset position.

## Broker

A broker is a single Kafka server. Brokers receive messages from producers, assigns offset to them, and then commit them to the partition log, which is basically writing data to disk, and this gives Kafka its **_durable_** nature.

# Cluster

A Kafka cluster is a group of broker nodes working together to provide, scalability, availability, and fault tolerance. One of the brokers in a cluster works as the Controller, which basically assigns partitions to brokers, monitors for broker failure to do certain administrative stuff.

In a cluster, partitions are replicated on multiple brokers depending on the replication factor of the topic to have **_failover_** capability. What I mean is, for a topic of replication factor 3, each partition of that topic will live onto 3 different brokers. When a partition is replicated onto 3 brokers, one of the brokers will act as the leader for that partition and the rest two will be followers. Data is always written on the leader broker and then replicated to the followers. This way we do not lose data nor availability of the cluster, and if the leader goes down another leader is elected.

# Zookeeper

Kafka does not function without zookeeper( at least for now, they have plans to deprecate zookeeper in near future). Zookeeper works as the central configuration and consensus management system for Kafka. It tracks the brokers, topics, and partition assignment, leader election, basically all the metadata about the cluster.