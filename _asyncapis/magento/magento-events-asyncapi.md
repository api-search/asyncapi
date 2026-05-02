---
api_specs:
- filename: magento-rest-api-openapi.yml
  format: yaml
  label: Magento REST API
  slug: rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/magento/refs/heads/main/openapi/magento-rest-api-openapi.yml
- filename: magento-webhooks-asyncapi.yml
  format: yaml
  label: Adobe Commerce Webhooks
  slug: webhooks
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/magento/refs/heads/main/asyncapi/magento-webhooks-asyncapi.yml
- filename: magento-events-asyncapi.yml
  format: yaml
  label: Adobe Commerce Eventing
  slug: events
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/magento/refs/heads/main/asyncapi/magento-events-asyncapi.yml
channels:
- description: Emitted after a new sales order is successfully placed. Published to Adobe I/O Events and routed to all subscribed App Builder applications. Use this event to trigger order processing workflows, notify fulfilment systems, or update external ERP records.
  name: com.adobe.commerce.observer.sales_order_place_after
  operation: subscribe
  operation_id: consumeOrderPlaced
  summary: Order placed event
- description: Emitted after any committed save of an order record. Covers status changes, invoice creation, shipment creation, and admin edits. Use this event to maintain real-time order status synchronization in external systems.
  name: com.adobe.commerce.observer.sales_order_save_commit_after
  operation: subscribe
  operation_id: consumeOrderSaved
  summary: Order saved event
- description: Emitted when a new customer successfully registers an account in the storefront. Published to Adobe I/O Events for downstream CRM, marketing automation, or loyalty program integrations.
  name: com.adobe.commerce.observer.customer_register_success
  operation: subscribe
  operation_id: consumeCustomerRegistered
  summary: Customer registered event
- description: Emitted after a customer account is created or updated. Covers both admin-initiated profile changes and customer self-service updates. Use this to synchronize customer data with external CRM systems.
  name: com.adobe.commerce.observer.customer_save_after_data_object
  operation: subscribe
  operation_id: consumeCustomerSaved
  summary: Customer saved event
- description: Emitted after a product record is saved in the catalog. Covers new product creation and updates to existing products. Use this to propagate catalog changes to external PIM, search, or marketplace systems.
  name: com.adobe.commerce.observer.catalog_product_save_after
  operation: subscribe
  operation_id: consumeProductSaved
  summary: Product saved event
- description: Emitted after a product is permanently deleted from the catalog. Use this to remove the product from external search indexes, PIM systems, or marketplace listings.
  name: com.adobe.commerce.observer.catalog_product_delete_after_done
  operation: subscribe
  operation_id: consumeProductDeleted
  summary: Product deleted event
- description: Emitted after the checkout process completes and an order has been submitted. This event fires after the order is fully placed including payment authorization. Use for post-checkout analytics and campaign triggers.
  name: com.adobe.commerce.observer.checkout_submit_all_after
  operation: subscribe
  operation_id: consumeCheckoutComplete
  summary: Checkout completed event
- description: Emitted after a credit memo (refund) is created for an order. Use this event to trigger refund processing in accounting systems, loyalty point deductions, or customer service platforms.
  name: com.adobe.commerce.observer.sales_order_creditmemo_save_after
  operation: subscribe
  operation_id: consumeCreditMemoSaved
  summary: Credit memo created event
description: Adobe Commerce Eventing provides an asynchronous event-driven integration framework that publishes Commerce business events to Adobe I/O Events, enabling App Builder applications and other Adobe Experience Cloud services to subscribe and react to store activity. Events are transmitted over the Adobe I/O Events pub/sub infrastructure and delivered to registered consumer applications via HTTPS webhook delivery or journal polling. Supported event types cover the full commerce lifecycle including order placement, customer registration, product updates, inventory changes, and payment processing. Events are configured by subscribing to specific Commerce observer or plugin events in the event_subscriptions.xml configuration file or via the Commerce Admin. Each event carries a structured JSON payload with the fields defined in the subscription configuration, keeping data transfer lean and targeted.
layout: asyncapi
messages:
- description: ''
  name: OrderPlaced
  summary: Event published when a new Commerce order is placed.
  title: Order Placed
- description: ''
  name: OrderSaved
  summary: Event published when a Commerce order is updated.
  title: Order Saved
- description: ''
  name: CustomerRegistered
  summary: Event published when a new customer account is created.
  title: Customer Registered
- description: ''
  name: CustomerSaved
  summary: Event published when a customer account is created or updated.
  title: Customer Saved
- description: ''
  name: ProductSaved
  summary: Event published when a catalog product is created or updated.
  title: Product Saved
- description: ''
  name: ProductDeleted
  summary: Event published when a catalog product is deleted.
  title: Product Deleted
- description: ''
  name: CheckoutComplete
  summary: Event published when a customer completes checkout.
  title: Checkout Completed
- description: ''
  name: CreditMemoSaved
  summary: Event published when a refund credit memo is created for an order.
  title: Credit Memo Created
name: Adobe Commerce Eventing
provider_name: magento
provider_slug: magento
servers:
- description: Adobe I/O Events ingress endpoint. Commerce publishes events here; consumer applications receive them via registered I/O Events webhooks or the journal polling API at https://api.adobe.io/events/organizations/{org}/integrations/{cred}/journal.
  name: adobeIOEvents
  protocol: https
  url: https://eventsingress.adobe.io
slug: magento-events-asyncapi
source_filename: magento-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Adobe Commerce Eventing\n  description: >-\n    Adobe Commerce Eventing provides an asynchronous event-driven integration\n    framework that publishes Commerce business events to Adobe I/O Events,\n    enabling App Builder applications and other Adobe Experience Cloud services\n    to subscribe and react to store activity. Events are transmitted over the\n    Adobe I/O Events pub/sub infrastructure and delivered to registered consumer\n    applications via HTTPS webhook delivery or journal polling. Supported event\n    types cover the full commerce lifecycle including order placement, customer\n    registration, product updates, inventory changes, and payment processing.\n    Events are configured by subscribing to specific Commerce observer or plugin\n    events in the event_subscriptions.xml configuration file or via the Commerce\n    Admin. Each event carries a structured JSON payload with the fields defined\n    in the subscription configuration,\
  \ keeping data transfer lean and targeted.\n  version: '1.0'\n  contact:\n    name: Adobe Commerce Developer Support\n    url: https://developer.adobe.com/commerce/extensibility/events/\nexternalDocs:\n  description: Adobe I/O Events for Adobe Commerce Documentation\n  url: https://developer.adobe.com/commerce/extensibility/events/\nservers:\n  adobeIOEvents:\n    url: 'https://eventsingress.adobe.io'\n    protocol: https\n    description: >-\n      Adobe I/O Events ingress endpoint. Commerce publishes events here;\n      consumer applications receive them via registered I/O Events webhooks\n      or the journal polling API at https://api.adobe.io/events/organizations/{org}/integrations/{cred}/journal.\n    security:\n      - imsOAuth: []\nchannels:\n  com.adobe.commerce.observer.sales_order_place_after:\n    description: >-\n      Emitted after a new sales order is successfully placed. Published to\n      Adobe I/O Events and routed to all subscribed App Builder applications.\n      Use\
  \ this event to trigger order processing workflows, notify fulfilment\n      systems, or update external ERP records.\n    subscribe:\n      operationId: consumeOrderPlaced\n      summary: Order placed event\n      description: >-\n        Consumed by App Builder applications subscribed to the\n        com.adobe.commerce.observer.sales_order_place_after event type.\n        The payload includes order metadata and the configured subset of\n        order fields defined in the event subscription.\n      message:\n        $ref: '#/components/messages/OrderPlaced'\n\n  com.adobe.commerce.observer.sales_order_save_commit_after:\n    description: >-\n      Emitted after any committed save of an order record. Covers status\n      changes, invoice creation, shipment creation, and admin edits. Use\n      this event to maintain real-time order status synchronization in\n      external systems.\n    subscribe:\n      operationId: consumeOrderSaved\n      summary: Order saved event\n      description:\
  \ >-\n        Consumed by App Builder applications subscribed to order save events.\n        Fires on any commit of an order record change, providing the current\n        state of the order including its updated status and totals.\n      message:\n        $ref: '#/components/messages/OrderSaved'\n\n  com.adobe.commerce.observer.customer_register_success:\n    description: >-\n      Emitted when a new customer successfully registers an account in the\n      storefront. Published to Adobe I/O Events for downstream CRM, marketing\n      automation, or loyalty program integrations.\n    subscribe:\n      operationId: consumeCustomerRegistered\n      summary: Customer registered event\n      description: >-\n        Consumed by App Builder applications handling new customer onboarding.\n        The payload includes the new customer account details as configured\n        in the event subscription fields.\n      message:\n        $ref: '#/components/messages/CustomerRegistered'\n\n  com.adobe.commerce.observer.customer_save_after_data_object:\n\
  \    description: >-\n      Emitted after a customer account is created or updated. Covers both\n      admin-initiated profile changes and customer self-service updates.\n      Use this to synchronize customer data with external CRM systems.\n    subscribe:\n      operationId: consumeCustomerSaved\n      summary: Customer saved event\n      description: >-\n        Consumed by App Builder applications that synchronize customer profile\n        data. The payload includes the customer data object with the fields\n        configured in the subscription, enabling detection of which data changed.\n      message:\n        $ref: '#/components/messages/CustomerSaved'\n\n  com.adobe.commerce.observer.catalog_product_save_after:\n    description: >-\n      Emitted after a product record is saved in the catalog. Covers new\n      product creation and updates to existing products. Use this to propagate\n      catalog changes to external PIM, search, or marketplace systems.\n    subscribe:\n      operationId:\
  \ consumeProductSaved\n      summary: Product saved event\n      description: >-\n        Consumed by App Builder applications that maintain product catalog\n        synchronization with external systems. The payload includes product\n        attribute data as configured in the event subscription fields.\n      message:\n        $ref: '#/components/messages/ProductSaved'\n\n  com.adobe.commerce.observer.catalog_product_delete_after_done:\n    description: >-\n      Emitted after a product is permanently deleted from the catalog. Use this\n      to remove the product from external search indexes, PIM systems, or\n      marketplace listings.\n    subscribe:\n      operationId: consumeProductDeleted\n      summary: Product deleted event\n      description: >-\n        Consumed by App Builder applications that need to react to catalog\n        product removal. The payload includes the deleted product's entity ID\n        and SKU for external record lookup and deletion.\n      message:\n  \
  \      $ref: '#/components/messages/ProductDeleted'\n\n  com.adobe.commerce.observer.checkout_submit_all_after:\n    description: >-\n      Emitted after the checkout process completes and an order has been\n      submitted. This event fires after the order is fully placed including\n      payment authorization. Use for post-checkout analytics and campaign\n      triggers.\n    subscribe:\n      operationId: consumeCheckoutComplete\n      summary: Checkout completed event\n      description: >-\n        Consumed by App Builder applications handling post-checkout workflows\n        such as abandonment recovery reset, loyalty point awards, or\n        personalization updates.\n      message:\n        $ref: '#/components/messages/CheckoutComplete'\n\n  com.adobe.commerce.observer.sales_order_creditmemo_save_after:\n    description: >-\n      Emitted after a credit memo (refund) is created for an order. Use this\n      event to trigger refund processing in accounting systems, loyalty point\n\
  \      deductions, or customer service platforms.\n    subscribe:\n      operationId: consumeCreditMemoSaved\n      summary: Credit memo created event\n      description: >-\n        Consumed by App Builder applications that handle refund and return\n        workflows. The payload includes the credit memo with the refunded\n        items and amounts.\n      message:\n        $ref: '#/components/messages/CreditMemoSaved'\n\ncomponents:\n  securitySchemes:\n    imsOAuth:\n      type: oauth2\n      description: >-\n        Adobe Identity Management System (IMS) OAuth 2.0. Consumer applications\n        authenticate with Adobe I/O using a service account (JWT) or OAuth\n        server-to-server credential to receive events from the journal or\n        via registered webhook delivery.\n      flows:\n        clientCredentials:\n          tokenUrl: https://ims-na1.adobelogin.com/ims/token\n          scopes:\n            aio_api_management: Manage Adobe I/O event subscriptions\n\n  messages:\n\
  \    OrderPlaced:\n      name: OrderPlaced\n      title: Order Placed\n      summary: Event published when a new Commerce order is placed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CommerceEventEnvelope'\n      examples:\n        - name: OrderPlacedExample\n          payload:\n            specversion: '1.0'\n            type: com.adobe.commerce.observer.sales_order_place_after\n            source: urn:uuid:commerceInstanceId\n            id: abc123-def456\n            time: '2026-03-21T10:00:00Z'\n            datacontenttype: application/json\n            data:\n              uid: abc123-def456\n              event:\n                order:\n                  entity_id: 1001\n                  increment_id: '000001001'\n                  status: pending\n                  customer_email: customer@example.com\n                  grand_total: '99.95'\n\n    OrderSaved:\n      name: OrderSaved\n      title: Order Saved\n      summary: Event published\
  \ when a Commerce order is updated.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CommerceEventEnvelope'\n\n    CustomerRegistered:\n      name: CustomerRegistered\n      title: Customer Registered\n      summary: Event published when a new customer account is created.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CommerceEventEnvelope'\n\n    CustomerSaved:\n      name: CustomerSaved\n      title: Customer Saved\n      summary: Event published when a customer account is created or updated.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CommerceEventEnvelope'\n\n    ProductSaved:\n      name: ProductSaved\n      title: Product Saved\n      summary: Event published when a catalog product is created or updated.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CommerceEventEnvelope'\n\n    ProductDeleted:\n      name: ProductDeleted\n\
  \      title: Product Deleted\n      summary: Event published when a catalog product is deleted.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CommerceEventEnvelope'\n\n    CheckoutComplete:\n      name: CheckoutComplete\n      title: Checkout Completed\n      summary: Event published when a customer completes checkout.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CommerceEventEnvelope'\n\n    CreditMemoSaved:\n      name: CreditMemoSaved\n      title: Credit Memo Created\n      summary: Event published when a refund credit memo is created for an order.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CommerceEventEnvelope'\n\n  schemas:\n    CommerceEventEnvelope:\n      type: object\n      description: >-\n        CloudEvents 1.0 compliant envelope wrapping all Adobe Commerce I/O Events\n        payloads. Adobe I/O Events uses the CloudEvents specification\
  \ for all\n        event metadata.\n      required:\n        - specversion\n        - type\n        - source\n        - id\n        - time\n        - data\n      properties:\n        specversion:\n          type: string\n          description: CloudEvents specification version. Always \"1.0\".\n          const: '1.0'\n        type:\n          type: string\n          description: >-\n            The fully qualified event type name. For Commerce events, follows\n            the pattern com.adobe.commerce.{observer|plugin}.{event_name}.\n          example: com.adobe.commerce.observer.sales_order_place_after\n        source:\n          type: string\n          description: >-\n            URN identifying the Commerce instance that produced the event.\n            Format: urn:uuid:{commerce_instance_id}.\n          format: uri\n        id:\n          type: string\n          description: Unique identifier for this specific event occurrence.\n          format: uuid\n        time:\n          type:\
  \ string\n          format: date-time\n          description: ISO 8601 timestamp when the event was produced.\n        datacontenttype:\n          type: string\n          description: MIME type of the data field content.\n          const: application/json\n        subject:\n          type: string\n          description: Optional subject providing additional context about the event source entity.\n        data:\n          $ref: '#/components/schemas/CommerceEventData'\n\n    CommerceEventData:\n      type: object\n      description: >-\n        The inner data object of a Commerce I/O Event. Contains event metadata\n        and the nested event payload with the Commerce entity data.\n      properties:\n        uid:\n          type: string\n          description: Unique identifier for this event delivery instance.\n        timestamp:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp of the event.\n        merchant_id:\n          type: string\n\
  \          description: Adobe Commerce merchant identifier string.\n        environment_id:\n          type: string\n          description: Commerce environment identifier (production, staging, etc.).\n        event:\n          type: object\n          description: >-\n            The event-specific payload object. The shape of this object depends\n            on which fields were configured in the Commerce event subscription.\n            Common top-level keys are the entity type (e.g. order, customer, product).\n          additionalProperties: true\n\n    OrderEventData:\n      type: object\n      description: Order data fields commonly included in order event payloads.\n      properties:\n        entity_id:\n          type: integer\n          description: Numeric order entity ID.\n        increment_id:\n          type: string\n          description: Human-readable order number.\n        status:\n          type: string\n          description: Current order status code.\n        state:\n\
  \          type: string\n          description: Internal order state.\n        customer_id:\n          type: integer\n          description: Numeric customer entity ID.\n        customer_email:\n          type: string\n          format: email\n          description: Customer email address.\n        grand_total:\n          type: string\n          description: Order grand total as a decimal string.\n        created_at:\n          type: string\n          format: date-time\n          description: ISO 8601 order creation timestamp.\n\n    CustomerEventData:\n      type: object\n      description: Customer data fields commonly included in customer event payloads.\n      properties:\n        entity_id:\n          type: integer\n          description: Numeric customer entity ID.\n        email:\n          type: string\n          format: email\n          description: Customer email address.\n        firstname:\n          type: string\n          description: Customer first name.\n        lastname:\n\
  \          type: string\n          description: Customer last name.\n        group_id:\n          type: integer\n          description: Customer group ID.\n        store_id:\n          type: integer\n          description: Store view ID.\n        website_id:\n          type: integer\n          description: Website ID.\n        created_at:\n          type: string\n          format: date-time\n          description: Account creation timestamp.\n\n    ProductEventData:\n      type: object\n      description: Product data fields commonly included in product event payloads.\n      properties:\n        entity_id:\n          type: integer\n          description: Numeric product entity ID.\n        sku:\n          type: string\n          description: Product SKU.\n        name:\n          type: string\n          description: Product display name.\n        type_id:\n          type: string\n          description: Product type.\n        status:\n          type: integer\n          description: Product\
  \ status. 1 = enabled, 2 = disabled.\n          enum: [1, 2]\n        price:\n          type: number\n          description: Product base price.\n        updated_at:\n          type: string\n          format: date-time\n          description: Last update timestamp.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/magento/refs/heads/main/asyncapi/magento-events-asyncapi.yml
spec_file: asyncapi/magento-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/magento/refs/heads/main/asyncapi/magento-events-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
