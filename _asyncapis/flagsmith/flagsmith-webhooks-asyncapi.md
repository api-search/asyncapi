---
api_specs:
- filename: flagsmith-flags-api-openapi.yml
  format: yaml
  label: Flagsmith Flags API
  slug: flags-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/flagsmith/refs/heads/main/openapi/flagsmith-flags-api-openapi.yml
- filename: flagsmith-admin-api-openapi.yml
  format: yaml
  label: Flagsmith Admin API
  slug: admin-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/flagsmith/refs/heads/main/openapi/flagsmith-admin-api-openapi.yml
channels:
- description: Environment webhooks receive flag evaluation data for identified users. Every time an identity's flags are evaluated via the Get Identity Flags endpoint, Flagsmith sends the full set of flag evaluations, traits, and segments for that user to the configured webhook URL.
  name: /environment-webhook
  operation: publish
  operation_id: receiveEnvironmentWebhook
  summary: Receive flag evaluation events for identified users
- description: Organisation webhooks receive audit log events when changes are made to resources across the organisation. This includes feature flag changes, environment updates, segment modifications, and other administrative actions performed via the dashboard or Admin API.
  name: /organisation-webhook
  operation: publish
  operation_id: receiveOrganisationWebhook
  summary: Receive audit log events for organisation changes
description: Flagsmith provides two types of webhooks for receiving event notifications. Environment webhooks automatically send flag evaluations for identified users whenever an identity's flags are evaluated via the Get Identity Flags endpoint. Organisation webhooks send audit log events whenever changes are made to feature flags, environments, or other resources across the organisation. Both webhook types support HMAC-SHA256 signature verification using a configurable secret.
layout: asyncapi
messages:
- description: Contains the complete set of flag evaluations for an identified user, including the enabled state and value of each feature flag. This payload is sent as a POST request to the configured environment webhook URL whenever the Get Identity Flags endpoint is called.
  name: EnvironmentWebhookEvent
  summary: Flag evaluation data sent when an identity's flags are evaluated
  title: Environment Webhook Event
- description: Contains details about a change made within the organisation, such as creating, updating, or deleting a feature flag, environment, or other resource. The event includes information about what changed, who made the change, and when it occurred.
  name: OrganisationWebhookEvent
  summary: Audit log event sent when changes occur within the organisation
  title: Organisation Webhook Event
name: Flagsmith Webhook Events
provider_name: flagsmith
provider_slug: flagsmith
servers:
- description: Your webhook receiver endpoint. Flagsmith sends POST requests to this URL when events occur. The URL is configured per environment or per organisation in the Flagsmith dashboard or via the Admin API.
  name: webhookReceiver
  protocol: https
  url: '{webhookUrl}'
slug: flagsmith-webhooks-asyncapi
source_filename: flagsmith-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Flagsmith Webhook Events\n  description: >-\n    Flagsmith provides two types of webhooks for receiving event notifications.\n    Environment webhooks automatically send flag evaluations for identified\n    users whenever an identity's flags are evaluated via the Get Identity Flags\n    endpoint. Organisation webhooks send audit log events whenever changes are\n    made to feature flags, environments, or other resources across the\n    organisation. Both webhook types support HMAC-SHA256 signature verification\n    using a configurable secret.\n  version: '1.0'\n  contact:\n    name: Flagsmith Support\n    url: https://www.flagsmith.com/contact-us\nservers:\n  webhookReceiver:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your webhook receiver endpoint. Flagsmith sends POST requests to this\n      URL when events occur. The URL is configured per environment or per\n      organisation in the Flagsmith dashboard or\
  \ via the Admin API.\n    variables:\n      webhookUrl:\n        description: The URL configured to receive webhook events\n    security:\n      - hmacSignature: []\nchannels:\n  /environment-webhook:\n    description: >-\n      Environment webhooks receive flag evaluation data for identified users.\n      Every time an identity's flags are evaluated via the Get Identity Flags\n      endpoint, Flagsmith sends the full set of flag evaluations, traits, and\n      segments for that user to the configured webhook URL.\n    publish:\n      operationId: receiveEnvironmentWebhook\n      summary: Receive flag evaluation events for identified users\n      message:\n        $ref: '#/components/messages/EnvironmentWebhookEvent'\n  /organisation-webhook:\n    description: >-\n      Organisation webhooks receive audit log events when changes are made\n      to resources across the organisation. This includes feature flag\n      changes, environment updates, segment modifications, and other\n      administrative\
  \ actions performed via the dashboard or Admin API.\n    publish:\n      operationId: receiveOrganisationWebhook\n      summary: Receive audit log events for organisation changes\n      message:\n        $ref: '#/components/messages/OrganisationWebhookEvent'\ncomponents:\n  securitySchemes:\n    hmacSignature:\n      type: httpApiKey\n      name: X-Flagsmith-Signature\n      in: header\n      description: >-\n        HMAC-SHA256 signature computed using the webhook secret as the key\n        and the request body as the message. When a webhook secret is\n        configured, Flagsmith includes this signature header with each\n        webhook request so the receiver can verify the payload authenticity.\n  messages:\n    EnvironmentWebhookEvent:\n      name: EnvironmentWebhookEvent\n      title: Environment Webhook Event\n      summary: >-\n        Flag evaluation data sent when an identity's flags are evaluated\n      description: >-\n        Contains the complete set of flag evaluations\
  \ for an identified user,\n        including the enabled state and value of each feature flag. This\n        payload is sent as a POST request to the configured environment\n        webhook URL whenever the Get Identity Flags endpoint is called.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EnvironmentWebhookPayload'\n    OrganisationWebhookEvent:\n      name: OrganisationWebhookEvent\n      title: Organisation Webhook Event\n      summary: >-\n        Audit log event sent when changes occur within the organisation\n      description: >-\n        Contains details about a change made within the organisation, such\n        as creating, updating, or deleting a feature flag, environment, or\n        other resource. The event includes information about what changed,\n        who made the change, and when it occurred.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrganisationWebhookPayload'\n  schemas:\n\
  \    EnvironmentWebhookPayload:\n      type: object\n      description: >-\n        The payload sent to environment webhooks containing flag evaluation\n        data for an identified user.\n      properties:\n        data:\n          type: array\n          description: >-\n            Array of flag evaluation results for the identified user\n          items:\n            $ref: '#/components/schemas/FlagEvaluation'\n        event_type:\n          type: string\n          const: FLAG_UPDATED\n          description: The type of event that triggered the webhook\n        timestamp:\n          type: string\n          format: date-time\n          description: When the event occurred\n    FlagEvaluation:\n      type: object\n      description: >-\n        A single flag evaluation result containing the feature definition,\n        its state, and the associated value for the identity.\n      properties:\n        id:\n          type: integer\n          description: The unique identifier for this\
  \ feature state\n        enabled:\n          type: boolean\n          description: Whether the flag is enabled for this identity\n        environment:\n          type: integer\n          description: The ID of the environment\n        feature:\n          $ref: '#/components/schemas/WebhookFeature'\n        feature_segment:\n          type: integer\n          nullable: true\n          description: >-\n            The feature segment ID if this evaluation is a segment override\n        feature_state_value:\n          description: >-\n            The evaluated value of the flag for this identity\n          oneOf:\n            - type: string\n            - type: integer\n            - type: boolean\n            - type: 'null'\n        identity:\n          type: integer\n          nullable: true\n          description: The identity ID this evaluation applies to\n    WebhookFeature:\n      type: object\n      description: >-\n        Feature metadata included in webhook payloads describing the\
  \ feature\n        flag definition.\n      properties:\n        id:\n          type: integer\n          description: The unique identifier for the feature\n        name:\n          type: string\n          description: The name of the feature flag\n        created_date:\n          type: string\n          format: date-time\n          description: When the feature was created\n        description:\n          type: string\n          nullable: true\n          description: A description of the feature\n        initial_value:\n          type: string\n          nullable: true\n          description: The initial value of the feature\n        default_enabled:\n          type: boolean\n          description: Whether the feature is enabled by default\n        type:\n          type: string\n          enum:\n            - STANDARD\n            - MULTIVARIATE\n          description: The type of feature flag\n    OrganisationWebhookPayload:\n      type: object\n      description: >-\n        The payload\
  \ sent to organisation webhooks containing audit log event\n        data about changes made within the organisation.\n      properties:\n        data:\n          $ref: '#/components/schemas/AuditLogEntry'\n        event_type:\n          type: string\n          enum:\n            - FLAG_UPDATED\n            - FLAG_DELETED\n            - AUDIT_LOG_CREATED\n          description: The type of event that triggered the webhook\n        timestamp:\n          type: string\n          format: date-time\n          description: When the event occurred\n    AuditLogEntry:\n      type: object\n      description: >-\n        An audit log entry recording a change made within the organisation,\n        including what was changed, who made the change, and the resulting\n        state.\n      properties:\n        id:\n          type: integer\n          description: The unique identifier for this audit log entry\n        created_date:\n          type: string\n          format: date-time\n          description:\
  \ When the change was recorded\n        log:\n          type: string\n          description: >-\n            A human-readable description of the change that was made\n        author:\n          $ref: '#/components/schemas/AuditLogAuthor'\n        environment:\n          type: string\n          nullable: true\n          description: The name of the environment affected by the change\n        project:\n          type: string\n          nullable: true\n          description: The name of the project affected by the change\n        related_object_id:\n          type: integer\n          nullable: true\n          description: The ID of the object that was changed\n        related_object_type:\n          type: string\n          nullable: true\n          enum:\n            - FEATURE\n            - FEATURE_STATE\n            - SEGMENT\n            - ENVIRONMENT\n            - CHANGE_REQUEST\n          description: The type of object that was changed\n    AuditLogAuthor:\n      type: object\n   \
  \   description: >-\n        Information about the user who made the change recorded in the\n        audit log.\n      properties:\n        id:\n          type: integer\n          description: The unique identifier for the user\n        email:\n          type: string\n          format: email\n          description: The email address of the user\n        first_name:\n          type: string\n          description: The first name of the user\n        last_name:\n          type: string\n          description: The last name of the user\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/flagsmith/refs/heads/main/asyncapi/flagsmith-webhooks-asyncapi.yml
spec_file: asyncapi/flagsmith-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/flagsmith/refs/heads/main/asyncapi/flagsmith-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
