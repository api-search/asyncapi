---
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
