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
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Binance Spot WebSocket Streams\n  description: >-\n    Binance Spot WebSocket Streams deliver real-time market data updates\n    via persistent WebSocket connections. Developers can subscribe to\n    individual symbol ticker streams, aggregate trade streams, kline and\n    candlestick data, depth-of-book updates, and mini-ticker streams.\n    A single connection is valid for 24 hours. The server sends a ping\n    frame every 20 minutes and will disconnect if no pong is received\n    within 60 seconds.\n  version: '1.0.0'\n  contact:\n    name: Binance Support\n    url: https://www.binance.com/en/support\n  externalDocs:\n    description: Binance WebSocket Streams Documentation\n    url: https://developers.binance.com/docs/binance-spot-api-docs/web-socket-streams\nservers:\n  production:\n    url: wss://stream.binance.com:9443\n    protocol: wss\n    description: >-\n      Production WebSocket stream server. Supports up to 1024 streams\n    \
  \  per connection and 300 connections per 5 minutes per IP.\n  productionAlt:\n    url: wss://stream.binance.com:443\n    protocol: wss\n    description: >-\n      Alternative production WebSocket stream server on port 443.\nchannels:\n  /ws/{symbol}@aggTrade:\n    description: >-\n      Aggregate trade stream. Pushes trade information that is aggregated\n      for a single taker order.\n    parameters:\n      symbol:\n        description: >-\n          Trading pair symbol in lowercase, e.g. btcusdt.\n        schema:\n          type: string\n    publish:\n      operationId: receiveAggTrade\n      summary: Receive aggregate trade events\n      message:\n        $ref: '#/components/messages/AggTrade'\n  /ws/{symbol}@trade:\n    description: >-\n      Raw trade stream. Pushes raw trade information; each trade has a\n      unique buyer and seller.\n    parameters:\n      symbol:\n        description: >-\n          Trading pair symbol in lowercase.\n        schema:\n          type: string\n\
  \    publish:\n      operationId: receiveTrade\n      summary: Receive individual trade events\n      message:\n        $ref: '#/components/messages/Trade'\n  /ws/{symbol}@kline_{interval}:\n    description: >-\n      Kline/candlestick stream. Pushes updates to the current kline\n      every two seconds.\n    parameters:\n      symbol:\n        description: >-\n          Trading pair symbol in lowercase.\n        schema:\n          type: string\n      interval:\n        description: >-\n          Kline interval (1m, 3m, 5m, 15m, 30m, 1h, 2h, 4h, 6h, 8h,\n          12h, 1d, 3d, 1w, 1M).\n        schema:\n          type: string\n    publish:\n      operationId: receiveKline\n      summary: Receive kline/candlestick events\n      message:\n        $ref: '#/components/messages/Kline'\n  /ws/{symbol}@miniTicker:\n    description: >-\n      Individual symbol mini ticker stream. Pushes 24hr rolling window\n      mini-ticker statistics every second.\n    parameters:\n      symbol:\n        description:\
  \ >-\n          Trading pair symbol in lowercase.\n        schema:\n          type: string\n    publish:\n      operationId: receiveMiniTicker\n      summary: Receive mini ticker events\n      message:\n        $ref: '#/components/messages/MiniTicker'\n  /ws/!miniTicker@arr:\n    description: >-\n      All market mini tickers stream. Pushes mini-ticker for all symbols\n      every second.\n    publish:\n      operationId: receiveAllMiniTickers\n      summary: Receive all market mini ticker events\n      message:\n        payload:\n          type: array\n          items:\n            $ref: '#/components/schemas/MiniTickerPayload'\n  /ws/{symbol}@ticker:\n    description: >-\n      Individual symbol ticker stream. Pushes 24hr rolling window ticker\n      statistics every second.\n    parameters:\n      symbol:\n        description: >-\n          Trading pair symbol in lowercase.\n        schema:\n          type: string\n    publish:\n      operationId: receiveTicker\n      summary: Receive\
  \ ticker events\n      message:\n        $ref: '#/components/messages/Ticker'\n  /ws/{symbol}@bookTicker:\n    description: >-\n      Individual symbol book ticker stream. Pushes the best bid or ask\n      in real-time.\n    parameters:\n      symbol:\n        description: >-\n          Trading pair symbol in lowercase.\n        schema:\n          type: string\n    publish:\n      operationId: receiveBookTicker\n      summary: Receive book ticker events\n      message:\n        $ref: '#/components/messages/BookTicker'\n  /ws/{symbol}@depth{levels}:\n    description: >-\n      Partial book depth stream. Pushes the top bids and asks at\n      specified depth levels (5, 10, or 20). Updated every second\n      or 100ms depending on the update speed parameter.\n    parameters:\n      symbol:\n        description: >-\n          Trading pair symbol in lowercase.\n        schema:\n          type: string\n      levels:\n        description: >-\n          Number of levels (5, 10, or 20).\n     \
  \   schema:\n          type: string\n          enum: ['5', '10', '20']\n    publish:\n      operationId: receivePartialDepth\n      summary: Receive partial order book depth events\n      message:\n        $ref: '#/components/messages/PartialDepth'\n  /ws/{symbol}@depth:\n    description: >-\n      Diff depth stream. Pushes order book price and quantity changes\n      in real-time.\n    parameters:\n      symbol:\n        description: >-\n          Trading pair symbol in lowercase.\n        schema:\n          type: string\n    publish:\n      operationId: receiveDiffDepth\n      summary: Receive order book diff depth events\n      message:\n        $ref: '#/components/messages/DiffDepth'\n  /ws/{symbol}@avgPrice:\n    description: >-\n      Average price stream. Pushes changes in the average price over\n      a fixed time window.\n    parameters:\n      symbol:\n        description: >-\n          Trading pair symbol in lowercase.\n        schema:\n          type: string\n    publish:\n\
  \      operationId: receiveAvgPrice\n      summary: Receive average price events\n      message:\n        $ref: '#/components/messages/AvgPrice'\ncomponents:\n  messages:\n    AggTrade:\n      name: aggTrade\n      title: Aggregate Trade\n      summary: >-\n        Aggregate trade event with price, quantity, and trade IDs.\n      payload:\n        type: object\n        properties:\n          e:\n            type: string\n            description: >-\n              Event type.\n          E:\n            type: integer\n            format: int64\n            description: >-\n              Event time.\n          s:\n            type: string\n            description: >-\n              Symbol.\n          a:\n            type: integer\n            format: int64\n            description: >-\n              Aggregate trade ID.\n          p:\n            type: string\n            description: >-\n              Price.\n          q:\n            type: string\n            description: >-\n          \
  \    Quantity.\n          f:\n            type: integer\n            format: int64\n            description: >-\n              First trade ID.\n          l:\n            type: integer\n            format: int64\n            description: >-\n              Last trade ID.\n          T:\n            type: integer\n            format: int64\n            description: >-\n              Trade time.\n          m:\n            type: boolean\n            description: >-\n              Is the buyer the market maker.\n          M:\n            type: boolean\n            description: >-\n              Ignore.\n    Trade:\n      name: trade\n      title: Trade\n      summary: >-\n        Individual trade event.\n      payload:\n        type: object\n        properties:\n          e:\n            type: string\n            description: >-\n              Event type.\n          E:\n            type: integer\n            format: int64\n            description: >-\n              Event time.\n          s:\n\
  \            type: string\n            description: >-\n              Symbol.\n          t:\n            type: integer\n            format: int64\n            description: >-\n              Trade ID.\n          p:\n            type: string\n            description: >-\n              Price.\n          q:\n            type: string\n            description: >-\n              Quantity.\n          T:\n            type: integer\n            format: int64\n            description: >-\n              Trade time.\n          m:\n            type: boolean\n            description: >-\n              Is the buyer the market maker.\n          M:\n            type: boolean\n            description: >-\n              Ignore.\n    Kline:\n      name: kline\n      title: Kline/Candlestick\n      summary: >-\n        Kline/candlestick update event.\n      payload:\n        type: object\n        properties:\n          e:\n            type: string\n            description: >-\n              Event type.\n  \
  \        E:\n            type: integer\n            format: int64\n            description: >-\n              Event time.\n          s:\n            type: string\n            description: >-\n              Symbol.\n          k:\n            type: object\n            description: >-\n              Kline data object.\n            properties:\n              t:\n                type: integer\n                format: int64\n                description: >-\n                  Kline start time.\n              T:\n                type: integer\n                format: int64\n                description: >-\n                  Kline close time.\n              s:\n                type: string\n                description: >-\n                  Symbol.\n              i:\n                type: string\n                description: >-\n                  Interval.\n              f:\n                type: integer\n                format: int64\n                description: >-\n                  First trade\
  \ ID.\n              L:\n                type: integer\n                format: int64\n                description: >-\n                  Last trade ID.\n              o:\n                type: string\n                description: >-\n                  Open price.\n              c:\n                type: string\n                description: >-\n                  Close price.\n              h:\n                type: string\n                description: >-\n                  High price.\n              l:\n                type: string\n                description: >-\n                  Low price.\n              v:\n                type: string\n                description: >-\n                  Base asset volume.\n              n:\n                type: integer\n                description: >-\n                  Number of trades.\n              x:\n                type: boolean\n                description: >-\n                  Is this kline closed.\n              q:\n                type:\
  \ string\n                description: >-\n                  Quote asset volume.\n              V:\n                type: string\n                description: >-\n                  Taker buy base asset volume.\n              Q:\n                type: string\n                description: >-\n                  Taker buy quote asset volume.\n    MiniTicker:\n      name: miniTicker\n      title: Mini Ticker\n      summary: >-\n        24hr mini ticker event with basic price statistics.\n      payload:\n        $ref: '#/components/schemas/MiniTickerPayload'\n    Ticker:\n      name: ticker\n      title: 24hr Ticker\n      summary: >-\n        24hr rolling window ticker statistics event.\n      payload:\n        type: object\n        properties:\n          e:\n            type: string\n            description: >-\n              Event type.\n          E:\n            type: integer\n            format: int64\n            description: >-\n              Event time.\n          s:\n            type:\
  \ string\n            description: >-\n              Symbol.\n          p:\n            type: string\n            description: >-\n              Price change.\n          P:\n            type: string\n            description: >-\n              Price change percent.\n          w:\n            type: string\n            description: >-\n              Weighted average price.\n          x:\n            type: string\n            description: >-\n              Previous close price.\n          c:\n            type: string\n            description: >-\n              Last price.\n          Q:\n            type: string\n            description: >-\n              Last quantity.\n          b:\n            type: string\n            description: >-\n              Best bid price.\n          B:\n            type: string\n            description: >-\n              Best bid quantity.\n          a:\n            type: string\n            description: >-\n              Best ask price.\n          A:\n       \
  \     type: string\n            description: >-\n              Best ask quantity.\n          o:\n            type: string\n            description: >-\n              Open price.\n          h:\n            type: string\n            description: >-\n              High price.\n          l:\n            type: string\n            description: >-\n              Low price.\n          v:\n            type: string\n            description: >-\n              Total traded base asset volume.\n          q:\n            type: string\n            description: >-\n              Total traded quote asset volume.\n          O:\n            type: integer\n            format: int64\n            description: >-\n              Statistics open time.\n          C:\n            type: integer\n            format: int64\n            description: >-\n              Statistics close time.\n          F:\n            type: integer\n            format: int64\n            description: >-\n              First trade ID.\n\
  \          L:\n            type: integer\n            format: int64\n            description: >-\n              Last trade ID.\n          n:\n            type: integer\n            description: >-\n              Total number of trades.\n    BookTicker:\n      name: bookTicker\n      title: Book Ticker\n      summary: >-\n        Best bid and ask update event.\n      payload:\n        type: object\n        properties:\n          u:\n            type: integer\n            format: int64\n            description: >-\n              Order book update ID.\n          s:\n            type: string\n            description: >-\n              Symbol.\n          b:\n            type: string\n            description: >-\n              Best bid price.\n          B:\n            type: string\n            description: >-\n              Best bid quantity.\n          a:\n            type: string\n            description: >-\n              Best ask price.\n          A:\n            type: string\n        \
  \    description: >-\n              Best ask quantity.\n    PartialDepth:\n      name: partialDepth\n      title: Partial Book Depth\n      summary: >-\n        Top bids and asks at specified levels.\n      payload:\n        type: object\n        properties:\n          lastUpdateId:\n            type: integer\n            format: int64\n            description: >-\n              Last update ID.\n          bids:\n            type: array\n            items:\n              type: array\n              items:\n                type: string\n            description: >-\n              Bid levels.\n          asks:\n            type: array\n            items:\n              type: array\n              items:\n                type: string\n            description: >-\n              Ask levels.\n    DiffDepth:\n      name: diffDepth\n      title: Diff Depth\n      summary: >-\n        Order book price and quantity changes.\n      payload:\n        type: object\n        properties:\n          e:\n  \
  \          type: string\n            description: >-\n              Event type.\n          E:\n            type: integer\n            format: int64\n            description: >-\n              Event time.\n          s:\n            type: string\n            description: >-\n              Symbol.\n          U:\n            type: integer\n            format: int64\n            description: >-\n              First update ID in event.\n          u:\n            type: integer\n            format: int64\n            description: >-\n              Final update ID in event.\n          b:\n            type: array\n            items:\n              type: array\n              items:\n                type: string\n            description: >-\n              Bids to be updated.\n          a:\n            type: array\n            items:\n              type: array\n              items:\n                type: string\n            description: >-\n              Asks to be updated.\n    AvgPrice:\n      name:\
  \ avgPrice\n      title: Average Price\n      summary: >-\n        Average price update event.\n      payload:\n        type: object\n        properties:\n          e:\n            type: string\n            description: >-\n              Event type.\n          E:\n            type: integer\n            format: int64\n            description: >-\n              Event time.\n          s:\n            type: string\n            description: >-\n              Symbol.\n          i:\n            type: string\n            description: >-\n              Average price interval.\n          w:\n            type: string\n            description: >-\n              Average price.\n          T:\n            type: integer\n            format: int64\n            description: >-\n              Last trade time.\n  schemas:\n    MiniTickerPayload:\n      type: object\n      properties:\n        e:\n          type: string\n          description: >-\n            Event type.\n        E:\n          type: integer\n\
  \          format: int64\n          description: >-\n            Event time.\n        s:\n          type: string\n          description: >-\n            Symbol.\n        c:\n          type: string\n          description: >-\n            Close price.\n        o:\n          type: string\n          description: >-\n            Open price.\n        h:\n          type: string\n          description: >-\n            High price.\n        l:\n          type: string\n          description: >-\n            Low price.\n        v:\n          type: string\n          description: >-\n            Total traded base asset volume.\n        q:\n          type: string\n          description: >-\n            Total traded quote asset volume.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/binance/refs/heads/main/asyncapi/binance-spot-websocket-streams-asyncapi.yml
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
