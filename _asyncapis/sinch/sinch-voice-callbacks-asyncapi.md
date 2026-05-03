---
api_specs:
- filename: sinch-sms-openapi.yml
  format: yaml
  label: Sinch SMS API
  slug: sms-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-sms-openapi.yml
- filename: sinch-conversation-openapi.yml
  format: yaml
  label: Sinch Conversation API
  slug: conversation-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-conversation-openapi.yml
- filename: sinch-voice-openapi.yml
  format: yaml
  label: Sinch Voice API
  slug: voice-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-voice-openapi.yml
- filename: sinch-verification-openapi.yml
  format: yaml
  label: Sinch Verification API
  slug: verification-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-verification-openapi.yml
- filename: sinch-numbers-openapi.yml
  format: yaml
  label: Sinch Numbers API
  slug: numbers-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-numbers-openapi.yml
- filename: sinch-fax-openapi.yml
  format: yaml
  label: Sinch Fax API
  slug: fax-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-fax-openapi.yml
- filename: sinch-elastic-sip-trunking-openapi.yml
  format: yaml
  label: Sinch Elastic SIP Trunking API
  slug: elastic-sip-trunking-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-elastic-sip-trunking-openapi.yml
- filename: sinch-brands-openapi.yml
  format: yaml
  label: Sinch Brands API
  slug: brands-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-brands-openapi.yml
- filename: sinch-provisioning-openapi.yml
  format: yaml
  label: Sinch Provisioning API
  slug: provisioning-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-provisioning-openapi.yml
- filename: sinch-registration-openapi.yml
  format: yaml
  label: Sinch Registration API
  slug: registration-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-registration-openapi.yml
channels:
- description: Receives Incoming Call Event (ICE) callbacks when the Sinch platform receives an incoming call. Your response instructs the platform how to handle the call using SVAML.
  name: /voice/ice
  operation: publish
  operation_id: receiveIncomingCallEvent
  summary: Receive an Incoming Call Event
- description: Receives Answered Call Event (ACE) callbacks when a call is answered. Your response can provide additional SVAML instructions.
  name: /voice/ace
  operation: publish
  operation_id: receiveAnsweredCallEvent
  summary: Receive an Answered Call Event
- description: Receives Disconnected Call Event (DiCE) callbacks when a call is disconnected for any reason.
  name: /voice/dice
  operation: publish
  operation_id: receiveDisconnectedCallEvent
  summary: Receive a Disconnected Call Event
- description: Receives Prompt Input Event (PIE) callbacks when a user provides DTMF input during an IVR session.
  name: /voice/pie
  operation: publish
  operation_id: receivePromptInputEvent
  summary: Receive a Prompt Input Event
- description: Receives notification callbacks for various call events such as call progress and recording completion.
  name: /voice/notify
  operation: publish
  operation_id: receiveNotification
  summary: Receive a notification event
description: Event-driven callbacks for the Sinch Voice API. The Voice API sends HTTP POST callbacks to your application during the lifecycle of a voice call. Your application responds with SVAML (Sinch Voice Application Markup Language) instructions to control the call flow including playing prompts, connecting calls, and handling DTMF input.
layout: asyncapi
messages:
- description: ''
  name: IncomingCallEvent
  summary: An incoming call has been received
  title: Incoming Call Event
- description: ''
  name: AnsweredCallEvent
  summary: A call has been answered
  title: Answered Call Event
- description: ''
  name: DisconnectedCallEvent
  summary: A call has been disconnected
  title: Disconnected Call Event
- description: ''
  name: PromptInputEvent
  summary: User DTMF input received
  title: Prompt Input Event
- description: ''
  name: NotifyEvent
  summary: Asynchronous call notification
  title: Notification Event
name: Sinch Voice Callbacks
provider_name: Sinch
provider_slug: sinch
servers:
- description: Your server endpoint configured to receive Voice API callbacks. Callback URLs are configured per application in the Sinch Dashboard.
  name: customerServer
  protocol: https
  url: '{callbackUrl}'
slug: sinch-voice-callbacks-asyncapi
source_filename: sinch-voice-callbacks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Sinch Voice Callbacks\n  description: >-\n    Event-driven callbacks for the Sinch Voice API. The Voice API sends HTTP\n    POST callbacks to your application during the lifecycle of a voice call.\n    Your application responds with SVAML (Sinch Voice Application Markup\n    Language) instructions to control the call flow including playing prompts,\n    connecting calls, and handling DTMF input.\n  version: '1.0'\n  contact:\n    name: Sinch Support\n    url: https://www.sinch.com/contact-us/\nservers:\n  customerServer:\n    url: '{callbackUrl}'\n    protocol: https\n    description: >-\n      Your server endpoint configured to receive Voice API callbacks.\n      Callback URLs are configured per application in the Sinch Dashboard.\n    variables:\n      callbackUrl:\n        description: Your callback endpoint URL\nchannels:\n  /voice/ice:\n    description: >-\n      Receives Incoming Call Event (ICE) callbacks when the Sinch platform\n   \
  \   receives an incoming call. Your response instructs the platform how\n      to handle the call using SVAML.\n    publish:\n      operationId: receiveIncomingCallEvent\n      summary: Receive an Incoming Call Event\n      description: >-\n        Triggered when an incoming call is received by the Sinch platform.\n        The response must contain SVAML instructions to control the call.\n      message:\n        $ref: '#/components/messages/IncomingCallEvent'\n  /voice/ace:\n    description: >-\n      Receives Answered Call Event (ACE) callbacks when a call is answered.\n      Your response can provide additional SVAML instructions.\n    publish:\n      operationId: receiveAnsweredCallEvent\n      summary: Receive an Answered Call Event\n      description: >-\n        Triggered when a call is answered by the callee. Can be used to\n        render additional IVR prompts or connect to a conference.\n      message:\n        $ref: '#/components/messages/AnsweredCallEvent'\n  /voice/dice:\n\
  \    description: >-\n      Receives Disconnected Call Event (DiCE) callbacks when a call is\n      disconnected for any reason.\n    publish:\n      operationId: receiveDisconnectedCallEvent\n      summary: Receive a Disconnected Call Event\n      description: >-\n        Triggered when a call is disconnected. Provides the reason for\n        disconnection, call duration, and pricing information.\n      message:\n        $ref: '#/components/messages/DisconnectedCallEvent'\n  /voice/pie:\n    description: >-\n      Receives Prompt Input Event (PIE) callbacks when a user provides\n      DTMF input during an IVR session.\n    publish:\n      operationId: receivePromptInputEvent\n      summary: Receive a Prompt Input Event\n      description: >-\n        Triggered when a user enters DTMF digits during an IVR prompt.\n        Your response can provide new SVAML instructions based on the input.\n      message:\n        $ref: '#/components/messages/PromptInputEvent'\n  /voice/notify:\n    description:\
  \ >-\n      Receives notification callbacks for various call events such as\n      call progress and recording completion.\n    publish:\n      operationId: receiveNotification\n      summary: Receive a notification event\n      description: >-\n        Triggered for various asynchronous call events including recording\n        completion and call progress updates.\n      message:\n        $ref: '#/components/messages/NotifyEvent'\ncomponents:\n  messages:\n    IncomingCallEvent:\n      name: ice\n      title: Incoming Call Event\n      summary: An incoming call has been received\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/IcePayload'\n    AnsweredCallEvent:\n      name: ace\n      title: Answered Call Event\n      summary: A call has been answered\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AcePayload'\n    DisconnectedCallEvent:\n      name: dice\n      title: Disconnected Call Event\n      summary:\
  \ A call has been disconnected\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DicePayload'\n    PromptInputEvent:\n      name: pie\n      title: Prompt Input Event\n      summary: User DTMF input received\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PiePayload'\n    NotifyEvent:\n      name: notify\n      title: Notification Event\n      summary: Asynchronous call notification\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/NotifyPayload'\n  schemas:\n    IcePayload:\n      type: object\n      properties:\n        event:\n          type: string\n          enum:\n            - ice\n          description: The event type\n        callId:\n          type: string\n          description: The unique call identifier\n        callResourceUrl:\n          type: string\n          format: uri\n          description: URL to manage this call\n        timestamp:\n         \
  \ type: string\n          format: date-time\n          description: When the event occurred\n        version:\n          type: integer\n          description: The callback version\n        cli:\n          type: string\n          description: The caller ID\n        to:\n          type: object\n          description: The destination\n          properties:\n            type:\n              type: string\n              description: The destination type\n            endpoint:\n              type: string\n              description: The destination endpoint\n        domain:\n          type: string\n          enum:\n            - pstn\n            - mxp\n          description: The call domain\n        applicationKey:\n          type: string\n          description: The application key\n        originationType:\n          type: string\n          enum:\n            - MXP\n            - PSTN\n          description: The origination type\n        rdnis:\n          type: string\n          description:\
  \ The redirecting number\n        userRate:\n          type: object\n          description: The user rate for the call\n          properties:\n            currencyId:\n              type: string\n              description: Currency code\n            amount:\n              type: number\n              description: Rate amount\n    AcePayload:\n      type: object\n      properties:\n        event:\n          type: string\n          enum:\n            - ace\n          description: The event type\n        callId:\n          type: string\n          description: The unique call identifier\n        callResourceUrl:\n          type: string\n          format: uri\n          description: URL to manage this call\n        timestamp:\n          type: string\n          format: date-time\n          description: When the event occurred\n        version:\n          type: integer\n          description: The callback version\n        amd:\n          type: object\n          description: Answering machine detection\
  \ result\n          properties:\n            status:\n              type: string\n              enum:\n                - human\n                - machine\n              description: Whether a human or machine answered\n            reason:\n              type: string\n              description: The detection reason\n            duration:\n              type: integer\n              description: Detection duration in milliseconds\n    DicePayload:\n      type: object\n      properties:\n        event:\n          type: string\n          enum:\n            - dice\n          description: The event type\n        callId:\n          type: string\n          description: The unique call identifier\n        callResourceUrl:\n          type: string\n          format: uri\n          description: URL to manage this call\n        timestamp:\n          type: string\n          format: date-time\n          description: When the event occurred\n        version:\n          type: integer\n          description:\
  \ The callback version\n        reason:\n          type: string\n          enum:\n            - N/A\n            - TIMEOUT\n            - CALLERHANGUP\n            - CALLEEHANGUP\n            - BLOCKED\n            - MANAGERHANGUP\n            - NOCREDITPARTNER\n            - GENERALERROR\n            - CANCEL\n            - USERNOTFOUND\n          description: The reason for disconnection\n        result:\n          type: string\n          enum:\n            - ANSWERED\n            - BUSY\n            - NOANSWER\n            - FAILED\n          description: The call result\n        from:\n          type: string\n          description: The caller number\n        to:\n          type: string\n          description: The callee number\n        duration:\n          type: integer\n          description: The call duration in seconds\n        debit:\n          type: object\n          description: The call charge\n          properties:\n            currencyId:\n              type: string\n    \
  \          description: Currency code\n            amount:\n              type: number\n              description: Charge amount\n        userRate:\n          type: object\n          description: The user rate\n          properties:\n            currencyId:\n              type: string\n              description: Currency code\n            amount:\n              type: number\n              description: Rate amount\n    PiePayload:\n      type: object\n      properties:\n        event:\n          type: string\n          enum:\n            - pie\n          description: The event type\n        callId:\n          type: string\n          description: The unique call identifier\n        callResourceUrl:\n          type: string\n          format: uri\n          description: URL to manage this call\n        timestamp:\n          type: string\n          format: date-time\n          description: When the event occurred\n        version:\n          type: integer\n          description: The callback\
  \ version\n        menuResult:\n          type: object\n          description: The IVR menu input result\n          properties:\n            menuId:\n              type: string\n              description: The menu identifier\n            type:\n              type: string\n              enum:\n                - sequence\n                - timeout\n                - hangup\n                - invalidinput\n              description: The input result type\n            value:\n              type: string\n              description: The DTMF digits entered\n            inputMethod:\n              type: string\n              enum:\n                - dtmf\n                - voice\n              description: How the input was provided\n    NotifyPayload:\n      type: object\n      properties:\n        event:\n          type: string\n          enum:\n            - notify\n          description: The event type\n        callId:\n          type: string\n          description: The unique call identifier\n\
  \        version:\n          type: integer\n          description: The callback version\n        type:\n          type: string\n          description: The notification type\n        custom:\n          type: string\n          description: Custom data passed from SVAML\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/asyncapi/sinch-voice-callbacks-asyncapi.yml
spec_file: asyncapi/sinch-voice-callbacks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/asyncapi/sinch-voice-callbacks-asyncapi.yml
tags:
- Communications
- Messaging
- SMS
- Voice
- Verification
- CPaaS
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
