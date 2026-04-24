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
