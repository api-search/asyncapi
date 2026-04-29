---
channels:
- description: Sent when an outbound call is answered or when an inbound call is received. This is the primary webhook for initiating call flow control via BXML response.
  name: /voice/answer
  operation: publish
  operation_id: onAnswerCallback
  summary: Call answered callback
- description: Sent when an inbound call is received, before the answer callback. Allows your application to perform pre-answer logic such as call screening or routing decisions.
  name: /voice/initiate
  operation: publish
  operation_id: onInitiateCallback
  summary: Call initiate callback
- description: Sent when a call is disconnected for any reason. Provides the disconnect cause and final call state.
  name: /voice/disconnect
  operation: publish
  operation_id: onDisconnectCallback
  summary: Call disconnect callback
- description: Sent when a transferred call is answered by the transfer target.
  name: /voice/transferAnswer
  operation: publish
  operation_id: onTransferAnswerCallback
  summary: Transfer answered callback
- description: Sent when a transferred call is disconnected.
  name: /voice/transferDisconnect
  operation: publish
  operation_id: onTransferDisconnectCallback
  summary: Transfer disconnect callback
- description: Sent when a call is redirected to a new BXML URL via the update call API endpoint.
  name: /voice/redirect
  operation: publish
  operation_id: onRedirectCallback
  summary: Call redirect callback
- description: Sent when a call recording has been completed and the media file is available for download.
  name: /voice/recordingComplete
  operation: publish
  operation_id: onRecordingCompleteCallback
  summary: Recording complete callback
- description: Sent when a recording transcription has been completed and is available for retrieval.
  name: /voice/transcriptionAvailable
  operation: publish
  operation_id: onTranscriptionAvailableCallback
  summary: Transcription available callback
- description: Sent when a DTMF gather operation completes, either because the user pressed the terminating digit or the gather timed out.
  name: /voice/gather
  operation: publish
  operation_id: onGatherCallback
  summary: DTMF gather callback
- description: Sent when a new conference is created.
  name: /voice/conferenceCreated
  operation: publish
  operation_id: onConferenceCreatedCallback
  summary: Conference created callback
- description: Sent when a new member joins a conference.
  name: /voice/conferenceMemberJoin
  operation: publish
  operation_id: onConferenceMemberJoinCallback
  summary: Conference member join callback
- description: Sent when a member leaves a conference.
  name: /voice/conferenceMemberExit
  operation: publish
  operation_id: onConferenceMemberExitCallback
  summary: Conference member exit callback
- description: Sent when a conference ends (all members have left or it was explicitly completed).
  name: /voice/conferenceCompleted
  operation: publish
  operation_id: onConferenceCompletedCallback
  summary: Conference completed callback
description: Bandwidth Voice API sends webhooks (BXML callbacks) to your application for real-time call event notifications. These webhooks inform your application of call state changes and request BXML instructions to control call flow. Your application must respond with HTTP 200 and BXML verbs to direct the call, or HTTP 200 with an empty body to acknowledge the event.
layout: asyncapi
messages:
- description: ''
  name: AnswerCallback
  summary: Sent when an outbound call is answered or an inbound call is received
  title: Answer Callback
- description: ''
  name: InitiateCallback
  summary: Sent when an inbound call is received before the answer callback
  title: Initiate Callback
- description: ''
  name: DisconnectCallback
  summary: Sent when a call is disconnected
  title: Disconnect Callback
- description: ''
  name: TransferAnswerCallback
  summary: Sent when a transferred call is answered
  title: Transfer Answer Callback
- description: ''
  name: TransferDisconnectCallback
  summary: Sent when a transferred call is disconnected
  title: Transfer Disconnect Callback
- description: ''
  name: RedirectCallback
  summary: Sent when a call is redirected
  title: Redirect Callback
- description: ''
  name: RecordingCompleteCallback
  summary: Sent when a call recording is completed
  title: Recording Complete Callback
- description: ''
  name: TranscriptionAvailableCallback
  summary: Sent when a recording transcription is available
  title: Transcription Available Callback
- description: ''
  name: GatherCallback
  summary: Sent when a DTMF gather operation completes
  title: Gather Callback
- description: ''
  name: ConferenceCreatedCallback
  summary: Sent when a conference is created
  title: Conference Created Callback
- description: ''
  name: ConferenceMemberJoinCallback
  summary: Sent when a member joins a conference
  title: Conference Member Join Callback
- description: ''
  name: ConferenceMemberExitCallback
  summary: Sent when a member leaves a conference
  title: Conference Member Exit Callback
- description: ''
  name: ConferenceCompletedCallback
  summary: Sent when a conference ends
  title: Conference Completed Callback
name: Bandwidth Voice Events
provider_name: Bandwidth
provider_slug: bandwidth
servers:
- description: Your application's webhook endpoint. The URL is configured per-call via the answerUrl, disconnectUrl, and other callback URL parameters when creating or updating calls.
  name: production
  protocol: https
  url: '{callbackUrl}'
slug: bandwidth-voice-events-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Bandwidth Voice Events\n  description: >-\n    Bandwidth Voice API sends webhooks (BXML callbacks) to your application\n    for real-time call event notifications. These webhooks inform your\n    application of call state changes and request BXML instructions to\n    control call flow. Your application must respond with HTTP 200 and\n    BXML verbs to direct the call, or HTTP 200 with an empty body to\n    acknowledge the event.\n  version: '2.0'\n  contact:\n    name: Bandwidth Support\n    url: https://support.bandwidth.com\nservers:\n  production:\n    url: '{callbackUrl}'\n    protocol: https\n    description: >-\n      Your application's webhook endpoint. The URL is configured per-call\n      via the answerUrl, disconnectUrl, and other callback URL parameters\n      when creating or updating calls.\n    variables:\n      callbackUrl:\n        description: The URL configured for receiving voice webhooks\n    security:\n      - basicAuth:\
  \ []\nchannels:\n  /voice/answer:\n    description: >-\n      Sent when an outbound call is answered or when an inbound call is\n      received. This is the primary webhook for initiating call flow\n      control via BXML response.\n    publish:\n      operationId: onAnswerCallback\n      summary: Call answered callback\n      message:\n        $ref: '#/components/messages/AnswerCallback'\n  /voice/initiate:\n    description: >-\n      Sent when an inbound call is received, before the answer callback.\n      Allows your application to perform pre-answer logic such as call\n      screening or routing decisions.\n    publish:\n      operationId: onInitiateCallback\n      summary: Call initiate callback\n      message:\n        $ref: '#/components/messages/InitiateCallback'\n  /voice/disconnect:\n    description: >-\n      Sent when a call is disconnected for any reason. Provides the\n      disconnect cause and final call state.\n    publish:\n      operationId: onDisconnectCallback\n   \
  \   summary: Call disconnect callback\n      message:\n        $ref: '#/components/messages/DisconnectCallback'\n  /voice/transferAnswer:\n    description: >-\n      Sent when a transferred call is answered by the transfer target.\n    publish:\n      operationId: onTransferAnswerCallback\n      summary: Transfer answered callback\n      message:\n        $ref: '#/components/messages/TransferAnswerCallback'\n  /voice/transferDisconnect:\n    description: >-\n      Sent when a transferred call is disconnected.\n    publish:\n      operationId: onTransferDisconnectCallback\n      summary: Transfer disconnect callback\n      message:\n        $ref: '#/components/messages/TransferDisconnectCallback'\n  /voice/redirect:\n    description: >-\n      Sent when a call is redirected to a new BXML URL via the update\n      call API endpoint.\n    publish:\n      operationId: onRedirectCallback\n      summary: Call redirect callback\n      message:\n        $ref: '#/components/messages/RedirectCallback'\n\
  \  /voice/recordingComplete:\n    description: >-\n      Sent when a call recording has been completed and the media file\n      is available for download.\n    publish:\n      operationId: onRecordingCompleteCallback\n      summary: Recording complete callback\n      message:\n        $ref: '#/components/messages/RecordingCompleteCallback'\n  /voice/transcriptionAvailable:\n    description: >-\n      Sent when a recording transcription has been completed and is\n      available for retrieval.\n    publish:\n      operationId: onTranscriptionAvailableCallback\n      summary: Transcription available callback\n      message:\n        $ref: '#/components/messages/TranscriptionAvailableCallback'\n  /voice/gather:\n    description: >-\n      Sent when a DTMF gather operation completes, either because the\n      user pressed the terminating digit or the gather timed out.\n    publish:\n      operationId: onGatherCallback\n      summary: DTMF gather callback\n      message:\n        $ref: '#/components/messages/GatherCallback'\n\
  \  /voice/conferenceCreated:\n    description: >-\n      Sent when a new conference is created.\n    publish:\n      operationId: onConferenceCreatedCallback\n      summary: Conference created callback\n      message:\n        $ref: '#/components/messages/ConferenceCreatedCallback'\n  /voice/conferenceMemberJoin:\n    description: >-\n      Sent when a new member joins a conference.\n    publish:\n      operationId: onConferenceMemberJoinCallback\n      summary: Conference member join callback\n      message:\n        $ref: '#/components/messages/ConferenceMemberJoinCallback'\n  /voice/conferenceMemberExit:\n    description: >-\n      Sent when a member leaves a conference.\n    publish:\n      operationId: onConferenceMemberExitCallback\n      summary: Conference member exit callback\n      message:\n        $ref: '#/components/messages/ConferenceMemberExitCallback'\n  /voice/conferenceCompleted:\n    description: >-\n      Sent when a conference ends (all members have left or it was\n\
  \      explicitly completed).\n    publish:\n      operationId: onConferenceCompletedCallback\n      summary: Conference completed callback\n      message:\n        $ref: '#/components/messages/ConferenceCompletedCallback'\ncomponents:\n  securitySchemes:\n    basicAuth:\n      type: http\n      scheme: basic\n      description: >-\n        Optional HTTP Basic Authentication for webhook endpoints.\n        Configure credentials in your Bandwidth application settings.\n  messages:\n    AnswerCallback:\n      name: AnswerCallback\n      title: Answer Callback\n      summary: >-\n        Sent when an outbound call is answered or an inbound call is received\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AnswerEvent'\n    InitiateCallback:\n      name: InitiateCallback\n      title: Initiate Callback\n      summary: >-\n        Sent when an inbound call is received before the answer callback\n      contentType: application/json\n      payload:\n  \
  \      $ref: '#/components/schemas/InitiateEvent'\n    DisconnectCallback:\n      name: DisconnectCallback\n      title: Disconnect Callback\n      summary: Sent when a call is disconnected\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DisconnectEvent'\n    TransferAnswerCallback:\n      name: TransferAnswerCallback\n      title: Transfer Answer Callback\n      summary: Sent when a transferred call is answered\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TransferAnswerEvent'\n    TransferDisconnectCallback:\n      name: TransferDisconnectCallback\n      title: Transfer Disconnect Callback\n      summary: Sent when a transferred call is disconnected\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TransferDisconnectEvent'\n    RedirectCallback:\n      name: RedirectCallback\n      title: Redirect Callback\n      summary: Sent when a call is redirected\n     \
  \ contentType: application/json\n      payload:\n        $ref: '#/components/schemas/RedirectEvent'\n    RecordingCompleteCallback:\n      name: RecordingCompleteCallback\n      title: Recording Complete Callback\n      summary: Sent when a call recording is completed\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/RecordingCompleteEvent'\n    TranscriptionAvailableCallback:\n      name: TranscriptionAvailableCallback\n      title: Transcription Available Callback\n      summary: Sent when a recording transcription is available\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TranscriptionAvailableEvent'\n    GatherCallback:\n      name: GatherCallback\n      title: Gather Callback\n      summary: Sent when a DTMF gather operation completes\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/GatherEvent'\n    ConferenceCreatedCallback:\n      name: ConferenceCreatedCallback\n\
  \      title: Conference Created Callback\n      summary: Sent when a conference is created\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ConferenceCreatedEvent'\n    ConferenceMemberJoinCallback:\n      name: ConferenceMemberJoinCallback\n      title: Conference Member Join Callback\n      summary: Sent when a member joins a conference\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ConferenceMemberJoinEvent'\n    ConferenceMemberExitCallback:\n      name: ConferenceMemberExitCallback\n      title: Conference Member Exit Callback\n      summary: Sent when a member leaves a conference\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ConferenceMemberExitEvent'\n    ConferenceCompletedCallback:\n      name: ConferenceCompletedCallback\n      title: Conference Completed Callback\n      summary: Sent when a conference ends\n      contentType: application/json\n   \
  \   payload:\n        $ref: '#/components/schemas/ConferenceCompletedEvent'\n  schemas:\n    BaseCallEvent:\n      type: object\n      properties:\n        eventType:\n          type: string\n          description: The type of voice event\n        accountId:\n          type: string\n          description: The Bandwidth account ID\n        applicationId:\n          type: string\n          description: The application ID associated with the call\n        callId:\n          type: string\n          description: The unique call identifier\n        to:\n          type: string\n          description: The destination phone number\n        from:\n          type: string\n          description: The originating phone number\n        direction:\n          type: string\n          enum:\n            - inbound\n            - outbound\n          description: The direction of the call\n        callUrl:\n          type: string\n          format: uri\n          description: The URL for the call resource\n\
  \        startTime:\n          type: string\n          format: date-time\n          description: The time the call started\n        tag:\n          type: string\n          description: Custom tag attached to the call\n    AnswerEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseCallEvent'\n        - type: object\n          properties:\n            eventType:\n              type: string\n              const: answer\n              description: Event type is always answer\n            answerTime:\n              type: string\n              format: date-time\n              description: The time the call was answered\n    InitiateEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseCallEvent'\n        - type: object\n          properties:\n            eventType:\n              type: string\n              const: initiate\n              description: Event type is always initiate\n    DisconnectEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseCallEvent'\n\
  \        - type: object\n          properties:\n            eventType:\n              type: string\n              const: disconnect\n              description: Event type is always disconnect\n            endTime:\n              type: string\n              format: date-time\n              description: The time the call ended\n            cause:\n              type: string\n              description: >-\n                The reason for the disconnect (e.g., hangup, timeout,\n                cancel, rejected, callback-error)\n            errorMessage:\n              type: string\n              description: Error message if the disconnect was due to an error\n            errorId:\n              type: string\n              description: Error ID for troubleshooting\n    TransferAnswerEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseCallEvent'\n        - type: object\n          properties:\n            eventType:\n              type: string\n              const: transferAnswer\n\
  \              description: Event type is always transferAnswer\n            transferCallId:\n              type: string\n              description: The call ID of the original call that initiated the transfer\n            transferTo:\n              type: string\n              description: The phone number the call was transferred to\n    TransferDisconnectEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseCallEvent'\n        - type: object\n          properties:\n            eventType:\n              type: string\n              const: transferDisconnect\n              description: Event type is always transferDisconnect\n            transferCallId:\n              type: string\n              description: The call ID of the original call\n            cause:\n              type: string\n              description: The reason for the disconnect\n    RedirectEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseCallEvent'\n        - type: object\n          properties:\n\
  \            eventType:\n              type: string\n              const: redirect\n              description: Event type is always redirect\n    RecordingCompleteEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseCallEvent'\n        - type: object\n          properties:\n            eventType:\n              type: string\n              const: recording\n              description: Event type is always recording\n            recordingId:\n              type: string\n              description: The unique recording identifier\n            channels:\n              type: integer\n              description: The number of audio channels\n            duration:\n              type: string\n              description: The duration of the recording\n            fileFormat:\n              type: string\n              enum:\n                - wav\n                - mp3\n              description: The audio format\n            mediaUrl:\n              type: string\n              format: uri\n\
  \              description: The URL to download the recording\n            status:\n              type: string\n              enum:\n                - complete\n                - partial\n                - error\n              description: The recording status\n    TranscriptionAvailableEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseCallEvent'\n        - type: object\n          properties:\n            eventType:\n              type: string\n              const: transcription\n              description: Event type is always transcription\n            recordingId:\n              type: string\n              description: The recording ID that was transcribed\n            transcriptionId:\n              type: string\n              description: The unique transcription identifier\n            transcriptionUrl:\n              type: string\n              format: uri\n              description: The URL to retrieve the transcription\n    GatherEvent:\n      allOf:\n        - $ref:\
  \ '#/components/schemas/BaseCallEvent'\n        - type: object\n          properties:\n            eventType:\n              type: string\n              const: gather\n              description: Event type is always gather\n            digits:\n              type: string\n              description: The DTMF digits collected from the caller\n            terminatingDigit:\n              type: string\n              description: The digit that terminated the gather\n    ConferenceCreatedEvent:\n      type: object\n      properties:\n        eventType:\n          type: string\n          const: conferenceCreated\n          description: Event type is always conferenceCreated\n        conferenceId:\n          type: string\n          description: The unique conference identifier\n        name:\n          type: string\n          description: The conference name\n        tag:\n          type: string\n          description: Custom tag for the conference\n    ConferenceMemberJoinEvent:\n      type:\
  \ object\n      properties:\n        eventType:\n          type: string\n          const: conferenceMemberJoin\n          description: Event type is always conferenceMemberJoin\n        conferenceId:\n          type: string\n          description: The conference identifier\n        name:\n          type: string\n          description: The conference name\n        callId:\n          type: string\n          description: The call ID of the member who joined\n        tag:\n          type: string\n          description: Custom tag\n    ConferenceMemberExitEvent:\n      type: object\n      properties:\n        eventType:\n          type: string\n          const: conferenceMemberExit\n          description: Event type is always conferenceMemberExit\n        conferenceId:\n          type: string\n          description: The conference identifier\n        name:\n          type: string\n          description: The conference name\n        callId:\n          type: string\n          description: The\
  \ call ID of the member who left\n        tag:\n          type: string\n          description: Custom tag\n    ConferenceCompletedEvent:\n      type: object\n      properties:\n        eventType:\n          type: string\n          const: conferenceCompleted\n          description: Event type is always conferenceCompleted\n        conferenceId:\n          type: string\n          description: The conference identifier\n        name:\n          type: string\n          description: The conference name\n        tag:\n          type: string\n          description: Custom tag\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/bandwidth/refs/heads/main/asyncapi/bandwidth-voice-events-asyncapi.yml
spec_file: asyncapi/bandwidth-voice-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/bandwidth/refs/heads/main/asyncapi/bandwidth-voice-events-asyncapi.yml
tags:
- Communications
- CPaaS
- Voice
- Messaging
- Telephony
- SMS
- MFA
- AsyncAPI
- Webhooks
- Events
version: '2.0'
---
