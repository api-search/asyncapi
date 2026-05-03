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
- description: Receives delivery report callbacks for sent SMS and MMS messages. Reports can be summary or full depending on the delivery_report setting when sending the batch.
  name: /sms/delivery-report
  operation: publish
  operation_id: receiveDeliveryReport
  summary: Receive a delivery report
- description: Receives inbound SMS and MMS messages sent to your short codes or long numbers from mobile phones.
  name: /sms/incoming
  operation: publish
  operation_id: receiveIncomingSms
  summary: Receive an incoming SMS
description: Event-driven webhooks for the Sinch SMS API. The SMS API delivers delivery reports and inbound messages via HTTP POST callbacks to your configured webhook URL. Delivery reports notify you of the delivery status of sent messages, while inbound message callbacks deliver messages sent to your numbers by end users.
layout: asyncapi
messages:
- description: ''
  name: DeliveryReportSms
  summary: Batch-level delivery report for SMS messages
  title: SMS Delivery Report
- description: ''
  name: RecipientDeliveryReportSms
  summary: Per-recipient delivery report for an SMS message
  title: SMS Recipient Delivery Report
- description: ''
  name: DeliveryReportMms
  summary: Batch-level delivery report for MMS messages
  title: MMS Delivery Report
- description: ''
  name: RecipientDeliveryReportMms
  summary: Per-recipient delivery report for an MMS message
  title: MMS Recipient Delivery Report
- description: ''
  name: IncomingSms
  summary: An inbound SMS message from an end user
  title: Incoming SMS
- description: ''
  name: IncomingMms
  summary: An inbound MMS message from an end user
  title: Incoming MMS
name: Sinch SMS Webhooks
provider_name: Sinch
provider_slug: sinch
servers:
- description: Your server endpoint configured to receive SMS webhook callbacks. The URL is configured per batch or globally in the Sinch Dashboard.
  name: customerServer
  protocol: https
  url: '{callbackUrl}'
slug: sinch-sms-webhooks-asyncapi
source_filename: sinch-sms-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Sinch SMS Webhooks\n  description: >-\n    Event-driven webhooks for the Sinch SMS API. The SMS API delivers delivery\n    reports and inbound messages via HTTP POST callbacks to your configured\n    webhook URL. Delivery reports notify you of the delivery status of sent\n    messages, while inbound message callbacks deliver messages sent to your\n    numbers by end users.\n  version: '1.0'\n  contact:\n    name: Sinch Support\n    url: https://www.sinch.com/contact-us/\nservers:\n  customerServer:\n    url: '{callbackUrl}'\n    protocol: https\n    description: >-\n      Your server endpoint configured to receive SMS webhook callbacks.\n      The URL is configured per batch or globally in the Sinch Dashboard.\n    variables:\n      callbackUrl:\n        description: Your webhook endpoint URL\n    security:\n      - basicAuth: []\nchannels:\n  /sms/delivery-report:\n    description: >-\n      Receives delivery report callbacks for sent SMS and\
  \ MMS messages.\n      Reports can be summary or full depending on the delivery_report\n      setting when sending the batch.\n    publish:\n      operationId: receiveDeliveryReport\n      summary: Receive a delivery report\n      description: >-\n        Called when the delivery status of a batch or individual recipient\n        changes. The type field indicates whether this is a summary report\n        for the entire batch or a per-recipient report.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/DeliveryReportSms'\n          - $ref: '#/components/messages/RecipientDeliveryReportSms'\n          - $ref: '#/components/messages/DeliveryReportMms'\n          - $ref: '#/components/messages/RecipientDeliveryReportMms'\n  /sms/incoming:\n    description: >-\n      Receives inbound SMS and MMS messages sent to your short codes or\n      long numbers from mobile phones.\n    publish:\n      operationId: receiveIncomingSms\n      summary: Receive an incoming SMS\n   \
  \   description: >-\n        Called when an end user sends an SMS or MMS message to one of your\n        configured numbers. The callback URL must be configured in the\n        Sinch Dashboard.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/IncomingSms'\n          - $ref: '#/components/messages/IncomingMms'\ncomponents:\n  securitySchemes:\n    basicAuth:\n      type: httpBasicAuth\n      description: >-\n        Optional Basic Authentication for webhook callbacks. Custom headers\n        and OAuth 2.0 are also supported for callback authentication.\n  messages:\n    DeliveryReportSms:\n      name: delivery_report_sms\n      title: SMS Delivery Report\n      summary: Batch-level delivery report for SMS messages\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DeliveryReportSmsPayload'\n    RecipientDeliveryReportSms:\n      name: recipient_delivery_report_sms\n      title: SMS Recipient Delivery Report\n      summary:\
  \ Per-recipient delivery report for an SMS message\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/RecipientDeliveryReportPayload'\n    DeliveryReportMms:\n      name: delivery_report_mms\n      title: MMS Delivery Report\n      summary: Batch-level delivery report for MMS messages\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DeliveryReportMmsPayload'\n    RecipientDeliveryReportMms:\n      name: recipient_delivery_report_mms\n      title: MMS Recipient Delivery Report\n      summary: Per-recipient delivery report for an MMS message\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/RecipientDeliveryReportPayload'\n    IncomingSms:\n      name: incoming_sms\n      title: Incoming SMS\n      summary: An inbound SMS message from an end user\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/IncomingSmsPayload'\n    IncomingMms:\n\
  \      name: incoming_mms\n      title: Incoming MMS\n      summary: An inbound MMS message from an end user\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/IncomingMmsPayload'\n  schemas:\n    DeliveryReportSmsPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          enum:\n            - delivery_report_sms\n          description: The callback event type\n        batch_id:\n          type: string\n          description: The batch identifier\n        statuses:\n          type: array\n          description: Aggregate status counts\n          items:\n            type: object\n            properties:\n              code:\n                type: integer\n                description: The status code\n              status:\n                type: string\n                enum:\n                  - Queued\n                  - Dispatched\n                  - Delivered\n                  - Failed\n                  -\
  \ Expired\n                  - Cancelled\n                  - Rejected\n                description: The delivery status\n              count:\n                type: integer\n                description: Number of recipients with this status\n              recipients:\n                type: array\n                description: List of recipient numbers\n                items:\n                  type: string\n        total_message_count:\n          type: integer\n          description: Total number of messages in the batch\n    RecipientDeliveryReportPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          enum:\n            - recipient_delivery_report_sms\n            - recipient_delivery_report_mms\n          description: The callback event type\n        batch_id:\n          type: string\n          description: The batch identifier\n        recipient:\n          type: string\n          description: The recipient phone number\n        code:\n   \
  \       type: integer\n          description: The delivery status code\n        status:\n          type: string\n          description: The delivery status\n        at:\n          type: string\n          format: date-time\n          description: When the status was updated\n        operator_status_at:\n          type: string\n          format: date-time\n          description: When the operator reported the status\n        client_reference:\n          type: string\n          description: Client reference from the batch\n        applied_originator:\n          type: string\n          description: The originator used for the message\n        encoding:\n          type: string\n          description: The message encoding used\n    DeliveryReportMmsPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          enum:\n            - delivery_report_mms\n          description: The callback event type\n        batch_id:\n          type: string\n          description:\
  \ The batch identifier\n        statuses:\n          type: array\n          description: Aggregate status counts\n          items:\n            type: object\n            properties:\n              code:\n                type: integer\n                description: The status code\n              status:\n                type: string\n                description: The delivery status\n              count:\n                type: integer\n                description: Number of recipients with this status\n        total_message_count:\n          type: integer\n          description: Total number of messages in the batch\n    IncomingSmsPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          enum:\n            - mo_text\n          description: The callback event type\n        id:\n          type: string\n          description: The inbound message identifier\n        from:\n          type: string\n          description: The sender phone number\n       \
  \ to:\n          type: string\n          description: The destination number\n        body:\n          type: string\n          description: The message body text\n        received_at:\n          type: string\n          format: date-time\n          description: When the message was received\n        operator_id:\n          type: string\n          description: The mobile operator identifier\n        client_reference:\n          type: string\n          description: Client reference if applicable\n        sent_at:\n          type: string\n          format: date-time\n          description: When the message was sent\n    IncomingMmsPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          enum:\n            - mo_media\n          description: The callback event type\n        id:\n          type: string\n          description: The inbound message identifier\n        from:\n          type: string\n          description: The sender phone number\n        to:\n\
  \          type: string\n          description: The destination number\n        body:\n          type: object\n          description: The MMS message body with media\n          properties:\n            subject:\n              type: string\n              description: The MMS subject\n            message:\n              type: string\n              description: The text portion of the MMS\n        received_at:\n          type: string\n          format: date-time\n          description: When the message was received\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/asyncapi/sinch-sms-webhooks-asyncapi.yml
spec_file: asyncapi/sinch-sms-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/asyncapi/sinch-sms-webhooks-asyncapi.yml
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
