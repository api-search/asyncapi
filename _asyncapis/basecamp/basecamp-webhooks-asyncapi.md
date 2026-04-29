---
api_specs:
- filename: basecamp-api-openapi.yml
  format: yaml
  label: Basecamp API
  slug: basecamp-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/basecamp/refs/heads/main/openapi/basecamp-api-openapi.yml
- filename: basecamp-webhooks-asyncapi.yml
  format: yaml
  label: Basecamp Webhooks
  slug: basecamp-webhooks
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/basecamp/refs/heads/main/asyncapi/basecamp-webhooks-asyncapi.yml
- filename: basecamp-oauth-openapi.yml
  format: yaml
  label: Basecamp OAuth
  slug: basecamp-oauth
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/basecamp/refs/heads/main/openapi/basecamp-oauth-openapi.yml
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
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Basecamp Webhook Events\n  description: >-\n    The Basecamp webhook system delivers real-time HTTP notifications to\n    registered HTTPS endpoints when events occur within a Basecamp project.\n    Webhooks are configured per project with a payload URL and an optional list\n    of resource types. Basecamp sends an HTTP POST with a JSON payload to the\n    registered URL whenever a subscribed event occurs. Delivery is attempted up\n    to 10 times with exponential backoff before a webhook is deactivated if the\n    endpoint fails to return a 2xx HTTP response.\n  version: '1.0'\n  contact:\n    name: Basecamp Developer Support\n    url: https://github.com/basecamp/bc3-api/blob/master/sections/webhooks.md\n  termsOfService: https://basecamp.com/terms\nexternalDocs:\n  description: Basecamp Webhooks Documentation\n  url: https://github.com/basecamp/bc3-api/blob/master/sections/webhooks.md\nservers:\n  basecamp:\n    url: 'https://3.basecampapi.com'\n\
  \    protocol: https\n    description: >-\n      Basecamp sends webhook event notifications as HTTP POST requests\n      originating from Basecamp infrastructure. Receiving endpoints must be\n      publicly accessible HTTPS URLs registered via the Webhooks REST API.\n    security:\n      - bearerAuth: []\nchannels:\n  /webhook:\n    description: >-\n      The HTTPS endpoint on the subscriber's server that receives webhook\n      notifications from Basecamp. Basecamp sends HTTP POST requests with JSON\n      payloads. Subscribers should respond with a 2xx status code within a\n      reasonable timeout to acknowledge receipt. Failure to respond with 2xx\n      after 10 attempts will cause Basecamp to deactivate the webhook.\n    publish:\n      operationId: receiveBasecampWebhook\n      summary: Receive a Basecamp webhook event notification\n      description: >-\n        Basecamp sends this message to the subscriber's registered payload URL\n        whenever a subscribed resource event\
  \ occurs within a project. The\n        payload includes the event kind, the recording object, the creator,\n        and any event-specific details.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/MessageCreated'\n          - $ref: '#/components/messages/MessageUpdated'\n          - $ref: '#/components/messages/MessageArchived'\n          - $ref: '#/components/messages/MessageTrashed'\n          - $ref: '#/components/messages/TodoCreated'\n          - $ref: '#/components/messages/TodoUpdated'\n          - $ref: '#/components/messages/TodoCompleted'\n          - $ref: '#/components/messages/TodoUncompleted'\n          - $ref: '#/components/messages/TodoArchived'\n          - $ref: '#/components/messages/TodoTrashed'\n          - $ref: '#/components/messages/TodolistCreated'\n          - $ref: '#/components/messages/TodolistUpdated'\n          - $ref: '#/components/messages/TodolistArchived'\n          - $ref: '#/components/messages/TodolistTrashed'\n          -\
  \ $ref: '#/components/messages/DocumentCreated'\n          - $ref: '#/components/messages/DocumentUpdated'\n          - $ref: '#/components/messages/DocumentArchived'\n          - $ref: '#/components/messages/DocumentTrashed'\n          - $ref: '#/components/messages/CommentCreated'\n          - $ref: '#/components/messages/CommentUpdated'\n          - $ref: '#/components/messages/CommentTrashed'\n          - $ref: '#/components/messages/CardCreated'\n          - $ref: '#/components/messages/CardUpdated'\n          - $ref: '#/components/messages/CardArchived'\n          - $ref: '#/components/messages/CardTrashed'\n          - $ref: '#/components/messages/ScheduleEntryCreated'\n          - $ref: '#/components/messages/ScheduleEntryUpdated'\n          - $ref: '#/components/messages/ScheduleEntryArchived'\n          - $ref: '#/components/messages/ScheduleEntryTrashed'\n          - $ref: '#/components/messages/UploadCreated'\n          - $ref: '#/components/messages/UploadUpdated'\n      \
  \    - $ref: '#/components/messages/UploadArchived'\n          - $ref: '#/components/messages/UploadTrashed'\n          - $ref: '#/components/messages/QuestionAnswerCreated'\n          - $ref: '#/components/messages/QuestionAnswerUpdated'\n          - $ref: '#/components/messages/QuestionPaused'\n          - $ref: '#/components/messages/QuestionResumed'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: http\n      scheme: bearer\n      description: >-\n        Bearer token used to authenticate REST API calls to configure webhooks.\n        Not used in the webhook delivery itself — delivery authentication relies\n        on verifying the source IP or using shared secrets in the payload URL.\n  messages:\n    MessageCreated:\n      name: message_created\n      title: Message Created\n      summary: A new message was created on a message board\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n      examples:\n        - name: MessageCreatedExample\n       \
  \   payload:\n            id: 9007199254741234\n            kind: message_created\n            created_at: '2024-01-15T10:00:00.000Z'\n            recording:\n              id: 1234567\n              type: Message\n              status: active\n              title: Project Kickoff\n            creator:\n              id: 99\n              name: Alice Smith\n            details: {}\n    MessageUpdated:\n      name: message_updated\n      title: Message Updated\n      summary: An existing message was updated\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    MessageArchived:\n      name: message_archived\n      title: Message Archived\n      summary: A message was archived\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    MessageTrashed:\n      name: message_trashed\n      title: Message Trashed\n      summary: A message was moved to trash\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    TodoCreated:\n      name: todo_created\n\
  \      title: To-Do Created\n      summary: A new to-do was created\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    TodoUpdated:\n      name: todo_updated\n      title: To-Do Updated\n      summary: An existing to-do was updated\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    TodoCompleted:\n      name: todo_completed\n      title: To-Do Completed\n      summary: A to-do was marked as completed\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    TodoUncompleted:\n      name: todo_uncompleted\n      title: To-Do Uncompleted\n      summary: A to-do was marked as incomplete\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    TodoArchived:\n      name: todo_archived\n      title: To-Do Archived\n      summary: A to-do was archived\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    TodoTrashed:\n      name: todo_trashed\n      title: To-Do Trashed\n      summary: A to-do was\
  \ moved to trash\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    TodolistCreated:\n      name: todolist_created\n      title: To-Do List Created\n      summary: A new to-do list was created\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    TodolistUpdated:\n      name: todolist_updated\n      title: To-Do List Updated\n      summary: An existing to-do list was updated\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    TodolistArchived:\n      name: todolist_archived\n      title: To-Do List Archived\n      summary: A to-do list was archived\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    TodolistTrashed:\n      name: todolist_trashed\n      title: To-Do List Trashed\n      summary: A to-do list was moved to trash\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    DocumentCreated:\n      name: document_created\n      title: Document Created\n      summary: A new document\
  \ was created in a vault\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    DocumentUpdated:\n      name: document_updated\n      title: Document Updated\n      summary: An existing document was updated\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    DocumentArchived:\n      name: document_archived\n      title: Document Archived\n      summary: A document was archived\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    DocumentTrashed:\n      name: document_trashed\n      title: Document Trashed\n      summary: A document was moved to trash\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    CommentCreated:\n      name: comment_created\n      title: Comment Created\n      summary: A new comment was posted on a recording\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    CommentUpdated:\n      name: comment_updated\n      title: Comment Updated\n      summary: An existing\
  \ comment was updated\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    CommentTrashed:\n      name: comment_trashed\n      title: Comment Trashed\n      summary: A comment was moved to trash\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    CardCreated:\n      name: card_created\n      title: Card Created\n      summary: A new card was created on a card table\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    CardUpdated:\n      name: card_updated\n      title: Card Updated\n      summary: An existing card was updated or moved\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    CardArchived:\n      name: card_archived\n      title: Card Archived\n      summary: A card was archived\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    CardTrashed:\n      name: card_trashed\n      title: Card Trashed\n      summary: A card was moved to trash\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n\
  \    ScheduleEntryCreated:\n      name: schedule_entry_created\n      title: Schedule Entry Created\n      summary: A new schedule entry was created\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    ScheduleEntryUpdated:\n      name: schedule_entry_updated\n      title: Schedule Entry Updated\n      summary: An existing schedule entry was updated\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    ScheduleEntryArchived:\n      name: schedule_entry_archived\n      title: Schedule Entry Archived\n      summary: A schedule entry was archived\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    ScheduleEntryTrashed:\n      name: schedule_entry_trashed\n      title: Schedule Entry Trashed\n      summary: A schedule entry was moved to trash\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    UploadCreated:\n      name: upload_created\n      title: Upload Created\n      summary: A new file upload was created\
  \ in a vault\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    UploadUpdated:\n      name: upload_updated\n      title: Upload Updated\n      summary: An existing upload was updated\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    UploadArchived:\n      name: upload_archived\n      title: Upload Archived\n      summary: An upload was archived\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    UploadTrashed:\n      name: upload_trashed\n      title: Upload Trashed\n      summary: An upload was moved to trash\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    QuestionAnswerCreated:\n      name: question_answer_created\n      title: Question Answer Created\n      summary: A new answer was submitted to an automatic check-in question\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    QuestionAnswerUpdated:\n      name: question_answer_updated\n      title: Question Answer Updated\n\
  \      summary: An answer to an automatic check-in question was updated\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    QuestionPaused:\n      name: question_paused\n      title: Question Paused\n      summary: An automatic check-in question was paused\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    QuestionResumed:\n      name: question_resumed\n      title: Question Resumed\n      summary: A paused automatic check-in question was resumed\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n  schemas:\n    WebhookPayload:\n      type: object\n      required: [id, kind, created_at, recording, creator]\n      description: >-\n        Standard JSON payload delivered by Basecamp to the registered webhook\n        endpoint for all event types. The recording field contains the full\n        representation of the resource that triggered the event.\n      properties:\n        id:\n          type: integer\n          description:\
  \ Unique identifier for this webhook event\n        kind:\n          type: string\n          description: >-\n            Event type descriptor in the format {resource}_{action}, such as\n            message_created, todo_completed, or document_updated.\n          examples:\n            - message_created\n            - todo_completed\n            - comment_created\n            - card_updated\n        created_at:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp when the event occurred\n        recording:\n          $ref: '#/components/schemas/RecordingPayload'\n        creator:\n          $ref: '#/components/schemas/PersonPayload'\n        details:\n          type: object\n          description: >-\n            Event-specific metadata. For copy and move events this includes a\n            copy object referencing the duplicated item. Contents vary by event\n            kind.\n          additionalProperties: true\n    RecordingPayload:\n    \
  \  type: object\n      description: >-\n        Full representation of the Basecamp resource that triggered the webhook\n        event. The exact fields present depend on the resource type.\n      properties:\n        id:\n          type: integer\n          description: Recording ID\n        status:\n          type: string\n          description: Recording status at the time of the event\n          enum: [active, archived, trashed]\n        visible_to_clients:\n          type: boolean\n          description: Whether the recording is visible to client users\n        created_at:\n          type: string\n          format: date-time\n          description: Timestamp when the recording was created\n        updated_at:\n          type: string\n          format: date-time\n          description: Timestamp when the recording was last updated\n        title:\n          type: string\n          description: Title or summary of the recording\n        inherits_status:\n          type: boolean\n   \
  \       description: Whether the recording inherits status from a parent\n        type:\n          type: string\n          description: Recording type (Message, Todo, Document, Comment, etc.)\n        url:\n          type: string\n          format: uri\n          description: API URL for this recording\n        app_url:\n          type: string\n          format: uri\n          description: Web URL for this recording\n        bucket:\n          $ref: '#/components/schemas/BucketPayload'\n        creator:\n          $ref: '#/components/schemas/PersonPayload'\n        content:\n          type: string\n          description: HTML-formatted body content (for messages, documents, comments)\n        completed:\n          type: boolean\n          description: Whether the to-do is completed (for Todo type)\n        due_on:\n          type: string\n          format: date\n          description: Due date for to-dos and schedule entries\n          nullable: true\n        starts_at:\n          type:\
  \ string\n          format: date-time\n          description: Start time for schedule entries\n        ends_at:\n          type: string\n          format: date-time\n          description: End time for schedule entries\n        assignees:\n          type: array\n          description: Assigned people (for Todos)\n          items:\n            $ref: '#/components/schemas/PersonPayload'\n    BucketPayload:\n      type: object\n      description: Reference to the Basecamp project containing the recording\n      properties:\n        id:\n          type: integer\n          description: Project ID\n        name:\n          type: string\n          description: Project name\n        type:\n          type: string\n          description: Always \"Project\"\n    PersonPayload:\n      type: object\n      description: Reference to the Basecamp user who created or triggered the event\n      properties:\n        id:\n          type: integer\n          description: Person ID\n        attachable_sgid:\n\
  \          type: string\n          description: Signed global ID\n        name:\n          type: string\n          description: Full name\n        email_address:\n          type: string\n          format: email\n          description: Email address\n        personable_type:\n          type: string\n          description: Type of personable (User, Client)\n        title:\n          type: string\n          description: Job title\n        avatar_url:\n          type: string\n          format: uri\n          description: URL to avatar image\n        created_at:\n          type: string\n          format: date-time\n          description: Account creation timestamp\n        updated_at:\n          type: string\n          format: date-time\n          description: Last update timestamp\n        admin:\n          type: boolean\n          description: Whether the person is an account administrator\n        time_zone:\n          type: string\n          description: IANA time zone name\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/basecamp/refs/heads/main/asyncapi/basecamp-webhooks-asyncapi.yml
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
