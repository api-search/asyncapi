---
api_specs:
- filename: cloudevents-http-asyncapi.yml
  format: yaml
  label: CloudEvents Specification
  slug: cloudevents-spec
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/cloudevents/refs/heads/main/asyncapi/cloudevents-http-asyncapi.yml
- filename: cloudevents-subscriptions-openapi.yml
  format: yaml
  label: CloudEvents Subscriptions API
  slug: cloudevents-subscriptions
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/cloudevents/refs/heads/main/openapi/cloudevents-subscriptions-openapi.yml
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
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: CloudEvents HTTP Delivery\n  description: >-\n    AsyncAPI definition for CloudEvents delivery over HTTP. This document\n    describes the event-driven interface by which a CloudEvents-compatible\n    broker pushes events to a subscriber's HTTP sink endpoint. Events are\n    formatted as CloudEvents v1.0 and delivered in either structured content\n    mode (application/cloudevents+json) or binary content mode (with\n    CloudEvents attributes in HTTP headers). The subscriber's endpoint acts\n    as an HTTP webhook that receives POST requests from the event broker.\n  version: '1.0'\n  contact:\n    name: CloudEvents Community\n    url: https://cloudevents.io\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\nexternalDocs:\n  description: CloudEvents HTTP Protocol Binding Specification\n  url: https://github.com/cloudevents/spec/blob/v1.0.2/cloudevents/bindings/http-protocol-binding.md\nservers:\n  subscriberSink:\n\
  \    url: '{sinkUrl}'\n    protocol: https\n    description: >-\n      The subscriber's HTTP sink endpoint where the event broker delivers\n      CloudEvents. Provided by the subscriber when creating a subscription.\n    variables:\n      sinkUrl:\n        description: >-\n          Fully qualified HTTPS URL of the subscriber's event receiver endpoint,\n          as registered in the CloudEvents Subscriptions API.\n    security:\n      - bearerAuth: []\nchannels:\n  /:\n    description: >-\n      The subscriber's sink endpoint receives HTTP POST requests from the\n      CloudEvents broker. Each request carries one CloudEvent (single delivery\n      mode) or a batch of CloudEvents (batch delivery mode). The subscriber\n      acknowledges receipt with a 2xx HTTP response.\n    publish:\n      operationId: receiveCloudEvent\n      summary: Receive a CloudEvent from the broker\n      description: >-\n        The event broker delivers a CloudEvent to this endpoint via HTTP POST.\n        In\
  \ structured content mode the Content-Type is application/cloudevents+json\n        and the full event including context attributes is in the request body.\n        In binary content mode event context attributes are mapped to HTTP headers\n        prefixed with 'ce-' and the data payload is the raw request body with\n        the event's datacontenttype as Content-Type.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/StructuredCloudEvent'\n          - $ref: '#/components/messages/BinaryCloudEvent'\n          - $ref: '#/components/messages/BatchedCloudEvents'\n  /batch:\n    description: >-\n      Batch delivery endpoint where the broker delivers multiple CloudEvents\n      in a single HTTP POST request using the application/cloudevents-batch+json\n      content type. Reduces per-event HTTP overhead for high-throughput scenarios.\n    publish:\n      operationId: receiveCloudEventBatch\n      summary: Receive a batch of CloudEvents from the broker\n      description:\
  \ >-\n        The event broker delivers multiple CloudEvents in a single HTTP POST\n        request using the application/cloudevents-batch+json media type. The\n        body is a JSON array where each element is a complete CloudEvent in\n        structured format. The subscriber should return 200 to acknowledge\n        successful receipt of the entire batch.\n      message:\n        $ref: '#/components/messages/BatchedCloudEvents'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: http\n      scheme: bearer\n      description: >-\n        Bearer token authentication for the subscriber sink endpoint. The\n        event broker includes this token in the Authorization header when\n        delivering events. Configure via protocolSettings in the subscription.\n  messages:\n    StructuredCloudEvent:\n      name: StructuredCloudEvent\n      title: CloudEvent (Structured Content Mode)\n      summary: >-\n        A single CloudEvent delivered in structured content mode where all\n\
  \        event data including context attributes is encoded as a JSON object\n        in the HTTP request body.\n      contentType: application/cloudevents+json\n      headers:\n        type: object\n        properties:\n          Content-Type:\n            type: string\n            const: application/cloudevents+json\n            description: >-\n              Indicates structured CloudEvents content mode. The full CloudEvent\n              is in the HTTP body as a JSON object.\n      payload:\n        $ref: '#/components/schemas/CloudEvent'\n    BinaryCloudEvent:\n      name: BinaryCloudEvent\n      title: CloudEvent (Binary Content Mode)\n      summary: >-\n        A single CloudEvent delivered in binary content mode where CloudEvents\n        context attributes are HTTP headers prefixed with 'ce-' and the event\n        data is the raw HTTP body.\n      headers:\n        type: object\n        required:\n          - ce-specversion\n          - ce-id\n          - ce-source\n        \
  \  - ce-type\n        properties:\n          ce-specversion:\n            type: string\n            const: '1.0'\n            description: CloudEvents spec version header. Always '1.0'.\n          ce-id:\n            type: string\n            description: Unique identifier for the event. Corresponds to the 'id' attribute.\n          ce-source:\n            type: string\n            description: URI-reference identifying the event origin. Corresponds to 'source'.\n          ce-type:\n            type: string\n            description: Type of the event. Corresponds to the 'type' attribute.\n          ce-subject:\n            type: string\n            description: Subject of the event in the producer context. Corresponds to 'subject'.\n          ce-time:\n            type: string\n            format: date-time\n            description: RFC 3339 timestamp of when the event occurred. Corresponds to 'time'.\n          ce-dataschema:\n            type: string\n            format: uri\n      \
  \      description: URI of the schema the data adheres to. Corresponds to 'dataschema'.\n          ce-traceparent:\n            type: string\n            description: W3C Trace Context traceparent for distributed tracing extension.\n          ce-tracestate:\n            type: string\n            description: W3C Trace Context tracestate for distributed tracing extension.\n          Content-Type:\n            type: string\n            description: >-\n              MIME type of the event data payload. Corresponds to the 'datacontenttype'\n              CloudEvents attribute.\n      payload:\n        description: >-\n          The raw event data payload. Its structure is defined by the event\n          type and the schema identified by the ce-dataschema header.\n    BatchedCloudEvents:\n      name: BatchedCloudEvents\n      title: CloudEvents Batch\n      summary: >-\n        A batch of CloudEvents delivered in a single HTTP POST using the\n        application/cloudevents-batch+json media\
  \ type. Improves throughput\n        by reducing per-event HTTP overhead.\n      contentType: application/cloudevents-batch+json\n      headers:\n        type: object\n        properties:\n          Content-Type:\n            type: string\n            const: application/cloudevents-batch+json\n            description: >-\n              Indicates batch CloudEvents content mode. The body is a JSON array\n              of CloudEvent objects.\n      payload:\n        type: array\n        description: JSON array of CloudEvent objects in structured format.\n        items:\n          $ref: '#/components/schemas/CloudEvent'\n        minItems: 0\n  schemas:\n    CloudEvent:\n      type: object\n      description: >-\n        A CloudEvents v1.0 event envelope with required context attributes\n        and optional data payload.\n      required:\n        - specversion\n        - id\n        - source\n        - type\n      properties:\n        specversion:\n          type: string\n          const:\
  \ '1.0'\n          description: CloudEvents specification version.\n        id:\n          type: string\n          description: >-\n            Unique identifier for this event, unique within the scope of the producer.\n        source:\n          type: string\n          description: URI-reference identifying the context in which the event occurred.\n        type:\n          type: string\n          description: >-\n            Reverse-DNS-prefixed string identifying the event type, e.g.\n            com.example.object.created.\n        datacontenttype:\n          type: string\n          description: RFC 2046 media type of the event data.\n        dataschema:\n          type: string\n          format: uri\n          description: URI of a schema the data attribute adheres to.\n        subject:\n          type: string\n          description: Subject of the event within the producer context.\n        time:\n          type: string\n          format: date-time\n          description: Timestamp\
  \ of when the event occurrence happened.\n        data:\n          description: Event-specific payload data. Structure defined by the event type.\n        data_base64:\n          type: string\n          contentEncoding: base64\n          description: Base64-encoded binary event data, mutually exclusive with 'data'.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cloudevents/refs/heads/main/asyncapi/cloudevents-http-asyncapi.yml
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
