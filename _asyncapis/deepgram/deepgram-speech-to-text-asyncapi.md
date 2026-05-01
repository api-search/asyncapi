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
- description: WebSocket channel for real-time speech-to-text streaming. The client sends binary audio frames and receives JSON transcription events. Connection parameters include model, language, punctuate, diarize, smart_format, interim_results, utterance_end_ms, vad_events, and encoding options.
  name: /v1/listen
  operation: publish
  operation_id: sendAudioData
  summary: Send audio data for real-time transcription
description: The Deepgram Speech-to-Text streaming API provides real-time transcription of audio using a WebSocket connection. Audio data is sent as binary WebSocket messages and transcription results are returned as JSON messages in real-time, supporting interim results, final results, speaker diarization, and speech detection events. The API supports the same model family and feature parameters as the pre-recorded API.
layout: asyncapi
messages:
- description: Raw binary audio data sent as a WebSocket binary message. The audio encoding format should be specified via connection query parameters.
  name: AudioFrame
  summary: Binary audio data frame
  title: Audio Frame
- description: JSON message sent by the client to signal the end of the audio stream, triggering final processing of any remaining audio.
  name: CloseStream
  summary: Signal to close the audio stream
  title: Close Stream
- description: JSON message sent by the client to keep the WebSocket connection alive during periods of silence without closing the stream.
  name: KeepAlive
  summary: Keep the connection alive
  title: Keep Alive
- description: JSON message containing transcription results. Can be an interim result (is_final=false) or a final result (is_final=true) depending on the interim_results connection parameter.
  name: TranscriptResult
  summary: Real-time transcription result
  title: Transcript Result
- description: Event indicating that speech activity has been detected in the audio stream. Sent when vad_events is enabled.
  name: SpeechStarted
  summary: Speech activity detected
  title: Speech Started
- description: Event indicating that the end of an utterance has been detected based on the configured utterance_end_ms threshold.
  name: UtteranceEnd
  summary: End of utterance detected
  title: Utterance End
- description: Metadata about the streaming session including request ID, model information, and session configuration.
  name: StreamMetadata
  summary: Stream metadata information
  title: Stream Metadata
- description: Error event indicating an issue with the streaming session.
  name: StreamError
  summary: Stream error event
  title: Stream Error
name: Deepgram Speech-to-Text Streaming Events
provider_name: Deepgram
provider_slug: deepgram
servers:
- description: Deepgram production WebSocket server for real-time speech-to-text streaming. Connect with query parameters to configure the transcription session.
  name: production
  protocol: wss
  url: wss://api.deepgram.com/v1/listen
- description: Deepgram EU WebSocket server for real-time speech-to-text streaming.
  name: eu
  protocol: wss
  url: wss://api.eu.deepgram.com/v1/listen
slug: deepgram-speech-to-text-asyncapi
source_filename: deepgram-speech-to-text-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Deepgram Speech-to-Text Streaming Events\n  description: >-\n    The Deepgram Speech-to-Text streaming API provides real-time transcription\n    of audio using a WebSocket connection. Audio data is sent as binary\n    WebSocket messages and transcription results are returned as JSON messages\n    in real-time, supporting interim results, final results, speaker\n    diarization, and speech detection events. The API supports the same model\n    family and feature parameters as the pre-recorded API.\n  version: '1.0'\n  contact:\n    name: Deepgram Support\n    url: https://developers.deepgram.com\nservers:\n  production:\n    url: 'wss://api.deepgram.com/v1/listen'\n    protocol: wss\n    description: >-\n      Deepgram production WebSocket server for real-time speech-to-text\n      streaming. Connect with query parameters to configure the transcription\n      session.\n    security:\n      - bearerAuth: []\n  eu:\n    url: 'wss://api.eu.deepgram.com/v1/listen'\n\
  \    protocol: wss\n    description: >-\n      Deepgram EU WebSocket server for real-time speech-to-text streaming.\n    security:\n      - bearerAuth: []\nchannels:\n  /v1/listen:\n    description: >-\n      WebSocket channel for real-time speech-to-text streaming. The client\n      sends binary audio frames and receives JSON transcription events.\n      Connection parameters include model, language, punctuate, diarize,\n      smart_format, interim_results, utterance_end_ms, vad_events, and\n      encoding options.\n    publish:\n      operationId: sendAudioData\n      summary: Send audio data for real-time transcription\n      description: >-\n        Client sends binary audio data frames to the WebSocket connection.\n        Audio should be sent as binary WebSocket messages. Send a JSON close\n        message to signal end of audio stream.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/AudioFrame'\n          - $ref: '#/components/messages/CloseStream'\n  \
  \        - $ref: '#/components/messages/KeepAlive'\n    subscribe:\n      operationId: receiveTranscriptionEvents\n      summary: Receive transcription events\n      description: >-\n        Server sends JSON messages containing transcription results, metadata,\n        and stream lifecycle events.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/TranscriptResult'\n          - $ref: '#/components/messages/SpeechStarted'\n          - $ref: '#/components/messages/UtteranceEnd'\n          - $ref: '#/components/messages/StreamMetadata'\n          - $ref: '#/components/messages/StreamError'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: http\n      scheme: bearer\n      description: >-\n        Deepgram API key passed as a token query parameter or Authorization\n        header when establishing the WebSocket connection.\n  messages:\n    AudioFrame:\n      name: AudioFrame\n      title: Audio Frame\n      summary: Binary audio data frame\n      description:\
  \ >-\n        Raw binary audio data sent as a WebSocket binary message. The audio\n        encoding format should be specified via connection query parameters.\n      contentType: application/octet-stream\n      payload:\n        type: string\n        format: binary\n        description: >-\n          Raw binary audio data in the configured encoding format.\n    CloseStream:\n      name: CloseStream\n      title: Close Stream\n      summary: Signal to close the audio stream\n      description: >-\n        JSON message sent by the client to signal the end of the audio\n        stream, triggering final processing of any remaining audio.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CloseStreamPayload'\n    KeepAlive:\n      name: KeepAlive\n      title: Keep Alive\n      summary: Keep the connection alive\n      description: >-\n        JSON message sent by the client to keep the WebSocket connection\n        alive during periods of silence without\
  \ closing the stream.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KeepAlivePayload'\n    TranscriptResult:\n      name: TranscriptResult\n      title: Transcript Result\n      summary: Real-time transcription result\n      description: >-\n        JSON message containing transcription results. Can be an interim\n        result (is_final=false) or a final result (is_final=true) depending\n        on the interim_results connection parameter.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TranscriptResultPayload'\n    SpeechStarted:\n      name: SpeechStarted\n      title: Speech Started\n      summary: Speech activity detected\n      description: >-\n        Event indicating that speech activity has been detected in the\n        audio stream. Sent when vad_events is enabled.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SpeechStartedPayload'\n    UtteranceEnd:\n\
  \      name: UtteranceEnd\n      title: Utterance End\n      summary: End of utterance detected\n      description: >-\n        Event indicating that the end of an utterance has been detected\n        based on the configured utterance_end_ms threshold.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/UtteranceEndPayload'\n    StreamMetadata:\n      name: StreamMetadata\n      title: Stream Metadata\n      summary: Stream metadata information\n      description: >-\n        Metadata about the streaming session including request ID, model\n        information, and session configuration.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/StreamMetadataPayload'\n    StreamError:\n      name: StreamError\n      title: Stream Error\n      summary: Stream error event\n      description: >-\n        Error event indicating an issue with the streaming session.\n      contentType: application/json\n      payload:\n  \
  \      $ref: '#/components/schemas/StreamErrorPayload'\n  schemas:\n    CloseStreamPayload:\n      type: object\n      required:\n        - type\n      properties:\n        type:\n          type: string\n          const: CloseStream\n          description: >-\n            Message type identifier.\n    KeepAlivePayload:\n      type: object\n      required:\n        - type\n      properties:\n        type:\n          type: string\n          const: KeepAlive\n          description: >-\n            Message type identifier.\n    TranscriptResultPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: Results\n          description: >-\n            Message type identifier.\n        channel_index:\n          type: array\n          items:\n            type: integer\n          description: >-\n            Channel index information.\n        duration:\n          type: number\n          format: float\n          description: >-\n            Duration\
  \ of audio processed in seconds.\n        start:\n          type: number\n          format: float\n          description: >-\n            Start time of this result in seconds.\n        is_final:\n          type: boolean\n          description: >-\n            Whether this is a final or interim result.\n        speech_final:\n          type: boolean\n          description: >-\n            Whether the speech endpoint has been detected.\n        channel:\n          type: object\n          properties:\n            alternatives:\n              type: array\n              items:\n                $ref: '#/components/schemas/StreamAlternative'\n              description: >-\n                Alternative transcriptions ordered by confidence.\n          description: >-\n            Channel transcription data.\n    StreamAlternative:\n      type: object\n      properties:\n        transcript:\n          type: string\n          description: >-\n            Transcript text for this alternative.\n   \
  \     confidence:\n          type: number\n          format: float\n          description: >-\n            Confidence score for this alternative.\n          minimum: 0\n          maximum: 1\n        words:\n          type: array\n          items:\n            $ref: '#/components/schemas/StreamWord'\n          description: >-\n            Individual words with timing information.\n    StreamWord:\n      type: object\n      properties:\n        word:\n          type: string\n          description: >-\n            The transcribed word.\n        start:\n          type: number\n          format: float\n          description: >-\n            Start time of the word in seconds.\n        end:\n          type: number\n          format: float\n          description: >-\n            End time of the word in seconds.\n        confidence:\n          type: number\n          format: float\n          description: >-\n            Confidence score for this word.\n        speaker:\n          type: integer\n\
  \          description: >-\n            Speaker identifier when diarization is enabled.\n        punctuated_word:\n          type: string\n          description: >-\n            The word with punctuation applied.\n    SpeechStartedPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: SpeechStarted\n          description: >-\n            Message type identifier.\n        channel:\n          type: array\n          items:\n            type: integer\n          description: >-\n            Channel indices where speech was detected.\n        timestamp:\n          type: number\n          format: float\n          description: >-\n            Timestamp in seconds when speech was detected.\n    UtteranceEndPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: UtteranceEnd\n          description: >-\n            Message type identifier.\n        channel:\n          type: array\n          items:\n\
  \            type: integer\n          description: >-\n            Channel indices for the utterance.\n        last_word_end:\n          type: number\n          format: float\n          description: >-\n            Timestamp in seconds of the last word in the utterance.\n    StreamMetadataPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: Metadata\n          description: >-\n            Message type identifier.\n        transaction_key:\n          type: string\n          description: >-\n            Transaction key for this session.\n        request_id:\n          type: string\n          description: >-\n            Unique request identifier for this session.\n        sha256:\n          type: string\n          description: >-\n            SHA-256 hash identifier.\n        created:\n          type: string\n          format: date-time\n          description: >-\n            Timestamp when the session was created.\n        duration:\n\
  \          type: number\n          format: float\n          description: >-\n            Total duration of audio processed.\n        channels:\n          type: integer\n          description: >-\n            Number of audio channels.\n        models:\n          type: array\n          items:\n            type: string\n          description: >-\n            Model identifiers used for transcription.\n        model_info:\n          type: object\n          additionalProperties: true\n          description: >-\n            Detailed model information.\n    StreamErrorPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: Error\n          description: >-\n            Message type identifier.\n        description:\n          type: string\n          description: >-\n            Human-readable error description.\n        message:\n          type: string\n          description: >-\n            Error message.\n        variant:\n          type: string\n\
  \          description: >-\n            Error variant classifier.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/deepgram/refs/heads/main/asyncapi/deepgram-speech-to-text-asyncapi.yml
spec_file: asyncapi/deepgram-speech-to-text-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/deepgram/refs/heads/main/asyncapi/deepgram-speech-to-text-asyncapi.yml
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
