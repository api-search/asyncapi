---
channels:
- description: Publish/subscribe channel for order creation events. Messages are published to a topic exchange and routed to all bound queues.
  name: orderCreated
- description: Point-to-point channel for order processing. Messages are sent to a direct exchange and consumed by a single worker from a shared queue.
  name: orderProcessing
- description: Request channel for the request/reply pattern. Clients send requests with a reply-to header and correlation ID for response matching.
  name: orderStatusRequest
- description: Reply channel for the request/reply pattern. The server publishes responses to the client-specified reply-to queue with the matching correlation ID.
  name: orderStatusReply
- description: Fanout channel for broadcasting notifications to all subscribers. Uses a fanout exchange to deliver messages to every bound queue regardless of routing key.
  name: notifications
description: AsyncAPI specification for AMQP (Advanced Message Queuing Protocol) messaging patterns including publish/subscribe, request/reply, and point-to-point messaging. AMQP 0-9-1 defines exchanges, queues, and bindings as the core building blocks for flexible message routing.
layout: asyncapi
messages:
- description: ''
  name: OrderCreated
  summary: Event published when a new order is created
  title: Order Created Event
- description: ''
  name: OrderProcess
  summary: Command to process an order
  title: Order Processing Command
- description: ''
  name: OrderStatusRequest
  summary: Request for the current status of an order
  title: Order Status Request
- description: ''
  name: OrderStatusReply
  summary: Reply containing the current status of an order
  title: Order Status Reply
- description: ''
  name: Notification
  summary: A notification broadcast to all subscribers
  title: Notification Message
name: AMQP Messaging API
provider_name: AMQP
provider_slug: amqp
servers:
- description: Production AMQP broker
  name: production
  protocol: amqp
  url: ''
slug: amqp-messaging
source_yaml: "asyncapi: 3.0.0\ninfo:\n  title: AMQP Messaging API\n  version: 1.0.0\n  description: >-\n    AsyncAPI specification for AMQP (Advanced Message Queuing Protocol)\n    messaging patterns including publish/subscribe, request/reply, and\n    point-to-point messaging. AMQP 0-9-1 defines exchanges, queues, and\n    bindings as the core building blocks for flexible message routing.\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\n\nservers:\n  production:\n    host: amqp.example.com:5672\n    protocol: amqp\n    protocolVersion: 0.9.1\n    description: Production AMQP broker\n    security:\n      - type: userPassword\n    tags:\n      - name: production\n\nchannels:\n  orderCreated:\n    address: orders.created\n    description: >-\n      Publish/subscribe channel for order creation events. Messages are\n      published to a topic exchange and routed to all bound queues.\n    messages:\n      orderCreatedMessage:\n        $ref: '#/components/messages/OrderCreated'\n\
  \    bindings:\n      amqp:\n        is: routingKey\n        exchange:\n          name: orders\n          type: topic\n          durable: true\n          autoDelete: false\n        queue:\n          name: orders.created\n          durable: true\n          exclusive: false\n          autoDelete: false\n\n  orderProcessing:\n    address: orders.process\n    description: >-\n      Point-to-point channel for order processing. Messages are sent to a\n      direct exchange and consumed by a single worker from a shared queue.\n    messages:\n      orderProcessMessage:\n        $ref: '#/components/messages/OrderProcess'\n    bindings:\n      amqp:\n        is: routingKey\n        exchange:\n          name: orders.direct\n          type: direct\n          durable: true\n          autoDelete: false\n        queue:\n          name: orders.process.queue\n          durable: true\n          exclusive: false\n          autoDelete: false\n\n  orderStatusRequest:\n    address: orders.status.request\n \
  \   description: >-\n      Request channel for the request/reply pattern. Clients send requests\n      with a reply-to header and correlation ID for response matching.\n    messages:\n      orderStatusRequestMessage:\n        $ref: '#/components/messages/OrderStatusRequest'\n    bindings:\n      amqp:\n        is: routingKey\n        exchange:\n          name: orders.rpc\n          type: direct\n          durable: true\n          autoDelete: false\n        queue:\n          name: orders.status.request.queue\n          durable: true\n          exclusive: false\n          autoDelete: false\n\n  orderStatusReply:\n    address: orders.status.reply\n    description: >-\n      Reply channel for the request/reply pattern. The server publishes\n      responses to the client-specified reply-to queue with the matching\n      correlation ID.\n    messages:\n      orderStatusReplyMessage:\n        $ref: '#/components/messages/OrderStatusReply'\n    bindings:\n      amqp:\n        is: routingKey\n\
  \        exchange:\n          name: ''\n          type: direct\n          durable: true\n          autoDelete: false\n        queue:\n          name: amq.rabbitmq.reply-to\n          durable: false\n          exclusive: true\n          autoDelete: true\n\n  notifications:\n    address: notifications.#\n    description: >-\n      Fanout channel for broadcasting notifications to all subscribers.\n      Uses a fanout exchange to deliver messages to every bound queue\n      regardless of routing key.\n    messages:\n      notificationMessage:\n        $ref: '#/components/messages/Notification'\n    bindings:\n      amqp:\n        is: routingKey\n        exchange:\n          name: notifications.fanout\n          type: fanout\n          durable: true\n          autoDelete: false\n\noperations:\n  publishOrderCreated:\n    action: send\n    channel:\n      $ref: '#/channels/orderCreated'\n    summary: Publish an order created event\n    description: >-\n      Publishes an order created event\
  \ to the topic exchange. All consumers\n      with matching routing key bindings will receive the message.\n    bindings:\n      amqp:\n        deliveryMode: 2\n        mandatory: true\n\n  consumeOrderCreated:\n    action: receive\n    channel:\n      $ref: '#/channels/orderCreated'\n    summary: Subscribe to order created events\n    description: >-\n      Subscribes to order created events from the topic exchange.\n\n  sendOrderForProcessing:\n    action: send\n    channel:\n      $ref: '#/channels/orderProcessing'\n    summary: Send an order for processing\n    description: >-\n      Sends an order to the processing queue. Only one consumer will\n      process each message (competing consumers pattern).\n    bindings:\n      amqp:\n        deliveryMode: 2\n        mandatory: true\n\n  processOrder:\n    action: receive\n    channel:\n      $ref: '#/channels/orderProcessing'\n    summary: Receive an order for processing\n    bindings:\n      amqp:\n        ack: true\n        prefetchCount:\
  \ 1\n\n  requestOrderStatus:\n    action: send\n    channel:\n      $ref: '#/channels/orderStatusRequest'\n    summary: Request the status of an order\n    description: >-\n      Sends a request for order status using the request/reply pattern.\n      The reply-to queue and correlation ID are set in message properties.\n    bindings:\n      amqp:\n        deliveryMode: 2\n\n  receiveOrderStatusReply:\n    action: receive\n    channel:\n      $ref: '#/channels/orderStatusReply'\n    summary: Receive the order status reply\n\n  broadcastNotification:\n    action: send\n    channel:\n      $ref: '#/channels/notifications'\n    summary: Broadcast a notification to all subscribers\n    bindings:\n      amqp:\n        deliveryMode: 1\n\ncomponents:\n  messages:\n    OrderCreated:\n      name: OrderCreated\n      title: Order Created Event\n      summary: Event published when a new order is created\n      contentType: application/json\n      traits:\n        - $ref: '#/components/messageTraits/commonHeaders'\n\
  \      payload:\n        type: object\n        required:\n          - orderId\n          - customerId\n          - createdAt\n        properties:\n          orderId:\n            type: string\n            format: uuid\n            description: Unique identifier for the order\n          customerId:\n            type: string\n            description: Identifier of the customer who placed the order\n          items:\n            type: array\n            items:\n              type: object\n              properties:\n                productId:\n                  type: string\n                quantity:\n                  type: integer\n                  minimum: 1\n                price:\n                  type: number\n                  format: double\n          totalAmount:\n            type: number\n            format: double\n          currency:\n            type: string\n            pattern: ^[A-Z]{3}$\n          createdAt:\n            type: string\n            format: date-time\n\n  \
  \  OrderProcess:\n      name: OrderProcess\n      title: Order Processing Command\n      summary: Command to process an order\n      contentType: application/json\n      traits:\n        - $ref: '#/components/messageTraits/commonHeaders'\n      payload:\n        type: object\n        required:\n          - orderId\n          - action\n        properties:\n          orderId:\n            type: string\n            format: uuid\n          action:\n            type: string\n            enum:\n              - validate\n              - fulfill\n              - ship\n              - cancel\n          priority:\n            type: integer\n            minimum: 0\n            maximum: 9\n\n    OrderStatusRequest:\n      name: OrderStatusRequest\n      title: Order Status Request\n      summary: Request for the current status of an order\n      contentType: application/json\n      correlationId:\n        location: $message.header#/correlationId\n      traits:\n        - $ref: '#/components/messageTraits/commonHeaders'\n\
  \      payload:\n        type: object\n        required:\n          - orderId\n        properties:\n          orderId:\n            type: string\n            format: uuid\n\n    OrderStatusReply:\n      name: OrderStatusReply\n      title: Order Status Reply\n      summary: Reply containing the current status of an order\n      contentType: application/json\n      correlationId:\n        location: $message.header#/correlationId\n      payload:\n        type: object\n        required:\n          - orderId\n          - status\n        properties:\n          orderId:\n            type: string\n            format: uuid\n          status:\n            type: string\n            enum:\n              - pending\n              - processing\n              - shipped\n              - delivered\n              - cancelled\n          updatedAt:\n            type: string\n            format: date-time\n          estimatedDelivery:\n            type: string\n            format: date-time\n\n    Notification:\n\
  \      name: Notification\n      title: Notification Message\n      summary: A notification broadcast to all subscribers\n      contentType: application/json\n      traits:\n        - $ref: '#/components/messageTraits/commonHeaders'\n      payload:\n        type: object\n        required:\n          - type\n          - message\n          - timestamp\n        properties:\n          type:\n            type: string\n            enum:\n              - info\n              - warning\n              - error\n              - alert\n          message:\n            type: string\n          timestamp:\n            type: string\n            format: date-time\n          metadata:\n            type: object\n            additionalProperties: true\n\n  messageTraits:\n    commonHeaders:\n      headers:\n        type: object\n        properties:\n          correlationId:\n            type: string\n            format: uuid\n            description: Unique identifier for correlating request/reply messages\n\
  \          messageId:\n            type: string\n            format: uuid\n            description: Unique identifier for the message\n          timestamp:\n            type: string\n            format: date-time\n            description: Timestamp when the message was created\n          contentType:\n            type: string\n            description: MIME type of the message body\n          replyTo:\n            type: string\n            description: Queue name for reply messages in request/reply pattern\n          expiration:\n            type: string\n            description: Message TTL in milliseconds\n          priority:\n            type: integer\n            minimum: 0\n            maximum: 9\n            description: Message priority (0-9)\n          deliveryMode:\n            type: integer\n            enum:\n              - 1\n              - 2\n            description: 1 for non-persistent, 2 for persistent delivery\n          appId:\n            type: string\n            description:\
  \ Identifier of the application that produced the message\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/amqp/refs/heads/main/asyncapi/amqp-messaging.yml
spec_file: asyncapi/amqp-messaging.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/amqp/refs/heads/main/asyncapi/amqp-messaging.yml
tags:
- AMQP
- Asynchronous
- Message Queue
- Messaging
- Middleware
- Open Standard
- Publish Subscribe
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
