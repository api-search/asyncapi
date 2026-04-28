---
channels:
- description: Triggered before a new document is created in a collection. Allows validation or transformation of the incoming document data.
  name: collection/beforeCreate
  operation: subscribe
  operation_id: onBeforeCreate
  summary: Before document creation hook
- description: Triggered after a new document has been successfully created in a collection.
  name: collection/afterCreate
  operation: subscribe
  operation_id: onAfterCreate
  summary: After document creation hook
- description: Triggered before a document is read from a collection. Allows modification of query parameters or access control enforcement.
  name: collection/beforeRead
  operation: subscribe
  operation_id: onBeforeRead
  summary: Before document read hook
- description: Triggered after a document has been read from a collection. Allows transformation or filtering of the returned data.
  name: collection/afterRead
  operation: subscribe
  operation_id: onAfterRead
  summary: After document read hook
- description: Triggered before a document is updated in a collection. Allows validation or transformation of the update data.
  name: collection/beforeUpdate
  operation: subscribe
  operation_id: onBeforeUpdate
  summary: Before document update hook
- description: Triggered after a document has been successfully updated in a collection.
  name: collection/afterUpdate
  operation: subscribe
  operation_id: onAfterUpdate
  summary: After document update hook
- description: Triggered before a document is deleted from a collection. Allows validation or prevention of the deletion.
  name: collection/beforeDelete
  operation: subscribe
  operation_id: onBeforeDelete
  summary: Before document deletion hook
- description: Triggered after a document has been successfully deleted from a collection.
  name: collection/afterDelete
  operation: subscribe
  operation_id: onAfterDelete
  summary: After document deletion hook
- description: Queue worker channel for processing asynchronous jobs. Worker functions registered for a topic receive jobs enqueued via the REST API or internal triggers.
  name: queue/{topic}
  operation: subscribe
  operation_id: onQueueJob
  summary: Queue worker job processing
description: Asynchronous event API for Codehooks serverless backend hooks and queue workers. Covers CRUD lifecycle hooks triggered on collection document operations and asynchronous queue worker processing for named topics.
layout: asyncapi
messages:
- description: ''
  name: DocumentEvent
  summary: Event payload containing a document from a Codehooks collection during CRUD lifecycle hooks.
  title: Document Event
- description: ''
  name: ReadEvent
  summary: Event payload containing query parameters for a read operation on a Codehooks collection.
  title: Read Event
- description: ''
  name: DocumentUpdateEvent
  summary: Event payload containing the update data and target document identifier during update hooks.
  title: Document Update Event
- description: ''
  name: DeleteEvent
  summary: Event payload containing the document identifier targeted for deletion during delete hooks.
  title: Delete Event
- description: ''
  name: QueueJobEvent
  summary: Event payload for a queued job delivered to a worker function for asynchronous processing.
  title: Queue Job Event
name: Codehooks Events API
provider_name: Codehooks
provider_slug: codehooks
servers:
- description: Codehooks serverless event endpoint
  name: production
  protocol: https
  url: https://{projectId}.api.codehooks.io/{space}
slug: codehooks-events-asyncapi
spec_file: asyncapi/codehooks-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/codehooks/refs/heads/main/asyncapi/codehooks-events-asyncapi.yml
tags:
- Backend
- Database
- Events
- Hooks
- JavaScript
- NoSQL
- Queues
- Serverless
- Webhooks
- Workers
- Workflows
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
