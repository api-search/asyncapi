---
channels:
- description: Triggered when a new version of an item is added in Data Management (Autodesk Docs, BIM 360 Docs, Fusion Team).
  name: /data-management/version-added
  operation: subscribe
  operation_id: onVersionAdded
  summary: Version Added
- description: Triggered when a version of an item is deleted.
  name: /data-management/version-deleted
  operation: subscribe
  operation_id: onVersionDeleted
  summary: Version Deleted
- description: Triggered when a version is modified (renamed, moved).
  name: /data-management/version-modified
  operation: subscribe
  operation_id: onVersionModified
  summary: Version Modified
- description: Triggered when a version is copied.
  name: /data-management/version-copied
  operation: subscribe
  operation_id: onVersionCopied
  summary: Version Copied
- description: Triggered when a version is moved.
  name: /data-management/version-moved
  operation: subscribe
  operation_id: onVersionMoved
  summary: Version Moved
- description: Triggered when a new folder is created.
  name: /data-management/folder-added
  operation: subscribe
  operation_id: onFolderAdded
  summary: Folder Added
- description: Triggered when a folder is modified (renamed).
  name: /data-management/folder-modified
  operation: subscribe
  operation_id: onFolderModified
  summary: Folder Modified
- description: Triggered when a folder is deleted.
  name: /data-management/folder-deleted
  operation: subscribe
  operation_id: onFolderDeleted
  summary: Folder Deleted
- description: Triggered when a folder is moved.
  name: /data-management/folder-moved
  operation: subscribe
  operation_id: onFolderMoved
  summary: Folder Moved
- description: Triggered when a folder is copied.
  name: /data-management/folder-copied
  operation: subscribe
  operation_id: onFolderCopied
  summary: Folder Copied
- description: Triggered when a Model Derivative translation job completes (either successfully or with failure).
  name: /model-derivative/extraction-finished
  operation: subscribe
  operation_id: onExtractionFinished
  summary: Extraction Finished
- description: Triggered when a Model Derivative translation job has a status update.
  name: /model-derivative/extraction-updated
  operation: subscribe
  operation_id: onExtractionUpdated
  summary: Extraction Updated
- description: Triggered when a Collaboration for Revit model is published (synced to the cloud).
  name: /c4r/model-sync-publish
  operation: subscribe
  operation_id: onC4rModelPublish
  summary: C4R Model Published
- description: Triggered when a document is locked in Autodesk Docs.
  name: /adsk-docs/item-locked
  operation: subscribe
  operation_id: onItemLocked
  summary: Item Locked
- description: Triggered when a document is unlocked in Autodesk Docs.
  name: /adsk-docs/item-unlocked
  operation: subscribe
  operation_id: onItemUnlocked
  summary: Item Unlocked
description: Event-driven API for receiving real-time notifications from Autodesk Platform Services. When subscribed via the Webhooks REST API, Autodesk sends HTTP POST callbacks to your registered URL when events occur across Data Management, Model Derivative, BIM 360, ACC, and Fusion Lifecycle systems.
layout: asyncapi
messages:
- description: ''
  name: DataManagementVersionEvent
  summary: Event payload sent when a version change occurs in Data Management.
  title: Data Management Version Event
- description: ''
  name: DataManagementFolderEvent
  summary: Event payload sent when a folder change occurs in Data Management.
  title: Data Management Folder Event
- description: ''
  name: ModelDerivativeExtractionEvent
  summary: Event payload sent when a translation job status changes.
  title: Model Derivative Extraction Event
- description: ''
  name: C4RModelEvent
  summary: Event payload sent when a C4R model is published.
  title: Collaboration for Revit Model Event
- description: ''
  name: DocsItemEvent
  summary: Event payload sent when an item is locked or unlocked in Autodesk Docs.
  title: Autodesk Docs Item Event
name: Autodesk Webhooks Events
provider_name: Autodesk
provider_slug: autodesk
servers:
- description: Your application's callback URL that receives webhook POST events from Autodesk services.
  name: production
  protocol: https
  url: '{callbackUrl}'
slug: autodesk-webhooks-asyncapi
spec_file: asyncapi/autodesk-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/autodesk/refs/heads/main/asyncapi/autodesk-webhooks-asyncapi.yml
tags:
- 3D Modeling
- Architecture
- BIM
- CAD
- Construction
- Design
- Digital Twins
- Engineering
- Manufacturing
- Media and Entertainment
- Sustainability
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
