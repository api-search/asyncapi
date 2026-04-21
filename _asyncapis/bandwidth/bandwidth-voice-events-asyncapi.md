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
