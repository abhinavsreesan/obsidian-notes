**Kafka is a Distributed Streaming Platform or a Distributed Commit Log**

**Distributed**  
Kafka works as a cluster of one or more nodes that can live in different Datacenters, we can distribute data/ load across different nodes in the Kafka Cluster, and it is inherently scalable, available, and fault-tolerant.

**Streaming Platform**

Kafka stores data as a **stream of continuous records** which can be processed in different methods.

**Commit Log**

This one is my favorite. When you push data to Kafka it takes and appends them to a stream of records, like appending logs in a log file or if you’re from a Database background like the [WAL](https://en.wikipedia.org/wiki/Write-ahead_logging). This stream of data can be “Replayed” or read from any point in time.

# **Is Kafka a message queue?**

It certainly can act as a message queue, but it’s not limited to that. It can act as a FIFO queue, as a Pub/ Sub messaging system, a real-time streaming platform. And because of the durable storage capability of Kafka, it can even be used as a Database ([read about it here](https://www.confluent.io/blog/okay-store-data-apache-kafka/)).

