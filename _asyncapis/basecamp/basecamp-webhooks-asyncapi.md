---
channels:
- description: The HTTPS endpoint on the subscriber's server that receives webhook notifications from Basecamp. Basecamp sends HTTP POST requests with JSON payloads. Subscribers should respond with a 2xx status code within a reasonable timeout to acknowledge receipt. Failure to respond with 2xx after 10 attempts will cause Basecamp to deactivate the webhook.
  name: /webhook
  operation: publish
  operation_id: receiveBasecampWebhook
  summary: Receive a Basecamp webhook event notification
description: The Basecamp webhook system delivers real-time HTTP notifications to registered HTTPS endpoints when events occur within a Basecamp project. Webhooks are configured per project with a payload URL and an optional list of resource types. Basecamp sends an HTTP POST with a JSON payload to the registered URL whenever a subscribed event occurs. Delivery is attempted up to 10 times with exponential backoff before a webhook is deactivated if the endpoint fails to return a 2xx HTTP response.
layout: asyncapi
messages:
- description: ''
  name: MessageCreated
  summary: A new message was created on a message board
  title: Message Created
- description: ''
  name: MessageUpdated
  summary: An existing message was updated
  title: Message Updated
- description: ''
  name: MessageArchived
  summary: A message was archived
  title: Message Archived
- description: ''
  name: MessageTrashed
  summary: A message was moved to trash
  title: Message Trashed
- description: ''
  name: TodoCreated
  summary: A new to-do was created
  title: To-Do Created
- description: ''
  name: TodoUpdated
  summary: An existing to-do was updated
  title: To-Do Updated
- description: ''
  name: TodoCompleted
  summary: A to-do was marked as completed
  title: To-Do Completed
- description: ''
  name: TodoUncompleted
  summary: A to-do was marked as incomplete
  title: To-Do Uncompleted
- description: ''
  name: TodoArchived
  summary: A to-do was archived
  title: To-Do Archived
- description: ''
  name: TodoTrashed
  summary: A to-do was moved to trash
  title: To-Do Trashed
- description: ''
  name: TodolistCreated
  summary: A new to-do list was created
  title: To-Do List Created
- description: ''
  name: TodolistUpdated
  summary: An existing to-do list was updated
  title: To-Do List Updated
- description: ''
  name: TodolistArchived
  summary: A to-do list was archived
  title: To-Do List Archived
- description: ''
  name: TodolistTrashed
  summary: A to-do list was moved to trash
  title: To-Do List Trashed
- description: ''
  name: DocumentCreated
  summary: A new document was created in a vault
  title: Document Created
- description: ''
  name: DocumentUpdated
  summary: An existing document was updated
  title: Document Updated
- description: ''
  name: DocumentArchived
  summary: A document was archived
  title: Document Archived
- description: ''
  name: DocumentTrashed
  summary: A document was moved to trash
  title: Document Trashed
- description: ''
  name: CommentCreated
  summary: A new comment was posted on a recording
  title: Comment Created
- description: ''
  name: CommentUpdated
  summary: An existing comment was updated
  title: Comment Updated
- description: ''
  name: CommentTrashed
  summary: A comment was moved to trash
  title: Comment Trashed
- description: ''
  name: CardCreated
  summary: A new card was created on a card table
  title: Card Created
- description: ''
  name: CardUpdated
  summary: An existing card was updated or moved
  title: Card Updated
- description: ''
  name: CardArchived
  summary: A card was archived
  title: Card Archived
- description: ''
  name: CardTrashed
  summary: A card was moved to trash
  title: Card Trashed
- description: ''
  name: ScheduleEntryCreated
  summary: A new schedule entry was created
  title: Schedule Entry Created
- description: ''
  name: ScheduleEntryUpdated
  summary: An existing schedule entry was updated
  title: Schedule Entry Updated
- description: ''
  name: ScheduleEntryArchived
  summary: A schedule entry was archived
  title: Schedule Entry Archived
- description: ''
  name: ScheduleEntryTrashed
  summary: A schedule entry was moved to trash
  title: Schedule Entry Trashed
- description: ''
  name: UploadCreated
  summary: A new file upload was created in a vault
  title: Upload Created
- description: ''
  name: UploadUpdated
  summary: An existing upload was updated
  title: Upload Updated
- description: ''
  name: UploadArchived
  summary: An upload was archived
  title: Upload Archived
- description: ''
  name: UploadTrashed
  summary: An upload was moved to trash
  title: Upload Trashed
- description: ''
  name: QuestionAnswerCreated
  summary: A new answer was submitted to an automatic check-in question
  title: Question Answer Created
- description: ''
  name: QuestionAnswerUpdated
  summary: An answer to an automatic check-in question was updated
  title: Question Answer Updated
- description: ''
  name: QuestionPaused
  summary: An automatic check-in question was paused
  title: Question Paused
- description: ''
  name: QuestionResumed
  summary: A paused automatic check-in question was resumed
  title: Question Resumed
name: Basecamp Webhook Events
provider_name: Basecamp
provider_slug: basecamp
servers:
- description: Basecamp sends webhook event notifications as HTTP POST requests originating from Basecamp infrastructure. Receiving endpoints must be publicly accessible HTTPS URLs registered via the Webhooks REST API.
  name: basecamp
  protocol: https
  url: https://3.basecampapi.com
slug: basecamp-webhooks-asyncapi
spec_file: asyncapi/basecamp-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/basecamp/refs/heads/main/asyncapi/basecamp-webhooks-asyncapi.yml
tags:
- Collaboration
- Project Management
- REST
- SaaS
- Team Communication
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
