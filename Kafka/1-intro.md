## What Is Apache Kafka?

- Apache Kafka is an event streaming platform used to collect, process, store, and integrate data at scale. It has numerous use cases including distributed streaming, stream processing, data integration, and pub/sub messaging.

<br />

## Why Kafka?

- Kafka is a distributed streaming platform
- It is horizontally scalable
- It is fault tolerant
- It is fast
- It is used by many companies including Uber, Netflix, LinkedIn, and many more

<br />
  
## Kafka Terms and Definitions

- **Producer** - A producer is a client that sends messages to a topic on the Kafka cluster

- **Consume**r - A consumer is a client that reads messages from a topic on the Kafka cluster

- **Topic** - A topic is a category or feed name to which records are published. Topics in Kafka are always multi-subscriber

- **Broker** - A broker is a server that hosts a topic. Each broker is identified by a unique id

- **Partition** - A partition is an ordered, immutable sequence of records that is continually appended to a file. The records in the partitions are each assigned a sequential id number called the offset that uniquely identifies each record within the partition.

- **Replication** - Replication is the process of duplicating data across multiple brokers. Replication provides fault tolerance and high availability. A topic can have multiple partitions, and each partition can have multiple replicas.

- **Consumer Group** - A consumer group is a group of consumers that cooperate to consume messages from a set of topics. Each consumer in a group can process the messages in parallel. The Kafka cluster ensures that each message is delivered to one consumer in each subscribing consumer group.

- **Offset** - The offset is a unique identifier for a message within a partition. The offset is assigned when a producer publishes a message to a partition. The offset is used by the consumer to determine the message to process next.

- **Leader** - The leader is the server that is currently the active controller for a partition. The leader handles all read and write requests for the partition. Only the leader can become a follower. - Follower - The follower is a passive server that replicates the log of the leader. The follower can become the leader if the current leader fails.

> Apache Kafka uses topics and partitions for efficient data processing. Topics are data categories to which records are published; consumers subscribe to these topics. For scalability and performance, topics are divided into partitions, allowing parallel data processing and fault tolerance. Partitions enable multiple consumers to read concurrently and are replicated across nodes for resilience against failures. Let's dive into these further.

<br />

### Why partition your data in Kafka?

- If you have so much load that you need more than a single instance of your application, you need to partition your data. How you partition serves as your load balancing for the downstream application. The producer clients decide which topic partition that the data ends up in, but it’s what the consumer applications do with that data that drives the decision logic.

<br />

## Kafka topic partitioning: Strategies and best practices

https://newrelic.com/blog/best-practices/effective-strategies-kafka-topic-partitioning

<br />

### Auto Create Topic

The kafka broker has a property: auto.create.topics.enable

If you set that to true if the producer publishes a message to the topic with the new topic name it will automatically create a topic for you.

The Confluent Team recommends not doing this because the explosion of topics, depending on your environment can become unwieldy, and the topic creation will always have the same defaults when created. It's important to have a replication-factor of at least 3 to ensure durability of your topics in the event of disk failure.
