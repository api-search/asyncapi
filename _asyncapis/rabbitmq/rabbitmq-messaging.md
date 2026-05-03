---
api_specs:
- filename: rabbitmq-management.yml
  format: yaml
  label: RabbitMQ Management HTTP API
  slug: rabbitmq-management-http-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rabbitmq/refs/heads/main/openapi/rabbitmq-management.yml
- filename: rabbitmq-messaging.yml
  format: yaml
  label: RabbitMQ AMQP Messaging API
  slug: rabbitmq-amqp-messaging-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/rabbitmq/refs/heads/main/asyncapi/rabbitmq-messaging.yml
channels:
- description: Messages are published to an exchange with a routing key. The exchange routes messages to bound queues based on exchange type and binding rules.
  name: '{exchange}/{routing_key}'
  operation: publish
  operation_id: publishMessage
  summary: Publish a message to an exchange
- description: Consumers subscribe to queues to receive messages. Queues can be durable, exclusive, or auto-delete. Messages are distributed to consumers in round-robin fashion.
  name: '{queue}'
  operation: subscribe
  operation_id: consumeMessage
  summary: Consume messages from a queue
description: RabbitMQ messaging via AMQP 0-9-1 protocol. Producers publish messages to exchanges which route them to queues based on bindings and routing keys. Consumers subscribe to queues to receive messages.
layout: asyncapi
messages:
- description: ''
  name: AMQPMessage
  summary: A message in RabbitMQ following the AMQP 0-9-1 protocol
  title: AMQP Message
name: RabbitMQ AMQP Messaging API
provider_name: RabbitMQ
provider_slug: rabbitmq
servers:
- description: Default RabbitMQ AMQP endpoint
  name: default
  protocol: amqp
  url: localhost:5672
slug: rabbitmq-messaging
source_filename: rabbitmq-messaging.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: RabbitMQ AMQP Messaging API\n  version: 3.13.0\n  description: >-\n    RabbitMQ messaging via AMQP 0-9-1 protocol. Producers publish messages to\n    exchanges which route them to queues based on bindings and routing keys.\n    Consumers subscribe to queues to receive messages.\n  contact:\n    name: RabbitMQ\n    url: https://www.rabbitmq.com/\n  license:\n    name: MPL 2.0\n    url: https://www.mozilla.org/en-US/MPL/2.0/\nservers:\n  default:\n    url: localhost:5672\n    protocol: amqp\n    protocolVersion: 0.9.1\n    description: Default RabbitMQ AMQP endpoint\ndefaultContentType: application/json\nchannels:\n  '{exchange}/{routing_key}':\n    description: >-\n      Messages are published to an exchange with a routing key. The exchange\n      routes messages to bound queues based on exchange type and binding rules.\n    parameters:\n      exchange:\n        description: The exchange name\n        schema:\n          type: string\n      routing_key:\n\
  \        description: The routing key for message routing\n        schema:\n          type: string\n    publish:\n      operationId: publishMessage\n      summary: Publish a message to an exchange\n      description: >-\n        Publish a message to the specified exchange with a routing key.\n        The exchange will route the message to matching queues based on\n        the exchange type (direct, fanout, topic, headers).\n      message:\n        $ref: '#/components/messages/AMQPMessage'\n      bindings:\n        amqp:\n          expiration: 60000\n          cc:\n            - additional.routing.key\n          priority: 10\n          deliveryMode: 2\n          mandatory: false\n          timestamp: true\n  '{queue}':\n    description: >-\n      Consumers subscribe to queues to receive messages. Queues can be durable,\n      exclusive, or auto-delete. Messages are distributed to consumers in\n      round-robin fashion.\n    parameters:\n      queue:\n        description: The queue name\n\
  \        schema:\n          type: string\n    subscribe:\n      operationId: consumeMessage\n      summary: Consume messages from a queue\n      description: >-\n        Subscribe to a queue to receive messages. Supports manual and\n        automatic acknowledgment modes.\n      message:\n        $ref: '#/components/messages/AMQPMessage'\n      bindings:\n        amqp:\n          ack: true\ncomponents:\n  messages:\n    AMQPMessage:\n      name: AMQPMessage\n      title: AMQP Message\n      summary: A message in RabbitMQ following the AMQP 0-9-1 protocol\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          content_type:\n            type: string\n          content_encoding:\n            type: string\n          delivery_mode:\n            type: integer\n            enum: [1, 2]\n            description: 1 for non-persistent, 2 for persistent\n          priority:\n            type: integer\n            minimum: 0\n            maximum:\
  \ 9\n          correlation_id:\n            type: string\n          reply_to:\n            type: string\n          expiration:\n            type: string\n          message_id:\n            type: string\n          timestamp:\n            type: integer\n          type:\n            type: string\n          user_id:\n            type: string\n          app_id:\n            type: string\n        additionalProperties:\n          description: Custom headers\n      payload:\n        type: object\n        description: The message body\n      bindings:\n        amqp:\n          contentEncoding: utf-8\n          messageType: application/json\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rabbitmq/refs/heads/main/asyncapi/rabbitmq-messaging.yml
spec_file: asyncapi/rabbitmq-messaging.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/rabbitmq/refs/heads/main/asyncapi/rabbitmq-messaging.yml
tags:
- AMQP
- Distributed Systems
- Event Streaming
- Message Broker
- Messaging
- Queue
- AsyncAPI
- Webhooks
- Events
version: 3.13.0
---
