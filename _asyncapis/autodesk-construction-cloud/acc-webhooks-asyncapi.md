---
channels:
- description: Events for construction issue lifecycle changes
  name: issues
  operation: subscribe
  operation_id: onIssueEvent
  summary: Issue lifecycle event
- description: Events for document management in BIM 360 Docs / ACC Docs
  name: data.management
  operation: subscribe
  operation_id: onDocumentEvent
  summary: Document management event
- description: Events for RFI lifecycle
  name: rfis
  operation: subscribe
  operation_id: onRfiEvent
  summary: RFI event
- description: Events for submittal workflow changes
  name: submittals
  operation: subscribe
  operation_id: onSubmittalEvent
  summary: Submittal event
description: Autodesk Construction Cloud (ACC) and APS Webhooks deliver event notifications for project activities including issue creation, document updates, RFI changes, submittal status changes, and model coordination events. Webhooks are registered via the APS Webhooks API and delivered via HTTPS POST.
layout: asyncapi
messages:
- description: ''
  name: IssueEvent
  summary: ACC issue lifecycle event notification
  title: Issue Event
- description: ''
  name: DocumentEvent
  summary: ACC document lifecycle event notification
  title: Document Event
- description: ''
  name: RfiEvent
  summary: ACC RFI lifecycle event notification
  title: RFI Event
- description: ''
  name: SubmittalEvent
  summary: ACC submittal lifecycle event notification
  title: Submittal Event
name: Autodesk Construction Cloud Webhooks
provider_name: Autodesk Construction Cloud
provider_slug: autodesk-construction-cloud
servers:
- description: Your registered HTTPS webhook endpoint. Register this URL via the APS Webhooks API at https://developer.api.autodesk.com/webhooks/v1/systems/
  name: webhookEndpoint
  protocol: https
  url: https://your-server.example.com/webhooks/acc
slug: acc-webhooks-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Autodesk Construction Cloud Webhooks\n  description: >-\n    Autodesk Construction Cloud (ACC) and APS Webhooks deliver event notifications\n    for project activities including issue creation, document updates, RFI changes,\n    submittal status changes, and model coordination events. Webhooks are registered\n    via the APS Webhooks API and delivered via HTTPS POST.\n  version: 1.0.0\n  contact:\n    name: Autodesk Platform Services\n    url: https://aps.autodesk.com/\n\nservers:\n  webhookEndpoint:\n    url: https://your-server.example.com/webhooks/acc\n    protocol: https\n    description: >-\n      Your registered HTTPS webhook endpoint. Register this URL via the\n      APS Webhooks API at https://developer.api.autodesk.com/webhooks/v1/systems/\n\nchannels:\n  issues:\n    description: Events for construction issue lifecycle changes\n    subscribe:\n      operationId: onIssueEvent\n      summary: Issue lifecycle event\n      description:\
  \ Received when an issue is created, updated, or closed.\n      tags:\n        - name: Issues\n      message:\n        $ref: '#/components/messages/IssueEvent'\n\n  data.management:\n    description: Events for document management in BIM 360 Docs / ACC Docs\n    subscribe:\n      operationId: onDocumentEvent\n      summary: Document management event\n      description: Received when a document is uploaded, updated, or approved in ACC Docs.\n      tags:\n        - name: Documents\n      message:\n        $ref: '#/components/messages/DocumentEvent'\n\n  rfis:\n    description: Events for RFI lifecycle\n    subscribe:\n      operationId: onRfiEvent\n      summary: RFI event\n      description: Received when an RFI is created, responded to, or closed.\n      tags:\n        - name: RFIs\n      message:\n        $ref: '#/components/messages/RfiEvent'\n\n  submittals:\n    description: Events for submittal workflow changes\n    subscribe:\n      operationId: onSubmittalEvent\n      summary: Submittal\
  \ event\n      description: Received when a submittal item changes status or is reviewed.\n      tags:\n        - name: Submittals\n      message:\n        $ref: '#/components/messages/SubmittalEvent'\n\ncomponents:\n  messages:\n    IssueEvent:\n      name: IssueEvent\n      title: Issue Event\n      summary: ACC issue lifecycle event notification\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          x-adsk-signature:\n            type: string\n            description: HMAC-SHA256 signature for webhook authenticity verification\n      payload:\n        $ref: '#/components/schemas/IssueEventPayload'\n\n    DocumentEvent:\n      name: DocumentEvent\n      title: Document Event\n      summary: ACC document lifecycle event notification\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          x-adsk-signature:\n            type: string\n      payload:\n        $ref: '#/components/schemas/DocumentEventPayload'\n\
  \n    RfiEvent:\n      name: RfiEvent\n      title: RFI Event\n      summary: ACC RFI lifecycle event notification\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/RfiEventPayload'\n\n    SubmittalEvent:\n      name: SubmittalEvent\n      title: Submittal Event\n      summary: ACC submittal lifecycle event notification\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SubmittalEventPayload'\n\n  schemas:\n    WebhookEnvelope:\n      type: object\n      required: [id, type, timestamp, projectId, accountId]\n      properties:\n        id:\n          type: string\n          description: Unique webhook event ID\n        type:\n          type: string\n          description: Event type identifier\n        timestamp:\n          type: string\n          format: date-time\n        projectId:\n          type: string\n        accountId:\n          type: string\n        hookId:\n          type: string\n          description:\
  \ Webhook registration ID that triggered this event\n\n    IssueEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEnvelope'\n        - type: object\n          properties:\n            type:\n              type: string\n              enum:\n                - \"autodesk.construction.quality:issue.create-1.0\"\n                - \"autodesk.construction.quality:issue.update-1.0\"\n                - \"autodesk.construction.quality:issue.close-1.0\"\n            payload:\n              type: object\n              properties:\n                issueId:\n                  type: string\n                containerId:\n                  type: string\n                title:\n                  type: string\n                status:\n                  type: string\n                  enum: [draft, open, pending, in_review, closed]\n                previousStatus:\n                  type: string\n                updatedBy:\n                  type: string\n\n    DocumentEventPayload:\n\
  \      allOf:\n        - $ref: '#/components/schemas/WebhookEnvelope'\n        - type: object\n          properties:\n            type:\n              type: string\n              enum:\n                - \"autodesk.data:dm.version.added-1.0\"\n                - \"autodesk.data:dm.version.modified-1.0\"\n                - \"autodesk.data:dm.version.deleted-1.0\"\n            payload:\n              type: object\n              properties:\n                urn:\n                  type: string\n                  description: APS URN of the document version\n                versionId:\n                  type: string\n                name:\n                  type: string\n                folderId:\n                  type: string\n                createdBy:\n                  type: string\n\n    RfiEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEnvelope'\n        - type: object\n          properties:\n            payload:\n              type: object\n              properties:\n\
  \                rfiId:\n                  type: string\n                displayId:\n                  type: integer\n                title:\n                  type: string\n                status:\n                  type: string\n                  enum: [draft, open, answered, closed, void]\n                previousStatus:\n                  type: string\n                updatedBy:\n                  type: string\n\n    SubmittalEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEnvelope'\n        - type: object\n          properties:\n            payload:\n              type: object\n              properties:\n                submittalId:\n                  type: string\n                displayId:\n                  type: string\n                title:\n                  type: string\n                status:\n                  type: string\n                  enum: [draft, submitted, under_review, approved, rejected, revise_resubmit]\n                previousStatus:\n\
  \                  type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/autodesk-construction-cloud/refs/heads/main/asyncapi/acc-webhooks-asyncapi.yml
spec_file: asyncapi/acc-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/autodesk-construction-cloud/refs/heads/main/asyncapi/acc-webhooks-asyncapi.yml
tags:
- Construction
- BIM
- Project Management
- AEC
- CAD
- Architecture
- Engineering
- Field Management
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
