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
