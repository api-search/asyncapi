---
api_specs:
- filename: nomba-authentication-openapi.yml
  format: yaml
  label: Nomba Authentication API
  slug: authentication
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/nomba/refs/heads/main/openapi/nomba-authentication-openapi.yml
- filename: nomba-accounts-openapi.yml
  format: yaml
  label: Nomba Accounts API
  slug: accounts
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/nomba/refs/heads/main/openapi/nomba-accounts-openapi.yml
- filename: nomba-virtual-accounts-openapi.yml
  format: yaml
  label: Nomba Virtual Accounts API
  slug: virtual-accounts
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/nomba/refs/heads/main/openapi/nomba-virtual-accounts-openapi.yml
- filename: nomba-transfers-openapi.yml
  format: yaml
  label: Nomba Transfers API
  slug: transfers
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/nomba/refs/heads/main/openapi/nomba-transfers-openapi.yml
- filename: nomba-online-checkout-openapi.yml
  format: yaml
  label: Nomba Online Checkout API
  slug: online-checkout
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/nomba/refs/heads/main/openapi/nomba-online-checkout-openapi.yml
- filename: nomba-charge-openapi.yml
  format: yaml
  label: Nomba Charge API
  slug: charge
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/nomba/refs/heads/main/openapi/nomba-charge-openapi.yml
- filename: nomba-transactions-openapi.yml
  format: yaml
  label: Nomba Transactions API
  slug: transactions
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/nomba/refs/heads/main/openapi/nomba-transactions-openapi.yml
- filename: nomba-global-payout-openapi.yml
  format: yaml
  label: Nomba Global Payout API
  slug: global-payout
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/nomba/refs/heads/main/openapi/nomba-global-payout-openapi.yml
channels:
- description: The webhook delivery channel. Nomba sends HTTP POST requests to the merchant webhook URL when subscribed events occur, such as payment completions, payout events, order updates, and reversals.
  name: /webhook
  operation: publish
  operation_id: receiveWebhookEvent
  summary: Receive a webhook event notification
description: The Nomba Webhooks system delivers real-time event notifications via HTTP POST callbacks when activities occur within a customer account. Events include payment successes and failures, payout completions, order updates, payment reversals, and refunds. Webhook payloads are delivered as JSON to merchant-configured URLs and include an optional HMAC signature for payload verification to prevent DDoS or Man-in-the-Middle attacks. Nomba implements a backoff retry policy for failed webhook deliveries.
layout: asyncapi
messages:
- description: ''
  name: PaymentSuccess
  summary: Triggered when a payment is successfully received in the merchant account, including POS terminal payments, web transactions, app payments, and virtual account transfers.
  title: Payment Success Event
- description: ''
  name: PaymentFailed
  summary: Triggered when a payment attempt fails due to insufficient funds, expired cards, declined transactions, or other payment errors.
  title: Payment Failed Event
- description: ''
  name: PayoutSuccess
  summary: Triggered when a payout (transfer to a bank account or wallet) is successfully completed.
  title: Payout Success Event
- description: ''
  name: PayoutFailed
  summary: Triggered when a payout attempt fails during processing.
  title: Payout Failed Event
- description: ''
  name: OrderSuccess
  summary: Triggered when a checkout order is successfully completed and payment has been confirmed.
  title: Order Success Event
- description: ''
  name: PaymentReversal
  summary: Triggered when a previously successful payment is reversed due to a dispute, chargeback, or system correction.
  title: Payment Reversal Event
- description: ''
  name: PayoutRefund
  summary: Triggered when a payout is refunded back to the merchant account, typically due to an invalid recipient or failed settlement.
  title: Payout Refund Event
name: Nomba Webhook Events
provider_name: Nomba
provider_slug: nomba
servers:
- description: The merchant-configured HTTPS webhook endpoint URL that receives event notifications from Nomba. Configured through the Nomba dashboard under webhook settings.
  name: webhookEndpoint
  protocol: https
  url: '{merchantWebhookUrl}'
slug: nomba-webhooks-asyncapi
source_filename: nomba-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Nomba Webhook Events\n  description: >-\n    The Nomba Webhooks system delivers real-time event notifications via HTTP\n    POST callbacks when activities occur within a customer account. Events\n    include payment successes and failures, payout completions, order\n    updates, payment reversals, and refunds. Webhook payloads are delivered\n    as JSON to merchant-configured URLs and include an optional HMAC\n    signature for payload verification to prevent DDoS or Man-in-the-Middle\n    attacks. Nomba implements a backoff retry policy for failed webhook\n    deliveries.\n  version: '1.0.0'\n  contact:\n    name: Nomba Developer Support\n    url: https://developer.nomba.com\nservers:\n  webhookEndpoint:\n    url: '{merchantWebhookUrl}'\n    protocol: https\n    description: >-\n      The merchant-configured HTTPS webhook endpoint URL that receives event\n      notifications from Nomba. Configured through the Nomba dashboard under\n      webhook\
  \ settings.\n    variables:\n      merchantWebhookUrl:\n        description: >-\n          The URL configured by the merchant in the Nomba dashboard to receive\n          webhook events.\nchannels:\n  /webhook:\n    description: >-\n      The webhook delivery channel. Nomba sends HTTP POST requests to the\n      merchant webhook URL when subscribed events occur, such as payment\n      completions, payout events, order updates, and reversals.\n    publish:\n      operationId: receiveWebhookEvent\n      summary: Receive a webhook event notification\n      description: >-\n        Receives webhook event notifications from Nomba when subscribed\n        events occur within the merchant account. Events are delivered as\n        HTTP POST requests with JSON payloads. Merchants must subscribe to\n        specific event types via the Nomba dashboard.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/PaymentSuccess'\n          - $ref: '#/components/messages/PaymentFailed'\n\
  \          - $ref: '#/components/messages/PayoutSuccess'\n          - $ref: '#/components/messages/PayoutFailed'\n          - $ref: '#/components/messages/OrderSuccess'\n          - $ref: '#/components/messages/PaymentReversal'\n          - $ref: '#/components/messages/PayoutRefund'\ncomponents:\n  securitySchemes:\n    signatureVerification:\n      type: httpApiKey\n      name: X-Nomba-Signature\n      in: header\n      description: >-\n        HMAC signature for verifying the authenticity of webhook payloads.\n        The signature key is configured when creating the webhook URL in\n        the Nomba dashboard. Verification is optional but strongly\n        recommended to prevent DDoS or Man-in-the-Middle attacks.\n  messages:\n    PaymentSuccess:\n      name: PaymentSuccess\n      title: Payment Success Event\n      summary: >-\n        Triggered when a payment is successfully received in the merchant\n        account, including POS terminal payments, web transactions, app\n       \
  \ payments, and virtual account transfers.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentSuccessPayload'\n    PaymentFailed:\n      name: PaymentFailed\n      title: Payment Failed Event\n      summary: >-\n        Triggered when a payment attempt fails due to insufficient funds,\n        expired cards, declined transactions, or other payment errors.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentFailedPayload'\n    PayoutSuccess:\n      name: PayoutSuccess\n      title: Payout Success Event\n      summary: >-\n        Triggered when a payout (transfer to a bank account or wallet)\n        is successfully completed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PayoutSuccessPayload'\n    PayoutFailed:\n      name: PayoutFailed\n      title: Payout Failed Event\n      summary: >-\n        Triggered when a payout attempt fails during processing.\n\
  \      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PayoutFailedPayload'\n    OrderSuccess:\n      name: OrderSuccess\n      title: Order Success Event\n      summary: >-\n        Triggered when a checkout order is successfully completed and\n        payment has been confirmed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderSuccessPayload'\n    PaymentReversal:\n      name: PaymentReversal\n      title: Payment Reversal Event\n      summary: >-\n        Triggered when a previously successful payment is reversed due\n        to a dispute, chargeback, or system correction.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentReversalPayload'\n    PayoutRefund:\n      name: PayoutRefund\n      title: Payout Refund Event\n      summary: >-\n        Triggered when a payout is refunded back to the merchant account,\n        typically due to an invalid recipient or\
  \ failed settlement.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PayoutRefundPayload'\n  schemas:\n    PaymentSuccessPayload:\n      type: object\n      required:\n        - event_type\n        - requestId\n        - data\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of event that triggered the webhook.\n          const: payment_success\n        requestId:\n          type: string\n          format: uuid\n          description: >-\n            A unique identifier for this webhook delivery request.\n          example: 999111df-9f20-4cf8-8740-3d2fc43c7149\n        data:\n          type: object\n          required:\n            - merchant\n            - transaction\n          properties:\n            merchant:\n              $ref: '#/components/schemas/MerchantData'\n            terminal:\n              $ref: '#/components/schemas/TerminalData'\n            transaction:\n      \
  \        $ref: '#/components/schemas/TransactionData'\n    PaymentFailedPayload:\n      type: object\n      required:\n        - event_type\n        - requestId\n        - data\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of event that triggered the webhook.\n          const: payment_failed\n        requestId:\n          type: string\n          format: uuid\n          description: >-\n            A unique identifier for this webhook delivery request.\n        data:\n          type: object\n          properties:\n            merchant:\n              $ref: '#/components/schemas/MerchantData'\n            terminal:\n              $ref: '#/components/schemas/TerminalData'\n            transaction:\n              $ref: '#/components/schemas/TransactionData'\n            error:\n              type: string\n              description: >-\n                A description of why the payment failed.\n    PayoutSuccessPayload:\n   \
  \   type: object\n      required:\n        - event_type\n        - requestId\n        - data\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of event that triggered the webhook.\n          const: payout_success\n        requestId:\n          type: string\n          format: uuid\n          description: >-\n            A unique identifier for this webhook delivery request.\n        data:\n          type: object\n          properties:\n            merchant:\n              $ref: '#/components/schemas/MerchantData'\n            transaction:\n              $ref: '#/components/schemas/TransactionData'\n    PayoutFailedPayload:\n      type: object\n      required:\n        - event_type\n        - requestId\n        - data\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of event that triggered the webhook.\n          const: payout_failed\n        requestId:\n       \
  \   type: string\n          format: uuid\n          description: >-\n            A unique identifier for this webhook delivery request.\n        data:\n          type: object\n          properties:\n            merchant:\n              $ref: '#/components/schemas/MerchantData'\n            transaction:\n              $ref: '#/components/schemas/TransactionData'\n            error:\n              type: string\n              description: >-\n                A description of why the payout failed.\n    OrderSuccessPayload:\n      type: object\n      required:\n        - event_type\n        - requestId\n        - data\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of event that triggered the webhook.\n          const: order_success\n        requestId:\n          type: string\n          format: uuid\n          description: >-\n            A unique identifier for this webhook delivery request.\n        data:\n          type: object\n\
  \          properties:\n            merchant:\n              $ref: '#/components/schemas/MerchantData'\n            order:\n              type: object\n              properties:\n                orderReference:\n                  type: string\n                  description: >-\n                    The unique reference for the checkout order.\n                amount:\n                  type: number\n                  format: double\n                  description: >-\n                    The order amount.\n                currency:\n                  type: string\n                  description: >-\n                    The currency of the order.\n            transaction:\n              $ref: '#/components/schemas/TransactionData'\n    PaymentReversalPayload:\n      type: object\n      required:\n        - event_type\n        - requestId\n        - data\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of event that triggered the\
  \ webhook.\n          const: payment_reversal\n        requestId:\n          type: string\n          format: uuid\n          description: >-\n            A unique identifier for this webhook delivery request.\n        data:\n          type: object\n          properties:\n            merchant:\n              $ref: '#/components/schemas/MerchantData'\n            transaction:\n              $ref: '#/components/schemas/TransactionData'\n            originalTransactionId:\n              type: string\n              description: >-\n                The transaction ID of the original payment that was reversed.\n    PayoutRefundPayload:\n      type: object\n      required:\n        - event_type\n        - requestId\n        - data\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of event that triggered the webhook.\n          const: payout_refund\n        requestId:\n          type: string\n          format: uuid\n          description:\
  \ >-\n            A unique identifier for this webhook delivery request.\n        data:\n          type: object\n          properties:\n            merchant:\n              $ref: '#/components/schemas/MerchantData'\n            transaction:\n              $ref: '#/components/schemas/TransactionData'\n            originalTransactionId:\n              type: string\n              description: >-\n                The transaction ID of the original payout that was refunded.\n    MerchantData:\n      type: object\n      properties:\n        walletId:\n          type: string\n          description: >-\n            The unique identifier for the merchant wallet.\n          example: 5f04b9ee600f1c00084affa2\n        walletBalance:\n          type: number\n          format: double\n          description: >-\n            The current wallet balance after the event.\n          example: 732233.66\n        userId:\n          type: string\n          format: uuid\n          description: >-\n           \
  \ The unique identifier of the merchant user.\n          example: 000000ab-154e-4a11-a0cf-2249fad063e3\n    TerminalData:\n      type: object\n      description: >-\n        Terminal information, populated for POS terminal transactions.\n      properties:\n        terminalId:\n          type: string\n          description: >-\n            The unique identifier of the POS terminal.\n        serialNumber:\n          type: string\n          description: >-\n            The serial number of the POS terminal.\n    TransactionData:\n      type: object\n      properties:\n        transactionId:\n          type: string\n          description: >-\n            The unique identifier for the transaction.\n          example: API-VACT_TRA-067fg-sdf78ghy-fd7f-4567-b404-3122939dc25f\n        type:\n          type: string\n          description: >-\n            The type of transaction.\n          example: vact_transfer\n        aliasAccountNumber:\n          type: string\n          description: >-\n  \
  \          The alias account number associated with the transaction.\n          example: '0010721887'\n        fee:\n          type: number\n          format: double\n          description: >-\n            The fee charged for the transaction.\n          example: 150\n        amount:\n          type: number\n          format: double\n          description: >-\n            The transaction amount.\n        sessionId:\n          type: string\n          description: >-\n            The session identifier for the transaction.\n          example: '100004240726191726000236980560'\n        status:\n          type: string\n          description: >-\n            The status of the transaction.\n          enum:\n            - successful\n            - failed\n            - reversed\n            - refunded\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/nomba/refs/heads/main/asyncapi/nomba-webhooks-asyncapi.yml
spec_file: asyncapi/nomba-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/nomba/refs/heads/main/asyncapi/nomba-webhooks-asyncapi.yml
tags:
- Payments
- Fintech
- Banking
- Transfers
- Virtual Accounts
- Checkout
- Cross-Border Payments
- Cards
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
