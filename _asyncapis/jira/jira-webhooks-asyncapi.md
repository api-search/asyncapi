---
api_specs:
- filename: jira-cloud-platform-rest-api-openapi.yml
  format: yaml
  label: Jira Cloud Platform REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/jira/refs/heads/main/openapi/jira-cloud-platform-rest-api-openapi.yml
channels:
- description: The endpoint that receives all Jira Cloud webhook event deliveries. The event type is identified by the webhookEvent field in the JSON payload. Jira retries failed deliveries (non-200 responses) up to 8 times with exponential backoff.
  name: /webhook
  operation: publish
  operation_id: receiveJiraWebhookEvent
  summary: Receive a Jira webhook event
description: Jira Cloud webhooks deliver HTTP POST payloads to a configured URL whenever specified events occur in your Jira instance. Webhooks can be registered via the Jira REST API or through the Jira administration UI. Each webhook delivery includes a JSON payload with details about the event, the affected entities, and a timestamp. Jira supports both dynamic webhooks (registered via REST API with expiration) and static webhooks (configured in app descriptors for Connect apps). Forge apps use a separate event trigger mechanism.
layout: asyncapi
messages:
- description: Triggered when a user creates a new issue. The payload includes the full issue details, the user who created it, and the changelog.
  name: jira:issue_created
  summary: Fired when a new issue is created in Jira.
  title: Issue Created
- description: Triggered when a user updates an issue. This includes field changes, status transitions, comments added, and other modifications. The payload includes the changelog showing what changed.
  name: jira:issue_updated
  summary: Fired when an existing issue is updated in Jira.
  title: Issue Updated
- description: Triggered when a user deletes an issue. The payload includes the issue details as they were before deletion.
  name: jira:issue_deleted
  summary: Fired when an issue is deleted from Jira.
  title: Issue Deleted
- description: Triggered when a user adds a comment to an issue. The payload includes the full comment details and the associated issue.
  name: comment_created
  summary: Fired when a comment is added to an issue.
  title: Comment Created
- description: Triggered when a user edits a comment on an issue. The payload includes the updated comment details and the associated issue.
  name: comment_updated
  summary: Fired when an existing comment on an issue is edited.
  title: Comment Updated
- description: Triggered when a user deletes a comment from an issue. The payload includes the deleted comment details and the associated issue.
  name: comment_deleted
  summary: Fired when a comment is removed from an issue.
  title: Comment Deleted
- description: ''
  name: issuelink_created
  summary: Fired when a link between issues is created.
  title: Issue Link Created
- description: ''
  name: issuelink_deleted
  summary: Fired when a link between issues is removed.
  title: Issue Link Deleted
- description: ''
  name: attachment_created
  summary: Fired when an attachment is added to an issue.
  title: Attachment Created
- description: ''
  name: attachment_deleted
  summary: Fired when an attachment is removed from an issue.
  title: Attachment Deleted
- description: ''
  name: worklog_created
  summary: Fired when a worklog entry is added to an issue.
  title: Worklog Created
- description: ''
  name: worklog_updated
  summary: Fired when a worklog entry is edited on an issue.
  title: Worklog Updated
- description: ''
  name: worklog_deleted
  summary: Fired when a worklog entry is removed from an issue.
  title: Worklog Deleted
- description: ''
  name: project_created
  summary: Fired when a new project is created.
  title: Project Created
- description: ''
  name: project_updated
  summary: Fired when a project is updated.
  title: Project Updated
- description: ''
  name: project_deleted
  summary: Fired when a project is permanently deleted.
  title: Project Deleted
- description: ''
  name: project_soft_deleted
  summary: Fired when a project is moved to the trash.
  title: Project Soft Deleted
- description: ''
  name: project_restored_deleted
  summary: Fired when a project is restored from the trash.
  title: Project Restored from Trash
- description: ''
  name: sprint_created
  summary: Fired when a sprint is created.
  title: Sprint Created
- description: ''
  name: sprint_updated
  summary: Fired when a sprint is updated.
  title: Sprint Updated
- description: ''
  name: sprint_deleted
  summary: Fired when a sprint is deleted.
  title: Sprint Deleted
- description: ''
  name: sprint_started
  summary: Fired when a sprint is started.
  title: Sprint Started
- description: ''
  name: sprint_closed
  summary: Fired when a sprint is closed (completed).
  title: Sprint Closed
- description: ''
  name: board_created
  summary: Fired when a board is created.
  title: Board Created
- description: ''
  name: board_updated
  summary: Fired when a board is updated.
  title: Board Updated
- description: ''
  name: board_deleted
  summary: Fired when a board is deleted.
  title: Board Deleted
- description: ''
  name: user_created
  summary: Fired when a new user is created.
  title: User Created
- description: ''
  name: user_updated
  summary: Fired when a user account is updated.
  title: User Updated
- description: ''
  name: user_deleted
  summary: Fired when a user account is deleted.
  title: User Deleted
- description: ''
  name: option_voting_changed
  summary: Fired when the voting option is enabled or disabled.
  title: Voting Option Changed
- description: ''
  name: option_watching_changed
  summary: Fired when the watching option is enabled or disabled.
  title: Watching Option Changed
- description: ''
  name: option_unassigned_issues_changed
  summary: Fired when the unassigned issues option is changed.
  title: Unassigned Issues Option Changed
- description: ''
  name: option_subtasks_changed
  summary: Fired when the sub-tasks option is enabled or disabled.
  title: Sub-tasks Option Changed
- description: ''
  name: option_attachments_changed
  summary: Fired when the attachments option is enabled or disabled.
  title: Attachments Option Changed
- description: ''
  name: option_issuelinks_changed
  summary: Fired when the issue links option is enabled or disabled.
  title: Issue Links Option Changed
- description: ''
  name: option_timetracking_changed
  summary: Fired when the time tracking option is enabled or disabled.
  title: Time Tracking Option Changed
name: Jira Cloud Webhooks
provider_name: Jira
provider_slug: jira
servers:
- description: Your webhook receiver endpoint. Jira sends POST requests to this URL when subscribed events occur. The URL must be publicly accessible and respond with a 200-level status code within 10 seconds.
  name: webhook-receiver
  protocol: https
  url: '{webhookUrl}'
slug: jira-webhooks-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Jira Cloud Webhooks\n  description: >-\n    Jira Cloud webhooks deliver HTTP POST payloads to a configured URL whenever\n    specified events occur in your Jira instance. Webhooks can be registered\n    via the Jira REST API or through the Jira administration UI. Each webhook\n    delivery includes a JSON payload with details about the event, the affected\n    entities, and a timestamp. Jira supports both dynamic webhooks (registered\n    via REST API with expiration) and static webhooks (configured in app\n    descriptors for Connect apps). Forge apps use a separate event trigger\n    mechanism.\n  version: '3'\n  contact:\n    name: Atlassian Developer Support\n    url: https://developer.atlassian.com/support\n    email: ecosystem@atlassian.com\n  license:\n    name: Atlassian Developer Terms\n    url: https://developer.atlassian.com/platform/marketplace/atlassian-developer-terms/\n  externalDocs:\n    description: Jira Cloud Webhooks Documentation\n\
  \    url: https://developer.atlassian.com/cloud/jira/platform/webhooks/\nservers:\n  webhook-receiver:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your webhook receiver endpoint. Jira sends POST requests to this URL\n      when subscribed events occur. The URL must be publicly accessible and\n      respond with a 200-level status code within 10 seconds.\n    variables:\n      webhookUrl:\n        description: The URL configured to receive Jira webhook deliveries.\nchannels:\n  /webhook:\n    description: >-\n      The endpoint that receives all Jira Cloud webhook event deliveries. The\n      event type is identified by the webhookEvent field in the JSON payload.\n      Jira retries failed deliveries (non-200 responses) up to 8 times with\n      exponential backoff.\n    publish:\n      operationId: receiveJiraWebhookEvent\n      summary: Receive a Jira webhook event\n      description: >-\n        Jira delivers webhook events as HTTP POST requests with JSON\
  \ payloads.\n        Each delivery includes a webhookEvent field identifying the event type,\n        a timestamp, and relevant entity data. The payload structure varies\n        by event type but always includes the webhookEvent and timestamp\n        fields.\n      bindings:\n        http:\n          type: request\n          method: POST\n          headers:\n            type: object\n            properties:\n              Content-Type:\n                type: string\n                enum:\n                  - application/json\n                description: The content type of the webhook payload.\n              User-Agent:\n                type: string\n                description: >-\n                  Identifies the request as originating from Atlassian. Typically\n                  prefixed with Atlassian Webhook.\n              X-Atlassian-Webhook-Identifier:\n                type: string\n                description: A unique identifier for the webhook configuration.\n      message:\n\
  \        oneOf:\n          - $ref: '#/components/messages/jira:issue_created'\n          - $ref: '#/components/messages/jira:issue_updated'\n          - $ref: '#/components/messages/jira:issue_deleted'\n          - $ref: '#/components/messages/comment_created'\n          - $ref: '#/components/messages/comment_updated'\n          - $ref: '#/components/messages/comment_deleted'\n          - $ref: '#/components/messages/issuelink_created'\n          - $ref: '#/components/messages/issuelink_deleted'\n          - $ref: '#/components/messages/attachment_created'\n          - $ref: '#/components/messages/attachment_deleted'\n          - $ref: '#/components/messages/worklog_created'\n          - $ref: '#/components/messages/worklog_updated'\n          - $ref: '#/components/messages/worklog_deleted'\n          - $ref: '#/components/messages/project_created'\n          - $ref: '#/components/messages/project_updated'\n          - $ref: '#/components/messages/project_deleted'\n          - $ref: '#/components/messages/project_soft_deleted'\n\
  \          - $ref: '#/components/messages/project_restored_deleted'\n          - $ref: '#/components/messages/sprint_created'\n          - $ref: '#/components/messages/sprint_updated'\n          - $ref: '#/components/messages/sprint_deleted'\n          - $ref: '#/components/messages/sprint_started'\n          - $ref: '#/components/messages/sprint_closed'\n          - $ref: '#/components/messages/board_created'\n          - $ref: '#/components/messages/board_updated'\n          - $ref: '#/components/messages/board_deleted'\n          - $ref: '#/components/messages/user_created'\n          - $ref: '#/components/messages/user_updated'\n          - $ref: '#/components/messages/user_deleted'\n          - $ref: '#/components/messages/option_voting_changed'\n          - $ref: '#/components/messages/option_watching_changed'\n          - $ref: '#/components/messages/option_unassigned_issues_changed'\n          - $ref: '#/components/messages/option_subtasks_changed'\n          - $ref: '#/components/messages/option_attachments_changed'\n\
  \          - $ref: '#/components/messages/option_issuelinks_changed'\n          - $ref: '#/components/messages/option_timetracking_changed'\ncomponents:\n  messages:\n    jira:issue_created:\n      name: jira:issue_created\n      title: Issue Created\n      summary: Fired when a new issue is created in Jira.\n      description: >-\n        Triggered when a user creates a new issue. The payload includes the\n        full issue details, the user who created it, and the changelog.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/IssueWebhookPayload'\n      examples:\n        - name: Bug created\n          payload:\n            timestamp: 1709478000000\n            webhookEvent: jira:issue_created\n            issue_event_type_name: issue_created\n            user:\n              accountId: 5b10a2844c20165700ede21g\n              displayName: Jane Developer\n              active: true\n            issue:\n              id: '10001'\n              key:\
  \ PROJ-123\n              fields:\n                summary: Login page returns 500 error\n                issuetype:\n                  name: Bug\n                project:\n                  key: PROJ\n                  name: My Project\n                status:\n                  name: To Do\n                priority:\n                  name: High\n    jira:issue_updated:\n      name: jira:issue_updated\n      title: Issue Updated\n      summary: Fired when an existing issue is updated in Jira.\n      description: >-\n        Triggered when a user updates an issue. This includes field changes,\n        status transitions, comments added, and other modifications. The\n        payload includes the changelog showing what changed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/IssueWebhookPayload'\n    jira:issue_deleted:\n      name: jira:issue_deleted\n      title: Issue Deleted\n      summary: Fired when an issue is deleted from Jira.\n      description:\
  \ >-\n        Triggered when a user deletes an issue. The payload includes the issue\n        details as they were before deletion.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/IssueWebhookPayload'\n    comment_created:\n      name: comment_created\n      title: Comment Created\n      summary: Fired when a comment is added to an issue.\n      description: >-\n        Triggered when a user adds a comment to an issue. The payload includes\n        the full comment details and the associated issue.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CommentWebhookPayload'\n    comment_updated:\n      name: comment_updated\n      title: Comment Updated\n      summary: Fired when an existing comment on an issue is edited.\n      description: >-\n        Triggered when a user edits a comment on an issue. The payload includes\n        the updated comment details and the associated issue.\n      contentType: application/json\n\
  \      payload:\n        $ref: '#/components/schemas/CommentWebhookPayload'\n    comment_deleted:\n      name: comment_deleted\n      title: Comment Deleted\n      summary: Fired when a comment is removed from an issue.\n      description: >-\n        Triggered when a user deletes a comment from an issue. The payload\n        includes the deleted comment details and the associated issue.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CommentWebhookPayload'\n    issuelink_created:\n      name: issuelink_created\n      title: Issue Link Created\n      summary: Fired when a link between issues is created.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/IssueLinkWebhookPayload'\n    issuelink_deleted:\n      name: issuelink_deleted\n      title: Issue Link Deleted\n      summary: Fired when a link between issues is removed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/IssueLinkWebhookPayload'\n\
  \    attachment_created:\n      name: attachment_created\n      title: Attachment Created\n      summary: Fired when an attachment is added to an issue.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BaseWebhookPayload'\n    attachment_deleted:\n      name: attachment_deleted\n      title: Attachment Deleted\n      summary: Fired when an attachment is removed from an issue.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BaseWebhookPayload'\n    worklog_created:\n      name: worklog_created\n      title: Worklog Created\n      summary: Fired when a worklog entry is added to an issue.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WorklogWebhookPayload'\n    worklog_updated:\n      name: worklog_updated\n      title: Worklog Updated\n      summary: Fired when a worklog entry is edited on an issue.\n      contentType: application/json\n      payload:\n        $ref:\
  \ '#/components/schemas/WorklogWebhookPayload'\n    worklog_deleted:\n      name: worklog_deleted\n      title: Worklog Deleted\n      summary: Fired when a worklog entry is removed from an issue.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WorklogWebhookPayload'\n    project_created:\n      name: project_created\n      title: Project Created\n      summary: Fired when a new project is created.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ProjectWebhookPayload'\n    project_updated:\n      name: project_updated\n      title: Project Updated\n      summary: Fired when a project is updated.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ProjectWebhookPayload'\n    project_deleted:\n      name: project_deleted\n      title: Project Deleted\n      summary: Fired when a project is permanently deleted.\n      contentType: application/json\n      payload:\n   \
  \     $ref: '#/components/schemas/ProjectWebhookPayload'\n    project_soft_deleted:\n      name: project_soft_deleted\n      title: Project Soft Deleted\n      summary: Fired when a project is moved to the trash.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ProjectWebhookPayload'\n    project_restored_deleted:\n      name: project_restored_deleted\n      title: Project Restored from Trash\n      summary: Fired when a project is restored from the trash.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ProjectWebhookPayload'\n    sprint_created:\n      name: sprint_created\n      title: Sprint Created\n      summary: Fired when a sprint is created.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SprintWebhookPayload'\n    sprint_updated:\n      name: sprint_updated\n      title: Sprint Updated\n      summary: Fired when a sprint is updated.\n      contentType: application/json\n\
  \      payload:\n        $ref: '#/components/schemas/SprintWebhookPayload'\n    sprint_deleted:\n      name: sprint_deleted\n      title: Sprint Deleted\n      summary: Fired when a sprint is deleted.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SprintWebhookPayload'\n    sprint_started:\n      name: sprint_started\n      title: Sprint Started\n      summary: Fired when a sprint is started.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SprintWebhookPayload'\n    sprint_closed:\n      name: sprint_closed\n      title: Sprint Closed\n      summary: Fired when a sprint is closed (completed).\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SprintWebhookPayload'\n    board_created:\n      name: board_created\n      title: Board Created\n      summary: Fired when a board is created.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BoardWebhookPayload'\n\
  \    board_updated:\n      name: board_updated\n      title: Board Updated\n      summary: Fired when a board is updated.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BoardWebhookPayload'\n    board_deleted:\n      name: board_deleted\n      title: Board Deleted\n      summary: Fired when a board is deleted.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BoardWebhookPayload'\n    user_created:\n      name: user_created\n      title: User Created\n      summary: Fired when a new user is created.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/UserWebhookPayload'\n    user_updated:\n      name: user_updated\n      title: User Updated\n      summary: Fired when a user account is updated.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/UserWebhookPayload'\n    user_deleted:\n      name: user_deleted\n      title: User Deleted\n\
  \      summary: Fired when a user account is deleted.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/UserWebhookPayload'\n    option_voting_changed:\n      name: option_voting_changed\n      title: Voting Option Changed\n      summary: Fired when the voting option is enabled or disabled.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BaseWebhookPayload'\n    option_watching_changed:\n      name: option_watching_changed\n      title: Watching Option Changed\n      summary: Fired when the watching option is enabled or disabled.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BaseWebhookPayload'\n    option_unassigned_issues_changed:\n      name: option_unassigned_issues_changed\n      title: Unassigned Issues Option Changed\n      summary: Fired when the unassigned issues option is changed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BaseWebhookPayload'\n\
  \    option_subtasks_changed:\n      name: option_subtasks_changed\n      title: Sub-tasks Option Changed\n      summary: Fired when the sub-tasks option is enabled or disabled.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BaseWebhookPayload'\n    option_attachments_changed:\n      name: option_attachments_changed\n      title: Attachments Option Changed\n      summary: Fired when the attachments option is enabled or disabled.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BaseWebhookPayload'\n    option_issuelinks_changed:\n      name: option_issuelinks_changed\n      title: Issue Links Option Changed\n      summary: Fired when the issue links option is enabled or disabled.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BaseWebhookPayload'\n    option_timetracking_changed:\n      name: option_timetracking_changed\n      title: Time Tracking Option Changed\n\
  \      summary: Fired when the time tracking option is enabled or disabled.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BaseWebhookPayload'\n  schemas:\n    BaseWebhookPayload:\n      type: object\n      description: Base fields present in all Jira webhook payloads.\n      required:\n        - timestamp\n        - webhookEvent\n      properties:\n        timestamp:\n          type: integer\n          format: int64\n          description: >-\n            The Unix timestamp (in milliseconds) of when the event occurred.\n        webhookEvent:\n          type: string\n          description: >-\n            The event type identifier (e.g., jira:issue_created,\n            jira:issue_updated, project_created).\n        matchedWebhookIds:\n          type: array\n          description: The IDs of the webhooks that matched this event.\n          items:\n            type: integer\n    IssueWebhookPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseWebhookPayload'\n\
  \        - type: object\n          properties:\n            issue_event_type_name:\n              type: string\n              description: >-\n                The specific issue event type (e.g., issue_created,\n                issue_updated, issue_generic, issue_assigned,\n                issue_comment_edited).\n            user:\n              $ref: '#/components/schemas/WebhookUser'\n            issue:\n              $ref: '#/components/schemas/WebhookIssue'\n            changelog:\n              $ref: '#/components/schemas/WebhookChangelog'\n    CommentWebhookPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseWebhookPayload'\n        - type: object\n          properties:\n            user:\n              $ref: '#/components/schemas/WebhookUser'\n            issue:\n              $ref: '#/components/schemas/WebhookIssue'\n            comment:\n              $ref: '#/components/schemas/WebhookComment'\n    IssueLinkWebhookPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseWebhookPayload'\n\
  \        - type: object\n          properties:\n            issueLink:\n              type: object\n              properties:\n                id:\n                  type: integer\n                  format: int64\n                sourceIssueId:\n                  type: integer\n                  format: int64\n                destinationIssueId:\n                  type: integer\n                  format: int64\n                issueLinkType:\n                  type: object\n                  properties:\n                    id:\n                      type: integer\n                      format: int64\n                    name:\n                      type: string\n                    outwardName:\n                      type: string\n                    inwardName:\n                      type: string\n    WorklogWebhookPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseWebhookPayload'\n        - type: object\n          properties:\n            worklog:\n              type:\
  \ object\n              properties:\n                id:\n                  type: integer\n                  format: int64\n                self:\n                  type: string\n                  format: uri\n                author:\n                  $ref: '#/components/schemas/WebhookUser'\n                updateAuthor:\n                  $ref: '#/components/schemas/WebhookUser'\n                timeSpent:\n                  type: string\n                timeSpentSeconds:\n                  type: integer\n                  format: int64\n                created:\n                  type: string\n                  format: date-time\n                updated:\n                  type: string\n                  format: date-time\n                started:\n                  type: string\n                  format: date-time\n                issueId:\n                  type: integer\n                  format: int64\n    ProjectWebhookPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseWebhookPayload'\n\
  \        - type: object\n          properties:\n            project:\n              type: object\n              properties:\n                id:\n                  type: integer\n                  format: int64\n                key:\n                  type: string\n                name:\n                  type: string\n                description:\n                  type: string\n                projectTypeKey:\n                  type: string\n                self:\n                  type: string\n                  format: uri\n                projectLead:\n                  $ref: '#/components/schemas/WebhookUser'\n    SprintWebhookPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseWebhookPayload'\n        - type: object\n          properties:\n            sprint:\n              type: object\n              properties:\n                id:\n                  type: integer\n                  format: int64\n                self:\n                  type: string\n          \
  \        format: uri\n                state:\n                  type: string\n                  enum:\n                    - future\n                    - active\n                    - closed\n                name:\n                  type: string\n                startDate:\n                  type: string\n                  format: date-time\n                endDate:\n                  type: string\n                  format: date-time\n                completeDate:\n                  type: string\n                  format: date-time\n                originBoardId:\n                  type: integer\n                  format: int64\n                goal:\n                  type: string\n    BoardWebhookPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseWebhookPayload'\n        - type: object\n          properties:\n            board:\n              type: object\n              properties:\n                id:\n                  type: integer\n                  format: int64\n\
  \                self:\n                  type: string\n                  format: uri\n                name:\n                  type: string\n                type:\n                  type: string\n                  enum:\n                    - scrum\n                    - kanban\n                    - simple\n    UserWebhookPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseWebhookPayload'\n        - type: object\n          properties:\n            user:\n              $ref: '#/components/schemas/WebhookUser'\n    WebhookUser:\n      type: object\n      description: A user as represented in webhook payloads.\n      properties:\n        self:\n          type: string\n          format: uri\n        accountId:\n          type: string\n          description: The account ID of the user.\n        accountType:\n          type: string\n          enum:\n            - atlassian\n            - app\n            - customer\n        displayName:\n          type: string\n        active:\n\
  \          type: boolean\n        timeZone:\n          type: string\n        avatarUrls:\n          type: object\n          properties:\n            16x16:\n              type: string\n              format: uri\n            24x24:\n              type: string\n              format: uri\n            32x32:\n              type: string\n              format: uri\n            48x48:\n              type: string\n              format: uri\n    WebhookIssue:\n      type: object\n      description: An issue as represented in webhook payloads.\n      properties:\n        id:\n          type: string\n        key:\n          type: string\n        self:\n          type: string\n          format: uri\n        fields:\n          type: object\n          properties:\n            summary:\n              type: string\n            description:\n              type: object\n              description: Atlassian Document Format (ADF) representation.\n            issuetype:\n              type: object\n      \
  \        properties:\n                id:\n                  type: string\n                name:\n                  type: string\n                subtask:\n                  type: boolean\n                iconUrl:\n                  type: string\n                  format: uri\n            project:\n              type: object\n              properties:\n                id:\n                  type: string\n                key:\n                  type: string\n                name:\n                  type: string\n                projectTypeKey:\n                  type: string\n            status:\n              type: object\n              properties:\n                id:\n                  type: string\n                name:\n                  type: string\n                statusCategory:\n                  type: object\n                  properties:\n                    id:\n                      type: integer\n                    key:\n                      type: string\n             \
  \       name:\n                      type: string\n            priority:\n              type: object\n              properties:\n                id:\n                  type: string\n                name:\n                  type: string\n                iconUrl:\n                  type: string\n                  format: uri\n            assignee:\n              $ref: '#/components/schemas/WebhookUser'\n            reporter:\n              $ref: '#/components/schemas/WebhookUser'\n            creator:\n              $ref: '#/components/schemas/WebhookUser'\n            labels:\n              type: array\n              items:\n                type: string\n            created:\n              type: string\n              format: date-time\n            updated:\n              type: string\n              format: date-time\n            resolution:\n              type: object\n              properties:\n                id:\n                  type: string\n                name:\n               \
  \   type: string\n          additionalProperties: true\n    WebhookComment:\n      type: object\n      description: A comment as represented in webhook payloads.\n      properties:\n        self:\n          type: string\n          format: uri\n        id:\n          type: string\n        author:\n          $ref: '#/components/schemas/WebhookUser'\n        body:\n          type: object\n          description: The comment body in ADF.\n        updateAuthor:\n          $ref: '#/components/schemas/WebhookUser'\n        created:\n          type: string\n          format: date-time\n        updated:\n          type: string\n          format: date-time\n    WebhookChangelog:\n      type: object\n      description: A changelog included with issue update webhook events.\n      properties:\n        id:\n          type: string\n        items:\n          type: array\n          items:\n            type: object\n            properties:\n              field:\n                type: string\n          \
  \      description: The human-readable name of the field changed.\n              fieldtype:\n                type: string\n                description: The type of the field (e.g., jira, custom).\n              fieldId:\n                type: string\n                description: The ID of the field changed.\n              from:\n                type:\n                  - string\n                  - 'null'\n                description: The previous value ID.\n              fromString:\n                type:\n                  - string\n                  - 'null'\n                description: The previous value as a string.\n              to:\n                type:\n                  - string\n                  - 'null'\n                description: The new value ID.\n              toString:\n                type:\n                  - string\n                  - 'null'\n                description: The new value as a string.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/jira/refs/heads/main/asyncapi/jira-webhooks-asyncapi.yml
spec_file: asyncapi/jira-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/jira/refs/heads/main/asyncapi/jira-webhooks-asyncapi.yml
tags:
- Agile
- Issue Tracking
- ITSM
- Project Management
- Service Management
- AsyncAPI
- Webhooks
- Events
version: '3'
---
