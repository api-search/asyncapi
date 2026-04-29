---
api_specs:
- filename: eventmesh-admin.yml
  format: yaml
  label: Apache EventMesh Admin API
  slug: eventmesh-admin-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/apache-event-mesh/refs/heads/main/openapi/eventmesh-admin.yml
- filename: eventmesh-messaging.yml
  format: yaml
  label: Apache EventMesh Messaging API
  slug: eventmesh-messaging-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/apache-event-mesh/refs/heads/main/asyncapi/eventmesh-messaging.yml
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
source_filename: eventmesh-messaging.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Apache EventMesh Messaging API\n  version: 1.10.0\n  description: >-\n    Apache EventMesh provides event-driven messaging via multiple protocols\n    including TCP, HTTP, and gRPC. Events follow the CloudEvents specification.\n    EventMesh decouples event producers and consumers, supporting pub-sub,\n    request-reply, and broadcast messaging patterns.\n  contact:\n    name: Apache EventMesh\n    url: https://eventmesh.apache.org/\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\nservers:\n  tcp:\n    url: localhost:10000\n    protocol: tcp\n    description: EventMesh TCP endpoint\n  grpc:\n    url: localhost:10205\n    protocol: grpc\n    description: EventMesh gRPC endpoint\ndefaultContentType: application/cloudevents+json\nchannels:\n  '{topic}':\n    description: >-\n      EventMesh topic for pub-sub messaging. Events are published to topics\n      and delivered to all subscribed consumer groups.\n\
  \    parameters:\n      topic:\n        description: The topic name\n        schema:\n          type: string\n    publish:\n      operationId: publishEvent\n      summary: Publish a CloudEvent to a topic\n      message:\n        $ref: '#/components/messages/CloudEventMessage'\n    subscribe:\n      operationId: subscribeEvent\n      summary: Subscribe to events on a topic\n      message:\n        $ref: '#/components/messages/CloudEventMessage'\n  '{topic}/request':\n    description: >-\n      EventMesh request-reply channel. A producer sends a request event and\n      awaits a reply event from a consumer.\n    parameters:\n      topic:\n        schema:\n          type: string\n    publish:\n      operationId: requestEvent\n      summary: Send a request event and await reply\n      message:\n        $ref: '#/components/messages/CloudEventMessage'\n    subscribe:\n      operationId: replyEvent\n      summary: Receive request and send reply\n      message:\n        $ref: '#/components/messages/CloudEventMessage'\n\
  \  '{topic}/broadcast':\n    description: >-\n      EventMesh broadcast channel. Events are delivered to all connected\n      consumers regardless of consumer group.\n    parameters:\n      topic:\n        schema:\n          type: string\n    publish:\n      operationId: broadcastEvent\n      summary: Broadcast a CloudEvent to all consumers\n      message:\n        $ref: '#/components/messages/CloudEventMessage'\n    subscribe:\n      operationId: receiveBroadcast\n      summary: Receive broadcast events\n      message:\n        $ref: '#/components/messages/CloudEventMessage'\ncomponents:\n  messages:\n    CloudEventMessage:\n      name: CloudEventMessage\n      title: CloudEvent Message\n      summary: A CloudEvents v1.0 compliant event routed through EventMesh\n      contentType: application/cloudevents+json\n      headers:\n        type: object\n        properties:\n          ce-specversion:\n            type: string\n            const: \"1.0\"\n          ce-id:\n            type: string\n\
  \          ce-source:\n            type: string\n          ce-type:\n            type: string\n          ce-time:\n            type: string\n            format: date-time\n          ce-subject:\n            type: string\n          ce-datacontenttype:\n            type: string\n          env:\n            type: string\n            description: EventMesh environment\n          idc:\n            type: string\n            description: EventMesh IDC\n          sys:\n            type: string\n            description: EventMesh system\n          pid:\n            type: string\n            description: Producer/consumer process ID\n          group:\n            type: string\n            description: Consumer group\n      payload:\n        type: object\n        description: The CloudEvent data payload\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/apache-event-mesh/refs/heads/main/asyncapi/eventmesh-messaging.yml
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
