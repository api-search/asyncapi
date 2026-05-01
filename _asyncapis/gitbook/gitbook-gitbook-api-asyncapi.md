---
api_specs:
- filename: gitbook-gitbook-api-openapi.yml
  format: yaml
  label: GitBook
  slug: gitbook
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/gitbook/refs/heads/main/openapi/gitbook-gitbook-api-openapi.yml
channels:
- description: Triggered when a new space is created within an organization.
  name: space.created
  operation: subscribe
  operation_id: onSpaceCreated
  summary: Space Created
- description: Triggered when a space is updated, including title or visibility changes.
  name: space.updated
  operation: subscribe
  operation_id: onSpaceUpdated
  summary: Space Updated
- description: Triggered when a space is deleted from an organization.
  name: space.deleted
  operation: subscribe
  operation_id: onSpaceDeleted
  summary: Space Deleted
- description: Triggered when a new page is created within a space.
  name: page.created
  operation: subscribe
  operation_id: onPageCreated
  summary: Page Created
- description: Triggered when the content or metadata of a page is updated.
  name: page.updated
  operation: subscribe
  operation_id: onPageUpdated
  summary: Page Updated
- description: Triggered when a page is deleted from a space.
  name: page.deleted
  operation: subscribe
  operation_id: onPageDeleted
  summary: Page Deleted
- description: Triggered when a new change request is opened for a space.
  name: changeRequest.created
  operation: subscribe
  operation_id: onChangeRequestCreated
  summary: Change Request Created
- description: Triggered when a change request is merged into the main content.
  name: changeRequest.merged
  operation: subscribe
  operation_id: onChangeRequestMerged
  summary: Change Request Merged
- description: Triggered when a change request is closed without merging.
  name: changeRequest.closed
  operation: subscribe
  operation_id: onChangeRequestClosed
  summary: Change Request Closed
- description: Triggered when an organization's settings or metadata are updated.
  name: organization.updated
  operation: subscribe
  operation_id: onOrganizationUpdated
  summary: Organization Updated
- description: Triggered when a new member is added to an organization.
  name: organization.memberAdded
  operation: subscribe
  operation_id: onOrganizationMemberAdded
  summary: Organization Member Added
- description: Triggered when a member is removed from an organization.
  name: organization.memberRemoved
  operation: subscribe
  operation_id: onOrganizationMemberRemoved
  summary: Organization Member Removed
- description: Triggered when a new collection is created within an organization.
  name: collection.created
  operation: subscribe
  operation_id: onCollectionCreated
  summary: Collection Created
- description: Triggered when a collection is updated.
  name: collection.updated
  operation: subscribe
  operation_id: onCollectionUpdated
  summary: Collection Updated
- description: Triggered when a collection is deleted.
  name: collection.deleted
  operation: subscribe
  operation_id: onCollectionDeleted
  summary: Collection Deleted
- description: Triggered when a new docs site is created.
  name: docsSite.created
  operation: subscribe
  operation_id: onDocsSiteCreated
  summary: Docs Site Created
- description: Triggered when a docs site is updated, including hostname or title changes.
  name: docsSite.updated
  operation: subscribe
  operation_id: onDocsSiteUpdated
  summary: Docs Site Updated
- description: Triggered when a docs site is deleted.
  name: docsSite.deleted
  operation: subscribe
  operation_id: onDocsSiteDeleted
  summary: Docs Site Deleted
- description: Triggered when a user's profile information is updated.
  name: user.updated
  operation: subscribe
  operation_id: onUserUpdated
  summary: User Updated
description: AsyncAPI specification for GitBook webhook events. GitBook emits webhook notifications when key events occur within organizations, spaces, pages, change requests, docs sites, collections, and user accounts. These events enable real-time monitoring of documentation lifecycle changes and collaborative editing workflows.
layout: asyncapi
messages:
- description: ''
  name: SpaceEvent
  summary: An event related to a GitBook space.
  title: Space Event
- description: ''
  name: PageEvent
  summary: An event related to a page within a GitBook space.
  title: Page Event
- description: ''
  name: ChangeRequestEvent
  summary: An event related to a change request in a GitBook space.
  title: Change Request Event
- description: ''
  name: OrganizationEvent
  summary: An event related to an organization.
  title: Organization Event
- description: ''
  name: OrganizationMemberEvent
  summary: An event related to organization membership changes.
  title: Organization Member Event
- description: ''
  name: CollectionEvent
  summary: An event related to a collection.
  title: Collection Event
- description: ''
  name: DocsSiteEvent
  summary: An event related to a docs site.
  title: Docs Site Event
- description: ''
  name: UserEvent
  summary: An event related to a user profile change.
  title: User Event
name: GitBook Webhook Events
provider_name: GitBook
provider_slug: gitbook
servers:
- description: GitBook API webhook delivery endpoint
  name: production
  protocol: https
  url: https://api.gitbook.com/v1
slug: gitbook-gitbook-api-asyncapi
source_filename: gitbook-gitbook-api-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: GitBook Webhook Events\n  version: 1.0.0\n  description: >-\n    AsyncAPI specification for GitBook webhook events. GitBook emits webhook\n    notifications when key events occur within organizations, spaces, pages,\n    change requests, docs sites, collections, and user accounts. These events\n    enable real-time monitoring of documentation lifecycle changes and\n    collaborative editing workflows.\n  contact:\n    name: GitBook\n    url: https://www.gitbook.com\n  license:\n    name: Proprietary\n    url: https://www.gitbook.com/terms\nservers:\n  production:\n    url: https://api.gitbook.com/v1\n    protocol: https\n    description: GitBook API webhook delivery endpoint\nchannels:\n  space.created:\n    description: Triggered when a new space is created within an organization.\n    subscribe:\n      operationId: onSpaceCreated\n      summary: Space Created\n      message:\n        $ref: '#/components/messages/SpaceEvent'\n  space.updated:\n\
  \    description: Triggered when a space is updated, including title or visibility changes.\n    subscribe:\n      operationId: onSpaceUpdated\n      summary: Space Updated\n      message:\n        $ref: '#/components/messages/SpaceEvent'\n  space.deleted:\n    description: Triggered when a space is deleted from an organization.\n    subscribe:\n      operationId: onSpaceDeleted\n      summary: Space Deleted\n      message:\n        $ref: '#/components/messages/SpaceEvent'\n  page.created:\n    description: Triggered when a new page is created within a space.\n    subscribe:\n      operationId: onPageCreated\n      summary: Page Created\n      message:\n        $ref: '#/components/messages/PageEvent'\n  page.updated:\n    description: Triggered when the content or metadata of a page is updated.\n    subscribe:\n      operationId: onPageUpdated\n      summary: Page Updated\n      message:\n        $ref: '#/components/messages/PageEvent'\n  page.deleted:\n    description: Triggered when\
  \ a page is deleted from a space.\n    subscribe:\n      operationId: onPageDeleted\n      summary: Page Deleted\n      message:\n        $ref: '#/components/messages/PageEvent'\n  changeRequest.created:\n    description: Triggered when a new change request is opened for a space.\n    subscribe:\n      operationId: onChangeRequestCreated\n      summary: Change Request Created\n      message:\n        $ref: '#/components/messages/ChangeRequestEvent'\n  changeRequest.merged:\n    description: Triggered when a change request is merged into the main content.\n    subscribe:\n      operationId: onChangeRequestMerged\n      summary: Change Request Merged\n      message:\n        $ref: '#/components/messages/ChangeRequestEvent'\n  changeRequest.closed:\n    description: Triggered when a change request is closed without merging.\n    subscribe:\n      operationId: onChangeRequestClosed\n      summary: Change Request Closed\n      message:\n        $ref: '#/components/messages/ChangeRequestEvent'\n\
  \  organization.updated:\n    description: Triggered when an organization's settings or metadata are updated.\n    subscribe:\n      operationId: onOrganizationUpdated\n      summary: Organization Updated\n      message:\n        $ref: '#/components/messages/OrganizationEvent'\n  organization.memberAdded:\n    description: Triggered when a new member is added to an organization.\n    subscribe:\n      operationId: onOrganizationMemberAdded\n      summary: Organization Member Added\n      message:\n        $ref: '#/components/messages/OrganizationMemberEvent'\n  organization.memberRemoved:\n    description: Triggered when a member is removed from an organization.\n    subscribe:\n      operationId: onOrganizationMemberRemoved\n      summary: Organization Member Removed\n      message:\n        $ref: '#/components/messages/OrganizationMemberEvent'\n  collection.created:\n    description: Triggered when a new collection is created within an organization.\n    subscribe:\n      operationId:\
  \ onCollectionCreated\n      summary: Collection Created\n      message:\n        $ref: '#/components/messages/CollectionEvent'\n  collection.updated:\n    description: Triggered when a collection is updated.\n    subscribe:\n      operationId: onCollectionUpdated\n      summary: Collection Updated\n      message:\n        $ref: '#/components/messages/CollectionEvent'\n  collection.deleted:\n    description: Triggered when a collection is deleted.\n    subscribe:\n      operationId: onCollectionDeleted\n      summary: Collection Deleted\n      message:\n        $ref: '#/components/messages/CollectionEvent'\n  docsSite.created:\n    description: Triggered when a new docs site is created.\n    subscribe:\n      operationId: onDocsSiteCreated\n      summary: Docs Site Created\n      message:\n        $ref: '#/components/messages/DocsSiteEvent'\n  docsSite.updated:\n    description: Triggered when a docs site is updated, including hostname or title changes.\n    subscribe:\n      operationId:\
  \ onDocsSiteUpdated\n      summary: Docs Site Updated\n      message:\n        $ref: '#/components/messages/DocsSiteEvent'\n  docsSite.deleted:\n    description: Triggered when a docs site is deleted.\n    subscribe:\n      operationId: onDocsSiteDeleted\n      summary: Docs Site Deleted\n      message:\n        $ref: '#/components/messages/DocsSiteEvent'\n  user.updated:\n    description: Triggered when a user's profile information is updated.\n    subscribe:\n      operationId: onUserUpdated\n      summary: User Updated\n      message:\n        $ref: '#/components/messages/UserEvent'\ncomponents:\n  messages:\n    SpaceEvent:\n      name: SpaceEvent\n      title: Space Event\n      summary: An event related to a GitBook space.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventId:\n            type: string\n            description: Unique identifier for this event.\n          eventType:\n            type: string\n         \
  \   description: The type of event.\n            enum:\n              - space.created\n              - space.updated\n              - space.deleted\n          timestamp:\n            type: string\n            format: date-time\n            description: The time the event occurred.\n          organizationId:\n            type: string\n            description: The organization the space belongs to.\n          space:\n            $ref: '#/components/schemas/Space'\n    PageEvent:\n      name: PageEvent\n      title: Page Event\n      summary: An event related to a page within a GitBook space.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventId:\n            type: string\n            description: Unique identifier for this event.\n          eventType:\n            type: string\n            description: The type of event.\n            enum:\n              - page.created\n              - page.updated\n              - page.deleted\n\
  \          timestamp:\n            type: string\n            format: date-time\n            description: The time the event occurred.\n          organizationId:\n            type: string\n            description: The organization the space belongs to.\n          spaceId:\n            type: string\n            description: The space the page belongs to.\n          page:\n            $ref: '#/components/schemas/Page'\n    ChangeRequestEvent:\n      name: ChangeRequestEvent\n      title: Change Request Event\n      summary: An event related to a change request in a GitBook space.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventId:\n            type: string\n            description: Unique identifier for this event.\n          eventType:\n            type: string\n            description: The type of event.\n            enum:\n              - changeRequest.created\n              - changeRequest.merged\n              - changeRequest.closed\n\
  \          timestamp:\n            type: string\n            format: date-time\n            description: The time the event occurred.\n          organizationId:\n            type: string\n            description: The organization the space belongs to.\n          spaceId:\n            type: string\n            description: The space the change request belongs to.\n          changeRequest:\n            $ref: '#/components/schemas/ChangeRequest'\n    OrganizationEvent:\n      name: OrganizationEvent\n      title: Organization Event\n      summary: An event related to an organization.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventId:\n            type: string\n            description: Unique identifier for this event.\n          eventType:\n            type: string\n            description: The type of event.\n            enum:\n              - organization.updated\n          timestamp:\n            type: string\n          \
  \  format: date-time\n            description: The time the event occurred.\n          organization:\n            $ref: '#/components/schemas/Organization'\n    OrganizationMemberEvent:\n      name: OrganizationMemberEvent\n      title: Organization Member Event\n      summary: An event related to organization membership changes.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventId:\n            type: string\n            description: Unique identifier for this event.\n          eventType:\n            type: string\n            description: The type of event.\n            enum:\n              - organization.memberAdded\n              - organization.memberRemoved\n          timestamp:\n            type: string\n            format: date-time\n            description: The time the event occurred.\n          organizationId:\n            type: string\n            description: The organization affected.\n          user:\n         \
  \   $ref: '#/components/schemas/User'\n    CollectionEvent:\n      name: CollectionEvent\n      title: Collection Event\n      summary: An event related to a collection.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventId:\n            type: string\n            description: Unique identifier for this event.\n          eventType:\n            type: string\n            description: The type of event.\n            enum:\n              - collection.created\n              - collection.updated\n              - collection.deleted\n          timestamp:\n            type: string\n            format: date-time\n            description: The time the event occurred.\n          organizationId:\n            type: string\n            description: The organization the collection belongs to.\n          collection:\n            $ref: '#/components/schemas/Collection'\n    DocsSiteEvent:\n      name: DocsSiteEvent\n      title: Docs Site Event\n\
  \      summary: An event related to a docs site.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventId:\n            type: string\n            description: Unique identifier for this event.\n          eventType:\n            type: string\n            description: The type of event.\n            enum:\n              - docsSite.created\n              - docsSite.updated\n              - docsSite.deleted\n          timestamp:\n            type: string\n            format: date-time\n            description: The time the event occurred.\n          organizationId:\n            type: string\n            description: The organization the docs site belongs to.\n          docsSite:\n            $ref: '#/components/schemas/DocsSite'\n    UserEvent:\n      name: UserEvent\n      title: User Event\n      summary: An event related to a user profile change.\n      contentType: application/json\n      payload:\n        type: object\n       \
  \ properties:\n          eventId:\n            type: string\n            description: Unique identifier for this event.\n          eventType:\n            type: string\n            description: The type of event.\n            enum:\n              - user.updated\n          timestamp:\n            type: string\n            format: date-time\n            description: The time the event occurred.\n          user:\n            $ref: '#/components/schemas/User'\n  schemas:\n    Organization:\n      type: object\n      properties:\n        id:\n          type: string\n          description: The unique identifier of the organization.\n        title:\n          type: string\n          description: The display name of the organization.\n        createdAt:\n          type: string\n          format: date-time\n        updatedAt:\n          type: string\n          format: date-time\n        urls:\n          type: object\n          properties:\n            app:\n              type: string\n        \
  \      format: uri\n            published:\n              type: string\n              format: uri\n    Space:\n      type: object\n      properties:\n        id:\n          type: string\n          description: The unique identifier of the space.\n        title:\n          type: string\n          description: The title of the space.\n        visibility:\n          type: string\n          enum:\n            - public\n            - unlisted\n            - share-link\n            - in-collection\n            - private\n          description: The visibility setting of the space.\n        createdAt:\n          type: string\n          format: date-time\n        updatedAt:\n          type: string\n          format: date-time\n        urls:\n          type: object\n          properties:\n            app:\n              type: string\n              format: uri\n            published:\n              type: string\n              format: uri\n    Page:\n      type: object\n      properties:\n       \
  \ id:\n          type: string\n          description: The unique identifier of the page.\n        title:\n          type: string\n          description: The title of the page.\n        description:\n          type: string\n          description: The description of the page.\n        kind:\n          type: string\n          enum:\n            - sheet\n            - group\n            - link\n          description: The type of page.\n        path:\n          type: string\n          description: The URL-friendly path of the page.\n    User:\n      type: object\n      properties:\n        id:\n          type: string\n          description: The unique identifier of the user.\n        displayName:\n          type: string\n          description: The display name of the user.\n        email:\n          type: string\n          format: email\n          description: The email address of the user.\n        photoURL:\n          type: string\n          format: uri\n          description: URL to the\
  \ user's profile photo.\n    ChangeRequest:\n      type: object\n      properties:\n        id:\n          type: string\n          description: The unique identifier of the change request.\n        number:\n          type: integer\n          description: The sequential number of the change request.\n        subject:\n          type: string\n          description: The title of the change request.\n        description:\n          type: string\n          description: A description of the change request.\n        status:\n          type: string\n          enum:\n            - open\n            - merged\n            - closed\n          description: The current status of the change request.\n        createdAt:\n          type: string\n          format: date-time\n        updatedAt:\n          type: string\n          format: date-time\n        mergedAt:\n          type: string\n          format: date-time\n    Collection:\n      type: object\n      properties:\n        id:\n          type: string\n\
  \          description: The unique identifier of the collection.\n        title:\n          type: string\n          description: The title of the collection.\n        description:\n          type: string\n          description: The description of the collection.\n        createdAt:\n          type: string\n          format: date-time\n        updatedAt:\n          type: string\n          format: date-time\n    DocsSite:\n      type: object\n      properties:\n        id:\n          type: string\n          description: The unique identifier of the docs site.\n        title:\n          type: string\n          description: The title of the docs site.\n        hostname:\n          type: string\n          description: The hostname of the docs site.\n        urls:\n          type: object\n          properties:\n            app:\n              type: string\n              format: uri\n            published:\n              type: string\n              format: uri\n        createdAt:\n          type:\
  \ string\n          format: date-time\n        updatedAt:\n          type: string\n          format: date-time\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/gitbook/refs/heads/main/asyncapi/gitbook-gitbook-api-asyncapi.yml
spec_file: asyncapi/gitbook-gitbook-api-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/gitbook/refs/heads/main/asyncapi/gitbook-gitbook-api-asyncapi.yml
tags:
- Content
- Documentation
- Experience
- Integrations
- Platform
- SDKs
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
