---
api_specs:
- filename: messagebird-sms-messaging-openapi.yml
  format: yaml
  label: MessageBird SMS Messaging API
  slug: sms-messaging-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/openapi/messagebird-sms-messaging-openapi.yml
- filename: messagebird-voice-calling-openapi.yml
  format: yaml
  label: MessageBird Voice Calling API
  slug: voice-calling-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/openapi/messagebird-voice-calling-openapi.yml
- filename: messagebird-voice-messaging-openapi.yml
  format: yaml
  label: MessageBird Voice Messaging API
  slug: voice-messaging-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/openapi/messagebird-voice-messaging-openapi.yml
- filename: messagebird-conversations-openapi.yml
  format: yaml
  label: MessageBird Conversations API
  slug: conversations-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/openapi/messagebird-conversations-openapi.yml
- filename: messagebird-whatsapp-openapi.yml
  format: yaml
  label: MessageBird WhatsApp API
  slug: whatsapp-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/openapi/messagebird-whatsapp-openapi.yml
- filename: messagebird-verify-openapi.yml
  format: yaml
  label: MessageBird Verify API
  slug: verify-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/openapi/messagebird-verify-openapi.yml
- filename: messagebird-lookup-openapi.yml
  format: yaml
  label: MessageBird Lookup API
  slug: lookup-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/openapi/messagebird-lookup-openapi.yml
- filename: messagebird-hlr-openapi.yml
  format: yaml
  label: MessageBird HLR API
  slug: hlr-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/openapi/messagebird-hlr-openapi.yml
- filename: messagebird-contacts-openapi.yml
  format: yaml
  label: MessageBird Contacts API
  slug: contacts-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/openapi/messagebird-contacts-openapi.yml
- filename: messagebird-numbers-openapi.yml
  format: yaml
  label: MessageBird Numbers API
  slug: numbers-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/openapi/messagebird-numbers-openapi.yml
- filename: messagebird-balance-openapi.yml
  format: yaml
  label: MessageBird Balance API
  slug: balance-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/openapi/messagebird-balance-openapi.yml
- filename: messagebird-integrations-openapi.yml
  format: yaml
  label: MessageBird Integrations API
  slug: integrations-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/openapi/messagebird-integrations-openapi.yml
channels:
- description: Endpoint on your server that receives conversation event notifications from MessageBird.
  name: /webhook
  operation: publish
  operation_id: receiveConversationEvent
  summary: Receive a conversation event
- description: Endpoint on your server that receives voice call event notifications from MessageBird.
  name: /voice-webhook
  operation: publish
  operation_id: receiveVoiceEvent
  summary: Receive a voice call event
- description: Endpoint on your server that receives SMS delivery status reports from MessageBird.
  name: /sms-status-webhook
  operation: publish
  operation_id: receiveSmsStatusReport
  summary: Receive an SMS status report
description: The MessageBird Conversations webhook system delivers real-time notifications for conversation events across all messaging channels including SMS, WhatsApp, Facebook Messenger, Telegram, and more. Webhooks are triggered when messages are created or updated, and when conversations are created or updated. The platform supports up to 10 channel-specific webhooks and 5 generic webhooks per account.
layout: asyncapi
messages:
- description: ''
  name: MessageCreated
  summary: Triggered when a new message is created in a conversation, either sent by the business or received from a customer.
  title: Message Created
- description: ''
  name: MessageUpdated
  summary: Triggered when a message status changes, such as transitioning from sent to delivered or read.
  title: Message Updated
- description: ''
  name: ConversationCreated
  summary: Triggered when a new conversation is created, typically when a new contact sends their first message.
  title: Conversation Created
- description: ''
  name: ConversationUpdated
  summary: Triggered when a conversation is updated, such as a status change from active to archived.
  title: Conversation Updated
- description: ''
  name: VoiceCallEvent
  summary: Triggered when a voice call event occurs, including call creation, ringing, answering, and hangup events.
  title: Voice Call Event
- description: ''
  name: SmsStatusReport
  summary: Triggered when the delivery status of an SMS message changes.
  title: SMS Status Report
name: MessageBird Conversations Events
provider_name: messagebird
provider_slug: messagebird
servers:
- description: Your server endpoint that receives webhook payloads from MessageBird when conversation events occur.
  name: webhook
  protocol: https
  url: '{webhookUrl}'
slug: messagebird-conversations-asyncapi
source_filename: messagebird-conversations-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: MessageBird Conversations Events\n  description: >-\n    The MessageBird Conversations webhook system delivers real-time\n    notifications for conversation events across all messaging channels\n    including SMS, WhatsApp, Facebook Messenger, Telegram, and more.\n    Webhooks are triggered when messages are created or updated, and when\n    conversations are created or updated. The platform supports up to 10\n    channel-specific webhooks and 5 generic webhooks per account.\n  version: '1.0'\n  contact:\n    name: MessageBird Support\n    url: https://support.messagebird.com\nservers:\n  webhook:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your server endpoint that receives webhook payloads from\n      MessageBird when conversation events occur.\n    variables:\n      webhookUrl:\n        description: >-\n          The URL configured in the webhook settings to receive event\n          notifications.\n    security:\n\
  \      - signatureAuth: []\nchannels:\n  /webhook:\n    description: >-\n      Endpoint on your server that receives conversation event\n      notifications from MessageBird.\n    publish:\n      operationId: receiveConversationEvent\n      summary: Receive a conversation event\n      description: >-\n        MessageBird sends a JSON payload to your webhook URL when a\n        subscribed event occurs. Events include message creation and\n        updates, as well as conversation creation and updates.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/MessageCreated'\n          - $ref: '#/components/messages/MessageUpdated'\n          - $ref: '#/components/messages/ConversationCreated'\n          - $ref: '#/components/messages/ConversationUpdated'\n  /voice-webhook:\n    description: >-\n      Endpoint on your server that receives voice call event\n      notifications from MessageBird.\n    publish:\n      operationId: receiveVoiceEvent\n      summary: Receive a voice\
  \ call event\n      description: >-\n        MessageBird sends call event data to your webhook URL when\n        voice call status changes occur, such as call creation,\n        ringing, answering, and hangup.\n      message:\n        $ref: '#/components/messages/VoiceCallEvent'\n  /sms-status-webhook:\n    description: >-\n      Endpoint on your server that receives SMS delivery status\n      reports from MessageBird.\n    publish:\n      operationId: receiveSmsStatusReport\n      summary: Receive an SMS status report\n      description: >-\n        MessageBird sends delivery status updates to the reportUrl\n        specified when sending an SMS message. Status reports indicate\n        whether the message was delivered, expired, or failed.\n      message:\n        $ref: '#/components/messages/SmsStatusReport'\ncomponents:\n  securitySchemes:\n    signatureAuth:\n      type: httpApiKey\n      name: MessageBird-Signature\n      in: header\n      description: >-\n        Webhook payloads\
  \ include a signature header for verifying the\n        authenticity of the request. The signature is computed using\n        the webhook signing key.\n  messages:\n    MessageCreated:\n      name: message.created\n      title: Message Created\n      summary: >-\n        Triggered when a new message is created in a conversation, either\n        sent by the business or received from a customer.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/MessageEvent'\n    MessageUpdated:\n      name: message.updated\n      title: Message Updated\n      summary: >-\n        Triggered when a message status changes, such as transitioning\n        from sent to delivered or read.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/MessageEvent'\n    ConversationCreated:\n      name: conversation.created\n      title: Conversation Created\n      summary: >-\n        Triggered when a new conversation is created, typically when\
  \ a\n        new contact sends their first message.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ConversationEvent'\n    ConversationUpdated:\n      name: conversation.updated\n      title: Conversation Updated\n      summary: >-\n        Triggered when a conversation is updated, such as a status\n        change from active to archived.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ConversationEvent'\n    VoiceCallEvent:\n      name: voice.call.event\n      title: Voice Call Event\n      summary: >-\n        Triggered when a voice call event occurs, including call\n        creation, ringing, answering, and hangup events.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/VoiceCallEventPayload'\n    SmsStatusReport:\n      name: sms.status.report\n      title: SMS Status Report\n      summary: >-\n        Triggered when the delivery status of an SMS message changes.\n\
  \      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SmsStatusReportPayload'\n  schemas:\n    MessageEvent:\n      type: object\n      properties:\n        type:\n          type: string\n          description: >-\n            The event type.\n          enum:\n            - message.created\n            - message.updated\n        conversation:\n          type: object\n          description: >-\n            The conversation associated with the event.\n          properties:\n            id:\n              type: string\n              description: >-\n                The conversation identifier.\n            contactId:\n              type: string\n              description: >-\n                The contact identifier.\n            status:\n              type: string\n              description: >-\n                The conversation status.\n              enum:\n                - active\n                - archived\n            createdDatetime:\n             \
  \ type: string\n              format: date-time\n              description: >-\n                When the conversation was created.\n            updatedDatetime:\n              type: string\n              format: date-time\n              description: >-\n                When the conversation was last updated.\n            lastReceivedDatetime:\n              type: string\n              format: date-time\n              description: >-\n                When the last message was received.\n        message:\n          type: object\n          description: >-\n            The message associated with the event.\n          properties:\n            id:\n              type: string\n              description: >-\n                The message identifier.\n            conversationId:\n              type: string\n              description: >-\n                The conversation identifier.\n            channelId:\n              type: string\n              description: >-\n                The channel identifier.\n\
  \            platform:\n              type: string\n              description: >-\n                The messaging platform.\n            to:\n              type: string\n              description: >-\n                The recipient identifier.\n            from:\n              type: string\n              description: >-\n                The sender identifier.\n            direction:\n              type: string\n              description: >-\n                The direction of the message.\n              enum:\n                - sent\n                - received\n            status:\n              type: string\n              description: >-\n                The delivery status.\n              enum:\n                - accepted\n                - pending\n                - sent\n                - delivered\n                - read\n                - failed\n                - deleted\n            type:\n              type: string\n              description: >-\n                The content type.\n\
  \              enum:\n                - text\n                - image\n                - video\n                - audio\n                - file\n                - location\n                - hsm\n            content:\n              type: object\n              description: >-\n                The message content.\n            createdDatetime:\n              type: string\n              format: date-time\n              description: >-\n                When the message was created.\n            updatedDatetime:\n              type: string\n              format: date-time\n              description: >-\n                When the message was last updated.\n    ConversationEvent:\n      type: object\n      properties:\n        type:\n          type: string\n          description: >-\n            The event type.\n          enum:\n            - conversation.created\n            - conversation.updated\n        conversation:\n          type: object\n          description: >-\n            The conversation\
  \ associated with the event.\n          properties:\n            id:\n              type: string\n              description: >-\n                The conversation identifier.\n            contactId:\n              type: string\n              description: >-\n                The contact identifier.\n            status:\n              type: string\n              description: >-\n                The conversation status.\n              enum:\n                - active\n                - archived\n            createdDatetime:\n              type: string\n              format: date-time\n              description: >-\n                When the conversation was created.\n            updatedDatetime:\n              type: string\n              format: date-time\n              description: >-\n                When the conversation was last updated.\n    VoiceCallEventPayload:\n      type: object\n      properties:\n        id:\n          type: string\n          description: >-\n            The call\
  \ identifier.\n        status:\n          type: string\n          description: >-\n            The call status.\n          enum:\n            - queued\n            - starting\n            - ringing\n            - ongoing\n            - busy\n            - no_answer\n            - failed\n            - ended\n        source:\n          type: string\n          description: >-\n            The source number.\n        destination:\n          type: string\n          description: >-\n            The destination number.\n        direction:\n          type: string\n          description: >-\n            The call direction.\n          enum:\n            - incoming\n            - outgoing\n        legs:\n          type: array\n          description: >-\n            The call legs.\n          items:\n            type: object\n            properties:\n              id:\n                type: string\n                description: >-\n                  The leg identifier.\n              status:\n    \
  \            type: string\n                description: >-\n                  The leg status.\n              source:\n                type: string\n                description: >-\n                  The leg source.\n              destination:\n                type: string\n                description: >-\n                  The leg destination.\n              direction:\n                type: string\n                description: >-\n                  The leg direction.\n        createdAt:\n          type: string\n          format: date-time\n          description: >-\n            When the call was created.\n        updatedAt:\n          type: string\n          format: date-time\n          description: >-\n            When the call was last updated.\n    SmsStatusReportPayload:\n      type: object\n      properties:\n        id:\n          type: string\n          description: >-\n            The message identifier.\n        reference:\n          type: string\n          description: >-\n\
  \            The client reference.\n        recipient:\n          type: string\n          description: >-\n            The recipient phone number.\n        status:\n          type: string\n          description: >-\n            The delivery status.\n          enum:\n            - scheduled\n            - sent\n            - buffered\n            - delivered\n            - expired\n            - delivery_failed\n        statusReason:\n          type: string\n          description: >-\n            The reason for the status, particularly for failures.\n        statusDatetime:\n          type: string\n          format: date-time\n          description: >-\n            The date and time of the status update.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/asyncapi/messagebird-conversations-asyncapi.yml
spec_file: asyncapi/messagebird-conversations-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/messagebird/refs/heads/main/asyncapi/messagebird-conversations-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
