---
channels:
- description: Published when a new customer account is created in the BSS system.
  name: customer/created
  operation: subscribe
  operation_id: onCustomerCreated
  summary: Customer account created
- description: Published when a customer account is modified.
  name: customer/updated
  operation: subscribe
  operation_id: onCustomerUpdated
  summary: Customer account updated
- description: Published when a service subscription becomes active.
  name: subscription/activated
  operation: subscribe
  operation_id: onSubscriptionActivated
  summary: Subscription activated
- description: Published when a service subscription is suspended.
  name: subscription/suspended
  operation: subscribe
  operation_id: onSubscriptionSuspended
  summary: Subscription suspended
- description: Published when a service subscription is cancelled.
  name: subscription/cancelled
  operation: subscribe
  operation_id: onSubscriptionCancelled
  summary: Subscription cancelled
- description: Published when a new invoice is generated for a customer.
  name: billing/invoice/created
  operation: subscribe
  operation_id: onInvoiceCreated
  summary: Invoice created
- description: Published when a payment is received against an invoice.
  name: billing/payment/received
  operation: subscribe
  operation_id: onPaymentReceived
  summary: Payment received
description: The Amdocs connectX BSS Event API delivers real-time event notifications for telecom BSS operations including customer lifecycle events, subscription changes, billing events, and provisioning status updates via webhooks and message queues.
layout: asyncapi
messages:
- description: ''
  name: CustomerCreatedEvent
  summary: Notification that a new customer account was created
  title: Customer Created
- description: ''
  name: CustomerUpdatedEvent
  summary: Notification that a customer account was modified
  title: Customer Updated
- description: ''
  name: SubscriptionEvent
  summary: Notification that a subscription status changed
  title: Subscription Status Changed
- description: ''
  name: InvoiceEvent
  summary: Notification that an invoice was generated
  title: Invoice Created
- description: ''
  name: PaymentEvent
  summary: Notification that a payment was recorded
  title: Payment Received
name: Amdocs connectX BSS Event API
provider_name: Amdocs
provider_slug: amdocs
servers:
- description: Amdocs BSS Production WebSocket event stream
  name: production
  protocol: wss
  url: wss://events.amdocs-dbs.com
slug: amdocs-events-asyncapi
source_filename: amdocs-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Amdocs connectX BSS Event API\n  description: >-\n    The Amdocs connectX BSS Event API delivers real-time event notifications for\n    telecom BSS operations including customer lifecycle events, subscription changes,\n    billing events, and provisioning status updates via webhooks and message queues.\n  version: 1.0.0\n  contact:\n    name: Amdocs Developer Portal\n    url: https://devportal.amdocs-dbs.com/\n\nservers:\n  production:\n    url: wss://events.amdocs-dbs.com\n    protocol: wss\n    description: Amdocs BSS Production WebSocket event stream\n\nchannels:\n  customer/created:\n    description: Published when a new customer account is created in the BSS system.\n    subscribe:\n      operationId: onCustomerCreated\n      summary: Customer account created\n      description: Receive notifications when a new customer is onboarded into the BSS.\n      tags:\n        - name: Customers\n      message:\n        $ref: '#/components/messages/CustomerCreatedEvent'\n\
  \n  customer/updated:\n    description: Published when a customer account is modified.\n    subscribe:\n      operationId: onCustomerUpdated\n      summary: Customer account updated\n      description: Receive notifications when customer account data changes including status transitions.\n      tags:\n        - name: Customers\n      message:\n        $ref: '#/components/messages/CustomerUpdatedEvent'\n\n  subscription/activated:\n    description: Published when a service subscription becomes active.\n    subscribe:\n      operationId: onSubscriptionActivated\n      summary: Subscription activated\n      description: Receive notifications when a service subscription transitions to Active status.\n      tags:\n        - name: Subscriptions\n      message:\n        $ref: '#/components/messages/SubscriptionEvent'\n\n  subscription/suspended:\n    description: Published when a service subscription is suspended.\n    subscribe:\n      operationId: onSubscriptionSuspended\n      summary: Subscription\
  \ suspended\n      description: Receive notifications when a service subscription is suspended (e.g., for non-payment).\n      tags:\n        - name: Subscriptions\n      message:\n        $ref: '#/components/messages/SubscriptionEvent'\n\n  subscription/cancelled:\n    description: Published when a service subscription is cancelled.\n    subscribe:\n      operationId: onSubscriptionCancelled\n      summary: Subscription cancelled\n      description: Receive notifications when a customer cancels a service subscription.\n      tags:\n        - name: Subscriptions\n      message:\n        $ref: '#/components/messages/SubscriptionEvent'\n\n  billing/invoice/created:\n    description: Published when a new invoice is generated for a customer.\n    subscribe:\n      operationId: onInvoiceCreated\n      summary: Invoice created\n      description: Receive notifications when a billing invoice is generated for a customer.\n      tags:\n        - name: Billing\n      message:\n        $ref: '#/components/messages/InvoiceEvent'\n\
  \n  billing/payment/received:\n    description: Published when a payment is received against an invoice.\n    subscribe:\n      operationId: onPaymentReceived\n      summary: Payment received\n      description: Receive notifications when a payment is recorded against a customer invoice.\n      tags:\n        - name: Billing\n      message:\n        $ref: '#/components/messages/PaymentEvent'\n\ncomponents:\n  messages:\n    CustomerCreatedEvent:\n      name: CustomerCreatedEvent\n      title: Customer Created\n      summary: Notification that a new customer account was created\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CustomerEventPayload'\n\n    CustomerUpdatedEvent:\n      name: CustomerUpdatedEvent\n      title: Customer Updated\n      summary: Notification that a customer account was modified\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CustomerEventPayload'\n\n    SubscriptionEvent:\n    \
  \  name: SubscriptionEvent\n      title: Subscription Status Changed\n      summary: Notification that a subscription status changed\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SubscriptionEventPayload'\n\n    InvoiceEvent:\n      name: InvoiceEvent\n      title: Invoice Created\n      summary: Notification that an invoice was generated\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/InvoiceEventPayload'\n\n    PaymentEvent:\n      name: PaymentEvent\n      title: Payment Received\n      summary: Notification that a payment was recorded\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentEventPayload'\n\n  schemas:\n    EventEnvelope:\n      type: object\n      required: [eventId, eventType, eventTime, tenantId]\n      properties:\n        eventId:\n          type: string\n          description: Unique event identifier (UUID)\n        eventType:\n       \
  \   type: string\n          description: Type of event\n        eventTime:\n          type: string\n          format: date-time\n        tenantId:\n          type: string\n          description: BSS tenant identifier\n\n    CustomerEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/EventEnvelope'\n        - type: object\n          properties:\n            customerId:\n              type: string\n            accountNumber:\n              type: string\n            customerType:\n              type: string\n              enum: [Individual, Business, Government]\n            status:\n              type: string\n              enum: [Active, Inactive, Suspended, Terminated]\n            email:\n              type: string\n            previousStatus:\n              type: string\n              description: Previous status (for update events)\n\n    SubscriptionEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/EventEnvelope'\n        - type: object\n          properties:\n\
  \            subscriptionId:\n              type: string\n            customerId:\n              type: string\n            productId:\n              type: string\n            productName:\n              type: string\n            status:\n              type: string\n              enum: [Active, Suspended, Cancelled, Pending]\n            previousStatus:\n              type: string\n            effectiveDate:\n              type: string\n              format: date\n\n    InvoiceEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/EventEnvelope'\n        - type: object\n          properties:\n            invoiceId:\n              type: string\n            invoiceNumber:\n              type: string\n            customerId:\n              type: string\n            totalAmount:\n              type: number\n            currency:\n              type: string\n            dueDate:\n              type: string\n              format: date\n\n    PaymentEventPayload:\n      allOf:\n  \
  \      - $ref: '#/components/schemas/EventEnvelope'\n        - type: object\n          properties:\n            paymentId:\n              type: string\n            invoiceId:\n              type: string\n            customerId:\n              type: string\n            amount:\n              type: number\n            currency:\n              type: string\n            paymentMethod:\n              type: string\n              enum: [CreditCard, BankTransfer, DirectDebit, Cash]\n            paymentDate:\n              type: string\n              format: date\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/amdocs/refs/heads/main/asyncapi/amdocs-events-asyncapi.yml
spec_file: asyncapi/amdocs-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/amdocs/refs/heads/main/asyncapi/amdocs-events-asyncapi.yml
tags:
- Telecom
- BSS
- OSS
- Billing
- Customer Management
- MVNO
- 5G
- SaaS
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
