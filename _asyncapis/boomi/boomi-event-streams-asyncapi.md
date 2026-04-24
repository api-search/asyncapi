---
channels:
- description: The root path of the topic-specific endpoint. POST to this channel to publish messages. Each topic has its own unique base URL.
  name: /
  operation: publish
  operation_id: publishMessage
  summary: Publish a message to the topic
description: Boomi Event Streams provides a publish-subscribe messaging system within the Boomi Enterprise Platform. Topics act as channels where producers publish messages and consumers receive them via Boomi recipes or HTTP REST. Event Streams integrate natively with the Boomi integration platform as triggers and actions, enabling loosely-coupled, event-driven integration workflows. Messages may be up to 5 MB and the API enforces a rate limit of 60,000 requests per IP per 5-minute window.
layout: asyncapi
messages:
- description: Publishes one or more messages in the predefined multi-message JSON format. Each message in the array has a payload field and an optional properties map for custom metadata.
  name: MultiMessage
  summary: Publish multiple messages in structured JSON format.
  title: Multi-Message Publish
- description: Publishes a single message without transformation. The content type can be application/json, text/plain, or application/xml. Message properties are passed via request headers prefixed with x-msg-props-.
  name: SingleMessage
  summary: Publish a single message in its original format.
  title: Single Message Publish
- description: A message delivered to a Boomi integration process that is configured to listen on this event topic. Contains the original payload and any properties set by the producer.
  name: DeliveredMessage
  summary: A message delivered to a Boomi recipe subscriber.
  title: Delivered Message
name: Boomi Event Streams
provider_name: Boomi
provider_slug: boomi
servers:
- description: Topic-specific REST endpoint. Each Boomi Event Streams topic has a unique URL available from the Event Streams UI in the Boomi platform.
  name: production
  protocol: https
  url: '{topicEndpoint}'
slug: boomi-event-streams-asyncapi
spec_file: asyncapi/boomi-event-streams-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/boomi/refs/heads/main/asyncapi/boomi-event-streams-asyncapi.yml
tags:
- AI Agents
- Automation
- B2B
- Data Integration
- EDI
- Integrations
- Management
- MFT
- Platform
- Workflows
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
