---
channels:
- description: Webhook endpoint that receives Binance Pay event notifications. Merchants must verify the signature header to authenticate webhook requests.
  name: /webhook
  operation: publish
  operation_id: receivePaymentNotification
  summary: Receive payment event notifications
description: Binance Pay sends webhook notifications to merchants for real-time payment status updates. When a customer completes a payment or a refund is processed, Binance Pay sends an HTTPS POST request to the merchant's configured webhook URL with event details.
layout: asyncapi
messages:
- description: ''
  name: PaymentSuccess
  summary: Notification sent when a customer successfully completes a payment.
  title: Payment Success
- description: ''
  name: PaymentCanceled
  summary: Notification sent when a payment is canceled.
  title: Payment Canceled
- description: ''
  name: PaymentExpired
  summary: Notification sent when a payment order expires.
  title: Payment Expired
- description: ''
  name: RefundSuccess
  summary: Notification sent when a refund is successfully processed.
  title: Refund Success
name: Binance Pay Webhooks
provider_name: Binance
provider_slug: binance
servers:
- description: Merchant-configured webhook endpoint that receives payment notifications from Binance Pay.
  name: merchantWebhook
  protocol: https
  url: '{merchantWebhookUrl}'
slug: binance-pay-webhooks-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Binance Pay Webhooks\n  description: >-\n    Binance Pay sends webhook notifications to merchants for real-time\n    payment status updates. When a customer completes a payment or a\n    refund is processed, Binance Pay sends an HTTPS POST request to\n    the merchant's configured webhook URL with event details.\n  version: '1.0.0'\n  contact:\n    name: Binance Pay Support\n    url: https://merchant.binance.com/en/docs/getting-started\n  externalDocs:\n    description: Binance Pay Webhook Documentation\n    url: https://developers.binance.com/docs/binance-pay/introduction\nservers:\n  merchantWebhook:\n    url: '{merchantWebhookUrl}'\n    protocol: https\n    description: >-\n      Merchant-configured webhook endpoint that receives payment\n      notifications from Binance Pay.\n    variables:\n      merchantWebhookUrl:\n        description: >-\n          The HTTPS URL configured by the merchant to receive webhooks.\nchannels:\n  /webhook:\n\
  \    description: >-\n      Webhook endpoint that receives Binance Pay event notifications.\n      Merchants must verify the signature header to authenticate\n      webhook requests.\n    publish:\n      operationId: receivePaymentNotification\n      summary: Receive payment event notifications\n      message:\n        oneOf:\n          - $ref: '#/components/messages/PaymentSuccess'\n          - $ref: '#/components/messages/PaymentCanceled'\n          - $ref: '#/components/messages/PaymentExpired'\n          - $ref: '#/components/messages/RefundSuccess'\ncomponents:\n  messages:\n    PaymentSuccess:\n      name: paymentSuccess\n      title: Payment Success\n      summary: >-\n        Notification sent when a customer successfully completes a payment.\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    PaymentCanceled:\n      name: paymentCanceled\n      title: Payment Canceled\n      summary: >-\n        Notification sent when a payment is canceled.\n      payload:\n\
  \        $ref: '#/components/schemas/WebhookPayload'\n    PaymentExpired:\n      name: paymentExpired\n      title: Payment Expired\n      summary: >-\n        Notification sent when a payment order expires.\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    RefundSuccess:\n      name: refundSuccess\n      title: Refund Success\n      summary: >-\n        Notification sent when a refund is successfully processed.\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n  schemas:\n    WebhookPayload:\n      type: object\n      properties:\n        bizType:\n          type: string\n          description: >-\n            Business type. PAY for payments, PAY_REFUND for refunds.\n          enum:\n            - PAY\n            - PAY_REFUND\n        bizId:\n          type: string\n          description: >-\n            Unique business ID for the event.\n        bizStatus:\n          type: string\n          description: >-\n            Business status of the\
  \ event.\n          enum:\n            - PAY_SUCCESS\n            - PAY_CLOSED\n            - REFUND_SUCCESS\n        merchantTradeNo:\n          type: string\n          description: >-\n            Merchant trade number from the original order.\n        productType:\n          type: string\n          description: >-\n            Product type.\n        productName:\n          type: string\n          description: >-\n            Product name.\n        transactTime:\n          type: integer\n          format: int64\n          description: >-\n            Transaction time in milliseconds.\n        totalFee:\n          type: string\n          description: >-\n            Total transaction amount.\n        currency:\n          type: string\n          description: >-\n            Transaction currency.\n        transactionId:\n          type: string\n          description: >-\n            Binance Pay transaction ID.\n        payerInfo:\n          type: object\n          description: >-\n    \
  \        Payer information.\n          properties:\n            payerId:\n              type: string\n              description: >-\n                Payer ID.\n            payerName:\n              type: string\n              description: >-\n                Payer name.\n        commission:\n          type: string\n          description: >-\n            Commission amount.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/binance/refs/heads/main/asyncapi/binance-pay-webhooks-asyncapi.yml
spec_file: asyncapi/binance-pay-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/binance/refs/heads/main/asyncapi/binance-pay-webhooks-asyncapi.yml
tags:
- Cryptocurrency
- Exchange
- Trading
- Blockchain
- Finance
- DeFi
- Market Data
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
