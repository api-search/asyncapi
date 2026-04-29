---
api_specs:
- filename: commercetools-http-api-openapi.yml
  format: yaml
  label: Commercetools HTTP API
  slug: http-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/commercetools/refs/heads/main/openapi/commercetools-http-api-openapi.yml
- filename: commercetools-import-api-openapi.yml
  format: yaml
  label: Commercetools Import API
  slug: import-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/commercetools/refs/heads/main/openapi/commercetools-import-api-openapi.yml
- filename: commercetools-change-history-api-openapi.yml
  format: yaml
  label: Commercetools Change History API
  slug: change-history-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/commercetools/refs/heads/main/openapi/commercetools-change-history-api-openapi.yml
channels:
- description: Delivered when a new order is created from a cart checkout. Contains the full order resource snapshot at the time of creation.
  name: orderCreated
  operation: publish
  operation_id: receiveOrderCreatedMessage
  summary: Order created notification
- description: Delivered when the order state transitions (e.g., from Open to Confirmed or Cancelled). Contains the new state and previous state values.
  name: orderStateChanged
  operation: publish
  operation_id: receiveOrderStateChangedMessage
  summary: Order state change notification
- description: Delivered when the shipment state of an order changes (e.g., from Pending to Shipped). Contains the new and previous shipment state values.
  name: orderShipmentStateChanged
  operation: publish
  operation_id: receiveOrderShipmentStateChangedMessage
  summary: Order shipment state change notification
- description: Delivered when the payment state of an order changes (e.g., from Pending to Paid). Contains the new and previous payment state values.
  name: orderPaymentStateChanged
  operation: publish
  operation_id: receiveOrderPaymentStateChangedMessage
  summary: Order payment state change notification
- description: Delivered when a new delivery is added to an order during fulfillment. Contains details of the delivery including items and parcel tracking.
  name: orderDeliveryAdded
  operation: publish
  operation_id: receiveOrderDeliveryAddedMessage
  summary: Order delivery added notification
- description: Delivered when a new customer account is created in the project. Contains the customer resource snapshot without the password hash.
  name: customerCreated
  operation: publish
  operation_id: receiveCustomerCreatedMessage
  summary: Customer created notification
- description: Delivered when a customer changes their password via the password reset or password change flow.
  name: customerPasswordChanged
  operation: publish
  operation_id: receiveCustomerPasswordChangedMessage
  summary: Customer password changed notification
- description: Delivered when a product is published, making staged changes visible in product projections. Contains the scope of the published data.
  name: productPublished
  operation: publish
  operation_id: receiveProductPublishedMessage
  summary: Product published notification
- description: Delivered when a product is unpublished, removing it from product projections in the storefront.
  name: productUnpublished
  operation: publish
  operation_id: receiveProductUnpublishedMessage
  summary: Product unpublished notification
- description: Delivered when the quantity of an inventory entry is explicitly set. Contains the old and new quantity values along with the supply channel.
  name: inventoryEntryQuantitySet
  operation: publish
  operation_id: receiveInventoryEntryQuantitySetMessage
  summary: Inventory quantity set notification
- description: Delivered when a new transaction is added to a payment resource. Contains the transaction details including type, amount, and state.
  name: paymentTransactionAdded
  operation: publish
  operation_id: receivePaymentTransactionAddedMessage
  summary: Payment transaction added notification
- description: Delivered for any resource create, update, or delete operation when a changes subscription is configured. The payload format follows the commercetools Change notification structure with resource type, action, and a list of changes.
  name: resourceChange
  operation: publish
  operation_id: receiveResourceChangeNotification
  summary: Generic resource change notification
description: 'The commercetools Subscriptions system delivers real-time change notifications and domain messages to external message queue destinations when resources are created, updated, or deleted within a Composable Commerce project. Subscriptions can deliver three payload types: Messages (predefined domain events such as OrderCreated or CustomerPasswordChanged), Changes (granular resource mutation records), and Events (BETA predefined event types). Supported destinations include AWS SQS, AWS SNS, AWS EventBridge, Azure Service Bus, Azure Event Grid, Google Cloud Pub/Sub, and Confluent Cloud. Payloads can be delivered in Platform format or CloudEvents format per subscription configuration.'
layout: asyncapi
messages:
- description: ''
  name: OrderCreatedMessage
  summary: Notification that a new order has been created.
  title: Order Created
- description: ''
  name: OrderStateChangedMessage
  summary: Notification that the state of an order has changed.
  title: Order State Changed
- description: ''
  name: OrderShipmentStateChangedMessage
  summary: Notification that the shipment state of an order has changed.
  title: Order Shipment State Changed
- description: ''
  name: OrderPaymentStateChangedMessage
  summary: Notification that the payment state of an order has changed.
  title: Order Payment State Changed
- description: ''
  name: OrderDeliveryAddedMessage
  summary: Notification that a delivery has been added to an order.
  title: Order Delivery Added
- description: ''
  name: CustomerCreatedMessage
  summary: Notification that a new customer account was created.
  title: Customer Created
- description: ''
  name: CustomerPasswordChangedMessage
  summary: Notification that a customer password was changed.
  title: Customer Password Changed
- description: ''
  name: ProductPublishedMessage
  summary: Notification that a product has been published.
  title: Product Published
- description: ''
  name: ProductUnpublishedMessage
  summary: Notification that a product has been unpublished.
  title: Product Unpublished
- description: ''
  name: InventoryEntryQuantitySetMessage
  summary: Notification that the quantity of an inventory entry was set.
  title: Inventory Entry Quantity Set
- description: ''
  name: PaymentTransactionAddedMessage
  summary: Notification that a transaction was added to a payment.
  title: Payment Transaction Added
- description: ''
  name: ChangeNotification
  summary: Notification that a resource was created, updated, or deleted.
  title: Resource Change Notification
name: commercetools Subscriptions Events
provider_name: commercetools
provider_slug: commercetools
servers:
- description: AWS Simple Queue Service destination for subscription messages.
  name: awsSqs
  protocol: https
  url: https://sqs.{region}.amazonaws.com/{account}/{queue}
- description: AWS Simple Notification Service destination for fan-out delivery.
  name: awsSns
  protocol: https
  url: arn:aws:sns:{region}:{account}:{topic}
- description: Google Cloud Pub/Sub destination for subscription messages.
  name: googlePubSub
  protocol: https
  url: https://pubsub.googleapis.com/v1/projects/{projectId}/topics/{topic}
- description: Azure Service Bus destination for subscription messages.
  name: azureServiceBus
  protocol: https
  url: https://{namespace}.servicebus.windows.net/{queue}
slug: commercetools-subscriptions-asyncapi
source_filename: commercetools-subscriptions-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: commercetools Subscriptions Events\n  description: >-\n    The commercetools Subscriptions system delivers real-time change notifications\n    and domain messages to external message queue destinations when resources are\n    created, updated, or deleted within a Composable Commerce project. Subscriptions\n    can deliver three payload types: Messages (predefined domain events such as\n    OrderCreated or CustomerPasswordChanged), Changes (granular resource mutation\n    records), and Events (BETA predefined event types). Supported destinations\n    include AWS SQS, AWS SNS, AWS EventBridge, Azure Service Bus, Azure Event Grid,\n    Google Cloud Pub/Sub, and Confluent Cloud. Payloads can be delivered in Platform\n    format or CloudEvents format per subscription configuration.\n  version: '1.0'\n  contact:\n    name: commercetools Support\n    url: https://support.commercetools.com\nexternalDocs:\n  description: commercetools Subscriptions Documentation\n\
  \  url: https://docs.commercetools.com/api/projects/subscriptions\nservers:\n  awsSqs:\n    url: 'https://sqs.{region}.amazonaws.com/{account}/{queue}'\n    protocol: https\n    description: AWS Simple Queue Service destination for subscription messages.\n    security:\n      - awsIam: []\n  awsSns:\n    url: 'arn:aws:sns:{region}:{account}:{topic}'\n    protocol: https\n    description: AWS Simple Notification Service destination for fan-out delivery.\n    security:\n      - awsIam: []\n  googlePubSub:\n    url: 'https://pubsub.googleapis.com/v1/projects/{projectId}/topics/{topic}'\n    protocol: https\n    description: Google Cloud Pub/Sub destination for subscription messages.\n    security:\n      - serviceAccountKey: []\n  azureServiceBus:\n    url: 'https://{namespace}.servicebus.windows.net/{queue}'\n    protocol: https\n    description: Azure Service Bus destination for subscription messages.\n    security:\n      - azureSharedAccessKey: []\nchannels:\n  orderCreated:\n    description:\
  \ >-\n      Delivered when a new order is created from a cart checkout. Contains the\n      full order resource snapshot at the time of creation.\n    publish:\n      operationId: receiveOrderCreatedMessage\n      summary: Order created notification\n      message:\n        $ref: '#/components/messages/OrderCreatedMessage'\n  orderStateChanged:\n    description: >-\n      Delivered when the order state transitions (e.g., from Open to Confirmed\n      or Cancelled). Contains the new state and previous state values.\n    publish:\n      operationId: receiveOrderStateChangedMessage\n      summary: Order state change notification\n      message:\n        $ref: '#/components/messages/OrderStateChangedMessage'\n  orderShipmentStateChanged:\n    description: >-\n      Delivered when the shipment state of an order changes (e.g., from Pending\n      to Shipped). Contains the new and previous shipment state values.\n    publish:\n      operationId: receiveOrderShipmentStateChangedMessage\n     \
  \ summary: Order shipment state change notification\n      message:\n        $ref: '#/components/messages/OrderShipmentStateChangedMessage'\n  orderPaymentStateChanged:\n    description: >-\n      Delivered when the payment state of an order changes (e.g., from Pending\n      to Paid). Contains the new and previous payment state values.\n    publish:\n      operationId: receiveOrderPaymentStateChangedMessage\n      summary: Order payment state change notification\n      message:\n        $ref: '#/components/messages/OrderPaymentStateChangedMessage'\n  orderDeliveryAdded:\n    description: >-\n      Delivered when a new delivery is added to an order during fulfillment.\n      Contains details of the delivery including items and parcel tracking.\n    publish:\n      operationId: receiveOrderDeliveryAddedMessage\n      summary: Order delivery added notification\n      message:\n        $ref: '#/components/messages/OrderDeliveryAddedMessage'\n  customerCreated:\n    description: >-\n     \
  \ Delivered when a new customer account is created in the project. Contains\n      the customer resource snapshot without the password hash.\n    publish:\n      operationId: receiveCustomerCreatedMessage\n      summary: Customer created notification\n      message:\n        $ref: '#/components/messages/CustomerCreatedMessage'\n  customerPasswordChanged:\n    description: >-\n      Delivered when a customer changes their password via the password reset\n      or password change flow.\n    publish:\n      operationId: receiveCustomerPasswordChangedMessage\n      summary: Customer password changed notification\n      message:\n        $ref: '#/components/messages/CustomerPasswordChangedMessage'\n  productPublished:\n    description: >-\n      Delivered when a product is published, making staged changes visible in\n      product projections. Contains the scope of the published data.\n    publish:\n      operationId: receiveProductPublishedMessage\n      summary: Product published notification\n\
  \      message:\n        $ref: '#/components/messages/ProductPublishedMessage'\n  productUnpublished:\n    description: >-\n      Delivered when a product is unpublished, removing it from product\n      projections in the storefront.\n    publish:\n      operationId: receiveProductUnpublishedMessage\n      summary: Product unpublished notification\n      message:\n        $ref: '#/components/messages/ProductUnpublishedMessage'\n  inventoryEntryQuantitySet:\n    description: >-\n      Delivered when the quantity of an inventory entry is explicitly set.\n      Contains the old and new quantity values along with the supply channel.\n    publish:\n      operationId: receiveInventoryEntryQuantitySetMessage\n      summary: Inventory quantity set notification\n      message:\n        $ref: '#/components/messages/InventoryEntryQuantitySetMessage'\n  paymentTransactionAdded:\n    description: >-\n      Delivered when a new transaction is added to a payment resource. Contains\n      the transaction\
  \ details including type, amount, and state.\n    publish:\n      operationId: receivePaymentTransactionAddedMessage\n      summary: Payment transaction added notification\n      message:\n        $ref: '#/components/messages/PaymentTransactionAddedMessage'\n  resourceChange:\n    description: >-\n      Delivered for any resource create, update, or delete operation when a\n      changes subscription is configured. The payload format follows the\n      commercetools Change notification structure with resource type, action,\n      and a list of changes.\n    publish:\n      operationId: receiveResourceChangeNotification\n      summary: Generic resource change notification\n      message:\n        $ref: '#/components/messages/ChangeNotification'\ncomponents:\n  securitySchemes:\n    awsIam:\n      type: httpApiKey\n      in: header\n      name: Authorization\n      description: AWS IAM-based authentication using STS-issued credentials or access keys.\n    serviceAccountKey:\n      type: httpApiKey\n\
  \      in: header\n      name: Authorization\n      description: Google Cloud service account key with Pub/Sub Publisher role.\n    azureSharedAccessKey:\n      type: httpApiKey\n      in: header\n      name: Authorization\n      description: Azure Shared Access Signature or connection string authentication.\n  messages:\n    OrderCreatedMessage:\n      name: OrderCreatedMessage\n      title: Order Created\n      summary: Notification that a new order has been created.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderCreatedPayload'\n    OrderStateChangedMessage:\n      name: OrderStateChangedMessage\n      title: Order State Changed\n      summary: Notification that the state of an order has changed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderStateChangedPayload'\n    OrderShipmentStateChangedMessage:\n      name: OrderShipmentStateChangedMessage\n      title: Order Shipment State Changed\n\
  \      summary: Notification that the shipment state of an order has changed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderShipmentStateChangedPayload'\n    OrderPaymentStateChangedMessage:\n      name: OrderPaymentStateChangedMessage\n      title: Order Payment State Changed\n      summary: Notification that the payment state of an order has changed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderPaymentStateChangedPayload'\n    OrderDeliveryAddedMessage:\n      name: OrderDeliveryAddedMessage\n      title: Order Delivery Added\n      summary: Notification that a delivery has been added to an order.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderDeliveryAddedPayload'\n    CustomerCreatedMessage:\n      name: CustomerCreatedMessage\n      title: Customer Created\n      summary: Notification that a new customer account was created.\n      contentType:\
  \ application/json\n      payload:\n        $ref: '#/components/schemas/CustomerCreatedPayload'\n    CustomerPasswordChangedMessage:\n      name: CustomerPasswordChangedMessage\n      title: Customer Password Changed\n      summary: Notification that a customer password was changed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CustomerPasswordChangedPayload'\n    ProductPublishedMessage:\n      name: ProductPublishedMessage\n      title: Product Published\n      summary: Notification that a product has been published.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ProductPublishedPayload'\n    ProductUnpublishedMessage:\n      name: ProductUnpublishedMessage\n      title: Product Unpublished\n      summary: Notification that a product has been unpublished.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ProductUnpublishedPayload'\n    InventoryEntryQuantitySetMessage:\n\
  \      name: InventoryEntryQuantitySetMessage\n      title: Inventory Entry Quantity Set\n      summary: Notification that the quantity of an inventory entry was set.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/InventoryEntryQuantitySetPayload'\n    PaymentTransactionAddedMessage:\n      name: PaymentTransactionAddedMessage\n      title: Payment Transaction Added\n      summary: Notification that a transaction was added to a payment.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentTransactionAddedPayload'\n    ChangeNotification:\n      name: ChangeNotification\n      title: Resource Change Notification\n      summary: Notification that a resource was created, updated, or deleted.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ChangeNotificationPayload'\n  schemas:\n    MessageBase:\n      type: object\n      description: Common fields shared by all\
  \ commercetools message notification payloads.\n      required:\n        - id\n        - version\n        - sequenceNumber\n        - resource\n        - resourceVersion\n        - type\n        - createdAt\n      properties:\n        id:\n          type: string\n          description: System-generated unique identifier for the message.\n        version:\n          type: integer\n          description: Version number of the message.\n        sequenceNumber:\n          type: integer\n          description: Monotonically increasing sequence number within the resource.\n        resource:\n          $ref: '#/components/schemas/Reference'\n        resourceVersion:\n          type: integer\n          description: Version of the resource when the message was generated.\n        type:\n          type: string\n          description: Message type discriminator string (e.g., \"OrderCreated\").\n        resourceUserProvidedIdentifiers:\n          type: object\n          description: User-defined identifiers\
  \ of the resource (key, orderNumber, etc.).\n        createdAt:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp when the message was created.\n        createdBy:\n          $ref: '#/components/schemas/LastModifiedBy'\n        lastModifiedAt:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp when the message was last modified.\n        lastModifiedBy:\n          $ref: '#/components/schemas/LastModifiedBy'\n    Reference:\n      type: object\n      description: A reference to a commercetools resource by typeId and id.\n      required:\n        - typeId\n        - id\n      properties:\n        typeId:\n          type: string\n          description: The type identifier of the referenced resource.\n        id:\n          type: string\n          description: The unique identifier of the referenced resource.\n    LastModifiedBy:\n      type: object\n      description: Information about the actor who\
  \ triggered the event.\n      properties:\n        clientId:\n          type: string\n          description: ID of the API client that triggered the event.\n        externalUserId:\n          type: string\n          description: External user ID if set on the API client.\n        customer:\n          $ref: '#/components/schemas/Reference'\n        anonymousId:\n          type: string\n          description: Anonymous session ID if triggered without customer login.\n    OrderCreatedPayload:\n      allOf:\n        - $ref: '#/components/schemas/MessageBase'\n        - type: object\n          description: Payload for the OrderCreated message type.\n          required:\n            - order\n          properties:\n            type:\n              type: string\n              enum: [OrderCreated]\n              description: Message type discriminator.\n            order:\n              type: object\n              description: The full Order resource at the time of creation.\n    OrderStateChangedPayload:\n\
  \      allOf:\n        - $ref: '#/components/schemas/MessageBase'\n        - type: object\n          description: Payload for the OrderStateChanged message type.\n          required:\n            - orderState\n            - oldOrderState\n          properties:\n            type:\n              type: string\n              enum: [OrderStateChanged]\n              description: Message type discriminator.\n            orderState:\n              type: string\n              enum: [Open, Confirmed, Complete, Cancelled]\n              description: The new order state after the change.\n            oldOrderState:\n              type: string\n              enum: [Open, Confirmed, Complete, Cancelled]\n              description: The order state before the change.\n    OrderShipmentStateChangedPayload:\n      allOf:\n        - $ref: '#/components/schemas/MessageBase'\n        - type: object\n          description: Payload for the OrderShipmentStateChanged message type.\n          required:\n     \
  \       - shipmentState\n          properties:\n            type:\n              type: string\n              enum: [OrderShipmentStateChanged]\n              description: Message type discriminator.\n            shipmentState:\n              type: string\n              enum: [Shipped, Ready, Pending, Delayed, Partial, Backorder]\n              description: The new shipment state.\n            oldShipmentState:\n              type: string\n              enum: [Shipped, Ready, Pending, Delayed, Partial, Backorder]\n              description: The previous shipment state.\n    OrderPaymentStateChangedPayload:\n      allOf:\n        - $ref: '#/components/schemas/MessageBase'\n        - type: object\n          description: Payload for the OrderPaymentStateChanged message type.\n          required:\n            - paymentState\n          properties:\n            type:\n              type: string\n              enum: [OrderPaymentStateChanged]\n              description: Message type discriminator.\n\
  \            paymentState:\n              type: string\n              enum: [Paid, Pending, Failed, CreditOwed, BalanceDue]\n              description: The new payment state.\n            oldPaymentState:\n              type: string\n              enum: [Paid, Pending, Failed, CreditOwed, BalanceDue]\n              description: The previous payment state.\n    OrderDeliveryAddedPayload:\n      allOf:\n        - $ref: '#/components/schemas/MessageBase'\n        - type: object\n          description: Payload for the DeliveryAdded message type.\n          required:\n            - delivery\n          properties:\n            type:\n              type: string\n              enum: [DeliveryAdded]\n              description: Message type discriminator.\n            delivery:\n              type: object\n              description: The delivery object that was added including items, parcels, and address.\n            shippingKey:\n              type: string\n              description: Key of the\
  \ shipping method in multi-shipping mode orders.\n    CustomerCreatedPayload:\n      allOf:\n        - $ref: '#/components/schemas/MessageBase'\n        - type: object\n          description: Payload for the CustomerCreated message type.\n          required:\n            - customer\n          properties:\n            type:\n              type: string\n              enum: [CustomerCreated]\n              description: Message type discriminator.\n            customer:\n              type: object\n              description: The Customer resource at the time of creation (password hash excluded).\n    CustomerPasswordChangedPayload:\n      allOf:\n        - $ref: '#/components/schemas/MessageBase'\n        - type: object\n          description: Payload for the CustomerPasswordChanged message type.\n          properties:\n            type:\n              type: string\n              enum: [CustomerPasswordChanged]\n              description: Message type discriminator.\n    ProductPublishedPayload:\n\
  \      allOf:\n        - $ref: '#/components/schemas/MessageBase'\n        - type: object\n          description: Payload for the ProductPublished message type.\n          required:\n            - scope\n          properties:\n            type:\n              type: string\n              enum: [ProductPublished]\n              description: Message type discriminator.\n            scope:\n              type: string\n              enum: [All, Prices]\n              description: The scope of product data that was published.\n            removedImageUrls:\n              type: array\n              items:\n                type: string\n              description: URLs of images removed during the publish operation.\n    ProductUnpublishedPayload:\n      allOf:\n        - $ref: '#/components/schemas/MessageBase'\n        - type: object\n          description: Payload for the ProductUnpublished message type.\n          properties:\n            type:\n              type: string\n              enum:\
  \ [ProductUnpublished]\n              description: Message type discriminator.\n    InventoryEntryQuantitySetPayload:\n      allOf:\n        - $ref: '#/components/schemas/MessageBase'\n        - type: object\n          description: Payload for the InventoryEntryQuantitySet message type.\n          required:\n            - oldQuantityOnStock\n            - newQuantityOnStock\n            - oldAvailableQuantity\n            - newAvailableQuantity\n          properties:\n            type:\n              type: string\n              enum: [InventoryEntryQuantitySet]\n              description: Message type discriminator.\n            oldQuantityOnStock:\n              type: integer\n              description: The previous quantity on stock value.\n            newQuantityOnStock:\n              type: integer\n              description: The new quantity on stock value.\n            oldAvailableQuantity:\n              type: integer\n              description: The previous available quantity value.\n\
  \            newAvailableQuantity:\n              type: integer\n              description: The new available quantity value.\n            supplyChannel:\n              $ref: '#/components/schemas/Reference'\n    PaymentTransactionAddedPayload:\n      allOf:\n        - $ref: '#/components/schemas/MessageBase'\n        - type: object\n          description: Payload for the PaymentTransactionAdded message type.\n          required:\n            - transaction\n          properties:\n            type:\n              type: string\n              enum: [PaymentTransactionAdded]\n              description: Message type discriminator.\n            transaction:\n              type: object\n              description: >-\n                The transaction that was added, including type (Authorization,\n                Charge, Refund, etc.), amount, and state.\n    ChangeNotificationPayload:\n      type: object\n      description: >-\n        A change notification payload delivered when a resource is\
  \ created,\n        updated, or deleted. Contains the resource reference, change type,\n        and a list of changes that occurred.\n      required:\n        - notificationType\n        - projectKey\n        - resource\n        - resourceUserProvidedIdentifiers\n        - version\n        - oldVersion\n        - modifiedAt\n      properties:\n        notificationType:\n          type: string\n          enum: [ResourceCreated, ResourceUpdated, ResourceDeleted]\n          description: The type of modification that triggered the notification.\n        projectKey:\n          type: string\n          description: Key of the project where the change occurred.\n        resource:\n          $ref: '#/components/schemas/Reference'\n        resourceUserProvidedIdentifiers:\n          type: object\n          description: User-defined identifiers of the changed resource.\n        version:\n          type: integer\n          description: New version of the resource after the change.\n        oldVersion:\n\
  \          type: integer\n          description: Previous version of the resource before the change.\n        modifiedAt:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp when the change was made.\n        changes:\n          type: array\n          items:\n            type: object\n          description: List of field-level changes that occurred in this operation.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/commercetools/refs/heads/main/asyncapi/commercetools-subscriptions-asyncapi.yml
spec_file: asyncapi/commercetools-subscriptions-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/commercetools/refs/heads/main/asyncapi/commercetools-subscriptions-asyncapi.yml
tags:
- Commerce
- Composable Commerce
- E-Commerce
- GraphQL
- REST
- SDK
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
