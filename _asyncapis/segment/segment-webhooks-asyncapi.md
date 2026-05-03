---
api_specs:
- filename: segment-public-api-openapi.yml
  format: yaml
  label: Segment Public API
  slug: public-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/segment/refs/heads/main/openapi/segment-public-api-openapi.yml
- filename: segment-http-tracking-api-openapi.yml
  format: yaml
  label: Segment HTTP Tracking API
  slug: http-tracking-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/segment/refs/heads/main/openapi/segment-http-tracking-api-openapi.yml
- filename: segment-profile-api-openapi.yml
  format: yaml
  label: Segment Profile API
  slug: profile-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/segment/refs/heads/main/openapi/segment-profile-api-openapi.yml
- filename: segment-config-api-openapi.yml
  format: yaml
  label: Segment Config API
  slug: config-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/segment/refs/heads/main/openapi/segment-config-api-openapi.yml
- filename: segment-pixel-tracking-api-openapi.yml
  format: yaml
  label: Segment Pixel Tracking API
  slug: pixel-tracking-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/segment/refs/heads/main/openapi/segment-pixel-tracking-api-openapi.yml
channels:
- description: The webhook endpoint that receives Segment events. Segment sends each event as an HTTP POST request with a JSON body.
  name: /webhook
  operation: publish
  operation_id: receiveSegmentEvent
  summary: Receive Segment event
description: Segment Webhooks submit real-time user data to HTTP endpoints as POST requests. When configured as a destination, Segment forwards identify, track, page, screen, group, and alias events to up to five webhook URLs. Each event is delivered as a JSON payload via HTTP POST with a configurable shared secret for authentication. The receiving service must respond within 5 seconds. If no response is received, Segment logs a timeout error and retries the event.
layout: asyncapi
messages:
- description: ''
  name: IdentifyEvent
  summary: An identify event that associates a user with their traits.
  title: Identify Event
- description: ''
  name: TrackEvent
  summary: A track event that records an action performed by a user.
  title: Track Event
- description: ''
  name: PageEvent
  summary: A page event that records a page view on a website.
  title: Page Event
- description: ''
  name: ScreenEvent
  summary: A screen event that records a screen view in a mobile app.
  title: Screen Event
- description: ''
  name: GroupEvent
  summary: A group event that associates a user with a group or account.
  title: Group Event
- description: ''
  name: AliasEvent
  summary: An alias event that merges two user identities.
  title: Alias Event
name: Segment Webhook Events
provider_name: segment
provider_slug: segment
servers:
- description: Your webhook endpoint URL configured in the Segment Webhooks destination settings. Up to five webhook URLs can be configured.
  name: webhookEndpoint
  protocol: https
  url: '{webhookUrl}'
slug: segment-webhooks-asyncapi
source_filename: segment-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Segment Webhook Events\n  description: >-\n    Segment Webhooks submit real-time user data to HTTP endpoints as\n    POST requests. When configured as a destination, Segment forwards\n    identify, track, page, screen, group, and alias events to up to\n    five webhook URLs. Each event is delivered as a JSON payload via\n    HTTP POST with a configurable shared secret for authentication.\n    The receiving service must respond within 5 seconds. If no response\n    is received, Segment logs a timeout error and retries the event.\n  version: '1.0.0'\n  contact:\n    name: Segment Support\n    url: https://segment.com/help/\n  externalDocs:\n    description: Segment Webhooks Destination Documentation\n    url: https://segment.com/docs/connections/destinations/catalog/webhooks/\nservers:\n  webhookEndpoint:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your webhook endpoint URL configured in the Segment Webhooks\n   \
  \   destination settings. Up to five webhook URLs can be configured.\n    variables:\n      webhookUrl:\n        description: >-\n          The URL of your webhook endpoint.\n    security:\n      - sharedSecret: []\nchannels:\n  /webhook:\n    description: >-\n      The webhook endpoint that receives Segment events. Segment\n      sends each event as an HTTP POST request with a JSON body.\n    publish:\n      operationId: receiveSegmentEvent\n      summary: Receive Segment event\n      description: >-\n        Receives a Segment event via HTTP POST. The event payload\n        matches one of the Segment spec types: identify, track, page,\n        screen, group, or alias. Your service must respond within\n        5 seconds with a 2xx status code.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/IdentifyEvent'\n          - $ref: '#/components/messages/TrackEvent'\n          - $ref: '#/components/messages/PageEvent'\n          - $ref: '#/components/messages/ScreenEvent'\n\
  \          - $ref: '#/components/messages/GroupEvent'\n          - $ref: '#/components/messages/AliasEvent'\ncomponents:\n  securitySchemes:\n    sharedSecret:\n      type: httpApiKey\n      name: x-signature\n      in: header\n      description: >-\n        A shared secret configured in the Segment Webhooks destination\n        settings. Segment includes a signature header that your service\n        can use to verify the authenticity of incoming webhook requests.\n  messages:\n    IdentifyEvent:\n      name: IdentifyEvent\n      title: Identify Event\n      summary: >-\n        An identify event that associates a user with their traits.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/IdentifyPayload'\n    TrackEvent:\n      name: TrackEvent\n      title: Track Event\n      summary: >-\n        A track event that records an action performed by a user.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TrackPayload'\n\
  \    PageEvent:\n      name: PageEvent\n      title: Page Event\n      summary: >-\n        A page event that records a page view on a website.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PagePayload'\n    ScreenEvent:\n      name: ScreenEvent\n      title: Screen Event\n      summary: >-\n        A screen event that records a screen view in a mobile app.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ScreenPayload'\n    GroupEvent:\n      name: GroupEvent\n      title: Group Event\n      summary: >-\n        A group event that associates a user with a group or account.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/GroupPayload'\n    AliasEvent:\n      name: AliasEvent\n      title: Alias Event\n      summary: >-\n        An alias event that merges two user identities.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AliasPayload'\n\
  \  schemas:\n    CommonFields:\n      type: object\n      properties:\n        type:\n          type: string\n          description: >-\n            The type of Segment event.\n          enum:\n            - identify\n            - track\n            - page\n            - screen\n            - group\n            - alias\n        userId:\n          type: string\n          description: >-\n            The unique user identifier.\n        anonymousId:\n          type: string\n          description: >-\n            A pseudo-unique substitute for a user ID.\n        messageId:\n          type: string\n          description: >-\n            Unique identifier for the message.\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            ISO 8601 timestamp of when the event occurred.\n        sentAt:\n          type: string\n          format: date-time\n          description: >-\n            ISO 8601 timestamp of when the event was sent.\n   \
  \     receivedAt:\n          type: string\n          format: date-time\n          description: >-\n            ISO 8601 timestamp of when Segment received the event.\n        context:\n          type: object\n          description: >-\n            Contextual information about the event.\n          additionalProperties: true\n        integrations:\n          type: object\n          description: >-\n            Destination-specific settings.\n          additionalProperties: true\n    IdentifyPayload:\n      allOf:\n        - $ref: '#/components/schemas/CommonFields'\n        - type: object\n          required:\n            - type\n          properties:\n            type:\n              type: string\n              const: identify\n            traits:\n              type: object\n              description: >-\n                User traits such as email, name, or custom attributes.\n              additionalProperties: true\n    TrackPayload:\n      allOf:\n        - $ref: '#/components/schemas/CommonFields'\n\
  \        - type: object\n          required:\n            - type\n            - event\n          properties:\n            type:\n              type: string\n              const: track\n            event:\n              type: string\n              description: >-\n                The name of the tracked event.\n            properties:\n              type: object\n              description: >-\n                Properties of the event, such as revenue or product\n                details.\n              additionalProperties: true\n    PagePayload:\n      allOf:\n        - $ref: '#/components/schemas/CommonFields'\n        - type: object\n          required:\n            - type\n          properties:\n            type:\n              type: string\n              const: page\n            name:\n              type: string\n              description: >-\n                The name of the page.\n            properties:\n              type: object\n              description: >-\n                Page\
  \ properties.\n              properties:\n                path:\n                  type: string\n                  description: >-\n                    The path of the page URL.\n                referrer:\n                  type: string\n                  description: >-\n                    The referrer URL.\n                title:\n                  type: string\n                  description: >-\n                    The page title.\n                url:\n                  type: string\n                  format: uri\n                  description: >-\n                    The full URL of the page.\n                search:\n                  type: string\n                  description: >-\n                    The search query string.\n              additionalProperties: true\n    ScreenPayload:\n      allOf:\n        - $ref: '#/components/schemas/CommonFields'\n        - type: object\n          required:\n            - type\n          properties:\n            type:\n              type:\
  \ string\n              const: screen\n            name:\n              type: string\n              description: >-\n                The name of the screen.\n            properties:\n              type: object\n              description: >-\n                Screen properties.\n              additionalProperties: true\n    GroupPayload:\n      allOf:\n        - $ref: '#/components/schemas/CommonFields'\n        - type: object\n          required:\n            - type\n            - groupId\n          properties:\n            type:\n              type: string\n              const: group\n            groupId:\n              type: string\n              description: >-\n                A unique identifier for the group.\n            traits:\n              type: object\n              description: >-\n                Group traits such as name, industry, or employee count.\n              properties:\n                name:\n                  type: string\n                  description: >-\n    \
  \                The name of the group or company.\n                industry:\n                  type: string\n                  description: >-\n                    The industry of the group.\n                employees:\n                  type: integer\n                  description: >-\n                    The number of employees.\n                plan:\n                  type: string\n                  description: >-\n                    The plan the group is on.\n              additionalProperties: true\n    AliasPayload:\n      allOf:\n        - $ref: '#/components/schemas/CommonFields'\n        - type: object\n          required:\n            - type\n            - previousId\n            - userId\n          properties:\n            type:\n              type: string\n              const: alias\n            previousId:\n              type: string\n              description: >-\n                The previous user ID to merge.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/segment/refs/heads/main/asyncapi/segment-webhooks-asyncapi.yml
spec_file: asyncapi/segment-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/segment/refs/heads/main/asyncapi/segment-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
