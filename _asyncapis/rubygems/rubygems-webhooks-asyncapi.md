---
api_specs:
- filename: rubygems-gems-api-openapi.yml
  format: yaml
  label: RubyGems Gems API
  slug: gems-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/openapi/rubygems-gems-api-openapi.yml
- filename: rubygems-api-v2-openapi.yml
  format: yaml
  label: RubyGems API V2
  slug: api-v2
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/openapi/rubygems-api-v2-openapi.yml
- filename: rubygems-downloads-api-openapi.yml
  format: yaml
  label: RubyGems Downloads API
  slug: downloads-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/openapi/rubygems-downloads-api-openapi.yml
- filename: rubygems-search-api-openapi.yml
  format: yaml
  label: RubyGems Search API
  slug: search-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/openapi/rubygems-search-api-openapi.yml
- filename: rubygems-activity-api-openapi.yml
  format: yaml
  label: RubyGems Activity API
  slug: activity-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/openapi/rubygems-activity-api-openapi.yml
- filename: rubygems-webhooks-api-openapi.yml
  format: yaml
  label: RubyGems Webhooks API
  slug: webhooks-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/openapi/rubygems-webhooks-api-openapi.yml
channels:
- description: Webhook endpoint that receives notifications when gems are pushed to RubyGems.org. The subscriber provides this URL when registering the webhook via the Webhooks API.
  name: /webhook
  operation: publish
  operation_id: onGemPush
  summary: Receive gem push notification
description: The RubyGems webhook event system delivers HTTP POST notifications when gems are pushed to RubyGems.org. Webhook subscribers receive a JSON payload containing the full gem metadata whenever a new version of a watched gem (or any gem, for global webhooks) is published. Each notification includes an Authorization header containing a SHA-256 HMAC signature that receivers can use to verify the notification originated from RubyGems.org.
layout: asyncapi
messages:
- description: Contains the full gem metadata for the newly pushed version, identical to the response from the GET /api/v1/gems endpoint. The HTTP request includes an Authorization header with a SHA-256 HMAC signature derived from the gem name and the API key of the webhook creator.
  name: GemPushEvent
  summary: Notification sent when a gem version is pushed to RubyGems.org.
  title: Gem Push Event
name: RubyGems Webhook Events
provider_name: RubyGems
provider_slug: rubygems
servers:
- description: RubyGems.org production server that sends webhook notifications when gems are pushed.
  name: rubygems
  protocol: https
  url: https://rubygems.org
slug: rubygems-webhooks-asyncapi
source_filename: rubygems-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: RubyGems Webhook Events\n  description: >-\n    The RubyGems webhook event system delivers HTTP POST notifications when\n    gems are pushed to RubyGems.org. Webhook subscribers receive a JSON\n    payload containing the full gem metadata whenever a new version of a\n    watched gem (or any gem, for global webhooks) is published. Each\n    notification includes an Authorization header containing a SHA-256\n    HMAC signature that receivers can use to verify the notification\n    originated from RubyGems.org.\n  version: '1.0'\n  contact:\n    name: RubyGems.org Support\n    url: https://help.rubygems.org\nservers:\n  rubygems:\n    url: https://rubygems.org\n    protocol: https\n    description: >-\n      RubyGems.org production server that sends webhook notifications\n      when gems are pushed.\nchannels:\n  /webhook:\n    description: >-\n      Webhook endpoint that receives notifications when gems are pushed\n      to RubyGems.org. The subscriber\
  \ provides this URL when registering\n      the webhook via the Webhooks API.\n    publish:\n      operationId: onGemPush\n      summary: Receive gem push notification\n      description: >-\n        Fired when a gem version is pushed to RubyGems.org. The notification\n        is sent as an HTTP POST request to the registered webhook URL. The\n        request includes an Authorization header with a SHA-256 HMAC\n        signature for verifying the notification authenticity.\n      message:\n        $ref: '#/components/messages/GemPushEvent'\ncomponents:\n  messages:\n    GemPushEvent:\n      name: GemPushEvent\n      title: Gem Push Event\n      summary: >-\n        Notification sent when a gem version is pushed to RubyGems.org.\n      description: >-\n        Contains the full gem metadata for the newly pushed version,\n        identical to the response from the GET /api/v1/gems endpoint.\n        The HTTP request includes an Authorization header with a SHA-256\n        HMAC signature\
  \ derived from the gem name and the API key of the\n        webhook creator.\n      headers:\n        type: object\n        properties:\n          Authorization:\n            type: string\n            description: >-\n              SHA-256 HMAC signature for verifying the webhook notification\n              authenticity. Computed from the gem name using the API key of\n              the user who registered the webhook.\n      payload:\n        type: object\n        description: Full gem metadata for the pushed version\n        properties:\n          name:\n            type: string\n            description: The name of the gem\n          downloads:\n            type: integer\n            description: Total number of downloads for this gem\n          version:\n            type: string\n            description: The version number that was pushed\n          version_created_at:\n            type: string\n            format: date-time\n            description: Timestamp when this version was\
  \ created\n          version_downloads:\n            type: integer\n            description: Download count for this version\n          platform:\n            type: string\n            description: The platform of the gem\n          authors:\n            type: string\n            description: Comma-separated list of gem authors\n          info:\n            type: string\n            description: Short description of the gem\n          licenses:\n            type: array\n            items:\n              type: string\n            description: List of licenses for the gem\n          metadata:\n            type: object\n            additionalProperties:\n              type: string\n            description: Additional metadata key-value pairs\n          sha:\n            type: string\n            description: SHA-256 checksum of the gem file\n          project_uri:\n            type: string\n            format: uri\n            description: URI to the gem project page on RubyGems.org\n   \
  \       gem_uri:\n            type: string\n            format: uri\n            description: URI to download the gem file\n          homepage_uri:\n            type: string\n            format: uri\n            description: URI to the gem homepage\n          documentation_uri:\n            type: string\n            format: uri\n            description: URI to the gem documentation\n          source_code_uri:\n            type: string\n            format: uri\n            description: URI to the gem source code\n          bug_tracker_uri:\n            type: string\n            format: uri\n            description: URI to the gem bug tracker\n          changelog_uri:\n            type: string\n            format: uri\n            description: URI to the gem changelog\n          dependencies:\n            type: object\n            properties:\n              development:\n                type: array\n                items:\n                  $ref: '#/components/schemas/Dependency'\n     \
  \           description: Development dependencies\n              runtime:\n                type: array\n                items:\n                  $ref: '#/components/schemas/Dependency'\n                description: Runtime dependencies\n            description: Gem dependency information\n  schemas:\n    Dependency:\n      type: object\n      description: A gem dependency\n      properties:\n        name:\n          type: string\n          description: Name of the dependency gem\n        requirements:\n          type: string\n          description: Version requirements string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/asyncapi/rubygems-webhooks-asyncapi.yml
spec_file: asyncapi/rubygems-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/asyncapi/rubygems-webhooks-asyncapi.yml
tags:
- Ruby
- Package Manager
- Open Source
- Developer Tools
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
