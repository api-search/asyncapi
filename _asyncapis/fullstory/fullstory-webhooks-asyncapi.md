---
api_specs:
- filename: fullstory-server-api-openapi.yml
  format: yaml
  label: FullStory Server API
  slug: fullstory-server-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/fullstory/refs/heads/main/openapi/fullstory-server-api-openapi.yml
- filename: fullstory-sessions-api-openapi.yml
  format: yaml
  label: FullStory Sessions API
  slug: fullstory-sessions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/fullstory/refs/heads/main/openapi/fullstory-sessions-api-openapi.yml
- filename: fullstory-segments-export-api-openapi.yml
  format: yaml
  label: FullStory Segments Export API
  slug: fullstory-segments-export-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/fullstory/refs/heads/main/openapi/fullstory-segments-export-api-openapi.yml
- filename: fullstory-webhooks-api-openapi.yml
  format: yaml
  label: FullStory Webhooks API
  slug: fullstory-webhooks-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/fullstory/refs/heads/main/openapi/fullstory-webhooks-api-openapi.yml
channels:
- description: Channel for all FullStory webhook event deliveries. Events are sent as HTTP POST requests to the configured endpoint URL with a JSON payload containing the event name, version, and event-specific data.
  name: /webhook
  operation: publish
  operation_id: receiveWebhookEvent
  summary: Receive webhook event notifications from FullStory
description: FullStory delivers real-time webhook notifications when specific events occur within the platform. Supported event types include segment creation, segment threshold alerts, custom event processing, and note creation. Webhooks enable event-driven integrations that respond immediately to behavioral signals detected by FullStory, eliminating the need for polling. Payloads are signed with a shared secret for verification.
layout: asyncapi
messages:
- description: ''
  name: SegmentCreated
  summary: Sent when a FullStory user creates a new segment in the platform
  title: Segment Created
- description: ''
  name: SegmentTrendAlert
  summary: Sent when a segment-based alert triggers because the active users in a saved segment cross a configured threshold
  title: Segment Threshold Alert
- description: ''
  name: CustomEvent
  summary: Sent when a custom event has been processed. Custom events are created during recording via the FS.event Browser API function.
  title: Custom Event Processed
- description: ''
  name: NoteCreated
  summary: Sent when a note is created in FullStory on a session recording
  title: Note Created
name: FullStory Webhook Events
provider_name: FullStory
provider_slug: fullstory
servers:
- description: The HTTPS endpoint configured to receive FullStory webhook events. This URL is set when creating a webhook endpoint via the Webhooks API.
  name: webhookReceiver
  protocol: https
  url: '{webhookUrl}'
slug: fullstory-webhooks-asyncapi
source_filename: fullstory-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: FullStory Webhook Events\n  description: >-\n    FullStory delivers real-time webhook notifications when specific events\n    occur within the platform. Supported event types include segment creation,\n    segment threshold alerts, custom event processing, and note creation.\n    Webhooks enable event-driven integrations that respond immediately to\n    behavioral signals detected by FullStory, eliminating the need for polling.\n    Payloads are signed with a shared secret for verification.\n  version: '1.0'\n  contact:\n    name: FullStory Support\n    url: https://help.fullstory.com/\nservers:\n  webhookReceiver:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      The HTTPS endpoint configured to receive FullStory webhook events.\n      This URL is set when creating a webhook endpoint via the Webhooks API.\n    variables:\n      webhookUrl:\n        description: >-\n          The destination URL configured for the webhook\
  \ endpoint\n    security:\n      - signingSecret: []\nchannels:\n  /webhook:\n    description: >-\n      Channel for all FullStory webhook event deliveries. Events are sent\n      as HTTP POST requests to the configured endpoint URL with a JSON\n      payload containing the event name, version, and event-specific data.\n    publish:\n      operationId: receiveWebhookEvent\n      summary: Receive webhook event notifications from FullStory\n      message:\n        oneOf:\n          - $ref: '#/components/messages/SegmentCreated'\n          - $ref: '#/components/messages/SegmentTrendAlert'\n          - $ref: '#/components/messages/CustomEvent'\n          - $ref: '#/components/messages/NoteCreated'\ncomponents:\n  securitySchemes:\n    signingSecret:\n      type: httpApiKey\n      name: X-FS-Signature\n      in: header\n      description: >-\n        Webhook payloads are signed using the signing secret configured for\n        the endpoint. The signature is included in the request headers for\n\
  \        verification by the receiving application.\n  messages:\n    SegmentCreated:\n      name: segment.created\n      title: Segment Created\n      summary: >-\n        Sent when a FullStory user creates a new segment in the platform\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SegmentCreatedPayload'\n    SegmentTrendAlert:\n      name: segment.trend.alert\n      title: Segment Threshold Alert\n      summary: >-\n        Sent when a segment-based alert triggers because the active users\n        in a saved segment cross a configured threshold\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SegmentTrendAlertPayload'\n    CustomEvent:\n      name: recording.event.custom\n      title: Custom Event Processed\n      summary: >-\n        Sent when a custom event has been processed. Custom events are\n        created during recording via the FS.event Browser API function.\n      contentType: application/json\n\
  \      payload:\n        $ref: '#/components/schemas/CustomEventPayload'\n    NoteCreated:\n      name: note.created\n      title: Note Created\n      summary: >-\n        Sent when a note is created in FullStory on a session recording\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/NoteCreatedPayload'\n  schemas:\n    SegmentCreatedPayload:\n      type: object\n      description: >-\n        Payload delivered when a new segment is created in FullStory\n      properties:\n        eventName:\n          type: string\n          const: segment.created\n          description: >-\n            The event type identifier\n        version:\n          type: integer\n          description: >-\n            Schema version of the event payload\n        data:\n          type: object\n          description: >-\n            Event-specific data for the segment creation\n          properties:\n            id:\n              type: string\n              description:\
  \ >-\n                Unique identifier for the created segment\n            creator:\n              type: string\n              format: email\n              description: >-\n                Email address of the FullStory user who created the segment\n            name:\n              type: string\n              description: >-\n                Display name of the created segment\n            url:\n              type: string\n              format: uri\n              description: >-\n                URL to view the segment in the FullStory application\n            created:\n              type: string\n              format: date-time\n              description: >-\n                ISO 8601 timestamp when the segment was created\n    SegmentTrendAlertPayload:\n      type: object\n      description: >-\n        Payload delivered when a segment-based threshold alert triggers\n      properties:\n        eventName:\n          type: string\n          const: segment.trend.alert\n          description:\
  \ >-\n            The event type identifier\n        version:\n          type: integer\n          description: >-\n            Schema version of the event payload\n        data:\n          type: object\n          description: >-\n            Event-specific data for the segment threshold alert\n          properties:\n            id:\n              type: string\n              description: >-\n                Unique identifier for the alert\n            timestamp:\n              type: string\n              format: date-time\n              description: >-\n                ISO 8601 timestamp when the alert triggered\n            value:\n              type: number\n              description: >-\n                The observed value that triggered the alert\n            notificationUrl:\n              type: string\n              format: uri\n              description: >-\n                URL to view the alert notification in FullStory\n            alertConfig:\n              type: object\n    \
  \          description: >-\n                Configuration details of the alert that triggered\n              properties:\n                description:\n                  type: string\n                  description: >-\n                    Human-readable description of the alert condition\n                threshold:\n                  type: number\n                  description: >-\n                    The configured threshold value\n                direction:\n                  type: string\n                  description: >-\n                    Whether the alert triggers when value goes above or below\n                    the threshold\n                  enum:\n                    - ABOVE\n                    - BELOW\n                duration:\n                  type: string\n                  description: >-\n                    The time window for measuring active users\n                  enum:\n                    - DAILY\n                    - WEEKLY\n                    - MONTHLY\n\
  \                alertUrl:\n                  type: string\n                  format: uri\n                  description: >-\n                    URL to view the alert configuration in FullStory\n                alertCreator:\n                  type: string\n                  format: email\n                  description: >-\n                    Email address of the user who created the alert\n                segmentUrl:\n                  type: string\n                  format: uri\n                  description: >-\n                    URL to view the associated segment in FullStory\n    CustomEventPayload:\n      type: object\n      description: >-\n        Payload delivered when a custom event is processed in FullStory\n      properties:\n        eventName:\n          type: string\n          const: recording.event.custom\n          description: >-\n            The event type identifier\n        version:\n          type: integer\n          description: >-\n            Schema version\
  \ of the event payload\n        data:\n          type: object\n          description: >-\n            Event-specific data for the custom event\n          properties:\n            name:\n              type: string\n              description: >-\n                The name of the custom event as defined via FS.event\n            sessionUrl:\n              type: string\n              format: uri\n              description: >-\n                URL to view the session replay in FullStory\n            properties:\n              type: object\n              description: >-\n                Custom properties attached to the event\n              additionalProperties: true\n    NoteCreatedPayload:\n      type: object\n      description: >-\n        Payload delivered when a note is created on a session recording\n      properties:\n        eventName:\n          type: string\n          const: note.created\n          description: >-\n            The event type identifier\n        version:\n          type:\
  \ integer\n          description: >-\n            Schema version of the event payload\n        data:\n          type: object\n          description: >-\n            Event-specific data for the note creation\n          properties:\n            id:\n              type: string\n              description: >-\n                Unique identifier for the note\n            creator:\n              type: string\n              format: email\n              description: >-\n                Email address of the user who created the note\n            sessionUrl:\n              type: string\n              format: uri\n              description: >-\n                URL to the session replay where the note was created\n            created:\n              type: string\n              format: date-time\n              description: >-\n                ISO 8601 timestamp when the note was created\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/fullstory/refs/heads/main/asyncapi/fullstory-webhooks-asyncapi.yml
spec_file: asyncapi/fullstory-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/fullstory/refs/heads/main/asyncapi/fullstory-webhooks-asyncapi.yml
tags:
- Session Replay
- Product Analytics
- Digital Experience
- Behavioral Analytics
- Frontend Monitoring
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
