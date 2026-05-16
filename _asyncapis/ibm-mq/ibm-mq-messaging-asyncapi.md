---
api_specs:
- filename: rest_api_swagger.json
  format: json
  label: IBM MQ REST API
  slug: ibm-mq-rest-api
  spec_type: OpenAPI
  url: https://www.ibm.com/docs/en/SSFKSJ_9.3.0/com.ibm.mq.dev.doc/rest_api_swagger.json
- filename: messaging_rest_api_swagger.json
  format: json
  label: IBM MQ Messaging REST API
  slug: ibm-mq-messaging-rest-api
  spec_type: OpenAPI
  url: https://www.ibm.com/docs/en/SSFKSJ_9.3.0/com.ibm.mq.dev.doc/messaging_rest_api_swagger.json
- filename: ibm-mq-messaging-asyncapi.yml
  format: yaml
  label: IBM MQ JMS API
  slug: ibm-mq-jms-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/ibm-mq/refs/heads/main/asyncapi/ibm-mq-messaging-asyncapi.yml
channels:
- description: Point-to-point messaging channel for sending and receiving messages on an IBM MQ local queue. Messages are delivered to exactly one consumer.
  name: queue/{queueName}
  operation: publish
  operation_id: sendToQueue
  summary: Send a message to a queue
- description: Publish/subscribe messaging channel for IBM MQ topics. Messages published to a topic are delivered to all active subscribers matching the topic string pattern.
  name: topic/{topicString}
  operation: publish
  operation_id: publishToTopic
  summary: Publish a message to a topic
- description: Dead-letter queue for messages that cannot be delivered to their intended destination. Undeliverable messages are routed here with a dead-letter header containing the reason for failure.
  name: deadLetterQueue
  operation: subscribe
  operation_id: receiveDeadLetterMessage
  summary: Receive undeliverable messages
- description: Request/reply messaging pattern where a requester sends a message to a request queue and waits for a response on a dynamically created or predefined reply queue.
  name: requestReply/{requestQueue}
  operation: publish
  operation_id: sendRequest
  summary: Send a request message
description: Asynchronous messaging interface for IBM MQ, supporting point-to-point queue-based messaging and publish/subscribe topic-based messaging. Defines the channels, operations, and message formats for applications integrating with IBM MQ via JMS, AMQP, or the native MQI protocol.
layout: asyncapi
messages:
- description: Standard IBM MQ message containing a message descriptor (MQMD) with metadata and a message body with the application payload.
  name: MQMessage
  summary: A message transmitted through IBM MQ
  title: IBM MQ Message
- description: Message that could not be delivered to its intended destination, prefixed with a dead-letter header (MQDLH) containing the reason code and original destination information.
  name: DeadLetterMessage
  summary: An undeliverable message routed to the dead-letter queue
  title: Dead Letter Message
- description: ''
  name: RequestMessage
  summary: A request message in a request/reply pattern
  title: Request Message
- description: ''
  name: ReplyMessage
  summary: A reply message correlated to a request
  title: Reply Message
name: IBM MQ Messaging
provider_name: IBM MQ
provider_slug: ibm-mq
servers:
- description: IBM MQ queue manager connection
  name: production
  protocol: ibmmq
  url: '{host}:{port}'
- description: IBM MQ AMQP 1.0 connection
  name: production-amqp
  protocol: amqp
  url: '{host}:{amqpPort}'
slug: ibm-mq-messaging-asyncapi
source_filename: ibm-mq-messaging-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: IBM MQ Messaging\n  version: '9.3'\n  description: >-\n    Asynchronous messaging interface for IBM MQ, supporting point-to-point\n    queue-based messaging and publish/subscribe topic-based messaging. Defines\n    the channels, operations, and message formats for applications integrating\n    with IBM MQ via JMS, AMQP, or the native MQI protocol.\n  contact:\n    name: IBM Support\n    url: https://www.ibm.com/mysupport\n    email: support@ibm.com\n  license:\n    name: IBM License\n    url: https://www.ibm.com/terms\n  externalDocs:\n    description: IBM MQ Documentation\n    url: https://www.ibm.com/docs/en/ibm-mq/latest\ndefaultContentType: application/json\n\nservers:\n  production:\n    url: '{host}:{port}'\n    protocol: ibmmq\n    protocolVersion: '9.3'\n    description: IBM MQ queue manager connection\n    variables:\n      host:\n        default: localhost\n        description: Hostname of the MQ queue manager\n      port:\n      \
  \  default: '1414'\n        description: Listener port of the MQ queue manager\n    security:\n      - mqAuth: []\n    bindings:\n      ibmmq:\n        groupId: PRODUCTION\n        cipherSpec: TLS_AES_256_GCM_SHA384\n        bindingVersion: 0.1.0\n  production-amqp:\n    url: '{host}:{amqpPort}'\n    protocol: amqp\n    protocolVersion: '1.0'\n    description: IBM MQ AMQP 1.0 connection\n    variables:\n      host:\n        default: localhost\n        description: Hostname of the MQ queue manager\n      amqpPort:\n        default: '5672'\n        description: AMQP listener port\n    security:\n      - mqAuth: []\n\nchannels:\n  queue/{queueName}:\n    description: >-\n      Point-to-point messaging channel for sending and receiving messages on\n      an IBM MQ local queue. Messages are delivered to exactly one consumer.\n    parameters:\n      queueName:\n        description: Name of the IBM MQ queue\n        schema:\n          type: string\n          maxLength: 48\n          pattern:\
  \ '^[A-Za-z0-9._/%]+$'\n    publish:\n      operationId: sendToQueue\n      summary: Send a message to a queue\n      description: >-\n        Put a message onto the specified MQ queue for asynchronous processing\n        by a consuming application.\n      message:\n        $ref: '#/components/messages/MQMessage'\n      bindings:\n        ibmmq:\n          type: jms\n          description: JMS message binding\n          bindingVersion: 0.1.0\n    subscribe:\n      operationId: receiveFromQueue\n      summary: Receive a message from a queue\n      description: >-\n        Get a message from the specified MQ queue. Supports both synchronous\n        get with wait and asynchronous message-driven consumption.\n      message:\n        $ref: '#/components/messages/MQMessage'\n      bindings:\n        ibmmq:\n          type: jms\n          bindingVersion: 0.1.0\n    bindings:\n      ibmmq:\n        destinationType: queue\n        queue:\n          objectName: '{queueName}'\n          isPartitioned:\
  \ false\n          exclusive: false\n        bindingVersion: 0.1.0\n\n  topic/{topicString}:\n    description: >-\n      Publish/subscribe messaging channel for IBM MQ topics. Messages\n      published to a topic are delivered to all active subscribers matching\n      the topic string pattern.\n    parameters:\n      topicString:\n        description: >-\n          IBM MQ topic string, supporting hierarchical topic levels separated\n          by forward slashes. Wildcards # (multi-level) and + (single-level)\n          are supported for subscriptions.\n        schema:\n          type: string\n    publish:\n      operationId: publishToTopic\n      summary: Publish a message to a topic\n      description: >-\n        Publish a message to the specified topic string. The message is\n        distributed to all matching subscribers.\n      message:\n        $ref: '#/components/messages/MQMessage'\n      bindings:\n        ibmmq:\n          type: jms\n          bindingVersion: 0.1.0\n    subscribe:\n\
  \      operationId: subscribeToTopic\n      summary: Subscribe to a topic\n      description: >-\n        Create a subscription to receive messages matching the topic string.\n        Supports both durable and non-durable subscriptions with wildcard\n        topic patterns.\n      message:\n        $ref: '#/components/messages/MQMessage'\n      bindings:\n        ibmmq:\n          type: jms\n          bindingVersion: 0.1.0\n    bindings:\n      ibmmq:\n        destinationType: topic\n        topic:\n          string: '{topicString}'\n          objectName: ''\n          durablePermitted: true\n          lastMsgRetained: false\n        bindingVersion: 0.1.0\n\n  deadLetterQueue:\n    description: >-\n      Dead-letter queue for messages that cannot be delivered to their\n      intended destination. Undeliverable messages are routed here with\n      a dead-letter header containing the reason for failure.\n    subscribe:\n      operationId: receiveDeadLetterMessage\n      summary: Receive\
  \ undeliverable messages\n      description: >-\n        Consume messages from the dead-letter queue for error handling\n        and reprocessing.\n      message:\n        $ref: '#/components/messages/DeadLetterMessage'\n    bindings:\n      ibmmq:\n        destinationType: queue\n        queue:\n          objectName: SYSTEM.DEAD.LETTER.QUEUE\n          isPartitioned: false\n          exclusive: false\n        bindingVersion: 0.1.0\n\n  requestReply/{requestQueue}:\n    description: >-\n      Request/reply messaging pattern where a requester sends a message to\n      a request queue and waits for a response on a dynamically created or\n      predefined reply queue.\n    parameters:\n      requestQueue:\n        description: Name of the request queue\n        schema:\n          type: string\n    publish:\n      operationId: sendRequest\n      summary: Send a request message\n      description: >-\n        Send a request message with a reply-to queue specified in the\n        message descriptor.\
  \ The responder processes the request and sends\n        the reply to the indicated queue.\n      message:\n        $ref: '#/components/messages/RequestMessage'\n    subscribe:\n      operationId: receiveReply\n      summary: Receive a reply message\n      description: >-\n        Receive a reply message correlated to the original request via\n        the correlation ID.\n      message:\n        $ref: '#/components/messages/ReplyMessage'\n    bindings:\n      ibmmq:\n        destinationType: queue\n        queue:\n          objectName: '{requestQueue}'\n        bindingVersion: 0.1.0\n\ncomponents:\n  securitySchemes:\n    mqAuth:\n      type: userPassword\n      description: IBM MQ user authentication via CONNAUTH\n\n  messages:\n    MQMessage:\n      name: MQMessage\n      title: IBM MQ Message\n      summary: A message transmitted through IBM MQ\n      description: >-\n        Standard IBM MQ message containing a message descriptor (MQMD) with\n        metadata and a message body with\
  \ the application payload.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          ibm-mq-md-messageId:\n            type: string\n            description: Unique message identifier (hex-encoded 24-byte value)\n          ibm-mq-md-correlationId:\n            type: string\n            description: Correlation identifier for linking related messages\n          ibm-mq-md-persistence:\n            type: string\n            enum:\n              - persistent\n              - nonPersistent\n            description: Whether the message survives queue manager restart\n          ibm-mq-md-expiry:\n            type: integer\n            description: Message expiry time in tenths of a second (-1 for unlimited)\n          ibm-mq-md-priority:\n            type: integer\n            minimum: 0\n            maximum: 9\n            description: Message priority (0 lowest, 9 highest)\n          ibm-mq-md-replyTo:\n            type: string\n            description:\
  \ Reply-to queue name\n          ibm-mq-md-replyToQmgr:\n            type: string\n            description: Reply-to queue manager name\n          ibm-mq-md-format:\n            type: string\n            description: Message format (e.g., MQSTR, MQHRF2)\n          ibm-mq-md-timestamp:\n            type: string\n            format: date-time\n            description: Message put timestamp\n      payload:\n        type: object\n        description: Application message payload\n\n    DeadLetterMessage:\n      name: DeadLetterMessage\n      title: Dead Letter Message\n      summary: An undeliverable message routed to the dead-letter queue\n      description: >-\n        Message that could not be delivered to its intended destination,\n        prefixed with a dead-letter header (MQDLH) containing the reason\n        code and original destination information.\n      headers:\n        type: object\n        properties:\n          ibm-mq-dlh-reason:\n            type: integer\n            description:\
  \ Reason code explaining why the message was undeliverable\n          ibm-mq-dlh-destQueueName:\n            type: string\n            description: Original destination queue name\n          ibm-mq-dlh-destQueueManager:\n            type: string\n            description: Original destination queue manager name\n          ibm-mq-dlh-putDate:\n            type: string\n            description: Date the message was put to the dead-letter queue\n          ibm-mq-dlh-putTime:\n            type: string\n            description: Time the message was put to the dead-letter queue\n      payload:\n        type: object\n        description: Original message payload\n\n    RequestMessage:\n      name: RequestMessage\n      title: Request Message\n      summary: A request message in a request/reply pattern\n      headers:\n        type: object\n        required:\n          - ibm-mq-md-replyTo\n        properties:\n          ibm-mq-md-messageId:\n            type: string\n            description: Unique\
  \ message identifier used for correlation\n          ibm-mq-md-replyTo:\n            type: string\n            description: Queue where the reply should be sent\n          ibm-mq-md-replyToQmgr:\n            type: string\n            description: Queue manager hosting the reply queue\n          ibm-mq-md-expiry:\n            type: integer\n            description: Message expiry in tenths of a second\n      payload:\n        type: object\n        description: Request payload\n\n    ReplyMessage:\n      name: ReplyMessage\n      title: Reply Message\n      summary: A reply message correlated to a request\n      headers:\n        type: object\n        properties:\n          ibm-mq-md-correlationId:\n            type: string\n            description: Correlation ID matching the original request message ID\n          ibm-mq-md-messageId:\n            type: string\n            description: Unique message identifier of the reply\n      payload:\n        type: object\n        description: Reply\
  \ payload\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/ibm-mq/refs/heads/main/asyncapi/ibm-mq-messaging-asyncapi.yml
spec_file: asyncapi/ibm-mq-messaging-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/ibm-mq/refs/heads/main/asyncapi/ibm-mq-messaging-asyncapi.yml
tags:
- Async
- Enterprise
- Integration
- Messaging
- Middleware
- Queue
- AsyncAPI
- Webhooks
- Events
version: '9.3'
---
