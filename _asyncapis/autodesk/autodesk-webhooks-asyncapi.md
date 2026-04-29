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
source_filename: autodesk-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Autodesk Webhooks Events\n  version: 1.0.0\n  description: >-\n    Event-driven API for receiving real-time notifications from Autodesk\n    Platform Services. When subscribed via the Webhooks REST API, Autodesk\n    sends HTTP POST callbacks to your registered URL when events occur across\n    Data Management, Model Derivative, BIM 360, ACC, and Fusion Lifecycle\n    systems.\n  termsOfService: >-\n    https://www.autodesk.com/company/legal-notices-trademarks/terms-of-service-autodesk360-web-services/autodesk-web-services-api-terms-of-service\n  contact:\n    name: Autodesk Platform Services\n    url: https://aps.autodesk.com\n    email: aps.help@autodesk.com\n  license:\n    name: Autodesk API Terms of Service\n    url: >-\n      https://www.autodesk.com/company/legal-notices-trademarks/terms-of-service-autodesk360-web-services/autodesk-web-services-api-terms-of-service\nservers:\n  production:\n    url: '{callbackUrl}'\n    protocol: https\n\
  \    description: >-\n      Your application's callback URL that receives webhook POST events\n      from Autodesk services.\n    variables:\n      callbackUrl:\n        description: The callback URL registered in your webhook subscription.\nchannels:\n  /data-management/version-added:\n    description: >-\n      Triggered when a new version of an item is added in Data Management\n      (Autodesk Docs, BIM 360 Docs, Fusion Team).\n    subscribe:\n      operationId: onVersionAdded\n      summary: Version Added\n      message:\n        $ref: '#/components/messages/DataManagementVersionEvent'\n  /data-management/version-deleted:\n    description: Triggered when a version of an item is deleted.\n    subscribe:\n      operationId: onVersionDeleted\n      summary: Version Deleted\n      message:\n        $ref: '#/components/messages/DataManagementVersionEvent'\n  /data-management/version-modified:\n    description: Triggered when a version is modified (renamed, moved).\n    subscribe:\n    \
  \  operationId: onVersionModified\n      summary: Version Modified\n      message:\n        $ref: '#/components/messages/DataManagementVersionEvent'\n  /data-management/version-copied:\n    description: Triggered when a version is copied.\n    subscribe:\n      operationId: onVersionCopied\n      summary: Version Copied\n      message:\n        $ref: '#/components/messages/DataManagementVersionEvent'\n  /data-management/version-moved:\n    description: Triggered when a version is moved.\n    subscribe:\n      operationId: onVersionMoved\n      summary: Version Moved\n      message:\n        $ref: '#/components/messages/DataManagementVersionEvent'\n  /data-management/folder-added:\n    description: Triggered when a new folder is created.\n    subscribe:\n      operationId: onFolderAdded\n      summary: Folder Added\n      message:\n        $ref: '#/components/messages/DataManagementFolderEvent'\n  /data-management/folder-modified:\n    description: Triggered when a folder is modified (renamed).\n\
  \    subscribe:\n      operationId: onFolderModified\n      summary: Folder Modified\n      message:\n        $ref: '#/components/messages/DataManagementFolderEvent'\n  /data-management/folder-deleted:\n    description: Triggered when a folder is deleted.\n    subscribe:\n      operationId: onFolderDeleted\n      summary: Folder Deleted\n      message:\n        $ref: '#/components/messages/DataManagementFolderEvent'\n  /data-management/folder-moved:\n    description: Triggered when a folder is moved.\n    subscribe:\n      operationId: onFolderMoved\n      summary: Folder Moved\n      message:\n        $ref: '#/components/messages/DataManagementFolderEvent'\n  /data-management/folder-copied:\n    description: Triggered when a folder is copied.\n    subscribe:\n      operationId: onFolderCopied\n      summary: Folder Copied\n      message:\n        $ref: '#/components/messages/DataManagementFolderEvent'\n  /model-derivative/extraction-finished:\n    description: >-\n      Triggered when\
  \ a Model Derivative translation job completes\n      (either successfully or with failure).\n    subscribe:\n      operationId: onExtractionFinished\n      summary: Extraction Finished\n      message:\n        $ref: '#/components/messages/ModelDerivativeExtractionEvent'\n  /model-derivative/extraction-updated:\n    description: >-\n      Triggered when a Model Derivative translation job has a status update.\n    subscribe:\n      operationId: onExtractionUpdated\n      summary: Extraction Updated\n      message:\n        $ref: '#/components/messages/ModelDerivativeExtractionEvent'\n  /c4r/model-sync-publish:\n    description: >-\n      Triggered when a Collaboration for Revit model is published\n      (synced to the cloud).\n    subscribe:\n      operationId: onC4rModelPublish\n      summary: C4R Model Published\n      message:\n        $ref: '#/components/messages/C4RModelEvent'\n  /adsk-docs/item-locked:\n    description: Triggered when a document is locked in Autodesk Docs.\n    subscribe:\n\
  \      operationId: onItemLocked\n      summary: Item Locked\n      message:\n        $ref: '#/components/messages/DocsItemEvent'\n  /adsk-docs/item-unlocked:\n    description: Triggered when a document is unlocked in Autodesk Docs.\n    subscribe:\n      operationId: onItemUnlocked\n      summary: Item Unlocked\n      message:\n        $ref: '#/components/messages/DocsItemEvent'\ncomponents:\n  messages:\n    DataManagementVersionEvent:\n      name: DataManagementVersionEvent\n      title: Data Management Version Event\n      summary: >-\n        Event payload sent when a version change occurs in Data Management.\n      headers:\n        type: object\n        properties:\n          x-adsk-signature:\n            type: string\n            description: >-\n              HMAC-SHA256 signature of the payload using your secret token\n              for verification.\n          Content-Type:\n            type: string\n            enum:\n              - application/json\n      payload:\n    \
  \    $ref: '#/components/schemas/DataManagementVersionPayload'\n    DataManagementFolderEvent:\n      name: DataManagementFolderEvent\n      title: Data Management Folder Event\n      summary: >-\n        Event payload sent when a folder change occurs in Data Management.\n      headers:\n        type: object\n        properties:\n          x-adsk-signature:\n            type: string\n            description: >-\n              HMAC-SHA256 signature of the payload.\n          Content-Type:\n            type: string\n            enum:\n              - application/json\n      payload:\n        $ref: '#/components/schemas/DataManagementFolderPayload'\n    ModelDerivativeExtractionEvent:\n      name: ModelDerivativeExtractionEvent\n      title: Model Derivative Extraction Event\n      summary: >-\n        Event payload sent when a translation job status changes.\n      headers:\n        type: object\n        properties:\n          x-adsk-signature:\n            type: string\n          Content-Type:\n\
  \            type: string\n            enum:\n              - application/json\n      payload:\n        $ref: '#/components/schemas/ModelDerivativePayload'\n    C4RModelEvent:\n      name: C4RModelEvent\n      title: Collaboration for Revit Model Event\n      summary: >-\n        Event payload sent when a C4R model is published.\n      headers:\n        type: object\n        properties:\n          x-adsk-signature:\n            type: string\n          Content-Type:\n            type: string\n            enum:\n              - application/json\n      payload:\n        $ref: '#/components/schemas/C4RPayload'\n    DocsItemEvent:\n      name: DocsItemEvent\n      title: Autodesk Docs Item Event\n      summary: >-\n        Event payload sent when an item is locked or unlocked in Autodesk Docs.\n      headers:\n        type: object\n        properties:\n          x-adsk-signature:\n            type: string\n          Content-Type:\n            type: string\n            enum:\n              -\
  \ application/json\n      payload:\n        $ref: '#/components/schemas/DocsItemPayload'\n  schemas:\n    DataManagementVersionPayload:\n      type: object\n      properties:\n        version:\n          type: string\n          description: Webhook payload version.\n        resourceUrn:\n          type: string\n          description: The URN of the affected resource.\n        hook:\n          type: object\n          properties:\n            hookId:\n              type: string\n            tenant:\n              type: string\n            callbackUrl:\n              type: string\n              format: uri\n            createdBy:\n              type: string\n            event:\n              type: string\n              description: >-\n                Event type (dm.version.added, dm.version.deleted,\n                dm.version.modified, dm.version.copied, dm.version.moved).\n            createdDate:\n              type: string\n              format: date-time\n            system:\n     \
  \         type: string\n              example: data\n            creatorType:\n              type: string\n            status:\n              type: string\n            scope:\n              type: object\n              properties:\n                folder:\n                  type: string\n            hookAttribute:\n              type: object\n              additionalProperties: true\n        payload:\n          type: object\n          properties:\n            ext:\n              type: object\n              properties:\n                type:\n                  type: string\n                version:\n                  type: string\n            project:\n              type: string\n              description: Project ID.\n            creator:\n              type: string\n              description: Creator user ID.\n            name:\n              type: string\n              description: File display name.\n            version:\n              type: integer\n              description: Version\
  \ number.\n            lineageUrn:\n              type: string\n              description: The lineage URN of the item.\n            sizeInBytes:\n              type: integer\n            ancestorUrn:\n              type: string\n            source:\n              type: string\n            createdTime:\n              type: string\n              format: date-time\n            modifiedTime:\n              type: string\n              format: date-time\n            hidden:\n              type: boolean\n            customMetadata:\n              type: object\n              additionalProperties: true\n    DataManagementFolderPayload:\n      type: object\n      properties:\n        version:\n          type: string\n        resourceUrn:\n          type: string\n        hook:\n          type: object\n          properties:\n            hookId:\n              type: string\n            tenant:\n              type: string\n            callbackUrl:\n              type: string\n              format:\
  \ uri\n            event:\n              type: string\n              description: >-\n                Event type (dm.folder.added, dm.folder.modified,\n                dm.folder.deleted, dm.folder.moved, dm.folder.copied).\n            system:\n              type: string\n        payload:\n          type: object\n          properties:\n            project:\n              type: string\n            creator:\n              type: string\n            name:\n              type: string\n              description: Folder display name.\n            parentFolderUrn:\n              type: string\n            ancestorUrn:\n              type: string\n            source:\n              type: string\n            createdTime:\n              type: string\n              format: date-time\n            modifiedTime:\n              type: string\n              format: date-time\n            hidden:\n              type: boolean\n    ModelDerivativePayload:\n      type: object\n      properties:\n        version:\n\
  \          type: string\n        resourceUrn:\n          type: string\n          description: The URN of the source design.\n        hook:\n          type: object\n          properties:\n            hookId:\n              type: string\n            tenant:\n              type: string\n            callbackUrl:\n              type: string\n              format: uri\n            event:\n              type: string\n              description: >-\n                Event type (extraction.finished, extraction.updated).\n            system:\n              type: string\n              example: derivative\n        payload:\n          type: object\n          properties:\n            status:\n              type: string\n              enum:\n                - success\n                - failed\n                - timeout\n                - inprogress\n            bubble:\n              type: object\n              description: >-\n                The manifest bubble containing derivative information.\n  \
  \            properties:\n                status:\n                  type: string\n                progress:\n                  type: string\n                success:\n                  type: string\n                hasThumbnail:\n                  type: string\n    C4RPayload:\n      type: object\n      properties:\n        version:\n          type: string\n        resourceUrn:\n          type: string\n        hook:\n          type: object\n          properties:\n            hookId:\n              type: string\n            tenant:\n              type: string\n            callbackUrl:\n              type: string\n              format: uri\n            event:\n              type: string\n              example: model.sync.publish\n            system:\n              type: string\n              example: adsk.c4r\n        payload:\n          type: object\n          properties:\n            project:\n              type: string\n            creator:\n              type: string\n            name:\n\
  \              type: string\n            ancestorUrn:\n              type: string\n    DocsItemPayload:\n      type: object\n      properties:\n        version:\n          type: string\n        resourceUrn:\n          type: string\n        hook:\n          type: object\n          properties:\n            hookId:\n              type: string\n            tenant:\n              type: string\n            callbackUrl:\n              type: string\n              format: uri\n            event:\n              type: string\n            system:\n              type: string\n              example: adsk.docs\n        payload:\n          type: object\n          properties:\n            project:\n              type: string\n            creator:\n              type: string\n            name:\n              type: string\n            lineageUrn:\n              type: string\n            lockedByUserId:\n              type: string\n            lockedTime:\n              type: string\n              format:\
  \ date-time\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/autodesk/refs/heads/main/asyncapi/autodesk-webhooks-asyncapi.yml
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
