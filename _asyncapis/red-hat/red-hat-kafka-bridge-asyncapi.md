---
api_specs:
- filename: red-hat-openshift-cluster-manager-openapi.yml
  format: yaml
  label: Red Hat OpenShift Cluster Manager API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/openapi/red-hat-openshift-cluster-manager-openapi.yml
- filename: red-hat-ansible-automation-platform-openapi.yml
  format: yaml
  label: Red Hat Ansible Automation Platform API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/openapi/red-hat-ansible-automation-platform-openapi.yml
- filename: red-hat-quay-openapi.yml
  format: yaml
  label: Red Hat Quay API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/openapi/red-hat-quay-openapi.yml
- filename: red-hat-insights-openapi.yml
  format: yaml
  label: Red Hat Insights API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/openapi/red-hat-insights-openapi.yml
- filename: red-hat-satellite-openapi.yml
  format: yaml
  label: Red Hat Satellite API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/openapi/red-hat-satellite-openapi.yml
- filename: red-hat-keycloak-admin-openapi.yml
  format: yaml
  label: Red Hat Build of Keycloak Admin REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/openapi/red-hat-keycloak-admin-openapi.yml
- filename: red-hat-kafka-bridge-asyncapi.yml
  format: yaml
  label: Red Hat Streams for Apache Kafka Bridge API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/asyncapi/red-hat-kafka-bridge-asyncapi.yml
- filename: red-hat-notifications-webhooks-asyncapi.yml
  format: yaml
  label: Red Hat Notifications API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/asyncapi/red-hat-notifications-webhooks-asyncapi.yml
channels:
- description: Channel representing messages produced to and consumed from a specific Kafka topic through the HTTP bridge. Producers send messages via HTTP POST and consumers receive messages by polling the bridge endpoint.
  name: topics.{topic}.messages
  operation: publish
  operation_id: produceMessage
  summary: Produce message to topic
- description: Channel representing offset management for a consumer group. Consumers can commit offsets to track their progress and seek to specific offsets for replay or recovery.
  name: consumers.{group_id}.offsets
  operation: publish
  operation_id: commitOffsets
  summary: Commit consumer offsets
description: The Red Hat Streams for Apache Kafka Bridge provides an HTTP-based interface for producing and consuming messages to and from Apache Kafka topics without requiring a native Kafka client. Deployed on OpenShift as part of Red Hat Streams for Apache Kafka, the bridge enables REST clients to participate in event streaming by sending and receiving messages through standard HTTP requests.
layout: asyncapi
messages:
- description: A message record containing the value to produce to a Kafka topic, with optional key, partition, and headers for controlling message routing and metadata.
  name: ProducerRecord
  summary: A single message to be produced to a Kafka topic.
  title: Producer Record
- description: A batch of message records to produce to a Kafka topic in a single HTTP request for improved throughput.
  name: ProducerRecordBatch
  summary: A batch of messages to be produced to a Kafka topic.
  title: Producer Record Batch
- description: A message record received from a Kafka topic through the bridge consumer, including the topic, partition, offset, and the message key and value.
  name: ConsumerRecord
  summary: A message consumed from a Kafka topic.
  title: Consumer Record
- description: A request to commit offsets for specific topic partitions, marking the consumer's progress in processing messages.
  name: OffsetCommit
  summary: Offset commit request for a consumer group.
  title: Offset Commit
name: Red Hat Streams for Apache Kafka Bridge Events
provider_name: Red Hat
provider_slug: red-hat
servers:
- description: The Kafka Bridge HTTP endpoint deployed on OpenShift. The bridge accepts HTTP requests and translates them to Kafka protocol operations for producing and consuming messages.
  name: kafkaBridge
  protocol: https
  url: '{bridge_url}'
slug: red-hat-kafka-bridge-asyncapi
source_filename: red-hat-kafka-bridge-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Red Hat Streams for Apache Kafka Bridge Events\n  description: >-\n    The Red Hat Streams for Apache Kafka Bridge provides an HTTP-based interface\n    for producing and consuming messages to and from Apache Kafka topics without\n    requiring a native Kafka client. Deployed on OpenShift as part of Red Hat\n    Streams for Apache Kafka, the bridge enables REST clients to participate\n    in event streaming by sending and receiving messages through standard\n    HTTP requests.\n  version: '3.1'\n  contact:\n    name: Red Hat Support\n    url: https://access.redhat.com/support\n  license:\n    name: Red Hat Terms of Use\n    url: https://www.redhat.com/en/about/terms-use\nservers:\n  kafkaBridge:\n    url: '{bridge_url}'\n    protocol: https\n    description: >-\n      The Kafka Bridge HTTP endpoint deployed on OpenShift. The bridge accepts\n      HTTP requests and translates them to Kafka protocol operations for\n      producing and consuming\
  \ messages.\n    variables:\n      bridge_url:\n        description: The URL of the deployed Kafka Bridge instance.\n        default: https://kafka-bridge.example.com\n    security:\n      - bearerAuth: []\ndefaultContentType: application/json\nchannels:\n  topics.{topic}.messages:\n    description: >-\n      Channel representing messages produced to and consumed from a specific\n      Kafka topic through the HTTP bridge. Producers send messages via HTTP\n      POST and consumers receive messages by polling the bridge endpoint.\n    parameters:\n      topic:\n        description: The name of the Kafka topic.\n        schema:\n          type: string\n    publish:\n      operationId: produceMessage\n      summary: Produce message to topic\n      description: >-\n        Produces one or more messages to the specified Kafka topic through\n        the HTTP bridge. Messages can include optional keys, partition\n        assignments, and headers.\n      tags:\n        - name: Producing\n     \
  \ message:\n        oneOf:\n          - $ref: '#/components/messages/ProducerRecord'\n          - $ref: '#/components/messages/ProducerRecordBatch'\n    subscribe:\n      operationId: consumeMessage\n      summary: Consume message from topic\n      description: >-\n        Receives messages consumed from the specified Kafka topic through\n        the HTTP bridge consumer. Messages include the topic, partition,\n        offset, and optional key and headers.\n      tags:\n        - name: Consuming\n      message:\n        $ref: '#/components/messages/ConsumerRecord'\n  consumers.{group_id}.offsets:\n    description: >-\n      Channel representing offset management for a consumer group. Consumers\n      can commit offsets to track their progress and seek to specific offsets\n      for replay or recovery.\n    parameters:\n      group_id:\n        description: The consumer group identifier.\n        schema:\n          type: string\n    publish:\n      operationId: commitOffsets\n      summary:\
  \ Commit consumer offsets\n      description: >-\n        Commits the current offsets for the consumer group, marking messages\n        as processed. This enables at-least-once delivery semantics.\n      tags:\n        - name: Consumer Management\n      message:\n        $ref: '#/components/messages/OffsetCommit'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: http\n      scheme: bearer\n      description: >-\n        OAuth 2.0 Bearer token for authenticating with the Kafka Bridge\n        when deployed with authentication enabled.\n  messages:\n    ProducerRecord:\n      name: ProducerRecord\n      title: Producer Record\n      summary: A single message to be produced to a Kafka topic.\n      description: >-\n        A message record containing the value to produce to a Kafka topic,\n        with optional key, partition, and headers for controlling message\n        routing and metadata.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ProducerRecordPayload'\n\
  \      examples:\n        - name: SimpleStringMessage\n          payload:\n            records:\n              - key: order-123\n                value: '{\"orderId\": \"123\", \"status\": \"created\"}'\n                partition: 0\n                headers:\n                  - key: source\n                    value: order-service\n    ProducerRecordBatch:\n      name: ProducerRecordBatch\n      title: Producer Record Batch\n      summary: A batch of messages to be produced to a Kafka topic.\n      description: >-\n        A batch of message records to produce to a Kafka topic in a single\n        HTTP request for improved throughput.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ProducerRecordPayload'\n    ConsumerRecord:\n      name: ConsumerRecord\n      title: Consumer Record\n      summary: A message consumed from a Kafka topic.\n      description: >-\n        A message record received from a Kafka topic through the bridge\n        consumer,\
  \ including the topic, partition, offset, and the message\n        key and value.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ConsumerRecordPayload'\n      examples:\n        - name: ConsumedMessage\n          payload:\n            topic: orders\n            key: order-123\n            value: '{\"orderId\": \"123\", \"status\": \"created\"}'\n            partition: 0\n            offset: 42\n            headers:\n              - key: source\n                value: order-service\n    OffsetCommit:\n      name: OffsetCommit\n      title: Offset Commit\n      summary: Offset commit request for a consumer group.\n      description: >-\n        A request to commit offsets for specific topic partitions, marking\n        the consumer's progress in processing messages.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OffsetCommitPayload'\n  schemas:\n    ProducerRecordPayload:\n      type: object\n      description:\
  \ >-\n        The payload for producing messages to a Kafka topic through the\n        HTTP bridge.\n      required:\n        - records\n      properties:\n        records:\n          type: array\n          description: The list of records to produce.\n          items:\n            type: object\n            required:\n              - value\n            properties:\n              key:\n                description: The message key for partitioning.\n              value:\n                description: The message value payload.\n              partition:\n                type: integer\n                description: The target partition number.\n              headers:\n                type: array\n                description: Optional message headers.\n                items:\n                  type: object\n                  properties:\n                    key:\n                      type: string\n                      description: The header key.\n                    value:\n              \
  \        type: string\n                      description: The header value encoded as a string.\n    ConsumerRecordPayload:\n      type: object\n      description: >-\n        The payload of a message consumed from a Kafka topic through the\n        HTTP bridge.\n      properties:\n        topic:\n          type: string\n          description: The topic the message was consumed from.\n        key:\n          description: The message key.\n        value:\n          description: The message value payload.\n        partition:\n          type: integer\n          description: The partition the message was consumed from.\n        offset:\n          type: integer\n          format: int64\n          description: The offset of the message within the partition.\n        headers:\n          type: array\n          description: Message headers.\n          items:\n            type: object\n            properties:\n              key:\n                type: string\n              value:\n             \
  \   type: string\n    OffsetCommitPayload:\n      type: object\n      description: >-\n        The payload for committing consumer offsets.\n      properties:\n        offsets:\n          type: array\n          description: The list of offsets to commit.\n          items:\n            type: object\n            required:\n              - topic\n              - partition\n              - offset\n            properties:\n              topic:\n                type: string\n                description: The topic name.\n              partition:\n                type: integer\n                description: The partition number.\n              offset:\n                type: integer\n                format: int64\n                description: The offset to commit.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/asyncapi/red-hat-kafka-bridge-asyncapi.yml
spec_file: asyncapi/red-hat-kafka-bridge-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/asyncapi/red-hat-kafka-bridge-asyncapi.yml
tags:
- Cloud
- Containers
- Enterprise
- Hybrid Cloud
- Kubernetes
- Linux
- Open Source
- AsyncAPI
- Webhooks
- Events
version: '3.1'
---
