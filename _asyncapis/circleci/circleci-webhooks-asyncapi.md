---
api_specs:
- filename: circleci-rest-api-v2-openapi.yml
  format: yaml
  label: CircleCI REST API V2
  slug: rest-api-v2
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/circleci/refs/heads/main/openapi/circleci-rest-api-v2-openapi.yml
- filename: circleci-rest-api-v1-openapi.yml
  format: yaml
  label: CircleCI REST API V1
  slug: rest-api-v1
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/circleci/refs/heads/main/openapi/circleci-rest-api-v1-openapi.yml
- filename: circleci-runner-api-openapi.yml
  format: yaml
  label: CircleCI Self-Hosted Runner API
  slug: runner-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/circleci/refs/heads/main/openapi/circleci-runner-api-openapi.yml
- filename: circleci-webhooks-asyncapi.yml
  format: yaml
  label: CircleCI Webhooks
  slug: webhooks
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/circleci/refs/heads/main/asyncapi/circleci-webhooks-asyncapi.yml
channels:
- description: CircleCI delivers webhook events as HTTP POST requests with JSON payloads to the configured endpoint URL. Each delivery includes a circleci-signature header containing an HMAC SHA256 digest of the request body for verification.
  name: /webhook
  operation: publish
  operation_id: receiveCircleCIWebhook
  summary: Receive CircleCI webhook events
description: CircleCI Webhooks allow developers to receive real-time notifications about events in their CI/CD pipelines by configuring HTTP callbacks. Webhooks can be set up through project settings or the API to notify external services when workflows and jobs complete, fail, or change status. This enables integration with monitoring systems, chat platforms, and custom automation workflows. Webhooks deliver JSON payloads via HTTP POST to configured endpoint URLs, signed with HMAC SHA256 for verification.
layout: asyncapi
messages:
- description: This event is triggered when a workflow reaches a terminal state (success, failed, error, canceled, or unauthorized). The payload contains information about the workflow, its pipeline, the project, the organization, and the trigger that started the pipeline. Use this event to track workflow completi
  name: WorkflowCompleted
  summary: Fired when all jobs in a workflow have finished running.
  title: Workflow Completed Event
- description: This event is triggered when a job reaches a terminal state (success, failed, canceled, or infrastructure_fail). The payload contains information about the specific job, the workflow it belongs to, the pipeline, the project, and the organization. Use this event for fine-grained tracking of individua
  name: JobCompleted
  summary: Fired when all steps in a job have completed.
  title: Job Completed Event
name: CircleCI Webhooks
provider_name: CircleCI
provider_slug: circleci
servers:
- description: Your webhook endpoint URL. CircleCI sends HTTP POST requests to this URL when events occur. The URL is configured when creating a webhook subscription via project settings or the API.
  name: circleci
  protocol: https
  url: '{webhookUrl}'
slug: circleci-webhooks-asyncapi
source_filename: circleci-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: CircleCI Webhooks\n  description: >-\n    CircleCI Webhooks allow developers to receive real-time notifications\n    about events in their CI/CD pipelines by configuring HTTP callbacks.\n    Webhooks can be set up through project settings or the API to notify\n    external services when workflows and jobs complete, fail, or change\n    status. This enables integration with monitoring systems, chat\n    platforms, and custom automation workflows. Webhooks deliver JSON\n    payloads via HTTP POST to configured endpoint URLs, signed with\n    HMAC SHA256 for verification.\n  version: '1.0'\n  contact:\n    name: CircleCI Support\n    url: https://support.circleci.com\n  license:\n    name: MIT\n  externalDocs:\n    description: CircleCI Webhooks Documentation\n    url: https://circleci.com/docs/webhooks/\nservers:\n  circleci:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your webhook endpoint URL. CircleCI sends HTTP\
  \ POST requests\n      to this URL when events occur. The URL is configured when\n      creating a webhook subscription via project settings or the API.\n    variables:\n      webhookUrl:\n        description: The URL of your webhook receiver endpoint\n    security:\n      - hmacSignature: []\nchannels:\n  /webhook:\n    description: >-\n      CircleCI delivers webhook events as HTTP POST requests with JSON\n      payloads to the configured endpoint URL. Each delivery includes\n      a circleci-signature header containing an HMAC SHA256 digest\n      of the request body for verification.\n    publish:\n      operationId: receiveCircleCIWebhook\n      summary: Receive CircleCI webhook events\n      description: >-\n        Receives webhook event notifications from CircleCI when\n        workflow or job events occur. Events are delivered as HTTP POST\n        requests with JSON payloads. Use the circleci-signature header\n        to verify the authenticity of the delivery.\n      message:\n\
  \        oneOf:\n          - $ref: '#/components/messages/WorkflowCompleted'\n          - $ref: '#/components/messages/JobCompleted'\ncomponents:\n  securitySchemes:\n    hmacSignature:\n      type: httpApiKey\n      name: circleci-signature\n      in: header\n      description: >-\n        HMAC SHA256 signature of the webhook request body, sent in the\n        format v1=<hmac-sha256-digest>. Computed using the signing\n        secret configured when creating the webhook subscription. Use\n        this to verify the authenticity of incoming webhook deliveries.\n  messages:\n    WorkflowCompleted:\n      name: workflow-completed\n      title: Workflow Completed Event\n      summary: >-\n        Fired when all jobs in a workflow have finished running.\n      description: >-\n        This event is triggered when a workflow reaches a terminal state\n        (success, failed, error, canceled, or unauthorized). The payload\n        contains information about the workflow, its pipeline, the\n\
  \        project, the organization, and the trigger that started the\n        pipeline. Use this event to track workflow completion status\n        and trigger downstream automation.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WorkflowCompletedPayload'\n    JobCompleted:\n      name: job-completed\n      title: Job Completed Event\n      summary: >-\n        Fired when all steps in a job have completed.\n      description: >-\n        This event is triggered when a job reaches a terminal state\n        (success, failed, canceled, or infrastructure_fail). The payload\n        contains information about the specific job, the workflow it\n        belongs to, the pipeline, the project, and the organization.\n        Use this event for fine-grained tracking of individual job\n        outcomes within workflows.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/JobCompletedPayload'\n  schemas:\n    WorkflowCompletedPayload:\n\
  \      type: object\n      required:\n        - id\n        - type\n        - happened_at\n        - webhook\n        - project\n        - organization\n        - workflow\n        - pipeline\n      properties:\n        id:\n          type: string\n          format: uuid\n          description: >-\n            Unique identifier for this webhook delivery. Use this to\n            deduplicate events if the same delivery is received multiple\n            times.\n        type:\n          type: string\n          const: workflow-completed\n          description: The type of webhook event\n        happened_at:\n          type: string\n          format: date-time\n          description: >-\n            ISO 8601 timestamp of when the event occurred\n        webhook:\n          $ref: '#/components/schemas/WebhookReference'\n        project:\n          $ref: '#/components/schemas/ProjectReference'\n        organization:\n          $ref: '#/components/schemas/OrganizationReference'\n        workflow:\n\
  \          $ref: '#/components/schemas/WorkflowReference'\n        pipeline:\n          $ref: '#/components/schemas/PipelineReference'\n    JobCompletedPayload:\n      type: object\n      required:\n        - id\n        - type\n        - happened_at\n        - webhook\n        - project\n        - organization\n        - job\n        - workflow\n        - pipeline\n      properties:\n        id:\n          type: string\n          format: uuid\n          description: >-\n            Unique identifier for this webhook delivery. Use this to\n            deduplicate events if the same delivery is received multiple\n            times.\n        type:\n          type: string\n          const: job-completed\n          description: The type of webhook event\n        happened_at:\n          type: string\n          format: date-time\n          description: >-\n            ISO 8601 timestamp of when the event occurred\n        webhook:\n          $ref: '#/components/schemas/WebhookReference'\n  \
  \      project:\n          $ref: '#/components/schemas/ProjectReference'\n        organization:\n          $ref: '#/components/schemas/OrganizationReference'\n        job:\n          $ref: '#/components/schemas/JobReference'\n        workflow:\n          $ref: '#/components/schemas/WorkflowReference'\n        pipeline:\n          $ref: '#/components/schemas/PipelineReference'\n    WebhookReference:\n      type: object\n      description: Reference to the webhook subscription that generated this delivery\n      properties:\n        id:\n          type: string\n          format: uuid\n          description: The unique identifier of the webhook subscription\n        name:\n          type: string\n          description: The name of the webhook subscription\n    ProjectReference:\n      type: object\n      description: The project associated with the event\n      properties:\n        id:\n          type: string\n          format: uuid\n          description: The unique identifier of the project\n\
  \        name:\n          type: string\n          description: The name of the project (repository name)\n        slug:\n          type: string\n          description: >-\n            The project slug in vcs-type/org-name/repo-name format\n    OrganizationReference:\n      type: object\n      description: The organization that owns the project\n      properties:\n        id:\n          type: string\n          format: uuid\n          description: The unique identifier of the organization\n        name:\n          type: string\n          description: The name of the organization\n    WorkflowReference:\n      type: object\n      description: The workflow associated with the event\n      properties:\n        id:\n          type: string\n          format: uuid\n          description: The unique identifier of the workflow\n        name:\n          type: string\n          description: The name of the workflow\n        created_at:\n          type: string\n          format: date-time\n       \
  \   description: When the workflow was created\n        stopped_at:\n          type: string\n          format: date-time\n          description: When the workflow stopped\n        url:\n          type: string\n          format: uri\n          description: URL to view the workflow in the CircleCI web app\n        status:\n          type: string\n          enum:\n            - success\n            - failed\n            - error\n            - canceled\n            - unauthorized\n          description: The terminal status of the workflow\n    JobReference:\n      type: object\n      description: The job associated with the event\n      properties:\n        id:\n          type: string\n          format: uuid\n          description: The unique identifier of the job\n        name:\n          type: string\n          description: The name of the job\n        number:\n          type: integer\n          description: The job number\n        started_at:\n          type: string\n          format: date-time\n\
  \          description: When the job started\n        stopped_at:\n          type: string\n          format: date-time\n          description: When the job stopped\n        status:\n          type: string\n          enum:\n            - success\n            - failed\n            - canceled\n            - infrastructure_fail\n          description: The terminal status of the job\n    PipelineReference:\n      type: object\n      description: The pipeline associated with the event\n      properties:\n        id:\n          type: string\n          format: uuid\n          description: The unique identifier of the pipeline\n        number:\n          type: integer\n          description: The pipeline number\n        created_at:\n          type: string\n          format: date-time\n          description: When the pipeline was created\n        trigger:\n          type: object\n          properties:\n            type:\n              type: string\n              description: >-\n               \
  \ The type of trigger that started the pipeline\n                (e.g., webhook, api, schedule)\n          description: Trigger information\n        vcs:\n          type: object\n          properties:\n            provider_name:\n              type: string\n              description: The VCS provider name\n            origin_repository_url:\n              type: string\n              format: uri\n              description: The origin repository URL\n            target_repository_url:\n              type: string\n              format: uri\n              description: The target repository URL\n            revision:\n              type: string\n              description: The VCS revision (commit SHA)\n            branch:\n              type: string\n              description: The branch name\n            tag:\n              type: string\n              description: The tag name, if applicable\n            commit:\n              type: object\n              properties:\n                subject:\n\
  \                  type: string\n                  description: The commit message subject\n                body:\n                  type: string\n                  description: The commit message body\n                author:\n                  type: object\n                  properties:\n                    name:\n                      type: string\n                      description: The commit author name\n                    email:\n                      type: string\n                      format: email\n                      description: The commit author email\n                  description: Commit author information\n                authored_at:\n                  type: string\n                  format: date-time\n                  description: When the commit was authored\n                committer:\n                  type: object\n                  properties:\n                    name:\n                      type: string\n                      description: The committer name\n\
  \                    email:\n                      type: string\n                      format: email\n                      description: The committer email\n                  description: Committer information\n                committed_at:\n                  type: string\n                  format: date-time\n                  description: When the commit was committed\n              description: Commit information\n          description: VCS information associated with the pipeline\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/circleci/refs/heads/main/asyncapi/circleci-webhooks-asyncapi.yml
spec_file: asyncapi/circleci-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/circleci/refs/heads/main/asyncapi/circleci-webhooks-asyncapi.yml
tags:
- CI/CD
- Continuous Integration
- Continuous Deployment
- DevOps
- Pipelines
- Workflows
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
