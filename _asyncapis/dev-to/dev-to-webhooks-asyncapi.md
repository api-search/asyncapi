---
api_specs:
- filename: dev-to-forem-api-openapi.yml
  format: yaml
  label: Dev.to Forem API
  slug: forem-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dev-to/refs/heads/main/openapi/dev-to-forem-api-openapi.yml
- filename: dev-to-webhooks-asyncapi.yml
  format: yaml
  label: Dev.to Webhooks API
  slug: webhooks-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/dev-to/refs/heads/main/asyncapi/dev-to-webhooks-asyncapi.yml
channels:
- description: The subscriber's webhook endpoint URL that receives HTTP POST callbacks from Dev.to. This URL is registered via the Forem REST API when creating a webhook subscription. Dev.to sends a JSON payload to this URL whenever a subscribed event occurs.
  name: /webhook
  operation: publish
  operation_id: receiveArticleEvent
  summary: Receive article lifecycle events
description: The Dev.to Webhooks event-driven interface allows applications to receive real-time HTTP POST callbacks when specific events occur on the Dev.to platform. Webhook subscriptions are managed via the Forem REST API, and once configured, the platform sends JSON payloads to the registered target URL whenever subscribed article lifecycle events are triggered. Supported events include article creation, updates, and deletion.
layout: asyncapi
messages:
- description: This event fires when a user publishes a new article on Dev.to. The payload contains the full article object including title, body, tags, author information, and publication metadata.
  name: ArticleCreated
  summary: Triggered when a new article is published on the platform.
  title: Article Created
- description: This event fires when a previously published article is edited on Dev.to. The payload contains the updated article object reflecting the latest changes to the article's content and metadata.
  name: ArticleUpdated
  summary: Triggered when an existing published article is updated.
  title: Article Updated
- description: This event fires when an article is removed from Dev.to. The payload contains the article object as it existed before deletion, allowing subscribers to identify which article was removed and take appropriate action.
  name: ArticleDestroyed
  summary: Triggered when a published article is deleted from the platform.
  title: Article Destroyed
name: Dev.to Webhooks Events
provider_name: dev-to
provider_slug: dev-to
servers:
- description: Dev.to platform server that dispatches webhook events to registered subscriber endpoints when article lifecycle events occur.
  name: devToWebhookSource
  protocol: https
  url: dev.to
slug: dev-to-webhooks-asyncapi
source_filename: dev-to-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Dev.to Webhooks Events\n  description: >-\n    The Dev.to Webhooks event-driven interface allows applications to receive\n    real-time HTTP POST callbacks when specific events occur on the Dev.to\n    platform. Webhook subscriptions are managed via the Forem REST API, and\n    once configured, the platform sends JSON payloads to the registered\n    target URL whenever subscribed article lifecycle events are triggered.\n    Supported events include article creation, updates, and deletion.\n  version: '1.0.0'\n  contact:\n    name: Forem Support\n    url: https://forem.com\nservers:\n  devToWebhookSource:\n    url: dev.to\n    protocol: https\n    description: >-\n      Dev.to platform server that dispatches webhook events to registered\n      subscriber endpoints when article lifecycle events occur.\nchannels:\n  /webhook:\n    description: >-\n      The subscriber's webhook endpoint URL that receives HTTP POST\n      callbacks from Dev.to.\
  \ This URL is registered via the Forem REST API\n      when creating a webhook subscription. Dev.to sends a JSON payload to\n      this URL whenever a subscribed event occurs.\n    publish:\n      operationId: receiveArticleEvent\n      summary: Receive article lifecycle events\n      description: >-\n        Receives article lifecycle event notifications from the Dev.to\n        platform. Each event includes the full article data as a JSON\n        payload delivered via HTTP POST to the registered target URL.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/ArticleCreated'\n          - $ref: '#/components/messages/ArticleUpdated'\n          - $ref: '#/components/messages/ArticleDestroyed'\ncomponents:\n  securitySchemes:\n    apiKey:\n      type: httpApiKey\n      name: api-key\n      in: header\n      description: >-\n        API key used to manage webhook subscriptions via the Forem REST API.\n        Webhook callback payloads themselves do not include authentication\n\
  \        headers from the sender.\n  messages:\n    ArticleCreated:\n      name: article_created\n      title: Article Created\n      summary: >-\n        Triggered when a new article is published on the platform.\n      description: >-\n        This event fires when a user publishes a new article on Dev.to.\n        The payload contains the full article object including title, body,\n        tags, author information, and publication metadata.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ArticleEventPayload'\n    ArticleUpdated:\n      name: article_updated\n      title: Article Updated\n      summary: >-\n        Triggered when an existing published article is updated.\n      description: >-\n        This event fires when a previously published article is edited on\n        Dev.to. The payload contains the updated article object reflecting\n        the latest changes to the article's content and metadata.\n      contentType: application/json\n\
  \      payload:\n        $ref: '#/components/schemas/ArticleEventPayload'\n    ArticleDestroyed:\n      name: article_destroyed\n      title: Article Destroyed\n      summary: >-\n        Triggered when a published article is deleted from the platform.\n      description: >-\n        This event fires when an article is removed from Dev.to. The\n        payload contains the article object as it existed before deletion,\n        allowing subscribers to identify which article was removed and\n        take appropriate action.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ArticleEventPayload'\n  schemas:\n    ArticleEventPayload:\n      type: object\n      description: >-\n        The webhook event payload sent by Dev.to when an article lifecycle\n        event occurs. Contains the full article data along with author and\n        organization information.\n      properties:\n        type_of:\n          type: string\n          description: >-\n   \
  \         The type of resource, always \"article\".\n        id:\n          type: integer\n          description: >-\n            The unique identifier of the article.\n        title:\n          type: string\n          description: >-\n            The title of the article.\n        description:\n          type: string\n          description: >-\n            A short description or subtitle for the article.\n        slug:\n          type: string\n          description: >-\n            The URL slug of the article.\n        path:\n          type: string\n          description: >-\n            The relative path to the article on DEV.\n        url:\n          type: string\n          format: uri\n          description: >-\n            The full URL of the article.\n        comments_count:\n          type: integer\n          description: >-\n            The number of comments on the article.\n        public_reactions_count:\n          type: integer\n          description: >-\n            The total\
  \ number of public reactions on the article.\n        published_timestamp:\n          type: string\n          format: date-time\n          description: >-\n            The ISO 8601 timestamp when the article was published.\n        positive_reactions_count:\n          type: integer\n          description: >-\n            The count of positive reactions.\n        cover_image:\n          type: string\n          format: uri\n          nullable: true\n          description: >-\n            The URL of the article's cover image.\n        social_image:\n          type: string\n          format: uri\n          description: >-\n            The URL of the social sharing image.\n        canonical_url:\n          type: string\n          format: uri\n          description: >-\n            The canonical URL of the article.\n        created_at:\n          type: string\n          format: date-time\n          description: >-\n            The ISO 8601 timestamp when the article was created.\n        edited_at:\n\
  \          type: string\n          format: date-time\n          nullable: true\n          description: >-\n            The ISO 8601 timestamp when the article was last edited.\n        published_at:\n          type: string\n          format: date-time\n          description: >-\n            The ISO 8601 timestamp when the article was published.\n        reading_time_minutes:\n          type: integer\n          description: >-\n            The estimated reading time in minutes.\n        tag_list:\n          type: array\n          items:\n            type: string\n          description: >-\n            A list of tags associated with the article.\n        body_html:\n          type: string\n          description: >-\n            The article body rendered as HTML.\n        body_markdown:\n          type: string\n          description: >-\n            The article body in the original Markdown format.\n        user:\n          $ref: '#/components/schemas/WebhookUser'\n        organization:\n\
  \          $ref: '#/components/schemas/WebhookOrganization'\n    WebhookUser:\n      type: object\n      description: >-\n        The author of the article included in webhook event payloads.\n      properties:\n        name:\n          type: string\n          description: >-\n            The display name of the user.\n        username:\n          type: string\n          description: >-\n            The unique username of the user.\n        twitter_username:\n          type: string\n          nullable: true\n          description: >-\n            The user's Twitter username.\n        github_username:\n          type: string\n          nullable: true\n          description: >-\n            The user's GitHub username.\n        website_url:\n          type: string\n          format: uri\n          nullable: true\n          description: >-\n            The user's website URL.\n        profile_image:\n          type: string\n          format: uri\n          description: >-\n            The\
  \ URL of the user's profile image.\n        profile_image_90:\n          type: string\n          format: uri\n          description: >-\n            The URL of the 90px profile image.\n    WebhookOrganization:\n      type: object\n      nullable: true\n      description: >-\n        The organization the article was published under, if applicable.\n        May be null if the article was not published under an organization.\n      properties:\n        name:\n          type: string\n          description: >-\n            The display name of the organization.\n        username:\n          type: string\n          description: >-\n            The unique username (slug) of the organization.\n        slug:\n          type: string\n          description: >-\n            The URL slug of the organization.\n        profile_image:\n          type: string\n          format: uri\n          description: >-\n            The URL of the organization's profile image.\n        profile_image_90:\n         \
  \ type: string\n          format: uri\n          description: >-\n            The URL of the 90px profile image.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/dev-to/refs/heads/main/asyncapi/dev-to-webhooks-asyncapi.yml
spec_file: asyncapi/dev-to-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/dev-to/refs/heads/main/asyncapi/dev-to-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
