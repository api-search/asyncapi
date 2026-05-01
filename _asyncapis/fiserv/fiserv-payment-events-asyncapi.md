---
api_specs:
- filename: fiserv-commercehub-openapi.yml
  format: yaml
  label: Fiserv CommerceHub API
  slug: commercehub
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/fiserv/refs/heads/main/openapi/fiserv-commercehub-openapi.yml
- filename: fiserv-cardpointe-gateway-openapi.yml
  format: yaml
  label: Fiserv CardPointe Gateway API
  slug: cardpointe-gateway
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/fiserv/refs/heads/main/openapi/fiserv-cardpointe-gateway-openapi.yml
- filename: fiserv-bankinghub-openapi.yml
  format: yaml
  label: Fiserv BankingHub API
  slug: bankinghub
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/fiserv/refs/heads/main/openapi/fiserv-bankinghub-openapi.yml
- filename: fiserv-carddeveloper-openapi.yml
  format: yaml
  label: Fiserv CardDeveloper API
  slug: carddeveloper
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/fiserv/refs/heads/main/openapi/fiserv-carddeveloper-openapi.yml
- filename: fiserv-payment-events-asyncapi.yml
  format: yaml
  label: Fiserv Payment Events
  slug: payment-events
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/fiserv/refs/heads/main/asyncapi/fiserv-payment-events-asyncapi.yml
channels:
- description: Receives transaction lifecycle event notifications including authorizations, captures, refunds, voids, and declines.
  name: /webhooks/transactions
  operation: publish
  operation_id: receiveTransactionEvent
  summary: Receive transaction event notification
- description: Receives settlement event notifications when transaction batches are settled and funds are deposited.
  name: /webhooks/settlements
  operation: publish
  operation_id: receiveSettlementEvent
  summary: Receive settlement event notification
- description: Receives dispute and chargeback event notifications when cardholders raise disputes against transactions.
  name: /webhooks/disputes
  operation: publish
  operation_id: receiveDisputeEvent
  summary: Receive dispute event notification
- description: Receives checkout session event notifications for hosted checkout page integrations.
  name: /webhooks/checkout
  operation: publish
  operation_id: receiveCheckoutEvent
  summary: Receive checkout event notification
description: Fiserv provides webhook-based event notifications across the payments lifecycle. Merchants can subscribe to webhooks to receive real-time notifications for key events including transaction status changes, settlement updates, dispute notifications, and checkout completions. Events are delivered as HTTP POST requests to merchant-configured URL endpoints.
layout: asyncapi
messages:
- description: ''
  name: TransactionAuthorized
  summary: Notification sent when a transaction is successfully authorized.
  title: Transaction Authorized
- description: ''
  name: TransactionCaptured
  summary: Notification sent when an authorized transaction is captured for settlement.
  title: Transaction Captured
- description: ''
  name: TransactionRefunded
  summary: Notification sent when a transaction refund is processed.
  title: Transaction Refunded
- description: ''
  name: TransactionVoided
  summary: Notification sent when a transaction is voided.
  title: Transaction Voided
- description: ''
  name: TransactionDeclined
  summary: Notification sent when a transaction is declined.
  title: Transaction Declined
- description: ''
  name: SettlementCompleted
  summary: Notification sent when a settlement batch is completed and funds are scheduled for deposit.
  title: Settlement Completed
- description: ''
  name: DisputeOpened
  summary: Notification sent when a new dispute is opened against a transaction.
  title: Dispute Opened
- description: ''
  name: DisputeUpdated
  summary: Notification sent when a dispute status changes.
  title: Dispute Updated
- description: ''
  name: DisputeResolved
  summary: Notification sent when a dispute is resolved, either in favor of the merchant or the cardholder.
  title: Dispute Resolved
- description: ''
  name: CheckoutCompleted
  summary: Notification sent when a hosted checkout session is completed successfully.
  title: Checkout Completed
- description: ''
  name: CheckoutAbandoned
  summary: Notification sent when a hosted checkout session is abandoned or expires.
  title: Checkout Abandoned
name: Fiserv Payment Events
provider_name: Fiserv
provider_slug: fiserv
servers:
- description: Merchant-configured webhook endpoint that receives event notifications from Fiserv.
  name: fiservWebhooks
  protocol: https
  url: '{merchantWebhookUrl}'
slug: fiserv-payment-events-asyncapi
source_filename: fiserv-payment-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Fiserv Payment Events\n  description: >-\n    Fiserv provides webhook-based event notifications across the payments\n    lifecycle. Merchants can subscribe to webhooks to receive real-time\n    notifications for key events including transaction status changes,\n    settlement updates, dispute notifications, and checkout completions.\n    Events are delivered as HTTP POST requests to merchant-configured\n    URL endpoints.\n  version: '1.0.0'\n  contact:\n    name: Fiserv Developer Support\n    url: https://developer.fiserv.com/support\nservers:\n  fiservWebhooks:\n    url: '{merchantWebhookUrl}'\n    protocol: https\n    description: >-\n      Merchant-configured webhook endpoint that receives event\n      notifications from Fiserv.\n    variables:\n      merchantWebhookUrl:\n        description: >-\n          The URL endpoint configured by the merchant to receive\n          webhook notifications.\n    security:\n      - hmacSignature: []\n\
  channels:\n  /webhooks/transactions:\n    description: >-\n      Receives transaction lifecycle event notifications including\n      authorizations, captures, refunds, voids, and declines.\n    publish:\n      operationId: receiveTransactionEvent\n      summary: Receive transaction event notification\n      description: >-\n        Fiserv sends transaction event notifications when the status\n        of a payment transaction changes, including successful\n        authorizations, captures, refunds, and declines.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/TransactionAuthorized'\n          - $ref: '#/components/messages/TransactionCaptured'\n          - $ref: '#/components/messages/TransactionRefunded'\n          - $ref: '#/components/messages/TransactionVoided'\n          - $ref: '#/components/messages/TransactionDeclined'\n  /webhooks/settlements:\n    description: >-\n      Receives settlement event notifications when transaction batches\n      are settled\
  \ and funds are deposited.\n    publish:\n      operationId: receiveSettlementEvent\n      summary: Receive settlement event notification\n      description: >-\n        Fiserv sends settlement notifications when transaction batches\n        are processed and funds are scheduled for deposit.\n      message:\n        $ref: '#/components/messages/SettlementCompleted'\n  /webhooks/disputes:\n    description: >-\n      Receives dispute and chargeback event notifications when\n      cardholders raise disputes against transactions.\n    publish:\n      operationId: receiveDisputeEvent\n      summary: Receive dispute event notification\n      description: >-\n        Fiserv sends dispute notifications when a cardholder raises\n        a dispute, when dispute status changes, or when a dispute\n        is resolved.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/DisputeOpened'\n          - $ref: '#/components/messages/DisputeUpdated'\n          - $ref: '#/components/messages/DisputeResolved'\n\
  \  /webhooks/checkout:\n    description: >-\n      Receives checkout session event notifications for hosted\n      checkout page integrations.\n    publish:\n      operationId: receiveCheckoutEvent\n      summary: Receive checkout event notification\n      description: >-\n        Fiserv sends checkout event notifications when a hosted\n        checkout session is completed, abandoned, or expires.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/CheckoutCompleted'\n          - $ref: '#/components/messages/CheckoutAbandoned'\ncomponents:\n  securitySchemes:\n    hmacSignature:\n      type: httpApiKey\n      name: X-Fiserv-Signature\n      in: header\n      description: >-\n        HMAC-SHA256 signature of the webhook payload, computed using\n        the merchant's webhook secret. Merchants should verify this\n        signature to ensure the authenticity and integrity of the\n        webhook notification.\n  messages:\n    TransactionAuthorized:\n      name: TransactionAuthorized\n\
  \      title: Transaction Authorized\n      summary: >-\n        Notification sent when a transaction is successfully authorized.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TransactionEvent'\n    TransactionCaptured:\n      name: TransactionCaptured\n      title: Transaction Captured\n      summary: >-\n        Notification sent when an authorized transaction is captured\n        for settlement.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TransactionEvent'\n    TransactionRefunded:\n      name: TransactionRefunded\n      title: Transaction Refunded\n      summary: >-\n        Notification sent when a transaction refund is processed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TransactionEvent'\n    TransactionVoided:\n      name: TransactionVoided\n      title: Transaction Voided\n      summary: >-\n        Notification sent when a transaction is voided.\n\
  \      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TransactionEvent'\n    TransactionDeclined:\n      name: TransactionDeclined\n      title: Transaction Declined\n      summary: >-\n        Notification sent when a transaction is declined.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TransactionEvent'\n    SettlementCompleted:\n      name: SettlementCompleted\n      title: Settlement Completed\n      summary: >-\n        Notification sent when a settlement batch is completed and\n        funds are scheduled for deposit.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SettlementEvent'\n    DisputeOpened:\n      name: DisputeOpened\n      title: Dispute Opened\n      summary: >-\n        Notification sent when a new dispute is opened against a\n        transaction.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DisputeEvent'\n\
  \    DisputeUpdated:\n      name: DisputeUpdated\n      title: Dispute Updated\n      summary: >-\n        Notification sent when a dispute status changes.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DisputeEvent'\n    DisputeResolved:\n      name: DisputeResolved\n      title: Dispute Resolved\n      summary: >-\n        Notification sent when a dispute is resolved, either in\n        favor of the merchant or the cardholder.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DisputeEvent'\n    CheckoutCompleted:\n      name: CheckoutCompleted\n      title: Checkout Completed\n      summary: >-\n        Notification sent when a hosted checkout session is\n        completed successfully.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CheckoutEvent'\n    CheckoutAbandoned:\n      name: CheckoutAbandoned\n      title: Checkout Abandoned\n      summary: >-\n     \
  \   Notification sent when a hosted checkout session is\n        abandoned or expires.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CheckoutEvent'\n  schemas:\n    TransactionEvent:\n      type: object\n      description: >-\n        Transaction lifecycle event payload.\n      required:\n        - eventId\n        - eventType\n        - timestamp\n        - transactionId\n      properties:\n        eventId:\n          type: string\n          format: uuid\n          description: >-\n            Unique identifier for this event.\n        eventType:\n          type: string\n          enum:\n            - TRANSACTION_AUTHORIZED\n            - TRANSACTION_CAPTURED\n            - TRANSACTION_REFUNDED\n            - TRANSACTION_VOIDED\n            - TRANSACTION_DECLINED\n          description: >-\n            The type of transaction event.\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n        \
  \    The timestamp when the event occurred.\n        transactionId:\n          type: string\n          description: >-\n            The unique transaction identifier.\n        orderId:\n          type: string\n          description: >-\n            The merchant order identifier.\n        amount:\n          type: number\n          format: double\n          description: >-\n            The transaction amount.\n        currency:\n          type: string\n          pattern: '^[A-Z]{3}$'\n          description: >-\n            The ISO 4217 currency code.\n        transactionState:\n          type: string\n          description: >-\n            The current state of the transaction.\n        merchantId:\n          type: string\n          description: >-\n            The merchant identifier.\n        paymentMethod:\n          type: string\n          description: >-\n            The payment method used (e.g., card brand).\n        responseCode:\n          type: string\n          description: >-\n\
  \            The processor response code.\n        responseMessage:\n          type: string\n          description: >-\n            The processor response message.\n    SettlementEvent:\n      type: object\n      description: >-\n        Settlement batch event payload.\n      required:\n        - eventId\n        - eventType\n        - timestamp\n      properties:\n        eventId:\n          type: string\n          format: uuid\n          description: >-\n            Unique identifier for this event.\n        eventType:\n          type: string\n          enum:\n            - SETTLEMENT_COMPLETED\n          description: >-\n            The type of settlement event.\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            The timestamp when the event occurred.\n        batchId:\n          type: string\n          description: >-\n            The settlement batch identifier.\n        merchantId:\n          type: string\n          description:\
  \ >-\n            The merchant identifier.\n        totalAmount:\n          type: number\n          format: double\n          description: >-\n            The total settlement amount.\n        currency:\n          type: string\n          description: >-\n            The ISO 4217 currency code.\n        transactionCount:\n          type: integer\n          description: >-\n            The number of transactions in the batch.\n        fundingDate:\n          type: string\n          format: date\n          description: >-\n            The expected funding date.\n    DisputeEvent:\n      type: object\n      description: >-\n        Dispute event payload.\n      required:\n        - eventId\n        - eventType\n        - timestamp\n        - disputeId\n      properties:\n        eventId:\n          type: string\n          format: uuid\n          description: >-\n            Unique identifier for this event.\n        eventType:\n          type: string\n          enum:\n            - DISPUTE_OPENED\n\
  \            - DISPUTE_UPDATED\n            - DISPUTE_RESOLVED\n          description: >-\n            The type of dispute event.\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            The timestamp when the event occurred.\n        disputeId:\n          type: string\n          description: >-\n            The unique dispute identifier.\n        transactionId:\n          type: string\n          description: >-\n            The disputed transaction identifier.\n        disputeStatus:\n          type: string\n          enum:\n            - OPEN\n            - UNDER_REVIEW\n            - MERCHANT_RESPONSE_REQUIRED\n            - RESOLVED_MERCHANT_FAVOR\n            - RESOLVED_CARDHOLDER_FAVOR\n          description: >-\n            The current dispute status.\n        disputeAmount:\n          type: number\n          format: double\n          description: >-\n            The disputed amount.\n        currency:\n          type: string\n\
  \          description: >-\n            The ISO 4217 currency code.\n        reason:\n          type: string\n          description: >-\n            The dispute reason description.\n        reasonCode:\n          type: string\n          description: >-\n            The dispute reason code.\n        responseDeadline:\n          type: string\n          format: date\n          description: >-\n            The deadline for merchant response.\n    CheckoutEvent:\n      type: object\n      description: >-\n        Checkout session event payload.\n      required:\n        - eventId\n        - eventType\n        - timestamp\n        - sessionId\n      properties:\n        eventId:\n          type: string\n          format: uuid\n          description: >-\n            Unique identifier for this event.\n        eventType:\n          type: string\n          enum:\n            - CHECKOUT_COMPLETED\n            - CHECKOUT_ABANDONED\n          description: >-\n            The type of checkout event.\n\
  \        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            The timestamp when the event occurred.\n        sessionId:\n          type: string\n          description: >-\n            The checkout session identifier.\n        transactionId:\n          type: string\n          description: >-\n            The transaction identifier if payment was processed.\n        orderId:\n          type: string\n          description: >-\n            The merchant order identifier.\n        amount:\n          type: number\n          format: double\n          description: >-\n            The checkout amount.\n        currency:\n          type: string\n          description: >-\n            The ISO 4217 currency code.\n        paymentStatus:\n          type: string\n          description: >-\n            The payment status.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/fiserv/refs/heads/main/asyncapi/fiserv-payment-events-asyncapi.yml
spec_file: asyncapi/fiserv-payment-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/fiserv/refs/heads/main/asyncapi/fiserv-payment-events-asyncapi.yml
tags:
- Banking
- Financial
- Payments
- Wealth Management
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
