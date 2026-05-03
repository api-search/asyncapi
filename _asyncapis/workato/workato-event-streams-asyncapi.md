---
api_specs:
- filename: workato-developer-api-openapi.yml
  format: yaml
  label: Workato
  slug: workato
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workato/refs/heads/main/openapi/workato-developer-api-openapi.yml
- filename: workato-event-streams-openapi.yml
  format: yaml
  label: Workato Event Streams Public API
  slug: event-streams-public-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workato/refs/heads/main/openapi/workato-event-streams-openapi.yml
- filename: workato-mcp-server-openapi.yml
  format: yaml
  label: Workato MCP Server API
  slug: mcp-server-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workato/refs/heads/main/openapi/workato-mcp-server-openapi.yml
channels:
- description: Channel for publishing a single message to an event topic. The message payload must conform to the topic's defined schema. Maximum payload size is 1 MB.
  name: /api/v1/topics/{topic_id}/publish
  operation: publish
  operation_id: publishMessage
  summary: Publish a message
- description: Channel for publishing a batch of up to 100 messages to an event topic in a single request. Enables efficient bulk event production.
  name: /api/v1/batch/topics/{topic_id}/publish
  operation: publish
  operation_id: publishBatchMessages
  summary: Publish a batch of messages
- description: Channel for consuming messages from an event topic. Supports replay from a message ID or timestamp, configurable batch sizes, and long polling for real-time consumption.
  name: /api/v1/topics/{topic_id}/consume
  operation: subscribe
  operation_id: consumeMessages
  summary: Consume messages from a topic
description: Workato Event Streams provides a publish-subscribe messaging system within the Workato platform. Topics act as channels through which producers publish messages and consumers retrieve them. Event Streams integrate with Workato recipes as triggers and actions, enabling loosely coupled, event-driven automation workflows. Messages are persisted and consumers can replay from a specific message ID or timestamp.
layout: asyncapi
messages:
- description: A message payload that conforms to the topic's schema definition. The exact structure depends on the schema configured for the topic.
  name: TopicMessage
  summary: A single message published to an event topic.
  title: Topic Message
- description: An array of message payloads, each conforming to the topic's schema. Maximum 100 messages per batch.
  name: BatchTopicMessage
  summary: A batch of messages published to an event topic.
  title: Batch Topic Message
- description: An array of messages retrieved from the event topic, each containing a message ID, payload, and publication timestamp.
  name: ConsumedMessages
  summary: A batch of messages consumed from an event topic.
  title: Consumed Messages
name: Workato Event Streams
provider_name: Workato
provider_slug: workato
servers:
- description: US Production event streams endpoint.
  name: us-production
  protocol: https
  url: event-streams.workato.com
- description: EU Production event streams endpoint.
  name: eu-production
  protocol: https
  url: event-streams.eu.workato.com
- description: JP Production event streams endpoint.
  name: jp-production
  protocol: https
  url: event-streams.jp.workato.com
- description: SG Production event streams endpoint.
  name: sg-production
  protocol: https
  url: event-streams.sg.workato.com
- description: AU Production event streams endpoint.
  name: au-production
  protocol: https
  url: event-streams.au.workato.com
- description: Developer sandbox for testing event streams integration.
  name: sandbox
  protocol: https
  url: event-streams.trial.workato.com
slug: workato-event-streams-asyncapi
source_filename: workato-event-streams-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Workato Event Streams\n  description: >-\n    Workato Event Streams provides a publish-subscribe messaging system within\n    the Workato platform. Topics act as channels through which producers publish\n    messages and consumers retrieve them. Event Streams integrate with Workato\n    recipes as triggers and actions, enabling loosely coupled, event-driven\n    automation workflows. Messages are persisted and consumers can replay from\n    a specific message ID or timestamp.\n  version: '1.0'\n  contact:\n    name: Workato Support\n    url: https://support.workato.com/\n  license:\n    name: Workato Terms of Service\n    url: https://www.workato.com/legal\nexternalDocs:\n  description: Workato Event Streams Documentation\n  url: https://docs.workato.com/event-streams.html\nservers:\n  us-production:\n    url: event-streams.workato.com\n    protocol: https\n    description: US Production event streams endpoint.\n    security:\n      - bearerAuth:\
  \ []\n  eu-production:\n    url: event-streams.eu.workato.com\n    protocol: https\n    description: EU Production event streams endpoint.\n    security:\n      - bearerAuth: []\n  jp-production:\n    url: event-streams.jp.workato.com\n    protocol: https\n    description: JP Production event streams endpoint.\n    security:\n      - bearerAuth: []\n  sg-production:\n    url: event-streams.sg.workato.com\n    protocol: https\n    description: SG Production event streams endpoint.\n    security:\n      - bearerAuth: []\n  au-production:\n    url: event-streams.au.workato.com\n    protocol: https\n    description: AU Production event streams endpoint.\n    security:\n      - bearerAuth: []\n  sandbox:\n    url: event-streams.trial.workato.com\n    protocol: https\n    description: Developer sandbox for testing event streams integration.\n    security:\n      - bearerAuth: []\nchannels:\n  /api/v1/topics/{topic_id}/publish:\n    description: >-\n      Channel for publishing a single message\
  \ to an event topic. The message\n      payload must conform to the topic's defined schema. Maximum payload\n      size is 1 MB.\n    parameters:\n      topic_id:\n        description: Unique integer identifier of the event topic.\n        schema:\n          type: integer\n    publish:\n      operationId: publishMessage\n      summary: Publish a message\n      description: >-\n        Publish a single message to the event topic. The payload must match\n        the topic's schema definition. Rate limit is 60 requests per minute.\n      message:\n        $ref: '#/components/messages/TopicMessage'\n  /api/v1/batch/topics/{topic_id}/publish:\n    description: >-\n      Channel for publishing a batch of up to 100 messages to an event topic\n      in a single request. Enables efficient bulk event production.\n    parameters:\n      topic_id:\n        description: Unique integer identifier of the event topic.\n        schema:\n          type: integer\n    publish:\n      operationId: publishBatchMessages\n\
  \      summary: Publish a batch of messages\n      description: >-\n        Publish up to 100 messages to the event topic in a single request.\n        Each payload in the batch must match the topic's schema definition.\n        Partial failures are indicated in the response.\n      message:\n        $ref: '#/components/messages/BatchTopicMessage'\n  /api/v1/topics/{topic_id}/consume:\n    description: >-\n      Channel for consuming messages from an event topic. Supports replay\n      from a message ID or timestamp, configurable batch sizes, and long\n      polling for real-time consumption.\n    parameters:\n      topic_id:\n        description: Unique integer identifier of the event topic.\n        schema:\n          type: integer\n    subscribe:\n      operationId: consumeMessages\n      summary: Consume messages from a topic\n      description: >-\n        Retrieve messages from the event topic. Use after_message_id or\n        since_time for replay. Set timeout_secs for long polling.\
  \ Returns\n        at most 50 messages per request.\n      message:\n        $ref: '#/components/messages/ConsumedMessages'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: http\n      scheme: bearer\n      description: >-\n        API client token obtained from the Workato platform. Include as\n        Authorization: Bearer {token}.\n  messages:\n    TopicMessage:\n      name: TopicMessage\n      title: Topic Message\n      summary: A single message published to an event topic.\n      description: >-\n        A message payload that conforms to the topic's schema definition.\n        The exact structure depends on the schema configured for the topic.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/MessagePayload'\n    BatchTopicMessage:\n      name: BatchTopicMessage\n      title: Batch Topic Message\n      summary: A batch of messages published to an event topic.\n      description: >-\n        An array of message payloads, each\
  \ conforming to the topic's schema.\n        Maximum 100 messages per batch.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BatchMessagePayload'\n    ConsumedMessages:\n      name: ConsumedMessages\n      title: Consumed Messages\n      summary: A batch of messages consumed from an event topic.\n      description: >-\n        An array of messages retrieved from the event topic, each containing\n        a message ID, payload, and publication timestamp.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ConsumedMessagesPayload'\n  schemas:\n    MessagePayload:\n      type: object\n      description: >-\n        A single message payload published to an event topic. The exact\n        properties depend on the topic's configured schema.\n      properties:\n        payloads:\n          type: object\n          description: The message data conforming to the topic's schema.\n          additionalProperties: true\n\
  \      additionalProperties: true\n    BatchMessagePayload:\n      type: object\n      description: Request payload for batch publishing messages to a topic.\n      required:\n        - payloads\n      properties:\n        payloads:\n          type: array\n          description: Array of message payloads, each conforming to the topic's schema.\n          maxItems: 100\n          items:\n            type: object\n            description: A single message payload.\n            additionalProperties: true\n    ConsumedMessagesPayload:\n      type: object\n      description: Response payload containing consumed messages from a topic.\n      properties:\n        messages:\n          type: array\n          description: List of messages retrieved from the topic.\n          items:\n            $ref: '#/components/schemas/Message'\n    Message:\n      type: object\n      description: A single message retrieved from an event topic.\n      properties:\n        message_id:\n          type: string\n\
  \          description: >-\n            Unique identifier of the message within the topic. Use this\n            value as after_message_id in subsequent consume requests to\n            retrieve only newer messages.\n        payload:\n          type: object\n          description: The message data conforming to the topic's schema.\n          additionalProperties: true\n        time:\n          type: string\n          format: date-time\n          description: RFC 3339 timestamp when the message was published to the topic.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/workato/refs/heads/main/asyncapi/workato-event-streams-asyncapi.yml
spec_file: asyncapi/workato-event-streams-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/workato/refs/heads/main/asyncapi/workato-event-streams-asyncapi.yml
tags:
- Agentic
- API Management
- Automation
- B2B
- Embedded iPaaS
- Enterprise
- Integration
- iPaaS
- Orchestration
- Workflow
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
