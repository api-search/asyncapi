---
api_specs:
- filename: webflux-websocket-asyncapi.yml
  format: yaml
  label: Spring WebFlux WebSocket
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflux/refs/heads/main/asyncapi/webflux-websocket-asyncapi.yml
channels:
- description: WebSocket channel mapped via Spring WebFlux WebSocketHandlerAdapter. A WebSocketSession is established on connection and provides reactive inbound() and outbound() message streams.
  name: websocketSession
- description: STOMP over WebSocket channel. Spring WebFlux integrates with STOMP messaging protocol for topic subscriptions, queued messages, and message broker relay.
  name: stompBroker
description: AsyncAPI specification describing WebSocket communication patterns for Spring WebFlux applications. Spring WebFlux provides reactive WebSocket support via WebSocketHandler and WebSocketSession, enabling full-duplex, bidirectional messaging between clients and servers.
layout: asyncapi
messages:
- description: ''
  name: TextMessage
  summary: A UTF-8 encoded text data frame (opcode 0x1)
  title: WebSocket Text Message
- description: ''
  name: BinaryMessage
  summary: A binary data frame (opcode 0x2)
  title: WebSocket Binary Message
- description: ''
  name: PingMessage
  summary: A control ping frame (opcode 0x9) for keep-alive
  title: WebSocket Ping Frame
- description: ''
  name: PongMessage
  summary: A control pong frame (opcode 0xA) in response to ping
  title: WebSocket Pong Frame
- description: ''
  name: CloseMessage
  summary: A control close frame (opcode 0x8) to initiate connection closure
  title: WebSocket Close Frame
- description: ''
  name: StompMessage
  summary: A STOMP protocol frame for topic messaging over WebSocket
  title: STOMP Frame
name: Spring WebFlux WebSocket API
provider_name: Spring WebFlux
provider_slug: webflux
servers:
- description: Spring WebFlux WebSocket endpoint
  name: production
  protocol: ws
  url: ''
- description: Secure Spring WebFlux WebSocket endpoint (TLS)
  name: secure
  protocol: wss
  url: ''
slug: webflux-websocket-asyncapi
source_filename: webflux-websocket-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 3.0.0\ninfo:\n  title: Spring WebFlux WebSocket API\n  version: 6.2.0\n  description: >-\n    AsyncAPI specification describing WebSocket communication patterns for\n    Spring WebFlux applications. Spring WebFlux provides reactive WebSocket\n    support via WebSocketHandler and WebSocketSession, enabling full-duplex,\n    bidirectional messaging between clients and servers.\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\n  externalDocs:\n    url: https://docs.spring.io/spring-framework/reference/web/webflux-websocket.html\n    description: Spring WebFlux WebSocket Documentation\n\nservers:\n  production:\n    host: '{host}:{port}'\n    protocol: ws\n    description: Spring WebFlux WebSocket endpoint\n    variables:\n      host:\n        default: localhost\n        description: Application host\n      port:\n        default: '8080'\n        description: Application port\n  secure:\n    host: '{host}:{port}'\n    protocol: wss\n\
  \    description: Secure Spring WebFlux WebSocket endpoint (TLS)\n    variables:\n      host:\n        default: localhost\n        description: Application host\n      port:\n        default: '8443'\n        description: Application port\n\nchannels:\n  websocketSession:\n    address: /ws\n    description: >-\n      WebSocket channel mapped via Spring WebFlux WebSocketHandlerAdapter.\n      A WebSocketSession is established on connection and provides reactive\n      inbound() and outbound() message streams.\n    messages:\n      textMessage:\n        $ref: '#/components/messages/TextMessage'\n      binaryMessage:\n        $ref: '#/components/messages/BinaryMessage'\n      pingMessage:\n        $ref: '#/components/messages/PingMessage'\n      pongMessage:\n        $ref: '#/components/messages/PongMessage'\n      closeMessage:\n        $ref: '#/components/messages/CloseMessage'\n\n  stompBroker:\n    address: /stomp\n    description: >-\n      STOMP over WebSocket channel. Spring WebFlux\
  \ integrates with STOMP messaging\n      protocol for topic subscriptions, queued messages, and message broker relay.\n    messages:\n      stompMessage:\n        $ref: '#/components/messages/StompMessage'\n\noperations:\n  sendTextMessage:\n    action: send\n    channel:\n      $ref: '#/channels/websocketSession'\n    summary: Send Text Message\n    description: >-\n      Client sends a text message over the WebSocket connection.\n      In Spring WebFlux, this corresponds to WebSocketSession.send(publisher).\n    messages:\n      - $ref: '#/components/messages/TextMessage'\n\n  receiveTextMessage:\n    action: receive\n    channel:\n      $ref: '#/channels/websocketSession'\n    summary: Receive Text Message\n    description: >-\n      Server receives a text message from the client.\n      In Spring WebFlux, WebSocketSession.receive() returns a Flux<WebSocketMessage>.\n    messages:\n      - $ref: '#/components/messages/TextMessage'\n\n  sendBinaryMessage:\n    action: send\n    channel:\n\
  \      $ref: '#/channels/websocketSession'\n    summary: Send Binary Message\n    description: Send a binary data frame over the WebSocket connection.\n    messages:\n      - $ref: '#/components/messages/BinaryMessage'\n\n  receiveBinaryMessage:\n    action: receive\n    channel:\n      $ref: '#/channels/websocketSession'\n    summary: Receive Binary Message\n    description: Receive a binary data frame from the WebSocket connection.\n    messages:\n      - $ref: '#/components/messages/BinaryMessage'\n\n  subscribeToTopic:\n    action: send\n    channel:\n      $ref: '#/channels/stompBroker'\n    summary: Subscribe to Topic\n    description: STOMP SUBSCRIBE frame to subscribe to a topic or queue.\n    messages:\n      - $ref: '#/components/messages/StompMessage'\n\n  receiveTopicMessage:\n    action: receive\n    channel:\n      $ref: '#/channels/stompBroker'\n    summary: Receive Topic Message\n    description: Receive a STOMP MESSAGE frame from a subscribed topic.\n    messages:\n  \
  \    - $ref: '#/components/messages/StompMessage'\n\ncomponents:\n  messages:\n    TextMessage:\n      name: TextMessage\n      title: WebSocket Text Message\n      summary: A UTF-8 encoded text data frame (opcode 0x1)\n      contentType: text/plain\n      payload:\n        $ref: '#/components/schemas/TextPayload'\n\n    BinaryMessage:\n      name: BinaryMessage\n      title: WebSocket Binary Message\n      summary: A binary data frame (opcode 0x2)\n      contentType: application/octet-stream\n      payload:\n        $ref: '#/components/schemas/BinaryPayload'\n\n    PingMessage:\n      name: PingMessage\n      title: WebSocket Ping Frame\n      summary: A control ping frame (opcode 0x9) for keep-alive\n      payload:\n        $ref: '#/components/schemas/ControlPayload'\n\n    PongMessage:\n      name: PongMessage\n      title: WebSocket Pong Frame\n      summary: A control pong frame (opcode 0xA) in response to ping\n      payload:\n        $ref: '#/components/schemas/ControlPayload'\n\
  \n    CloseMessage:\n      name: CloseMessage\n      title: WebSocket Close Frame\n      summary: A control close frame (opcode 0x8) to initiate connection closure\n      payload:\n        $ref: '#/components/schemas/ClosePayload'\n\n    StompMessage:\n      name: StompMessage\n      title: STOMP Frame\n      summary: A STOMP protocol frame for topic messaging over WebSocket\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/StompPayload'\n\n  schemas:\n    TextPayload:\n      type: object\n      properties:\n        content:\n          type: string\n          description: UTF-8 text content of the message\n        sessionId:\n          type: string\n          description: WebSocketSession identifier\n\n    BinaryPayload:\n      type: object\n      properties:\n        data:\n          type: string\n          format: binary\n          description: Binary data content\n\n    ControlPayload:\n      type: object\n      properties:\n        applicationData:\n\
  \          type: string\n          description: Optional application data in control frame\n\n    ClosePayload:\n      type: object\n      properties:\n        statusCode:\n          type: integer\n          description: RFC 6455 close status code (e.g. 1000 Normal Closure)\n        reason:\n          type: string\n          description: Human-readable reason for closure\n\n    StompPayload:\n      type: object\n      properties:\n        command:\n          type: string\n          enum: [CONNECT, CONNECTED, SUBSCRIBE, UNSUBSCRIBE, SEND, MESSAGE, ACK, NACK, DISCONNECT, ERROR]\n          description: STOMP command\n        headers:\n          type: object\n          additionalProperties:\n            type: string\n          description: STOMP frame headers\n        body:\n          type: string\n          description: STOMP frame body\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/webflux/refs/heads/main/asyncapi/webflux-websocket-asyncapi.yml
spec_file: asyncapi/webflux-websocket-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/webflux/refs/heads/main/asyncapi/webflux-websocket-asyncapi.yml
tags:
- Java
- Microservices
- Non-Blocking IO
- Reactive Programming
- REST API
- Spring Boot
- Spring Framework
- WebFlux
- AsyncAPI
- Webhooks
- Events
version: 6.2.0
---
