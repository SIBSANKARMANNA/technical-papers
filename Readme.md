# Apache Kafka

## What is Apache Kafka?

Apache Kafka is a distributed event streaming platform used to publish, store, process, and consume real-time streams of events.

---

## Why Kafka?

Suppose an e-commerce website receives:

- 1 million users
- Thousands of payments
- Thousands of orders
- Notifications
- Inventory updates

If every service communicates directly with every other service, the system becomes difficult to maintain and scale. Kafka acts as a central platform for exchanging data between services.

---

## What is Event Streaming?

An **event** means **something happened**.

Examples:

- Customer Registered
- Order Created
- Payment Completed
- Temperature = 32°C
- Car Location Updated
- Product Added

**Streaming** means events arrive continuously in real time. Kafka processes these continuous streams of events.

---

## Kafka Architecture

```text
Producer
    │
    ▼
  Topic
    ▲
    │
Consumer
```

---

## Important Components

### Producer

- Writes data into Kafka.
- Example:

```text
Order Service
      │
      ▼
    Kafka
```

### Consumer

- Reads data from Kafka.
- Example:

```text
Kafka
  │
  ▼
Email Service
```

### Topic

A **Topic** is like a folder where messages are stored.

Examples:

- Orders
- Payments
- Users
- Notifications

- Producers write data to a Topic.
- Consumers read data from a Topic.

### Message (Event)

A message is the actual data sent by a producer.

Example:

```text
Order ID : 102
Customer : John
Price : $100
```

The entire data above represents one message (event).

### Broker

A Broker is a Kafka server.

A Kafka cluster usually contains multiple brokers.

Example:

- Broker 1
- Broker 2
- Broker 3

If Broker 2 crashes, Broker 1 and Broker 3 continue serving requests.

---

## How Kafka Works

1. Producer sends an event (Order Created).
2. Kafka stores the event in a Topic.
3. Consumer reads the event.
4. Notification Service sends an email.

Flow:

```text
Producer
    │
    ▼
Kafka Topic
    │
    ▼
Consumer
    │
    ▼
Notification Service
```

---

## Applications of Kafka

- Banking
- Stock Market
- E-commerce
- Uber
- Netflix
- Food Delivery
- Internet of Things (IoT)
- Smart Cities
- Social Media
- Log Collection
- Fraud Detection
- Recommendation Systems

---

## Advantages of Kafka

| Advantage | Description |
|-----------|-------------|
| High Throughput | Can process millions of events per second. |
| Scalable | Add more brokers as traffic grows. |
| Fault Tolerant | Data is replicated across brokers. |
| Durable | Events remain stored according to the retention policy. |
| Real-Time Processing | Handles streaming data with low latency. |
| Loose Coupling | Producers and consumers work independently. |
| Distributed | Runs across multiple machines. |
| Open Source | Free under the Apache Software Foundation. |

---

## Disadvantages of Kafka

| Disadvantage | Description |
|--------------|-------------|
| Learning Curve | Concepts like partitions, offsets, and consumer groups require time to learn. |
| Cluster Management | Managing production clusters requires experience. |
| Ordering Limitations | Message ordering is guaranteed only within a partition. |
| Infrastructure Cost | Large deployments require multiple servers and monitoring. |
| Debugging | Distributed systems are harder to troubleshoot. |

---

## How to Implement Kafka

### Step 1

- Install Java or another supported language.

### Step 2

- Download Apache Kafka.

### Step 3

- Start the Kafka server.

### Step 4

- Create a Topic.

Example:

```text
orders
```

### Step 5

- Create a Producer.

### Step 6

- Create a Consumer.

### Step 7

- Producer sends messages to the Topic.

### Step 8

- Consumer receives messages from the Topic.

Kafka supports Java, Python, Go, C/C++, Scala, and many other languages through official and community clients.

---

## When Should We Use Kafka?

### Use Kafka When

- You need real-time data processing.
- Multiple services need the same data.
- Your system must handle very high traffic.
- You are building an event-driven or microservices architecture.
- You need reliable and scalable message delivery.

### Avoid Kafka When

- The application is small.
- Only two services communicate occasionally.
- A simple REST API or lightweight message queue is sufficient.

---

## References

- Apache Kafka Documentation  
  https://kafka.apache.org/documentation/

- Apache Kafka Getting Started  
  https://kafka.apache.org/getting-started