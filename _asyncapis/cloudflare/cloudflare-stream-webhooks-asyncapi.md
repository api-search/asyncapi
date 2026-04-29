---
channels:
- description: Webhook channel that receives video processing and live streaming event notifications from Cloudflare Stream.
  name: /webhook
  operation: publish
  operation_id: onStreamEvent
  summary: Receive Stream video event
description: Cloudflare Stream sends webhook notifications when videos finish processing and are ready to stream, or when a video enters an error state. Webhooks can also be configured for live streaming events. Configure a webhook URL in the Stream dashboard or via the API to receive these notifications.
layout: asyncapi
messages:
- description: Sent when a video upload has been successfully processed, encoded, and is available for playback. The payload includes the video UID, metadata, playback URLs, and duration.
  name: VideoReady
  summary: Notification that a video has been processed and is ready to stream
  title: Video Ready
- description: Sent when a video upload fails during processing or encoding. The payload includes error details and the video UID for troubleshooting.
  name: VideoError
  summary: Notification that video processing has encountered an error
  title: Video Error
- description: Sent when a live input begins receiving and broadcasting a live stream via RTMPS or SRT.
  name: LiveStreamStarted
  summary: Notification that a live stream has started
  title: Live Stream Started
- description: Sent when a live stream stops broadcasting. If recording is enabled, the recorded video will begin processing.
  name: LiveStreamEnded
  summary: Notification that a live stream has ended
  title: Live Stream Ended
name: Cloudflare Stream Webhooks
provider_name: Cloudflare
provider_slug: cloudflare
servers:
- description: Your configured webhook endpoint URL. Cloudflare Stream sends HTTP POST requests to this URL when video processing events occur. Validate the webhook-signing-key header to verify request authenticity.
  name: webhookEndpoint
  protocol: https
  url: '{webhookUrl}'
slug: cloudflare-stream-webhooks-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Cloudflare Stream Webhooks\n  description: >-\n    Cloudflare Stream sends webhook notifications when videos finish\n    processing and are ready to stream, or when a video enters an error\n    state. Webhooks can also be configured for live streaming events.\n    Configure a webhook URL in the Stream dashboard or via the API to\n    receive these notifications.\n  version: '1.0'\n  contact:\n    name: Cloudflare Support\n    url: https://support.cloudflare.com/\n  license:\n    name: Cloudflare Terms of Service\n    url: https://www.cloudflare.com/terms/\n  externalDocs:\n    description: Cloudflare Stream Webhooks Documentation\n    url: https://developers.cloudflare.com/stream/manage-video-library/using-webhooks/\nservers:\n  webhookEndpoint:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your configured webhook endpoint URL. Cloudflare Stream sends HTTP\n      POST requests to this URL when video processing events\
  \ occur. Validate\n      the webhook-signing-key header to verify request authenticity.\n    security:\n      - signingKey: []\n    variables:\n      webhookUrl:\n        description: The notification URL configured for Stream webhooks.\nchannels:\n  /webhook:\n    description: >-\n      Webhook channel that receives video processing and live streaming\n      event notifications from Cloudflare Stream.\n    publish:\n      operationId: onStreamEvent\n      summary: Receive Stream video event\n      message:\n        oneOf:\n          - $ref: '#/components/messages/VideoReady'\n          - $ref: '#/components/messages/VideoError'\n          - $ref: '#/components/messages/LiveStreamStarted'\n          - $ref: '#/components/messages/LiveStreamEnded'\ncomponents:\n  securitySchemes:\n    signingKey:\n      type: httpApiKey\n      name: Webhook-Signature\n      in: header\n      description: >-\n        HMAC signature for verifying webhook authenticity. The signature is\n        computed using\
  \ the webhook signing secret and the request body.\n  messages:\n    VideoReady:\n      name: VideoReady\n      title: Video Ready\n      summary: Notification that a video has been processed and is ready to stream\n      description: >-\n        Sent when a video upload has been successfully processed, encoded,\n        and is available for playback. The payload includes the video UID,\n        metadata, playback URLs, and duration.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/VideoReadyPayload'\n    VideoError:\n      name: VideoError\n      title: Video Error\n      summary: Notification that video processing has encountered an error\n      description: >-\n        Sent when a video upload fails during processing or encoding. The\n        payload includes error details and the video UID for troubleshooting.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/VideoErrorPayload'\n    LiveStreamStarted:\n\
  \      name: LiveStreamStarted\n      title: Live Stream Started\n      summary: Notification that a live stream has started\n      description: >-\n        Sent when a live input begins receiving and broadcasting a live\n        stream via RTMPS or SRT.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/LiveStreamEventPayload'\n    LiveStreamEnded:\n      name: LiveStreamEnded\n      title: Live Stream Ended\n      summary: Notification that a live stream has ended\n      description: >-\n        Sent when a live stream stops broadcasting. If recording is enabled,\n        the recorded video will begin processing.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/LiveStreamEventPayload'\n  schemas:\n    VideoReadyPayload:\n      type: object\n      required:\n        - uid\n        - readyToStream\n      properties:\n        uid:\n          type: string\n          description: The unique identifier of the video.\n\
  \        readyToStream:\n          type: boolean\n          description: Whether the video is ready for playback.\n          const: true\n        readyToStreamAt:\n          type: string\n          format: date-time\n          description: When the video became ready for streaming.\n        thumbnail:\n          type: string\n          format: uri\n          description: URL of the video thumbnail.\n        playback:\n          type: object\n          properties:\n            hls:\n              type: string\n              format: uri\n              description: HLS playback URL.\n            dash:\n              type: string\n              format: uri\n              description: DASH playback URL.\n        duration:\n          type: number\n          description: Duration of the video in seconds.\n        size:\n          type: integer\n          description: Size of the video in bytes.\n        meta:\n          type: object\n          description: User-defined metadata associated with\
  \ the video.\n        created:\n          type: string\n          format: date-time\n          description: When the video was uploaded.\n        modified:\n          type: string\n          format: date-time\n          description: When the video was last modified.\n    VideoErrorPayload:\n      type: object\n      required:\n        - uid\n        - readyToStream\n      properties:\n        uid:\n          type: string\n          description: The unique identifier of the video.\n        readyToStream:\n          type: boolean\n          description: Indicates the video is not ready for playback.\n          const: false\n        status:\n          type: object\n          properties:\n            state:\n              type: string\n              const: error\n              description: The error state.\n            errorReasonCode:\n              type: string\n              description: Error reason code.\n            errorReasonText:\n              type: string\n              description:\
  \ Human-readable error description.\n        meta:\n          type: object\n          description: User-defined metadata.\n        created:\n          type: string\n          format: date-time\n    LiveStreamEventPayload:\n      type: object\n      required:\n        - uid\n        - live_input\n      properties:\n        uid:\n          type: string\n          description: The unique identifier of the live stream or recording.\n        live_input:\n          type: string\n          description: The live input identifier.\n        status:\n          type: string\n          description: The current status of the live stream.\n          enum:\n            - connected\n            - disconnected\n        meta:\n          type: object\n          description: User-defined metadata for the live input.\n        created:\n          type: string\n          format: date-time\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cloudflare/refs/heads/main/asyncapi/cloudflare-stream-webhooks-asyncapi.yml
spec_file: asyncapi/cloudflare-stream-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/cloudflare/refs/heads/main/asyncapi/cloudflare-stream-webhooks-asyncapi.yml
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
