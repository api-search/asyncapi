---
channels:
- description: CircleCI delivers webhook events as HTTP POST requests with JSON payloads to the configured endpoint URL. Each delivery includes a circleci-signature header containing an HMAC SHA256 digest of the request body for verification.
  name: /webhook
  operation: publish
  operation_id: receiveCircleCIWebhook
  summary: Receive CircleCI webhook events
description: CircleCI Webhooks allow developers to receive real-time notifications about events in their CI/CD pipelines by configuring HTTP callbacks. Webhooks can be set up through project settings or the API to notify external services when workflows and jobs complete, fail, or change status. This enables integration with monitoring systems, chat platforms, and custom automation workflows. Webhooks deliver JSON payloads via HTTP POST to configured endpoint URLs, signed with HMAC SHA256 for verification.
layout: asyncapi
messages:
- description: This event is triggered when a workflow reaches a terminal state (success, failed, error, canceled, or unauthorized). The payload contains information about the workflow, its pipeline, the project, the organization, and the trigger that started the pipeline. Use this event to track workflow completi
  name: WorkflowCompleted
  summary: Fired when all jobs in a workflow have finished running.
  title: Workflow Completed Event
- description: This event is triggered when a job reaches a terminal state (success, failed, canceled, or infrastructure_fail). The payload contains information about the specific job, the workflow it belongs to, the pipeline, the project, and the organization. Use this event for fine-grained tracking of individua
  name: JobCompleted
  summary: Fired when all steps in a job have completed.
  title: Job Completed Event
name: CircleCI Webhooks
provider_name: CircleCI
provider_slug: circleci
servers:
- description: Your webhook endpoint URL. CircleCI sends HTTP POST requests to this URL when events occur. The URL is configured when creating a webhook subscription via project settings or the API.
  name: circleci
  protocol: https
  url: '{webhookUrl}'
slug: circleci-webhooks-asyncapi
spec_file: asyncapi/circleci-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/circleci/refs/heads/main/asyncapi/circleci-webhooks-asyncapi.yml
tags:
- CI/CD
- Continuous Integration
- Continuous Deployment
- DevOps
- Pipelines
- Workflows
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
