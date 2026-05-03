---
api_specs:
- filename: prometheus-http-api-openapi.yml
  format: yaml
  label: Prometheus HTTP API
  slug: prometheus-http-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/prometheus/refs/heads/main/openapi/prometheus-http-api-openapi.yml
- filename: prometheus-management-api-openapi.yml
  format: yaml
  label: Prometheus Management API
  slug: prometheus-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/prometheus/refs/heads/main/openapi/prometheus-management-api-openapi.yml
- filename: prometheus-pushgateway-api-openapi.yml
  format: yaml
  label: Prometheus Pushgateway API
  slug: prometheus-pushgateway-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/prometheus/refs/heads/main/openapi/prometheus-pushgateway-api-openapi.yml
- filename: prometheus-alertmanager-api-openapi.yml
  format: yaml
  label: Prometheus Alertmanager API
  slug: prometheus-alertmanager-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/prometheus/refs/heads/main/openapi/prometheus-alertmanager-api-openapi.yml
channels:
- description: Alertmanager sends HTTP POST requests to configured webhook receiver URLs when alert groups fire or resolve. The path is determined by the webhook receiver URL configuration.
  name: /{path}
  operation: publish
  operation_id: receiveAlertGroup
  summary: Receive alert group notification
description: The Prometheus Alertmanager webhook receiver sends HTTP POST requests to configured endpoints when alert groups are triggered. Each webhook payload contains a group of alerts sharing common routing labels, their annotations, firing status, and the external Alertmanager URL. Alertmanager delivers webhooks for both firing and resolved alerts, enabling downstream systems to react to alert lifecycle events.
layout: asyncapi
messages:
- description: The webhook payload sent by Alertmanager when a group of alerts transitions to firing or resolving state. Contains all alerts in the group, their current status (firing or resolved), and label/annotation data aggregated across the group.
  name: AlertGroupMessage
  summary: Batch of alerts sharing common group labels from Alertmanager
  title: Alert Group Webhook Payload
name: Prometheus Alertmanager Webhook Events
provider_name: Prometheus
provider_slug: prometheus
servers:
- description: The webhook receiver endpoint configured in Alertmanager's webhook_config. Alertmanager POSTs alert group payloads to this URL when routing rules match.
  name: webhookReceiver
  protocol: https
  url: '{webhookURL}'
slug: prometheus-alertmanager-webhook-asyncapi
source_filename: prometheus-alertmanager-webhook-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Prometheus Alertmanager Webhook Events\n  description: >-\n    The Prometheus Alertmanager webhook receiver sends HTTP POST requests to\n    configured endpoints when alert groups are triggered. Each webhook payload\n    contains a group of alerts sharing common routing labels, their annotations,\n    firing status, and the external Alertmanager URL. Alertmanager delivers\n    webhooks for both firing and resolved alerts, enabling downstream systems\n    to react to alert lifecycle events.\n  version: v0.28.0\n  contact:\n    name: Prometheus Project\n    url: https://prometheus.io/community/\nexternalDocs:\n  description: Alertmanager Webhook Receiver Documentation\n  url: https://prometheus.io/docs/alerting/latest/configuration/#webhook_config\nservers:\n  webhookReceiver:\n    url: '{webhookURL}'\n    protocol: https\n    description: >-\n      The webhook receiver endpoint configured in Alertmanager's webhook_config.\n      Alertmanager\
  \ POSTs alert group payloads to this URL when routing rules\n      match.\n    variables:\n      webhookURL:\n        description: The full URL of the webhook receiver endpoint.\nchannels:\n  /{path}:\n    description: >-\n      Alertmanager sends HTTP POST requests to configured webhook receiver\n      URLs when alert groups fire or resolve. The path is determined by the\n      webhook receiver URL configuration.\n    parameters:\n      path:\n        description: Path component of the webhook URL as configured.\n        schema:\n          type: string\n    publish:\n      operationId: receiveAlertGroup\n      summary: Receive alert group notification\n      description: >-\n        Alertmanager POSTs this payload when a group of alerts fires or\n        resolves. The payload includes the alert group's status, group labels,\n        common labels, common annotations, and individual alert details.\n        Webhook receivers should respond with 2xx to acknowledge receipt.\n        Non-2xx\
  \ responses cause Alertmanager to retry with exponential backoff.\n      message:\n        $ref: '#/components/messages/AlertGroupMessage'\ncomponents:\n  messages:\n    AlertGroupMessage:\n      name: AlertGroupMessage\n      title: Alert Group Webhook Payload\n      summary: Batch of alerts sharing common group labels from Alertmanager\n      description: >-\n        The webhook payload sent by Alertmanager when a group of alerts\n        transitions to firing or resolving state. Contains all alerts in the\n        group, their current status (firing or resolved), and label/annotation\n        data aggregated across the group.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AlertGroupPayload'\n  schemas:\n    AlertGroupPayload:\n      type: object\n      required:\n        - version\n        - groupKey\n        - status\n        - receiver\n        - groupLabels\n        - commonLabels\n        - commonAnnotations\n        - externalURL\n   \
  \     - alerts\n      description: >-\n        The top-level webhook payload from Alertmanager containing a group of\n        related alerts and their current firing or resolved state.\n      properties:\n        version:\n          type: string\n          description: Webhook payload version. Currently \"4\".\n          example: '4'\n        groupKey:\n          type: string\n          description: >-\n            Key identifying this alert group, composed of routing labels and\n            their values.\n          example: '{alertname=\"HighCPU\"}/{instance=\"server01\"}'\n        truncatedAlerts:\n          type: integer\n          description: >-\n            Number of alerts that were truncated from this payload due to the\n            max_alerts configuration setting. 0 if no truncation occurred.\n          default: 0\n        status:\n          type: string\n          enum:\n            - firing\n            - resolved\n          description: >-\n            Whether any alerts in\
  \ this group are still firing (firing) or\n            all have resolved (resolved).\n        receiver:\n          type: string\n          description: The name of the Alertmanager receiver that dispatched this webhook.\n          example: webhook-receiver\n        groupLabels:\n          type: object\n          additionalProperties:\n            type: string\n          description: >-\n            The labels used to group these alerts as configured in the routing\n            rules. These labels are common to all alerts in the group.\n        commonLabels:\n          type: object\n          additionalProperties:\n            type: string\n          description: >-\n            Labels present on every alert in the group. A superset of\n            groupLabels.\n        commonAnnotations:\n          type: object\n          additionalProperties:\n            type: string\n          description: >-\n            Annotations present on every alert in the group. Useful for\n            extracting\
  \ a shared runbook URL or description.\n        externalURL:\n          type: string\n          format: uri\n          description: >-\n            The external URL configured for this Alertmanager instance. Used\n            to construct links back to the Alertmanager web UI.\n        alerts:\n          type: array\n          items:\n            $ref: '#/components/schemas/WebhookAlert'\n          description: >-\n            The list of alerts in this group. Includes both firing and resolved\n            alerts depending on Alertmanager configuration.\n    WebhookAlert:\n      type: object\n      required:\n        - status\n        - labels\n        - annotations\n        - startsAt\n        - endsAt\n        - generatorURL\n        - fingerprint\n      description: An individual alert within a webhook payload.\n      properties:\n        status:\n          type: string\n          enum:\n            - firing\n            - resolved\n          description: Current status of this specific\
  \ alert.\n        labels:\n          type: object\n          additionalProperties:\n            type: string\n          description: >-\n            Identification labels for this alert. Always includes alertname and\n            any labels set by the alerting rule and its recording metric.\n        annotations:\n          type: object\n          additionalProperties:\n            type: string\n          description: >-\n            Non-identifying annotations for this alert such as summary,\n            description, and runbook_url.\n        startsAt:\n          type: string\n          format: date-time\n          description: Timestamp when this alert transitioned to firing state.\n        endsAt:\n          type: string\n          format: date-time\n          description: >-\n            Timestamp when this alert resolved. Set to a far-future timestamp\n            for currently firing alerts.\n        generatorURL:\n          type: string\n          format: uri\n          description:\
  \ >-\n            URL to the Prometheus expression browser for the rule that\n            generated this alert.\n        fingerprint:\n          type: string\n          description: >-\n            SHA256-based fingerprint of the alert's label set, used to\n            deduplicate alerts across Alertmanager instances.\n          example: b3e4e2c9a5b23e1f\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/prometheus/refs/heads/main/asyncapi/prometheus-alertmanager-webhook-asyncapi.yml
spec_file: asyncapi/prometheus-alertmanager-webhook-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/prometheus/refs/heads/main/asyncapi/prometheus-alertmanager-webhook-asyncapi.yml
tags:
- Alerting
- Metrics
- Monitoring
- Observability
- Time Series
- AsyncAPI
- Webhooks
- Events
version: v0.28.0
---
