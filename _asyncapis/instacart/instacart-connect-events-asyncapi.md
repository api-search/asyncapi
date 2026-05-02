---
api_specs:
- filename: instacart-developer-platform-api-openapi.yml
  format: yaml
  label: Instacart Developer Platform API
  slug: developer-platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/instacart/refs/heads/main/openapi/instacart-developer-platform-api-openapi.yml
- filename: instacart-connect-fulfillment-api-openapi.yml
  format: yaml
  label: Instacart Connect Fulfillment API
  slug: connect-fulfillment-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/instacart/refs/heads/main/openapi/instacart-connect-fulfillment-api-openapi.yml
- filename: instacart-connect-post-checkout-api-openapi.yml
  format: yaml
  label: Instacart Connect Post-Checkout API
  slug: connect-post-checkout-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/instacart/refs/heads/main/openapi/instacart-connect-post-checkout-api-openapi.yml
- filename: instacart-catalog-api-openapi.yml
  format: yaml
  label: Instacart Catalog API
  slug: catalog-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/instacart/refs/heads/main/openapi/instacart-catalog-api-openapi.yml
channels:
- description: The retailer's configured webhook endpoint that receives event callbacks from Instacart Connect. Events are sent as HTTP POST requests. The same event notification may be delivered multiple times when an order reverts to a previous status.
  name: /webhook
  operation: publish
  operation_id: receiveEventCallback
  summary: Receive an Instacart Connect event callback
description: Instacart Connect notifies retailers of order status changes and fulfillment events through webhook callbacks. Retailers configure callback endpoints to receive real-time notifications about order lifecycle events including order creation, shopper assignment, picking, delivery, cancellation, item replacements, and item refunds. Callback endpoints must be protected by OAuth 2.0 authentication.
layout: asyncapi
messages:
- description: ''
  name: OrderCreated
  summary: Sent when an order is successfully created in the Instacart system.
  title: Order Created
- description: ''
  name: OrderAcknowledged
  summary: Sent when a shopper acknowledges and accepts the order.
  title: Order Acknowledged
- description: ''
  name: OrderPicking
  summary: Sent when the shopper begins picking items for the order in the store.
  title: Order Picking
- description: ''
  name: OrderStaging
  summary: Sent when the order is being staged for delivery or pickup.
  title: Order Staging
- description: ''
  name: OrderDelivering
  summary: Sent when the order has left the store and is being delivered to the customer.
  title: Order Delivering
- description: ''
  name: OrderDelivered
  summary: Sent when the order has been successfully delivered to the customer.
  title: Order Delivered
- description: ''
  name: OrderCanceled
  summary: Sent when an order has been canceled.
  title: Order Canceled
- description: ''
  name: OrderRescheduled
  summary: Sent when an order will be fulfilled at a different time than originally scheduled.
  title: Order Rescheduled
- description: ''
  name: LateDelivery
  summary: Sent when the estimated delivery time has changed and the delivery will be later than originally scheduled.
  title: Late Delivery
- description: ''
  name: ItemReplacement
  summary: Sent when a shopper replaces an item in the order with a substitute product.
  title: Item Replacement
- description: ''
  name: ItemRefund
  summary: Sent when a shopper refunds an order item because it is unavailable and no suitable replacement is found.
  title: Item Refund
- description: ''
  name: CustomerMIA
  summary: Sent when the delivery driver arrives but cannot locate the customer at the delivery address.
  title: Customer MIA
name: Instacart Connect Event Callbacks
provider_name: instacart
provider_slug: instacart
servers:
- description: The retailer's webhook endpoint configured to receive event callbacks from Instacart Connect. Must support OAuth 2.0 authentication.
  name: retailerWebhook
  protocol: https
  url: '{retailer_callback_url}'
slug: instacart-connect-events-asyncapi
source_filename: instacart-connect-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Instacart Connect Event Callbacks\n  description: >-\n    Instacart Connect notifies retailers of order status changes and fulfillment\n    events through webhook callbacks. Retailers configure callback endpoints to\n    receive real-time notifications about order lifecycle events including order\n    creation, shopper assignment, picking, delivery, cancellation, item\n    replacements, and item refunds. Callback endpoints must be protected by\n    OAuth 2.0 authentication.\n  version: '2.0'\n  contact:\n    name: Instacart Connect Support\n    url: https://docs.instacart.com/connect/\nservers:\n  retailerWebhook:\n    url: '{retailer_callback_url}'\n    protocol: https\n    description: >-\n      The retailer's webhook endpoint configured to receive event callbacks\n      from Instacart Connect. Must support OAuth 2.0 authentication.\n    variables:\n      retailer_callback_url:\n        description: >-\n          The retailer's HTTPS endpoint\
  \ for receiving Instacart event\n          callbacks.\n    security:\n      - oauth2: []\nchannels:\n  /webhook:\n    description: >-\n      The retailer's configured webhook endpoint that receives event callbacks\n      from Instacart Connect. Events are sent as HTTP POST requests. The same\n      event notification may be delivered multiple times when an order reverts\n      to a previous status.\n    publish:\n      operationId: receiveEventCallback\n      summary: Receive an Instacart Connect event callback\n      description: >-\n        Receives event callbacks from Instacart Connect about order status\n        changes, item replacements, and item refunds. Retailers should handle\n        duplicate deliveries of the same event gracefully.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/OrderCreated'\n          - $ref: '#/components/messages/OrderAcknowledged'\n          - $ref: '#/components/messages/OrderPicking'\n          - $ref: '#/components/messages/OrderStaging'\n\
  \          - $ref: '#/components/messages/OrderDelivering'\n          - $ref: '#/components/messages/OrderDelivered'\n          - $ref: '#/components/messages/OrderCanceled'\n          - $ref: '#/components/messages/OrderRescheduled'\n          - $ref: '#/components/messages/LateDelivery'\n          - $ref: '#/components/messages/ItemReplacement'\n          - $ref: '#/components/messages/ItemRefund'\n          - $ref: '#/components/messages/CustomerMIA'\ncomponents:\n  securitySchemes:\n    oauth2:\n      type: oauth2\n      description: >-\n        OAuth 2.0 authentication required on the retailer's callback endpoint.\n        Instacart authenticates to the retailer's endpoint using OAuth 2.0\n        before sending event data.\n      flows:\n        clientCredentials:\n          tokenUrl: '{retailer_token_url}'\n          scopes: {}\n  messages:\n    OrderCreated:\n      name: fulfillment.order_created\n      title: Order Created\n      summary: >-\n        Sent when an order is successfully\
  \ created in the Instacart system.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderEventPayload'\n    OrderAcknowledged:\n      name: fulfillment.acknowledged\n      title: Order Acknowledged\n      summary: >-\n        Sent when a shopper acknowledges and accepts the order.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderEventPayload'\n    OrderPicking:\n      name: fulfillment.picking\n      title: Order Picking\n      summary: >-\n        Sent when the shopper begins picking items for the order in the store.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderEventPayload'\n    OrderStaging:\n      name: fulfillment.staging\n      title: Order Staging\n      summary: >-\n        Sent when the order is being staged for delivery or pickup.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderEventPayload'\n \
  \   OrderDelivering:\n      name: fulfillment.delivering\n      title: Order Delivering\n      summary: >-\n        Sent when the order has left the store and is being delivered to the\n        customer.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderEventPayload'\n    OrderDelivered:\n      name: fulfillment.delivered\n      title: Order Delivered\n      summary: >-\n        Sent when the order has been successfully delivered to the customer.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderEventPayload'\n    OrderCanceled:\n      name: fulfillment.canceled\n      title: Order Canceled\n      summary: >-\n        Sent when an order has been canceled.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderEventPayload'\n    OrderRescheduled:\n      name: fulfillment.rescheduled\n      title: Order Rescheduled\n      summary: >-\n        Sent when an order\
  \ will be fulfilled at a different time than\n        originally scheduled.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderEventPayload'\n    LateDelivery:\n      name: fulfillment.late_delivery\n      title: Late Delivery\n      summary: >-\n        Sent when the estimated delivery time has changed and the delivery\n        will be later than originally scheduled.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderEventPayload'\n    ItemReplacement:\n      name: fulfillment.order_item_replacement\n      title: Item Replacement\n      summary: >-\n        Sent when a shopper replaces an item in the order with a substitute\n        product.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ItemEventPayload'\n    ItemRefund:\n      name: fulfillment.order_item_refund\n      title: Item Refund\n      summary: >-\n        Sent when a shopper refunds an order item\
  \ because it is unavailable\n        and no suitable replacement is found.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ItemEventPayload'\n    CustomerMIA:\n      name: fulfillment.customer_mia\n      title: Customer MIA\n      summary: >-\n        Sent when the delivery driver arrives but cannot locate the customer\n        at the delivery address.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderEventPayload'\n  schemas:\n    OrderEventPayload:\n      type: object\n      properties:\n        event:\n          type: string\n          description: >-\n            The event type identifier such as fulfillment.delivered or\n            fulfillment.canceled.\n        order_id:\n          type: string\n          description: >-\n            The unique identifier for the order.\n        status:\n          type: string\n          enum:\n            - brand_new\n            - acknowledged\n            -\
  \ picking\n            - staging\n            - delivering\n            - delivered\n            - canceled\n            - rescheduled\n          description: >-\n            The current status of the order.\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            The timestamp when the event occurred.\n        order:\n          type: object\n          description: >-\n            Summary details about the order.\n          properties:\n            id:\n              type: string\n              description: >-\n                The order identifier.\n            user_id:\n              type: string\n              description: >-\n                The retailer's user identifier for the customer.\n            fulfillment_type:\n              type: string\n              enum:\n                - delivery\n                - pickup\n                - last_mile\n              description: >-\n                The fulfillment type of the order.\n\
  \            created_at:\n              type: string\n              format: date-time\n              description: >-\n                When the order was created.\n            estimated_delivery_at:\n              type: string\n              format: date-time\n              description: >-\n                The estimated delivery or pickup time.\n    ItemEventPayload:\n      type: object\n      properties:\n        event:\n          type: string\n          description: >-\n            The event type identifier such as fulfillment.order_item_refund\n            or fulfillment.order_item_replacement.\n        order_id:\n          type: string\n          description: >-\n            The unique identifier for the order.\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            The timestamp when the event occurred.\n        items:\n          type: array\n          description: >-\n            The full list of order items with their current\
  \ statuses. Check\n            the refunded or replaced fields to determine which items were\n            affected.\n          items:\n            type: object\n            properties:\n              product_id:\n                type: string\n                description: >-\n                  The product identifier.\n              name:\n                type: string\n                description: >-\n                  The name of the product.\n              quantity:\n                type: integer\n                description: >-\n                  The ordered quantity.\n              status:\n                type: string\n                enum:\n                  - found\n                  - replaced\n                  - refunded\n                  - pending\n                description: >-\n                  The current status of the item.\n              refunded:\n                type: boolean\n                description: >-\n                  Whether this item has been refunded.\n \
  \             replacement:\n                type: object\n                description: >-\n                  Details about the replacement product, if the item was\n                  replaced.\n                properties:\n                  product_id:\n                    type: string\n                    description: >-\n                      The product identifier of the replacement.\n                  name:\n                    type: string\n                    description: >-\n                      The name of the replacement product.\n                  quantity:\n                    type: integer\n                    description: >-\n                      The quantity of the replacement.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/instacart/refs/heads/main/asyncapi/instacart-connect-events-asyncapi.yml
spec_file: asyncapi/instacart-connect-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/instacart/refs/heads/main/asyncapi/instacart-connect-events-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '2.0'
---
