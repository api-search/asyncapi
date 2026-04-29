---
api_specs:
- filename: adobe-analytics-api-openapi.yml
  format: yaml
  label: Adobe Analytics 2.0 API
  slug: analytics-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-experience-cloud/refs/heads/main/openapi/adobe-analytics-api-openapi.yml
- filename: adobe-experience-platform-api-openapi.yml
  format: yaml
  label: Adobe Experience Platform API
  slug: experience-platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-experience-cloud/refs/heads/main/openapi/adobe-experience-platform-api-openapi.yml
- filename: adobe-target-api-openapi.yml
  format: yaml
  label: Adobe Target API
  slug: target-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-experience-cloud/refs/heads/main/openapi/adobe-target-api-openapi.yml
- filename: adobe-journey-optimizer-api-openapi.yml
  format: yaml
  label: Adobe Journey Optimizer API
  slug: journey-optimizer-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-experience-cloud/refs/heads/main/openapi/adobe-journey-optimizer-api-openapi.yml
- filename: adobe-campaign-api-openapi.yml
  format: yaml
  label: Adobe Campaign API
  slug: campaign-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-experience-cloud/refs/heads/main/openapi/adobe-campaign-api-openapi.yml
- filename: adobe-io-events-asyncapi.yml
  format: yaml
  label: Adobe I/O Events
  slug: io-events
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-experience-cloud/refs/heads/main/asyncapi/adobe-io-events-asyncapi.yml
channels:
- description: Events emitted when batch ingestion operations complete or fail on Adobe Experience Platform datasets.
  name: experience-platform/dataset-ingestion
  operation: subscribe
  operation_id: onDatasetIngestionEvent
  summary: Receive dataset ingestion events
- description: Events emitted when unified profile records are created or updated in Adobe Experience Platform.
  name: experience-platform/profile-update
  operation: subscribe
  operation_id: onProfileUpdateEvent
  summary: Receive profile update events
- description: Events emitted when audience segment evaluation jobs complete in Adobe Experience Platform.
  name: experience-platform/segment-evaluation
  operation: subscribe
  operation_id: onSegmentEvaluationEvent
  summary: Receive segment evaluation events
- description: Events emitted when configuration changes are made to Adobe Analytics report suites.
  name: analytics/report-suite-change
  operation: subscribe
  operation_id: onReportSuiteChangeEvent
  summary: Receive report suite change events
- description: Events emitted when Adobe Campaign email or message deliveries change status, including sends, bounces, and opens.
  name: campaign/delivery-status
  operation: subscribe
  operation_id: onDeliveryStatusEvent
  summary: Receive delivery status events
- description: Events emitted when Adobe Campaign workflow executions start, complete, or encounter errors.
  name: campaign/workflow-execution
  operation: subscribe
  operation_id: onWorkflowExecutionEvent
  summary: Receive workflow execution events
- description: Events emitted when Adobe Target activities change state, such as activation, deactivation, or archival.
  name: target/activity-state-change
  operation: subscribe
  operation_id: onActivityStateChangeEvent
  summary: Receive activity state change events
- description: Events emitted when profiles progress through journey steps in Adobe Journey Optimizer.
  name: journey-optimizer/journey-step
  operation: subscribe
  operation_id: onJourneyStepEvent
  summary: Receive journey step events
description: Adobe I/O Events enables developers to receive near-real-time notifications from Adobe services via webhooks and journal polling. Events are emitted when significant changes occur across Adobe Experience Cloud products including Experience Platform, Creative Cloud, Campaign, and Analytics. Developers register webhook endpoints or poll a journaling API to consume events for building reactive integrations and automated workflows.
layout: asyncapi
messages:
- description: ''
  name: DatasetIngestionEvent
  summary: Notification of a dataset batch ingestion completion or failure.
  title: Dataset Ingestion Event
- description: ''
  name: ProfileUpdateEvent
  summary: Notification of a unified profile creation or update.
  title: Profile Update Event
- description: ''
  name: SegmentEvaluationEvent
  summary: Notification of a segment evaluation job completion.
  title: Segment Evaluation Event
- description: ''
  name: ReportSuiteChangeEvent
  summary: Notification of an Analytics report suite configuration change.
  title: Report Suite Change Event
- description: ''
  name: DeliveryStatusEvent
  summary: Notification of a Campaign delivery status change.
  title: Delivery Status Event
- description: ''
  name: WorkflowExecutionEvent
  summary: Notification of a Campaign workflow execution status change.
  title: Workflow Execution Event
- description: ''
  name: ActivityStateChangeEvent
  summary: Notification of a Target activity state transition.
  title: Activity State Change Event
- description: ''
  name: JourneyStepEvent
  summary: Notification of a profile progressing through a journey step.
  title: Journey Step Event
name: Adobe I/O Events
provider_name: Adobe Experience Cloud
provider_slug: adobe-experience-cloud
servers:
- description: Your webhook endpoint that receives Adobe I/O Events via HTTP POST. Must respond to a challenge request for registration verification.
  name: webhook
  protocol: https
  url: https://{yourDomain}/webhook
- description: Adobe I/O Events journaling API for polling events. Use this as an alternative to webhooks for reliable, at-least-once event delivery.
  name: journal
  protocol: https
  url: https://events.adobe.io
slug: adobe-io-events-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Adobe I/O Events\n  version: 1.0.0\n  description: >-\n    Adobe I/O Events enables developers to receive near-real-time notifications\n    from Adobe services via webhooks and journal polling. Events are emitted\n    when significant changes occur across Adobe Experience Cloud products\n    including Experience Platform, Creative Cloud, Campaign, and Analytics.\n    Developers register webhook endpoints or poll a journaling API to consume\n    events for building reactive integrations and automated workflows.\n  contact:\n    name: Adobe Developer\n    url: https://developer.adobe.com/events/docs/\n  license:\n    name: Proprietary\n    url: https://www.adobe.com/legal/terms.html\nservers:\n  webhook:\n    url: https://{yourDomain}/webhook\n    protocol: https\n    description: >-\n      Your webhook endpoint that receives Adobe I/O Events via HTTP POST.\n      Must respond to a challenge request for registration verification.\n    variables:\n\
  \      yourDomain:\n        default: example.com\n        description: Your registered webhook domain.\n  journal:\n    url: https://events.adobe.io\n    protocol: https\n    description: >-\n      Adobe I/O Events journaling API for polling events. Use this as an\n      alternative to webhooks for reliable, at-least-once event delivery.\nchannels:\n  experience-platform/dataset-ingestion:\n    description: >-\n      Events emitted when batch ingestion operations complete or fail on\n      Adobe Experience Platform datasets.\n    subscribe:\n      operationId: onDatasetIngestionEvent\n      summary: Receive dataset ingestion events\n      description: >-\n        Triggered when a batch ingestion operation on an Experience Platform\n        dataset completes successfully or fails. Includes the batch ID,\n        dataset ID, and ingestion status.\n      tags:\n      - name: Experience Platform\n      - name: Data Ingestion\n      message:\n        $ref: '#/components/messages/DatasetIngestionEvent'\n\
  \  experience-platform/profile-update:\n    description: >-\n      Events emitted when unified profile records are created or updated in\n      Adobe Experience Platform.\n    subscribe:\n      operationId: onProfileUpdateEvent\n      summary: Receive profile update events\n      description: >-\n        Triggered when a unified customer profile is created or updated in\n        Experience Platform. Includes the profile identity and the nature of\n        the change.\n      tags:\n      - name: Experience Platform\n      - name: Profiles\n      message:\n        $ref: '#/components/messages/ProfileUpdateEvent'\n  experience-platform/segment-evaluation:\n    description: >-\n      Events emitted when audience segment evaluation jobs complete in\n      Adobe Experience Platform.\n    subscribe:\n      operationId: onSegmentEvaluationEvent\n      summary: Receive segment evaluation events\n      description: >-\n        Triggered when a segment evaluation job completes, indicating the\n \
  \       segment membership has been recalculated. Includes the segment ID,\n        job ID, and resulting profile count.\n      tags:\n      - name: Experience Platform\n      - name: Segmentation\n      message:\n        $ref: '#/components/messages/SegmentEvaluationEvent'\n  analytics/report-suite-change:\n    description: >-\n      Events emitted when configuration changes are made to Adobe Analytics\n      report suites.\n    subscribe:\n      operationId: onReportSuiteChangeEvent\n      summary: Receive report suite change events\n      description: >-\n        Triggered when a report suite configuration is modified, including\n        changes to processing rules, classification uploads, and data source\n        configurations.\n      tags:\n      - name: Analytics\n      - name: Configuration\n      message:\n        $ref: '#/components/messages/ReportSuiteChangeEvent'\n  campaign/delivery-status:\n    description: >-\n      Events emitted when Adobe Campaign email or message deliveries\
  \ change\n      status, including sends, bounces, and opens.\n    subscribe:\n      operationId: onDeliveryStatusEvent\n      summary: Receive delivery status events\n      description: >-\n        Triggered when the delivery status of a Campaign message changes.\n        Includes the delivery ID, recipient, and new status such as sent,\n        delivered, bounced, or opened.\n      tags:\n      - name: Campaign\n      - name: Delivery\n      message:\n        $ref: '#/components/messages/DeliveryStatusEvent'\n  campaign/workflow-execution:\n    description: >-\n      Events emitted when Adobe Campaign workflow executions start, complete,\n      or encounter errors.\n    subscribe:\n      operationId: onWorkflowExecutionEvent\n      summary: Receive workflow execution events\n      description: >-\n        Triggered when a Campaign workflow starts, finishes, or fails. Includes\n        the workflow ID, execution status, and any error details.\n      tags:\n      - name: Campaign\n    \
  \  - name: Workflows\n      message:\n        $ref: '#/components/messages/WorkflowExecutionEvent'\n  target/activity-state-change:\n    description: >-\n      Events emitted when Adobe Target activities change state, such as\n      activation, deactivation, or archival.\n    subscribe:\n      operationId: onActivityStateChangeEvent\n      summary: Receive activity state change events\n      description: >-\n        Triggered when a Target activity transitions between states. Includes\n        the activity ID, name, previous state, and new state.\n      tags:\n      - name: Target\n      - name: Activities\n      message:\n        $ref: '#/components/messages/ActivityStateChangeEvent'\n  journey-optimizer/journey-step:\n    description: >-\n      Events emitted when profiles progress through journey steps in Adobe\n      Journey Optimizer.\n    subscribe:\n      operationId: onJourneyStepEvent\n      summary: Receive journey step events\n      description: >-\n        Triggered when a\
  \ profile enters, exits, or completes a step within\n        a Journey Optimizer journey. Includes the journey ID, step ID,\n        profile identity, and step outcome.\n      tags:\n      - name: Journey Optimizer\n      - name: Journeys\n      message:\n        $ref: '#/components/messages/JourneyStepEvent'\ncomponents:\n  messages:\n    DatasetIngestionEvent:\n      name: DatasetIngestionEvent\n      title: Dataset Ingestion Event\n      summary: Notification of a dataset batch ingestion completion or failure.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DatasetIngestionPayload'\n      examples:\n      - name: DatasetIngestionEventDefaultExample\n        summary: Default DatasetIngestionEvent example\n        x-microcks-default: true\n        payload:\n          event_id: abc123\n          event:\n            body:\n              datasetId: abc123\n              batchId: abc123\n              status: success\n              recordCount: 1\n\
  \              completedAt: '2025-03-15T14:30:00Z'\n            header:\n              eventType: standard\n              imsOrgId: abc123\n              source: example\n    ProfileUpdateEvent:\n      name: ProfileUpdateEvent\n      title: Profile Update Event\n      summary: Notification of a unified profile creation or update.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ProfileUpdatePayload'\n      examples:\n      - name: ProfileUpdateEventDefaultExample\n        summary: Default ProfileUpdateEvent example\n        x-microcks-default: true\n        payload:\n          event_id: abc123\n          event:\n            body:\n              identityMap: {}\n              changeType: created\n              modifiedAt: '2025-03-15T14:30:00Z'\n            header:\n              eventType: standard\n              imsOrgId: abc123\n    SegmentEvaluationEvent:\n      name: SegmentEvaluationEvent\n      title: Segment Evaluation Event\n      summary:\
  \ Notification of a segment evaluation job completion.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SegmentEvaluationPayload'\n      examples:\n      - name: SegmentEvaluationEventDefaultExample\n        summary: Default SegmentEvaluationEvent example\n        x-microcks-default: true\n        payload:\n          event_id: abc123\n          event:\n            body:\n              segmentId: abc123\n              jobId: abc123\n              status: succeeded\n              profileCount: 1\n              completedAt: '2025-03-15T14:30:00Z'\n            header:\n              eventType: standard\n    ReportSuiteChangeEvent:\n      name: ReportSuiteChangeEvent\n      title: Report Suite Change Event\n      summary: Notification of an Analytics report suite configuration change.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ReportSuiteChangePayload'\n      examples:\n      - name: ReportSuiteChangeEventDefaultExample\n\
  \        summary: Default ReportSuiteChangeEvent example\n        x-microcks-default: true\n        payload:\n          event_id: abc123\n          event:\n            body:\n              rsid: abc123\n              changeType: standard\n              changedBy: example\n              changedAt: '2025-03-15T14:30:00Z'\n            header:\n              eventType: standard\n    DeliveryStatusEvent:\n      name: DeliveryStatusEvent\n      title: Delivery Status Event\n      summary: Notification of a Campaign delivery status change.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DeliveryStatusPayload'\n      examples:\n      - name: DeliveryStatusEventDefaultExample\n        summary: Default DeliveryStatusEvent example\n        x-microcks-default: true\n        payload:\n          event_id: abc123\n          event:\n            body:\n              deliveryId: abc123\n              recipientEmail: user@example.com\n              status: sent\n\
  \              timestamp: '2025-03-15T14:30:00Z'\n            header:\n              eventType: standard\n    WorkflowExecutionEvent:\n      name: WorkflowExecutionEvent\n      title: Workflow Execution Event\n      summary: Notification of a Campaign workflow execution status change.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WorkflowExecutionPayload'\n      examples:\n      - name: WorkflowExecutionEventDefaultExample\n        summary: Default WorkflowExecutionEvent example\n        x-microcks-default: true\n        payload:\n          event_id: abc123\n          event:\n            body:\n              workflowId: abc123\n              executionStatus: started\n              errorMessage: example\n              timestamp: '2025-03-15T14:30:00Z'\n            header:\n              eventType: standard\n    ActivityStateChangeEvent:\n      name: ActivityStateChangeEvent\n      title: Activity State Change Event\n      summary: Notification\
  \ of a Target activity state transition.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ActivityStateChangePayload'\n      examples:\n      - name: ActivityStateChangeEventDefaultExample\n        summary: Default ActivityStateChangeEvent example\n        x-microcks-default: true\n        payload:\n          event_id: abc123\n          event:\n            body:\n              activityId: 1\n              activityName: Example Name\n              previousState: example\n              newState: example\n              changedAt: '2025-03-15T14:30:00Z'\n            header:\n              eventType: standard\n    JourneyStepEvent:\n      name: JourneyStepEvent\n      title: Journey Step Event\n      summary: Notification of a profile progressing through a journey step.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/JourneyStepPayload'\n      examples:\n      - name: JourneyStepEventDefaultExample\n        summary:\
  \ Default JourneyStepEvent example\n        x-microcks-default: true\n        payload:\n          event_id: abc123\n          event:\n            body:\n              journeyId: abc123\n              journeyVersionId: abc123\n              stepId: abc123\n              profileId: abc123\n              stepStatus: entered\n              timestamp: '2025-03-15T14:30:00Z'\n            header:\n              eventType: standard\n  schemas:\n    EventEnvelope:\n      type: object\n      description: Common envelope for all Adobe I/O Events.\n      properties:\n        event_id:\n          type: string\n          description: Unique identifier for this event instance.\n        event:\n          type: object\n          description: The event payload.\n        recipient_client_id:\n          type: string\n          description: The client ID of the registered integration.\n    DatasetIngestionPayload:\n      type: object\n      properties:\n        event_id:\n          type: string\n        event:\n\
  \          type: object\n          properties:\n            body:\n              type: object\n              properties:\n                datasetId:\n                  type: string\n                batchId:\n                  type: string\n                status:\n                  type: string\n                  enum:\n                  - success\n                  - failed\n                recordCount:\n                  type: integer\n                completedAt:\n                  type: string\n                  format: date-time\n            header:\n              type: object\n              properties:\n                eventType:\n                  type: string\n                imsOrgId:\n                  type: string\n                source:\n                  type: string\n    ProfileUpdatePayload:\n      type: object\n      properties:\n        event_id:\n          type: string\n        event:\n          type: object\n          properties:\n            body:\n              type:\
  \ object\n              properties:\n                identityMap:\n                  type: object\n                changeType:\n                  type: string\n                  enum:\n                  - created\n                  - updated\n                modifiedAt:\n                  type: string\n                  format: date-time\n            header:\n              type: object\n              properties:\n                eventType:\n                  type: string\n                imsOrgId:\n                  type: string\n    SegmentEvaluationPayload:\n      type: object\n      properties:\n        event_id:\n          type: string\n        event:\n          type: object\n          properties:\n            body:\n              type: object\n              properties:\n                segmentId:\n                  type: string\n                jobId:\n                  type: string\n                status:\n                  type: string\n                  enum:\n               \
  \   - succeeded\n                  - failed\n                profileCount:\n                  type: integer\n                completedAt:\n                  type: string\n                  format: date-time\n            header:\n              type: object\n              properties:\n                eventType:\n                  type: string\n    ReportSuiteChangePayload:\n      type: object\n      properties:\n        event_id:\n          type: string\n        event:\n          type: object\n          properties:\n            body:\n              type: object\n              properties:\n                rsid:\n                  type: string\n                changeType:\n                  type: string\n                changedBy:\n                  type: string\n                changedAt:\n                  type: string\n                  format: date-time\n            header:\n              type: object\n              properties:\n                eventType:\n                  type: string\n\
  \    DeliveryStatusPayload:\n      type: object\n      properties:\n        event_id:\n          type: string\n        event:\n          type: object\n          properties:\n            body:\n              type: object\n              properties:\n                deliveryId:\n                  type: string\n                recipientEmail:\n                  type: string\n                status:\n                  type: string\n                  enum:\n                  - sent\n                  - delivered\n                  - bounced\n                  - opened\n                  - clicked\n                timestamp:\n                  type: string\n                  format: date-time\n            header:\n              type: object\n              properties:\n                eventType:\n                  type: string\n    WorkflowExecutionPayload:\n      type: object\n      properties:\n        event_id:\n          type: string\n        event:\n          type: object\n          properties:\n\
  \            body:\n              type: object\n              properties:\n                workflowId:\n                  type: string\n                executionStatus:\n                  type: string\n                  enum:\n                  - started\n                  - completed\n                  - failed\n                  - paused\n                errorMessage:\n                  type: string\n                timestamp:\n                  type: string\n                  format: date-time\n            header:\n              type: object\n              properties:\n                eventType:\n                  type: string\n    ActivityStateChangePayload:\n      type: object\n      properties:\n        event_id:\n          type: string\n        event:\n          type: object\n          properties:\n            body:\n              type: object\n              properties:\n                activityId:\n                  type: integer\n                activityName:\n               \
  \   type: string\n                previousState:\n                  type: string\n                newState:\n                  type: string\n                changedAt:\n                  type: string\n                  format: date-time\n            header:\n              type: object\n              properties:\n                eventType:\n                  type: string\n    JourneyStepPayload:\n      type: object\n      properties:\n        event_id:\n          type: string\n        event:\n          type: object\n          properties:\n            body:\n              type: object\n              properties:\n                journeyId:\n                  type: string\n                journeyVersionId:\n                  type: string\n                stepId:\n                  type: string\n                profileId:\n                  type: string\n                stepStatus:\n                  type: string\n                  enum:\n                  - entered\n                  - completed\n\
  \                  - timedOut\n                  - error\n                timestamp:\n                  type: string\n                  format: date-time\n            header:\n              type: object\n              properties:\n                eventType:\n                  type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/adobe-experience-cloud/refs/heads/main/asyncapi/adobe-io-events-asyncapi.yml
spec_file: asyncapi/adobe-io-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/adobe-experience-cloud/refs/heads/main/asyncapi/adobe-io-events-asyncapi.yml
tags:
- Analytics
- Customer Experience
- Digital Marketing
- Personalization
- Campaign Management
- Journey Orchestration
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
