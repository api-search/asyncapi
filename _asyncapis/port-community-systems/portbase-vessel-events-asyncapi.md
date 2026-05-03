---
api_specs:
- filename: portbase-port-community-openapi.yml
  format: yaml
  label: Portbase Port Community System API
  slug: portbase
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/port-community-systems/refs/heads/main/openapi/portbase-port-community-openapi.yml
channels:
- description: Event published when a vessel call status changes (e.g., from EXPECTED to ARRIVED)
  name: vessel-call/status-changed
  operation: subscribe
  operation_id: onVesselCallStatusChanged
  summary: Vessel call status change event
- description: Event published when a cargo manifest is accepted by Dutch Customs
  name: cargo-manifest/accepted
  operation: subscribe
  operation_id: onCargoManifestAccepted
  summary: Cargo manifest accepted event
- description: Event published when a container receives customs release
  name: container/customs-released
  operation: subscribe
  operation_id: onContainerCustomsReleased
  summary: Container customs released event
- description: Event published when a container departs the terminal gate
  name: container/gate-out
  operation: subscribe
  operation_id: onContainerGateOut
  summary: Container gate-out event
description: Portbase publishes real-time vessel call and cargo events via webhooks to connected port community members. Events notify subscribers of vessel status changes, customs release notifications, and container gate events.
layout: asyncapi
messages:
- description: ''
  name: VesselCallStatusChangedEvent
  summary: Fired when vessel call status changes
  title: Vessel Call Status Changed
- description: ''
  name: CargoManifestAcceptedEvent
  summary: Fired when a manifest is accepted by customs
  title: Cargo Manifest Accepted
- description: ''
  name: ContainerCustomsReleasedEvent
  summary: Fired when a container is customs released
  title: Container Customs Released
- description: ''
  name: ContainerGateOutEvent
  summary: Fired when a container exits through the terminal gate
  title: Container Gate Out
name: Portbase Vessel Events API
provider_name: Port Community Systems
provider_slug: port-community-systems
servers:
- description: Portbase webhook delivery endpoint
  name: portbase-webhook
  protocol: https
  url: https://api.portbase.com/webhooks
slug: portbase-vessel-events-asyncapi
source_filename: portbase-vessel-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Portbase Vessel Events API\n  version: 1.0.0\n  description: >-\n    Portbase publishes real-time vessel call and cargo events via webhooks to\n    connected port community members. Events notify subscribers of vessel\n    status changes, customs release notifications, and container gate events.\n  contact:\n    name: Portbase Support\n    url: https://www.portbase.com/en/contact/\n  license:\n    name: Portbase Terms of Service\n    url: https://www.portbase.com/en/about-portbase/terms-and-conditions/\n\nservers:\n  portbase-webhook:\n    url: https://api.portbase.com/webhooks\n    protocol: https\n    description: Portbase webhook delivery endpoint\n\ndefaultContentType: application/json\n\nchannels:\n  vessel-call/status-changed:\n    description: Event published when a vessel call status changes (e.g., from EXPECTED to ARRIVED)\n    subscribe:\n      operationId: onVesselCallStatusChanged\n      summary: Vessel call status change event\n\
  \      description: >-\n        Triggered when a vessel's status changes at the port. Includes\n        updated timestamps for ATA, ATD, or berth allocation.\n      tags:\n        - name: VesselCalls\n      message:\n        $ref: '#/components/messages/VesselCallStatusChangedEvent'\n\n  cargo-manifest/accepted:\n    description: Event published when a cargo manifest is accepted by Dutch Customs\n    subscribe:\n      operationId: onCargoManifestAccepted\n      summary: Cargo manifest accepted event\n      description: Triggered when the manifest is validated and accepted by customs.\n      tags:\n        - name: CargoManifests\n      message:\n        $ref: '#/components/messages/CargoManifestAcceptedEvent'\n\n  container/customs-released:\n    description: Event published when a container receives customs release\n    subscribe:\n      operationId: onContainerCustomsReleased\n      summary: Container customs released event\n      description: >-\n        Triggered when Dutch Customs\
  \ issues a release order for a container,\n        allowing it to exit the port.\n      tags:\n        - name: Containers\n      message:\n        $ref: '#/components/messages/ContainerCustomsReleasedEvent'\n\n  container/gate-out:\n    description: Event published when a container departs the terminal gate\n    subscribe:\n      operationId: onContainerGateOut\n      summary: Container gate-out event\n      description: Triggered when a container passes through the terminal gate upon pick-up.\n      tags:\n        - name: Containers\n      message:\n        $ref: '#/components/messages/ContainerGateOutEvent'\n\ncomponents:\n  messages:\n    VesselCallStatusChangedEvent:\n      name: VesselCallStatusChanged\n      title: Vessel Call Status Changed\n      summary: Fired when vessel call status changes\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          portbase-event-id:\n            type: string\n            format: uuid\n        \
  \  portbase-event-timestamp:\n            type: string\n            format: date-time\n          portbase-event-type:\n            type: string\n            const: vessel-call.status-changed\n      payload:\n        $ref: '#/components/schemas/VesselCallStatusChangedPayload'\n\n    CargoManifestAcceptedEvent:\n      name: CargoManifestAccepted\n      title: Cargo Manifest Accepted\n      summary: Fired when a manifest is accepted by customs\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CargoManifestAcceptedPayload'\n\n    ContainerCustomsReleasedEvent:\n      name: ContainerCustomsReleased\n      title: Container Customs Released\n      summary: Fired when a container is customs released\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ContainerCustomsReleasedPayload'\n\n    ContainerGateOutEvent:\n      name: ContainerGateOut\n      title: Container Gate Out\n      summary: Fired when a container exits\
  \ through the terminal gate\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ContainerGateOutPayload'\n\n  schemas:\n    VesselCallStatusChangedPayload:\n      type: object\n      required:\n        - eventId\n        - eventTimestamp\n        - vesselCallId\n        - previousStatus\n        - newStatus\n      properties:\n        eventId:\n          type: string\n          format: uuid\n        eventTimestamp:\n          type: string\n          format: date-time\n        vesselCallId:\n          type: string\n        imoNumber:\n          type: string\n        vesselName:\n          type: string\n        portCode:\n          type: string\n        terminalCode:\n          type: string\n        previousStatus:\n          type: string\n          enum: [EXPECTED, ARRIVED, BERTHED, DEPARTED]\n        newStatus:\n          type: string\n          enum: [EXPECTED, ARRIVED, BERTHED, DEPARTED, CANCELLED]\n        ata:\n          type: string\n        \
  \  format: date-time\n          nullable: true\n        atd:\n          type: string\n          format: date-time\n          nullable: true\n\n    CargoManifestAcceptedPayload:\n      type: object\n      required:\n        - eventId\n        - eventTimestamp\n        - manifestId\n        - vesselCallId\n      properties:\n        eventId:\n          type: string\n          format: uuid\n        eventTimestamp:\n          type: string\n          format: date-time\n        manifestId:\n          type: string\n        vesselCallId:\n          type: string\n        acceptanceDatetime:\n          type: string\n          format: date-time\n        declarantId:\n          type: string\n\n    ContainerCustomsReleasedPayload:\n      type: object\n      required:\n        - eventId\n        - eventTimestamp\n        - containerNumber\n      properties:\n        eventId:\n          type: string\n          format: uuid\n        eventTimestamp:\n          type: string\n          format: date-time\n\
  \        containerNumber:\n          type: string\n        vesselCallId:\n          type: string\n        terminalCode:\n          type: string\n        releaseDatetime:\n          type: string\n          format: date-time\n        mrn:\n          type: string\n          description: Customs Movement Reference Number\n\n    ContainerGateOutPayload:\n      type: object\n      required:\n        - eventId\n        - eventTimestamp\n        - containerNumber\n        - gateOutDatetime\n      properties:\n        eventId:\n          type: string\n          format: uuid\n        eventTimestamp:\n          type: string\n          format: date-time\n        containerNumber:\n          type: string\n        terminalCode:\n          type: string\n        gateOutDatetime:\n          type: string\n          format: date-time\n        truckLicensePlate:\n          type: string\n        transporterId:\n          type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/port-community-systems/refs/heads/main/asyncapi/portbase-vessel-events-asyncapi.yml
spec_file: asyncapi/portbase-vessel-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/port-community-systems/refs/heads/main/asyncapi/portbase-vessel-events-asyncapi.yml
tags:
- Maritime
- Port
- Logistics
- Customs
- Cargo
- Shipping
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
