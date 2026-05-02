---
api_specs:
- filename: nats-monitoring-api-openapi.yml
  format: yaml
  label: NATS Monitoring API
  slug: nats-monitoring-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/nats/refs/heads/main/properties/nats-monitoring-api-openapi.yml
- filename: nats-messaging-asyncapi.yml
  format: yaml
  label: NATS Messaging API
  slug: nats-messaging-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/nats/refs/heads/main/properties/nats-messaging-asyncapi.yml
- filename: nats-jetstream-api-asyncapi.yml
  format: yaml
  label: NATS JetStream Management API
  slug: nats-jetstream-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/nats/refs/heads/main/properties/nats-jetstream-api-asyncapi.yml
channels:
- description: NATS core pub-sub channel. Messages published to a subject are delivered to all subscribers matching that subject. Supports wildcards (* for single token, > for multiple tokens).
  name: '{subject}'
  operation: publish
  operation_id: publish
  summary: Publish a message to a NATS subject
- description: NATS request-reply pattern. A requestor publishes a message with a unique reply subject and waits for a response.
  name: '{subject}.request'
  operation: publish
  operation_id: request
  summary: Send a request and await reply
- description: Create a JetStream stream
  name: $JS.API.STREAM.CREATE.{stream}
  operation: publish
  operation_id: createStream
  summary: Create a new JetStream stream
- description: Get JetStream stream info
  name: $JS.API.STREAM.INFO.{stream}
  operation: publish
  operation_id: getStreamInfo
  summary: Get stream information
- description: Delete a JetStream stream
  name: $JS.API.STREAM.DELETE.{stream}
  operation: publish
  operation_id: deleteStream
  summary: Delete a stream
- description: Create a JetStream consumer
  name: $JS.API.CONSUMER.CREATE.{stream}.{consumer}
  operation: publish
  operation_id: createConsumer
  summary: Create a new JetStream consumer
- description: List JetStream stream names
  name: $JS.API.STREAM.NAMES
  operation: publish
  operation_id: listStreamNames
  summary: Request list of stream names
description: NATS provides cloud-native messaging with core pub-sub, request-reply, and queue group patterns, plus JetStream for persistent streaming with streams, consumers, key-value stores, and object stores.
layout: asyncapi
messages:
- description: ''
  name: NATSMessage
  summary: A message in the NATS messaging system
  title: NATS Message
- description: ''
  name: StreamConfig
  summary: ''
  title: JetStream Stream Configuration
- description: ''
  name: StreamInfo
  summary: ''
  title: JetStream Stream Info
- description: ''
  name: ConsumerConfig
  summary: ''
  title: JetStream Consumer Configuration
name: NATS Core and JetStream Messaging API
provider_name: NATS
provider_slug: nats
servers:
- description: Default NATS server
  name: default
  protocol: nats
  url: localhost:4222
slug: nats-messaging
source_filename: nats-messaging.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: NATS Core and JetStream Messaging API\n  version: 2.10.0\n  description: >-\n    NATS provides cloud-native messaging with core pub-sub, request-reply, and\n    queue group patterns, plus JetStream for persistent streaming with streams,\n    consumers, key-value stores, and object stores.\n  contact:\n    name: NATS.io\n    url: https://nats.io/\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\nservers:\n  default:\n    url: localhost:4222\n    protocol: nats\n    description: Default NATS server\ndefaultContentType: application/json\nchannels:\n  '{subject}':\n    description: >-\n      NATS core pub-sub channel. Messages published to a subject are delivered\n      to all subscribers matching that subject. Supports wildcards (* for single\n      token, > for multiple tokens).\n    parameters:\n      subject:\n        description: >-\n          NATS subject, a dot-separated string. Supports wildcards:\n\
  \          * matches a single token, > matches one or more tokens.\n        schema:\n          type: string\n    publish:\n      operationId: publish\n      summary: Publish a message to a NATS subject\n      message:\n        $ref: '#/components/messages/NATSMessage'\n    subscribe:\n      operationId: subscribe\n      summary: Subscribe to a NATS subject\n      message:\n        $ref: '#/components/messages/NATSMessage'\n  '{subject}.request':\n    description: >-\n      NATS request-reply pattern. A requestor publishes a message with a\n      unique reply subject and waits for a response.\n    parameters:\n      subject:\n        schema:\n          type: string\n    publish:\n      operationId: request\n      summary: Send a request and await reply\n      message:\n        $ref: '#/components/messages/NATSMessage'\n    subscribe:\n      operationId: reply\n      summary: Receive request and send reply\n      message:\n        $ref: '#/components/messages/NATSMessage'\n  '$JS.API.STREAM.CREATE.{stream}':\n\
  \    description: Create a JetStream stream\n    parameters:\n      stream:\n        schema:\n          type: string\n    publish:\n      operationId: createStream\n      summary: Create a new JetStream stream\n      message:\n        $ref: '#/components/messages/StreamConfig'\n  '$JS.API.STREAM.INFO.{stream}':\n    description: Get JetStream stream info\n    parameters:\n      stream:\n        schema:\n          type: string\n    publish:\n      operationId: getStreamInfo\n      summary: Get stream information\n      message:\n        name: Empty\n        payload:\n          type: object\n    subscribe:\n      operationId: streamInfoResponse\n      summary: Stream info response\n      message:\n        $ref: '#/components/messages/StreamInfo'\n  '$JS.API.STREAM.DELETE.{stream}':\n    description: Delete a JetStream stream\n    parameters:\n      stream:\n        schema:\n          type: string\n    publish:\n      operationId: deleteStream\n      summary: Delete a stream\n      message:\n\
  \        name: Empty\n        payload:\n          type: object\n  '$JS.API.CONSUMER.CREATE.{stream}.{consumer}':\n    description: Create a JetStream consumer\n    parameters:\n      stream:\n        schema:\n          type: string\n      consumer:\n        schema:\n          type: string\n    publish:\n      operationId: createConsumer\n      summary: Create a new JetStream consumer\n      message:\n        $ref: '#/components/messages/ConsumerConfig'\n  '$JS.API.STREAM.NAMES':\n    description: List JetStream stream names\n    publish:\n      operationId: listStreamNames\n      summary: Request list of stream names\n      message:\n        name: ListRequest\n        payload:\n          type: object\n          properties:\n            offset:\n              type: integer\n            subject:\n              type: string\ncomponents:\n  messages:\n    NATSMessage:\n      name: NATSMessage\n      title: NATS Message\n      summary: A message in the NATS messaging system\n      contentType:\
  \ application/json\n      headers:\n        type: object\n        properties:\n          Nats-Msg-Id:\n            type: string\n            description: Unique message ID for deduplication\n          Nats-Expected-Stream:\n            type: string\n            description: Expected stream for publish\n          Nats-Expected-Last-Msg-Id:\n            type: string\n            description: Expected last message ID for optimistic concurrency\n          Nats-Expected-Last-Sequence:\n            type: string\n            description: Expected last sequence for optimistic concurrency\n      payload:\n        type: object\n        description: The message payload\n    StreamConfig:\n      name: StreamConfig\n      title: JetStream Stream Configuration\n      payload:\n        type: object\n        properties:\n          name:\n            type: string\n          subjects:\n            type: array\n            items:\n              type: string\n          retention:\n            type: string\n\
  \            enum: [limits, interest, workqueue]\n          max_consumers:\n            type: integer\n          max_msgs:\n            type: integer\n          max_bytes:\n            type: integer\n          max_age:\n            type: integer\n            description: Maximum age in nanoseconds\n          max_msg_size:\n            type: integer\n          storage:\n            type: string\n            enum: [file, memory]\n          num_replicas:\n            type: integer\n          discard:\n            type: string\n            enum: [old, new]\n          duplicate_window:\n            type: integer\n          allow_rollup_hdrs:\n            type: boolean\n          deny_delete:\n            type: boolean\n          deny_purge:\n            type: boolean\n    StreamInfo:\n      name: StreamInfo\n      title: JetStream Stream Info\n      payload:\n        type: object\n        properties:\n          config:\n            type: object\n          state:\n            type: object\n\
  \            properties:\n              messages:\n                type: integer\n              bytes:\n                type: integer\n              first_seq:\n                type: integer\n              last_seq:\n                type: integer\n              consumer_count:\n                type: integer\n          created:\n            type: string\n            format: date-time\n          cluster:\n            type: object\n    ConsumerConfig:\n      name: ConsumerConfig\n      title: JetStream Consumer Configuration\n      payload:\n        type: object\n        properties:\n          stream_name:\n            type: string\n          config:\n            type: object\n            properties:\n              durable_name:\n                type: string\n              deliver_subject:\n                type: string\n              deliver_group:\n                type: string\n              ack_policy:\n                type: string\n                enum: [none, all, explicit]\n        \
  \      ack_wait:\n                type: integer\n              max_deliver:\n                type: integer\n              filter_subject:\n                type: string\n              replay_policy:\n                type: string\n                enum: [instant, original]\n              max_ack_pending:\n                type: integer\n              deliver_policy:\n                type: string\n                enum: [all, last, new, by_start_sequence, by_start_time, last_per_subject]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/nats/refs/heads/main/asyncapi/nats-messaging.yml
spec_file: asyncapi/nats-messaging.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/nats/refs/heads/main/asyncapi/nats-messaging.yml
tags:
- Cloud Native
- IoT
- Message Broker
- Microservices
- Pub Sub
- AsyncAPI
- Webhooks
- Events
version: 2.10.0
---
