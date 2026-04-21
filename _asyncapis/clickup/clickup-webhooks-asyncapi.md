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
spec_file: asyncapi/clickup-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/clickup/refs/heads/main/asyncapi/clickup-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '2.0'
---
