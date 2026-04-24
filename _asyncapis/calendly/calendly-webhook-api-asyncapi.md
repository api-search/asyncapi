---
channels:
- description: Channel for invitee.created events. Triggered when a new invitee schedules a meeting through Calendly. Also triggered as part of a reschedule operation (the new booking). The payload includes the full invitee resource with event details, contact information, and answers to custom questions.
  name: /webhook/invitee-created
  operation: publish
  operation_id: onInviteeCreated
  summary: Invitee created event
- description: Channel for invitee.canceled events. Triggered when an existing scheduled event is canceled by either the host or the invitee. Also triggered as part of a reschedule operation (the old booking being canceled). The payload includes cancellation details and the reason if provided.
  name: /webhook/invitee-canceled
  operation: publish
  operation_id: onInviteeCanceled
  summary: Invitee canceled event
- description: Channel for routing_form_submission.created events. Triggered when someone submits a routing form, regardless of whether they subsequently book a meeting. The payload includes the form submission with all questions and answers.
  name: /webhook/routing-form-submission-created
  operation: publish
  operation_id: onRoutingFormSubmissionCreated
  summary: Routing form submission created event
description: The Calendly Webhook API enables developers to receive real-time notifications when scheduling events occur in Calendly. By creating webhook subscriptions, applications can automatically receive data whenever invitees schedule, cancel, or reschedule meetings, or when routing form submissions are created. This eliminates the need for polling the API and allows for event-driven integrations that respond immediately to changes in scheduling activity. Webhook payloads are signed for verification and delivered via HTTP POST to the configured callback URL.
layout: asyncapi
messages:
- description: ''
  name: InviteeCreatedEvent
  summary: Delivered when a new invitee schedules a meeting through Calendly.
  title: Invitee Created
- description: ''
  name: InviteeCanceledEvent
  summary: Delivered when an invitee or host cancels a scheduled meeting.
  title: Invitee Canceled
- description: ''
  name: RoutingFormSubmissionCreatedEvent
  summary: Delivered when someone submits a routing form, whether or not they subsequently book a meeting.
  title: Routing Form Submission Created
name: Calendly Webhook Events
provider_name: Calendly
provider_slug: calendly
servers:
- description: Calendly production server. Webhook subscriptions are managed via the REST API, and payloads are delivered to the subscriber-configured callback URL.
  name: production
  protocol: https
  url: https://api.calendly.com
slug: calendly-webhook-api-asyncapi
spec_file: asyncapi/calendly-webhook-api-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/calendly/refs/heads/main/asyncapi/calendly-webhook-api-asyncapi.yml
tags:
- Appointments
- Automation
- Booking
- Calendars
- Meetings
- Scheduling
- AsyncAPI
- Webhooks
- Events
version: 2.0.0
---
