---
api_specs:
- filename: npm-registry-api-openapi.yml
  format: yaml
  label: npm Registry API
  slug: registry
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/npm/refs/heads/main/openapi/npm-registry-api-openapi.yml
- filename: npm-public-api-openapi.yml
  format: yaml
  label: npm Public API
  slug: public
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/npm/refs/heads/main/openapi/npm-public-api-openapi.yml
- filename: npm-hooks-api-openapi.yml
  format: yaml
  label: npm Hooks API
  slug: hooks
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/npm/refs/heads/main/openapi/npm-hooks-api-openapi.yml
channels:
- description: Receives HTTP POST payloads from the npm registry when a watched entity changes. Each delivery includes an x-npm-signature header containing an HMAC SHA-256 signature of the payload body using the shared secret configured during hook creation.
  name: /webhook
  operation: publish
  operation_id: receiveRegistryEvent
  summary: Receive an npm registry change event
description: The npm Hooks event system delivers HTTP POST payloads to subscriber endpoints whenever changes occur in the npm registry. Hooks can be configured to watch for changes to individual packages, all packages within a scope, or all packages published by a specific npm user. Each payload is signed with a shared secret using HMAC SHA-256, and the signature is included in the x-npm-signature header for verification. Note that npm hooks services have been deprecated as of July 2024.
layout: asyncapi
messages:
- description: ''
  name: PackageChanged
  summary: Sent when a package is modified in any way.
  title: Package Changed
- description: ''
  name: PackagePublished
  summary: Sent when a new version of a package is published to the registry.
  title: Package Published
- description: ''
  name: PackageUnpublished
  summary: Sent when a package version is unpublished from the registry.
  title: Package Unpublished
- description: ''
  name: OwnerChanged
  summary: Sent when the maintainers or owner of a package changes.
  title: Owner Changed
- description: ''
  name: DistTagChanged
  summary: Sent when a distribution tag is added, modified, or removed on a package.
  title: Dist-Tag Changed
- description: ''
  name: DeprecationChanged
  summary: Sent when a package version is deprecated or undeprecated.
  title: Deprecation Changed
- description: ''
  name: StarChanged
  summary: Sent when a user stars or unstars a package.
  title: Star Changed
name: npm Hooks Events
provider_name: npm
provider_slug: npm
servers:
- description: The subscriber's HTTP endpoint that receives webhook payloads. This URL is configured when creating a hook subscription.
  name: subscriber
  protocol: https
  url: '{subscriberUrl}'
slug: npm-hooks-asyncapi
source_filename: npm-hooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: npm Hooks Events\n  description: >-\n    The npm Hooks event system delivers HTTP POST payloads to subscriber\n    endpoints whenever changes occur in the npm registry. Hooks can be\n    configured to watch for changes to individual packages, all packages\n    within a scope, or all packages published by a specific npm user.\n    Each payload is signed with a shared secret using HMAC SHA-256, and\n    the signature is included in the x-npm-signature header for\n    verification. Note that npm hooks services have been deprecated as\n    of July 2024.\n  version: '1.0.0'\n  contact:\n    name: npm Support\n    url: https://www.npmjs.com/support\nservers:\n  subscriber:\n    url: '{subscriberUrl}'\n    protocol: https\n    description: >-\n      The subscriber's HTTP endpoint that receives webhook payloads.\n      This URL is configured when creating a hook subscription.\n    variables:\n      subscriberUrl:\n        description: >-\n         \
  \ The URL of the subscriber endpoint.\nchannels:\n  /webhook:\n    description: >-\n      Receives HTTP POST payloads from the npm registry when a watched\n      entity changes. Each delivery includes an x-npm-signature header\n      containing an HMAC SHA-256 signature of the payload body using\n      the shared secret configured during hook creation.\n    publish:\n      operationId: receiveRegistryEvent\n      summary: Receive an npm registry change event\n      description: >-\n        Receives a webhook payload when a package is published,\n        unpublished, updated, or when ownership or scope membership\n        changes occur.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/PackageChanged'\n          - $ref: '#/components/messages/PackagePublished'\n          - $ref: '#/components/messages/PackageUnpublished'\n          - $ref: '#/components/messages/OwnerChanged'\n          - $ref: '#/components/messages/DistTagChanged'\n          - $ref: '#/components/messages/DeprecationChanged'\n\
  \          - $ref: '#/components/messages/StarChanged'\ncomponents:\n  messages:\n    PackageChanged:\n      name: packageChanged\n      title: Package Changed\n      summary: >-\n        Sent when a package is modified in any way.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          x-npm-signature:\n            type: string\n            description: >-\n              HMAC SHA-256 signature of the payload body, using the\n              shared secret configured on the hook.\n      payload:\n        $ref: '#/components/schemas/PackageChangeEvent'\n    PackagePublished:\n      name: packagePublished\n      title: Package Published\n      summary: >-\n        Sent when a new version of a package is published to the\n        registry.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          x-npm-signature:\n            type: string\n            description: >-\n              HMAC SHA-256\
  \ signature of the payload body.\n      payload:\n        $ref: '#/components/schemas/PackagePublishEvent'\n    PackageUnpublished:\n      name: packageUnpublished\n      title: Package Unpublished\n      summary: >-\n        Sent when a package version is unpublished from the registry.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          x-npm-signature:\n            type: string\n            description: >-\n              HMAC SHA-256 signature of the payload body.\n      payload:\n        $ref: '#/components/schemas/PackageUnpublishEvent'\n    OwnerChanged:\n      name: ownerChanged\n      title: Owner Changed\n      summary: >-\n        Sent when the maintainers or owner of a package changes.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          x-npm-signature:\n            type: string\n            description: >-\n              HMAC SHA-256 signature of the payload body.\n\
  \      payload:\n        $ref: '#/components/schemas/OwnerChangeEvent'\n    DistTagChanged:\n      name: distTagChanged\n      title: Dist-Tag Changed\n      summary: >-\n        Sent when a distribution tag is added, modified, or removed\n        on a package.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          x-npm-signature:\n            type: string\n            description: >-\n              HMAC SHA-256 signature of the payload body.\n      payload:\n        $ref: '#/components/schemas/DistTagChangeEvent'\n    DeprecationChanged:\n      name: deprecationChanged\n      title: Deprecation Changed\n      summary: >-\n        Sent when a package version is deprecated or undeprecated.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          x-npm-signature:\n            type: string\n            description: >-\n              HMAC SHA-256 signature of the payload body.\n      payload:\n\
  \        $ref: '#/components/schemas/DeprecationChangeEvent'\n    StarChanged:\n      name: starChanged\n      title: Star Changed\n      summary: >-\n        Sent when a user stars or unstars a package.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          x-npm-signature:\n            type: string\n            description: >-\n              HMAC SHA-256 signature of the payload body.\n      payload:\n        $ref: '#/components/schemas/StarChangeEvent'\n  schemas:\n    BaseEvent:\n      type: object\n      description: >-\n        Common fields present in all npm hook event payloads.\n      properties:\n        event:\n          type: string\n          description: >-\n            The type of event that occurred.\n        name:\n          type: string\n          description: >-\n            The name of the package associated with the event.\n        type:\n          type: string\n          description: >-\n            The type of entity\
  \ that triggered the hook.\n          enum:\n            - package\n            - scope\n            - owner\n        version:\n          type: string\n          description: >-\n            The version of the package associated with the event,\n            if applicable.\n        hookOwner:\n          type: object\n          description: >-\n            The npm user who owns the hook subscription.\n          properties:\n            username:\n              type: string\n              description: >-\n                The npm username of the hook owner.\n        payload:\n          type: object\n          description: >-\n            The event-specific payload data.\n        change:\n          type: object\n          description: >-\n            Details about what changed.\n        time:\n          type: string\n          format: date-time\n          description: >-\n            The timestamp of when the event occurred.\n    PackageChangeEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseEvent'\n\
  \        - type: object\n          description: >-\n            Event payload for a general package change.\n          properties:\n            event:\n              type: string\n              enum:\n                - package:change\n            payload:\n              type: object\n              properties:\n                name:\n                  type: string\n                  description: >-\n                    The package name.\n                version:\n                  type: string\n                  description: >-\n                    The affected version.\n                description:\n                  type: string\n                  description: >-\n                    The package description.\n    PackagePublishEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseEvent'\n        - type: object\n          description: >-\n            Event payload for a new package version publication.\n          properties:\n            event:\n              type: string\n \
  \             enum:\n                - package:publish\n            payload:\n              type: object\n              properties:\n                name:\n                  type: string\n                  description: >-\n                    The package name.\n                version:\n                  type: string\n                  description: >-\n                    The newly published version.\n                description:\n                  type: string\n                  description: >-\n                    The package description.\n                dist:\n                  type: object\n                  description: >-\n                    Distribution metadata for the published version.\n                  properties:\n                    shasum:\n                      type: string\n                      description: >-\n                        SHA-1 checksum of the tarball.\n                    tarball:\n                      type: string\n                      format: uri\n\
  \                      description: >-\n                        URL of the published tarball.\n    PackageUnpublishEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseEvent'\n        - type: object\n          description: >-\n            Event payload for a package version being unpublished.\n          properties:\n            event:\n              type: string\n              enum:\n                - package:unpublish\n            payload:\n              type: object\n              properties:\n                name:\n                  type: string\n                  description: >-\n                    The package name.\n                version:\n                  type: string\n                  description: >-\n                    The unpublished version.\n    OwnerChangeEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseEvent'\n        - type: object\n          description: >-\n            Event payload for an ownership change on a package.\n          properties:\n\
  \            event:\n              type: string\n              enum:\n                - package:owner\n            payload:\n              type: object\n              properties:\n                name:\n                  type: string\n                  description: >-\n                    The package name.\n                maintainers:\n                  type: array\n                  description: >-\n                    Updated list of maintainers.\n                  items:\n                    type: object\n                    properties:\n                      name:\n                        type: string\n                        description: >-\n                          Maintainer username.\n                      email:\n                        type: string\n                        format: email\n                        description: >-\n                          Maintainer email.\n    DistTagChangeEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseEvent'\n        - type:\
  \ object\n          description: >-\n            Event payload for a dist-tag change on a package.\n          properties:\n            event:\n              type: string\n              enum:\n                - package:dist-tag\n            payload:\n              type: object\n              properties:\n                name:\n                  type: string\n                  description: >-\n                    The package name.\n                dist-tags:\n                  type: object\n                  description: >-\n                    Updated mapping of dist-tags to versions.\n                  additionalProperties:\n                    type: string\n    DeprecationChangeEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseEvent'\n        - type: object\n          description: >-\n            Event payload for a deprecation change on a package version.\n          properties:\n            event:\n              type: string\n              enum:\n                - package:deprecate\n\
  \            payload:\n              type: object\n              properties:\n                name:\n                  type: string\n                  description: >-\n                    The package name.\n                version:\n                  type: string\n                  description: >-\n                    The affected version.\n                deprecated:\n                  type: string\n                  description: >-\n                    The deprecation message, or empty string if\n                    undeprecated.\n    StarChangeEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseEvent'\n        - type: object\n          description: >-\n            Event payload for a star or unstar action on a package.\n          properties:\n            event:\n              type: string\n              enum:\n                - package:star\n            payload:\n              type: object\n              properties:\n                name:\n                  type: string\n\
  \                  description: >-\n                    The package name.\n                user:\n                  type: string\n                  description: >-\n                    The npm user who starred or unstarred the package.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/npm/refs/heads/main/asyncapi/npm-hooks-asyncapi.yml
spec_file: asyncapi/npm-hooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/npm/refs/heads/main/asyncapi/npm-hooks-asyncapi.yml
tags:
- Packages
- JavaScript
- Node.js
- Package Management
- Registry
- Security
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
