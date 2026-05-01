---
api_specs:
- filename: azure-service-bus-openapi.yml
  format: yaml
  label: Azure Service Bus
  slug: azure-service-bus
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/azure-service-bus/refs/heads/main/openapi/azure-service-bus-openapi.yml
channels:
- description: A Service Bus queue provides FIFO message delivery to one or more competing consumers. Messages are stored durably in the queue until retrieved by a receiver.
  name: '{queueName}'
  operation: publish
  operation_id: sendToQueue
  summary: Send a message to a queue
- description: A Service Bus topic enables publish-subscribe messaging. Publishers send messages to a topic, and subscribers receive messages from subscriptions associated with the topic.
  name: '{topicName}'
  operation: publish
  operation_id: sendToTopic
  summary: Publish a message to a topic
- description: A subscription to a Service Bus topic. Each subscription receives a copy of messages published to the topic, filtered by subscription rules.
  name: '{topicName}/subscriptions/{subscriptionName}'
  operation: subscribe
  operation_id: receiveFromSubscription
  summary: Receive a message from a topic subscription
description: Azure Service Bus is a fully managed enterprise message broker with message queues and publish-subscribe topics. This AsyncAPI spec describes the messaging patterns for sending and receiving messages via Service Bus queues and topics.
layout: asyncapi
messages:
- description: ''
  name: ServiceBusMessage
  summary: A message sent or received via Azure Service Bus.
  title: Service Bus Message
- description: ''
  name: DeadLetterMessage
  summary: A message moved to the dead-letter queue.
  title: Dead Letter Message
name: Azure Service Bus Messaging
provider_name: Azure Service Bus
provider_slug: azure-service-bus
servers:
- description: Azure Service Bus AMQP endpoint
  name: azure-service-bus
  protocol: amqp
  url: '{namespaceName}.servicebus.windows.net'
- description: Azure Service Bus HTTP endpoint
  name: azure-service-bus-https
  protocol: https
  url: '{namespaceName}.servicebus.windows.net'
slug: azure-service-bus-asyncapi
source_filename: azure-service-bus-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Azure Service Bus Messaging\n  version: '2021-11-01'\n  description: >-\n    Azure Service Bus is a fully managed enterprise message broker with message\n    queues and publish-subscribe topics. This AsyncAPI spec describes the\n    messaging patterns for sending and receiving messages via Service Bus\n    queues and topics.\n  contact:\n    name: Microsoft Azure\n    url: https://azure.microsoft.com/en-us/products/service-bus\nservers:\n  azure-service-bus:\n    url: '{namespaceName}.servicebus.windows.net'\n    protocol: amqp\n    protocolVersion: '1.0'\n    description: Azure Service Bus AMQP endpoint\n    variables:\n      namespaceName:\n        description: The Service Bus namespace name\n  azure-service-bus-https:\n    url: '{namespaceName}.servicebus.windows.net'\n    protocol: https\n    description: Azure Service Bus HTTP endpoint\n    variables:\n      namespaceName:\n        description: The Service Bus namespace name\nchannels:\n\
  \  '{queueName}':\n    description: >-\n      A Service Bus queue provides FIFO message delivery to one or more\n      competing consumers. Messages are stored durably in the queue until\n      retrieved by a receiver.\n    parameters:\n      queueName:\n        description: The name of the Service Bus queue.\n        schema:\n          type: string\n    publish:\n      operationId: sendToQueue\n      summary: Send a message to a queue\n      description: >-\n        Send a message to a Service Bus queue. Messages can include a body,\n        application properties, and system properties such as TTL and\n        session ID.\n      message:\n        $ref: '#/components/messages/ServiceBusMessage'\n    subscribe:\n      operationId: receiveFromQueue\n      summary: Receive a message from a queue\n      description: >-\n        Receive messages from a Service Bus queue using peek-lock or\n        receive-and-delete mode.\n      message:\n        $ref: '#/components/messages/ServiceBusMessage'\n\
  \  '{topicName}':\n    description: >-\n      A Service Bus topic enables publish-subscribe messaging. Publishers\n      send messages to a topic, and subscribers receive messages from\n      subscriptions associated with the topic.\n    parameters:\n      topicName:\n        description: The name of the Service Bus topic.\n        schema:\n          type: string\n    publish:\n      operationId: sendToTopic\n      summary: Publish a message to a topic\n      description: >-\n        Publish a message to a Service Bus topic. The message is delivered\n        to all matching subscriptions based on filter rules.\n      message:\n        $ref: '#/components/messages/ServiceBusMessage'\n  '{topicName}/subscriptions/{subscriptionName}':\n    description: >-\n      A subscription to a Service Bus topic. Each subscription receives a\n      copy of messages published to the topic, filtered by subscription\n      rules.\n    parameters:\n      topicName:\n        description: The name of the Service\
  \ Bus topic.\n        schema:\n          type: string\n      subscriptionName:\n        description: The name of the subscription.\n        schema:\n          type: string\n    subscribe:\n      operationId: receiveFromSubscription\n      summary: Receive a message from a topic subscription\n      description: >-\n        Receive messages from a topic subscription using peek-lock or\n        receive-and-delete mode.\n      message:\n        $ref: '#/components/messages/ServiceBusMessage'\ncomponents:\n  messages:\n    ServiceBusMessage:\n      name: ServiceBusMessage\n      title: Service Bus Message\n      summary: A message sent or received via Azure Service Bus.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          body:\n            description: The message body. Can be any serializable content.\n          contentType:\n            type: string\n            description: The content type of the message body.\n          correlationId:\n\
  \            type: string\n            description: Correlation identifier for request-reply patterns.\n          subject:\n            type: string\n            description: Application-specific label (also known as Label).\n          messageId:\n            type: string\n            description: >-\n              Unique identifier for the message, used for duplicate\n              detection.\n          replyTo:\n            type: string\n            description: Address to reply to.\n          replyToSessionId:\n            type: string\n            description: Session identifier for reply messages.\n          sessionId:\n            type: string\n            description: Session identifier for session-aware queues/subscriptions.\n          timeToLive:\n            type: string\n            description: Message time-to-live (ISO 8601 duration).\n          to:\n            type: string\n            description: Destination address.\n          applicationProperties:\n            type:\
  \ object\n            additionalProperties: true\n            description: Application-specific custom properties.\n          enqueuedTime:\n            type: string\n            format: date-time\n            description: UTC time when the message was enqueued.\n          sequenceNumber:\n            type: integer\n            format: int64\n            description: Unique 64-bit integer assigned to a message by Service Bus.\n          deliveryCount:\n            type: integer\n            description: Number of deliveries attempted for this message.\n          lockToken:\n            type: string\n            format: uuid\n            description: Token for the current lock on the message (peek-lock mode).\n    DeadLetterMessage:\n      name: DeadLetterMessage\n      title: Dead Letter Message\n      summary: A message moved to the dead-letter queue.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          body:\n            description:\
  \ The original message body.\n          deadLetterReason:\n            type: string\n            description: Reason for dead-lettering.\n          deadLetterErrorDescription:\n            type: string\n            description: Error description for dead-lettering.\n          messageId:\n            type: string\n          enqueuedTime:\n            type: string\n            format: date-time\n          sequenceNumber:\n            type: integer\n            format: int64\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/azure-service-bus/refs/heads/main/asyncapi/azure-service-bus-asyncapi.yml
spec_file: asyncapi/azure-service-bus-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/azure-service-bus/refs/heads/main/asyncapi/azure-service-bus-asyncapi.yml
tags:
- Azure
- Cloud
- Enterprise
- Message Broker
- Messaging
- Pub/Sub
- Queues
- AsyncAPI
- Webhooks
- Events
version: '2021-11-01'
---
