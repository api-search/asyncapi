---
api_specs:
- filename: openapi.json
  format: json
  label: TIBCO Cloud Integration API
  slug: ''
  spec_type: OpenAPI
  url: https://integration.cloud.tibco.com/docs/api/openapi.json
- filename: io-docs
  format: yaml
  label: TIBCO Mashery API Management
  slug: ''
  spec_type: OpenAPI
  url: https://developer.mashery.com/io-docs
- filename: tibco-businessevents-openapi.yml
  format: yaml
  label: TIBCO BusinessEvents API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tibco/refs/heads/main/openapi/tibco-businessevents-openapi.yml
- filename: tibco-messaging-asyncapi.yml
  format: yaml
  label: TIBCO Messaging API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/tibco/refs/heads/main/asyncapi/tibco-messaging-asyncapi.yml
- filename: tibco-spotfire-openapi.yml
  format: yaml
  label: TIBCO Spotfire Analytics API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tibco/refs/heads/main/openapi/tibco-spotfire-openapi.yml
channels:
- description: Channel for newly created order events. Producers publish order creation notifications and consumers receive them for downstream processing such as fulfillment, inventory, and billing.
  name: orders/created
  operation: publish
  operation_id: publishOrderCreated
  summary: Publish order created event
- description: Channel for order status update events. Consumers receive notifications when order status changes (e.g., shipped, delivered).
  name: orders/updated
  operation: publish
  operation_id: publishOrderUpdated
  summary: Publish order update event
- description: Channel for inventory change events. Published when stock levels change due to orders, returns, or manual adjustments.
  name: inventory/changed
  operation: publish
  operation_id: publishInventoryChanged
  summary: Publish inventory change event
- description: Channel for system alert notifications. Used for broadcasting operational alerts, threshold violations, and system health events.
  name: notifications/alerts
  operation: publish
  operation_id: publishAlert
  summary: Publish system alert
- description: General-purpose integration event channel for inter-application messaging. Supports custom event types with flexible payloads.
  name: integration/events
  operation: publish
  operation_id: publishIntegrationEvent
  summary: Publish integration event
- description: High-throughput data streaming channel for real-time data distribution using TIBCO FTL transport layer.
  name: data/stream
  operation: publish
  operation_id: publishDataStream
  summary: Publish data stream message
description: Enterprise messaging API supporting TIBCO Enterprise Message Service (EMS) and FTL (TIBCO FTL) for reliable, high-performance messaging. Supports JMS-compatible publish-subscribe and point-to-point messaging patterns for real-time data distribution across enterprise applications.
layout: asyncapi
messages:
- description: ''
  name: OrderCreated
  summary: Notification that a new order has been created
  title: Order Created Event
- description: ''
  name: OrderUpdated
  summary: Notification that an order status has changed
  title: Order Updated Event
- description: ''
  name: InventoryChanged
  summary: Notification that inventory levels have changed
  title: Inventory Changed Event
- description: ''
  name: Alert
  summary: System alert notification for operational monitoring
  title: System Alert
- description: ''
  name: IntegrationEvent
  summary: General-purpose integration event for inter-application messaging
  title: Integration Event
- description: ''
  name: DataStreamMessage
  summary: High-throughput data stream message via FTL
  title: Data Stream Message
name: TIBCO Messaging API
provider_name: TIBCO
provider_slug: tibco
servers:
- description: TIBCO EMS Production Server (SSL)
  name: ems-production
  protocol: jms
  url: ssl://messaging.cloud.tibco.com:7243
- description: TIBCO EMS Development Server
  name: ems-development
  protocol: jms
  url: tcp://messaging.cloud.tibco.com:7222
- description: TIBCO FTL Realm Server
  name: ftl-production
  protocol: https
  url: https://messaging.cloud.tibco.com:8585
slug: tibco-messaging-asyncapi
source_filename: tibco-messaging-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: TIBCO Messaging API\n  version: '1.0'\n  description: >-\n    Enterprise messaging API supporting TIBCO Enterprise Message Service (EMS)\n    and FTL (TIBCO FTL) for reliable, high-performance messaging. Supports\n    JMS-compatible publish-subscribe and point-to-point messaging patterns\n    for real-time data distribution across enterprise applications.\n  contact:\n    name: TIBCO Support\n    url: https://support.tibco.com\n  license:\n    name: TIBCO License\n    url: https://www.tibco.com/legal/terms-of-use\n  termsOfService: https://www.tibco.com/legal/terms-of-use\nexternalDocs:\n  description: TIBCO Enterprise Message Service Documentation\n  url: https://docs.tibco.com/products/tibco-enterprise-message-service\nservers:\n  ems-production:\n    url: ssl://messaging.cloud.tibco.com:7243\n    protocol: jms\n    description: TIBCO EMS Production Server (SSL)\n    security:\n      - userPassword: []\n  ems-development:\n    url: tcp://messaging.cloud.tibco.com:7222\n\
  \    protocol: jms\n    description: TIBCO EMS Development Server\n    security:\n      - userPassword: []\n  ftl-production:\n    url: https://messaging.cloud.tibco.com:8585\n    protocol: https\n    description: TIBCO FTL Realm Server\n    security:\n      - bearerAuth: []\ndefaultContentType: application/json\nchannels:\n  orders/created:\n    description: >-\n      Channel for newly created order events. Producers publish order\n      creation notifications and consumers receive them for downstream\n      processing such as fulfillment, inventory, and billing.\n    subscribe:\n      operationId: receiveOrderCreated\n      summary: Receive order created events\n      description: >-\n        Subscribe to receive notifications when new orders are created.\n      message:\n        $ref: '#/components/messages/OrderCreated'\n      tags:\n        - name: orders\n    publish:\n      operationId: publishOrderCreated\n      summary: Publish order created event\n      description: >-\n    \
  \    Publish a notification that a new order has been created.\n      message:\n        $ref: '#/components/messages/OrderCreated'\n      tags:\n        - name: orders\n  orders/updated:\n    description: >-\n      Channel for order status update events. Consumers receive\n      notifications when order status changes (e.g., shipped, delivered).\n    subscribe:\n      operationId: receiveOrderUpdated\n      summary: Receive order update events\n      message:\n        $ref: '#/components/messages/OrderUpdated'\n      tags:\n        - name: orders\n    publish:\n      operationId: publishOrderUpdated\n      summary: Publish order update event\n      message:\n        $ref: '#/components/messages/OrderUpdated'\n      tags:\n        - name: orders\n  inventory/changed:\n    description: >-\n      Channel for inventory change events. Published when stock levels\n      change due to orders, returns, or manual adjustments.\n    subscribe:\n      operationId: receiveInventoryChanged\n      summary:\
  \ Receive inventory change events\n      message:\n        $ref: '#/components/messages/InventoryChanged'\n      tags:\n        - name: inventory\n    publish:\n      operationId: publishInventoryChanged\n      summary: Publish inventory change event\n      message:\n        $ref: '#/components/messages/InventoryChanged'\n      tags:\n        - name: inventory\n  notifications/alerts:\n    description: >-\n      Channel for system alert notifications. Used for broadcasting\n      operational alerts, threshold violations, and system health events.\n    subscribe:\n      operationId: receiveAlert\n      summary: Receive system alerts\n      message:\n        $ref: '#/components/messages/Alert'\n      tags:\n        - name: notifications\n    publish:\n      operationId: publishAlert\n      summary: Publish system alert\n      message:\n        $ref: '#/components/messages/Alert'\n      tags:\n        - name: notifications\n  integration/events:\n    description: >-\n      General-purpose\
  \ integration event channel for inter-application\n      messaging. Supports custom event types with flexible payloads.\n    subscribe:\n      operationId: receiveIntegrationEvent\n      summary: Receive integration events\n      message:\n        $ref: '#/components/messages/IntegrationEvent'\n      tags:\n        - name: integration\n    publish:\n      operationId: publishIntegrationEvent\n      summary: Publish integration event\n      message:\n        $ref: '#/components/messages/IntegrationEvent'\n      tags:\n        - name: integration\n  data/stream:\n    description: >-\n      High-throughput data streaming channel for real-time data\n      distribution using TIBCO FTL transport layer.\n    subscribe:\n      operationId: receiveDataStream\n      summary: Receive data stream messages\n      message:\n        $ref: '#/components/messages/DataStreamMessage'\n      tags:\n        - name: streaming\n    publish:\n      operationId: publishDataStream\n      summary: Publish data stream\
  \ message\n      message:\n        $ref: '#/components/messages/DataStreamMessage'\n      tags:\n        - name: streaming\ncomponents:\n  securitySchemes:\n    userPassword:\n      type: userPassword\n      description: EMS username and password authentication\n    bearerAuth:\n      type: http\n      scheme: bearer\n      bearerFormat: JWT\n      description: OAuth 2.0 bearer token for FTL API access\n  messages:\n    OrderCreated:\n      name: OrderCreated\n      title: Order Created Event\n      summary: Notification that a new order has been created\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          correlationId:\n            type: string\n            description: Correlation ID for message tracking\n          messageType:\n            type: string\n            const: OrderCreated\n          timestamp:\n            type: string\n            format: date-time\n          source:\n            type: string\n            description:\
  \ Source system identifier\n      payload:\n        $ref: '#/components/schemas/OrderEvent'\n    OrderUpdated:\n      name: OrderUpdated\n      title: Order Updated Event\n      summary: Notification that an order status has changed\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          correlationId:\n            type: string\n          messageType:\n            type: string\n            const: OrderUpdated\n          timestamp:\n            type: string\n            format: date-time\n          source:\n            type: string\n      payload:\n        $ref: '#/components/schemas/OrderStatusUpdate'\n    InventoryChanged:\n      name: InventoryChanged\n      title: Inventory Changed Event\n      summary: Notification that inventory levels have changed\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          correlationId:\n            type: string\n          messageType:\n           \
  \ type: string\n            const: InventoryChanged\n          timestamp:\n            type: string\n            format: date-time\n      payload:\n        $ref: '#/components/schemas/InventoryEvent'\n    Alert:\n      name: Alert\n      title: System Alert\n      summary: System alert notification for operational monitoring\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          correlationId:\n            type: string\n          messageType:\n            type: string\n            const: Alert\n          priority:\n            type: integer\n            minimum: 0\n            maximum: 9\n          timestamp:\n            type: string\n            format: date-time\n      payload:\n        $ref: '#/components/schemas/AlertEvent'\n    IntegrationEvent:\n      name: IntegrationEvent\n      title: Integration Event\n      summary: General-purpose integration event for inter-application messaging\n      contentType: application/json\n   \
  \   headers:\n        type: object\n        properties:\n          correlationId:\n            type: string\n          messageType:\n            type: string\n          timestamp:\n            type: string\n            format: date-time\n          source:\n            type: string\n          replyTo:\n            type: string\n            description: Reply destination for request-reply patterns\n      payload:\n        $ref: '#/components/schemas/GenericEvent'\n    DataStreamMessage:\n      name: DataStreamMessage\n      title: Data Stream Message\n      summary: High-throughput data stream message via FTL\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          sequenceNumber:\n            type: integer\n            description: Message sequence number for ordering\n          timestamp:\n            type: string\n            format: date-time\n          contentName:\n            type: string\n            description: FTL content matcher\
  \ name\n      payload:\n        $ref: '#/components/schemas/StreamPayload'\n  schemas:\n    OrderEvent:\n      type: object\n      required:\n        - orderId\n        - customerId\n        - totalAmount\n      properties:\n        orderId:\n          type: string\n          description: Unique order identifier\n        customerId:\n          type: string\n          description: Customer identifier\n        items:\n          type: array\n          items:\n            type: object\n            properties:\n              productId:\n                type: string\n              productName:\n                type: string\n              quantity:\n                type: integer\n                minimum: 1\n              unitPrice:\n                type: number\n                format: double\n          description: Order line items\n        totalAmount:\n          type: number\n          format: double\n          description: Total order amount\n        currency:\n          type: string\n  \
  \        description: Currency code (ISO 4217)\n        orderDate:\n          type: string\n          format: date-time\n          description: When the order was placed\n    OrderStatusUpdate:\n      type: object\n      required:\n        - orderId\n        - previousStatus\n        - newStatus\n      properties:\n        orderId:\n          type: string\n          description: Order identifier\n        previousStatus:\n          type: string\n          enum:\n            - created\n            - confirmed\n            - processing\n            - shipped\n            - delivered\n            - cancelled\n          description: Previous order status\n        newStatus:\n          type: string\n          enum:\n            - created\n            - confirmed\n            - processing\n            - shipped\n            - delivered\n            - cancelled\n          description: New order status\n        updatedAt:\n          type: string\n          format: date-time\n        reason:\n \
  \         type: string\n          description: Reason for status change\n    InventoryEvent:\n      type: object\n      required:\n        - productId\n        - changeType\n        - quantity\n      properties:\n        productId:\n          type: string\n          description: Product identifier\n        productName:\n          type: string\n          description: Product name\n        warehouseId:\n          type: string\n          description: Warehouse identifier\n        changeType:\n          type: string\n          enum:\n            - increment\n            - decrement\n            - adjustment\n          description: Type of inventory change\n        quantity:\n          type: integer\n          description: Quantity changed\n        previousLevel:\n          type: integer\n          description: Stock level before change\n        currentLevel:\n          type: integer\n          description: Stock level after change\n        timestamp:\n          type: string\n          format:\
  \ date-time\n    AlertEvent:\n      type: object\n      required:\n        - alertId\n        - severity\n        - message\n      properties:\n        alertId:\n          type: string\n          description: Alert unique identifier\n        severity:\n          type: string\n          enum:\n            - info\n            - warning\n            - error\n            - critical\n          description: Alert severity level\n        message:\n          type: string\n          description: Alert message\n        source:\n          type: string\n          description: Source system or component\n        category:\n          type: string\n          description: Alert category\n        details:\n          type: object\n          additionalProperties: true\n          description: Additional alert details\n        timestamp:\n          type: string\n          format: date-time\n    GenericEvent:\n      type: object\n      required:\n        - eventType\n      properties:\n        eventType:\n\
  \          type: string\n          description: Event type identifier\n        data:\n          type: object\n          additionalProperties: true\n          description: Event payload data\n        metadata:\n          type: object\n          additionalProperties: true\n          description: Event metadata\n    StreamPayload:\n      type: object\n      properties:\n        recordType:\n          type: string\n          description: Type of data record\n        data:\n          type: object\n          additionalProperties: true\n          description: Record data\n        timestamp:\n          type: string\n          format: date-time\n          description: Record timestamp\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tibco/refs/heads/main/asyncapi/tibco-messaging-asyncapi.yml
spec_file: asyncapi/tibco-messaging-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/tibco/refs/heads/main/asyncapi/tibco-messaging-asyncapi.yml
tags:
- Analytics
- API Management
- Cloud
- Enterprise Software
- Integration
- Messaging
- Real-Time Data
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
