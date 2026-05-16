---
api_specs:
- filename: postman-webhooks-asyncapi.yml
  format: yaml
  label: Postman
  slug: postman
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/asyncapi/postman-webhooks-asyncapi.yml
- filename: postman-collections-api-openapi.yml
  format: yaml
  label: Postman Collections API
  slug: collections-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-collections-api-openapi.yml
- filename: postman-workspaces-api-openapi.yml
  format: yaml
  label: Postman Workspaces API
  slug: workspaces-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-workspaces-api-openapi.yml
- filename: postman-environments-api-openapi.yml
  format: yaml
  label: Postman Environments API
  slug: environments-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-environments-api-openapi.yml
- filename: postman-mock-servers-api-openapi.yml
  format: yaml
  label: Postman Mock Servers API
  slug: mock-servers-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-mock-servers-api-openapi.yml
- filename: postman-monitors-api-openapi.yml
  format: yaml
  label: Postman Monitors API
  slug: monitors-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-monitors-api-openapi.yml
- filename: postman-apis-api-openapi.yml
  format: yaml
  label: Postman APIs / Spec Hub API
  slug: apis-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-apis-api-openapi.yml
- filename: postman-private-api-network-api-openapi.yml
  format: yaml
  label: Postman Private API Network API
  slug: private-api-network-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-private-api-network-api-openapi.yml
- filename: postman-webhooks-api-openapi.yml
  format: yaml
  label: Postman Webhooks API
  slug: webhooks-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-webhooks-api-openapi.yml
- filename: postman-collection-runs-api-openapi.yml
  format: yaml
  label: Postman Collection Runs API
  slug: collection-runs-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-collection-runs-api-openapi.yml
- filename: postman-tags-api-openapi.yml
  format: yaml
  label: Postman Tags API
  slug: tags-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-tags-api-openapi.yml
- filename: postman-audit-logs-api-openapi.yml
  format: yaml
  label: Postman Audit Logs API
  slug: audit-logs-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-audit-logs-api-openapi.yml
- filename: postman-secret-scanner-api-openapi.yml
  format: yaml
  label: Postman Secret Scanner API
  slug: secret-scanner-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-secret-scanner-api-openapi.yml
channels:
- description: Channel for incoming webhook triggers that initiate collection runs. When an external system sends a POST request to the webhook URL, Postman triggers the associated collection run and passes the request payload as variables available during the run.
  name: /webhook/trigger
  operation: publish
  operation_id: triggerCollectionRun
  summary: Trigger a collection run via webhook
- description: Channel for outgoing monitor run notifications. When a monitor run completes with failures or errors, Postman sends a notification to configured webhook endpoints with details about the run results.
  name: /webhook/monitor-notification
  operation: subscribe
  operation_id: receiveMonitorNotification
  summary: Receive a monitor run notification
- description: Channel for integration webhook notifications. Postman can send notifications to external services (Slack, Microsoft Teams, PagerDuty, etc.) when specific events occur, such as monitor failures, collection updates, or team activity changes.
  name: /webhook/integration-notification
  operation: subscribe
  operation_id: receiveIntegrationNotification
  summary: Receive an integration notification
description: Postman Webhooks enable you to receive incoming HTTP POST requests that trigger collection runs. When an external system sends a POST request to a Postman webhook URL, the webhook triggers a collection run and makes the incoming payload available as variables during the run. This provides a way to integrate Postman with CI/CD pipelines, monitoring systems, and other external services that need to trigger automated API testing workflows. Postman also supports custom webhooks for monitor notifications, which deliver alerts about monitor run failures and errors to your configured endpoints.
layout: asyncapi
messages:
- description: ''
  name: WebhookTriggerPayload
  summary: The payload sent to a Postman webhook URL to trigger a collection run. The payload contents are user-defined and become available as variables during the collection run.
  title: Webhook Trigger Payload
- description: ''
  name: MonitorNotification
  summary: Notification sent when a Postman monitor run completes. Contains run results including test pass/fail counts, response times, and error details.
  title: Monitor Run Notification
- description: ''
  name: IntegrationNotification
  summary: Notification sent to external integrations when specific Postman events occur, such as monitor failures, collection updates, or team changes.
  title: Integration Notification
name: Postman Webhooks
provider_name: Postman
provider_slug: postman
servers:
- description: Your webhook receiver endpoint. External systems send POST requests to the Postman-generated webhook URL to trigger collection runs. The webhook URL is generated when you create a webhook via the Postman API.
  name: webhook-receiver
  protocol: https
  url: '{webhookUrl}'
- description: Your notification endpoint that receives monitor run results. Configure this URL in your Postman monitor's notification settings or through integrations.
  name: monitor-notification-receiver
  protocol: https
  url: '{notificationUrl}'
slug: postman-webhooks-asyncapi
source_filename: postman-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Postman Webhooks\n  description: >-\n    Postman Webhooks enable you to receive incoming HTTP POST requests that\n    trigger collection runs. When an external system sends a POST request to\n    a Postman webhook URL, the webhook triggers a collection run and makes the\n    incoming payload available as variables during the run. This provides a way\n    to integrate Postman with CI/CD pipelines, monitoring systems, and other\n    external services that need to trigger automated API testing workflows.\n\n    Postman also supports custom webhooks for monitor notifications, which\n    deliver alerts about monitor run failures and errors to your configured\n    endpoints.\n  version: '1.0.0'\n  contact:\n    name: Postman Developer Support\n    url: https://learning.postman.com/docs/developer/postman-api/intro-api/\n    email: help@postman.com\n  license:\n    name: Postman Terms of Service\n    url: https://www.postman.com/legal/terms/\n  externalDocs:\n\
  \    description: Postman Webhooks Documentation\n    url: https://learning.postman.com/docs/developer/postman-api/intro-api/\nservers:\n  webhook-receiver:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your webhook receiver endpoint. External systems send POST requests to\n      the Postman-generated webhook URL to trigger collection runs. The webhook\n      URL is generated when you create a webhook via the Postman API.\n    variables:\n      webhookUrl:\n        description: >-\n          The webhook URL generated by Postman when the webhook is created.\n          This URL is unique to each webhook and includes authentication\n          built into the URL path.\n  monitor-notification-receiver:\n    url: '{notificationUrl}'\n    protocol: https\n    description: >-\n      Your notification endpoint that receives monitor run results. Configure\n      this URL in your Postman monitor's notification settings or through\n      integrations.\n    variables:\n\
  \      notificationUrl:\n        description: >-\n          The URL configured to receive monitor notification webhooks.\nchannels:\n  /webhook/trigger:\n    description: >-\n      Channel for incoming webhook triggers that initiate collection runs.\n      When an external system sends a POST request to the webhook URL, Postman\n      triggers the associated collection run and passes the request payload\n      as variables available during the run.\n    publish:\n      operationId: triggerCollectionRun\n      summary: Trigger a collection run via webhook\n      description: >-\n        External systems send POST requests with JSON payloads to this\n        channel. The payload data becomes available as variables in the\n        collection being run, accessible via pm.variables.get() in\n        pre-request and test scripts.\n      bindings:\n        http:\n          type: request\n          method: POST\n          headers:\n            type: object\n            properties:\n          \
  \    Content-Type:\n                type: string\n                enum: [application/json]\n      message:\n        $ref: '#/components/messages/WebhookTriggerPayload'\n  /webhook/monitor-notification:\n    description: >-\n      Channel for outgoing monitor run notifications. When a monitor run\n      completes with failures or errors, Postman sends a notification to\n      configured webhook endpoints with details about the run results.\n    subscribe:\n      operationId: receiveMonitorNotification\n      summary: Receive a monitor run notification\n      description: >-\n        Postman sends monitor run result notifications as HTTP POST requests\n        with JSON payloads to configured webhook endpoints. Notifications are\n        sent when a monitor run completes with test failures or errors.\n      bindings:\n        http:\n          type: request\n          method: POST\n          headers:\n            type: object\n            properties:\n              Content-Type:\n       \
  \         type: string\n                enum: [application/json]\n              User-Agent:\n                type: string\n                description: Postman user agent string\n      message:\n        $ref: '#/components/messages/MonitorNotification'\n  /webhook/integration-notification:\n    description: >-\n      Channel for integration webhook notifications. Postman can send\n      notifications to external services (Slack, Microsoft Teams, PagerDuty,\n      etc.) when specific events occur, such as monitor failures, collection\n      updates, or team activity changes.\n    subscribe:\n      operationId: receiveIntegrationNotification\n      summary: Receive an integration notification\n      description: >-\n        Postman sends event notifications to configured integration endpoints.\n        These notifications are triggered by various Postman events and\n        delivered as HTTP POST requests.\n      bindings:\n        http:\n          type: request\n          method: POST\n\
  \          headers:\n            type: object\n            properties:\n              Content-Type:\n                type: string\n                enum: [application/json]\n      message:\n        $ref: '#/components/messages/IntegrationNotification'\ncomponents:\n  messages:\n    WebhookTriggerPayload:\n      name: WebhookTriggerPayload\n      title: Webhook Trigger Payload\n      summary: >-\n        The payload sent to a Postman webhook URL to trigger a collection run.\n        The payload contents are user-defined and become available as variables\n        during the collection run.\n      contentType: application/json\n      payload:\n        type: object\n        description: >-\n          User-defined payload. All top-level keys become available as\n          variables in the collection run via pm.variables.get(key).\n        additionalProperties: true\n        example:\n          environment: production\n          buildNumber: \"1234\"\n          triggeredBy: ci-pipeline\n    \
  \      testSuite: regression\n    MonitorNotification:\n      name: MonitorNotification\n      title: Monitor Run Notification\n      summary: >-\n        Notification sent when a Postman monitor run completes. Contains\n        run results including test pass/fail counts, response times, and\n        error details.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          monitorId:\n            type: string\n            description: The monitor's unique ID\n          monitorName:\n            type: string\n            description: The monitor's display name\n          collectionUid:\n            type: string\n            description: The UID of the collection that was run\n          environmentUid:\n            type: string\n            description: The UID of the environment used during the run\n          status:\n            type: string\n            enum: [success, failure, error, abort]\n            description: The overall run status\n\
  \          startedAt:\n            type: string\n            format: date-time\n            description: When the run started\n          finishedAt:\n            type: string\n            format: date-time\n            description: When the run completed\n          stats:\n            type: object\n            properties:\n              requests:\n                type: object\n                properties:\n                  total:\n                    type: integer\n                  failed:\n                    type: integer\n              assertions:\n                type: object\n                properties:\n                  total:\n                    type: integer\n                  failed:\n                    type: integer\n          failures:\n            type: array\n            description: Details of failed test assertions\n            items:\n              type: object\n              properties:\n                name:\n                  type: string\n                  description:\
  \ The test assertion name\n                error:\n                  type: string\n                  description: The error message\n                request:\n                  type: object\n                  properties:\n                    name:\n                      type: string\n                    method:\n                      type: string\n                    url:\n                      type: string\n                response:\n                  type: object\n                  properties:\n                    statusCode:\n                      type: integer\n                    responseTime:\n                      type: integer\n          region:\n            type: string\n            description: The region the monitor ran from\n    IntegrationNotification:\n      name: IntegrationNotification\n      title: Integration Notification\n      summary: >-\n        Notification sent to external integrations when specific Postman\n        events occur, such as monitor failures, collection\
  \ updates, or\n        team changes.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          event:\n            type: string\n            description: The event type that triggered the notification\n            enum:\n              - monitor.run.success\n              - monitor.run.failure\n              - monitor.run.error\n              - collection.updated\n              - environment.updated\n              - team.member_added\n              - team.member_removed\n          timestamp:\n            type: string\n            format: date-time\n          data:\n            type: object\n            description: Event-specific data. Structure varies by event type.\n            additionalProperties: true\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/asyncapi/postman-webhooks-asyncapi.yml
spec_file: asyncapi/postman-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/asyncapi/postman-webhooks-asyncapi.yml
tags:
- AI Agent Builder
- AI Agents
- API Catalog
- API Client
- API Design
- API Development
- API Documentation
- API Governance
- API Lifecycle
- API Monitoring
- API Network
- API Platform
- API Testing
- Audit Logs
- Automation
- CI/CD
- Collaboration
- Collections
- Compliance
- Discovery
- Environments
- Flows
- GraphQL
- gRPC
- HTTP
- Insights
- MCP
- MCP Generator
- Mock Servers
- Mocking
- Monitors
- Newman
- OpenAPI
- Platform
- Private API Network
- Public API Network
- Secret Scanning
- Spec Hub
- Specifications
- SSO
- Testing
- Vault
- WebSocket
- Workflows
- Workspaces
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
