---
api_specs:
- filename: doordash-drive-openapi.yml
  format: yaml
  label: DoorDash Drive API
  slug: drive-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-drive-openapi.yml
- filename: doordash-drive-classic-openapi.yml
  format: yaml
  label: DoorDash Drive Classic API
  slug: drive-classic-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-drive-classic-openapi.yml
- filename: doordash-marketplace-openapi.yml
  format: yaml
  label: DoorDash Marketplace API
  slug: marketplace-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-marketplace-openapi.yml
- filename: doordash-item-management-openapi.yml
  format: yaml
  label: DoorDash Item Management API
  slug: marketplace-item-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-item-management-openapi.yml
- filename: doordash-reporting-openapi.yml
  format: yaml
  label: DoorDash Reporting API
  slug: reporting-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-reporting-openapi.yml
channels:
- description: DoorDash sends new order notifications to this channel when customers place orders through the marketplace.
  name: /orders
  operation: publish
  operation_id: receiveOrderWebhook
  summary: Receive new order webhooks
- description: DoorDash sends menu processing status notifications after a menu creation or update request is processed.
  name: /menus
  operation: publish
  operation_id: receiveMenuWebhook
  summary: Receive menu status webhooks
- description: DoorDash sends delivery status updates for marketplace orders including Dasher assignment, pickup, and dropoff events.
  name: /deliveries
  operation: publish
  operation_id: receiveDeliveryStatusWebhook
  summary: Receive delivery status webhooks
- description: DoorDash sends store onboarding status notifications during the partner integration setup process.
  name: /onboarding
  operation: publish
  operation_id: receiveOnboardingWebhook
  summary: Receive store onboarding webhooks
description: DoorDash Marketplace sends webhook notifications for order events, menu processing status, delivery status updates, and store onboarding events. Each environment (Sandbox and Production) supports only one webhook endpoint. Production access must be requested before configuring a production webhook endpoint. Partners confirm order receipt by returning a 200 status code; non-2xx responses are treated as order failures.
layout: asyncapi
messages:
- description: ''
  name: NewOrder
  summary: A new order has been placed through the DoorDash marketplace and needs to be confirmed by the partner.
  title: New Order Event
- description: ''
  name: MenuStatus
  summary: A menu creation or update has completed processing or encountered an error.
  title: Menu Processing Status Event
- description: ''
  name: DeliveryStatus
  summary: A delivery status update for a marketplace order including Dasher location and status.
  title: Delivery Status Update Event
- description: ''
  name: StoreOnboarding
  summary: A store onboarding status change during the integration setup process.
  title: Store Onboarding Event
name: DoorDash Marketplace Webhooks
provider_name: doordash
provider_slug: doordash
servers:
- description: The partner-provided HTTPS webhook endpoint for receiving marketplace events. Each environment supports only one webhook endpoint.
  name: partnerWebhook
  protocol: https
  url: '{webhook_url}'
slug: doordash-marketplace-webhooks-asyncapi
source_filename: doordash-marketplace-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: DoorDash Marketplace Webhooks\n  description: >-\n    DoorDash Marketplace sends webhook notifications for order events, menu\n    processing status, delivery status updates, and store onboarding events.\n    Each environment (Sandbox and Production) supports only one webhook\n    endpoint. Production access must be requested before configuring a\n    production webhook endpoint. Partners confirm order receipt by returning\n    a 200 status code; non-2xx responses are treated as order failures.\n  version: '1.0'\n  contact:\n    name: DoorDash Developer Support\n    url: https://developer.doordash.com/en-US/\nservers:\n  partnerWebhook:\n    url: '{webhook_url}'\n    protocol: https\n    description: >-\n      The partner-provided HTTPS webhook endpoint for receiving marketplace\n      events. Each environment supports only one webhook endpoint.\n    security:\n      - basicAuth: []\n    variables:\n      webhook_url:\n        description: >-\n\
  \          The HTTPS URL of the partner's webhook endpoint.\nchannels:\n  /orders:\n    description: >-\n      DoorDash sends new order notifications to this channel when customers\n      place orders through the marketplace.\n    publish:\n      operationId: receiveOrderWebhook\n      summary: Receive new order webhooks\n      description: >-\n        Receives webhook notifications for new orders placed through DoorDash.\n        Partners must return 200 to confirm the order. Non-2xx responses are\n        treated as order failures.\n      message:\n        $ref: '#/components/messages/NewOrder'\n  /menus:\n    description: >-\n      DoorDash sends menu processing status notifications after a menu\n      creation or update request is processed.\n    publish:\n      operationId: receiveMenuWebhook\n      summary: Receive menu status webhooks\n      description: >-\n        Receives webhook notifications about menu creation or update\n        processing results. Sent when the menu processing\
  \ pipeline\n        completes or encounters an error.\n      message:\n        $ref: '#/components/messages/MenuStatus'\n  /deliveries:\n    description: >-\n      DoorDash sends delivery status updates for marketplace orders\n      including Dasher assignment, pickup, and dropoff events.\n    publish:\n      operationId: receiveDeliveryStatusWebhook\n      summary: Receive delivery status webhooks\n      description: >-\n        Receives webhook notifications about delivery status changes for\n        marketplace orders, including Dasher tracking information.\n      message:\n        $ref: '#/components/messages/DeliveryStatus'\n  /onboarding:\n    description: >-\n      DoorDash sends store onboarding status notifications during the\n      partner integration setup process.\n    publish:\n      operationId: receiveOnboardingWebhook\n      summary: Receive store onboarding webhooks\n      description: >-\n        Receives webhook notifications about store onboarding status\n        changes\
  \ during the integration setup process.\n      message:\n        $ref: '#/components/messages/StoreOnboarding'\ncomponents:\n  securitySchemes:\n    basicAuth:\n      type: http\n      scheme: basic\n      description: >-\n        Basic authentication for webhook endpoint security.\n  messages:\n    NewOrder:\n      name: NewOrder\n      title: New Order Event\n      summary: >-\n        A new order has been placed through the DoorDash marketplace and\n        needs to be confirmed by the partner.\n      payload:\n        $ref: '#/components/schemas/OrderWebhookPayload'\n    MenuStatus:\n      name: MenuStatus\n      title: Menu Processing Status Event\n      summary: >-\n        A menu creation or update has completed processing or encountered\n        an error.\n      payload:\n        $ref: '#/components/schemas/MenuWebhookPayload'\n    DeliveryStatus:\n      name: DeliveryStatus\n      title: Delivery Status Update Event\n      summary: >-\n        A delivery status update for a marketplace\
  \ order including Dasher\n        location and status.\n      payload:\n        $ref: '#/components/schemas/MarketplaceDeliveryWebhookPayload'\n    StoreOnboarding:\n      name: StoreOnboarding\n      title: Store Onboarding Event\n      summary: >-\n        A store onboarding status change during the integration setup\n        process.\n      payload:\n        $ref: '#/components/schemas/OnboardingWebhookPayload'\n  schemas:\n    OrderWebhookPayload:\n      type: object\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of order event.\n          enum:\n            - new_order\n            - order_cancelled\n        order_id:\n          type: string\n          description: >-\n            The unique DoorDash order identifier.\n        store_id:\n          type: string\n          description: >-\n            The merchant-supplied store identifier.\n        status:\n          type: string\n          description: >-\n        \
  \    The order status.\n        subtotal:\n          type: integer\n          description: >-\n            The order subtotal in cents.\n        tax:\n          type: integer\n          description: >-\n            The tax amount in cents.\n        tip:\n          type: integer\n          description: >-\n            The tip amount in cents.\n        items:\n          type: array\n          description: >-\n            The items in the order.\n          items:\n            $ref: '#/components/schemas/OrderItem'\n        customer:\n          $ref: '#/components/schemas/Customer'\n        delivery_address:\n          type: string\n          description: >-\n            The delivery address.\n        special_instructions:\n          type: string\n          description: >-\n            Special instructions from the customer.\n        estimated_pickup_time:\n          type: string\n          format: date-time\n          description: >-\n            The estimated time the Dasher will arrive\
  \ for pickup.\n        created_at:\n          type: string\n          format: date-time\n          description: >-\n            When the order was created.\n    OrderItem:\n      type: object\n      properties:\n        id:\n          type: string\n          description: >-\n            The unique item identifier.\n        name:\n          type: string\n          description: >-\n            The item name.\n        quantity:\n          type: integer\n          description: >-\n            The quantity ordered.\n        price:\n          type: integer\n          description: >-\n            The item price in cents.\n        special_instructions:\n          type: string\n          description: >-\n            Special instructions for this item.\n        options:\n          type: array\n          description: >-\n            Selected options for the item.\n          items:\n            $ref: '#/components/schemas/ItemOption'\n    ItemOption:\n      type: object\n      properties:\n      \
  \  id:\n          type: string\n          description: >-\n            The option identifier.\n        name:\n          type: string\n          description: >-\n            The option name.\n        quantity:\n          type: integer\n          description: >-\n            The quantity of this option.\n        price:\n          type: integer\n          description: >-\n            The option price in cents.\n    Customer:\n      type: object\n      properties:\n        first_name:\n          type: string\n          description: >-\n            The customer's first name.\n        last_name:\n          type: string\n          description: >-\n            The customer's last name.\n        phone_number:\n          type: string\n          description: >-\n            The customer's phone number.\n    MenuWebhookPayload:\n      type: object\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of menu event.\n          enum:\n     \
  \       - menu_created\n            - menu_updated\n            - menu_failed\n        menu_id:\n          type: string\n          description: >-\n            The unique menu identifier.\n        store_id:\n          type: string\n          description: >-\n            The merchant-supplied store identifier.\n        status:\n          type: string\n          description: >-\n            The menu processing status.\n          enum:\n            - completed\n            - failed\n        error_message:\n          type: string\n          description: >-\n            Error details if the menu processing failed.\n        processed_at:\n          type: string\n          format: date-time\n          description: >-\n            When the menu processing completed.\n    MarketplaceDeliveryWebhookPayload:\n      type: object\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of delivery event.\n          enum:\n            - dasher_confirmed\n\
  \            - dasher_at_store\n            - dasher_picked_up\n            - dasher_at_customer\n            - dasher_delivered\n        order_id:\n          type: string\n          description: >-\n            The DoorDash order identifier.\n        dasher_name:\n          type: string\n          description: >-\n            The Dasher's first name.\n        dasher_phone_number:\n          type: string\n          description: >-\n            The Dasher's phone number.\n        dasher_location_lat:\n          type: number\n          format: double\n          description: >-\n            The Dasher's current latitude.\n        dasher_location_lng:\n          type: number\n          format: double\n          description: >-\n            The Dasher's current longitude.\n        estimated_delivery_time:\n          type: string\n          format: date-time\n          description: >-\n            The estimated delivery time.\n        tracking_url:\n          type: string\n          format:\
  \ uri\n          description: >-\n            A URL for tracking the delivery.\n    OnboardingWebhookPayload:\n      type: object\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of onboarding event.\n          enum:\n            - store_activated\n            - store_deactivated\n            - onboarding_completed\n            - onboarding_failed\n        store_id:\n          type: string\n          description: >-\n            The merchant-supplied store identifier.\n        status:\n          type: string\n          description: >-\n            The onboarding status.\n        message:\n          type: string\n          description: >-\n            Additional details about the onboarding event.\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            When the onboarding event occurred.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/asyncapi/doordash-marketplace-webhooks-asyncapi.yml
spec_file: asyncapi/doordash-marketplace-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/asyncapi/doordash-marketplace-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
