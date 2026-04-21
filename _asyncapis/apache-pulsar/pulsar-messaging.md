---
channels:
- description: A persistent Pulsar topic. Messages are durably stored in Apache BookKeeper and available for replay. Supports partitioned and non-partitioned topics.
  name: persistent/{tenant}/{namespace}/{topic}
  operation: publish
  operation_id: produceMessage
  summary: Produce a message to a Pulsar topic
- description: A non-persistent Pulsar topic. Messages are not stored to disk and are only delivered to currently connected consumers. Offers lower latency at the cost of durability.
  name: non-persistent/{tenant}/{namespace}/{topic}
  operation: publish
  operation_id: produceNonPersistentMessage
  summary: Produce a message to a non-persistent topic
description: Apache Pulsar is a cloud-native, multi-tenant, high-performance messaging and streaming platform. This spec describes the messaging patterns for producing and consuming messages on Pulsar topics with support for multiple subscription types and schema enforcement.
layout: asyncapi
messages:
- description: ''
  name: PulsarMessage
  summary: A message in Apache Pulsar
  title: Pulsar Message
name: Apache Pulsar Messaging API
provider_name: Apache Pulsar
provider_slug: apache-pulsar
servers:
- description: Default Pulsar binary protocol endpoint
  name: default
  protocol: pulsar
  url: pulsar://localhost:6650
- description: Pulsar WebSocket API endpoint
  name: websocket
  protocol: ws
  url: ws://localhost:8080/ws/v2
slug: pulsar-messaging
spec_file: asyncapi/pulsar-messaging.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/apache-pulsar/refs/heads/main/asyncapi/pulsar-messaging.yml
tags:
- Cloud Native
- Messaging
- Multi-Tenant
- Pub-Sub
- Streaming
- Apache
- Open Source
- AsyncAPI
- Webhooks
- Events
version: 3.3.0
---
