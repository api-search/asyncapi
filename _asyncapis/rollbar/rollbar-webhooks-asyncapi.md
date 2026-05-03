---
api_specs:
- filename: openapi.yaml
  format: yaml
  label: Rollbar REST API
  slug: rollbar-rest-api
  spec_type: OpenAPI
  url: https://explorer.docs.rollbar.com/
- filename: rollbar-deployment-api-openapi.yml
  format: yaml
  label: Rollbar Deployment API
  slug: rollbar-deployment-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rollbar/refs/heads/main/openapi/rollbar-deployment-api-openapi.yml
- filename: rollbar-metrics-api-openapi.yml
  format: yaml
  label: Rollbar Metrics API
  slug: rollbar-metrics-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rollbar/refs/heads/main/openapi/rollbar-metrics-api-openapi.yml
- filename: rollbar-rql-api-openapi.yml
  format: yaml
  label: Rollbar RQL API
  slug: rollbar-rql-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rollbar/refs/heads/main/openapi/rollbar-rql-api-openapi.yml
- filename: rollbar-webhooks-asyncapi.yml
  format: yaml
  label: Rollbar Webhooks
  slug: rollbar-webhooks
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/rollbar/refs/heads/main/asyncapi/rollbar-webhooks-asyncapi.yml
channels:
- description: The webhook delivery channel. All Rollbar webhook events are sent as HTTP POST requests to the configured URL. Rules can override the destination URL on a per-rule basis.
  name: /webhook
  operation: publish
  operation_id: receiveWebhookEvent
  summary: Receive a Rollbar webhook event
description: Rollbar's webhook notification system delivers real-time event notifications to configured endpoints when errors, deployments, and other significant events occur. Webhooks are triggered based on configurable rules and deliver payloads in JSON or XML format via HTTP POST requests. The webhook endpoint should respond with a 200, 201, 202, or 204 status code. If another response code is received or the request times out after 3 seconds, Rollbar will retry up to 10 times with exponential backoff, with the first retry after 1 second and the 10th retry after 16 days.
layout: asyncapi
messages:
- description: ''
  name: NewItemEvent
  summary: Triggered when an error or message is seen for the first time.
  title: New Item Event
- description: ''
  name: OccurrenceEvent
  summary: Triggered on every occurrence of an error or message.
  title: Every Occurrence Event
- description: ''
  name: ExponentialRepeatItemEvent
  summary: Triggered on the 10th, 100th, 1000th, and subsequent exponential occurrences of an item.
  title: Exponential Repeat Item Event
- description: ''
  name: ItemVelocityEvent
  summary: Triggered when an item's occurrence rate exceeds a configured threshold.
  title: High Occurrence Rate Event
- description: ''
  name: ResolvedItemEvent
  summary: Triggered when an item is marked as resolved.
  title: Item Resolved Event
- description: ''
  name: ReactivatedItemEvent
  summary: Triggered when a resolved item occurs again, changing its status back to active.
  title: Item Reactivated Event
- description: ''
  name: ReopenedItemEvent
  summary: Triggered when a resolved or muted item is manually reopened.
  title: Item Reopened Event
- description: ''
  name: DeployEvent
  summary: Triggered when a deployment is reported to Rollbar.
  title: Deploy Event
name: Rollbar Webhook Events
provider_name: Rollbar
provider_slug: rollbar
servers:
- description: The webhook URL configured in Rollbar project settings under Settings > Notifications > Webhook. This is the destination endpoint that receives event payloads.
  name: rollbarWebhook
  protocol: https
  url: '{webhookUrl}'
slug: rollbar-webhooks-asyncapi
source_filename: rollbar-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Rollbar Webhook Events\n  description: >-\n    Rollbar's webhook notification system delivers real-time event\n    notifications to configured endpoints when errors, deployments, and\n    other significant events occur. Webhooks are triggered based on\n    configurable rules and deliver payloads in JSON or XML format via\n    HTTP POST requests. The webhook endpoint should respond with a 200,\n    201, 202, or 204 status code. If another response code is received\n    or the request times out after 3 seconds, Rollbar will retry up to\n    10 times with exponential backoff, with the first retry after 1 second\n    and the 10th retry after 16 days.\n  version: '1'\n  contact:\n    name: Rollbar Support\n    url: https://rollbar.com/support/\n  termsOfService: https://rollbar.com/terms/\nservers:\n  rollbarWebhook:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      The webhook URL configured in Rollbar project settings under\n\
  \      Settings > Notifications > Webhook. This is the destination\n      endpoint that receives event payloads.\n    variables:\n      webhookUrl:\n        description: >-\n          The fully qualified URL where Rollbar sends webhook payloads.\n    security:\n      - {}\nchannels:\n  /webhook:\n    description: >-\n      The webhook delivery channel. All Rollbar webhook events are sent\n      as HTTP POST requests to the configured URL. Rules can override\n      the destination URL on a per-rule basis.\n    publish:\n      operationId: receiveWebhookEvent\n      summary: Receive a Rollbar webhook event\n      description: >-\n        Receives webhook event payloads from Rollbar when configured\n        notification rules are triggered. All payloads share a common\n        structure with event_name and data top-level keys.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/NewItemEvent'\n          - $ref: '#/components/messages/OccurrenceEvent'\n          - $ref:\
  \ '#/components/messages/ExponentialRepeatItemEvent'\n          - $ref: '#/components/messages/ItemVelocityEvent'\n          - $ref: '#/components/messages/ResolvedItemEvent'\n          - $ref: '#/components/messages/ReactivatedItemEvent'\n          - $ref: '#/components/messages/ReopenedItemEvent'\n          - $ref: '#/components/messages/DeployEvent'\ncomponents:\n  messages:\n    NewItemEvent:\n      name: new_item\n      title: New Item Event\n      summary: >-\n        Triggered when an error or message is seen for the first time.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/NewItemPayload'\n    OccurrenceEvent:\n      name: occurrence\n      title: Every Occurrence Event\n      summary: >-\n        Triggered on every occurrence of an error or message.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OccurrencePayload'\n    ExponentialRepeatItemEvent:\n      name: exp_repeat_item\n      title: Exponential\
  \ Repeat Item Event\n      summary: >-\n        Triggered on the 10th, 100th, 1000th, and subsequent exponential\n        occurrences of an item.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ExponentialRepeatPayload'\n    ItemVelocityEvent:\n      name: item_velocity\n      title: High Occurrence Rate Event\n      summary: >-\n        Triggered when an item's occurrence rate exceeds a configured threshold.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ItemVelocityPayload'\n    ResolvedItemEvent:\n      name: resolved_item\n      title: Item Resolved Event\n      summary: >-\n        Triggered when an item is marked as resolved.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ResolvedItemPayload'\n    ReactivatedItemEvent:\n      name: reactivated_item\n      title: Item Reactivated Event\n      summary: >-\n        Triggered when a resolved item occurs again,\
  \ changing its status\n        back to active.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ReactivatedItemPayload'\n    ReopenedItemEvent:\n      name: reopened_item\n      title: Item Reopened Event\n      summary: >-\n        Triggered when a resolved or muted item is manually reopened.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ReopenedItemPayload'\n    DeployEvent:\n      name: deploy\n      title: Deploy Event\n      summary: >-\n        Triggered when a deployment is reported to Rollbar.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DeployPayload'\n  schemas:\n    BaseWebhookPayload:\n      type: object\n      description: >-\n        Common structure shared by all Rollbar webhook payloads.\n      required:\n        - event_name\n        - data\n      properties:\n        event_name:\n          type: string\n          description: >-\n         \
  \   The type of event that triggered this webhook. Useful for\n            branching behavior in webhook handlers.\n        data:\n          type: object\n          description: >-\n            The event data containing information about what triggered\n            the webhook.\n    NewItemPayload:\n      type: object\n      description: >-\n        Payload sent when a new item is created in Rollbar.\n      required:\n        - event_name\n        - data\n      properties:\n        event_name:\n          type: string\n          description: >-\n            The event type identifier.\n          const: new_item\n        data:\n          type: object\n          description: >-\n            The event data.\n          properties:\n            item:\n              $ref: '#/components/schemas/WebhookItem'\n    OccurrencePayload:\n      type: object\n      description: >-\n        Payload sent on every occurrence of an item.\n      required:\n        - event_name\n        - data\n      properties:\n\
  \        event_name:\n          type: string\n          description: >-\n            The event type identifier.\n          const: occurrence\n        data:\n          type: object\n          description: >-\n            The event data.\n          properties:\n            item:\n              $ref: '#/components/schemas/WebhookItem'\n            occurrence:\n              $ref: '#/components/schemas/WebhookOccurrence'\n    ExponentialRepeatPayload:\n      type: object\n      description: >-\n        Payload sent on exponential repeat occurrences (10th, 100th, etc.).\n      required:\n        - event_name\n        - data\n      properties:\n        event_name:\n          type: string\n          description: >-\n            The event type identifier.\n          const: exp_repeat_item\n        data:\n          type: object\n          description: >-\n            The event data.\n          properties:\n            item:\n              $ref: '#/components/schemas/WebhookItem'\n            occurrences:\n\
  \              type: integer\n              description: >-\n                The occurrence count threshold that was crossed (e.g., 10,\n                100, 1000).\n    ItemVelocityPayload:\n      type: object\n      description: >-\n        Payload sent when an item exceeds a high occurrence rate.\n      required:\n        - event_name\n        - data\n      properties:\n        event_name:\n          type: string\n          description: >-\n            The event type identifier.\n          const: item_velocity\n        data:\n          type: object\n          description: >-\n            The event data.\n          properties:\n            item:\n              $ref: '#/components/schemas/WebhookItem'\n            rate:\n              type: number\n              description: >-\n                The occurrence rate that triggered the event.\n    ResolvedItemPayload:\n      type: object\n      description: >-\n        Payload sent when an item is resolved.\n      required:\n        - event_name\n\
  \        - data\n      properties:\n        event_name:\n          type: string\n          description: >-\n            The event type identifier.\n          const: resolved_item\n        data:\n          type: object\n          description: >-\n            The event data.\n          properties:\n            item:\n              $ref: '#/components/schemas/WebhookItem'\n    ReactivatedItemPayload:\n      type: object\n      description: >-\n        Payload sent when a resolved item is reactivated by a new occurrence.\n      required:\n        - event_name\n        - data\n      properties:\n        event_name:\n          type: string\n          description: >-\n            The event type identifier.\n          const: reactivated_item\n        data:\n          type: object\n          description: >-\n            The event data.\n          properties:\n            item:\n              $ref: '#/components/schemas/WebhookItem'\n    ReopenedItemPayload:\n      type: object\n      description:\
  \ >-\n        Payload sent when an item is manually reopened.\n      required:\n        - event_name\n        - data\n      properties:\n        event_name:\n          type: string\n          description: >-\n            The event type identifier.\n          const: reopened_item\n        data:\n          type: object\n          description: >-\n            The event data.\n          properties:\n            item:\n              $ref: '#/components/schemas/WebhookItem'\n    DeployPayload:\n      type: object\n      description: >-\n        Payload sent when a deployment is reported to Rollbar.\n      required:\n        - event_name\n        - data\n      properties:\n        event_name:\n          type: string\n          description: >-\n            The event type identifier.\n          const: deploy\n        data:\n          type: object\n          description: >-\n            The event data.\n          properties:\n            deploy:\n              $ref: '#/components/schemas/WebhookDeploy'\n\
  \    WebhookItem:\n      type: object\n      description: >-\n        Item data included in webhook payloads.\n      properties:\n        id:\n          type: integer\n          description: >-\n            The item ID.\n        counter:\n          type: integer\n          description: >-\n            The project-specific counter.\n        environment:\n          type: string\n          description: >-\n            The environment where the item was seen.\n        title:\n          type: string\n          description: >-\n            The title or summary of the item.\n        level:\n          type: string\n          description: >-\n            The severity level.\n          enum:\n            - critical\n            - error\n            - warning\n            - info\n            - debug\n        status:\n          type: string\n          description: >-\n            The item status.\n          enum:\n            - active\n            - resolved\n            - muted\n        total_occurrences:\n\
  \          type: integer\n          description: >-\n            Total number of occurrences.\n        project_id:\n          type: integer\n          description: >-\n            The project ID.\n        last_occurrence_timestamp:\n          type: integer\n          description: >-\n            Unix timestamp of the most recent occurrence.\n        first_occurrence_timestamp:\n          type: integer\n          description: >-\n            Unix timestamp of the first occurrence.\n    WebhookOccurrence:\n      type: object\n      description: >-\n        Occurrence data included in webhook payloads.\n      properties:\n        id:\n          type: integer\n          description: >-\n            The occurrence instance ID.\n        timestamp:\n          type: integer\n          description: >-\n            Unix timestamp of the occurrence.\n        version:\n          type: string\n          description: >-\n            The code version when the occurrence happened.\n        data:\n   \
  \       type: object\n          description: >-\n            Full occurrence data payload.\n    WebhookDeploy:\n      type: object\n      description: >-\n        Deploy data included in webhook payloads.\n      properties:\n        id:\n          type: integer\n          description: >-\n            The deploy ID.\n        environment:\n          type: string\n          description: >-\n            The environment deployed to.\n        project_id:\n          type: integer\n          description: >-\n            The project ID.\n        revision:\n          type: string\n          description: >-\n            The revision or commit SHA.\n        local_username:\n          type: string\n          description: >-\n            The local username of the deployer.\n        comment:\n          type: string\n          description: >-\n            The deploy comment.\n        user_id:\n          type: integer\n          description: >-\n            The Rollbar user ID.\n        start_time:\n \
  \         type: integer\n          description: >-\n            Unix timestamp when the deploy started.\n        finish_time:\n          type: integer\n          description: >-\n            Unix timestamp when the deploy finished.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rollbar/refs/heads/main/asyncapi/rollbar-webhooks-asyncapi.yml
spec_file: asyncapi/rollbar-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/rollbar/refs/heads/main/asyncapi/rollbar-webhooks-asyncapi.yml
tags:
- Error Tracking
- Monitoring
- Debugging
- DevOps
- Application Performance
- AsyncAPI
- Webhooks
- Events
version: '1'
---
