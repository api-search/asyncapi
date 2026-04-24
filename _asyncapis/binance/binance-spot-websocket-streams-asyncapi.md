---
channels:
- description: Aggregate trade stream. Pushes trade information that is aggregated for a single taker order.
  name: /ws/{symbol}@aggTrade
  operation: publish
  operation_id: receiveAggTrade
  summary: Receive aggregate trade events
- description: Raw trade stream. Pushes raw trade information; each trade has a unique buyer and seller.
  name: /ws/{symbol}@trade
  operation: publish
  operation_id: receiveTrade
  summary: Receive individual trade events
- description: Kline/candlestick stream. Pushes updates to the current kline every two seconds.
  name: /ws/{symbol}@kline_{interval}
  operation: publish
  operation_id: receiveKline
  summary: Receive kline/candlestick events
- description: Individual symbol mini ticker stream. Pushes 24hr rolling window mini-ticker statistics every second.
  name: /ws/{symbol}@miniTicker
  operation: publish
  operation_id: receiveMiniTicker
  summary: Receive mini ticker events
- description: All market mini tickers stream. Pushes mini-ticker for all symbols every second.
  name: /ws/!miniTicker@arr
  operation: publish
  operation_id: receiveAllMiniTickers
  summary: Receive all market mini ticker events
- description: Individual symbol ticker stream. Pushes 24hr rolling window ticker statistics every second.
  name: /ws/{symbol}@ticker
  operation: publish
  operation_id: receiveTicker
  summary: Receive ticker events
- description: Individual symbol book ticker stream. Pushes the best bid or ask in real-time.
  name: /ws/{symbol}@bookTicker
  operation: publish
  operation_id: receiveBookTicker
  summary: Receive book ticker events
- description: Partial book depth stream. Pushes the top bids and asks at specified depth levels (5, 10, or 20). Updated every second or 100ms depending on the update speed parameter.
  name: /ws/{symbol}@depth{levels}
  operation: publish
  operation_id: receivePartialDepth
  summary: Receive partial order book depth events
- description: Diff depth stream. Pushes order book price and quantity changes in real-time.
  name: /ws/{symbol}@depth
  operation: publish
  operation_id: receiveDiffDepth
  summary: Receive order book diff depth events
- description: Average price stream. Pushes changes in the average price over a fixed time window.
  name: /ws/{symbol}@avgPrice
  operation: publish
  operation_id: receiveAvgPrice
  summary: Receive average price events
description: Binance Spot WebSocket Streams deliver real-time market data updates via persistent WebSocket connections. Developers can subscribe to individual symbol ticker streams, aggregate trade streams, kline and candlestick data, depth-of-book updates, and mini-ticker streams. A single connection is valid for 24 hours. The server sends a ping frame every 20 minutes and will disconnect if no pong is received within 60 seconds.
layout: asyncapi
messages:
- description: ''
  name: AggTrade
  summary: Aggregate trade event with price, quantity, and trade IDs.
  title: Aggregate Trade
- description: ''
  name: Trade
  summary: Individual trade event.
  title: Trade
- description: ''
  name: Kline
  summary: Kline/candlestick update event.
  title: Kline/Candlestick
- description: ''
  name: MiniTicker
  summary: 24hr mini ticker event with basic price statistics.
  title: Mini Ticker
- description: ''
  name: Ticker
  summary: 24hr rolling window ticker statistics event.
  title: 24hr Ticker
- description: ''
  name: BookTicker
  summary: Best bid and ask update event.
  title: Book Ticker
- description: ''
  name: PartialDepth
  summary: Top bids and asks at specified levels.
  title: Partial Book Depth
- description: ''
  name: DiffDepth
  summary: Order book price and quantity changes.
  title: Diff Depth
- description: ''
  name: AvgPrice
  summary: Average price update event.
  title: Average Price
name: Binance Spot WebSocket Streams
provider_name: Binance
provider_slug: binance
servers:
- description: Production WebSocket stream server. Supports up to 1024 streams per connection and 300 connections per 5 minutes per IP.
  name: production
  protocol: wss
  url: wss://stream.binance.com:9443
- description: Alternative production WebSocket stream server on port 443.
  name: productionAlt
  protocol: wss
  url: wss://stream.binance.com:443
slug: binance-spot-websocket-streams-asyncapi
spec_file: asyncapi/binance-spot-websocket-streams-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/binance/refs/heads/main/asyncapi/binance-spot-websocket-streams-asyncapi.yml
tags:
- Cryptocurrency
- Exchange
- Trading
- Blockchain
- Finance
- DeFi
- Market Data
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
