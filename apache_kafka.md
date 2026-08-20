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

An event means something happened.

Examples:

- Customer Registered
- Order Created
- Payment Completed
- Temperature = 32°C
- Car Location Updated
- Product Added

Streaming means events arrive continuously in real time. Kafka processes these continuous streams of events.

---


### Topic

A Topic is like a folder where messages are stored.

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

---

## Applications of Kafka

- Banking
- Stock Market
- E-commerce
- Uber
- Netflix
- Food Delivery
- Internet of Things (IoT)
- Recommendation Systems

---


## References


- Apache Kafka Introduction
  https://kafka.apache.org/43/getting-started/introduction/

- Uses of Apache Kafka
  https://kafka.apache.org/uses/
