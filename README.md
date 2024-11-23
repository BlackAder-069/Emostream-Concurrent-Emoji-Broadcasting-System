# Emostream - Concurrent Emoji Broadcasting System

A distributed real-time emoji broadcasting system built using event-driven architecture with Kafka, Flask, and Apache Spark.

## Overview

Emostream is a scalable system that enables real-time emoji broadcasting across multiple clients through a distributed architecture. The system handles concurrent emoji streams, aggregates them, and broadcasts them to subscribers efficiently.

## System Architecture

1. Client Layer
   - Multiple clients can send and receive emojis concurrently
   - Clients register with a load balancer for automatic server assignment
   - Supports Server-Sent Events (SSE) for real-time updates

2. Server Layer
   - Flask servers handling client registration and emoji submissions
   - Load balancing across multiple subscriber servers
   - Event streaming using Kafka for message distribution

3. Processing Layer
   - Apache Spark for real-time stream processing
   - Emoji aggregation with time-windowed operations
   - Configurable emission rates and batching

4. Distribution Layer
   - Clustered architecture for scalable message broadcasting
   - Multiple Kafka topics for different stages of processing
   - Subscriber pattern for efficient message delivery

## Components

- Main Server: Handles client registration and initial emoji submissions
- Spark Streaming: Processes and aggregates emoji data in real-time
- Main Publisher: Distributes processed data to clusters
- Cluster Publishers: Handle final distribution to subscribers
- Subscriber Servers: Manage client connections and emoji delivery
- Client Consumers: Send and receive emojis in real-time

## Setup Requirements

- Python 3.x
- Apache Kafka
- Apache Spark
- Flask
- Required Python packages: `kafka-python`, `flask`, `sseclient`, `requests`

## How to Run

1. Start Kafka server
2. Create required Kafka topics:

bash
/usr/local/kafka/bin/kafka-topics.sh --create --topic emoji-topic --bootstrap-server localhost:9092
/usr/local/kafka/bin/kafka-topics.sh --create --topic emoji-aggregated --bootstrap-server localhost:9092

3. Start components in order:
   - Main server (main4.py)
   - Spark streaming (spark_stream.py)
   - Main publisher (main_publisher.py)
   - Cluster publishers (cluster_1.py, cluster_2.py)
   - Subscriber servers (subscriber2.py, subscriber4.py)

4. Run clients (client_consumer1.py, client_consumer2.py, client_consumer3.py)

- Real-time emoji broadcasting
- Load balancing across multiple servers
- Automatic client registration and server assignment
- Time-windowed emoji aggregation
- Scalable cluster-based distribution
- Fault tolerance and error handling
- Support for concurrent users

## System Flow

1. Clients register with the main server
2. Server assigns clients to least loaded subscriber
3. Clients send emojis through REST API
4. Spark processes and aggregates emoji streams
5. Main publisher distributes to clusters
6. Clusters broadcast to assigned subscribers
7. Clients receive real-time emoji updates through SSE

## Configuration

- Server ports: 5000-5006
- Kafka broker: localhost:9092
- Spark configuration: 4 partitions
- Processing window: 2 seconds
- Aggregation rules: Custom scaling for high-volume emojis

## Error Handling

- Automatic reconnection for dropped connections
- Graceful client disconnection handling
- Invalid emoji filtering
- Server overload protection

## Monitor and Debug

- Built-in logging for all components
- Real-time client count tracking
- Message flow verification through demo_consumer.py
- Timestamp tracking for performance analysis

## Future Improvements

- Add authentication and security
- Implement message persistence
- Add more advanced load balancing strategies
- Enhance monitoring and analytics
- Scale to multiple Kafka brokers
