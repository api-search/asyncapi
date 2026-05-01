---
api_specs:
- filename: elastic-io-platform-api-openapi.yml
  format: yaml
  label: Elastic.io
  slug: elastic-io
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/elastic-io/refs/heads/main/openapi/elastic-io-platform-api-openapi.yml
channels:
- description: Inbound webhook channel that triggers a specific integration flow when an external system sends an HTTP request.
  name: webhook/flow/{flowId}
  operation: publish
  operation_id: receiveWebhookTrigger
  summary: Receive a webhook trigger
- description: Pub/sub topic channel for inter-flow messaging. Flows can publish messages to a topic, and other flows subscribed to the same topic will receive and process them.
  name: topic/{topicName}
  operation: publish
  operation_id: publishToTopic
  summary: Publish a message to a topic
- description: Channel for flow execution lifecycle events including start, completion, and failure notifications.
  name: flow/{flowId}/execution
  operation: subscribe
  operation_id: receiveExecutionEvent
  summary: Receive flow execution events
- description: Channel for flow error events emitted when a step within an integration flow encounters a processing error.
  name: flow/{flowId}/error
  operation: subscribe
  operation_id: receiveFlowError
  summary: Receive flow error events
- description: Channel for workspace-level activity events such as flow creation, updates, deletion, and membership changes.
  name: workspace/{workspaceId}/activity
  operation: subscribe
  operation_id: receiveWorkspaceActivity
  summary: Receive workspace activity events
description: The elastic.io Platform Events API describes the asynchronous event-driven interactions of the elastic.io iPaaS platform. This includes webhook triggers that initiate integration flows when external systems send HTTP requests, pub/sub topic messaging for inter-flow communication, and platform event notifications for flow execution lifecycle, error handling, and workspace activity.
layout: asyncapi
messages:
- description: ''
  name: WebhookTriggerMessage
  summary: An inbound HTTP payload that triggers an integration flow.
  title: Webhook Trigger Message
- description: ''
  name: TopicMessage
  summary: A message published to or received from a pub/sub topic.
  title: Topic Message
- description: ''
  name: FlowExecutionEvent
  summary: Lifecycle event for flow execution status changes.
  title: Flow Execution Event
- description: ''
  name: FlowErrorEvent
  summary: Error event emitted when a flow step encounters a failure.
  title: Flow Error Event
- description: ''
  name: WorkspaceActivityEvent
  summary: Activity event tracking changes within a workspace.
  title: Workspace Activity Event
name: elastic.io Platform Events API
provider_name: Elastic.io
provider_slug: elastic-io
servers:
- description: Webhook trigger endpoint that receives inbound HTTP requests to start integration flows.
  name: webhooks
  protocol: https
  url: https://in.elastic.io
- description: Platform event notifications for flow executions, errors, and lifecycle events.
  name: platform
  protocol: https
  url: https://api.elastic.io
- description: AMQP message broker used for internal pub/sub topic messaging between integration flows.
  name: amqp
  protocol: amqp
  url: amqp://mq.elastic.io
slug: elastic-io-platform-events-asyncapi
source_filename: elastic-io-platform-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: '2.6.0'\ninfo:\n  title: elastic.io Platform Events API\n  version: 1.0.0\n  description: >-\n    The elastic.io Platform Events API describes the asynchronous event-driven\n    interactions of the elastic.io iPaaS platform. This includes webhook\n    triggers that initiate integration flows when external systems send HTTP\n    requests, pub/sub topic messaging for inter-flow communication, and\n    platform event notifications for flow execution lifecycle, error handling,\n    and workspace activity.\n  contact:\n    name: elastic.io\n    url: https://www.elastic.io/\n  license:\n    name: Proprietary\n    url: https://www.elastic.io/\n\nservers:\n  webhooks:\n    url: https://in.elastic.io\n    protocol: https\n    description: >-\n      Webhook trigger endpoint that receives inbound HTTP requests to\n      start integration flows.\n  platform:\n    url: https://api.elastic.io\n    protocol: https\n    description: >-\n      Platform event notifications for flow\
  \ executions, errors, and\n      lifecycle events.\n  amqp:\n    url: amqp://mq.elastic.io\n    protocol: amqp\n    description: >-\n      AMQP message broker used for internal pub/sub topic messaging\n      between integration flows.\n\nchannels:\n  webhook/flow/{flowId}:\n    description: >-\n      Inbound webhook channel that triggers a specific integration flow\n      when an external system sends an HTTP request.\n    parameters:\n      flowId:\n        description: The unique identifier of the integration flow to trigger.\n        schema:\n          type: string\n          format: uuid\n    publish:\n      operationId: receiveWebhookTrigger\n      summary: Receive a webhook trigger\n      description: >-\n        External systems publish HTTP payloads to this channel to trigger\n        an integration flow execution.\n      message:\n        $ref: '#/components/messages/WebhookTriggerMessage'\n\n  topic/{topicName}:\n    description: >-\n      Pub/sub topic channel for inter-flow\
  \ messaging. Flows can publish\n      messages to a topic, and other flows subscribed to the same topic\n      will receive and process them.\n    parameters:\n      topicName:\n        description: The name of the pub/sub topic.\n        schema:\n          type: string\n    publish:\n      operationId: publishToTopic\n      summary: Publish a message to a topic\n      description: >-\n        An integration flow publishes a message to a named topic for\n        consumption by subscribing flows.\n      message:\n        $ref: '#/components/messages/TopicMessage'\n    subscribe:\n      operationId: subscribeToTopic\n      summary: Receive a message from a topic\n      description: >-\n        An integration flow subscribes to a named topic and receives\n        messages published by other flows.\n      message:\n        $ref: '#/components/messages/TopicMessage'\n\n  flow/{flowId}/execution:\n    description: >-\n      Channel for flow execution lifecycle events including start,\n     \
  \ completion, and failure notifications.\n    parameters:\n      flowId:\n        description: The unique identifier of the integration flow.\n        schema:\n          type: string\n          format: uuid\n    subscribe:\n      operationId: receiveExecutionEvent\n      summary: Receive flow execution events\n      description: >-\n        Subscribe to execution lifecycle events for a specific flow,\n        including started, completed, and failed statuses.\n      message:\n        $ref: '#/components/messages/FlowExecutionEvent'\n\n  flow/{flowId}/error:\n    description: >-\n      Channel for flow error events emitted when a step within an\n      integration flow encounters a processing error.\n    parameters:\n      flowId:\n        description: The unique identifier of the integration flow.\n        schema:\n          type: string\n          format: uuid\n    subscribe:\n      operationId: receiveFlowError\n      summary: Receive flow error events\n      description: >-\n       \
  \ Subscribe to error events for a specific integration flow to\n        monitor failures and trigger alerting.\n      message:\n        $ref: '#/components/messages/FlowErrorEvent'\n\n  workspace/{workspaceId}/activity:\n    description: >-\n      Channel for workspace-level activity events such as flow creation,\n      updates, deletion, and membership changes.\n    parameters:\n      workspaceId:\n        description: The unique identifier of the workspace.\n        schema:\n          type: string\n          format: uuid\n    subscribe:\n      operationId: receiveWorkspaceActivity\n      summary: Receive workspace activity events\n      description: >-\n        Subscribe to activity events within a workspace to track\n        changes to flows, credentials, and members.\n      message:\n        $ref: '#/components/messages/WorkspaceActivityEvent'\n\ncomponents:\n  messages:\n    WebhookTriggerMessage:\n      name: WebhookTriggerMessage\n      title: Webhook Trigger Message\n      summary:\
  \ An inbound HTTP payload that triggers an integration flow.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          headers:\n            type: object\n            description: HTTP headers from the inbound webhook request.\n            additionalProperties:\n              type: string\n          body:\n            type: object\n            description: The parsed JSON body of the webhook request.\n          queryParameters:\n            type: object\n            description: Query string parameters from the webhook URL.\n            additionalProperties:\n              type: string\n          method:\n            type: string\n            description: The HTTP method of the inbound request.\n            enum:\n              - GET\n              - POST\n              - PUT\n              - PATCH\n              - DELETE\n\n    TopicMessage:\n      name: TopicMessage\n      title: Topic Message\n      summary: A message published to or\
  \ received from a pub/sub topic.\n      contentType: application/json\n      payload:\n        type: object\n        required:\n          - id\n          - topicName\n          - data\n        properties:\n          id:\n            type: string\n            format: uuid\n            description: Unique identifier for this message.\n          topicName:\n            type: string\n            description: The name of the topic this message belongs to.\n          data:\n            type: object\n            description: The message payload data.\n          metadata:\n            type: object\n            properties:\n              publishedAt:\n                type: string\n                format: date-time\n                description: Timestamp when the message was published.\n              sourceFlowId:\n                type: string\n                format: uuid\n                description: The flow that published this message.\n              correlationId:\n                type: string\n\
  \                description: Correlation ID for tracing message chains.\n\n    FlowExecutionEvent:\n      name: FlowExecutionEvent\n      title: Flow Execution Event\n      summary: Lifecycle event for flow execution status changes.\n      contentType: application/json\n      payload:\n        type: object\n        required:\n          - executionId\n          - flowId\n          - status\n          - timestamp\n        properties:\n          executionId:\n            type: string\n            format: uuid\n            description: Unique identifier for this execution.\n          flowId:\n            type: string\n            format: uuid\n            description: The flow being executed.\n          status:\n            type: string\n            enum:\n              - started\n              - completed\n              - failed\n              - suspended\n            description: Current execution status.\n          timestamp:\n            type: string\n            format: date-time\n \
  \           description: Timestamp of the status change.\n          duration:\n            type: integer\n            description: Execution duration in milliseconds (when completed).\n          stepCount:\n            type: integer\n            description: Number of steps executed.\n\n    FlowErrorEvent:\n      name: FlowErrorEvent\n      title: Flow Error Event\n      summary: Error event emitted when a flow step encounters a failure.\n      contentType: application/json\n      payload:\n        type: object\n        required:\n          - executionId\n          - flowId\n          - stepId\n          - error\n          - timestamp\n        properties:\n          executionId:\n            type: string\n            format: uuid\n            description: The execution during which the error occurred.\n          flowId:\n            type: string\n            format: uuid\n            description: The flow that encountered the error.\n          stepId:\n            type: string\n      \
  \      description: The step within the flow that failed.\n          error:\n            type: object\n            properties:\n              name:\n                type: string\n                description: Error type name.\n              message:\n                type: string\n                description: Human-readable error message.\n              stack:\n                type: string\n                description: Error stack trace if available.\n          timestamp:\n            type: string\n            format: date-time\n            description: Timestamp when the error occurred.\n          retryable:\n            type: boolean\n            description: Whether the failed step can be retried.\n\n    WorkspaceActivityEvent:\n      name: WorkspaceActivityEvent\n      title: Workspace Activity Event\n      summary: Activity event tracking changes within a workspace.\n      contentType: application/json\n      payload:\n        type: object\n        required:\n          - eventId\n \
  \         - workspaceId\n          - activityType\n          - resourceType\n          - timestamp\n        properties:\n          eventId:\n            type: string\n            format: uuid\n            description: Unique identifier for this activity event.\n          workspaceId:\n            type: string\n            format: uuid\n            description: The workspace where the activity occurred.\n          activityType:\n            type: string\n            enum:\n              - created\n              - updated\n              - deleted\n              - started\n              - stopped\n            description: Type of activity that occurred.\n          resourceType:\n            type: string\n            enum:\n              - flow\n              - credential\n              - component\n              - member\n              - recipe\n            description: Type of resource affected.\n          resourceId:\n            type: string\n            description: Identifier of the\
  \ affected resource.\n          userId:\n            type: string\n            format: uuid\n            description: The user who performed the action.\n          timestamp:\n            type: string\n            format: date-time\n            description: Timestamp of the activity.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/elastic-io/refs/heads/main/asyncapi/elastic-io-platform-events-asyncapi.yml
spec_file: asyncapi/elastic-io-platform-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/elastic-io/refs/heads/main/asyncapi/elastic-io-platform-events-asyncapi.yml
tags:
- Integrations
- iPaaS
- SaaS Integration
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
