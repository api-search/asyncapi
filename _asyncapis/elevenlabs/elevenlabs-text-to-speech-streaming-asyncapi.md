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
- description: Bidirectional WebSocket channel for streaming text-to-speech. Clients send text chunks and receive audio chunks in real time as the model generates speech.
  name: /stream-input
  operation: publish
  operation_id: receiveAudioChunk
  summary: Receive generated audio chunks
description: The ElevenLabs Text to Speech WebSocket API enables bidirectional streaming for text-to-speech conversion. Clients send text chunks incrementally and receive audio chunks as they are generated, enabling ultra-low latency speech synthesis for real-time applications.
layout: asyncapi
messages:
- description: Contains a base64-encoded chunk of generated audio. Chunks are sent as they are produced by the model for low-latency playback.
  name: AudioChunkEvent
  summary: Generated audio data chunk
  title: Audio Chunk
- description: Contains timing information mapping generated audio to the input text, enabling synchronized text highlighting.
  name: AlignmentEvent
  summary: Word-level timing alignment data
  title: Alignment Data
- description: Sent when the server has finished generating all audio for the provided text input.
  name: FinalEvent
  summary: Signals the end of audio generation
  title: Final Event
- description: The first message sent by the client to configure the streaming session, including model selection, voice settings, and output format preferences.
  name: InitMessage
  summary: Initial configuration for the streaming session
  title: Initialization Message
- description: Contains a chunk of text to be converted to speech. Text can be sent incrementally as it becomes available.
  name: TextChunkMessage
  summary: Text input for speech synthesis
  title: Text Chunk
- description: Triggers the model to generate audio for any buffered text that has not yet been processed. Useful for ensuring all pending text is synthesized.
  name: FlushMessage
  summary: Forces generation of remaining audio
  title: Flush
- description: Sent by the client to indicate that no more text will be sent, triggering final audio generation and connection cleanup.
  name: CloseMessage
  summary: Signals the end of text input
  title: Close
name: ElevenLabs Text to Speech Streaming Events
provider_name: elevenlabs
provider_slug: elevenlabs
servers:
- description: ElevenLabs Text to Speech WebSocket server for bidirectional streaming synthesis.
  name: production
  protocol: wss
  url: wss://api.elevenlabs.io/v1/text-to-speech/{voice_id}/stream-input
slug: elevenlabs-text-to-speech-streaming-asyncapi
source_filename: elevenlabs-text-to-speech-streaming-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: ElevenLabs Text to Speech Streaming Events\n  description: >-\n    The ElevenLabs Text to Speech WebSocket API enables bidirectional\n    streaming for text-to-speech conversion. Clients send text chunks\n    incrementally and receive audio chunks as they are generated, enabling\n    ultra-low latency speech synthesis for real-time applications.\n  version: '1.0'\n  contact:\n    name: ElevenLabs Support\n    url: https://help.elevenlabs.io\nservers:\n  production:\n    url: wss://api.elevenlabs.io/v1/text-to-speech/{voice_id}/stream-input\n    protocol: wss\n    description: >-\n      ElevenLabs Text to Speech WebSocket server for bidirectional\n      streaming synthesis.\n    security:\n      - apiKeyHeader: []\nchannels:\n  /stream-input:\n    description: >-\n      Bidirectional WebSocket channel for streaming text-to-speech. Clients\n      send text chunks and receive audio chunks in real time as the model\n      generates speech.\n   \
  \ publish:\n      operationId: receiveAudioChunk\n      summary: Receive generated audio chunks\n      description: >-\n        Audio chunks sent from the server as the text-to-speech model\n        generates speech from the provided text input.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/AudioChunkEvent'\n          - $ref: '#/components/messages/AlignmentEvent'\n          - $ref: '#/components/messages/FinalEvent'\n    subscribe:\n      operationId: sendTextChunk\n      summary: Send text chunks for synthesis\n      description: >-\n        Text chunks sent from the client for incremental speech synthesis.\n        Includes the initial configuration message and subsequent text\n        input messages.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/InitMessage'\n          - $ref: '#/components/messages/TextChunkMessage'\n          - $ref: '#/components/messages/FlushMessage'\n          - $ref: '#/components/messages/CloseMessage'\n\
  components:\n  securitySchemes:\n    apiKeyHeader:\n      type: httpApiKey\n      in: header\n      name: xi-api-key\n      description: >-\n        ElevenLabs API key for WebSocket authentication.\n  messages:\n    AudioChunkEvent:\n      name: audio_chunk\n      title: Audio Chunk\n      summary: Generated audio data chunk\n      description: >-\n        Contains a base64-encoded chunk of generated audio. Chunks are\n        sent as they are produced by the model for low-latency playback.\n      payload:\n        $ref: '#/components/schemas/AudioChunkPayload'\n    AlignmentEvent:\n      name: alignment\n      title: Alignment Data\n      summary: Word-level timing alignment data\n      description: >-\n        Contains timing information mapping generated audio to the input\n        text, enabling synchronized text highlighting.\n      payload:\n        $ref: '#/components/schemas/AlignmentPayload'\n    FinalEvent:\n      name: final\n      title: Final Event\n      summary: Signals\
  \ the end of audio generation\n      description: >-\n        Sent when the server has finished generating all audio for the\n        provided text input.\n      payload:\n        $ref: '#/components/schemas/FinalPayload'\n    InitMessage:\n      name: init\n      title: Initialization Message\n      summary: Initial configuration for the streaming session\n      description: >-\n        The first message sent by the client to configure the streaming\n        session, including model selection, voice settings, and output\n        format preferences.\n      payload:\n        $ref: '#/components/schemas/InitPayload'\n    TextChunkMessage:\n      name: text_chunk\n      title: Text Chunk\n      summary: Text input for speech synthesis\n      description: >-\n        Contains a chunk of text to be converted to speech. Text can be\n        sent incrementally as it becomes available.\n      payload:\n        $ref: '#/components/schemas/TextChunkPayload'\n    FlushMessage:\n      name: flush\n\
  \      title: Flush\n      summary: Forces generation of remaining audio\n      description: >-\n        Triggers the model to generate audio for any buffered text that\n        has not yet been processed. Useful for ensuring all pending text\n        is synthesized.\n      payload:\n        $ref: '#/components/schemas/FlushPayload'\n    CloseMessage:\n      name: close\n      title: Close\n      summary: Signals the end of text input\n      description: >-\n        Sent by the client to indicate that no more text will be sent,\n        triggering final audio generation and connection cleanup.\n      payload:\n        $ref: '#/components/schemas/ClosePayload'\n  schemas:\n    AudioChunkPayload:\n      type: object\n      properties:\n        audio:\n          type: string\n          description: >-\n            Base64-encoded audio data chunk.\n        isFinal:\n          type: boolean\n          description: >-\n            Whether this is the final audio chunk.\n    AlignmentPayload:\n\
  \      type: object\n      properties:\n        chars:\n          type: array\n          description: >-\n            Character-level alignment data.\n          items:\n            type: string\n        charStartTimesMs:\n          type: array\n          description: >-\n            Start times in milliseconds for each character.\n          items:\n            type: number\n        charDurationsMs:\n          type: array\n          description: >-\n            Durations in milliseconds for each character.\n          items:\n            type: number\n    FinalPayload:\n      type: object\n      properties:\n        isFinal:\n          type: boolean\n          const: true\n          description: >-\n            Indicates this is the final message for the session.\n    InitPayload:\n      type: object\n      required:\n        - text\n      properties:\n        text:\n          type: string\n          description: >-\n            Initial text to begin generation. Can be a space to start\n\
  \            an empty session.\n        voice_settings:\n          type: object\n          description: >-\n            Voice settings for the session.\n          properties:\n            stability:\n              type: number\n              description: >-\n                Voice stability setting.\n              minimum: 0\n              maximum: 1\n            similarity_boost:\n              type: number\n              description: >-\n                Voice similarity boost setting.\n              minimum: 0\n              maximum: 1\n        generation_config:\n          type: object\n          description: >-\n            Generation configuration.\n          properties:\n            chunk_length_schedule:\n              type: array\n              description: >-\n                Schedule of chunk lengths for audio generation.\n              items:\n                type: integer\n        xi_api_key:\n          type: string\n          description: >-\n            API key for authentication\
  \ if not provided in headers.\n        model_id:\n          type: string\n          description: >-\n            The TTS model to use for generation.\n        output_format:\n          type: string\n          description: >-\n            The desired audio output format.\n    TextChunkPayload:\n      type: object\n      required:\n        - text\n      properties:\n        text:\n          type: string\n          description: >-\n            A chunk of text to convert to speech.\n        try_trigger_generation:\n          type: boolean\n          description: >-\n            Whether to attempt immediate generation of available text.\n    FlushPayload:\n      type: object\n      properties:\n        text:\n          type: string\n          const: \"\"\n          description: >-\n            Empty text string signals a flush.\n        flush:\n          type: boolean\n          const: true\n          description: >-\n            Flag to trigger flushing of buffered text.\n    ClosePayload:\n\
  \      type: object\n      properties:\n        text:\n          type: string\n          const: \"\"\n          description: >-\n            Empty text string.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/asyncapi/elevenlabs-text-to-speech-streaming-asyncapi.yml
spec_file: asyncapi/elevenlabs-text-to-speech-streaming-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/asyncapi/elevenlabs-text-to-speech-streaming-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
