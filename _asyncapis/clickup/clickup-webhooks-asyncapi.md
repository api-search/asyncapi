---
channels:
- description: Channel for all ClickUp webhook events. Events are delivered as HTTP POST requests with a JSON body. The X-Signature header contains the HMAC-SHA256 signature for payload verification.
  name: /webhook
  operation: publish
  operation_id: receiveWebhookEvent
  summary: Receive a webhook event from ClickUp
description: The ClickUp Webhooks event system delivers real-time notifications when changes occur within a ClickUp Workspace. When subscribed events happen, ClickUp sends HTTP POST requests to a registered endpoint URL with a JSON payload describing the event. Each payload is signed using HMAC-SHA256 with a shared secret for verification. Events cover tasks, lists, folders, spaces, goals, and key results.
layout: asyncapi
messages:
- description: Triggered when a new task is created within the subscribed scope.
  name: TaskCreated
  summary: A new task was created
  title: Task Created
- description: Triggered when a task field is modified. The history_items array contains the specific field changes with before and after values.
  name: TaskUpdated
  summary: A task was updated
  title: Task Updated
- description: Triggered when a task is permanently deleted.
  name: TaskDeleted
  summary: A task was deleted
  title: Task Deleted
- description: Triggered when a task's status changes. The history_items include the previous and new status values.
  name: TaskStatusUpdated
  summary: A task status was changed
  title: Task Status Updated
- description: Triggered when assignees are added to or removed from a task.
  name: TaskAssigneeUpdated
  summary: A task assignee was added or removed
  title: Task Assignee Updated
- description: Triggered when a task's priority level is changed.
  name: TaskPriorityUpdated
  summary: A task priority was changed
  title: Task Priority Updated
- description: Triggered when a task's due date is set, changed, or removed.
  name: TaskDueDateUpdated
  summary: A task due date was changed
  title: Task Due Date Updated
- description: Triggered when tags are added to or removed from a task.
  name: TaskTagUpdated
  summary: A task tag was added or removed
  title: Task Tag Updated
- description: Triggered when a task is moved from one list to another.
  name: TaskMoved
  summary: A task was moved to a different list
  title: Task Moved
- description: Triggered when a new comment is added to a task.
  name: TaskCommentPosted
  summary: A comment was posted on a task
  title: Task Comment Posted
- description: Triggered when an existing comment on a task is modified.
  name: TaskCommentUpdated
  summary: A comment on a task was updated
  title: Task Comment Updated
- description: Triggered when a task's time estimate is set or modified.
  name: TaskTimeEstimateUpdated
  summary: A task time estimate was changed
  title: Task Time Estimate Updated
- description: Triggered when a time entry is added, modified, or deleted on a task.
  name: TaskTimeTrackedUpdated
  summary: Time tracked on a task was updated
  title: Task Time Tracked Updated
- description: Triggered when a new list is created within the subscribed scope.
  name: ListCreated
  summary: A new list was created
  title: List Created
- description: Triggered when a list's properties are modified.
  name: ListUpdated
  summary: A list was updated
  title: List Updated
- description: Triggered when a list is permanently deleted.
  name: ListDeleted
  summary: A list was deleted
  title: List Deleted
- description: Triggered when a new folder is created within the subscribed scope.
  name: FolderCreated
  summary: A new folder was created
  title: Folder Created
- description: Triggered when a folder's properties are modified.
  name: FolderUpdated
  summary: A folder was updated
  title: Folder Updated
- description: Triggered when a folder is permanently deleted.
  name: FolderDeleted
  summary: A folder was deleted
  title: Folder Deleted
- description: Triggered when a new space is created within the Workspace.
  name: SpaceCreated
  summary: A new space was created
  title: Space Created
- description: Triggered when a space's properties are modified.
  name: SpaceUpdated
  summary: A space was updated
  title: Space Updated
- description: Triggered when a space is permanently deleted.
  name: SpaceDeleted
  summary: A space was deleted
  title: Space Deleted
- description: Triggered when a new goal is created within the Workspace.
  name: GoalCreated
  summary: A new goal was created
  title: Goal Created
- description: Triggered when a goal's properties are modified.
  name: GoalUpdated
  summary: A goal was updated
  title: Goal Updated
- description: Triggered when a goal is permanently deleted.
  name: GoalDeleted
  summary: A goal was deleted
  title: Goal Deleted
- description: Triggered when a new key result is added to a goal.
  name: KeyResultCreated
  summary: A new key result was created
  title: Key Result Created
- description: Triggered when a key result's progress or properties are modified.
  name: KeyResultUpdated
  summary: A key result was updated
  title: Key Result Updated
- description: Triggered when a key result is permanently deleted from a goal.
  name: KeyResultDeleted
  summary: A key result was deleted
  title: Key Result Deleted
name: ClickUp Webhooks Events
provider_name: clickup
provider_slug: clickup
servers:
- description: The HTTPS endpoint URL registered when creating a webhook subscription. ClickUp sends event payloads as POST requests to this URL.
  name: webhookEndpoint
  protocol: https
  url: '{webhookUrl}'
slug: clickup-webhooks-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: ClickUp Webhooks Events\n  description: >-\n    The ClickUp Webhooks event system delivers real-time notifications when\n    changes occur within a ClickUp Workspace. When subscribed events happen,\n    ClickUp sends HTTP POST requests to a registered endpoint URL with a\n    JSON payload describing the event. Each payload is signed using\n    HMAC-SHA256 with a shared secret for verification. Events cover tasks,\n    lists, folders, spaces, goals, and key results.\n  version: '2.0'\n  contact:\n    name: ClickUp Support\n    url: https://help.clickup.com\n  license:\n    name: ClickUp API Terms\n    url: https://clickup.com/terms\nservers:\n  webhookEndpoint:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      The HTTPS endpoint URL registered when creating a webhook subscription.\n      ClickUp sends event payloads as POST requests to this URL.\n    variables:\n      webhookUrl:\n        description: >-\n          The\
  \ URL configured as the webhook endpoint during webhook creation.\n    security:\n      - hmacSignature: []\nchannels:\n  /webhook:\n    description: >-\n      Channel for all ClickUp webhook events. Events are delivered as HTTP\n      POST requests with a JSON body. The X-Signature header contains the\n      HMAC-SHA256 signature for payload verification.\n    publish:\n      operationId: receiveWebhookEvent\n      summary: Receive a webhook event from ClickUp\n      description: >-\n        ClickUp publishes webhook events to the registered endpoint. Each\n        event includes the event type, webhook ID, and event-specific data\n        in the history_items array. The payload is signed with the shared\n        secret using HMAC-SHA256.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/TaskCreated'\n          - $ref: '#/components/messages/TaskUpdated'\n          - $ref: '#/components/messages/TaskDeleted'\n          - $ref: '#/components/messages/TaskStatusUpdated'\n\
  \          - $ref: '#/components/messages/TaskAssigneeUpdated'\n          - $ref: '#/components/messages/TaskPriorityUpdated'\n          - $ref: '#/components/messages/TaskDueDateUpdated'\n          - $ref: '#/components/messages/TaskTagUpdated'\n          - $ref: '#/components/messages/TaskMoved'\n          - $ref: '#/components/messages/TaskCommentPosted'\n          - $ref: '#/components/messages/TaskCommentUpdated'\n          - $ref: '#/components/messages/TaskTimeEstimateUpdated'\n          - $ref: '#/components/messages/TaskTimeTrackedUpdated'\n          - $ref: '#/components/messages/ListCreated'\n          - $ref: '#/components/messages/ListUpdated'\n          - $ref: '#/components/messages/ListDeleted'\n          - $ref: '#/components/messages/FolderCreated'\n          - $ref: '#/components/messages/FolderUpdated'\n          - $ref: '#/components/messages/FolderDeleted'\n          - $ref: '#/components/messages/SpaceCreated'\n          - $ref: '#/components/messages/SpaceUpdated'\n\
  \          - $ref: '#/components/messages/SpaceDeleted'\n          - $ref: '#/components/messages/GoalCreated'\n          - $ref: '#/components/messages/GoalUpdated'\n          - $ref: '#/components/messages/GoalDeleted'\n          - $ref: '#/components/messages/KeyResultCreated'\n          - $ref: '#/components/messages/KeyResultUpdated'\n          - $ref: '#/components/messages/KeyResultDeleted'\ncomponents:\n  securitySchemes:\n    hmacSignature:\n      type: httpApiKey\n      name: X-Signature\n      in: header\n      description: >-\n        HMAC-SHA256 signature of the request body, signed with the shared\n        secret returned when the webhook was created. Verify by computing\n        HMAC-SHA256 of the raw request body using the secret and comparing\n        with the X-Signature header value.\n  messages:\n    TaskCreated:\n      name: taskCreated\n      title: Task Created\n      summary: A new task was created\n      description: >-\n        Triggered when a new task is created\
  \ within the subscribed scope.\n      payload:\n        $ref: '#/components/schemas/TaskWebhookPayload'\n    TaskUpdated:\n      name: taskUpdated\n      title: Task Updated\n      summary: A task was updated\n      description: >-\n        Triggered when a task field is modified. The history_items array\n        contains the specific field changes with before and after values.\n      payload:\n        $ref: '#/components/schemas/TaskWebhookPayload'\n    TaskDeleted:\n      name: taskDeleted\n      title: Task Deleted\n      summary: A task was deleted\n      description: >-\n        Triggered when a task is permanently deleted.\n      payload:\n        $ref: '#/components/schemas/TaskWebhookPayload'\n    TaskStatusUpdated:\n      name: taskStatusUpdated\n      title: Task Status Updated\n      summary: A task status was changed\n      description: >-\n        Triggered when a task's status changes. The history_items include\n        the previous and new status values.\n      payload:\n\
  \        $ref: '#/components/schemas/TaskWebhookPayload'\n    TaskAssigneeUpdated:\n      name: taskAssigneeUpdated\n      title: Task Assignee Updated\n      summary: A task assignee was added or removed\n      description: >-\n        Triggered when assignees are added to or removed from a task.\n      payload:\n        $ref: '#/components/schemas/TaskWebhookPayload'\n    TaskPriorityUpdated:\n      name: taskPriorityUpdated\n      title: Task Priority Updated\n      summary: A task priority was changed\n      description: >-\n        Triggered when a task's priority level is changed.\n      payload:\n        $ref: '#/components/schemas/TaskWebhookPayload'\n    TaskDueDateUpdated:\n      name: taskDueDateUpdated\n      title: Task Due Date Updated\n      summary: A task due date was changed\n      description: >-\n        Triggered when a task's due date is set, changed, or removed.\n      payload:\n        $ref: '#/components/schemas/TaskWebhookPayload'\n    TaskTagUpdated:\n      name:\
  \ taskTagUpdated\n      title: Task Tag Updated\n      summary: A task tag was added or removed\n      description: >-\n        Triggered when tags are added to or removed from a task.\n      payload:\n        $ref: '#/components/schemas/TaskWebhookPayload'\n    TaskMoved:\n      name: taskMoved\n      title: Task Moved\n      summary: A task was moved to a different list\n      description: >-\n        Triggered when a task is moved from one list to another.\n      payload:\n        $ref: '#/components/schemas/TaskWebhookPayload'\n    TaskCommentPosted:\n      name: taskCommentPosted\n      title: Task Comment Posted\n      summary: A comment was posted on a task\n      description: >-\n        Triggered when a new comment is added to a task.\n      payload:\n        $ref: '#/components/schemas/TaskWebhookPayload'\n    TaskCommentUpdated:\n      name: taskCommentUpdated\n      title: Task Comment Updated\n      summary: A comment on a task was updated\n      description: >-\n        Triggered\
  \ when an existing comment on a task is modified.\n      payload:\n        $ref: '#/components/schemas/TaskWebhookPayload'\n    TaskTimeEstimateUpdated:\n      name: taskTimeEstimateUpdated\n      title: Task Time Estimate Updated\n      summary: A task time estimate was changed\n      description: >-\n        Triggered when a task's time estimate is set or modified.\n      payload:\n        $ref: '#/components/schemas/TaskWebhookPayload'\n    TaskTimeTrackedUpdated:\n      name: taskTimeTrackedUpdated\n      title: Task Time Tracked Updated\n      summary: Time tracked on a task was updated\n      description: >-\n        Triggered when a time entry is added, modified, or deleted on a task.\n      payload:\n        $ref: '#/components/schemas/TaskWebhookPayload'\n    ListCreated:\n      name: listCreated\n      title: List Created\n      summary: A new list was created\n      description: >-\n        Triggered when a new list is created within the subscribed scope.\n      payload:\n \
  \       $ref: '#/components/schemas/ListWebhookPayload'\n    ListUpdated:\n      name: listUpdated\n      title: List Updated\n      summary: A list was updated\n      description: >-\n        Triggered when a list's properties are modified.\n      payload:\n        $ref: '#/components/schemas/ListWebhookPayload'\n    ListDeleted:\n      name: listDeleted\n      title: List Deleted\n      summary: A list was deleted\n      description: >-\n        Triggered when a list is permanently deleted.\n      payload:\n        $ref: '#/components/schemas/ListWebhookPayload'\n    FolderCreated:\n      name: folderCreated\n      title: Folder Created\n      summary: A new folder was created\n      description: >-\n        Triggered when a new folder is created within the subscribed scope.\n      payload:\n        $ref: '#/components/schemas/FolderWebhookPayload'\n    FolderUpdated:\n      name: folderUpdated\n      title: Folder Updated\n      summary: A folder was updated\n      description: >-\n\
  \        Triggered when a folder's properties are modified.\n      payload:\n        $ref: '#/components/schemas/FolderWebhookPayload'\n    FolderDeleted:\n      name: folderDeleted\n      title: Folder Deleted\n      summary: A folder was deleted\n      description: >-\n        Triggered when a folder is permanently deleted.\n      payload:\n        $ref: '#/components/schemas/FolderWebhookPayload'\n    SpaceCreated:\n      name: spaceCreated\n      title: Space Created\n      summary: A new space was created\n      description: >-\n        Triggered when a new space is created within the Workspace.\n      payload:\n        $ref: '#/components/schemas/SpaceWebhookPayload'\n    SpaceUpdated:\n      name: spaceUpdated\n      title: Space Updated\n      summary: A space was updated\n      description: >-\n        Triggered when a space's properties are modified.\n      payload:\n        $ref: '#/components/schemas/SpaceWebhookPayload'\n    SpaceDeleted:\n      name: spaceDeleted\n      title:\
  \ Space Deleted\n      summary: A space was deleted\n      description: >-\n        Triggered when a space is permanently deleted.\n      payload:\n        $ref: '#/components/schemas/SpaceWebhookPayload'\n    GoalCreated:\n      name: goalCreated\n      title: Goal Created\n      summary: A new goal was created\n      description: >-\n        Triggered when a new goal is created within the Workspace.\n      payload:\n        $ref: '#/components/schemas/GoalWebhookPayload'\n    GoalUpdated:\n      name: goalUpdated\n      title: Goal Updated\n      summary: A goal was updated\n      description: >-\n        Triggered when a goal's properties are modified.\n      payload:\n        $ref: '#/components/schemas/GoalWebhookPayload'\n    GoalDeleted:\n      name: goalDeleted\n      title: Goal Deleted\n      summary: A goal was deleted\n      description: >-\n        Triggered when a goal is permanently deleted.\n      payload:\n        $ref: '#/components/schemas/GoalWebhookPayload'\n    KeyResultCreated:\n\
  \      name: keyResultCreated\n      title: Key Result Created\n      summary: A new key result was created\n      description: >-\n        Triggered when a new key result is added to a goal.\n      payload:\n        $ref: '#/components/schemas/GoalWebhookPayload'\n    KeyResultUpdated:\n      name: keyResultUpdated\n      title: Key Result Updated\n      summary: A key result was updated\n      description: >-\n        Triggered when a key result's progress or properties are modified.\n      payload:\n        $ref: '#/components/schemas/GoalWebhookPayload'\n    KeyResultDeleted:\n      name: keyResultDeleted\n      title: Key Result Deleted\n      summary: A key result was deleted\n      description: >-\n        Triggered when a key result is permanently deleted from a goal.\n      payload:\n        $ref: '#/components/schemas/GoalWebhookPayload'\n  schemas:\n    TaskWebhookPayload:\n      type: object\n      description: >-\n        Payload delivered for task-related webhook events.\n\
  \      properties:\n        event:\n          type: string\n          description: >-\n            The event name (e.g., taskCreated, taskUpdated, taskDeleted).\n        webhook_id:\n          type: string\n          description: >-\n            The ID of the webhook subscription that triggered this event.\n        task_id:\n          type: string\n          description: >-\n            The ID of the task that was affected.\n        history_items:\n          type: array\n          items:\n            $ref: '#/components/schemas/HistoryItem'\n          description: >-\n            Array of change records describing what was modified. Each item\n            contains the field name, the before and after values, the user\n            who made the change, and the timestamp.\n    ListWebhookPayload:\n      type: object\n      description: >-\n        Payload delivered for list-related webhook events.\n      properties:\n        event:\n          type: string\n          description: >-\n    \
  \        The event name (e.g., listCreated, listUpdated, listDeleted).\n        webhook_id:\n          type: string\n          description: >-\n            The ID of the webhook subscription that triggered this event.\n        list_id:\n          type: string\n          description: >-\n            The ID of the list that was affected.\n        history_items:\n          type: array\n          items:\n            $ref: '#/components/schemas/HistoryItem'\n          description: >-\n            Array of change records.\n    FolderWebhookPayload:\n      type: object\n      description: >-\n        Payload delivered for folder-related webhook events.\n      properties:\n        event:\n          type: string\n          description: >-\n            The event name (e.g., folderCreated, folderUpdated, folderDeleted).\n        webhook_id:\n          type: string\n          description: >-\n            The ID of the webhook subscription that triggered this event.\n        folder_id:\n          type:\
  \ string\n          description: >-\n            The ID of the folder that was affected.\n        history_items:\n          type: array\n          items:\n            $ref: '#/components/schemas/HistoryItem'\n          description: >-\n            Array of change records.\n    SpaceWebhookPayload:\n      type: object\n      description: >-\n        Payload delivered for space-related webhook events.\n      properties:\n        event:\n          type: string\n          description: >-\n            The event name (e.g., spaceCreated, spaceUpdated, spaceDeleted).\n        webhook_id:\n          type: string\n          description: >-\n            The ID of the webhook subscription that triggered this event.\n        space_id:\n          type: string\n          description: >-\n            The ID of the space that was affected.\n        history_items:\n          type: array\n          items:\n            $ref: '#/components/schemas/HistoryItem'\n          description: >-\n            Array\
  \ of change records.\n    GoalWebhookPayload:\n      type: object\n      description: >-\n        Payload delivered for goal and key result-related webhook events.\n      properties:\n        event:\n          type: string\n          description: >-\n            The event name (e.g., goalCreated, goalUpdated, keyResultUpdated).\n        webhook_id:\n          type: string\n          description: >-\n            The ID of the webhook subscription that triggered this event.\n        goal_id:\n          type: string\n          description: >-\n            The ID of the goal that was affected.\n        history_items:\n          type: array\n          items:\n            $ref: '#/components/schemas/HistoryItem'\n          description: >-\n            Array of change records.\n    HistoryItem:\n      type: object\n      description: >-\n        A record of a single change within a webhook event. Describes what\n        field was changed, by whom, and the before and after values.\n      properties:\n\
  \        id:\n          type: string\n          description: >-\n            The unique identifier of the history item.\n        type:\n          type: integer\n          description: >-\n            The type code of the history item.\n        date:\n          type: string\n          description: >-\n            Unix timestamp in milliseconds when the change occurred.\n        field:\n          type: string\n          description: >-\n            The name of the field that was changed (e.g., status, priority,\n            assignee, due_date, tag, comment, name, description).\n        parent_id:\n          type: string\n          description: >-\n            The parent resource ID.\n        data:\n          type: object\n          description: >-\n            Additional data about the change.\n        source:\n          type: string\n          nullable: true\n          description: >-\n            The source of the change (e.g., null for UI, api for API).\n        user:\n          type:\
  \ object\n          properties:\n            id:\n              type: integer\n              description: >-\n                The user ID who made the change.\n            username:\n              type: string\n              description: >-\n                The username.\n            email:\n              type: string\n              format: email\n              description: >-\n                The email address.\n            color:\n              type: string\n              description: >-\n                The user color.\n            profilePicture:\n              type: string\n              format: uri\n              nullable: true\n              description: >-\n                URL of the profile picture.\n            initials:\n              type: string\n              description: >-\n                The user initials.\n          description: >-\n            The user who made the change.\n        before:\n          description: >-\n            The value before the change. Type varies\
  \ based on the field.\n        after:\n          description: >-\n            The value after the change. Type varies based on the field.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/clickup/refs/heads/main/asyncapi/clickup-webhooks-asyncapi.yml
spec_file: asyncapi/clickup-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/clickup/refs/heads/main/asyncapi/clickup-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '2.0'
---
