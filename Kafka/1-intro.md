# What Is Apache Kafka?

- Apache Kafka is an event streaming platform used to collect, process, store, and integrate data at scale. It has numerous use cases including distributed streaming, stream processing, data integration, and pub/sub messaging.

<br />

### What are Kafka topics and partitions?

- Apache Kafka uses topics and partitions for efficient data processing. Topics are data categories to which records are published; consumers subscribe to these topics. For scalability and performance, topics are divided into partitions, allowing parallel data processing and fault tolerance. Partitions enable multiple consumers to read concurrently and are replicated across nodes for resilience against failures. Let's dive into these further.

### Why partition your data in Kafka?

- If you have so much load that you need more than a single instance of your application, you need to partition your data. How you partition serves as your load balancing for the downstream application. The producer clients decide which topic partition that the data ends up in, but it’s what the consumer applications do with that data that drives the decision logic.

=======================

https://newrelic.com/blog/best-practices/effective-strategies-kafka-topic-partitioning

=======================

**Auto Create Topic**
The kafka broker has a property: auto.create.topics.enable

If you set that to true if the producer publishes a message to the topic with the new topic name it will automatically create a topic for you.

The Confluent Team recommends not doing this because the explosion of topics, depending on your environment can become unwieldy, and the topic creation will always have the same defaults when created. It's important to have a replication-factor of at least 3 to ensure durability of your topics in the event of disk failure.
