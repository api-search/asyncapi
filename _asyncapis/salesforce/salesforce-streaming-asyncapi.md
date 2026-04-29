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
- description: Channel for subscribing to a PushTopic that monitors SOQL-defined record changes. Receives events when records matching the PushTopic query are created, updated, deleted, or undeleted in Salesforce.
  name: /topic/{pushTopicName}
  operation: subscribe
  operation_id: receivePushTopicEvent
  summary: Receive a PushTopic record change event
- description: Channel for subscribing to a Generic Streaming channel. Receives custom events published to this channel by Salesforce Apex or REST API calls.
  name: /u/{streamingChannelName}
  operation: subscribe
  operation_id: receiveGenericStreamingEvent
  summary: Receive a generic streaming event
description: The Salesforce Streaming API uses a publish-subscribe model based on Bayeux/CometD to push near-real-time event notifications to subscribed clients. It supports PushTopic events (triggered by SOQL queries on record changes) and Generic Streaming events (custom notifications). Clients connect via long-polling over HTTPS to receive events as they occur.
layout: asyncapi
messages:
- description: ''
  name: PushTopicEvent
  summary: Notification of a Salesforce record change matching a PushTopic query
  title: Salesforce PushTopic Record Change Event
- description: ''
  name: GenericStreamingEvent
  summary: Custom event published to a Generic Streaming channel
  title: Salesforce Generic Streaming Event
name: Salesforce Streaming API
provider_name: Salesforce
provider_slug: salesforce
servers:
- description: Salesforce CometD streaming endpoint
  name: salesforce
  protocol: https
  url: https://{instanceName}.salesforce.com/cometd/{apiVersion}
slug: salesforce-streaming-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Salesforce Streaming API\n  description: >-\n    The Salesforce Streaming API uses a publish-subscribe model based on\n    Bayeux/CometD to push near-real-time event notifications to subscribed\n    clients. It supports PushTopic events (triggered by SOQL queries on record\n    changes) and Generic Streaming events (custom notifications). Clients\n    connect via long-polling over HTTPS to receive events as they occur.\n  version: '44.0'\n  contact:\n    name: Salesforce Developer Support\n    url: https://developer.salesforce.com/developer-centers/integration-apis\n  termsOfService: https://www.salesforce.com/company/legal/agreements/\nservers:\n  salesforce:\n    url: 'https://{instanceName}.salesforce.com/cometd/{apiVersion}'\n    protocol: https\n    description: Salesforce CometD streaming endpoint\n    variables:\n      instanceName:\n        description: Your Salesforce org instance (e.g., na1, eu3, or mydomain)\n        default: myorg\n\
  \      apiVersion:\n        description: Salesforce API version\n        default: '59.0'\n    security:\n      - oauthAccessToken: []\nchannels:\n  /topic/{pushTopicName}:\n    description: >-\n      Channel for subscribing to a PushTopic that monitors SOQL-defined record\n      changes. Receives events when records matching the PushTopic query are\n      created, updated, deleted, or undeleted in Salesforce.\n    parameters:\n      pushTopicName:\n        description: The developer name of the PushTopic to subscribe to\n        schema:\n          type: string\n          examples:\n            - InvoiceStatementUpdates\n            - OpportunityUpdates\n    subscribe:\n      operationId: receivePushTopicEvent\n      summary: Receive a PushTopic record change event\n      description: >-\n        Fired when a Salesforce record change matches the SOQL query defined\n        in the PushTopic. The event payload includes the changed record data\n        and change metadata.\n      message:\n\
  \        $ref: '#/components/messages/PushTopicEvent'\n  /u/{streamingChannelName}:\n    description: >-\n      Channel for subscribing to a Generic Streaming channel. Receives\n      custom events published to this channel by Salesforce Apex or REST API calls.\n    parameters:\n      streamingChannelName:\n        description: The developer name of the Generic Streaming channel\n        schema:\n          type: string\n    subscribe:\n      operationId: receiveGenericStreamingEvent\n      summary: Receive a generic streaming event\n      description: >-\n        Fired when an event is published to a Generic Streaming channel via\n        the Salesforce REST API or Apex code.\n      message:\n        $ref: '#/components/messages/GenericStreamingEvent'\ncomponents:\n  securitySchemes:\n    oauthAccessToken:\n      type: oauth2\n      description: Salesforce OAuth 2.0 access token\n      flows:\n        authorizationCode:\n          authorizationUrl: https://login.salesforce.com/services/oauth2/authorize\n\
  \          tokenUrl: https://login.salesforce.com/services/oauth2/token\n          scopes:\n            api: Access and manage Salesforce data\n  messages:\n    PushTopicEvent:\n      name: PushTopicEvent\n      title: Salesforce PushTopic Record Change Event\n      summary: Notification of a Salesforce record change matching a PushTopic query\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PushTopicEventPayload'\n    GenericStreamingEvent:\n      name: GenericStreamingEvent\n      title: Salesforce Generic Streaming Event\n      summary: Custom event published to a Generic Streaming channel\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/GenericStreamingEventPayload'\n  schemas:\n    PushTopicEventPayload:\n      type: object\n      description: The envelope delivered to CometD subscribers for PushTopic events\n      properties:\n        channel:\n          type: string\n          description: The CometD\
  \ channel the event was received on\n          examples:\n            - /topic/InvoiceStatementUpdates\n        clientId:\n          type: string\n          description: The CometD client ID of the subscriber\n        data:\n          type: object\n          description: The event data container\n          properties:\n            event:\n              type: object\n              description: Metadata about the record change event\n              properties:\n                type:\n                  type: string\n                  description: The type of DML operation that triggered the event\n                  enum:\n                    - created\n                    - updated\n                    - deleted\n                    - undeleted\n                replayId:\n                  type: integer\n                  description: >-\n                    Monotonically increasing replay ID used to replay missed events.\n                    Use -1 to replay all retained events or -2 for\
  \ only new events.\n            sobject:\n              type: object\n              description: >-\n                The Salesforce record fields returned, based on the fields\n                in the PushTopic SOQL query\n              additionalProperties: true\n    GenericStreamingEventPayload:\n      type: object\n      description: The envelope for Generic Streaming channel events\n      properties:\n        channel:\n          type: string\n          description: The CometD channel path\n          examples:\n            - /u/BroadcastChannel\n        clientId:\n          type: string\n        data:\n          type: object\n          properties:\n            event:\n              type: object\n              properties:\n                replayId:\n                  type: integer\n                  description: Replay ID for event replay\n            payload:\n              type: string\n              description: Application-defined JSON string payload (max 10,000 characters)\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/asyncapi/salesforce-streaming-asyncapi.yml
spec_file: asyncapi/salesforce-streaming-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/asyncapi/salesforce-streaming-asyncapi.yml
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
version: '44.0'
---
