---
api_specs:
- filename: supabase-management-api-openapi.yml
  format: yaml
  label: Supabase Management API
  slug: management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/openapi/supabase-management-api-openapi.yml
- filename: supabase-auth-api-openapi.yml
  format: yaml
  label: Supabase Auth API
  slug: auth-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/openapi/supabase-auth-api-openapi.yml
- filename: supabase-storage-api-openapi.yml
  format: yaml
  label: Supabase Storage API
  slug: storage-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/openapi/supabase-storage-api-openapi.yml
- filename: supabase-database-rest-api-openapi.yml
  format: yaml
  label: Supabase Database REST API
  slug: database-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/openapi/supabase-database-rest-api-openapi.yml
- filename: supabase-edge-functions-api-openapi.yml
  format: yaml
  label: Supabase Edge Functions API
  slug: edge-functions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/openapi/supabase-edge-functions-api-openapi.yml
- filename: supabase-realtime-api-asyncapi.yml
  format: yaml
  label: Supabase Realtime API
  slug: realtime-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/asyncapi/supabase-realtime-api-asyncapi.yml
channels:
- description: A Realtime channel identified by a topic string. Clients join a channel by sending a phx_join message with configuration for the desired features (postgres_changes, broadcast, presence). Multiple features can be configured on a single channel.
  name: realtime/{topic}
  operation: publish
  operation_id: sendRealtimeMessages
  summary: Send messages to a channel
description: 'The Supabase Realtime API enables real-time communication over WebSocket connections using the Phoenix Channel protocol (v2). It supports three main features: Postgres Changes for subscribing to INSERT, UPDATE, and DELETE events on database tables; Broadcast for sending ephemeral messages between connected clients on a channel; and Presence for tracking and synchronizing shared state across clients such as online status indicators. Row Level Security policies are enforced for Postgres Changes to ensure authorized access to real-time data. Messages use JSON-encoded text frames except for Broadcast which also supports binary frames.'
layout: asyncapi
messages:
- description: 'The initial message required to join a channel. Contains configuration for which features to enable: postgres_changes (database event subscriptions), broadcast (client-to-client messaging), and presence (shared state tracking). An access_token can be included for authenticated access.'
  name: PhxJoin
  summary: Join a Realtime channel with feature configuration
  title: Join Channel
- description: Sent by the client to leave a channel and stop receiving messages for its subscriptions.
  name: PhxLeave
  summary: Leave a Realtime channel
  title: Leave Channel
- description: Sent by the server when a database change occurs in a subscribed schema and table. Contains the event type (INSERT, UPDATE, DELETE), the affected table, and the new and old record data. Row Level Security policies determine which clients receive each change.
  name: PostgresChange
  summary: Database change notification
  title: Postgres Change Event
- description: Sent by the server to all clients subscribed to a channel when another client broadcasts a message. Messages are ephemeral and not persisted.
  name: BroadcastMessage
  summary: Ephemeral message broadcast to channel clients
  title: Broadcast Message
- description: Sent by a client to broadcast an ephemeral message to all other clients connected to the same channel.
  name: BroadcastSend
  summary: Broadcast a message to channel clients
  title: Send Broadcast
- description: Sent by the server after joining a channel with presence enabled. Contains the complete presence state of all tracked clients in the channel, backed by a CRDT for consistency across nodes.
  name: PresenceState
  summary: Full presence state for the channel
  title: Presence State
- description: Sent by the server when the presence state changes due to clients joining or leaving. Contains the joins and leaves since the last update.
  name: PresenceDiff
  summary: Incremental presence state change
  title: Presence Diff
- description: Sent by a client to register its presence state in the channel. The payload contains arbitrary metadata to be tracked and shared with other clients.
  name: PresenceTrack
  summary: Start tracking client presence
  title: Track Presence
- description: Sent by a client to remove its presence state from the channel.
  name: PresenceUntrack
  summary: Stop tracking client presence
  title: Untrack Presence
- description: Sent by the server in response to client messages such as phx_join, broadcast, and presence operations. Contains the status of the operation and any response data.
  name: SystemReply
  summary: Server reply to client messages
  title: System Reply
- description: Sent by the server in response to a client heartbeat to confirm the connection is alive.
  name: Heartbeat
  summary: Server heartbeat reply
  title: Heartbeat Reply
- description: Sent periodically by the client (typically every 30 seconds) to keep the WebSocket connection alive and prevent server-side timeout.
  name: HeartbeatSend
  summary: Client heartbeat to keep connection alive
  title: Send Heartbeat
name: Supabase Realtime API
provider_name: Supabase
provider_slug: supabase
servers:
- description: Supabase Realtime WebSocket server. Connect with the apikey query parameter containing your project anon key.
  name: supabaseRealtime
  protocol: wss
  url: wss://{project_ref}.supabase.co/realtime/v1/websocket
slug: supabase-realtime-api-asyncapi
source_filename: supabase-realtime-api-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Supabase Realtime API\n  description: >-\n    The Supabase Realtime API enables real-time communication over WebSocket\n    connections using the Phoenix Channel protocol (v2). It supports three\n    main features: Postgres Changes for subscribing to INSERT, UPDATE, and\n    DELETE events on database tables; Broadcast for sending ephemeral messages\n    between connected clients on a channel; and Presence for tracking and\n    synchronizing shared state across clients such as online status indicators.\n    Row Level Security policies are enforced for Postgres Changes to ensure\n    authorized access to real-time data. Messages use JSON-encoded text frames\n    except for Broadcast which also supports binary frames.\n  version: '2.0.0'\n  contact:\n    name: Supabase Support\n    url: https://supabase.com/support\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\nservers:\n  supabaseRealtime:\n    url: 'wss://{project_ref}.supabase.co/realtime/v1/websocket'\n\
  \    protocol: wss\n    description: >-\n      Supabase Realtime WebSocket server. Connect with the apikey query\n      parameter containing your project anon key.\n    variables:\n      project_ref:\n        description: Your Supabase project reference ID\n    security:\n      - apiKeyQuery: []\nchannels:\n  realtime/{topic}:\n    description: >-\n      A Realtime channel identified by a topic string. Clients join a channel\n      by sending a phx_join message with configuration for the desired\n      features (postgres_changes, broadcast, presence). Multiple features\n      can be configured on a single channel.\n    parameters:\n      topic:\n        description: >-\n          The channel topic identifier. For Postgres Changes, this typically\n          follows the pattern realtime:schema:table. For Broadcast and\n          Presence, any unique string can be used.\n        schema:\n          type: string\n    subscribe:\n      operationId: receiveRealtimeMessages\n      summary: Receive\
  \ real-time messages from a channel\n      description: >-\n        After joining a channel, the client receives messages for all\n        subscribed events including database changes, broadcast messages,\n        presence state changes, and system events.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/PostgresChange'\n          - $ref: '#/components/messages/BroadcastMessage'\n          - $ref: '#/components/messages/PresenceState'\n          - $ref: '#/components/messages/PresenceDiff'\n          - $ref: '#/components/messages/SystemReply'\n          - $ref: '#/components/messages/Heartbeat'\n    publish:\n      operationId: sendRealtimeMessages\n      summary: Send messages to a channel\n      description: >-\n        Clients send messages to join channels, broadcast to other clients,\n        track presence state, and maintain the connection heartbeat.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/PhxJoin'\n          - $ref: '#/components/messages/BroadcastSend'\n\
  \          - $ref: '#/components/messages/PresenceTrack'\n          - $ref: '#/components/messages/PresenceUntrack'\n          - $ref: '#/components/messages/PhxLeave'\n          - $ref: '#/components/messages/HeartbeatSend'\ncomponents:\n  securitySchemes:\n    apiKeyQuery:\n      type: apiKey\n      in: query\n      name: apikey\n      description: >-\n        Supabase project anon API key passed as a query parameter on the\n        WebSocket connection URL.\n    bearerToken:\n      type: http\n      scheme: bearer\n      bearerFormat: JWT\n      description: >-\n        JWT access token passed in the access_token field of the phx_join\n        payload for authenticated channel access.\n  messages:\n    PhxJoin:\n      name: phx_join\n      title: Join Channel\n      summary: Join a Realtime channel with feature configuration\n      description: >-\n        The initial message required to join a channel. Contains configuration\n        for which features to enable: postgres_changes (database\
  \ event\n        subscriptions), broadcast (client-to-client messaging), and presence\n        (shared state tracking). An access_token can be included for\n        authenticated access.\n      payload:\n        $ref: '#/components/schemas/PhxJoinPayload'\n    PhxLeave:\n      name: phx_leave\n      title: Leave Channel\n      summary: Leave a Realtime channel\n      description: >-\n        Sent by the client to leave a channel and stop receiving messages\n        for its subscriptions.\n      payload:\n        $ref: '#/components/schemas/PhxLeavePayload'\n    PostgresChange:\n      name: postgres_changes\n      title: Postgres Change Event\n      summary: Database change notification\n      description: >-\n        Sent by the server when a database change occurs in a subscribed\n        schema and table. Contains the event type (INSERT, UPDATE, DELETE),\n        the affected table, and the new and old record data. Row Level\n        Security policies determine which clients receive\
  \ each change.\n      payload:\n        $ref: '#/components/schemas/PostgresChangePayload'\n    BroadcastMessage:\n      name: broadcast\n      title: Broadcast Message\n      summary: Ephemeral message broadcast to channel clients\n      description: >-\n        Sent by the server to all clients subscribed to a channel when\n        another client broadcasts a message. Messages are ephemeral and\n        not persisted.\n      payload:\n        $ref: '#/components/schemas/BroadcastPayload'\n    BroadcastSend:\n      name: broadcast\n      title: Send Broadcast\n      summary: Broadcast a message to channel clients\n      description: >-\n        Sent by a client to broadcast an ephemeral message to all other\n        clients connected to the same channel.\n      payload:\n        $ref: '#/components/schemas/BroadcastSendPayload'\n    PresenceState:\n      name: presence_state\n      title: Presence State\n      summary: Full presence state for the channel\n      description: >-\n     \
  \   Sent by the server after joining a channel with presence enabled.\n        Contains the complete presence state of all tracked clients in\n        the channel, backed by a CRDT for consistency across nodes.\n      payload:\n        $ref: '#/components/schemas/PresenceStatePayload'\n    PresenceDiff:\n      name: presence_diff\n      title: Presence Diff\n      summary: Incremental presence state change\n      description: >-\n        Sent by the server when the presence state changes due to clients\n        joining or leaving. Contains the joins and leaves since the last\n        update.\n      payload:\n        $ref: '#/components/schemas/PresenceDiffPayload'\n    PresenceTrack:\n      name: presence\n      title: Track Presence\n      summary: Start tracking client presence\n      description: >-\n        Sent by a client to register its presence state in the channel.\n        The payload contains arbitrary metadata to be tracked and shared\n        with other clients.\n      payload:\n\
  \        $ref: '#/components/schemas/PresenceTrackPayload'\n    PresenceUntrack:\n      name: presence\n      title: Untrack Presence\n      summary: Stop tracking client presence\n      description: >-\n        Sent by a client to remove its presence state from the channel.\n      payload:\n        $ref: '#/components/schemas/PresenceUntrackPayload'\n    SystemReply:\n      name: phx_reply\n      title: System Reply\n      summary: Server reply to client messages\n      description: >-\n        Sent by the server in response to client messages such as phx_join,\n        broadcast, and presence operations. Contains the status of the\n        operation and any response data.\n      payload:\n        $ref: '#/components/schemas/SystemReplyPayload'\n    Heartbeat:\n      name: phx_reply\n      title: Heartbeat Reply\n      summary: Server heartbeat reply\n      description: >-\n        Sent by the server in response to a client heartbeat to confirm\n        the connection is alive.\n    \
  \  payload:\n        $ref: '#/components/schemas/HeartbeatReplyPayload'\n    HeartbeatSend:\n      name: heartbeat\n      title: Send Heartbeat\n      summary: Client heartbeat to keep connection alive\n      description: >-\n        Sent periodically by the client (typically every 30 seconds) to\n        keep the WebSocket connection alive and prevent server-side\n        timeout.\n      payload:\n        $ref: '#/components/schemas/HeartbeatSendPayload'\n  schemas:\n    PhxJoinPayload:\n      type: object\n      properties:\n        topic:\n          type: string\n          description: Channel topic to join\n        event:\n          type: string\n          const: phx_join\n          description: Event type\n        ref:\n          type: string\n          description: Unique message reference for correlation\n        join_ref:\n          type: string\n          description: Reference for the join operation\n        payload:\n          type: object\n          properties:\n          \
  \  config:\n              type: object\n              properties:\n                broadcast:\n                  type: object\n                  properties:\n                    self:\n                      type: boolean\n                      description: Whether the sender receives their own broadcasts\n                    ack:\n                      type: boolean\n                      description: Whether to acknowledge broadcast messages\n                  description: Broadcast configuration\n                presence:\n                  type: object\n                  properties:\n                    key:\n                      type: string\n                      description: Unique key for presence tracking\n                  description: Presence configuration\n                postgres_changes:\n                  type: array\n                  items:\n                    type: object\n                    properties:\n                      event:\n                        type: string\n\
  \                        description: Database event to listen for\n                        enum:\n                          - INSERT\n                          - UPDATE\n                          - DELETE\n                          - '*'\n                      schema:\n                        type: string\n                        description: PostgreSQL schema name\n                        default: public\n                      table:\n                        type: string\n                        description: Table name to watch\n                      filter:\n                        type: string\n                        description: >-\n                          Optional filter expression (e.g. column=eq.value)\n                  description: Postgres change subscriptions\n            access_token:\n              type: string\n              description: JWT access token for authenticated access\n    PhxLeavePayload:\n      type: object\n      properties:\n        topic:\n          type:\
  \ string\n          description: Channel topic to leave\n        event:\n          type: string\n          const: phx_leave\n        ref:\n          type: string\n          description: Unique message reference\n    PostgresChangePayload:\n      type: object\n      properties:\n        topic:\n          type: string\n          description: Channel topic\n        event:\n          type: string\n          const: postgres_changes\n        ref:\n          type: string\n          description: Message reference\n        payload:\n          type: object\n          properties:\n            data:\n              type: object\n              properties:\n                schema:\n                  type: string\n                  description: Database schema name\n                table:\n                  type: string\n                  description: Table name\n                commit_timestamp:\n                  type: string\n                  format: date-time\n                  description: Timestamp\
  \ of the database transaction\n                eventType:\n                  type: string\n                  description: Type of database event\n                  enum:\n                    - INSERT\n                    - UPDATE\n                    - DELETE\n                new:\n                  type: object\n                  description: New row data (present for INSERT and UPDATE)\n                old:\n                  type: object\n                  description: Previous row data (present for UPDATE and DELETE)\n                errors:\n                  type: array\n                  items:\n                    type: string\n                  description: Any errors processing the change\n            ids:\n              type: array\n              items:\n                type: integer\n              description: Subscription IDs that matched this change\n    BroadcastPayload:\n      type: object\n      properties:\n        topic:\n          type: string\n          description:\
  \ Channel topic\n        event:\n          type: string\n          const: broadcast\n        payload:\n          type: object\n          properties:\n            event:\n              type: string\n              description: Custom event name\n            payload:\n              type: object\n              description: Custom message payload\n            type:\n              type: string\n              const: broadcast\n    BroadcastSendPayload:\n      type: object\n      properties:\n        topic:\n          type: string\n          description: Channel topic\n        event:\n          type: string\n          const: broadcast\n        ref:\n          type: string\n          description: Message reference\n        payload:\n          type: object\n          properties:\n            event:\n              type: string\n              description: Custom event name\n            payload:\n              type: object\n              description: Custom message payload\n            type:\n    \
  \          type: string\n              const: broadcast\n    PresenceStatePayload:\n      type: object\n      properties:\n        topic:\n          type: string\n          description: Channel topic\n        event:\n          type: string\n          const: presence_state\n        payload:\n          type: object\n          additionalProperties:\n            type: object\n            properties:\n              metas:\n                type: array\n                items:\n                  type: object\n                  properties:\n                    phx_ref:\n                      type: string\n                      description: Phoenix reference for this presence entry\n                  additionalProperties: true\n                description: Presence metadata entries\n          description: >-\n            Map of presence keys to their tracked state. Each key contains\n            a metas array with one entry per connected device/tab.\n    PresenceDiffPayload:\n      type: object\n\
  \      properties:\n        topic:\n          type: string\n          description: Channel topic\n        event:\n          type: string\n          const: presence_diff\n        payload:\n          type: object\n          properties:\n            joins:\n              type: object\n              additionalProperties:\n                type: object\n                properties:\n                  metas:\n                    type: array\n                    items:\n                      type: object\n                      additionalProperties: true\n              description: Presence entries that joined since last update\n            leaves:\n              type: object\n              additionalProperties:\n                type: object\n                properties:\n                  metas:\n                    type: array\n                    items:\n                      type: object\n                      additionalProperties: true\n              description: Presence entries that left since\
  \ last update\n    PresenceTrackPayload:\n      type: object\n      properties:\n        topic:\n          type: string\n          description: Channel topic\n        event:\n          type: string\n          const: presence\n        ref:\n          type: string\n          description: Message reference\n        payload:\n          type: object\n          properties:\n            type:\n              type: string\n              const: presence\n            event:\n              type: string\n              const: track\n            payload:\n              type: object\n              description: Custom presence metadata to track\n              additionalProperties: true\n    PresenceUntrackPayload:\n      type: object\n      properties:\n        topic:\n          type: string\n          description: Channel topic\n        event:\n          type: string\n          const: presence\n        ref:\n          type: string\n          description: Message reference\n        payload:\n         \
  \ type: object\n          properties:\n            type:\n              type: string\n              const: presence\n            event:\n              type: string\n              const: untrack\n    SystemReplyPayload:\n      type: object\n      properties:\n        topic:\n          type: string\n          description: Channel topic\n        event:\n          type: string\n          const: phx_reply\n        ref:\n          type: string\n          description: Reference matching the original message\n        payload:\n          type: object\n          properties:\n            status:\n              type: string\n              description: Status of the operation\n              enum:\n                - ok\n                - error\n            response:\n              type: object\n              description: Response data from the operation\n    HeartbeatSendPayload:\n      type: object\n      properties:\n        topic:\n          type: string\n          const: phoenix\n          description:\
  \ Heartbeat topic is always phoenix\n        event:\n          type: string\n          const: heartbeat\n        ref:\n          type: string\n          description: Message reference\n        payload:\n          type: object\n    HeartbeatReplyPayload:\n      type: object\n      properties:\n        topic:\n          type: string\n          const: phoenix\n        event:\n          type: string\n          const: phx_reply\n        ref:\n          type: string\n          description: Reference matching the heartbeat message\n        payload:\n          type: object\n          properties:\n            status:\n              type: string\n              const: ok\n            response:\n              type: object\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/asyncapi/supabase-realtime-api-asyncapi.yml
spec_file: asyncapi/supabase-realtime-api-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/supabase/refs/heads/main/asyncapi/supabase-realtime-api-asyncapi.yml
tags:
- Backend As A Service
- PostgreSQL
- Open Source
- Authentication
- Real Time
- Storage
- Edge Functions
- Database
- AsyncAPI
- Webhooks
- Events
version: 2.0.0
---
