---
api_specs:
- filename: resources_list.htm
  format: yaml
  label: Salesforce Service Cloud REST API
  slug: ''
  spec_type: OpenAPI
  url: https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_list.htm
- filename: salesforce-streaming-api-asyncapi.yml
  format: yaml
  label: Service Cloud Streaming API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-service-cloud/refs/heads/main/asyncapi/salesforce-streaming-api-asyncapi.yml
- filename: salesforce-live-agent-openapi.yml
  format: yaml
  label: Live Agent REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-service-cloud/refs/heads/main/openapi/salesforce-live-agent-openapi.yml
channels:
- description: PushTopic channel for receiving notifications when sObject records matching a SOQL query are created, updated, deleted, or undeleted.
  name: /topic/{pushTopicName}
  operation: subscribe
  operation_id: receivePushTopicEvent
  summary: Receive PushTopic notifications
- description: Platform Event channel for receiving custom event messages published by Apex, Flow, or API triggers in the service cloud context.
  name: /event/{platformEventName}__e
  operation: subscribe
  operation_id: receivePlatformEvent
  summary: Receive Platform Event notifications
- description: Change Data Capture channel for tracking field-level changes to Case records in real-time.
  name: /data/CaseChangeEvent
  operation: subscribe
  operation_id: receiveCaseChangeEvent
  summary: Receive Case change events
description: Real-time event streaming API for Salesforce Service Cloud using the Bayeux protocol over CometD. Supports PushTopic events for sObject changes, Platform Events for custom event-driven architectures, and Change Data Capture events for tracking field-level changes to service cloud records.
layout: asyncapi
messages:
- description: ''
  name: PushTopicEvent
  summary: Notification triggered when an sObject record matching the PushTopic SOQL query is created, updated, deleted, or undeleted.
  title: PushTopic Event Notification
- description: ''
  name: PlatformEvent
  summary: Custom event message published through the Salesforce Platform Events framework.
  title: Platform Event Message
- description: ''
  name: ChangeDataCaptureEvent
  summary: Event containing field-level change details for a modified sObject record.
  title: Change Data Capture Event
name: Salesforce Service Cloud Streaming API
provider_name: Salesforce Service Cloud
provider_slug: salesforce-service-cloud
servers:
- description: Salesforce CometD streaming endpoint
  name: production
  protocol: https
  url: https://{instance}.salesforce.com/cometd/59.0
slug: salesforce-streaming-api-asyncapi
source_filename: salesforce-streaming-api-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Salesforce Service Cloud Streaming API\n  description: >-\n    Real-time event streaming API for Salesforce Service Cloud using the\n    Bayeux protocol over CometD. Supports PushTopic events for sObject\n    changes, Platform Events for custom event-driven architectures, and\n    Change Data Capture events for tracking field-level changes to\n    service cloud records.\n  version: '59.0'\n  contact:\n    name: Salesforce Developer Support\n    url: https://developer.salesforce.com/support\n  license:\n    name: Salesforce Master Subscription Agreement\n    url: https://www.salesforce.com/company/legal/agreements/\nservers:\n  production:\n    url: https://{instance}.salesforce.com/cometd/59.0\n    protocol: https\n    description: Salesforce CometD streaming endpoint\n    security:\n      - oauth2: []\n    variables:\n      instance:\n        default: yourInstance\n        description: Your Salesforce instance identifier\nchannels:\n  /topic/{pushTopicName}:\n\
  \    description: >-\n      PushTopic channel for receiving notifications when sObject records\n      matching a SOQL query are created, updated, deleted, or undeleted.\n    parameters:\n      pushTopicName:\n        description: Name of the PushTopic record defining the SOQL query\n        schema:\n          type: string\n    subscribe:\n      operationId: receivePushTopicEvent\n      summary: Receive PushTopic notifications\n      description: >-\n        Subscribe to receive real-time notifications when Case, Contact,\n        Account, or other service cloud sObject records are modified.\n      message:\n        $ref: '#/components/messages/PushTopicEvent'\n  /event/{platformEventName}__e:\n    description: >-\n      Platform Event channel for receiving custom event messages published\n      by Apex, Flow, or API triggers in the service cloud context.\n    parameters:\n      platformEventName:\n        description: API name of the Platform Event definition\n        schema:\n       \
  \   type: string\n    subscribe:\n      operationId: receivePlatformEvent\n      summary: Receive Platform Event notifications\n      description: >-\n        Subscribe to custom platform events such as service case\n        escalations, SLA breach notifications, or agent assignment\n        changes.\n      message:\n        $ref: '#/components/messages/PlatformEvent'\n  /data/CaseChangeEvent:\n    description: >-\n      Change Data Capture channel for tracking field-level changes to\n      Case records in real-time.\n    subscribe:\n      operationId: receiveCaseChangeEvent\n      summary: Receive Case change events\n      description: >-\n        Subscribe to receive notifications whenever a Case record is\n        created, updated, deleted, or undeleted, including the specific\n        fields that changed.\n      message:\n        $ref: '#/components/messages/ChangeDataCaptureEvent'\ncomponents:\n  securitySchemes:\n    oauth2:\n      type: oauth2\n      flows:\n        authorizationCode:\n\
  \          authorizationUrl: https://login.salesforce.com/services/oauth2/authorize\n          tokenUrl: https://login.salesforce.com/services/oauth2/token\n          scopes:\n            streaming: Access Streaming API\n  messages:\n    PushTopicEvent:\n      name: PushTopicEvent\n      title: PushTopic Event Notification\n      summary: >-\n        Notification triggered when an sObject record matching the\n        PushTopic SOQL query is created, updated, deleted, or undeleted.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PushTopicPayload'\n    PlatformEvent:\n      name: PlatformEvent\n      title: Platform Event Message\n      summary: >-\n        Custom event message published through the Salesforce Platform\n        Events framework.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PlatformEventPayload'\n    ChangeDataCaptureEvent:\n      name: ChangeDataCaptureEvent\n      title: Change Data Capture\
  \ Event\n      summary: >-\n        Event containing field-level change details for a modified\n        sObject record.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ChangeEventPayload'\n  schemas:\n    PushTopicPayload:\n      type: object\n      properties:\n        channel:\n          type: string\n          description: The channel the event was received on\n        data:\n          type: object\n          properties:\n            event:\n              type: object\n              properties:\n                type:\n                  type: string\n                  description: Type of change\n                  enum:\n                    - created\n                    - updated\n                    - deleted\n                    - undeleted\n                createdDate:\n                  type: string\n                  format: date-time\n                  description: Timestamp of the event\n                replayId:\n                  type:\
  \ integer\n                  description: Replay ID for event replay\n            sobject:\n              type: object\n              description: The sObject record data matching the PushTopic query\n              properties:\n                Id:\n                  type: string\n                  description: Record ID\n    PlatformEventPayload:\n      type: object\n      properties:\n        channel:\n          type: string\n          description: The platform event channel\n        data:\n          type: object\n          properties:\n            schema:\n              type: string\n              description: Schema ID of the event definition\n            payload:\n              type: object\n              description: Custom event payload fields\n            event:\n              type: object\n              properties:\n                replayId:\n                  type: integer\n                  description: Replay ID for event replay\n    ChangeEventPayload:\n      type: object\n\
  \      properties:\n        channel:\n          type: string\n          description: The Change Data Capture channel\n        data:\n          type: object\n          properties:\n            schema:\n              type: string\n              description: Schema ID\n            payload:\n              type: object\n              properties:\n                ChangeEventHeader:\n                  type: object\n                  properties:\n                    entityName:\n                      type: string\n                      description: sObject type name\n                    recordIds:\n                      type: array\n                      items:\n                        type: string\n                      description: IDs of changed records\n                    changeType:\n                      type: string\n                      description: Type of change\n                      enum:\n                        - CREATE\n                        - UPDATE\n                      \
  \  - DELETE\n                        - UNDELETE\n                    changedFields:\n                      type: array\n                      items:\n                        type: string\n                      description: List of fields that changed\n                    commitTimestamp:\n                      type: integer\n                      description: Commit timestamp in epoch milliseconds\n                    commitUser:\n                      type: string\n                      description: User ID who made the change\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesforce-service-cloud/refs/heads/main/asyncapi/salesforce-streaming-api-asyncapi.yml
spec_file: asyncapi/salesforce-streaming-api-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/salesforce-service-cloud/refs/heads/main/asyncapi/salesforce-streaming-api-asyncapi.yml
tags:
- Case Management
- CRM
- Customer Service
- Help Desk
- Support
- Ticketing
- AsyncAPI
- Webhooks
- Events
version: '59.0'
---
