---
channels:
- description: Single WebSocket connection for sending trading requests and receiving responses. All requests and responses are JSON-formatted messages on this channel. Requests include a method name and parameters; responses include a matching id field.
  name: /
  operation: publish
  operation_id: receiveResponse
  summary: Receive API responses
description: The Binance Spot WebSocket API provides an alternative way to access spot trading functionality through persistent WebSocket connections. It is functionally equivalent to the REST API, accepting the same parameters and returning the same status and error codes, but offers lower latency for time-sensitive trading operations. Developers can place orders, cancel orders, and query account information over a single WebSocket connection.
layout: asyncapi
messages:
- description: ''
  name: OrderRequest
  summary: Request to place a new order via WebSocket.
  title: Order Request
- description: ''
  name: CancelOrderRequest
  summary: Request to cancel an order via WebSocket.
  title: Cancel Order Request
- description: ''
  name: AccountRequest
  summary: Request for account information via WebSocket.
  title: Account Request
- description: ''
  name: MarketDataRequest
  summary: Request for market data via WebSocket.
  title: Market Data Request
- description: ''
  name: OrderResponse
  summary: Response to an order request.
  title: Order Response
- description: ''
  name: AccountResponse
  summary: Response to an account query.
  title: Account Response
- description: ''
  name: MarketDataResponse
  summary: Response to a market data query.
  title: Market Data Response
- description: ''
  name: ErrorResponse
  summary: Error response for failed requests.
  title: Error Response
name: Binance Spot WebSocket API
provider_name: Binance
provider_slug: binance
servers:
- description: Production WebSocket API server for spot trading operations.
  name: production
  protocol: wss
  url: wss://ws-api.binance.com:443/ws-api/v3
- description: Testnet WebSocket API server.
  name: testnet
  protocol: wss
  url: wss://testnet.binance.vision/ws-api/v3
slug: binance-spot-websocket-api-asyncapi
spec_file: asyncapi/binance-spot-websocket-api-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/binance/refs/heads/main/asyncapi/binance-spot-websocket-api-asyncapi.yml
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
