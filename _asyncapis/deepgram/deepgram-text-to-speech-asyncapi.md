---
api_specs:
- filename: deepgram-speech-to-text-openapi.yml
  format: yaml
  label: Deepgram Speech-To-Text API
  slug: speech-to-text-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/deepgram/refs/heads/main/openapi/deepgram-speech-to-text-openapi.yml
- filename: deepgram-text-to-speech-openapi.yml
  format: yaml
  label: Deepgram Text-To-Speech API
  slug: text-to-speech-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/deepgram/refs/heads/main/openapi/deepgram-text-to-speech-openapi.yml
- filename: deepgram-voice-agent-asyncapi.yml
  format: yaml
  label: Deepgram Voice Agent API
  slug: voice-agent-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/deepgram/refs/heads/main/asyncapi/deepgram-voice-agent-asyncapi.yml
- filename: deepgram-speech-to-text-openapi.yml
  format: yaml
  label: Deepgram Audio Intelligence API
  slug: audio-intelligence-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/deepgram/refs/heads/main/openapi/deepgram-speech-to-text-openapi.yml
- filename: deepgram-management-openapi.yml
  format: yaml
  label: Deepgram Management API
  slug: management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/deepgram/refs/heads/main/openapi/deepgram-management-openapi.yml
channels:
- description: WebSocket channel for real-time text-to-speech streaming. The client sends text as JSON messages and receives synthesized audio as binary frames. Connection parameters include model, encoding, sample_rate, and container settings.
  name: /v1/speak
  operation: publish
  operation_id: sendTextForSpeech
  summary: Send text for speech synthesis
description: The Deepgram Text-to-Speech streaming API provides real-time speech synthesis over a WebSocket connection. Text is sent as JSON messages and audio data is returned as binary WebSocket messages, enabling continuous streaming text-to-speech for conversational AI applications, voice agents, and real-time voice interfaces.
layout: asyncapi
messages:
- description: JSON message containing text to be converted to speech audio. Text is synthesized incrementally as it is received.
  name: TextInput
  summary: Text to synthesize into speech
  title: Text Input
- description: Signals the server to immediately synthesize any buffered text and return audio for it.
  name: Flush
  summary: Flush pending text
  title: Flush
- description: Resets the text-to-speech synthesis state, clearing any buffered text that has not yet been synthesized.
  name: Reset
  summary: Reset the synthesis state
  title: Reset
- description: Signals the server to finalize synthesis and close the connection after all pending audio has been returned.
  name: Close
  summary: Close the streaming session
  title: Close
- description: Binary WebSocket message containing synthesized speech audio in the encoding format configured at connection time.
  name: AudioData
  summary: Synthesized speech audio data
  title: Audio Data
- description: Confirmation that all buffered text has been synthesized and the corresponding audio has been sent.
  name: Flushed
  summary: Flush confirmation
  title: Flushed
- description: Non-fatal warning about the streaming session.
  name: Warning
  summary: Warning message
  title: Warning
- description: Error event indicating an issue with the text-to-speech session.
  name: TTSError
  summary: Error message
  title: Error
name: Deepgram Text-to-Speech Streaming Events
provider_name: Deepgram
provider_slug: deepgram
servers:
- description: Deepgram production WebSocket server for real-time text-to-speech streaming. Connect with query parameters to configure the voice model, encoding, and sample rate.
  name: production
  protocol: wss
  url: wss://api.deepgram.com/v1/speak
- description: Deepgram EU WebSocket server for real-time text-to-speech streaming.
  name: eu
  protocol: wss
  url: wss://api.eu.deepgram.com/v1/speak
slug: deepgram-text-to-speech-asyncapi
source_filename: deepgram-text-to-speech-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Deepgram Text-to-Speech Streaming Events\n  description: >-\n    The Deepgram Text-to-Speech streaming API provides real-time speech\n    synthesis over a WebSocket connection. Text is sent as JSON messages\n    and audio data is returned as binary WebSocket messages, enabling\n    continuous streaming text-to-speech for conversational AI applications,\n    voice agents, and real-time voice interfaces.\n  version: '1.0'\n  contact:\n    name: Deepgram Support\n    url: https://developers.deepgram.com\nservers:\n  production:\n    url: 'wss://api.deepgram.com/v1/speak'\n    protocol: wss\n    description: >-\n      Deepgram production WebSocket server for real-time text-to-speech\n      streaming. Connect with query parameters to configure the voice model,\n      encoding, and sample rate.\n    security:\n      - bearerAuth: []\n  eu:\n    url: 'wss://api.eu.deepgram.com/v1/speak'\n    protocol: wss\n    description: >-\n      Deepgram EU WebSocket\
  \ server for real-time text-to-speech streaming.\n    security:\n      - bearerAuth: []\nchannels:\n  /v1/speak:\n    description: >-\n      WebSocket channel for real-time text-to-speech streaming. The client\n      sends text as JSON messages and receives synthesized audio as binary\n      frames. Connection parameters include model, encoding, sample_rate,\n      and container settings.\n    publish:\n      operationId: sendTextForSpeech\n      summary: Send text for speech synthesis\n      description: >-\n        Client sends JSON messages containing text to be synthesized into\n        speech. Supports continuous streaming of text segments.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/TextInput'\n          - $ref: '#/components/messages/Flush'\n          - $ref: '#/components/messages/Reset'\n          - $ref: '#/components/messages/Close'\n    subscribe:\n      operationId: receiveSpeechAudio\n      summary: Receive synthesized speech audio\n      description:\
  \ >-\n        Server sends binary audio frames and JSON control messages as\n        speech is synthesized from the input text.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/AudioData'\n          - $ref: '#/components/messages/Flushed'\n          - $ref: '#/components/messages/Warning'\n          - $ref: '#/components/messages/TTSError'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: http\n      scheme: bearer\n      description: >-\n        Deepgram API key passed as a token query parameter or Authorization\n        header when establishing the WebSocket connection.\n  messages:\n    TextInput:\n      name: TextInput\n      title: Text Input\n      summary: Text to synthesize into speech\n      description: >-\n        JSON message containing text to be converted to speech audio. Text\n        is synthesized incrementally as it is received.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TextInputPayload'\n\
  \    Flush:\n      name: Flush\n      title: Flush\n      summary: Flush pending text\n      description: >-\n        Signals the server to immediately synthesize any buffered text and\n        return audio for it.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/FlushPayload'\n    Reset:\n      name: Reset\n      title: Reset\n      summary: Reset the synthesis state\n      description: >-\n        Resets the text-to-speech synthesis state, clearing any buffered\n        text that has not yet been synthesized.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ResetPayload'\n    Close:\n      name: Close\n      title: Close\n      summary: Close the streaming session\n      description: >-\n        Signals the server to finalize synthesis and close the connection\n        after all pending audio has been returned.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ClosePayload'\n\
  \    AudioData:\n      name: AudioData\n      title: Audio Data\n      summary: Synthesized speech audio data\n      description: >-\n        Binary WebSocket message containing synthesized speech audio in the\n        encoding format configured at connection time.\n      contentType: application/octet-stream\n      payload:\n        type: string\n        format: binary\n        description: >-\n          Raw binary audio data in the configured encoding format.\n    Flushed:\n      name: Flushed\n      title: Flushed\n      summary: Flush confirmation\n      description: >-\n        Confirmation that all buffered text has been synthesized and the\n        corresponding audio has been sent.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/FlushedPayload'\n    Warning:\n      name: Warning\n      title: Warning\n      summary: Warning message\n      description: >-\n        Non-fatal warning about the streaming session.\n      contentType: application/json\n\
  \      payload:\n        $ref: '#/components/schemas/WarningPayload'\n    TTSError:\n      name: TTSError\n      title: Error\n      summary: Error message\n      description: >-\n        Error event indicating an issue with the text-to-speech session.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TTSErrorPayload'\n  schemas:\n    TextInputPayload:\n      type: object\n      required:\n        - type\n        - text\n      properties:\n        type:\n          type: string\n          const: Speak\n          description: >-\n            Message type identifier.\n        text:\n          type: string\n          description: >-\n            Text content to synthesize into speech.\n    FlushPayload:\n      type: object\n      required:\n        - type\n      properties:\n        type:\n          type: string\n          const: Flush\n          description: >-\n            Message type identifier.\n    ResetPayload:\n      type: object\n      required:\n\
  \        - type\n      properties:\n        type:\n          type: string\n          const: Reset\n          description: >-\n            Message type identifier.\n    ClosePayload:\n      type: object\n      required:\n        - type\n      properties:\n        type:\n          type: string\n          const: Close\n          description: >-\n            Message type identifier.\n    FlushedPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: Flushed\n          description: >-\n            Message type identifier.\n        sequence_id:\n          type: integer\n          description: >-\n            Sequence identifier for the flush operation.\n    WarningPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: Warning\n          description: >-\n            Message type identifier.\n        warn_code:\n          type: string\n          description: >-\n            Warning code.\n      \
  \  warn_msg:\n          type: string\n          description: >-\n            Human-readable warning message.\n    TTSErrorPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: Error\n          description: >-\n            Message type identifier.\n        err_code:\n          type: string\n          description: >-\n            Error code.\n        err_msg:\n          type: string\n          description: >-\n            Human-readable error message.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/deepgram/refs/heads/main/asyncapi/deepgram-text-to-speech-asyncapi.yml
spec_file: asyncapi/deepgram-text-to-speech-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/deepgram/refs/heads/main/asyncapi/deepgram-text-to-speech-asyncapi.yml
tags:
- Artificial Intelligence
- Speech-To-Text
- Text-To-Speech
- Transcription
- Voice AI
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
