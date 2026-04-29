---
api_specs:
- filename: kafka-rest-proxy.yml
  format: yaml
  label: Kafka REST Proxy API
  slug: kafka-rest-proxy-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/apache-kafka/refs/heads/main/openapi/kafka-rest-proxy.yml
- filename: kafka-connect.yml
  format: yaml
  label: Kafka Connect REST API
  slug: kafka-connect-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/apache-kafka/refs/heads/main/openapi/kafka-connect.yml
- filename: kafka-messaging.yml
  format: yaml
  label: Apache Kafka Messaging API
  slug: kafka-messaging-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/apache-kafka/refs/heads/main/asyncapi/kafka-messaging.yml
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
source_filename: kafka-messaging.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Apache Kafka Messaging API\n  version: 3.7.0\n  description: >-\n    Apache Kafka is a distributed event streaming platform capable of handling\n    trillions of events a day. This spec describes the core messaging protocol\n    for producing and consuming records to/from Kafka topics.\n  contact:\n    name: Apache Kafka\n    url: https://kafka.apache.org/\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\nservers:\n  default:\n    url: localhost:9092\n    protocol: kafka\n    description: Default Kafka bootstrap server\n    protocolVersion: '3.7'\ndefaultContentType: application/json\nchannels:\n  '{topic}':\n    description: >-\n      A Kafka topic is a category or feed name to which records are published.\n      Topics are partitioned, and each partition is an ordered, immutable\n      sequence of records that is continually appended to.\n    parameters:\n      topic:\n        description: The topic name\n\
  \        schema:\n          type: string\n    publish:\n      operationId: produceRecord\n      summary: Produce a record to a Kafka topic\n      description: >-\n        Producers publish records to topics. Each record consists of a key,\n        a value, a timestamp, and optional headers. Records are appended\n        to the partition determined by the partitioner.\n      message:\n        $ref: '#/components/messages/KafkaRecord'\n      bindings:\n        kafka:\n          groupId:\n            type: string\n          clientId:\n            type: string\n    subscribe:\n      operationId: consumeRecord\n      summary: Consume records from a Kafka topic\n      description: >-\n        Consumers read records from topics by subscribing to one or more topics\n        and processing the stream of records produced to them. Consumers belong\n        to consumer groups for parallel processing.\n      message:\n        $ref: '#/components/messages/KafkaRecord'\n      bindings:\n        kafka:\n\
  \          groupId:\n            type: string\n          clientId:\n            type: string\ncomponents:\n  messages:\n    KafkaRecord:\n      name: KafkaRecord\n      title: Kafka Record\n      summary: A record (message) in a Kafka topic\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          kafka_offset:\n            type: integer\n            description: The offset of the record in the partition\n          kafka_partition:\n            type: integer\n            description: The partition the record belongs to\n          kafka_timestamp:\n            type: integer\n            description: The timestamp of the record (CreateTime or LogAppendTime)\n          kafka_timestampType:\n            type: string\n            enum: [CREATE_TIME, LOG_APPEND_TIME]\n        additionalProperties:\n          type: string\n          description: Custom headers as key-value string pairs\n      payload:\n        type: object\n        properties:\n\
  \          key:\n            description: The record key used for partitioning\n          value:\n            description: The record value (the message payload)\n          timestamp:\n            type: integer\n            description: Unix timestamp in milliseconds\n          headers:\n            type: object\n            additionalProperties:\n              type: string\n      bindings:\n        kafka:\n          key:\n            type: string\n            description: Record key for partitioning\n  schemas:\n    KafkaRecordKey:\n      type: object\n      description: A generic Kafka record key\n    KafkaRecordValue:\n      type: object\n      description: A generic Kafka record value\n    ConsumerGroupMetadata:\n      type: object\n      properties:\n        groupId:\n          type: string\n        generationId:\n          type: integer\n        memberId:\n          type: string\n        groupInstanceId:\n          type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/apache-kafka/refs/heads/main/asyncapi/kafka-messaging.yml
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
