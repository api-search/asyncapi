---
api_specs:
- filename: launchdarkly-rest-api-openapi.yml
  format: yaml
  label: LaunchDarkly REST API
  slug: rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/launchdarkly/refs/heads/main/openapi/launchdarkly-rest-api-openapi.yml
- filename: launchdarkly-webhooks-asyncapi.yml
  format: yaml
  label: LaunchDarkly Webhooks API
  slug: webhooks-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/launchdarkly/refs/heads/main/asyncapi/launchdarkly-webhooks-asyncapi.yml
- filename: launchdarkly-relay-proxy-openapi.yml
  format: yaml
  label: LaunchDarkly Relay Proxy
  slug: relay-proxy
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/launchdarkly/refs/heads/main/openapi/launchdarkly-relay-proxy-openapi.yml
channels:
- description: LaunchDarkly sends audit log events to this channel when changes occur in the platform. Events can be filtered using policy statements configured on the webhook. By default, all flag change events in the production environment are sent.
  name: /webhook
  operation: publish
  operation_id: receiveWebhookEvent
  summary: Receive a webhook event from LaunchDarkly
description: LaunchDarkly sends webhook notifications as HTTP POST requests when changes occur within the platform. The webhook payload format is identical to audit log entries and includes details about what changed, who made the change, and when it occurred. Webhooks may not be delivered in chronological order, so consumers should use the payload date field as a timestamp to reorder events. Payloads can be verified using HMAC-SHA256 signature validation with a shared secret.
layout: asyncapi
messages:
- description: ''
  name: FlagChangeEvent
  summary: An event triggered when a feature flag is created, updated, or deleted.
  title: Feature Flag Change Event
- description: ''
  name: ProjectChangeEvent
  summary: An event triggered when a project is created, updated, or deleted.
  title: Project Change Event
- description: ''
  name: EnvironmentChangeEvent
  summary: An event triggered when an environment is created, updated, or deleted.
  title: Environment Change Event
- description: ''
  name: SegmentChangeEvent
  summary: An event triggered when a user segment is created, updated, or deleted.
  title: Segment Change Event
- description: ''
  name: MemberChangeEvent
  summary: An event triggered when an account member is invited, updated, or removed.
  title: Member Change Event
- description: ''
  name: GenericChangeEvent
  summary: A catch-all event for any change to a LaunchDarkly resource that does not have a more specific event type defined.
  title: Generic Change Event
name: LaunchDarkly Webhooks Events
provider_name: launchdarkly
provider_slug: launchdarkly
servers:
- description: The customer-configured webhook endpoint URL that receives HTTP POST notifications from LaunchDarkly.
  name: webhookReceiver
  protocol: https
  url: '{webhookUrl}'
slug: launchdarkly-webhooks-asyncapi
source_filename: launchdarkly-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: LaunchDarkly Webhooks Events\n  description: >-\n    LaunchDarkly sends webhook notifications as HTTP POST requests when\n    changes occur within the platform. The webhook payload format is\n    identical to audit log entries and includes details about what changed,\n    who made the change, and when it occurred. Webhooks may not be\n    delivered in chronological order, so consumers should use the payload\n    date field as a timestamp to reorder events. Payloads can be verified\n    using HMAC-SHA256 signature validation with a shared secret.\n  version: '2.0'\n  contact:\n    name: LaunchDarkly Support\n    url: https://support.launchdarkly.com\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\n  externalDocs:\n    description: LaunchDarkly Webhooks Documentation\n    url: https://launchdarkly.com/docs/api/webhooks\nservers:\n  webhookReceiver:\n    url: '{webhookUrl}'\n    protocol: https\n    description:\
  \ >-\n      The customer-configured webhook endpoint URL that receives\n      HTTP POST notifications from LaunchDarkly.\n    variables:\n      webhookUrl:\n        description: >-\n          The URL configured in the LaunchDarkly webhook settings.\n    security:\n      - hmacSignature: []\nchannels:\n  /webhook:\n    description: >-\n      LaunchDarkly sends audit log events to this channel when changes\n      occur in the platform. Events can be filtered using policy\n      statements configured on the webhook. By default, all flag\n      change events in the production environment are sent.\n    publish:\n      operationId: receiveWebhookEvent\n      summary: Receive a webhook event from LaunchDarkly\n      description: >-\n        Receives an HTTP POST notification from LaunchDarkly containing\n        an audit log event payload. The event describes a change made\n        to a resource such as a feature flag, project, environment,\n        segment, or other LaunchDarkly resource.\n\
  \      message:\n        oneOf:\n          - $ref: '#/components/messages/FlagChangeEvent'\n          - $ref: '#/components/messages/ProjectChangeEvent'\n          - $ref: '#/components/messages/EnvironmentChangeEvent'\n          - $ref: '#/components/messages/SegmentChangeEvent'\n          - $ref: '#/components/messages/MemberChangeEvent'\n          - $ref: '#/components/messages/GenericChangeEvent'\ncomponents:\n  securitySchemes:\n    hmacSignature:\n      type: httpApiKey\n      name: X-LD-Signature\n      in: header\n      description: >-\n        HMAC-SHA256 signature of the request body computed using the\n        shared secret configured on the webhook. Consumers should\n        compute the signature of the payload using the same shared\n        secret and compare it to this header value to verify\n        authenticity.\n  messages:\n    FlagChangeEvent:\n      name: FlagChangeEvent\n      title: Feature Flag Change Event\n      summary: >-\n        An event triggered when a feature\
  \ flag is created, updated,\n        or deleted.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-LD-Signature:\n            type: string\n            description: >-\n              HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/AuditLogEvent'\n      examples:\n        - name: flagToggled\n          summary: A feature flag was toggled on\n          payload:\n            _id: 615a8b3d1234567890abcdef\n            date: 1633312573000\n            kind: flag\n            name: dark-mode\n            description: '**dark-mode** turned on in **production**'\n            shortDescription: turned on\n            accesses:\n              - action: updateOn\n                resource: proj/default:env/production:flag/dark-mode\n            member:\n              _id: 507f1f77bcf86cd799439011\n              email: dev@example.com\n              firstName: Jane\n              lastName:\
  \ Developer\n    ProjectChangeEvent:\n      name: ProjectChangeEvent\n      title: Project Change Event\n      summary: >-\n        An event triggered when a project is created, updated,\n        or deleted.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AuditLogEvent'\n    EnvironmentChangeEvent:\n      name: EnvironmentChangeEvent\n      title: Environment Change Event\n      summary: >-\n        An event triggered when an environment is created, updated,\n        or deleted.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AuditLogEvent'\n    SegmentChangeEvent:\n      name: SegmentChangeEvent\n      title: Segment Change Event\n      summary: >-\n        An event triggered when a user segment is created, updated,\n        or deleted.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AuditLogEvent'\n    MemberChangeEvent:\n      name: MemberChangeEvent\n      title:\
  \ Member Change Event\n      summary: >-\n        An event triggered when an account member is invited,\n        updated, or removed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AuditLogEvent'\n    GenericChangeEvent:\n      name: GenericChangeEvent\n      title: Generic Change Event\n      summary: >-\n        A catch-all event for any change to a LaunchDarkly resource\n        that does not have a more specific event type defined.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AuditLogEvent'\n  schemas:\n    AuditLogEvent:\n      type: object\n      description: >-\n        An audit log event representing a change made to a resource\n        in LaunchDarkly. This is the standard payload format for\n        webhook notifications.\n      required:\n        - _id\n        - date\n        - kind\n        - name\n      properties:\n        _id:\n          type: string\n          description: >-\n    \
  \        The unique identifier of this audit log event.\n        date:\n          type: integer\n          format: int64\n          description: >-\n            Unix epoch timestamp in milliseconds when the change\n            occurred. Use this field to reorder webhook events since\n            they may not arrive in chronological order.\n        kind:\n          type: string\n          description: >-\n            The kind of resource that was changed.\n          enum:\n            - flag\n            - project\n            - environment\n            - segment\n            - metric\n            - member\n            - role\n            - webhook\n            - integration\n            - token\n            - destination\n            - relay-proxy-config\n            - experiment\n            - team\n            - release-pipeline\n        name:\n          type: string\n          description: >-\n            The name of the resource that was changed.\n        description:\n          type:\
  \ string\n          description: >-\n            A markdown-formatted description of the changes made\n            to the resource.\n        shortDescription:\n          type: string\n          description: >-\n            A brief plain-text summary of the change.\n        comment:\n          type: string\n          description: >-\n            An optional comment provided by the member who made\n            the change.\n        accesses:\n          type: array\n          description: >-\n            The access details describing what action was taken\n            and on which resource.\n          items:\n            $ref: '#/components/schemas/Access'\n        member:\n          $ref: '#/components/schemas/MemberRef'\n        titleVerb:\n          type: string\n          description: >-\n            The verb describing the action taken, such as \"created\",\n            \"updated\", or \"deleted\".\n        title:\n          type: string\n          description: >-\n            A human-readable\
  \ title for the event.\n        target:\n          type: object\n          description: >-\n            Details about the target resource of the change.\n          properties:\n            _links:\n              type: object\n              description: >-\n                Links to the target resource.\n              additionalProperties:\n                type: object\n                properties:\n                  href:\n                    type: string\n                    description: >-\n                      The URL of the linked resource.\n                  type:\n                    type: string\n                    description: >-\n                      The media type.\n            name:\n              type: string\n              description: >-\n                The name of the target resource.\n            resources:\n              type: array\n              description: >-\n                The resource specifiers for the target.\n              items:\n                type: string\n\
  \        _links:\n          type: object\n          description: >-\n            HATEOAS links to related resources.\n          additionalProperties:\n            type: object\n            properties:\n              href:\n                type: string\n                description: >-\n                  The URL of the linked resource.\n              type:\n                type: string\n                description: >-\n                  The media type.\n    Access:\n      type: object\n      description: >-\n        An access record describing what action was performed\n        on which resource.\n      properties:\n        action:\n          type: string\n          description: >-\n            The action that was performed, such as \"createFlag\",\n            \"updateOn\", \"deleteFlag\", or \"updateTargets\".\n        resource:\n          type: string\n          description: >-\n            A resource specifier in the format\n            \"proj/{projKey}:env/{envKey}:flag/{flagKey}\"\
  \ identifying\n            the affected resource.\n    MemberRef:\n      type: object\n      description: >-\n        A reference to the account member who made the change.\n      properties:\n        _id:\n          type: string\n          description: >-\n            The unique identifier of the member.\n        email:\n          type: string\n          format: email\n          description: >-\n            The email address of the member.\n        firstName:\n          type: string\n          description: >-\n            The first name of the member.\n        lastName:\n          type: string\n          description: >-\n            The last name of the member.\n        _links:\n          type: object\n          description: >-\n            Links related to the member.\n          additionalProperties:\n            type: object\n            properties:\n              href:\n                type: string\n                description: >-\n                  The URL.\n              type:\n\
  \                type: string\n                description: >-\n                  The media type.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/launchdarkly/refs/heads/main/asyncapi/launchdarkly-webhooks-asyncapi.yml
spec_file: asyncapi/launchdarkly-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/launchdarkly/refs/heads/main/asyncapi/launchdarkly-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '2.0'
---
