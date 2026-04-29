---
channels:
- description: The root path of the topic-specific endpoint. POST to this channel to publish messages. Each topic has its own unique base URL.
  name: /
  operation: publish
  operation_id: publishMessage
  summary: Publish a message to the topic
description: Boomi Event Streams provides a publish-subscribe messaging system within the Boomi Enterprise Platform. Topics act as channels where producers publish messages and consumers receive them via Boomi recipes or HTTP REST. Event Streams integrate natively with the Boomi integration platform as triggers and actions, enabling loosely-coupled, event-driven integration workflows. Messages may be up to 5 MB and the API enforces a rate limit of 60,000 requests per IP per 5-minute window.
layout: asyncapi
messages:
- description: Publishes one or more messages in the predefined multi-message JSON format. Each message in the array has a payload field and an optional properties map for custom metadata.
  name: MultiMessage
  summary: Publish multiple messages in structured JSON format.
  title: Multi-Message Publish
- description: Publishes a single message without transformation. The content type can be application/json, text/plain, or application/xml. Message properties are passed via request headers prefixed with x-msg-props-.
  name: SingleMessage
  summary: Publish a single message in its original format.
  title: Single Message Publish
- description: A message delivered to a Boomi integration process that is configured to listen on this event topic. Contains the original payload and any properties set by the producer.
  name: DeliveredMessage
  summary: A message delivered to a Boomi recipe subscriber.
  title: Delivered Message
name: Boomi Event Streams
provider_name: Boomi
provider_slug: boomi
servers:
- description: Topic-specific REST endpoint. Each Boomi Event Streams topic has a unique URL available from the Event Streams UI in the Boomi platform.
  name: production
  protocol: https
  url: '{topicEndpoint}'
slug: boomi-event-streams-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Boomi Event Streams\n  description: >-\n    Boomi Event Streams provides a publish-subscribe messaging system within\n    the Boomi Enterprise Platform. Topics act as channels where producers\n    publish messages and consumers receive them via Boomi recipes or HTTP REST.\n    Event Streams integrate natively with the Boomi integration platform as\n    triggers and actions, enabling loosely-coupled, event-driven integration\n    workflows. Messages may be up to 5 MB and the API enforces a rate limit of\n    60,000 requests per IP per 5-minute window.\n  version: '1.0'\n  contact:\n    name: Boomi Support\n    url: https://community.boomi.com/s/support\n  license:\n    name: Boomi Terms of Service\n    url: https://boomi.com/legal/service/\nexternalDocs:\n  description: Boomi Event Streams Documentation\n  url: https://help.boomi.com/docs/Atomsphere/Event%20Streams/es-REST_API\nservers:\n  production:\n    url: '{topicEndpoint}'\n    protocol:\
  \ https\n    description: >-\n      Topic-specific REST endpoint. Each Boomi Event Streams topic has a\n      unique URL available from the Event Streams UI in the Boomi platform.\n    variables:\n      topicEndpoint:\n        description: The unique hostname for this event topic's REST endpoint.\n        default: your-topic.event-streams.boomi.com\n    security:\n      - bearerAuth: []\nchannels:\n  /:\n    description: >-\n      The root path of the topic-specific endpoint. POST to this channel to\n      publish messages. Each topic has its own unique base URL.\n    publish:\n      operationId: publishMessage\n      summary: Publish a message to the topic\n      description: >-\n        Publish one or more messages to this event topic. Supports two modes:\n        multi-message JSON format (payload + properties per message) and\n        single-message mode (original format with properties in headers).\n        Maximum message size is 5 MB and total request size is 10 MB.\n      message:\n\
  \        oneOf:\n          - $ref: '#/components/messages/MultiMessage'\n          - $ref: '#/components/messages/SingleMessage'\n    subscribe:\n      operationId: receiveMessage\n      summary: Receive messages from the topic\n      description: >-\n        Messages received by Boomi recipes subscribed to this topic. Each\n        delivered message contains the payload and any properties set by the\n        producer. Messages can be consumed via Boomi integration triggers\n        configured to listen on the topic.\n      message:\n        $ref: '#/components/messages/DeliveredMessage'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: http\n      scheme: bearer\n      description: >-\n        Environment Token obtained from the Boomi Event Streams UI. Include as\n        Authorization: Bearer {environment_token}.\n  messages:\n    MultiMessage:\n      name: MultiMessage\n      title: Multi-Message Publish\n      summary: Publish multiple messages in structured JSON format.\n\
  \      description: >-\n        Publishes one or more messages in the predefined multi-message JSON\n        format. Each message in the array has a payload field and an optional\n        properties map for custom metadata.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/MultiMessagePayload'\n    SingleMessage:\n      name: SingleMessage\n      title: Single Message Publish\n      summary: Publish a single message in its original format.\n      description: >-\n        Publishes a single message without transformation. The content type\n        can be application/json, text/plain, or application/xml. Message\n        properties are passed via request headers prefixed with x-msg-props-.\n      contentType: application/json\n      headers:\n        type: object\n        description: >-\n          Headers prefixed with x-msg-props- are treated as message\n          properties. For example, x-msg-props-priority: high.\n        additionalProperties:\n\
  \          type: string\n      payload:\n        $ref: '#/components/schemas/SingleMessagePayload'\n    DeliveredMessage:\n      name: DeliveredMessage\n      title: Delivered Message\n      summary: A message delivered to a Boomi recipe subscriber.\n      description: >-\n        A message delivered to a Boomi integration process that is configured\n        to listen on this event topic. Contains the original payload and\n        any properties set by the producer.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DeliveredMessagePayload'\n  schemas:\n    MultiMessagePayload:\n      type: object\n      description: Request body for the multi-message publish mode.\n      required: [messages]\n      properties:\n        messages:\n          type: array\n          description: >-\n            Array of messages to publish. Each must include a payload;\n            properties are optional custom metadata.\n          items:\n            type: object\n\
  \            required: [payload]\n            properties:\n              payload:\n                type: string\n                description: Message content as a string (text, JSON, or XML).\n              properties:\n                type: object\n                description: Optional key-value metadata for this message.\n                additionalProperties:\n                  type: string\n    SingleMessagePayload:\n      description: >-\n        A single message payload in its original format. Content type\n        determines parsing — application/json, text/plain, or application/xml.\n      oneOf:\n        - type: object\n          description: JSON message payload.\n          additionalProperties: true\n        - type: string\n          description: Plain text or XML message payload.\n    DeliveredMessagePayload:\n      type: object\n      description: The structure of a message as received by a Boomi recipe.\n      properties:\n        payload:\n          description: The original\
  \ message content.\n          oneOf:\n            - type: string\n            - type: object\n              additionalProperties: true\n        properties:\n          type: object\n          description: Message metadata set by the producer.\n          additionalProperties:\n            type: string\n        messageId:\n          type: string\n          description: Unique identifier assigned to this message by Event Streams.\n        topicId:\n          type: string\n          description: ID of the topic this message was published to.\n        timestamp:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp when the message was published.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/boomi/refs/heads/main/asyncapi/boomi-event-streams-asyncapi.yml
spec_file: asyncapi/boomi-event-streams-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/boomi/refs/heads/main/asyncapi/boomi-event-streams-asyncapi.yml
tags:
- AI Agents
- Automation
- B2B
- Data Integration
- EDI
- Integrations
- Management
- MFT
- Platform
- Workflows
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
