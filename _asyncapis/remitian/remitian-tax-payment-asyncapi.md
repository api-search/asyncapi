---
api_specs:
- filename: remitian-tax-payment-openapi.yml
  format: yaml
  label: Remitian Tax Payment API
  slug: tax-payment-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/remitian/refs/heads/main/openapi/remitian-tax-payment-openapi.yml
channels:
- description: Webhook delivery channel for all Remitian tax payment events. Events are delivered as HTTP POST requests with a JSON payload and an X-Remitian-Signature header containing the HMAC-SHA256 signature.
  name: /webhook
  operation: publish
  operation_id: receivePaymentEvent
  summary: Receive a tax payment event
description: Real-time webhook events from the Remitian Tax Payment API. These events provide status updates for tax payments as they move through initiation, validation, processing, and completion. All webhook deliveries include an HMAC signature header for authenticity verification using the signing secret provided during webhook subscription creation.
layout: asyncapi
messages:
- description: Fired when a new tax payment is created via the API. The payment is in draft status and awaits validation and confirmation.
  name: PaymentInitiated
  summary: A new tax payment has been initiated
  title: Payment Initiated
- description: Fired when a payment passes all jurisdiction-specific validation checks and is ready for confirmation.
  name: PaymentValidated
  summary: A tax payment has passed jurisdiction validation
  title: Payment Validated
- description: Fired when a partner confirms a validated payment. The payment is now queued for routing to the tax authority.
  name: PaymentConfirmed
  summary: A tax payment has been confirmed for processing
  title: Payment Confirmed
- description: Fired when the payment has been submitted to the tax authority and is awaiting confirmation of receipt and processing.
  name: PaymentProcessing
  summary: A tax payment is being processed by the tax authority
  title: Payment Processing
- description: Fired when the tax authority confirms successful receipt and processing of the payment. The payment now includes a confirmation number from the authority.
  name: PaymentCompleted
  summary: A tax payment has been successfully completed
  title: Payment Completed
- description: Fired when a payment fails during processing. Includes an error code and description of the failure reason. The partner may need to take corrective action and retry.
  name: PaymentFailed
  summary: A tax payment has failed
  title: Payment Failed
- description: Fired when a payment is cancelled either by the partner or by the system due to expiration or other automated rules.
  name: PaymentCancelled
  summary: A tax payment has been cancelled
  title: Payment Cancelled
name: Remitian Tax Payment Events
provider_name: Remitian
provider_slug: remitian
servers:
- description: Partner-provided webhook endpoint. Remitian delivers events to the HTTPS URL registered via the Webhooks API.
  name: partner
  protocol: https
  url: '{webhookUrl}'
slug: remitian-tax-payment-asyncapi
source_filename: remitian-tax-payment-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Remitian Tax Payment Events\n  description: >-\n    Real-time webhook events from the Remitian Tax Payment API. These events\n    provide status updates for tax payments as they move through initiation,\n    validation, processing, and completion. All webhook deliveries include an\n    HMAC signature header for authenticity verification using the signing\n    secret provided during webhook subscription creation.\n  version: '1.0.0'\n  contact:\n    name: Remitian Support\n    url: https://help.remitian.com\nservers:\n  partner:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Partner-provided webhook endpoint. Remitian delivers events to the\n      HTTPS URL registered via the Webhooks API.\n    variables:\n      webhookUrl:\n        description: The webhook endpoint URL configured by the partner\n    security:\n      - hmacSignature: []\nchannels:\n  /webhook:\n    description: >-\n      Webhook delivery channel for\
  \ all Remitian tax payment events. Events\n      are delivered as HTTP POST requests with a JSON payload and an\n      X-Remitian-Signature header containing the HMAC-SHA256 signature.\n    publish:\n      operationId: receivePaymentEvent\n      summary: Receive a tax payment event\n      description: >-\n        Receive real-time notifications about tax payment lifecycle events.\n        Partners should respond with a 2xx status code within 30 seconds\n        to acknowledge receipt. Failed deliveries are retried with\n        exponential backoff.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/PaymentInitiated'\n          - $ref: '#/components/messages/PaymentValidated'\n          - $ref: '#/components/messages/PaymentConfirmed'\n          - $ref: '#/components/messages/PaymentProcessing'\n          - $ref: '#/components/messages/PaymentCompleted'\n          - $ref: '#/components/messages/PaymentFailed'\n          - $ref: '#/components/messages/PaymentCancelled'\n\
  components:\n  securitySchemes:\n    hmacSignature:\n      type: httpApiKey\n      name: X-Remitian-Signature\n      in: header\n      description: >-\n        HMAC-SHA256 signature of the request body using the signing secret\n        provided during webhook subscription creation. Verify this signature\n        to ensure the webhook delivery originated from Remitian.\n  messages:\n    PaymentInitiated:\n      name: payment.initiated\n      title: Payment Initiated\n      summary: A new tax payment has been initiated\n      description: >-\n        Fired when a new tax payment is created via the API. The payment\n        is in draft status and awaits validation and confirmation.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentEvent'\n    PaymentValidated:\n      name: payment.validated\n      title: Payment Validated\n      summary: A tax payment has passed jurisdiction validation\n      description: >-\n        Fired when a payment passes\
  \ all jurisdiction-specific validation\n        checks and is ready for confirmation.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentEvent'\n    PaymentConfirmed:\n      name: payment.confirmed\n      title: Payment Confirmed\n      summary: A tax payment has been confirmed for processing\n      description: >-\n        Fired when a partner confirms a validated payment. The payment is\n        now queued for routing to the tax authority.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentEvent'\n    PaymentProcessing:\n      name: payment.processing\n      title: Payment Processing\n      summary: A tax payment is being processed by the tax authority\n      description: >-\n        Fired when the payment has been submitted to the tax authority\n        and is awaiting confirmation of receipt and processing.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentEvent'\n\
  \    PaymentCompleted:\n      name: payment.completed\n      title: Payment Completed\n      summary: A tax payment has been successfully completed\n      description: >-\n        Fired when the tax authority confirms successful receipt and\n        processing of the payment. The payment now includes a\n        confirmation number from the authority.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentCompletedEvent'\n    PaymentFailed:\n      name: payment.failed\n      title: Payment Failed\n      summary: A tax payment has failed\n      description: >-\n        Fired when a payment fails during processing. Includes an error\n        code and description of the failure reason. The partner may\n        need to take corrective action and retry.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentFailedEvent'\n    PaymentCancelled:\n      name: payment.cancelled\n      title: Payment Cancelled\n  \
  \    summary: A tax payment has been cancelled\n      description: >-\n        Fired when a payment is cancelled either by the partner or by\n        the system due to expiration or other automated rules.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentEvent'\n  schemas:\n    PaymentEvent:\n      type: object\n      required:\n        - id\n        - type\n        - timestamp\n        - data\n      properties:\n        id:\n          type: string\n          description: Unique event identifier for idempotency\n        type:\n          type: string\n          description: Event type identifier\n          enum:\n            - payment.initiated\n            - payment.validated\n            - payment.confirmed\n            - payment.processing\n            - payment.completed\n            - payment.failed\n            - payment.cancelled\n        timestamp:\n          type: string\n          format: date-time\n          description: When the\
  \ event occurred\n        data:\n          type: object\n          properties:\n            paymentId:\n              type: string\n              description: Unique payment identifier\n            status:\n              type: string\n              description: Current payment status\n            amount:\n              type: number\n              format: double\n              description: Payment amount\n            currency:\n              type: string\n              description: Three-letter ISO 4217 currency code\n            taxType:\n              type: string\n              description: Type of tax being paid\n            taxPeriod:\n              type: string\n              description: Tax period for the payment\n            jurisdictionId:\n              type: string\n              description: Target tax jurisdiction identifier\n            accountId:\n              type: string\n              description: Client account identifier\n    PaymentCompletedEvent:\n      allOf:\n\
  \        - $ref: '#/components/schemas/PaymentEvent'\n        - type: object\n          properties:\n            data:\n              type: object\n              properties:\n                confirmationNumber:\n                  type: string\n                  description: >-\n                    Confirmation number issued by the tax authority\n                completedAt:\n                  type: string\n                  format: date-time\n                  description: Timestamp of successful completion\n    PaymentFailedEvent:\n      allOf:\n        - $ref: '#/components/schemas/PaymentEvent'\n        - type: object\n          properties:\n            data:\n              type: object\n              properties:\n                errorCode:\n                  type: string\n                  description: Machine-readable error code\n                errorMessage:\n                  type: string\n                  description: Human-readable failure description\n                retryable:\n\
  \                  type: boolean\n                  description: Whether the payment can be retried\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/remitian/refs/heads/main/asyncapi/remitian-tax-payment-asyncapi.yml
spec_file: asyncapi/remitian-tax-payment-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/remitian/refs/heads/main/asyncapi/remitian-tax-payment-asyncapi.yml
tags:
- Tax
- Payments
- Fintech
- Accounting
- Webhooks
- Embedded Payments
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
