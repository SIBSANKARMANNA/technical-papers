### Apache Kafka

## What is this?
Apache Kafka is a distributed event streaming platform used to publish, store, process, and consume real-time streams of events.


## Why it is?
Suppose an e-commerce website receives
    -1 million users
    -thousands of payments
    -thousands of orders
    -notifications
    -inventory updates
If every service communicates directly,This becomes difficult to maintain.

## What is Event Streaming?
An event means Something happened.
    -Customer Registered
    -Order Created
    -Payment Completed
    -Temperature = 32°C
    -Car Location Updated
    -Product Added

Streaming means
    -Events arrive continuously.
    -Kafka processes these continuous streams.


## Kafka Architecture
Producer ->Topic <- Consumer

## Important Component
Producer
    -Writes data into Kafka.
    -Example: Order Service -> Kafka
Consumer
    -Reads data.
    -Example: Kafka -> Email Service
Topic
    -Topic like a folder
    -Orders
    -Payments
    -Users
    -Notifications

Producer write to Topic and Consumer read from Topic.

Message(Event):
    -Order ID : 102
    -Customer : John
    -Price : $100
This entire data is one message.

Broker:
    -A Kafka cluster usually has multiple Brokers.
    -Example:
    -Broker 1
    -Broker 2
    -Broker 3

If Broker 2 crashes,
Broker 1 and Broker 3 continue working.

## How Kafka works?
Step 1: Producer sends event(order created)
Step 2: Kafka stores it.
Step 3: Consumer reads it.
Step 4: Notification Service sends email.


## Application of Kafka
Banking
Stock Market
Amazon-like e-commerce
Uber
Netflix
Food Delivery
IoT
Smart Cities
Social Media
Log Collection
Fraud Detection
Recommendation Systems


## Advantages of Kafka
High Throughput	
    -Can process millions of events per second.
Scalable	
    -Add more brokers as traffic grows.
Fault Tolerant	
    -Data is replicated across brokers.
Durable	
    -Events remain stored based on the retention policy.
Real-Time Processing	
    -Handles streaming data with low latency.
Loose Coupling	
    -Producers and consumers operate independently.
Distributed	
    -Runs across multiple machines.
Open Source	
    -Free under the Apache Software Foundation.


## Disadvantages of Kafka
Learning Curve	
    -Concepts like partitions, offsets, and consumer groups take time to learn.
Cluster Management	
    -Managing production clusters requires experience.
Ordering Limitations	
    -Message order is guaranteed only within a partition.
Infrastructure 
    -Cost	Large deployments need multiple servers and monitoring.
Debugging	
    -Distributed systems are generally harder to troubleshoot.


## How to implement Kafka?
Step 1
    -Install Java or supported Language
Step 2
    -Download Kafka.
Step 3
    -Start the Kafka server.
Step 4
    -Create a Topic.
    -orders
Step 5
    -Create a Producer.
Step 6
    -Create a Consumer.
Step 7
    -Producer sends messages.
Step 8
    -Consumer receives messages.

Kafka supports Java, Python, Go, C/C++, Scala, and many other languages through official and community clients.

## When should we use Kafka?
Use Kafka when:
    -You need real-time data processing.
    -Multiple services need the same data.
    -Your system must handle very high traffic.
    -You are building an event-driven or microservices architecture.
    -You want reliable and scalable message delivery.

Avoid Kafka when:
    -The application is small.
    -Only two services communicate occasionally.
    -A simple REST API or lightweight message queue is sufficient.


## References
Use these official sources as primary references:
    -Apache Kafka Documentation  https://kafka.apache.org/43/getting-started
