---
api_specs:
- filename: adobe-photoshop-api-openapi-original.yml
  format: yaml
  label: Adobe Photoshop API
  slug: photoshop-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-photoshop/refs/heads/main/openapi/adobe-photoshop-api-openapi-original.yml
channels:
- description: Notification delivered when a Photoshop API job has completed successfully. The event payload contains the job ID, output locations, and job metadata. Applies to all PSD service operations including document operations, renditions, Smart Objects, text editing, and Actions execution.
  name: photoshop/job/completed
  operation: subscribe
  operation_id: onJobCompleted
  summary: Receive job completion notifications
- description: Notification delivered when a Photoshop API job has failed. The event payload contains the job ID, error details, and failure reason.
  name: photoshop/job/failed
  operation: subscribe
  operation_id: onJobFailed
  summary: Receive job failure notifications
- description: Notification delivered when a Sensei AI service job has completed successfully. Applies to background removal, mask creation, and other AI-powered image operations.
  name: sensei/job/completed
  operation: subscribe
  operation_id: onSenseiJobCompleted
  summary: Receive Sensei AI job completion notifications
- description: Notification delivered when a Sensei AI service job has failed.
  name: sensei/job/failed
  operation: subscribe
  operation_id: onSenseiJobFailed
  summary: Receive Sensei AI job failure notifications
description: Event-driven notifications for Adobe Photoshop API asynchronous job processing. When registered through Adobe I/O Events, webhooks deliver real-time notifications when Photoshop API jobs complete or fail, eliminating the need to poll status endpoints. Covers all asynchronous operations including background removal, PSD document operations, rendition creation, Smart Object replacement, text editing, Actions execution, product crop, depth blur, and generative fill.
layout: asyncapi
messages:
- description: Webhook event payload delivered when an asynchronous Photoshop API job has completed successfully. Contains the job identifier, output details, and timestamps.
  name: JobCompletedEvent
  summary: Job completed successfully
  title: JobCompletedEvent
- description: Webhook event payload delivered when an asynchronous Photoshop API job has failed. Contains the job identifier, error details, and failure reason.
  name: JobFailedEvent
  summary: Job failed
  title: JobFailedEvent
name: Adobe Photoshop API Webhook Events
provider_name: Adobe Photoshop
provider_slug: adobe-photoshop
servers:
- description: Adobe Photoshop API production server. Webhook events are delivered via Adobe I/O Events to your registered webhook URL when async jobs complete or fail.
  name: production
  protocol: https
  url: https://image.adobe.io
slug: adobe-photoshop-api-asyncapi-original
source_yaml: "asyncapi: 2.0.0\ninfo:\n  title: Adobe Photoshop API Webhook Events\n  description: >-\n    Event-driven notifications for Adobe Photoshop API asynchronous job\n    processing. When registered through Adobe I/O Events, webhooks deliver\n    real-time notifications when Photoshop API jobs complete or fail,\n    eliminating the need to poll status endpoints. Covers all asynchronous\n    operations including background removal, PSD document operations,\n    rendition creation, Smart Object replacement, text editing, Actions\n    execution, product crop, depth blur, and generative fill.\n  version: 1.0.0\n  contact:\n    name: Adobe Developer Support\n    url: https://developer.adobe.com/\n  license:\n    name: Proprietary\n    url: https://www.adobe.com/legal/terms.html\nservers:\n  production:\n    url: https://image.adobe.io\n    protocol: https\n    description: >-\n      Adobe Photoshop API production server. Webhook events are delivered\n      via Adobe I/O Events to your\
  \ registered webhook URL when async jobs\n      complete or fail.\nchannels:\n  photoshop/job/completed:\n    description: >-\n      Notification delivered when a Photoshop API job has completed\n      successfully. The event payload contains the job ID, output\n      locations, and job metadata. Applies to all PSD service operations\n      including document operations, renditions, Smart Objects, text\n      editing, and Actions execution.\n    subscribe:\n      summary: Receive job completion notifications\n      operationId: onJobCompleted\n      message:\n        $ref: '#/components/messages/JobCompletedEvent'\n      bindings:\n        http:\n          type: request\n          method: POST\n          headers:\n            type: object\n            properties:\n              Content-Type:\n                type: string\n                enum:\n                  - application/json\n  photoshop/job/failed:\n    description: >-\n      Notification delivered when a Photoshop API job has failed.\
  \ The event\n      payload contains the job ID, error details, and failure reason.\n    subscribe:\n      summary: Receive job failure notifications\n      operationId: onJobFailed\n      message:\n        $ref: '#/components/messages/JobFailedEvent'\n      bindings:\n        http:\n          type: request\n          method: POST\n          headers:\n            type: object\n            properties:\n              Content-Type:\n                type: string\n                enum:\n                  - application/json\n  sensei/job/completed:\n    description: >-\n      Notification delivered when a Sensei AI service job has completed\n      successfully. Applies to background removal, mask creation, and\n      other AI-powered image operations.\n    subscribe:\n      summary: Receive Sensei AI job completion notifications\n      operationId: onSenseiJobCompleted\n      message:\n        $ref: '#/components/messages/JobCompletedEvent'\n      bindings:\n        http:\n          type: request\n\
  \          method: POST\n          headers:\n            type: object\n            properties:\n              Content-Type:\n                type: string\n                enum:\n                  - application/json\n  sensei/job/failed:\n    description: >-\n      Notification delivered when a Sensei AI service job has failed.\n    subscribe:\n      summary: Receive Sensei AI job failure notifications\n      operationId: onSenseiJobFailed\n      message:\n        $ref: '#/components/messages/JobFailedEvent'\n      bindings:\n        http:\n          type: request\n          method: POST\n          headers:\n            type: object\n            properties:\n              Content-Type:\n                type: string\n                enum:\n                  - application/json\ncomponents:\n  messages:\n    JobCompletedEvent:\n      summary: Job completed successfully\n      description: >-\n        Webhook event payload delivered when an asynchronous Photoshop API\n        job has completed\
  \ successfully. Contains the job identifier, output\n        details, and timestamps.\n      payload:\n        $ref: '#/components/schemas/JobCompletedPayload'\n    JobFailedEvent:\n      summary: Job failed\n      description: >-\n        Webhook event payload delivered when an asynchronous Photoshop API\n        job has failed. Contains the job identifier, error details, and\n        failure reason.\n      payload:\n        $ref: '#/components/schemas/JobFailedPayload'\n  schemas:\n    JobCompletedPayload:\n      type: object\n      properties:\n        jobId:\n          type: string\n          format: uuid\n          description: Unique identifier of the completed job.\n        created:\n          type: string\n          format: date-time\n          description: Timestamp when the job was created.\n        modified:\n          type: string\n          format: date-time\n          description: Timestamp when the job completed.\n        status:\n          type: string\n          const:\
  \ succeeded\n          description: Job completion status.\n        outputs:\n          type: array\n          description: List of output files produced by the job.\n          items:\n            type: object\n            properties:\n              input:\n                type: string\n                description: Original input file reference.\n              status:\n                type: string\n                const: succeeded\n              _links:\n                type: object\n                properties:\n                  self:\n                    type: object\n                    properties:\n                      href:\n                        type: string\n                        format: uri\n                        description: URL to the output file.\n                      storage:\n                        type: string\n                        enum:\n                          - external\n                          - adobe\n                          - azure\n              \
  \            - dropbox\n                        description: Storage type of the output.\n        _links:\n          type: object\n          properties:\n            self:\n              type: object\n              properties:\n                href:\n                  type: string\n                  format: uri\n                  description: URL to the job status resource.\n    JobFailedPayload:\n      type: object\n      properties:\n        jobId:\n          type: string\n          format: uuid\n          description: Unique identifier of the failed job.\n        created:\n          type: string\n          format: date-time\n          description: Timestamp when the job was created.\n        modified:\n          type: string\n          format: date-time\n          description: Timestamp when the job failed.\n        status:\n          type: string\n          const: failed\n          description: Job failure status.\n        outputs:\n          type: array\n          description: Output\
  \ entries with failure details.\n          items:\n            type: object\n            properties:\n              input:\n                type: string\n                description: Original input file reference.\n              status:\n                type: string\n                const: failed\n              errors:\n                type: object\n                properties:\n                  type:\n                    type: string\n                    description: Error type code.\n                  title:\n                    type: string\n                    description: Human-readable error description.\n                  code:\n                    type: integer\n                    description: Error code.\n                  details:\n                    type: object\n                    properties:\n                      reason:\n                        type: string\n                        description: Detailed failure reason.\n        _links:\n          type: object\n      \
  \    properties:\n            self:\n              type: object\n              properties:\n                href:\n                  type: string\n                  format: uri\n                  description: URL to the job status resource.\n    EventMetadata:\n      type: object\n      description: Adobe I/O Events metadata wrapper.\n      properties:\n        eventId:\n          type: string\n          description: Unique event identifier from Adobe I/O Events.\n        eventType:\n          type: string\n          description: >-\n            Event type identifier (e.g., Photoshop API events, Imaging\n            API Events).\n        publishDate:\n          type: string\n          format: date-time\n          description: Timestamp when the event was published.\n        imsOrgId:\n          type: string\n          description: IMS Organization ID associated with the event.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/adobe-photoshop/refs/heads/main/asyncapi/adobe-photoshop-api-asyncapi-original.yml
spec_file: asyncapi/adobe-photoshop-api-asyncapi-original.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/adobe-photoshop/refs/heads/main/asyncapi/adobe-photoshop-api-asyncapi-original.yml
tags:
- AI/ML
- Creative Cloud
- Image Editing
- Photoshop
- Plugins
- REST API
- Scripting
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
