---
api_specs:
- filename: sinch-sms-openapi.yml
  format: yaml
  label: Sinch SMS API
  slug: sms-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-sms-openapi.yml
- filename: sinch-conversation-openapi.yml
  format: yaml
  label: Sinch Conversation API
  slug: conversation-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-conversation-openapi.yml
- filename: sinch-voice-openapi.yml
  format: yaml
  label: Sinch Voice API
  slug: voice-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-voice-openapi.yml
- filename: sinch-verification-openapi.yml
  format: yaml
  label: Sinch Verification API
  slug: verification-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-verification-openapi.yml
- filename: sinch-numbers-openapi.yml
  format: yaml
  label: Sinch Numbers API
  slug: numbers-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-numbers-openapi.yml
- filename: sinch-fax-openapi.yml
  format: yaml
  label: Sinch Fax API
  slug: fax-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-fax-openapi.yml
- filename: sinch-elastic-sip-trunking-openapi.yml
  format: yaml
  label: Sinch Elastic SIP Trunking API
  slug: elastic-sip-trunking-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-elastic-sip-trunking-openapi.yml
- filename: sinch-brands-openapi.yml
  format: yaml
  label: Sinch Brands API
  slug: brands-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-brands-openapi.yml
- filename: sinch-provisioning-openapi.yml
  format: yaml
  label: Sinch Provisioning API
  slug: provisioning-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-provisioning-openapi.yml
- filename: sinch-registration-openapi.yml
  format: yaml
  label: Sinch Registration API
  slug: registration-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-registration-openapi.yml
channels:
- description: Receives inbound message events from end users across all connected messaging channels.
  name: /conversation/message-inbound
  operation: publish
  operation_id: receiveInboundMessage
  summary: Receive an inbound message
- description: Receives delivery receipt events for messages sent to contacts.
  name: /conversation/message-delivery
  operation: publish
  operation_id: receiveMessageDelivery
  summary: Receive a message delivery receipt
- description: Receives inbound events from end users such as composing indicators and read receipts.
  name: /conversation/event-inbound
  operation: publish
  operation_id: receiveInboundEvent
  summary: Receive an inbound event
- description: Receives notifications when a new contact is created.
  name: /conversation/contact-create
  operation: publish
  operation_id: receiveContactCreate
  summary: Receive a contact creation event
- description: Receives notifications when a contact is updated.
  name: /conversation/contact-update
  operation: publish
  operation_id: receiveContactUpdate
  summary: Receive a contact update event
- description: Receives notifications when a contact is deleted.
  name: /conversation/contact-delete
  operation: publish
  operation_id: receiveContactDelete
  summary: Receive a contact deletion event
- description: Receives notifications when two contacts are merged.
  name: /conversation/contact-merge
  operation: publish
  operation_id: receiveContactMerge
  summary: Receive a contact merge event
- description: Receives notifications when a new conversation is started.
  name: /conversation/conversation-start
  operation: publish
  operation_id: receiveConversationStart
  summary: Receive a conversation start event
- description: Receives notifications when a conversation is stopped.
  name: /conversation/conversation-stop
  operation: publish
  operation_id: receiveConversationStop
  summary: Receive a conversation stop event
- description: Receives channel-specific events that do not map to the standard Conversation API event model.
  name: /conversation/channel-event
  operation: publish
  operation_id: receiveChannelEvent
  summary: Receive a channel event
- description: Receives capability lookup results for contacts.
  name: /conversation/capability
  operation: publish
  operation_id: receiveCapabilityResult
  summary: Receive a capability lookup result
- description: Receives opt-in events when contacts opt in to messaging.
  name: /conversation/opt-in
  operation: publish
  operation_id: receiveOptIn
  summary: Receive an opt-in event
- description: Receives opt-out events when contacts opt out of messaging.
  name: /conversation/opt-out
  operation: publish
  operation_id: receiveOptOut
  summary: Receive an opt-out event
- description: Receives smart conversation analysis results including sentiment analysis and intent classification.
  name: /conversation/smart-conversations
  operation: publish
  operation_id: receiveSmartConversationResult
  summary: Receive a smart conversation result
description: Event-driven webhooks for the Sinch Conversation API. The Conversation API delivers contact messages, delivery receipts, and various notifications through HTTP POST callbacks. Up to 5 webhooks can be configured per app, each subscribing to specific event triggers including inbound messages, delivery reports, contact changes, and conversation lifecycle events.
layout: asyncapi
messages:
- description: ''
  name: MessageInbound
  summary: An inbound message from an end user
  title: Inbound Message
- description: ''
  name: MessageDelivery
  summary: Delivery status update for a sent message
  title: Message Delivery Receipt
- description: ''
  name: EventInbound
  summary: An inbound event from an end user
  title: Inbound Event
- description: ''
  name: ContactEvent
  summary: A contact lifecycle event
  title: Contact Event
- description: ''
  name: ContactMergeEvent
  summary: Two contacts were merged
  title: Contact Merge Event
- description: ''
  name: ConversationEvent
  summary: A conversation lifecycle event
  title: Conversation Event
- description: ''
  name: ChannelEvent
  summary: A channel-specific event
  title: Channel Event
- description: ''
  name: CapabilityEvent
  summary: Capability lookup result
  title: Capability Event
- description: ''
  name: OptEvent
  summary: An opt-in or opt-out event
  title: Opt Event
- description: ''
  name: SmartConversationEvent
  summary: Smart conversation analysis result
  title: Smart Conversation Event
name: Sinch Conversation API Webhooks
provider_name: Sinch
provider_slug: sinch
servers:
- description: Your server endpoint configured as a webhook target for the Conversation API app. Webhooks are configured via the API or Sinch Dashboard.
  name: customerServer
  protocol: https
  url: '{webhookTarget}'
slug: sinch-conversation-webhooks-asyncapi
source_filename: sinch-conversation-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Sinch Conversation API Webhooks\n  description: >-\n    Event-driven webhooks for the Sinch Conversation API. The Conversation API\n    delivers contact messages, delivery receipts, and various notifications\n    through HTTP POST callbacks. Up to 5 webhooks can be configured per app,\n    each subscribing to specific event triggers including inbound messages,\n    delivery reports, contact changes, and conversation lifecycle events.\n  version: '1.0'\n  contact:\n    name: Sinch Support\n    url: https://www.sinch.com/contact-us/\nservers:\n  customerServer:\n    url: '{webhookTarget}'\n    protocol: https\n    description: >-\n      Your server endpoint configured as a webhook target for the Conversation\n      API app. Webhooks are configured via the API or Sinch Dashboard.\n    variables:\n      webhookTarget:\n        description: Your webhook target URL\n    security:\n      - hmacAuth: []\nchannels:\n  /conversation/message-inbound:\n\
  \    description: >-\n      Receives inbound message events from end users across all connected\n      messaging channels.\n    publish:\n      operationId: receiveInboundMessage\n      summary: Receive an inbound message\n      description: >-\n        Triggered when an end user sends a message on any connected channel.\n        The message is normalized to the Conversation API format.\n      message:\n        $ref: '#/components/messages/MessageInbound'\n  /conversation/message-delivery:\n    description: >-\n      Receives delivery receipt events for messages sent to contacts.\n    publish:\n      operationId: receiveMessageDelivery\n      summary: Receive a message delivery receipt\n      description: >-\n        Triggered when the delivery status of a sent message changes,\n        indicating delivery success or failure on the channel.\n      message:\n        $ref: '#/components/messages/MessageDelivery'\n  /conversation/event-inbound:\n    description: >-\n      Receives inbound\
  \ events from end users such as composing indicators\n      and read receipts.\n    publish:\n      operationId: receiveInboundEvent\n      summary: Receive an inbound event\n      description: >-\n        Triggered when an end user generates an event on a channel, such as\n        starting to type or reading a message.\n      message:\n        $ref: '#/components/messages/EventInbound'\n  /conversation/contact-create:\n    description: >-\n      Receives notifications when a new contact is created.\n    publish:\n      operationId: receiveContactCreate\n      summary: Receive a contact creation event\n      message:\n        $ref: '#/components/messages/ContactEvent'\n  /conversation/contact-update:\n    description: >-\n      Receives notifications when a contact is updated.\n    publish:\n      operationId: receiveContactUpdate\n      summary: Receive a contact update event\n      message:\n        $ref: '#/components/messages/ContactEvent'\n  /conversation/contact-delete:\n    description:\
  \ >-\n      Receives notifications when a contact is deleted.\n    publish:\n      operationId: receiveContactDelete\n      summary: Receive a contact deletion event\n      message:\n        $ref: '#/components/messages/ContactEvent'\n  /conversation/contact-merge:\n    description: >-\n      Receives notifications when two contacts are merged.\n    publish:\n      operationId: receiveContactMerge\n      summary: Receive a contact merge event\n      message:\n        $ref: '#/components/messages/ContactMergeEvent'\n  /conversation/conversation-start:\n    description: >-\n      Receives notifications when a new conversation is started.\n    publish:\n      operationId: receiveConversationStart\n      summary: Receive a conversation start event\n      message:\n        $ref: '#/components/messages/ConversationEvent'\n  /conversation/conversation-stop:\n    description: >-\n      Receives notifications when a conversation is stopped.\n    publish:\n      operationId: receiveConversationStop\n\
  \      summary: Receive a conversation stop event\n      message:\n        $ref: '#/components/messages/ConversationEvent'\n  /conversation/channel-event:\n    description: >-\n      Receives channel-specific events that do not map to the standard\n      Conversation API event model.\n    publish:\n      operationId: receiveChannelEvent\n      summary: Receive a channel event\n      message:\n        $ref: '#/components/messages/ChannelEvent'\n  /conversation/capability:\n    description: >-\n      Receives capability lookup results for contacts.\n    publish:\n      operationId: receiveCapabilityResult\n      summary: Receive a capability lookup result\n      message:\n        $ref: '#/components/messages/CapabilityEvent'\n  /conversation/opt-in:\n    description: >-\n      Receives opt-in events when contacts opt in to messaging.\n    publish:\n      operationId: receiveOptIn\n      summary: Receive an opt-in event\n      message:\n        $ref: '#/components/messages/OptEvent'\n  /conversation/opt-out:\n\
  \    description: >-\n      Receives opt-out events when contacts opt out of messaging.\n    publish:\n      operationId: receiveOptOut\n      summary: Receive an opt-out event\n      message:\n        $ref: '#/components/messages/OptEvent'\n  /conversation/smart-conversations:\n    description: >-\n      Receives smart conversation analysis results including sentiment\n      analysis and intent classification.\n    publish:\n      operationId: receiveSmartConversationResult\n      summary: Receive a smart conversation result\n      message:\n        $ref: '#/components/messages/SmartConversationEvent'\ncomponents:\n  securitySchemes:\n    hmacAuth:\n      type: httpApiKey\n      in: header\n      name: x-sinch-webhook-signature\n      description: >-\n        HMAC signature for webhook payload verification using the secret\n        configured on the webhook.\n  messages:\n    MessageInbound:\n      name: MESSAGE_INBOUND\n      title: Inbound Message\n      summary: An inbound message\
  \ from an end user\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/MessageInboundPayload'\n    MessageDelivery:\n      name: MESSAGE_DELIVERY\n      title: Message Delivery Receipt\n      summary: Delivery status update for a sent message\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/MessageDeliveryPayload'\n    EventInbound:\n      name: EVENT_INBOUND\n      title: Inbound Event\n      summary: An inbound event from an end user\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventInboundPayload'\n    ContactEvent:\n      name: CONTACT_EVENT\n      title: Contact Event\n      summary: A contact lifecycle event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ContactEventPayload'\n    ContactMergeEvent:\n      name: CONTACT_MERGE\n      title: Contact Merge Event\n      summary: Two contacts were merged\n      contentType:\
  \ application/json\n      payload:\n        $ref: '#/components/schemas/ContactMergeEventPayload'\n    ConversationEvent:\n      name: CONVERSATION_EVENT\n      title: Conversation Event\n      summary: A conversation lifecycle event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ConversationEventPayload'\n    ChannelEvent:\n      name: CHANNEL_EVENT\n      title: Channel Event\n      summary: A channel-specific event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ChannelEventPayload'\n    CapabilityEvent:\n      name: CAPABILITY\n      title: Capability Event\n      summary: Capability lookup result\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CapabilityEventPayload'\n    OptEvent:\n      name: OPT_EVENT\n      title: Opt Event\n      summary: An opt-in or opt-out event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OptEventPayload'\n\
  \    SmartConversationEvent:\n      name: SMART_CONVERSATIONS\n      title: Smart Conversation Event\n      summary: Smart conversation analysis result\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SmartConversationPayload'\n  schemas:\n    MessageInboundPayload:\n      type: object\n      properties:\n        app_id:\n          type: string\n          description: The app identifier\n        accepted_time:\n          type: string\n          format: date-time\n          description: When the event was accepted\n        event_time:\n          type: string\n          format: date-time\n          description: When the event occurred\n        project_id:\n          type: string\n          description: The project identifier\n        message:\n          type: object\n          description: The inbound message\n          properties:\n            id:\n              type: string\n              description: The message identifier\n            direction:\n\
  \              type: string\n              description: The message direction\n            contact_message:\n              type: object\n              description: The contact message content\n              properties:\n                text_message:\n                  type: object\n                  properties:\n                    text:\n                      type: string\n                      description: The message text\n                media_message:\n                  type: object\n                  properties:\n                    url:\n                      type: string\n                      description: Media URL\n            channel_identity:\n              type: object\n              description: The channel identity\n              properties:\n                channel:\n                  type: string\n                  description: The channel type\n                identity:\n                  type: string\n                  description: The channel-specific identity\n   \
  \             app_id:\n                  type: string\n                  description: The app ID\n            conversation_id:\n              type: string\n              description: The conversation identifier\n            contact_id:\n              type: string\n              description: The contact identifier\n            metadata:\n              type: string\n              description: Message metadata\n            accept_time:\n              type: string\n              format: date-time\n              description: When the message was accepted\n        message_metadata:\n          type: string\n          description: Additional message metadata\n    MessageDeliveryPayload:\n      type: object\n      properties:\n        app_id:\n          type: string\n          description: The app identifier\n        accepted_time:\n          type: string\n          format: date-time\n          description: When the event was accepted\n        event_time:\n          type: string\n          format:\
  \ date-time\n          description: When the event occurred\n        project_id:\n          type: string\n          description: The project identifier\n        message_delivery_report:\n          type: object\n          description: The delivery report\n          properties:\n            message_id:\n              type: string\n              description: The message identifier\n            conversation_id:\n              type: string\n              description: The conversation identifier\n            status:\n              type: string\n              enum:\n                - QUEUED_ON_CHANNEL\n                - DELIVERED\n                - READ\n                - FAILED\n                - SWITCHING_CHANNEL\n              description: The delivery status\n            channel_identity:\n              type: object\n              description: The channel identity\n              properties:\n                channel:\n                  type: string\n                  description: The channel\
  \ type\n                identity:\n                  type: string\n                  description: The channel identity\n            contact_id:\n              type: string\n              description: The contact identifier\n            reason:\n              type: string\n              description: Reason for failure if applicable\n            metadata:\n              type: string\n              description: Delivery metadata\n    EventInboundPayload:\n      type: object\n      properties:\n        app_id:\n          type: string\n          description: The app identifier\n        accepted_time:\n          type: string\n          format: date-time\n          description: When the event was accepted\n        project_id:\n          type: string\n          description: The project identifier\n        event:\n          type: object\n          description: The inbound event\n          properties:\n            composing_event:\n              type: object\n              description: Composing\
  \ indicator event\n            contact_id:\n              type: string\n              description: The contact identifier\n            channel_identity:\n              type: object\n              description: The channel identity\n              properties:\n                channel:\n                  type: string\n                  description: The channel type\n                identity:\n                  type: string\n                  description: The channel identity\n    ContactEventPayload:\n      type: object\n      properties:\n        app_id:\n          type: string\n          description: The app identifier\n        accepted_time:\n          type: string\n          format: date-time\n          description: When the event was accepted\n        project_id:\n          type: string\n          description: The project identifier\n        contact:\n          type: object\n          description: The contact object\n          properties:\n            id:\n              type: string\n\
  \              description: The contact identifier\n            display_name:\n              type: string\n              description: The contact display name\n            channel_identities:\n              type: array\n              description: Channel identities\n              items:\n                type: object\n                properties:\n                  channel:\n                    type: string\n                  identity:\n                    type: string\n    ContactMergeEventPayload:\n      type: object\n      properties:\n        app_id:\n          type: string\n          description: The app identifier\n        project_id:\n          type: string\n          description: The project identifier\n        preserved_contact:\n          type: object\n          description: The surviving contact after merge\n          properties:\n            id:\n              type: string\n              description: The contact identifier\n        deleted_contact:\n          type: object\n \
  \         description: The contact that was merged and deleted\n          properties:\n            id:\n              type: string\n              description: The contact identifier\n    ConversationEventPayload:\n      type: object\n      properties:\n        app_id:\n          type: string\n          description: The app identifier\n        project_id:\n          type: string\n          description: The project identifier\n        conversation:\n          type: object\n          description: The conversation\n          properties:\n            id:\n              type: string\n              description: The conversation identifier\n            app_id:\n              type: string\n              description: The app identifier\n            contact_id:\n              type: string\n              description: The contact identifier\n            active:\n              type: boolean\n              description: Whether the conversation is active\n    ChannelEventPayload:\n      type: object\n\
  \      properties:\n        app_id:\n          type: string\n          description: The app identifier\n        project_id:\n          type: string\n          description: The project identifier\n        channel:\n          type: string\n          description: The channel type\n        event_type:\n          type: string\n          description: The channel-specific event type\n        additional_data:\n          type: object\n          description: Channel-specific event data\n    CapabilityEventPayload:\n      type: object\n      properties:\n        app_id:\n          type: string\n          description: The app identifier\n        project_id:\n          type: string\n          description: The project identifier\n        request_id:\n          type: string\n          description: The capability query request ID\n        contact_id:\n          type: string\n          description: The contact identifier\n        channel:\n          type: string\n          description: The channel queried\n\
  \        capability_status:\n          type: string\n          description: The capability status result\n        reason:\n          type: string\n          description: Reason if capability is unavailable\n    OptEventPayload:\n      type: object\n      properties:\n        app_id:\n          type: string\n          description: The app identifier\n        project_id:\n          type: string\n          description: The project identifier\n        contact_id:\n          type: string\n          description: The contact identifier\n        channel:\n          type: string\n          description: The channel\n        identity:\n          type: string\n          description: The channel identity\n        status:\n          type: string\n          enum:\n            - OPT_IN_SUCCEEDED\n            - OPT_IN_FAILED\n            - OPT_OUT_SUCCEEDED\n            - OPT_OUT_FAILED\n          description: The opt event status\n        request_id:\n          type: string\n          description: The\
  \ request identifier\n    SmartConversationPayload:\n      type: object\n      properties:\n        app_id:\n          type: string\n          description: The app identifier\n        project_id:\n          type: string\n          description: The project identifier\n        message_id:\n          type: string\n          description: The analyzed message identifier\n        contact_id:\n          type: string\n          description: The contact identifier\n        conversation_id:\n          type: string\n          description: The conversation identifier\n        analysis_results:\n          type: object\n          description: Smart conversation analysis results\n          properties:\n            sentiment_analysis:\n              type: object\n              description: Sentiment analysis result\n              properties:\n                sentiment:\n                  type: string\n                  description: The detected sentiment\n                score:\n                  type:\
  \ number\n                  description: The confidence score\n            intent_analysis:\n              type: object\n              description: Intent classification result\n              properties:\n                intent:\n                  type: string\n                  description: The detected intent\n                score:\n                  type: number\n                  description: The confidence score\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/asyncapi/sinch-conversation-webhooks-asyncapi.yml
spec_file: asyncapi/sinch-conversation-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/asyncapi/sinch-conversation-webhooks-asyncapi.yml
tags:
- Communications
- Messaging
- SMS
- Voice
- Verification
- CPaaS
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
