---
channels:
- description: A named resource to which messages are sent by publishers and from which messages are delivered to subscribers.
  name: projects/{projectId}/topics/{topicId}
  operation: publish
  operation_id: publishMessage
  summary: Publish a message to a topic
- description: A named resource representing the stream of messages from a single specific topic to be delivered to the subscribing application.
  name: projects/{projectId}/subscriptions/{subscriptionId}
  operation: subscribe
  operation_id: pullMessage
  summary: Pull messages from a subscription
description: Google Cloud Pub/Sub is a fully managed real-time messaging service that allows you to send and receive messages between independent applications. This AsyncAPI spec describes the event-driven messaging patterns for publishing and subscribing to messages via Pub/Sub topics.
layout: asyncapi
messages:
- description: ''
  name: PubsubMessage
  summary: A message published to or received from a Pub/Sub topic.
  title: Pub/Sub Message
- description: ''
  name: ReceivedMessage
  summary: A message received from a subscription with acknowledgement metadata.
  title: Received Message
- description: ''
  name: PushNotification
  summary: HTTP POST body sent by Pub/Sub to a push subscription endpoint.
  title: Push Notification
name: Google Cloud Pub/Sub
provider_name: Google Pub/Sub
provider_slug: google-pub-sub
servers:
- description: Google Cloud Pub/Sub service endpoint
  name: google-cloud
  protocol: https
  url: pubsub.googleapis.com
slug: google-pub-sub-asyncapi
source_filename: google-pub-sub-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Google Cloud Pub/Sub\n  version: v1\n  description: >-\n    Google Cloud Pub/Sub is a fully managed real-time messaging service that\n    allows you to send and receive messages between independent applications.\n    This AsyncAPI spec describes the event-driven messaging patterns for\n    publishing and subscribing to messages via Pub/Sub topics.\n  contact:\n    name: Google Cloud\n    url: https://cloud.google.com/pubsub\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\nservers:\n  google-cloud:\n    url: pubsub.googleapis.com\n    protocol: https\n    description: Google Cloud Pub/Sub service endpoint\nchannels:\n  projects/{projectId}/topics/{topicId}:\n    description: >-\n      A named resource to which messages are sent by publishers and from which\n      messages are delivered to subscribers.\n    parameters:\n      projectId:\n        description: The Google Cloud project ID.\n        schema:\n\
  \          type: string\n      topicId:\n        description: The Pub/Sub topic ID.\n        schema:\n          type: string\n    publish:\n      operationId: publishMessage\n      summary: Publish a message to a topic\n      description: >-\n        Publishers send messages to a Pub/Sub topic. Messages contain a\n        base64-encoded data payload and optional attributes.\n      message:\n        $ref: '#/components/messages/PubsubMessage'\n    subscribe:\n      operationId: receiveMessage\n      summary: Receive a message from a topic via subscription\n      description: >-\n        Subscribers receive messages delivered from a topic either via push\n        (HTTP POST to an endpoint) or pull (polling the Pub/Sub API).\n      message:\n        $ref: '#/components/messages/PubsubMessage'\n  projects/{projectId}/subscriptions/{subscriptionId}:\n    description: >-\n      A named resource representing the stream of messages from a single\n      specific topic to be delivered to the subscribing\
  \ application.\n    parameters:\n      projectId:\n        description: The Google Cloud project ID.\n        schema:\n          type: string\n      subscriptionId:\n        description: The subscription ID.\n        schema:\n          type: string\n    subscribe:\n      operationId: pullMessage\n      summary: Pull messages from a subscription\n      description: >-\n        Pull messages from a subscription. The subscriber acknowledges\n        messages after processing them.\n      message:\n        $ref: '#/components/messages/ReceivedMessage'\ncomponents:\n  messages:\n    PubsubMessage:\n      name: PubsubMessage\n      title: Pub/Sub Message\n      summary: A message published to or received from a Pub/Sub topic.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          data:\n            type: string\n            format: byte\n            description: The message data field (base64 encoded).\n          attributes:\n            type:\
  \ object\n            additionalProperties:\n              type: string\n            description: Attributes for this message as key-value pairs.\n          messageId:\n            type: string\n            description: ID of this message assigned by the server at publication time.\n          publishTime:\n            type: string\n            format: date-time\n            description: The time at which the message was published.\n          orderingKey:\n            type: string\n            description: Key for ordering delivery to subscribers.\n    ReceivedMessage:\n      name: ReceivedMessage\n      title: Received Message\n      summary: A message received from a subscription with acknowledgement metadata.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          ackId:\n            type: string\n            description: Acknowledgement ID used to acknowledge the message.\n          message:\n            type: object\n            properties:\n\
  \              data:\n                type: string\n                format: byte\n              attributes:\n                type: object\n                additionalProperties:\n                  type: string\n              messageId:\n                type: string\n              publishTime:\n                type: string\n                format: date-time\n              orderingKey:\n                type: string\n          deliveryAttempt:\n            type: integer\n            description: The approximate number of times the message has been delivered.\n    PushNotification:\n      name: PushNotification\n      title: Push Notification\n      summary: >-\n        HTTP POST body sent by Pub/Sub to a push subscription endpoint.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          message:\n            type: object\n            properties:\n              data:\n                type: string\n                format: byte\n            \
  \  attributes:\n                type: object\n                additionalProperties:\n                  type: string\n              messageId:\n                type: string\n              publishTime:\n                type: string\n                format: date-time\n          subscription:\n            type: string\n            description: The full subscription resource name.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/google-pub-sub/refs/heads/main/asyncapi/google-pub-sub-asyncapi.yml
spec_file: asyncapi/google-pub-sub-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/google-pub-sub/refs/heads/main/asyncapi/google-pub-sub-asyncapi.yml
tags:
- Cloud
- Event-Driven
- Google Cloud
- Messaging
- Pub/Sub
- Streaming
- AsyncAPI
- Webhooks
- Events
version: v1
---
