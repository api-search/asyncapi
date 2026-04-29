---
api_specs:
- filename: customer-io-track-api-openapi.yml
  format: yaml
  label: Customer.io Track API
  slug: track-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/customer-io/refs/heads/main/openapi/customer-io-track-api-openapi.yml
- filename: customer-io-app-api-openapi.yml
  format: yaml
  label: Customer.io App API
  slug: app-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/customer-io/refs/heads/main/openapi/customer-io-app-api-openapi.yml
- filename: customer-io-pipelines-api-openapi.yml
  format: yaml
  label: Customer.io Pipelines API
  slug: pipelines-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/customer-io/refs/heads/main/openapi/customer-io-pipelines-api-openapi.yml
channels:
- description: The webhook endpoint that receives real-time message activity events from Customer.io. Each event is delivered as an HTTP POST with a JSON payload. Events include a unique delivery ID in the X-CIO-Delivery-ID header for deduplication and tracking.
  name: /webhook
  operation: publish
  operation_id: receiveReportingEvent
  summary: Receive a reporting webhook event
description: Customer.io Reporting Webhooks send real-time message activity events as JSON payloads via HTTP POST to a configured endpoint. These events include message sends, deliveries, opens, clicks, bounces, unsubscribes, and other engagement actions. Reporting webhooks are configured in Data and Integrations settings and can be filtered to receive specific event types. They are useful for analyzing message activity outside of Customer.io, syncing delivery data to external systems, and building real-time dashboards.
layout: asyncapi
messages:
- description: ''
  name: EmailSent
  summary: Triggered when an email message is sent to a recipient.
  title: Email Sent
- description: ''
  name: EmailDelivered
  summary: Triggered when an email is successfully delivered to the recipient mail server.
  title: Email Delivered
- description: ''
  name: EmailOpened
  summary: Triggered when a recipient opens an email message.
  title: Email Opened
- description: ''
  name: EmailClicked
  summary: Triggered when a recipient clicks a link in an email message.
  title: Email Clicked
- description: ''
  name: EmailBounced
  summary: Triggered when an email bounces due to a permanent or temporary delivery failure.
  title: Email Bounced
- description: ''
  name: EmailSpammed
  summary: Triggered when a recipient marks an email as spam.
  title: Email Marked as Spam
- description: ''
  name: EmailDropped
  summary: Triggered when an email is dropped and not sent, typically due to the recipient being suppressed or unsubscribed.
  title: Email Dropped
- description: ''
  name: Unsubscribed
  summary: Triggered when a recipient unsubscribes from messages.
  title: Unsubscribed
- description: ''
  name: EmailConverted
  summary: Triggered when a conversion goal is met after sending an email.
  title: Email Converted
- description: ''
  name: EmailFailed
  summary: Triggered when an email fails to send due to a system error.
  title: Email Failed
- description: ''
  name: PushSent
  summary: Triggered when a push notification is sent to a device.
  title: Push Notification Sent
- description: ''
  name: PushOpened
  summary: Triggered when a recipient opens a push notification.
  title: Push Notification Opened
- description: ''
  name: PushBounced
  summary: Triggered when a push notification fails to deliver to the device.
  title: Push Notification Bounced
- description: ''
  name: SmsSent
  summary: Triggered when an SMS message is sent.
  title: SMS Sent
- description: ''
  name: SmsDelivered
  summary: Triggered when an SMS message is successfully delivered.
  title: SMS Delivered
- description: ''
  name: SmsFailed
  summary: Triggered when an SMS message fails to send.
  title: SMS Failed
- description: ''
  name: SmsBounced
  summary: Triggered when an SMS message bounces.
  title: SMS Bounced
name: Customer.io Reporting Webhooks
provider_name: Customer.io
provider_slug: customer-io
servers:
- description: Your webhook endpoint that receives reporting events from Customer.io. Configure this URL in your Customer.io workspace under Data and Integrations.
  name: userEndpoint
  protocol: https
  url: '{webhookUrl}'
slug: customer-io-reporting-webhooks-asyncapi
source_filename: customer-io-reporting-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Customer.io Reporting Webhooks\n  description: >-\n    Customer.io Reporting Webhooks send real-time message activity events as\n    JSON payloads via HTTP POST to a configured endpoint. These events include\n    message sends, deliveries, opens, clicks, bounces, unsubscribes, and other\n    engagement actions. Reporting webhooks are configured in Data and\n    Integrations settings and can be filtered to receive specific event types.\n    They are useful for analyzing message activity outside of Customer.io,\n    syncing delivery data to external systems, and building real-time\n    dashboards.\n  version: '1.0.0'\n  contact:\n    name: Customer.io Support\n    url: https://customer.io/contact\n  license:\n    name: Proprietary\n    url: https://customer.io/legal/terms-of-service\nservers:\n  userEndpoint:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your webhook endpoint that receives reporting events from Customer.io.\n\
  \      Configure this URL in your Customer.io workspace under Data and\n      Integrations.\n    variables:\n      webhookUrl:\n        description: >-\n          The URL of your webhook endpoint.\n    security:\n      - hmacSignature: []\nchannels:\n  /webhook:\n    description: >-\n      The webhook endpoint that receives real-time message activity events\n      from Customer.io. Each event is delivered as an HTTP POST with a JSON\n      payload. Events include a unique delivery ID in the X-CIO-Delivery-ID\n      header for deduplication and tracking.\n    publish:\n      operationId: receiveReportingEvent\n      summary: Receive a reporting webhook event\n      description: >-\n        Customer.io sends reporting webhook events to your configured endpoint\n        when message activity occurs. Events are sent in real-time and include\n        details about the message, recipient, and action taken.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/EmailSent'\n\
  \          - $ref: '#/components/messages/EmailDelivered'\n          - $ref: '#/components/messages/EmailOpened'\n          - $ref: '#/components/messages/EmailClicked'\n          - $ref: '#/components/messages/EmailBounced'\n          - $ref: '#/components/messages/EmailSpammed'\n          - $ref: '#/components/messages/EmailDropped'\n          - $ref: '#/components/messages/Unsubscribed'\n          - $ref: '#/components/messages/EmailConverted'\n          - $ref: '#/components/messages/EmailFailed'\n          - $ref: '#/components/messages/PushSent'\n          - $ref: '#/components/messages/PushOpened'\n          - $ref: '#/components/messages/PushBounced'\n          - $ref: '#/components/messages/SmsSent'\n          - $ref: '#/components/messages/SmsDelivered'\n          - $ref: '#/components/messages/SmsFailed'\n          - $ref: '#/components/messages/SmsBounced'\ncomponents:\n  securitySchemes:\n    hmacSignature:\n      type: httpApiKey\n      name: X-CIO-Signature\n      in: header\n\
  \      description: >-\n        Customer.io signs webhook payloads using HMAC-SHA256 with your\n        webhook signing key. The signature is included in the\n        X-CIO-Signature header. Verify this signature to ensure the\n        webhook payload is authentic and has not been tampered with.\n  messages:\n    EmailSent:\n      name: email_sent\n      title: Email Sent\n      summary: >-\n        Triggered when an email message is sent to a recipient.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EmailEvent'\n    EmailDelivered:\n      name: email_delivered\n      title: Email Delivered\n      summary: >-\n        Triggered when an email is successfully delivered to the recipient\n        mail server.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EmailEvent'\n    EmailOpened:\n      name: email_opened\n      title: Email Opened\n      summary: >-\n        Triggered when a recipient opens an email\
  \ message.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EmailEvent'\n    EmailClicked:\n      name: email_clicked\n      title: Email Clicked\n      summary: >-\n        Triggered when a recipient clicks a link in an email message.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EmailClickEvent'\n    EmailBounced:\n      name: email_bounced\n      title: Email Bounced\n      summary: >-\n        Triggered when an email bounces due to a permanent or temporary\n        delivery failure.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EmailEvent'\n    EmailSpammed:\n      name: email_spammed\n      title: Email Marked as Spam\n      summary: >-\n        Triggered when a recipient marks an email as spam.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EmailEvent'\n    EmailDropped:\n      name: email_dropped\n      title:\
  \ Email Dropped\n      summary: >-\n        Triggered when an email is dropped and not sent, typically due to\n        the recipient being suppressed or unsubscribed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EmailEvent'\n    Unsubscribed:\n      name: unsubscribed\n      title: Unsubscribed\n      summary: >-\n        Triggered when a recipient unsubscribes from messages.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EmailEvent'\n    EmailConverted:\n      name: email_converted\n      title: Email Converted\n      summary: >-\n        Triggered when a conversion goal is met after sending an email.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EmailEvent'\n    EmailFailed:\n      name: email_failed\n      title: Email Failed\n      summary: >-\n        Triggered when an email fails to send due to a system error.\n      contentType: application/json\n \
  \     payload:\n        $ref: '#/components/schemas/EmailEvent'\n    PushSent:\n      name: push_sent\n      title: Push Notification Sent\n      summary: >-\n        Triggered when a push notification is sent to a device.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PushEvent'\n    PushOpened:\n      name: push_opened\n      title: Push Notification Opened\n      summary: >-\n        Triggered when a recipient opens a push notification.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PushEvent'\n    PushBounced:\n      name: push_bounced\n      title: Push Notification Bounced\n      summary: >-\n        Triggered when a push notification fails to deliver to the device.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PushEvent'\n    SmsSent:\n      name: sms_sent\n      title: SMS Sent\n      summary: >-\n        Triggered when an SMS message is sent.\n    \
  \  contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SmsEvent'\n    SmsDelivered:\n      name: sms_delivered\n      title: SMS Delivered\n      summary: >-\n        Triggered when an SMS message is successfully delivered.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SmsEvent'\n    SmsFailed:\n      name: sms_failed\n      title: SMS Failed\n      summary: >-\n        Triggered when an SMS message fails to send.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SmsEvent'\n    SmsBounced:\n      name: sms_bounced\n      title: SMS Bounced\n      summary: >-\n        Triggered when an SMS message bounces.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SmsEvent'\n  schemas:\n    EmailEvent:\n      type: object\n      description: >-\n        An email reporting webhook event payload.\n      required:\n        - event_id\n        - metric\n\
  \        - timestamp\n      properties:\n        event_id:\n          type: string\n          description: >-\n            A unique identifier for this event.\n        metric:\n          type: string\n          description: >-\n            The type of event.\n          enum:\n            - sent\n            - delivered\n            - opened\n            - clicked\n            - bounced\n            - spammed\n            - dropped\n            - unsubscribed\n            - converted\n            - failed\n        timestamp:\n          type: integer\n          description: >-\n            UNIX timestamp of when the event occurred.\n        data:\n          type: object\n          description: >-\n            Event data with details about the message and recipient.\n          properties:\n            customer_id:\n              type: string\n              description: >-\n                The recipient customer identifier.\n            email_address:\n              type: string\n        \
  \      format: email\n              description: >-\n                The recipient email address.\n            delivery_id:\n              type: string\n              description: >-\n                The unique delivery identifier for the message.\n            action_id:\n              type: integer\n              description: >-\n                The campaign action identifier that sent the message.\n            campaign_id:\n              type: integer\n              description: >-\n                The campaign identifier.\n            newsletter_id:\n              type: integer\n              description: >-\n                The newsletter identifier if applicable.\n            broadcast_id:\n              type: integer\n              description: >-\n                The broadcast identifier if applicable.\n            subject:\n              type: string\n              description: >-\n                The email subject line.\n            template_id:\n              type: integer\n\
  \              description: >-\n                The message template identifier.\n            content_id:\n              type: integer\n              description: >-\n                The content variant identifier.\n    EmailClickEvent:\n      type: object\n      description: >-\n        An email click reporting webhook event payload with link details.\n      required:\n        - event_id\n        - metric\n        - timestamp\n      properties:\n        event_id:\n          type: string\n          description: >-\n            A unique identifier for this event.\n        metric:\n          type: string\n          description: >-\n            The event type.\n          const: clicked\n        timestamp:\n          type: integer\n          description: >-\n            UNIX timestamp of when the event occurred.\n        data:\n          type: object\n          description: >-\n            Event data with details about the message, recipient, and link.\n          properties:\n            customer_id:\n\
  \              type: string\n              description: >-\n                The recipient customer identifier.\n            email_address:\n              type: string\n              format: email\n              description: >-\n                The recipient email address.\n            delivery_id:\n              type: string\n              description: >-\n                The unique delivery identifier.\n            action_id:\n              type: integer\n              description: >-\n                The campaign action identifier.\n            campaign_id:\n              type: integer\n              description: >-\n                The campaign identifier.\n            href:\n              type: string\n              format: uri\n              description: >-\n                The URL that was clicked.\n            link_id:\n              type: integer\n              description: >-\n                The link identifier within the message.\n            subject:\n              type: string\n\
  \              description: >-\n                The email subject line.\n    PushEvent:\n      type: object\n      description: >-\n        A push notification reporting webhook event payload.\n      required:\n        - event_id\n        - metric\n        - timestamp\n      properties:\n        event_id:\n          type: string\n          description: >-\n            A unique identifier for this event.\n        metric:\n          type: string\n          description: >-\n            The event type.\n          enum:\n            - sent\n            - opened\n            - bounced\n        timestamp:\n          type: integer\n          description: >-\n            UNIX timestamp of when the event occurred.\n        data:\n          type: object\n          description: >-\n            Event data with details about the notification and recipient.\n          properties:\n            customer_id:\n              type: string\n              description: >-\n                The recipient customer\
  \ identifier.\n            delivery_id:\n              type: string\n              description: >-\n                The unique delivery identifier.\n            action_id:\n              type: integer\n              description: >-\n                The campaign action identifier.\n            campaign_id:\n              type: integer\n              description: >-\n                The campaign identifier.\n            device_id:\n              type: string\n              description: >-\n                The device identifier that received the notification.\n            platform:\n              type: string\n              description: >-\n                The device platform.\n              enum:\n                - ios\n                - android\n    SmsEvent:\n      type: object\n      description: >-\n        An SMS reporting webhook event payload.\n      required:\n        - event_id\n        - metric\n        - timestamp\n      properties:\n        event_id:\n          type: string\n\
  \          description: >-\n            A unique identifier for this event.\n        metric:\n          type: string\n          description: >-\n            The event type.\n          enum:\n            - sent\n            - delivered\n            - failed\n            - bounced\n        timestamp:\n          type: integer\n          description: >-\n            UNIX timestamp of when the event occurred.\n        data:\n          type: object\n          description: >-\n            Event data with details about the SMS and recipient.\n          properties:\n            customer_id:\n              type: string\n              description: >-\n                The recipient customer identifier.\n            delivery_id:\n              type: string\n              description: >-\n                The unique delivery identifier.\n            action_id:\n              type: integer\n              description: >-\n                The campaign action identifier.\n            campaign_id:\n     \
  \         type: integer\n              description: >-\n                The campaign identifier.\n            from_phone:\n              type: string\n              description: >-\n                The sender phone number.\n            to_phone:\n              type: string\n              description: >-\n                The recipient phone number.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/customer-io/refs/heads/main/asyncapi/customer-io-reporting-webhooks-asyncapi.yml
spec_file: asyncapi/customer-io-reporting-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/customer-io/refs/heads/main/asyncapi/customer-io-reporting-webhooks-asyncapi.yml
tags:
- Behavioral Data
- Broadcasts
- Campaigns
- CDP
- Customer Data
- Customer Data Platform
- Data Ingestion
- Email
- Event Tracking
- Marketing Automation
- Messaging
- Push Notifications
- Segments
- SMS
- Transactional Email
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
