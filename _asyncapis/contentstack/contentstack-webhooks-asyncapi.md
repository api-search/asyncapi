---
api_specs:
- filename: contentstack-content-delivery-api-openapi.yml
  format: yaml
  label: Contentstack Content Delivery API
  slug: content-delivery-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/contentstack/refs/heads/main/openapi/contentstack-content-delivery-api-openapi.yml
- filename: contentstack-content-management-api-openapi.yml
  format: yaml
  label: Contentstack Content Management API
  slug: content-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/contentstack/refs/heads/main/openapi/contentstack-content-management-api-openapi.yml
- filename: contentstack-personalize-management-api-openapi.yml
  format: yaml
  label: Contentstack Personalize Management API
  slug: personalize-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/contentstack/refs/heads/main/openapi/contentstack-personalize-management-api-openapi.yml
- filename: contentstack-personalize-edge-api-openapi.yml
  format: yaml
  label: Contentstack Personalize Edge API
  slug: personalize-edge-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/contentstack/refs/heads/main/openapi/contentstack-personalize-edge-api-openapi.yml
- filename: contentstack-automate-management-api-openapi.yml
  format: yaml
  label: Contentstack Automate Management API
  slug: automate-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/contentstack/refs/heads/main/openapi/contentstack-automate-management-api-openapi.yml
- filename: contentstack-analytics-api-openapi.yml
  format: yaml
  label: Contentstack Analytics API
  slug: analytics-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/contentstack/refs/heads/main/openapi/contentstack-analytics-api-openapi.yml
- filename: contentstack-scim-api-openapi.yml
  format: yaml
  label: Contentstack SCIM API
  slug: scim-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/contentstack/refs/heads/main/openapi/contentstack-scim-api-openapi.yml
- filename: contentstack-brand-kit-management-api-openapi.yml
  format: yaml
  label: Contentstack Brand Kit Management API
  slug: brand-kit-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/contentstack/refs/heads/main/openapi/contentstack-brand-kit-management-api-openapi.yml
- filename: contentstack-knowledge-vault-api-openapi.yml
  format: yaml
  label: Contentstack Knowledge Vault API
  slug: knowledge-vault-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/contentstack/refs/heads/main/openapi/contentstack-knowledge-vault-api-openapi.yml
- filename: contentstack-generative-ai-api-openapi.yml
  format: yaml
  label: Contentstack Generative AI API
  slug: generative-ai-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/contentstack/refs/heads/main/openapi/contentstack-generative-ai-api-openapi.yml
- filename: contentstack-launch-api-openapi.yml
  format: yaml
  label: Contentstack Launch API
  slug: launch-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/contentstack/refs/heads/main/openapi/contentstack-launch-api-openapi.yml
channels:
- description: Contentstack delivers all webhook event payloads via HTTP POST to this channel. Each delivery includes event metadata and the content payload relevant to the triggered action.
  name: /webhook
  operation: publish
  operation_id: receiveWebhookEvent
  summary: Receive a Contentstack webhook event
description: Contentstack Webhooks provide event-driven notifications for content lifecycle events within a stack. When configured, Contentstack sends HTTP POST requests to your specified endpoint URL whenever matching events occur, such as entries being published, assets being deleted, or workflow stages changing. Webhooks support filtering by content type, entry UID, environment, and locale. Bulk operations trigger a single webhook notification at job completion rather than one notification per item, making them efficient for static site generation and cache invalidation workflows.
layout: asyncapi
messages:
- description: Triggered when a content entry is successfully published to at least one environment. Contains the full entry data and the list of environments and locales the entry was published to.
  name: EntryPublished
  summary: An entry was published to one or more environments.
  title: Entry Published
- description: Triggered when a content entry is removed from publication in one or more environments, making it unavailable via the Content Delivery API.
  name: EntryUnpublished
  summary: An entry was unpublished from one or more environments.
  title: Entry Unpublished
- description: Triggered when a content entry is permanently deleted. The payload contains the entry metadata but not the full content since the entry no longer exists.
  name: EntryDeleted
  summary: An entry was permanently deleted from the stack.
  title: Entry Deleted
- description: Triggered when a new content entry is created within a content type. The entry is in draft state at this point and not yet published.
  name: EntryCreated
  summary: A new entry was created in the stack.
  title: Entry Created
- description: Triggered when the field values of an existing entry are modified and saved. Does not require the entry to be published for this event to fire.
  name: EntryUpdated
  summary: An existing entry's content was updated.
  title: Entry Updated
- description: Triggered when a media asset is published to one or more environments, making it available via the Content Delivery API for the affected environments.
  name: AssetPublished
  summary: An asset was published to one or more environments.
  title: Asset Published
- description: Triggered when a media asset is removed from publication in one or more environments.
  name: AssetUnpublished
  summary: An asset was unpublished from one or more environments.
  title: Asset Unpublished
- description: Triggered when a media asset is permanently deleted from the stack's asset library.
  name: AssetDeleted
  summary: An asset was permanently deleted from the stack.
  title: Asset Deleted
- description: Triggered when a new content type schema is created in the stack. Contains the full content type schema definition.
  name: ContentTypeCreated
  summary: A new content type was created in the stack.
  title: Content Type Created
- description: Triggered when the schema, options, or settings of an existing content type are modified.
  name: ContentTypeUpdated
  summary: An existing content type schema was updated.
  title: Content Type Updated
- description: Triggered when a content type is permanently deleted from the stack. This event also causes all entries of that content type to be permanently removed.
  name: ContentTypeDeleted
  summary: A content type was deleted from the stack.
  title: Content Type Deleted
- description: Triggered when an entry's workflow stage is changed. Contains both the previous and new workflow stage information for tracking content progression through editorial workflows.
  name: WorkflowStageChanged
  summary: An entry moved to a different workflow stage.
  title: Workflow Stage Changed
- description: Triggered when a Contentstack release — a collection of entries and assets — is deployed to one or more environments simultaneously.
  name: ReleaseDeployed
  summary: A content release was deployed to an environment.
  title: Release Deployed
- description: Triggered once when a bulk publish or unpublish job finishes processing all items. Unlike individual entry webhooks, this fires only once per job regardless of how many entries were affected, making it more efficient for static site generation cache invalidation.
  name: BulkJobCompleted
  summary: A bulk publish or unpublish job completed.
  title: Bulk Job Completed
name: Contentstack Webhooks
provider_name: contentstack
provider_slug: contentstack
servers:
- description: Your HTTPS endpoint that receives webhook event payloads from Contentstack. Must be publicly accessible and return a 2xx status code to acknowledge receipt.
  name: yourWebhookEndpoint
  protocol: https
  url: '{webhookUrl}'
slug: contentstack-webhooks-asyncapi
source_filename: contentstack-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Contentstack Webhooks\n  description: >-\n    Contentstack Webhooks provide event-driven notifications for content\n    lifecycle events within a stack. When configured, Contentstack sends HTTP\n    POST requests to your specified endpoint URL whenever matching events occur,\n    such as entries being published, assets being deleted, or workflow stages\n    changing. Webhooks support filtering by content type, entry UID, environment,\n    and locale. Bulk operations trigger a single webhook notification at job\n    completion rather than one notification per item, making them efficient for\n    static site generation and cache invalidation workflows.\n  version: 'v3'\n  contact:\n    name: Contentstack Support\n    url: https://www.contentstack.com/contact\nservers:\n  yourWebhookEndpoint:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your HTTPS endpoint that receives webhook event payloads from Contentstack.\n  \
  \    Must be publicly accessible and return a 2xx status code to acknowledge\n      receipt.\n    variables:\n      webhookUrl:\n        description: The URL of your webhook listener endpoint.\nchannels:\n  /webhook:\n    description: >-\n      Contentstack delivers all webhook event payloads via HTTP POST to this\n      channel. Each delivery includes event metadata and the content payload\n      relevant to the triggered action.\n    publish:\n      operationId: receiveWebhookEvent\n      summary: Receive a Contentstack webhook event\n      description: >-\n        Contentstack sends this message to your configured endpoint whenever\n        a matching content event occurs. The event type is indicated by the\n        event and module fields in the payload. Your endpoint must respond\n        with an HTTP 2xx status within 10 seconds to confirm receipt.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/EntryPublished'\n          - $ref: '#/components/messages/EntryUnpublished'\n\
  \          - $ref: '#/components/messages/EntryDeleted'\n          - $ref: '#/components/messages/EntryCreated'\n          - $ref: '#/components/messages/EntryUpdated'\n          - $ref: '#/components/messages/AssetPublished'\n          - $ref: '#/components/messages/AssetUnpublished'\n          - $ref: '#/components/messages/AssetDeleted'\n          - $ref: '#/components/messages/ContentTypeCreated'\n          - $ref: '#/components/messages/ContentTypeUpdated'\n          - $ref: '#/components/messages/ContentTypeDeleted'\n          - $ref: '#/components/messages/WorkflowStageChanged'\n          - $ref: '#/components/messages/ReleaseDeployed'\n          - $ref: '#/components/messages/BulkJobCompleted'\ncomponents:\n  messages:\n    EntryPublished:\n      name: EntryPublished\n      title: Entry Published\n      summary: An entry was published to one or more environments.\n      description: >-\n        Triggered when a content entry is successfully published to at least\n        one environment.\
  \ Contains the full entry data and the list of\n        environments and locales the entry was published to.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EntryEventPayload'\n      headers:\n        type: object\n        properties:\n          X-Contentstack-Request-ID:\n            type: string\n            description: Unique identifier for this webhook delivery request.\n          X-Contentstack-Timestamp:\n            type: string\n            description: Unix timestamp of when the webhook was dispatched.\n\n    EntryUnpublished:\n      name: EntryUnpublished\n      title: Entry Unpublished\n      summary: An entry was unpublished from one or more environments.\n      description: >-\n        Triggered when a content entry is removed from publication in one or\n        more environments, making it unavailable via the Content Delivery API.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EntryEventPayload'\n\
  \n    EntryDeleted:\n      name: EntryDeleted\n      title: Entry Deleted\n      summary: An entry was permanently deleted from the stack.\n      description: >-\n        Triggered when a content entry is permanently deleted. The payload\n        contains the entry metadata but not the full content since the entry\n        no longer exists.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EntryEventPayload'\n\n    EntryCreated:\n      name: EntryCreated\n      title: Entry Created\n      summary: A new entry was created in the stack.\n      description: >-\n        Triggered when a new content entry is created within a content type.\n        The entry is in draft state at this point and not yet published.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EntryEventPayload'\n\n    EntryUpdated:\n      name: EntryUpdated\n      title: Entry Updated\n      summary: An existing entry's content was updated.\n \
  \     description: >-\n        Triggered when the field values of an existing entry are modified and\n        saved. Does not require the entry to be published for this event to fire.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EntryEventPayload'\n\n    AssetPublished:\n      name: AssetPublished\n      title: Asset Published\n      summary: An asset was published to one or more environments.\n      description: >-\n        Triggered when a media asset is published to one or more environments,\n        making it available via the Content Delivery API for the affected\n        environments.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AssetEventPayload'\n\n    AssetUnpublished:\n      name: AssetUnpublished\n      title: Asset Unpublished\n      summary: An asset was unpublished from one or more environments.\n      description: >-\n        Triggered when a media asset is removed from publication\
  \ in one or\n        more environments.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AssetEventPayload'\n\n    AssetDeleted:\n      name: AssetDeleted\n      title: Asset Deleted\n      summary: An asset was permanently deleted from the stack.\n      description: >-\n        Triggered when a media asset is permanently deleted from the stack's\n        asset library.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AssetEventPayload'\n\n    ContentTypeCreated:\n      name: ContentTypeCreated\n      title: Content Type Created\n      summary: A new content type was created in the stack.\n      description: >-\n        Triggered when a new content type schema is created in the stack.\n        Contains the full content type schema definition.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ContentTypeEventPayload'\n\n    ContentTypeUpdated:\n      name: ContentTypeUpdated\n\
  \      title: Content Type Updated\n      summary: An existing content type schema was updated.\n      description: >-\n        Triggered when the schema, options, or settings of an existing content\n        type are modified.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ContentTypeEventPayload'\n\n    ContentTypeDeleted:\n      name: ContentTypeDeleted\n      title: Content Type Deleted\n      summary: A content type was deleted from the stack.\n      description: >-\n        Triggered when a content type is permanently deleted from the stack.\n        This event also causes all entries of that content type to be\n        permanently removed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ContentTypeEventPayload'\n\n    WorkflowStageChanged:\n      name: WorkflowStageChanged\n      title: Workflow Stage Changed\n      summary: An entry moved to a different workflow stage.\n      description: >-\n \
  \       Triggered when an entry's workflow stage is changed. Contains both\n        the previous and new workflow stage information for tracking content\n        progression through editorial workflows.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WorkflowEventPayload'\n\n    ReleaseDeployed:\n      name: ReleaseDeployed\n      title: Release Deployed\n      summary: A content release was deployed to an environment.\n      description: >-\n        Triggered when a Contentstack release — a collection of entries and\n        assets — is deployed to one or more environments simultaneously.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ReleaseEventPayload'\n\n    BulkJobCompleted:\n      name: BulkJobCompleted\n      title: Bulk Job Completed\n      summary: A bulk publish or unpublish job completed.\n      description: >-\n        Triggered once when a bulk publish or unpublish job finishes processing\n\
  \        all items. Unlike individual entry webhooks, this fires only once per\n        job regardless of how many entries were affected, making it more\n        efficient for static site generation cache invalidation.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BulkJobEventPayload'\n\n  schemas:\n    WebhookBase:\n      type: object\n      description: Common fields present in all Contentstack webhook payloads.\n      properties:\n        event:\n          type: string\n          description: The specific event action that triggered the webhook (e.g., publish, create, delete).\n        module:\n          type: string\n          description: The content module that generated the event (e.g., entry, asset, content_type).\n        api_key:\n          type: string\n          description: The API key of the stack where the event occurred.\n        uid:\n          type: string\n          description: The UID of the resource that triggered the event.\n\
  \        triggered_at:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp of when the event was triggered.\n\n    EntryEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type: object\n          description: Payload for entry-related webhook events.\n          properties:\n            data:\n              type: object\n              description: The entry data and publication context for this event.\n              properties:\n                entry:\n                  type: object\n                  description: The entry object containing all field values at the time of the event.\n                  properties:\n                    uid:\n                      type: string\n                      description: Unique identifier of the entry.\n                    title:\n                      type: string\n                      description: Title of the entry.\n                    locale:\n               \
  \       type: string\n                      description: Locale of the entry.\n                    _version:\n                      type: integer\n                      description: Version number of the entry.\n                    created_at:\n                      type: string\n                      format: date-time\n                      description: ISO 8601 timestamp when the entry was created.\n                    updated_at:\n                      type: string\n                      format: date-time\n                      description: ISO 8601 timestamp when the entry was last updated.\n                content_type:\n                  type: object\n                  description: The content type this entry belongs to.\n                  properties:\n                    uid:\n                      type: string\n                      description: UID of the content type.\n                    title:\n                      type: string\n                      description: Title of\
  \ the content type.\n                environments:\n                  type: array\n                  description: List of environments affected by this publish or unpublish event.\n                  items:\n                    type: object\n                    properties:\n                      name:\n                        type: string\n                        description: Name of the environment.\n                      uid:\n                        type: string\n                        description: UID of the environment.\n                locales:\n                  type: array\n                  description: List of locales affected by this event.\n                  items:\n                    type: object\n                    properties:\n                      code:\n                        type: string\n                        description: Locale code (e.g., en-us).\n                      name:\n                        type: string\n                        description: Display name\
  \ of the locale.\n\n    AssetEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type: object\n          description: Payload for asset-related webhook events.\n          properties:\n            data:\n              type: object\n              description: The asset data and event context.\n              properties:\n                asset:\n                  type: object\n                  description: The asset object.\n                  properties:\n                    uid:\n                      type: string\n                      description: Unique identifier of the asset.\n                    title:\n                      type: string\n                      description: Title of the asset.\n                    url:\n                      type: string\n                      format: uri\n                      description: CDN URL of the asset.\n                    filename:\n                      type: string\n                      description:\
  \ Original file name of the asset.\n                    content_type:\n                      type: string\n                      description: MIME type of the asset.\n                    file_size:\n                      type: string\n                      description: File size in bytes.\n                environments:\n                  type: array\n                  description: Environments affected by this publish or unpublish event.\n                  items:\n                    type: object\n                    properties:\n                      name:\n                        type: string\n                      uid:\n                        type: string\n\n    ContentTypeEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type: object\n          description: Payload for content type lifecycle webhook events.\n          properties:\n            data:\n              type: object\n              description: The content type data.\n            \
  \  properties:\n                content_type:\n                  type: object\n                  description: The content type schema at the time of the event.\n                  properties:\n                    uid:\n                      type: string\n                      description: Unique identifier of the content type.\n                    title:\n                      type: string\n                      description: Display name of the content type.\n                    schema:\n                      type: array\n                      description: Array of field definitions.\n                      items:\n                        type: object\n\n    WorkflowEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type: object\n          description: Payload for workflow stage change events.\n          properties:\n            data:\n              type: object\n              description: Workflow transition data.\n              properties:\n    \
  \            entry:\n                  type: object\n                  description: The entry that changed workflow stage.\n                  properties:\n                    uid:\n                      type: string\n                      description: UID of the entry.\n                    title:\n                      type: string\n                      description: Title of the entry.\n                content_type:\n                  type: object\n                  description: The content type of the entry.\n                  properties:\n                    uid:\n                      type: string\n                    title:\n                      type: string\n                workflow:\n                  type: object\n                  description: Workflow transition details.\n                  properties:\n                    uid:\n                      type: string\n                      description: UID of the workflow.\n                    name:\n                      type: string\n\
  \                      description: Name of the workflow.\n                    current_stage:\n                      type: object\n                      description: The new workflow stage.\n                      properties:\n                        uid:\n                          type: string\n                          description: UID of the new stage.\n                        title:\n                          type: string\n                          description: Title of the new stage.\n                    previous_stage:\n                      type: object\n                      description: The previous workflow stage.\n                      properties:\n                        uid:\n                          type: string\n                          description: UID of the previous stage.\n                        title:\n                          type: string\n                          description: Title of the previous stage.\n\n    ReleaseEventPayload:\n      allOf:\n        - $ref:\
  \ '#/components/schemas/WebhookBase'\n        - type: object\n          description: Payload for release deployment events.\n          properties:\n            data:\n              type: object\n              description: Release deployment data.\n              properties:\n                release:\n                  type: object\n                  description: The deployed release.\n                  properties:\n                    uid:\n                      type: string\n                      description: UID of the release.\n                    name:\n                      type: string\n                      description: Name of the release.\n                environments:\n                  type: array\n                  description: Environments the release was deployed to.\n                  items:\n                    type: object\n                    properties:\n                      name:\n                        type: string\n                      uid:\n                   \
  \     type: string\n\n    BulkJobEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type: object\n          description: Payload for bulk job completion events.\n          properties:\n            data:\n              type: object\n              description: Bulk job completion data.\n              properties:\n                job:\n                  type: object\n                  description: Summary of the completed bulk job.\n                  properties:\n                    uid:\n                      type: string\n                      description: UID of the bulk job.\n                    type:\n                      type: string\n                      description: Type of bulk operation performed.\n                      enum:\n                        - bulk_publish\n                        - bulk_unpublish\n                    status:\n                      type: string\n                      description: Completion status of the job.\n\
  \                      enum:\n                        - complete\n                        - partial\n                        - failed\n                    total_count:\n                      type: integer\n                      description: Total number of items in the bulk job.\n                    success_count:\n                      type: integer\n                      description: Number of items successfully processed.\n                    failed_count:\n                      type: integer\n                      description: Number of items that failed to process.\n                environments:\n                  type: array\n                  description: Target environments for the bulk operation.\n                  items:\n                    type: object\n                    properties:\n                      name:\n                        type: string\n                      uid:\n                        type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/contentstack/refs/heads/main/asyncapi/contentstack-webhooks-asyncapi.yml
spec_file: asyncapi/contentstack-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/contentstack/refs/heads/main/asyncapi/contentstack-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: v3
---
