---
api_specs:
- filename: squarespace-commerce-api-openapi.yml
  format: yaml
  label: Squarespace Commerce API
  slug: squarespace-commerce-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-commerce-api-openapi.yml
- filename: squarespace-orders-api-openapi.yml
  format: yaml
  label: Squarespace Orders API
  slug: squarespace-orders-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-orders-api-openapi.yml
- filename: squarespace-products-api-openapi.yml
  format: yaml
  label: Squarespace Products API
  slug: squarespace-products-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-products-api-openapi.yml
- filename: squarespace-inventory-api-openapi.yml
  format: yaml
  label: Squarespace Inventory API
  slug: squarespace-inventory-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-inventory-api-openapi.yml
- filename: squarespace-profiles-api-openapi.yml
  format: yaml
  label: Squarespace Profiles API
  slug: squarespace-profiles-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-profiles-api-openapi.yml
- filename: squarespace-transactions-api-openapi.yml
  format: yaml
  label: Squarespace Transactions API
  slug: squarespace-transactions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-transactions-api-openapi.yml
- filename: squarespace-webhook-subscriptions-api-openapi.yml
  format: yaml
  label: Squarespace Webhook Subscriptions API
  slug: squarespace-webhook-subscriptions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/openapi/squarespace-webhook-subscriptions-api-openapi.yml
channels:
- description: The endpoint on the subscriber's server that receives webhook notifications from Squarespace. Squarespace sends HTTP POST requests with JSON payloads and a Squarespace-Signature header for verification.
  name: /webhook
  operation: publish
  operation_id: receiveWebhookNotification
  summary: Receive a webhook notification from Squarespace
description: The Squarespace webhook system delivers real-time event notifications to registered endpoint URLs when commerce activity occurs on a merchant site. Supported events include order creation, order updates, and extension uninstalls. Each notification includes a unique identifier, the website ID, subscription ID, topic, and a data payload specific to the event type. Notifications are signed using HMAC-SHA256 with the subscription secret, enabling receivers to verify authenticity via the Squarespace-Signature header.
layout: asyncapi
messages:
- description: Squarespace sends this notification when a customer places a new order on the merchant site. The data payload contains the unique order ID. Use the Orders API to retrieve full order details using this ID.
  name: OrderCreateNotification
  summary: Notification sent when a new order is created on the merchant site
  title: Order Create Notification
- description: Squarespace sends this notification when an order is modified, such as when fulfillment status changes or the order is refunded. The data payload contains the order ID and an update type description.
  name: OrderUpdateNotification
  summary: Notification sent when an existing order is updated on the merchant site
  title: Order Update Notification
- description: Squarespace sends this notification when a merchant uninstalls a Squarespace Extension. Receiving this event should trigger cleanup of any stored data or active resources associated with the merchant's site in the extension's backend systems.
  name: ExtensionUninstallNotification
  summary: Notification sent when a Squarespace Extension is uninstalled from a site
  title: Extension Uninstall Notification
name: Squarespace Webhook Events
provider_name: Squarespace
provider_slug: squarespace
servers:
- description: Squarespace sends webhook notifications as HTTP POST requests from this origin. Receiving endpoints must be publicly accessible HTTPS URLs registered via the Webhook Subscriptions API.
  name: squarespace
  protocol: https
  url: https://api.squarespace.com
slug: squarespace-webhooks-asyncapi
source_filename: squarespace-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Squarespace Webhook Events\n  description: >-\n    The Squarespace webhook system delivers real-time event notifications to\n    registered endpoint URLs when commerce activity occurs on a merchant site.\n    Supported events include order creation, order updates, and extension uninstalls.\n    Each notification includes a unique identifier, the website ID, subscription ID,\n    topic, and a data payload specific to the event type. Notifications are signed\n    using HMAC-SHA256 with the subscription secret, enabling receivers to verify\n    authenticity via the Squarespace-Signature header.\n  version: '1.0'\n  contact:\n    name: Squarespace Developer Support\n    url: https://developers.squarespace.com/webhooks/overview\n  termsOfService: https://www.squarespace.com/terms-of-service\nexternalDocs:\n  description: Squarespace Webhooks Documentation\n  url: https://developers.squarespace.com/webhooks/overview\nservers:\n  squarespace:\n   \
  \ url: 'https://api.squarespace.com'\n    protocol: https\n    description: >-\n      Squarespace sends webhook notifications as HTTP POST requests from this\n      origin. Receiving endpoints must be publicly accessible HTTPS URLs registered\n      via the Webhook Subscriptions API.\n    security:\n      - hmacSignature: []\nchannels:\n  /webhook:\n    description: >-\n      The endpoint on the subscriber's server that receives webhook notifications\n      from Squarespace. Squarespace sends HTTP POST requests with JSON payloads\n      and a Squarespace-Signature header for verification.\n    publish:\n      operationId: receiveWebhookNotification\n      summary: Receive a webhook notification from Squarespace\n      description: >-\n        Squarespace sends this message to the subscriber's registered endpoint URL\n        when a subscribed event occurs on the merchant site. The receiver should\n        validate the Squarespace-Signature header before processing the payload.\n      \
  \  Squarespace expects a 2xx response within a short timeout window.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/OrderCreateNotification'\n          - $ref: '#/components/messages/OrderUpdateNotification'\n          - $ref: '#/components/messages/ExtensionUninstallNotification'\ncomponents:\n  securitySchemes:\n    hmacSignature:\n      type: httpApiKey\n      name: Squarespace-Signature\n      in: header\n      description: >-\n        HMAC-SHA256 signature generated by signing the raw request body with the\n        webhook subscription secret as the key. Recipients must compute the same\n        signature and compare it to the header value to verify the notification\n        originated from Squarespace.\n  messages:\n    OrderCreateNotification:\n      name: order.create\n      title: Order Create Notification\n      summary: Notification sent when a new order is created on the merchant site\n      description: >-\n        Squarespace sends this notification\
  \ when a customer places a new order on\n        the merchant site. The data payload contains the unique order ID. Use the\n        Orders API to retrieve full order details using this ID.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          Squarespace-Signature:\n            type: string\n            description: >-\n              HMAC-SHA256 signature of the request body using the subscription\n              secret as the key. Used to verify notification authenticity.\n      payload:\n        $ref: '#/components/schemas/OrderCreatePayload'\n    OrderUpdateNotification:\n      name: order.update\n      title: Order Update Notification\n      summary: Notification sent when an existing order is updated on the merchant site\n      description: >-\n        Squarespace sends this notification when an order is modified, such as when\n        fulfillment status changes or the order is refunded. The data payload contains\n        the order\
  \ ID and an update type description.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          Squarespace-Signature:\n            type: string\n            description: >-\n              HMAC-SHA256 signature of the request body using the subscription\n              secret as the key. Used to verify notification authenticity.\n      payload:\n        $ref: '#/components/schemas/OrderUpdatePayload'\n    ExtensionUninstallNotification:\n      name: extension.uninstall\n      title: Extension Uninstall Notification\n      summary: Notification sent when a Squarespace Extension is uninstalled from a site\n      description: >-\n        Squarespace sends this notification when a merchant uninstalls a Squarespace\n        Extension. Receiving this event should trigger cleanup of any stored data\n        or active resources associated with the merchant's site in the extension's\n        backend systems.\n      contentType: application/json\n \
  \     headers:\n        type: object\n        properties:\n          Squarespace-Signature:\n            type: string\n            description: >-\n              HMAC-SHA256 signature of the request body using the subscription\n              secret as the key. Used to verify notification authenticity.\n      payload:\n        $ref: '#/components/schemas/ExtensionUninstallPayload'\n  schemas:\n    NotificationBase:\n      type: object\n      description: Common fields present in all Squarespace webhook notification payloads\n      required:\n        - notificationId\n        - websiteId\n        - subscriptionId\n        - topic\n        - createdOn\n      properties:\n        notificationId:\n          type: string\n          description: Unique identifier for this specific notification delivery\n        websiteId:\n          type: string\n          description: >-\n            Unique identifier of the Squarespace website that triggered the\n            notification\n        subscriptionId:\n\
  \          type: string\n          description: Unique identifier of the webhook subscription that received this event\n        topic:\n          type: string\n          description: The event topic that triggered this notification\n          enum:\n            - order.create\n            - order.update\n            - extension.uninstall\n        createdOn:\n          type: string\n          format: date-time\n          description: ISO 8601 UTC timestamp when the notification was created\n    OrderCreatePayload:\n      allOf:\n        - $ref: '#/components/schemas/NotificationBase'\n        - type: object\n          description: Payload for an order.create webhook notification\n          required:\n            - data\n          properties:\n            topic:\n              type: string\n              enum:\n                - order.create\n            data:\n              type: object\n              description: Data payload for the order create event\n              required:\n      \
  \          - orderId\n              properties:\n                orderId:\n                  type: string\n                  description: >-\n                    Unique identifier of the newly created order. Use this ID with\n                    the Orders API to retrieve full order details.\n    OrderUpdatePayload:\n      allOf:\n        - $ref: '#/components/schemas/NotificationBase'\n        - type: object\n          description: Payload for an order.update webhook notification\n          required:\n            - data\n          properties:\n            topic:\n              type: string\n              enum:\n                - order.update\n            data:\n              type: object\n              description: Data payload for the order update event\n              required:\n                - orderId\n              properties:\n                orderId:\n                  type: string\n                  description: >-\n                    Unique identifier of the updated order. Use\
  \ this ID with the\n                    Orders API to retrieve the current order state.\n                orderUpdate:\n                  type: string\n                  description: >-\n                    A string describing the type of update that was made to the\n                    order, such as fulfillment status changes or refunds.\n    ExtensionUninstallPayload:\n      allOf:\n        - $ref: '#/components/schemas/NotificationBase'\n        - type: object\n          description: Payload for an extension.uninstall webhook notification\n          required:\n            - data\n          properties:\n            topic:\n              type: string\n              enum:\n                - extension.uninstall\n            data:\n              type: object\n              description: Data payload for the extension uninstall event\n              properties:\n                clientId:\n                  type: string\n                  description: The client ID of the extension that was\
  \ uninstalled\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/asyncapi/squarespace-webhooks-asyncapi.yml
spec_file: asyncapi/squarespace-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/asyncapi/squarespace-webhooks-asyncapi.yml
tags:
- Commerce
- E-Commerce
- Marketing
- Payments
- Retail
- Website Builder
- Webhooks
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
