---
channels:
- description: HTTP webhook channel for receiving events from external systems such as GitHub, GitLab, Bitbucket, or custom HTTP callers. Each EventSource can define multiple named webhook endpoints on different ports.
  name: /webhook/{eventName}
  operation: subscribe
  operation_id: receiveWebhookEvent
  summary: Receive an HTTP webhook event
- description: Internal EventBus channel through which EventSources publish events and Sensors consume them. The EventBus is backed by NATS JetStream or Apache Kafka depending on the EventBus configuration.
  name: /eventsource/{namespace}/{eventSourceName}/{eventName}
  operation: publish
  operation_id: publishEventToEventBus
  summary: EventSource publishes event to EventBus
description: Argo Events is a Kubernetes-native event-driven automation framework that listens to over 20 event sources and triggers Argo Workflows, Kubernetes objects, HTTP requests, and other actions in response. Event sources include webhooks, S3 bucket notifications, GitHub/GitLab webhooks, Kafka topics, NATS subjects, Redis streams, GCP Pub/Sub, SNS/SQS, cron schedules, and resource watches. Sensors define the event dependencies and trigger targets.
layout: asyncapi
messages:
- description: An arbitrary HTTP POST body received by the Argo Events webhook EventSource. The raw body bytes are wrapped in a CloudEvent and published to the EventBus. The content type and structure depend on the sending application.
  name: WebhookEvent
  summary: A generic HTTP webhook payload received by an EventSource
  title: Generic Webhook Event
- description: A webhook event delivered by GitHub to the Argo Events GitHub EventSource. The event type is identified by the X-GitHub-Event header. Argo Events validates the HMAC signature and publishes the event to the EventBus. Common event types include push, pull_request, release, and create.
  name: GitHubEvent
  summary: A GitHub webhook event payload
  title: GitHub Webhook Event
- description: A webhook event delivered by GitLab to the Argo Events GitLab EventSource. The event type is identified by the X-Gitlab-Event header. Argo Events validates the X-Gitlab-Token secret header and publishes the event to the EventBus.
  name: GitLabEvent
  summary: A GitLab webhook event payload
  title: GitLab Webhook Event
- description: All events flowing through the Argo Events EventBus are wrapped in a CloudEvents 1.0 envelope. The data field contains the original event payload from the EventSource. Sensors use the source and type fields to match events to their dependency conditions.
  name: CloudEvent
  summary: A CloudEvents 1.0 envelope wrapping an Argo Events payload
  title: Argo Events CloudEvent
name: Argo Events
provider_name: Argo
provider_slug: argo
servers:
- description: Argo Events webhook EventSource service. Each EventSource that exposes an HTTP endpoint is deployed as a Kubernetes Service. The host and port depend on the EventSource configuration.
  name: argoEventsWebhook
  protocol: http
  url: http://{eventsource-service}:{port}
slug: argo-events-asyncapi
spec_file: asyncapi/argo-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/argo/refs/heads/main/asyncapi/argo-events-asyncapi.yml
tags:
- CNCF
- CI/CD
- GitOps
- Kubernetes
- Open Source
- Progressive Delivery
- Workflow Engine
- AsyncAPI
- Webhooks
- Events
version: v1.9
---
