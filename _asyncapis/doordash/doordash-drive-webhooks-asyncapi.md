---
api_specs:
- filename: doordash-drive-openapi.yml
  format: yaml
  label: DoorDash Drive API
  slug: drive-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-drive-openapi.yml
- filename: doordash-drive-classic-openapi.yml
  format: yaml
  label: DoorDash Drive Classic API
  slug: drive-classic-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-drive-classic-openapi.yml
- filename: doordash-marketplace-openapi.yml
  format: yaml
  label: DoorDash Marketplace API
  slug: marketplace-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-marketplace-openapi.yml
- filename: doordash-item-management-openapi.yml
  format: yaml
  label: DoorDash Item Management API
  slug: marketplace-item-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-item-management-openapi.yml
- filename: doordash-reporting-openapi.yml
  format: yaml
  label: DoorDash Reporting API
  slug: reporting-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/openapi/doordash-reporting-openapi.yml
channels:
- description: DoorDash sends delivery status update events to this channel whenever a delivery progresses through its lifecycle.
  name: /webhook
  operation: publish
  operation_id: receiveDeliveryWebhook
  summary: Receive delivery status webhooks
description: DoorDash Drive sends webhook notifications for delivery status updates, enabling near-real-time information flow from DoorDash and Dashers to partner applications. Webhooks support scenarios like map views showing customers how far away their Dasher is and push notifications about order status. DoorDash sends each webhook event up to 3 times, retrying if it receives a response other than 200 OK or no response at all. Webhook payloads contain all available delivery details at the time of sending. Fields that are empty or unavailable are omitted. All time fields are sent as ISO-8601 date-times in UTC.
layout: asyncapi
messages:
- description: ''
  name: DasherConfirmed
  summary: A Dasher has accepted the delivery and is on the way to the pickup location.
  title: Dasher Confirmed
- description: ''
  name: DasherConfirmedPickupArrival
  summary: The Dasher has confirmed arrival at the pickup location and is attempting to pick up the delivery.
  title: Dasher Confirmed Pickup Arrival
- description: ''
  name: DasherConfirmedDropoffArrival
  summary: The Dasher has confirmed arrival at the dropoff location.
  title: Dasher Confirmed Dropoff Arrival
- description: ''
  name: DasherDroppedOff
  summary: The Dasher has dropped off the delivery at the dropoff location and the delivery is complete.
  title: Dasher Dropped Off
- description: ''
  name: DeliveryReturnInitialized
  summary: The Dasher was unable to deliver to the dropoff location and has contacted support to arrange a return-to-pickup delivery.
  title: Delivery Return Initialized
- description: ''
  name: DasherConfirmedReturnArrival
  summary: The Dasher has confirmed arrival at the pickup location to return the delivery.
  title: Dasher Confirmed Return Arrival
- description: ''
  name: DeliveryReturned
  summary: The delivery has been returned successfully to the pickup location.
  title: Delivery Returned
- description: ''
  name: DeliveryCancelled
  summary: The delivery has been cancelled. When the reason is failed_to_return, the delivery was unable to be returned.
  title: Delivery Cancelled
- description: ''
  name: DeliveryBatched
  summary: The delivery has been assigned to a batch and will only be assigned to the same Dasher as all other deliveries with the matching force_batch_id.
  title: Delivery Batched
name: DoorDash Drive Delivery Webhooks
provider_name: doordash
provider_slug: doordash
servers:
- description: The partner-provided HTTPS webhook endpoint. Must be protected with authentication. DoorDash supports Basic Auth and OAuth for webhook endpoint security.
  name: partnerWebhook
  protocol: https
  url: '{webhook_url}'
slug: doordash-drive-webhooks-asyncapi
source_filename: doordash-drive-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: DoorDash Drive Delivery Webhooks\n  description: >-\n    DoorDash Drive sends webhook notifications for delivery status updates,\n    enabling near-real-time information flow from DoorDash and Dashers to\n    partner applications. Webhooks support scenarios like map views showing\n    customers how far away their Dasher is and push notifications about\n    order status. DoorDash sends each webhook event up to 3 times, retrying\n    if it receives a response other than 200 OK or no response at all.\n    Webhook payloads contain all available delivery details at the time of\n    sending. Fields that are empty or unavailable are omitted. All time\n    fields are sent as ISO-8601 date-times in UTC.\n  version: '2.0'\n  contact:\n    name: DoorDash Developer Support\n    url: https://developer.doordash.com/en-US/\nservers:\n  partnerWebhook:\n    url: '{webhook_url}'\n    protocol: https\n    description: >-\n      The partner-provided HTTPS webhook\
  \ endpoint. Must be protected with\n      authentication. DoorDash supports Basic Auth and OAuth for webhook\n      endpoint security.\n    security:\n      - basicAuth: []\n    variables:\n      webhook_url:\n        description: >-\n          The HTTPS URL of the partner's webhook endpoint.\nchannels:\n  /webhook:\n    description: >-\n      DoorDash sends delivery status update events to this channel whenever\n      a delivery progresses through its lifecycle.\n    publish:\n      operationId: receiveDeliveryWebhook\n      summary: Receive delivery status webhooks\n      description: >-\n        Receives webhook notifications from DoorDash about delivery status\n        changes. Partners must respond with 200 OK to acknowledge receipt.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/DasherConfirmed'\n          - $ref: '#/components/messages/DasherConfirmedPickupArrival'\n          - $ref: '#/components/messages/DasherConfirmedDropoffArrival'\n          - $ref:\
  \ '#/components/messages/DasherDroppedOff'\n          - $ref: '#/components/messages/DeliveryReturnInitialized'\n          - $ref: '#/components/messages/DasherConfirmedReturnArrival'\n          - $ref: '#/components/messages/DeliveryReturned'\n          - $ref: '#/components/messages/DeliveryCancelled'\n          - $ref: '#/components/messages/DeliveryBatched'\ncomponents:\n  securitySchemes:\n    basicAuth:\n      type: http\n      scheme: basic\n      description: >-\n        Basic authentication for webhook endpoint security.\n    oauth2:\n      type: oauth2\n      description: >-\n        OAuth 2.0 authentication for webhook endpoint security.\n      flows:\n        clientCredentials:\n          tokenUrl: ''\n          scopes: {}\n  messages:\n    DasherConfirmed:\n      name: DASHER_CONFIRMED\n      title: Dasher Confirmed\n      summary: >-\n        A Dasher has accepted the delivery and is on the way to the pickup\n        location.\n      payload:\n        $ref: '#/components/schemas/DeliveryWebhookPayload'\n\
  \    DasherConfirmedPickupArrival:\n      name: DASHER_CONFIRMED_PICKUP_ARRIVAL\n      title: Dasher Confirmed Pickup Arrival\n      summary: >-\n        The Dasher has confirmed arrival at the pickup location and is\n        attempting to pick up the delivery.\n      payload:\n        $ref: '#/components/schemas/DeliveryWebhookPayload'\n    DasherConfirmedDropoffArrival:\n      name: DASHER_CONFIRMED_DROPOFF_ARRIVAL\n      title: Dasher Confirmed Dropoff Arrival\n      summary: >-\n        The Dasher has confirmed arrival at the dropoff location.\n      payload:\n        $ref: '#/components/schemas/DeliveryWebhookPayload'\n    DasherDroppedOff:\n      name: DASHER_DROPPED_OFF\n      title: Dasher Dropped Off\n      summary: >-\n        The Dasher has dropped off the delivery at the dropoff location\n        and the delivery is complete.\n      payload:\n        $ref: '#/components/schemas/DeliveryWebhookPayload'\n    DeliveryReturnInitialized:\n      name: DELIVERY_RETURN_INITIALIZED\n\
  \      title: Delivery Return Initialized\n      summary: >-\n        The Dasher was unable to deliver to the dropoff location and has\n        contacted support to arrange a return-to-pickup delivery.\n      payload:\n        $ref: '#/components/schemas/DeliveryWebhookPayload'\n    DasherConfirmedReturnArrival:\n      name: DASHER_CONFIRMED_RETURN_ARRIVAL\n      title: Dasher Confirmed Return Arrival\n      summary: >-\n        The Dasher has confirmed arrival at the pickup location to return\n        the delivery.\n      payload:\n        $ref: '#/components/schemas/DeliveryWebhookPayload'\n    DeliveryReturned:\n      name: DELIVERY_RETURNED\n      title: Delivery Returned\n      summary: >-\n        The delivery has been returned successfully to the pickup location.\n      payload:\n        $ref: '#/components/schemas/DeliveryWebhookPayload'\n    DeliveryCancelled:\n      name: DELIVERY_CANCELLED\n      title: Delivery Cancelled\n      summary: >-\n        The delivery has been cancelled.\
  \ When the reason is failed_to_return,\n        the delivery was unable to be returned.\n      payload:\n        $ref: '#/components/schemas/DeliveryWebhookPayload'\n    DeliveryBatched:\n      name: DELIVERY_BATCHED\n      title: Delivery Batched\n      summary: >-\n        The delivery has been assigned to a batch and will only be assigned\n        to the same Dasher as all other deliveries with the matching\n        force_batch_id.\n      payload:\n        $ref: '#/components/schemas/DeliveryWebhookPayload'\n  schemas:\n    DeliveryWebhookPayload:\n      type: object\n      properties:\n        external_delivery_id:\n          type: string\n          description: >-\n            The unique external delivery ID.\n        event_type:\n          type: string\n          description: >-\n            The type of delivery event.\n          enum:\n            - DASHER_CONFIRMED\n            - DASHER_CONFIRMED_PICKUP_ARRIVAL\n            - DASHER_CONFIRMED_DROPOFF_ARRIVAL\n            - DASHER_DROPPED_OFF\n\
  \            - DELIVERY_RETURN_INITIALIZED\n            - DASHER_CONFIRMED_RETURN_ARRIVAL\n            - DELIVERY_RETURNED\n            - DELIVERY_CANCELLED\n            - DELIVERY_BATCHED\n        delivery_status:\n          type: string\n          description: >-\n            The current status of the delivery.\n        fee:\n          type: integer\n          description: >-\n            The delivery fee in cents.\n        currency:\n          type: string\n          description: >-\n            The currency code.\n        tip:\n          type: integer\n          description: >-\n            The tip amount in cents.\n        order_value:\n          type: integer\n          description: >-\n            The total order value in cents.\n        pickup_address:\n          type: string\n          description: >-\n            The pickup address.\n        pickup_business_name:\n          type: string\n          description: >-\n            The business name at the pickup location.\n      \
  \  pickup_time_estimated:\n          type: string\n          format: date-time\n          description: >-\n            The estimated pickup time in UTC ISO-8601 format.\n        pickup_time_actual:\n          type: string\n          format: date-time\n          description: >-\n            The actual pickup time. Only included after pickup occurs.\n        dropoff_address:\n          type: string\n          description: >-\n            The dropoff address.\n        dropoff_time_estimated:\n          type: string\n          format: date-time\n          description: >-\n            The estimated dropoff time in UTC ISO-8601 format.\n        dropoff_time_actual:\n          type: string\n          format: date-time\n          description: >-\n            The actual dropoff time. Only included after dropoff occurs.\n        dropoff_contact_given_name:\n          type: string\n          description: >-\n            The first name of the dropoff contact.\n        dropoff_contact_family_name:\n\
  \          type: string\n          description: >-\n            The last name of the dropoff contact.\n        dasher_id:\n          type: integer\n          description: >-\n            The assigned Dasher's ID.\n        dasher_name:\n          type: string\n          description: >-\n            The assigned Dasher's first name.\n        dasher_phone_number:\n          type: string\n          description: >-\n            The assigned Dasher's phone number.\n        dasher_location_lat:\n          type: number\n          format: double\n          description: >-\n            The Dasher's current latitude.\n        dasher_location_lng:\n          type: number\n          format: double\n          description: >-\n            The Dasher's current longitude.\n        tracking_url:\n          type: string\n          format: uri\n          description: >-\n            A URL for tracking the delivery.\n        cancellation_reason:\n          type: string\n          description: >-\n        \
  \    The reason for cancellation. Only present for DELIVERY_CANCELLED\n            events.\n        force_batch_id:\n          type: string\n          description: >-\n            The batch identifier. Only present for DELIVERY_BATCHED events.\n        contains_alcohol:\n          type: boolean\n          description: >-\n            Whether the order contains alcohol.\n        created_at:\n          type: string\n          format: date-time\n          description: >-\n            When the delivery was created.\n        updated_at:\n          type: string\n          format: date-time\n          description: >-\n            When the delivery was last updated.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/asyncapi/doordash-drive-webhooks-asyncapi.yml
spec_file: asyncapi/doordash-drive-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/doordash/refs/heads/main/asyncapi/doordash-drive-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '2.0'
---
