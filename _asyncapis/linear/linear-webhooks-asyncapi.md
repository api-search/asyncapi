---
api_specs:
- filename: linear-graphql-openapi.yml
  format: yaml
  label: Linear GraphQL API
  slug: linear-graphql-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/linear/refs/heads/main/openapi/linear-graphql-openapi.yml
- filename: linear-webhooks-asyncapi.yml
  format: yaml
  label: Linear Webhooks API
  slug: linear-webhooks-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/linear/refs/heads/main/asyncapi/linear-webhooks-asyncapi.yml
channels:
- description: Fired when a new issue is created
  name: issue/created
  operation: subscribe
  operation_id: onIssueCreated
  summary: Issue created
- description: Fired when an issue is updated
  name: issue/updated
  operation: subscribe
  operation_id: onIssueUpdated
  summary: Issue updated
- description: Fired when an issue is deleted or trashed
  name: issue/removed
  operation: subscribe
  operation_id: onIssueRemoved
  summary: Issue removed
- description: Fired when a comment is added to an issue
  name: comment/created
  operation: subscribe
  operation_id: onCommentCreated
  summary: Comment created
- description: Fired when a comment is edited
  name: comment/updated
  operation: subscribe
  operation_id: onCommentUpdated
  summary: Comment updated
- description: Fired when a project is created
  name: project/created
  operation: subscribe
  operation_id: onProjectCreated
  summary: Project created
- description: Fired when a project is updated
  name: project/updated
  operation: subscribe
  operation_id: onProjectUpdated
  summary: Project updated
- description: Fired when a cycle (sprint) is created
  name: cycle/created
  operation: subscribe
  operation_id: onCycleCreated
  summary: Cycle created
- description: Fired when an issue label is created
  name: issueLabelCreated
  operation: subscribe
  operation_id: onIssueLabelCreated
  summary: Issue label created
description: Linear webhooks deliver HTTP push notifications whenever data is created, updated, or removed. Webhooks are organization-scoped and can be configured for all public teams or a single team, enabling integrations that trigger CI builds, update external systems, or send messages based on issue activity.
layout: asyncapi
messages:
- description: ''
  name: IssueCreated
  summary: Payload for issue.create webhook events
  title: Issue Created Event
- description: ''
  name: IssueUpdated
  summary: Payload for issue.update webhook events
  title: Issue Updated Event
- description: ''
  name: IssueRemoved
  summary: Payload for issue.remove webhook events
  title: Issue Removed Event
- description: ''
  name: CommentCreated
  summary: Payload for comment.create webhook events
  title: Comment Created Event
- description: ''
  name: CommentUpdated
  summary: Payload for comment.update webhook events
  title: Comment Updated Event
- description: ''
  name: ProjectCreated
  summary: Payload for project.create webhook events
  title: Project Created Event
- description: ''
  name: ProjectUpdated
  summary: Payload for project.update webhook events
  title: Project Updated Event
- description: ''
  name: CycleCreated
  summary: Payload for cycle.create webhook events
  title: Cycle Created Event
- description: ''
  name: IssueLabelCreated
  summary: Payload for issueLabel.create webhook events
  title: Issue Label Created Event
name: Linear Webhooks API
provider_name: linear
provider_slug: linear
servers:
- description: Linear production server (webhook source)
  name: production
  protocol: https
  url: https://api.linear.app
slug: linear-webhooks-asyncapi
source_filename: linear-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Linear Webhooks API\n  version: 2.0.0\n  description: >-\n    Linear webhooks deliver HTTP push notifications whenever data is created,\n    updated, or removed. Webhooks are organization-scoped and can be configured\n    for all public teams or a single team, enabling integrations that trigger\n    CI builds, update external systems, or send messages based on issue activity.\n  contact:\n    name: Linear Support\n    url: https://linear.app/contact/support\n  license:\n    name: Proprietary\n    url: https://linear.app/terms\nexternalDocs:\n  description: Linear Webhooks Documentation\n  url: https://linear.app/developers/webhooks\nservers:\n  production:\n    url: https://api.linear.app\n    protocol: https\n    description: Linear production server (webhook source)\ndefaultContentType: application/json\nchannels:\n  issue/created:\n    description: Fired when a new issue is created\n    subscribe:\n      operationId: onIssueCreated\n    \
  \  summary: Issue created\n      description: >-\n        Delivered when a new issue is created in a team. Contains the full issue\n        object including title, state, assignee, priority, and team.\n      tags:\n        - name: Issues\n      message:\n        $ref: '#/components/messages/IssueCreated'\n  issue/updated:\n    description: Fired when an issue is updated\n    subscribe:\n      operationId: onIssueUpdated\n      summary: Issue updated\n      description: >-\n        Delivered when any field of an issue changes including state transitions,\n        assignee changes, priority updates, and label modifications.\n      tags:\n        - name: Issues\n      message:\n        $ref: '#/components/messages/IssueUpdated'\n  issue/removed:\n    description: Fired when an issue is deleted or trashed\n    subscribe:\n      operationId: onIssueRemoved\n      summary: Issue removed\n      description: Delivered when an issue is deleted or moved to trash.\n      tags:\n        - name: Issues\n\
  \      message:\n        $ref: '#/components/messages/IssueRemoved'\n  comment/created:\n    description: Fired when a comment is added to an issue\n    subscribe:\n      operationId: onCommentCreated\n      summary: Comment created\n      description: >-\n        Delivered when a new comment is added to an issue or a reply is added\n        to an existing comment.\n      tags:\n        - name: Comments\n      message:\n        $ref: '#/components/messages/CommentCreated'\n  comment/updated:\n    description: Fired when a comment is edited\n    subscribe:\n      operationId: onCommentUpdated\n      summary: Comment updated\n      description: Delivered when the body of a comment is edited by its author.\n      tags:\n        - name: Comments\n      message:\n        $ref: '#/components/messages/CommentUpdated'\n  project/created:\n    description: Fired when a project is created\n    subscribe:\n      operationId: onProjectCreated\n      summary: Project created\n      description: Delivered\
  \ when a new project is created within the organization.\n      tags:\n        - name: Projects\n      message:\n        $ref: '#/components/messages/ProjectCreated'\n  project/updated:\n    description: Fired when a project is updated\n    subscribe:\n      operationId: onProjectUpdated\n      summary: Project updated\n      description: >-\n        Delivered when project details, state, milestones, or member lists change.\n      tags:\n        - name: Projects\n      message:\n        $ref: '#/components/messages/ProjectUpdated'\n  cycle/created:\n    description: Fired when a cycle (sprint) is created\n    subscribe:\n      operationId: onCycleCreated\n      summary: Cycle created\n      description: Delivered when a new cycle is created in a team.\n      tags:\n        - name: Cycles\n      message:\n        $ref: '#/components/messages/CycleCreated'\n  issueLabelCreated:\n    description: Fired when an issue label is created\n    subscribe:\n      operationId: onIssueLabelCreated\n\
  \      summary: Issue label created\n      description: Delivered when a new label is created in a team.\n      tags:\n        - name: Labels\n      message:\n        $ref: '#/components/messages/IssueLabelCreated'\ncomponents:\n  messages:\n    IssueCreated:\n      name: IssueCreated\n      title: Issue Created Event\n      summary: Payload for issue.create webhook events\n      payload:\n        $ref: '#/components/schemas/IssueWebhookPayload'\n    IssueUpdated:\n      name: IssueUpdated\n      title: Issue Updated Event\n      summary: Payload for issue.update webhook events\n      payload:\n        $ref: '#/components/schemas/IssueWebhookPayload'\n    IssueRemoved:\n      name: IssueRemoved\n      title: Issue Removed Event\n      summary: Payload for issue.remove webhook events\n      payload:\n        $ref: '#/components/schemas/IssueWebhookPayload'\n    CommentCreated:\n      name: CommentCreated\n      title: Comment Created Event\n      summary: Payload for comment.create webhook\
  \ events\n      payload:\n        $ref: '#/components/schemas/CommentWebhookPayload'\n    CommentUpdated:\n      name: CommentUpdated\n      title: Comment Updated Event\n      summary: Payload for comment.update webhook events\n      payload:\n        $ref: '#/components/schemas/CommentWebhookPayload'\n    ProjectCreated:\n      name: ProjectCreated\n      title: Project Created Event\n      summary: Payload for project.create webhook events\n      payload:\n        $ref: '#/components/schemas/ProjectWebhookPayload'\n    ProjectUpdated:\n      name: ProjectUpdated\n      title: Project Updated Event\n      summary: Payload for project.update webhook events\n      payload:\n        $ref: '#/components/schemas/ProjectWebhookPayload'\n    CycleCreated:\n      name: CycleCreated\n      title: Cycle Created Event\n      summary: Payload for cycle.create webhook events\n      payload:\n        $ref: '#/components/schemas/CycleWebhookPayload'\n    IssueLabelCreated:\n      name: IssueLabelCreated\n\
  \      title: Issue Label Created Event\n      summary: Payload for issueLabel.create webhook events\n      payload:\n        $ref: '#/components/schemas/IssueLabelWebhookPayload'\n  schemas:\n    WebhookBase:\n      type: object\n      required:\n        - action\n      properties:\n        action:\n          type: string\n          enum: [create, update, remove]\n          description: The type of action that triggered the webhook\n        organizationId:\n          type: string\n          description: ID of the organization that owns the webhook\n        webhookTimestamp:\n          type: integer\n          description: Unix timestamp (ms) when the webhook was fired\n        webhookId:\n          type: string\n          description: UUID of the webhook configuration\n        type:\n          type: string\n          description: The entity type (e.g., Issue, Comment, Project)\n    IssueWebhookPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type:\
  \ object\n          properties:\n            type:\n              type: string\n              enum: [Issue]\n            data:\n              type: object\n              description: The full issue object\n              properties:\n                id:\n                  type: string\n                identifier:\n                  type: string\n                title:\n                  type: string\n                description:\n                  type: string\n                priority:\n                  type: integer\n                  enum: [0, 1, 2, 3, 4]\n                state:\n                  type: object\n                  properties:\n                    id: { type: string }\n                    name: { type: string }\n                    type: { type: string }\n                assignee:\n                  type: object\n                  properties:\n                    id: { type: string }\n                    name: { type: string }\n                    email: { type: string\
  \ }\n                team:\n                  type: object\n                  properties:\n                    id: { type: string }\n                    name: { type: string }\n                    key: { type: string }\n                url:\n                  type: string\n                  format: uri\n                createdAt:\n                  type: string\n                  format: date-time\n                updatedAt:\n                  type: string\n                  format: date-time\n            updatedFrom:\n              type: object\n              description: Previous values for updated fields (only on update events)\n              additionalProperties: true\n    CommentWebhookPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type: object\n          properties:\n            type:\n              type: string\n              enum: [Comment]\n            data:\n              type: object\n              properties:\n                id:\n   \
  \               type: string\n                body:\n                  type: string\n                user:\n                  type: object\n                  properties:\n                    id: { type: string }\n                    name: { type: string }\n                issue:\n                  type: object\n                  properties:\n                    id: { type: string }\n                    identifier: { type: string }\n                    title: { type: string }\n                createdAt:\n                  type: string\n                  format: date-time\n                updatedAt:\n                  type: string\n                  format: date-time\n    ProjectWebhookPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type: object\n          properties:\n            type:\n              type: string\n              enum: [Project]\n            data:\n              type: object\n              properties:\n                id:\n          \
  \        type: string\n                name:\n                  type: string\n                description:\n                  type: string\n                state:\n                  type: string\n                  enum: [planned, started, paused, completed, cancelled]\n                createdAt:\n                  type: string\n                  format: date-time\n                updatedAt:\n                  type: string\n                  format: date-time\n    CycleWebhookPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type: object\n          properties:\n            type:\n              type: string\n              enum: [Cycle]\n            data:\n              type: object\n              properties:\n                id:\n                  type: string\n                number:\n                  type: integer\n                name:\n                  type: string\n                startsAt:\n                  type: string\n                  format:\
  \ date-time\n                endsAt:\n                  type: string\n                  format: date-time\n                teamId:\n                  type: string\n    IssueLabelWebhookPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type: object\n          properties:\n            type:\n              type: string\n              enum: [IssueLabel]\n            data:\n              type: object\n              properties:\n                id:\n                  type: string\n                name:\n                  type: string\n                color:\n                  type: string\n                teamId:\n                  type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/linear/refs/heads/main/asyncapi/linear-webhooks-asyncapi.yml
spec_file: asyncapi/linear-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/linear/refs/heads/main/asyncapi/linear-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: 2.0.0
---
