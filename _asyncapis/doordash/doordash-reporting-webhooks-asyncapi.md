---
api_specs:
- filename: doordash-drive-openapi.yml
  format: yaml
  label: DoorDash Drive API
  slug: drive-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-drive-openapi.yml
- filename: doordash-drive-classic-openapi.yml
  format: yaml
  label: DoorDash Drive Classic API
  slug: drive-classic-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-drive-classic-openapi.yml
- filename: doordash-marketplace-openapi.yml
  format: yaml
  label: DoorDash Marketplace API
  slug: marketplace-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-marketplace-openapi.yml
- filename: doordash-item-management-openapi.yml
  format: yaml
  label: DoorDash Item Management API
  slug: marketplace-item-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-item-management-openapi.yml
- filename: doordash-reporting-openapi.yml
  format: yaml
  label: DoorDash Reporting API
  slug: reporting-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-reporting-openapi.yml
channels:
- description: DoorDash sends report ready notifications to this channel when a requested report has been generated and is available for download.
  name: /reports
  operation: publish
  operation_id: receiveReportReadyWebhook
  summary: Receive report ready webhooks
description: DoorDash Reporting API sends webhook notifications when report generation is complete and the report is ready for download. Partners configure a webhook endpoint to receive these notifications instead of polling the report status endpoint.
layout: asyncapi
messages:
- description: ''
  name: ReportReady
  summary: A report has been generated and is ready for download.
  title: Report Ready Event
name: DoorDash Reporting Webhooks
provider_name: doordash
provider_slug: doordash
servers:
- description: The partner-provided HTTPS webhook endpoint for receiving report ready notifications.
  name: partnerWebhook
  protocol: https
  url: '{webhook_url}'
slug: doordash-reporting-webhooks-asyncapi
source_filename: doordash-reporting-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: DoorDash Reporting Webhooks\n  description: >-\n    DoorDash Reporting API sends webhook notifications when report generation\n    is complete and the report is ready for download. Partners configure a\n    webhook endpoint to receive these notifications instead of polling the\n    report status endpoint.\n  version: '1.0'\n  contact:\n    name: DoorDash Developer Support\n    url: https://developer.doordash.com/en-US/\nservers:\n  partnerWebhook:\n    url: '{webhook_url}'\n    protocol: https\n    description: >-\n      The partner-provided HTTPS webhook endpoint for receiving report\n      ready notifications.\n    security:\n      - basicAuth: []\n    variables:\n      webhook_url:\n        description: >-\n          The HTTPS URL of the partner's webhook endpoint.\nchannels:\n  /reports:\n    description: >-\n      DoorDash sends report ready notifications to this channel when a\n      requested report has been generated and is available\
  \ for download.\n    publish:\n      operationId: receiveReportReadyWebhook\n      summary: Receive report ready webhooks\n      description: >-\n        Receives webhook notifications from DoorDash when a report has\n        been generated and is ready for download.\n      message:\n        $ref: '#/components/messages/ReportReady'\ncomponents:\n  securitySchemes:\n    basicAuth:\n      type: http\n      scheme: basic\n      description: >-\n        Basic authentication for webhook endpoint security.\n  messages:\n    ReportReady:\n      name: ReportReady\n      title: Report Ready Event\n      summary: >-\n        A report has been generated and is ready for download.\n      payload:\n        $ref: '#/components/schemas/ReportReadyPayload'\n  schemas:\n    ReportReadyPayload:\n      type: object\n      properties:\n        report_id:\n          type: string\n          description: >-\n            The unique identifier for the report.\n        report_type:\n          type: string\n  \
  \        description: >-\n            The type of report that was generated.\n          enum:\n            - financial\n            - operations\n            - menu\n            - feedback\n        status:\n          type: string\n          description: >-\n            The report processing status.\n          enum:\n            - SUCCEEDED\n            - FAILED\n        download_url:\n          type: string\n          format: uri\n          description: >-\n            A temporary URL to download the report. Only present when\n            status is SUCCEEDED.\n        error_message:\n          type: string\n          description: >-\n            Error details if report generation failed. Only present when\n            status is FAILED.\n        created_at:\n          type: string\n          format: date-time\n          description: >-\n            When the report request was originally created.\n        completed_at:\n          type: string\n          format: date-time\n          description:\
  \ >-\n            When the report generation completed.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/asyncapi/doordash-reporting-webhooks-asyncapi.yml
spec_file: asyncapi/doordash-reporting-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/asyncapi/doordash-reporting-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
