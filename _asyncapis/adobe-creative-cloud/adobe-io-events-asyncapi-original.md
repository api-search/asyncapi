---
api_specs:
- filename: adobe-firefly-api-openapi-original.yml
  format: yaml
  label: Adobe Firefly API
  slug: firefly-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-creative-cloud/refs/heads/main/openapi/adobe-firefly-api-openapi-original.yml
- filename: adobe-cc-libraries-api-openapi-original.yml
  format: yaml
  label: Creative Cloud Libraries API
  slug: cc-libraries-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-creative-cloud/refs/heads/main/openapi/adobe-cc-libraries-api-openapi-original.yml
- filename: adobe-stock-api-openapi-original.yml
  format: yaml
  label: Adobe Stock API
  slug: stock-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-creative-cloud/refs/heads/main/openapi/adobe-stock-api-openapi-original.yml
- filename: adobe-pdf-services-api-openapi-original.yml
  format: yaml
  label: Adobe PDF Services API
  slug: pdf-services-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-creative-cloud/refs/heads/main/openapi/adobe-pdf-services-api-openapi-original.yml
- filename: adobe-io-events-asyncapi-original.yml
  format: yaml
  label: Adobe I/O Events
  slug: io-events
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-creative-cloud/refs/heads/main/asyncapi/adobe-io-events-asyncapi-original.yml
channels:
- description: Challenge verification channel. When a webhook is registered, Adobe sends a GET request with a challenge query parameter. The webhook must respond with the challenge value in the body to prove ownership.
  name: /webhook/challenge
  operation: subscribe
  operation_id: onWebhookChallenge
  summary: Receive webhook challenge verification
- description: Primary event delivery channel. Adobe I/O Events sends POST requests to registered webhooks when events occur. Events conform to the CloudEvents specification.
  name: /webhook/event
  operation: subscribe
  operation_id: onEvent
  summary: Receive event notification
- description: Batch event delivery channel for high-volume event scenarios. Multiple events are grouped into a single POST request as a JSON array.
  name: /webhook/batch
  operation: subscribe
  operation_id: onBatchEvent
  summary: Receive batch event notifications
- description: Journaling channel for pull-based event consumption. Clients poll this endpoint with a position cursor to retrieve events. Events are retained for 7 days. Use the Link header from each response to get the next batch of events.
  name: /events/organizations/{orgId}/integrations/{integrationId}/{registrationId}
  operation: subscribe
  operation_id: pollJournalEvents
  summary: Poll journaling endpoint for events
description: Adobe I/O Events enables developers to receive near-real-time notifications when events occur across Adobe products and services. Events are delivered via webhooks or journaling (pull-based polling). Supported event providers include Creative Cloud, Experience Cloud, Document Cloud, and custom applications built on Adobe App Builder. Events follow the CloudEvents specification and include provenance metadata for traceability.
layout: asyncapi
messages:
- description: ''
  name: CreativeCloudAssetEvent
  summary: Event triggered when assets are created, updated, or deleted in Creative Cloud Libraries, Lightroom, or other CC storage.
  title: Creative Cloud Asset Event
- description: ''
  name: AEMAssetEvent
  summary: Event triggered by asset operations in Adobe Experience Manager such as asset creation, modification, or processing completion.
  title: AEM Asset Event
- description: ''
  name: AnalyticsEvent
  summary: Event triggered by Adobe Analytics notifications such as report completion, classification import completion, or segment publication.
  title: Adobe Analytics Event
- description: ''
  name: CampaignEvent
  summary: Event triggered by Adobe Campaign Standard operations such as delivery status updates, workflow transitions, or profile changes.
  title: Adobe Campaign Event
- description: ''
  name: CustomAppEvent
  summary: Event published by custom Adobe App Builder applications via the Events SDK. Developers define their own event types and payload structures.
  title: Custom Application Event
name: Adobe I/O Events
provider_name: Adobe Creative Cloud
provider_slug: adobe-creative-cloud
servers:
- description: Your webhook endpoint that receives event notifications from Adobe I/O Events. Must respond to a challenge verification request during registration and acknowledge events with a 200 status.
  name: webhook
  protocol: https
  url: '{webhookUrl}'
- description: Adobe I/O Events journaling endpoint for pull-based event consumption. Events are retained for 7 days and retrieved via polling with a position cursor.
  name: journaling
  protocol: https
  url: https://events-va6.adobe.io
slug: adobe-io-events-asyncapi-original
source_filename: adobe-io-events-asyncapi-original.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Adobe I/O Events\n  version: '1.0'\n  description: >-\n    Adobe I/O Events enables developers to receive near-real-time notifications\n    when events occur across Adobe products and services. Events are delivered\n    via webhooks or journaling (pull-based polling). Supported event providers\n    include Creative Cloud, Experience Cloud, Document Cloud, and custom\n    applications built on Adobe App Builder. Events follow the CloudEvents\n    specification and include provenance metadata for traceability.\n  contact:\n    name: Adobe Developer Support\n    url: https://developer.adobe.com/\n  license:\n    name: Proprietary\n    url: https://www.adobe.com/legal/terms.html\nservers:\n  webhook:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your webhook endpoint that receives event notifications from Adobe I/O\n      Events. Must respond to a challenge verification request during\n      registration and acknowledge\
  \ events with a 200 status.\n    variables:\n      webhookUrl:\n        description: The URL of your registered webhook endpoint.\n  journaling:\n    url: https://events-va6.adobe.io\n    protocol: https\n    description: >-\n      Adobe I/O Events journaling endpoint for pull-based event consumption.\n      Events are retained for 7 days and retrieved via polling with a position\n      cursor.\nchannels:\n  /webhook/challenge:\n    description: >-\n      Challenge verification channel. When a webhook is registered, Adobe sends\n      a GET request with a challenge query parameter. The webhook must respond\n      with the challenge value in the body to prove ownership.\n    subscribe:\n      operationId: onWebhookChallenge\n      summary: Receive webhook challenge verification\n      message:\n        name: ChallengeRequest\n        title: Webhook Challenge Request\n        contentType: application/json\n        payload:\n          type: object\n          properties:\n            challenge:\n\
  \              type: string\n              description: >-\n                Challenge token sent as a query parameter. Must be returned\n                in the response body to verify the webhook endpoint.\n  /webhook/event:\n    description: >-\n      Primary event delivery channel. Adobe I/O Events sends POST requests\n      to registered webhooks when events occur. Events conform to the\n      CloudEvents specification.\n    subscribe:\n      operationId: onEvent\n      summary: Receive event notification\n      message:\n        oneOf:\n          - $ref: '#/components/messages/CreativeCloudAssetEvent'\n          - $ref: '#/components/messages/AEMAssetEvent'\n          - $ref: '#/components/messages/AnalyticsEvent'\n          - $ref: '#/components/messages/CampaignEvent'\n          - $ref: '#/components/messages/CustomAppEvent'\n  /webhook/batch:\n    description: >-\n      Batch event delivery channel for high-volume event scenarios. Multiple\n      events are grouped into a single\
  \ POST request as a JSON array.\n    subscribe:\n      operationId: onBatchEvent\n      summary: Receive batch event notifications\n      message:\n        name: BatchEventNotification\n        title: Batch Event Notification\n        contentType: application/json\n        payload:\n          type: array\n          items:\n            $ref: '#/components/schemas/CloudEvent'\n  /events/organizations/{orgId}/integrations/{integrationId}/{registrationId}:\n    description: >-\n      Journaling channel for pull-based event consumption. Clients poll this\n      endpoint with a position cursor to retrieve events. Events are retained\n      for 7 days. Use the Link header from each response to get the next\n      batch of events.\n    parameters:\n      orgId:\n        description: Adobe organization ID.\n        schema:\n          type: string\n      integrationId:\n        description: Integration ID from Adobe Developer Console.\n        schema:\n          type: string\n      registrationId:\n\
  \        description: Event registration ID.\n        schema:\n          type: string\n    subscribe:\n      operationId: pollJournalEvents\n      summary: Poll journaling endpoint for events\n      message:\n        name: JournalingResponse\n        title: Journaling Event Response\n        contentType: application/json\n        payload:\n          type: object\n          properties:\n            events:\n              type: array\n              description: Array of events since the last position.\n              items:\n                $ref: '#/components/schemas/CloudEvent'\n            _page:\n              type: object\n              properties:\n                last:\n                  type: string\n                  description: Position cursor for the last event in this batch.\n                count:\n                  type: integer\n                  description: Number of events in this batch.\n            link:\n              type: object\n              properties:\n       \
  \         next:\n                  type: string\n                  description: URL to poll for the next batch of events.\ncomponents:\n  messages:\n    CreativeCloudAssetEvent:\n      name: CreativeCloudAssetEvent\n      title: Creative Cloud Asset Event\n      summary: >-\n        Event triggered when assets are created, updated, or deleted in\n        Creative Cloud Libraries, Lightroom, or other CC storage.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/CloudEvent'\n          - type: object\n            properties:\n              data:\n                type: object\n                properties:\n                  xdmEntity:\n                    type: object\n                    properties:\n                      asset:id:\n                        type: string\n                        description: Unique identifier for the asset.\n                      asset:name:\n                        type: string\n                  \
  \      description: Name of the asset.\n                      asset:path:\n                        type: string\n                        description: Path to the asset within the repository.\n                      asset:format:\n                        type: string\n                        description: MIME type of the asset.\n                      repo:action:\n                        type: string\n                        enum:\n                          - created\n                          - updated\n                          - deleted\n                        description: The action performed on the asset.\n    AEMAssetEvent:\n      name: AEMAssetEvent\n      title: AEM Asset Event\n      summary: >-\n        Event triggered by asset operations in Adobe Experience Manager\n        such as asset creation, modification, or processing completion.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/CloudEvent'\n          - type:\
  \ object\n            properties:\n              data:\n                type: object\n                properties:\n                  xdmEntity:\n                    type: object\n                    properties:\n                      asset:id:\n                        type: string\n                      asset:name:\n                        type: string\n                      asset:path:\n                        type: string\n                      repo:action:\n                        type: string\n                        enum:\n                          - created\n                          - updated\n                          - deleted\n                          - processed\n    AnalyticsEvent:\n      name: AnalyticsEvent\n      title: Adobe Analytics Event\n      summary: >-\n        Event triggered by Adobe Analytics notifications such as report\n        completion, classification import completion, or segment publication.\n      contentType: application/json\n      payload:\n      \
  \  allOf:\n          - $ref: '#/components/schemas/CloudEvent'\n          - type: object\n            properties:\n              data:\n                type: object\n                properties:\n                  reportSuiteId:\n                    type: string\n                    description: Analytics report suite ID.\n                  notificationType:\n                    type: string\n                    description: Type of analytics notification.\n    CampaignEvent:\n      name: CampaignEvent\n      title: Adobe Campaign Event\n      summary: >-\n        Event triggered by Adobe Campaign Standard operations such as\n        delivery status updates, workflow transitions, or profile changes.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/CloudEvent'\n          - type: object\n            properties:\n              data:\n                type: object\n                properties:\n                  deliveryId:\n      \
  \              type: string\n                  status:\n                    type: string\n                  eventType:\n                    type: string\n    CustomAppEvent:\n      name: CustomAppEvent\n      title: Custom Application Event\n      summary: >-\n        Event published by custom Adobe App Builder applications via the\n        Events SDK. Developers define their own event types and payload\n        structures.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/CloudEvent'\n          - type: object\n            properties:\n              data:\n                type: object\n                description: Custom event payload defined by the application.\n                additionalProperties: true\n  schemas:\n    CloudEvent:\n      type: object\n      description: >-\n        Base event envelope following the CloudEvents specification v1.0.\n        All Adobe I/O Events conform to this structure.\n      required:\n  \
  \      - id\n        - source\n        - specversion\n        - type\n      properties:\n        id:\n          type: string\n          description: Unique identifier for this event instance.\n        source:\n          type: string\n          format: uri\n          description: >-\n            URI identifying the event source (e.g.,\n            urn:uuid:{provider-id}).\n        specversion:\n          type: string\n          const: '1.0'\n          description: CloudEvents specification version.\n        type:\n          type: string\n          description: >-\n            Event type identifier (e.g.,\n            com.adobe.platform.event.created).\n        time:\n          type: string\n          format: date-time\n          description: Timestamp when the event occurred.\n        datacontenttype:\n          type: string\n          description: Content type of the data payload.\n          default: application/json\n        data:\n          type: object\n          description: Event-specific\
  \ payload data.\n          additionalProperties: true\n        recipient_client_id:\n          type: string\n          description: >-\n            Client ID of the integration receiving this event, from the\n            Adobe Developer Console project.\n        event_id:\n          type: string\n          description: Adobe-specific event identifier.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/adobe-creative-cloud/refs/heads/main/asyncapi/adobe-io-events-asyncapi-original.yml
spec_file: asyncapi/adobe-io-events-asyncapi-original.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/adobe-creative-cloud/refs/heads/main/asyncapi/adobe-io-events-asyncapi-original.yml
tags:
- AI/ML
- Cloud
- Creative
- Design
- Documents
- Photography
- SaaS
- Video
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
