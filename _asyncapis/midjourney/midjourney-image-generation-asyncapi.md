---
api_specs:
- filename: midjourney-image-generation-openapi.yml
  format: yaml
  label: Midjourney Image Generation API
  slug: image-generation-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/midjourney/refs/heads/main/openapi/midjourney-image-generation-openapi.yml
channels:
- description: Webhook delivery channel for image generation job status events. Events are sent as HTTP POST requests with a JSON payload containing the full job object. The webhook_type parameter specified during job creation controls whether progress updates or only final results are delivered.
  name: /webhook
  operation: publish
  operation_id: receiveJobStatusEvent
  summary: Receive job status change notifications
description: The Midjourney Image Generation webhook interface delivers real-time notifications about image generation job status changes. When a webhook URL is provided during job creation, Midjourney sends HTTP POST requests to the specified URL whenever a job transitions between states such as pending, in progress, completed, or failed. This eliminates the need for polling the job status endpoint and enables event-driven integration patterns for applications consuming Midjourney's image generation capabilities.
layout: asyncapi
messages:
- description: ''
  name: JobProgressEvent
  summary: Sent when a job's progress percentage updates during processing. Only delivered when webhook_type is set to progress.
  title: Job Progress Event
- description: ''
  name: JobCompletedEvent
  summary: Sent when a job finishes successfully and generated images are available for download. The result field contains URLs of all generated images.
  title: Job Completed Event
- description: ''
  name: JobFailedEvent
  summary: Sent when a job fails due to an error such as content policy violation, invalid parameters, or an internal processing error. The error field contains details about the failure.
  title: Job Failed Event
- description: ''
  name: JobCancelledEvent
  summary: Sent when a job is cancelled by the user before completion.
  title: Job Cancelled Event
name: Midjourney Image Generation Webhooks
provider_name: midjourney
provider_slug: midjourney
servers:
- description: The webhook receiver endpoint configured by the client application. Midjourney sends HTTP POST requests to this URL when job status changes occur. The URL is specified per-job in the webhook_url parameter of generation requests.
  name: webhookReceiver
  protocol: https
  url: '{webhookUrl}'
slug: midjourney-image-generation-asyncapi
source_filename: midjourney-image-generation-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Midjourney Image Generation Webhooks\n  description: >-\n    The Midjourney Image Generation webhook interface delivers real-time\n    notifications about image generation job status changes. When a webhook\n    URL is provided during job creation, Midjourney sends HTTP POST requests\n    to the specified URL whenever a job transitions between states such as\n    pending, in progress, completed, or failed. This eliminates the need\n    for polling the job status endpoint and enables event-driven integration\n    patterns for applications consuming Midjourney's image generation\n    capabilities.\n  version: '1.0.0'\n  contact:\n    name: Midjourney Support\n    url: https://docs.midjourney.com/hc/en-us\nservers:\n  webhookReceiver:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      The webhook receiver endpoint configured by the client application.\n      Midjourney sends HTTP POST requests to this URL when job status\n\
  \      changes occur. The URL is specified per-job in the webhook_url\n      parameter of generation requests.\n    variables:\n      webhookUrl:\n        description: >-\n          The client-provided webhook URL that receives job status\n          notifications.\n    security:\n      - webhookSignature: []\nchannels:\n  /webhook:\n    description: >-\n      Webhook delivery channel for image generation job status events.\n      Events are sent as HTTP POST requests with a JSON payload containing\n      the full job object. The webhook_type parameter specified during job\n      creation controls whether progress updates or only final results\n      are delivered.\n    publish:\n      operationId: receiveJobStatusEvent\n      summary: Receive job status change notifications\n      description: >-\n        Receives webhook notifications when an image generation job changes\n        status. The payload includes the complete job object with current\n        status, progress percentage, and\
  \ result data when available. Events\n        are delivered for status transitions including pending to in_progress,\n        in_progress progress updates, and terminal states such as completed,\n        failed, or cancelled.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/JobProgressEvent'\n          - $ref: '#/components/messages/JobCompletedEvent'\n          - $ref: '#/components/messages/JobFailedEvent'\n          - $ref: '#/components/messages/JobCancelledEvent'\ncomponents:\n  securitySchemes:\n    webhookSignature:\n      type: httpApiKey\n      name: X-Midjourney-Signature\n      in: header\n      description: >-\n        HMAC-SHA256 signature of the webhook payload for verifying that\n        the notification originated from Midjourney. The signature is\n        computed using the webhook secret associated with the API key.\n        Clients should validate this signature before processing the\n        webhook payload to prevent spoofed notifications.\n\
  \  messages:\n    JobProgressEvent:\n      name: jobProgress\n      title: Job Progress Event\n      summary: >-\n        Sent when a job's progress percentage updates during processing.\n        Only delivered when webhook_type is set to progress.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/JobWebhookPayload'\n    JobCompletedEvent:\n      name: jobCompleted\n      title: Job Completed Event\n      summary: >-\n        Sent when a job finishes successfully and generated images are\n        available for download. The result field contains URLs of all\n        generated images.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/JobWebhookPayload'\n    JobFailedEvent:\n      name: jobFailed\n      title: Job Failed Event\n      summary: >-\n        Sent when a job fails due to an error such as content policy\n        violation, invalid parameters, or an internal processing error.\n        The error field\
  \ contains details about the failure.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/JobWebhookPayload'\n    JobCancelledEvent:\n      name: jobCancelled\n      title: Job Cancelled Event\n      summary: >-\n        Sent when a job is cancelled by the user before completion.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/JobWebhookPayload'\n  schemas:\n    JobWebhookPayload:\n      type: object\n      description: >-\n        The webhook payload delivered for job status change events.\n        Contains the complete job object with current state and results.\n      required:\n        - event\n        - job_id\n        - status\n        - timestamp\n      properties:\n        event:\n          type: string\n          description: >-\n            The type of webhook event being delivered.\n          enum:\n            - job.progress\n            - job.completed\n            - job.failed\n            - job.cancelled\n\
  \        job_id:\n          type: string\n          format: uuid\n          description: >-\n            The unique identifier of the job that triggered this event.\n        status:\n          type: string\n          description: >-\n            The current status of the job.\n          enum:\n            - pending\n            - in_progress\n            - completed\n            - failed\n            - cancelled\n        progress:\n          type: integer\n          description: >-\n            The completion progress as a percentage from 0 to 100.\n          minimum: 0\n          maximum: 100\n        type:\n          type: string\n          description: >-\n            The type of image generation operation.\n          enum:\n            - imagine\n            - upscale\n            - variation\n            - describe\n            - blend\n        prompt:\n          type: string\n          description: >-\n            The text prompt used for the generation job.\n        result:\n  \
  \        type: object\n          description: >-\n            The generation results, present when the job has completed\n            successfully.\n          properties:\n            images:\n              type: array\n              description: >-\n                List of generated image URLs and metadata.\n              items:\n                type: object\n                properties:\n                  url:\n                    type: string\n                    format: uri\n                    description: >-\n                      The download URL for the generated image.\n                  index:\n                    type: integer\n                    description: >-\n                      The position of this image in the generation grid.\n                  width:\n                    type: integer\n                    description: >-\n                      The width of the image in pixels.\n                  height:\n                    type: integer\n                    description:\
  \ >-\n                      The height of the image in pixels.\n            prompts:\n              type: array\n              description: >-\n                Generated prompt suggestions for describe jobs.\n              items:\n                type: string\n        error:\n          type: object\n          description: >-\n            Error details, present when the job has failed.\n          properties:\n            code:\n              type: string\n              description: >-\n                Machine-readable error code.\n            message:\n              type: string\n              description: >-\n                Human-readable error description.\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            ISO 8601 timestamp when this webhook event was generated.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/midjourney/refs/heads/main/asyncapi/midjourney-image-generation-asyncapi.yml
spec_file: asyncapi/midjourney-image-generation-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/midjourney/refs/heads/main/asyncapi/midjourney-image-generation-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
