---
api_specs:
- filename: project44-tracking-openapi.yml
  format: yaml
  label: project44 API v4
  slug: project44-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/project44/refs/heads/main/openapi/project44-tracking-openapi.yml
channels:
- description: Event published when a shipment status changes
  name: shipment/status-updated
  operation: subscribe
  operation_id: onShipmentStatusUpdated
  summary: Shipment status updated event
- description: Event published when a shipment GPS position is updated
  name: shipment/position-updated
  operation: subscribe
  operation_id: onShipmentPositionUpdated
  summary: Shipment position updated event
- description: Event published when the predicted delivery ETA changes
  name: shipment/eta-changed
  operation: subscribe
  operation_id: onShipmentEtaChanged
  summary: Shipment ETA changed event
- description: Event published when a shipment exception is detected
  name: shipment/exception
  operation: subscribe
  operation_id: onShipmentException
  summary: Shipment exception event
- description: Event published when a shipment delivery is confirmed
  name: shipment/completed
  operation: subscribe
  operation_id: onShipmentCompleted
  summary: Shipment completed (delivered) event
description: project44 publishes real-time freight visibility events via webhooks. Events include shipment status updates, position changes, ETA revisions, and exception alerts across TL, LTL, ocean, air, and parcel modes.
layout: asyncapi
messages:
- description: ''
  name: ShipmentStatusUpdatedEvent
  summary: ''
  title: Shipment Status Updated
- description: ''
  name: ShipmentPositionUpdatedEvent
  summary: ''
  title: Shipment Position Updated
- description: ''
  name: ShipmentEtaChangedEvent
  summary: ''
  title: Shipment ETA Changed
- description: ''
  name: ShipmentExceptionEvent
  summary: ''
  title: Shipment Exception Detected
- description: ''
  name: ShipmentCompletedEvent
  summary: ''
  title: Shipment Delivered
name: project44 Shipment Events API
provider_name: project44
provider_slug: project44
servers:
- description: Customer-provided HTTPS endpoint to receive project44 webhook events. Register via the project44 Webhooks API.
  name: project44-webhook
  protocol: https
  url: https://your-endpoint.example.com/webhooks/project44
slug: project44-shipment-events-asyncapi
source_filename: project44-shipment-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: project44 Shipment Events API\n  version: 2.0.0\n  description: >-\n    project44 publishes real-time freight visibility events via webhooks.\n    Events include shipment status updates, position changes, ETA revisions,\n    and exception alerts across TL, LTL, ocean, air, and parcel modes.\n  contact:\n    name: project44 Support\n    url: https://support.project44.com\n  license:\n    name: project44 Terms of Service\n    url: https://www.project44.com/legal/\n\nservers:\n  project44-webhook:\n    url: https://your-endpoint.example.com/webhooks/project44\n    protocol: https\n    description: >-\n      Customer-provided HTTPS endpoint to receive project44 webhook events.\n      Register via the project44 Webhooks API.\n\ndefaultContentType: application/json\n\nchannels:\n  shipment/status-updated:\n    description: Event published when a shipment status changes\n    subscribe:\n      operationId: onShipmentStatusUpdated\n      summary: Shipment\
  \ status updated event\n      description: >-\n        Triggered when a new status update is received for a tracked shipment\n        from carrier EDI, carrier API, or telematics providers.\n      tags:\n        - name: Shipments\n      message:\n        $ref: '#/components/messages/ShipmentStatusUpdatedEvent'\n\n  shipment/position-updated:\n    description: Event published when a shipment GPS position is updated\n    subscribe:\n      operationId: onShipmentPositionUpdated\n      summary: Shipment position updated event\n      description: Triggered periodically when a new GPS position is received from a telematics provider.\n      tags:\n        - name: Tracking\n      message:\n        $ref: '#/components/messages/ShipmentPositionUpdatedEvent'\n\n  shipment/eta-changed:\n    description: Event published when the predicted delivery ETA changes\n    subscribe:\n      operationId: onShipmentEtaChanged\n      summary: Shipment ETA changed event\n      description: >-\n        Triggered\
  \ when the machine-learning ETA prediction changes significantly\n        (typically by more than 30 minutes from previous prediction).\n      tags:\n        - name: ETA\n      message:\n        $ref: '#/components/messages/ShipmentEtaChangedEvent'\n\n  shipment/exception:\n    description: Event published when a shipment exception is detected\n    subscribe:\n      operationId: onShipmentException\n      summary: Shipment exception event\n      description: >-\n        Triggered when a delay, missed stop, delivery attempt failure, or other\n        exception condition is detected on the shipment.\n      tags:\n        - name: Shipments\n      message:\n        $ref: '#/components/messages/ShipmentExceptionEvent'\n\n  shipment/completed:\n    description: Event published when a shipment delivery is confirmed\n    subscribe:\n      operationId: onShipmentCompleted\n      summary: Shipment completed (delivered) event\n      description: Triggered when the shipment is confirmed as delivered.\n\
  \      tags:\n        - name: Shipments\n      message:\n        $ref: '#/components/messages/ShipmentCompletedEvent'\n\ncomponents:\n  messages:\n    ShipmentStatusUpdatedEvent:\n      name: ShipmentStatusUpdated\n      title: Shipment Status Updated\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          x-p44-event-id:\n            type: string\n            format: uuid\n          x-p44-event-type:\n            type: string\n            const: shipment.status-updated\n          x-p44-signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification\n      payload:\n        $ref: '#/components/schemas/ShipmentStatusUpdatedPayload'\n\n    ShipmentPositionUpdatedEvent:\n      name: ShipmentPositionUpdated\n      title: Shipment Position Updated\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ShipmentPositionUpdatedPayload'\n\n    ShipmentEtaChangedEvent:\n\
  \      name: ShipmentEtaChanged\n      title: Shipment ETA Changed\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ShipmentEtaChangedPayload'\n\n    ShipmentExceptionEvent:\n      name: ShipmentException\n      title: Shipment Exception Detected\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ShipmentExceptionPayload'\n\n    ShipmentCompletedEvent:\n      name: ShipmentCompleted\n      title: Shipment Delivered\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ShipmentCompletedPayload'\n\n  schemas:\n    ShipmentStatusUpdatedPayload:\n      type: object\n      required:\n        - eventId\n        - eventTimestamp\n        - shipmentId\n        - statusCode\n      properties:\n        eventId:\n          type: string\n          format: uuid\n        eventTimestamp:\n          type: string\n          format: date-time\n        shipmentId:\n          type: string\n\
  \          format: uuid\n        masterShipmentId:\n          type: string\n        mode:\n          type: string\n          enum: [TL, LTL, OCEAN, AIR, RAIL, PARCEL, DRAY]\n        carrierCode:\n          type: string\n        proNumber:\n          type: string\n        statusCode:\n          type: string\n        statusDescription:\n          type: string\n        statusTimestamp:\n          type: string\n          format: date-time\n        city:\n          type: string\n        state:\n          type: string\n        country:\n          type: string\n          maxLength: 3\n        source:\n          type: string\n          enum: [CARRIER_EDI, CARRIER_API, TELEMATICS, MANUAL]\n\n    ShipmentPositionUpdatedPayload:\n      type: object\n      required:\n        - eventId\n        - eventTimestamp\n        - shipmentId\n        - position\n      properties:\n        eventId:\n          type: string\n          format: uuid\n        eventTimestamp:\n          type: string\n          format:\
  \ date-time\n        shipmentId:\n          type: string\n          format: uuid\n        masterShipmentId:\n          type: string\n        position:\n          type: object\n          properties:\n            timestamp:\n              type: string\n              format: date-time\n            latitude:\n              type: number\n              format: double\n            longitude:\n              type: number\n              format: double\n            heading:\n              type: number\n              format: double\n              nullable: true\n            speed:\n              type: number\n              format: double\n              nullable: true\n            speedUnit:\n              type: string\n              enum: [MPH, KPH]\n\n    ShipmentEtaChangedPayload:\n      type: object\n      required:\n        - eventId\n        - eventTimestamp\n        - shipmentId\n        - previousEta\n        - newEta\n      properties:\n        eventId:\n          type: string\n          format:\
  \ uuid\n        eventTimestamp:\n          type: string\n          format: date-time\n        shipmentId:\n          type: string\n          format: uuid\n        masterShipmentId:\n          type: string\n        previousEta:\n          type: string\n          format: date-time\n        newEta:\n          type: string\n          format: date-time\n        deltaMinutes:\n          type: integer\n          description: Change in ETA in minutes (positive = later, negative = earlier)\n        predictedOnTime:\n          type: boolean\n\n    ShipmentExceptionPayload:\n      type: object\n      required:\n        - eventId\n        - eventTimestamp\n        - shipmentId\n        - exceptionCode\n      properties:\n        eventId:\n          type: string\n          format: uuid\n        eventTimestamp:\n          type: string\n          format: date-time\n        shipmentId:\n          type: string\n          format: uuid\n        masterShipmentId:\n          type: string\n        exceptionCode:\n\
  \          type: string\n        description:\n          type: string\n        severity:\n          type: string\n          enum: [LOW, MEDIUM, HIGH, CRITICAL]\n        estimatedImpactMinutes:\n          type: integer\n          nullable: true\n\n    ShipmentCompletedPayload:\n      type: object\n      required:\n        - eventId\n        - eventTimestamp\n        - shipmentId\n        - deliveryDatetime\n      properties:\n        eventId:\n          type: string\n          format: uuid\n        eventTimestamp:\n          type: string\n          format: date-time\n        shipmentId:\n          type: string\n          format: uuid\n        masterShipmentId:\n          type: string\n        deliveryDatetime:\n          type: string\n          format: date-time\n        signedBy:\n          type: string\n          nullable: true\n        podAvailable:\n          type: boolean\n          description: Whether proof-of-delivery document is available\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/project44/refs/heads/main/asyncapi/project44-shipment-events-asyncapi.yml
spec_file: asyncapi/project44-shipment-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/project44/refs/heads/main/asyncapi/project44-shipment-events-asyncapi.yml
tags:
- Logistics
- Supply Chain Visibility
- Tracking
- Freight
- Multi-modal
- AsyncAPI
- Webhooks
- Events
version: 2.0.0
---
