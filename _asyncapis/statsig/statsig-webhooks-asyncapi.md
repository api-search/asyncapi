---
api_specs:
- filename: statsig-http-api-openapi.yml
  format: yaml
  label: Statsig HTTP API
  slug: http-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/openapi/statsig-http-api-openapi.yml
- filename: statsig-console-api-openapi.yml
  format: yaml
  label: Statsig Console API
  slug: console-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/openapi/statsig-console-api-openapi.yml
- filename: statsig-client-sdk-api-openapi.yml
  format: yaml
  label: Statsig Client SDK API
  slug: client-sdk-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/openapi/statsig-client-sdk-api-openapi.yml
- filename: statsig-server-sdk-api-openapi.yml
  format: yaml
  label: Statsig Server SDK API
  slug: server-sdk-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/openapi/statsig-server-sdk-api-openapi.yml
- filename: statsig-events-api-openapi.yml
  format: yaml
  label: Statsig Events API
  slug: events-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/openapi/statsig-events-api-openapi.yml
channels:
- description: Channel for receiving batched event notifications from Statsig. Events are sent as HTTP POST requests with JSON payloads. The channel supports event filtering to control which event types are forwarded.
  name: /webhook
  operation: publish
  operation_id: receiveWebhookEvents
  summary: Receive webhook event batches
description: 'Statsig''s webhook system provides real-time event-driven notifications for exposure events and configuration changes. Webhooks are triggered at runtime as users are assigned to gates and experiments, and events are sent in batches in JSON format. Two main types of events are supported: Exposures (events logged via the SDK such as gate checks and experiment evaluations) and Config Changes (changelogs for Statsig Console actions). Webhook delivery includes signature verification for security using HMAC-SHA256.'
layout: asyncapi
messages:
- description: ''
  name: ExposureEvent
  summary: An exposure event triggered when a user is evaluated against a gate, experiment, or dynamic config via the SDK.
  title: Exposure Event
- description: ''
  name: ConfigChangeEvent
  summary: A configuration change event triggered when a gate, experiment, dynamic config, or other entity is created, updated, or deleted through the Statsig Console or API.
  title: Config Change Event
- description: ''
  name: EventBatch
  summary: A batch of events containing one or more exposure or config change events sent together for efficiency.
  title: Event Batch
name: Statsig Webhook Events
provider_name: statsig
provider_slug: statsig
servers:
- description: Your webhook receiver endpoint configured in Statsig integration settings. Statsig sends HTTP POST requests to this URL with batched event payloads.
  name: webhookReceiver
  protocol: https
  url: '{webhookUrl}'
slug: statsig-webhooks-asyncapi
source_filename: statsig-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Statsig Webhook Events\n  description: >-\n    Statsig's webhook system provides real-time event-driven notifications for\n    exposure events and configuration changes. Webhooks are triggered at runtime\n    as users are assigned to gates and experiments, and events are sent in\n    batches in JSON format. Two main types of events are supported: Exposures\n    (events logged via the SDK such as gate checks and experiment evaluations)\n    and Config Changes (changelogs for Statsig Console actions). Webhook\n    delivery includes signature verification for security using HMAC-SHA256.\n  version: '1.0.0'\n  contact:\n    name: Statsig Support\n    url: https://statsig.com/support\nservers:\n  webhookReceiver:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your webhook receiver endpoint configured in Statsig integration\n      settings. Statsig sends HTTP POST requests to this URL with batched\n      event payloads.\n\
  \    variables:\n      webhookUrl:\n        description: >-\n          The URL of your webhook endpoint registered in Statsig.\n    security:\n      - webhookSignature: []\nchannels:\n  /webhook:\n    description: >-\n      Channel for receiving batched event notifications from Statsig. Events\n      are sent as HTTP POST requests with JSON payloads. The channel supports\n      event filtering to control which event types are forwarded.\n    publish:\n      operationId: receiveWebhookEvents\n      summary: Receive webhook event batches\n      description: >-\n        Receives batched event notifications from Statsig. Events are sent\n        in real-time as users interact with gates, experiments, and configs.\n        Batches contain one or more events of mixed types. Verify the\n        webhook signature using the X-Statsig-Signature header before\n        processing.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/ExposureEvent'\n          - $ref: '#/components/messages/ConfigChangeEvent'\n\
  \          - $ref: '#/components/messages/EventBatch'\ncomponents:\n  securitySchemes:\n    webhookSignature:\n      type: httpApiKey\n      name: X-Statsig-Signature\n      in: header\n      description: >-\n        HMAC-SHA256 signature for verifying webhook authenticity. The\n        signature is computed as v0= followed by the HMAC-SHA256 hex digest\n        of the signature basestring, which is constructed by concatenating\n        v0, the X-Statsig-Request-Timestamp header value, and the request\n        body, separated by colons. Compare this header value against your\n        locally computed signature using your webhook signing secret from\n        the Statsig integration settings.\n  messages:\n    ExposureEvent:\n      name: ExposureEvent\n      title: Exposure Event\n      summary: >-\n        An exposure event triggered when a user is evaluated against a gate,\n        experiment, or dynamic config via the SDK.\n      contentType: application/json\n      headers:\n       \
  \ type: object\n        properties:\n          X-Statsig-Signature:\n            type: string\n            description: >-\n              HMAC-SHA256 webhook signature for verification.\n          X-Statsig-Request-Timestamp:\n            type: string\n            description: >-\n              Unix timestamp of when the request was sent, used in\n              signature verification.\n      payload:\n        $ref: '#/components/schemas/ExposureEventPayload'\n    ConfigChangeEvent:\n      name: ConfigChangeEvent\n      title: Config Change Event\n      summary: >-\n        A configuration change event triggered when a gate, experiment,\n        dynamic config, or other entity is created, updated, or deleted\n        through the Statsig Console or API.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Statsig-Signature:\n            type: string\n            description: >-\n              HMAC-SHA256 webhook signature for verification.\n\
  \          X-Statsig-Request-Timestamp:\n            type: string\n            description: >-\n              Unix timestamp of when the request was sent.\n      payload:\n        $ref: '#/components/schemas/ConfigChangeEventPayload'\n    EventBatch:\n      name: EventBatch\n      title: Event Batch\n      summary: >-\n        A batch of events containing one or more exposure or config change\n        events sent together for efficiency.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Statsig-Signature:\n            type: string\n            description: >-\n              HMAC-SHA256 webhook signature for verification.\n          X-Statsig-Request-Timestamp:\n            type: string\n            description: >-\n              Unix timestamp of when the request was sent.\n      payload:\n        $ref: '#/components/schemas/EventBatchPayload'\n  schemas:\n    ExposureEventPayload:\n      type: object\n      description: >-\n \
  \       Payload for an SDK exposure event triggered during gate checks,\n        experiment evaluations, or config fetches.\n      properties:\n        eventName:\n          type: string\n          description: >-\n            The event name, typically in the format statsig::gate_exposure,\n            statsig::config_exposure, or statsig::experiment_exposure.\n        user:\n          $ref: '#/components/schemas/WebhookUser'\n        timestamp:\n          type: integer\n          format: int64\n          description: >-\n            Timestamp of the event in milliseconds since epoch.\n        value:\n          oneOf:\n            - type: string\n            - type: number\n            - type: boolean\n          description: >-\n            The evaluation result value.\n        metadata:\n          type: object\n          properties:\n            gate:\n              type: string\n              description: >-\n                The name of the gate, if this is a gate exposure.\n       \
  \     config:\n              type: string\n              description: >-\n                The name of the config or experiment, if applicable.\n            ruleID:\n              type: string\n              description: >-\n                The rule that matched during evaluation.\n          description: >-\n            Metadata about the exposure evaluation.\n        statsigMetadata:\n          type: object\n          properties:\n            sdkType:\n              type: string\n              description: >-\n                The type of SDK that generated the event.\n            sdkVersion:\n              type: string\n              description: >-\n                The version of the SDK.\n          description: >-\n            SDK metadata associated with the exposure.\n        timeUUID:\n          type: string\n          description: >-\n            A unique identifier for this event instance.\n    ConfigChangeEventPayload:\n      type: object\n      description: >-\n        Payload\
  \ for a configuration change event triggered by console or\n        API actions.\n      properties:\n        eventName:\n          type: string\n          const: statsig::config_change\n          description: >-\n            The event name is always statsig::config_change for config\n            change events.\n        user:\n          $ref: '#/components/schemas/WebhookUser'\n        timestamp:\n          type: integer\n          format: int64\n          description: >-\n            Timestamp of the change in milliseconds since epoch.\n        metadata:\n          type: object\n          properties:\n            type:\n              type: string\n              enum:\n                - Gate\n                - DynamicConfig\n                - Experiment\n                - Segment\n                - Layer\n                - Holdout\n                - Autotune\n              description: >-\n                The type of entity that was changed.\n            name:\n              type: string\n\
  \              description: >-\n                The name of the entity that was changed.\n            description:\n              type: string\n              description: >-\n                A description of the change, often including the entity\n                description.\n            action:\n              type: string\n              enum:\n                - created\n                - updated\n                - deleted\n                - enabled\n                - disabled\n                - launched\n                - archived\n              description: >-\n                The action that was performed on the entity.\n          description: >-\n            Metadata describing the configuration change.\n    EventBatchPayload:\n      type: object\n      description: >-\n        A batch of events sent in a single webhook request.\n      required:\n        - data\n      properties:\n        data:\n          type: array\n          items:\n            oneOf:\n              - $ref: '#/components/schemas/ExposureEventPayload'\n\
  \              - $ref: '#/components/schemas/ConfigChangeEventPayload'\n          minItems: 1\n          description: >-\n            An array of one or more events in the batch.\n    WebhookUser:\n      type: object\n      description: >-\n        User information associated with a webhook event.\n      properties:\n        name:\n          type: string\n          description: >-\n            The name of the user who triggered the event.\n        email:\n          type: string\n          format: email\n          description: >-\n            The email of the user who triggered the event.\n        userID:\n          type: string\n          description: >-\n            The unique identifier of the user.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/asyncapi/statsig-webhooks-asyncapi.yml
spec_file: asyncapi/statsig-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/asyncapi/statsig-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
