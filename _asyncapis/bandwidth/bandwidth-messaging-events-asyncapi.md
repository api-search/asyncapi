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
