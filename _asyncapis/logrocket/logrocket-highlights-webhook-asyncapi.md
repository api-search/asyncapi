---
api_specs:
- filename: logrocket-rest-api-openapi.yml
  format: yaml
  label: LogRocket REST API
  slug: rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/logrocket/refs/heads/main/openapi/logrocket-rest-api-openapi.yml
- filename: logrocket-graphql-api-openapi.yml
  format: yaml
  label: LogRocket GraphQL API
  slug: graphql-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/logrocket/refs/heads/main/openapi/logrocket-graphql-api-openapi.yml
- filename: logrocket-highlights-webhook-asyncapi.yml
  format: yaml
  label: LogRocket Galileo Highlights API
  slug: session-highlights-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/logrocket/refs/heads/main/asyncapi/logrocket-highlights-webhook-asyncapi.yml
channels:
- description: Webhook delivery channel for Galileo AI highlights results. LogRocket sends a POST request to the customer-specified URL when highlights generation is complete.
  name: /
  operation: publish
  operation_id: receiveHighlightsResult
  summary: Receive Galileo AI highlights results
description: The LogRocket Galileo Highlights webhook delivers AI-generated session highlights to a customer-specified URL when processing completes. When a highlights request includes a webhookURL parameter, LogRocket sends a POST request to that URL containing the highlights results once Galileo AI finishes analyzing the requested sessions.
layout: asyncapi
messages:
- description: ''
  name: HighlightsWebhookPayload
  summary: Payload delivered to the webhook URL when highlights generation completes.
  title: Galileo Highlights Webhook Payload
name: LogRocket Galileo Highlights Webhook
provider_name: LogRocket
provider_slug: logrocket
servers:
- description: Customer-provided webhook endpoint that receives highlights results.
  name: customerWebhook
  protocol: https
  url: '{webhookUrl}'
slug: logrocket-highlights-webhook-asyncapi
source_filename: logrocket-highlights-webhook-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: LogRocket Galileo Highlights Webhook\n  description: >-\n    The LogRocket Galileo Highlights webhook delivers AI-generated session\n    highlights to a customer-specified URL when processing completes.\n    When a highlights request includes a webhookURL parameter, LogRocket\n    sends a POST request to that URL containing the highlights results\n    once Galileo AI finishes analyzing the requested sessions.\n  version: '1.0'\n  contact:\n    name: LogRocket Support\n    url: https://logrocket.com/support\nservers:\n  customerWebhook:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Customer-provided webhook endpoint that receives highlights results.\n    variables:\n      webhookUrl:\n        description: >-\n          The URL provided in the webhookURL field of the highlights\n          request body.\nchannels:\n  /:\n    description: >-\n      Webhook delivery channel for Galileo AI highlights results. LogRocket\n\
  \      sends a POST request to the customer-specified URL when highlights\n      generation is complete.\n    publish:\n      operationId: receiveHighlightsResult\n      summary: Receive Galileo AI highlights results\n      description: >-\n        Receives the completed highlights results from Galileo AI, including\n        an overall summary across all matched sessions and individual\n        per-session highlights with Markdown-formatted links to relevant\n        times in the session recordings.\n      message:\n        $ref: '#/components/messages/HighlightsWebhookPayload'\ncomponents:\n  messages:\n    HighlightsWebhookPayload:\n      name: HighlightsWebhookPayload\n      title: Galileo Highlights Webhook Payload\n      summary: >-\n        Payload delivered to the webhook URL when highlights generation\n        completes.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/HighlightsWebhookBody'\n  schemas:\n    HighlightsWebhookBody:\n    \
  \  type: object\n      description: >-\n        The webhook POST body containing the highlights results from\n        Galileo AI.\n      properties:\n        requestID:\n          type: string\n          description: >-\n            Unique identifier for the highlights request that triggered\n            this webhook delivery.\n        appID:\n          type: string\n          description: >-\n            The application ID associated with the highlights request.\n        status:\n          type: string\n          description: >-\n            The completion status of the highlights generation.\n          enum:\n            - COMPLETE\n            - FAILED\n        result:\n          description: >-\n            The highlights result, or null if generation failed.\n          oneOf:\n            - type: 'null'\n            - $ref: '#/components/schemas/HighlightsResult'\n    HighlightsResult:\n      type: object\n      description: >-\n        The generated highlights across all matched\
  \ sessions.\n      properties:\n        highlights:\n          type: string\n          description: >-\n            Markdown-formatted summary across all sessions, with links\n            to relevant times in the referenced sessions.\n        sessions:\n          type: array\n          description: >-\n            Individual session summaries.\n          items:\n            $ref: '#/components/schemas/SessionHighlight'\n    SessionHighlight:\n      type: object\n      description: >-\n        Highlights for an individual session.\n      properties:\n        sessionId:\n          type: string\n          description: >-\n            The unique identifier for the session.\n        highlights:\n          type: string\n          description: >-\n            Markdown-formatted highlights for this specific session,\n            with links to relevant times.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/logrocket/refs/heads/main/asyncapi/logrocket-highlights-webhook-asyncapi.yml
spec_file: asyncapi/logrocket-highlights-webhook-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/logrocket/refs/heads/main/asyncapi/logrocket-highlights-webhook-asyncapi.yml
tags:
- Analytics
- Error Monitoring
- Frontend Monitoring
- Observability
- Session Replay
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
