---
api_specs:
- filename: sinch-sms-openapi.yml
  format: yaml
  label: Sinch SMS API
  slug: sms-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-sms-openapi.yml
- filename: sinch-conversation-openapi.yml
  format: yaml
  label: Sinch Conversation API
  slug: conversation-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-conversation-openapi.yml
- filename: sinch-voice-openapi.yml
  format: yaml
  label: Sinch Voice API
  slug: voice-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-voice-openapi.yml
- filename: sinch-verification-openapi.yml
  format: yaml
  label: Sinch Verification API
  slug: verification-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-verification-openapi.yml
- filename: sinch-numbers-openapi.yml
  format: yaml
  label: Sinch Numbers API
  slug: numbers-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-numbers-openapi.yml
- filename: sinch-fax-openapi.yml
  format: yaml
  label: Sinch Fax API
  slug: fax-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-fax-openapi.yml
- filename: sinch-elastic-sip-trunking-openapi.yml
  format: yaml
  label: Sinch Elastic SIP Trunking API
  slug: elastic-sip-trunking-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-elastic-sip-trunking-openapi.yml
- filename: sinch-brands-openapi.yml
  format: yaml
  label: Sinch Brands API
  slug: brands-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-brands-openapi.yml
- filename: sinch-provisioning-openapi.yml
  format: yaml
  label: Sinch Provisioning API
  slug: provisioning-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-provisioning-openapi.yml
- filename: sinch-registration-openapi.yml
  format: yaml
  label: Sinch Registration API
  slug: registration-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-registration-openapi.yml
channels:
- description: Receives verification request events when a new verification is initiated. Your response can allow or deny the verification and override the verification method.
  name: /verification/request
  operation: publish
  operation_id: receiveVerificationRequest
  summary: Receive a verification request event
- description: Receives verification result events when a verification is completed, either successfully or with a failure.
  name: /verification/result
  operation: publish
  operation_id: receiveVerificationResult
  summary: Receive a verification result event
description: Event-driven callbacks for the Sinch Verification API. The Verification API sends HTTP POST callbacks to your application during the verification lifecycle. These include verification request events when a verification is initiated and verification result events when a verification is completed or fails.
layout: asyncapi
messages:
- description: ''
  name: VerificationRequestEvent
  summary: A new verification has been initiated
  title: Verification Request Event
- description: ''
  name: VerificationResultEvent
  summary: A verification has reached a terminal state
  title: Verification Result Event
name: Sinch Verification Callbacks
provider_name: Sinch
provider_slug: sinch
servers:
- description: Your server endpoint configured to receive Verification API callbacks. The callback URL is configured per application.
  name: customerServer
  protocol: https
  url: '{callbackUrl}'
slug: sinch-verification-callbacks-asyncapi
source_filename: sinch-verification-callbacks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Sinch Verification Callbacks\n  description: >-\n    Event-driven callbacks for the Sinch Verification API. The Verification API\n    sends HTTP POST callbacks to your application during the verification\n    lifecycle. These include verification request events when a verification\n    is initiated and verification result events when a verification is\n    completed or fails.\n  version: '1.0'\n  contact:\n    name: Sinch Support\n    url: https://www.sinch.com/contact-us/\nservers:\n  customerServer:\n    url: '{callbackUrl}'\n    protocol: https\n    description: >-\n      Your server endpoint configured to receive Verification API callbacks.\n      The callback URL is configured per application.\n    variables:\n      callbackUrl:\n        description: Your callback endpoint URL\nchannels:\n  /verification/request:\n    description: >-\n      Receives verification request events when a new verification is\n      initiated. Your response can\
  \ allow or deny the verification and\n      override the verification method.\n    publish:\n      operationId: receiveVerificationRequest\n      summary: Receive a verification request event\n      description: >-\n        Triggered when a new verification is initiated via the SDK or API.\n        Your response determines whether the verification proceeds and can\n        override the method (SMS, flashcall, callout).\n      message:\n        $ref: '#/components/messages/VerificationRequestEvent'\n  /verification/result:\n    description: >-\n      Receives verification result events when a verification is completed,\n      either successfully or with a failure.\n    publish:\n      operationId: receiveVerificationResult\n      summary: Receive a verification result event\n      description: >-\n        Triggered when a verification reaches a terminal state, either\n        successful, failed, or denied. Includes the verification method\n        and identity details.\n      message:\n\
  \        $ref: '#/components/messages/VerificationResultEvent'\ncomponents:\n  messages:\n    VerificationRequestEvent:\n      name: VerificationRequestEvent\n      title: Verification Request Event\n      summary: A new verification has been initiated\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/VerificationRequestPayload'\n    VerificationResultEvent:\n      name: VerificationResultEvent\n      title: Verification Result Event\n      summary: A verification has reached a terminal state\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/VerificationResultPayload'\n  schemas:\n    VerificationRequestPayload:\n      type: object\n      properties:\n        id:\n          type: string\n          description: The verification request identifier\n        event:\n          type: string\n          enum:\n            - VerificationRequestEvent\n          description: The event type\n        method:\n         \
  \ type: string\n          enum:\n            - sms\n            - flashcall\n            - callout\n            - seamless\n          description: The requested verification method\n        identity:\n          type: object\n          description: The identity being verified\n          properties:\n            type:\n              type: string\n              description: The identity type\n            endpoint:\n              type: string\n              description: The phone number in E.164 format\n        reference:\n          type: string\n          description: Custom reference string if provided\n        custom:\n          type: string\n          description: Custom data if provided\n        price:\n          type: object\n          description: The verification price\n          properties:\n            currencyId:\n              type: string\n              description: Currency code\n            amount:\n              type: number\n              description: Price amount\n      \
  \  acceptLanguage:\n          type: array\n          description: Accepted languages from the SDK\n          items:\n            type: string\n    VerificationResultPayload:\n      type: object\n      properties:\n        id:\n          type: string\n          description: The verification request identifier\n        event:\n          type: string\n          enum:\n            - VerificationResultEvent\n          description: The event type\n        method:\n          type: string\n          enum:\n            - sms\n            - flashcall\n            - callout\n            - seamless\n          description: The verification method used\n        identity:\n          type: object\n          description: The verified identity\n          properties:\n            type:\n              type: string\n              description: The identity type\n            endpoint:\n              type: string\n              description: The phone number\n        status:\n          type: string\n         \
  \ enum:\n            - SUCCESSFUL\n            - FAIL\n            - DENIED\n            - ERROR\n          description: The verification result\n        reason:\n          type: string\n          description: The reason for the result\n        reference:\n          type: string\n          description: Custom reference string\n        source:\n          type: string\n          enum:\n            - intercepted\n            - manual\n          description: How the code was reported\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/asyncapi/sinch-verification-callbacks-asyncapi.yml
spec_file: asyncapi/sinch-verification-callbacks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/asyncapi/sinch-verification-callbacks-asyncapi.yml
tags:
- Communications
- Messaging
- SMS
- Voice
- Verification
- CPaaS
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
