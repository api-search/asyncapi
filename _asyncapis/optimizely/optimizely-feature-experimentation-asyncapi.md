---
api_specs:
- filename: optimizely-web-experimentation-openapi.yml
  format: yaml
  label: Optimizely Web Experimentation REST API
  slug: web-experimentation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-web-experimentation-openapi.yml
- filename: optimizely-feature-experimentation-openapi.yml
  format: yaml
  label: Optimizely Feature Experimentation REST API
  slug: feature-experimentation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-feature-experimentation-openapi.yml
- filename: optimizely-campaign-openapi.yml
  format: yaml
  label: Optimizely Campaign REST API
  slug: campaign
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-campaign-openapi.yml
- filename: optimizely-content-delivery-openapi.yml
  format: yaml
  label: Optimizely Content Delivery API
  slug: content-delivery
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-content-delivery-openapi.yml
- filename: optimizely-content-management-openapi.yml
  format: yaml
  label: Optimizely Content Management API
  slug: content-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-content-management-openapi.yml
- filename: optimizely-graph-openapi.yml
  format: yaml
  label: Optimizely Graph API
  slug: graph
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-graph-openapi.yml
- filename: optimizely-data-platform-openapi.yml
  format: yaml
  label: Optimizely Data Platform REST API
  slug: data-platform
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-data-platform-openapi.yml
- filename: optimizely-cmp-openapi.yml
  format: yaml
  label: Optimizely CMP Open REST API
  slug: cmp
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-cmp-openapi.yml
- filename: optimizely-commerce-service-openapi.yml
  format: yaml
  label: Optimizely Commerce Service API
  slug: commerce-service
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/openapi/optimizely-commerce-service-openapi.yml
channels:
- description: Receives webhook notifications from Optimizely Feature Experimentation when project configuration changes occur, particularly datafile updates.
  name: /webhook
  operation: publish
  operation_id: receiveDatafileUpdate
  summary: Receive a datafile update notification
description: Optimizely Feature Experimentation provides webhook notifications when configuration changes occur, such as datafile updates. Webhooks notify external servers of changes, eliminating the need to constantly poll for updates. Each webhook request includes a signature header (X-Hub-Signature) for verifying the request originated from Optimizely.
layout: asyncapi
messages:
- description: Sent when the configuration datafile for a project environment is updated. This can occur when experiments are started, paused, or modified, when feature flags are toggled, or when audience conditions are changed.
  name: DatafileUpdated
  summary: Notification that a project datafile has been updated
  title: Datafile Updated
name: Optimizely Feature Experimentation Webhooks
provider_name: Optimizely
provider_slug: optimizely
servers:
- description: The HTTPS endpoint on your server that receives webhook POST requests from Optimizely Feature Experimentation.
  name: webhookReceiver
  protocol: https
  url: '{callbackUrl}'
slug: optimizely-feature-experimentation-asyncapi
source_filename: optimizely-feature-experimentation-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Optimizely Feature Experimentation Webhooks\n  description: >-\n    Optimizely Feature Experimentation provides webhook notifications when\n    configuration changes occur, such as datafile updates. Webhooks notify\n    external servers of changes, eliminating the need to constantly poll\n    for updates. Each webhook request includes a signature header\n    (X-Hub-Signature) for verifying the request originated from Optimizely.\n  version: '1.0'\n  contact:\n    name: Optimizely Support\n    url: https://support.optimizely.com\nservers:\n  webhookReceiver:\n    url: '{callbackUrl}'\n    protocol: https\n    description: >-\n      The HTTPS endpoint on your server that receives webhook\n      POST requests from Optimizely Feature Experimentation.\n    variables:\n      callbackUrl:\n        description: The callback URL registered for receiving webhooks\nchannels:\n  /webhook:\n    description: >-\n      Receives webhook notifications from Optimizely\
  \ Feature Experimentation\n      when project configuration changes occur, particularly datafile updates.\n    publish:\n      operationId: receiveDatafileUpdate\n      summary: Receive a datafile update notification\n      description: >-\n        Optimizely sends an HTTP POST request to the registered callback\n        URL when the datafile for a project environment is updated. The\n        payload includes the project ID, revision number, and URLs to\n        download the updated datafile. A hash signature is included in\n        the X-Hub-Signature header for payload verification.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/DatafileUpdated'\ncomponents:\n  securitySchemes:\n    webhookSignature:\n      type: httpApiKey\n      in: header\n      name: X-Hub-Signature\n      description: >-\n        HMAC-SHA256 hash signature of the webhook payload, generated\n        using the secret token created when the webhook was registered.\n        Used to verify\
  \ the request originated from Optimizely.\n  messages:\n    DatafileUpdated:\n      name: DatafileUpdated\n      title: Datafile Updated\n      summary: Notification that a project datafile has been updated\n      description: >-\n        Sent when the configuration datafile for a project environment\n        is updated. This can occur when experiments are started, paused,\n        or modified, when feature flags are toggled, or when audience\n        conditions are changed.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Hub-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification\n      payload:\n        $ref: '#/components/schemas/DatafileUpdatePayload'\n  schemas:\n    DatafileUpdatePayload:\n      type: object\n      description: Payload sent when a project datafile is updated\n      required:\n        - project_id\n        - timestamp\n        - event\n        - data\n\
  \      properties:\n        project_id:\n          type: integer\n          format: int64\n          description: The project ID associated with the datafile update\n        timestamp:\n          type: integer\n          format: int64\n          description: Unix timestamp of when the update occurred\n        event:\n          type: string\n          description: The event type identifier\n          enum:\n            - project.datafile_updated\n        data:\n          type: object\n          description: Event data containing datafile details\n          required:\n            - revision\n            - origin_url\n            - cdn_url\n            - environment\n          properties:\n            revision:\n              type: integer\n              description: The revision number of the updated datafile\n            origin_url:\n              type: string\n              format: uri\n              description: Origin URL to download the updated datafile\n            cdn_url:\n     \
  \         type: string\n              format: uri\n              description: CDN URL to download the updated datafile\n            environment:\n              type: string\n              description: The environment the datafile belongs to (e.g., Production)\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/asyncapi/optimizely-feature-experimentation-asyncapi.yml
spec_file: asyncapi/optimizely-feature-experimentation-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/optimizely/refs/heads/main/asyncapi/optimizely-feature-experimentation-asyncapi.yml
tags:
- A/B Testing
- Content Management
- Customer Data
- E-Commerce
- Experimentation
- Feature Flags
- Marketing
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
