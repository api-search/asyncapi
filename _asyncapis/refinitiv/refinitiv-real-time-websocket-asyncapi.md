---
api_specs:
- filename: refinitiv-data-platform-openapi.yml
  format: yaml
  label: Refinitiv Data Platform (RDP) API
  slug: refinitiv-data-platform-rdp-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/openapi/refinitiv-data-platform-openapi.yml
- filename: refinitiv-real-time-websocket-asyncapi.yml
  format: yaml
  label: Refinitiv Real-Time WebSocket API
  slug: refinitiv-real-time-websocket-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/asyncapi/refinitiv-real-time-websocket-asyncapi.yml
- filename: refinitiv-datascope-select-openapi.yml
  format: yaml
  label: LSEG DataScope Select - REST API
  slug: lseg-datascope-select-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/openapi/refinitiv-datascope-select-openapi.yml
- filename: refinitiv-world-check-one-openapi.yml
  format: yaml
  label: World-Check One API
  slug: world-check-one-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/openapi/refinitiv-world-check-one-openapi.yml
- filename: refinitiv-qual-id-openapi.yml
  format: yaml
  label: Qual-ID API
  slug: qual-id-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/openapi/refinitiv-qual-id-openapi.yml
- filename: refinitiv-permid-entity-search-openapi.yml
  format: yaml
  label: PermID Entity Search API
  slug: permid-entity-search-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/openapi/refinitiv-permid-entity-search-openapi.yml
channels:
- description: Authentication channel for establishing a streaming session. A Login request must be the first message sent after opening the WebSocket connection. The server responds with a Login refresh indicating session status and entitlements.
  name: login
  operation: publish
  operation_id: sendLoginRequest
  summary: Send login request
- description: Channel for subscribing to and receiving real-time pricing updates for financial instruments. Clients send Market Price requests specifying RICs and receive refresh messages with initial snapshots followed by update messages as prices change.
  name: pricingStream
  operation: publish
  operation_id: sendMarketPriceRequest
  summary: Request market price streaming data
- description: Channel for subscribing to Level 2 market depth data showing the full order book for financial instruments. Provides bid and ask levels with associated sizes.
  name: marketDepth
  operation: publish
  operation_id: sendMarketByPriceRequest
  summary: Request market depth data
- description: Heartbeat channel for keeping the WebSocket connection alive. The server sends periodic ping messages and the client must respond with pong messages to maintain the connection.
  name: ping
  operation: publish
  operation_id: sendPong
  summary: Send pong heartbeat response
description: Low-latency streaming API for real-time market data using WebSocket connections. It supports the Open Message Model (OMM) and allows applications to connect directly to Refinitiv Real-Time distribution systems or the LSEG Data Platform for streaming pricing data, market depth, news, and other real-time content using JSON message formats over standard WebSocket connections.
layout: asyncapi
messages:
- description: ''
  name: LoginRequest
  summary: Initial authentication message sent to establish a streaming session.
  title: Login Request
- description: ''
  name: LoginResponse
  summary: Response to the login request indicating session status and entitlements.
  title: Login Response
- description: ''
  name: MarketPriceRequest
  summary: Request to subscribe to real-time pricing data for instruments.
  title: Market Price Request
- description: ''
  name: MarketPriceRefresh
  summary: Initial snapshot of pricing data for a subscribed instrument.
  title: Market Price Refresh
- description: ''
  name: MarketPriceUpdate
  summary: Incremental pricing update for a subscribed instrument containing only changed fields.
  title: Market Price Update
- description: ''
  name: MarketByPriceRequest
  summary: Request to subscribe to Level 2 market depth data.
  title: Market By Price Request
- description: ''
  name: MarketByPriceRefresh
  summary: Initial snapshot of the full order book for a subscribed instrument.
  title: Market By Price Refresh
- description: ''
  name: MarketByPriceUpdate
  summary: Incremental update to the order book for a subscribed instrument.
  title: Market By Price Update
- description: ''
  name: StatusMessage
  summary: Status message indicating stream state changes such as errors, closures, or redirects.
  title: Status Message
- description: ''
  name: PingMessage
  summary: Server heartbeat message that must be responded to with a pong.
  title: Ping Message
- description: ''
  name: PongMessage
  summary: Client heartbeat response to a server ping message.
  title: Pong Message
name: Refinitiv Real-Time WebSocket API
provider_name: Refinitiv
provider_slug: refinitiv
servers:
- description: LSEG Real-Time Optimized (RTO) cloud streaming service. Endpoint discovery is performed via the RDP streaming/pricing/v1 REST API before connecting. Requires a valid OAuth 2.0 access token from the RDP authentication service.
  name: realTimeOptimized
  protocol: wss
  url: wss://api.refinitiv.com/streaming/pricing/v1/
- description: On-premise Real-Time Distribution System (ADS/RTDS) WebSocket endpoint. Hostname and port are configured based on the local deployment. Authentication uses DACS username and optional application ID.
  name: realTimeDistribution
  protocol: wss
  url: wss://{ads-hostname}:{port}/WebSocket
slug: refinitiv-real-time-websocket-asyncapi
source_filename: refinitiv-real-time-websocket-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Refinitiv Real-Time WebSocket API\n  version: '1.0.0'\n  description: >-\n    Low-latency streaming API for real-time market data using WebSocket\n    connections. It supports the Open Message Model (OMM) and allows\n    applications to connect directly to Refinitiv Real-Time distribution\n    systems or the LSEG Data Platform for streaming pricing data, market\n    depth, news, and other real-time content using JSON message formats\n    over standard WebSocket connections.\n  contact:\n    name: LSEG Developer Support\n    url: https://developers.lseg.com/en/support\n  license:\n    name: LSEG Terms of Service\n    url: https://developers.lseg.com/en/terms-and-conditions\nexternalDocs:\n  description: Refinitiv Real-Time WebSocket API Documentation\n  url: https://developers.lseg.com/en/api-catalog/refinitiv-real-time-opnsrc/refinitiv-websocket-api/documentation\nservers:\n  realTimeOptimized:\n    url: wss://api.refinitiv.com/streaming/pricing/v1/\n\
  \    protocol: wss\n    description: >-\n      LSEG Real-Time Optimized (RTO) cloud streaming service. Endpoint\n      discovery is performed via the RDP streaming/pricing/v1 REST API\n      before connecting. Requires a valid OAuth 2.0 access token from the\n      RDP authentication service.\n    security:\n      - bearerToken: []\n  realTimeDistribution:\n    url: wss://{ads-hostname}:{port}/WebSocket\n    protocol: wss\n    description: >-\n      On-premise Real-Time Distribution System (ADS/RTDS) WebSocket\n      endpoint. Hostname and port are configured based on the local\n      deployment. Authentication uses DACS username and optional\n      application ID.\ndefaultContentType: application/json\nchannels:\n  login:\n    description: >-\n      Authentication channel for establishing a streaming session. A Login\n      request must be the first message sent after opening the WebSocket\n      connection. The server responds with a Login refresh indicating\n      session status and\
  \ entitlements.\n    publish:\n      operationId: sendLoginRequest\n      summary: Send login request\n      message:\n        $ref: '#/components/messages/LoginRequest'\n    subscribe:\n      operationId: receiveLoginResponse\n      summary: Receive login response\n      message:\n        $ref: '#/components/messages/LoginResponse'\n  pricingStream:\n    description: >-\n      Channel for subscribing to and receiving real-time pricing updates\n      for financial instruments. Clients send Market Price requests\n      specifying RICs and receive refresh messages with initial snapshots\n      followed by update messages as prices change.\n    publish:\n      operationId: sendMarketPriceRequest\n      summary: Request market price streaming data\n      message:\n        $ref: '#/components/messages/MarketPriceRequest'\n    subscribe:\n      operationId: receiveMarketPriceData\n      summary: Receive market price updates\n      message:\n        oneOf:\n          - $ref: '#/components/messages/MarketPriceRefresh'\n\
  \          - $ref: '#/components/messages/MarketPriceUpdate'\n          - $ref: '#/components/messages/StatusMessage'\n  marketDepth:\n    description: >-\n      Channel for subscribing to Level 2 market depth data showing the\n      full order book for financial instruments. Provides bid and ask\n      levels with associated sizes.\n    publish:\n      operationId: sendMarketByPriceRequest\n      summary: Request market depth data\n      message:\n        $ref: '#/components/messages/MarketByPriceRequest'\n    subscribe:\n      operationId: receiveMarketByPriceData\n      summary: Receive market depth updates\n      message:\n        oneOf:\n          - $ref: '#/components/messages/MarketByPriceRefresh'\n          - $ref: '#/components/messages/MarketByPriceUpdate'\n          - $ref: '#/components/messages/StatusMessage'\n  ping:\n    description: >-\n      Heartbeat channel for keeping the WebSocket connection alive. The\n      server sends periodic ping messages and the client must\
  \ respond with\n      pong messages to maintain the connection.\n    publish:\n      operationId: sendPong\n      summary: Send pong heartbeat response\n      message:\n        $ref: '#/components/messages/PongMessage'\n    subscribe:\n      operationId: receivePing\n      summary: Receive ping heartbeat\n      message:\n        $ref: '#/components/messages/PingMessage'\ncomponents:\n  securitySchemes:\n    bearerToken:\n      type: http\n      scheme: bearer\n      bearerFormat: JWT\n      description: >-\n        OAuth 2.0 Bearer token obtained from the RDP authentication\n        service at /auth/oauth2/v1/token.\n  messages:\n    LoginRequest:\n      name: LoginRequest\n      title: Login Request\n      summary: >-\n        Initial authentication message sent to establish a streaming session.\n      payload:\n        type: object\n        required:\n          - ID\n          - Domain\n          - Key\n        properties:\n          ID:\n            type: integer\n            description:\
  \ >-\n              Stream identifier for the login stream, typically 1.\n          Domain:\n            type: string\n            const: Login\n            description: >-\n              The message domain, always Login for authentication.\n          Key:\n            type: object\n            properties:\n              Name:\n                type: string\n                description: >-\n                  The machine ID or DACS username for authentication.\n              Elements:\n                type: object\n                properties:\n                  ApplicationId:\n                    type: string\n                    description: >-\n                      The application identifier, typically 256.\n                  Position:\n                    type: string\n                    description: >-\n                      The application position, typically the IP address\n                      and hostname.\n                  AuthenticationToken:\n                    type: string\n\
  \                    description: >-\n                      The OAuth 2.0 access token for RTO connections.\n              NameType:\n                type: string\n                description: >-\n                  The type of name used for authentication.\n                enum:\n                  - AuthnToken\n                  - USER_NAME\n    LoginResponse:\n      name: LoginResponse\n      title: Login Response\n      summary: >-\n        Response to the login request indicating session status and\n        entitlements.\n      payload:\n        type: object\n        properties:\n          ID:\n            type: integer\n            description: >-\n              The stream identifier matching the login request.\n          Type:\n            type: string\n            description: >-\n              The message type, typically Refresh for a successful login.\n            enum:\n              - Refresh\n              - Status\n          Domain:\n            type: string\n            const:\
  \ Login\n          Key:\n            type: object\n            properties:\n              Name:\n                type: string\n                description: >-\n                  The authenticated username.\n          State:\n            type: object\n            properties:\n              Stream:\n                type: string\n                description: >-\n                  Stream state, Open for active sessions.\n              Data:\n                type: string\n                description: >-\n                  Data state, Ok for successful authentication.\n              Text:\n                type: string\n                description: >-\n                  Status text message.\n          Elements:\n            type: object\n            properties:\n              MaxMsgSize:\n                type: integer\n                description: >-\n                  Maximum message size supported.\n    MarketPriceRequest:\n      name: MarketPriceRequest\n      title: Market Price Request\n\
  \      summary: >-\n        Request to subscribe to real-time pricing data for instruments.\n      payload:\n        type: object\n        required:\n          - ID\n          - Key\n        properties:\n          ID:\n            type: integer\n            description: >-\n              Unique stream identifier for this subscription.\n          Key:\n            type: object\n            properties:\n              Name:\n                type: string\n                description: >-\n                  The RIC or instrument identifier to subscribe to.\n              Service:\n                type: string\n                description: >-\n                  The data service name such as ELEKTRON_DD.\n          Streaming:\n            type: boolean\n            description: >-\n              Whether to receive streaming updates or just a snapshot.\n          View:\n            type: array\n            items:\n              type: integer\n            description: >-\n              Field IDs\
  \ to include in the response, for bandwidth\n              optimization.\n    MarketPriceRefresh:\n      name: MarketPriceRefresh\n      title: Market Price Refresh\n      summary: >-\n        Initial snapshot of pricing data for a subscribed instrument.\n      payload:\n        type: object\n        properties:\n          ID:\n            type: integer\n            description: >-\n              The stream identifier for this subscription.\n          Type:\n            type: string\n            const: Refresh\n          Key:\n            type: object\n            properties:\n              Name:\n                type: string\n                description: >-\n                  The RIC of the instrument.\n              Service:\n                type: string\n                description: >-\n                  The data service name.\n          State:\n            type: object\n            properties:\n              Stream:\n                type: string\n                description: >-\n \
  \                 Stream state.\n              Data:\n                type: string\n                description: >-\n                  Data state.\n          Fields:\n            type: object\n            additionalProperties: true\n            description: >-\n              Map of field names to their current values. Common fields\n              include BID, ASK, TRDPRC_1 (last trade), ACVOL_1 (volume),\n              HIGH_1, LOW_1, OPEN_PRC, and HST_CLOSE.\n    MarketPriceUpdate:\n      name: MarketPriceUpdate\n      title: Market Price Update\n      summary: >-\n        Incremental pricing update for a subscribed instrument containing\n        only changed fields.\n      payload:\n        type: object\n        properties:\n          ID:\n            type: integer\n            description: >-\n              The stream identifier for this subscription.\n          Type:\n            type: string\n            const: Update\n          UpdateType:\n            type: string\n            description:\
  \ >-\n              The type of update such as Trade or Quote.\n          Fields:\n            type: object\n            additionalProperties: true\n            description: >-\n              Map of changed field names to their new values.\n    MarketByPriceRequest:\n      name: MarketByPriceRequest\n      title: Market By Price Request\n      summary: >-\n        Request to subscribe to Level 2 market depth data.\n      payload:\n        type: object\n        required:\n          - ID\n          - Domain\n          - Key\n        properties:\n          ID:\n            type: integer\n            description: >-\n              Unique stream identifier.\n          Domain:\n            type: string\n            const: MarketByPrice\n          Key:\n            type: object\n            properties:\n              Name:\n                type: string\n                description: >-\n                  The RIC of the instrument.\n              Service:\n                type: string\n       \
  \         description: >-\n                  The data service name.\n    MarketByPriceRefresh:\n      name: MarketByPriceRefresh\n      title: Market By Price Refresh\n      summary: >-\n        Initial snapshot of the full order book for a subscribed instrument.\n      payload:\n        type: object\n        properties:\n          ID:\n            type: integer\n          Type:\n            type: string\n            const: Refresh\n          Domain:\n            type: string\n            const: MarketByPrice\n          Key:\n            type: object\n            properties:\n              Name:\n                type: string\n              Service:\n                type: string\n          Map:\n            type: object\n            description: >-\n              Map entries containing bid and ask price levels with\n              associated order sizes.\n    MarketByPriceUpdate:\n      name: MarketByPriceUpdate\n      title: Market By Price Update\n      summary: >-\n        Incremental\
  \ update to the order book for a subscribed instrument.\n      payload:\n        type: object\n        properties:\n          ID:\n            type: integer\n          Type:\n            type: string\n            const: Update\n          Domain:\n            type: string\n            const: MarketByPrice\n          Map:\n            type: object\n            description: >-\n              Updated map entries for changed price levels.\n    StatusMessage:\n      name: StatusMessage\n      title: Status Message\n      summary: >-\n        Status message indicating stream state changes such as errors,\n        closures, or redirects.\n      payload:\n        type: object\n        properties:\n          ID:\n            type: integer\n            description: >-\n              The stream identifier.\n          Type:\n            type: string\n            const: Status\n          State:\n            type: object\n            properties:\n              Stream:\n                type: string\n\
  \                description: >-\n                  Stream state such as Open, Closed, or ClosedRecover.\n              Data:\n                type: string\n                description: >-\n                  Data state such as Ok or Suspect.\n              Code:\n                type: string\n                description: >-\n                  Status code such as NotFound or NotEntitled.\n              Text:\n                type: string\n                description: >-\n                  Human-readable status message.\n    PingMessage:\n      name: PingMessage\n      title: Ping Message\n      summary: >-\n        Server heartbeat message that must be responded to with a pong.\n      payload:\n        type: object\n        properties:\n          Type:\n            type: string\n            const: Ping\n    PongMessage:\n      name: PongMessage\n      title: Pong Message\n      summary: >-\n        Client heartbeat response to a server ping message.\n      payload:\n        type: object\n\
  \        properties:\n          Type:\n            type: string\n            const: Pong\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/asyncapi/refinitiv-real-time-websocket-asyncapi.yml
spec_file: asyncapi/refinitiv-real-time-websocket-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/asyncapi/refinitiv-real-time-websocket-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
