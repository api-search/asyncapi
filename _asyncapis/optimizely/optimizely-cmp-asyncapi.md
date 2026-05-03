---
api_specs:
- filename: optimizely-web-experimentation-openapi.yml
  format: yaml
  label: Optimizely Web Experimentation REST API
  slug: web-experimentation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-web-experimentation-openapi.yml
- filename: optimizely-feature-experimentation-openapi.yml
  format: yaml
  label: Optimizely Feature Experimentation REST API
  slug: feature-experimentation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-feature-experimentation-openapi.yml
- filename: optimizely-campaign-openapi.yml
  format: yaml
  label: Optimizely Campaign REST API
  slug: campaign
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-campaign-openapi.yml
- filename: optimizely-content-delivery-openapi.yml
  format: yaml
  label: Optimizely Content Delivery API
  slug: content-delivery
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-content-delivery-openapi.yml
- filename: optimizely-content-management-openapi.yml
  format: yaml
  label: Optimizely Content Management API
  slug: content-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-content-management-openapi.yml
- filename: optimizely-graph-openapi.yml
  format: yaml
  label: Optimizely Graph API
  slug: graph
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-graph-openapi.yml
- filename: optimizely-data-platform-openapi.yml
  format: yaml
  label: Optimizely Data Platform REST API
  slug: data-platform
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-data-platform-openapi.yml
- filename: optimizely-cmp-openapi.yml
  format: yaml
  label: Optimizely CMP Open REST API
  slug: cmp
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-cmp-openapi.yml
- filename: optimizely-commerce-service-openapi.yml
  format: yaml
  label: Optimizely Commerce Service API
  slug: commerce-service
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-commerce-service-openapi.yml
channels:
- description: Receives webhook notifications related to task lifecycle events in the CMP, including asset additions, step completions, and assignee changes.
  name: /webhook/task-events
  operation: publish
  operation_id: receiveTaskEvent
  summary: Receive a task event notification
- description: Receives webhook notifications related to content events in the CMP, including content publication and updates.
  name: /webhook/content-events
  operation: publish
  operation_id: receiveContentEvent
  summary: Receive a content event notification
description: The Optimizely Content Marketing Platform (CMP) provides webhook notifications when content events occur, such as when assets are published, tasks are completed or modified, and content items are updated. Webhooks send HTTP POST payloads with JSON bodies to configured callback URLs. An optional secret can be provided during webhook registration for signature verification via the Callback-Secret header.
layout: asyncapi
messages:
- description: Sent when a digital asset (image, video, article, or raw file) is added to a content task in the CMP workflow.
  name: TaskAssetAdded
  summary: An asset was added to a task
  title: Task Asset Added
- description: Sent when a substep in the content workflow is marked as complete.
  name: TaskStepCompleted
  summary: A workflow step was completed
  title: Task Step Completed
- description: Sent when a substep in the content workflow is started.
  name: TaskStepStarted
  summary: A workflow step was started
  title: Task Step Started
- description: Sent when the assignee or due date of a task step is modified.
  name: TaskAssigneeChanged
  summary: A task assignee was changed
  title: Task Assignee Changed
- description: Sent when an asset is approved and published to the CMP digital asset library, making it available for use in campaigns and content.
  name: AssetAdded
  summary: An asset was published to the CMP library
  title: Asset Added to Library
- description: Sent when a content item is published from the CMP content repository, making it available for distribution.
  name: ContentPublished
  summary: Content was published
  title: Content Published
name: Optimizely CMP Webhooks
provider_name: Optimizely
provider_slug: optimizely
servers:
- description: The HTTPS endpoint on your server that receives webhook POST requests from Optimizely CMP.
  name: webhookReceiver
  protocol: https
  url: '{callbackUrl}'
slug: optimizely-cmp-asyncapi
source_filename: optimizely-cmp-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Optimizely CMP Webhooks\n  description: >-\n    The Optimizely Content Marketing Platform (CMP) provides webhook\n    notifications when content events occur, such as when assets are\n    published, tasks are completed or modified, and content items are\n    updated. Webhooks send HTTP POST payloads with JSON bodies to\n    configured callback URLs. An optional secret can be provided during\n    webhook registration for signature verification via the\n    Callback-Secret header.\n  version: '1.0'\n  contact:\n    name: Optimizely Support\n    url: https://support.optimizely.com\nservers:\n  webhookReceiver:\n    url: '{callbackUrl}'\n    protocol: https\n    description: >-\n      The HTTPS endpoint on your server that receives webhook\n      POST requests from Optimizely CMP.\n    variables:\n      callbackUrl:\n        description: The callback URL registered for receiving webhooks\nchannels:\n  /webhook/task-events:\n    description: >-\n\
  \      Receives webhook notifications related to task lifecycle events\n      in the CMP, including asset additions, step completions, and\n      assignee changes.\n    publish:\n      operationId: receiveTaskEvent\n      summary: Receive a task event notification\n      description: >-\n        Optimizely CMP sends an HTTP POST request when task-related\n        events occur, such as when an asset is added to a task, a\n        workflow step is completed, started, or skipped, or when a\n        task assignee or due date is changed.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/TaskAssetAdded'\n          - $ref: '#/components/messages/TaskStepCompleted'\n          - $ref: '#/components/messages/TaskStepStarted'\n          - $ref: '#/components/messages/TaskAssigneeChanged'\n  /webhook/content-events:\n    description: >-\n      Receives webhook notifications related to content events\n      in the CMP, including content publication and updates.\n    publish:\n\
  \      operationId: receiveContentEvent\n      summary: Receive a content event notification\n      description: >-\n        Optimizely CMP sends an HTTP POST request when content-related\n        events occur in the content repository.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/AssetAdded'\n          - $ref: '#/components/messages/ContentPublished'\ncomponents:\n  securitySchemes:\n    callbackSecret:\n      type: httpApiKey\n      in: header\n      name: Callback-Secret\n      description: >-\n        Optional secret provided during webhook registration, sent with\n        each webhook request for verification.\n  messages:\n    TaskAssetAdded:\n      name: TaskAssetAdded\n      title: Task Asset Added\n      summary: An asset was added to a task\n      description: >-\n        Sent when a digital asset (image, video, article, or raw file)\n        is added to a content task in the CMP workflow.\n      contentType: application/json\n      payload:\n   \
  \     $ref: '#/components/schemas/TaskAssetEvent'\n    TaskStepCompleted:\n      name: TaskStepCompleted\n      title: Task Step Completed\n      summary: A workflow step was completed\n      description: >-\n        Sent when a substep in the content workflow is marked as complete.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TaskStepEvent'\n    TaskStepStarted:\n      name: TaskStepStarted\n      title: Task Step Started\n      summary: A workflow step was started\n      description: >-\n        Sent when a substep in the content workflow is started.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TaskStepEvent'\n    TaskAssigneeChanged:\n      name: TaskAssigneeChanged\n      title: Task Assignee Changed\n      summary: A task assignee was changed\n      description: >-\n        Sent when the assignee or due date of a task step is modified.\n      contentType: application/json\n      payload:\n  \
  \      $ref: '#/components/schemas/TaskAssigneeEvent'\n    AssetAdded:\n      name: AssetAdded\n      title: Asset Added to Library\n      summary: An asset was published to the CMP library\n      description: >-\n        Sent when an asset is approved and published to the CMP digital\n        asset library, making it available for use in campaigns and content.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AssetEvent'\n    ContentPublished:\n      name: ContentPublished\n      title: Content Published\n      summary: Content was published\n      description: >-\n        Sent when a content item is published from the CMP content\n        repository, making it available for distribution.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ContentEvent'\n  schemas:\n    TaskAssetEvent:\n      type: object\n      description: Event payload for task asset events\n      properties:\n        event_name:\n      \
  \    type: string\n          description: Name of the event\n          enum:\n            - task_asset_added\n        task_id:\n          type: string\n          description: Identifier of the task\n        asset:\n          type: object\n          description: The asset that was added\n          properties:\n            id:\n              type: string\n              description: Asset identifier\n            type:\n              type: string\n              description: Type of asset\n              enum:\n                - image\n                - video\n                - article\n                - raw_file\n            links:\n              type: object\n              description: Links related to the asset\n              properties:\n                self:\n                  type: string\n                  format: uri\n                  description: URL to the asset\n        timestamp:\n          type: string\n          format: date-time\n          description: When the event occurred\n\
  \    TaskStepEvent:\n      type: object\n      description: Event payload for task workflow step events\n      properties:\n        event_name:\n          type: string\n          description: Name of the event\n          enum:\n            - task_step_completed\n            - task_step_started\n            - task_step_skipped\n        task_id:\n          type: string\n          description: Identifier of the task\n        step:\n          type: object\n          description: The workflow step\n          properties:\n            id:\n              type: string\n              description: Step identifier\n            name:\n              type: string\n              description: Step name\n            status:\n              type: string\n              description: Step status\n              enum:\n                - started\n                - completed\n                - skipped\n        timestamp:\n          type: string\n          format: date-time\n          description: When the event\
  \ occurred\n    TaskAssigneeEvent:\n      type: object\n      description: Event payload for task assignee changes\n      properties:\n        event_name:\n          type: string\n          description: Name of the event\n          enum:\n            - task_assignee_changed\n            - task_due_date_changed\n        task_id:\n          type: string\n          description: Identifier of the task\n        assignee:\n          type: object\n          description: The new assignee\n          properties:\n            id:\n              type: string\n              description: User identifier\n            name:\n              type: string\n              description: User display name\n        due_date:\n          type: string\n          format: date\n          description: Updated due date\n        timestamp:\n          type: string\n          format: date-time\n          description: When the event occurred\n    AssetEvent:\n      type: object\n      description: Event payload for asset\
  \ library events\n      properties:\n        event_name:\n          type: string\n          description: Name of the event\n          enum:\n            - asset_added\n        asset:\n          type: object\n          description: The asset that was published\n          properties:\n            id:\n              type: string\n              description: Asset identifier\n            title:\n              type: string\n              description: Asset title\n            type:\n              type: string\n              description: Asset type\n            url:\n              type: string\n              format: uri\n              description: URL to access the asset\n        timestamp:\n          type: string\n          format: date-time\n          description: When the event occurred\n    ContentEvent:\n      type: object\n      description: Event payload for content publication events\n      properties:\n        event_name:\n          type: string\n          description: Name of the event\n\
  \          enum:\n            - content_published\n        content:\n          type: object\n          description: The published content\n          properties:\n            id:\n              type: string\n              description: Content identifier\n            title:\n              type: string\n              description: Content title\n            content_type:\n              type: string\n              description: Content type\n        timestamp:\n          type: string\n          format: date-time\n          description: When the event occurred\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/asyncapi/optimizely-cmp-asyncapi.yml
spec_file: asyncapi/optimizely-cmp-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/asyncapi/optimizely-cmp-asyncapi.yml
tags:
- A/B Testing
- Content Management
- Customer Data
- E-Commerce
- Experimentation
- Feature Flags
- Marketing
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
