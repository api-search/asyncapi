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
  operation_id: sendGatewayMessage
  summary: Send message to Gateway
description: The Discord Gateway API provides persistent, stateful WebSocket connections between your client and Discord servers. These connections are used for sending and receiving real-time events your client can use to track and update local state, including message creation, guild updates, presence changes, and voice state updates.
layout: asyncapi
messages:
- description: ''
  name: Identify
  summary: Sent to trigger the initial handshake with the gateway
  title: Identify (Opcode 2)
- description: ''
  name: Resume
  summary: Sent to resume a disconnected session
  title: Resume (Opcode 6)
- description: ''
  name: Heartbeat
  summary: Sent periodically to maintain the connection
  title: Heartbeat (Opcode 1)
- description: ''
  name: RequestGuildMembers
  summary: Request guild members for a guild
  title: Request Guild Members (Opcode 8)
- description: ''
  name: UpdateVoiceState
  summary: Sent to join, move, or disconnect from a voice channel
  title: Update Voice State (Opcode 4)
- description: ''
  name: UpdatePresence
  summary: Sent to update the client's presence
  title: Update Presence (Opcode 3)
- description: ''
  name: Hello
  summary: Received after connecting, contains heartbeat interval
  title: Hello (Opcode 10)
- description: ''
  name: HeartbeatAck
  summary: Acknowledgment of a heartbeat
  title: Heartbeat ACK (Opcode 11)
- description: ''
  name: Ready
  summary: Dispatched after a successful Identify
  title: Ready
- description: ''
  name: Resumed
  summary: Dispatched after a successful Resume
  title: Resumed
- description: ''
  name: Reconnect
  summary: Server requests the client to reconnect
  title: Reconnect (Opcode 7)
- description: ''
  name: InvalidSession
  summary: Session is invalid, d indicates if resumable
  title: Invalid Session (Opcode 9)
- description: Requires GUILDS intent
  name: ChannelCreate
  summary: New channel created
  title: CHANNEL_CREATE
- description: Requires GUILDS intent
  name: ChannelUpdate
  summary: Channel was updated
  title: CHANNEL_UPDATE
- description: Requires GUILDS intent
  name: ChannelDelete
  summary: Channel was deleted
  title: CHANNEL_DELETE
- description: Requires GUILDS or DIRECT_MESSAGES intent
  name: ChannelPinsUpdate
  summary: Message was pinned or unpinned
  title: CHANNEL_PINS_UPDATE
- description: Requires GUILDS intent
  name: ThreadCreate
  summary: Thread created or current user added to thread
  title: THREAD_CREATE
- description: Requires GUILDS intent
  name: ThreadUpdate
  summary: Thread was updated
  title: THREAD_UPDATE
- description: Requires GUILDS intent
  name: ThreadDelete
  summary: Thread was deleted
  title: THREAD_DELETE
- description: Requires GUILDS intent
  name: ThreadListSync
  summary: Sent when gaining access to a channel with active threads
  title: THREAD_LIST_SYNC
- description: Requires GUILDS intent
  name: GuildCreate
  summary: Lazy-loaded guild available or user joined a new guild
  title: GUILD_CREATE
- description: Requires GUILDS intent
  name: GuildUpdate
  summary: Guild was updated
  title: GUILD_UPDATE
- description: Requires GUILDS intent
  name: GuildDelete
  summary: Guild became unavailable or user left/was removed from guild
  title: GUILD_DELETE
- description: Requires GUILD_MODERATION intent
  name: GuildBanAdd
  summary: User was banned from a guild
  title: GUILD_BAN_ADD
- description: Requires GUILD_MODERATION intent
  name: GuildBanRemove
  summary: User was unbanned from a guild
  title: GUILD_BAN_REMOVE
- description: Requires GUILD_EMOJIS_AND_STICKERS intent
  name: GuildEmojisUpdate
  summary: Guild emojis were updated
  title: GUILD_EMOJIS_UPDATE
- description: Requires GUILD_EMOJIS_AND_STICKERS intent
  name: GuildStickersUpdate
  summary: Guild stickers were updated
  title: GUILD_STICKERS_UPDATE
- description: Requires GUILD_MEMBERS privileged intent
  name: GuildMemberAdd
  summary: New user joined a guild
  title: GUILD_MEMBER_ADD
- description: Requires GUILD_MEMBERS privileged intent
  name: GuildMemberRemove
  summary: User was removed from a guild
  title: GUILD_MEMBER_REMOVE
- description: Requires GUILD_MEMBERS privileged intent
  name: GuildMemberUpdate
  summary: Guild member was updated
  title: GUILD_MEMBER_UPDATE
- description: ''
  name: GuildMembersChunk
  summary: Response to Request Guild Members
  title: GUILD_MEMBERS_CHUNK
- description: Requires GUILDS intent
  name: GuildRoleCreate
  summary: Guild role was created
  title: GUILD_ROLE_CREATE
- description: Requires GUILDS intent
  name: GuildRoleUpdate
  summary: Guild role was updated
  title: GUILD_ROLE_UPDATE
- description: Requires GUILDS intent
  name: GuildRoleDelete
  summary: Guild role was deleted
  title: GUILD_ROLE_DELETE
- description: Requires GUILD_SCHEDULED_EVENTS intent
  name: GuildScheduledEventCreate
  summary: Guild scheduled event was created
  title: GUILD_SCHEDULED_EVENT_CREATE
- description: Requires GUILD_SCHEDULED_EVENTS intent
  name: GuildScheduledEventUpdate
  summary: Guild scheduled event was updated
  title: GUILD_SCHEDULED_EVENT_UPDATE
- description: Requires GUILD_SCHEDULED_EVENTS intent
  name: GuildScheduledEventDelete
  summary: Guild scheduled event was deleted
  title: GUILD_SCHEDULED_EVENT_DELETE
- description: ''
  name: InteractionCreate
  summary: User used an interaction
  title: INTERACTION_CREATE
- description: Requires GUILD_INVITES intent
  name: InviteCreate
  summary: Invite to a channel was created
  title: INVITE_CREATE
- description: Requires GUILD_INVITES intent
  name: InviteDelete
  summary: Invite to a channel was deleted
  title: INVITE_DELETE
- description: Requires GUILD_MESSAGES or DIRECT_MESSAGES intent. MESSAGE_CONTENT privileged intent required for content in guilds.
  name: MessageCreate
  summary: Message was created
  title: MESSAGE_CREATE
- description: Requires GUILD_MESSAGES or DIRECT_MESSAGES intent
  name: MessageUpdate
  summary: Message was edited
  title: MESSAGE_UPDATE
- description: Requires GUILD_MESSAGES or DIRECT_MESSAGES intent
  name: MessageDelete
  summary: Message was deleted
  title: MESSAGE_DELETE
- description: Requires GUILD_MESSAGES intent
  name: MessageDeleteBulk
  summary: Multiple messages were deleted at once
  title: MESSAGE_DELETE_BULK
- description: Requires GUILD_MESSAGE_REACTIONS or DIRECT_MESSAGE_REACTIONS intent
  name: MessageReactionAdd
  summary: User reacted to a message
  title: MESSAGE_REACTION_ADD
- description: Requires GUILD_MESSAGE_REACTIONS or DIRECT_MESSAGE_REACTIONS intent
  name: MessageReactionRemove
  summary: User removed a reaction from a message
  title: MESSAGE_REACTION_REMOVE
- description: Requires GUILD_MESSAGE_REACTIONS or DIRECT_MESSAGE_REACTIONS intent
  name: MessageReactionRemoveAll
  summary: All reactions were explicitly removed from a message
  title: MESSAGE_REACTION_REMOVE_ALL
- description: Requires GUILD_PRESENCES privileged intent
  name: PresenceUpdate
  summary: User's presence or info was updated
  title: PRESENCE_UPDATE
- description: Requires GUILD_MESSAGE_TYPING or DIRECT_MESSAGE_TYPING intent
  name: TypingStart
  summary: User started typing in a channel
  title: TYPING_START
- description: ''
  name: UserUpdate
  summary: Properties about the current user changed
  title: USER_UPDATE
- description: Requires GUILD_VOICE_STATES intent
  name: VoiceStateUpdate
  summary: Someone joined, left, or moved a voice channel
  title: VOICE_STATE_UPDATE
- description: ''
  name: VoiceServerUpdate
  summary: Guild's voice server was updated
  title: VOICE_SERVER_UPDATE
- description: ''
  name: WebhooksUpdate
  summary: Guild channel webhook was created, updated, or deleted
  title: WEBHOOKS_UPDATE
name: Discord Gateway API
provider_name: Discord
provider_slug: discord
servers:
- description: Discord Gateway WebSocket server
  name: gateway
  protocol: wss
  url: wss://gateway.discord.gg/?v=10&encoding=json
slug: discord-gateway-api-asyncapi
source_filename: discord-gateway-api-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Discord Gateway API\n  version: '10'\n  description: >-\n    The Discord Gateway API provides persistent, stateful WebSocket\n    connections between your client and Discord servers. These connections\n    are used for sending and receiving real-time events your client can use\n    to track and update local state, including message creation, guild\n    updates, presence changes, and voice state updates.\n  contact:\n    name: Discord Support\n    url: https://support-dev.discord.com/hc/en-us\n    email: support@discord.com\n  license:\n    name: MIT\n  externalDocs:\n    description: Discord Gateway Documentation\n    url: https://discord.com/developers/docs/events/gateway\nservers:\n  gateway:\n    url: wss://gateway.discord.gg/?v=10&encoding=json\n    protocol: wss\n    description: Discord Gateway WebSocket server\nchannels:\n  /:\n    publish:\n      operationId: sendGatewayMessage\n      summary: Send message to Gateway\n      description:\
  \ Messages sent from the client to the Discord Gateway\n      message:\n        oneOf:\n          - $ref: '#/components/messages/Identify'\n          - $ref: '#/components/messages/Resume'\n          - $ref: '#/components/messages/Heartbeat'\n          - $ref: '#/components/messages/RequestGuildMembers'\n          - $ref: '#/components/messages/UpdateVoiceState'\n          - $ref: '#/components/messages/UpdatePresence'\n    subscribe:\n      operationId: receiveGatewayEvent\n      summary: Receive events from Gateway\n      description: Events received from the Discord Gateway\n      message:\n        oneOf:\n          - $ref: '#/components/messages/Hello'\n          - $ref: '#/components/messages/HeartbeatAck'\n          - $ref: '#/components/messages/Ready'\n          - $ref: '#/components/messages/Resumed'\n          - $ref: '#/components/messages/Reconnect'\n          - $ref: '#/components/messages/InvalidSession'\n          - $ref: '#/components/messages/ChannelCreate'\n         \
  \ - $ref: '#/components/messages/ChannelUpdate'\n          - $ref: '#/components/messages/ChannelDelete'\n          - $ref: '#/components/messages/ChannelPinsUpdate'\n          - $ref: '#/components/messages/ThreadCreate'\n          - $ref: '#/components/messages/ThreadUpdate'\n          - $ref: '#/components/messages/ThreadDelete'\n          - $ref: '#/components/messages/ThreadListSync'\n          - $ref: '#/components/messages/GuildCreate'\n          - $ref: '#/components/messages/GuildUpdate'\n          - $ref: '#/components/messages/GuildDelete'\n          - $ref: '#/components/messages/GuildBanAdd'\n          - $ref: '#/components/messages/GuildBanRemove'\n          - $ref: '#/components/messages/GuildEmojisUpdate'\n          - $ref: '#/components/messages/GuildStickersUpdate'\n          - $ref: '#/components/messages/GuildMemberAdd'\n          - $ref: '#/components/messages/GuildMemberRemove'\n          - $ref: '#/components/messages/GuildMemberUpdate'\n          - $ref: '#/components/messages/GuildMembersChunk'\n\
  \          - $ref: '#/components/messages/GuildRoleCreate'\n          - $ref: '#/components/messages/GuildRoleUpdate'\n          - $ref: '#/components/messages/GuildRoleDelete'\n          - $ref: '#/components/messages/GuildScheduledEventCreate'\n          - $ref: '#/components/messages/GuildScheduledEventUpdate'\n          - $ref: '#/components/messages/GuildScheduledEventDelete'\n          - $ref: '#/components/messages/InteractionCreate'\n          - $ref: '#/components/messages/InviteCreate'\n          - $ref: '#/components/messages/InviteDelete'\n          - $ref: '#/components/messages/MessageCreate'\n          - $ref: '#/components/messages/MessageUpdate'\n          - $ref: '#/components/messages/MessageDelete'\n          - $ref: '#/components/messages/MessageDeleteBulk'\n          - $ref: '#/components/messages/MessageReactionAdd'\n          - $ref: '#/components/messages/MessageReactionRemove'\n          - $ref: '#/components/messages/MessageReactionRemoveAll'\n          - $ref:\
  \ '#/components/messages/PresenceUpdate'\n          - $ref: '#/components/messages/TypingStart'\n          - $ref: '#/components/messages/UserUpdate'\n          - $ref: '#/components/messages/VoiceStateUpdate'\n          - $ref: '#/components/messages/VoiceServerUpdate'\n          - $ref: '#/components/messages/WebhooksUpdate'\ncomponents:\n  messages:\n    Identify:\n      name: Identify\n      title: Identify (Opcode 2)\n      summary: Sent to trigger the initial handshake with the gateway\n      payload:\n        type: object\n        required:\n          - op\n          - d\n        properties:\n          op:\n            type: integer\n            const: 2\n          d:\n            type: object\n            required:\n              - token\n              - intents\n              - properties\n            properties:\n              token:\n                type: string\n                description: Authentication token\n              intents:\n                type: integer\n      \
  \          description: Gateway Intents bitfield\n              properties:\n                type: object\n                properties:\n                  os:\n                    type: string\n                  browser:\n                    type: string\n                  device:\n                    type: string\n              compress:\n                type: boolean\n              large_threshold:\n                type: integer\n                minimum: 50\n                maximum: 250\n              shard:\n                type: array\n                items:\n                  type: integer\n                minItems: 2\n                maxItems: 2\n              presence:\n                type: object\n                properties:\n                  since:\n                    type: integer\n                    nullable: true\n                  activities:\n                    type: array\n                    items:\n                      $ref: '#/components/schemas/Activity'\n     \
  \             status:\n                    type: string\n                    enum:\n                      - online\n                      - dnd\n                      - idle\n                      - invisible\n                      - offline\n                  afk:\n                    type: boolean\n    Resume:\n      name: Resume\n      title: Resume (Opcode 6)\n      summary: Sent to resume a disconnected session\n      payload:\n        type: object\n        required:\n          - op\n          - d\n        properties:\n          op:\n            type: integer\n            const: 6\n          d:\n            type: object\n            required:\n              - token\n              - session_id\n              - seq\n            properties:\n              token:\n                type: string\n              session_id:\n                type: string\n              seq:\n                type: integer\n    Heartbeat:\n      name: Heartbeat\n      title: Heartbeat (Opcode 1)\n      summary:\
  \ Sent periodically to maintain the connection\n      payload:\n        type: object\n        required:\n          - op\n          - d\n        properties:\n          op:\n            type: integer\n            const: 1\n          d:\n            type: integer\n            nullable: true\n            description: Last sequence number received\n    RequestGuildMembers:\n      name: RequestGuildMembers\n      title: Request Guild Members (Opcode 8)\n      summary: Request guild members for a guild\n      payload:\n        type: object\n        required:\n          - op\n          - d\n        properties:\n          op:\n            type: integer\n            const: 8\n          d:\n            type: object\n            required:\n              - guild_id\n            properties:\n              guild_id:\n                type: string\n              query:\n                type: string\n              limit:\n                type: integer\n              presences:\n                type: boolean\n\
  \              user_ids:\n                oneOf:\n                  - type: string\n                  - type: array\n                    items:\n                      type: string\n              nonce:\n                type: string\n    UpdateVoiceState:\n      name: UpdateVoiceState\n      title: Update Voice State (Opcode 4)\n      summary: Sent to join, move, or disconnect from a voice channel\n      payload:\n        type: object\n        required:\n          - op\n          - d\n        properties:\n          op:\n            type: integer\n            const: 4\n          d:\n            type: object\n            required:\n              - guild_id\n              - channel_id\n              - self_mute\n              - self_deaf\n            properties:\n              guild_id:\n                type: string\n              channel_id:\n                type: string\n                nullable: true\n              self_mute:\n                type: boolean\n              self_deaf:\n  \
  \              type: boolean\n    UpdatePresence:\n      name: UpdatePresence\n      title: Update Presence (Opcode 3)\n      summary: Sent to update the client's presence\n      payload:\n        type: object\n        required:\n          - op\n          - d\n        properties:\n          op:\n            type: integer\n            const: 3\n          d:\n            type: object\n            required:\n              - since\n              - activities\n              - status\n              - afk\n            properties:\n              since:\n                type: integer\n                nullable: true\n              activities:\n                type: array\n                items:\n                  $ref: '#/components/schemas/Activity'\n              status:\n                type: string\n                enum:\n                  - online\n                  - dnd\n                  - idle\n                  - invisible\n                  - offline\n              afk:\n            \
  \    type: boolean\n    Hello:\n      name: Hello\n      title: Hello (Opcode 10)\n      summary: Received after connecting, contains heartbeat interval\n      payload:\n        type: object\n        properties:\n          op:\n            type: integer\n            const: 10\n          d:\n            type: object\n            properties:\n              heartbeat_interval:\n                type: integer\n                description: Interval in milliseconds to send heartbeats\n    HeartbeatAck:\n      name: HeartbeatAck\n      title: Heartbeat ACK (Opcode 11)\n      summary: Acknowledgment of a heartbeat\n      payload:\n        type: object\n        properties:\n          op:\n            type: integer\n            const: 11\n    Ready:\n      name: Ready\n      title: Ready\n      summary: Dispatched after a successful Identify\n      payload:\n        type: object\n        properties:\n          op:\n            type: integer\n            const: 0\n          t:\n            type: string\n\
  \            const: READY\n          s:\n            type: integer\n          d:\n            type: object\n            properties:\n              v:\n                type: integer\n              user:\n                $ref: '#/components/schemas/User'\n              guilds:\n                type: array\n                items:\n                  type: object\n              session_id:\n                type: string\n              resume_gateway_url:\n                type: string\n              shard:\n                type: array\n                items:\n                  type: integer\n              application:\n                type: object\n                properties:\n                  id:\n                    type: string\n                  flags:\n                    type: integer\n    Resumed:\n      name: Resumed\n      title: Resumed\n      summary: Dispatched after a successful Resume\n      payload:\n        type: object\n        properties:\n          op:\n            type: integer\n\
  \            const: 0\n          t:\n            type: string\n            const: RESUMED\n          s:\n            type: integer\n    Reconnect:\n      name: Reconnect\n      title: Reconnect (Opcode 7)\n      summary: Server requests the client to reconnect\n      payload:\n        type: object\n        properties:\n          op:\n            type: integer\n            const: 7\n    InvalidSession:\n      name: InvalidSession\n      title: Invalid Session (Opcode 9)\n      summary: Session is invalid, d indicates if resumable\n      payload:\n        type: object\n        properties:\n          op:\n            type: integer\n            const: 9\n          d:\n            type: boolean\n            description: Whether the session is resumable\n    ChannelCreate:\n      name: ChannelCreate\n      title: CHANNEL_CREATE\n      summary: New channel created\n      description: Requires GUILDS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    ChannelUpdate:\n\
  \      name: ChannelUpdate\n      title: CHANNEL_UPDATE\n      summary: Channel was updated\n      description: Requires GUILDS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    ChannelDelete:\n      name: ChannelDelete\n      title: CHANNEL_DELETE\n      summary: Channel was deleted\n      description: Requires GUILDS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    ChannelPinsUpdate:\n      name: ChannelPinsUpdate\n      title: CHANNEL_PINS_UPDATE\n      summary: Message was pinned or unpinned\n      description: Requires GUILDS or DIRECT_MESSAGES intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    ThreadCreate:\n      name: ThreadCreate\n      title: THREAD_CREATE\n      summary: Thread created or current user added to thread\n      description: Requires GUILDS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    ThreadUpdate:\n      name: ThreadUpdate\n      title: THREAD_UPDATE\n\
  \      summary: Thread was updated\n      description: Requires GUILDS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    ThreadDelete:\n      name: ThreadDelete\n      title: THREAD_DELETE\n      summary: Thread was deleted\n      description: Requires GUILDS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    ThreadListSync:\n      name: ThreadListSync\n      title: THREAD_LIST_SYNC\n      summary: Sent when gaining access to a channel with active threads\n      description: Requires GUILDS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildCreate:\n      name: GuildCreate\n      title: GUILD_CREATE\n      summary: Lazy-loaded guild available or user joined a new guild\n      description: Requires GUILDS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildUpdate:\n      name: GuildUpdate\n      title: GUILD_UPDATE\n      summary: Guild was updated\n      description:\
  \ Requires GUILDS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildDelete:\n      name: GuildDelete\n      title: GUILD_DELETE\n      summary: Guild became unavailable or user left/was removed from guild\n      description: Requires GUILDS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildBanAdd:\n      name: GuildBanAdd\n      title: GUILD_BAN_ADD\n      summary: User was banned from a guild\n      description: Requires GUILD_MODERATION intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildBanRemove:\n      name: GuildBanRemove\n      title: GUILD_BAN_REMOVE\n      summary: User was unbanned from a guild\n      description: Requires GUILD_MODERATION intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildEmojisUpdate:\n      name: GuildEmojisUpdate\n      title: GUILD_EMOJIS_UPDATE\n      summary: Guild emojis were updated\n      description: Requires GUILD_EMOJIS_AND_STICKERS\
  \ intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildStickersUpdate:\n      name: GuildStickersUpdate\n      title: GUILD_STICKERS_UPDATE\n      summary: Guild stickers were updated\n      description: Requires GUILD_EMOJIS_AND_STICKERS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildMemberAdd:\n      name: GuildMemberAdd\n      title: GUILD_MEMBER_ADD\n      summary: New user joined a guild\n      description: Requires GUILD_MEMBERS privileged intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildMemberRemove:\n      name: GuildMemberRemove\n      title: GUILD_MEMBER_REMOVE\n      summary: User was removed from a guild\n      description: Requires GUILD_MEMBERS privileged intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildMemberUpdate:\n      name: GuildMemberUpdate\n      title: GUILD_MEMBER_UPDATE\n      summary: Guild member was updated\n      description:\
  \ Requires GUILD_MEMBERS privileged intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildMembersChunk:\n      name: GuildMembersChunk\n      title: GUILD_MEMBERS_CHUNK\n      summary: Response to Request Guild Members\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildRoleCreate:\n      name: GuildRoleCreate\n      title: GUILD_ROLE_CREATE\n      summary: Guild role was created\n      description: Requires GUILDS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildRoleUpdate:\n      name: GuildRoleUpdate\n      title: GUILD_ROLE_UPDATE\n      summary: Guild role was updated\n      description: Requires GUILDS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildRoleDelete:\n      name: GuildRoleDelete\n      title: GUILD_ROLE_DELETE\n      summary: Guild role was deleted\n      description: Requires GUILDS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n\
  \    GuildScheduledEventCreate:\n      name: GuildScheduledEventCreate\n      title: GUILD_SCHEDULED_EVENT_CREATE\n      summary: Guild scheduled event was created\n      description: Requires GUILD_SCHEDULED_EVENTS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildScheduledEventUpdate:\n      name: GuildScheduledEventUpdate\n      title: GUILD_SCHEDULED_EVENT_UPDATE\n      summary: Guild scheduled event was updated\n      description: Requires GUILD_SCHEDULED_EVENTS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    GuildScheduledEventDelete:\n      name: GuildScheduledEventDelete\n      title: GUILD_SCHEDULED_EVENT_DELETE\n      summary: Guild scheduled event was deleted\n      description: Requires GUILD_SCHEDULED_EVENTS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    InteractionCreate:\n      name: InteractionCreate\n      title: INTERACTION_CREATE\n      summary: User used an interaction\n\
  \      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    InviteCreate:\n      name: InviteCreate\n      title: INVITE_CREATE\n      summary: Invite to a channel was created\n      description: Requires GUILD_INVITES intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    InviteDelete:\n      name: InviteDelete\n      title: INVITE_DELETE\n      summary: Invite to a channel was deleted\n      description: Requires GUILD_INVITES intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    MessageCreate:\n      name: MessageCreate\n      title: MESSAGE_CREATE\n      summary: Message was created\n      description: Requires GUILD_MESSAGES or DIRECT_MESSAGES intent. MESSAGE_CONTENT privileged intent required for content in guilds.\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    MessageUpdate:\n      name: MessageUpdate\n      title: MESSAGE_UPDATE\n      summary: Message was edited\n      description: Requires\
  \ GUILD_MESSAGES or DIRECT_MESSAGES intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    MessageDelete:\n      name: MessageDelete\n      title: MESSAGE_DELETE\n      summary: Message was deleted\n      description: Requires GUILD_MESSAGES or DIRECT_MESSAGES intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    MessageDeleteBulk:\n      name: MessageDeleteBulk\n      title: MESSAGE_DELETE_BULK\n      summary: Multiple messages were deleted at once\n      description: Requires GUILD_MESSAGES intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    MessageReactionAdd:\n      name: MessageReactionAdd\n      title: MESSAGE_REACTION_ADD\n      summary: User reacted to a message\n      description: Requires GUILD_MESSAGE_REACTIONS or DIRECT_MESSAGE_REACTIONS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    MessageReactionRemove:\n      name: MessageReactionRemove\n      title: MESSAGE_REACTION_REMOVE\n\
  \      summary: User removed a reaction from a message\n      description: Requires GUILD_MESSAGE_REACTIONS or DIRECT_MESSAGE_REACTIONS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    MessageReactionRemoveAll:\n      name: MessageReactionRemoveAll\n      title: MESSAGE_REACTION_REMOVE_ALL\n      summary: All reactions were explicitly removed from a message\n      description: Requires GUILD_MESSAGE_REACTIONS or DIRECT_MESSAGE_REACTIONS intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    PresenceUpdate:\n      name: PresenceUpdate\n      title: PRESENCE_UPDATE\n      summary: User's presence or info was updated\n      description: Requires GUILD_PRESENCES privileged intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    TypingStart:\n      name: TypingStart\n      title: TYPING_START\n      summary: User started typing in a channel\n      description: Requires GUILD_MESSAGE_TYPING or DIRECT_MESSAGE_TYPING\
  \ intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    UserUpdate:\n      name: UserUpdate\n      title: USER_UPDATE\n      summary: Properties about the current user changed\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    VoiceStateUpdate:\n      name: VoiceStateUpdate\n      title: VOICE_STATE_UPDATE\n      summary: Someone joined, left, or moved a voice channel\n      description: Requires GUILD_VOICE_STATES intent\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    VoiceServerUpdate:\n      name: VoiceServerUpdate\n      title: VOICE_SERVER_UPDATE\n      summary: Guild's voice server was updated\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n    WebhooksUpdate:\n      name: WebhooksUpdate\n      title: WEBHOOKS_UPDATE\n      summary: Guild channel webhook was created, updated, or deleted\n      payload:\n        $ref: '#/components/schemas/DispatchEvent'\n  schemas:\n    DispatchEvent:\n\
  \      type: object\n      properties:\n        op:\n          type: integer\n          const: 0\n          description: Opcode 0 for Dispatch events\n        s:\n          type: integer\n          description: Sequence number for resuming\n        t:\n          type: string\n          description: Event name\n        d:\n          type: object\n          description: Event data payload\n      required:\n        - op\n        - s\n        - t\n        - d\n    User:\n      type: object\n      properties:\n        id:\n          type: string\n        username:\n          type: string\n        discriminator:\n          type: string\n        global_name:\n          type: string\n          nullable: true\n        avatar:\n          type: string\n          nullable: true\n        bot:\n          type: boolean\n        flags:\n          type: integer\n      required:\n        - id\n        - username\n    Activity:\n      type: object\n      properties:\n        name:\n          type: string\n\
  \        type:\n          type: integer\n          description: 0=Playing, 1=Streaming, 2=Listening, 3=Watching, 4=Custom, 5=Competing\n        url:\n          type: string\n          nullable: true\n        state:\n          type: string\n          nullable: true\n      required:\n        - name\n        - type\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/discord/refs/heads/main/asyncapi/discord-gateway-api-asyncapi.yml
spec_file: asyncapi/discord-gateway-api-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/discord/refs/heads/main/asyncapi/discord-gateway-api-asyncapi.yml
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
