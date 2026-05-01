---
api_specs:
- filename: cargosmart-shipment-tracking-openapi.yml
  format: yaml
  label: CargoSmart Container Booking API
  slug: cargosmart-container-booking-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/cargosmart/refs/heads/main/openapi/cargosmart-shipment-tracking-openapi.yml
- filename: cargosmart-shipment-tracking-openapi.yml
  format: yaml
  label: CargoSmart Shipment Tracking API
  slug: cargosmart-shipment-tracking-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/cargosmart/refs/heads/main/openapi/cargosmart-shipment-tracking-openapi.yml
- filename: cargosmart-shipment-tracking-openapi.yml
  format: yaml
  label: CargoSmart Vessel Schedule API
  slug: cargosmart-vessel-schedule-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/cargosmart/refs/heads/main/openapi/cargosmart-shipment-tracking-openapi.yml
- filename: cargosmart-shipment-tracking-openapi.yml
  format: yaml
  label: CargoSmart Shipping Documentation API
  slug: cargosmart-shipping-documents-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/cargosmart/refs/heads/main/openapi/cargosmart-shipment-tracking-openapi.yml
channels:
- description: Published when a container tracking event occurs (gate in/out, load, discharge, arrival, departure).
  name: container.event
  operation: subscribe
  operation_id: onContainerEvent
  summary: Container tracking event
- description: Published when a shipment reaches a key milestone.
  name: shipment.milestone
  operation: subscribe
  operation_id: onShipmentMilestone
  summary: Shipment milestone reached
- description: Published when a vessel arrives at a port.
  name: vessel.arrival
  operation: subscribe
  operation_id: onVesselArrival
  summary: Vessel arrived at port
- description: Published when a vessel departs from a port.
  name: vessel.departure
  operation: subscribe
  operation_id: onVesselDeparture
  summary: Vessel departed from port
- description: Published when a container booking status changes.
  name: booking.status
  operation: subscribe
  operation_id: onBookingStatusChanged
  summary: Booking status changed
- description: Published when the ETA for a container/vessel is updated.
  name: eta.update
  operation: subscribe
  operation_id: onEtaUpdated
  summary: ETA updated
description: The CargoSmart Shipment Events API delivers real-time event notifications for container movements, shipment milestones, and vessel arrivals/departures via webhooks or server-sent events. Subscribe to tracking events for automated supply chain visibility and exception management.
layout: asyncapi
messages:
- description: ''
  name: ContainerEventMessage
  summary: Container tracking event notification
  title: Container Event
- description: ''
  name: ShipmentMilestoneMessage
  summary: ''
  title: Shipment Milestone
- description: ''
  name: VesselArrivalMessage
  summary: ''
  title: Vessel Arrival
- description: ''
  name: VesselDepartureMessage
  summary: ''
  title: Vessel Departure
- description: ''
  name: BookingStatusMessage
  summary: ''
  title: Booking Status Changed
- description: ''
  name: EtaUpdateMessage
  summary: ''
  title: ETA Updated
name: CargoSmart Shipment Events API
provider_name: CargoSmart
provider_slug: cargosmart
servers:
- description: CargoSmart Event Delivery endpoint
  name: production
  protocol: https
  url: https://events.cargosmart.com
slug: cargosmart-events-asyncapi
source_filename: cargosmart-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: CargoSmart Shipment Events API\n  description: >-\n    The CargoSmart Shipment Events API delivers real-time event notifications for\n    container movements, shipment milestones, and vessel arrivals/departures via\n    webhooks or server-sent events. Subscribe to tracking events for automated\n    supply chain visibility and exception management.\n  version: 1.0.0\n  contact:\n    name: CargoSmart\n    url: https://www.cargosmart.com/\n\nservers:\n  production:\n    url: https://events.cargosmart.com\n    protocol: https\n    description: CargoSmart Event Delivery endpoint\n\nchannels:\n  container.event:\n    description: Published when a container tracking event occurs (gate in/out, load, discharge, arrival, departure).\n    subscribe:\n      operationId: onContainerEvent\n      summary: Container tracking event\n      description: Receive real-time notifications for container movement events.\n      tags:\n        - name: Containers\n  \
  \    message:\n        $ref: '#/components/messages/ContainerEventMessage'\n\n  shipment.milestone:\n    description: Published when a shipment reaches a key milestone.\n    subscribe:\n      operationId: onShipmentMilestone\n      summary: Shipment milestone reached\n      description: Receive notifications for important shipment milestones (departure, arrival, delivery).\n      tags:\n        - name: Shipments\n      message:\n        $ref: '#/components/messages/ShipmentMilestoneMessage'\n\n  vessel.arrival:\n    description: Published when a vessel arrives at a port.\n    subscribe:\n      operationId: onVesselArrival\n      summary: Vessel arrived at port\n      description: Receive notifications when a tracked vessel arrives at a port.\n      tags:\n        - name: Vessels\n      message:\n        $ref: '#/components/messages/VesselArrivalMessage'\n\n  vessel.departure:\n    description: Published when a vessel departs from a port.\n    subscribe:\n      operationId: onVesselDeparture\n\
  \      summary: Vessel departed from port\n      description: Receive notifications when a tracked vessel departs from a port.\n      tags:\n        - name: Vessels\n      message:\n        $ref: '#/components/messages/VesselDepartureMessage'\n\n  booking.status:\n    description: Published when a container booking status changes.\n    subscribe:\n      operationId: onBookingStatusChanged\n      summary: Booking status changed\n      description: Receive notifications when a booking is confirmed, amended, or cancelled.\n      tags:\n        - name: Bookings\n      message:\n        $ref: '#/components/messages/BookingStatusMessage'\n\n  eta.update:\n    description: Published when the ETA for a container/vessel is updated.\n    subscribe:\n      operationId: onEtaUpdated\n      summary: ETA updated\n      description: Receive notifications when the estimated time of arrival changes.\n      tags:\n        - name: Vessels\n      message:\n        $ref: '#/components/messages/EtaUpdateMessage'\n\
  \ncomponents:\n  messages:\n    ContainerEventMessage:\n      name: ContainerEventMessage\n      title: Container Event\n      summary: Container tracking event notification\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          x-cargosmart-signature:\n            type: string\n            description: HMAC-SHA256 signature for event authenticity\n          x-cargosmart-event-id:\n            type: string\n      payload:\n        $ref: '#/components/schemas/ContainerEventPayload'\n\n    ShipmentMilestoneMessage:\n      name: ShipmentMilestoneMessage\n      title: Shipment Milestone\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ShipmentMilestonePayload'\n\n    VesselArrivalMessage:\n      name: VesselArrivalMessage\n      title: Vessel Arrival\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/VesselEventPayload'\n\n    VesselDepartureMessage:\n      name:\
  \ VesselDepartureMessage\n      title: Vessel Departure\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/VesselEventPayload'\n\n    BookingStatusMessage:\n      name: BookingStatusMessage\n      title: Booking Status Changed\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BookingStatusPayload'\n\n    EtaUpdateMessage:\n      name: EtaUpdateMessage\n      title: ETA Updated\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EtaUpdatePayload'\n\n  schemas:\n    EventEnvelope:\n      type: object\n      required: [eventId, eventType, timestamp]\n      properties:\n        eventId:\n          type: string\n          description: Unique event identifier\n        eventType:\n          type: string\n        timestamp:\n          type: string\n          format: date-time\n\n    ContainerEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/EventEnvelope'\n    \
  \    - type: object\n          properties:\n            containerId:\n              type: string\n              description: Container number\n            eventType:\n              type: string\n              enum: [GateIn, GateOut, Load, Discharge, Departure, Arrival, Customs, Delivery, EmptyReturn]\n            location:\n              type: object\n              properties:\n                locode:\n                  type: string\n                portName:\n                  type: string\n                terminalName:\n                  type: string\n            vesselName:\n              type: string\n            voyageNumber:\n              type: string\n            carrierCode:\n              type: string\n            isActual:\n              type: boolean\n\n    ShipmentMilestonePayload:\n      allOf:\n        - $ref: '#/components/schemas/EventEnvelope'\n        - type: object\n          properties:\n            billOfLadingNumber:\n              type: string\n            bookingNumber:\n\
  \              type: string\n            milestone:\n              type: string\n              enum: [Booked, VGMSubmitted, Loaded, Departed, InTransit, Arrived, CustomsCleared, Delivered]\n            containers:\n              type: array\n              items:\n                type: string\n            originPort:\n              type: string\n            destinationPort:\n              type: string\n\n    VesselEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/EventEnvelope'\n        - type: object\n          properties:\n            vesselIMO:\n              type: string\n            vesselName:\n              type: string\n            voyageNumber:\n              type: string\n            carrierCode:\n              type: string\n            portLocode:\n              type: string\n            portName:\n              type: string\n            terminalName:\n              type: string\n            eventTime:\n              type: string\n              format: date-time\n\
  \n    BookingStatusPayload:\n      allOf:\n        - $ref: '#/components/schemas/EventEnvelope'\n        - type: object\n          properties:\n            bookingId:\n              type: string\n            bookingNumber:\n              type: string\n            carrierCode:\n              type: string\n            newStatus:\n              type: string\n              enum: [Submitted, Confirmed, Amended, Cancelled]\n            previousStatus:\n              type: string\n            confirmedVessel:\n              type: string\n            confirmedVoyage:\n              type: string\n\n    EtaUpdatePayload:\n      allOf:\n        - $ref: '#/components/schemas/EventEnvelope'\n        - type: object\n          properties:\n            containerId:\n              type: string\n            vesselIMO:\n              type: string\n            vesselName:\n              type: string\n            portLocode:\n              type: string\n            portName:\n              type: string\n \
  \           previousEta:\n              type: string\n              format: date-time\n            updatedEta:\n              type: string\n              format: date-time\n            delayHours:\n              type: integer\n              description: Positive = delayed, negative = early\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cargosmart/refs/heads/main/asyncapi/cargosmart-events-asyncapi.yml
spec_file: asyncapi/cargosmart-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/cargosmart/refs/heads/main/asyncapi/cargosmart-events-asyncapi.yml
tags:
- Booking
- Container
- Documentation
- GSBN
- IQAX
- Logistics
- Maritime
- Ocean Freight
- Schedule
- Shipping
- Supply Chain
- Tracking
- Visibility
- Vessel
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
