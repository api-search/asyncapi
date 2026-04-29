---
api_specs:
- filename: codehooks-database-rest-api-openapi.yml
  format: yaml
  label: Codehooks Database REST API
  slug: codehooks-database-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/codehooks/refs/heads/main/openapi/codehooks-database-rest-api-openapi.yml
- filename: codehooks-events-asyncapi.yml
  format: yaml
  label: Codehooks Events (AsyncAPI)
  slug: codehooks-events
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/codehooks/refs/heads/main/asyncapi/codehooks-events-asyncapi.yml
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
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Codehooks Events API\n  version: 1.0.0\n  description: >-\n    Asynchronous event API for Codehooks serverless backend hooks and queue\n    workers. Covers CRUD lifecycle hooks triggered on collection document\n    operations and asynchronous queue worker processing for named topics.\n  contact:\n    name: Codehooks\n    url: https://codehooks.io/\n  license:\n    name: Proprietary\n    url: https://codehooks.io/terms\n\nservers:\n  production:\n    url: https://{projectId}.api.codehooks.io/{space}\n    protocol: https\n    description: Codehooks serverless event endpoint\n    variables:\n      projectId:\n        default: myproject-ff00\n        description: The project ID assigned to your Codehooks project\n      space:\n        default: dev\n        description: The datastore space name (e.g. dev, staging, prod)\n\nchannels:\n  collection/beforeCreate:\n    description: >-\n      Triggered before a new document is created in a collection.\
  \ Allows\n      validation or transformation of the incoming document data.\n    subscribe:\n      operationId: onBeforeCreate\n      summary: Before document creation hook\n      message:\n        $ref: '#/components/messages/DocumentEvent'\n\n  collection/afterCreate:\n    description: >-\n      Triggered after a new document has been successfully created in a\n      collection.\n    subscribe:\n      operationId: onAfterCreate\n      summary: After document creation hook\n      message:\n        $ref: '#/components/messages/DocumentEvent'\n\n  collection/beforeRead:\n    description: >-\n      Triggered before a document is read from a collection. Allows\n      modification of query parameters or access control enforcement.\n    subscribe:\n      operationId: onBeforeRead\n      summary: Before document read hook\n      message:\n        $ref: '#/components/messages/ReadEvent'\n\n  collection/afterRead:\n    description: >-\n      Triggered after a document has been read from a collection.\
  \ Allows\n      transformation or filtering of the returned data.\n    subscribe:\n      operationId: onAfterRead\n      summary: After document read hook\n      message:\n        $ref: '#/components/messages/DocumentEvent'\n\n  collection/beforeUpdate:\n    description: >-\n      Triggered before a document is updated in a collection. Allows\n      validation or transformation of the update data.\n    subscribe:\n      operationId: onBeforeUpdate\n      summary: Before document update hook\n      message:\n        $ref: '#/components/messages/DocumentUpdateEvent'\n\n  collection/afterUpdate:\n    description: >-\n      Triggered after a document has been successfully updated in a collection.\n    subscribe:\n      operationId: onAfterUpdate\n      summary: After document update hook\n      message:\n        $ref: '#/components/messages/DocumentEvent'\n\n  collection/beforeDelete:\n    description: >-\n      Triggered before a document is deleted from a collection. Allows\n      validation\
  \ or prevention of the deletion.\n    subscribe:\n      operationId: onBeforeDelete\n      summary: Before document deletion hook\n      message:\n        $ref: '#/components/messages/DeleteEvent'\n\n  collection/afterDelete:\n    description: >-\n      Triggered after a document has been successfully deleted from a\n      collection.\n    subscribe:\n      operationId: onAfterDelete\n      summary: After document deletion hook\n      message:\n        $ref: '#/components/messages/DeleteEvent'\n\n  queue/{topic}:\n    description: >-\n      Queue worker channel for processing asynchronous jobs. Worker functions\n      registered for a topic receive jobs enqueued via the REST API or\n      internal triggers.\n    parameters:\n      topic:\n        description: The named queue topic\n        schema:\n          type: string\n    subscribe:\n      operationId: onQueueJob\n      summary: Queue worker job processing\n      message:\n        $ref: '#/components/messages/QueueJobEvent'\n\ncomponents:\n\
  \  messages:\n    DocumentEvent:\n      name: DocumentEvent\n      title: Document Event\n      summary: >-\n        Event payload containing a document from a Codehooks collection\n        during CRUD lifecycle hooks.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DocumentEventPayload'\n\n    ReadEvent:\n      name: ReadEvent\n      title: Read Event\n      summary: >-\n        Event payload containing query parameters for a read operation\n        on a Codehooks collection.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ReadEventPayload'\n\n    DocumentUpdateEvent:\n      name: DocumentUpdateEvent\n      title: Document Update Event\n      summary: >-\n        Event payload containing the update data and target document\n        identifier during update hooks.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DocumentUpdateEventPayload'\n\n    DeleteEvent:\n \
  \     name: DeleteEvent\n      title: Delete Event\n      summary: >-\n        Event payload containing the document identifier targeted for\n        deletion during delete hooks.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DeleteEventPayload'\n\n    QueueJobEvent:\n      name: QueueJobEvent\n      title: Queue Job Event\n      summary: >-\n        Event payload for a queued job delivered to a worker function\n        for asynchronous processing.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/QueueJobEventPayload'\n\n  schemas:\n    DocumentEventPayload:\n      type: object\n      properties:\n        collection:\n          type: string\n          description: The name of the collection the event pertains to.\n        document:\n          type: object\n          additionalProperties: true\n          description: The document data involved in the event.\n        _id:\n          type: string\n      \
  \    description: The unique identifier of the document.\n\n    ReadEventPayload:\n      type: object\n      properties:\n        collection:\n          type: string\n          description: The name of the collection being read.\n        query:\n          type: object\n          additionalProperties: true\n          description: The query parameters used for the read operation.\n        hints:\n          type: object\n          additionalProperties: true\n          description: Query hints including sort, limit, skip, and projection.\n\n    DocumentUpdateEventPayload:\n      type: object\n      properties:\n        collection:\n          type: string\n          description: The name of the collection being updated.\n        _id:\n          type: string\n          description: The unique identifier of the document being updated.\n        updateData:\n          type: object\n          additionalProperties: true\n          description: >-\n            The update data, which may include direct\
  \ field values or\n            MongoDB-like operators such as $set, $inc, $unset, $push, $pull.\n\n    DeleteEventPayload:\n      type: object\n      properties:\n        collection:\n          type: string\n          description: The name of the collection the document is being deleted from.\n        _id:\n          type: string\n          description: The unique identifier of the document being deleted.\n\n    QueueJobEventPayload:\n      type: object\n      properties:\n        _id:\n          type: string\n          description: Unique identifier of the queued job.\n        topic:\n          type: string\n          description: The queue topic name.\n        payload:\n          type: object\n          additionalProperties: true\n          description: The job payload data to be processed by the worker.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/codehooks/refs/heads/main/asyncapi/codehooks-events-asyncapi.yml
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
