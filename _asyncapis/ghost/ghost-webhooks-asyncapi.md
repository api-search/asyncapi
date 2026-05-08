---
channels:
- description: Triggered whenever any content changes in the site data or settings. This is a catch-all event useful for triggering site rebuilds or cache invalidation.
  name: /webhook/site.changed
  operation: publish
  operation_id: onSiteChanged
  summary: Site content or settings changed
- description: Triggered whenever a new post is created in Ghost, regardless of its publication status.
  name: /webhook/post.added
  operation: publish
  operation_id: onPostAdded
  summary: New post created
- description: Triggered whenever a post is permanently deleted from Ghost.
  name: /webhook/post.deleted
  operation: publish
  operation_id: onPostDeleted
  summary: Post deleted
- description: Triggered whenever a post is edited in Ghost.
  name: /webhook/post.edited
  operation: publish
  operation_id: onPostEdited
  summary: Post edited
- description: Triggered whenever a post transitions to the published status.
  name: /webhook/post.published
  operation: publish
  operation_id: onPostPublished
  summary: Post published
- description: Triggered whenever a previously published post is edited while remaining in the published state.
  name: /webhook/post.published.edited
  operation: publish
  operation_id: onPostPublishedEdited
  summary: Published post edited
- description: Triggered whenever a published post is unpublished (reverted to draft).
  name: /webhook/post.unpublished
  operation: publish
  operation_id: onPostUnpublished
  summary: Post unpublished
- description: Triggered whenever a post is scheduled for future publication.
  name: /webhook/post.scheduled
  operation: publish
  operation_id: onPostScheduled
  summary: Post scheduled
- description: Triggered whenever a scheduled post is unscheduled.
  name: /webhook/post.unscheduled
  operation: publish
  operation_id: onPostUnscheduled
  summary: Post unscheduled
- description: Triggered whenever a scheduled post has its publication date changed.
  name: /webhook/post.rescheduled
  operation: publish
  operation_id: onPostRescheduled
  summary: Post rescheduled
- description: Triggered whenever a new page is created in Ghost.
  name: /webhook/page.added
  operation: publish
  operation_id: onPageAdded
  summary: New page created
- description: Triggered whenever a page is permanently deleted from Ghost.
  name: /webhook/page.deleted
  operation: publish
  operation_id: onPageDeleted
  summary: Page deleted
- description: Triggered whenever a page is edited in Ghost.
  name: /webhook/page.edited
  operation: publish
  operation_id: onPageEdited
  summary: Page edited
- description: Triggered whenever a page transitions to the published status.
  name: /webhook/page.published
  operation: publish
  operation_id: onPagePublished
  summary: Page published
- description: Triggered whenever a published page is edited while remaining published.
  name: /webhook/page.published.edited
  operation: publish
  operation_id: onPagePublishedEdited
  summary: Published page edited
- description: Triggered whenever a published page is unpublished.
  name: /webhook/page.unpublished
  operation: publish
  operation_id: onPageUnpublished
  summary: Page unpublished
- description: Triggered whenever a page is scheduled for future publication.
  name: /webhook/page.scheduled
  operation: publish
  operation_id: onPageScheduled
  summary: Page scheduled
- description: Triggered whenever a scheduled page is unscheduled.
  name: /webhook/page.unscheduled
  operation: publish
  operation_id: onPageUnscheduled
  summary: Page unscheduled
- description: Triggered whenever a scheduled page has its publication date changed.
  name: /webhook/page.rescheduled
  operation: publish
  operation_id: onPageRescheduled
  summary: Page rescheduled
- description: Triggered whenever a new tag is created in Ghost.
  name: /webhook/tag.added
  operation: publish
  operation_id: onTagAdded
  summary: New tag created
- description: Triggered whenever a tag is edited in Ghost.
  name: /webhook/tag.edited
  operation: publish
  operation_id: onTagEdited
  summary: Tag edited
- description: Triggered whenever a tag is deleted from Ghost.
  name: /webhook/tag.deleted
  operation: publish
  operation_id: onTagDeleted
  summary: Tag deleted
- description: Triggered whenever a tag is attached to a post.
  name: /webhook/post.tag.attached
  operation: publish
  operation_id: onPostTagAttached
  summary: Tag attached to post
- description: Triggered whenever a tag is detached from a post.
  name: /webhook/post.tag.detached
  operation: publish
  operation_id: onPostTagDetached
  summary: Tag detached from post
- description: Triggered whenever a tag is attached to a page.
  name: /webhook/page.tag.attached
  operation: publish
  operation_id: onPageTagAttached
  summary: Tag attached to page
- description: Triggered whenever a tag is detached from a page.
  name: /webhook/page.tag.detached
  operation: publish
  operation_id: onPageTagDetached
  summary: Tag detached from page
- description: Triggered whenever a new member signs up for the publication.
  name: /webhook/member.added
  operation: publish
  operation_id: onMemberAdded
  summary: New member signed up
- description: Triggered whenever a member record is updated.
  name: /webhook/member.edited
  operation: publish
  operation_id: onMemberEdited
  summary: Member updated
- description: Triggered whenever a member is deleted from the publication.
  name: /webhook/member.deleted
  operation: publish
  operation_id: onMemberDeleted
  summary: Member deleted
description: Ghost Webhooks allow developers to receive real-time HTTP notifications when specific events occur within a Ghost publication, such as publishing a new post, updating a page, or gaining a new member. Webhooks can be configured through the Ghost Admin interface under custom integrations or created programmatically via the Admin API. The webhook sends an HTTP POST request to the configured target URL with a JSON payload containing the relevant resource data.
layout: asyncapi
messages:
- description: ''
  name: SiteChangedEvent
  summary: Notification that site content or settings have been modified.
  title: Site Changed Event
- description: ''
  name: PostEvent
  summary: Notification containing post data when a post-related event occurs.
  title: Post Event
- description: ''
  name: PageEvent
  summary: Notification containing page data when a page-related event occurs.
  title: Page Event
- description: ''
  name: TagEvent
  summary: Notification containing tag data when a tag-related event occurs.
  title: Tag Event
- description: ''
  name: TagAttachmentEvent
  summary: Notification when a tag is attached to or detached from a post or page.
  title: Tag Attachment Event
- description: ''
  name: MemberEvent
  summary: Notification containing member data when a member-related event occurs.
  title: Member Event
name: Ghost Webhooks
provider_name: Ghost
provider_slug: ghost
servers:
- description: Your server that receives webhook HTTP POST requests from Ghost. The URL is configured when creating a webhook via the Ghost Admin UI or Admin API.
  name: yourServer
  protocol: https
  url: '{webhookTargetUrl}'
slug: ghost-webhooks-asyncapi
source_filename: ghost-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Ghost Webhooks\n  description: >-\n    Ghost Webhooks allow developers to receive real-time HTTP notifications when\n    specific events occur within a Ghost publication, such as publishing a new\n    post, updating a page, or gaining a new member. Webhooks can be configured\n    through the Ghost Admin interface under custom integrations or created\n    programmatically via the Admin API. The webhook sends an HTTP POST request to\n    the configured target URL with a JSON payload containing the relevant\n    resource data.\n  version: '5.0'\n  contact:\n    name: Ghost Foundation\n    url: https://ghost.org/docs/webhooks/\n  license:\n    name: MIT\n    url: https://github.com/TryGhost/Ghost/blob/main/LICENSE\nexternalDocs:\n  description: Ghost Webhooks Documentation\n  url: https://ghost.org/docs/webhooks/\nservers:\n  yourServer:\n    url: '{webhookTargetUrl}'\n    protocol: https\n    description: >-\n      Your server that receives webhook\
  \ HTTP POST requests from Ghost. The URL\n      is configured when creating a webhook via the Ghost Admin UI or Admin API.\n    variables:\n      webhookTargetUrl:\n        description: The target URL configured for the webhook\n    security:\n      - webhookSecret: []\nchannels:\n  /webhook/site.changed:\n    description: >-\n      Triggered whenever any content changes in the site data or settings. This\n      is a catch-all event useful for triggering site rebuilds or cache\n      invalidation.\n    publish:\n      operationId: onSiteChanged\n      summary: Site content or settings changed\n      message:\n        $ref: '#/components/messages/SiteChangedEvent'\n  /webhook/post.added:\n    description: >-\n      Triggered whenever a new post is created in Ghost, regardless of its\n      publication status.\n    publish:\n      operationId: onPostAdded\n      summary: New post created\n      message:\n        $ref: '#/components/messages/PostEvent'\n  /webhook/post.deleted:\n    description:\
  \ >-\n      Triggered whenever a post is permanently deleted from Ghost.\n    publish:\n      operationId: onPostDeleted\n      summary: Post deleted\n      message:\n        $ref: '#/components/messages/PostEvent'\n  /webhook/post.edited:\n    description: >-\n      Triggered whenever a post is edited in Ghost.\n    publish:\n      operationId: onPostEdited\n      summary: Post edited\n      message:\n        $ref: '#/components/messages/PostEvent'\n  /webhook/post.published:\n    description: >-\n      Triggered whenever a post transitions to the published status.\n    publish:\n      operationId: onPostPublished\n      summary: Post published\n      message:\n        $ref: '#/components/messages/PostEvent'\n  /webhook/post.published.edited:\n    description: >-\n      Triggered whenever a previously published post is edited while remaining\n      in the published state.\n    publish:\n      operationId: onPostPublishedEdited\n      summary: Published post edited\n      message:\n  \
  \      $ref: '#/components/messages/PostEvent'\n  /webhook/post.unpublished:\n    description: >-\n      Triggered whenever a published post is unpublished (reverted to draft).\n    publish:\n      operationId: onPostUnpublished\n      summary: Post unpublished\n      message:\n        $ref: '#/components/messages/PostEvent'\n  /webhook/post.scheduled:\n    description: >-\n      Triggered whenever a post is scheduled for future publication.\n    publish:\n      operationId: onPostScheduled\n      summary: Post scheduled\n      message:\n        $ref: '#/components/messages/PostEvent'\n  /webhook/post.unscheduled:\n    description: >-\n      Triggered whenever a scheduled post is unscheduled.\n    publish:\n      operationId: onPostUnscheduled\n      summary: Post unscheduled\n      message:\n        $ref: '#/components/messages/PostEvent'\n  /webhook/post.rescheduled:\n    description: >-\n      Triggered whenever a scheduled post has its publication date changed.\n    publish:\n    \
  \  operationId: onPostRescheduled\n      summary: Post rescheduled\n      message:\n        $ref: '#/components/messages/PostEvent'\n  /webhook/page.added:\n    description: >-\n      Triggered whenever a new page is created in Ghost.\n    publish:\n      operationId: onPageAdded\n      summary: New page created\n      message:\n        $ref: '#/components/messages/PageEvent'\n  /webhook/page.deleted:\n    description: >-\n      Triggered whenever a page is permanently deleted from Ghost.\n    publish:\n      operationId: onPageDeleted\n      summary: Page deleted\n      message:\n        $ref: '#/components/messages/PageEvent'\n  /webhook/page.edited:\n    description: >-\n      Triggered whenever a page is edited in Ghost.\n    publish:\n      operationId: onPageEdited\n      summary: Page edited\n      message:\n        $ref: '#/components/messages/PageEvent'\n  /webhook/page.published:\n    description: >-\n      Triggered whenever a page transitions to the published status.\n    publish:\n\
  \      operationId: onPagePublished\n      summary: Page published\n      message:\n        $ref: '#/components/messages/PageEvent'\n  /webhook/page.published.edited:\n    description: >-\n      Triggered whenever a published page is edited while remaining published.\n    publish:\n      operationId: onPagePublishedEdited\n      summary: Published page edited\n      message:\n        $ref: '#/components/messages/PageEvent'\n  /webhook/page.unpublished:\n    description: >-\n      Triggered whenever a published page is unpublished.\n    publish:\n      operationId: onPageUnpublished\n      summary: Page unpublished\n      message:\n        $ref: '#/components/messages/PageEvent'\n  /webhook/page.scheduled:\n    description: >-\n      Triggered whenever a page is scheduled for future publication.\n    publish:\n      operationId: onPageScheduled\n      summary: Page scheduled\n      message:\n        $ref: '#/components/messages/PageEvent'\n  /webhook/page.unscheduled:\n    description:\
  \ >-\n      Triggered whenever a scheduled page is unscheduled.\n    publish:\n      operationId: onPageUnscheduled\n      summary: Page unscheduled\n      message:\n        $ref: '#/components/messages/PageEvent'\n  /webhook/page.rescheduled:\n    description: >-\n      Triggered whenever a scheduled page has its publication date changed.\n    publish:\n      operationId: onPageRescheduled\n      summary: Page rescheduled\n      message:\n        $ref: '#/components/messages/PageEvent'\n  /webhook/tag.added:\n    description: >-\n      Triggered whenever a new tag is created in Ghost.\n    publish:\n      operationId: onTagAdded\n      summary: New tag created\n      message:\n        $ref: '#/components/messages/TagEvent'\n  /webhook/tag.edited:\n    description: >-\n      Triggered whenever a tag is edited in Ghost.\n    publish:\n      operationId: onTagEdited\n      summary: Tag edited\n      message:\n        $ref: '#/components/messages/TagEvent'\n  /webhook/tag.deleted:\n    description:\
  \ >-\n      Triggered whenever a tag is deleted from Ghost.\n    publish:\n      operationId: onTagDeleted\n      summary: Tag deleted\n      message:\n        $ref: '#/components/messages/TagEvent'\n  /webhook/post.tag.attached:\n    description: >-\n      Triggered whenever a tag is attached to a post.\n    publish:\n      operationId: onPostTagAttached\n      summary: Tag attached to post\n      message:\n        $ref: '#/components/messages/TagAttachmentEvent'\n  /webhook/post.tag.detached:\n    description: >-\n      Triggered whenever a tag is detached from a post.\n    publish:\n      operationId: onPostTagDetached\n      summary: Tag detached from post\n      message:\n        $ref: '#/components/messages/TagAttachmentEvent'\n  /webhook/page.tag.attached:\n    description: >-\n      Triggered whenever a tag is attached to a page.\n    publish:\n      operationId: onPageTagAttached\n      summary: Tag attached to page\n      message:\n        $ref: '#/components/messages/TagAttachmentEvent'\n\
  \  /webhook/page.tag.detached:\n    description: >-\n      Triggered whenever a tag is detached from a page.\n    publish:\n      operationId: onPageTagDetached\n      summary: Tag detached from page\n      message:\n        $ref: '#/components/messages/TagAttachmentEvent'\n  /webhook/member.added:\n    description: >-\n      Triggered whenever a new member signs up for the publication.\n    publish:\n      operationId: onMemberAdded\n      summary: New member signed up\n      message:\n        $ref: '#/components/messages/MemberEvent'\n  /webhook/member.edited:\n    description: >-\n      Triggered whenever a member record is updated.\n    publish:\n      operationId: onMemberEdited\n      summary: Member updated\n      message:\n        $ref: '#/components/messages/MemberEvent'\n  /webhook/member.deleted:\n    description: >-\n      Triggered whenever a member is deleted from the publication.\n    publish:\n      operationId: onMemberDeleted\n      summary: Member deleted\n      message:\n\
  \        $ref: '#/components/messages/MemberEvent'\ncomponents:\n  securitySchemes:\n    webhookSecret:\n      type: httpApiKey\n      name: X-Ghost-Signature\n      in: header\n      description: >-\n        HMAC-SHA256 signature computed from the request body using the webhook\n        secret. The header contains both the signature and a timestamp in the\n        format sha256=SIGNATURE, t=TIMESTAMP.\n  messages:\n    SiteChangedEvent:\n      name: SiteChangedEvent\n      title: Site Changed Event\n      summary: >-\n        Notification that site content or settings have been modified.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SiteChangedPayload'\n    PostEvent:\n      name: PostEvent\n      title: Post Event\n      summary: >-\n        Notification containing post data when a post-related event occurs.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PostPayload'\n    PageEvent:\n      name: PageEvent\n\
  \      title: Page Event\n      summary: >-\n        Notification containing page data when a page-related event occurs.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PagePayload'\n    TagEvent:\n      name: TagEvent\n      title: Tag Event\n      summary: >-\n        Notification containing tag data when a tag-related event occurs.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TagPayload'\n    TagAttachmentEvent:\n      name: TagAttachmentEvent\n      title: Tag Attachment Event\n      summary: >-\n        Notification when a tag is attached to or detached from a post or page.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TagAttachmentPayload'\n    MemberEvent:\n      name: MemberEvent\n      title: Member Event\n      summary: >-\n        Notification containing member data when a member-related event occurs.\n      contentType: application/json\n      payload:\n\
  \        $ref: '#/components/schemas/MemberPayload'\n  schemas:\n    SiteChangedPayload:\n      type: object\n      description: >-\n        Payload for site.changed events. This event does not include resource\n        data as it represents a general site change notification.\n      properties: {}\n    PostPayload:\n      type: object\n      description: >-\n        Payload containing post data delivered via webhook when a post event\n        occurs.\n      properties:\n        post:\n          type: object\n          description: The post resource that triggered the event\n          properties:\n            current:\n              $ref: '#/components/schemas/PostResource'\n            previous:\n              description: >-\n                Previous version of the post for edit events, containing only\n                changed fields\n              oneOf:\n                - $ref: '#/components/schemas/PostResource'\n                - type: object\n    PagePayload:\n      type: object\n\
  \      description: >-\n        Payload containing page data delivered via webhook when a page event\n        occurs.\n      properties:\n        page:\n          type: object\n          description: The page resource that triggered the event\n          properties:\n            current:\n              $ref: '#/components/schemas/PostResource'\n            previous:\n              description: >-\n                Previous version of the page for edit events, containing only\n                changed fields\n              oneOf:\n                - $ref: '#/components/schemas/PostResource'\n                - type: object\n    TagPayload:\n      type: object\n      description: >-\n        Payload containing tag data delivered via webhook when a tag event\n        occurs.\n      properties:\n        tag:\n          type: object\n          description: The tag resource that triggered the event\n          properties:\n            current:\n              $ref: '#/components/schemas/TagResource'\n\
  \            previous:\n              description: Previous version of the tag for edit events\n              oneOf:\n                - $ref: '#/components/schemas/TagResource'\n                - type: object\n    TagAttachmentPayload:\n      type: object\n      description: >-\n        Payload containing data about a tag being attached to or detached from\n        a post or page.\n      properties:\n        tag:\n          type: object\n          description: The tag and the content it was attached to or detached from\n          properties:\n            current:\n              $ref: '#/components/schemas/TagResource'\n    MemberPayload:\n      type: object\n      description: >-\n        Payload containing member data delivered via webhook when a member event\n        occurs.\n      properties:\n        member:\n          type: object\n          description: The member resource that triggered the event\n          properties:\n            current:\n              $ref: '#/components/schemas/MemberResource'\n\
  \            previous:\n              description: Previous version of the member for edit events\n              oneOf:\n                - $ref: '#/components/schemas/MemberResource'\n                - type: object\n    PostResource:\n      type: object\n      description: >-\n        Post resource data included in webhook payloads.\n      properties:\n        id:\n          type: string\n          format: uuid\n          description: Unique identifier\n        uuid:\n          type: string\n          format: uuid\n          description: Universally unique identifier\n        title:\n          type: string\n          description: Post title\n        slug:\n          type: string\n          description: URL slug\n        html:\n          type: string\n          description: HTML content\n        plaintext:\n          type: string\n          description: Plain text content\n        feature_image:\n          type: string\n          format: uri\n          description: Featured image URL\n\
  \          nullable: true\n        featured:\n          type: boolean\n          description: Whether the post is featured\n        status:\n          type: string\n          description: Publication status\n          enum:\n            - published\n            - draft\n            - scheduled\n            - sent\n        visibility:\n          type: string\n          description: Access visibility\n          enum:\n            - public\n            - members\n            - paid\n            - tiers\n        created_at:\n          type: string\n          format: date-time\n          description: Creation timestamp\n        updated_at:\n          type: string\n          format: date-time\n          description: Last update timestamp\n        published_at:\n          type: string\n          format: date-time\n          description: Publication timestamp\n          nullable: true\n        custom_excerpt:\n          type: string\n          description: Custom excerpt\n          nullable: true\n\
  \        url:\n          type: string\n          format: uri\n          description: Full URL of the post\n        tags:\n          type: array\n          description: Associated tags\n          items:\n            $ref: '#/components/schemas/TagResource'\n    TagResource:\n      type: object\n      description: >-\n        Tag resource data included in webhook payloads.\n      properties:\n        id:\n          type: string\n          format: uuid\n          description: Unique identifier\n        name:\n          type: string\n          description: Tag name\n        slug:\n          type: string\n          description: URL slug\n        description:\n          type: string\n          description: Tag description\n          nullable: true\n        feature_image:\n          type: string\n          format: uri\n          description: Featured image URL\n          nullable: true\n        visibility:\n          type: string\n          description: Tag visibility\n          enum:\n     \
  \       - public\n            - internal\n        created_at:\n          type: string\n          format: date-time\n          description: Creation timestamp\n        updated_at:\n          type: string\n          format: date-time\n          description: Last update timestamp\n    MemberResource:\n      type: object\n      description: >-\n        Member resource data included in webhook payloads.\n      properties:\n        id:\n          type: string\n          format: uuid\n          description: Unique identifier\n        uuid:\n          type: string\n          format: uuid\n          description: Universally unique identifier\n        email:\n          type: string\n          format: email\n          description: Member email address\n        name:\n          type: string\n          description: Member name\n          nullable: true\n        status:\n          type: string\n          description: Member status\n          enum:\n            - free\n            - paid\n          \
  \  - comped\n        labels:\n          type: array\n          description: Member labels\n          items:\n            type: object\n            properties:\n              id:\n                type: string\n                format: uuid\n                description: Label identifier\n              name:\n                type: string\n                description: Label name\n              slug:\n                type: string\n                description: Label slug\n        created_at:\n          type: string\n          format: date-time\n          description: Signup timestamp\n        updated_at:\n          type: string\n          format: date-time\n          description: Last update timestamp\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/ghost/refs/heads/main/asyncapi/ghost-webhooks-asyncapi.yml
spec_file: asyncapi/ghost-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/ghost/refs/heads/main/asyncapi/ghost-webhooks-asyncapi.yml
tags:
- Publishing
- Newsletters
- Memberships
- Content
- Open Source
- AsyncAPI
- Webhooks
- Events
version: '5.0'
---
