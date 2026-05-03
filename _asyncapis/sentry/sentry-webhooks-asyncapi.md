---
api_specs:
- filename: sentry-api-openapi.yml
  format: yaml
  label: Sentry Error Monitoring API
  slug: sentry-error-monitoring-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sentry/refs/heads/main/openapi/sentry-api-openapi.yml
- filename: sentry-webhooks-asyncapi.yml
  format: yaml
  label: Sentry Integration Platform API
  slug: sentry-integration-platform-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/sentry/refs/heads/main/asyncapi/sentry-webhooks-asyncapi.yml
channels:
- description: Issue lifecycle events — created, resolved, assigned, archived, unresolved, ignored.
  name: issue
  operation: subscribe
  operation_id: receiveIssueEvent
  summary: Issue lifecycle webhook
- description: Individual error event notifications for new and recurring errors.
  name: error
  operation: subscribe
  operation_id: receiveErrorEvent
  summary: Error event webhook
- description: Comment activity on issues.
  name: comment
  operation: subscribe
  operation_id: receiveCommentEvent
  summary: Issue comment webhook
- description: Integration install/uninstall lifecycle events.
  name: install
  operation: subscribe
  operation_id: receiveInstallEvent
  summary: Integration install webhook
- description: Metric alert threshold events.
  name: alert
  operation: subscribe
  operation_id: receiveAlertEvent
  summary: Metric alert webhook
description: Sentry Integration Platform delivers webhook notifications to registered integrations when events occur in Sentry. Webhooks are sent as HTTP POST requests signed with HMAC-SHA256 using the client secret.
layout: asyncapi
messages:
- description: ''
  name: IssueEvent
  summary: ''
  title: Issue Lifecycle Event
- description: ''
  name: ErrorEvent
  summary: ''
  title: Raw Error Event
- description: ''
  name: CommentEvent
  summary: ''
  title: Issue Comment Event
- description: ''
  name: InstallEvent
  summary: ''
  title: Integration Installation Event
- description: ''
  name: AlertEvent
  summary: ''
  title: Metric Alert Event
name: Sentry Integration Platform Webhooks
provider_name: Sentry
provider_slug: sentry
servers:
- description: Webhook endpoint registered in the Sentry Integration Platform. Sentry POSTs signed payloads to this URL.
  name: sentry-webhook-delivery
  protocol: http
  url: https://{your-integration-endpoint}/webhook
slug: sentry-webhooks-asyncapi
source_filename: sentry-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Sentry Integration Platform Webhooks\n  description: >-\n    Sentry Integration Platform delivers webhook notifications to registered\n    integrations when events occur in Sentry. Webhooks are sent as HTTP POST\n    requests signed with HMAC-SHA256 using the client secret.\n  version: \"0\"\n  contact:\n    name: Sentry Developer Documentation\n    url: https://docs.sentry.io/api/integration/\n  license:\n    name: Sentry Terms of Service\n    url: https://sentry.io/terms/\n\nservers:\n  sentry-webhook-delivery:\n    url: https://{your-integration-endpoint}/webhook\n    protocol: http\n    description: >-\n      Webhook endpoint registered in the Sentry Integration Platform.\n      Sentry POSTs signed payloads to this URL.\n    variables:\n      your-integration-endpoint:\n        description: Your registered webhook handler URL\n\ndefaultContentType: application/json\n\nchannels:\n  issue:\n    description: >-\n      Issue lifecycle events\
  \ — created, resolved, assigned, archived,\n      unresolved, ignored.\n    subscribe:\n      operationId: receiveIssueEvent\n      summary: Issue lifecycle webhook\n      description: >-\n        Fired when an issue is created, resolved, assigned, archived,\n        or changes state. Used to sync Sentry issues with external ticketing\n        systems such as Jira, Linear, or custom workflows.\n      tags:\n        - name: Issues\n      message:\n        $ref: '#/components/messages/IssueEvent'\n\n  error:\n    description: >-\n      Individual error event notifications for new and recurring errors.\n    subscribe:\n      operationId: receiveErrorEvent\n      summary: Error event webhook\n      description: >-\n        Fired when a new error event is received that matches configured\n        alert rules. Delivers raw event data for custom alerting pipelines.\n      tags:\n        - name: Events\n      message:\n        $ref: '#/components/messages/ErrorEvent'\n\n  comment:\n    description:\
  \ Comment activity on issues.\n    subscribe:\n      operationId: receiveCommentEvent\n      summary: Issue comment webhook\n      description: Fired when a comment is created, edited, or deleted on an issue.\n      tags:\n        - name: Issues\n      message:\n        $ref: '#/components/messages/CommentEvent'\n\n  install:\n    description: Integration install/uninstall lifecycle events.\n    subscribe:\n      operationId: receiveInstallEvent\n      summary: Integration install webhook\n      description: Fired when an organization installs or uninstalls your integration.\n      tags:\n        - name: Integration\n      message:\n        $ref: '#/components/messages/InstallEvent'\n\n  alert:\n    description: Metric alert threshold events.\n    subscribe:\n      operationId: receiveAlertEvent\n      summary: Metric alert webhook\n      description: >-\n        Fired when a metric alert transitions between triggered, warning,\n        and resolved states.\n      tags:\n        - name:\
  \ Alerts\n      message:\n        $ref: '#/components/messages/AlertEvent'\n\ncomponents:\n  messages:\n    IssueEvent:\n      name: IssueEvent\n      title: Issue Lifecycle Event\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          sentry-hook-signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification\n          sentry-hook-resource:\n            type: string\n            enum: [issue]\n          sentry-hook-timestamp:\n            type: string\n            format: date-time\n      payload:\n        type: object\n        required:\n          - action\n          - data\n          - actor\n          - installation\n        properties:\n          action:\n            type: string\n            enum: [created, resolved, assigned, archived, unresolved, ignored]\n          data:\n            type: object\n            properties:\n              issue:\n                $ref: '#/components/schemas/WebhookIssue'\n\
  \          actor:\n            $ref: '#/components/schemas/Actor'\n          installation:\n            type: object\n            properties:\n              uuid:\n                type: string\n\n    ErrorEvent:\n      name: ErrorEvent\n      title: Raw Error Event\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          sentry-hook-signature:\n            type: string\n          sentry-hook-resource:\n            type: string\n            enum: [event_alert]\n          sentry-hook-timestamp:\n            type: string\n            format: date-time\n      payload:\n        type: object\n        properties:\n          action:\n            type: string\n            enum: [triggered]\n          data:\n            type: object\n            properties:\n              event:\n                type: object\n                properties:\n                  id:\n                    type: string\n                  project:\n                    type:\
  \ string\n                  release:\n                    type: string\n                  environment:\n                    type: string\n                  platform:\n                    type: string\n                  message:\n                    type: string\n                  exception:\n                    type: object\n                  user:\n                    type: object\n                  tags:\n                    type: array\n                    items:\n                      type: array\n                      items:\n                        type: string\n                  timestamp:\n                    type: string\n                    format: date-time\n\n    CommentEvent:\n      name: CommentEvent\n      title: Issue Comment Event\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          sentry-hook-signature:\n            type: string\n          sentry-hook-resource:\n            type: string\n            enum: [comment]\n\
  \      payload:\n        type: object\n        properties:\n          action:\n            type: string\n            enum: [created, updated, deleted]\n          data:\n            type: object\n            properties:\n              comment:\n                type: object\n                properties:\n                  id:\n                    type: integer\n                  text:\n                    type: string\n                  issue_id:\n                    type: string\n                  timestamp:\n                    type: string\n                    format: date-time\n          actor:\n            $ref: '#/components/schemas/Actor'\n\n    InstallEvent:\n      name: InstallEvent\n      title: Integration Installation Event\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          sentry-hook-signature:\n            type: string\n          sentry-hook-resource:\n            type: string\n            enum: [installation]\n      payload:\n\
  \        type: object\n        properties:\n          action:\n            type: string\n            enum: [created, deleted]\n          data:\n            type: object\n            properties:\n              installation:\n                type: object\n                properties:\n                  uuid:\n                    type: string\n                  status:\n                    type: string\n                    enum: [pending, installed]\n                  organization:\n                    type: object\n                    properties:\n                      slug:\n                        type: string\n                      name:\n                        type: string\n                  code:\n                    type: string\n                    description: OAuth authorization code for token exchange\n\n    AlertEvent:\n      name: AlertEvent\n      title: Metric Alert Event\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n     \
  \     sentry-hook-signature:\n            type: string\n          sentry-hook-resource:\n            type: string\n            enum: [metric_alert]\n      payload:\n        type: object\n        properties:\n          action:\n            type: string\n            enum: [resolved, warning, critical]\n          data:\n            type: object\n            properties:\n              metric_alert:\n                type: object\n                properties:\n                  id:\n                    type: string\n                  alert_rule:\n                    type: object\n                    properties:\n                      id:\n                        type: string\n                      name:\n                        type: string\n                      threshold_type:\n                        type: integer\n                  status:\n                    type: string\n                  type:\n                    type: string\n                  date_started:\n                    type:\
  \ string\n                    format: date-time\n                  date_closed:\n                    type: string\n                    format: date-time\n                    nullable: true\n\n  schemas:\n    WebhookIssue:\n      type: object\n      properties:\n        id:\n          type: string\n        shortId:\n          type: string\n        title:\n          type: string\n        culprit:\n          type: string\n        status:\n          type: string\n          enum: [resolved, unresolved, ignored]\n        level:\n          type: string\n          enum: [fatal, error, warning, info, debug]\n        project:\n          type: object\n          properties:\n            id:\n              type: string\n            name:\n              type: string\n            slug:\n              type: string\n        firstSeen:\n          type: string\n          format: date-time\n        lastSeen:\n          type: string\n          format: date-time\n        count:\n          type: string\n   \
  \     userCount:\n          type: integer\n        permalink:\n          type: string\n          format: uri\n\n    Actor:\n      type: object\n      properties:\n        type:\n          type: string\n          enum: [user, application]\n        id:\n          type: string\n        name:\n          type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sentry/refs/heads/main/asyncapi/sentry-webhooks-asyncapi.yml
spec_file: asyncapi/sentry-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/sentry/refs/heads/main/asyncapi/sentry-webhooks-asyncapi.yml
tags:
- Error Monitoring
- Debugging
- Observability
- Application Performance Management
- Developer Tools
- AsyncAPI
- Webhooks
- Events
version: '0'
---
