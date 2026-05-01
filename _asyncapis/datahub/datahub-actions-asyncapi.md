---
api_specs:
- filename: datahub-openapi-openapi.yml
  format: yaml
  label: DataHub OpenAPI
  slug: datahub-openapi
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/datahub/refs/heads/main/openapi/datahub-openapi-openapi.yml
- filename: datahub-actions-asyncapi.yml
  format: yaml
  label: DataHub Actions Framework
  slug: datahub-actions-framework
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/datahub/refs/heads/main/asyncapi/datahub-actions-asyncapi.yml
channels:
- description: Kafka topic for versioned aspect changes. Emitted when any versioned aspect on the DataHub metadata graph is created, updated, or removed. Versioned aspects maintain numeric versions and are persisted in the relational database. Examples include ownership, tags, glossary terms, dataset properties, and schema metadata.
  name: MetadataChangeLog_Versioned_v1
  operation: subscribe
  operation_id: onVersionedMetadataChange
  summary: Receive versioned metadata change log events
- description: Kafka topic for time-series aspect changes. Emitted when any time-series aspect on the DataHub metadata graph is created or updated. Time-series aspects carry timestamps and are stored in search indexes. Examples include dataset profiles, data quality assertions, and usage statistics.
  name: MetadataChangeLog_Timeseries_v1
  operation: subscribe
  operation_id: onTimeseriesMetadataChange
  summary: Receive time-series metadata change log events
- description: Kafka topic for platform-level events. Contains semantic change events that represent higher-level operations on the DataHub platform, such as entity creation, tag additions, ownership changes, and glossary term assignments. The Entity Change Event is the most important platform event type and serves as a key component of the DataHub Actions Framework.
  name: PlatformEvent_v1
  operation: subscribe
  operation_id: onPlatformEvent
  summary: Receive platform events
description: Event-driven interface for responding to real-time changes in the DataHub metadata graph. The Actions Framework consumes Metadata Change Log events and Platform Events from Kafka topics, enabling seamless integration of DataHub into a broader event-based architecture. Events are emitted when any aspect on the DataHub metadata graph is changed, including creates, updates, and removals of both versioned and time-series aspects.
layout: asyncapi
messages:
- description: A metadata change log event recording a modification to an entity's aspect in the DataHub metadata graph. Contains the entity URN, entity type, change type, aspect name, new aspect value, previous aspect value, system metadata, and audit information. These events are the primary mechanism for tracki
  name: MetadataChangeLogEvent
  summary: Emitted when any aspect on the DataHub metadata graph is changed.
  title: Metadata Change Log Event
- description: An entity change event representing a semantic change in the DataHub metadata graph. Unlike raw metadata change log events, entity change events provide higher-level abstractions that describe business-meaningful operations such as tag additions, ownership assignments, and glossary term linkages.
  name: EntityChangeEvent
  summary: Semantic change event representing a meaningful operation on an entity.
  title: Entity Change Event
name: DataHub Actions Framework Events
provider_name: DataHub
provider_slug: datahub
servers:
- description: Kafka broker for consuming DataHub metadata events. The default event source used by the DataHub Actions Framework subscribes to Kafka topics that stream metadata changes and platform events from the DataHub metadata service.
  name: kafkaBroker
  protocol: kafka
  url: '{kafkaHost}:{kafkaPort}'
slug: datahub-actions-asyncapi
source_filename: datahub-actions-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: DataHub Actions Framework Events\n  description: >-\n    Event-driven interface for responding to real-time changes in the DataHub\n    metadata graph. The Actions Framework consumes Metadata Change Log events\n    and Platform Events from Kafka topics, enabling seamless integration of\n    DataHub into a broader event-based architecture. Events are emitted when\n    any aspect on the DataHub metadata graph is changed, including creates,\n    updates, and removals of both versioned and time-series aspects.\n  version: '1.4.0'\n  contact:\n    name: DataHub Project\n    url: https://datahubproject.io\n  license:\n    name: Apache License 2.0\n    url: https://github.com/datahub-project/datahub/blob/master/LICENSE\nexternalDocs:\n  description: DataHub Actions Framework Documentation\n  url: https://docs.datahub.com/docs/actions\nservers:\n  kafkaBroker:\n    url: '{kafkaHost}:{kafkaPort}'\n    protocol: kafka\n    description: >-\n      Kafka\
  \ broker for consuming DataHub metadata events. The default event\n      source used by the DataHub Actions Framework subscribes to Kafka topics\n      that stream metadata changes and platform events from the DataHub\n      metadata service.\n    variables:\n      kafkaHost:\n        default: localhost\n        description: Kafka broker hostname\n      kafkaPort:\n        default: '9092'\n        description: Kafka broker port\n    security:\n      - saslPlain: []\nchannels:\n  MetadataChangeLog_Versioned_v1:\n    description: >-\n      Kafka topic for versioned aspect changes. Emitted when any versioned\n      aspect on the DataHub metadata graph is created, updated, or removed.\n      Versioned aspects maintain numeric versions and are persisted in the\n      relational database. Examples include ownership, tags, glossary terms,\n      dataset properties, and schema metadata.\n    subscribe:\n      operationId: onVersionedMetadataChange\n      summary: Receive versioned metadata change\
  \ log events\n      description: >-\n        Subscribe to versioned metadata change events emitted when entities\n        have their versioned aspects modified. These events contain the new\n        aspect value, the previous aspect value (if applicable), the change\n        type, and audit information about who made the change and when.\n      message:\n        $ref: '#/components/messages/MetadataChangeLogEvent'\n  MetadataChangeLog_Timeseries_v1:\n    description: >-\n      Kafka topic for time-series aspect changes. Emitted when any time-series\n      aspect on the DataHub metadata graph is created or updated. Time-series\n      aspects carry timestamps and are stored in search indexes. Examples\n      include dataset profiles, data quality assertions, and usage statistics.\n    subscribe:\n      operationId: onTimeseriesMetadataChange\n      summary: Receive time-series metadata change log events\n      description: >-\n        Subscribe to time-series metadata change events emitted\
  \ when entities\n        have their time-series aspects modified. These events are useful for\n        tracking operational metadata such as profiling results, quality checks,\n        and usage patterns over time.\n      message:\n        $ref: '#/components/messages/MetadataChangeLogEvent'\n  PlatformEvent_v1:\n    description: >-\n      Kafka topic for platform-level events. Contains semantic change events\n      that represent higher-level operations on the DataHub platform, such as\n      entity creation, tag additions, ownership changes, and glossary term\n      assignments. The Entity Change Event is the most important platform event\n      type and serves as a key component of the DataHub Actions Framework.\n    subscribe:\n      operationId: onPlatformEvent\n      summary: Receive platform events\n      description: >-\n        Subscribe to platform events that represent semantic changes in the\n        DataHub metadata graph. These events provide a higher-level abstraction\n\
  \        over raw metadata changes and are useful for triggering actions based\n        on specific business-meaningful operations.\n      message:\n        $ref: '#/components/messages/EntityChangeEvent'\ncomponents:\n  securitySchemes:\n    saslPlain:\n      type: plain\n      description: >-\n        SASL/PLAIN authentication for Kafka broker connections. Configure\n        with the appropriate credentials for your Kafka deployment.\n  messages:\n    MetadataChangeLogEvent:\n      name: MetadataChangeLogEvent_v1\n      title: Metadata Change Log Event\n      summary: >-\n        Emitted when any aspect on the DataHub metadata graph is changed.\n      description: >-\n        A metadata change log event recording a modification to an entity's\n        aspect in the DataHub metadata graph. Contains the entity URN, entity\n        type, change type, aspect name, new aspect value, previous aspect\n        value, system metadata, and audit information. These events are the\n        primary\
  \ mechanism for tracking all metadata modifications in DataHub.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/MetadataChangeLogEventPayload'\n    EntityChangeEvent:\n      name: EntityChangeEvent_v1\n      title: Entity Change Event\n      summary: >-\n        Semantic change event representing a meaningful operation on an entity.\n      description: >-\n        An entity change event representing a semantic change in the DataHub\n        metadata graph. Unlike raw metadata change log events, entity change\n        events provide higher-level abstractions that describe business-meaningful\n        operations such as tag additions, ownership assignments, and glossary\n        term linkages.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EntityChangeEventPayload'\n  schemas:\n    MetadataChangeLogEventPayload:\n      type: object\n      description: >-\n        Payload of a Metadata Change Log event containing\
  \ the full details\n        of a metadata change in the DataHub graph.\n      required:\n        - entityUrn\n        - entityType\n        - changeType\n        - aspectName\n      properties:\n        entityUrn:\n          type: string\n          description: >-\n            The unique URN identifier for the entity being changed.\n          example: urn:li:dataset:(urn:li:dataPlatform:hive,SampleHiveDataset,PROD)\n        entityType:\n          type: string\n          description: >-\n            The type of the entity being changed, such as dataset, chart,\n            dashboard, dataFlow, dataJob, corpUser, corpGroup, tag, domain,\n            glossaryTerm, or glossaryNode.\n          example: dataset\n        changeType:\n          type: string\n          description: >-\n            The type of change that occurred on the aspect.\n          enum:\n            - UPSERT\n            - DELETE\n            - CREATE\n            - RESTATE\n        aspectName:\n          type: string\n\
  \          description: >-\n            The name of the entity aspect that was changed, such as\n            datasetProperties, schemaMetadata, ownership, globalTags,\n            glossaryTerms, or status.\n          example: globalTags\n        aspect:\n          $ref: '#/components/schemas/SerializedAspect'\n        previousAspectValue:\n          $ref: '#/components/schemas/SerializedAspect'\n        systemMetadata:\n          $ref: '#/components/schemas/SystemMetadata'\n        created:\n          $ref: '#/components/schemas/AuditStamp'\n    EntityChangeEventPayload:\n      type: object\n      description: >-\n        Payload of an Entity Change Event representing a semantic change\n        in the DataHub metadata graph.\n      required:\n        - entityUrn\n        - entityType\n        - category\n        - operation\n      properties:\n        entityUrn:\n          type: string\n          description: >-\n            The unique URN identifier for the entity that was changed.\n\
  \          example: urn:li:dataset:(urn:li:dataPlatform:hive,SampleHiveDataset,PROD)\n        entityType:\n          type: string\n          description: >-\n            The type of the entity that was changed.\n          example: dataset\n        category:\n          type: string\n          description: >-\n            The category of the change, representing the semantic domain\n            of the modification.\n          enum:\n            - TAG\n            - GLOSSARY_TERM\n            - OWNERSHIP\n            - TECHNICAL_SCHEMA\n            - DOCUMENTATION\n            - DOMAIN\n            - DEPRECATION\n            - LIFECYCLE\n        operation:\n          type: string\n          description: >-\n            The semantic operation that was performed.\n          enum:\n            - ADD\n            - REMOVE\n            - MODIFY\n        modifier:\n          type: string\n          description: >-\n            Additional context about the change, such as the specific tag\n    \
  \        URN or glossary term URN that was added or removed.\n          example: urn:li:tag:PII\n        parameters:\n          type: object\n          description: >-\n            Additional parameters providing context for the change event.\n          additionalProperties:\n            type: string\n        auditStamp:\n          $ref: '#/components/schemas/AuditStamp'\n    SerializedAspect:\n      type: object\n      description: >-\n        A serialized aspect value containing the content type and the\n        JSON-encoded aspect payload.\n      properties:\n        contentType:\n          type: string\n          description: >-\n            The content type of the serialized aspect value.\n          example: application/json\n        value:\n          type: string\n          description: >-\n            The JSON-serialized aspect value following the PDL schema\n            definition for the given aspect name.\n    SystemMetadata:\n      type: object\n      description: >-\n     \
  \   System-level metadata associated with a metadata change, providing\n        provenance and tracking information.\n      properties:\n        runId:\n          type: string\n          description: >-\n            The identifier of the ingestion run that produced this change.\n        lastObserved:\n          type: integer\n          format: int64\n          description: >-\n            The timestamp when this metadata was last observed in epoch\n            milliseconds.\n        registryName:\n          type: string\n          description: >-\n            The name of the model registry associated with this change.\n        registryVersion:\n          type: string\n          description: >-\n            The version of the model registry.\n    AuditStamp:\n      type: object\n      description: >-\n        An audit stamp recording who made a change and when.\n      properties:\n        time:\n          type: integer\n          format: int64\n          description: >-\n            The\
  \ timestamp of the change in epoch milliseconds.\n        actor:\n          type: string\n          description: >-\n            The URN of the actor who made the change.\n          example: urn:li:corpuser:datahub\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/datahub/refs/heads/main/asyncapi/datahub-actions-asyncapi.yml
spec_file: asyncapi/datahub-actions-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/datahub/refs/heads/main/asyncapi/datahub-actions-asyncapi.yml
tags:
- Data Catalog
- Data Discovery
- Data Governance
- Data Lineage
- Metadata
- AsyncAPI
- Webhooks
- Events
version: 1.4.0
---
