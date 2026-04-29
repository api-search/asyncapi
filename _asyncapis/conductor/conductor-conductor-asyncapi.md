---
api_specs:
- filename: conductor-conductor-openapi.yml
  format: yaml
  label: Conductor
  slug: conductor
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/conductor/refs/heads/main/openapi/conductor-conductor-openapi.yml
channels:
- description: Emitted when a workflow execution is started
  name: workflow.started
  operation: subscribe
  operation_id: onWorkflowStarted
  summary: Receive workflow started events
- description: Emitted when a workflow execution completes successfully
  name: workflow.completed
  operation: subscribe
  operation_id: onWorkflowCompleted
  summary: Receive workflow completed events
- description: Emitted when a workflow execution fails
  name: workflow.failed
  operation: subscribe
  operation_id: onWorkflowFailed
  summary: Receive workflow failed events
- description: Emitted when a workflow execution is terminated
  name: workflow.terminated
  operation: subscribe
  operation_id: onWorkflowTerminated
  summary: Receive workflow terminated events
- description: Emitted when a workflow execution times out
  name: workflow.timed_out
  operation: subscribe
  operation_id: onWorkflowTimedOut
  summary: Receive workflow timed out events
- description: Emitted when a workflow execution is paused
  name: workflow.paused
  operation: subscribe
  operation_id: onWorkflowPaused
  summary: Receive workflow paused events
- description: Emitted when a task is scheduled for execution
  name: task.scheduled
  operation: subscribe
  operation_id: onTaskScheduled
  summary: Receive task scheduled events
- description: Emitted when a task execution begins
  name: task.in_progress
  operation: subscribe
  operation_id: onTaskInProgress
  summary: Receive task in progress events
- description: Emitted when a task execution completes successfully
  name: task.completed
  operation: subscribe
  operation_id: onTaskCompleted
  summary: Receive task completed events
- description: Emitted when a task execution fails
  name: task.failed
  operation: subscribe
  operation_id: onTaskFailed
  summary: Receive task failed events
- description: Emitted when a task execution times out
  name: task.timed_out
  operation: subscribe
  operation_id: onTaskTimedOut
  summary: Receive task timed out events
- description: Emitted when a task execution is canceled
  name: task.canceled
  operation: subscribe
  operation_id: onTaskCanceled
  summary: Receive task canceled events
description: Asynchronous event API for Conductor workflow orchestration platform. Conductor emits events when workflows and tasks change state, enabling reactive event-driven architectures. Event handlers can be configured to trigger workflows, complete tasks, or fail tasks in response to these events.
layout: asyncapi
messages:
- description: ''
  name: WorkflowStatusEvent
  summary: An event indicating a change in workflow execution status
  title: Workflow Status Event
- description: ''
  name: TaskStatusEvent
  summary: An event indicating a change in task execution status
  title: Task Status Event
name: Conductor Events API
provider_name: Conductor
provider_slug: conductor
servers:
- description: Local Conductor Server
  name: local
  protocol: http
  url: localhost:8080
- description: Orkes Conductor Playground
  name: playground
  protocol: https
  url: play.orkes.io
slug: conductor-conductor-asyncapi
source_filename: conductor-conductor-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Conductor Events API\n  version: 3.x\n  description: >-\n    Asynchronous event API for Conductor workflow orchestration platform.\n    Conductor emits events when workflows and tasks change state, enabling\n    reactive event-driven architectures. Event handlers can be configured\n    to trigger workflows, complete tasks, or fail tasks in response to\n    these events.\n  contact:\n    name: Conductor OSS\n    url: https://conductor-oss.github.io/conductor/\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\nservers:\n  local:\n    url: localhost:8080\n    protocol: http\n    description: Local Conductor Server\n  playground:\n    url: play.orkes.io\n    protocol: https\n    description: Orkes Conductor Playground\nchannels:\n  workflow.started:\n    description: Emitted when a workflow execution is started\n    subscribe:\n      operationId: onWorkflowStarted\n      summary: Receive workflow started events\n\
  \      message:\n        $ref: '#/components/messages/WorkflowStatusEvent'\n  workflow.completed:\n    description: Emitted when a workflow execution completes successfully\n    subscribe:\n      operationId: onWorkflowCompleted\n      summary: Receive workflow completed events\n      message:\n        $ref: '#/components/messages/WorkflowStatusEvent'\n  workflow.failed:\n    description: Emitted when a workflow execution fails\n    subscribe:\n      operationId: onWorkflowFailed\n      summary: Receive workflow failed events\n      message:\n        $ref: '#/components/messages/WorkflowStatusEvent'\n  workflow.terminated:\n    description: Emitted when a workflow execution is terminated\n    subscribe:\n      operationId: onWorkflowTerminated\n      summary: Receive workflow terminated events\n      message:\n        $ref: '#/components/messages/WorkflowStatusEvent'\n  workflow.timed_out:\n    description: Emitted when a workflow execution times out\n    subscribe:\n      operationId:\
  \ onWorkflowTimedOut\n      summary: Receive workflow timed out events\n      message:\n        $ref: '#/components/messages/WorkflowStatusEvent'\n  workflow.paused:\n    description: Emitted when a workflow execution is paused\n    subscribe:\n      operationId: onWorkflowPaused\n      summary: Receive workflow paused events\n      message:\n        $ref: '#/components/messages/WorkflowStatusEvent'\n  task.scheduled:\n    description: Emitted when a task is scheduled for execution\n    subscribe:\n      operationId: onTaskScheduled\n      summary: Receive task scheduled events\n      message:\n        $ref: '#/components/messages/TaskStatusEvent'\n  task.in_progress:\n    description: Emitted when a task execution begins\n    subscribe:\n      operationId: onTaskInProgress\n      summary: Receive task in progress events\n      message:\n        $ref: '#/components/messages/TaskStatusEvent'\n  task.completed:\n    description: Emitted when a task execution completes successfully\n    subscribe:\n\
  \      operationId: onTaskCompleted\n      summary: Receive task completed events\n      message:\n        $ref: '#/components/messages/TaskStatusEvent'\n  task.failed:\n    description: Emitted when a task execution fails\n    subscribe:\n      operationId: onTaskFailed\n      summary: Receive task failed events\n      message:\n        $ref: '#/components/messages/TaskStatusEvent'\n  task.timed_out:\n    description: Emitted when a task execution times out\n    subscribe:\n      operationId: onTaskTimedOut\n      summary: Receive task timed out events\n      message:\n        $ref: '#/components/messages/TaskStatusEvent'\n  task.canceled:\n    description: Emitted when a task execution is canceled\n    subscribe:\n      operationId: onTaskCanceled\n      summary: Receive task canceled events\n      message:\n        $ref: '#/components/messages/TaskStatusEvent'\ncomponents:\n  messages:\n    WorkflowStatusEvent:\n      name: WorkflowStatusEvent\n      title: Workflow Status Event\n \
  \     summary: An event indicating a change in workflow execution status\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WorkflowStatusEvent'\n    TaskStatusEvent:\n      name: TaskStatusEvent\n      title: Task Status Event\n      summary: An event indicating a change in task execution status\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TaskStatusEvent'\n  schemas:\n    WorkflowStatusEvent:\n      type: object\n      properties:\n        workflowId:\n          type: string\n          description: Unique workflow instance ID\n        workflowName:\n          type: string\n          description: Name of the workflow definition\n        workflowVersion:\n          type: integer\n          description: Version of the workflow definition\n        correlationId:\n          type: string\n          description: Correlation ID\n        status:\n          type: string\n          description: Current status of\
  \ the workflow\n          enum:\n            - RUNNING\n            - COMPLETED\n            - FAILED\n            - TIMED_OUT\n            - TERMINATED\n            - PAUSED\n        startTime:\n          type: integer\n          description: Start time in epoch milliseconds\n        endTime:\n          type: integer\n          description: End time in epoch milliseconds\n        input:\n          type: object\n          description: Workflow input\n          additionalProperties: true\n        output:\n          type: object\n          description: Workflow output\n          additionalProperties: true\n        reasonForIncompletion:\n          type: string\n          description: Reason for failure or termination\n        priority:\n          type: integer\n          description: Workflow priority\n        parentWorkflowId:\n          type: string\n          description: Parent workflow ID if this is a sub-workflow\n    TaskStatusEvent:\n      type: object\n      properties:\n      \
  \  taskId:\n          type: string\n          description: Unique task instance ID\n        taskType:\n          type: string\n          description: The type of the task\n        taskDefName:\n          type: string\n          description: Task definition name\n        status:\n          type: string\n          description: Current status of the task\n          enum:\n            - IN_PROGRESS\n            - CANCELED\n            - FAILED\n            - FAILED_WITH_TERMINAL_ERROR\n            - COMPLETED\n            - COMPLETED_WITH_ERRORS\n            - SCHEDULED\n            - TIMED_OUT\n            - SKIPPED\n        referenceTaskName:\n          type: string\n          description: Reference name of the task in the workflow\n        workflowInstanceId:\n          type: string\n          description: ID of the workflow instance this task belongs to\n        workflowType:\n          type: string\n          description: Type/name of the workflow\n        correlationId:\n          type:\
  \ string\n          description: Correlation ID\n        scheduledTime:\n          type: integer\n          description: Scheduled time in epoch milliseconds\n        startTime:\n          type: integer\n          description: Start time in epoch milliseconds\n        endTime:\n          type: integer\n          description: End time in epoch milliseconds\n        workerId:\n          type: string\n          description: ID of the worker that polled this task\n        reasonForIncompletion:\n          type: string\n          description: Reason for failure\n        retryCount:\n          type: integer\n          description: Current retry count\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/conductor/refs/heads/main/asyncapi/conductor-conductor-asyncapi.yml
spec_file: asyncapi/conductor-conductor-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/conductor/refs/heads/main/asyncapi/conductor-conductor-asyncapi.yml
tags:
- Automation
- Orchestration
- State
- Tasks
- Workflows
- AsyncAPI
- Webhooks
- Events
version: 3.x
---
