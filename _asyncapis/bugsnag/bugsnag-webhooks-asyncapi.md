---
channels:
- description: Receives Bugsnag event notifications. The webhook sends a JSON payload via HTTP POST when a configured trigger condition is met. Supported triggers include new errors, frequent errors, error milestones, every error occurrence, and auto-reopened errors.
  name: /webhook
  operation: publish
  operation_id: receiveWebhookNotification
  summary: Receive a Bugsnag webhook notification
description: Bugsnag webhooks deliver real-time notifications about error events to a configured callback URL via HTTP POST. The webhook integration sends JSON payloads containing information about the triggering event, the error, the project, and the account. Webhooks can be configured per project in the Bugsnag dashboard under Project Settings, Data Forwarding, and support filtering by notification trigger type.
layout: asyncapi
messages:
- description: Triggered when Bugsnag detects the first occurrence of a new error in a specific release stage. This notification helps teams respond quickly to newly introduced bugs.
  name: NewErrorNotification
  summary: Sent when the first event of an error is received for a release stage.
  title: New Error Notification
- description: Triggered when an error receives a configured number of events or impacts a configured number of users within a specified time window. This notification identifies errors that are rapidly affecting users.
  name: FrequentErrorNotification
  summary: Sent when an error occurs frequently within a time window.
  title: Frequent Error Notification
- description: Triggered when the total number of events for an error reaches a milestone such as 10, 100, 1000, or 10000 occurrences. This notification highlights errors that continue to accumulate events.
  name: ErrorMilestoneNotification
  summary: Sent when an error reaches an event count milestone.
  title: Error Milestone Notification
- description: Triggered on every single error event that matches the configured filters. Use with caution as this can generate a high volume of webhook requests for frequently occurring errors.
  name: EveryErrorNotification
  summary: Sent every time an error event occurs.
  title: Every Error Notification
- description: Triggered when an error that was previously marked as fixed or snoozed receives a new event that causes it to be automatically reopened. This indicates a regression in the application.
  name: ErrorReopenedNotification
  summary: Sent when a fixed or snoozed error is automatically reopened.
  title: Error Reopened Notification
name: Bugsnag Webhook Events
provider_name: bugsnag
provider_slug: bugsnag
servers:
- description: The customer-configured webhook callback URL that receives Bugsnag event notifications via HTTP POST.
  name: customerEndpoint
  protocol: https
  url: '{webhookUrl}'
slug: bugsnag-webhooks-asyncapi
spec_file: asyncapi/bugsnag-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/bugsnag/refs/heads/main/asyncapi/bugsnag-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
