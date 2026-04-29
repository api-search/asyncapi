---
api_specs:
- filename: salesforce-openapi.yml
  format: yaml
  label: Salesforce REST API
  slug: salesforce-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/openapi/salesforce-openapi.yml
- filename: salesforce-bulk-api-2-openapi.yml
  format: yaml
  label: Salesforce Bulk API 2.0
  slug: salesforce-bulk-api-2
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/openapi/salesforce-bulk-api-2-openapi.yml
- filename: salesforce-streaming-asyncapi.yml
  format: yaml
  label: Salesforce Streaming API
  slug: salesforce-streaming-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/asyncapi/salesforce-streaming-asyncapi.yml
- filename: salesforce-platform-events-asyncapi.yml
  format: yaml
  label: Salesforce Platform Events API
  slug: salesforce-platform-events-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/asyncapi/salesforce-platform-events-asyncapi.yml
- filename: salesforce-change-data-capture-asyncapi.yml
  format: yaml
  label: Salesforce Change Data Capture API
  slug: salesforce-change-data-capture-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/asyncapi/salesforce-change-data-capture-asyncapi.yml
- filename: salesforce-ui-api-openapi.yml
  format: yaml
  label: Salesforce UI API
  slug: salesforce-ui-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/openapi/salesforce-ui-api-openapi.yml
- filename: salesforce-marketing-cloud-rest-openapi.yml
  format: yaml
  label: Salesforce Marketing Cloud REST API
  slug: salesforce-marketing-cloud-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/openapi/salesforce-marketing-cloud-rest-openapi.yml
- filename: salesforce-openapi.yml
  format: yaml
  label: Salesforce
  slug: salesforce-salesforce
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/openapi/salesforce-openapi.yml
channels:
- description: CometD channel for subscribing to change events for a specific Salesforce standard or custom object. Delivers events when records of that type are created, updated, deleted, or undeleted.
  name: /data/{objectApiName}ChangeEvent
  operation: subscribe
  operation_id: receiveChangeEvent
  summary: Receive a record change event for a specific object
- description: Omnibus channel that delivers change events for all objects configured for Change Data Capture in your org's settings. Use this channel to receive all CDC events in a single subscription.
  name: /data/ChangeEvents
  operation: subscribe
  operation_id: receiveAllChangeEvents
  summary: Receive change events for all CDC-enabled objects
description: Salesforce Change Data Capture (CDC) delivers change events that represent changes to Salesforce records including creates, updates, deletes, and undeletes. Subscribers receive rich change events with header metadata, changed fields, and entity metadata. Change events are durable and retained for 72 hours. CDC enables near-real-time data replication and synchronization of Salesforce data to external systems.
layout: asyncapi
messages:
- description: ''
  name: ChangeEventMessage
  summary: A record change notification for a Salesforce object
  title: Salesforce Change Data Capture Event
name: Salesforce Change Data Capture API
provider_name: Salesforce
provider_slug: salesforce
servers:
- description: CometD endpoint for subscribing to Change Data Capture events
  name: salesforce-cometd
  protocol: https
  url: https://{instanceName}.salesforce.com/cometd/{apiVersion}
slug: salesforce-change-data-capture-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Salesforce Change Data Capture API\n  description: >-\n    Salesforce Change Data Capture (CDC) delivers change events that represent\n    changes to Salesforce records including creates, updates, deletes, and\n    undeletes. Subscribers receive rich change events with header metadata,\n    changed fields, and entity metadata. Change events are durable and retained\n    for 72 hours. CDC enables near-real-time data replication and synchronization\n    of Salesforce data to external systems.\n  version: '59.0'\n  contact:\n    name: Salesforce Developer Support\n    url: https://developer.salesforce.com/docs/atlas.en-us.change_data_capture.meta/change_data_capture/\n  termsOfService: https://www.salesforce.com/company/legal/agreements/\nservers:\n  salesforce-cometd:\n    url: 'https://{instanceName}.salesforce.com/cometd/{apiVersion}'\n    protocol: https\n    description: CometD endpoint for subscribing to Change Data Capture events\n    variables:\n\
  \      instanceName:\n        description: Salesforce org instance name or custom domain\n        default: myorg\n      apiVersion:\n        description: Salesforce API version\n        default: '59.0'\n    security:\n      - oauthAccessToken: []\nchannels:\n  /data/{objectApiName}ChangeEvent:\n    description: >-\n      CometD channel for subscribing to change events for a specific Salesforce\n      standard or custom object. Delivers events when records of that type are\n      created, updated, deleted, or undeleted.\n    parameters:\n      objectApiName:\n        description: >-\n          The API name of the Salesforce object (without __c suffix for custom objects\n          in the channel path). Standard objects use their standard name.\n          Examples: Account, Contact, MyCustomObject__c becomes MyCustomObject__cChangeEvent.\n        schema:\n          type: string\n          examples:\n            - Account\n            - Contact\n            - Opportunity\n            - MyCustomObject__c\n\
  \    subscribe:\n      operationId: receiveChangeEvent\n      summary: Receive a record change event for a specific object\n      description: >-\n        Fired when a record of this Salesforce object type is created, updated,\n        deleted, or undeleted. The change event includes only the fields that\n        changed (for updates), plus header metadata about the change operation.\n      message:\n        $ref: '#/components/messages/ChangeEventMessage'\n  /data/ChangeEvents:\n    description: >-\n      Omnibus channel that delivers change events for all objects configured\n      for Change Data Capture in your org's settings. Use this channel to\n      receive all CDC events in a single subscription.\n    subscribe:\n      operationId: receiveAllChangeEvents\n      summary: Receive change events for all CDC-enabled objects\n      description: >-\n        Delivers change events for every object type enabled for Change Data\n        Capture in Salesforce Setup > Integrations > Change\
  \ Data Capture.\n      message:\n        $ref: '#/components/messages/ChangeEventMessage'\ncomponents:\n  securitySchemes:\n    oauthAccessToken:\n      type: oauth2\n      description: Salesforce OAuth 2.0 Connected App access token\n      flows:\n        authorizationCode:\n          authorizationUrl: https://login.salesforce.com/services/oauth2/authorize\n          tokenUrl: https://login.salesforce.com/services/oauth2/token\n          scopes:\n            api: Access and manage Salesforce data\n            cdp_api: Subscribe to Change Data Capture events\n  messages:\n    ChangeEventMessage:\n      name: ChangeEventMessage\n      title: Salesforce Change Data Capture Event\n      summary: A record change notification for a Salesforce object\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ChangeEventEnvelope'\n  schemas:\n    ChangeEventEnvelope:\n      type: object\n      description: The CometD envelope wrapping a Change Data Capture event\n\
  \      properties:\n        channel:\n          type: string\n          description: The CometD channel this event was delivered on\n          examples:\n            - /data/AccountChangeEvent\n            - /data/ChangeEvents\n        data:\n          type: object\n          description: Event data container\n          properties:\n            schema:\n              type: string\n              description: Avro schema ID identifying the event schema version\n            event:\n              type: object\n              properties:\n                replayId:\n                  type: integer\n                  description: >-\n                    Durable replay ID used to replay missed events. Pass -1 to\n                    replay from earliest available, -2 for new events only.\n            payload:\n              $ref: '#/components/schemas/ChangeEventPayload'\n    ChangeEventPayload:\n      type: object\n      description: The change event payload with header metadata and changed field\
  \ values\n      properties:\n        ChangeEventHeader:\n          $ref: '#/components/schemas/ChangeEventHeader'\n        Id:\n          type: string\n          description: >-\n            For create and undelete events, the Salesforce record ID.\n            Absent for update and delete events (use recordIds in the header).\n        CreatedDate:\n          type: string\n          format: date-time\n          description: Timestamp for create events\n        LastModifiedDate:\n          type: string\n          format: date-time\n          description: Timestamp for update events\n      additionalProperties:\n        description: Changed field values. Only fields that changed are included for updates.\n    ChangeEventHeader:\n      type: object\n      description: Metadata about the change event\n      required:\n        - entityName\n        - recordIds\n        - changeType\n        - changeOrigin\n        - transactionKey\n        - sequenceNumber\n        - commitTimestamp\n     \
  \   - commitUser\n        - commitNumber\n      properties:\n        entityName:\n          type: string\n          description: The API name of the Salesforce object that changed\n          examples:\n            - Account\n            - Contact\n        recordIds:\n          type: array\n          description: >-\n            Array of record IDs affected by this change event. Multiple IDs\n            indicate a mass update or delete operation.\n          items:\n            type: string\n        changeType:\n          type: string\n          description: The DML operation that caused the change\n          enum:\n            - CREATE\n            - UPDATE\n            - DELETE\n            - UNDELETE\n            - GAP_CREATE\n            - GAP_UPDATE\n            - GAP_DELETE\n            - GAP_UNDELETE\n            - GAP_OVERFLOW\n        changeOrigin:\n          type: string\n          description: >-\n            The Salesforce client that initiated the change (e.g., com/salesforce/api/rest/59.0)\n\
  \        transactionKey:\n          type: string\n          description: Unique key identifying the transaction that caused this event\n        sequenceNumber:\n          type: integer\n          description: Sequence number within the transaction for ordering multiple changes\n        commitTimestamp:\n          type: integer\n          description: Unix timestamp in milliseconds when the transaction was committed\n        commitUser:\n          type: string\n          description: Salesforce user ID of the user who made the change\n        commitNumber:\n          type: integer\n          description: Transaction commit number for ordering across transactions\n        nulledFields:\n          type: array\n          description: List of field API names that were explicitly set to null in this update\n          items:\n            type: string\n        diffFields:\n          type: array\n          description: List of field API names that changed in this update\n          items:\n    \
  \        type: string\n        changedFields:\n          type: array\n          description: Compound field names that changed\n          items:\n            type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/asyncapi/salesforce-change-data-capture-asyncapi.yml
spec_file: asyncapi/salesforce-change-data-capture-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/salesforce/refs/heads/main/asyncapi/salesforce-change-data-capture-asyncapi.yml
tags:
- AI
- Analytics
- Cloud
- Commerce
- CRM
- Customer Service
- Enterprise
- Marketing
- Platform
- Sales
- AsyncAPI
- Webhooks
- Events
version: '59.0'
---
