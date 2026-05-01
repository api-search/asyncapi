---
api_specs:
- filename: elevenlabs-text-to-speech-openapi.yml
  format: yaml
  label: ElevenLabs Text to Speech API
  slug: text-to-speech
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/openapi/elevenlabs-text-to-speech-openapi.yml
- filename: elevenlabs-speech-to-text-openapi.yml
  format: yaml
  label: ElevenLabs Speech to Text API
  slug: speech-to-text
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/openapi/elevenlabs-speech-to-text-openapi.yml
- filename: elevenlabs-voice-cloning-openapi.yml
  format: yaml
  label: ElevenLabs Voice Cloning API
  slug: voice-cloning
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/openapi/elevenlabs-voice-cloning-openapi.yml
- filename: elevenlabs-voices-openapi.yml
  format: yaml
  label: ElevenLabs Voices API
  slug: voices
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/openapi/elevenlabs-voices-openapi.yml
- filename: elevenlabs-sound-effects-openapi.yml
  format: yaml
  label: ElevenLabs Sound Effects API
  slug: sound-effects
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/openapi/elevenlabs-sound-effects-openapi.yml
- filename: elevenlabs-audio-isolation-openapi.yml
  format: yaml
  label: ElevenLabs Audio Isolation API
  slug: audio-isolation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/openapi/elevenlabs-audio-isolation-openapi.yml
- filename: elevenlabs-dubbing-openapi.yml
  format: yaml
  label: ElevenLabs Dubbing API
  slug: dubbing
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/openapi/elevenlabs-dubbing-openapi.yml
- filename: elevenlabs-voice-changer-openapi.yml
  format: yaml
  label: ElevenLabs Voice Changer API
  slug: voice-changer
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/openapi/elevenlabs-voice-changer-openapi.yml
- filename: elevenlabs-music-openapi.yml
  format: yaml
  label: ElevenLabs Music Generation API
  slug: music
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/openapi/elevenlabs-music-openapi.yml
- filename: elevenlabs-conversational-ai-openapi.yml
  format: yaml
  label: ElevenLabs Conversational AI API
  slug: conversational-ai
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/openapi/elevenlabs-conversational-ai-openapi.yml
- filename: elevenlabs-studio-openapi.yml
  format: yaml
  label: ElevenLabs Studio API
  slug: studio
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/openapi/elevenlabs-studio-openapi.yml
channels:
- description: Webhook channel for receiving conversation transcription data after a Conversational AI call ends. Delivers the full transcript of the conversation.
  name: /post-call-transcription
  operation: publish
  operation_id: receivePostCallTranscription
  summary: Post-call transcription webhook
- description: Webhook channel for receiving conversation audio recordings after a Conversational AI call ends. Audio is delivered as a streaming HTTP request with chunked transfer encoding.
  name: /post-call-audio
  operation: publish
  operation_id: receivePostCallAudio
  summary: Post-call audio webhook
- description: Webhook channel for receiving notifications when a Conversational AI call fails to initiate.
  name: /call-initiation-failure
  operation: publish
  operation_id: receiveCallInitiationFailure
  summary: Call initiation failure webhook
- description: Webhook channel for workspace-level events such as usage alerts, subscription changes, and administrative notifications.
  name: /workspace-events
  operation: publish
  operation_id: receiveWorkspaceEvent
  summary: Workspace event webhook
description: The ElevenLabs Webhook system delivers event notifications to configured endpoints when specific actions occur within the platform. This includes post-call webhooks from Conversational AI conversations delivering transcripts and audio recordings, and workspace-level event notifications. Webhook payloads are signed with HMAC-SHA256 for verification.
layout: asyncapi
messages:
- description: Contains the full transcript of a completed Conversational AI conversation, including speaker roles, timestamps, and metadata. The webhook must return a 200 status code to be considered successful. Webhooks that repeatedly fail are automatically disabled after 10 consecutive failures.
  name: PostCallTranscriptionEvent
  summary: Conversation transcript delivered after call completion
  title: Post-Call Transcription
- description: Contains the audio recording of a completed conversation. Delivered as a streaming HTTP request with the transfer-encoding chunked header. Ensure the receiving endpoint can handle streaming requests and has sufficient storage capacity.
  name: PostCallAudioEvent
  summary: Conversation audio recording delivered after call completion
  title: Post-Call Audio
- description: Sent when a Conversational AI call could not be initiated, including the error reason and agent context.
  name: CallInitiationFailureEvent
  summary: Notification that a call failed to start
  title: Call Initiation Failure
- description: Generic workspace event notification for administrative and operational events.
  name: WorkspaceEvent
  summary: Workspace-level event notification
  title: Workspace Event
name: ElevenLabs Webhook Events
provider_name: elevenlabs
provider_slug: elevenlabs
servers:
- description: The customer's webhook endpoint that receives event notifications from ElevenLabs.
  name: webhookReceiver
  protocol: https
  url: '{webhookUrl}'
slug: elevenlabs-webhooks-asyncapi
source_filename: elevenlabs-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: ElevenLabs Webhook Events\n  description: >-\n    The ElevenLabs Webhook system delivers event notifications to configured\n    endpoints when specific actions occur within the platform. This includes\n    post-call webhooks from Conversational AI conversations delivering\n    transcripts and audio recordings, and workspace-level event\n    notifications. Webhook payloads are signed with HMAC-SHA256 for\n    verification.\n  version: '1.0'\n  contact:\n    name: ElevenLabs Support\n    url: https://help.elevenlabs.io\nservers:\n  webhookReceiver:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      The customer's webhook endpoint that receives event notifications\n      from ElevenLabs.\n    variables:\n      webhookUrl:\n        description: >-\n          The URL configured by the customer to receive webhook events.\n    security:\n      - hmacSignature: []\nchannels:\n  /post-call-transcription:\n    description: >-\n\
  \      Webhook channel for receiving conversation transcription data after\n      a Conversational AI call ends. Delivers the full transcript of the\n      conversation.\n    publish:\n      operationId: receivePostCallTranscription\n      summary: Post-call transcription webhook\n      description: >-\n        Delivered after a Conversational AI conversation ends, containing\n        the full conversation transcript with speaker roles and timestamps.\n      message:\n        $ref: '#/components/messages/PostCallTranscriptionEvent'\n  /post-call-audio:\n    description: >-\n      Webhook channel for receiving conversation audio recordings after\n      a Conversational AI call ends. Audio is delivered as a streaming\n      HTTP request with chunked transfer encoding.\n    publish:\n      operationId: receivePostCallAudio\n      summary: Post-call audio webhook\n      description: >-\n        Delivered after a Conversational AI conversation ends, containing\n        the audio recording of\
  \ the conversation. Uses chunked transfer\n        encoding for large audio files.\n      message:\n        $ref: '#/components/messages/PostCallAudioEvent'\n  /call-initiation-failure:\n    description: >-\n      Webhook channel for receiving notifications when a Conversational AI\n      call fails to initiate.\n    publish:\n      operationId: receiveCallInitiationFailure\n      summary: Call initiation failure webhook\n      description: >-\n        Delivered when a Conversational AI call fails to start,\n        providing error details and context.\n      message:\n        $ref: '#/components/messages/CallInitiationFailureEvent'\n  /workspace-events:\n    description: >-\n      Webhook channel for workspace-level events such as usage alerts,\n      subscription changes, and administrative notifications.\n    publish:\n      operationId: receiveWorkspaceEvent\n      summary: Workspace event webhook\n      description: >-\n        Delivered when workspace-level events occur, such as\
  \ usage\n        threshold alerts or configuration changes.\n      message:\n        $ref: '#/components/messages/WorkspaceEvent'\ncomponents:\n  securitySchemes:\n    hmacSignature:\n      type: httpApiKey\n      in: header\n      name: ElevenLabs-Signature\n      description: >-\n        HMAC-SHA256 signature for webhook payload verification. The\n        signature is computed using the shared secret generated when\n        the webhook is created. Verify this header to ensure the\n        webhook was sent by ElevenLabs.\n  messages:\n    PostCallTranscriptionEvent:\n      name: post_call_transcription\n      title: Post-Call Transcription\n      summary: Conversation transcript delivered after call completion\n      description: >-\n        Contains the full transcript of a completed Conversational AI\n        conversation, including speaker roles, timestamps, and metadata.\n        The webhook must return a 200 status code to be considered\n        successful. Webhooks that repeatedly\
  \ fail are automatically\n        disabled after 10 consecutive failures.\n      payload:\n        $ref: '#/components/schemas/PostCallTranscriptionPayload'\n    PostCallAudioEvent:\n      name: post_call_audio\n      title: Post-Call Audio\n      summary: Conversation audio recording delivered after call completion\n      description: >-\n        Contains the audio recording of a completed conversation. Delivered\n        as a streaming HTTP request with the transfer-encoding chunked\n        header. Ensure the receiving endpoint can handle streaming requests\n        and has sufficient storage capacity.\n      payload:\n        $ref: '#/components/schemas/PostCallAudioPayload'\n    CallInitiationFailureEvent:\n      name: call_initiation_failure\n      title: Call Initiation Failure\n      summary: Notification that a call failed to start\n      description: >-\n        Sent when a Conversational AI call could not be initiated,\n        including the error reason and agent context.\n\
  \      payload:\n        $ref: '#/components/schemas/CallInitiationFailurePayload'\n    WorkspaceEvent:\n      name: workspace_event\n      title: Workspace Event\n      summary: Workspace-level event notification\n      description: >-\n        Generic workspace event notification for administrative and\n        operational events.\n      payload:\n        $ref: '#/components/schemas/WorkspaceEventPayload'\n  schemas:\n    PostCallTranscriptionPayload:\n      type: object\n      properties:\n        event_type:\n          type: string\n          const: post_call_transcription\n          description: >-\n            The type of webhook event.\n        conversation_id:\n          type: string\n          description: >-\n            The unique identifier of the conversation.\n        agent_id:\n          type: string\n          description: >-\n            The identifier of the agent involved in the conversation.\n        transcript:\n          type: array\n          description: >-\n  \
  \          The full conversation transcript.\n          items:\n            type: object\n            properties:\n              role:\n                type: string\n                description: >-\n                  The speaker role.\n                enum:\n                  - agent\n                  - user\n              message:\n                type: string\n                description: >-\n                  The spoken message text.\n              timestamp:\n                type: number\n                description: >-\n                  Timestamp in seconds from conversation start.\n        metadata:\n          type: object\n          description: >-\n            Additional metadata about the conversation.\n          properties:\n            duration_seconds:\n              type: number\n              description: >-\n                Total conversation duration in seconds.\n            started_at:\n              type: string\n              format: date-time\n              description:\
  \ >-\n                Timestamp when the conversation started.\n            ended_at:\n              type: string\n              format: date-time\n              description: >-\n                Timestamp when the conversation ended.\n    PostCallAudioPayload:\n      type: object\n      properties:\n        event_type:\n          type: string\n          const: post_call_audio\n          description: >-\n            The type of webhook event.\n        conversation_id:\n          type: string\n          description: >-\n            The unique identifier of the conversation.\n        agent_id:\n          type: string\n          description: >-\n            The identifier of the agent involved in the conversation.\n        audio_format:\n          type: string\n          description: >-\n            The format of the audio data.\n        audio_data:\n          type: string\n          description: >-\n            The audio recording data, delivered via chunked transfer\n            encoding.\n\
  \    CallInitiationFailurePayload:\n      type: object\n      properties:\n        event_type:\n          type: string\n          const: call_initiation_failure\n          description: >-\n            The type of webhook event.\n        agent_id:\n          type: string\n          description: >-\n            The identifier of the agent that failed to start a call.\n        error:\n          type: string\n          description: >-\n            Description of the error that prevented call initiation.\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            Timestamp when the failure occurred.\n    WorkspaceEventPayload:\n      type: object\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of workspace event.\n        workspace_id:\n          type: string\n          description: >-\n            The identifier of the workspace.\n        data:\n          type: object\n   \
  \       description: >-\n            Event-specific data payload.\n          additionalProperties: true\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            Timestamp when the event occurred.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/asyncapi/elevenlabs-webhooks-asyncapi.yml
spec_file: asyncapi/elevenlabs-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/asyncapi/elevenlabs-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
