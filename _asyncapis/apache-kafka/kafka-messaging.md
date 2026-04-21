---
channels:
- description: A Kafka topic is a category or feed name to which records are published. Topics are partitioned, and each partition is an ordered, immutable sequence of records that is continually appended to.
  name: '{topic}'
  operation: publish
  operation_id: produceRecord
  summary: Produce a record to a Kafka topic
description: Apache Kafka is a distributed event streaming platform capable of handling trillions of events a day. This spec describes the core messaging protocol for producing and consuming records to/from Kafka topics.
layout: asyncapi
messages:
- description: ''
  name: KafkaRecord
  summary: A record (message) in a Kafka topic
  title: Kafka Record
name: Apache Kafka Messaging API
provider_name: Apache Kafka
provider_slug: apache-kafka
servers:
- description: Default Kafka bootstrap server
  name: default
  protocol: kafka
  url: localhost:9092
slug: kafka-messaging
spec_file: asyncapi/kafka-messaging.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/apache-kafka/refs/heads/main/asyncapi/kafka-messaging.yml
tags:
- Distributed Systems
- Event Streaming
- Messaging
- Open Source
- Pub-Sub
- AsyncAPI
- Webhooks
- Events
version: 3.7.0
---
