---
api_specs:
- filename: freshworks-freshdesk-api-openapi.yml
  format: yaml
  label: Freshworks Freshdesk API
  slug: freshdesk-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/freshworks/refs/heads/main/openapi/freshworks-freshdesk-api-openapi.yml
- filename: freshworks-freshservice-api-openapi.yml
  format: yaml
  label: Freshworks Freshservice API
  slug: freshservice-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/freshworks/refs/heads/main/openapi/freshworks-freshservice-api-openapi.yml
- filename: freshworks-freshsales-api-openapi.yml
  format: yaml
  label: Freshworks Freshsales API
  slug: freshsales-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/freshworks/refs/heads/main/openapi/freshworks-freshsales-api-openapi.yml
- filename: freshworks-freshchat-api-openapi.yml
  format: yaml
  label: Freshworks Freshchat API
  slug: freshchat-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/freshworks/refs/heads/main/openapi/freshworks-freshchat-api-openapi.yml
- filename: freshworks-freshcaller-api-openapi.yml
  format: yaml
  label: Freshworks Freshcaller API
  slug: freshcaller-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/freshworks/refs/heads/main/openapi/freshworks-freshcaller-api-openapi.yml
- filename: freshworks-freshteam-api-openapi.yml
  format: yaml
  label: Freshworks Freshteam API
  slug: freshteam-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/freshworks/refs/heads/main/openapi/freshworks-freshteam-api-openapi.yml
channels:
- description: Triggered when a new ticket is created in Freshdesk. Configured through ticket creation automation rules.
  name: /freshdesk/ticket-created
  operation: publish
  operation_id: onFreshdeskTicketCreated
  summary: Freshdesk ticket created event
- description: Triggered when an existing ticket is updated in Freshdesk. This includes status changes, assignment changes, priority updates, and custom field modifications.
  name: /freshdesk/ticket-updated
  operation: publish
  operation_id: onFreshdeskTicketUpdated
  summary: Freshdesk ticket updated event
- description: Triggered when a new ticket is created in Freshservice. Configured through the Workflow Automator.
  name: /freshservice/ticket-created
  operation: publish
  operation_id: onFreshserviceTicketCreated
  summary: Freshservice ticket created event
- description: Triggered when an existing ticket is updated in Freshservice, including status changes, assignment updates, and field modifications.
  name: /freshservice/ticket-updated
  operation: publish
  operation_id: onFreshserviceTicketUpdated
  summary: Freshservice ticket updated event
- description: Triggered when a new message is sent in a Freshchat conversation, whether by a user, agent, or bot.
  name: /freshchat/message-create
  operation: publish
  operation_id: onFreshchatMessageCreate
  summary: Freshchat message created event
- description: Triggered when a conversation is assigned or reassigned to an agent or group in Freshchat.
  name: /freshchat/conversation-assignment
  operation: publish
  operation_id: onFreshchatConversationAssignment
  summary: Freshchat conversation assignment event
- description: Triggered when a conversation is resolved in Freshchat.
  name: /freshchat/conversation-resolution
  operation: publish
  operation_id: onFreshchatConversationResolution
  summary: Freshchat conversation resolution event
- description: Triggered when a previously resolved conversation is reopened in Freshchat.
  name: /freshchat/conversation-reopen
  operation: publish
  operation_id: onFreshchatConversationReopen
  summary: Freshchat conversation reopen event
description: Freshworks products support webhook callbacks that notify external applications when specific events occur within the helpdesk, service desk, CRM, and messaging platforms. Webhooks are configured through automation rules and workflow automators, triggering HTTP POST requests to registered callback URLs when events such as ticket creation, conversation updates, and status changes occur. Rate limits of 1000 webhook requests per hour apply across all Freshworks products.
layout: asyncapi
messages:
- description: ''
  name: FreshdeskTicketEvent
  summary: Payload sent by Freshdesk when a ticket event occurs via automation rule webhooks.
  title: Freshdesk Ticket Webhook Event
- description: ''
  name: FreshserviceTicketEvent
  summary: Payload sent by Freshservice when a ticket event occurs via the Workflow Automator.
  title: Freshservice Ticket Webhook Event
- description: ''
  name: FreshchatMessageEvent
  summary: Payload sent by Freshchat when a new message is created in a conversation.
  title: Freshchat Message Webhook Event
- description: ''
  name: FreshchatConversationEvent
  summary: Payload sent by Freshchat when a conversation lifecycle event occurs such as assignment, resolution, or reopening.
  title: Freshchat Conversation Webhook Event
name: Freshworks Webhook Events
provider_name: freshworks
provider_slug: freshworks
servers:
- description: Freshdesk sends webhook POST requests to the callback URL configured in automation rules. The URL is set by the customer.
  name: freshdeskWebhook
  protocol: https
  url: '{callbackUrl}'
- description: Freshservice sends webhook POST requests to the callback URL configured in the Workflow Automator.
  name: freshserviceWebhook
  protocol: https
  url: '{callbackUrl}'
- description: Freshchat sends webhook POST requests to the registered callback URL when messaging events occur.
  name: freshchatWebhook
  protocol: https
  url: '{callbackUrl}'
slug: freshworks-webhooks-asyncapi
source_filename: freshworks-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Freshworks Webhook Events\n  description: >-\n    Freshworks products support webhook callbacks that notify external\n    applications when specific events occur within the helpdesk, service\n    desk, CRM, and messaging platforms. Webhooks are configured through\n    automation rules and workflow automators, triggering HTTP POST requests\n    to registered callback URLs when events such as ticket creation,\n    conversation updates, and status changes occur. Rate limits of 1000\n    webhook requests per hour apply across all Freshworks products.\n  version: '1.0'\n  contact:\n    name: Freshworks Support\n    url: https://support.freshworks.com/\n  license:\n    name: Proprietary\nservers:\n  freshdeskWebhook:\n    url: '{callbackUrl}'\n    protocol: https\n    description: >-\n      Freshdesk sends webhook POST requests to the callback URL configured\n      in automation rules. The URL is set by the customer.\n    variables:\n      callbackUrl:\n\
  \        description: The customer-configured webhook callback URL.\n  freshserviceWebhook:\n    url: '{callbackUrl}'\n    protocol: https\n    description: >-\n      Freshservice sends webhook POST requests to the callback URL\n      configured in the Workflow Automator.\n    variables:\n      callbackUrl:\n        description: The customer-configured webhook callback URL.\n  freshchatWebhook:\n    url: '{callbackUrl}'\n    protocol: https\n    description: >-\n      Freshchat sends webhook POST requests to the registered callback\n      URL when messaging events occur.\n    variables:\n      callbackUrl:\n        description: The customer-configured webhook callback URL.\nchannels:\n  /freshdesk/ticket-created:\n    description: >-\n      Triggered when a new ticket is created in Freshdesk. Configured\n      through ticket creation automation rules.\n    publish:\n      operationId: onFreshdeskTicketCreated\n      summary: Freshdesk ticket created event\n      message:\n        $ref:\
  \ '#/components/messages/FreshdeskTicketEvent'\n  /freshdesk/ticket-updated:\n    description: >-\n      Triggered when an existing ticket is updated in Freshdesk. This\n      includes status changes, assignment changes, priority updates,\n      and custom field modifications.\n    publish:\n      operationId: onFreshdeskTicketUpdated\n      summary: Freshdesk ticket updated event\n      message:\n        $ref: '#/components/messages/FreshdeskTicketEvent'\n  /freshservice/ticket-created:\n    description: >-\n      Triggered when a new ticket is created in Freshservice. Configured\n      through the Workflow Automator.\n    publish:\n      operationId: onFreshserviceTicketCreated\n      summary: Freshservice ticket created event\n      message:\n        $ref: '#/components/messages/FreshserviceTicketEvent'\n  /freshservice/ticket-updated:\n    description: >-\n      Triggered when an existing ticket is updated in Freshservice,\n      including status changes, assignment updates, and field\
  \ modifications.\n    publish:\n      operationId: onFreshserviceTicketUpdated\n      summary: Freshservice ticket updated event\n      message:\n        $ref: '#/components/messages/FreshserviceTicketEvent'\n  /freshchat/message-create:\n    description: >-\n      Triggered when a new message is sent in a Freshchat conversation,\n      whether by a user, agent, or bot.\n    publish:\n      operationId: onFreshchatMessageCreate\n      summary: Freshchat message created event\n      message:\n        $ref: '#/components/messages/FreshchatMessageEvent'\n  /freshchat/conversation-assignment:\n    description: >-\n      Triggered when a conversation is assigned or reassigned to an\n      agent or group in Freshchat.\n    publish:\n      operationId: onFreshchatConversationAssignment\n      summary: Freshchat conversation assignment event\n      message:\n        $ref: '#/components/messages/FreshchatConversationEvent'\n  /freshchat/conversation-resolution:\n    description: >-\n      Triggered\
  \ when a conversation is resolved in Freshchat.\n    publish:\n      operationId: onFreshchatConversationResolution\n      summary: Freshchat conversation resolution event\n      message:\n        $ref: '#/components/messages/FreshchatConversationEvent'\n  /freshchat/conversation-reopen:\n    description: >-\n      Triggered when a previously resolved conversation is reopened\n      in Freshchat.\n    publish:\n      operationId: onFreshchatConversationReopen\n      summary: Freshchat conversation reopen event\n      message:\n        $ref: '#/components/messages/FreshchatConversationEvent'\ncomponents:\n  messages:\n    FreshdeskTicketEvent:\n      name: FreshdeskTicketEvent\n      title: Freshdesk Ticket Webhook Event\n      summary: >-\n        Payload sent by Freshdesk when a ticket event occurs via\n        automation rule webhooks.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/FreshdeskTicketPayload'\n    FreshserviceTicketEvent:\n    \
  \  name: FreshserviceTicketEvent\n      title: Freshservice Ticket Webhook Event\n      summary: >-\n        Payload sent by Freshservice when a ticket event occurs via\n        the Workflow Automator.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/FreshserviceTicketPayload'\n    FreshchatMessageEvent:\n      name: FreshchatMessageEvent\n      title: Freshchat Message Webhook Event\n      summary: >-\n        Payload sent by Freshchat when a new message is created in a\n        conversation.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/FreshchatMessagePayload'\n    FreshchatConversationEvent:\n      name: FreshchatConversationEvent\n      title: Freshchat Conversation Webhook Event\n      summary: >-\n        Payload sent by Freshchat when a conversation lifecycle event\n        occurs such as assignment, resolution, or reopening.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/FreshchatConversationPayload'\n\
  \  schemas:\n    FreshdeskTicketPayload:\n      type: object\n      description: >-\n        Webhook payload for Freshdesk ticket events. The exact fields\n        included depend on the automation rule configuration.\n      properties:\n        freshdesk_webhook:\n          type: object\n          description: Wrapper object for the webhook data.\n          properties:\n            ticket_id:\n              type: integer\n              description: ID of the ticket.\n            ticket_subject:\n              type: string\n              description: Subject of the ticket.\n            ticket_description:\n              type: string\n              description: Description text of the ticket.\n            ticket_status:\n              type: string\n              description: Status name of the ticket.\n            ticket_priority:\n              type: string\n              description: Priority name of the ticket.\n            ticket_source:\n              type: string\n              description:\
  \ Source channel of the ticket.\n            ticket_type:\n              type: string\n              description: Type of the ticket.\n            ticket_requester_name:\n              type: string\n              description: Name of the requester.\n            ticket_requester_email:\n              type: string\n              format: email\n              description: Email of the requester.\n            ticket_agent_name:\n              type: string\n              description: Name of the assigned agent.\n            ticket_agent_email:\n              type: string\n              format: email\n              description: Email of the assigned agent.\n            ticket_group_name:\n              type: string\n              description: Name of the assigned group.\n            ticket_company_name:\n              type: string\n              description: Name of the associated company.\n            ticket_product_name:\n              type: string\n              description: Name of the associated\
  \ product.\n            ticket_tags:\n              type: string\n              description: Comma-separated list of ticket tags.\n            ticket_due_by_time:\n              type: string\n              format: date-time\n              description: Due by timestamp.\n            ticket_created_at:\n              type: string\n              format: date-time\n              description: Ticket creation timestamp.\n            ticket_updated_at:\n              type: string\n              format: date-time\n              description: Last update timestamp.\n            ticket_url:\n              type: string\n              format: uri\n              description: URL to view the ticket in Freshdesk.\n    FreshserviceTicketPayload:\n      type: object\n      description: >-\n        Webhook payload for Freshservice ticket events. Fields are\n        determined by the Workflow Automator configuration.\n      properties:\n        freshservice_webhook:\n          type: object\n          description:\
  \ Wrapper object for the webhook data.\n          properties:\n            ticket_id:\n              type: integer\n              description: ID of the ticket.\n            ticket_subject:\n              type: string\n              description: Subject of the ticket.\n            ticket_description:\n              type: string\n              description: Description of the ticket.\n            ticket_status:\n              type: string\n              description: Status name.\n            ticket_priority:\n              type: string\n              description: Priority name.\n            ticket_type:\n              type: string\n              description: Ticket type (Incident, Service Request).\n            ticket_source:\n              type: string\n              description: Source channel.\n            ticket_requester_name:\n              type: string\n              description: Name of the requester.\n            ticket_requester_email:\n              type: string\n            \
  \  format: email\n              description: Email of the requester.\n            ticket_agent_name:\n              type: string\n              description: Name of the assigned agent.\n            ticket_group_name:\n              type: string\n              description: Name of the assigned group.\n            ticket_department_name:\n              type: string\n              description: Name of the department.\n            ticket_category:\n              type: string\n              description: Category of the ticket.\n            ticket_sub_category:\n              type: string\n              description: Sub-category.\n            ticket_due_by_time:\n              type: string\n              format: date-time\n              description: Due by timestamp.\n            ticket_created_at:\n              type: string\n              format: date-time\n              description: Ticket creation timestamp.\n            ticket_updated_at:\n              type: string\n              format:\
  \ date-time\n              description: Last update timestamp.\n            ticket_url:\n              type: string\n              format: uri\n              description: URL to view the ticket in Freshservice.\n    FreshchatMessagePayload:\n      type: object\n      description: >-\n        Webhook payload for Freshchat message creation events.\n      properties:\n        actor:\n          type: object\n          description: The actor who triggered the event.\n          properties:\n            actor_type:\n              type: string\n              description: Type of actor (user, agent, system).\n              enum:\n                - user\n                - agent\n                - system\n            actor_id:\n              type: string\n              description: ID of the actor.\n        action:\n          type: string\n          description: The action that triggered the event.\n          const: message_create\n        action_time:\n          type: string\n          format: date-time\n\
  \          description: Timestamp when the action occurred.\n        data:\n          type: object\n          description: Event data containing the message details.\n          properties:\n            message:\n              type: object\n              description: The message that was created.\n              properties:\n                message_id:\n                  type: string\n                  description: ID of the message.\n                conversation_id:\n                  type: string\n                  description: ID of the conversation.\n                message_type:\n                  type: string\n                  description: Type of message (normal, private).\n                  enum:\n                    - normal\n                    - private\n                message_parts:\n                  type: array\n                  description: Parts composing the message.\n                  items:\n                    type: object\n                    properties:\n       \
  \               text:\n                        type: object\n                        properties:\n                          content:\n                            type: string\n                            description: Text content.\n                app_id:\n                  type: string\n                  description: ID of the application.\n                channel_id:\n                  type: string\n                  description: ID of the channel.\n                created_time:\n                  type: string\n                  format: date-time\n                  description: Message creation timestamp.\n    FreshchatConversationPayload:\n      type: object\n      description: >-\n        Webhook payload for Freshchat conversation lifecycle events\n        including assignment, resolution, and reopening.\n      properties:\n        actor:\n          type: object\n          description: The actor who triggered the event.\n          properties:\n            actor_type:\n            \
  \  type: string\n              description: Type of actor (user, agent, system).\n              enum:\n                - user\n                - agent\n                - system\n            actor_id:\n              type: string\n              description: ID of the actor.\n        action:\n          type: string\n          description: The action that triggered the event.\n          enum:\n            - conversation_assignment\n            - conversation_resolution\n            - conversation_reopen\n        action_time:\n          type: string\n          format: date-time\n          description: Timestamp when the action occurred.\n        data:\n          type: object\n          description: Event data containing conversation details.\n          properties:\n            conversation:\n              type: object\n              description: The conversation involved in the event.\n              properties:\n                conversation_id:\n                  type: string\n            \
  \      description: ID of the conversation.\n                app_id:\n                  type: string\n                  description: ID of the application.\n                channel_id:\n                  type: string\n                  description: ID of the channel.\n                status:\n                  type: string\n                  description: Current status of the conversation.\n                  enum:\n                    - new\n                    - assigned\n                    - resolved\n                    - reopened\n                assigned_agent_id:\n                  type: string\n                  description: ID of the assigned agent.\n                assigned_group_id:\n                  type: string\n                  description: ID of the assigned group.\n            assignment:\n              type: object\n              description: >-\n                Assignment details (present only for assignment events).\n              properties:\n                from_agent_id:\n\
  \                  type: string\n                  description: Previous agent ID.\n                to_agent_id:\n                  type: string\n                  description: New agent ID.\n                from_group_id:\n                  type: string\n                  description: Previous group ID.\n                to_group_id:\n                  type: string\n                  description: New group ID.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/freshworks/refs/heads/main/asyncapi/freshworks-webhooks-asyncapi.yml
spec_file: asyncapi/freshworks-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/freshworks/refs/heads/main/asyncapi/freshworks-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
