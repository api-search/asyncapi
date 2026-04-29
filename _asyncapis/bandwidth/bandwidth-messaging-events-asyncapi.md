---
channels:
- description: Inbound message webhook sent when a message is received by one of your Bandwidth phone numbers. Provides the full message content, sender, and recipient information.
  name: /messaging/inbound
  operation: publish
  operation_id: onInboundMessage
  summary: Inbound message received
- description: Message delivery status webhook sent for outbound messages. You will receive either a Message Delivered or Message Failed event for each outbound message, but never both.
  name: /messaging/status
  operation: publish
  operation_id: onMessageStatus
  summary: Message delivery status update
description: Bandwidth Messaging API sends webhooks to your application for real-time message delivery notifications and inbound message alerts. Callbacks are sent via HTTP POST to the callback URL configured on the Bandwidth application associated with the message. You MUST respond with an HTTP 2xx status code for every callback. Bandwidth will retry callbacks over the next 24 hours until a 2xx response is received.
layout: asyncapi
messages:
- description: ''
  name: InboundMessageCallback
  summary: Sent when an inbound message is received by a Bandwidth number
  title: Inbound Message Callback
- description: ''
  name: MessageDeliveredCallback
  summary: Sent when an outbound message is successfully delivered
  title: Message Delivered Callback
- description: ''
  name: MessageFailedCallback
  summary: Sent when an outbound message fails to deliver
  title: Message Failed Callback
- description: ''
  name: MessageSendingCallback
  summary: Sent when an outbound message is being sent to the carrier
  title: Message Sending Callback
name: Bandwidth Messaging Events
provider_name: Bandwidth
provider_slug: bandwidth
servers:
- description: Your application's webhook endpoint. The URL is configured on the Bandwidth application associated with the message.
  name: production
  protocol: https
  url: '{callbackUrl}'
slug: bandwidth-messaging-events-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Bandwidth Messaging Events\n  description: >-\n    Bandwidth Messaging API sends webhooks to your application for\n    real-time message delivery notifications and inbound message alerts.\n    Callbacks are sent via HTTP POST to the callback URL configured on\n    the Bandwidth application associated with the message. You MUST\n    respond with an HTTP 2xx status code for every callback. Bandwidth\n    will retry callbacks over the next 24 hours until a 2xx response\n    is received.\n  version: '2.0'\n  contact:\n    name: Bandwidth Support\n    url: https://support.bandwidth.com\nservers:\n  production:\n    url: '{callbackUrl}'\n    protocol: https\n    description: >-\n      Your application's webhook endpoint. The URL is configured on\n      the Bandwidth application associated with the message.\n    variables:\n      callbackUrl:\n        description: The callback URL configured on your Bandwidth application\n    security:\n      - basicAuth:\
  \ []\nchannels:\n  /messaging/inbound:\n    description: >-\n      Inbound message webhook sent when a message is received by one\n      of your Bandwidth phone numbers. Provides the full message content,\n      sender, and recipient information.\n    publish:\n      operationId: onInboundMessage\n      summary: Inbound message received\n      message:\n        $ref: '#/components/messages/InboundMessageCallback'\n  /messaging/status:\n    description: >-\n      Message delivery status webhook sent for outbound messages. You\n      will receive either a Message Delivered or Message Failed event\n      for each outbound message, but never both.\n    publish:\n      operationId: onMessageStatus\n      summary: Message delivery status update\n      message:\n        oneOf:\n          - $ref: '#/components/messages/MessageDeliveredCallback'\n          - $ref: '#/components/messages/MessageFailedCallback'\n          - $ref: '#/components/messages/MessageSendingCallback'\ncomponents:\n  securitySchemes:\n\
  \    basicAuth:\n      type: http\n      scheme: basic\n      description: >-\n        Optional HTTP Basic Authentication for webhook endpoints.\n        Configure credentials in your Bandwidth application settings.\n  messages:\n    InboundMessageCallback:\n      name: InboundMessageCallback\n      title: Inbound Message Callback\n      summary: >-\n        Sent when an inbound message is received by a Bandwidth number\n      contentType: application/json\n      payload:\n        type: array\n        items:\n          $ref: '#/components/schemas/InboundMessageEvent'\n    MessageDeliveredCallback:\n      name: MessageDeliveredCallback\n      title: Message Delivered Callback\n      summary: >-\n        Sent when an outbound message is successfully delivered\n      contentType: application/json\n      payload:\n        type: array\n        items:\n          $ref: '#/components/schemas/MessageDeliveredEvent'\n    MessageFailedCallback:\n      name: MessageFailedCallback\n      title: Message\
  \ Failed Callback\n      summary: >-\n        Sent when an outbound message fails to deliver\n      contentType: application/json\n      payload:\n        type: array\n        items:\n          $ref: '#/components/schemas/MessageFailedEvent'\n    MessageSendingCallback:\n      name: MessageSendingCallback\n      title: Message Sending Callback\n      summary: >-\n        Sent when an outbound message is being sent to the carrier\n      contentType: application/json\n      payload:\n        type: array\n        items:\n          $ref: '#/components/schemas/MessageSendingEvent'\n  schemas:\n    BaseMessageEvent:\n      type: object\n      properties:\n        time:\n          type: string\n          format: date-time\n          description: The time of the event\n        type:\n          type: string\n          description: The type of messaging event\n        to:\n          type: string\n          description: The destination phone number\n        description:\n          type: string\n\
  \          description: A human-readable description of the event\n        message:\n          type: object\n          properties:\n            id:\n              type: string\n              description: The unique message identifier\n            owner:\n              type: string\n              description: The Bandwidth number that owns the message\n            applicationId:\n              type: string\n              description: The application ID\n            time:\n              type: string\n              format: date-time\n              description: The time the message was created\n            segmentCount:\n              type: integer\n              description: The number of message segments\n            direction:\n              type: string\n              enum:\n                - in\n                - out\n              description: The message direction\n            to:\n              type: array\n              items:\n                type: string\n              description:\
  \ The destination phone numbers\n            from:\n              type: string\n              description: The source phone number\n            media:\n              type: array\n              items:\n                type: string\n                format: uri\n              description: Media URLs for MMS attachments\n            text:\n              type: string\n              description: The message text content\n            tag:\n              type: string\n              description: Custom tag attached to the message\n            priority:\n              type: string\n              enum:\n                - default\n                - high\n              description: The message priority\n    InboundMessageEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseMessageEvent'\n        - type: object\n          properties:\n            type:\n              type: string\n              const: message-received\n              description: Event type is always message-received\n   \
  \ MessageDeliveredEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseMessageEvent'\n        - type: object\n          properties:\n            type:\n              type: string\n              const: message-delivered\n              description: Event type is always message-delivered\n    MessageFailedEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseMessageEvent'\n        - type: object\n          properties:\n            type:\n              type: string\n              const: message-failed\n              description: Event type is always message-failed\n            errorCode:\n              type: integer\n              description: >-\n                The Bandwidth error code indicating the failure reason\n    MessageSendingEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseMessageEvent'\n        - type: object\n          properties:\n            type:\n              type: string\n              const: message-sending\n              description:\
  \ Event type is always message-sending\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/bandwidth/refs/heads/main/asyncapi/bandwidth-messaging-events-asyncapi.yml
spec_file: asyncapi/bandwidth-messaging-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/bandwidth/refs/heads/main/asyncapi/bandwidth-messaging-events-asyncapi.yml
tags:
- Communications
- CPaaS
- Voice
- Messaging
- Telephony
- SMS
- MFA
- AsyncAPI
- Webhooks
- Events
version: '2.0'
---
