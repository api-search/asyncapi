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
