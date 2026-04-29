---
channels:
- description: Generic webhook channel that receives all notification events from Cloudflare. Each notification includes the alert type, alert data, and metadata about the notification policy that triggered it.
  name: /webhook
  operation: publish
  operation_id: onNotificationEvent
  summary: Receive Cloudflare notification webhook
description: Cloudflare Notifications sends webhook events to configured endpoints when various alerts fire across your account. Webhooks deliver JSON payloads for events including DDoS attacks, SSL certificate expirations, origin health check failures, Workers errors, and many other alertable conditions. Professional and higher plans can configure generic webhooks or use pre-built integrations with Slack, Discord, PagerDuty, OpsGenie, and other services.
layout: asyncapi
messages:
- description: Fired when Cloudflare detects and mitigates a Layer 4 DDoS attack targeting your infrastructure. Contains details about the attack vector, protocol, target, and mitigation actions taken.
  name: DdosAttackL4Alert
  summary: Notification of a Layer 4 DDoS attack detected and mitigated
  title: DDoS Attack Layer 4 Alert
- description: Fired when Cloudflare detects a Layer 7 DDoS attack targeting your web application. Contains attack type, target hostname, and request rate information.
  name: DdosAttackL7Alert
  summary: Notification of a Layer 7 DDoS attack detected
  title: DDoS Attack Layer 7 Alert
- description: Fired when an SSL certificate is expiring soon, has expired, or has a status change. Contains certificate details, hostnames, and expiration information.
  name: SslCertificateAlert
  summary: Notification about an SSL certificate status change or upcoming expiration
  title: SSL Certificate Expiration Alert
- description: Fired when an origin health check detects a status change such as an origin becoming unhealthy or recovering. Contains the health check details and failing regions.
  name: HealthCheckAlert
  summary: Notification of an origin health status change
  title: Origin Health Check Alert
- description: Fired when a Workers script exceeds configured thresholds for CPU time, duration, request count, or error rates. Contains script metrics and route information.
  name: WorkersAlert
  summary: Notification about Workers script performance or error thresholds
  title: Workers Alert
- description: Generic payload structure for any Cloudflare notification alert. The data field contents vary depending on the specific alert type.
  name: GenericNotification
  summary: A generic notification event for any alert type
  title: Generic Notification
name: Cloudflare Notifications Webhooks
provider_name: Cloudflare
provider_slug: cloudflare
servers:
- description: Your configured webhook endpoint URL. Cloudflare sends HTTP POST requests to this URL when notification alerts fire. Validate incoming requests using the cf-webhook-auth header which contains your configured secret value.
  name: webhookEndpoint
  protocol: https
  url: '{webhookUrl}'
slug: cloudflare-notifications-webhooks-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Cloudflare Notifications Webhooks\n  description: >-\n    Cloudflare Notifications sends webhook events to configured endpoints when\n    various alerts fire across your account. Webhooks deliver JSON payloads\n    for events including DDoS attacks, SSL certificate expirations, origin\n    health check failures, Workers errors, and many other alertable\n    conditions. Professional and higher plans can configure generic webhooks\n    or use pre-built integrations with Slack, Discord, PagerDuty, OpsGenie,\n    and other services.\n  version: '1.0'\n  contact:\n    name: Cloudflare Support\n    url: https://support.cloudflare.com/\n  license:\n    name: Cloudflare Terms of Service\n    url: https://www.cloudflare.com/terms/\n  externalDocs:\n    description: Cloudflare Webhook Payload Schema\n    url: https://developers.cloudflare.com/notifications/reference/webhook-payload-schema/\nservers:\n  webhookEndpoint:\n    url: '{webhookUrl}'\n    protocol:\
  \ https\n    description: >-\n      Your configured webhook endpoint URL. Cloudflare sends HTTP POST\n      requests to this URL when notification alerts fire. Validate incoming\n      requests using the cf-webhook-auth header which contains your\n      configured secret value.\n    security:\n      - webhookSecret: []\n    variables:\n      webhookUrl:\n        description: The URL configured in the Cloudflare dashboard for webhook delivery.\nchannels:\n  /webhook:\n    description: >-\n      Generic webhook channel that receives all notification events from\n      Cloudflare. Each notification includes the alert type, alert data,\n      and metadata about the notification policy that triggered it.\n    publish:\n      operationId: onNotificationEvent\n      summary: Receive Cloudflare notification webhook\n      message:\n        oneOf:\n          - $ref: '#/components/messages/DdosAttackL4Alert'\n          - $ref: '#/components/messages/DdosAttackL7Alert'\n          - $ref: '#/components/messages/SslCertificateAlert'\n\
  \          - $ref: '#/components/messages/HealthCheckAlert'\n          - $ref: '#/components/messages/WorkersAlert'\n          - $ref: '#/components/messages/GenericNotification'\ncomponents:\n  securitySchemes:\n    webhookSecret:\n      type: httpApiKey\n      name: cf-webhook-auth\n      in: header\n      description: >-\n        The secret value configured when creating the webhook destination.\n        Validate this header to ensure the request originates from Cloudflare.\n  messages:\n    DdosAttackL4Alert:\n      name: DdosAttackL4Alert\n      title: DDoS Attack Layer 4 Alert\n      summary: Notification of a Layer 4 DDoS attack detected and mitigated\n      description: >-\n        Fired when Cloudflare detects and mitigates a Layer 4 DDoS attack\n        targeting your infrastructure. Contains details about the attack\n        vector, protocol, target, and mitigation actions taken.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DdosL4Payload'\n\
  \    DdosAttackL7Alert:\n      name: DdosAttackL7Alert\n      title: DDoS Attack Layer 7 Alert\n      summary: Notification of a Layer 7 DDoS attack detected\n      description: >-\n        Fired when Cloudflare detects a Layer 7 DDoS attack targeting\n        your web application. Contains attack type, target hostname,\n        and request rate information.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DdosL7Payload'\n    SslCertificateAlert:\n      name: SslCertificateAlert\n      title: SSL Certificate Expiration Alert\n      summary: Notification about an SSL certificate status change or upcoming expiration\n      description: >-\n        Fired when an SSL certificate is expiring soon, has expired, or\n        has a status change. Contains certificate details, hostnames, and\n        expiration information.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SslCertificatePayload'\n    HealthCheckAlert:\n\
  \      name: HealthCheckAlert\n      title: Origin Health Check Alert\n      summary: Notification of an origin health status change\n      description: >-\n        Fired when an origin health check detects a status change such as\n        an origin becoming unhealthy or recovering. Contains the health\n        check details and failing regions.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/HealthCheckPayload'\n    WorkersAlert:\n      name: WorkersAlert\n      title: Workers Alert\n      summary: Notification about Workers script performance or error thresholds\n      description: >-\n        Fired when a Workers script exceeds configured thresholds for CPU\n        time, duration, request count, or error rates. Contains script\n        metrics and route information.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WorkersAlertPayload'\n    GenericNotification:\n      name: GenericNotification\n     \
  \ title: Generic Notification\n      summary: A generic notification event for any alert type\n      description: >-\n        Generic payload structure for any Cloudflare notification alert.\n        The data field contents vary depending on the specific alert type.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/GenericNotificationPayload'\n  schemas:\n    BaseNotification:\n      type: object\n      required:\n        - name\n        - text\n        - data\n        - ts\n      properties:\n        name:\n          type: string\n          description: The notification policy name.\n        text:\n          type: string\n          description: Human-readable description of the alert.\n        ts:\n          type: integer\n          description: Unix timestamp when the notification was generated.\n        account_id:\n          type: string\n          description: The Cloudflare account identifier.\n        policy_id:\n          type: string\n \
  \         format: uuid\n          description: The notification policy UUID.\n        policy_name:\n          type: string\n          description: Name of the notification policy.\n        alert_type:\n          type: string\n          description: Unique identifier for the alert category.\n        alert_correlation_id:\n          type: string\n          format: uuid\n          description: UUID grouping related alerts.\n        alert_event:\n          type: string\n          description: The event state of the alert.\n          enum:\n            - ALERT_STATE_EVENT_START\n            - ALERT_STATE_EVENT_END\n    DdosL4Payload:\n      allOf:\n        - $ref: '#/components/schemas/BaseNotification'\n        - type: object\n          properties:\n            data:\n              type: object\n              properties:\n                attack_id:\n                  type: string\n                  description: Unique identifier for the attack.\n                attack_vector:\n           \
  \       type: string\n                  description: The attack vector type.\n                protocol:\n                  type: string\n                  description: The protocol targeted.\n                target_ip:\n                  type: string\n                  description: The targeted IP address.\n                target_port:\n                  type: integer\n                  description: The targeted port.\n                packets_per_second:\n                  type: integer\n                  description: Peak packets per second during the attack.\n                megabits_per_second:\n                  type: number\n                  description: Peak bandwidth in megabits per second.\n    DdosL7Payload:\n      allOf:\n        - $ref: '#/components/schemas/BaseNotification'\n        - type: object\n          properties:\n            data:\n              type: object\n              properties:\n                attack_id:\n                  type: string\n                  description:\
  \ Unique identifier for the attack.\n                attack_type:\n                  type: string\n                  description: The type of Layer 7 attack.\n                target_hostname:\n                  type: string\n                  description: The targeted hostname.\n                zone_name:\n                  type: string\n                  description: The zone name.\n                requests_per_second:\n                  type: integer\n                  description: Peak requests per second.\n    SslCertificatePayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseNotification'\n        - type: object\n          properties:\n            data:\n              type: object\n              properties:\n                certificate_id:\n                  type: string\n                  description: The certificate identifier.\n                certificate_status:\n                  type: string\n                  description: Current certificate status.\n         \
  \       hostnames:\n                  type: array\n                  items:\n                    type: string\n                  description: Hostnames covered by the certificate.\n                zone_name:\n                  type: string\n                  description: The zone name.\n    HealthCheckPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseNotification'\n        - type: object\n          properties:\n            data:\n              type: object\n              properties:\n                health_check_id:\n                  type: string\n                  description: The health check identifier.\n                health_check_name:\n                  type: string\n                  description: Name of the health check.\n                origin_ip:\n                  type: string\n                  description: The origin IP address.\n                new_health_status:\n                  type: string\n                  description: The new health status.\n   \
  \               enum:\n                    - healthy\n                    - unhealthy\n                failing_regions:\n                  type: array\n                  items:\n                    type: string\n                  description: Regions where the health check is failing.\n    WorkersAlertPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseNotification'\n        - type: object\n          properties:\n            data:\n              type: object\n              properties:\n                cpu_time:\n                  type: number\n                  description: CPU time usage in milliseconds.\n                duration:\n                  type: number\n                  description: Request duration in milliseconds.\n                request_count:\n                  type: integer\n                  description: Total request count.\n                data_egress:\n                  type: integer\n                  description: Data egress in bytes.\n           \
  \     account_script_count:\n                  type: integer\n                  description: Number of scripts in the account.\n                routes:\n                  type: array\n                  items:\n                    type: string\n                  description: Worker routes affected.\n    GenericNotificationPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseNotification'\n        - type: object\n          properties:\n            data:\n              type: object\n              description: >-\n                Alert-specific data whose structure varies depending on the\n                alert_type field.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cloudflare/refs/heads/main/asyncapi/cloudflare-notifications-webhooks-asyncapi.yml
spec_file: asyncapi/cloudflare-notifications-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/cloudflare/refs/heads/main/asyncapi/cloudflare-notifications-webhooks-asyncapi.yml
tags:
- AI Gateway
- API Gateway
- Artificial Intelligence
- CDN
- Cloud
- Containers
- DDoS Protection
- DNS
- Edge
- Edge Computing
- Object Storage
- Platform
- Real-Time Communication
- Security
- Serverless
- Web Performance
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
