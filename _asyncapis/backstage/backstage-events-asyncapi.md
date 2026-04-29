---
channels:
- description: Events emitted when catalog entities are created, updated, or deleted. These events are triggered by catalog processors and entity providers when the state of the software catalog changes.
  name: catalogEntityChange
- description: Events emitted when catalog locations are added, updated, or removed.
  name: catalogLocationChange
- description: Events emitted when a scaffolder task changes status, including creation, completion, or failure.
  name: scaffolderTaskComplete
- description: Events emitted when TechDocs documentation is built or updated.
  name: techdocsBuild
description: The Backstage Events system provides a publish-subscribe mechanism for broadcasting and consuming events within a Backstage instance. It enables plugins to emit events when significant actions occur (such as catalog entity changes, scaffolder task completions, or permission policy updates) and allows other plugins or external systems to subscribe to those events via HTTP webhooks or the internal event bus.
layout: asyncapi
messages:
- description: ''
  name: CatalogEntityChangeEvent
  summary: ''
  title: Catalog Entity Change Event
- description: ''
  name: CatalogLocationChangeEvent
  summary: ''
  title: Catalog Location Change Event
- description: ''
  name: ScaffolderTaskEvent
  summary: ''
  title: Scaffolder Task Event
- description: ''
  name: TechDocsBuildEvent
  summary: ''
  title: TechDocs Build Event
name: Backstage Events System
provider_name: Backstage
provider_slug: backstage
servers: []
slug: backstage-events-asyncapi
source_yaml: "asyncapi: 3.0.0\ninfo:\n  title: Backstage Events System\n  version: 1.0.0\n  description: >-\n    The Backstage Events system provides a publish-subscribe mechanism for\n    broadcasting and consuming events within a Backstage instance. It enables\n    plugins to emit events when significant actions occur (such as catalog\n    entity changes, scaffolder task completions, or permission policy updates)\n    and allows other plugins or external systems to subscribe to those events\n    via HTTP webhooks or the internal event bus.\n  contact:\n    name: Backstage\n    url: https://backstage.io\n  license:\n    name: Apache-2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\n  externalDocs:\n    description: Backstage Events Plugin Documentation\n    url: https://backstage.io/docs/plugins/backends-and-plugins/\ndefaultContentType: application/json\nchannels:\n  catalogEntityChange:\n    address: backstage/catalog/entity\n    description: >-\n      Events emitted when catalog\
  \ entities are created, updated, or deleted.\n      These events are triggered by catalog processors and entity providers\n      when the state of the software catalog changes.\n    messages:\n      catalogEntityChangeMessage:\n        $ref: '#/components/messages/CatalogEntityChangeEvent'\n  catalogLocationChange:\n    address: backstage/catalog/location\n    description: >-\n      Events emitted when catalog locations are added, updated, or removed.\n    messages:\n      catalogLocationChangeMessage:\n        $ref: '#/components/messages/CatalogLocationChangeEvent'\n  scaffolderTaskComplete:\n    address: backstage/scaffolder/task\n    description: >-\n      Events emitted when a scaffolder task changes status, including\n      creation, completion, or failure.\n    messages:\n      scaffolderTaskCompleteMessage:\n        $ref: '#/components/messages/ScaffolderTaskEvent'\n  techdocsBuild:\n    address: backstage/techdocs/build\n    description: >-\n      Events emitted when TechDocs\
  \ documentation is built or updated.\n    messages:\n      techdocsBuildMessage:\n        $ref: '#/components/messages/TechDocsBuildEvent'\noperations:\n  onCatalogEntityChange:\n    action: receive\n    channel:\n      $ref: '#/channels/catalogEntityChange'\n    summary: Receive catalog entity change events.\n    description: >-\n      Subscribe to notifications when catalog entities are created, updated,\n      or deleted from the software catalog.\n  onCatalogLocationChange:\n    action: receive\n    channel:\n      $ref: '#/channels/catalogLocationChange'\n    summary: Receive catalog location change events.\n  onScaffolderTaskComplete:\n    action: receive\n    channel:\n      $ref: '#/channels/scaffolderTaskComplete'\n    summary: Receive scaffolder task lifecycle events.\n  onTechDocsBuild:\n    action: receive\n    channel:\n      $ref: '#/channels/techdocsBuild'\n    summary: Receive TechDocs build events.\ncomponents:\n  messages:\n    CatalogEntityChangeEvent:\n      name: CatalogEntityChangeEvent\n\
  \      title: Catalog Entity Change Event\n      contentType: application/json\n      payload:\n        type: object\n        required:\n          - topic\n          - eventPayload\n          - metadata\n        properties:\n          topic:\n            type: string\n            const: catalog\n            description: The event topic.\n          eventPayload:\n            type: object\n            required:\n              - action\n              - entity\n            properties:\n              action:\n                type: string\n                enum:\n                  - created\n                  - updated\n                  - deleted\n                description: The action that occurred.\n              entity:\n                type: object\n                properties:\n                  apiVersion:\n                    type: string\n                  kind:\n                    type: string\n                  metadata:\n                    type: object\n                    properties:\n\
  \                      name:\n                        type: string\n                      namespace:\n                        type: string\n                      uid:\n                        type: string\n                description: The affected catalog entity.\n          metadata:\n            $ref: '#/components/schemas/EventMetadata'\n    CatalogLocationChangeEvent:\n      name: CatalogLocationChangeEvent\n      title: Catalog Location Change Event\n      contentType: application/json\n      payload:\n        type: object\n        required:\n          - topic\n          - eventPayload\n          - metadata\n        properties:\n          topic:\n            type: string\n            const: catalog\n          eventPayload:\n            type: object\n            properties:\n              action:\n                type: string\n                enum:\n                  - added\n                  - updated\n                  - removed\n              location:\n                type: object\n\
  \                properties:\n                  type:\n                    type: string\n                  target:\n                    type: string\n          metadata:\n            $ref: '#/components/schemas/EventMetadata'\n    ScaffolderTaskEvent:\n      name: ScaffolderTaskEvent\n      title: Scaffolder Task Event\n      contentType: application/json\n      payload:\n        type: object\n        required:\n          - topic\n          - eventPayload\n          - metadata\n        properties:\n          topic:\n            type: string\n            const: scaffolder\n          eventPayload:\n            type: object\n            properties:\n              action:\n                type: string\n                enum:\n                  - created\n                  - processing\n                  - completed\n                  - failed\n                  - cancelled\n              taskId:\n                type: string\n              templateRef:\n                type: string\n      \
  \          description: >-\n                  Entity reference of the template used\n                  (e.g., template:default/create-react-app).\n              createdBy:\n                type: string\n                description: Entity reference of the user who created the task.\n          metadata:\n            $ref: '#/components/schemas/EventMetadata'\n    TechDocsBuildEvent:\n      name: TechDocsBuildEvent\n      title: TechDocs Build Event\n      contentType: application/json\n      payload:\n        type: object\n        required:\n          - topic\n          - eventPayload\n          - metadata\n        properties:\n          topic:\n            type: string\n            const: techdocs\n          eventPayload:\n            type: object\n            properties:\n              action:\n                type: string\n                enum:\n                  - build_started\n                  - build_completed\n                  - build_failed\n              entityRef:\n       \
  \         type: string\n                description: >-\n                  Entity reference for the documented entity\n                  (e.g., component:default/my-service).\n              buildTimestamp:\n                type: string\n                format: date-time\n          metadata:\n            $ref: '#/components/schemas/EventMetadata'\n  schemas:\n    EventMetadata:\n      type: object\n      properties:\n        source:\n          type: string\n          description: The source plugin or system that emitted the event.\n        eventId:\n          type: string\n          format: uuid\n          description: Unique identifier for this event.\n        timestamp:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp of when the event was emitted.\n        correlationId:\n          type: string\n          description: Correlation ID for tracing related events.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/backstage/refs/heads/main/asyncapi/backstage-events-asyncapi.yml
spec_file: asyncapi/backstage-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/backstage/refs/heads/main/asyncapi/backstage-events-asyncapi.yml
tags:
- Developer Portal
- Internal Developer Platform
- Software Catalog
- Open Source
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
