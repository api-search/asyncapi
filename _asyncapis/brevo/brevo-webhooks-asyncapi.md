---
channels:
- description: Transactional email event notifications including delivery status, opens, clicks, bounces, spam reports, and unsubscribes.
  name: /transactional-email-events
  operation: publish
  operation_id: receiveTransactionalEmailEvent
  summary: Receive transactional email event
- description: Marketing campaign event notifications including delivery, opens, clicks, bounces, spam reports, unsubscribes, and contact list changes.
  name: /marketing-email-events
  operation: publish
  operation_id: receiveMarketingEmailEvent
  summary: Receive marketing email event
- description: Transactional SMS event notifications including delivery status, bounces, and subscriber changes.
  name: /transactional-sms-events
  operation: publish
  operation_id: receiveTransactionalSmsEvent
  summary: Receive transactional SMS event
- description: Inbound email processing event notifications when incoming emails are received and processed.
  name: /inbound-email-events
  operation: publish
  operation_id: receiveInboundEmailEvent
  summary: Receive inbound email processed event
- description: Conversations event notifications for chat messages and visitor interactions.
  name: /conversations-events
  operation: publish
  operation_id: receiveConversationsEvent
  summary: Receive conversations event
description: Brevo delivers real-time event notifications via webhooks for transactional emails, marketing campaigns, transactional SMS, and conversations. When configured, Brevo sends HTTP POST requests to your specified endpoint URL with event payloads describing delivery status changes, recipient interactions, and contact list updates.
layout: asyncapi
messages:
- description: ''
  name: EmailDeliveredEvent
  summary: Fired when a transactional email is successfully delivered to the recipient's mail server.
  title: Email Delivered
- description: ''
  name: EmailOpenedEvent
  summary: Fired when a recipient opens a transactional email.
  title: Email Opened
- description: ''
  name: EmailClickedEvent
  summary: Fired when a recipient clicks a link in a transactional email.
  title: Email Link Clicked
- description: ''
  name: EmailHardBounceEvent
  summary: Fired when a transactional email permanently bounces due to an invalid or non-existent email address.
  title: Email Hard Bounce
- description: ''
  name: EmailSoftBounceEvent
  summary: Fired when a transactional email temporarily bounces due to a full mailbox or temporary server issue.
  title: Email Soft Bounce
- description: ''
  name: EmailSpamEvent
  summary: Fired when a recipient marks a transactional email as spam.
  title: Email Marked as Spam
- description: ''
  name: EmailBlockedEvent
  summary: Fired when a transactional email is blocked from sending.
  title: Email Blocked
- description: ''
  name: EmailInvalidEvent
  summary: Fired when a transactional email is sent to an invalid email address.
  title: Invalid Email
- description: ''
  name: EmailDeferredEvent
  summary: Fired when delivery of a transactional email is temporarily deferred by the receiving mail server.
  title: Email Deferred
- description: ''
  name: EmailUnsubscribedEvent
  summary: Fired when a recipient unsubscribes from transactional emails.
  title: Email Unsubscribed
- description: ''
  name: MarketingDeliveredEvent
  summary: Fired when a marketing campaign email is successfully delivered.
  title: Marketing Email Delivered
- description: ''
  name: MarketingOpenedEvent
  summary: Fired when a recipient opens a marketing campaign email.
  title: Marketing Email Opened
- description: ''
  name: MarketingClickedEvent
  summary: Fired when a recipient clicks a link in a marketing campaign email.
  title: Marketing Email Link Clicked
- description: ''
  name: MarketingHardBounceEvent
  summary: Fired when a marketing campaign email permanently bounces.
  title: Marketing Email Hard Bounce
- description: ''
  name: MarketingSoftBounceEvent
  summary: Fired when a marketing campaign email temporarily bounces.
  title: Marketing Email Soft Bounce
- description: ''
  name: MarketingSpamEvent
  summary: Fired when a recipient marks a marketing campaign email as spam.
  title: Marketing Email Marked as Spam
- description: ''
  name: MarketingUnsubscribedEvent
  summary: Fired when a recipient unsubscribes from marketing emails.
  title: Marketing Email Unsubscribed
- description: ''
  name: MarketingListAdditionEvent
  summary: Fired when a contact is added to a marketing list.
  title: Contact Added to List
- description: ''
  name: ContactDeletedEvent
  summary: Fired when a contact is deleted from the account.
  title: Contact Deleted
- description: ''
  name: ContactUpdatedEvent
  summary: Fired when a contact's attributes are updated.
  title: Contact Updated
- description: ''
  name: SmsSentEvent
  summary: Fired when a transactional SMS is sent to the carrier.
  title: SMS Sent
- description: ''
  name: SmsDeliveredEvent
  summary: Fired when a transactional SMS is delivered to the recipient.
  title: SMS Delivered
- description: ''
  name: SmsSoftBounceEvent
  summary: Fired when a transactional SMS temporarily bounces.
  title: SMS Soft Bounce
- description: ''
  name: SmsHardBounceEvent
  summary: Fired when a transactional SMS permanently bounces.
  title: SMS Hard Bounce
- description: ''
  name: SmsUnsubscribeEvent
  summary: Fired when a recipient unsubscribes from SMS messages.
  title: SMS Unsubscribe
- description: ''
  name: InboundEmailProcessedEvent
  summary: Fired when an inbound email is received and processed by Brevo.
  title: Inbound Email Processed
- description: ''
  name: ConversationMessageEvent
  summary: Fired when a new message is sent in a conversation by a visitor, agent, or bot.
  title: Conversation Message Received
- description: ''
  name: ConversationPushEvent
  summary: Fired when a pushed or automated message is delivered to a visitor in the chat widget.
  title: Conversation Push Notification
name: Brevo Webhook Events
provider_name: brevo
provider_slug: brevo
servers:
- description: Your application's webhook endpoint that receives event notifications from Brevo via HTTP POST requests.
  name: webhookEndpoint
  protocol: https
  url: '{webhookUrl}'
slug: brevo-webhooks-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Brevo Webhook Events\n  description: >-\n    Brevo delivers real-time event notifications via webhooks for\n    transactional emails, marketing campaigns, transactional SMS, and\n    conversations. When configured, Brevo sends HTTP POST requests to\n    your specified endpoint URL with event payloads describing delivery\n    status changes, recipient interactions, and contact list updates.\n  version: '3.0'\n  contact:\n    name: Brevo Support\n    url: https://help.brevo.com\nservers:\n  webhookEndpoint:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your application's webhook endpoint that receives event\n      notifications from Brevo via HTTP POST requests.\n    variables:\n      webhookUrl:\n        description: >-\n          The HTTPS URL configured in your Brevo webhook subscription.\n    security:\n      - apiKeyAuth: []\nchannels:\n  /transactional-email-events:\n    description: >-\n      Transactional email\
  \ event notifications including delivery status,\n      opens, clicks, bounces, spam reports, and unsubscribes.\n    publish:\n      operationId: receiveTransactionalEmailEvent\n      summary: Receive transactional email event\n      description: >-\n        Brevo sends a POST request to your webhook URL when a\n        transactional email event occurs such as delivery, open,\n        click, bounce, spam report, or unsubscribe.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/EmailDeliveredEvent'\n          - $ref: '#/components/messages/EmailOpenedEvent'\n          - $ref: '#/components/messages/EmailClickedEvent'\n          - $ref: '#/components/messages/EmailHardBounceEvent'\n          - $ref: '#/components/messages/EmailSoftBounceEvent'\n          - $ref: '#/components/messages/EmailSpamEvent'\n          - $ref: '#/components/messages/EmailBlockedEvent'\n          - $ref: '#/components/messages/EmailInvalidEvent'\n          - $ref: '#/components/messages/EmailDeferredEvent'\n\
  \          - $ref: '#/components/messages/EmailUnsubscribedEvent'\n  /marketing-email-events:\n    description: >-\n      Marketing campaign event notifications including delivery,\n      opens, clicks, bounces, spam reports, unsubscribes, and\n      contact list changes.\n    publish:\n      operationId: receiveMarketingEmailEvent\n      summary: Receive marketing email event\n      description: >-\n        Brevo sends a POST request to your webhook URL when a\n        marketing campaign event occurs such as delivery, unsubscribe,\n        or contact list addition.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/MarketingDeliveredEvent'\n          - $ref: '#/components/messages/MarketingOpenedEvent'\n          - $ref: '#/components/messages/MarketingClickedEvent'\n          - $ref: '#/components/messages/MarketingHardBounceEvent'\n          - $ref: '#/components/messages/MarketingSoftBounceEvent'\n          - $ref: '#/components/messages/MarketingSpamEvent'\n\
  \          - $ref: '#/components/messages/MarketingUnsubscribedEvent'\n          - $ref: '#/components/messages/MarketingListAdditionEvent'\n          - $ref: '#/components/messages/ContactDeletedEvent'\n          - $ref: '#/components/messages/ContactUpdatedEvent'\n  /transactional-sms-events:\n    description: >-\n      Transactional SMS event notifications including delivery status,\n      bounces, and subscriber changes.\n    publish:\n      operationId: receiveTransactionalSmsEvent\n      summary: Receive transactional SMS event\n      description: >-\n        Brevo sends a POST request to your webhook URL when a\n        transactional SMS event occurs such as delivery, bounce,\n        or unsubscribe.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/SmsSentEvent'\n          - $ref: '#/components/messages/SmsDeliveredEvent'\n          - $ref: '#/components/messages/SmsSoftBounceEvent'\n          - $ref: '#/components/messages/SmsHardBounceEvent'\n        \
  \  - $ref: '#/components/messages/SmsUnsubscribeEvent'\n  /inbound-email-events:\n    description: >-\n      Inbound email processing event notifications when incoming\n      emails are received and processed.\n    publish:\n      operationId: receiveInboundEmailEvent\n      summary: Receive inbound email processed event\n      description: >-\n        Brevo sends a POST request to your webhook URL when an\n        inbound email is received and processed.\n      message:\n        $ref: '#/components/messages/InboundEmailProcessedEvent'\n  /conversations-events:\n    description: >-\n      Conversations event notifications for chat messages and\n      visitor interactions.\n    publish:\n      operationId: receiveConversationsEvent\n      summary: Receive conversations event\n      description: >-\n        Brevo sends a POST request to your webhook URL when a\n        conversation event occurs such as a new message from a\n        visitor or agent.\n      message:\n        oneOf:\n    \
  \      - $ref: '#/components/messages/ConversationMessageEvent'\n          - $ref: '#/components/messages/ConversationPushEvent'\ncomponents:\n  securitySchemes:\n    apiKeyAuth:\n      type: httpApiKey\n      in: header\n      name: api-key\n      description: >-\n        Brevo API key used to authenticate webhook configurations.\n  messages:\n    EmailDeliveredEvent:\n      name: emailDelivered\n      title: Email Delivered\n      summary: >-\n        Fired when a transactional email is successfully delivered\n        to the recipient's mail server.\n      payload:\n        $ref: '#/components/schemas/TransactionalEmailEvent'\n    EmailOpenedEvent:\n      name: emailOpened\n      title: Email Opened\n      summary: >-\n        Fired when a recipient opens a transactional email.\n      payload:\n        $ref: '#/components/schemas/TransactionalEmailEvent'\n    EmailClickedEvent:\n      name: emailClicked\n      title: Email Link Clicked\n      summary: >-\n        Fired when a recipient\
  \ clicks a link in a transactional email.\n      payload:\n        $ref: '#/components/schemas/TransactionalEmailClickEvent'\n    EmailHardBounceEvent:\n      name: emailHardBounce\n      title: Email Hard Bounce\n      summary: >-\n        Fired when a transactional email permanently bounces due to\n        an invalid or non-existent email address.\n      payload:\n        $ref: '#/components/schemas/TransactionalEmailEvent'\n    EmailSoftBounceEvent:\n      name: emailSoftBounce\n      title: Email Soft Bounce\n      summary: >-\n        Fired when a transactional email temporarily bounces due to\n        a full mailbox or temporary server issue.\n      payload:\n        $ref: '#/components/schemas/TransactionalEmailEvent'\n    EmailSpamEvent:\n      name: emailSpam\n      title: Email Marked as Spam\n      summary: >-\n        Fired when a recipient marks a transactional email as spam.\n      payload:\n        $ref: '#/components/schemas/TransactionalEmailEvent'\n    EmailBlockedEvent:\n\
  \      name: emailBlocked\n      title: Email Blocked\n      summary: >-\n        Fired when a transactional email is blocked from sending.\n      payload:\n        $ref: '#/components/schemas/TransactionalEmailEvent'\n    EmailInvalidEvent:\n      name: emailInvalid\n      title: Invalid Email\n      summary: >-\n        Fired when a transactional email is sent to an invalid\n        email address.\n      payload:\n        $ref: '#/components/schemas/TransactionalEmailEvent'\n    EmailDeferredEvent:\n      name: emailDeferred\n      title: Email Deferred\n      summary: >-\n        Fired when delivery of a transactional email is temporarily\n        deferred by the receiving mail server.\n      payload:\n        $ref: '#/components/schemas/TransactionalEmailEvent'\n    EmailUnsubscribedEvent:\n      name: emailUnsubscribed\n      title: Email Unsubscribed\n      summary: >-\n        Fired when a recipient unsubscribes from transactional emails.\n      payload:\n        $ref: '#/components/schemas/TransactionalEmailEvent'\n\
  \    MarketingDeliveredEvent:\n      name: marketingDelivered\n      title: Marketing Email Delivered\n      summary: >-\n        Fired when a marketing campaign email is successfully delivered.\n      payload:\n        $ref: '#/components/schemas/MarketingEmailEvent'\n    MarketingOpenedEvent:\n      name: marketingOpened\n      title: Marketing Email Opened\n      summary: >-\n        Fired when a recipient opens a marketing campaign email.\n      payload:\n        $ref: '#/components/schemas/MarketingEmailEvent'\n    MarketingClickedEvent:\n      name: marketingClicked\n      title: Marketing Email Link Clicked\n      summary: >-\n        Fired when a recipient clicks a link in a marketing campaign email.\n      payload:\n        $ref: '#/components/schemas/MarketingEmailClickEvent'\n    MarketingHardBounceEvent:\n      name: marketingHardBounce\n      title: Marketing Email Hard Bounce\n      summary: >-\n        Fired when a marketing campaign email permanently bounces.\n      payload:\n\
  \        $ref: '#/components/schemas/MarketingEmailEvent'\n    MarketingSoftBounceEvent:\n      name: marketingSoftBounce\n      title: Marketing Email Soft Bounce\n      summary: >-\n        Fired when a marketing campaign email temporarily bounces.\n      payload:\n        $ref: '#/components/schemas/MarketingEmailEvent'\n    MarketingSpamEvent:\n      name: marketingSpam\n      title: Marketing Email Marked as Spam\n      summary: >-\n        Fired when a recipient marks a marketing campaign email as spam.\n      payload:\n        $ref: '#/components/schemas/MarketingEmailEvent'\n    MarketingUnsubscribedEvent:\n      name: marketingUnsubscribed\n      title: Marketing Email Unsubscribed\n      summary: >-\n        Fired when a recipient unsubscribes from marketing emails.\n      payload:\n        $ref: '#/components/schemas/MarketingEmailEvent'\n    MarketingListAdditionEvent:\n      name: marketingListAddition\n      title: Contact Added to List\n      summary: >-\n        Fired when\
  \ a contact is added to a marketing list.\n      payload:\n        $ref: '#/components/schemas/ContactListEvent'\n    ContactDeletedEvent:\n      name: contactDeleted\n      title: Contact Deleted\n      summary: >-\n        Fired when a contact is deleted from the account.\n      payload:\n        $ref: '#/components/schemas/ContactEvent'\n    ContactUpdatedEvent:\n      name: contactUpdated\n      title: Contact Updated\n      summary: >-\n        Fired when a contact's attributes are updated.\n      payload:\n        $ref: '#/components/schemas/ContactEvent'\n    SmsSentEvent:\n      name: smsSent\n      title: SMS Sent\n      summary: >-\n        Fired when a transactional SMS is sent to the carrier.\n      payload:\n        $ref: '#/components/schemas/SmsEvent'\n    SmsDeliveredEvent:\n      name: smsDelivered\n      title: SMS Delivered\n      summary: >-\n        Fired when a transactional SMS is delivered to the recipient.\n      payload:\n        $ref: '#/components/schemas/SmsEvent'\n\
  \    SmsSoftBounceEvent:\n      name: smsSoftBounce\n      title: SMS Soft Bounce\n      summary: >-\n        Fired when a transactional SMS temporarily bounces.\n      payload:\n        $ref: '#/components/schemas/SmsEvent'\n    SmsHardBounceEvent:\n      name: smsHardBounce\n      title: SMS Hard Bounce\n      summary: >-\n        Fired when a transactional SMS permanently bounces.\n      payload:\n        $ref: '#/components/schemas/SmsEvent'\n    SmsUnsubscribeEvent:\n      name: smsUnsubscribe\n      title: SMS Unsubscribe\n      summary: >-\n        Fired when a recipient unsubscribes from SMS messages.\n      payload:\n        $ref: '#/components/schemas/SmsEvent'\n    InboundEmailProcessedEvent:\n      name: inboundEmailProcessed\n      title: Inbound Email Processed\n      summary: >-\n        Fired when an inbound email is received and processed by Brevo.\n      payload:\n        $ref: '#/components/schemas/InboundEmailEvent'\n    ConversationMessageEvent:\n      name: conversationMessage\n\
  \      title: Conversation Message Received\n      summary: >-\n        Fired when a new message is sent in a conversation by a\n        visitor, agent, or bot.\n      payload:\n        $ref: '#/components/schemas/ConversationEvent'\n    ConversationPushEvent:\n      name: conversationPush\n      title: Conversation Push Notification\n      summary: >-\n        Fired when a pushed or automated message is delivered to a\n        visitor in the chat widget.\n      payload:\n        $ref: '#/components/schemas/ConversationEvent'\n  schemas:\n    TransactionalEmailEvent:\n      type: object\n      properties:\n        event:\n          type: string\n          description: >-\n            Type of transactional email event.\n          enum:\n            - sent\n            - request\n            - delivered\n            - hardBounce\n            - softBounce\n            - blocked\n            - spam\n            - invalid\n            - deferred\n            - opened\n            - uniqueOpened\n\
  \            - unsubscribed\n        email:\n          type: string\n          format: email\n          description: >-\n            Recipient email address.\n        id:\n          type: integer\n          format: int64\n          description: >-\n            Internal event identifier.\n        date:\n          type: string\n          format: date-time\n          description: >-\n            UTC date-time when the event occurred.\n        messageId:\n          type: string\n          description: >-\n            Unique identifier of the email message.\n        subject:\n          type: string\n          description: >-\n            Subject line of the email.\n        tag:\n          type: string\n          description: >-\n            Tag assigned to the email for categorization.\n        sendingIp:\n          type: string\n          description: >-\n            IP address used to send the email.\n        ts:\n          type: integer\n          format: int64\n          description: >-\n\
  \            Unix timestamp in seconds when the event occurred.\n        ts_epoch:\n          type: integer\n          format: int64\n          description: >-\n            Unix timestamp in milliseconds when the event occurred.\n        reason:\n          type: string\n          description: >-\n            Reason for the event if applicable, such as bounce details.\n        templateId:\n          type: integer\n          format: int64\n          description: >-\n            Template ID used for the email if applicable.\n    TransactionalEmailClickEvent:\n      allOf:\n        - $ref: '#/components/schemas/TransactionalEmailEvent'\n        - type: object\n          properties:\n            link:\n              type: string\n              format: uri\n              description: >-\n                URL of the link that was clicked.\n    MarketingEmailEvent:\n      type: object\n      properties:\n        event:\n          type: string\n          description: >-\n            Type of marketing\
  \ email event.\n          enum:\n            - delivered\n            - opened\n            - clicked\n            - hardBounce\n            - softBounce\n            - spam\n            - unsubscribed\n            - proxyOpen\n        email:\n          type: string\n          format: email\n          description: >-\n            Recipient email address.\n        id:\n          type: integer\n          format: int64\n          description: >-\n            Internal event identifier.\n        date:\n          type: string\n          format: date-time\n          description: >-\n            UTC date-time when the event occurred.\n        messageId:\n          type: string\n          description: >-\n            Unique identifier of the campaign message.\n        campaignId:\n          type: integer\n          format: int64\n          description: >-\n            ID of the email campaign.\n        ts:\n          type: integer\n          format: int64\n          description: >-\n          \
  \  Unix timestamp in seconds when the event occurred.\n        ts_epoch:\n          type: integer\n          format: int64\n          description: >-\n            Unix timestamp in milliseconds when the event occurred.\n    MarketingEmailClickEvent:\n      allOf:\n        - $ref: '#/components/schemas/MarketingEmailEvent'\n        - type: object\n          properties:\n            link:\n              type: string\n              format: uri\n              description: >-\n                URL of the link that was clicked.\n    ContactListEvent:\n      type: object\n      properties:\n        event:\n          type: string\n          description: >-\n            Type of contact list event.\n          enum:\n            - listAddition\n        email:\n          type: string\n          format: email\n          description: >-\n            Email address of the contact added to the list.\n        id:\n          type: integer\n          format: int64\n          description: >-\n            Internal\
  \ event identifier.\n        date:\n          type: string\n          format: date-time\n          description: >-\n            UTC date-time when the event occurred.\n        listId:\n          type: integer\n          format: int64\n          description: >-\n            ID of the list the contact was added to.\n        ts:\n          type: integer\n          format: int64\n          description: >-\n            Unix timestamp in seconds when the event occurred.\n    ContactEvent:\n      type: object\n      properties:\n        event:\n          type: string\n          description: >-\n            Type of contact event.\n          enum:\n            - contactDeleted\n            - contactUpdated\n        email:\n          type: string\n          format: email\n          description: >-\n            Email address of the affected contact.\n        id:\n          type: integer\n          format: int64\n          description: >-\n            Internal event identifier.\n        date:\n  \
  \        type: string\n          format: date-time\n          description: >-\n            UTC date-time when the event occurred.\n        ts:\n          type: integer\n          format: int64\n          description: >-\n            Unix timestamp in seconds when the event occurred.\n    SmsEvent:\n      type: object\n      properties:\n        event:\n          type: string\n          description: >-\n            Type of SMS event.\n          enum:\n            - sent\n            - accepted\n            - delivered\n            - replied\n            - softBounce\n            - hardBounce\n            - subscribe\n            - unsubscribe\n            - skip\n            - rejected\n        phoneNumber:\n          type: string\n          description: >-\n            Recipient phone number in international format.\n        date:\n          type: string\n          format: date-time\n          description: >-\n            UTC date-time when the event occurred.\n        messageId:\n   \
  \       type: string\n          description: >-\n            Unique identifier of the SMS message.\n        tag:\n          type: string\n          description: >-\n            Tag assigned to the SMS.\n        reason:\n          type: string\n          description: >-\n            Reason for the event if applicable.\n        ts:\n          type: integer\n          format: int64\n          description: >-\n            Unix timestamp in seconds when the event occurred.\n    InboundEmailEvent:\n      type: object\n      properties:\n        event:\n          type: string\n          description: >-\n            Type of inbound email event.\n          enum:\n            - inboundEmailProcessed\n        sender:\n          type: string\n          format: email\n          description: >-\n            Email address of the inbound email sender.\n        recipient:\n          type: string\n          format: email\n          description: >-\n            Email address the inbound email was sent to.\n\
  \        subject:\n          type: string\n          description: >-\n            Subject line of the inbound email.\n        date:\n          type: string\n          format: date-time\n          description: >-\n            UTC date-time when the email was processed.\n        messageId:\n          type: string\n          description: >-\n            Unique identifier of the inbound email.\n        ts:\n          type: integer\n          format: int64\n          description: >-\n            Unix timestamp in seconds when the event occurred.\n    ConversationEvent:\n      type: object\n      properties:\n        event:\n          type: string\n          description: >-\n            Type of conversation event.\n          enum:\n            - message\n            - push\n        visitorId:\n          type: string\n          description: >-\n            Unique identifier of the visitor.\n        messageId:\n          type: string\n          description: >-\n            Unique identifier of\
  \ the message.\n        text:\n          type: string\n          description: >-\n            Text content of the message.\n        type:\n          type: string\n          description: >-\n            Type of message sender.\n          enum:\n            - agent\n            - visitor\n            - bot\n        agentId:\n          type: string\n          description: >-\n            Identifier of the agent if the message was sent by an agent.\n        date:\n          type: string\n          format: date-time\n          description: >-\n            UTC date-time when the event occurred.\n        ts:\n          type: integer\n          format: int64\n          description: >-\n            Unix timestamp in seconds when the event occurred.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/brevo/refs/heads/main/asyncapi/brevo-webhooks-asyncapi.yml
spec_file: asyncapi/brevo-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/brevo/refs/heads/main/asyncapi/brevo-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '3.0'
---
