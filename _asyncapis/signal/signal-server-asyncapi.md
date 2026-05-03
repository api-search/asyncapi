---
api_specs:
- filename: signal-server-openapi.yml
  format: yaml
  label: Signal Server
  slug: signal-server
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/signal/refs/heads/main/openapi/signal-server-openapi.yml
channels:
- description: The primary authenticated WebSocket channel for real-time message delivery, receipt confirmations, and typing indicators. Clients maintain a persistent connection on this channel to receive encrypted messages as they arrive. The server uses a request-response framing protocol over the WebSocket where both sides can initiate requests.
  name: /v1/websocket
  operation: publish
  operation_id: receiveMessages
  summary: Receive real-time messages from the server
- description: The provisioning WebSocket channel used during the device linking flow. A new device connects to this channel and receives a provisioning UUID. The primary device then sends an encrypted provisioning message containing the account identity key and other credentials needed to complete the linking process.
  name: /v1/websocket/provisioning
  operation: publish
  operation_id: receiveProvisioningMessages
  summary: Receive provisioning messages during device linking
- description: Apple Push Notification Service channel for delivering push notifications to iOS devices when they are not connected via WebSocket. Notifications alert the device to connect to the server and retrieve pending messages.
  name: /push/apns
  operation: publish
  operation_id: sendApnsPush
  summary: Send push notification to iOS device
- description: Firebase Cloud Messaging channel for delivering push notifications to Android devices when they are not connected via WebSocket. Notifications alert the device to connect and retrieve pending messages.
  name: /push/fcm
  operation: publish
  operation_id: sendFcmPush
  summary: Send push notification to Android device
description: The Signal Server real-time messaging interface provides WebSocket connections for persistent, bidirectional communication between Signal clients and the server. When a client has an active WebSocket connection, encrypted messages are delivered in real-time through that connection. For offline clients, the server sends push notifications via APNs (Apple) or FCM (Google) to alert the client to connect and retrieve pending messages. The WebSocket protocol also supports keepalive pings, provisioning of new linked devices, and contact discovery operations.
layout: asyncapi
messages:
- description: ''
  name: MessageEnvelope
  summary: An encrypted message envelope containing a Signal Protocol message.
  title: Encrypted Message Envelope
- description: ''
  name: ReceiptMessage
  summary: A receipt message confirming delivery or read status of a previously sent message.
  title: Delivery or Read Receipt
- description: ''
  name: TypingIndicator
  summary: A typing indicator showing that a contact is currently composing a message.
  title: Typing Indicator
- description: ''
  name: StorySendMessage
  summary: A message containing a story post sent by a contact.
  title: Story Send Message
- description: ''
  name: WebSocketRequestMessage
  summary: A request message sent over the WebSocket connection using the Signal WebSocket framing protocol.
  title: WebSocket Request
- description: ''
  name: WebSocketResponseMessage
  summary: A response message sent over the WebSocket connection acknowledging a previous request.
  title: WebSocket Response
- description: ''
  name: ProvisioningUUID
  summary: The server assigns a provisioning UUID to a new device during the device linking process.
  title: Provisioning UUID Assignment
- description: ''
  name: ProvisioningMessage
  summary: An encrypted provisioning message from the primary device containing account credentials for the new linked device.
  title: Encrypted Provisioning Message
- description: ''
  name: PushNotification
  summary: A push notification sent to an offline device to alert it of pending messages.
  title: Push Notification
name: Signal Server Real-Time Events
provider_name: Signal
provider_slug: signal
servers:
- description: Signal production WebSocket server for authenticated real-time messaging. Clients establish a persistent WebSocket connection after authentication to receive messages in real-time.
  name: production
  protocol: wss
  url: wss://chat.signal.org/v1/websocket/
- description: Signal provisioning WebSocket server used during the device linking process. New devices connect to receive provisioning messages from the primary device.
  name: provisioning
  protocol: wss
  url: wss://chat.signal.org/v1/websocket/provisioning/
slug: signal-server-asyncapi
source_filename: signal-server-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Signal Server Real-Time Events\n  description: >-\n    The Signal Server real-time messaging interface provides WebSocket\n    connections for persistent, bidirectional communication between Signal\n    clients and the server. When a client has an active WebSocket connection,\n    encrypted messages are delivered in real-time through that connection.\n    For offline clients, the server sends push notifications via APNs (Apple)\n    or FCM (Google) to alert the client to connect and retrieve pending\n    messages. The WebSocket protocol also supports keepalive pings,\n    provisioning of new linked devices, and contact discovery operations.\n  version: '2.0'\n  contact:\n    name: Signal Support\n    url: https://support.signal.org/\n  license:\n    name: AGPL-3.0\n    url: https://github.com/signalapp/Signal-Server/blob/main/LICENSE\nservers:\n  production:\n    url: wss://chat.signal.org/v1/websocket/\n    protocol: wss\n    description: >-\n\
  \      Signal production WebSocket server for authenticated real-time\n      messaging. Clients establish a persistent WebSocket connection after\n      authentication to receive messages in real-time.\n    security:\n      - basicAuth: []\n  provisioning:\n    url: wss://chat.signal.org/v1/websocket/provisioning/\n    protocol: wss\n    description: >-\n      Signal provisioning WebSocket server used during the device linking\n      process. New devices connect to receive provisioning messages from\n      the primary device.\nchannels:\n  /v1/websocket:\n    description: >-\n      The primary authenticated WebSocket channel for real-time message\n      delivery, receipt confirmations, and typing indicators. Clients\n      maintain a persistent connection on this channel to receive encrypted\n      messages as they arrive. The server uses a request-response framing\n      protocol over the WebSocket where both sides can initiate requests.\n    publish:\n      operationId: receiveMessages\n\
  \      summary: Receive real-time messages from the server\n      description: >-\n        The server pushes encrypted message envelopes to connected clients\n        through this channel. Each message includes the envelope type,\n        encrypted content, sender information (when not using sealed\n        sender), timestamp, and the server delivery timestamp. Clients must\n        acknowledge receipt of each message.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/MessageEnvelope'\n          - $ref: '#/components/messages/ReceiptMessage'\n          - $ref: '#/components/messages/TypingIndicator'\n          - $ref: '#/components/messages/StorySendMessage'\n    subscribe:\n      operationId: sendWebSocketRequest\n      summary: Send requests over the WebSocket channel\n      description: >-\n        Clients can send requests over the WebSocket channel, including\n        message acknowledgements, keepalive pings, and REST-like requests\n        that are framed\
  \ as WebSocket messages.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/WebSocketRequestMessage'\n          - $ref: '#/components/messages/WebSocketResponseMessage'\n  /v1/websocket/provisioning:\n    description: >-\n      The provisioning WebSocket channel used during the device linking\n      flow. A new device connects to this channel and receives a\n      provisioning UUID. The primary device then sends an encrypted\n      provisioning message containing the account identity key and other\n      credentials needed to complete the linking process.\n    publish:\n      operationId: receiveProvisioningMessages\n      summary: Receive provisioning messages during device linking\n      description: >-\n        The server sends provisioning messages to new devices during the\n        linking process. This includes the provisioning UUID assignment\n        and the encrypted provisioning message from the primary device.\n      message:\n        oneOf:\n        \
  \  - $ref: '#/components/messages/ProvisioningUUID'\n          - $ref: '#/components/messages/ProvisioningMessage'\n  /push/apns:\n    description: >-\n      Apple Push Notification Service channel for delivering push\n      notifications to iOS devices when they are not connected via\n      WebSocket. Notifications alert the device to connect to the server\n      and retrieve pending messages.\n    publish:\n      operationId: sendApnsPush\n      summary: Send push notification to iOS device\n      description: >-\n        The server sends a silent or alert push notification to an iOS\n        device via APNs when it has pending messages and no active\n        WebSocket connection.\n      message:\n        $ref: '#/components/messages/PushNotification'\n  /push/fcm:\n    description: >-\n      Firebase Cloud Messaging channel for delivering push notifications\n      to Android devices when they are not connected via WebSocket.\n      Notifications alert the device to connect and retrieve\
  \ pending\n      messages.\n    publish:\n      operationId: sendFcmPush\n      summary: Send push notification to Android device\n      description: >-\n        The server sends a data-only push notification to an Android\n        device via FCM when it has pending messages and no active\n        WebSocket connection.\n      message:\n        $ref: '#/components/messages/PushNotification'\ncomponents:\n  securitySchemes:\n    basicAuth:\n      type: httpBasic\n      description: >-\n        HTTP Basic authentication using the account UUID and password,\n        passed as query parameters during WebSocket upgrade.\n  messages:\n    MessageEnvelope:\n      name: MessageEnvelope\n      title: Encrypted Message Envelope\n      summary: >-\n        An encrypted message envelope containing a Signal Protocol message.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/Envelope'\n    ReceiptMessage:\n      name: ReceiptMessage\n      title: Delivery or Read\
  \ Receipt\n      summary: >-\n        A receipt message confirming delivery or read status of a\n        previously sent message.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/Receipt'\n    TypingIndicator:\n      name: TypingIndicator\n      title: Typing Indicator\n      summary: >-\n        A typing indicator showing that a contact is currently composing a\n        message.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TypingEvent'\n    StorySendMessage:\n      name: StorySendMessage\n      title: Story Send Message\n      summary: >-\n        A message containing a story post sent by a contact.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/StorySend'\n    WebSocketRequestMessage:\n      name: WebSocketRequestMessage\n      title: WebSocket Request\n      summary: >-\n        A request message sent over the WebSocket connection using the\n        Signal\
  \ WebSocket framing protocol.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebSocketRequest'\n    WebSocketResponseMessage:\n      name: WebSocketResponseMessage\n      title: WebSocket Response\n      summary: >-\n        A response message sent over the WebSocket connection acknowledging\n        a previous request.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebSocketResponse'\n    ProvisioningUUID:\n      name: ProvisioningUUID\n      title: Provisioning UUID Assignment\n      summary: >-\n        The server assigns a provisioning UUID to a new device during the\n        device linking process.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ProvisioningUUIDPayload'\n    ProvisioningMessage:\n      name: ProvisioningMessage\n      title: Encrypted Provisioning Message\n      summary: >-\n        An encrypted provisioning message from the primary device\n\
  \        containing account credentials for the new linked device.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ProvisioningMessagePayload'\n    PushNotification:\n      name: PushNotification\n      title: Push Notification\n      summary: >-\n        A push notification sent to an offline device to alert it of\n        pending messages.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PushNotificationPayload'\n  schemas:\n    Envelope:\n      type: object\n      description: >-\n        A Signal Protocol message envelope containing encrypted content\n        and delivery metadata.\n      properties:\n        type:\n          type: integer\n          description: >-\n            The envelope type. 1 for ciphertext, 3 for prekey bundle\n            message, 6 for plaintext content, 7 for unidentified sender.\n          enum:\n            - 1\n            - 3\n            - 6\n            - 7\n       \
  \ sourceUuid:\n          type: string\n          format: uuid\n          description: >-\n            The sender's account UUID. Absent for sealed sender messages.\n        sourceDevice:\n          type: integer\n          description: >-\n            The sender's device identifier. Absent for sealed sender\n            messages.\n        timestamp:\n          type: integer\n          format: int64\n          description: >-\n            The client-side timestamp in milliseconds when the message was\n            sent.\n        serverTimestamp:\n          type: integer\n          format: int64\n          description: >-\n            The server-side timestamp in milliseconds when the message was\n            received.\n        serverDeliveredTimestamp:\n          type: integer\n          format: int64\n          description: >-\n            The server-side timestamp in milliseconds when the message was\n            delivered to this device.\n        content:\n          type: string\n   \
  \       description: >-\n            The Base64-encoded encrypted message content.\n        serverGuid:\n          type: string\n          format: uuid\n          description: >-\n            A server-assigned unique identifier for this message delivery.\n        destinationUuid:\n          type: string\n          format: uuid\n          description: >-\n            The recipient's account UUID.\n        urgent:\n          type: boolean\n          description: >-\n            Whether this message is flagged as urgent.\n        story:\n          type: boolean\n          description: >-\n            Whether this message is a story message.\n        reportSpamToken:\n          type: string\n          description: >-\n            A token for spam reporting, included in sealed sender messages.\n    Receipt:\n      type: object\n      description: >-\n        A delivery or read receipt for one or more messages.\n      properties:\n        type:\n          type: string\n          description:\
  \ >-\n            The receipt type.\n          enum:\n            - DELIVERY\n            - READ\n        timestamps:\n          type: array\n          description: >-\n            The timestamps of the messages being acknowledged.\n          items:\n            type: integer\n            format: int64\n    TypingEvent:\n      type: object\n      description: >-\n        A typing indicator event.\n      properties:\n        action:\n          type: string\n          description: >-\n            Whether typing has started or stopped.\n          enum:\n            - STARTED\n            - STOPPED\n        timestamp:\n          type: integer\n          format: int64\n          description: >-\n            The client timestamp of the typing event.\n        groupId:\n          type: string\n          description: >-\n            The Base64-encoded group identifier if typing in a group\n            conversation.\n    StorySend:\n      type: object\n      description: >-\n        A story message\
  \ sent to contacts or groups.\n      properties:\n        content:\n          type: string\n          description: >-\n            The Base64-encoded encrypted story content.\n        timestamp:\n          type: integer\n          format: int64\n          description: >-\n            The client timestamp of the story message.\n        allowsReplies:\n          type: boolean\n          description: >-\n            Whether replies are permitted on this story.\n    WebSocketRequest:\n      type: object\n      description: >-\n        A request message in the Signal WebSocket framing protocol.\n      properties:\n        id:\n          type: integer\n          format: int64\n          description: >-\n            The request identifier for correlating responses.\n        verb:\n          type: string\n          description: >-\n            The HTTP method (GET, PUT, POST, DELETE).\n        path:\n          type: string\n          description: >-\n            The request path, corresponding\
  \ to a REST API endpoint.\n        body:\n          type: string\n          description: >-\n            The Base64-encoded request body.\n        headers:\n          type: array\n          description: >-\n            HTTP headers for the request.\n          items:\n            type: string\n    WebSocketResponse:\n      type: object\n      description: >-\n        A response message in the Signal WebSocket framing protocol.\n      properties:\n        id:\n          type: integer\n          format: int64\n          description: >-\n            The request identifier being responded to.\n        status:\n          type: integer\n          description: >-\n            The HTTP status code of the response.\n        message:\n          type: string\n          description: >-\n            The status message.\n        body:\n          type: string\n          description: >-\n            The Base64-encoded response body.\n        headers:\n          type: array\n          description: >-\n\
  \            HTTP headers for the response.\n          items:\n            type: string\n    ProvisioningUUIDPayload:\n      type: object\n      description: >-\n        A provisioning UUID assignment sent to a new device during linking.\n      properties:\n        uuid:\n          type: string\n          format: uuid\n          description: >-\n            The provisioning UUID assigned to the new device.\n    ProvisioningMessagePayload:\n      type: object\n      description: >-\n        An encrypted provisioning message containing account credentials.\n      properties:\n        body:\n          type: string\n          description: >-\n            The Base64-encoded encrypted provisioning message from the\n            primary device.\n    PushNotificationPayload:\n      type: object\n      description: >-\n        A push notification payload sent to offline devices.\n      properties:\n        type:\n          type: string\n          description: >-\n            The notification type\
  \ identifier.\n          enum:\n            - notification\n            - challenge\n            - rateLimitChallenge\n        data:\n          type: object\n          description: >-\n            Additional data included in the push notification.\n          properties:\n            urgent:\n              type: boolean\n              description: >-\n                Whether the notification is for an urgent message.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/signal/refs/heads/main/asyncapi/signal-server-asyncapi.yml
spec_file: asyncapi/signal-server-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/signal/refs/heads/main/asyncapi/signal-server-asyncapi.yml
tags:
- Encryption
- Messaging
- Security
- Cryptography
- Open Source
- Privacy
- AsyncAPI
- Webhooks
- Events
version: '2.0'
---
