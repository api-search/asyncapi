---
api_specs:
- filename: salesforce-openapi.yml
  format: yaml
  label: Salesforce REST API
  slug: salesforce-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/openapi/salesforce-openapi.yml
- filename: salesforce-bulk-api-2-openapi.yml
  format: yaml
  label: Salesforce Bulk API 2.0
  slug: salesforce-bulk-api-2
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/openapi/salesforce-bulk-api-2-openapi.yml
- filename: salesforce-streaming-asyncapi.yml
  format: yaml
  label: Salesforce Streaming API
  slug: salesforce-streaming-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/asyncapi/salesforce-streaming-asyncapi.yml
- filename: salesforce-platform-events-asyncapi.yml
  format: yaml
  label: Salesforce Platform Events API
  slug: salesforce-platform-events-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/asyncapi/salesforce-platform-events-asyncapi.yml
- filename: salesforce-change-data-capture-asyncapi.yml
  format: yaml
  label: Salesforce Change Data Capture API
  slug: salesforce-change-data-capture-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/asyncapi/salesforce-change-data-capture-asyncapi.yml
- filename: salesforce-ui-api-openapi.yml
  format: yaml
  label: Salesforce UI API
  slug: salesforce-ui-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/openapi/salesforce-ui-api-openapi.yml
- filename: salesforce-marketing-cloud-rest-openapi.yml
  format: yaml
  label: Salesforce Marketing Cloud REST API
  slug: salesforce-marketing-cloud-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/openapi/salesforce-marketing-cloud-rest-openapi.yml
- filename: salesforce-openapi.yml
  format: yaml
  label: Salesforce
  slug: salesforce-salesforce
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/openapi/salesforce-openapi.yml
channels:
- description: CometD channel for subscribing to a Platform Event type. Receives events published to this event type from Apex triggers, flows, REST API calls, or external systems via the REST API.
  name: /event/{platformEventApiName}
  operation: publish
  operation_id: publishPlatformEvent
  summary: Publish a Platform Event via CometD (internal use)
description: Salesforce Platform Events enables event-driven integration architectures on the Salesforce platform. Developers define custom event types as Salesforce objects with the __e suffix and publish or subscribe to events using the REST API, Apex triggers, or CometD subscriptions. Events are durable and stored for 72 hours, supporting replay for missed events.
layout: asyncapi
messages:
- description: ''
  name: PlatformEventMessage
  summary: A Platform Event notification received via CometD
  title: Salesforce Platform Event
- description: ''
  name: PlatformEventPublishMessage
  summary: Payload structure for publishing a Platform Event via REST API
  title: Platform Event Publish Payload
name: Salesforce Platform Events API
provider_name: Salesforce
provider_slug: salesforce
servers:
- description: CometD endpoint for subscribing to Platform Events
  name: salesforce-cometd
  protocol: https
  url: https://{instanceName}.salesforce.com/cometd/{apiVersion}
- description: Pub/Sub API gRPC endpoint (recommended for high-throughput subscriptions)
  name: salesforce-pubsub
  protocol: grpc
  url: api.pubsub.salesforce.com:443
slug: salesforce-platform-events-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Salesforce Platform Events API\n  description: >-\n    Salesforce Platform Events enables event-driven integration architectures\n    on the Salesforce platform. Developers define custom event types as Salesforce\n    objects with the __e suffix and publish or subscribe to events using the REST\n    API, Apex triggers, or CometD subscriptions. Events are durable and stored for\n    72 hours, supporting replay for missed events.\n  version: '59.0'\n  contact:\n    name: Salesforce Developer Support\n    url: https://developer.salesforce.com/docs/atlas.en-us.platform_events.meta/platform_events/\n  termsOfService: https://www.salesforce.com/company/legal/agreements/\nservers:\n  salesforce-cometd:\n    url: 'https://{instanceName}.salesforce.com/cometd/{apiVersion}'\n    protocol: https\n    description: CometD endpoint for subscribing to Platform Events\n    variables:\n      instanceName:\n        description: Salesforce org instance name or\
  \ custom domain\n        default: myorg\n      apiVersion:\n        description: Salesforce API version\n        default: '59.0'\n    security:\n      - oauthAccessToken: []\n  salesforce-pubsub:\n    url: 'api.pubsub.salesforce.com:443'\n    protocol: grpc\n    description: Pub/Sub API gRPC endpoint (recommended for high-throughput subscriptions)\n    security:\n      - oauthAccessToken: []\nchannels:\n  /event/{platformEventApiName}:\n    description: >-\n      CometD channel for subscribing to a Platform Event type. Receives events\n      published to this event type from Apex triggers, flows, REST API calls,\n      or external systems via the REST API.\n    parameters:\n      platformEventApiName:\n        description: >-\n          The API name of the Platform Event object including the __e suffix\n          (e.g., Order_Event__e, Low_Ink__e)\n        schema:\n          type: string\n          pattern: '^[a-zA-Z][a-zA-Z0-9_]*__e$'\n          examples:\n            - Order_Event__e\n\
  \            - Low_Ink__e\n    subscribe:\n      operationId: receivePlatformEvent\n      summary: Receive a Platform Event notification\n      description: >-\n        Fired when a Platform Event of this type is published. Includes the\n        event payload fields defined in the custom Platform Event object definition\n        plus system-generated metadata fields.\n      message:\n        $ref: '#/components/messages/PlatformEventMessage'\n    publish:\n      operationId: publishPlatformEvent\n      summary: Publish a Platform Event via CometD (internal use)\n      description: >-\n        Platform Events are typically published via the Salesforce REST API\n        (POST to /sobjects/{EventApiName__e}) or from Apex code. This represents\n        the event structure for publishing.\n      message:\n        $ref: '#/components/messages/PlatformEventPublishMessage'\ncomponents:\n  securitySchemes:\n    oauthAccessToken:\n      type: oauth2\n      description: Salesforce OAuth 2.0 Connected\
  \ App access token\n      flows:\n        authorizationCode:\n          authorizationUrl: https://login.salesforce.com/services/oauth2/authorize\n          tokenUrl: https://login.salesforce.com/services/oauth2/token\n          scopes:\n            api: Access and manage Salesforce data\n            event_api: Subscribe and publish Platform Events\n  messages:\n    PlatformEventMessage:\n      name: PlatformEventMessage\n      title: Salesforce Platform Event\n      summary: A Platform Event notification received via CometD\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PlatformEventEnvelope'\n    PlatformEventPublishMessage:\n      name: PlatformEventPublish\n      title: Platform Event Publish Payload\n      summary: Payload structure for publishing a Platform Event via REST API\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PlatformEventPublishPayload'\n  schemas:\n    PlatformEventEnvelope:\n    \
  \  type: object\n      description: The CometD envelope wrapping a received Platform Event\n      properties:\n        channel:\n          type: string\n          description: CometD channel path\n          examples:\n            - /event/Low_Ink__e\n        data:\n          type: object\n          description: Event data container\n          properties:\n            schema:\n              type: string\n              description: The Avro schema ID for this event type version\n            event:\n              $ref: '#/components/schemas/PlatformEventData'\n            payload:\n              type: object\n              description: >-\n                The event payload containing the custom fields defined on\n                the Platform Event object, plus standard fields.\n              additionalProperties: true\n    PlatformEventData:\n      type: object\n      description: Event metadata\n      properties:\n        replayId:\n          type: integer\n          description: >-\n  \
  \          Durable replay ID. Use -1 to replay from the earliest retained event,\n            -2 for only new events, or a specific replayId to replay from that point.\n        createdDate:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp when the event was published\n        createdById:\n          type: string\n          description: Salesforce user ID of the publisher\n    PlatformEventPublishPayload:\n      type: object\n      description: >-\n        Payload for publishing a Platform Event via POST to\n        /services/data/v{version}/sobjects/{EventApiName__e}\n      properties:\n        CreatedDate:\n          type: string\n          format: date-time\n          description: Optional publication timestamp. Defaults to current time.\n        CreatedById:\n          type: string\n          description: Optional publisher identity override (requires special permission)\n      additionalProperties:\n        description: Custom fields defined\
  \ on the Platform Event object (field API names)\n        oneOf:\n          - type: string\n          - type: number\n          - type: boolean\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/asyncapi/salesforce-platform-events-asyncapi.yml
spec_file: asyncapi/salesforce-platform-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/asyncapi/salesforce-platform-events-asyncapi.yml
tags:
- AI
- Analytics
- Cloud
- Commerce
- CRM
- Customer Service
- Enterprise
- Marketing
- Platform
- Sales
- AsyncAPI
- Webhooks
- Events
version: '59.0'
---
