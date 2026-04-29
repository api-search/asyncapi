---
api_specs:
- filename: coinbase-advanced-trade-openapi.yml
  format: yaml
  label: Coinbase Advanced Trade API
  slug: advanced-trade-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/openapi/coinbase-advanced-trade-openapi.yml
- filename: coinbase-exchange-openapi.yml
  format: yaml
  label: Coinbase Exchange API
  slug: exchange-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/openapi/coinbase-exchange-openapi.yml
- filename: coinbase-prime-openapi.yml
  format: yaml
  label: Coinbase Prime API
  slug: prime-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/openapi/coinbase-prime-openapi.yml
- filename: coinbase-onramp-openapi.yml
  format: yaml
  label: Coinbase Onramp API
  slug: onramp-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/openapi/coinbase-onramp-openapi.yml
- filename: coinbase-commerce-openapi.yml
  format: yaml
  label: Coinbase Commerce API
  slug: commerce-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/openapi/coinbase-commerce-openapi.yml
channels:
- description: Heartbeat channel that sends messages once per second for subscribed products. Used to track the last trade ID and detect any missed messages from the REST API.
  name: /heartbeat
  operation: subscribe
  operation_id: receiveHeartbeat
  summary: Receive heartbeat messages
- description: Ticker channel that provides real-time price updates when bids and offers are matched. Provides snapshot-level market data.
  name: /ticker
  operation: subscribe
  operation_id: receiveTickerUpdate
  summary: Receive ticker updates
- description: Level 2 channel that guarantees delivery of all order book updates. Sends an initial snapshot followed by l2update messages with price level changes. The easiest way to maintain an accurate order book.
  name: /level2
  operation: subscribe
  operation_id: receiveLevel2Update
  summary: Receive level 2 order book updates
- description: Level 2 batch channel that delivers order book updates in batches every 50 milliseconds. Does not require authentication and provides a good balance between accuracy and bandwidth usage.
  name: /level2_batch
  operation: subscribe
  operation_id: receiveLevel2BatchUpdate
  summary: Receive batched level 2 updates
- description: Matches channel that provides real-time trade execution data. Each message represents a trade that has been executed on the exchange.
  name: /matches
  operation: subscribe
  operation_id: receiveMatch
  summary: Receive trade match events
- description: Full channel that provides the complete order lifecycle feed including received, open, done, match, and change messages. Provides the most detailed view of order book activity but generates significant traffic.
  name: /full
  operation: subscribe
  operation_id: receiveFullFeed
  summary: Receive full order lifecycle events
- description: Status channel that provides product status updates including trading status and currency details.
  name: /status
  operation: subscribe
  operation_id: receiveStatus
  summary: Receive product status updates
description: The Coinbase Exchange WebSocket Feed provides real-time market data for the Exchange platform. It supports multiple channels including heartbeat, ticker, level2 order book, full order feed, and user order updates. The WebSocket feed delivers low-latency streaming data for professional and institutional traders.
layout: asyncapi
messages:
- description: ''
  name: HeartbeatMessage
  summary: Periodic heartbeat message with last trade ID
  title: Heartbeat
- description: ''
  name: TickerMessage
  summary: Real-time ticker update on match
  title: Ticker
- description: ''
  name: Level2SnapshotMessage
  summary: Full order book snapshot
  title: Level 2 Snapshot
- description: ''
  name: Level2UpdateMessage
  summary: Incremental order book update
  title: Level 2 Update
- description: ''
  name: MatchMessage
  summary: Trade execution match event
  title: Match
- description: ''
  name: ReceivedMessage
  summary: New order received by the exchange
  title: Order Received
- description: ''
  name: OpenMessage
  summary: Order placed on the order book
  title: Order Opened
- description: ''
  name: DoneMessage
  summary: Order removed from the order book
  title: Order Done
- description: ''
  name: ChangeMessage
  summary: Order size or funds changed
  title: Order Changed
- description: ''
  name: StatusMessage
  summary: Product trading status update
  title: Product Status
name: Coinbase Exchange WebSocket Feed
provider_name: Coinbase
provider_slug: coinbase
servers:
- description: Production WebSocket feed for Exchange market data
  name: production
  protocol: wss
  url: wss://ws-feed.exchange.coinbase.com
slug: coinbase-exchange-asyncapi
source_filename: coinbase-exchange-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Coinbase Exchange WebSocket Feed\n  description: >-\n    The Coinbase Exchange WebSocket Feed provides real-time market data for\n    the Exchange platform. It supports multiple channels including heartbeat,\n    ticker, level2 order book, full order feed, and user order updates. The\n    WebSocket feed delivers low-latency streaming data for professional and\n    institutional traders.\n  version: '1.0'\n  contact:\n    name: Coinbase Developer Support\n    url: https://help.coinbase.com\nexternalDocs:\n  description: Exchange WebSocket Documentation\n  url: https://docs.cdp.coinbase.com/exchange/websocket-feed/channels\nservers:\n  production:\n    url: wss://ws-feed.exchange.coinbase.com\n    protocol: wss\n    description: Production WebSocket feed for Exchange market data\n    security:\n      - apiKey: []\nchannels:\n  /heartbeat:\n    description: >-\n      Heartbeat channel that sends messages once per second for subscribed\n      products.\
  \ Used to track the last trade ID and detect any missed\n      messages from the REST API.\n    subscribe:\n      operationId: receiveHeartbeat\n      summary: Receive heartbeat messages\n      message:\n        $ref: '#/components/messages/HeartbeatMessage'\n  /ticker:\n    description: >-\n      Ticker channel that provides real-time price updates when bids and\n      offers are matched. Provides snapshot-level market data.\n    subscribe:\n      operationId: receiveTickerUpdate\n      summary: Receive ticker updates\n      message:\n        $ref: '#/components/messages/TickerMessage'\n  /level2:\n    description: >-\n      Level 2 channel that guarantees delivery of all order book updates.\n      Sends an initial snapshot followed by l2update messages with price\n      level changes. The easiest way to maintain an accurate order book.\n    subscribe:\n      operationId: receiveLevel2Update\n      summary: Receive level 2 order book updates\n      message:\n        oneOf:\n         \
  \ - $ref: '#/components/messages/Level2SnapshotMessage'\n          - $ref: '#/components/messages/Level2UpdateMessage'\n  /level2_batch:\n    description: >-\n      Level 2 batch channel that delivers order book updates in batches\n      every 50 milliseconds. Does not require authentication and provides\n      a good balance between accuracy and bandwidth usage.\n    subscribe:\n      operationId: receiveLevel2BatchUpdate\n      summary: Receive batched level 2 updates\n      message:\n        $ref: '#/components/messages/Level2UpdateMessage'\n  /matches:\n    description: >-\n      Matches channel that provides real-time trade execution data. Each\n      message represents a trade that has been executed on the exchange.\n    subscribe:\n      operationId: receiveMatch\n      summary: Receive trade match events\n      message:\n        $ref: '#/components/messages/MatchMessage'\n  /full:\n    description: >-\n      Full channel that provides the complete order lifecycle feed including\n\
  \      received, open, done, match, and change messages. Provides the most\n      detailed view of order book activity but generates significant traffic.\n    subscribe:\n      operationId: receiveFullFeed\n      summary: Receive full order lifecycle events\n      message:\n        oneOf:\n          - $ref: '#/components/messages/ReceivedMessage'\n          - $ref: '#/components/messages/OpenMessage'\n          - $ref: '#/components/messages/DoneMessage'\n          - $ref: '#/components/messages/MatchMessage'\n          - $ref: '#/components/messages/ChangeMessage'\n  /status:\n    description: >-\n      Status channel that provides product status updates including trading\n      status and currency details.\n    subscribe:\n      operationId: receiveStatus\n      summary: Receive product status updates\n      message:\n        $ref: '#/components/messages/StatusMessage'\ncomponents:\n  securitySchemes:\n    apiKey:\n      type: apiKey\n      in: user\n      description: >-\n        Exchange\
  \ API key authentication for WebSocket connections using HMAC\n        SHA-256 signature in the subscription message.\n  messages:\n    HeartbeatMessage:\n      name: heartbeat\n      title: Heartbeat\n      summary: Periodic heartbeat message with last trade ID\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/HeartbeatPayload'\n    TickerMessage:\n      name: ticker\n      title: Ticker\n      summary: Real-time ticker update on match\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TickerPayload'\n    Level2SnapshotMessage:\n      name: snapshot\n      title: Level 2 Snapshot\n      summary: Full order book snapshot\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/Level2SnapshotPayload'\n    Level2UpdateMessage:\n      name: l2update\n      title: Level 2 Update\n      summary: Incremental order book update\n      contentType: application/json\n      payload:\n \
  \       $ref: '#/components/schemas/Level2UpdatePayload'\n    MatchMessage:\n      name: match\n      title: Match\n      summary: Trade execution match event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/MatchPayload'\n    ReceivedMessage:\n      name: received\n      title: Order Received\n      summary: New order received by the exchange\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ReceivedPayload'\n    OpenMessage:\n      name: open\n      title: Order Opened\n      summary: Order placed on the order book\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OpenPayload'\n    DoneMessage:\n      name: done\n      title: Order Done\n      summary: Order removed from the order book\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DonePayload'\n    ChangeMessage:\n      name: change\n      title: Order Changed\n      summary:\
  \ Order size or funds changed\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ChangePayload'\n    StatusMessage:\n      name: status\n      title: Product Status\n      summary: Product trading status update\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/StatusPayload'\n  schemas:\n    HeartbeatPayload:\n      type: object\n      description: Heartbeat message with connection and trade info\n      properties:\n        type:\n          type: string\n          enum:\n            - heartbeat\n        sequence:\n          type: integer\n          description: Sequence number\n        last_trade_id:\n          type: integer\n          description: Last trade ID to detect missed trades\n        product_id:\n          type: string\n          description: Product identifier\n        time:\n          type: string\n          format: date-time\n          description: Server timestamp\n    TickerPayload:\n      type:\
  \ object\n      description: Ticker update with latest trade and market stats\n      properties:\n        type:\n          type: string\n          enum:\n            - ticker\n        trade_id:\n          type: integer\n          description: Latest trade ID\n        sequence:\n          type: integer\n          description: Sequence number\n        product_id:\n          type: string\n          description: Product identifier\n        price:\n          type: string\n          description: Latest trade price\n        side:\n          type: string\n          description: Taker side\n          enum:\n            - buy\n            - sell\n        last_size:\n          type: string\n          description: Size of the last trade\n        best_bid:\n          type: string\n          description: Best bid price\n        best_ask:\n          type: string\n          description: Best ask price\n        open_24h:\n          type: string\n          description: 24-hour opening price\n        volume_24h:\n\
  \          type: string\n          description: 24-hour volume\n        low_24h:\n          type: string\n          description: 24-hour low price\n        high_24h:\n          type: string\n          description: 24-hour high price\n        volume_30d:\n          type: string\n          description: 30-day volume\n        time:\n          type: string\n          format: date-time\n          description: Timestamp\n    Level2SnapshotPayload:\n      type: object\n      description: Full order book snapshot with all price levels\n      properties:\n        type:\n          type: string\n          enum:\n            - snapshot\n        product_id:\n          type: string\n          description: Product identifier\n        bids:\n          type: array\n          description: Bid levels as [price, size] tuples\n          items:\n            type: array\n            items:\n              type: string\n        asks:\n          type: array\n          description: Ask levels as [price, size] tuples\n\
  \          items:\n            type: array\n            items:\n              type: string\n    Level2UpdatePayload:\n      type: object\n      description: Incremental order book update\n      properties:\n        type:\n          type: string\n          enum:\n            - l2update\n        product_id:\n          type: string\n          description: Product identifier\n        time:\n          type: string\n          format: date-time\n          description: Update timestamp\n        changes:\n          type: array\n          description: Price level changes as [side, price, size] tuples\n          items:\n            type: array\n            items:\n              type: string\n    MatchPayload:\n      type: object\n      description: Trade execution match event\n      properties:\n        type:\n          type: string\n          enum:\n            - match\n            - last_match\n        trade_id:\n          type: integer\n          description: Trade identifier\n        sequence:\n\
  \          type: integer\n          description: Sequence number\n        maker_order_id:\n          type: string\n          description: Maker order ID\n        taker_order_id:\n          type: string\n          description: Taker order ID\n        product_id:\n          type: string\n          description: Product identifier\n        size:\n          type: string\n          description: Trade size\n        price:\n          type: string\n          description: Trade price\n        side:\n          type: string\n          description: Taker side\n          enum:\n            - buy\n            - sell\n        time:\n          type: string\n          format: date-time\n          description: Trade time\n    ReceivedPayload:\n      type: object\n      description: Order received by the matching engine\n      properties:\n        type:\n          type: string\n          enum:\n            - received\n        order_id:\n          type: string\n          description: Order identifier\n   \
  \     order_type:\n          type: string\n          description: Order type\n          enum:\n            - limit\n            - market\n        size:\n          type: string\n          description: Order size\n        price:\n          type: string\n          description: Order price\n        side:\n          type: string\n          description: Order side\n          enum:\n            - buy\n            - sell\n        product_id:\n          type: string\n          description: Product identifier\n        sequence:\n          type: integer\n          description: Sequence number\n        time:\n          type: string\n          format: date-time\n          description: Received time\n    OpenPayload:\n      type: object\n      description: Order opened on the order book\n      properties:\n        type:\n          type: string\n          enum:\n            - open\n        order_id:\n          type: string\n          description: Order identifier\n        price:\n          type: string\n\
  \          description: Order price\n        remaining_size:\n          type: string\n          description: Remaining size on the book\n        side:\n          type: string\n          description: Order side\n          enum:\n            - buy\n            - sell\n        product_id:\n          type: string\n          description: Product identifier\n        sequence:\n          type: integer\n          description: Sequence number\n        time:\n          type: string\n          format: date-time\n          description: Open time\n    DonePayload:\n      type: object\n      description: Order removed from the order book\n      properties:\n        type:\n          type: string\n          enum:\n            - done\n        order_id:\n          type: string\n          description: Order identifier\n        reason:\n          type: string\n          description: Reason the order was removed\n          enum:\n            - filled\n            - canceled\n        price:\n          type:\
  \ string\n          description: Order price\n        remaining_size:\n          type: string\n          description: Remaining size when removed\n        side:\n          type: string\n          description: Order side\n          enum:\n            - buy\n            - sell\n        product_id:\n          type: string\n          description: Product identifier\n        sequence:\n          type: integer\n          description: Sequence number\n        time:\n          type: string\n          format: date-time\n          description: Done time\n    ChangePayload:\n      type: object\n      description: Order size or funds changed\n      properties:\n        type:\n          type: string\n          enum:\n            - change\n        order_id:\n          type: string\n          description: Order identifier\n        new_size:\n          type: string\n          description: New order size\n        old_size:\n          type: string\n          description: Previous order size\n        price:\n\
  \          type: string\n          description: Order price\n        side:\n          type: string\n          description: Order side\n          enum:\n            - buy\n            - sell\n        product_id:\n          type: string\n          description: Product identifier\n        sequence:\n          type: integer\n          description: Sequence number\n        time:\n          type: string\n          format: date-time\n          description: Change time\n    StatusPayload:\n      type: object\n      description: Product status update\n      properties:\n        type:\n          type: string\n          enum:\n            - status\n        products:\n          type: array\n          description: Product status entries\n          items:\n            type: object\n            properties:\n              id:\n                type: string\n                description: Product identifier\n              base_currency:\n                type: string\n                description: Base currency\n\
  \              quote_currency:\n                type: string\n                description: Quote currency\n              status:\n                type: string\n                description: Trading status\n              status_message:\n                type: string\n                description: Status message\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/asyncapi/coinbase-exchange-asyncapi.yml
spec_file: asyncapi/coinbase-exchange-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/asyncapi/coinbase-exchange-asyncapi.yml
tags:
- Blockchain
- Cryptocurrency
- Custody
- Exchange
- Onramp
- Payments
- Trading
- Wallet
- Web3
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
