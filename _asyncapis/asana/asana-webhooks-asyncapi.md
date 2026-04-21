---
channels:
- description: Channel for receiving Asana webhook events. Events are delivered as HTTP POST requests to the target URL configured when the webhook was created. Events bubble up from child resources (e.g., subscribing to a project will include events for tasks within that project).
  name: /webhooks/events
  operation: subscribe
  operation_id: receiveWebhookEvents
  summary: Receive webhook events
description: The Asana Webhooks Events API delivers real-time event notifications to your application when changes occur on Asana resources. Webhooks use HTTP POST to deliver events to a target URL you configure. Events are delivered within a minute on average using an at-most-once delivery system. Establishing a webhook requires a two-part handshake process. When a webhook is created, Asana sends a test POST to the target URL with an X-Hook-Secret header. The target must respond with a 200 OK or 204 No Content and echo back the X-Hook-Secret header to confirm the subscription. Subsequent event deliveries include an X-Hook-Signature header containing an HMAC-SHA256 signature of the request body using the X-Hook-Secret as the key, which can be used to verify event authenticity.
layout: asyncapi
messages:
- description: ''
  name: WebhookHandshake
  summary: Initial handshake request sent by Asana when a webhook is created. The target must respond with a 200 OK and echo back the X-Hook-Secret.
  title: Webhook Confirmation Handshake
- description: ''
  name: WebhookEvent
  summary: An event delivery containing one or more change events on Asana resources.
  title: Webhook Event Delivery
name: Asana Webhooks Events API
provider_name: Asana
provider_slug: asana
servers:
- description: Asana sends webhook events via HTTP POST to your configured target URL. You configure the target URL when establishing a webhook via the REST API.
  name: production
  protocol: http
  url: https://app.asana.com/api/1.0
slug: asana-webhooks-asyncapi
spec_file: asyncapi/asana-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/asana/refs/heads/main/asyncapi/asana-webhooks-asyncapi.yml
tags:
- Collaboration
- Productivity
- Project Management
- Projects
- Task Management
- Tasks
- Workflow
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
