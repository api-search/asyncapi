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
- description: Bidirectional WebSocket channel for real-time conversational AI interactions. Clients send audio input and receive agent audio responses, transcriptions, and conversation events.
  name: /conversation
  operation: publish
  operation_id: receiveConversationEvent
  summary: Receive conversation events from the agent
- description: WebSocket channel for real-time monitoring of active agent conversations. Provides text events and metadata for live observation and intervention.
  name: /monitoring
  operation: publish
  operation_id: receiveMonitoringEvent
  summary: Receive monitoring events
description: The ElevenLabs Conversational AI WebSocket API enables real-time, interactive voice conversations with AI agents. It supports bidirectional audio streaming, text events, and conversation lifecycle management through WebSocket connections. Clients send audio input and receive audio responses, transcriptions, and metadata events in real time.
layout: asyncapi
messages:
- description: Contains initialization data including the conversation ID, agent configuration, and available features. Sent once at the start of each conversation.
  name: ConversationInitiationMetadata
  summary: Metadata sent when the WebSocket connection is established
  title: Conversation Initiation Metadata
- description: Contains a base64-encoded audio chunk from the agent's speech response. Audio is streamed in small chunks for low-latency playback.
  name: AgentAudioEvent
  summary: Audio chunk from the agent's speech output
  title: Agent Audio
- description: Contains the text content of the agent's response, streamed as start, delta, and stop events for real-time text display.
  name: AgentResponseEvent
  summary: Text of the agent's response
  title: Agent Response
- description: Contains the transcribed text of the user's spoken input, updated in real time as the speech-to-text model processes the audio.
  name: UserTranscriptEvent
  summary: Transcription of the user's speech input
  title: User Transcript
- description: Sent when the conversation has ended, either by user action, agent decision, or timeout. Includes summary and analysis data.
  name: ConversationEndEvent
  summary: Signals the end of the conversation
  title: Conversation End
- description: Sent when the user begins speaking while the agent is still responding, indicating the agent's current response should be truncated.
  name: AgentInterruptionEvent
  summary: Signals that the agent was interrupted
  title: Agent Interruption
- description: Periodic ping sent by the server to keep the WebSocket connection alive. The client should respond with a pong message.
  name: PingEvent
  summary: Server ping for connection keep-alive
  title: Ping
- description: Contains a base64-encoded audio chunk from the user's microphone input for real-time speech processing.
  name: UserAudioInput
  summary: Audio chunk from the user's microphone
  title: User Audio Input
- description: Sent by the client in response to a server ping to maintain the WebSocket connection.
  name: PongResponse
  summary: Client pong response to server ping
  title: Pong Response
- description: Real-time transcript of the conversation being monitored.
  name: MonitoringTranscriptEvent
  summary: Live transcript event during monitoring
  title: Monitoring Transcript
- description: Text of the agent's response as observed during real-time monitoring.
  name: MonitoringAgentResponseEvent
  summary: Agent response during monitoring
  title: Monitoring Agent Response
name: ElevenLabs Conversational AI Events
provider_name: elevenlabs
provider_slug: elevenlabs
servers:
- description: ElevenLabs Conversational AI WebSocket server for real-time voice agent interactions.
  name: production
  protocol: wss
  url: wss://api.elevenlabs.io/v1/convai/conversation
slug: elevenlabs-conversational-ai-asyncapi
source_filename: elevenlabs-conversational-ai-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: ElevenLabs Conversational AI Events\n  description: >-\n    The ElevenLabs Conversational AI WebSocket API enables real-time,\n    interactive voice conversations with AI agents. It supports bidirectional\n    audio streaming, text events, and conversation lifecycle management\n    through WebSocket connections. Clients send audio input and receive\n    audio responses, transcriptions, and metadata events in real time.\n  version: '1.0'\n  contact:\n    name: ElevenLabs Support\n    url: https://help.elevenlabs.io\nservers:\n  production:\n    url: wss://api.elevenlabs.io/v1/convai/conversation\n    protocol: wss\n    description: >-\n      ElevenLabs Conversational AI WebSocket server for real-time voice\n      agent interactions.\n    security:\n      - apiKeyQuery: []\nchannels:\n  /conversation:\n    description: >-\n      Bidirectional WebSocket channel for real-time conversational AI\n      interactions. Clients send audio input and receive\
  \ agent audio\n      responses, transcriptions, and conversation events.\n    publish:\n      operationId: receiveConversationEvent\n      summary: Receive conversation events from the agent\n      description: >-\n        Events sent from the server to the client during a conversation,\n        including audio responses, transcriptions, agent messages, and\n        conversation lifecycle events.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/ConversationInitiationMetadata'\n          - $ref: '#/components/messages/AgentAudioEvent'\n          - $ref: '#/components/messages/AgentResponseEvent'\n          - $ref: '#/components/messages/UserTranscriptEvent'\n          - $ref: '#/components/messages/ConversationEndEvent'\n          - $ref: '#/components/messages/AgentInterruptionEvent'\n          - $ref: '#/components/messages/PingEvent'\n    subscribe:\n      operationId: sendConversationInput\n      summary: Send input to the conversation\n      description: >-\n\
  \        Events sent from the client to the server, including audio input\n        from the user's microphone and control messages.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/UserAudioInput'\n          - $ref: '#/components/messages/PongResponse'\n  /monitoring:\n    description: >-\n      WebSocket channel for real-time monitoring of active agent\n      conversations. Provides text events and metadata for live\n      observation and intervention.\n    publish:\n      operationId: receiveMonitoringEvent\n      summary: Receive monitoring events\n      description: >-\n        Events streamed during real-time monitoring of active conversations,\n        including transcriptions, agent responses, and control events.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/MonitoringTranscriptEvent'\n          - $ref: '#/components/messages/MonitoringAgentResponseEvent'\ncomponents:\n  securitySchemes:\n    apiKeyQuery:\n      type: httpApiKey\n\
  \      in: query\n      name: agent_id\n      description: >-\n        The agent_id query parameter identifies which agent to start a\n        conversation with. For private agents, a signed URL obtained via\n        the REST API is required instead.\n  messages:\n    ConversationInitiationMetadata:\n      name: conversation_initiation_metadata\n      title: Conversation Initiation Metadata\n      summary: Metadata sent when the WebSocket connection is established\n      description: >-\n        Contains initialization data including the conversation ID, agent\n        configuration, and available features. Sent once at the start of\n        each conversation.\n      payload:\n        $ref: '#/components/schemas/ConversationInitiationMetadataPayload'\n    AgentAudioEvent:\n      name: audio\n      title: Agent Audio\n      summary: Audio chunk from the agent's speech output\n      description: >-\n        Contains a base64-encoded audio chunk from the agent's speech\n        response.\
  \ Audio is streamed in small chunks for low-latency playback.\n      payload:\n        $ref: '#/components/schemas/AgentAudioPayload'\n    AgentResponseEvent:\n      name: agent_response\n      title: Agent Response\n      summary: Text of the agent's response\n      description: >-\n        Contains the text content of the agent's response, streamed as\n        start, delta, and stop events for real-time text display.\n      payload:\n        $ref: '#/components/schemas/AgentResponsePayload'\n    UserTranscriptEvent:\n      name: user_transcript\n      title: User Transcript\n      summary: Transcription of the user's speech input\n      description: >-\n        Contains the transcribed text of the user's spoken input, updated\n        in real time as the speech-to-text model processes the audio.\n      payload:\n        $ref: '#/components/schemas/UserTranscriptPayload'\n    ConversationEndEvent:\n      name: conversation_end\n      title: Conversation End\n      summary: Signals the\
  \ end of the conversation\n      description: >-\n        Sent when the conversation has ended, either by user action,\n        agent decision, or timeout. Includes summary and analysis data.\n      payload:\n        $ref: '#/components/schemas/ConversationEndPayload'\n    AgentInterruptionEvent:\n      name: interruption\n      title: Agent Interruption\n      summary: Signals that the agent was interrupted\n      description: >-\n        Sent when the user begins speaking while the agent is still\n        responding, indicating the agent's current response should be\n        truncated.\n      payload:\n        $ref: '#/components/schemas/InterruptionPayload'\n    PingEvent:\n      name: ping\n      title: Ping\n      summary: Server ping for connection keep-alive\n      description: >-\n        Periodic ping sent by the server to keep the WebSocket connection\n        alive. The client should respond with a pong message.\n      payload:\n        $ref: '#/components/schemas/PingPayload'\n\
  \    UserAudioInput:\n      name: user_audio_chunk\n      title: User Audio Input\n      summary: Audio chunk from the user's microphone\n      description: >-\n        Contains a base64-encoded audio chunk from the user's microphone\n        input for real-time speech processing.\n      payload:\n        $ref: '#/components/schemas/UserAudioInputPayload'\n    PongResponse:\n      name: pong\n      title: Pong Response\n      summary: Client pong response to server ping\n      description: >-\n        Sent by the client in response to a server ping to maintain the\n        WebSocket connection.\n      payload:\n        $ref: '#/components/schemas/PongPayload'\n    MonitoringTranscriptEvent:\n      name: monitoring_transcript\n      title: Monitoring Transcript\n      summary: Live transcript event during monitoring\n      description: >-\n        Real-time transcript of the conversation being monitored.\n      payload:\n        $ref: '#/components/schemas/MonitoringTranscriptPayload'\n\
  \    MonitoringAgentResponseEvent:\n      name: monitoring_agent_response\n      title: Monitoring Agent Response\n      summary: Agent response during monitoring\n      description: >-\n        Text of the agent's response as observed during real-time monitoring.\n      payload:\n        $ref: '#/components/schemas/MonitoringAgentResponsePayload'\n  schemas:\n    ConversationInitiationMetadataPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: conversation_initiation_metadata\n          description: >-\n            The event type identifier.\n        conversation_id:\n          type: string\n          description: >-\n            Unique identifier for the conversation session.\n        agent_output_audio_format:\n          type: string\n          description: >-\n            The audio format used for agent output.\n    AgentAudioPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const:\
  \ audio\n          description: >-\n            The event type identifier.\n        audio:\n          type: string\n          description: >-\n            Base64-encoded audio data chunk.\n    AgentResponsePayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: agent_response\n          description: >-\n            The event type identifier.\n        agent_response_type:\n          type: string\n          description: >-\n            The sub-type of the response event.\n          enum:\n            - start\n            - delta\n            - stop\n        text:\n          type: string\n          description: >-\n            The text content of the agent's response or delta.\n    UserTranscriptPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: user_transcript\n          description: >-\n            The event type identifier.\n        text:\n          type: string\n          description:\
  \ >-\n            The transcribed text of the user's speech.\n        is_final:\n          type: boolean\n          description: >-\n            Whether this is the final transcription for the current\n            utterance.\n    ConversationEndPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: conversation_end\n          description: >-\n            The event type identifier.\n        reason:\n          type: string\n          description: >-\n            The reason the conversation ended.\n          enum:\n            - user_ended\n            - agent_ended\n            - timeout\n            - error\n    InterruptionPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: interruption\n          description: >-\n            The event type identifier.\n    PingPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: ping\n          description:\
  \ >-\n            The event type identifier.\n        ping_id:\n          type: string\n          description: >-\n            Identifier for the ping, to be echoed in the pong response.\n    UserAudioInputPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: user_audio_chunk\n          description: >-\n            The event type identifier.\n        audio:\n          type: string\n          description: >-\n            Base64-encoded audio data from the user's microphone.\n    PongPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: pong\n          description: >-\n            The event type identifier.\n        ping_id:\n          type: string\n          description: >-\n            The ping_id from the original ping event.\n    MonitoringTranscriptPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: monitoring_transcript\n       \
  \   description: >-\n            The event type identifier.\n        text:\n          type: string\n          description: >-\n            The transcript text being monitored.\n        role:\n          type: string\n          description: >-\n            The speaker role.\n          enum:\n            - agent\n            - user\n    MonitoringAgentResponsePayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: monitoring_agent_response\n          description: >-\n            The event type identifier.\n        text:\n          type: string\n          description: >-\n            The agent's response text.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/asyncapi/elevenlabs-conversational-ai-asyncapi.yml
spec_file: asyncapi/elevenlabs-conversational-ai-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/elevenlabs/refs/heads/main/asyncapi/elevenlabs-conversational-ai-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
