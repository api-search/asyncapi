---
api_specs:
- filename: opsgenie-alert-openapi.yml
  format: yaml
  label: OpsGenie Alert API
  slug: opsgenie-alert
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/openapi/opsgenie-alert-openapi.yml
- filename: opsgenie-incident-openapi.yml
  format: yaml
  label: OpsGenie Incident API
  slug: opsgenie-incident
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/openapi/opsgenie-incident-openapi.yml
- filename: opsgenie-user-openapi.yml
  format: yaml
  label: OpsGenie User API
  slug: opsgenie-user
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/openapi/opsgenie-user-openapi.yml
- filename: opsgenie-team-openapi.yml
  format: yaml
  label: OpsGenie Team API
  slug: opsgenie-team
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/openapi/opsgenie-team-openapi.yml
- filename: opsgenie-schedule-openapi.yml
  format: yaml
  label: OpsGenie Schedule API
  slug: opsgenie-schedule
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/openapi/opsgenie-schedule-openapi.yml
- filename: opsgenie-escalation-openapi.yml
  format: yaml
  label: OpsGenie Escalation API
  slug: opsgenie-escalation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/openapi/opsgenie-escalation-openapi.yml
- filename: opsgenie-integration-openapi.yml
  format: yaml
  label: OpsGenie Integration API
  slug: opsgenie-integration
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/openapi/opsgenie-integration-openapi.yml
- filename: opsgenie-heartbeat-openapi.yml
  format: yaml
  label: OpsGenie Heartbeat API
  slug: opsgenie-heartbeat
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/openapi/opsgenie-heartbeat-openapi.yml
- filename: opsgenie-service-openapi.yml
  format: yaml
  label: OpsGenie Service API
  slug: opsgenie-service
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/openapi/opsgenie-service-openapi.yml
- filename: opsgenie-notification-rule-openapi.yml
  format: yaml
  label: OpsGenie Notification Rule API
  slug: opsgenie-notification-rule
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/openapi/opsgenie-notification-rule-openapi.yml
- filename: opsgenie-account-openapi.yml
  format: yaml
  label: OpsGenie Account API
  slug: opsgenie-account
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/openapi/opsgenie-account-openapi.yml
- filename: opsgenie-maintenance-openapi.yml
  format: yaml
  label: OpsGenie Maintenance API
  slug: opsgenie-maintenance
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/openapi/opsgenie-maintenance-openapi.yml
channels:
- description: Webhook endpoint that receives OpsGenie alert event notifications. OpsGenie posts JSON payloads to this channel when alert actions occur.
  name: /webhook
  operation: publish
  operation_id: receiveAlertEvent
  summary: Receive alert event notification
description: OpsGenie sends webhook notifications for alert actions to configured webhook URLs. When alert events occur such as create, acknowledge, close, or delete, OpsGenie posts a JSON payload to the registered webhook endpoint containing alert details and the action performed. The webhook payload format is fixed and includes a subset of alert fields along with the triggering action and source information.
layout: asyncapi
messages:
- description: ''
  name: AlertCreated
  summary: Notification sent when a new alert is created in OpsGenie.
  title: Alert Created
- description: ''
  name: AlertAcknowledged
  summary: Notification sent when an alert is acknowledged.
  title: Alert Acknowledged
- description: ''
  name: AlertClosed
  summary: Notification sent when an alert is closed.
  title: Alert Closed
- description: ''
  name: AlertDeleted
  summary: Notification sent when an alert is deleted.
  title: Alert Deleted
- description: ''
  name: AlertNoteAdded
  summary: Notification sent when a note is added to an alert.
  title: Alert Note Added
- description: ''
  name: AlertOwnershipAssigned
  summary: Notification sent when ownership of an alert is assigned to a user.
  title: Alert Ownership Assigned
- description: ''
  name: AlertCustomAction
  summary: Notification sent when a custom action is executed on an alert.
  title: Alert Custom Action
name: OpsGenie Webhook Events
provider_name: OpsGenie
provider_slug: opsgenie
servers:
- description: Customer-configured webhook endpoint URL that receives alert event notifications from OpsGenie.
  name: webhookEndpoint
  protocol: https
  url: '{webhookUrl}'
slug: opsgenie-webhook-asyncapi
source_filename: opsgenie-webhook-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: OpsGenie Webhook Events\n  description: >-\n    OpsGenie sends webhook notifications for alert actions to configured\n    webhook URLs. When alert events occur such as create, acknowledge,\n    close, or delete, OpsGenie posts a JSON payload to the registered\n    webhook endpoint containing alert details and the action performed.\n    The webhook payload format is fixed and includes a subset of alert\n    fields along with the triggering action and source information.\n  version: '2.0.0'\n  contact:\n    name: Atlassian Support\n    url: https://support.atlassian.com/opsgenie/\nservers:\n  webhookEndpoint:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Customer-configured webhook endpoint URL that receives alert\n      event notifications from OpsGenie.\n    variables:\n      webhookUrl:\n        description: >-\n          The URL configured in the OpsGenie webhook integration settings.\n    security:\n      - {}\n\
  channels:\n  /webhook:\n    description: >-\n      Webhook endpoint that receives OpsGenie alert event notifications.\n      OpsGenie posts JSON payloads to this channel when alert actions\n      occur.\n    publish:\n      operationId: receiveAlertEvent\n      summary: Receive alert event notification\n      description: >-\n        OpsGenie sends alert event notifications to this endpoint when\n        alert actions are performed. The payload includes the action type,\n        alert details, and source information.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/AlertCreated'\n          - $ref: '#/components/messages/AlertAcknowledged'\n          - $ref: '#/components/messages/AlertClosed'\n          - $ref: '#/components/messages/AlertDeleted'\n          - $ref: '#/components/messages/AlertNoteAdded'\n          - $ref: '#/components/messages/AlertOwnershipAssigned'\n          - $ref: '#/components/messages/AlertCustomAction'\ncomponents:\n  messages:\n    AlertCreated:\n\
  \      name: AlertCreated\n      title: Alert Created\n      summary: >-\n        Notification sent when a new alert is created in OpsGenie.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n      examples:\n        - name: AlertCreatedExample\n          payload:\n            action: Create\n            alert:\n              alertId: 44f717bf-44bd-11c9-44c7-2d0cf1d07b23\n              message: Test alert from monitoring\n              username: admin@example.com\n              alias: monitoring-alert-001\n              tinyId: '454'\n              entity: ''\n              userId: 4caaaa77-9222-4322-8622-d3522fbd7dda\n            source:\n              name: MonitoringTool\n              type: api\n    AlertAcknowledged:\n      name: AlertAcknowledged\n      title: Alert Acknowledged\n      summary: >-\n        Notification sent when an alert is acknowledged.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n\
  \    AlertClosed:\n      name: AlertClosed\n      title: Alert Closed\n      summary: >-\n        Notification sent when an alert is closed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    AlertDeleted:\n      name: AlertDeleted\n      title: Alert Deleted\n      summary: >-\n        Notification sent when an alert is deleted.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    AlertNoteAdded:\n      name: AlertNoteAdded\n      title: Alert Note Added\n      summary: >-\n        Notification sent when a note is added to an alert.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    AlertOwnershipAssigned:\n      name: AlertOwnershipAssigned\n      title: Alert Ownership Assigned\n      summary: >-\n        Notification sent when ownership of an alert is assigned to a user.\n      contentType: application/json\n\
  \      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    AlertCustomAction:\n      name: AlertCustomAction\n      title: Alert Custom Action\n      summary: >-\n        Notification sent when a custom action is executed on an alert.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n  schemas:\n    WebhookPayload:\n      type: object\n      required:\n        - action\n        - alert\n        - source\n      properties:\n        action:\n          type: string\n          description: >-\n            The alert action that triggered the webhook. Standard values\n            are Create, Acknowledge, AddNote, AssignOwnership, Close, and\n            Delete. Custom action names are also possible.\n          enum:\n            - Create\n            - Acknowledge\n            - AddNote\n            - AssignOwnership\n            - Close\n            - Delete\n        alert:\n          $ref: '#/components/schemas/WebhookAlert'\n\
  \        source:\n          $ref: '#/components/schemas/WebhookSource'\n        escalationNotify:\n          type: object\n          description: >-\n            Escalation notification details, if the event involves an\n            escalation.\n          properties:\n            id:\n              type: string\n              description: >-\n                Escalation ID.\n            name:\n              type: string\n              description: >-\n                Escalation name.\n            type:\n              type: string\n              description: >-\n                Entity type.\n    WebhookAlert:\n      type: object\n      description: >-\n        Subset of alert fields included in the webhook payload.\n      properties:\n        alertId:\n          type: string\n          description: >-\n            Unique identifier of the alert.\n        message:\n          type: string\n          description: >-\n            Alert message text.\n        username:\n          type: string\n\
  \          description: >-\n            Username of the user who performed the action.\n        alias:\n          type: string\n          description: >-\n            Client-defined alias for the alert.\n        tinyId:\n          type: string\n          description: >-\n            Short human-readable identifier.\n        entity:\n          type: string\n          description: >-\n            Entity field of the alert.\n        userId:\n          type: string\n          description: >-\n            ID of the user who performed the action.\n        createdAt:\n          type: integer\n          description: >-\n            Timestamp of alert creation in milliseconds since epoch.\n        updatedAt:\n          type: integer\n          description: >-\n            Timestamp of last update in milliseconds since epoch.\n        tags:\n          type: array\n          items:\n            type: string\n          description: >-\n            Tags attached to the alert.\n        description:\n\
  \          type: string\n          description: >-\n            Detailed description of the alert.\n        priority:\n          type: string\n          description: >-\n            Priority level (P1-P5).\n        source:\n          type: string\n          description: >-\n            Source of the alert.\n        note:\n          type: string\n          description: >-\n            Note content, if the action involves a note.\n    WebhookSource:\n      type: object\n      description: >-\n        Information about the source that triggered the alert action.\n      properties:\n        name:\n          type: string\n          description: >-\n            Name of the source (integration or tool name).\n        type:\n          type: string\n          description: >-\n            Type of the source (e.g. api, web, system).\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/asyncapi/opsgenie-webhook-asyncapi.yml
spec_file: asyncapi/opsgenie-webhook-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/opsgenie/refs/heads/main/asyncapi/opsgenie-webhook-asyncapi.yml
tags:
- Alerts
- Incident Management
- Monitoring
- On-Call
- Operations
- AsyncAPI
- Webhooks
- Events
version: 2.0.0
---
