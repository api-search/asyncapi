---
api_specs:
- filename: strapi-rest-api-openapi.yml
  format: yaml
  label: Strapi REST API
  slug: strapi-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/strapi/refs/heads/main/openapi/strapi-rest-api-openapi.yml
- filename: strapi-admin-panel-api-openapi.yml
  format: yaml
  label: Strapi Admin Panel API
  slug: strapi-admin-panel-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/strapi/refs/heads/main/openapi/strapi-admin-panel-api-openapi.yml
- filename: strapi-users-and-permissions-api-openapi.yml
  format: yaml
  label: Strapi Users and Permissions API
  slug: strapi-users-permissions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/strapi/refs/heads/main/openapi/strapi-users-and-permissions-api-openapi.yml
- filename: strapi-webhooks-asyncapi.yml
  format: yaml
  label: Strapi Webhooks
  slug: strapi-webhooks
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/strapi/refs/heads/main/asyncapi/strapi-webhooks-asyncapi.yml
channels:
- description: The webhook delivery channel. Strapi sends HTTP POST requests to the configured URL whenever a subscribed event occurs. Each request includes an X-Strapi-Event header with the event type and any globally configured headers.
  name: /webhook
  operation: publish
  operation_id: receiveWebhookEvent
  summary: Receive a Strapi webhook event
description: Strapi includes a built-in webhook system that notifies external services whenever certain events occur in the CMS. Rather than polling the Strapi API for changes, you can configure Strapi to send HTTP POST requests to a specified URL when content entries or media assets are created, updated, deleted, published, or unpublished. Webhooks are configured through the Strapi admin panel under Settings > Webhooks and include a custom X-Strapi-Event header identifying the event type. Global webhook headers can also be configured in the server configuration file.
layout: asyncapi
messages:
- description: ''
  name: EntryCreate
  summary: Triggered when a new content entry is created in Strapi.
  title: Entry Created
- description: ''
  name: EntryUpdate
  summary: Triggered when an existing content entry is updated in Strapi.
  title: Entry Updated
- description: ''
  name: EntryDelete
  summary: Triggered when a content entry is deleted from Strapi.
  title: Entry Deleted
- description: ''
  name: EntryPublish
  summary: Triggered when a draft content entry is published. Only available when Draft and Publish is enabled on the content-type.
  title: Entry Published
- description: ''
  name: EntryUnpublish
  summary: Triggered when a published content entry is unpublished and reverted to draft status. Only available when Draft and Publish is enabled on the content-type.
  title: Entry Unpublished
- description: ''
  name: MediaCreate
  summary: Triggered when a new file is uploaded to the Strapi media library, either directly or as part of a content entry creation.
  title: Media Created
- description: ''
  name: MediaUpdate
  summary: Triggered when a file in the Strapi media library is updated, such as changing its metadata or replacing the file.
  title: Media Updated
- description: ''
  name: MediaDelete
  summary: Triggered when a file is deleted from the Strapi media library.
  title: Media Deleted
name: Strapi Webhooks
provider_name: Strapi
provider_slug: strapi
servers:
- description: The external URL configured to receive webhook events from Strapi. This URL is set by the user in the Strapi admin panel when creating a webhook configuration.
  name: webhookReceiver
  protocol: https
  url: '{webhookUrl}'
slug: strapi-webhooks-asyncapi
source_filename: strapi-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Strapi Webhooks\n  description: >-\n    Strapi includes a built-in webhook system that notifies external services\n    whenever certain events occur in the CMS. Rather than polling the Strapi\n    API for changes, you can configure Strapi to send HTTP POST requests to\n    a specified URL when content entries or media assets are created, updated,\n    deleted, published, or unpublished. Webhooks are configured through the\n    Strapi admin panel under Settings > Webhooks and include a custom\n    X-Strapi-Event header identifying the event type. Global webhook headers\n    can also be configured in the server configuration file.\n  version: '5.0.0'\n  contact:\n    name: Strapi Support\n    url: https://strapi.io/support\n  externalDocs:\n    description: Strapi Webhooks Documentation\n    url: https://docs.strapi.io/cms/backend-customization/webhooks\nservers:\n  webhookReceiver:\n    url: '{webhookUrl}'\n    protocol: https\n    description:\
  \ >-\n      The external URL configured to receive webhook events from Strapi.\n      This URL is set by the user in the Strapi admin panel when creating\n      a webhook configuration.\n    variables:\n      webhookUrl:\n        description: The URL of the webhook receiver endpoint\nchannels:\n  /webhook:\n    description: >-\n      The webhook delivery channel. Strapi sends HTTP POST requests to the\n      configured URL whenever a subscribed event occurs. Each request\n      includes an X-Strapi-Event header with the event type and any\n      globally configured headers.\n    publish:\n      operationId: receiveWebhookEvent\n      summary: Receive a Strapi webhook event\n      description: >-\n        Strapi publishes webhook events to this channel when content entries\n        or media assets are created, updated, deleted, published, or\n        unpublished. The receiving application processes these events to\n        trigger downstream actions such as cache invalidation, search index\n\
  \        updates, or notifications.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/EntryCreate'\n          - $ref: '#/components/messages/EntryUpdate'\n          - $ref: '#/components/messages/EntryDelete'\n          - $ref: '#/components/messages/EntryPublish'\n          - $ref: '#/components/messages/EntryUnpublish'\n          - $ref: '#/components/messages/MediaCreate'\n          - $ref: '#/components/messages/MediaUpdate'\n          - $ref: '#/components/messages/MediaDelete'\ncomponents:\n  messages:\n    EntryCreate:\n      name: entry.create\n      title: Entry Created\n      summary: >-\n        Triggered when a new content entry is created in Strapi.\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/EntryEventPayload'\n    EntryUpdate:\n      name: entry.update\n      title: Entry Updated\n      summary: >-\n        Triggered when an existing content entry is updated in Strapi.\n\
  \      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/EntryEventPayload'\n    EntryDelete:\n      name: entry.delete\n      title: Entry Deleted\n      summary: >-\n        Triggered when a content entry is deleted from Strapi.\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/EntryEventPayload'\n    EntryPublish:\n      name: entry.publish\n      title: Entry Published\n      summary: >-\n        Triggered when a draft content entry is published. Only available\n        when Draft and Publish is enabled on the content-type.\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/EntryEventPayload'\n    EntryUnpublish:\n      name: entry.unpublish\n      title: Entry Unpublished\n      summary: >-\n        Triggered when a published content entry is unpublished and reverted\n       \
  \ to draft status. Only available when Draft and Publish is enabled on\n        the content-type.\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/EntryEventPayload'\n    MediaCreate:\n      name: media.create\n      title: Media Created\n      summary: >-\n        Triggered when a new file is uploaded to the Strapi media library,\n        either directly or as part of a content entry creation.\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/MediaEventPayload'\n    MediaUpdate:\n      name: media.update\n      title: Media Updated\n      summary: >-\n        Triggered when a file in the Strapi media library is updated, such\n        as changing its metadata or replacing the file.\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/MediaEventPayload'\n    MediaDelete:\n   \
  \   name: media.delete\n      title: Media Deleted\n      summary: >-\n        Triggered when a file is deleted from the Strapi media library.\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/MediaEventPayload'\n  schemas:\n    WebhookHeaders:\n      type: object\n      properties:\n        X-Strapi-Event:\n          type: string\n          description: >-\n            The event type that triggered the webhook (e.g., entry.create,\n            entry.update, media.delete)\n          enum:\n            - entry.create\n            - entry.update\n            - entry.delete\n            - entry.publish\n            - entry.unpublish\n            - media.create\n            - media.update\n            - media.delete\n        Content-Type:\n          type: string\n          description: The content type of the webhook payload\n          const: application/json\n    EntryEventPayload:\n      type: object\n      description:\
  \ >-\n        The payload sent when a content entry event occurs. Contains the\n        event type, the date it occurred, the content-type model, and the\n        entry data.\n      properties:\n        event:\n          type: string\n          description: The event type identifier\n          enum:\n            - entry.create\n            - entry.update\n            - entry.delete\n            - entry.publish\n            - entry.unpublish\n        createdAt:\n          type: string\n          format: date-time\n          description: The timestamp when the event occurred\n        model:\n          type: string\n          description: >-\n            The singular name of the content-type model (e.g., article,\n            category, product)\n        uid:\n          type: string\n          description: >-\n            The unique identifier of the content-type (e.g.,\n            api::article.article)\n        entry:\n          type: object\n          description: >-\n            The full\
  \ content entry data including all field values,\n            timestamps, and the document ID\n          properties:\n            id:\n              type: integer\n              description: The unique integer ID of the entry\n            documentId:\n              type: string\n              description: The unique document identifier\n            createdAt:\n              type: string\n              format: date-time\n              description: The timestamp when the entry was created\n            updatedAt:\n              type: string\n              format: date-time\n              description: The timestamp when the entry was last updated\n            publishedAt:\n              type: string\n              format: date-time\n              nullable: true\n              description: The timestamp when the entry was published\n            locale:\n              type: string\n              nullable: true\n              description: The locale code if internationalization is enabled\n \
  \         additionalProperties: true\n    MediaEventPayload:\n      type: object\n      description: >-\n        The payload sent when a media file event occurs. Contains the event\n        type, the date it occurred, and the media file data.\n      properties:\n        event:\n          type: string\n          description: The event type identifier\n          enum:\n            - media.create\n            - media.update\n            - media.delete\n        createdAt:\n          type: string\n          format: date-time\n          description: The timestamp when the event occurred\n        media:\n          type: object\n          description: >-\n            The media file data including metadata, URL, and format\n            information\n          properties:\n            id:\n              type: integer\n              description: The unique ID of the file\n            name:\n              type: string\n              description: The original file name\n            alternativeText:\n\
  \              type: string\n              nullable: true\n              description: Alternative text for accessibility\n            caption:\n              type: string\n              nullable: true\n              description: A caption for the file\n            width:\n              type: integer\n              nullable: true\n              description: The width in pixels for image files\n            height:\n              type: integer\n              nullable: true\n              description: The height in pixels for image files\n            formats:\n              type: object\n              nullable: true\n              description: >-\n                Responsive image format variants (thumbnail, small,\n                medium, large)\n            hash:\n              type: string\n              description: A unique hash identifier for the file\n            ext:\n              type: string\n              description: The file extension\n            mime:\n              type: string\n\
  \              description: The MIME type of the file\n            size:\n              type: number\n              description: The file size in kilobytes\n            url:\n              type: string\n              description: The URL path to access the file\n            provider:\n              type: string\n              description: >-\n                The storage provider (e.g., local, aws-s3, cloudinary)\n            createdAt:\n              type: string\n              format: date-time\n              description: The timestamp when the file was uploaded\n            updatedAt:\n              type: string\n              format: date-time\n              description: The timestamp when the file was last updated\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/strapi/refs/heads/main/asyncapi/strapi-webhooks-asyncapi.yml
spec_file: asyncapi/strapi-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/strapi/refs/heads/main/asyncapi/strapi-webhooks-asyncapi.yml
tags:
- CMS
- Content Management
- Headless CMS
- Node.js
- Open Source
- AsyncAPI
- Webhooks
- Events
version: 5.0.0
---
