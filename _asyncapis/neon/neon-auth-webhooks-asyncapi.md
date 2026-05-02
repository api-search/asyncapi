---
api_specs:
- filename: neon-management-api-openapi.yml
  format: yaml
  label: Neon Management API
  slug: management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/neon/refs/heads/main/openapi/neon-management-api-openapi.yml
- filename: neon-auth-webhooks-asyncapi.yml
  format: yaml
  label: Neon Auth
  slug: auth
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/neon/refs/heads/main/asyncapi/neon-auth-webhooks-asyncapi.yml
channels:
- description: Neon Auth sends webhook events to your configured endpoint as HTTP POST requests with JSON payloads. Each event includes a type field identifying the event and relevant data. Your endpoint should respond with a 2xx status code to acknowledge receipt.
  name: /webhook
  operation: publish
  operation_id: receiveAuthWebhookEvent
  summary: Receive authentication webhook events
description: Neon Auth webhooks deliver HTTP POST requests when authentication events occur, including OTP delivery, magic link delivery, and user creation. Webhooks can be used to replace built-in email delivery with custom channels (SMS, custom email, WhatsApp), validate signups before they complete, or sync new users to CRMs and analytics systems.
layout: asyncapi
messages:
- description: This event fires when Neon Auth generates a one-time password that needs to be delivered to a user. Use this webhook to send the OTP via your own delivery channel such as SMS, custom email template, or WhatsApp instead of the default built-in email.
  name: OtpDeliveryEvent
  summary: Sent when an OTP code needs to be delivered to a user for email verification or two-factor authentication.
  title: OTP Delivery Event
- description: This event fires when Neon Auth generates a magic link for passwordless sign-in. Use this webhook to deliver the magic link via your own email service or messaging channel instead of the default built-in delivery.
  name: MagicLinkDeliveryEvent
  summary: Sent when a magic link needs to be delivered to a user for passwordless authentication.
  title: Magic Link Delivery Event
- description: This event fires after a new user successfully registers through Neon Auth. Use this webhook to sync the new user to your CRM, analytics platform, or other downstream systems, or to perform additional onboarding tasks.
  name: UserCreatedEvent
  summary: Sent when a new user account is created through Neon Auth.
  title: User Created Event
name: Neon Auth Webhook Events
provider_name: Neon
provider_slug: neon
servers:
- description: Your webhook receiver endpoint configured in Neon Auth settings. Neon sends HTTP POST requests to this URL when authentication events occur.
  name: webhookReceiver
  protocol: https
  url: '{webhookUrl}'
slug: neon-auth-webhooks-asyncapi
source_filename: neon-auth-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Neon Auth Webhook Events\n  description: >-\n    Neon Auth webhooks deliver HTTP POST requests when authentication events\n    occur, including OTP delivery, magic link delivery, and user creation.\n    Webhooks can be used to replace built-in email delivery with custom\n    channels (SMS, custom email, WhatsApp), validate signups before they\n    complete, or sync new users to CRMs and analytics systems.\n  version: '1.0'\n  contact:\n    name: Neon Support\n    url: https://neon.com/docs/introduction/support\n  license:\n    name: Proprietary\n    url: https://neon.com/terms-of-service\nservers:\n  webhookReceiver:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your webhook receiver endpoint configured in Neon Auth settings.\n      Neon sends HTTP POST requests to this URL when authentication\n      events occur.\n    variables:\n      webhookUrl:\n        description: The URL of your webhook endpoint\n    security:\n\
  \      - signatureVerification: []\nchannels:\n  /webhook:\n    description: >-\n      Neon Auth sends webhook events to your configured endpoint as HTTP POST\n      requests with JSON payloads. Each event includes a type field identifying\n      the event and relevant data. Your endpoint should respond with a 2xx\n      status code to acknowledge receipt.\n    publish:\n      operationId: receiveAuthWebhookEvent\n      summary: Receive authentication webhook events\n      description: >-\n        Receives webhook events from Neon Auth when authentication-related\n        actions occur. Events include OTP code delivery, magic link delivery,\n        and user creation. Your server must respond with a 2xx status code\n        within a reasonable timeframe. Failed deliveries will be retried.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/OtpDeliveryEvent'\n          - $ref: '#/components/messages/MagicLinkDeliveryEvent'\n          - $ref: '#/components/messages/UserCreatedEvent'\n\
  components:\n  securitySchemes:\n    signatureVerification:\n      type: httpApiKey\n      name: x-webhook-signature\n      in: header\n      description: >-\n        Webhook signature for verifying the authenticity of webhook payloads.\n        Verify this signature against the payload using your webhook secret\n        to ensure the request originated from Neon Auth.\n  messages:\n    OtpDeliveryEvent:\n      name: otpDelivery\n      title: OTP Delivery Event\n      summary: >-\n        Sent when an OTP code needs to be delivered to a user for email\n        verification or two-factor authentication.\n      description: >-\n        This event fires when Neon Auth generates a one-time password that\n        needs to be delivered to a user. Use this webhook to send the OTP\n        via your own delivery channel such as SMS, custom email template,\n        or WhatsApp instead of the default built-in email.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OtpDeliveryPayload'\n\
  \    MagicLinkDeliveryEvent:\n      name: magicLinkDelivery\n      title: Magic Link Delivery Event\n      summary: >-\n        Sent when a magic link needs to be delivered to a user for\n        passwordless authentication.\n      description: >-\n        This event fires when Neon Auth generates a magic link for\n        passwordless sign-in. Use this webhook to deliver the magic link\n        via your own email service or messaging channel instead of the\n        default built-in delivery.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/MagicLinkDeliveryPayload'\n    UserCreatedEvent:\n      name: userCreated\n      title: User Created Event\n      summary: >-\n        Sent when a new user account is created through Neon Auth.\n      description: >-\n        This event fires after a new user successfully registers through\n        Neon Auth. Use this webhook to sync the new user to your CRM,\n        analytics platform, or other downstream systems,\
  \ or to perform\n        additional onboarding tasks.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/UserCreatedPayload'\n  schemas:\n    OtpDeliveryPayload:\n      type: object\n      description: >-\n        Payload for OTP delivery webhook events containing the OTP code\n        and recipient information.\n      required:\n        - type\n        - email\n        - otp\n      properties:\n        type:\n          type: string\n          const: otp_delivery\n          description: The event type identifier\n        email:\n          type: string\n          format: email\n          description: The email address of the user receiving the OTP\n        otp:\n          type: string\n          description: >-\n            The one-time password code to be delivered to the user\n        expires_at:\n          type: string\n          format: date-time\n          description: The expiration time for the OTP code\n        user_id:\n          type: string\n\
  \          description: The ID of the user associated with this OTP request\n    MagicLinkDeliveryPayload:\n      type: object\n      description: >-\n        Payload for magic link delivery webhook events containing the\n        magic link URL and recipient information.\n      required:\n        - type\n        - email\n        - url\n      properties:\n        type:\n          type: string\n          const: magic_link_delivery\n          description: The event type identifier\n        email:\n          type: string\n          format: email\n          description: The email address of the user receiving the magic link\n        url:\n          type: string\n          format: uri\n          description: >-\n            The magic link URL that the user should click to authenticate\n        token:\n          type: string\n          description: The magic link token\n        expires_at:\n          type: string\n          format: date-time\n          description: The expiration time for the\
  \ magic link\n        user_id:\n          type: string\n          description: The ID of the user associated with this magic link request\n    UserCreatedPayload:\n      type: object\n      description: >-\n        Payload for user created webhook events containing the new user\n        information.\n      required:\n        - type\n        - user\n      properties:\n        type:\n          type: string\n          const: user_created\n          description: The event type identifier\n        user:\n          type: object\n          description: The newly created user object\n          properties:\n            id:\n              type: string\n              description: The unique user ID\n            email:\n              type: string\n              format: email\n              description: The user email address\n            name:\n              type: string\n              description: The user display name\n            image:\n              type: string\n              format: uri\n \
  \             description: The user avatar image URL\n            email_verified:\n              type: boolean\n              description: Whether the email has been verified\n            created_at:\n              type: string\n              format: date-time\n              description: User creation timestamp\n            updated_at:\n              type: string\n              format: date-time\n              description: Last update timestamp\n        timestamp:\n          type: string\n          format: date-time\n          description: The time the event occurred\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/neon/refs/heads/main/asyncapi/neon-auth-webhooks-asyncapi.yml
spec_file: asyncapi/neon-auth-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/neon/refs/heads/main/asyncapi/neon-auth-webhooks-asyncapi.yml
tags:
- Databases
- Serverless
- Postgres
- Infrastructure
- Authentication
- Edge
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
