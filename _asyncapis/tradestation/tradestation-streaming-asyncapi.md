---
api_specs:
- filename: tradestation-api-openapi.yml
  format: yaml
  label: TradeStation API
  slug: tradestation-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tradestation/refs/heads/main/openapi/tradestation-api-openapi.yml
- filename: tradestation-streaming-asyncapi.yml
  format: yaml
  label: TradeStation Streaming API
  slug: tradestation-streaming
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/tradestation/refs/heads/main/asyncapi/tradestation-streaming-asyncapi.yml
channels:
- description: Streams real-time quote changes for one or more symbols. Delivers updated bid, ask, last price, volume, and other quote fields as they change. Only changed fields are sent in subsequent updates after the initial snapshot.
  name: /v3/marketdata/stream/quotes/{symbols}
  operation: publish
  operation_id: streamQuotes
  summary: Stream quote changes
- description: Streams real-time bar chart data (OHLC) for a given symbol. Delivers bar updates as they form including open, high, low, close, volume, and tick count information. Supports minute, daily, weekly, and monthly intervals.
  name: /v3/marketdata/stream/barcharts/{symbol}
  operation: publish
  operation_id: streamBars
  summary: Stream bar chart data
- description: Streams real-time option chain data for a given underlying symbol. Delivers updates to option quotes across multiple expirations and strikes as they change.
  name: /v3/marketdata/stream/options/chains/{underlying}
  operation: publish
  operation_id: streamOptionChain
  summary: Stream option chain
- description: Streams real-time quote data for specific option contracts. Delivers bid, ask, last price, greeks, and other option-specific data as it changes.
  name: /v3/marketdata/stream/options/quotes
  operation: publish
  operation_id: streamOptionQuotes
  summary: Stream option quotes
- description: Streams real-time aggregated market depth data for a symbol. Delivers updates to the order book showing aggregated bid and ask quantities at each price level.
  name: /v3/marketdata/stream/marketdepth/aggregates/{symbol}
  operation: publish
  operation_id: streamMarketDepthAggregates
  summary: Stream market depth aggregates
- description: Streams real-time order status updates for one or more brokerage accounts. Delivers order state changes including fills, partial fills, cancellations, and rejections as they occur.
  name: /v3/brokerage/stream/accounts/{accountIds}/orders
  operation: publish
  operation_id: streamOrders
  summary: Stream order updates
- description: Streams real-time status updates for specific orders by order identifier. Delivers state changes for the specified orders only.
  name: /v3/brokerage/stream/accounts/{accountIds}/orders/{orderIds}
  operation: publish
  operation_id: streamOrdersByIds
  summary: Stream specific order updates
- description: Streams real-time position updates for one or more brokerage accounts. Delivers changes to position quantities, market values, and profit/loss as they occur throughout the trading session.
  name: /v3/brokerage/stream/accounts/{accountIds}/positions
  operation: publish
  operation_id: streamPositions
  summary: Stream position updates
- description: Streams real-time cryptocurrency wallet updates for a specific brokerage account. Delivers changes to wallet balances and available amounts.
  name: /v3/brokerage/stream/accounts/{accountId}/wallets
  operation: publish
  operation_id: streamWallets
  summary: Stream wallet updates
description: The TradeStation Streaming API provides real-time HTTP streaming endpoints for market data and brokerage events. Streams use HTTP chunked transfer encoding with newline-delimited JSON objects. Each stream maintains a persistent HTTP connection that delivers updates as they occur, significantly reducing network latency compared to polling. Streams consist of a series of chunks containing individual JSON objects parsed separately using the newline character delimiter. TradeStation streams can terminate under certain conditions, unlike canonical HTTP/1.1 streams. The streaming content type is application/vnd.tradestation.streams.v3+json.
layout: asyncapi
messages:
- description: ''
  name: QuoteUpdate
  summary: A real-time quote update for a symbol with changed fields.
  title: Quote Update
- description: ''
  name: BarUpdate
  summary: A real-time bar chart update with OHLC data.
  title: Bar Chart Update
- description: ''
  name: OptionChainUpdate
  summary: A real-time option chain update for an underlying symbol.
  title: Option Chain Update
- description: ''
  name: OptionQuoteUpdate
  summary: A real-time quote update for specific option contracts.
  title: Option Quote Update
- description: ''
  name: MarketDepthUpdate
  summary: A real-time aggregated market depth update showing order book bid and ask levels.
  title: Market Depth Update
- description: ''
  name: OrderUpdate
  summary: A real-time order status update for a brokerage account.
  title: Order Update
- description: ''
  name: PositionUpdate
  summary: A real-time position update for a brokerage account.
  title: Position Update
- description: ''
  name: WalletUpdate
  summary: A real-time cryptocurrency wallet update.
  title: Wallet Update
name: TradeStation Streaming API
provider_name: TradeStation
provider_slug: tradestation
servers:
- description: TradeStation production streaming server. Uses HTTP chunked transfer encoding for real-time data delivery.
  name: production
  protocol: https
  url: https://api.tradestation.com
- description: TradeStation simulator streaming server for paper trading and development testing.
  name: simulator
  protocol: https
  url: https://sim-api.tradestation.com
slug: tradestation-streaming-asyncapi
source_filename: tradestation-streaming-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: TradeStation Streaming API\n  description: >-\n    The TradeStation Streaming API provides real-time HTTP streaming\n    endpoints for market data and brokerage events. Streams use HTTP\n    chunked transfer encoding with newline-delimited JSON objects.\n    Each stream maintains a persistent HTTP connection that delivers\n    updates as they occur, significantly reducing network latency\n    compared to polling. Streams consist of a series of chunks\n    containing individual JSON objects parsed separately using the\n    newline character delimiter. TradeStation streams can terminate\n    under certain conditions, unlike canonical HTTP/1.1 streams.\n    The streaming content type is application/vnd.tradestation.streams.v3+json.\n  version: '3.0'\n  contact:\n    name: TradeStation API Support\n    url: https://api.tradestation.com/docs/\n  license:\n    name: Proprietary\n    url: https://www.tradestation.com/important-information/\nservers:\n\
  \  production:\n    url: https://api.tradestation.com\n    protocol: https\n    description: >-\n      TradeStation production streaming server. Uses HTTP chunked\n      transfer encoding for real-time data delivery.\n    security:\n      - oauth2AuthCode: []\n  simulator:\n    url: https://sim-api.tradestation.com\n    protocol: https\n    description: >-\n      TradeStation simulator streaming server for paper trading\n      and development testing.\n    security:\n      - oauth2AuthCode: []\nchannels:\n  /v3/marketdata/stream/quotes/{symbols}:\n    description: >-\n      Streams real-time quote changes for one or more symbols. Delivers\n      updated bid, ask, last price, volume, and other quote fields as\n      they change. Only changed fields are sent in subsequent updates\n      after the initial snapshot.\n    parameters:\n      symbols:\n        description: >-\n          One or more symbol identifiers, comma-separated.\n        schema:\n          type: string\n    publish:\n \
  \     operationId: streamQuotes\n      summary: Stream quote changes\n      message:\n        $ref: '#/components/messages/QuoteUpdate'\n  /v3/marketdata/stream/barcharts/{symbol}:\n    description: >-\n      Streams real-time bar chart data (OHLC) for a given symbol.\n      Delivers bar updates as they form including open, high, low,\n      close, volume, and tick count information. Supports minute,\n      daily, weekly, and monthly intervals.\n    parameters:\n      symbol:\n        description: >-\n          The symbol to stream bar chart data for.\n        schema:\n          type: string\n    publish:\n      operationId: streamBars\n      summary: Stream bar chart data\n      message:\n        $ref: '#/components/messages/BarUpdate'\n  /v3/marketdata/stream/options/chains/{underlying}:\n    description: >-\n      Streams real-time option chain data for a given underlying symbol.\n      Delivers updates to option quotes across multiple expirations and\n      strikes as they change.\n\
  \    parameters:\n      underlying:\n        description: >-\n          The underlying symbol for the option chain.\n        schema:\n          type: string\n    publish:\n      operationId: streamOptionChain\n      summary: Stream option chain\n      message:\n        $ref: '#/components/messages/OptionChainUpdate'\n  /v3/marketdata/stream/options/quotes:\n    description: >-\n      Streams real-time quote data for specific option contracts.\n      Delivers bid, ask, last price, greeks, and other option-specific\n      data as it changes.\n    publish:\n      operationId: streamOptionQuotes\n      summary: Stream option quotes\n      message:\n        $ref: '#/components/messages/OptionQuoteUpdate'\n  /v3/marketdata/stream/marketdepth/aggregates/{symbol}:\n    description: >-\n      Streams real-time aggregated market depth data for a symbol.\n      Delivers updates to the order book showing aggregated bid and\n      ask quantities at each price level.\n    parameters:\n      symbol:\n\
  \        description: >-\n          The symbol to stream market depth data for.\n        schema:\n          type: string\n    publish:\n      operationId: streamMarketDepthAggregates\n      summary: Stream market depth aggregates\n      message:\n        $ref: '#/components/messages/MarketDepthUpdate'\n  /v3/brokerage/stream/accounts/{accountIds}/orders:\n    description: >-\n      Streams real-time order status updates for one or more brokerage\n      accounts. Delivers order state changes including fills, partial\n      fills, cancellations, and rejections as they occur.\n    parameters:\n      accountIds:\n        description: >-\n          One or more account identifiers, comma-separated.\n        schema:\n          type: string\n    publish:\n      operationId: streamOrders\n      summary: Stream order updates\n      message:\n        $ref: '#/components/messages/OrderUpdate'\n  /v3/brokerage/stream/accounts/{accountIds}/orders/{orderIds}:\n    description: >-\n      Streams real-time\
  \ status updates for specific orders by order\n      identifier. Delivers state changes for the specified orders only.\n    parameters:\n      accountIds:\n        description: >-\n          One or more account identifiers, comma-separated.\n        schema:\n          type: string\n      orderIds:\n        description: >-\n          One or more order identifiers, comma-separated.\n        schema:\n          type: string\n    publish:\n      operationId: streamOrdersByIds\n      summary: Stream specific order updates\n      message:\n        $ref: '#/components/messages/OrderUpdate'\n  /v3/brokerage/stream/accounts/{accountIds}/positions:\n    description: >-\n      Streams real-time position updates for one or more brokerage\n      accounts. Delivers changes to position quantities, market values,\n      and profit/loss as they occur throughout the trading session.\n    parameters:\n      accountIds:\n        description: >-\n          One or more account identifiers, comma-separated.\n\
  \        schema:\n          type: string\n    publish:\n      operationId: streamPositions\n      summary: Stream position updates\n      message:\n        $ref: '#/components/messages/PositionUpdate'\n  /v3/brokerage/stream/accounts/{accountId}/wallets:\n    description: >-\n      Streams real-time cryptocurrency wallet updates for a specific\n      brokerage account. Delivers changes to wallet balances and\n      available amounts.\n    parameters:\n      accountId:\n        description: >-\n          The account identifier for wallet streaming.\n        schema:\n          type: string\n    publish:\n      operationId: streamWallets\n      summary: Stream wallet updates\n      message:\n        $ref: '#/components/messages/WalletUpdate'\ncomponents:\n  securitySchemes:\n    oauth2AuthCode:\n      type: oauth2\n      description: >-\n        OAuth 2.0 authorization code flow for accessing TradeStation\n        streaming resources.\n      flows:\n        authorizationCode:\n          authorizationUrl:\
  \ https://signin.tradestation.com/authorize\n          tokenUrl: https://signin.tradestation.com/oauth/token\n          scopes:\n            marketdata: Access to market data streams\n            readaccount: Read access to account streams\n            trade: Access to order and position streams\n  messages:\n    QuoteUpdate:\n      name: QuoteUpdate\n      title: Quote Update\n      summary: >-\n        A real-time quote update for a symbol with changed fields.\n      contentType: application/vnd.tradestation.streams.v3+json\n      payload:\n        $ref: '#/components/schemas/QuoteStreamData'\n    BarUpdate:\n      name: BarUpdate\n      title: Bar Chart Update\n      summary: >-\n        A real-time bar chart update with OHLC data.\n      contentType: application/vnd.tradestation.streams.v3+json\n      payload:\n        $ref: '#/components/schemas/BarStreamData'\n    OptionChainUpdate:\n      name: OptionChainUpdate\n      title: Option Chain Update\n      summary: >-\n        A real-time\
  \ option chain update for an underlying symbol.\n      contentType: application/vnd.tradestation.streams.v3+json\n      payload:\n        $ref: '#/components/schemas/OptionChainStreamData'\n    OptionQuoteUpdate:\n      name: OptionQuoteUpdate\n      title: Option Quote Update\n      summary: >-\n        A real-time quote update for specific option contracts.\n      contentType: application/vnd.tradestation.streams.v3+json\n      payload:\n        $ref: '#/components/schemas/OptionQuoteStreamData'\n    MarketDepthUpdate:\n      name: MarketDepthUpdate\n      title: Market Depth Update\n      summary: >-\n        A real-time aggregated market depth update showing order\n        book bid and ask levels.\n      contentType: application/vnd.tradestation.streams.v3+json\n      payload:\n        $ref: '#/components/schemas/MarketDepthStreamData'\n    OrderUpdate:\n      name: OrderUpdate\n      title: Order Update\n      summary: >-\n        A real-time order status update for a brokerage account.\n\
  \      contentType: application/vnd.tradestation.streams.v3+json\n      payload:\n        $ref: '#/components/schemas/OrderStreamData'\n    PositionUpdate:\n      name: PositionUpdate\n      title: Position Update\n      summary: >-\n        A real-time position update for a brokerage account.\n      contentType: application/vnd.tradestation.streams.v3+json\n      payload:\n        $ref: '#/components/schemas/PositionStreamData'\n    WalletUpdate:\n      name: WalletUpdate\n      title: Wallet Update\n      summary: >-\n        A real-time cryptocurrency wallet update.\n      contentType: application/vnd.tradestation.streams.v3+json\n      payload:\n        $ref: '#/components/schemas/WalletStreamData'\n  schemas:\n    QuoteStreamData:\n      type: object\n      description: >-\n        Streaming quote data with fields that have changed since the\n        last update.\n      properties:\n        Symbol:\n          type: string\n          description: >-\n            The symbol identifier.\n\
  \        Last:\n          type: number\n          format: double\n          description: >-\n            The last traded price.\n        Bid:\n          type: number\n          format: double\n          description: >-\n            The current bid price.\n        Ask:\n          type: number\n          format: double\n          description: >-\n            The current ask price.\n        BidSize:\n          type: integer\n          description: >-\n            The size of the bid.\n        AskSize:\n          type: integer\n          description: >-\n            The size of the ask.\n        Volume:\n          type: integer\n          description: >-\n            The total volume traded today.\n        Open:\n          type: number\n          format: double\n          description: >-\n            The opening price.\n        High:\n          type: number\n          format: double\n          description: >-\n            The session high price.\n        Low:\n          type: number\n    \
  \      format: double\n          description: >-\n            The session low price.\n        Close:\n          type: number\n          format: double\n          description: >-\n            The previous close price.\n        NetChange:\n          type: number\n          format: double\n          description: >-\n            Net change from previous close.\n        NetChangePct:\n          type: number\n          format: double\n          description: >-\n            Net change as a percentage.\n        TradeTime:\n          type: string\n          format: date-time\n          description: >-\n            The timestamp of the last trade.\n        Heartbeat:\n          type: integer\n          description: >-\n            Heartbeat counter sent periodically to keep the stream alive.\n    BarStreamData:\n      type: object\n      description: >-\n        Streaming bar chart data with OHLC values.\n      properties:\n        High:\n          type: number\n          format: double\n      \
  \    description: >-\n            The highest price during the bar interval.\n        Low:\n          type: number\n          format: double\n          description: >-\n            The lowest price during the bar interval.\n        Open:\n          type: number\n          format: double\n          description: >-\n            The opening price of the bar interval.\n        Close:\n          type: number\n          format: double\n          description: >-\n            The closing price of the bar interval.\n        Volume:\n          type: integer\n          description: >-\n            The total volume during the bar interval.\n        TimeStamp:\n          type: string\n          format: date-time\n          description: >-\n            The timestamp for the bar interval.\n        TotalTicks:\n          type: integer\n          description: >-\n            The total number of ticks during the bar interval.\n        UpTicks:\n          type: integer\n          description: >-\n      \
  \      The number of up ticks.\n        DownTicks:\n          type: integer\n          description: >-\n            The number of down ticks.\n        Status:\n          type: string\n          description: >-\n            The status of the bar such as Open, Closed, or New.\n        Heartbeat:\n          type: integer\n          description: >-\n            Heartbeat counter for keeping the stream alive.\n    OptionChainStreamData:\n      type: object\n      description: >-\n        Streaming option chain data for an underlying symbol.\n      properties:\n        Symbol:\n          type: string\n          description: >-\n            The option symbol.\n        Underlying:\n          type: string\n          description: >-\n            The underlying symbol.\n        StrikePrice:\n          type: number\n          format: double\n          description: >-\n            The strike price.\n        ExpirationDate:\n          type: string\n          format: date\n          description: >-\n\
  \            The expiration date.\n        OptionType:\n          type: string\n          description: >-\n            The option type.\n          enum:\n            - Call\n            - Put\n        Bid:\n          type: number\n          format: double\n          description: >-\n            The current bid price.\n        Ask:\n          type: number\n          format: double\n          description: >-\n            The current ask price.\n        Last:\n          type: number\n          format: double\n          description: >-\n            The last traded price.\n        Volume:\n          type: integer\n          description: >-\n            The volume traded today.\n        OpenInterest:\n          type: integer\n          description: >-\n            The current open interest.\n        Delta:\n          type: number\n          format: double\n          description: >-\n            The option delta greek.\n        Gamma:\n          type: number\n          format: double\n      \
  \    description: >-\n            The option gamma greek.\n        Theta:\n          type: number\n          format: double\n          description: >-\n            The option theta greek.\n        Vega:\n          type: number\n          format: double\n          description: >-\n            The option vega greek.\n        ImpliedVolatility:\n          type: number\n          format: double\n          description: >-\n            The implied volatility.\n        Heartbeat:\n          type: integer\n          description: >-\n            Heartbeat counter for keeping the stream alive.\n    OptionQuoteStreamData:\n      type: object\n      description: >-\n        Streaming quote data for a specific option contract.\n      properties:\n        Symbol:\n          type: string\n          description: >-\n            The option symbol.\n        Bid:\n          type: number\n          format: double\n          description: >-\n            The current bid price.\n        Ask:\n          type:\
  \ number\n          format: double\n          description: >-\n            The current ask price.\n        Last:\n          type: number\n          format: double\n          description: >-\n            The last traded price.\n        Volume:\n          type: integer\n          description: >-\n            The volume traded today.\n        Delta:\n          type: number\n          format: double\n          description: >-\n            The option delta.\n        Gamma:\n          type: number\n          format: double\n          description: >-\n            The option gamma.\n        Theta:\n          type: number\n          format: double\n          description: >-\n            The option theta.\n        Vega:\n          type: number\n          format: double\n          description: >-\n            The option vega.\n        ImpliedVolatility:\n          type: number\n          format: double\n          description: >-\n            The implied volatility.\n        Heartbeat:\n         \
  \ type: integer\n          description: >-\n            Heartbeat counter for keeping the stream alive.\n    MarketDepthStreamData:\n      type: object\n      description: >-\n        Streaming aggregated market depth data showing bid and ask\n        levels in the order book.\n      properties:\n        Symbol:\n          type: string\n          description: >-\n            The symbol identifier.\n        Bids:\n          type: array\n          description: >-\n            Aggregated bid levels.\n          items:\n            $ref: '#/components/schemas/DepthLevel'\n        Asks:\n          type: array\n          description: >-\n            Aggregated ask levels.\n          items:\n            $ref: '#/components/schemas/DepthLevel'\n        Heartbeat:\n          type: integer\n          description: >-\n            Heartbeat counter for keeping the stream alive.\n    DepthLevel:\n      type: object\n      description: >-\n        A single price level in the market depth order book.\n\
  \      properties:\n        Price:\n          type: number\n          format: double\n          description: >-\n            The price level.\n        Size:\n          type: integer\n          description: >-\n            The aggregate size at this price level.\n        OrderCount:\n          type: integer\n          description: >-\n            The number of orders at this price level.\n    OrderStreamData:\n      type: object\n      description: >-\n        Streaming order status update data.\n      properties:\n        OrderID:\n          type: string\n          description: >-\n            The unique order identifier.\n        AccountID:\n          type: string\n          description: >-\n            The account identifier.\n        Symbol:\n          type: string\n          description: >-\n            The symbol being traded.\n        Quantity:\n          type: number\n          format: double\n          description: >-\n            The order quantity.\n        FilledQuantity:\n\
  \          type: number\n          format: double\n          description: >-\n            The quantity filled so far.\n        OrderType:\n          type: string\n          description: >-\n            The order type.\n          enum:\n            - Market\n            - Limit\n            - StopMarket\n            - StopLimit\n            - TrailingStop\n            - TrailingStopLimit\n        Status:\n          type: string\n          description: >-\n            The current order status.\n          enum:\n            - Open\n            - Filled\n            - PartiallyFilled\n            - Cancelled\n            - Rejected\n            - Expired\n            - Queued\n            - Received\n        Side:\n          type: string\n          description: >-\n            The order side.\n          enum:\n            - Buy\n            - Sell\n            - BuyToOpen\n            - BuyToClose\n            - SellToOpen\n            - SellToClose\n            - SellShort\n            -\
  \ BuyToCover\n        LimitPrice:\n          type: number\n          format: double\n          description: >-\n            The limit price.\n        StopPrice:\n          type: number\n          format: double\n          description: >-\n            The stop price.\n        FilledPrice:\n          type: number\n          format: double\n          description: >-\n            The average fill price.\n        TimeInForce:\n          type: string\n          description: >-\n            Time-in-force setting.\n        Heartbeat:\n          type: integer\n          description: >-\n            Heartbeat counter for keeping the stream alive.\n    PositionStreamData:\n      type: object\n      description: >-\n        Streaming position update data.\n      properties:\n        AccountID:\n          type: string\n          description: >-\n            The account identifier.\n        Symbol:\n          type: string\n          description: >-\n            The position symbol.\n        Quantity:\n\
  \          type: number\n          format: double\n          description: >-\n            The current position quantity.\n        AveragePrice:\n          type: number\n          format: double\n          description: >-\n            The average entry price.\n        Last:\n          type: number\n          format: double\n          description: >-\n            The last traded price.\n        MarketValue:\n          type: number\n          format: double\n          description: >-\n            The current market value.\n        UnrealizedProfitLoss:\n          type: number\n          format: double\n          description: >-\n            The unrealized profit or loss.\n        AssetType:\n          type: string\n          description: >-\n            The asset type.\n          enum:\n            - Stock\n            - Option\n            - Future\n            - Crypto\n        LongShort:\n          type: string\n          description: >-\n            Whether the position is long or short.\n\
  \          enum:\n            - Long\n            - Short\n        Heartbeat:\n          type: integer\n          description: >-\n            Heartbeat counter for keeping the stream alive.\n    WalletStreamData:\n      type: object\n      description: >-\n        Streaming cryptocurrency wallet update data.\n      properties:\n        Currency:\n          type: string\n          description: >-\n            The cryptocurrency currency code.\n        Balance:\n          type: number\n          format: double\n          description: >-\n            The wallet balance.\n        Available:\n          type: number\n          format: double\n          description: >-\n            The available balance for trading.\n        Heartbeat:\n          type: integer\n          description: >-\n            Heartbeat counter for keeping the stream alive.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tradestation/refs/heads/main/asyncapi/tradestation-streaming-asyncapi.yml
spec_file: asyncapi/tradestation-streaming-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/tradestation/refs/heads/main/asyncapi/tradestation-streaming-asyncapi.yml
tags:
- Brokerage
- Cryptocurrency
- Finance
- Futures
- Market Data
- Options
- Stocks
- Trading
- AsyncAPI
- Webhooks
- Events
version: '3.0'
---
