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
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Apache Pulsar Messaging API\n  version: 3.3.0\n  description: >-\n    Apache Pulsar is a cloud-native, multi-tenant, high-performance messaging\n    and streaming platform. This spec describes the messaging patterns for\n    producing and consuming messages on Pulsar topics with support for\n    multiple subscription types and schema enforcement.\n  contact:\n    name: Apache Pulsar\n    url: https://pulsar.apache.org/\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\nservers:\n  default:\n    url: pulsar://localhost:6650\n    protocol: pulsar\n    description: Default Pulsar binary protocol endpoint\n  websocket:\n    url: ws://localhost:8080/ws/v2\n    protocol: ws\n    description: Pulsar WebSocket API endpoint\ndefaultContentType: application/json\nchannels:\n  'persistent/{tenant}/{namespace}/{topic}':\n    description: >-\n      A persistent Pulsar topic. Messages are durably stored in Apache BookKeeper\n\
  \      and available for replay. Supports partitioned and non-partitioned topics.\n    parameters:\n      tenant:\n        description: The tenant name\n        schema:\n          type: string\n      namespace:\n        description: The namespace within the tenant\n        schema:\n          type: string\n      topic:\n        description: The topic name\n        schema:\n          type: string\n    publish:\n      operationId: produceMessage\n      summary: Produce a message to a Pulsar topic\n      description: >-\n        Producers publish messages to topics. Each message can include a key,\n        properties (headers), event time, and a schema-validated payload.\n      message:\n        $ref: '#/components/messages/PulsarMessage'\n    subscribe:\n      operationId: consumeMessage\n      summary: Consume messages from a Pulsar topic\n      description: >-\n        Consumers subscribe to topics using one of four subscription types:\n        Exclusive, Shared, Failover, or Key_Shared.\n\
  \      message:\n        $ref: '#/components/messages/PulsarMessage'\n      bindings:\n        pulsar:\n          subscriptionType:\n            type: string\n            enum: [Exclusive, Shared, Failover, Key_Shared]\n  'non-persistent/{tenant}/{namespace}/{topic}':\n    description: >-\n      A non-persistent Pulsar topic. Messages are not stored to disk and are\n      only delivered to currently connected consumers. Offers lower latency\n      at the cost of durability.\n    parameters:\n      tenant:\n        schema:\n          type: string\n      namespace:\n        schema:\n          type: string\n      topic:\n        schema:\n          type: string\n    publish:\n      operationId: produceNonPersistentMessage\n      summary: Produce a message to a non-persistent topic\n      message:\n        $ref: '#/components/messages/PulsarMessage'\n    subscribe:\n      operationId: consumeNonPersistentMessage\n      summary: Consume from a non-persistent topic\n      message:\n        $ref:\
  \ '#/components/messages/PulsarMessage'\ncomponents:\n  messages:\n    PulsarMessage:\n      name: PulsarMessage\n      title: Pulsar Message\n      summary: A message in Apache Pulsar\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Pulsar-Message-Id:\n            type: string\n            description: Unique message ID (ledgerId:entryId:partitionIndex)\n          X-Pulsar-Publish-Time:\n            type: string\n            format: date-time\n          X-Pulsar-Event-Time:\n            type: string\n            format: date-time\n          X-Pulsar-Sequence-Id:\n            type: integer\n          X-Pulsar-Producer-Name:\n            type: string\n          X-Pulsar-Partition-Key:\n            type: string\n          X-Pulsar-Ordering-Key:\n            type: string\n        additionalProperties:\n          type: string\n          description: User-defined message properties\n      payload:\n        type: object\n        description:\
  \ The message payload (schema-enforced if a schema is registered)\n  schemas:\n    MessageId:\n      type: object\n      properties:\n        ledgerId:\n          type: integer\n        entryId:\n          type: integer\n        partitionIndex:\n          type: integer\n    SubscriptionConfig:\n      type: object\n      properties:\n        subscriptionName:\n          type: string\n        subscriptionType:\n          type: string\n          enum: [Exclusive, Shared, Failover, Key_Shared]\n        receiverQueueSize:\n          type: integer\n        ackTimeoutMillis:\n          type: integer\n        negativeAckRedeliveryDelayMillis:\n          type: integer\n        deadLetterPolicy:\n          type: object\n          properties:\n            maxRedeliverCount:\n              type: integer\n            deadLetterTopic:\n              type: string\n            initialSubscriptionName:\n              type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/apache-pulsar/refs/heads/main/asyncapi/pulsar-messaging.yml
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
