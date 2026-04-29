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
- description: Heartbeat channel that sends a message every second to verify the connection is alive. Includes a heartbeat counter to detect missed messages.
  name: /heartbeats
  operation: subscribe
  operation_id: receiveHeartbeat
  summary: Receive heartbeat messages
- description: Candle channel that streams OHLCV candle data updates for subscribed products. Each message includes the start time, open, high, low, close prices, and volume for the current candle interval.
  name: /candles
  operation: subscribe
  operation_id: receiveCandleUpdate
  summary: Receive candle data updates
- description: Market trades channel that streams real-time trade executions as they happen. Each message includes the trade ID, product, price, size, and side of the trade.
  name: /market_trades
  operation: subscribe
  operation_id: receiveMarketTrade
  summary: Receive market trade events
- description: Ticker channel that provides real-time price updates every time a match happens. Updates are batched in case of cascading matches, reducing bandwidth requirements while maintaining price accuracy.
  name: /ticker
  operation: subscribe
  operation_id: receiveTickerUpdate
  summary: Receive ticker price updates
- description: Ticker batch channel that provides batched price updates at a reduced frequency compared to the ticker channel, suitable for applications that do not need real-time updates.
  name: /ticker_batch
  operation: subscribe
  operation_id: receiveTickerBatchUpdate
  summary: Receive batched ticker updates
- description: Level 2 order book channel that guarantees delivery of all order book updates. Sends an initial snapshot followed by incremental updates. The most reliable way to maintain a local copy of the order book.
  name: /level2
  operation: subscribe
  operation_id: receiveLevel2Update
  summary: Receive level 2 order book updates
- description: User channel that sends updates on all open orders and current positions for the authenticated user. Accepts multiple product IDs in the subscription; if none are provided, updates for all products are sent. Requires authentication.
  name: /user
  operation: subscribe
  operation_id: receiveUserUpdate
  summary: Receive user order and position updates
description: The Coinbase Advanced Trade WebSocket API provides real-time market data streaming including heartbeats, ticker updates, candle data, market trades, level2 order book updates, and user order status changes. All channels except the User channel can be used without authentication, though authenticated connections provide a more reliable experience.
layout: asyncapi
messages:
- description: ''
  name: HeartbeatMessage
  summary: Periodic heartbeat to verify connection liveness
  title: Heartbeat
- description: ''
  name: CandleMessage
  summary: OHLCV candle data update for a product
  title: Candle Update
- description: ''
  name: MarketTradeMessage
  summary: Real-time trade execution event
  title: Market Trade
- description: ''
  name: TickerMessage
  summary: Real-time price update on match
  title: Ticker Update
- description: ''
  name: Level2SnapshotMessage
  summary: Full order book snapshot
  title: Level 2 Snapshot
- description: ''
  name: Level2UpdateMessage
  summary: Incremental order book update
  title: Level 2 Update
- description: ''
  name: UserMessage
  summary: User order and position update
  title: User Update
name: Coinbase Advanced Trade WebSocket
provider_name: Coinbase
provider_slug: coinbase
servers:
- description: Production WebSocket server for Advanced Trade market data
  name: production
  protocol: wss
  url: wss://advanced-trade-ws.coinbase.com
slug: coinbase-advanced-trade-asyncapi
source_filename: coinbase-advanced-trade-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Coinbase Advanced Trade WebSocket\n  description: >-\n    The Coinbase Advanced Trade WebSocket API provides real-time market data\n    streaming including heartbeats, ticker updates, candle data, market trades,\n    level2 order book updates, and user order status changes. All channels\n    except the User channel can be used without authentication, though\n    authenticated connections provide a more reliable experience.\n  version: '1.0'\n  contact:\n    name: Coinbase Developer Support\n    url: https://help.coinbase.com\nexternalDocs:\n  description: Advanced Trade WebSocket Documentation\n  url: https://docs.cdp.coinbase.com/coinbase-app/advanced-trade-apis/websocket/websocket-channels\nservers:\n  production:\n    url: wss://advanced-trade-ws.coinbase.com\n    protocol: wss\n    description: Production WebSocket server for Advanced Trade market data\n    security:\n      - apiKey: []\nchannels:\n  /heartbeats:\n    description: >-\n \
  \     Heartbeat channel that sends a message every second to verify the\n      connection is alive. Includes a heartbeat counter to detect missed\n      messages.\n    subscribe:\n      operationId: receiveHeartbeat\n      summary: Receive heartbeat messages\n      message:\n        $ref: '#/components/messages/HeartbeatMessage'\n  /candles:\n    description: >-\n      Candle channel that streams OHLCV candle data updates for subscribed\n      products. Each message includes the start time, open, high, low, close\n      prices, and volume for the current candle interval.\n    subscribe:\n      operationId: receiveCandleUpdate\n      summary: Receive candle data updates\n      message:\n        $ref: '#/components/messages/CandleMessage'\n  /market_trades:\n    description: >-\n      Market trades channel that streams real-time trade executions as they\n      happen. Each message includes the trade ID, product, price, size, and\n      side of the trade.\n    subscribe:\n      operationId:\
  \ receiveMarketTrade\n      summary: Receive market trade events\n      message:\n        $ref: '#/components/messages/MarketTradeMessage'\n  /ticker:\n    description: >-\n      Ticker channel that provides real-time price updates every time a match\n      happens. Updates are batched in case of cascading matches, reducing\n      bandwidth requirements while maintaining price accuracy.\n    subscribe:\n      operationId: receiveTickerUpdate\n      summary: Receive ticker price updates\n      message:\n        $ref: '#/components/messages/TickerMessage'\n  /ticker_batch:\n    description: >-\n      Ticker batch channel that provides batched price updates at a reduced\n      frequency compared to the ticker channel, suitable for applications\n      that do not need real-time updates.\n    subscribe:\n      operationId: receiveTickerBatchUpdate\n      summary: Receive batched ticker updates\n      message:\n        $ref: '#/components/messages/TickerMessage'\n  /level2:\n    description:\
  \ >-\n      Level 2 order book channel that guarantees delivery of all order book\n      updates. Sends an initial snapshot followed by incremental updates.\n      The most reliable way to maintain a local copy of the order book.\n    subscribe:\n      operationId: receiveLevel2Update\n      summary: Receive level 2 order book updates\n      message:\n        oneOf:\n          - $ref: '#/components/messages/Level2SnapshotMessage'\n          - $ref: '#/components/messages/Level2UpdateMessage'\n  /user:\n    description: >-\n      User channel that sends updates on all open orders and current positions\n      for the authenticated user. Accepts multiple product IDs in the\n      subscription; if none are provided, updates for all products are sent.\n      Requires authentication.\n    subscribe:\n      operationId: receiveUserUpdate\n      summary: Receive user order and position updates\n      message:\n        $ref: '#/components/messages/UserMessage'\ncomponents:\n  securitySchemes:\n\
  \    apiKey:\n      type: apiKey\n      in: user\n      description: >-\n        CDP API key authentication for WebSocket connections. Include the\n        API key, signature, and timestamp in the subscription message.\n  messages:\n    HeartbeatMessage:\n      name: heartbeat\n      title: Heartbeat\n      summary: Periodic heartbeat to verify connection liveness\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/HeartbeatPayload'\n    CandleMessage:\n      name: candle\n      title: Candle Update\n      summary: OHLCV candle data update for a product\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CandlePayload'\n    MarketTradeMessage:\n      name: market_trade\n      title: Market Trade\n      summary: Real-time trade execution event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/MarketTradePayload'\n    TickerMessage:\n      name: ticker\n      title: Ticker\
  \ Update\n      summary: Real-time price update on match\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TickerPayload'\n    Level2SnapshotMessage:\n      name: l2_snapshot\n      title: Level 2 Snapshot\n      summary: Full order book snapshot\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/Level2SnapshotPayload'\n    Level2UpdateMessage:\n      name: l2_update\n      title: Level 2 Update\n      summary: Incremental order book update\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/Level2UpdatePayload'\n    UserMessage:\n      name: user\n      title: User Update\n      summary: User order and position update\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/UserPayload'\n  schemas:\n    HeartbeatPayload:\n      type: object\n      description: Heartbeat message payload\n      properties:\n        channel:\n          type:\
  \ string\n          description: Channel name\n          enum:\n            - heartbeats\n        client_id:\n          type: string\n          description: Client connection identifier\n        timestamp:\n          type: string\n          format: date-time\n          description: Server timestamp\n        heartbeat_counter:\n          type: integer\n          description: >-\n            Incrementing counter to verify no messages were missed\n        sequence_num:\n          type: integer\n          description: Sequence number\n    CandlePayload:\n      type: object\n      description: Candle update payload\n      properties:\n        channel:\n          type: string\n          description: Channel name\n          enum:\n            - candles\n        client_id:\n          type: string\n          description: Client connection identifier\n        timestamp:\n          type: string\n          format: date-time\n          description: Event timestamp\n        sequence_num:\n         \
  \ type: integer\n          description: Sequence number\n        events:\n          type: array\n          description: Candle events\n          items:\n            type: object\n            properties:\n              type:\n                type: string\n                description: Event type\n              candles:\n                type: array\n                items:\n                  type: object\n                  properties:\n                    start:\n                      type: string\n                      description: UNIX timestamp for candle start\n                    high:\n                      type: string\n                      description: Highest price\n                    low:\n                      type: string\n                      description: Lowest price\n                    open:\n                      type: string\n                      description: Opening price\n                    close:\n                      type: string\n                      description:\
  \ Closing price\n                    volume:\n                      type: string\n                      description: Volume traded\n                    product_id:\n                      type: string\n                      description: Product identifier\n    MarketTradePayload:\n      type: object\n      description: Market trade event payload\n      properties:\n        channel:\n          type: string\n          description: Channel name\n          enum:\n            - market_trades\n        client_id:\n          type: string\n          description: Client connection identifier\n        timestamp:\n          type: string\n          format: date-time\n          description: Event timestamp\n        sequence_num:\n          type: integer\n          description: Sequence number\n        events:\n          type: array\n          description: Trade events\n          items:\n            type: object\n            properties:\n              type:\n                type: string\n            \
  \    description: Event type\n              trades:\n                type: array\n                items:\n                  type: object\n                  properties:\n                    trade_id:\n                      type: string\n                      description: Trade identifier\n                    product_id:\n                      type: string\n                      description: Product identifier\n                    price:\n                      type: string\n                      description: Trade price\n                    size:\n                      type: string\n                      description: Trade size\n                    side:\n                      type: string\n                      description: Taker side\n                      enum:\n                        - BUY\n                        - SELL\n                    time:\n                      type: string\n                      format: date-time\n                      description: Trade time\n    TickerPayload:\n\
  \      type: object\n      description: Ticker update payload\n      properties:\n        channel:\n          type: string\n          description: Channel name\n          enum:\n            - ticker\n            - ticker_batch\n        client_id:\n          type: string\n          description: Client connection identifier\n        timestamp:\n          type: string\n          format: date-time\n          description: Event timestamp\n        sequence_num:\n          type: integer\n          description: Sequence number\n        events:\n          type: array\n          description: Ticker events\n          items:\n            type: object\n            properties:\n              type:\n                type: string\n                description: Event type\n              tickers:\n                type: array\n                items:\n                  type: object\n                  properties:\n                    product_id:\n                      type: string\n                      description:\
  \ Product identifier\n                    price:\n                      type: string\n                      description: Current price\n                    volume_24_h:\n                      type: string\n                      description: 24-hour volume\n                    low_24_h:\n                      type: string\n                      description: 24-hour low\n                    high_24_h:\n                      type: string\n                      description: 24-hour high\n                    low_52_w:\n                      type: string\n                      description: 52-week low\n                    high_52_w:\n                      type: string\n                      description: 52-week high\n                    price_percent_chg_24_h:\n                      type: string\n                      description: 24-hour price change percentage\n                    best_bid:\n                      type: string\n                      description: Best bid price\n           \
  \         best_bid_quantity:\n                      type: string\n                      description: Best bid quantity\n                    best_ask:\n                      type: string\n                      description: Best ask price\n                    best_ask_quantity:\n                      type: string\n                      description: Best ask quantity\n    Level2SnapshotPayload:\n      type: object\n      description: Level 2 order book snapshot\n      properties:\n        channel:\n          type: string\n          description: Channel name\n          enum:\n            - l2_data\n        client_id:\n          type: string\n          description: Client connection identifier\n        timestamp:\n          type: string\n          format: date-time\n          description: Snapshot timestamp\n        sequence_num:\n          type: integer\n          description: Sequence number\n        events:\n          type: array\n          description: Snapshot events\n          items:\n\
  \            type: object\n            properties:\n              type:\n                type: string\n                description: Event type\n                enum:\n                  - snapshot\n              product_id:\n                type: string\n                description: Product identifier\n              updates:\n                type: array\n                items:\n                  type: object\n                  properties:\n                    side:\n                      type: string\n                      description: Order side\n                      enum:\n                        - bid\n                        - offer\n                    price_level:\n                      type: string\n                      description: Price level\n                    new_quantity:\n                      type: string\n                      description: Quantity at this level\n    Level2UpdatePayload:\n      type: object\n      description: Level 2 incremental order book update\n \
  \     properties:\n        channel:\n          type: string\n          description: Channel name\n          enum:\n            - l2_data\n        client_id:\n          type: string\n          description: Client connection identifier\n        timestamp:\n          type: string\n          format: date-time\n          description: Update timestamp\n        sequence_num:\n          type: integer\n          description: Sequence number\n        events:\n          type: array\n          description: Update events\n          items:\n            type: object\n            properties:\n              type:\n                type: string\n                description: Event type\n                enum:\n                  - update\n              product_id:\n                type: string\n                description: Product identifier\n              updates:\n                type: array\n                items:\n                  type: object\n                  properties:\n                    side:\n\
  \                      type: string\n                      description: Order side\n                      enum:\n                        - bid\n                        - offer\n                    price_level:\n                      type: string\n                      description: Price level\n                    new_quantity:\n                      type: string\n                      description: New quantity at this level\n    UserPayload:\n      type: object\n      description: User order update payload\n      properties:\n        channel:\n          type: string\n          description: Channel name\n          enum:\n            - user\n        client_id:\n          type: string\n          description: Client connection identifier\n        timestamp:\n          type: string\n          format: date-time\n          description: Event timestamp\n        sequence_num:\n          type: integer\n          description: Sequence number\n        events:\n          type: array\n          description:\
  \ User events\n          items:\n            type: object\n            properties:\n              type:\n                type: string\n                description: Event type\n              orders:\n                type: array\n                items:\n                  type: object\n                  properties:\n                    order_id:\n                      type: string\n                      description: Order identifier\n                    client_order_id:\n                      type: string\n                      description: Client-specified order ID\n                    product_id:\n                      type: string\n                      description: Product identifier\n                    side:\n                      type: string\n                      description: Order side\n                    status:\n                      type: string\n                      description: Order status\n                    order_type:\n                      type: string\n           \
  \           description: Order type\n                    cumulative_quantity:\n                      type: string\n                      description: Cumulative filled quantity\n                    avg_price:\n                      type: string\n                      description: Average fill price\n                    total_fees:\n                      type: string\n                      description: Total fees\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/asyncapi/coinbase-advanced-trade-asyncapi.yml
spec_file: asyncapi/coinbase-advanced-trade-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/asyncapi/coinbase-advanced-trade-asyncapi.yml
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
