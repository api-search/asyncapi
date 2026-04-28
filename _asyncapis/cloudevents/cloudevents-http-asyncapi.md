---
channels:
- description: The subscriber's sink endpoint receives HTTP POST requests from the CloudEvents broker. Each request carries one CloudEvent (single delivery mode) or a batch of CloudEvents (batch delivery mode). The subscriber acknowledges receipt with a 2xx HTTP response.
  name: /
  operation: publish
  operation_id: receiveCloudEvent
  summary: Receive a CloudEvent from the broker
- description: Batch delivery endpoint where the broker delivers multiple CloudEvents in a single HTTP POST request using the application/cloudevents-batch+json content type. Reduces per-event HTTP overhead for high-throughput scenarios.
  name: /batch
  operation: publish
  operation_id: receiveCloudEventBatch
  summary: Receive a batch of CloudEvents from the broker
description: AsyncAPI definition for CloudEvents delivery over HTTP. This document describes the event-driven interface by which a CloudEvents-compatible broker pushes events to a subscriber's HTTP sink endpoint. Events are formatted as CloudEvents v1.0 and delivered in either structured content mode (application/cloudevents+json) or binary content mode (with CloudEvents attributes in HTTP headers). The subscriber's endpoint acts as an HTTP webhook that receives POST requests from the event broker.
layout: asyncapi
messages:
- description: ''
  name: StructuredCloudEvent
  summary: A single CloudEvent delivered in structured content mode where all event data including context attributes is encoded as a JSON object in the HTTP request body.
  title: CloudEvent (Structured Content Mode)
- description: ''
  name: BinaryCloudEvent
  summary: A single CloudEvent delivered in binary content mode where CloudEvents context attributes are HTTP headers prefixed with 'ce-' and the event data is the raw HTTP body.
  title: CloudEvent (Binary Content Mode)
- description: ''
  name: BatchedCloudEvents
  summary: A batch of CloudEvents delivered in a single HTTP POST using the application/cloudevents-batch+json media type. Improves throughput by reducing per-event HTTP overhead.
  title: CloudEvents Batch
name: CloudEvents HTTP Delivery
provider_name: CloudEvents
provider_slug: cloudevents
servers:
- description: The subscriber's HTTP sink endpoint where the event broker delivers CloudEvents. Provided by the subscriber when creating a subscription.
  name: subscriberSink
  protocol: https
  url: '{sinkUrl}'
slug: cloudevents-http-asyncapi
spec_file: asyncapi/cloudevents-http-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/cloudevents/refs/heads/main/asyncapi/cloudevents-http-asyncapi.yml
tags:
- Cloud Native
- Events
- Graduated
- Interoperability
- Messaging
- Specification
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
