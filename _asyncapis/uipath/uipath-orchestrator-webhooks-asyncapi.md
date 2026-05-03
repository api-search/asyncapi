---
api_specs:
- filename: uipath-orchestrator-openapi.yml
  format: yaml
  label: UiPath Orchestrator API
  slug: uipath-orchestrator-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/openapi/uipath-orchestrator-openapi.yml
- filename: uipath-automation-hub-openapi.yml
  format: yaml
  label: UiPath Automation Hub API
  slug: uipath-automation-hub-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/openapi/uipath-automation-hub-openapi.yml
- filename: uipath-document-understanding-openapi.yml
  format: yaml
  label: UiPath Document Understanding API
  slug: uipath-document-understanding-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/openapi/uipath-document-understanding-openapi.yml
- filename: uipath-data-service-openapi.yml
  format: yaml
  label: UiPath Data Service API
  slug: uipath-data-service-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/openapi/uipath-data-service-openapi.yml
- filename: uipath-platform-management-openapi.yml
  format: yaml
  label: UiPath Platform Management API
  slug: uipath-platform-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/openapi/uipath-platform-management-openapi.yml
- filename: uipath-test-manager-openapi.yml
  format: yaml
  label: UiPath Test Manager API
  slug: uipath-test-manager-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/openapi/uipath-test-manager-openapi.yml
channels:
- description: The channel through which UiPath Orchestrator delivers event notifications to registered webhook subscribers. All event types are delivered to the same configured URL. The event type is identified by the Type field in the payload envelope.
  name: /{organizationName}/{tenantName}/orchestrator_/webhook
  operation: publish
  operation_id: receiveOrchestratorEvent
  summary: Receive an Orchestrator webhook event
description: The UiPath Orchestrator webhook system delivers real-time event notifications to registered HTTP endpoints when automation events occur within the platform. Webhooks cover events for jobs, robots, queues, queue items, processes, and triggers. Each event is delivered as an HTTP POST request with a JSON payload to the subscriber's configured URL. Payload authenticity can be verified using the HMAC-SHA256 signature included in the X-UiPath-Signature header, computed from the raw request body and the webhook's configured secret. Webhook subscriptions are managed via the Orchestrator REST API or the Orchestrator web interface.
layout: asyncapi
messages:
- description: Delivered when a new job is created and queued for execution. Contains the job details including the process name, assigned robot, and initial state. EventId provides a unique identifier for idempotent processing.
  name: JobCreated
  summary: A new automation job was created in Orchestrator
  title: Job Created
- description: Delivered when a job transitions from the Pending state to the Running state, indicating a robot has begun executing the automation process.
  name: JobStarted
  summary: An automation job started executing
  title: Job Started
- description: Delivered when a job finishes execution with a Successful state. The payload includes the job's output arguments if the process returned any output parameters.
  name: JobCompleted
  summary: An automation job completed successfully
  title: Job Completed
- description: Delivered when a job terminates with a Faulted state due to an unhandled exception or system error. The Info field in the job payload contains the error message and stack trace details.
  name: JobFaulted
  summary: An automation job encountered a fatal error
  title: Job Faulted
- description: Delivered when a job is manually stopped or terminated by a Kill command. The payload contains the final job state and stop time.
  name: JobStopped
  summary: An automation job was stopped by a user or system
  title: Job Stopped
- description: Delivered when a UiPath Robot establishes a connection to the Orchestrator service and becomes available for job execution.
  name: RobotConnected
  summary: A robot connected to Orchestrator
  title: Robot Connected
- description: Delivered when a UiPath Robot loses its connection to the Orchestrator service, either due to a network interruption or a graceful shutdown.
  name: RobotDisconnected
  summary: A robot disconnected from Orchestrator
  title: Robot Disconnected
- description: Delivered when a robot registration is permanently removed from Orchestrator. The payload contains the deleted robot's identifiers and last known properties.
  name: RobotDeleted
  summary: A robot was deleted from Orchestrator
  title: Robot Deleted
- description: Delivered when a new transaction item is added to a queue, either via the Orchestrator API or by a robot using the Add Queue Item activity. Contains the queue item details and the target queue.
  name: QueueItemAdded
  summary: A new item was added to a queue
  title: Queue Item Added
- description: Delivered when a robot picks up a queue item for processing, transitioning the item status from New to InProgress.
  name: QueueItemTransactionStarted
  summary: A robot began processing a queue transaction item
  title: Queue Item Transaction Started
- description: Delivered when a robot successfully completes processing of a queue item, setting its status to Successful. The payload includes the robot, processing times, and any output written by the robot.
  name: QueueItemTransactionCompleted
  summary: A queue transaction item was successfully processed
  title: Queue Item Transaction Completed
- description: Delivered when a robot fails to process a queue item, setting its status to Failed. The payload includes the error type, message, and retry count. If retries are configured, the item may be automatically re-queued.
  name: QueueItemTransactionFailed
  summary: A queue transaction item processing failed
  title: Queue Item Transaction Failed
- description: Delivered when a queue item is abandoned, typically when the robot processing it disconnects unexpectedly. The item may be automatically returned to the queue for retry depending on queue configuration.
  name: QueueItemTransactionAbandoned
  summary: A queue transaction item was abandoned without processing
  title: Queue Item Transaction Abandoned
- description: Delivered when a new process (release) is created by deploying a package to a folder in Orchestrator.
  name: ProcessCreated
  summary: A new automation process was deployed to a folder
  title: Process Created
- description: Delivered when an existing process is updated, such as when a newer package version is associated with the process definition.
  name: ProcessUpdated
  summary: An automation process was updated
  title: Process Updated
- description: Delivered when a process is permanently removed from Orchestrator. Any jobs associated with this process that have not yet started will be cancelled.
  name: ProcessDeleted
  summary: An automation process was deleted
  title: Process Deleted
name: UiPath Orchestrator Webhook Events
provider_name: UiPath
provider_slug: uipath
servers:
- description: The subscriber-configured HTTPS endpoint that receives webhook event POST requests from UiPath Orchestrator. The URL is specified when creating a webhook subscription via the Orchestrator API or interface.
  name: subscriberEndpoint
  protocol: https
  url: '{webhookUrl}'
slug: uipath-orchestrator-webhooks-asyncapi
source_filename: uipath-orchestrator-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: UiPath Orchestrator Webhook Events\n  description: >-\n    The UiPath Orchestrator webhook system delivers real-time event\n    notifications to registered HTTP endpoints when automation events occur\n    within the platform. Webhooks cover events for jobs, robots, queues,\n    queue items, processes, and triggers. Each event is delivered as an\n    HTTP POST request with a JSON payload to the subscriber's configured URL.\n    Payload authenticity can be verified using the HMAC-SHA256 signature\n    included in the X-UiPath-Signature header, computed from the raw request\n    body and the webhook's configured secret. Webhook subscriptions are\n    managed via the Orchestrator REST API or the Orchestrator web interface.\n  version: '2024.10'\n  contact:\n    name: UiPath Support\n    url: https://support.uipath.com\nexternalDocs:\n  description: UiPath Orchestrator Webhooks Documentation\n  url: https://docs.uipath.com/orchestrator/automation-cloud/latest/user-guide/about-webhooks\n\
  servers:\n  subscriberEndpoint:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      The subscriber-configured HTTPS endpoint that receives webhook event\n      POST requests from UiPath Orchestrator. The URL is specified when\n      creating a webhook subscription via the Orchestrator API or interface.\n    variables:\n      webhookUrl:\n        description: The HTTPS URL of the webhook receiver endpoint\n        default: https://your-app.example.com/webhook\n    security:\n      - hmacSignature: []\nchannels:\n  /{organizationName}/{tenantName}/orchestrator_/webhook:\n    description: >-\n      The channel through which UiPath Orchestrator delivers event notifications\n      to registered webhook subscribers. All event types are delivered to the\n      same configured URL. The event type is identified by the Type field in\n      the payload envelope.\n    parameters:\n      organizationName:\n        description: The UiPath organization name\n        schema:\n  \
  \        type: string\n      tenantName:\n        description: The UiPath tenant name\n        schema:\n          type: string\n    publish:\n      operationId: receiveOrchestratorEvent\n      summary: Receive an Orchestrator webhook event\n      description: >-\n        An HTTP POST request delivered by UiPath Orchestrator to the subscriber\n        URL whenever a subscribed event occurs. The payload contains a Type\n        field identifying the event, an EventId for idempotency, a Timestamp,\n        and event-specific data. The X-UiPath-Signature header contains the\n        HMAC-SHA256 signature for payload verification.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/JobCreated'\n          - $ref: '#/components/messages/JobStarted'\n          - $ref: '#/components/messages/JobCompleted'\n          - $ref: '#/components/messages/JobFaulted'\n          - $ref: '#/components/messages/JobStopped'\n          - $ref: '#/components/messages/RobotConnected'\n  \
  \        - $ref: '#/components/messages/RobotDisconnected'\n          - $ref: '#/components/messages/RobotDeleted'\n          - $ref: '#/components/messages/QueueItemAdded'\n          - $ref: '#/components/messages/QueueItemTransactionStarted'\n          - $ref: '#/components/messages/QueueItemTransactionCompleted'\n          - $ref: '#/components/messages/QueueItemTransactionFailed'\n          - $ref: '#/components/messages/QueueItemTransactionAbandoned'\n          - $ref: '#/components/messages/ProcessCreated'\n          - $ref: '#/components/messages/ProcessUpdated'\n          - $ref: '#/components/messages/ProcessDeleted'\ncomponents:\n  securitySchemes:\n    hmacSignature:\n      type: httpApiKey\n      name: X-UiPath-Signature\n      in: header\n      description: >-\n        HMAC-SHA256 signature of the raw request body, computed using the\n        webhook secret configured at subscription time. Verify this signature\n        to ensure the payload originated from UiPath Orchestrator\
  \ and has\n        not been tampered with.\n  messages:\n    JobCreated:\n      name: job.created\n      title: Job Created\n      summary: A new automation job was created in Orchestrator\n      description: >-\n        Delivered when a new job is created and queued for execution. Contains\n        the job details including the process name, assigned robot, and initial\n        state. EventId provides a unique identifier for idempotent processing.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/JobEventPayload'\n    JobStarted:\n      name: job.started\n      title: Job Started\n      summary: An automation job started executing\n      description: >-\n        Delivered when a job transitions from the Pending state to the Running\n        state, indicating a robot has begun\
  \ executing the automation process.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/JobEventPayload'\n    JobCompleted:\n      name: job.completed\n      title: Job Completed\n      summary: An automation job completed successfully\n      description: >-\n        Delivered when a job finishes execution with a Successful state.\n        The payload includes the job's output arguments if the process\n        returned any output parameters.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/JobEventPayload'\n    JobFaulted:\n      name: job.faulted\n      title: Job Faulted\n\
  \      summary: An automation job encountered a fatal error\n      description: >-\n        Delivered when a job terminates with a Faulted state due to an\n        unhandled exception or system error. The Info field in the job\n        payload contains the error message and stack trace details.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/JobEventPayload'\n    JobStopped:\n      name: job.stopped\n      title: Job Stopped\n      summary: An automation job was stopped by a user or system\n      description: >-\n        Delivered when a job is manually stopped or terminated by a Kill\n        command. The payload contains the final job state and stop time.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n  \
  \          description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/JobEventPayload'\n    RobotConnected:\n      name: robot.connected\n      title: Robot Connected\n      summary: A robot connected to Orchestrator\n      description: >-\n        Delivered when a UiPath Robot establishes a connection to the\n        Orchestrator service and becomes available for job execution.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/RobotEventPayload'\n    RobotDisconnected:\n      name: robot.disconnected\n      title: Robot Disconnected\n      summary: A robot disconnected from Orchestrator\n      description: >-\n        Delivered when a UiPath Robot loses its connection to the Orchestrator\n        service,\
  \ either due to a network interruption or a graceful shutdown.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/RobotEventPayload'\n    RobotDeleted:\n      name: robot.deleted\n      title: Robot Deleted\n      summary: A robot was deleted from Orchestrator\n      description: >-\n        Delivered when a robot registration is permanently removed from\n        Orchestrator. The payload contains the deleted robot's identifiers\n        and last known properties.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/RobotEventPayload'\n    QueueItemAdded:\n      name: queueItem.added\n\
  \      title: Queue Item Added\n      summary: A new item was added to a queue\n      description: >-\n        Delivered when a new transaction item is added to a queue, either\n        via the Orchestrator API or by a robot using the Add Queue Item\n        activity. Contains the queue item details and the target queue.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/QueueItemEventPayload'\n    QueueItemTransactionStarted:\n      name: queueItem.transactionStarted\n      title: Queue Item Transaction Started\n      summary: A robot began processing a queue transaction item\n      description: >-\n        Delivered when a robot picks up a queue item for processing,\n        transitioning the item status from New to InProgress.\n      headers:\n        type: object\n        properties:\n\
  \          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/QueueItemEventPayload'\n    QueueItemTransactionCompleted:\n      name: queueItem.transactionCompleted\n      title: Queue Item Transaction Completed\n      summary: A queue transaction item was successfully processed\n      description: >-\n        Delivered when a robot successfully completes processing of a queue\n        item, setting its status to Successful. The payload includes the\n        robot, processing times, and any output written by the robot.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/QueueItemEventPayload'\n    QueueItemTransactionFailed:\n      name: queueItem.transactionFailed\n\
  \      title: Queue Item Transaction Failed\n      summary: A queue transaction item processing failed\n      description: >-\n        Delivered when a robot fails to process a queue item, setting its\n        status to Failed. The payload includes the error type, message,\n        and retry count. If retries are configured, the item may be\n        automatically re-queued.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/QueueItemEventPayload'\n    QueueItemTransactionAbandoned:\n      name: queueItem.transactionAbandoned\n      title: Queue Item Transaction Abandoned\n      summary: A queue transaction item was abandoned without processing\n      description: >-\n        Delivered when a queue item is abandoned, typically when the robot\n        processing it disconnects unexpectedly.\
  \ The item may be automatically\n        returned to the queue for retry depending on queue configuration.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/QueueItemEventPayload'\n    ProcessCreated:\n      name: process.created\n      title: Process Created\n      summary: A new automation process was deployed to a folder\n      description: >-\n        Delivered when a new process (release) is created by deploying a\n        package to a folder in Orchestrator.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/ProcessEventPayload'\n    ProcessUpdated:\n      name: process.updated\n\
  \      title: Process Updated\n      summary: An automation process was updated\n      description: >-\n        Delivered when an existing process is updated, such as when a\n        newer package version is associated with the process definition.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description: HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/ProcessEventPayload'\n    ProcessDeleted:\n      name: process.deleted\n      title: Process Deleted\n      summary: An automation process was deleted\n      description: >-\n        Delivered when a process is permanently removed from Orchestrator.\n        Any jobs associated with this process that have not yet started\n        will be cancelled.\n      headers:\n        type: object\n        properties:\n          X-UiPath-Signature:\n            type: string\n            description:\
  \ HMAC-SHA256 signature of the request body for payload verification\n      payload:\n        $ref: '#/components/schemas/ProcessEventPayload'\n  schemas:\n    WebhookEventEnvelope:\n      type: object\n      description: Common envelope fields present in all Orchestrator webhook event payloads\n      required:\n        - Type\n        - EventId\n        - Timestamp\n      properties:\n        Type:\n          type: string\n          description: >-\n            Machine-readable event type identifier (e.g., job.faulted,\n            queueItem.transactionCompleted). Use this field to route the\n            payload to the appropriate handler.\n        EventId:\n          type: string\n          format: uuid\n          description: Unique GUID identifier for this event delivery. Use for idempotent processing.\n        Timestamp:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp when the event occurred in Orchestrator\n    JobEventPayload:\n  \
  \    allOf:\n        - $ref: '#/components/schemas/WebhookEventEnvelope'\n        - type: object\n          description: Webhook event payload for job lifecycle events\n          properties:\n            Job:\n              $ref: '#/components/schemas/WebhookJob'\n    WebhookJob:\n      type: object\n      description: Job data included in job lifecycle webhook events\n      properties:\n        Id:\n          type: integer\n          format: int64\n          description: Unique integer identifier of the job\n        Key:\n          type: string\n          format: uuid\n          description: Unique GUID key of the job\n        ReleaseName:\n          type: string\n          description: Name of the process that the job executes\n        ProcessVersion:\n          type: string\n          description: Package version used by the job\n        State:\n          type: string\n          enum: [Pending, Running, Stopping, Terminating, Faulted, Successful, Stopped, Suspended, Resumed]\n     \
  \     description: Current execution state of the job\n        StartTime:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp when the job started\n        EndTime:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp when the job ended\n        Info:\n          type: string\n          description: Additional information or error message, especially relevant for Faulted state\n        Robot:\n          $ref: '#/components/schemas/WebhookRobotRef'\n        OrganizationUnitId:\n          type: integer\n          format: int64\n          description: Folder ID in which the job ran\n        OutputArguments:\n          type: string\n          description: JSON-serialized output arguments returned by the process on completion\n    WebhookRobotRef:\n      type: object\n      description: Robot reference included in job event payloads\n      properties:\n        Id:\n          type: integer\n          format:\
  \ int64\n          description: Unique integer identifier of the robot\n        Name:\n          type: string\n          description: Display name of the robot\n        MachineName:\n          type: string\n          description: Hostname of the machine the robot executed on\n        MachineId:\n          type: integer\n          format: int64\n          description: Unique integer identifier of the machine\n        Version:\n          type: string\n          description: Version of the UiPath Robot software\n        Type:\n          type: string\n          description: Licensing type of the robot\n        HostingType:\n          type: string\n          enum: [Standard, Serverless, NonProduction]\n          description: Robot hosting classification\n        UserName:\n          type: string\n          description: Windows or Linux username the robot runs under\n    RobotEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEventEnvelope'\n        - type: object\n  \
  \        description: Webhook event payload for robot lifecycle events\n          properties:\n            Robot:\n              $ref: '#/components/schemas/WebhookRobot'\n    WebhookRobot:\n      type: object\n      description: Robot data included in robot lifecycle webhook events\n      properties:\n        Id:\n          type: integer\n          format: int64\n          description: Unique integer identifier of the robot\n        Name:\n          type: string\n          description: Display name of the robot\n        MachineName:\n          type: string\n          description: Hostname of the machine this robot is registered on\n        MachineId:\n          type: integer\n          format: int64\n          description: Unique integer identifier of the machine\n        Type:\n          type: string\n          description: Licensing type of the robot\n        OrganizationUnitId:\n          type: integer\n          format: int64\n          description: Folder ID to which the robot is\
  \ assigned\n    QueueItemEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEventEnvelope'\n        - type: object\n          description: Webhook event payload for queue item lifecycle events\n          properties:\n            QueueItem:\n              $ref: '#/components/schemas/WebhookQueueItem'\n            Queue:\n              $ref: '#/components/schemas/WebhookQueueRef'\n    WebhookQueueItem:\n      type: object\n      description: Queue item data included in queue item lifecycle webhook events\n      properties:\n        Id:\n          type: integer\n          format: int64\n          description: Unique integer identifier of the queue item\n        Key:\n          type: string\n          format: uuid\n          description: Unique GUID key of the queue item\n        QueueDefinitionId:\n          type: integer\n          format: int64\n          description: ID of the queue this item belongs to\n        Status:\n          type: string\n          enum: [New,\
  \ InProgress, Failed, Successful, Abandoned, Retried, Deleted]\n          description: Processing status of the queue item at event time\n        ReviewStatus:\n          type: string\n          enum: [None, InReview, Verified, Retried]\n          description: Manual review status for failed items\n        Priority:\n          type: string\n          enum: [Low, Normal, High]\n          description: Processing priority of the queue item\n        CreationTime:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp when the item was added to the queue\n        StartProcessing:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp when processing began\n        EndProcessing:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp when processing ended\n        RetryNumber:\n          type: integer\n          description: Number of times this item has been retried\n \
  \       Robot:\n          $ref: '#/components/schemas/WebhookRobotRef'\n        SpecificContent:\n          type: object\n          additionalProperties: true\n          description: Custom key-value payload data for the queue item\n        Output:\n          type: object\n          additionalProperties: true\n          description: Output data written by the robot during processing\n    WebhookQueueRef:\n      type: object\n      description: Queue reference included in queue item event payloads\n      properties:\n        Id:\n          type: integer\n          format: int64\n          description: Unique integer identifier of the queue definition\n        Name:\n          type: string\n          description: Display name of the queue\n        Description:\n          type: string\n          description: Description of the queue\n        MaxNumberOfRetries:\n          type: integer\n          description: Maximum number of automatic retries configured for the queue\n        AcceptAutomaticallyRetry:\n\
  \          type: boolean\n          description: Whether failed items are automatically requeued for retry\n        EnforceUniqueReference:\n          type: boolean\n          description: Whether unique references are enforced on this queue\n    ProcessEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEventEnvelope'\n        - type: object\n          description: Webhook event payload for process lifecycle events\n          properties:\n            Process:\n              $ref: '#/components/schemas/WebhookProcess'\n    WebhookProcess:\n      type: object\n      description: Process data included in process lifecycle webhook events\n      properties:\n        Id:\n          type: integer\n          format: int64\n          description: Unique integer identifier of the process\n        Name:\n          type: string\n          description: Display name of the process\n        Key:\n          type: string\n          format: uuid\n          description: Unique GUID\
  \ key of the process\n        ProcessVersion:\n          type: string\n          description: Version of the underlying package\n        OrganizationUnitId:\n          type: integer\n          format: int64\n          description: Folder ID in which the process is deployed\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/asyncapi/uipath-orchestrator-webhooks-asyncapi.yml
spec_file: asyncapi/uipath-orchestrator-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/uipath/refs/heads/main/asyncapi/uipath-orchestrator-webhooks-asyncapi.yml
tags:
- Automation
- Robotic Process Automation
- RPA
- Artificial Intelligence
- Document Processing
- Enterprise Automation
- Orchestration
- Testing
- AsyncAPI
- Webhooks
- Events
version: '2024.10'
---
