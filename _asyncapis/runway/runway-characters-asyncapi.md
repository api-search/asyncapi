---
api_specs:
- filename: runway-video-generation-openapi.yml
  format: yaml
  label: Runway Video Generation API
  slug: video-generation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/runway/refs/heads/main/openapi/runway-video-generation-openapi.yml
- filename: runway-image-generation-openapi.yml
  format: yaml
  label: Runway Image Generation API
  slug: image-generation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/runway/refs/heads/main/openapi/runway-image-generation-openapi.yml
- filename: runway-characters-openapi.yml
  format: yaml
  label: Runway Characters API
  slug: characters
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/runway/refs/heads/main/openapi/runway-characters-openapi.yml
channels:
- description: Bidirectional audio channel for real-time voice communication between the user and the avatar. The user sends microphone audio, and the avatar responds with synthesized speech audio.
  name: /session/audio
  operation: publish
  operation_id: sendUserAudio
  summary: Send user audio to avatar
- description: Video channel carrying the avatar's real-time generated video stream to the user. The avatar produces photorealistic or animated video frames showing facial expressions, lip movements, and gestures synchronized with the conversation.
  name: /session/video
  operation: subscribe
  operation_id: receiveAvatarVideo
  summary: Receive avatar video stream
- description: Data channel for exchanging session control messages and metadata between the client and server, including session state changes, errors, and transcript data.
  name: /session/data
  operation: publish
  operation_id: sendControlMessage
  summary: Send session control message
description: The Runway Characters realtime event interface describes the WebRTC-based communication protocol for live conversational avatar sessions powered by GWM-1. Once a realtime session is created via the REST API, clients connect to a WebRTC room and exchange audio, video, and data channel messages with the avatar in real time. Sessions support bidirectional audio and video streams with a maximum duration of 5 minutes.
layout: asyncapi
messages:
- description: ''
  name: AudioStream
  summary: Real-time audio data for bidirectional voice communication.
  title: Audio Stream
- description: ''
  name: VideoStream
  summary: Real-time video frames from the avatar showing facial expressions and lip movements synchronized with speech.
  title: Video Stream
- description: ''
  name: SessionControlMessage
  summary: Client-initiated control message for managing session behavior.
  title: Session Control Message
- description: ''
  name: SessionStateEvent
  summary: Server-sent event indicating a change in session state.
  title: Session State Event
- description: ''
  name: TranscriptEvent
  summary: Server-sent event containing transcript data from the conversation, including both user speech and avatar responses.
  title: Transcript Event
- description: ''
  name: SessionErrorEvent
  summary: Server-sent event indicating an error occurred during the session.
  title: Session Error Event
name: Runway Characters Realtime Events
provider_name: Runway
provider_slug: runway
servers:
- description: WebRTC signaling server for realtime avatar sessions. The server URL is provided dynamically when a session is created via the REST API.
  name: realtimeServer
  protocol: wss
  url: '{serverUrl}'
slug: runway-characters-asyncapi
source_filename: runway-characters-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Runway Characters Realtime Events\n  description: >-\n    The Runway Characters realtime event interface describes the WebRTC-based\n    communication protocol for live conversational avatar sessions powered by\n    GWM-1. Once a realtime session is created via the REST API, clients connect\n    to a WebRTC room and exchange audio, video, and data channel messages with\n    the avatar in real time. Sessions support bidirectional audio and video\n    streams with a maximum duration of 5 minutes.\n  version: '2024-11-06'\n  contact:\n    name: Runway Support\n    url: https://support.runwayml.com/\nservers:\n  realtimeServer:\n    url: '{serverUrl}'\n    protocol: wss\n    description: >-\n      WebRTC signaling server for realtime avatar sessions. The server URL is\n      provided dynamically when a session is created via the REST API.\n    variables:\n      serverUrl:\n        description: >-\n          The WebRTC server URL returned by the\
  \ POST /v1/realtime_sessions\n          endpoint.\n    security:\n      - sessionToken: []\nchannels:\n  /session/audio:\n    description: >-\n      Bidirectional audio channel for real-time voice communication between the\n      user and the avatar. The user sends microphone audio, and the avatar\n      responds with synthesized speech audio.\n    publish:\n      operationId: sendUserAudio\n      summary: Send user audio to avatar\n      description: >-\n        User sends their microphone audio stream to the avatar for processing.\n        The avatar listens, interprets the speech, and formulates a response.\n      message:\n        $ref: '#/components/messages/AudioStream'\n    subscribe:\n      operationId: receiveAvatarAudio\n      summary: Receive avatar audio response\n      description: >-\n        The avatar sends synthesized speech audio back to the user as part of\n        the conversational interaction.\n      message:\n        $ref: '#/components/messages/AudioStream'\n  /session/video:\n\
  \    description: >-\n      Video channel carrying the avatar's real-time generated video stream to\n      the user. The avatar produces photorealistic or animated video frames\n      showing facial expressions, lip movements, and gestures synchronized\n      with the conversation.\n    subscribe:\n      operationId: receiveAvatarVideo\n      summary: Receive avatar video stream\n      description: >-\n        The avatar sends a continuous video stream showing the character's face,\n        expressions, and lip movements synchronized with the audio response.\n      message:\n        $ref: '#/components/messages/VideoStream'\n  /session/data:\n    description: >-\n      Data channel for exchanging session control messages and metadata between\n      the client and server, including session state changes, errors, and\n      transcript data.\n    publish:\n      operationId: sendControlMessage\n      summary: Send session control message\n      description: >-\n        Client sends control\
  \ messages to manage the session, such as mute/unmute\n        or session termination signals.\n      message:\n        $ref: '#/components/messages/SessionControlMessage'\n    subscribe:\n      operationId: receiveSessionEvent\n      summary: Receive session event\n      description: >-\n        The server sends session events including state transitions, transcript\n        updates, and error notifications.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/SessionStateEvent'\n          - $ref: '#/components/messages/TranscriptEvent'\n          - $ref: '#/components/messages/SessionErrorEvent'\ncomponents:\n  securitySchemes:\n    sessionToken:\n      type: httpApiKey\n      name: token\n      in: query\n      description: >-\n        Session authentication token returned by the POST /v1/realtime_sessions\n        endpoint. This token can only be used once. If the WebRTC connection\n        fails after the token is consumed, a new session must be created.\n  messages:\n\
  \    AudioStream:\n      name: AudioStream\n      title: Audio Stream\n      summary: >-\n        Real-time audio data for bidirectional voice communication.\n      contentType: audio/opus\n      payload:\n        type: string\n        format: binary\n        description: >-\n          Raw audio data encoded in Opus format for low-latency voice\n          transmission over WebRTC.\n    VideoStream:\n      name: VideoStream\n      title: Video Stream\n      summary: >-\n        Real-time video frames from the avatar showing facial expressions and\n        lip movements synchronized with speech.\n      contentType: video/vp8\n      payload:\n        type: string\n        format: binary\n        description: >-\n          Encoded video frames showing the avatar's real-time generated\n          appearance and movements.\n    SessionControlMessage:\n      name: SessionControlMessage\n      title: Session Control Message\n      summary: >-\n        Client-initiated control message for managing\
  \ session behavior.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SessionControl'\n    SessionStateEvent:\n      name: SessionStateEvent\n      title: Session State Event\n      summary: >-\n        Server-sent event indicating a change in session state.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SessionState'\n    TranscriptEvent:\n      name: TranscriptEvent\n      title: Transcript Event\n      summary: >-\n        Server-sent event containing transcript data from the conversation,\n        including both user speech and avatar responses.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/Transcript'\n    SessionErrorEvent:\n      name: SessionErrorEvent\n      title: Session Error Event\n      summary: >-\n        Server-sent event indicating an error occurred during the session.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SessionError'\n\
  \  schemas:\n    SessionControl:\n      type: object\n      required:\n        - type\n      properties:\n        type:\n          type: string\n          description: >-\n            The type of control action to perform.\n          enum:\n            - mute\n            - unmute\n            - end_session\n        metadata:\n          type: object\n          description: >-\n            Optional metadata associated with the control action.\n          additionalProperties: true\n    SessionState:\n      type: object\n      required:\n        - type\n        - state\n        - timestamp\n      properties:\n        type:\n          type: string\n          description: >-\n            The event type identifier.\n          const: session_state\n        state:\n          type: string\n          description: >-\n            The current state of the session.\n          enum:\n            - connecting\n            - connected\n            - speaking\n            - listening\n            - thinking\n\
  \            - ended\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            The timestamp when the state change occurred.\n    Transcript:\n      type: object\n      required:\n        - type\n        - role\n        - text\n        - timestamp\n      properties:\n        type:\n          type: string\n          description: >-\n            The event type identifier.\n          const: transcript\n        role:\n          type: string\n          description: >-\n            The speaker role for this transcript segment.\n          enum:\n            - user\n            - avatar\n        text:\n          type: string\n          description: >-\n            The transcribed text of the spoken content.\n        isFinal:\n          type: boolean\n          description: >-\n            Whether this transcript segment is final or still being updated\n            as more audio is processed.\n        timestamp:\n          type: string\n  \
  \        format: date-time\n          description: >-\n            The timestamp when this transcript segment was generated.\n    SessionError:\n      type: object\n      required:\n        - type\n        - error\n        - timestamp\n      properties:\n        type:\n          type: string\n          description: >-\n            The event type identifier.\n          const: session_error\n        error:\n          type: string\n          description: >-\n            A human-readable description of the error.\n        code:\n          type: string\n          description: >-\n            A machine-readable error code.\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            The timestamp when the error occurred.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/runway/refs/heads/main/asyncapi/runway-characters-asyncapi.yml
spec_file: asyncapi/runway-characters-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/runway/refs/heads/main/asyncapi/runway-characters-asyncapi.yml
tags:
- Video Generation
- Image Generation
- Artificial Intelligence
- Machine Learning
- Generative AI
- Avatars
- Characters
- WebRTC
- Creative Tools
- AsyncAPI
- Webhooks
- Events
version: '2024-11-06'
---
