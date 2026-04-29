---
api_specs:
- filename: coinbase-advanced-trade-openapi.yml
  format: yaml
  label: Coinbase Advanced Trade API
  slug: advanced-trade-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/openapi/coinbase-advanced-trade-openapi.yml
- filename: coinbase-exchange-openapi.yml
  format: yaml
  label: Coinbase Exchange API
  slug: exchange-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/openapi/coinbase-exchange-openapi.yml
- filename: coinbase-prime-openapi.yml
  format: yaml
  label: Coinbase Prime API
  slug: prime-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/openapi/coinbase-prime-openapi.yml
- filename: coinbase-onramp-openapi.yml
  format: yaml
  label: Coinbase Onramp API
  slug: onramp-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/openapi/coinbase-onramp-openapi.yml
- filename: coinbase-commerce-openapi.yml
  format: yaml
  label: Coinbase Commerce API
  slug: commerce-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/openapi/coinbase-commerce-openapi.yml
channels:
- description: Webhook endpoint that receives Commerce event notifications. All events are delivered as HTTPS POST requests with a JSON payload and X-CC-Webhook-Signature header for verification.
  name: /webhook
  operation: publish
  operation_id: receiveCommerceWebhook
  summary: Receive Commerce webhook events
description: Coinbase Commerce sends webhook events to notify your application when charges are created, confirmed, delayed, pending, failed, or resolved. Each webhook event is signed with a SHA-256 HMAC signature using your webhook shared secret, included in the X-CC-Webhook-Signature header. Webhooks are delivered via HTTPS POST to your configured endpoint URL.
layout: asyncapi
messages:
- description: ''
  name: ChargeCreatedEvent
  summary: Fired when a new charge is created
  title: Charge Created
- description: ''
  name: ChargeConfirmedEvent
  summary: Fired when a charge receives sufficient blockchain confirmations
  title: Charge Confirmed
- description: ''
  name: ChargeFailedEvent
  summary: Fired when a charge expires without receiving payment
  title: Charge Failed
- description: ''
  name: ChargeDelayedEvent
  summary: Fired when a charge payment is detected but awaiting confirmations
  title: Charge Delayed
- description: ''
  name: ChargePendingEvent
  summary: Fired when a charge payment is pending
  title: Charge Pending
- description: ''
  name: ChargeResolvedEvent
  summary: Fired when an unresolved charge is manually resolved
  title: Charge Resolved
name: Coinbase Commerce Webhooks
provider_name: Coinbase
provider_slug: coinbase
servers:
- description: Your HTTPS endpoint that receives webhook notifications from Coinbase Commerce. Configure this URL in the Commerce Settings page.
  name: webhookReceiver
  protocol: https
  url: '{webhookUrl}'
slug: coinbase-commerce-webhooks-asyncapi
source_filename: coinbase-commerce-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Coinbase Commerce Webhooks\n  description: >-\n    Coinbase Commerce sends webhook events to notify your application when\n    charges are created, confirmed, delayed, pending, failed, or resolved.\n    Each webhook event is signed with a SHA-256 HMAC signature using your\n    webhook shared secret, included in the X-CC-Webhook-Signature header.\n    Webhooks are delivered via HTTPS POST to your configured endpoint URL.\n  version: '1.0'\n  contact:\n    name: Coinbase Commerce Support\n    url: https://help.coinbase.com/en/commerce\nexternalDocs:\n  description: Commerce Webhooks Documentation\n  url: https://docs.cdp.coinbase.com/commerce-onchain/docs/webhooks\nservers:\n  webhookReceiver:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your HTTPS endpoint that receives webhook notifications from Coinbase\n      Commerce. Configure this URL in the Commerce Settings page.\n    variables:\n      webhookUrl:\n      \
  \  description: Your webhook endpoint URL\nchannels:\n  /webhook:\n    description: >-\n      Webhook endpoint that receives Commerce event notifications. All\n      events are delivered as HTTPS POST requests with a JSON payload and\n      X-CC-Webhook-Signature header for verification.\n    publish:\n      operationId: receiveCommerceWebhook\n      summary: Receive Commerce webhook events\n      message:\n        oneOf:\n          - $ref: '#/components/messages/ChargeCreatedEvent'\n          - $ref: '#/components/messages/ChargeConfirmedEvent'\n          - $ref: '#/components/messages/ChargeFailedEvent'\n          - $ref: '#/components/messages/ChargeDelayedEvent'\n          - $ref: '#/components/messages/ChargePendingEvent'\n          - $ref: '#/components/messages/ChargeResolvedEvent'\ncomponents:\n  messages:\n    ChargeCreatedEvent:\n      name: charge:created\n      title: Charge Created\n      summary: Fired when a new charge is created\n      contentType: application/json\n  \
  \    payload:\n        $ref: '#/components/schemas/WebhookEvent'\n      headers:\n        type: object\n        properties:\n          X-CC-Webhook-Signature:\n            type: string\n            description: SHA-256 HMAC signature of the raw request payload\n    ChargeConfirmedEvent:\n      name: charge:confirmed\n      title: Charge Confirmed\n      summary: Fired when a charge receives sufficient blockchain confirmations\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookEvent'\n      headers:\n        type: object\n        properties:\n          X-CC-Webhook-Signature:\n            type: string\n            description: SHA-256 HMAC signature of the raw request payload\n    ChargeFailedEvent:\n      name: charge:failed\n      title: Charge Failed\n      summary: Fired when a charge expires without receiving payment\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookEvent'\n      headers:\n\
  \        type: object\n        properties:\n          X-CC-Webhook-Signature:\n            type: string\n            description: SHA-256 HMAC signature of the raw request payload\n    ChargeDelayedEvent:\n      name: charge:delayed\n      title: Charge Delayed\n      summary: Fired when a charge payment is detected but awaiting confirmations\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookEvent'\n      headers:\n        type: object\n        properties:\n          X-CC-Webhook-Signature:\n            type: string\n            description: SHA-256 HMAC signature of the raw request payload\n    ChargePendingEvent:\n      name: charge:pending\n      title: Charge Pending\n      summary: Fired when a charge payment is pending\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookEvent'\n      headers:\n        type: object\n        properties:\n          X-CC-Webhook-Signature:\n            type: string\n\
  \            description: SHA-256 HMAC signature of the raw request payload\n    ChargeResolvedEvent:\n      name: charge:resolved\n      title: Charge Resolved\n      summary: Fired when an unresolved charge is manually resolved\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookEvent'\n      headers:\n        type: object\n        properties:\n          X-CC-Webhook-Signature:\n            type: string\n            description: SHA-256 HMAC signature of the raw request payload\n  schemas:\n    WebhookEvent:\n      type: object\n      description: Webhook event payload delivered to your endpoint\n      properties:\n        id:\n          type: string\n          description: Unique event identifier\n        resource:\n          type: string\n          description: Resource type\n          enum:\n            - event\n        type:\n          type: string\n          description: Event type\n          enum:\n            - charge:created\n    \
  \        - charge:confirmed\n            - charge:failed\n            - charge:delayed\n            - charge:pending\n            - charge:resolved\n        api_version:\n          type: string\n          description: API version that generated the event\n        created_at:\n          type: string\n          format: date-time\n          description: When the event was created\n        data:\n          $ref: '#/components/schemas/ChargeData'\n    ChargeData:\n      type: object\n      description: Charge data included in webhook events\n      properties:\n        id:\n          type: string\n          description: Charge identifier\n        code:\n          type: string\n          description: Charge code\n        name:\n          type: string\n          description: Charge name\n        description:\n          type: string\n          description: Charge description\n        hosted_url:\n          type: string\n          format: uri\n          description: Hosted payment page URL\n   \
  \     created_at:\n          type: string\n          format: date-time\n          description: Creation time\n        expires_at:\n          type: string\n          format: date-time\n          description: Expiration time\n        confirmed_at:\n          type: string\n          format: date-time\n          description: Confirmation time\n        pricing:\n          type: object\n          description: Pricing in various currencies\n          additionalProperties:\n            type: object\n            properties:\n              amount:\n                type: string\n                description: Amount\n              currency:\n                type: string\n                description: Currency code\n        pricing_type:\n          type: string\n          description: Pricing model\n          enum:\n            - no_price\n            - fixed_price\n        addresses:\n          type: object\n          description: Payment blockchain addresses\n          additionalProperties:\n     \
  \       type: string\n        payments:\n          type: array\n          description: Payments received\n          items:\n            type: object\n            properties:\n              network:\n                type: string\n                description: Blockchain network\n              transaction_id:\n                type: string\n                description: Transaction hash\n              status:\n                type: string\n                description: Payment status\n              value:\n                type: object\n                properties:\n                  amount:\n                    type: string\n                    description: Amount\n                  currency:\n                    type: string\n                    description: Currency\n        timeline:\n          type: array\n          description: Status change timeline\n          items:\n            type: object\n            properties:\n              time:\n                type: string\n                format:\
  \ date-time\n                description: Time of status change\n              status:\n                type: string\n                description: Status at this point\n        metadata:\n          type: object\n          description: Custom metadata\n          additionalProperties:\n            type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/asyncapi/coinbase-commerce-webhooks-asyncapi.yml
spec_file: asyncapi/coinbase-commerce-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/coinbase/refs/heads/main/asyncapi/coinbase-commerce-webhooks-asyncapi.yml
tags:
- Blockchain
- Cryptocurrency
- Custody
- Exchange
- Onramp
- Payments
- Trading
- Wallet
- Web3
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
