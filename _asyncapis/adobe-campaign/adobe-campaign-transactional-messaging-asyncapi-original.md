---
channels:
- description: Channel for triggering transactional email messages. Events submitted here are processed asynchronously by the Campaign transactional messaging engine and result in personalized email delivery to the specified recipient.
  name: transactionalEvent/email
  operation: publish
  operation_id: triggerEmailEvent
  summary: Trigger a transactional email event
- description: Channel for triggering transactional SMS messages. Events submitted here result in personalized SMS delivery to the specified mobile phone number.
  name: transactionalEvent/sms
  operation: publish
  operation_id: triggerSmsEvent
  summary: Trigger a transactional SMS event
- description: Channel for triggering transactional push notifications. Events submitted here result in push notification delivery to the specified device via Apple Push Notification service (APNs) or Firebase Cloud Messaging (FCM).
  name: transactionalEvent/push
  operation: publish
  operation_id: triggerPushEvent
  summary: Trigger a transactional push notification event
- description: Channel for receiving transactional event status updates. After an event is submitted, its status transitions through the processing lifecycle and can be polled to determine the outcome.
  name: transactionalEvent/status
  operation: subscribe
  operation_id: receiveEventStatus
  summary: Receive event processing status updates
- description: Channel for submitting batches of real-time events via Campaign Classic SOAP interface. More efficient than individual event submission when processing high volumes of transactional events.
  name: batchEvent
  operation: publish
  operation_id: submitBatchEvents
  summary: Submit a batch of transactional events
description: Event-driven transactional messaging system for Adobe Campaign. Supports triggering personalized messages across email, SMS, and push notification channels in response to real-time customer events. Events follow an asynchronous lifecycle from submission through delivery or failure. Covers both Campaign Standard REST event triggers and Campaign Classic SOAP PushEvent patterns.
layout: asyncapi
messages:
- description: Event payload for triggering a transactional email message with personalization context data.
  name: TransactionalEmailEvent
  summary: Transactional email event
  title: TransactionalEmailEvent
- description: Event payload for triggering a transactional SMS message.
  name: TransactionalSmsEvent
  summary: Transactional SMS event
  title: TransactionalSmsEvent
- description: Event payload for triggering a transactional push notification.
  name: TransactionalPushEvent
  summary: Transactional push notification event
  title: TransactionalPushEvent
- description: Status update for a previously submitted transactional event, indicating its current position in the processing lifecycle.
  name: EventStatusUpdate
  summary: Event processing status
  title: EventStatusUpdate
- description: SOAP payload containing multiple real-time events for batch processing by Campaign Classic Message Center.
  name: BatchEventSubmission
  summary: Batch event submission
  title: BatchEventSubmission
name: Adobe Campaign Transactional Messaging Events
provider_name: Adobe Campaign
provider_slug: adobe-campaign
servers:
- description: Campaign Standard transactional event endpoint. Events are triggered via REST POST and status is polled via GET.
  name: standard
  protocol: https
  url: https://mc.adobe.io/{ORGANIZATION}/campaign
- description: Campaign Classic SOAP-based event endpoint. Events are pushed via nms:rtEvent#PushEvent and nms:batchEvent#PushEvents SOAP methods.
  name: classic
  protocol: https
  url: https://{instance}.campaign.adobe.com
slug: adobe-campaign-transactional-messaging-asyncapi-original
source_yaml: "asyncapi: 2.0.0\ninfo:\n  title: Adobe Campaign Transactional Messaging Events\n  description: >-\n    Event-driven transactional messaging system for Adobe Campaign. Supports\n    triggering personalized messages across email, SMS, and push notification\n    channels in response to real-time customer events. Events follow an\n    asynchronous lifecycle from submission through delivery or failure. Covers\n    both Campaign Standard REST event triggers and Campaign Classic SOAP\n    PushEvent patterns.\n  version: 1.0.0\n  contact:\n    name: Adobe Developer Support\n    url: https://developer.adobe.com/\n  license:\n    name: Proprietary\n    url: https://www.adobe.com/legal/terms.html\nservers:\n  standard:\n    url: https://mc.adobe.io/{ORGANIZATION}/campaign\n    protocol: https\n    description: >-\n      Campaign Standard transactional event endpoint. Events are triggered\n      via REST POST and status is polled via GET.\n  classic:\n    url: https://{instance}.campaign.adobe.com\n\
  \    protocol: https\n    description: >-\n      Campaign Classic SOAP-based event endpoint. Events are pushed via\n      nms:rtEvent#PushEvent and nms:batchEvent#PushEvents SOAP methods.\nchannels:\n  transactionalEvent/email:\n    description: >-\n      Channel for triggering transactional email messages. Events submitted\n      here are processed asynchronously by the Campaign transactional\n      messaging engine and result in personalized email delivery to the\n      specified recipient.\n    publish:\n      summary: Trigger a transactional email event\n      operationId: triggerEmailEvent\n      message:\n        $ref: '#/components/messages/TransactionalEmailEvent'\n      bindings:\n        http:\n          type: request\n          method: POST\n          headers:\n            type: object\n            properties:\n              Content-Type:\n                type: string\n                enum:\n                  - application/json\n              Authorization:\n               \
  \ type: string\n                description: Bearer token from Adobe IMS OAuth.\n              X-Api-Key:\n                type: string\n                description: Adobe Developer Console API Key.\n  transactionalEvent/sms:\n    description: >-\n      Channel for triggering transactional SMS messages. Events submitted\n      here result in personalized SMS delivery to the specified mobile\n      phone number.\n    publish:\n      summary: Trigger a transactional SMS event\n      operationId: triggerSmsEvent\n      message:\n        $ref: '#/components/messages/TransactionalSmsEvent'\n      bindings:\n        http:\n          type: request\n          method: POST\n          headers:\n            type: object\n            properties:\n              Content-Type:\n                type: string\n                enum:\n                  - application/json\n  transactionalEvent/push:\n    description: >-\n      Channel for triggering transactional push notifications. Events\n      submitted\
  \ here result in push notification delivery to the specified\n      device via Apple Push Notification service (APNs) or Firebase Cloud\n      Messaging (FCM).\n    publish:\n      summary: Trigger a transactional push notification event\n      operationId: triggerPushEvent\n      message:\n        $ref: '#/components/messages/TransactionalPushEvent'\n      bindings:\n        http:\n          type: request\n          method: POST\n          headers:\n            type: object\n            properties:\n              Content-Type:\n                type: string\n                enum:\n                  - application/json\n  transactionalEvent/status:\n    description: >-\n      Channel for receiving transactional event status updates. After an\n      event is submitted, its status transitions through the processing\n      lifecycle and can be polled to determine the outcome.\n    subscribe:\n      summary: Receive event processing status updates\n      operationId: receiveEventStatus\n   \
  \   message:\n        $ref: '#/components/messages/EventStatusUpdate'\n      bindings:\n        http:\n          type: request\n          method: GET\n  batchEvent:\n    description: >-\n      Channel for submitting batches of real-time events via Campaign\n      Classic SOAP interface. More efficient than individual event\n      submission when processing high volumes of transactional events.\n    publish:\n      summary: Submit a batch of transactional events\n      operationId: submitBatchEvents\n      message:\n        $ref: '#/components/messages/BatchEventSubmission'\n      bindings:\n        http:\n          type: request\n          method: POST\n          headers:\n            type: object\n            properties:\n              Content-Type:\n                type: string\n                enum:\n                  - text/xml\n              SOAPAction:\n                type: string\n                enum:\n                  - 'nms:batchEvent#PushEvents'\ncomponents:\n  messages:\n\
  \    TransactionalEmailEvent:\n      summary: Transactional email event\n      description: >-\n        Event payload for triggering a transactional email message with\n        personalization context data.\n      payload:\n        $ref: '#/components/schemas/EmailEvent'\n    TransactionalSmsEvent:\n      summary: Transactional SMS event\n      description: >-\n        Event payload for triggering a transactional SMS message.\n      payload:\n        $ref: '#/components/schemas/SmsEvent'\n    TransactionalPushEvent:\n      summary: Transactional push notification event\n      description: >-\n        Event payload for triggering a transactional push notification.\n      payload:\n        $ref: '#/components/schemas/PushEvent'\n    EventStatusUpdate:\n      summary: Event processing status\n      description: >-\n        Status update for a previously submitted transactional event,\n        indicating its current position in the processing lifecycle.\n      payload:\n        $ref: '#/components/schemas/EventStatus'\n\
  \    BatchEventSubmission:\n      summary: Batch event submission\n      description: >-\n        SOAP payload containing multiple real-time events for batch\n        processing by Campaign Classic Message Center.\n      payload:\n        $ref: '#/components/schemas/BatchEvent'\n  schemas:\n    EmailEvent:\n      type: object\n      required:\n        - email\n        - ctx\n      properties:\n        email:\n          type: string\n          format: email\n          description: Recipient email address for the transactional message.\n        ctx:\n          type: object\n          description: >-\n            Context data for message personalization. Fields must match\n            the variables defined in the transactional message template.\n          additionalProperties: true\n        scheduled:\n          type: string\n          format: date-time\n          description: Optional scheduled send time for delayed delivery.\n        expiration:\n          type: string\n          format:\
  \ date-time\n          description: >-\n            Optional expiration time after which the event will not be\n            processed.\n    SmsEvent:\n      type: object\n      required:\n        - mobilePhone\n        - ctx\n      properties:\n        mobilePhone:\n          type: string\n          description: Recipient mobile phone number in international format.\n        ctx:\n          type: object\n          description: Context data for SMS message personalization.\n          additionalProperties: true\n        scheduled:\n          type: string\n          format: date-time\n          description: Optional scheduled send time.\n        expiration:\n          type: string\n          format: date-time\n          description: Optional event expiration time.\n    PushEvent:\n      type: object\n      required:\n        - ctx\n      properties:\n        registrationToken:\n          type: string\n          description: >-\n            Device registration token for push notification delivery\n\
  \            (APNs or FCM token).\n        pushPlatform:\n          type: string\n          enum:\n            - apns\n            - gcm\n          description: >-\n            Target push platform. apns for Apple Push Notification service,\n            gcm for Firebase Cloud Messaging (Google).\n        ctx:\n          type: object\n          description: Context data for push notification personalization.\n          additionalProperties: true\n        scheduled:\n          type: string\n          format: date-time\n          description: Optional scheduled send time.\n        expiration:\n          type: string\n          format: date-time\n          description: Optional event expiration time.\n    EventStatus:\n      type: object\n      properties:\n        PKey:\n          type: string\n          description: Unique PKEY identifier of the event.\n        eventId:\n          type: string\n          description: Unique event identifier.\n        status:\n          type: string\n   \
  \       enum:\n            - pending\n            - processing\n            - paused\n            - processed\n            - ignored\n            - deliveryFailed\n            - routingFailed\n            - targetingFailed\n            - tooOld\n          description: >-\n            Current processing status. pending = queued for processing,\n            processing = currently being handled, paused = temporarily\n            held, processed = successfully delivered, ignored = skipped\n            by rules, deliveryFailed = delivery attempt failed,\n            routingFailed = could not route to execution instance,\n            targetingFailed = recipient targeting failed, tooOld = event\n            exceeded its expiration time.\n        reason:\n          type: string\n          description: >-\n            Human-readable reason for failure status. Only present when\n            status indicates a failure condition.\n        channel:\n          type: string\n          enum:\n       \
  \     - email\n            - sms\n            - push\n          description: The delivery channel used for the event.\n        timestamp:\n          type: string\n          format: date-time\n          description: Timestamp of the last status update.\n    BatchEvent:\n      type: object\n      description: >-\n        Container for multiple real-time events submitted via Campaign\n        Classic SOAP PushEvents method.\n      properties:\n        events:\n          type: array\n          description: Array of individual transactional events.\n          items:\n            type: object\n            properties:\n              type:\n                type: string\n                description: >-\n                  Event type name matching the Message Center event\n                  configuration.\n              email:\n                type: string\n                format: email\n                description: Recipient email address.\n              mobilePhone:\n                type: string\n\
  \                description: Recipient mobile phone number.\n              origin:\n                type: string\n                description: Origin identifier for tracking the event source.\n              wishedChannel:\n                type: integer\n                description: >-\n                  Preferred delivery channel. 0 = email, 1 = mobile (SMS),\n                  2 = phone, 3 = push notification.\n              externalId:\n                type: string\n                description: External identifier for deduplication.\n              ctx:\n                type: object\n                description: Context data for message personalization.\n                additionalProperties: true\n    EventMetadata:\n      type: object\n      description: Metadata about the event publication.\n      properties:\n        topic:\n          type: string\n          description: The event topic or channel.\n        schemaVersion:\n          type: string\n          description: Schema version\
  \ for the event payload.\n        publishDate:\n          type: string\n          format: date-time\n          description: Timestamp when the event was published.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/adobe-campaign/refs/heads/main/asyncapi/adobe-campaign-transactional-messaging-asyncapi-original.yml
spec_file: asyncapi/adobe-campaign-transactional-messaging-asyncapi-original.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/adobe-campaign/refs/heads/main/asyncapi/adobe-campaign-transactional-messaging-asyncapi-original.yml
tags:
- Campaign Management
- Customer Experience
- Email Marketing
- Marketing Automation
- Multi-Channel Marketing
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
