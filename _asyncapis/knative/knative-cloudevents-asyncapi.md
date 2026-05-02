---
api_specs:
- filename: knative-serving-api-openapi.yml
  format: yaml
  label: Knative Serving API
  slug: knative-serving-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/knative/refs/heads/main/openapi/knative-serving-api-openapi.yml
- filename: knative-eventing-api-openapi.yml
  format: yaml
  label: Knative Eventing API
  slug: knative-eventing-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/knative/refs/heads/main/openapi/knative-eventing-api-openapi.yml
channels:
- description: CloudEvents are sent to Broker ingress via HTTP POST and delivered to all matching Triggers. Events must conform to the CloudEvents 1.0 specification in either structured JSON or binary encoding.
  name: /broker
  operation: publish
  operation_id: sendEventToBroker
  summary: Send a CloudEvent to a Broker
- description: CloudEvents are sent to Channel ingress via HTTP POST and fanned out to all Subscriptions. Each Subscription receives the event independently.
  name: /channel
  operation: publish
  operation_id: sendEventToChannel
  summary: Send a CloudEvent to a Channel
- description: Event sinks receive CloudEvents from sources like ApiServerSource, PingSource, and SinkBinding via HTTP POST. The sink URL is injected as K_SINK for SinkBinding subjects or specified in source specs.
  name: /sink
  operation: subscribe
  operation_id: receiveEventFromSource
  summary: Receive a CloudEvent from an event source
description: Knative Eventing uses HTTP POST requests conforming to the CloudEvents specification to deliver events between event sources, Brokers, Triggers, Channels, and Subscriptions. Events can carry structured JSON data or binary payloads. This AsyncAPI document describes the CloudEvents message format and event types emitted by built-in Knative sources including ApiServerSource, PingSource, and generic Broker-routed events.
layout: asyncapi
messages:
- description: ''
  name: KubernetesApiEvent
  summary: A CloudEvent emitted by ApiServerSource when a Kubernetes resource event occurs (Added, Modified, or Deleted).
  title: Kubernetes API Server Event
- description: ''
  name: PingEvent
  summary: A CloudEvent emitted by PingSource on a cron schedule with a configurable payload.
  title: PingSource Scheduled Event
- description: ''
  name: GenericCloudEvent
  summary: A generic CloudEvent conforming to the CloudEvents 1.0 specification, used for custom event producers including SinkBinding subjects and custom event sources sending events through Brokers or Channels.
  title: Generic CloudEvent
name: Knative Eventing CloudEvents
provider_name: Knative
provider_slug: knative
servers:
- description: Knative Broker ingress URL. Events are sent via HTTP POST to the Broker address. The broker URL is available in the Broker resource's status.address.url field.
  name: broker
  protocol: http
  url: '{brokerURL}'
- description: Knative Channel ingress URL. Events sent to this URL are fanned out to all Channel Subscriptions. The channel URL is available in the Channel resource's status.address.url field.
  name: channel
  protocol: http
  url: '{channelURL}'
slug: knative-cloudevents-asyncapi
source_filename: knative-cloudevents-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Knative Eventing CloudEvents\n  description: >-\n    Knative Eventing uses HTTP POST requests conforming to the CloudEvents\n    specification to deliver events between event sources, Brokers, Triggers,\n    Channels, and Subscriptions. Events can carry structured JSON data or\n    binary payloads. This AsyncAPI document describes the CloudEvents message\n    format and event types emitted by built-in Knative sources including\n    ApiServerSource, PingSource, and generic Broker-routed events.\n  version: '1.0'\n  contact:\n    name: Knative Community\n    url: https://knative.dev/community/\nexternalDocs:\n  description: Knative Eventing Documentation\n  url: https://knative.dev/docs/eventing/\nservers:\n  broker:\n    url: '{brokerURL}'\n    protocol: http\n    description: >-\n      Knative Broker ingress URL. Events are sent via HTTP POST to the Broker\n      address. The broker URL is available in the Broker resource's\n      status.address.url\
  \ field.\n    variables:\n      brokerURL:\n        description: The URL of a Knative Broker ingress endpoint.\n    security:\n      - bearerAuth: []\n  channel:\n    url: '{channelURL}'\n    protocol: http\n    description: >-\n      Knative Channel ingress URL. Events sent to this URL are fanned out to\n      all Channel Subscriptions. The channel URL is available in the Channel\n      resource's status.address.url field.\n    variables:\n      channelURL:\n        description: The URL of a Knative Channel ingress endpoint.\n    security:\n      - bearerAuth: []\nchannels:\n  /broker:\n    description: >-\n      CloudEvents are sent to Broker ingress via HTTP POST and delivered to\n      all matching Triggers. Events must conform to the CloudEvents 1.0\n      specification in either structured JSON or binary encoding.\n    publish:\n      operationId: sendEventToBroker\n      summary: Send a CloudEvent to a Broker\n      description: >-\n        Publishes a CloudEvent to a Knative Broker.\
  \ The Broker evaluates all\n        associated Triggers and delivers the event to each Trigger whose\n        attribute filters match the event's CloudEvent attributes.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/KubernetesApiEvent'\n          - $ref: '#/components/messages/PingEvent'\n          - $ref: '#/components/messages/GenericCloudEvent'\n    subscribe:\n      operationId: receiveEventFromBroker\n      summary: Receive a CloudEvent from a Broker via Trigger\n      description: >-\n        A subscriber receives CloudEvents forwarded from a Broker via a Trigger.\n        Events are delivered as HTTP POST requests to the subscriber's address\n        in CloudEvents structured or binary format.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/KubernetesApiEvent'\n          - $ref: '#/components/messages/PingEvent'\n          - $ref: '#/components/messages/GenericCloudEvent'\n  /channel:\n    description: >-\n      CloudEvents are\
  \ sent to Channel ingress via HTTP POST and fanned out to\n      all Subscriptions. Each Subscription receives the event independently.\n    publish:\n      operationId: sendEventToChannel\n      summary: Send a CloudEvent to a Channel\n      description: >-\n        Publishes a CloudEvent to a Knative Channel. The Channel delivers the\n        event to all associated Subscriptions independently.\n      message:\n        $ref: '#/components/messages/GenericCloudEvent'\n    subscribe:\n      operationId: receiveEventFromChannel\n      summary: Receive a CloudEvent from a Channel via Subscription\n      description: >-\n        A subscriber receives CloudEvents forwarded from a Channel via a\n        Subscription. Events are delivered as HTTP POST requests.\n      message:\n        $ref: '#/components/messages/GenericCloudEvent'\n  /sink:\n    description: >-\n      Event sinks receive CloudEvents from sources like ApiServerSource,\n      PingSource, and SinkBinding via HTTP POST. The sink\
  \ URL is injected\n      as K_SINK for SinkBinding subjects or specified in source specs.\n    subscribe:\n      operationId: receiveEventFromSource\n      summary: Receive a CloudEvent from an event source\n      description: >-\n        An event sink receives CloudEvents from Knative event sources. Events\n        from ApiServerSource carry Kubernetes API event data; PingSource events\n        carry the configured payload; SinkBinding subjects send custom events.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/KubernetesApiEvent'\n          - $ref: '#/components/messages/PingEvent'\n          - $ref: '#/components/messages/GenericCloudEvent'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: http\n      scheme: bearer\n      bearerFormat: JWT\n      description: >-\n        Kubernetes service account token for authenticating event delivery.\n        Used when OIDC token-based authentication is enabled on Knative Eventing.\n  messages:\n    KubernetesApiEvent:\n\
  \      name: KubernetesApiEvent\n      title: Kubernetes API Server Event\n      summary: >-\n        A CloudEvent emitted by ApiServerSource when a Kubernetes resource\n        event occurs (Added, Modified, or Deleted).\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          ce-specversion:\n            type: string\n            const: '1.0'\n            description: CloudEvents specification version.\n          ce-type:\n            type: string\n            enum:\n              - dev.knative.apiserver.resource.add\n              - dev.knative.apiserver.resource.update\n              - dev.knative.apiserver.resource.delete\n              - dev.knative.apiserver.ref.add\n              - dev.knative.apiserver.ref.update\n              - dev.knative.apiserver.ref.delete\n            description: >-\n              CloudEvents type indicating the Kubernetes API event type.\n              Resource modes include the full resource body; ref\
  \ modes include\n              only the resource reference.\n          ce-source:\n            type: string\n            description: >-\n              URI identifying the ApiServerSource that emitted this event,\n              typically the Kubernetes API server URL.\n          ce-id:\n            type: string\n            description: Unique identifier for this CloudEvent.\n          ce-time:\n            type: string\n            format: date-time\n            description: Timestamp when the event was created.\n          ce-subject:\n            type: string\n            description: >-\n              Subject identifying the Kubernetes resource that triggered the event,\n              typically in the format namespace/name.\n      payload:\n        $ref: '#/components/schemas/KubernetesApiEventPayload'\n    PingEvent:\n      name: PingEvent\n      title: PingSource Scheduled Event\n      summary: >-\n        A CloudEvent emitted by PingSource on a cron schedule with a\n        configurable\
  \ payload.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          ce-specversion:\n            type: string\n            const: '1.0'\n            description: CloudEvents specification version.\n          ce-type:\n            type: string\n            const: dev.knative.sources.ping\n            description: CloudEvents type for PingSource events.\n          ce-source:\n            type: string\n            description: >-\n              URI identifying the PingSource, typically in the form\n              /apis/v1/namespaces/{namespace}/pingsources/{name}.\n          ce-id:\n            type: string\n            description: Unique identifier for this CloudEvent.\n          ce-time:\n            type: string\n            format: date-time\n            description: Timestamp when the ping event was fired.\n      payload:\n        $ref: '#/components/schemas/PingEventPayload'\n    GenericCloudEvent:\n      name: GenericCloudEvent\n  \
  \    title: Generic CloudEvent\n      summary: >-\n        A generic CloudEvent conforming to the CloudEvents 1.0 specification,\n        used for custom event producers including SinkBinding subjects and\n        custom event sources sending events through Brokers or Channels.\n      contentType: application/json\n      headers:\n        type: object\n        required:\n          - ce-specversion\n          - ce-type\n          - ce-source\n          - ce-id\n        properties:\n          ce-specversion:\n            type: string\n            const: '1.0'\n            description: CloudEvents specification version. Must be 1.0.\n          ce-type:\n            type: string\n            description: >-\n              CloudEvents type attribute identifying the kind of event. Should\n              be reverse-DNS formatted, for example com.example.order.created.\n          ce-source:\n            type: string\n            description: >-\n              URI identifying the context in which\
  \ this event occurred,\n              such as the system or service that produced the event.\n          ce-id:\n            type: string\n            description: >-\n              Unique identifier for this event within the scope of the source.\n              Combined with source, must be globally unique.\n          ce-time:\n            type: string\n            format: date-time\n            description: Timestamp when the event occurred.\n          ce-subject:\n            type: string\n            description: Subject of the event within the context of the source.\n          ce-datacontenttype:\n            type: string\n            description: Content type of the data payload, typically application/json.\n          ce-schemaurl:\n            type: string\n            format: uri\n            description: URI identifying the schema for the event data.\n      payload:\n        type: object\n        description: Arbitrary event payload. Structure depends on the event type.\n  schemas:\n\
  \    KubernetesApiEventPayload:\n      type: object\n      description: >-\n        Payload of a Kubernetes API server event emitted by ApiServerSource.\n        In Resource mode, contains the full Kubernetes resource object.\n        In Reference mode, contains a reference to the affected resource.\n      properties:\n        apiVersion:\n          type: string\n          description: API version of the Kubernetes resource that triggered the event.\n        kind:\n          type: string\n          description: Kind of the Kubernetes resource.\n        metadata:\n          type: object\n          description: Kubernetes object metadata for the affected resource.\n          properties:\n            name:\n              type: string\n              description: Name of the resource.\n            namespace:\n              type: string\n              description: Namespace of the resource.\n            uid:\n              type: string\n              description: Unique identifier of the resource.\n\
  \            resourceVersion:\n              type: string\n              description: Resource version at the time of the event.\n            creationTimestamp:\n              type: string\n              format: date-time\n              description: Time the resource was created.\n        spec:\n          type: object\n          description: Spec of the Kubernetes resource (Resource mode only).\n        status:\n          type: object\n          description: Status of the Kubernetes resource (Resource mode only).\n    PingEventPayload:\n      type: object\n      description: >-\n        Payload of a PingSource event. The content is the configured data\n        field of the PingSource spec. Can be any valid JSON value.\n      additionalProperties: true\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/knative/refs/heads/main/asyncapi/knative-cloudevents-asyncapi.yml
spec_file: asyncapi/knative-cloudevents-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/knative/refs/heads/main/asyncapi/knative-cloudevents-asyncapi.yml
tags:
- Auto-Scaling
- Cloud Native
- Event-Driven
- Graduated
- Kubernetes
- Serverless
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
