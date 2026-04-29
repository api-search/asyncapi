---
api_specs:
- filename: confluence-cloud-v2.yml
  format: yaml
  label: Confluence Cloud REST API v2
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/confluence/refs/heads/main/openapi/confluence-cloud-v2.yml
channels:
- description: Channel for page_created events
  name: pageCreated
- description: Channel for page_updated events
  name: pageUpdated
- description: Channel for page_removed events
  name: pageRemoved
- description: Channel for page_trashed events
  name: pageTrashed
- description: Channel for page_restored events
  name: pageRestored
- description: Channel for space_created events
  name: spaceCreated
- description: Channel for space_updated events
  name: spaceUpdated
- description: Channel for space_removed events
  name: spaceRemoved
- description: Channel for comment_created events
  name: commentCreated
- description: Channel for comment_updated events
  name: commentUpdated
- description: Channel for comment_removed events
  name: commentRemoved
- description: Channel for attachment_created events
  name: attachmentCreated
- description: Channel for attachment_updated events
  name: attachmentUpdated
- description: Channel for attachment_removed events
  name: attachmentRemoved
- description: Channel for label_created events
  name: labelCreated
- description: Channel for label_removed events
  name: labelRemoved
- description: Channel for blog_created events
  name: blogCreated
- description: Channel for blog_updated events
  name: blogUpdated
- description: Channel for blog_removed events
  name: blogRemoved
description: Asynchronous event notifications from Confluence Cloud. Webhooks allow applications to receive real-time notifications when content, spaces, or other entities are created, updated, or deleted in Confluence. Webhooks can be registered through the Confluence UI, REST API, or via Atlassian Connect app descriptors.
layout: asyncapi
messages:
- description: ''
  name: PageCreated
  summary: A new page has been created in Confluence.
  title: Page Created
- description: ''
  name: PageUpdated
  summary: An existing page has been updated in Confluence.
  title: Page Updated
- description: ''
  name: PageRemoved
  summary: A page has been permanently removed from Confluence.
  title: Page Removed
- description: ''
  name: PageTrashed
  summary: A page has been moved to the trash in Confluence.
  title: Page Trashed
- description: ''
  name: PageRestored
  summary: A page has been restored from the trash in Confluence.
  title: Page Restored
- description: ''
  name: SpaceCreated
  summary: A new space has been created in Confluence.
  title: Space Created
- description: ''
  name: SpaceUpdated
  summary: A space has been updated in Confluence.
  title: Space Updated
- description: ''
  name: SpaceRemoved
  summary: A space has been removed from Confluence.
  title: Space Removed
- description: ''
  name: CommentCreated
  summary: A new comment has been added to a page or blog post.
  title: Comment Created
- description: ''
  name: CommentUpdated
  summary: A comment has been updated on a page or blog post.
  title: Comment Updated
- description: ''
  name: CommentRemoved
  summary: A comment has been removed from a page or blog post.
  title: Comment Removed
- description: ''
  name: AttachmentCreated
  summary: A file has been attached to a page or blog post.
  title: Attachment Created
- description: ''
  name: AttachmentUpdated
  summary: An attachment has been updated with a new version.
  title: Attachment Updated
- description: ''
  name: AttachmentRemoved
  summary: An attachment has been removed from content.
  title: Attachment Removed
- description: ''
  name: LabelCreated
  summary: A label has been added to content.
  title: Label Created
- description: ''
  name: LabelRemoved
  summary: A label has been removed from content.
  title: Label Removed
- description: ''
  name: BlogCreated
  summary: A new blog post has been created in Confluence.
  title: Blog Post Created
- description: ''
  name: BlogUpdated
  summary: A blog post has been updated in Confluence.
  title: Blog Post Updated
- description: ''
  name: BlogRemoved
  summary: A blog post has been removed from Confluence.
  title: Blog Post Removed
name: Confluence Cloud Webhooks
provider_name: Confluence
provider_slug: confluence
servers:
- description: Your application endpoint that receives webhook callbacks from Confluence Cloud. This URL is configured when registering the webhook.
  name: webhookReceiver
  protocol: https
  url: ''
slug: confluence-webhooks
source_filename: confluence-webhooks.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 3.0.0\ninfo:\n  title: Confluence Cloud Webhooks\n  version: 1.0.0\n  description: >-\n    Asynchronous event notifications from Confluence Cloud. Webhooks allow\n    applications to receive real-time notifications when content, spaces, or\n    other entities are created, updated, or deleted in Confluence. Webhooks\n    can be registered through the Confluence UI, REST API, or via Atlassian\n    Connect app descriptors.\n  contact:\n    name: Atlassian\n    url: https://developer.atlassian.com/cloud/confluence/\n    email: ecosystem@atlassian.com\n  license:\n    name: Atlassian Developer Terms\n    url: https://developer.atlassian.com/platform/marketplace/atlassian-developer-terms/\n  externalDocs:\n    description: Confluence Webhooks Documentation\n    url: https://developer.atlassian.com/cloud/confluence/using-webhooks/\n  tags:\n    - name: content\n      description: Events related to Confluence content (pages, blog posts)\n    - name: space\n      description:\
  \ Events related to Confluence spaces\n    - name: comment\n      description: Events related to comments on content\n    - name: attachment\n      description: Events related to file attachments\n    - name: label\n      description: Events related to labels\n    - name: user\n      description: Events related to user actions\nservers:\n  webhookReceiver:\n    host: your-app.example.com\n    protocol: https\n    description: >-\n      Your application endpoint that receives webhook callbacks from\n      Confluence Cloud. This URL is configured when registering the webhook.\n    security:\n      - $ref: '#/components/securitySchemes/webhookSecret'\nchannels:\n  pageCreated:\n    address: /webhooks/confluence\n    description: Channel for page_created events\n    messages:\n      pageCreated:\n        $ref: '#/components/messages/PageCreated'\n  pageUpdated:\n    address: /webhooks/confluence\n    description: Channel for page_updated events\n    messages:\n      pageUpdated:\n        $ref:\
  \ '#/components/messages/PageUpdated'\n  pageRemoved:\n    address: /webhooks/confluence\n    description: Channel for page_removed events\n    messages:\n      pageRemoved:\n        $ref: '#/components/messages/PageRemoved'\n  pageTrashed:\n    address: /webhooks/confluence\n    description: Channel for page_trashed events\n    messages:\n      pageTrashed:\n        $ref: '#/components/messages/PageTrashed'\n  pageRestored:\n    address: /webhooks/confluence\n    description: Channel for page_restored events\n    messages:\n      pageRestored:\n        $ref: '#/components/messages/PageRestored'\n  spaceCreated:\n    address: /webhooks/confluence\n    description: Channel for space_created events\n    messages:\n      spaceCreated:\n        $ref: '#/components/messages/SpaceCreated'\n  spaceUpdated:\n    address: /webhooks/confluence\n    description: Channel for space_updated events\n    messages:\n      spaceUpdated:\n        $ref: '#/components/messages/SpaceUpdated'\n  spaceRemoved:\n\
  \    address: /webhooks/confluence\n    description: Channel for space_removed events\n    messages:\n      spaceRemoved:\n        $ref: '#/components/messages/SpaceRemoved'\n  commentCreated:\n    address: /webhooks/confluence\n    description: Channel for comment_created events\n    messages:\n      commentCreated:\n        $ref: '#/components/messages/CommentCreated'\n  commentUpdated:\n    address: /webhooks/confluence\n    description: Channel for comment_updated events\n    messages:\n      commentUpdated:\n        $ref: '#/components/messages/CommentUpdated'\n  commentRemoved:\n    address: /webhooks/confluence\n    description: Channel for comment_removed events\n    messages:\n      commentRemoved:\n        $ref: '#/components/messages/CommentRemoved'\n  attachmentCreated:\n    address: /webhooks/confluence\n    description: Channel for attachment_created events\n    messages:\n      attachmentCreated:\n        $ref: '#/components/messages/AttachmentCreated'\n  attachmentUpdated:\n\
  \    address: /webhooks/confluence\n    description: Channel for attachment_updated events\n    messages:\n      attachmentUpdated:\n        $ref: '#/components/messages/AttachmentUpdated'\n  attachmentRemoved:\n    address: /webhooks/confluence\n    description: Channel for attachment_removed events\n    messages:\n      attachmentRemoved:\n        $ref: '#/components/messages/AttachmentRemoved'\n  labelCreated:\n    address: /webhooks/confluence\n    description: Channel for label_created events\n    messages:\n      labelCreated:\n        $ref: '#/components/messages/LabelCreated'\n  labelRemoved:\n    address: /webhooks/confluence\n    description: Channel for label_removed events\n    messages:\n      labelRemoved:\n        $ref: '#/components/messages/LabelRemoved'\n  blogCreated:\n    address: /webhooks/confluence\n    description: Channel for blog_created events\n    messages:\n      blogCreated:\n        $ref: '#/components/messages/BlogCreated'\n  blogUpdated:\n    address: /webhooks/confluence\n\
  \    description: Channel for blog_updated events\n    messages:\n      blogUpdated:\n        $ref: '#/components/messages/BlogUpdated'\n  blogRemoved:\n    address: /webhooks/confluence\n    description: Channel for blog_removed events\n    messages:\n      blogRemoved:\n        $ref: '#/components/messages/BlogRemoved'\noperations:\n  onPageCreated:\n    action: receive\n    channel:\n      $ref: '#/channels/pageCreated'\n    title: Page created\n    summary: Triggered when a new page is created in Confluence.\n    tags:\n      - $ref: '#/components/tags/content'\n    messages:\n      - $ref: '#/channels/pageCreated/messages/pageCreated'\n  onPageUpdated:\n    action: receive\n    channel:\n      $ref: '#/channels/pageUpdated'\n    title: Page updated\n    summary: Triggered when an existing page is updated in Confluence.\n    tags:\n      - $ref: '#/components/tags/content'\n    messages:\n      - $ref: '#/channels/pageUpdated/messages/pageUpdated'\n  onPageRemoved:\n    action: receive\n\
  \    channel:\n      $ref: '#/channels/pageRemoved'\n    title: Page removed\n    summary: Triggered when a page is permanently removed from Confluence.\n    tags:\n      - $ref: '#/components/tags/content'\n    messages:\n      - $ref: '#/channels/pageRemoved/messages/pageRemoved'\n  onPageTrashed:\n    action: receive\n    channel:\n      $ref: '#/channels/pageTrashed'\n    title: Page trashed\n    summary: Triggered when a page is moved to the trash.\n    tags:\n      - $ref: '#/components/tags/content'\n    messages:\n      - $ref: '#/channels/pageTrashed/messages/pageTrashed'\n  onPageRestored:\n    action: receive\n    channel:\n      $ref: '#/channels/pageRestored'\n    title: Page restored\n    summary: Triggered when a page is restored from the trash.\n    tags:\n      - $ref: '#/components/tags/content'\n    messages:\n      - $ref: '#/channels/pageRestored/messages/pageRestored'\n  onSpaceCreated:\n    action: receive\n    channel:\n      $ref: '#/channels/spaceCreated'\n  \
  \  title: Space created\n    summary: Triggered when a new space is created in Confluence.\n    tags:\n      - $ref: '#/components/tags/space'\n    messages:\n      - $ref: '#/channels/spaceCreated/messages/spaceCreated'\n  onSpaceUpdated:\n    action: receive\n    channel:\n      $ref: '#/channels/spaceUpdated'\n    title: Space updated\n    summary: Triggered when a space is updated in Confluence.\n    tags:\n      - $ref: '#/components/tags/space'\n    messages:\n      - $ref: '#/channels/spaceUpdated/messages/spaceUpdated'\n  onSpaceRemoved:\n    action: receive\n    channel:\n      $ref: '#/channels/spaceRemoved'\n    title: Space removed\n    summary: Triggered when a space is removed from Confluence.\n    tags:\n      - $ref: '#/components/tags/space'\n    messages:\n      - $ref: '#/channels/spaceRemoved/messages/spaceRemoved'\n  onCommentCreated:\n    action: receive\n    channel:\n      $ref: '#/channels/commentCreated'\n    title: Comment created\n    summary: Triggered when\
  \ a new comment is added to a page or blog post.\n    tags:\n      - $ref: '#/components/tags/comment'\n    messages:\n      - $ref: '#/channels/commentCreated/messages/commentCreated'\n  onCommentUpdated:\n    action: receive\n    channel:\n      $ref: '#/channels/commentUpdated'\n    title: Comment updated\n    summary: Triggered when a comment is updated.\n    tags:\n      - $ref: '#/components/tags/comment'\n    messages:\n      - $ref: '#/channels/commentUpdated/messages/commentUpdated'\n  onCommentRemoved:\n    action: receive\n    channel:\n      $ref: '#/channels/commentRemoved'\n    title: Comment removed\n    summary: Triggered when a comment is removed.\n    tags:\n      - $ref: '#/components/tags/comment'\n    messages:\n      - $ref: '#/channels/commentRemoved/messages/commentRemoved'\n  onAttachmentCreated:\n    action: receive\n    channel:\n      $ref: '#/channels/attachmentCreated'\n    title: Attachment created\n    summary: Triggered when a file is attached to a page\
  \ or blog post.\n    tags:\n      - $ref: '#/components/tags/attachment'\n    messages:\n      - $ref: '#/channels/attachmentCreated/messages/attachmentCreated'\n  onAttachmentUpdated:\n    action: receive\n    channel:\n      $ref: '#/channels/attachmentUpdated'\n    title: Attachment updated\n    summary: Triggered when an attachment is updated with a new version.\n    tags:\n      - $ref: '#/components/tags/attachment'\n    messages:\n      - $ref: '#/channels/attachmentUpdated/messages/attachmentUpdated'\n  onAttachmentRemoved:\n    action: receive\n    channel:\n      $ref: '#/channels/attachmentRemoved'\n    title: Attachment removed\n    summary: Triggered when an attachment is removed from content.\n    tags:\n      - $ref: '#/components/tags/attachment'\n    messages:\n      - $ref: '#/channels/attachmentRemoved/messages/attachmentRemoved'\n  onLabelCreated:\n    action: receive\n    channel:\n      $ref: '#/channels/labelCreated'\n    title: Label created\n    summary: Triggered\
  \ when a label is added to content.\n    tags:\n      - $ref: '#/components/tags/label'\n    messages:\n      - $ref: '#/channels/labelCreated/messages/labelCreated'\n  onLabelRemoved:\n    action: receive\n    channel:\n      $ref: '#/channels/labelRemoved'\n    title: Label removed\n    summary: Triggered when a label is removed from content.\n    tags:\n      - $ref: '#/components/tags/label'\n    messages:\n      - $ref: '#/channels/labelRemoved/messages/labelRemoved'\n  onBlogCreated:\n    action: receive\n    channel:\n      $ref: '#/channels/blogCreated'\n    title: Blog post created\n    summary: Triggered when a new blog post is created.\n    tags:\n      - $ref: '#/components/tags/content'\n    messages:\n      - $ref: '#/channels/blogCreated/messages/blogCreated'\n  onBlogUpdated:\n    action: receive\n    channel:\n      $ref: '#/channels/blogUpdated'\n    title: Blog post updated\n    summary: Triggered when a blog post is updated.\n    tags:\n      - $ref: '#/components/tags/content'\n\
  \    messages:\n      - $ref: '#/channels/blogUpdated/messages/blogUpdated'\n  onBlogRemoved:\n    action: receive\n    channel:\n      $ref: '#/channels/blogRemoved'\n    title: Blog post removed\n    summary: Triggered when a blog post is removed.\n    tags:\n      - $ref: '#/components/tags/content'\n    messages:\n      - $ref: '#/channels/blogRemoved/messages/blogRemoved'\ncomponents:\n  tags:\n    content:\n      name: content\n      description: Events related to Confluence content\n    space:\n      name: space\n      description: Events related to Confluence spaces\n    comment:\n      name: comment\n      description: Events related to comments\n    attachment:\n      name: attachment\n      description: Events related to attachments\n    label:\n      name: label\n      description: Events related to labels\n  securitySchemes:\n    webhookSecret:\n      type: httpApiKey\n      name: X-Hub-Signature\n      in: header\n      description: >-\n        HMAC-SHA256 signature of the\
  \ webhook payload, computed using\n        the shared secret configured when registering the webhook.\n  messages:\n    PageCreated:\n      name: page_created\n      title: Page Created\n      summary: A new page has been created in Confluence.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/PageEvent'\n    PageUpdated:\n      name: page_updated\n      title: Page Updated\n      summary: An existing page has been updated in Confluence.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/PageEvent'\n    PageRemoved:\n      name: page_removed\n      title: Page Removed\n      summary: A page has been permanently removed from Confluence.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/PageEvent'\n\
  \    PageTrashed:\n      name: page_trashed\n      title: Page Trashed\n      summary: A page has been moved to the trash in Confluence.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/PageEvent'\n    PageRestored:\n      name: page_restored\n      title: Page Restored\n      summary: A page has been restored from the trash in Confluence.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/PageEvent'\n    SpaceCreated:\n      name: space_created\n      title: Space Created\n      summary: A new space has been created in Confluence.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/SpaceEvent'\n    SpaceUpdated:\n      name: space_updated\n      title: Space Updated\n\
  \      summary: A space has been updated in Confluence.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/SpaceEvent'\n    SpaceRemoved:\n      name: space_removed\n      title: Space Removed\n      summary: A space has been removed from Confluence.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/SpaceEvent'\n    CommentCreated:\n      name: comment_created\n      title: Comment Created\n      summary: A new comment has been added to a page or blog post.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/CommentEvent'\n    CommentUpdated:\n      name: comment_updated\n      title: Comment Updated\n      summary: A comment has been updated on a page or blog post.\n\
  \      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/CommentEvent'\n    CommentRemoved:\n      name: comment_removed\n      title: Comment Removed\n      summary: A comment has been removed from a page or blog post.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/CommentEvent'\n    AttachmentCreated:\n      name: attachment_created\n      title: Attachment Created\n      summary: A file has been attached to a page or blog post.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/AttachmentEvent'\n    AttachmentUpdated:\n      name: attachment_updated\n      title: Attachment Updated\n      summary: An attachment has been updated with a new version.\n      contentType:\
  \ application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/AttachmentEvent'\n    AttachmentRemoved:\n      name: attachment_removed\n      title: Attachment Removed\n      summary: An attachment has been removed from content.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/AttachmentEvent'\n    LabelCreated:\n      name: label_created\n      title: Label Created\n      summary: A label has been added to content.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/LabelEvent'\n    LabelRemoved:\n      name: label_removed\n      title: Label Removed\n      summary: A label has been removed from content.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n\
  \      payload:\n        $ref: '#/components/schemas/LabelEvent'\n    BlogCreated:\n      name: blog_created\n      title: Blog Post Created\n      summary: A new blog post has been created in Confluence.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/BlogPostEvent'\n    BlogUpdated:\n      name: blog_updated\n      title: Blog Post Updated\n      summary: A blog post has been updated in Confluence.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/BlogPostEvent'\n    BlogRemoved:\n      name: blog_removed\n      title: Blog Post Removed\n      summary: A blog post has been removed from Confluence.\n      contentType: application/json\n      headers:\n        $ref: '#/components/schemas/WebhookHeaders'\n      payload:\n        $ref: '#/components/schemas/BlogPostEvent'\n\
  \  schemas:\n    WebhookHeaders:\n      type: object\n      properties:\n        X-Atlassian-Webhook-Identifier:\n          type: string\n          description: Unique identifier for this webhook registration.\n        X-Hub-Signature:\n          type: string\n          description: HMAC-SHA256 signature of the request body.\n        Content-Type:\n          type: string\n          enum:\n            - application/json\n    WebhookBase:\n      type: object\n      description: Common fields present in all Confluence webhook payloads.\n      properties:\n        timestamp:\n          type: integer\n          format: int64\n          description: Unix timestamp in milliseconds when the event occurred.\n        event:\n          type: string\n          description: The event type identifier.\n        userAccountId:\n          type: string\n          description: The Atlassian account ID of the user who triggered the event.\n    PageEvent:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n\
  \        - type: object\n          properties:\n            event:\n              type: string\n              enum:\n                - page_created\n                - page_updated\n                - page_removed\n                - page_trashed\n                - page_restored\n            page:\n              $ref: '#/components/schemas/PagePayload'\n    PagePayload:\n      type: object\n      description: Page data included in webhook payloads.\n      properties:\n        id:\n          type: string\n          description: The unique identifier of the page.\n        type:\n          type: string\n          description: The content type, always \"page\" for pages.\n          enum:\n            - page\n        status:\n          type: string\n          description: The status of the page.\n          enum:\n            - current\n            - draft\n            - trashed\n        title:\n          type: string\n          description: The title of the page.\n        spaceKey:\n         \
  \ type: string\n          description: The key of the space the page belongs to.\n        version:\n          type: object\n          properties:\n            number:\n              type: integer\n              description: The version number.\n            when:\n              type: string\n              format: date-time\n              description: Timestamp of this version.\n            message:\n              type: string\n              description: Version message.\n            minorEdit:\n              type: boolean\n              description: Whether this was a minor edit.\n        creatorAccountId:\n          type: string\n          description: Atlassian account ID of the page creator.\n        lastModifierAccountId:\n          type: string\n          description: Atlassian account ID of the last modifier.\n        self:\n          type: string\n          format: uri\n          description: The REST API URL for this page.\n    SpaceEvent:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n\
  \        - type: object\n          properties:\n            event:\n              type: string\n              enum:\n                - space_created\n                - space_updated\n                - space_removed\n            space:\n              $ref: '#/components/schemas/SpacePayload'\n    SpacePayload:\n      type: object\n      description: Space data included in webhook payloads.\n      properties:\n        id:\n          type: integer\n          format: int64\n          description: The unique identifier of the space.\n        key:\n          type: string\n          description: The key of the space.\n        name:\n          type: string\n          description: The name of the space.\n        type:\n          type: string\n          description: The type of space.\n          enum:\n            - global\n            - personal\n        status:\n          type: string\n          description: The status of the space.\n          enum:\n            - current\n            - archived\n\
  \        creatorAccountId:\n          type: string\n          description: Atlassian account ID of the space creator.\n        self:\n          type: string\n          format: uri\n          description: The REST API URL for this space.\n    CommentEvent:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type: object\n          properties:\n            event:\n              type: string\n              enum:\n                - comment_created\n                - comment_updated\n                - comment_removed\n            comment:\n              $ref: '#/components/schemas/CommentPayload'\n    CommentPayload:\n      type: object\n      description: Comment data included in webhook payloads.\n      properties:\n        id:\n          type: string\n          description: The unique identifier of the comment.\n        type:\n          type: string\n          description: The content type.\n          enum:\n            - comment\n        status:\n          type:\
  \ string\n          description: The status of the comment.\n          enum:\n            - current\n            - trashed\n        title:\n          type: string\n          description: The title of the comment.\n        version:\n          type: object\n          properties:\n            number:\n              type: integer\n            when:\n              type: string\n              format: date-time\n        container:\n          type: object\n          description: The content the comment is on.\n          properties:\n            id:\n              type: string\n            type:\n              type: string\n              enum:\n                - page\n                - blogpost\n                - comment\n            title:\n              type: string\n        creatorAccountId:\n          type: string\n          description: Atlassian account ID of the comment creator.\n        self:\n          type: string\n          format: uri\n          description: The REST API URL for this\
  \ comment.\n    AttachmentEvent:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type: object\n          properties:\n            event:\n              type: string\n              enum:\n                - attachment_created\n                - attachment_updated\n                - attachment_removed\n            attachment:\n              $ref: '#/components/schemas/AttachmentPayload'\n    AttachmentPayload:\n      type: object\n      description: Attachment data included in webhook payloads.\n      properties:\n        id:\n          type: string\n          description: The unique identifier of the attachment.\n        type:\n          type: string\n          enum:\n            - attachment\n        status:\n          type: string\n          enum:\n            - current\n            - trashed\n        title:\n          type: string\n          description: The filename of the attachment.\n        mediaType:\n          type: string\n          description: The\
  \ MIME type of the attachment.\n        fileSize:\n          type: integer\n          format: int64\n          description: The file size in bytes.\n        container:\n          type: object\n          description: The content the attachment is on.\n          properties:\n            id:\n              type: string\n            type:\n              type: string\n              enum:\n                - page\n                - blogpost\n            title:\n              type: string\n        creatorAccountId:\n          type: string\n        self:\n          type: string\n          format: uri\n    LabelEvent:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type: object\n          properties:\n            event:\n              type: string\n              enum:\n                - label_created\n                - label_removed\n            label:\n              type: object\n              properties:\n                name:\n                  type: string\n    \
  \              description: The name of the label.\n                prefix:\n                  type: string\n                  description: The prefix of the label.\n            associatedContent:\n              type: object\n              description: The content the label was added to or removed from.\n              properties:\n                id:\n                  type: string\n                type:\n                  type: string\n                  enum:\n                    - page\n                    - blogpost\n                title:\n                  type: string\n    BlogPostEvent:\n      allOf:\n        - $ref: '#/components/schemas/WebhookBase'\n        - type: object\n          properties:\n            event:\n              type: string\n              enum:\n                - blog_created\n                - blog_updated\n                - blog_removed\n            blogPost:\n              $ref: '#/components/schemas/BlogPostPayload'\n    BlogPostPayload:\n      type: object\n\
  \      description: Blog post data included in webhook payloads.\n      properties:\n        id:\n          type: string\n          description: The unique identifier of the blog post.\n        type:\n          type: string\n          enum:\n            - blogpost\n        status:\n          type: string\n          enum:\n            - current\n            - draft\n            - trashed\n        title:\n          type: string\n          description: The title of the blog post.\n        spaceKey:\n          type: string\n          description: The key of the space the blog post belongs to.\n        version:\n          type: object\n          properties:\n            number:\n              type: integer\n            when:\n              type: string\n              format: date-time\n            message:\n              type: string\n            minorEdit:\n              type: boolean\n        creatorAccountId:\n          type: string\n        lastModifierAccountId:\n          type: string\n\
  \        self:\n          type: string\n          format: uri\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/confluence/refs/heads/main/asyncapi/confluence-webhooks.yml
spec_file: asyncapi/confluence-webhooks.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/confluence/refs/heads/main/asyncapi/confluence-webhooks.yml
tags:
- Collaboration
- Content Management
- Documentation
- Knowledge Base
- Wiki
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
