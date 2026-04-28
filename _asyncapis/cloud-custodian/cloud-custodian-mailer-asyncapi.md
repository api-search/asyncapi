---
channels:
- description: Channel through which Cloud Custodian publishes policy violation notification messages. Each message describes the policy that matched, the resources that were affected, and the account context. The c7n-mailer subscribes to this channel to deliver alerts to operators.
  name: /policy-notification
  operation: publish
  operation_id: publishPolicyNotification
  summary: Publish Policy Notification
description: The Cloud Custodian c7n-mailer AsyncAPI defines the event-driven notification interface used by the Cloud Custodian policy engine to deliver policy violation alerts. When a policy's notify action fires, the Custodian runtime encodes a structured message payload and publishes it to an AWS SQS queue. The c7n-mailer daemon dequeues these messages and delivers notifications via email (SES), Slack, DataDog, Splunk, or webhook endpoints. Messages are base64-encoded, gzip-compressed JSON identified by the maidmsg/1.0 message type.
layout: asyncapi
messages:
- description: ''
  name: PolicyNotification
  summary: A notification message emitted by a Cloud Custodian policy notify action describing the matched resources and execution context.
  title: Cloud Custodian Policy Notification
name: Cloud Custodian c7n-mailer Notification Events
provider_name: Cloud Custodian
provider_slug: cloud-custodian
servers:
- description: AWS SQS queue that receives policy notification messages from Cloud Custodian notify actions. The c7n-mailer daemon polls this queue and processes messages for delivery to configured notification channels.
  name: aws-sqs
  protocol: https
  url: https://sqs.{region}.amazonaws.com/{account-id}/{queue-name}
slug: cloud-custodian-mailer-asyncapi
spec_file: asyncapi/cloud-custodian-mailer-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/cloud-custodian/refs/heads/main/asyncapi/cloud-custodian-mailer-asyncapi.yml
tags:
- Cloud Security
- Compliance
- Cost Optimization
- Multi-Cloud
- Policy as Code
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
