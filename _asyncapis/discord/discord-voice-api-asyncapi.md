---
api_specs:
- filename: discord-rest-api-openapi.yml
  format: yaml
  label: Discord REST API
  slug: discord-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/discord/refs/heads/main/openapi/discord-rest-api-openapi.yml
- filename: discord-gateway-api-asyncapi.yml
  format: yaml
  label: Discord Gateway API
  slug: discord-gateway-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/discord/refs/heads/main/asyncapi/discord-gateway-api-asyncapi.yml
- filename: discord-interactions-api-openapi.yml
  format: yaml
  label: Discord Interactions API
  slug: discord-interactions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/discord/refs/heads/main/openapi/discord-interactions-api-openapi.yml
- filename: discord-oauth2-api-openapi.yml
  format: yaml
  label: Discord OAuth2 API
  slug: discord-oauth2-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/discord/refs/heads/main/openapi/discord-oauth2-api-openapi.yml
- filename: discord-webhook-events-api-openapi.yml
  format: yaml
  label: Discord Webhook Events API
  slug: discord-webhook-events-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/discord/refs/heads/main/openapi/discord-webhook-events-api-openapi.yml
- filename: discord-voice-api-asyncapi.yml
  format: yaml
  label: Discord Voice API
  slug: discord-voice-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/discord/refs/heads/main/asyncapi/discord-voice-api-asyncapi.yml
- filename: discord-linked-roles-api-openapi.yml
  format: yaml
  label: Discord Linked Roles API
  slug: discord-linked-roles-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/discord/refs/heads/main/openapi/discord-linked-roles-api-openapi.yml
channels:
- description: ''
  name: /
  operation: publish
  operation_id: sendVoiceMessage
  summary: Send message to voice server
description: The Discord Voice API provides the protocol for establishing and managing voice connections between clients and Discord voice servers. It handles UDP-based voice data transmission, encryption with XSalsa20-Poly1305, and supports features like speaking indicators and voice state updates. The voice connection lifecycle begins via the main Gateway with Opcode 4 (Update Voice State) and continues with a dedicated voice WebSocket.
layout: asyncapi
messages:
- description: ''
  name: VoiceIdentify
  summary: Begin a voice WebSocket connection
  title: Voice Identify (Opcode 0)
- description: ''
  name: SelectProtocol
  summary: Select the voice protocol and provide connection details
  title: Select Protocol (Opcode 1)
- description: ''
  name: VoiceHeartbeat
  summary: Sent periodically to maintain the voice connection
  title: Voice Heartbeat (Opcode 3)
- description: ''
  name: Speaking
  summary: Indicate speaking status
  title: Speaking (Opcode 5)
- description: ''
  name: VoiceResume
  summary: Resume a voice connection
  title: Voice Resume (Opcode 7)
- description: ''
  name: VoiceReady
  summary: Voice server is ready, provides connection information
  title: Voice Ready (Opcode 2)
- description: ''
  name: SessionDescription
  summary: Voice session description with encryption details
  title: Session Description (Opcode 4)
- description: ''
  name: VoiceHeartbeatAck
  summary: Acknowledgment of a voice heartbeat
  title: Voice Heartbeat ACK (Opcode 6)
- description: ''
  name: VoiceHello
  summary: Received after connecting, contains heartbeat interval
  title: Voice Hello (Opcode 8)
- description: ''
  name: VoiceResumed
  summary: Voice connection successfully resumed
  title: Voice Resumed (Opcode 9)
- description: ''
  name: ClientDisconnect
  summary: A user disconnected from the voice channel
  title: Client Disconnect (Opcode 13)
name: Discord Voice API
provider_name: Discord
provider_slug: discord
servers:
- description: Discord Voice WebSocket server (endpoint provided via VOICE_SERVER_UPDATE)
  name: voice
  protocol: wss
  url: wss://{voice_server_hostname}/?v=8
slug: discord-voice-api-asyncapi
source_filename: discord-voice-api-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Discord Voice API\n  version: '10'\n  description: >-\n    The Discord Voice API provides the protocol for establishing and managing\n    voice connections between clients and Discord voice servers. It handles\n    UDP-based voice data transmission, encryption with XSalsa20-Poly1305,\n    and supports features like speaking indicators and voice state updates.\n    The voice connection lifecycle begins via the main Gateway with Opcode 4\n    (Update Voice State) and continues with a dedicated voice WebSocket.\n  contact:\n    name: Discord Support\n    url: https://support-dev.discord.com/hc/en-us\n    email: support@discord.com\n  license:\n    name: MIT\n  externalDocs:\n    description: Discord Voice Connections Documentation\n    url: https://discord.com/developers/docs/topics/voice-connections\nservers:\n  voice:\n    url: wss://{voice_server_hostname}/?v=8\n    protocol: wss\n    description: Discord Voice WebSocket server (endpoint provided\
  \ via VOICE_SERVER_UPDATE)\n    variables:\n      voice_server_hostname:\n        description: Voice server hostname from VOICE_SERVER_UPDATE event\nchannels:\n  /:\n    publish:\n      operationId: sendVoiceMessage\n      summary: Send message to voice server\n      description: Messages sent from the client to the Discord voice server\n      message:\n        oneOf:\n          - $ref: '#/components/messages/VoiceIdentify'\n          - $ref: '#/components/messages/SelectProtocol'\n          - $ref: '#/components/messages/VoiceHeartbeat'\n          - $ref: '#/components/messages/Speaking'\n          - $ref: '#/components/messages/VoiceResume'\n    subscribe:\n      operationId: receiveVoiceEvent\n      summary: Receive events from voice server\n      description: Events received from the Discord voice server\n      message:\n        oneOf:\n          - $ref: '#/components/messages/VoiceReady'\n          - $ref: '#/components/messages/SessionDescription'\n          - $ref: '#/components/messages/VoiceHeartbeatAck'\n\
  \          - $ref: '#/components/messages/VoiceHello'\n          - $ref: '#/components/messages/VoiceResumed'\n          - $ref: '#/components/messages/ClientDisconnect'\ncomponents:\n  messages:\n    VoiceIdentify:\n      name: VoiceIdentify\n      title: Voice Identify (Opcode 0)\n      summary: Begin a voice WebSocket connection\n      payload:\n        type: object\n        required:\n          - op\n          - d\n        properties:\n          op:\n            type: integer\n            const: 0\n          d:\n            type: object\n            required:\n              - server_id\n              - user_id\n              - session_id\n              - token\n            properties:\n              server_id:\n                type: string\n                description: Guild ID or channel ID for DM calls\n              user_id:\n                type: string\n              session_id:\n                type: string\n                description: Session ID from the main Gateway READY\
  \ event\n              token:\n                type: string\n                description: Voice token from VOICE_SERVER_UPDATE\n    SelectProtocol:\n      name: SelectProtocol\n      title: Select Protocol (Opcode 1)\n      summary: Select the voice protocol and provide connection details\n      payload:\n        type: object\n        required:\n          - op\n          - d\n        properties:\n          op:\n            type: integer\n            const: 1\n          d:\n            type: object\n            required:\n              - protocol\n              - data\n            properties:\n              protocol:\n                type: string\n                enum:\n                  - udp\n              data:\n                type: object\n                required:\n                  - address\n                  - port\n                  - mode\n                properties:\n                  address:\n                    type: string\n                    description: External IP discovered\
  \ via IP Discovery\n                  port:\n                    type: integer\n                    description: External port discovered via IP Discovery\n                  mode:\n                    type: string\n                    description: Encryption mode\n                    enum:\n                      - aead_aes256_gcm_rtpsize\n                      - aead_xchacha20_poly1305_rtpsize\n                      - xsalsa20_poly1305_lite\n                      - xsalsa20_poly1305_suffix\n                      - xsalsa20_poly1305\n    VoiceHeartbeat:\n      name: VoiceHeartbeat\n      title: Voice Heartbeat (Opcode 3)\n      summary: Sent periodically to maintain the voice connection\n      payload:\n        type: object\n        required:\n          - op\n          - d\n        properties:\n          op:\n            type: integer\n            const: 3\n          d:\n            type: integer\n            description: Nonce value (timestamp)\n    Speaking:\n      name: Speaking\n  \
  \    title: Speaking (Opcode 5)\n      summary: Indicate speaking status\n      payload:\n        type: object\n        required:\n          - op\n          - d\n        properties:\n          op:\n            type: integer\n            const: 5\n          d:\n            type: object\n            required:\n              - speaking\n              - delay\n              - ssrc\n            properties:\n              speaking:\n                type: integer\n                description: >-\n                  Bitfield: 1=Microphone, 2=Soundshare, 4=Priority\n              delay:\n                type: integer\n              ssrc:\n                type: integer\n                description: Synchronization Source identifier\n    VoiceResume:\n      name: VoiceResume\n      title: Voice Resume (Opcode 7)\n      summary: Resume a voice connection\n      payload:\n        type: object\n        required:\n          - op\n          - d\n        properties:\n          op:\n            type: integer\n\
  \            const: 7\n          d:\n            type: object\n            required:\n              - server_id\n              - session_id\n              - token\n            properties:\n              server_id:\n                type: string\n              session_id:\n                type: string\n              token:\n                type: string\n    VoiceReady:\n      name: VoiceReady\n      title: Voice Ready (Opcode 2)\n      summary: Voice server is ready, provides connection information\n      payload:\n        type: object\n        properties:\n          op:\n            type: integer\n            const: 2\n          d:\n            type: object\n            properties:\n              ssrc:\n                type: integer\n                description: SSRC for this connection\n              ip:\n                type: string\n                description: Voice server IP\n              port:\n                type: integer\n                description: Voice server UDP port\n  \
  \            modes:\n                type: array\n                items:\n                  type: string\n                description: Available encryption modes\n    SessionDescription:\n      name: SessionDescription\n      title: Session Description (Opcode 4)\n      summary: Voice session description with encryption details\n      payload:\n        type: object\n        properties:\n          op:\n            type: integer\n            const: 4\n          d:\n            type: object\n            properties:\n              mode:\n                type: string\n                description: Selected encryption mode\n              secret_key:\n                type: array\n                items:\n                  type: integer\n                description: 32-byte secret key for encryption\n    VoiceHeartbeatAck:\n      name: VoiceHeartbeatAck\n      title: Voice Heartbeat ACK (Opcode 6)\n      summary: Acknowledgment of a voice heartbeat\n      payload:\n        type: object\n       \
  \ properties:\n          op:\n            type: integer\n            const: 6\n          d:\n            type: integer\n            description: Nonce echoed back\n    VoiceHello:\n      name: VoiceHello\n      title: Voice Hello (Opcode 8)\n      summary: Received after connecting, contains heartbeat interval\n      payload:\n        type: object\n        properties:\n          op:\n            type: integer\n            const: 8\n          d:\n            type: object\n            properties:\n              heartbeat_interval:\n                type: number\n                description: Heartbeat interval in milliseconds\n    VoiceResumed:\n      name: VoiceResumed\n      title: Voice Resumed (Opcode 9)\n      summary: Voice connection successfully resumed\n      payload:\n        type: object\n        properties:\n          op:\n            type: integer\n            const: 9\n    ClientDisconnect:\n      name: ClientDisconnect\n      title: Client Disconnect (Opcode 13)\n      summary:\
  \ A user disconnected from the voice channel\n      payload:\n        type: object\n        properties:\n          op:\n            type: integer\n            const: 13\n          d:\n            type: object\n            properties:\n              user_id:\n                type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/discord/refs/heads/main/asyncapi/discord-voice-api-asyncapi.yml
spec_file: asyncapi/discord-voice-api-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/discord/refs/heads/main/asyncapi/discord-voice-api-asyncapi.yml
tags:
- Chat
- Communication
- Gaming
- Messaging
- Social
- Video
- Voice
- AsyncAPI
- Webhooks
- Events
version: '10'
---
