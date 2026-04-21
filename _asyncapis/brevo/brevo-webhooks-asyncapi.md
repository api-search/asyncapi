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
spec_file: asyncapi/brevo-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/brevo/refs/heads/main/asyncapi/brevo-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '3.0'
---
