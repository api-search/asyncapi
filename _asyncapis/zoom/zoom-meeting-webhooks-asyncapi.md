---
api_specs:
- filename: zoom-chat--openapi-original.yml
  format: yaml
  label: Zoom Chat API
  slug: zoom-chat-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/openapi/zoom-chat--openapi-original.yml
- filename: zoom-group--openapi-original.yml
  format: yaml
  label: Zoom Group API
  slug: zoom-group-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/openapi/zoom-group--openapi-original.yml
- filename: zoom-device--openapi-original.yml
  format: yaml
  label: Zoom Device API
  slug: zoom-device-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/openapi/zoom-device--openapi-original.yml
- filename: zoom-im--openapi-original.yml
  format: yaml
  label: Zoom Instant Message API
  slug: zoom-instant-message-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/openapi/zoom-im--openapi-original.yml
- filename: zoom-account--openapi-original.yml
  format: yaml
  label: Zoom Account API
  slug: zoom-account-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/openapi/zoom-account--openapi-original.yml
- filename: zoom-recording--openapi-original.yml
  format: yaml
  label: Zoom Recording API
  slug: zoom-recording-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/openapi/zoom-recording--openapi-original.yml
- filename: zoom-meeting--openapi-original.yml
  format: yaml
  label: Zoom Meeting API
  slug: zoom-meeting-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/openapi/zoom-meeting--openapi-original.yml
- filename: zoom-metrics--openapi-original.yml
  format: yaml
  label: Zoom Metrics API
  slug: zoom-metrics-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/openapi/zoom-metrics--openapi-original.yml
- filename: zoom-report--openapi-original.yml
  format: yaml
  label: Zoom Report API
  slug: zoom-report-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/openapi/zoom-report--openapi-original.yml
- filename: zoom-user--openapi-original.yml
  format: yaml
  label: Zoom User API
  slug: zoom-user-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/openapi/zoom-user--openapi-original.yml
- filename: zoom-webinar--openapi-original.yml
  format: yaml
  label: Zoom Webinar API
  slug: zoom-webinar-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/openapi/zoom-webinar--openapi-original.yml
channels:
- description: Triggered when a meeting is created by a host or on behalf of a host.
  name: meetingCreated
- description: Triggered when a meeting is updated, including changes to topic, time, settings, or other meeting properties.
  name: meetingUpdated
- description: Triggered when a meeting is deleted by the host or an admin.
  name: meetingDeleted
- description: Triggered when a meeting starts. This event fires when the host or the first participant joins the meeting.
  name: meetingStarted
- description: Triggered when a meeting ends. This event fires when all participants have left the meeting or the host ends the meeting.
  name: meetingEnded
- description: Triggered when a previously deleted meeting is recovered from trash.
  name: meetingRecoveredFromTrash
- description: Triggered when a meeting is permanently deleted and can no longer be recovered.
  name: meetingPermanentlyDeleted
- description: Triggered when a participant joins a meeting. Includes participant details such as name, email, and join time.
  name: meetingParticipantJoined
- description: Triggered when a participant leaves a meeting. Includes participant details and leave reason.
  name: meetingParticipantLeft
- description: Triggered when a participant is waiting in the waiting room or waiting for the host to start the meeting.
  name: meetingParticipantWaitingForHost
- description: Triggered when a participant is admitted from the waiting room.
  name: meetingParticipantAdmittedFromWaitingRoom
- description: Triggered when a participant is placed in the waiting room during a meeting.
  name: meetingParticipantPutInWaitingRoom
- description: Triggered when a new registrant registers for a meeting.
  name: meetingRegistrationCreated
- description: Triggered when a meeting registration is approved.
  name: meetingRegistrationApproved
- description: Triggered when a meeting registration is cancelled.
  name: meetingRegistrationCancelled
- description: Triggered when a meeting registration is denied.
  name: meetingRegistrationDenied
- description: Triggered when a participant starts sharing their screen in a meeting.
  name: meetingSharingStarted
- description: Triggered when a participant stops sharing their screen in a meeting.
  name: meetingSharingEnded
- description: Triggered when a cloud recording for a meeting has been processed and is available for download.
  name: meetingRecordingCompleted
- description: Triggered when cloud recording starts for a meeting.
  name: meetingRecordingStarted
- description: Triggered when cloud recording stops for a meeting.
  name: meetingRecordingStopped
- description: Triggered when cloud recording is paused during a meeting.
  name: meetingRecordingPaused
- description: Triggered when cloud recording is resumed during a meeting.
  name: meetingRecordingResumed
- description: Triggered when a cloud recording is moved to trash.
  name: meetingRecordingTrashed
- description: Triggered when a cloud recording is permanently deleted.
  name: meetingRecordingDeleted
- description: Triggered when a cloud recording is recovered from trash.
  name: meetingRecordingRecovered
- description: Triggered when a recording transcript is completed and available.
  name: meetingRecordingTranscriptCompleted
- description: Triggered when a meeting quality alert is detected, such as poor network quality or audio issues.
  name: meetingAlert
description: Zoom delivers webhook event notifications to your application when meeting-related events occur on the Zoom platform. These webhooks enable real-time integration with meeting lifecycle events including creation, updates, starts, ends, participant joins and leaves, recordings, and alerts. Configure your webhook endpoint in the Zoom Marketplace to receive these event notifications.
layout: asyncapi
messages:
- description: ''
  name: MeetingCreated
  summary: A meeting has been created.
  title: Meeting Created
- description: ''
  name: MeetingUpdated
  summary: A meeting has been updated.
  title: Meeting Updated
- description: ''
  name: MeetingDeleted
  summary: A meeting has been deleted.
  title: Meeting Deleted
- description: ''
  name: MeetingStarted
  summary: A meeting has started.
  title: Meeting Started
- description: ''
  name: MeetingEnded
  summary: A meeting has ended.
  title: Meeting Ended
- description: ''
  name: MeetingRecovered
  summary: A deleted meeting has been recovered from trash.
  title: Meeting Recovered from Trash
- description: ''
  name: MeetingPermanentlyDeleted
  summary: A meeting has been permanently deleted.
  title: Meeting Permanently Deleted
- description: ''
  name: ParticipantJoined
  summary: A participant has joined a meeting.
  title: Participant Joined Meeting
- description: ''
  name: ParticipantLeft
  summary: A participant has left a meeting.
  title: Participant Left Meeting
- description: ''
  name: ParticipantWaitingForHost
  summary: A participant is waiting for the host or in the waiting room.
  title: Participant Waiting for Host
- description: ''
  name: ParticipantAdmittedFromWaitingRoom
  summary: A participant has been admitted from the waiting room.
  title: Participant Admitted from Waiting Room
- description: ''
  name: ParticipantPutInWaitingRoom
  summary: A participant has been placed in the waiting room.
  title: Participant Put in Waiting Room
- description: ''
  name: RegistrationCreated
  summary: A new registrant has registered for a meeting.
  title: Meeting Registration Created
- description: ''
  name: RegistrationApproved
  summary: A meeting registration has been approved.
  title: Meeting Registration Approved
- description: ''
  name: RegistrationCancelled
  summary: A meeting registration has been cancelled.
  title: Meeting Registration Cancelled
- description: ''
  name: RegistrationDenied
  summary: A meeting registration has been denied.
  title: Meeting Registration Denied
- description: ''
  name: MeetingSharingStarted
  summary: Screen sharing has started in a meeting.
  title: Meeting Sharing Started
- description: ''
  name: MeetingSharingEnded
  summary: Screen sharing has ended in a meeting.
  title: Meeting Sharing Ended
- description: ''
  name: RecordingCompleted
  summary: Cloud recording has been processed and is available for download.
  title: Recording Completed
- description: ''
  name: RecordingStarted
  summary: Cloud recording has started.
  title: Recording Started
- description: ''
  name: RecordingStopped
  summary: Cloud recording has stopped.
  title: Recording Stopped
- description: ''
  name: RecordingPaused
  summary: Cloud recording has been paused.
  title: Recording Paused
- description: ''
  name: RecordingResumed
  summary: Cloud recording has been resumed.
  title: Recording Resumed
- description: ''
  name: RecordingTrashed
  summary: A cloud recording has been moved to trash.
  title: Recording Trashed
- description: ''
  name: RecordingDeleted
  summary: A cloud recording has been permanently deleted.
  title: Recording Deleted
- description: ''
  name: RecordingRecovered
  summary: A cloud recording has been recovered from trash.
  title: Recording Recovered
- description: ''
  name: RecordingTranscriptCompleted
  summary: A recording transcript has been completed and is available.
  title: Recording Transcript Completed
- description: ''
  name: MeetingAlert
  summary: A meeting quality alert has been triggered, such as poor network quality or audio/video issues.
  title: Meeting Alert
name: Zoom Meeting Webhooks
provider_name: Zoom
provider_slug: zoom
servers:
- description: Your application's webhook endpoint URL. Zoom sends HTTP POST requests to this URL when events occur. Configure this URL in your Zoom Marketplace app settings under the Event Subscriptions section.
  name: zoomWebhookEndpoint
  protocol: https
  url: ''
slug: zoom-meeting-webhooks-asyncapi
source_filename: zoom-meeting-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 3.0.0\ninfo:\n  title: Zoom Meeting Webhooks\n  version: 2.0.0\n  description: >-\n    Zoom delivers webhook event notifications to your application when meeting-related\n    events occur on the Zoom platform. These webhooks enable real-time integration\n    with meeting lifecycle events including creation, updates, starts, ends,\n    participant joins and leaves, recordings, and alerts. Configure your webhook\n    endpoint in the Zoom Marketplace to receive these event notifications.\n  contact:\n    name: Zoom Developer Support\n    url: https://developers.zoom.us\n    email: developer-support@zoom.us\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\n  termsOfService: https://explore.zoom.us/en/terms/\n  externalDocs:\n    description: Zoom Webhook Event Reference\n    url: https://developers.zoom.us/docs/api/rest/reference/zoom-api/events/\n  tags:\n    - name: meeting\n      description: Meeting lifecycle webhook events.\n\
  \    - name: recording\n      description: Recording-related webhook events.\n    - name: participant\n      description: Participant join and leave webhook events.\nservers:\n  zoomWebhookEndpoint:\n    host: '{yourWebhookEndpoint}'\n    protocol: https\n    description: >-\n      Your application's webhook endpoint URL. Zoom sends HTTP POST requests\n      to this URL when events occur. Configure this URL in your Zoom Marketplace\n      app settings under the Event Subscriptions section.\n    variables:\n      yourWebhookEndpoint:\n        description: >-\n          The fully qualified domain and path of your webhook receiver\n          (e.g., api.example.com/webhooks/zoom).\n    security:\n      - $ref: '#/components/securitySchemes/webhookVerificationToken'\ndefaultContentType: application/json\nchannels:\n  meetingCreated:\n    address: /webhook\n    description: >-\n      Triggered when a meeting is created by a host or on behalf of a host.\n    messages:\n      meetingCreatedMessage:\n\
  \        $ref: '#/components/messages/MeetingCreated'\n  meetingUpdated:\n    address: /webhook\n    description: >-\n      Triggered when a meeting is updated, including changes to topic, time,\n      settings, or other meeting properties.\n    messages:\n      meetingUpdatedMessage:\n        $ref: '#/components/messages/MeetingUpdated'\n  meetingDeleted:\n    address: /webhook\n    description: >-\n      Triggered when a meeting is deleted by the host or an admin.\n    messages:\n      meetingDeletedMessage:\n        $ref: '#/components/messages/MeetingDeleted'\n  meetingStarted:\n    address: /webhook\n    description: >-\n      Triggered when a meeting starts. This event fires when the host or\n      the first participant joins the meeting.\n    messages:\n      meetingStartedMessage:\n        $ref: '#/components/messages/MeetingStarted'\n  meetingEnded:\n    address: /webhook\n    description: >-\n      Triggered when a meeting ends. This event fires when all participants\n      have\
  \ left the meeting or the host ends the meeting.\n    messages:\n      meetingEndedMessage:\n        $ref: '#/components/messages/MeetingEnded'\n  meetingRecoveredFromTrash:\n    address: /webhook\n    description: >-\n      Triggered when a previously deleted meeting is recovered from trash.\n    messages:\n      meetingRecoveredMessage:\n        $ref: '#/components/messages/MeetingRecovered'\n  meetingPermanentlyDeleted:\n    address: /webhook\n    description: >-\n      Triggered when a meeting is permanently deleted and can no longer\n      be recovered.\n    messages:\n      meetingPermanentlyDeletedMessage:\n        $ref: '#/components/messages/MeetingPermanentlyDeleted'\n  meetingParticipantJoined:\n    address: /webhook\n    description: >-\n      Triggered when a participant joins a meeting. Includes participant\n      details such as name, email, and join time.\n    messages:\n      participantJoinedMessage:\n        $ref: '#/components/messages/ParticipantJoined'\n  meetingParticipantLeft:\n\
  \    address: /webhook\n    description: >-\n      Triggered when a participant leaves a meeting. Includes participant\n      details and leave reason.\n    messages:\n      participantLeftMessage:\n        $ref: '#/components/messages/ParticipantLeft'\n  meetingParticipantWaitingForHost:\n    address: /webhook\n    description: >-\n      Triggered when a participant is waiting in the waiting room or\n      waiting for the host to start the meeting.\n    messages:\n      participantWaitingMessage:\n        $ref: '#/components/messages/ParticipantWaitingForHost'\n  meetingParticipantAdmittedFromWaitingRoom:\n    address: /webhook\n    description: >-\n      Triggered when a participant is admitted from the waiting room.\n    messages:\n      participantAdmittedMessage:\n        $ref: '#/components/messages/ParticipantAdmittedFromWaitingRoom'\n  meetingParticipantPutInWaitingRoom:\n    address: /webhook\n    description: >-\n      Triggered when a participant is placed in the waiting room\
  \ during\n      a meeting.\n    messages:\n      participantPutInWaitingRoomMessage:\n        $ref: '#/components/messages/ParticipantPutInWaitingRoom'\n  meetingRegistrationCreated:\n    address: /webhook\n    description: >-\n      Triggered when a new registrant registers for a meeting.\n    messages:\n      registrationCreatedMessage:\n        $ref: '#/components/messages/RegistrationCreated'\n  meetingRegistrationApproved:\n    address: /webhook\n    description: >-\n      Triggered when a meeting registration is approved.\n    messages:\n      registrationApprovedMessage:\n        $ref: '#/components/messages/RegistrationApproved'\n  meetingRegistrationCancelled:\n    address: /webhook\n    description: >-\n      Triggered when a meeting registration is cancelled.\n    messages:\n      registrationCancelledMessage:\n        $ref: '#/components/messages/RegistrationCancelled'\n  meetingRegistrationDenied:\n    address: /webhook\n    description: >-\n      Triggered when a meeting\
  \ registration is denied.\n    messages:\n      registrationDeniedMessage:\n        $ref: '#/components/messages/RegistrationDenied'\n  meetingSharingStarted:\n    address: /webhook\n    description: >-\n      Triggered when a participant starts sharing their screen in a meeting.\n    messages:\n      sharingStartedMessage:\n        $ref: '#/components/messages/MeetingSharingStarted'\n  meetingSharingEnded:\n    address: /webhook\n    description: >-\n      Triggered when a participant stops sharing their screen in a meeting.\n    messages:\n      sharingEndedMessage:\n        $ref: '#/components/messages/MeetingSharingEnded'\n  meetingRecordingCompleted:\n    address: /webhook\n    description: >-\n      Triggered when a cloud recording for a meeting has been processed\n      and is available for download.\n    messages:\n      recordingCompletedMessage:\n        $ref: '#/components/messages/RecordingCompleted'\n  meetingRecordingStarted:\n    address: /webhook\n    description: >-\n\
  \      Triggered when cloud recording starts for a meeting.\n    messages:\n      recordingStartedMessage:\n        $ref: '#/components/messages/RecordingStarted'\n  meetingRecordingStopped:\n    address: /webhook\n    description: >-\n      Triggered when cloud recording stops for a meeting.\n    messages:\n      recordingStoppedMessage:\n        $ref: '#/components/messages/RecordingStopped'\n  meetingRecordingPaused:\n    address: /webhook\n    description: >-\n      Triggered when cloud recording is paused during a meeting.\n    messages:\n      recordingPausedMessage:\n        $ref: '#/components/messages/RecordingPaused'\n  meetingRecordingResumed:\n    address: /webhook\n    description: >-\n      Triggered when cloud recording is resumed during a meeting.\n    messages:\n      recordingResumedMessage:\n        $ref: '#/components/messages/RecordingResumed'\n  meetingRecordingTrashed:\n    address: /webhook\n    description: >-\n      Triggered when a cloud recording is moved to\
  \ trash.\n    messages:\n      recordingTrashedMessage:\n        $ref: '#/components/messages/RecordingTrashed'\n  meetingRecordingDeleted:\n    address: /webhook\n    description: >-\n      Triggered when a cloud recording is permanently deleted.\n    messages:\n      recordingDeletedMessage:\n        $ref: '#/components/messages/RecordingDeleted'\n  meetingRecordingRecovered:\n    address: /webhook\n    description: >-\n      Triggered when a cloud recording is recovered from trash.\n    messages:\n      recordingRecoveredMessage:\n        $ref: '#/components/messages/RecordingRecovered'\n  meetingRecordingTranscriptCompleted:\n    address: /webhook\n    description: >-\n      Triggered when a recording transcript is completed and available.\n    messages:\n      transcriptCompletedMessage:\n        $ref: '#/components/messages/RecordingTranscriptCompleted'\n  meetingAlert:\n    address: /webhook\n    description: >-\n      Triggered when a meeting quality alert is detected, such as\
  \ poor\n      network quality or audio issues.\n    messages:\n      meetingAlertMessage:\n        $ref: '#/components/messages/MeetingAlert'\noperations:\n  receiveMeetingCreated:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingCreated'\n    summary: Receive meeting.created event\n    tags:\n      - $ref: '#/components/tags/meeting'\n  receiveMeetingUpdated:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingUpdated'\n    summary: Receive meeting.updated event\n    tags:\n      - $ref: '#/components/tags/meeting'\n  receiveMeetingDeleted:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingDeleted'\n    summary: Receive meeting.deleted event\n    tags:\n      - $ref: '#/components/tags/meeting'\n  receiveMeetingStarted:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingStarted'\n    summary: Receive meeting.started event\n    tags:\n      - $ref: '#/components/tags/meeting'\n  receiveMeetingEnded:\n    action: receive\n\
  \    channel:\n      $ref: '#/channels/meetingEnded'\n    summary: Receive meeting.ended event\n    tags:\n      - $ref: '#/components/tags/meeting'\n  receiveMeetingRecovered:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRecoveredFromTrash'\n    summary: Receive meeting.recovered event\n    tags:\n      - $ref: '#/components/tags/meeting'\n  receiveMeetingPermanentlyDeleted:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingPermanentlyDeleted'\n    summary: Receive meeting.permanently_deleted event\n    tags:\n      - $ref: '#/components/tags/meeting'\n  receiveParticipantJoined:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingParticipantJoined'\n    summary: Receive meeting.participant_joined event\n    tags:\n      - $ref: '#/components/tags/participant'\n  receiveParticipantLeft:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingParticipantLeft'\n    summary: Receive meeting.participant_left event\n    tags:\n\
  \      - $ref: '#/components/tags/participant'\n  receiveParticipantWaiting:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingParticipantWaitingForHost'\n    summary: Receive meeting.participant_joined_waiting_room event\n    tags:\n      - $ref: '#/components/tags/participant'\n  receiveParticipantAdmitted:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingParticipantAdmittedFromWaitingRoom'\n    summary: Receive meeting.participant_admitted event\n    tags:\n      - $ref: '#/components/tags/participant'\n  receiveParticipantPutInWaitingRoom:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingParticipantPutInWaitingRoom'\n    summary: Receive meeting.participant_put_in_waiting_room event\n    tags:\n      - $ref: '#/components/tags/participant'\n  receiveRegistrationCreated:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRegistrationCreated'\n    summary: Receive meeting.registration_created event\n    tags:\n    \
  \  - $ref: '#/components/tags/meeting'\n  receiveRegistrationApproved:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRegistrationApproved'\n    summary: Receive meeting.registration_approved event\n    tags:\n      - $ref: '#/components/tags/meeting'\n  receiveRegistrationCancelled:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRegistrationCancelled'\n    summary: Receive meeting.registration_cancelled event\n    tags:\n      - $ref: '#/components/tags/meeting'\n  receiveRegistrationDenied:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRegistrationDenied'\n    summary: Receive meeting.registration_denied event\n    tags:\n      - $ref: '#/components/tags/meeting'\n  receiveSharingStarted:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingSharingStarted'\n    summary: Receive meeting.sharing_started event\n    tags:\n      - $ref: '#/components/tags/meeting'\n  receiveSharingEnded:\n    action: receive\n   \
  \ channel:\n      $ref: '#/channels/meetingSharingEnded'\n    summary: Receive meeting.sharing_ended event\n    tags:\n      - $ref: '#/components/tags/meeting'\n  receiveRecordingCompleted:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRecordingCompleted'\n    summary: Receive recording.completed event\n    tags:\n      - $ref: '#/components/tags/recording'\n  receiveRecordingStarted:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRecordingStarted'\n    summary: Receive recording.started event\n    tags:\n      - $ref: '#/components/tags/recording'\n  receiveRecordingStopped:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRecordingStopped'\n    summary: Receive recording.stopped event\n    tags:\n      - $ref: '#/components/tags/recording'\n  receiveRecordingPaused:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRecordingPaused'\n    summary: Receive recording.paused event\n    tags:\n      - $ref: '#/components/tags/recording'\n\
  \  receiveRecordingResumed:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRecordingResumed'\n    summary: Receive recording.resumed event\n    tags:\n      - $ref: '#/components/tags/recording'\n  receiveRecordingTrashed:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRecordingTrashed'\n    summary: Receive recording.trashed event\n    tags:\n      - $ref: '#/components/tags/recording'\n  receiveRecordingDeleted:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRecordingDeleted'\n    summary: Receive recording.deleted event\n    tags:\n      - $ref: '#/components/tags/recording'\n  receiveRecordingRecovered:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRecordingRecovered'\n    summary: Receive recording.recovered event\n    tags:\n      - $ref: '#/components/tags/recording'\n  receiveRecordingTranscriptCompleted:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingRecordingTranscriptCompleted'\n\
  \    summary: Receive recording.transcript_completed event\n    tags:\n      - $ref: '#/components/tags/recording'\n  receiveMeetingAlert:\n    action: receive\n    channel:\n      $ref: '#/channels/meetingAlert'\n    summary: Receive meeting.alert event\n    tags:\n      - $ref: '#/components/tags/meeting'\ncomponents:\n  tags:\n    meeting:\n      name: meeting\n      description: Meeting lifecycle events\n    recording:\n      name: recording\n      description: Recording events\n    participant:\n      name: participant\n      description: Participant events\n  securitySchemes:\n    webhookVerificationToken:\n      type: httpApiKey\n      name: Authorization\n      in: header\n      description: >-\n        Zoom uses a verification token sent in webhook headers to validate\n        that requests originate from Zoom. Your app must verify the token\n        in the `authorization` header matches your app's verification token.\n        Zoom also supports URL validation via a challenge-response\
  \ mechanism\n        and webhook signature verification using the `x-zm-signature` and\n        `x-zm-request-timestamp` headers with HMAC-SHA256.\n  schemas:\n    WebhookEventEnvelope:\n      type: object\n      description: >-\n        The standard envelope for all Zoom webhook event payloads. Every\n        webhook notification includes these top-level fields.\n      required:\n        - event\n        - event_ts\n        - payload\n      properties:\n        event:\n          type: string\n          description: >-\n            The event type identifier (e.g., meeting.started,\n            meeting.participant_joined).\n        event_ts:\n          type: integer\n          format: int64\n          description: Timestamp of the event in milliseconds since epoch.\n        payload:\n          type: object\n          description: Event-specific payload data.\n          properties:\n            account_id:\n              type: string\n              description: The account ID of the Zoom\
  \ account.\n            operator:\n              type: string\n              description: >-\n                Email address of the user who triggered the event, if\n                applicable.\n            operator_id:\n              type: string\n              description: User ID of the operator.\n            object:\n              type: object\n              description: The event-specific object data.\n        download_token:\n          type: string\n          description: >-\n            A short-lived token for downloading recording files. Only present\n            in recording events. Valid for a limited time.\n    MeetingObject:\n      type: object\n      description: Core meeting object included in webhook payloads.\n      properties:\n        uuid:\n          type: string\n          description: Unique meeting instance ID.\n        id:\n          type: integer\n          format: int64\n          description: Meeting ID (meeting number).\n        host_id:\n          type: string\n\
  \          description: User ID of the meeting host.\n        topic:\n          type: string\n          description: Meeting topic.\n        type:\n          type: integer\n          description: >-\n            Meeting type: 1 - Instant, 2 - Scheduled, 3 - Recurring no\n            fixed time, 4 - PMI meeting, 8 - Recurring fixed time.\n          enum:\n            - 1\n            - 2\n            - 3\n            - 4\n            - 8\n        start_time:\n          type: string\n          format: date-time\n          description: Scheduled start time.\n        duration:\n          type: integer\n          description: Scheduled duration in minutes.\n        timezone:\n          type: string\n          description: Timezone of the meeting.\n    MeetingObjectWithTimes:\n      allOf:\n        - $ref: '#/components/schemas/MeetingObject'\n        - type: object\n          properties:\n            start_time:\n              type: string\n              format: date-time\n              description:\
  \ Actual start time of the meeting instance.\n            end_time:\n              type: string\n              format: date-time\n              description: End time of the meeting instance.\n    ParticipantObject:\n      type: object\n      description: Participant object in webhook payloads.\n      properties:\n        user_id:\n          type: string\n          description: Participant's unique identifier within the meeting session.\n        user_name:\n          type: string\n          description: Participant display name.\n        id:\n          type: string\n          description: Zoom user ID if the participant is a registered Zoom user.\n        email:\n          type: string\n          format: email\n          description: Participant email address.\n        participant_user_id:\n          type: string\n          description: Participant user ID.\n        participant_uuid:\n          type: string\n          description: Participant UUID.\n        join_time:\n          type: string\n\
  \          format: date-time\n          description: Time the participant joined.\n        leave_time:\n          type: string\n          format: date-time\n          description: Time the participant left.\n        date_time:\n          type: string\n          format: date-time\n          description: Event timestamp.\n        registrant_id:\n          type: string\n          description: Registrant ID if applicable.\n        participant_pin_code:\n          type: integer\n          description: Participant PIN code for phone dial-in.\n    RegistrantObject:\n      type: object\n      description: Registrant object in webhook payloads.\n      properties:\n        id:\n          type: string\n          description: Registrant ID.\n        email:\n          type: string\n          format: email\n          description: Registrant email.\n        first_name:\n          type: string\n          description: Registrant first name.\n        last_name:\n          type: string\n          description:\
  \ Registrant last name.\n        address:\n          type: string\n        city:\n          type: string\n        state:\n          type: string\n        zip:\n          type: string\n        country:\n          type: string\n        phone:\n          type: string\n        industry:\n          type: string\n        org:\n          type: string\n        job_title:\n          type: string\n        status:\n          type: string\n          enum:\n            - approved\n            - pending\n            - denied\n    RecordingFileObject:\n      type: object\n      description: Recording file object in webhook payloads.\n      properties:\n        id:\n          type: string\n          description: Recording file ID.\n        meeting_id:\n          type: string\n          description: Meeting ID.\n        recording_start:\n          type: string\n          format: date-time\n          description: Recording start time.\n        recording_end:\n          type: string\n          format: date-time\n\
  \          description: Recording end time.\n        file_type:\n          type: string\n          description: Recording file type.\n          enum:\n            - MP4\n            - M4A\n            - CHAT\n            - TRANSCRIPT\n            - CSV\n            - TB\n            - CC\n            - CHAT_MESSAGE\n            - SUMMARY\n        file_size:\n          type: number\n          description: File size in bytes.\n        file_extension:\n          type: string\n          enum:\n            - MP4\n            - M4A\n            - TXT\n            - VTT\n            - CSV\n            - JSON\n        download_url:\n          type: string\n          format: uri\n          description: URL to download the file (requires download_token).\n        play_url:\n          type: string\n          format: uri\n          description: URL to play the file.\n        status:\n          type: string\n          enum:\n            - completed\n        recording_type:\n          type: string\n\
  \          enum:\n            - shared_screen_with_speaker_view(CC)\n            - shared_screen_with_speaker_view\n            - shared_screen_with_gallery_view\n            - active_speaker\n            - gallery_view\n            - shared_screen\n            - audio_only\n            - audio_transcript\n            - chat_file\n            - poll\n            - timeline\n            - closed_caption\n  messages:\n    MeetingCreated:\n      name: meeting.created\n      title: Meeting Created\n      summary: A meeting has been created.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n          - type: object\n            properties:\n              event:\n                const: meeting.created\n              payload:\n                type: object\n                properties:\n                  object:\n                    $ref: '#/components/schemas/MeetingObject'\n    MeetingUpdated:\n      name: meeting.updated\n\
  \      title: Meeting Updated\n      summary: A meeting has been updated.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n          - type: object\n            properties:\n              event:\n                const: meeting.updated\n              payload:\n                type: object\n                properties:\n                  old_object:\n                    $ref: '#/components/schemas/MeetingObject'\n                  object:\n                    $ref: '#/components/schemas/MeetingObject'\n    MeetingDeleted:\n      name: meeting.deleted\n      title: Meeting Deleted\n      summary: A meeting has been deleted.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n          - type: object\n            properties:\n              event:\n                const: meeting.deleted\n              payload:\n                type:\
  \ object\n                properties:\n                  object:\n                    $ref: '#/components/schemas/MeetingObject'\n    MeetingStarted:\n      name: meeting.started\n      title: Meeting Started\n      summary: A meeting has started.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n          - type: object\n            properties:\n              event:\n                const: meeting.started\n              payload:\n                type: object\n                properties:\n                  object:\n                    $ref: '#/components/schemas/MeetingObjectWithTimes'\n    MeetingEnded:\n      name: meeting.ended\n      title: Meeting Ended\n      summary: A meeting has ended.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n          - type: object\n            properties:\n              event:\n      \
  \          const: meeting.ended\n              payload:\n                type: object\n                properties:\n                  object:\n                    $ref: '#/components/schemas/MeetingObjectWithTimes'\n    MeetingRecovered:\n      name: meeting.recovered\n      title: Meeting Recovered from Trash\n      summary: A deleted meeting has been recovered from trash.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n          - type: object\n            properties:\n              event:\n                const: meeting.recovered\n              payload:\n                type: object\n                properties:\n                  object:\n                    $ref: '#/components/schemas/MeetingObject'\n    MeetingPermanentlyDeleted:\n      name: meeting.permanently_deleted\n      title: Meeting Permanently Deleted\n      summary: A meeting has been permanently deleted.\n      contentType: application/json\n\
  \      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n          - type: object\n            properties:\n              event:\n                const: meeting.permanently_deleted\n              payload:\n                type: object\n                properties:\n                  object:\n                    $ref: '#/components/schemas/MeetingObject'\n    ParticipantJoined:\n      name: meeting.participant_joined\n      title: Participant Joined Meeting\n      summary: A participant has joined a meeting.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n          - type: object\n            properties:\n              event:\n                const: meeting.participant_joined\n              payload:\n                type: object\n                properties:\n                  object:\n                    allOf:\n                      - $ref: '#/components/schemas/MeetingObject'\n\
  \                      - type: object\n                        properties:\n                          participant:\n                            $ref: '#/components/schemas/ParticipantObject'\n    ParticipantLeft:\n      name: meeting.participant_left\n      title: Participant Left Meeting\n      summary: A participant has left a meeting.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n          - type: object\n            properties:\n              event:\n                const: meeting.participant_left\n              payload:\n                type: object\n                properties:\n                  object:\n                    allOf:\n                      - $ref: '#/components/schemas/MeetingObject'\n                      - type: object\n                        properties:\n                          participant:\n                            allOf:\n                              - $ref: '#/components/schemas/ParticipantObject'\n\
  \                              - type: object\n                                properties:\n                                  leave_reason:\n                                    type: string\n                                    description: Reason the participant left.\n    ParticipantWaitingForHost:\n      name: meeting.participant_joined_waiting_room\n      title: Participant Waiting for Host\n      summary: A participant is waiting for the host or in the waiting room.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n          - type: object\n            properties:\n              event:\n                const: meeting.participant_joined_waiting_room\n              payload:\n                type: object\n                properties:\n                  object:\n                    allOf:\n                      - $ref: '#/components/schemas/MeetingObject'\n                      - type: object\n          \
  \              properties:\n                          participant:\n                            $ref: '#/components/schemas/ParticipantObject'\n    ParticipantAdmittedFromWaitingRoom:\n      name: meeting.participant_admitted\n      title: Participant Admitted from Waiting Room\n      summary: A participant has been admitted from the waiting room.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n          - type: object\n            properties:\n              event:\n                const: meeting.participant_admitted\n              payload:\n                type: object\n                properties:\n                  object:\n                    allOf:\n                      - $ref: '#/components/schemas/MeetingObject'\n                      - type: object\n                        properties:\n                          participant:\n                            $ref: '#/components/schemas/ParticipantObject'\n\
  \    ParticipantPutInWaitingRoom:\n      name: meeting.participant_put_in_waiting_room\n      title: Participant Put in Waiting Room\n      summary: A participant has been placed in the waiting room.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n          - type: object\n            properties:\n              event:\n                const: meeting.participant_put_in_waiting_room\n              payload:\n                type: object\n                properties:\n                  object:\n                    allOf:\n                      - $ref: '#/components/schemas/MeetingObject'\n                      - type: object\n                        properties:\n                          participant:\n                            $ref: '#/components/schemas/ParticipantObject'\n    RegistrationCreated:\n      name: meeting.registration_created\n      title: Meeting Registration Created\n      summary: A new registrant\
  \ has registered for a meeting.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n          - type: object\n            properties:\n              event:\n                const: meeting.registration_created\n              payload:\n                type: object\n                properties:\n                  object:\n                    allOf:\n                      - $ref: '#/components/schemas/MeetingObject'\n                      - type: object\n                        properties:\n                          registrant:\n                            $ref: '#/components/schemas/RegistrantObject'\n    RegistrationApproved:\n      name: meeting.registration_approved\n      title: Meeting Registration Approved\n      summary: A meeting registration has been approved.\n      contentType: application/json\n      payload:\n        allOf:\n          - $ref: '#/components/schemas/WebhookEventEnvelope'\n         \
  \ - type: object\n            properties:\n              event:\n                const: meeting.registration_approved\n              payload:\n                type: object\n                properties:\n                  object:\n                    allOf:\n                      - $ref: '#/components/schemas/MeetingObject'\n                      - type: object\n                        properties:\n                          registrant:\n                            $ref: '#/components/schemas/RegistrantObject'\n    RegistrationCancelled:\n      name: meeting.registration_cancelled\n      title: Meeting Registration Cancelled\n      \n\n# --- truncated at 32 KB (43 KB total) ---\n# Full source: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/asyncapi/zoom-meeting-webhooks-asyncapi.yml\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/asyncapi/zoom-meeting-webhooks-asyncapi.yml
spec_file: asyncapi/zoom-meeting-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/zoom/refs/heads/main/asyncapi/zoom-meeting-webhooks-asyncapi.yml
tags:
- Chat
- Collaboration
- Communications
- Meetings
- Video Conferencing
- Videos
- Webinars
- AsyncAPI
- Webhooks
- Events
version: 2.0.0
---
