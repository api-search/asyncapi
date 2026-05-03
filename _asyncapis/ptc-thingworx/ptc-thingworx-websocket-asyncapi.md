---
api_specs:
- filename: ptc-thingworx-rest-openapi.yml
  format: yaml
  label: PTC ThingWorx REST API
  slug: thingworx-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ptc-thingworx/refs/heads/main/openapi/ptc-thingworx-rest-openapi.yml
- filename: ptc-thingworx-websocket-asyncapi.yml
  format: yaml
  label: PTC ThingWorx WebSocket/AlwaysOn API
  slug: thingworx-websocket-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/ptc-thingworx/refs/heads/main/asyncapi/ptc-thingworx-websocket-asyncapi.yml
channels:
- description: Channel for receiving real-time property value updates from connected things
  name: thing/property-update
  operation: subscribe
  operation_id: onPropertyUpdate
  summary: Real-time property value update
- description: Channel for receiving real-time event notifications from things
  name: thing/event-fired
  operation: subscribe
  operation_id: onEventFired
  summary: Thing event notification
- description: Channel for receiving alert notifications from things
  name: thing/alert
  operation: subscribe
  operation_id: onAlert
  summary: Thing alert notification
- description: Channel for device connection lifecycle notifications
  name: device/connect
  operation: subscribe
  operation_id: onDeviceConnect
  summary: Device connected event
- description: Channel for device disconnection lifecycle notifications
  name: device/disconnect
  operation: subscribe
  operation_id: onDeviceDisconnect
  summary: Device disconnected event
description: PTC ThingWorx AlwaysOn WebSocket API enables persistent bidirectional connections for industrial edge devices and remote assets. Supports real-time telemetry streaming, command and control, event notifications, and device lifecycle management over WebSocket transport using the ThingWorx AlwaysOn protocol.
layout: asyncapi
messages:
- description: ''
  name: PropertyUpdateMessage
  summary: ''
  title: Property Value Update
- description: ''
  name: EventFiredMessage
  summary: ''
  title: Thing Event Fired
- description: ''
  name: AlertMessage
  summary: ''
  title: Thing Alert
- description: ''
  name: DeviceConnectMessage
  summary: ''
  title: Device Connected
- description: ''
  name: DeviceDisconnectMessage
  summary: ''
  title: Device Disconnected
name: PTC ThingWorx AlwaysOn WebSocket API
provider_name: ptc-thingworx
provider_slug: ptc-thingworx
servers:
- description: ThingWorx WebSocket endpoint
  name: thingworx-production
  protocol: wss
  url: wss://{host}/Thingworx/WS
slug: ptc-thingworx-websocket-asyncapi
source_filename: ptc-thingworx-websocket-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: PTC ThingWorx AlwaysOn WebSocket API\n  version: 9.5.0\n  description: >-\n    PTC ThingWorx AlwaysOn WebSocket API enables persistent bidirectional connections\n    for industrial edge devices and remote assets. Supports real-time telemetry\n    streaming, command and control, event notifications, and device lifecycle\n    management over WebSocket transport using the ThingWorx AlwaysOn protocol.\n  contact:\n    name: PTC Support\n    url: https://www.ptc.com/en/support\n  license:\n    name: PTC Software License\n    url: https://www.ptc.com/en/legal-agreements\n\nservers:\n  thingworx-production:\n    url: wss://{host}/Thingworx/WS\n    protocol: wss\n    description: ThingWorx WebSocket endpoint\n    variables:\n      host:\n        default: thingworx.example.com\n\ndefaultContentType: application/json\n\nchannels:\n  thing/property-update:\n    description: Channel for receiving real-time property value updates from connected things\n\
  \    subscribe:\n      operationId: onPropertyUpdate\n      summary: Real-time property value update\n      description: >-\n        Published when a thing property value changes and property change notification\n        is enabled. Delivers the new value with timestamp and quality.\n      tags:\n        - name: Properties\n      message:\n        $ref: '#/components/messages/PropertyUpdateMessage'\n\n  thing/event-fired:\n    description: Channel for receiving real-time event notifications from things\n    subscribe:\n      operationId: onEventFired\n      summary: Thing event notification\n      description: >-\n        Published when a thing fires an event (e.g., alert threshold crossed,\n        state change, fault detected). Contains event name and associated data.\n      tags:\n        - name: Events\n      message:\n        $ref: '#/components/messages/EventFiredMessage'\n\n  thing/alert:\n    description: Channel for receiving alert notifications from things\n    subscribe:\n \
  \     operationId: onAlert\n      summary: Thing alert notification\n      description: >-\n        Published when a thing triggers an alert condition based on a property\n        value crossing a configured threshold.\n      tags:\n        - name: Alerts\n      message:\n        $ref: '#/components/messages/AlertMessage'\n\n  device/connect:\n    description: Channel for device connection lifecycle notifications\n    subscribe:\n      operationId: onDeviceConnect\n      summary: Device connected event\n      description: Published when an edge device establishes an AlwaysOn WebSocket connection.\n      tags:\n        - name: Devices\n      message:\n        $ref: '#/components/messages/DeviceConnectMessage'\n\n  device/disconnect:\n    description: Channel for device disconnection lifecycle notifications\n    subscribe:\n      operationId: onDeviceDisconnect\n      summary: Device disconnected event\n      description: Published when an edge device connection is terminated.\n      tags:\n\
  \        - name: Devices\n      message:\n        $ref: '#/components/messages/DeviceDisconnectMessage'\n\ncomponents:\n  messages:\n    PropertyUpdateMessage:\n      name: PropertyUpdate\n      title: Property Value Update\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PropertyUpdatePayload'\n\n    EventFiredMessage:\n      name: EventFired\n      title: Thing Event Fired\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventFiredPayload'\n\n    AlertMessage:\n      name: Alert\n      title: Thing Alert\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AlertPayload'\n\n    DeviceConnectMessage:\n      name: DeviceConnect\n      title: Device Connected\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DeviceConnectionPayload'\n\n    DeviceDisconnectMessage:\n      name: DeviceDisconnect\n      title: Device Disconnected\n  \
  \    contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DeviceConnectionPayload'\n\n  schemas:\n    PropertyUpdatePayload:\n      type: object\n      required:\n        - thingName\n        - propertyName\n        - value\n        - timestamp\n      properties:\n        thingName:\n          type: string\n          description: Name of the thing that reported the update\n        propertyName:\n          type: string\n          description: Name of the updated property\n        value:\n          description: New property value\n        timestamp:\n          type: integer\n          format: int64\n          description: Value timestamp in epoch milliseconds (UTC)\n        quality:\n          type: string\n          description: Data quality string (GOOD, BAD, UNCERTAIN)\n          enum: [GOOD, BAD, UNCERTAIN]\n\n    EventFiredPayload:\n      type: object\n      required:\n        - thingName\n        - eventName\n        - timestamp\n      properties:\n  \
  \      thingName:\n          type: string\n        eventName:\n          type: string\n        timestamp:\n          type: integer\n          format: int64\n        eventData:\n          type: object\n          additionalProperties: true\n          description: Event-specific data fields based on data shape\n\n    AlertPayload:\n      type: object\n      required:\n        - thingName\n        - propertyName\n        - alertName\n        - alertType\n        - timestamp\n      properties:\n        thingName:\n          type: string\n        propertyName:\n          type: string\n        alertName:\n          type: string\n        alertType:\n          type: string\n          enum: [Above, Below, Equal, NotEqual, AboveOrEqual, BelowOrEqual]\n        isAcknowledged:\n          type: boolean\n        isCleared:\n          type: boolean\n        timestamp:\n          type: integer\n          format: int64\n        value:\n          description: Property value when alert triggered\n       \
  \ threshold:\n          description: Configured threshold value\n\n    DeviceConnectionPayload:\n      type: object\n      required:\n        - thingName\n        - timestamp\n      properties:\n        thingName:\n          type: string\n          description: Name of the connected/disconnected thing\n        deviceId:\n          type: string\n          description: Physical device identifier\n        timestamp:\n          type: integer\n          format: int64\n        ipAddress:\n          type: string\n          nullable: true\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/ptc-thingworx/refs/heads/main/asyncapi/ptc-thingworx-websocket-asyncapi.yml
spec_file: asyncapi/ptc-thingworx-websocket-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/ptc-thingworx/refs/heads/main/asyncapi/ptc-thingworx-websocket-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: 9.5.0
---
