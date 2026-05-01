---
api_specs:
- filename: dapr-state-management-openapi.yml
  format: yaml
  label: Dapr State Management API
  slug: state-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/openapi/dapr-state-management-openapi.yml
- filename: dapr-pubsub-openapi.yml
  format: yaml
  label: Dapr Pub/Sub API
  slug: pubsub
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/openapi/dapr-pubsub-openapi.yml
- filename: dapr-service-invocation-openapi.yml
  format: yaml
  label: Dapr Service Invocation API
  slug: service-invocation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/openapi/dapr-service-invocation-openapi.yml
- filename: dapr-bindings-openapi.yml
  format: yaml
  label: Dapr Bindings API
  slug: bindings
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/openapi/dapr-bindings-openapi.yml
- filename: dapr-secrets-openapi.yml
  format: yaml
  label: Dapr Secrets API
  slug: secrets
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/openapi/dapr-secrets-openapi.yml
- filename: dapr-actors-openapi.yml
  format: yaml
  label: Dapr Actors API
  slug: actors
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/openapi/dapr-actors-openapi.yml
- filename: dapr-workflow-openapi.yml
  format: yaml
  label: Dapr Workflow API
  slug: workflow
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/openapi/dapr-workflow-openapi.yml
- filename: dapr-configuration-openapi.yml
  format: yaml
  label: Dapr Configuration API
  slug: configuration
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/openapi/dapr-configuration-openapi.yml
- filename: dapr-distributed-lock-openapi.yml
  format: yaml
  label: Dapr Distributed Lock API
  slug: distributed-lock
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/openapi/dapr-distributed-lock-openapi.yml
- filename: dapr-cryptography-openapi.yml
  format: yaml
  label: Dapr Cryptography API
  slug: cryptography
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/openapi/dapr-cryptography-openapi.yml
- filename: dapr-jobs-openapi.yml
  format: yaml
  label: Dapr Jobs API
  slug: jobs
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/openapi/dapr-jobs-openapi.yml
- filename: dapr-health-openapi.yml
  format: yaml
  label: Dapr Health API
  slug: health
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/openapi/dapr-health-openapi.yml
- filename: dapr-metadata-openapi.yml
  format: yaml
  label: Dapr Metadata API
  slug: metadata
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/openapi/dapr-metadata-openapi.yml
channels:
- description: Channel for publishing events to a topic on a named pub/sub component. The Dapr sidecar wraps payloads in CloudEvents format unless raw payload mode is enabled.
  name: publish
  operation: publish
  operation_id: publishEvent
  summary: Publish Event
- description: Channel for receiving events from subscribed topics. Dapr delivers events to application endpoints based on programmatic or declarative subscription configurations.
  name: subscribe
  operation: subscribe
  operation_id: receiveEvent
  summary: Receive Event
- description: Channel for publishing multiple events to a topic in a single request. Supports partial failure reporting for individual entries.
  name: bulk-publish
  operation: publish
  operation_id: bulkPublishEvents
  summary: Bulk Publish Events
description: The Dapr Pub/Sub AsyncAPI defines the event-driven messaging interfaces for Dapr publish and subscribe operations. Applications publish events to topics and subscribe to receive events using the CloudEvents 1.0 specification format. Dapr supports pluggable pub/sub components including Kafka, RabbitMQ, Redis Streams, Azure Service Bus, AWS SNS/SQS, GCP Pub/Sub, and more.
layout: asyncapi
messages:
- description: ''
  name: CloudEvent
  summary: A message conforming to the CloudEvents 1.0 specification used for all Dapr pub/sub event payloads.
  title: CloudEvent Message
- description: ''
  name: BulkPublishEntry
  summary: A single entry in a bulk publish request containing the event data and metadata.
  title: Bulk Publish Entry
name: Dapr Pub/Sub Messaging API
provider_name: Dapr
provider_slug: dapr
servers:
- description: Dapr sidecar HTTP endpoint for publishing events. The sidecar handles routing messages to the configured pub/sub component.
  name: dapr-sidecar
  protocol: http
  url: localhost:3500
slug: dapr-pubsub-asyncapi
source_filename: dapr-pubsub-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Dapr Pub/Sub Messaging API\n  version: 1.0.0\n  description: >-\n    The Dapr Pub/Sub AsyncAPI defines the event-driven messaging interfaces\n    for Dapr publish and subscribe operations. Applications publish events\n    to topics and subscribe to receive events using the CloudEvents 1.0\n    specification format. Dapr supports pluggable pub/sub components\n    including Kafka, RabbitMQ, Redis Streams, Azure Service Bus, AWS SNS/SQS,\n    GCP Pub/Sub, and more.\n  contact:\n    name: Dapr\n    url: https://dapr.io\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\n  externalDocs:\n    description: Dapr Pub/Sub API Reference\n    url: https://docs.dapr.io/reference/api/pubsub_api/\nservers:\n  dapr-sidecar:\n    url: localhost:3500\n    protocol: http\n    description: >-\n      Dapr sidecar HTTP endpoint for publishing events. The sidecar handles\n      routing messages to the configured pub/sub component.\n\
  channels:\n  publish:\n    description: >-\n      Channel for publishing events to a topic on a named pub/sub component.\n      The Dapr sidecar wraps payloads in CloudEvents format unless raw payload\n      mode is enabled.\n    publish:\n      operationId: publishEvent\n      summary: Publish Event\n      description: >-\n        Publishes an event to the specified topic. If content type is not\n        application/cloudevents+json, the payload is automatically wrapped\n        in a CloudEvent envelope by the Dapr sidecar.\n      message:\n        $ref: '#/components/messages/CloudEvent'\n      tags:\n        - name: PubSub\n        - name: Messaging\n  subscribe:\n    description: >-\n      Channel for receiving events from subscribed topics. Dapr delivers\n      events to application endpoints based on programmatic or declarative\n      subscription configurations.\n    subscribe:\n      operationId: receiveEvent\n      summary: Receive Event\n      description: >-\n        Receives\
  \ an event from a subscribed topic. Events are delivered in\n        CloudEvents format to the application endpoint registered for the\n        topic subscription.\n      message:\n        $ref: '#/components/messages/CloudEvent'\n      tags:\n        - name: PubSub\n        - name: Messaging\n  bulk-publish:\n    description: >-\n      Channel for publishing multiple events to a topic in a single request.\n      Supports partial failure reporting for individual entries.\n    publish:\n      operationId: bulkPublishEvents\n      summary: Bulk Publish Events\n      description: >-\n        Publishes multiple events to the specified topic in a single\n        operation. Each entry includes an entryId, event data, and optional\n        content type and metadata.\n      message:\n        $ref: '#/components/messages/BulkPublishEntry'\n      tags:\n        - name: PubSub\n        - name: Messaging\n        - name: Bulk\ncomponents:\n  messages:\n    CloudEvent:\n      name: CloudEvent\n   \
  \   title: CloudEvent Message\n      summary: >-\n        A message conforming to the CloudEvents 1.0 specification used\n        for all Dapr pub/sub event payloads.\n      contentType: application/cloudevents+json\n      payload:\n        $ref: '#/components/schemas/CloudEvent'\n    BulkPublishEntry:\n      name: BulkPublishEntry\n      title: Bulk Publish Entry\n      summary: >-\n        A single entry in a bulk publish request containing the event data\n        and metadata.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BulkPublishEntry'\n  schemas:\n    CloudEvent:\n      type: object\n      description: >-\n        CloudEvents 1.0 specification envelope used by Dapr for pub/sub\n        messaging. All published events are wrapped in this format unless\n        raw payload mode is enabled.\n      required:\n        - specversion\n        - type\n        - source\n        - id\n      properties:\n        specversion:\n          type: string\n\
  \          description: The version of the CloudEvents specification (1.0).\n          enum:\n            - '1.0'\n        type:\n          type: string\n          description: The type of the event.\n        source:\n          type: string\n          description: The source of the event.\n        id:\n          type: string\n          description: Unique identifier for the event.\n        subject:\n          type: string\n          description: The subject of the event in context of the producer.\n        time:\n          type: string\n          format: date-time\n          description: Timestamp of when the event occurred.\n        datacontenttype:\n          type: string\n          description: Content type of the data attribute.\n        data:\n          description: The event payload data.\n        topic:\n          type: string\n          description: The topic the event is published to.\n        pubsubname:\n          type: string\n          description: The name of the pub/sub\
  \ component.\n        traceid:\n          type: string\n          description: The distributed tracing identifier.\n        traceparent:\n          type: string\n          description: The W3C trace context traceparent header value.\n        tracestate:\n          type: string\n          description: The W3C trace context tracestate header value.\n    BulkPublishEntry:\n      type: object\n      description: A single entry in a bulk publish request.\n      required:\n        - entryId\n        - event\n      properties:\n        entryId:\n          type: string\n          description: Unique identifier for the entry.\n        event:\n          description: The event data payload.\n        contentType:\n          type: string\n          description: Content type of the event data.\n        metadata:\n          type: object\n          additionalProperties:\n            type: string\n          description: Additional metadata for the entry.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/asyncapi/dapr-pubsub-asyncapi.yml
spec_file: asyncapi/dapr-pubsub-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/dapr/refs/heads/main/asyncapi/dapr-pubsub-asyncapi.yml
tags:
- Distributed Systems
- Microservices
- Platform
- Pub/Sub
- State Management
- Workflows
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
