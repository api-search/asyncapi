---
api_specs:
- filename: red5-server-api-openapi.yml
  format: yaml
  label: Red5 Pro Server API
  slug: server-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/openapi/red5-server-api-openapi.yml
- filename: red5-stream-manager-2-openapi.yml
  format: yaml
  label: Red5 Pro Stream Manager 2.0 API
  slug: stream-manager-2-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/openapi/red5-stream-manager-2-openapi.yml
- filename: red5-brew-mixer-api-openapi.yml
  format: yaml
  label: Red5 Pro Brew Mixer API
  slug: brew-mixer-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/openapi/red5-brew-mixer-api-openapi.yml
- filename: red5-restreamer-api-openapi.yml
  format: yaml
  label: Red5 Pro Restreamer API
  slug: restreamer-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/openapi/red5-restreamer-api-openapi.yml
- filename: red5-webrtc-streaming-asyncapi.yml
  format: yaml
  label: Red5 Pro WebRTC SDK
  slug: webrtc-sdk
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/asyncapi/red5-webrtc-streaming-asyncapi.yml
channels:
- description: WebSocket channel for a publisher to establish a WebRTC session and broadcast a live stream to the Red5 Pro server. The publisher sends an SDP offer and ICE candidates; the server responds with an SDP answer and its ICE candidates.
  name: /publish
  operation: publish
  operation_id: publisherSend
  summary: Publisher sends signaling message to server
- description: WebSocket channel for a subscriber to establish a WebRTC session and receive a live stream from the Red5 Pro server. The subscriber sends an SDP offer and ICE candidates; the server responds with an SDP answer and its ICE candidates.
  name: /subscribe
  operation: publish
  operation_id: subscriberSend
  summary: Subscriber sends signaling message to server
description: AsyncAPI specification for the Red5 Pro WebRTC streaming event system, covering WebSocket signaling messages exchanged during publish and subscribe sessions. Red5 Pro WebRTC uses WebSocket connections for signaling SDP offers, answers, and ICE candidates between clients and the streaming server. This specification documents the message types and payloads used in the WebRTC session lifecycle.
layout: asyncapi
messages:
- description: Sent by a WebRTC publisher to initiate a broadcast session on the server. Contains the stream name and any authentication credentials.
  name: PublishRequest
  summary: Initial request from a publisher to start a streaming session
  title: Publish Stream Request
- description: Sent by a WebRTC subscriber to initiate playback of a live stream from the server. Contains the stream name to subscribe to.
  name: SubscribeRequest
  summary: Initial request from a subscriber to join a streaming session
  title: Subscribe Stream Request
- description: Session Description Protocol (SDP) offer sent from a WebRTC client (publisher or subscriber) to the server to negotiate media capabilities and establish the peer connection.
  name: SdpOffer
  summary: WebRTC SDP offer from a client
  title: SDP Offer
- description: Session Description Protocol (SDP) answer sent from the Red5 Pro server in response to a client's SDP offer, completing the WebRTC negotiation.
  name: SdpAnswer
  summary: WebRTC SDP answer from the server
  title: SDP Answer
- description: Interactive Connectivity Establishment (ICE) candidate message exchanged between the client and server to discover and negotiate network paths for the WebRTC media connection.
  name: IceCandidate
  summary: ICE candidate for WebRTC peer connection establishment
  title: ICE Candidate
- description: Notification from the Red5 Pro server about changes in stream state, such as stream started, stopped, error conditions, or publisher disconnected.
  name: StreamEvent
  summary: Server-sent event about stream state changes
  title: Stream Lifecycle Event
name: Red5 Pro WebRTC Streaming Events
provider_name: Red5
provider_slug: red5
servers:
- description: Red5 Pro WebRTC WebSocket signaling endpoint for live streaming. Clients connect per-stream for publish or subscribe sessions.
  name: red5ProServer
  protocol: wss
  url: wss://{host}:443/live/{streamName}
slug: red5-webrtc-streaming-asyncapi
source_filename: red5-webrtc-streaming-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Red5 Pro WebRTC Streaming Events\n  description: >-\n    AsyncAPI specification for the Red5 Pro WebRTC streaming event system,\n    covering WebSocket signaling messages exchanged during publish and subscribe\n    sessions. Red5 Pro WebRTC uses WebSocket connections for signaling SDP\n    offers, answers, and ICE candidates between clients and the streaming server.\n    This specification documents the message types and payloads used in the\n    WebRTC session lifecycle.\n  version: '1.0'\n  contact:\n    name: Red5 Support\n    url: https://www.red5.net/contact/\nexternalDocs:\n  description: Red5 Pro WebRTC SDK Documentation\n  url: https://www.red5.net/docs/red5-pro/development/sdks/red5-webrtc-sdk/\nservers:\n  red5ProServer:\n    url: 'wss://{host}:443/live/{streamName}'\n    protocol: wss\n    description: >-\n      Red5 Pro WebRTC WebSocket signaling endpoint for live streaming.\n      Clients connect per-stream for publish or subscribe\
  \ sessions.\n    variables:\n      host:\n        description: Hostname or IP of the Red5 Pro server\n        default: localhost\n      streamName:\n        description: Name of the stream to publish or subscribe to\n        default: mystream\n    security:\n      - bearerToken: []\nchannels:\n  /publish:\n    description: >-\n      WebSocket channel for a publisher to establish a WebRTC session and\n      broadcast a live stream to the Red5 Pro server. The publisher sends\n      an SDP offer and ICE candidates; the server responds with an SDP answer\n      and its ICE candidates.\n    publish:\n      operationId: publisherSend\n      summary: Publisher sends signaling message to server\n      message:\n        oneOf:\n          - $ref: '#/components/messages/SdpOffer'\n          - $ref: '#/components/messages/IceCandidate'\n          - $ref: '#/components/messages/PublishRequest'\n    subscribe:\n      operationId: publisherReceive\n      summary: Publisher receives signaling message\
  \ from server\n      message:\n        oneOf:\n          - $ref: '#/components/messages/SdpAnswer'\n          - $ref: '#/components/messages/IceCandidate'\n          - $ref: '#/components/messages/StreamEvent'\n  /subscribe:\n    description: >-\n      WebSocket channel for a subscriber to establish a WebRTC session and\n      receive a live stream from the Red5 Pro server. The subscriber sends\n      an SDP offer and ICE candidates; the server responds with an SDP answer\n      and its ICE candidates.\n    publish:\n      operationId: subscriberSend\n      summary: Subscriber sends signaling message to server\n      message:\n        oneOf:\n          - $ref: '#/components/messages/SdpOffer'\n          - $ref: '#/components/messages/IceCandidate'\n          - $ref: '#/components/messages/SubscribeRequest'\n    subscribe:\n      operationId: subscriberReceive\n      summary: Subscriber receives signaling message from server\n      message:\n        oneOf:\n          - $ref: '#/components/messages/SdpAnswer'\n\
  \          - $ref: '#/components/messages/IceCandidate'\n          - $ref: '#/components/messages/StreamEvent'\ncomponents:\n  securitySchemes:\n    bearerToken:\n      type: http\n      scheme: bearer\n      description: JWT bearer token for authenticating WebSocket connections\n  messages:\n    PublishRequest:\n      name: PublishRequest\n      title: Publish Stream Request\n      summary: Initial request from a publisher to start a streaming session\n      description: >-\n        Sent by a WebRTC publisher to initiate a broadcast session on the server.\n        Contains the stream name and any authentication credentials.\n      payload:\n        $ref: '#/components/schemas/PublishRequestPayload'\n    SubscribeRequest:\n      name: SubscribeRequest\n      title: Subscribe Stream Request\n      summary: Initial request from a subscriber to join a streaming session\n      description: >-\n        Sent by a WebRTC subscriber to initiate playback of a live stream\n        from the server.\
  \ Contains the stream name to subscribe to.\n      payload:\n        $ref: '#/components/schemas/SubscribeRequestPayload'\n    SdpOffer:\n      name: SdpOffer\n      title: SDP Offer\n      summary: WebRTC SDP offer from a client\n      description: >-\n        Session Description Protocol (SDP) offer sent from a WebRTC client\n        (publisher or subscriber) to the server to negotiate media capabilities\n        and establish the peer connection.\n      payload:\n        $ref: '#/components/schemas/SdpPayload'\n    SdpAnswer:\n      name: SdpAnswer\n      title: SDP Answer\n      summary: WebRTC SDP answer from the server\n      description: >-\n        Session Description Protocol (SDP) answer sent from the Red5 Pro server\n        in response to a client's SDP offer, completing the WebRTC negotiation.\n      payload:\n        $ref: '#/components/schemas/SdpPayload'\n    IceCandidate:\n      name: IceCandidate\n      title: ICE Candidate\n      summary: ICE candidate for WebRTC peer\
  \ connection establishment\n      description: >-\n        Interactive Connectivity Establishment (ICE) candidate message exchanged\n        between the client and server to discover and negotiate network paths\n        for the WebRTC media connection.\n      payload:\n        $ref: '#/components/schemas/IceCandidatePayload'\n    StreamEvent:\n      name: StreamEvent\n      title: Stream Lifecycle Event\n      summary: Server-sent event about stream state changes\n      description: >-\n        Notification from the Red5 Pro server about changes in stream state,\n        such as stream started, stopped, error conditions, or publisher disconnected.\n      payload:\n        $ref: '#/components/schemas/StreamEventPayload'\n  schemas:\n    PublishRequestPayload:\n      type: object\n      description: Payload for initiating a WebRTC publish session\n      required:\n        - type\n        - streamName\n      properties:\n        type:\n          type: string\n          description: Message\
  \ type identifier\n          const: publishRequest\n        streamName:\n          type: string\n          description: Name of the stream to publish\n        username:\n          type: string\n          description: Publisher authentication username if required\n        password:\n          type: string\n          description: Publisher authentication password if required\n        record:\n          type: boolean\n          description: Whether to enable server-side recording of this stream\n          default: false\n    SubscribeRequestPayload:\n      type: object\n      description: Payload for initiating a WebRTC subscribe session\n      required:\n        - type\n        - streamName\n      properties:\n        type:\n          type: string\n          description: Message type identifier\n          const: subscribeRequest\n        streamName:\n          type: string\n          description: Name of the stream to subscribe to\n    SdpPayload:\n      type: object\n      description:\
  \ WebRTC Session Description Protocol message payload\n      required:\n        - type\n        - sdp\n      properties:\n        type:\n          type: string\n          description: SDP message type (offer or answer)\n          enum:\n            - offer\n            - answer\n        sdp:\n          type: string\n          description: SDP body string containing media negotiation details\n    IceCandidatePayload:\n      type: object\n      description: WebRTC ICE candidate message payload\n      required:\n        - type\n        - candidate\n      properties:\n        type:\n          type: string\n          description: Message type identifier\n          const: iceCandidate\n        candidate:\n          type: string\n          description: ICE candidate string in RFC 5245 format\n        sdpMid:\n          type: string\n          description: Media stream identification tag this candidate is associated with\n        sdpMLineIndex:\n          type: integer\n          description:\
  \ Index of the media description in the SDP for this candidate\n          minimum: 0\n    StreamEventPayload:\n      type: object\n      description: Server-sent stream lifecycle event payload\n      required:\n        - type\n        - code\n      properties:\n        type:\n          type: string\n          description: Message type identifier\n          const: event\n        code:\n          type: string\n          description: Event code identifying the stream state change\n          enum:\n            - NetStream.Play.Start\n            - NetStream.Play.Stop\n            - NetStream.Play.Failed\n            - NetStream.Publish.Start\n            - NetStream.Publish.BadName\n            - NetStream.Unpublish.Success\n            - NetConnection.Connect.Success\n            - NetConnection.Connect.Failed\n            - NetConnection.Connect.Closed\n        level:\n          type: string\n          description: Event severity level\n          enum:\n            - status\n           \
  \ - warning\n            - error\n        description:\n          type: string\n          description: Human-readable description of the event\n        streamName:\n          type: string\n          description: Name of the stream this event relates to\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/asyncapi/red5-webrtc-streaming-asyncapi.yml
spec_file: asyncapi/red5-webrtc-streaming-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/red5/refs/heads/main/asyncapi/red5-webrtc-streaming-asyncapi.yml
tags:
- Live Streaming
- Media
- Real-Time
- RTMP
- Streaming
- Video
- WebRTC
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
