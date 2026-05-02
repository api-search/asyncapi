---
api_specs:
- filename: grubhub-menu-openapi.yml
  format: yaml
  label: Grubhub Menu API
  slug: menu-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/openapi/grubhub-menu-openapi.yml
- filename: grubhub-orders-openapi.yml
  format: yaml
  label: Grubhub Orders API
  slug: orders-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/openapi/grubhub-orders-openapi.yml
- filename: grubhub-merchant-data-openapi.yml
  format: yaml
  label: Grubhub Merchant Data API
  slug: merchant-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/openapi/grubhub-merchant-data-openapi.yml
- filename: grubhub-merchant-schedules-openapi.yml
  format: yaml
  label: Grubhub Merchant Schedules API
  slug: merchant-schedules-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/openapi/grubhub-merchant-schedules-openapi.yml
- filename: grubhub-deliveries-openapi.yml
  format: yaml
  label: Grubhub Deliveries API
  slug: deliveries-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/openapi/grubhub-deliveries-openapi.yml
- filename: grubhub-onboarding-openapi.yml
  format: yaml
  label: Grubhub Onboarding API
  slug: onboarding-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/openapi/grubhub-onboarding-openapi.yml
channels:
- description: Channel for receiving order notification events. Grubhub posts webhook payloads to the partner's configured endpoint when order events occur.
  name: /webhook/orders
  operation: publish
  operation_id: receiveOrderEvent
  summary: Receive order notification events
description: Event-driven interface for receiving real-time order notifications from Grubhub. When a diner places an order, Grubhub monitors that order and sends notifications based on the current status. The webhook channel passes a payload of information about the order to a specified URI. New orders are expected to be received through webhooks rather than by polling API endpoints. Partners configure webhook subscriptions to receive order lifecycle events in real time.
layout: asyncapi
messages:
- description: ''
  name: NewOrder
  summary: A new order has been placed by a diner on Grubhub and is ready for the partner to process.
  title: New Order
- description: ''
  name: OrderStatusChange
  summary: An order's status has changed in the Grubhub system, such as moving to confirmed, in progress, or ready states.
  title: Order Status Change
- description: ''
  name: OrderCancellation
  summary: An order has been cancelled by either the diner or the Grubhub system.
  title: Order Cancellation
- description: ''
  name: OrderChangeRequest
  summary: A change has been requested for an existing order, such as item modifications or special instruction updates.
  title: Order Change Request
name: Grubhub Order Events
provider_name: grubhub
provider_slug: grubhub
servers:
- description: Partner-hosted webhook endpoint. Grubhub sends order event payloads to this URL. Partners cannot set up or modify webhook URLs on their own as manual verification is required.
  name: partnerWebhook
  protocol: https
  url: '{webhookUrl}'
slug: grubhub-order-events-asyncapi
source_filename: grubhub-order-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Grubhub Order Events\n  description: >-\n    Event-driven interface for receiving real-time order notifications from\n    Grubhub. When a diner places an order, Grubhub monitors that order and\n    sends notifications based on the current status. The webhook channel\n    passes a payload of information about the order to a specified URI.\n    New orders are expected to be received through webhooks rather than\n    by polling API endpoints. Partners configure webhook subscriptions\n    to receive order lifecycle events in real time.\n  version: '1.0.0'\n  contact:\n    name: Grubhub Developer Support\n    url: https://grubhub-developers.zendesk.com/hc/en-us\nservers:\n  partnerWebhook:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Partner-hosted webhook endpoint. Grubhub sends order event payloads\n      to this URL. Partners cannot set up or modify webhook URLs on their\n      own as manual verification is required.\n\
  \    variables:\n      webhookUrl:\n        description: >-\n          The partner's webhook endpoint URL configured during onboarding.\n    security:\n      - basicAuth: []\n      - hmacAuth: []\nchannels:\n  /webhook/orders:\n    description: >-\n      Channel for receiving order notification events. Grubhub posts\n      webhook payloads to the partner's configured endpoint when order\n      events occur.\n    publish:\n      operationId: receiveOrderEvent\n      summary: Receive order notification events\n      description: >-\n        Receives order lifecycle events from Grubhub including new orders,\n        order confirmations, status changes, and cancellations.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/NewOrder'\n          - $ref: '#/components/messages/OrderStatusChange'\n          - $ref: '#/components/messages/OrderCancellation'\n          - $ref: '#/components/messages/OrderChangeRequest'\ncomponents:\n  securitySchemes:\n    basicAuth:\n    \
  \  type: userPassword\n      description: >-\n        Basic authentication using a username and password selected\n        during partner signup. Credentials are included in the header\n        of webhook requests from Grubhub.\n    hmacAuth:\n      type: httpApiKey\n      name: Authorization\n      in: header\n      description: >-\n        HMAC authentication providing a higher level of security by\n        constructing a signature in the request header. Includes details\n        about the sender and ensures the integrity of the message.\n        HMAC is recommended for most webhook integrations.\n  messages:\n    NewOrder:\n      name: NewOrder\n      title: New Order\n      summary: >-\n        A new order has been placed by a diner on Grubhub and is ready\n        for the partner to process.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderWebhookPayload'\n    OrderStatusChange:\n      name: OrderStatusChange\n      title: Order Status\
  \ Change\n      summary: >-\n        An order's status has changed in the Grubhub system, such as\n        moving to confirmed, in progress, or ready states.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderStatusWebhookPayload'\n    OrderCancellation:\n      name: OrderCancellation\n      title: Order Cancellation\n      summary: >-\n        An order has been cancelled by either the diner or the Grubhub\n        system.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderCancellationPayload'\n    OrderChangeRequest:\n      name: OrderChangeRequest\n      title: Order Change Request\n      summary: >-\n        A change has been requested for an existing order, such as item\n        modifications or special instruction updates.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderChangeRequestPayload'\n  schemas:\n    OrderWebhookPayload:\n      type: object\n\
  \      description: >-\n        Webhook payload for a new order placed through Grubhub.\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of event that triggered this webhook.\n          const: NEW_ORDER\n        order_uuid:\n          type: string\n          format: uuid\n          description: >-\n            The unique identifier for the order.\n        merchant_id:\n          type: string\n          description: >-\n            The Grubhub merchant identifier.\n        placed_at:\n          type: string\n          format: date-time\n          description: >-\n            When the order was placed.\n        fulfillment_type:\n          type: string\n          description: >-\n            The type of fulfillment requested.\n          enum:\n            - DELIVERY\n            - PICKUP\n        customer:\n          type: object\n          description: >-\n            Customer details for the order.\n          properties:\n\
  \            first_name:\n              type: string\n              description: >-\n                Customer's first name.\n            last_name:\n              type: string\n              description: >-\n                Customer's last name.\n            phone:\n              type: string\n              description: >-\n                Customer's phone number.\n        items:\n          type: array\n          description: >-\n            Items included in the order.\n          items:\n            type: object\n            properties:\n              item_id:\n                type: string\n                description: >-\n                  The menu item identifier.\n              name:\n                type: string\n                description: >-\n                  The item name.\n              quantity:\n                type: integer\n                description: >-\n                  The quantity ordered.\n              price:\n                type: number\n                format:\
  \ double\n                description: >-\n                  The unit price.\n              modifiers:\n                type: array\n                description: >-\n                  Applied modifiers.\n                items:\n                  type: object\n                  properties:\n                    name:\n                      type: string\n                      description: >-\n                        Modifier name.\n                    price:\n                      type: number\n                      format: double\n                      description: >-\n                        Modifier price.\n        totals:\n          type: object\n          description: >-\n            Financial totals for the order.\n          properties:\n            subtotal:\n              type: number\n              format: double\n              description: >-\n                Subtotal before taxes and fees.\n            tax:\n              type: number\n              format: double\n           \
  \   description: >-\n                Tax amount.\n            tip:\n              type: number\n              format: double\n              description: >-\n                Tip amount.\n            total:\n              type: number\n              format: double\n              description: >-\n                Total order amount.\n        delivery_address:\n          type: object\n          description: >-\n            Delivery address for the order.\n          properties:\n            street_address:\n              type: string\n              description: >-\n                Street address.\n            city:\n              type: string\n              description: >-\n                City name.\n            state:\n              type: string\n              description: >-\n                State abbreviation.\n            zip:\n              type: string\n              description: >-\n                ZIP code.\n        special_instructions:\n          type: string\n          description:\
  \ >-\n            Special instructions from the customer.\n    OrderStatusWebhookPayload:\n      type: object\n      description: >-\n        Webhook payload for an order status change event.\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of event that triggered this webhook.\n          const: ORDER_STATUS_CHANGE\n        order_uuid:\n          type: string\n          format: uuid\n          description: >-\n            The unique identifier for the order.\n        merchant_id:\n          type: string\n          description: >-\n            The Grubhub merchant identifier.\n        previous_status:\n          type: string\n          description: >-\n            The previous order status.\n        new_status:\n          type: string\n          description: >-\n            The new order status.\n          enum:\n            - CONFIRMED\n            - IN_PROGRESS\n            - READY\n            - OUT_FOR_DELIVERY\n      \
  \      - COMPLETED\n        updated_at:\n          type: string\n          format: date-time\n          description: >-\n            When the status was updated.\n    OrderCancellationPayload:\n      type: object\n      description: >-\n        Webhook payload for an order cancellation event.\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of event that triggered this webhook.\n          const: ORDER_CANCELLED\n        order_uuid:\n          type: string\n          format: uuid\n          description: >-\n            The unique identifier for the cancelled order.\n        merchant_id:\n          type: string\n          description: >-\n            The Grubhub merchant identifier.\n        cancelled_by:\n          type: string\n          description: >-\n            Who initiated the cancellation.\n          enum:\n            - DINER\n            - MERCHANT\n            - SYSTEM\n        reason:\n          type: string\n\
  \          description: >-\n            The reason for cancellation.\n        cancelled_at:\n          type: string\n          format: date-time\n          description: >-\n            When the order was cancelled.\n    OrderChangeRequestPayload:\n      type: object\n      description: >-\n        Webhook payload for an order change request event.\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of event that triggered this webhook.\n          const: ORDER_CHANGE_REQUEST\n        order_uuid:\n          type: string\n          format: uuid\n          description: >-\n            The unique identifier for the order.\n        merchant_id:\n          type: string\n          description: >-\n            The Grubhub merchant identifier.\n        change_request_id:\n          type: string\n          description: >-\n            The unique identifier for the change request.\n        change_type:\n          type: string\n         \
  \ description: >-\n            The type of change being requested.\n        details:\n          type: string\n          description: >-\n            Details about the requested change.\n        requested_at:\n          type: string\n          format: date-time\n          description: >-\n            When the change was requested.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/asyncapi/grubhub-order-events-asyncapi.yml
spec_file: asyncapi/grubhub-order-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/asyncapi/grubhub-order-events-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
