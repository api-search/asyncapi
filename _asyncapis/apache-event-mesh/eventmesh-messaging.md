---
channels:
- description: EventMesh topic for pub-sub messaging. Events are published to topics and delivered to all subscribed consumer groups.
  name: '{topic}'
  operation: publish
  operation_id: publishEvent
  summary: Publish a CloudEvent to a topic
- description: EventMesh request-reply channel. A producer sends a request event and awaits a reply event from a consumer.
  name: '{topic}/request'
  operation: publish
  operation_id: requestEvent
  summary: Send a request event and await reply
- description: EventMesh broadcast channel. Events are delivered to all connected consumers regardless of consumer group.
  name: '{topic}/broadcast'
  operation: publish
  operation_id: broadcastEvent
  summary: Broadcast a CloudEvent to all consumers
description: Apache EventMesh provides event-driven messaging via multiple protocols including TCP, HTTP, and gRPC. Events follow the CloudEvents specification. EventMesh decouples event producers and consumers, supporting pub-sub, request-reply, and broadcast messaging patterns.
layout: asyncapi
messages:
- description: ''
  name: CloudEventMessage
  summary: A CloudEvents v1.0 compliant event routed through EventMesh
  title: CloudEvent Message
name: Apache EventMesh Messaging API
provider_name: Apache EventMesh
provider_slug: apache-event-mesh
servers:
- description: EventMesh TCP endpoint
  name: tcp
  protocol: tcp
  url: localhost:10000
- description: EventMesh gRPC endpoint
  name: grpc
  protocol: grpc
  url: localhost:10205
slug: eventmesh-messaging
spec_file: asyncapi/eventmesh-messaging.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/apache-event-mesh/refs/heads/main/asyncapi/eventmesh-messaging.yml
tags:
- Apache
- CloudEvents
- Event-Driven
- Messaging
- Open Source
- Pub-Sub
- Serverless
- AsyncAPI
- Webhooks
- Events
version: 1.10.0
---
