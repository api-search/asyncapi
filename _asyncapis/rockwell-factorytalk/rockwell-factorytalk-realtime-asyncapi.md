---
api_specs:
- filename: rockwell-factorytalk-optix-openapi.yml
  format: yaml
  label: Rockwell FactoryTalk Optix REST API
  slug: factorytalk-optix-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rockwell-factorytalk/refs/heads/main/openapi/rockwell-factorytalk-optix-openapi.yml
- filename: rockwell-factorytalk-realtime-asyncapi.yml
  format: yaml
  label: Rockwell FactoryTalk Hub API
  slug: factorytalk-hub-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/rockwell-factorytalk/refs/heads/main/asyncapi/rockwell-factorytalk-realtime-asyncapi.yml
channels:
- description: Event published when a monitored tag value changes beyond deadband
  name: tag/value-changed
  operation: subscribe
  operation_id: onTagValueChanged
  summary: Tag value change notification
- description: Event published when an alarm condition is triggered
  name: alarm/activated
  operation: subscribe
  operation_id: onAlarmActivated
  summary: Alarm activated notification
- description: Event published when an alarm is acknowledged by an operator
  name: alarm/acknowledged
  operation: subscribe
  operation_id: onAlarmAcknowledged
  summary: Alarm acknowledged notification
- description: Event published when a connected device connectivity status changes
  name: device/status-changed
  operation: subscribe
  operation_id: onDeviceStatusChanged
  summary: Device connectivity status change
description: Rockwell FactoryTalk Hub provides real-time industrial event streaming via webhooks and subscriptions. Events include tag value changes, alarm activations, and device connectivity notifications for connected FactoryTalk applications.
layout: asyncapi
messages:
- description: ''
  name: TagValueChangedEvent
  summary: ''
  title: Tag Value Changed
- description: ''
  name: AlarmActivatedEvent
  summary: ''
  title: Alarm Activated
- description: ''
  name: AlarmAcknowledgedEvent
  summary: ''
  title: Alarm Acknowledged
- description: ''
  name: DeviceStatusChangedEvent
  summary: ''
  title: Device Status Changed
name: Rockwell FactoryTalk Hub Real-Time Events API
provider_name: rockwell-factorytalk
provider_slug: rockwell-factorytalk
servers:
- description: FactoryTalk Hub event stream endpoint
  name: factorytalk-hub
  protocol: https
  url: https://ftconnect.rockwellautomation.com/events
slug: rockwell-factorytalk-realtime-asyncapi
source_filename: rockwell-factorytalk-realtime-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Rockwell FactoryTalk Hub Real-Time Events API\n  version: 1.0.0\n  description: >-\n    Rockwell FactoryTalk Hub provides real-time industrial event streaming via\n    webhooks and subscriptions. Events include tag value changes, alarm activations,\n    and device connectivity notifications for connected FactoryTalk applications.\n  contact:\n    name: Rockwell Automation Support\n    url: https://www.rockwellautomation.com/en-us/support/\n  license:\n    name: Rockwell Automation Software License\n    url: https://www.rockwellautomation.com/en-us/company/about-us/legal-notices/\n\nservers:\n  factorytalk-hub:\n    url: https://ftconnect.rockwellautomation.com/events\n    protocol: https\n    description: FactoryTalk Hub event stream endpoint\n\ndefaultContentType: application/json\n\nchannels:\n  tag/value-changed:\n    description: Event published when a monitored tag value changes beyond deadband\n    subscribe:\n      operationId: onTagValueChanged\n\
  \      summary: Tag value change notification\n      description: >-\n        Published when a subscribed tag value changes. Subscription filters\n        control which tags generate events and deadband settings.\n      tags:\n        - name: Tags\n      message:\n        $ref: '#/components/messages/TagValueChangedEvent'\n\n  alarm/activated:\n    description: Event published when an alarm condition is triggered\n    subscribe:\n      operationId: onAlarmActivated\n      summary: Alarm activated notification\n      description: >-\n        Published when a tag value crosses a configured alarm setpoint,\n        triggering an alarm condition.\n      tags:\n        - name: Alarms\n      message:\n        $ref: '#/components/messages/AlarmActivatedEvent'\n\n  alarm/acknowledged:\n    description: Event published when an alarm is acknowledged by an operator\n    subscribe:\n      operationId: onAlarmAcknowledged\n      summary: Alarm acknowledged notification\n      description: Published\
  \ when an operator acknowledges an active alarm.\n      tags:\n        - name: Alarms\n      message:\n        $ref: '#/components/messages/AlarmAcknowledgedEvent'\n\n  device/status-changed:\n    description: Event published when a connected device connectivity status changes\n    subscribe:\n      operationId: onDeviceStatusChanged\n      summary: Device connectivity status change\n      description: Published when an industrial device goes online or offline.\n      tags:\n        - name: Devices\n      message:\n        $ref: '#/components/messages/DeviceStatusChangedEvent'\n\ncomponents:\n  messages:\n    TagValueChangedEvent:\n      name: TagValueChanged\n      title: Tag Value Changed\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          x-ft-event-id:\n            type: string\n            format: uuid\n          x-ft-event-type:\n            type: string\n            const: tag.value-changed\n      payload:\n        $ref: '#/components/schemas/TagValueChangedPayload'\n\
  \n    AlarmActivatedEvent:\n      name: AlarmActivated\n      title: Alarm Activated\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AlarmEventPayload'\n\n    AlarmAcknowledgedEvent:\n      name: AlarmAcknowledged\n      title: Alarm Acknowledged\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AlarmAcknowledgedPayload'\n\n    DeviceStatusChangedEvent:\n      name: DeviceStatusChanged\n      title: Device Status Changed\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DeviceStatusChangedPayload'\n\n  schemas:\n    TagValueChangedPayload:\n      type: object\n      required:\n        - eventId\n        - eventTimestamp\n        - tagName\n        - newValue\n      properties:\n        eventId:\n          type: string\n          format: uuid\n        eventTimestamp:\n          type: string\n          format: date-time\n        tagName:\n          type: string\n    \
  \      description: Fully qualified tag name\n        newValue:\n          description: New tag value\n        previousValue:\n          description: Previous tag value\n        quality:\n          type: string\n          enum: [GOOD, BAD, UNCERTAIN, COMM_FAILURE]\n        engineeringUnit:\n          type: string\n          nullable: true\n        deviceName:\n          type: string\n          nullable: true\n\n    AlarmEventPayload:\n      type: object\n      required:\n        - eventId\n        - eventTimestamp\n        - alarmId\n        - tagName\n        - alarmName\n        - severity\n      properties:\n        eventId:\n          type: string\n          format: uuid\n        eventTimestamp:\n          type: string\n          format: date-time\n        alarmId:\n          type: string\n        tagName:\n          type: string\n        alarmName:\n          type: string\n        description:\n          type: string\n        severity:\n          type: string\n          enum: [LOW,\
  \ MEDIUM, HIGH, CRITICAL]\n        triggerValue:\n          description: Tag value that triggered the alarm\n        setpoint:\n          description: Configured alarm setpoint\n        activationTime:\n          type: string\n          format: date-time\n\n    AlarmAcknowledgedPayload:\n      type: object\n      required:\n        - eventId\n        - eventTimestamp\n        - alarmId\n        - acknowledgedBy\n      properties:\n        eventId:\n          type: string\n          format: uuid\n        eventTimestamp:\n          type: string\n          format: date-time\n        alarmId:\n          type: string\n        tagName:\n          type: string\n        alarmName:\n          type: string\n        acknowledgedBy:\n          type: string\n          description: Username of the operator who acknowledged the alarm\n        comment:\n          type: string\n          nullable: true\n        acknowledgmentTime:\n          type: string\n          format: date-time\n\n    DeviceStatusChangedPayload:\n\
  \      type: object\n      required:\n        - eventId\n        - eventTimestamp\n        - deviceName\n        - newStatus\n      properties:\n        eventId:\n          type: string\n          format: uuid\n        eventTimestamp:\n          type: string\n          format: date-time\n        deviceName:\n          type: string\n        deviceType:\n          type: string\n        previousStatus:\n          type: string\n          enum: [ONLINE, OFFLINE, DEGRADED, UNKNOWN]\n        newStatus:\n          type: string\n          enum: [ONLINE, OFFLINE, DEGRADED, UNKNOWN]\n        ipAddress:\n          type: string\n          nullable: true\n        location:\n          type: string\n          nullable: true\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rockwell-factorytalk/refs/heads/main/asyncapi/rockwell-factorytalk-realtime-asyncapi.yml
spec_file: asyncapi/rockwell-factorytalk-realtime-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/rockwell-factorytalk/refs/heads/main/asyncapi/rockwell-factorytalk-realtime-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
