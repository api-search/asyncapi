---
api_specs:
- filename: storyblok-content-delivery-api-v2-openapi.yml
  format: yaml
  label: Storyblok Content Delivery API
  slug: storyblok-content-delivery-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/storyblok/refs/heads/main/openapi/storyblok-content-delivery-api-v2-openapi.yml
- filename: storyblok-management-api-openapi.yml
  format: yaml
  label: Storyblok Management API
  slug: storyblok-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/storyblok/refs/heads/main/openapi/storyblok-management-api-openapi.yml
- filename: storyblok-image-service-openapi.yml
  format: yaml
  label: Storyblok Image Service
  slug: storyblok-image-service
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/storyblok/refs/heads/main/openapi/storyblok-image-service-openapi.yml
- filename: storyblok-webhooks-asyncapi.yml
  format: yaml
  label: Storyblok Webhooks
  slug: storyblok-webhooks
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/storyblok/refs/heads/main/asyncapi/storyblok-webhooks-asyncapi.yml
channels:
- description: The webhook delivery channel. Storyblok POSTs event payloads to the registered endpoint URL when subscribed actions occur in the space. The endpoint must respond with a 2xx HTTP status code within 120 seconds to be considered a successful delivery. For long-running tasks, respond immediately with 202 Accepted and process asynchronously.
  name: /webhook
  operation: publish
  operation_id: receiveStoryblokEvent
  summary: Receive a Storyblok space event notification
description: The Storyblok Webhook system delivers real-time event notifications to registered HTTP endpoints when content events occur in a Storyblok space. Events are triggered by actions such as story publication, unpublication, deletion, asset upload, and datasource updates. Webhook payloads are delivered as HTTP POST requests with a JSON body and an optional HMAC-SHA1 signature header for payload integrity verification. Webhooks are configured per space and managed via the Management API or the Storyblok dashboard.
layout: asyncapi
messages:
- description: Delivered when a story transitions to published state, either via the editor, the Management API, or a scheduled publication. This event is useful for triggering cache invalidation, static site rebuilds, or search index updates.
  name: StoryPublished
  summary: A story was published in the space.
  title: Story Published
- description: Delivered when a published story is unpublished, removing it from public access via the Content Delivery API. Useful for cache invalidation and removal from search indexes.
  name: StoryUnpublished
  summary: A story was unpublished in the space.
  title: Story Unpublished
- description: Delivered when a story is deleted from the space. After deletion, the story is no longer accessible via either the Content Delivery or Management APIs. Useful for cleaning up derived data such as search index entries or generated files.
  name: StoryDeleted
  summary: A story was permanently deleted from the space.
  title: Story Deleted
- description: Delivered when a story's position in the folder hierarchy changes, resulting in a new full_slug. Useful for updating navigation caches, redirects, and sitemap data that depend on story URLs.
  name: StoryMoved
  summary: A story was moved to a different folder in the space.
  title: Story Moved
- description: Delivered when a new file is successfully uploaded to the space's asset library. Includes the asset ID so the asset details can be retrieved via the Management API if needed.
  name: AssetCreated
  summary: A new asset was uploaded to the space.
  title: Asset Created
- description: Delivered when an asset is removed from the space's asset library. Stories that reference the deleted asset will display broken media. Use this event to clean up any external references to the asset.
  name: AssetDeleted
  summary: An asset was deleted from the space.
  title: Asset Deleted
- description: Delivered when entries in a datasource are modified via the Management API or editor. Useful for invalidating caches that depend on datasource values such as navigation options or translations.
  name: DatasourceEntriesUpdated
  summary: Datasource entries were created, updated, or deleted.
  title: Datasource Entries Updated
name: Storyblok Webhooks
provider_name: Storyblok
provider_slug: storyblok
servers:
- description: The customer-defined HTTPS endpoint registered to receive webhook event notifications from Storyblok. The URL is configured when creating a webhook endpoint via the Management API or dashboard.
  name: customerEndpoint
  protocol: https
  url: '{webhookUrl}'
slug: storyblok-webhooks-asyncapi
source_filename: storyblok-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Storyblok Webhooks\n  description: >-\n    The Storyblok Webhook system delivers real-time event notifications to\n    registered HTTP endpoints when content events occur in a Storyblok space.\n    Events are triggered by actions such as story publication, unpublication,\n    deletion, asset upload, and datasource updates. Webhook payloads are\n    delivered as HTTP POST requests with a JSON body and an optional\n    HMAC-SHA1 signature header for payload integrity verification.\n    Webhooks are configured per space and managed via the Management API or\n    the Storyblok dashboard.\n  version: '1'\n  contact:\n    name: Storyblok Support\n    url: https://www.storyblok.com/contact\nexternalDocs:\n  description: Storyblok Webhooks Documentation\n  url: https://www.storyblok.com/docs/concepts/webhooks\nservers:\n  customerEndpoint:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      The customer-defined HTTPS endpoint registered\
  \ to receive webhook event\n      notifications from Storyblok. The URL is configured when creating a\n      webhook endpoint via the Management API or dashboard.\n    variables:\n      webhookUrl:\n        description: >-\n          The fully-qualified HTTPS URL of the endpoint that will receive\n          webhook POST requests from Storyblok.\n    security:\n      - webhookSignature: []\nchannels:\n  /webhook:\n    description: >-\n      The webhook delivery channel. Storyblok POSTs event payloads to the\n      registered endpoint URL when subscribed actions occur in the space.\n      The endpoint must respond with a 2xx HTTP status code within 120 seconds\n      to be considered a successful delivery. For long-running tasks, respond\n      immediately with 202 Accepted and process asynchronously.\n    publish:\n      operationId: receiveStoryblokEvent\n      summary: Receive a Storyblok space event notification\n      description: >-\n        Called by Storyblok when a subscribed event\
  \ fires in the space. The\n        payload identifies the action type, the affected resource IDs, and the\n        space context. Verify the webhook-signature header before processing\n        the payload to ensure the request originated from Storyblok.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/StoryPublished'\n          - $ref: '#/components/messages/StoryUnpublished'\n          - $ref: '#/components/messages/StoryDeleted'\n          - $ref: '#/components/messages/StoryMoved'\n          - $ref: '#/components/messages/AssetCreated'\n          - $ref: '#/components/messages/AssetDeleted'\n          - $ref: '#/components/messages/DatasourceEntriesUpdated'\ncomponents:\n  securitySchemes:\n    webhookSignature:\n      type: httpApiKey\n      in: header\n      name: webhook-signature\n      description: >-\n        HMAC-SHA1 signature of the raw request body, generated using the\n        webhook secret configured on the endpoint. Recipients should compute\n\
  \        the HMAC-SHA1 of the raw body bytes using the shared secret and\n        compare it to this header value to verify authenticity.\n\n  messages:\n    StoryPublished:\n      name: StoryPublished\n      title: Story Published\n      summary: A story was published in the space.\n      description: >-\n        Delivered when a story transitions to published state, either via\n        the editor, the Management API, or a scheduled publication. This\n        event is useful for triggering cache invalidation, static site\n        rebuilds, or search index updates.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          webhook-signature:\n            type: string\n            description: >-\n              HMAC-SHA1 signature of the raw request body for integrity\n              verification.\n          content-type:\n            type: string\n            description: Always application/json.\n      payload:\n        $ref: '#/components/schemas/StoryEventPayload'\n\
  \      examples:\n        - name: StoryPublishedExample\n          payload:\n            action: published\n            story_id: 123456\n            space_id: 12345\n            text: Story \"My Blog Post\" (123456) published\n            full_slug: blog/my-blog-post\n\n    StoryUnpublished:\n      name: StoryUnpublished\n      title: Story Unpublished\n      summary: A story was unpublished in the space.\n      description: >-\n        Delivered when a published story is unpublished, removing it from\n        public access via the Content Delivery API. Useful for cache\n        invalidation and removal from search indexes.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          webhook-signature:\n            type: string\n            description: HMAC-SHA1 signature for integrity verification.\n      payload:\n        $ref: '#/components/schemas/StoryEventPayload'\n      examples:\n        - name: StoryUnpublishedExample\n         \
  \ payload:\n            action: unpublished\n            story_id: 123456\n            space_id: 12345\n            text: Story \"My Blog Post\" (123456) unpublished\n\n    StoryDeleted:\n      name: StoryDeleted\n      title: Story Deleted\n      summary: A story was permanently deleted from the space.\n      description: >-\n        Delivered when a story is deleted from the space. After deletion, the\n        story is no longer accessible via either the Content Delivery or\n        Management APIs. Useful for cleaning up derived data such as search\n        index entries or generated files.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          webhook-signature:\n            type: string\n            description: HMAC-SHA1 signature for integrity verification.\n      payload:\n        $ref: '#/components/schemas/StoryEventPayload'\n      examples:\n        - name: StoryDeletedExample\n          payload:\n            action: deleted\n\
  \            story_id: 123456\n            space_id: 12345\n            text: Story \"My Blog Post\" (123456) deleted\n\n    StoryMoved:\n      name: StoryMoved\n      title: Story Moved\n      summary: A story was moved to a different folder in the space.\n      description: >-\n        Delivered when a story's position in the folder hierarchy changes,\n        resulting in a new full_slug. Useful for updating navigation caches,\n        redirects, and sitemap data that depend on story URLs.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          webhook-signature:\n            type: string\n            description: HMAC-SHA1 signature for integrity verification.\n      payload:\n        $ref: '#/components/schemas/StoryEventPayload'\n      examples:\n        - name: StoryMovedExample\n          payload:\n            action: moved\n            story_id: 123456\n            space_id: 12345\n            text: Story \"My Blog Post\" (123456)\
  \ moved\n\n    AssetCreated:\n      name: AssetCreated\n      title: Asset Created\n      summary: A new asset was uploaded to the space.\n      description: >-\n        Delivered when a new file is successfully uploaded to the space's\n        asset library. Includes the asset ID so the asset details can be\n        retrieved via the Management API if needed.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          webhook-signature:\n            type: string\n            description: HMAC-SHA1 signature for integrity verification.\n      payload:\n        $ref: '#/components/schemas/AssetEventPayload'\n      examples:\n        - name: AssetCreatedExample\n          payload:\n            action: created\n            asset_id: 78901\n            space_id: 12345\n            text: Asset \"hero-image.jpg\" (78901) created\n\n    AssetDeleted:\n      name: AssetDeleted\n      title: Asset Deleted\n      summary: An asset was deleted from the\
  \ space.\n      description: >-\n        Delivered when an asset is removed from the space's asset library.\n        Stories that reference the deleted asset will display broken media.\n        Use this event to clean up any external references to the asset.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          webhook-signature:\n            type: string\n            description: HMAC-SHA1 signature for integrity verification.\n      payload:\n        $ref: '#/components/schemas/AssetEventPayload'\n      examples:\n        - name: AssetDeletedExample\n          payload:\n            action: deleted\n            asset_id: 78901\n            space_id: 12345\n            text: Asset \"hero-image.jpg\" (78901) deleted\n\n    DatasourceEntriesUpdated:\n      name: DatasourceEntriesUpdated\n      title: Datasource Entries Updated\n      summary: Datasource entries were created, updated, or deleted.\n      description: >-\n        Delivered\
  \ when entries in a datasource are modified via the Management\n        API or editor. Useful for invalidating caches that depend on datasource\n        values such as navigation options or translations.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          webhook-signature:\n            type: string\n            description: HMAC-SHA1 signature for integrity verification.\n      payload:\n        $ref: '#/components/schemas/DatasourceEventPayload'\n      examples:\n        - name: DatasourceUpdatedExample\n          payload:\n            action: entries_updated\n            datasource_id: 456\n            space_id: 12345\n            text: Datasource \"Colors\" (456) entries updated\n\n  schemas:\n    StoryEventPayload:\n      type: object\n      description: >-\n        Payload delivered by Storyblok for story-related webhook events.\n        Identifies the affected story, the action performed, and the space\n        context.\n  \
  \    required:\n        - action\n        - story_id\n        - space_id\n        - text\n      properties:\n        action:\n          type: string\n          description: >-\n            The event action that triggered the webhook. One of published,\n            unpublished, deleted, or moved.\n          enum:\n            - published\n            - unpublished\n            - deleted\n            - moved\n        story_id:\n          type: integer\n          description: Numeric ID of the story that triggered the event.\n        space_id:\n          type: integer\n          description: Numeric ID of the space in which the event occurred.\n        text:\n          type: string\n          description: >-\n            Human-readable description of the event, including the story name,\n            ID, and action.\n        full_slug:\n          type: string\n          description: >-\n            Full URL slug of the story at the time of the event. Present for\n            published and\
  \ moved events.\n\n    AssetEventPayload:\n      type: object\n      description: >-\n        Payload delivered by Storyblok for asset-related webhook events.\n        Identifies the affected asset, the action performed, and the space\n        context.\n      required:\n        - action\n        - asset_id\n        - space_id\n        - text\n      properties:\n        action:\n          type: string\n          description: The event action. One of created or deleted.\n          enum:\n            - created\n            - deleted\n        asset_id:\n          type: integer\n          description: Numeric ID of the asset that triggered the event.\n        space_id:\n          type: integer\n          description: Numeric ID of the space in which the event occurred.\n        text:\n          type: string\n          description: >-\n            Human-readable description of the event, including the asset\n            filename, ID, and action.\n\n    DatasourceEventPayload:\n      type: object\n\
  \      description: >-\n        Payload delivered by Storyblok for datasource-related webhook events.\n        Identifies the affected datasource and the space context.\n      required:\n        - action\n        - datasource_id\n        - space_id\n        - text\n      properties:\n        action:\n          type: string\n          description: The event action. Currently entries_updated.\n          enum:\n            - entries_updated\n        datasource_id:\n          type: integer\n          description: Numeric ID of the datasource that was updated.\n        space_id:\n          type: integer\n          description: Numeric ID of the space in which the event occurred.\n        text:\n          type: string\n          description: Human-readable description of the datasource update event.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/storyblok/refs/heads/main/asyncapi/storyblok-webhooks-asyncapi.yml
spec_file: asyncapi/storyblok-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/storyblok/refs/heads/main/asyncapi/storyblok-webhooks-asyncapi.yml
tags:
- CMS
- Content Delivery
- Content Management
- Headless CMS
- Image Optimization
- REST API
- Visual Editor
- Webhooks
- AsyncAPI
- Webhooks
- Events
version: '1'
---
