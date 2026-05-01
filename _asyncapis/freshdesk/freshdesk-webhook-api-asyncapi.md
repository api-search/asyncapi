---
api_specs:
- filename: freshdesk-rest-api-openapi.yml
  format: yaml
  label: Freshdesk REST API
  slug: rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/freshdesk/refs/heads/main/openapi/freshdesk-rest-api-openapi.yml
- filename: freshdesk-webhook-api-asyncapi.yml
  format: yaml
  label: Freshdesk Webhook API
  slug: webhook-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/freshdesk/refs/heads/main/asyncapi/freshdesk-webhook-api-asyncapi.yml
channels:
- description: Webhook endpoint that receives event payloads from Freshdesk automation rules. Freshdesk sends JSON-encoded HTTP POST requests to this endpoint when the configured automation rule conditions are met.
  name: /webhook
  operation: publish
  operation_id: receiveWebhookEvent
  summary: Receive a webhook event from Freshdesk
description: The Freshdesk Webhook API enables real-time communication between Freshdesk and external systems by sending HTTP POST requests when specific events occur within the helpdesk. Webhooks can be triggered by ticket creation, updates, status changes, agent assignments, and other support events through automation rules. This allows developers to build event-driven integrations without polling the REST API, useful for synchronizing Freshdesk data with CRM systems, triggering notifications in messaging platforms, or updating external dashboards in real time.
layout: asyncapi
messages:
- description: ''
  name: TicketCreated
  summary: Fired when a new ticket is created in Freshdesk.
  title: Ticket Created
- description: ''
  name: TicketUpdated
  summary: Fired when a ticket is updated, including status changes, priority changes, agent reassignments, and field modifications.
  title: Ticket Updated
- description: ''
  name: TicketDeleted
  summary: Fired when a ticket is deleted from the helpdesk.
  title: Ticket Deleted
- description: ''
  name: NoteAdded
  summary: Fired when a note is added to a ticket.
  title: Note Added
- description: ''
  name: ReplyReceived
  summary: Fired when a reply is received on a ticket.
  title: Reply Received
name: Freshdesk Webhook Events
provider_name: freshdesk
provider_slug: freshdesk
servers:
- description: Your external webhook endpoint that receives HTTP POST requests from Freshdesk automation rules.
  name: external
  protocol: https
  url: '{webhookUrl}'
slug: freshdesk-webhook-api-asyncapi
source_filename: freshdesk-webhook-api-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Freshdesk Webhook Events\n  description: >-\n    The Freshdesk Webhook API enables real-time communication between Freshdesk\n    and external systems by sending HTTP POST requests when specific events occur\n    within the helpdesk. Webhooks can be triggered by ticket creation, updates,\n    status changes, agent assignments, and other support events through\n    automation rules. This allows developers to build event-driven integrations\n    without polling the REST API, useful for synchronizing Freshdesk data with\n    CRM systems, triggering notifications in messaging platforms, or updating\n    external dashboards in real time.\n  version: '2.0'\n  contact:\n    name: Freshdesk Support\n    url: https://support.freshdesk.com/\n  license:\n    name: Proprietary\n  externalDocs:\n    description: Freshdesk Webhook Documentation\n    url: https://support.freshdesk.com/support/solutions/articles/132589-using-webhooks-in-automation-rules\nservers:\n\
  \  external:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your external webhook endpoint that receives HTTP POST requests from\n      Freshdesk automation rules.\n    variables:\n      webhookUrl:\n        description: >-\n          The URL of your webhook endpoint configured in the Freshdesk\n          automation rule.\n    security:\n      - httpBasic: []\nchannels:\n  /webhook:\n    description: >-\n      Webhook endpoint that receives event payloads from Freshdesk automation\n      rules. Freshdesk sends JSON-encoded HTTP POST requests to this endpoint\n      when the configured automation rule conditions are met.\n    publish:\n      operationId: receiveWebhookEvent\n      summary: Receive a webhook event from Freshdesk\n      description: >-\n        Freshdesk publishes event payloads to your configured webhook URL when\n        automation rule conditions are met. Events include ticket creation,\n        ticket updates, status changes, priority changes,\
  \ agent assignments,\n        and other helpdesk activities.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/TicketCreated'\n          - $ref: '#/components/messages/TicketUpdated'\n          - $ref: '#/components/messages/TicketDeleted'\n          - $ref: '#/components/messages/NoteAdded'\n          - $ref: '#/components/messages/ReplyReceived'\ncomponents:\n  securitySchemes:\n    httpBasic:\n      type: http\n      scheme: basic\n      description: >-\n        Freshdesk can send webhooks with HTTP Basic authentication credentials.\n        Configure the username and password in your automation rule webhook\n        action.\n  messages:\n    TicketCreated:\n      name: ticketCreated\n      title: Ticket Created\n      summary: >-\n        Fired when a new ticket is created in Freshdesk.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    TicketUpdated:\n      name: ticketUpdated\n      title: Ticket\
  \ Updated\n      summary: >-\n        Fired when a ticket is updated, including status changes, priority\n        changes, agent reassignments, and field modifications.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    TicketDeleted:\n      name: ticketDeleted\n      title: Ticket Deleted\n      summary: >-\n        Fired when a ticket is deleted from the helpdesk.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    NoteAdded:\n      name: noteAdded\n      title: Note Added\n      summary: >-\n        Fired when a note is added to a ticket.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    ReplyReceived:\n      name: replyReceived\n      title: Reply Received\n      summary: >-\n        Fired when a reply is received on a ticket.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n\
  \  schemas:\n    WebhookPayload:\n      type: object\n      description: >-\n        The webhook payload sent by Freshdesk automation rules. The structure\n        depends on whether Simple or Advanced content mode is selected in the\n        automation rule. In Simple mode, Freshdesk sends a predefined set of\n        ticket fields. In Advanced mode, you can customize the JSON payload\n        using placeholders.\n      properties:\n        freshdesk_webhook:\n          type: object\n          description: >-\n            Container object for the webhook data. Present when using the\n            Simple content format.\n          properties:\n            ticket_id:\n              type: integer\n              format: int64\n              description: >-\n                Unique identifier of the ticket that triggered the event.\n            ticket_url:\n              type: string\n              format: uri\n              description: >-\n                URL to view the ticket in the Freshdesk\
  \ portal.\n            ticket_subject:\n              type: string\n              description: >-\n                Subject line of the ticket.\n            ticket_description:\n              type: string\n              description: >-\n                Description or body of the ticket in text format.\n            ticket_status:\n              type: string\n              description: >-\n                Current status of the ticket, e.g. Open, Pending, Resolved,\n                Closed.\n            ticket_priority:\n              type: string\n              description: >-\n                Current priority of the ticket, e.g. Low, Medium, High, Urgent.\n            ticket_source:\n              type: string\n              description: >-\n                Channel through which the ticket was created, e.g. Email,\n                Portal, Phone, Chat.\n            ticket_type:\n              type: string\n              nullable: true\n              description: >-\n                Type of\
  \ the ticket, e.g. Question, Incident, Problem.\n            ticket_due_by_time:\n              type: string\n              format: date-time\n              description: >-\n                Timestamp when the ticket resolution is due.\n            ticket_tags:\n              type: string\n              description: >-\n                Comma-separated list of tags on the ticket.\n            ticket_requester_name:\n              type: string\n              description: >-\n                Name of the contact who raised the ticket.\n            ticket_requester_email:\n              type: string\n              format: email\n              description: >-\n                Email of the contact who raised the ticket.\n            ticket_requester_phone:\n              type: string\n              nullable: true\n              description: >-\n                Phone number of the requester.\n            ticket_agent_name:\n              type: string\n              nullable: true\n            \
  \  description: >-\n                Name of the agent assigned to the ticket.\n            ticket_agent_email:\n              type: string\n              format: email\n              nullable: true\n              description: >-\n                Email of the agent assigned to the ticket.\n            ticket_group_name:\n              type: string\n              nullable: true\n              description: >-\n                Name of the group the ticket is assigned to.\n            ticket_company_name:\n              type: string\n              nullable: true\n              description: >-\n                Name of the company associated with the ticket.\n            ticket_product_name:\n              type: string\n              nullable: true\n              description: >-\n                Name of the product associated with the ticket.\n            ticket_latest_public_comment:\n              type: string\n              nullable: true\n              description: >-\n                The\
  \ most recent public reply or comment on the ticket.\n            ticket_created_at:\n              type: string\n              format: date-time\n              description: >-\n                Timestamp when the ticket was created.\n            ticket_updated_at:\n              type: string\n              format: date-time\n              description: >-\n                Timestamp when the ticket was last updated.\n    ExternalEventPayload:\n      type: object\n      description: >-\n        Payload structure used by the Freshdesk App SDK external events feature.\n        When an external product sends webhook data to the app framework target\n        URL, this structure wraps the event data and passes it to the serverless\n        app callback.\n      properties:\n        account_id:\n          type: string\n          description: >-\n            Identifier of the Freshdesk account, auto-generated when the\n            account is configured.\n        domain:\n          type: string\n\
  \          description: >-\n            Domain name for the Freshdesk account, e.g. acme.freshdesk.com.\n        event:\n          type: string\n          description: >-\n            Name of the event that triggered the webhook.\n        timestamp:\n          type: integer\n          format: int64\n          description: >-\n            When the external event occurred, in Unix epoch format.\n        region:\n          type: string\n          description: >-\n            Data center region of the Freshdesk account.\n        headers:\n          type: object\n          additionalProperties:\n            type: string\n          description: >-\n            HTTP headers associated with the incoming webhook request.\n        data:\n          type: object\n          additionalProperties: true\n          description: >-\n            Event-specific data passed by the external product as key-value\n            pairs.\n        iparams:\n          type: object\n          additionalProperties: true\n\
  \          description: >-\n            Installation parameters configured for the app.\n        app_settings:\n          type: object\n          additionalProperties: true\n          description: >-\n            Application settings configured for the Freshdesk account.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/freshdesk/refs/heads/main/asyncapi/freshdesk-webhook-api-asyncapi.yml
spec_file: asyncapi/freshdesk-webhook-api-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/freshdesk/refs/heads/main/asyncapi/freshdesk-webhook-api-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '2.0'
---
