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
- description: WebSocket channel for the Voice Agent API. After connecting, the client sends a Settings message to configure the agent's listen (STT), think (LLM), and speak (TTS) providers, followed by binary audio frames. The server responds with agent audio, transcription events, and lifecycle messages.
  name: /v1/agent/converse
  operation: publish
  operation_id: sendAgentInput
  summary: Send input to the voice agent
description: The Deepgram Voice Agent API is an end-to-end solution that combines speech-to-text, LLM orchestration, and text-to-speech into a single real-time WebSocket API. It simplifies building conversational voice agents by handling barge-in detection, turn-taking prediction, function calling, and mid-session control. The client sends a settings configuration message after connection, followed by audio frames, and receives agent audio responses along with lifecycle and control events.
layout: asyncapi
messages:
- description: Initialization message sent immediately after opening the WebSocket and before sending any audio. Configures the agent's audio format, STT (listen), LLM (think), and TTS (speak) providers, agent instructions, and optional context.
  name: Settings
  summary: Agent session configuration
  title: Settings
- description: Binary WebSocket message containing raw audio data from the user's microphone in the encoding configured in the Settings message.
  name: AudioInput
  summary: User audio data
  title: Audio Input
- description: Updates the agent's system instructions during an active session without restarting the connection.
  name: UpdateInstructions
  summary: Update agent instructions mid-session
  title: Update Instructions
- description: Updates the text-to-speech provider settings during an active session.
  name: UpdateSpeak
  summary: Update TTS settings mid-session
  title: Update Speak Settings
- description: Injects a text message into the agent's conversation context, allowing external events to influence the conversation flow.
  name: InjectAgentMessage
  summary: Inject a message into the agent conversation
  title: Inject Agent Message
- description: Sends the result of a function call back to the agent after the client has executed the requested function.
  name: FunctionCallResponse
  summary: Response to a function call request
  title: Function Call Response
- description: Keeps the WebSocket connection alive during periods of inactivity.
  name: AgentKeepAlive
  summary: Keep the agent connection alive
  title: Keep Alive
- description: Binary WebSocket message containing synthesized speech audio from the agent in the encoding configured in the Settings message.
  name: AgentAudioData
  summary: Agent speech audio
  title: Agent Audio Data
- description: Event indicating that the user has started speaking, which may trigger barge-in behavior to interrupt the agent.
  name: UserStartedSpeaking
  summary: User speech activity detected
  title: User Started Speaking
- description: Event indicating that the agent has started generating and sending audio output.
  name: AgentStartedSpeaking
  summary: Agent has begun speaking
  title: Agent Started Speaking
- description: Event indicating that the agent's LLM is generating a response to the user's input.
  name: AgentThinking
  summary: Agent is processing a response
  title: Agent Thinking
- description: Text transcript of the conversation including both user speech transcriptions and agent response text.
  name: ConversationText
  summary: Transcript of conversation
  title: Conversation Text
- description: The agent's LLM has determined that a function should be called. The client must execute the function and return the result via a FunctionCallResponse message.
  name: FunctionCallRequest
  summary: Agent requests a function call
  title: Function Call Request
- description: Event indicating that the agent is in the process of calling a function.
  name: FunctionCalling
  summary: Agent is invoking a function
  title: Function Calling
- description: Welcome message sent by the server after the WebSocket connection is established and the Settings message has been processed.
  name: Welcome
  summary: Connection established
  title: Welcome
- description: Error event indicating an issue with the voice agent session.
  name: AgentError
  summary: Agent error event
  title: Error
name: Deepgram Voice Agent Events
provider_name: Deepgram
provider_slug: deepgram
servers:
- description: Deepgram production WebSocket server for the Voice Agent API. Connect and send a Settings message to configure the agent before sending audio data.
  name: production
  protocol: wss
  url: wss://agent.deepgram.com/v1/agent/converse
slug: deepgram-voice-agent-asyncapi
source_filename: deepgram-voice-agent-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Deepgram Voice Agent Events\n  description: >-\n    The Deepgram Voice Agent API is an end-to-end solution that combines\n    speech-to-text, LLM orchestration, and text-to-speech into a single\n    real-time WebSocket API. It simplifies building conversational voice\n    agents by handling barge-in detection, turn-taking prediction, function\n    calling, and mid-session control. The client sends a settings\n    configuration message after connection, followed by audio frames, and\n    receives agent audio responses along with lifecycle and control events.\n  version: '1.0'\n  contact:\n    name: Deepgram Support\n    url: https://developers.deepgram.com\nservers:\n  production:\n    url: 'wss://agent.deepgram.com/v1/agent/converse'\n    protocol: wss\n    description: >-\n      Deepgram production WebSocket server for the Voice Agent API. Connect\n      and send a Settings message to configure the agent before sending\n      audio data.\n\
  \    security:\n      - bearerAuth: []\nchannels:\n  /v1/agent/converse:\n    description: >-\n      WebSocket channel for the Voice Agent API. After connecting, the\n      client sends a Settings message to configure the agent's listen\n      (STT), think (LLM), and speak (TTS) providers, followed by binary\n      audio frames. The server responds with agent audio, transcription\n      events, and lifecycle messages.\n    publish:\n      operationId: sendAgentInput\n      summary: Send input to the voice agent\n      description: >-\n        Client sends settings configuration, audio frames, function call\n        results, and control messages to the voice agent.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/Settings'\n          - $ref: '#/components/messages/AudioInput'\n          - $ref: '#/components/messages/UpdateInstructions'\n          - $ref: '#/components/messages/UpdateSpeak'\n          - $ref: '#/components/messages/InjectAgentMessage'\n        \
  \  - $ref: '#/components/messages/FunctionCallResponse'\n          - $ref: '#/components/messages/AgentKeepAlive'\n    subscribe:\n      operationId: receiveAgentOutput\n      summary: Receive output from the voice agent\n      description: >-\n        Server sends agent audio responses, transcription results, function\n        call requests, and agent lifecycle events.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/AgentAudioData'\n          - $ref: '#/components/messages/UserStartedSpeaking'\n          - $ref: '#/components/messages/AgentStartedSpeaking'\n          - $ref: '#/components/messages/AgentThinking'\n          - $ref: '#/components/messages/ConversationText'\n          - $ref: '#/components/messages/FunctionCallRequest'\n          - $ref: '#/components/messages/FunctionCalling'\n          - $ref: '#/components/messages/Welcome'\n          - $ref: '#/components/messages/AgentError'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: http\n\
  \      scheme: bearer\n      description: >-\n        Deepgram API key passed as a token query parameter or Authorization\n        header when establishing the WebSocket connection.\n  messages:\n    Settings:\n      name: Settings\n      title: Settings\n      summary: Agent session configuration\n      description: >-\n        Initialization message sent immediately after opening the WebSocket\n        and before sending any audio. Configures the agent's audio format,\n        STT (listen), LLM (think), and TTS (speak) providers, agent\n        instructions, and optional context.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SettingsPayload'\n    AudioInput:\n      name: AudioInput\n      title: Audio Input\n      summary: User audio data\n      description: >-\n        Binary WebSocket message containing raw audio data from the user's\n        microphone in the encoding configured in the Settings message.\n      contentType: application/octet-stream\n\
  \      payload:\n        type: string\n        format: binary\n        description: >-\n          Raw binary audio from the user.\n    UpdateInstructions:\n      name: UpdateInstructions\n      title: Update Instructions\n      summary: Update agent instructions mid-session\n      description: >-\n        Updates the agent's system instructions during an active session\n        without restarting the connection.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/UpdateInstructionsPayload'\n    UpdateSpeak:\n      name: UpdateSpeak\n      title: Update Speak Settings\n      summary: Update TTS settings mid-session\n      description: >-\n        Updates the text-to-speech provider settings during an active\n        session.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/UpdateSpeakPayload'\n    InjectAgentMessage:\n      name: InjectAgentMessage\n      title: Inject Agent Message\n      summary: Inject a message\
  \ into the agent conversation\n      description: >-\n        Injects a text message into the agent's conversation context,\n        allowing external events to influence the conversation flow.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/InjectAgentMessagePayload'\n    FunctionCallResponse:\n      name: FunctionCallResponse\n      title: Function Call Response\n      summary: Response to a function call request\n      description: >-\n        Sends the result of a function call back to the agent after the\n        client has executed the requested function.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/FunctionCallResponsePayload'\n    AgentKeepAlive:\n      name: AgentKeepAlive\n      title: Keep Alive\n      summary: Keep the agent connection alive\n      description: >-\n        Keeps the WebSocket connection alive during periods of inactivity.\n      contentType: application/json\n      payload:\n\
  \        $ref: '#/components/schemas/KeepAlivePayload'\n    AgentAudioData:\n      name: AgentAudioData\n      title: Agent Audio Data\n      summary: Agent speech audio\n      description: >-\n        Binary WebSocket message containing synthesized speech audio from\n        the agent in the encoding configured in the Settings message.\n      contentType: application/octet-stream\n      payload:\n        type: string\n        format: binary\n        description: >-\n          Raw binary audio from the agent's TTS output.\n    UserStartedSpeaking:\n      name: UserStartedSpeaking\n      title: User Started Speaking\n      summary: User speech activity detected\n      description: >-\n        Event indicating that the user has started speaking, which may\n        trigger barge-in behavior to interrupt the agent.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/UserStartedSpeakingPayload'\n    AgentStartedSpeaking:\n      name: AgentStartedSpeaking\n\
  \      title: Agent Started Speaking\n      summary: Agent has begun speaking\n      description: >-\n        Event indicating that the agent has started generating and sending\n        audio output.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AgentStartedSpeakingPayload'\n    AgentThinking:\n      name: AgentThinking\n      title: Agent Thinking\n      summary: Agent is processing a response\n      description: >-\n        Event indicating that the agent's LLM is generating a response to\n        the user's input.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AgentThinkingPayload'\n    ConversationText:\n      name: ConversationText\n      title: Conversation Text\n      summary: Transcript of conversation\n      description: >-\n        Text transcript of the conversation including both user speech\n        transcriptions and agent response text.\n      contentType: application/json\n      payload:\n\
  \        $ref: '#/components/schemas/ConversationTextPayload'\n    FunctionCallRequest:\n      name: FunctionCallRequest\n      title: Function Call Request\n      summary: Agent requests a function call\n      description: >-\n        The agent's LLM has determined that a function should be called.\n        The client must execute the function and return the result via\n        a FunctionCallResponse message.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/FunctionCallRequestPayload'\n    FunctionCalling:\n      name: FunctionCalling\n      title: Function Calling\n      summary: Agent is invoking a function\n      description: >-\n        Event indicating that the agent is in the process of calling a\n        function.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/FunctionCallingPayload'\n    Welcome:\n      name: Welcome\n      title: Welcome\n      summary: Connection established\n      description:\
  \ >-\n        Welcome message sent by the server after the WebSocket connection\n        is established and the Settings message has been processed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WelcomePayload'\n    AgentError:\n      name: AgentError\n      title: Error\n      summary: Agent error event\n      description: >-\n        Error event indicating an issue with the voice agent session.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AgentErrorPayload'\n  schemas:\n    SettingsPayload:\n      type: object\n      required:\n        - type\n      properties:\n        type:\n          type: string\n          const: Settings\n          description: >-\n            Message type identifier.\n        audio:\n          type: object\n          properties:\n            input:\n              type: object\n              properties:\n                encoding:\n                  type: string\n           \
  \       description: >-\n                    Audio encoding format for input audio from the user.\n                sample_rate:\n                  type: integer\n                  description: >-\n                    Sample rate in Hertz for input audio.\n              description: >-\n                Input audio configuration.\n            output:\n              type: object\n              properties:\n                encoding:\n                  type: string\n                  description: >-\n                    Audio encoding format for output audio from the agent.\n                sample_rate:\n                  type: integer\n                  description: >-\n                    Sample rate in Hertz for output audio.\n                container:\n                  type: string\n                  description: >-\n                    Container format for output audio.\n              description: >-\n                Output audio configuration.\n          description: >-\n          \
  \  Audio format configuration for both input and output.\n        agent:\n          type: object\n          properties:\n            listen:\n              type: object\n              properties:\n                model:\n                  type: string\n                  description: >-\n                    Speech-to-text model to use for transcription.\n                language:\n                  type: string\n                  description: >-\n                    Language for speech recognition.\n              description: >-\n                STT provider configuration.\n            think:\n              type: object\n              properties:\n                provider:\n                  type: object\n                  properties:\n                    type:\n                      type: string\n                      description: >-\n                        LLM provider type such as open_ai, anthropic, or\n                        deepgram.\n                  description: >-\n        \
  \            LLM provider settings.\n                model:\n                  type: string\n                  description: >-\n                    LLM model identifier.\n                instructions:\n                  type: string\n                  description: >-\n                    System instructions for the agent's behavior.\n                functions:\n                  type: array\n                  items:\n                    $ref: '#/components/schemas/FunctionDefinition'\n                  description: >-\n                    Functions available for the agent to call.\n              description: >-\n                LLM provider configuration.\n            speak:\n              type: object\n              properties:\n                model:\n                  type: string\n                  description: >-\n                    Text-to-speech model or voice to use.\n              description: >-\n                TTS provider configuration.\n          description: >-\n      \
  \      Agent provider configuration for listen, think, and speak.\n        context:\n          type: object\n          properties:\n            messages:\n              type: array\n              items:\n                type: object\n                properties:\n                  role:\n                    type: string\n                    description: >-\n                      Role of the message sender.\n                  content:\n                    type: string\n                    description: >-\n                      Content of the message.\n              description: >-\n                Initial conversation context messages.\n            replay:\n              type: boolean\n              description: >-\n                Whether to replay context messages to the user.\n          description: >-\n            Optional initial conversation context.\n    FunctionDefinition:\n      type: object\n      properties:\n        name:\n          type: string\n          description: >-\n \
  \           Name of the function.\n        description:\n          type: string\n          description: >-\n            Description of what the function does.\n        parameters:\n          type: object\n          description: >-\n            JSON Schema defining the function's parameters.\n    UpdateInstructionsPayload:\n      type: object\n      required:\n        - type\n        - instructions\n      properties:\n        type:\n          type: string\n          const: UpdateInstructions\n          description: >-\n            Message type identifier.\n        instructions:\n          type: string\n          description: >-\n            New system instructions for the agent.\n    UpdateSpeakPayload:\n      type: object\n      required:\n        - type\n      properties:\n        type:\n          type: string\n          const: UpdateSpeak\n          description: >-\n            Message type identifier.\n        model:\n          type: string\n          description: >-\n            New\
  \ text-to-speech model or voice.\n    InjectAgentMessagePayload:\n      type: object\n      required:\n        - type\n        - message\n      properties:\n        type:\n          type: string\n          const: InjectAgentMessage\n          description: >-\n            Message type identifier.\n        message:\n          type: string\n          description: >-\n            Text message to inject into the conversation.\n    FunctionCallResponsePayload:\n      type: object\n      required:\n        - type\n        - function_call_id\n        - output\n      properties:\n        type:\n          type: string\n          const: FunctionCallResponse\n          description: >-\n            Message type identifier.\n        function_call_id:\n          type: string\n          description: >-\n            Identifier of the function call being responded to.\n        output:\n          type: string\n          description: >-\n            String result of the function execution.\n    KeepAlivePayload:\n\
  \      type: object\n      required:\n        - type\n      properties:\n        type:\n          type: string\n          const: KeepAlive\n          description: >-\n            Message type identifier.\n    UserStartedSpeakingPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: UserStartedSpeaking\n          description: >-\n            Message type identifier.\n    AgentStartedSpeakingPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: AgentStartedSpeaking\n          description: >-\n            Message type identifier.\n        total_latency:\n          type: number\n          format: float\n          description: >-\n            Total latency in seconds from user input to agent response.\n        tts_latency:\n          type: number\n          format: float\n          description: >-\n            Text-to-speech processing latency in seconds.\n        ttt_latency:\n          type:\
  \ number\n          format: float\n          description: >-\n            Text-to-text (LLM) processing latency in seconds.\n    AgentThinkingPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: AgentThinking\n          description: >-\n            Message type identifier.\n    ConversationTextPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: ConversationText\n          description: >-\n            Message type identifier.\n        role:\n          type: string\n          enum:\n            - user\n            - assistant\n          description: >-\n            Role of the speaker in the conversation.\n        content:\n          type: string\n          description: >-\n            Text content of the conversation turn.\n    FunctionCallRequestPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: FunctionCallRequest\n          description:\
  \ >-\n            Message type identifier.\n        function_call_id:\n          type: string\n          description: >-\n            Unique identifier for this function call.\n        function_name:\n          type: string\n          description: >-\n            Name of the function to call.\n        input:\n          type: object\n          additionalProperties: true\n          description: >-\n            Arguments to pass to the function.\n    FunctionCallingPayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: FunctionCalling\n          description: >-\n            Message type identifier.\n    WelcomePayload:\n      type: object\n      properties:\n        type:\n          type: string\n          const: Welcome\n          description: >-\n            Message type identifier.\n        session_id:\n          type: string\n          description: >-\n            Unique identifier for this agent session.\n    AgentErrorPayload:\n    \
  \  type: object\n      properties:\n        type:\n          type: string\n          const: Error\n          description: >-\n            Message type identifier.\n        description:\n          type: string\n          description: >-\n            Human-readable error description.\n        message:\n          type: string\n          description: >-\n            Error message.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/deepgram/refs/heads/main/asyncapi/deepgram-voice-agent-asyncapi.yml
spec_file: asyncapi/deepgram-voice-agent-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/deepgram/refs/heads/main/asyncapi/deepgram-voice-agent-asyncapi.yml
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
