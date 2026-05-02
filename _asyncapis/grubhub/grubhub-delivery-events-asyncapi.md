---
api_specs:
- filename: grubhub-menu-openapi.yml
  format: yaml
  label: Grubhub Menu API
  slug: menu-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/openapi/grubhub-menu-openapi.yml
- filename: grubhub-orders-openapi.yml
  format: yaml
  label: Grubhub Orders API
  slug: orders-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/openapi/grubhub-orders-openapi.yml
- filename: grubhub-merchant-data-openapi.yml
  format: yaml
  label: Grubhub Merchant Data API
  slug: merchant-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/openapi/grubhub-merchant-data-openapi.yml
- filename: grubhub-merchant-schedules-openapi.yml
  format: yaml
  label: Grubhub Merchant Schedules API
  slug: merchant-schedules-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/openapi/grubhub-merchant-schedules-openapi.yml
- filename: grubhub-deliveries-openapi.yml
  format: yaml
  label: Grubhub Deliveries API
  slug: deliveries-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/openapi/grubhub-deliveries-openapi.yml
- filename: grubhub-onboarding-openapi.yml
  format: yaml
  label: Grubhub Onboarding API
  slug: onboarding-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/openapi/grubhub-onboarding-openapi.yml
channels:
- description: Channel for receiving delivery status update events including driver assignment, courier location, ETA updates, and delivery completion.
  name: /webhook/delivery-status
  operation: publish
  operation_id: receiveDeliveryStatusUpdate
  summary: Receive delivery status updates
- description: Channel for receiving delivery refund update events including acceptance or rejection of refund requests.
  name: /webhook/delivery-refund
  operation: publish
  operation_id: receiveDeliveryRefundUpdate
  summary: Receive delivery refund updates
description: Event-driven interface for receiving real-time delivery status updates from Grubhub. Partners can subscribe to webhook notifications for delivery updates including driver assignment, courier location updates, ETA updates, order cancellations, and refund decisions. This eliminates the need for polling delivery status endpoints.
layout: asyncapi
messages:
- description: ''
  name: DriverAssigned
  summary: A delivery driver has been assigned to the order.
  title: Driver Assigned
- description: ''
  name: DeliveryStatusUpdate
  summary: The delivery status has changed, such as pickup, en route, or delivered.
  title: Delivery Status Update
- description: ''
  name: CourierLocationUpdate
  summary: The courier's location or ETA has been updated.
  title: Courier Location Update
- description: ''
  name: DeliveryCancelled
  summary: The delivery has been cancelled.
  title: Delivery Cancelled
- description: ''
  name: DeliveryRefundUpdate
  summary: A refund request has been accepted or rejected with details on the decision and amount.
  title: Delivery Refund Update
name: Grubhub Delivery Events
provider_name: grubhub
provider_slug: grubhub
servers:
- description: Partner-hosted webhook endpoint. Grubhub sends delivery event payloads to this URL. Webhook URLs require manual verification by Grubhub to avoid sending requests to unauthorized endpoints.
  name: partnerWebhook
  protocol: https
  url: '{webhookUrl}'
slug: grubhub-delivery-events-asyncapi
source_filename: grubhub-delivery-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Grubhub Delivery Events\n  description: >-\n    Event-driven interface for receiving real-time delivery status updates\n    from Grubhub. Partners can subscribe to webhook notifications for\n    delivery updates including driver assignment, courier location updates,\n    ETA updates, order cancellations, and refund decisions. This eliminates\n    the need for polling delivery status endpoints.\n  version: '1.0.0'\n  contact:\n    name: Grubhub Developer Support\n    url: https://grubhub-developers.zendesk.com/hc/en-us\nservers:\n  partnerWebhook:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Partner-hosted webhook endpoint. Grubhub sends delivery event\n      payloads to this URL. Webhook URLs require manual verification\n      by Grubhub to avoid sending requests to unauthorized endpoints.\n    variables:\n      webhookUrl:\n        description: >-\n          The partner's webhook endpoint URL configured during onboarding.\n\
  \    security:\n      - basicAuth: []\n      - hmacAuth: []\nchannels:\n  /webhook/delivery-status:\n    description: >-\n      Channel for receiving delivery status update events including driver\n      assignment, courier location, ETA updates, and delivery completion.\n    publish:\n      operationId: receiveDeliveryStatusUpdate\n      summary: Receive delivery status updates\n      description: >-\n        Receives delivery status update events from Grubhub including\n        driver assigned, order canceled, courier location updates, and\n        ETA updates for a specific delivery. Also includes courier\n        information such as name and delivery method.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/DriverAssigned'\n          - $ref: '#/components/messages/DeliveryStatusUpdate'\n          - $ref: '#/components/messages/CourierLocationUpdate'\n          - $ref: '#/components/messages/DeliveryCancelled'\n  /webhook/delivery-refund:\n    description: >-\n\
  \      Channel for receiving delivery refund update events including\n      acceptance or rejection of refund requests.\n    publish:\n      operationId: receiveDeliveryRefundUpdate\n      summary: Receive delivery refund updates\n      description: >-\n        Receives updates on refund request acceptance or rejection\n        including details on the decision and the refund amount.\n      message:\n        $ref: '#/components/messages/DeliveryRefundUpdate'\ncomponents:\n  securitySchemes:\n    basicAuth:\n      type: userPassword\n      description: >-\n        Basic authentication using credentials provided during partner\n        signup, included in the header of webhook requests.\n    hmacAuth:\n      type: httpApiKey\n      name: Authorization\n      in: header\n      description: >-\n        HMAC authentication providing message integrity verification.\n        Recommended for most webhook integrations.\n  messages:\n    DriverAssigned:\n      name: DriverAssigned\n      title:\
  \ Driver Assigned\n      summary: >-\n        A delivery driver has been assigned to the order.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DriverAssignedPayload'\n    DeliveryStatusUpdate:\n      name: DeliveryStatusUpdate\n      title: Delivery Status Update\n      summary: >-\n        The delivery status has changed, such as pickup, en route,\n        or delivered.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DeliveryStatusPayload'\n    CourierLocationUpdate:\n      name: CourierLocationUpdate\n      title: Courier Location Update\n      summary: >-\n        The courier's location or ETA has been updated.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CourierLocationPayload'\n    DeliveryCancelled:\n      name: DeliveryCancelled\n      title: Delivery Cancelled\n      summary: >-\n        The delivery has been cancelled.\n      contentType: application/json\n\
  \      payload:\n        $ref: '#/components/schemas/DeliveryCancelledPayload'\n    DeliveryRefundUpdate:\n      name: DeliveryRefundUpdate\n      title: Delivery Refund Update\n      summary: >-\n        A refund request has been accepted or rejected with details\n        on the decision and amount.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DeliveryRefundPayload'\n  schemas:\n    DriverAssignedPayload:\n      type: object\n      description: >-\n        Webhook payload when a driver is assigned to a delivery.\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of delivery event.\n          const: DRIVER_ASSIGNED\n        order_uuid:\n          type: string\n          format: uuid\n          description: >-\n            The UUID of the associated order.\n        delivery_id:\n          type: string\n          description: >-\n            The unique identifier for the delivery.\n\
  \        driver:\n          type: object\n          description: >-\n            Information about the assigned driver.\n          properties:\n            name:\n              type: string\n              description: >-\n                The driver's display name.\n            phone:\n              type: string\n              description: >-\n                The driver's contact phone number.\n            delivery_method:\n              type: string\n              description: >-\n                The delivery method being used.\n              enum:\n                - CAR\n                - BIKE\n                - WALKING\n        pickup_eta:\n          type: string\n          format: date-time\n          description: >-\n            Estimated time of arrival at the pickup location.\n        dropoff_eta:\n          type: string\n          format: date-time\n          description: >-\n            Estimated time of arrival at the delivery location.\n        timestamp:\n          type: string\n\
  \          format: date-time\n          description: >-\n            When this event occurred.\n    DeliveryStatusPayload:\n      type: object\n      description: >-\n        Webhook payload for a delivery status change.\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of delivery event.\n          const: DELIVERY_STATUS_UPDATE\n        order_uuid:\n          type: string\n          format: uuid\n          description: >-\n            The UUID of the associated order.\n        delivery_id:\n          type: string\n          description: >-\n            The unique identifier for the delivery.\n        status:\n          type: string\n          description: >-\n            The new delivery status.\n          enum:\n            - DRIVER_EN_ROUTE_TO_PICKUP\n            - ARRIVED_AT_PICKUP\n            - PICKED_UP\n            - OUT_FOR_DELIVERY\n            - ARRIVED_AT_DROPOFF\n            - DELIVERED\n        pickup_eta:\n \
  \         type: string\n          format: date-time\n          description: >-\n            Updated estimated time of arrival at pickup.\n        dropoff_eta:\n          type: string\n          format: date-time\n          description: >-\n            Updated estimated time of arrival at dropoff.\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            When this event occurred.\n    CourierLocationPayload:\n      type: object\n      description: >-\n        Webhook payload for a courier location or ETA update.\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of delivery event.\n          const: COURIER_LOCATION_UPDATE\n        order_uuid:\n          type: string\n          format: uuid\n          description: >-\n            The UUID of the associated order.\n        delivery_id:\n          type: string\n          description: >-\n            The unique identifier for\
  \ the delivery.\n        latitude:\n          type: number\n          format: double\n          description: >-\n            The courier's current latitude coordinate.\n        longitude:\n          type: number\n          format: double\n          description: >-\n            The courier's current longitude coordinate.\n        pickup_eta:\n          type: string\n          format: date-time\n          description: >-\n            Updated estimated time of arrival at pickup.\n        dropoff_eta:\n          type: string\n          format: date-time\n          description: >-\n            Updated estimated time of arrival at dropoff.\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            When this location update was recorded.\n    DeliveryCancelledPayload:\n      type: object\n      description: >-\n        Webhook payload when a delivery is cancelled.\n      properties:\n        event_type:\n          type: string\n          description:\
  \ >-\n            The type of delivery event.\n          const: DELIVERY_CANCELLED\n        order_uuid:\n          type: string\n          format: uuid\n          description: >-\n            The UUID of the associated order.\n        delivery_id:\n          type: string\n          description: >-\n            The unique identifier for the delivery.\n        reason:\n          type: string\n          description: >-\n            The reason for cancellation.\n        cancelled_at:\n          type: string\n          format: date-time\n          description: >-\n            When the delivery was cancelled.\n    DeliveryRefundPayload:\n      type: object\n      description: >-\n        Webhook payload for a delivery refund decision.\n      properties:\n        event_type:\n          type: string\n          description: >-\n            The type of delivery event.\n          const: DELIVERY_REFUND_UPDATE\n        order_uuid:\n          type: string\n          format: uuid\n          description:\
  \ >-\n            The UUID of the associated order.\n        delivery_id:\n          type: string\n          description: >-\n            The unique identifier for the delivery.\n        refund_status:\n          type: string\n          description: >-\n            Whether the refund was accepted or rejected.\n          enum:\n            - ACCEPTED\n            - REJECTED\n        refund_amount:\n          type: number\n          format: double\n          description: >-\n            The amount of the refund.\n        decision_reason:\n          type: string\n          description: >-\n            Explanation of the refund decision.\n        decided_at:\n          type: string\n          format: date-time\n          description: >-\n            When the refund decision was made.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/asyncapi/grubhub-delivery-events-asyncapi.yml
spec_file: asyncapi/grubhub-delivery-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/grubhub/refs/heads/main/asyncapi/grubhub-delivery-events-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
