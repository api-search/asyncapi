---
api_specs:
- filename: fauna-core-http-api-openapi.yml
  format: yaml
  label: Fauna Core HTTP API
  slug: core-http-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/fauna/refs/heads/main/openapi/fauna-core-http-api-openapi.yml
- filename: fauna-event-streaming-asyncapi.yml
  format: yaml
  label: Fauna Event Streaming API
  slug: event-streaming-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/fauna/refs/heads/main/asyncapi/fauna-event-streaming-asyncapi.yml
- filename: fauna-graphql-api-openapi.yml
  format: yaml
  label: Fauna GraphQL API
  slug: graphql-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/fauna/refs/heads/main/openapi/fauna-graphql-api-openapi.yml
channels:
- description: Event stream channel for real-time change data capture. Clients send a POST request with an event source token to open a persistent connection. Fauna pushes events through the open connection as changes occur in the subscribed document or set. The connection remains open until closed by the client or server. If a tracked change occurs, the event source emits a related add, remove, or update event.
  name: /stream/1
  operation: publish
  operation_id: receiveStreamEvents
  summary: Receive real-time change events
description: The Fauna Event Streaming API enables real-time change data capture by maintaining an open connection to the Fauna database and pushing events to clients as they occur. Developers can subscribe to document or set changes and receive add, remove, and update events in real time. The API supports reconnection with a start timestamp or cursor to avoid missing events during disconnections. It is accessible via the /stream/1 HTTP endpoint with token-based authentication.
layout: asyncapi
messages:
- description: ''
  name: StreamSubscription
  summary: Request to open an event stream connection.
  title: Stream Subscription Request
- description: ''
  name: StatusEvent
  summary: Heartbeat or connection status event sent when the stream is opened or periodically to keep the connection alive.
  title: Status Event
- description: ''
  name: AddEvent
  summary: Event emitted when a new document is added to the tracked set or a document begins matching the tracked criteria.
  title: Add Event
- description: ''
  name: RemoveEvent
  summary: Event emitted when a document is removed from the tracked set or a document stops matching the tracked criteria.
  title: Remove Event
- description: ''
  name: UpdateEvent
  summary: Event emitted when a tracked document is updated.
  title: Update Event
name: Fauna Event Streaming
provider_name: fauna
provider_slug: fauna
servers:
- description: Fauna Global Production Server. The /stream/1 endpoint maintains a persistent HTTP connection that pushes events as server-sent data.
  name: production
  protocol: https
  url: https://db.fauna.com
slug: fauna-event-streaming-asyncapi
source_filename: fauna-event-streaming-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Fauna Event Streaming\n  description: >-\n    The Fauna Event Streaming API enables real-time change data capture by\n    maintaining an open connection to the Fauna database and pushing events\n    to clients as they occur. Developers can subscribe to document or set\n    changes and receive add, remove, and update events in real time. The API\n    supports reconnection with a start timestamp or cursor to avoid missing\n    events during disconnections. It is accessible via the /stream/1 HTTP\n    endpoint with token-based authentication.\n  version: '1'\n  contact:\n    name: Fauna Support\n    url: https://support.fauna.com\n  license:\n    name: Proprietary\n    url: https://fauna.com/terms\n  externalDocs:\n    description: Fauna Event Streaming Documentation\n    url: https://docs.fauna.com/fauna/current/reference/streaming/\nservers:\n  production:\n    url: https://db.fauna.com\n    protocol: https\n    description: >-\n      Fauna Global\
  \ Production Server. The /stream/1 endpoint maintains a\n      persistent HTTP connection that pushes events as server-sent data.\n    security:\n      - bearerAuth: []\nchannels:\n  /stream/1:\n    description: >-\n      Event stream channel for real-time change data capture. Clients send\n      a POST request with an event source token to open a persistent\n      connection. Fauna pushes events through the open connection as changes\n      occur in the subscribed document or set. The connection remains open\n      until closed by the client or server. If a tracked change occurs, the\n      event source emits a related add, remove, or update event.\n    publish:\n      operationId: receiveStreamEvents\n      summary: Receive real-time change events\n      description: >-\n        Events pushed from Fauna to the client through the open stream\n        connection. Events include document additions, removals, updates,\n        and periodic status heartbeats. Each event includes a transaction\n\
  \        timestamp and cursor for reconnection support.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/StatusEvent'\n          - $ref: '#/components/messages/AddEvent'\n          - $ref: '#/components/messages/RemoveEvent'\n          - $ref: '#/components/messages/UpdateEvent'\n    subscribe:\n      operationId: subscribeToStream\n      summary: Subscribe to an event stream\n      description: >-\n        Client sends a subscription request containing an event source token\n        obtained from an FQL query. Optional parameters include start_ts for\n        reconnecting from a specific timestamp and cursor for resuming from\n        a specific event position.\n      message:\n        $ref: '#/components/messages/StreamSubscription'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: http\n      scheme: bearer\n      description: >-\n        Fauna authentication secret passed as a bearer token in the\n        Authorization header of the initial HTTP\
  \ request.\n  messages:\n    StreamSubscription:\n      name: StreamSubscription\n      title: Stream Subscription Request\n      summary: >-\n        Request to open an event stream connection.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/StreamSubscriptionPayload'\n    StatusEvent:\n      name: StatusEvent\n      title: Status Event\n      summary: >-\n        Heartbeat or connection status event sent when the stream is opened\n        or periodically to keep the connection alive.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/StatusEventPayload'\n    AddEvent:\n      name: AddEvent\n      title: Add Event\n      summary: >-\n        Event emitted when a new document is added to the tracked set or\n        a document begins matching the tracked criteria.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AddEventPayload'\n    RemoveEvent:\n      name: RemoveEvent\n\
  \      title: Remove Event\n      summary: >-\n        Event emitted when a document is removed from the tracked set or\n        a document stops matching the tracked criteria.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/RemoveEventPayload'\n    UpdateEvent:\n      name: UpdateEvent\n      title: Update Event\n      summary: >-\n        Event emitted when a tracked document is updated.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/UpdateEventPayload'\n  schemas:\n    StreamSubscriptionPayload:\n      type: object\n      required:\n        - token\n      properties:\n        token:\n          type: string\n          description: >-\n            Event source token obtained from an FQL query that returns an\n            event source. The token identifies the document or set to track.\n        start_ts:\n          type: integer\n          format: int64\n          description: >-\n            Optional\
  \ start timestamp in microseconds since the Unix epoch.\n            Fauna will replay events that occurred after this timestamp.\n            The period between stream restart and start_ts cannot exceed\n            the history_days value for the source collection. Mutually\n            exclusive with cursor.\n        cursor:\n          type: string\n          description: >-\n            Optional cursor from a previous event for resuming the stream.\n            Used to restart a stream from a specific event position without\n            missing events. Mutually exclusive with start_ts.\n    StatusEventPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: status\n          description: >-\n            Event type identifier.\n        txn_ts:\n          type: integer\n          format: int64\n          description: >-\n            Transaction timestamp in microseconds since the Unix epoch.\n        cursor:\n          type: string\n   \
  \       description: >-\n            Cursor position for this event, used for reconnection.\n        stats:\n          $ref: '#/components/schemas/StreamStats'\n    AddEventPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: add\n          description: >-\n            Event type identifier.\n        txn_ts:\n          type: integer\n          format: int64\n          description: >-\n            Transaction timestamp of the change.\n        cursor:\n          type: string\n          description: >-\n            Cursor position for this event.\n        data:\n          type: object\n          additionalProperties: true\n          description: >-\n            The full document data that was added.\n        stats:\n          $ref: '#/components/schemas/StreamStats'\n    RemoveEventPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: remove\n          description: >-\n            Event\
  \ type identifier.\n        txn_ts:\n          type: integer\n          format: int64\n          description: >-\n            Transaction timestamp of the change.\n        cursor:\n          type: string\n          description: >-\n            Cursor position for this event.\n        data:\n          type: object\n          additionalProperties: true\n          description: >-\n            The document data that was removed.\n        stats:\n          $ref: '#/components/schemas/StreamStats'\n    UpdateEventPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: update\n          description: >-\n            Event type identifier.\n        txn_ts:\n          type: integer\n          format: int64\n          description: >-\n            Transaction timestamp of the change.\n        cursor:\n          type: string\n          description: >-\n            Cursor position for this event.\n        data:\n          type: object\n          additionalProperties:\
  \ true\n          description: >-\n            The updated document data.\n        stats:\n          $ref: '#/components/schemas/StreamStats'\n    StreamStats:\n      type: object\n      description: >-\n        Operational statistics for the event.\n      properties:\n        read_ops:\n          type: integer\n          description: >-\n            Number of Transactional Read Operations consumed.\n        storage_bytes_read:\n          type: integer\n          description: >-\n            Number of bytes read from storage.\n        compute_ops:\n          type: integer\n          description: >-\n            Number of Transactional Compute Operations consumed.\n        processing_time_ms:\n          type: integer\n          description: >-\n            Processing time in milliseconds.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/fauna/refs/heads/main/asyncapi/fauna-event-streaming-asyncapi.yml
spec_file: asyncapi/fauna-event-streaming-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/fauna/refs/heads/main/asyncapi/fauna-event-streaming-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '1'
---
