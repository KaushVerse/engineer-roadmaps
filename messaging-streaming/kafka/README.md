# 🐘 Apache Kafka Roadmap
**From Distributed Logs to Enterprise-Scale Event Streaming**

Apache Kafka is a **high-throughput, distributed event streaming platform**
used for **real-time data pipelines, microservices communication, analytics,
stream processing, and event-driven architectures**.

This roadmap takes you from **Kafka basics → production clusters → enterprise streaming systems**.

---

## 🧠 What You’ll Learn
- 📡 Event streaming fundamentals
- 🧱 Kafka internals (brokers, partitions, replication)
- ⚙️ Producers, consumers & consumer groups
- 🔄 Exactly-once & fault-tolerant systems
- ☁️ Kafka at scale (cloud + Kubernetes)

---

## 🟢 Beginner Level

### 🔹 Basics
- 🐘 What is Apache Kafka?
- 🧾 Messaging vs Event Streaming
- 📦 Kafka Use Cases (Logs, Metrics, Events)
- ⚖️ Kafka vs RabbitMQ (high-level)

### 🔹 Core Architecture
- 🧱 Broker
- 📂 Topic
- 🧩 Partition
- 🔁 Replication
- 🗳️ Leader & Followers
- 🧠 ZooKeeper vs KRaft (Kafka without ZooKeeper)

### 🔹 Message Model
- 📨 Event / Record
- 🔑 Key, Value, Headers
- 🕒 Offset
- 📜 Log-based storage (append-only)

---

## 🟡 Intermediate Level

### 🔹 Producers
- 🚀 Kafka Producer API
- 🔁 Message Ordering
- 🧮 Partitioning Strategy
- 🧱 Key-based routing
- ⚙️ acks, retries, batching

### 🔹 Consumers
- 👥 Consumer Groups
- 📊 Offset Management
- 🔄 Auto vs Manual Commit
- 🧠 Rebalancing
- ⚖️ At-least-once vs At-most-once

### 🔹 Topics & Partitions
- 📦 Topic design
- 🧩 Partition count strategy
- 🔁 Replication factor
- 📈 Throughput vs ordering tradeoffs

---

## 🔴 Advanced Level

### 🔹 Reliability & Guarantees
- ✅ At-least-once delivery
- 🎯 Exactly-once semantics (EOS)
- 🔐 Idempotent Producers
- 🧾 Transactions in Kafka

### 🔹 Kafka Storage Internals
- 📂 Log segments
- 🧹 Log retention (time / size)
- 🗜️ Compaction vs Retention
- 📦 Tombstone messages

### 🔹 Scaling Kafka
- 📡 Broker scaling
- 🔁 Partition rebalancing
- 🧩 ISR (In-Sync Replicas)
- 🚦 Leader election

---

## 🔵 Expert Level

### 🔹 Kafka Streams
- 🌊 Stream Processing Basics
- 🧠 Stateless vs Stateful processing
- 🪟 Windowing
- 🔄 Joins & Aggregations
- 🧾 Exactly-once processing

### 🔹 Kafka Connect
- 🔌 Source Connectors
- 📤 Sink Connectors
- 🧩 JDBC, S3, Elasticsearch connectors
- ⚙️ Distributed Connect Mode

### 🔹 Schema Management
- 📜 Schema Registry
- 🧩 Avro / Protobuf / JSON Schema
- 🔁 Schema evolution & compatibility

---

## 🟣 Enterprise Level

### 🔹 Security
- 🔐 TLS Encryption
- 🧑‍💻 SASL (PLAIN, SCRAM, OAuth)
- 🛡️ ACLs (Authorization)
- 🧱 Multi-tenant Kafka

### 🔹 Monitoring & Observability
- 📊 JMX Metrics
- 📈 Prometheus + Grafana
- 🧠 Consumer Lag Monitoring
- 🧾 Broker Health & Alerts

### 🔹 Kafka in Production
- ☁️ Kafka on AWS / GCP / Azure
- ☸️ Kafka on Kubernetes (Strimzi)
- 🧱 Capacity planning
- 🔄 Disaster Recovery & MirrorMaker 2

---

## 🧩 Ecosystem & Tools
- 🧪 kcat (kafkacat)
- 🧰 Kafka CLI tools
- 🔁 MirrorMaker
- 🧠 Burrow (lag monitoring)
- 🧩 Confluent Platform

---

## ⚖️ Kafka vs RabbitMQ
| Feature | Kafka | RabbitMQ |
|------|------|---------|
| Model | Event streaming | Message queue |
| Throughput | Very high | Medium |
| Retention | Yes | No |
| Replay | Yes | No |
| Ordering | Per partition | Per queue |
| Use case | Analytics, streams | Task queues |

---

## 🎯 When to Use Kafka
✅ Event-driven architecture  
✅ High-throughput pipelines  
✅ Real-time analytics  
✅ Data streaming & ETL  
❌ Simple background jobs (RabbitMQ better)

---

## 🧠 Architecture Patterns
- 📡 Event Sourcing
- 🔄 CQRS
- 📦 Log aggregation
- 🧠 Stream processing
- 🔁 CDC (Change Data Capture)

---

## ⭐ Final Note
> Kafka is not just a queue —  
> it’s a **distributed commit log** that powers **real-time systems at scale**.

If you master Kafka, you master **modern distributed systems** 🐘🔥
