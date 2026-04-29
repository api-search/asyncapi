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
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Binance Spot WebSocket API\n  description: >-\n    The Binance Spot WebSocket API provides an alternative way to access\n    spot trading functionality through persistent WebSocket connections. It\n    is functionally equivalent to the REST API, accepting the same parameters\n    and returning the same status and error codes, but offers lower latency\n    for time-sensitive trading operations. Developers can place orders, cancel\n    orders, and query account information over a single WebSocket connection.\n  version: '1.0.0'\n  contact:\n    name: Binance Support\n    url: https://www.binance.com/en/support\n  externalDocs:\n    description: Binance Spot WebSocket API Documentation\n    url: https://developers.binance.com/docs/binance-spot-api-docs/web-socket-api\nservers:\n  production:\n    url: wss://ws-api.binance.com:443/ws-api/v3\n    protocol: wss\n    description: >-\n      Production WebSocket API server for spot trading operations.\n\
  \  testnet:\n    url: wss://testnet.binance.vision/ws-api/v3\n    protocol: wss\n    description: >-\n      Testnet WebSocket API server.\nchannels:\n  /:\n    description: >-\n      Single WebSocket connection for sending trading requests and\n      receiving responses. All requests and responses are JSON-formatted\n      messages on this channel. Requests include a method name and\n      parameters; responses include a matching id field.\n    publish:\n      operationId: receiveResponse\n      summary: Receive API responses\n      message:\n        oneOf:\n          - $ref: '#/components/messages/OrderResponse'\n          - $ref: '#/components/messages/AccountResponse'\n          - $ref: '#/components/messages/MarketDataResponse'\n          - $ref: '#/components/messages/ErrorResponse'\n    subscribe:\n      operationId: sendRequest\n      summary: Send API requests\n      message:\n        oneOf:\n          - $ref: '#/components/messages/OrderRequest'\n          - $ref: '#/components/messages/CancelOrderRequest'\n\
  \          - $ref: '#/components/messages/AccountRequest'\n          - $ref: '#/components/messages/MarketDataRequest'\ncomponents:\n  messages:\n    OrderRequest:\n      name: orderRequest\n      title: Order Request\n      summary: >-\n        Request to place a new order via WebSocket.\n      payload:\n        type: object\n        properties:\n          id:\n            type: string\n            description: >-\n              Arbitrary ID used to match responses.\n          method:\n            type: string\n            description: >-\n              Method name, e.g. order.place.\n            enum:\n              - order.place\n              - order.test\n          params:\n            type: object\n            description: >-\n              Order parameters matching REST API.\n            properties:\n              symbol:\n                type: string\n              side:\n                type: string\n                enum: [BUY, SELL]\n              type:\n                type:\
  \ string\n              timeInForce:\n                type: string\n              price:\n                type: string\n              quantity:\n                type: string\n              apiKey:\n                type: string\n              signature:\n                type: string\n              timestamp:\n                type: integer\n                format: int64\n    CancelOrderRequest:\n      name: cancelOrderRequest\n      title: Cancel Order Request\n      summary: >-\n        Request to cancel an order via WebSocket.\n      payload:\n        type: object\n        properties:\n          id:\n            type: string\n          method:\n            type: string\n            enum:\n              - order.cancel\n              - openOrders.cancelAll\n          params:\n            type: object\n            properties:\n              symbol:\n                type: string\n              orderId:\n                type: integer\n                format: int64\n              origClientOrderId:\n\
  \                type: string\n              apiKey:\n                type: string\n              signature:\n                type: string\n              timestamp:\n                type: integer\n                format: int64\n    AccountRequest:\n      name: accountRequest\n      title: Account Request\n      summary: >-\n        Request for account information via WebSocket.\n      payload:\n        type: object\n        properties:\n          id:\n            type: string\n          method:\n            type: string\n            enum:\n              - account.status\n              - order.status\n              - openOrders.status\n              - allOrders\n              - myTrades\n          params:\n            type: object\n            properties:\n              symbol:\n                type: string\n              apiKey:\n                type: string\n              signature:\n                type: string\n              timestamp:\n                type: integer\n              \
  \  format: int64\n    MarketDataRequest:\n      name: marketDataRequest\n      title: Market Data Request\n      summary: >-\n        Request for market data via WebSocket.\n      payload:\n        type: object\n        properties:\n          id:\n            type: string\n          method:\n            type: string\n            enum:\n              - ping\n              - time\n              - exchangeInfo\n              - depth\n              - trades.recent\n              - trades.historical\n              - trades.aggregate\n              - klines\n              - avgPrice\n              - ticker.24hr\n              - ticker.price\n              - ticker.book\n          params:\n            type: object\n            properties:\n              symbol:\n                type: string\n              symbols:\n                type: array\n                items:\n                  type: string\n              limit:\n                type: integer\n    OrderResponse:\n      name: orderResponse\n\
  \      title: Order Response\n      summary: >-\n        Response to an order request.\n      payload:\n        type: object\n        properties:\n          id:\n            type: string\n          status:\n            type: integer\n          result:\n            type: object\n            properties:\n              symbol:\n                type: string\n              orderId:\n                type: integer\n                format: int64\n              clientOrderId:\n                type: string\n              transactTime:\n                type: integer\n                format: int64\n              price:\n                type: string\n              origQty:\n                type: string\n              executedQty:\n                type: string\n              status:\n                type: string\n              timeInForce:\n                type: string\n              type:\n                type: string\n              side:\n                type: string\n          rateLimits:\n     \
  \       type: array\n            items:\n              type: object\n    AccountResponse:\n      name: accountResponse\n      title: Account Response\n      summary: >-\n        Response to an account query.\n      payload:\n        type: object\n        properties:\n          id:\n            type: string\n          status:\n            type: integer\n          result:\n            type: object\n    MarketDataResponse:\n      name: marketDataResponse\n      title: Market Data Response\n      summary: >-\n        Response to a market data query.\n      payload:\n        type: object\n        properties:\n          id:\n            type: string\n          status:\n            type: integer\n          result:\n            type: object\n    ErrorResponse:\n      name: errorResponse\n      title: Error Response\n      summary: >-\n        Error response for failed requests.\n      payload:\n        type: object\n        properties:\n          id:\n            type: string\n          status:\n\
  \            type: integer\n          error:\n            type: object\n            properties:\n              code:\n                type: integer\n              msg:\n                type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/binance/refs/heads/main/asyncapi/binance-spot-websocket-api-asyncapi.yml
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
