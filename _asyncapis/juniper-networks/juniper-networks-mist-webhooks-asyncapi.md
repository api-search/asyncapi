---
api_specs:
- filename: juniper-networks-apstra-openapi.yml
  format: yaml
  label: Juniper Apstra API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/juniper-networks/refs/heads/main/openapi/juniper-networks-apstra-openapi.yml
- filename: juniper-networks-junos-telemetry-asyncapi.yml
  format: yaml
  label: Junos XML API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/juniper-networks/refs/heads/main/asyncapi/juniper-networks-junos-telemetry-asyncapi.yml
- filename: juniper-networks-mist-openapi.yml
  format: yaml
  label: Juniper Mist API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/juniper-networks/refs/heads/main/openapi/juniper-networks-mist-openapi.yml
- filename: juniper-networks-contrail-openapi.yml
  format: yaml
  label: Juniper Contrail API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/juniper-networks/refs/heads/main/openapi/juniper-networks-contrail-openapi.yml
- filename: juniper-networks-junos-space-openapi.yml
  format: yaml
  label: Junos Space REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/juniper-networks/refs/heads/main/openapi/juniper-networks-junos-space-openapi.yml
- filename: juniper-networks-vsrx-openapi.yml
  format: yaml
  label: Juniper vSRX REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/juniper-networks/refs/heads/main/openapi/juniper-networks-vsrx-openapi.yml
channels:
- description: Channel for device state change events. Triggered when access points, switches, or gateways come online, go offline, or experience configuration changes. Includes AP restarts, firmware upgrades, and connectivity state transitions.
  name: /device-events
  operation: subscribe
  operation_id: onDeviceEvents
  summary: Device event notifications
- description: Channel for alarm notifications. Triggered when new alarms are raised or existing alarms are cleared. Alarm types include device health, connectivity, configuration, capacity, and security events.
  name: /alarms
  operation: subscribe
  operation_id: onAlarms
  summary: Alarm notifications
- description: Channel for audit log notifications. Triggered when administrative actions are performed such as configuration changes, user logins, device operations, and policy updates.
  name: /audits
  operation: subscribe
  operation_id: onAudits
  summary: Audit log notifications
- description: Channel for wireless client session events. Triggered when clients connect, disconnect, or roam between access points. Includes session duration, data usage, and connection quality metrics.
  name: /client-sessions
  operation: subscribe
  operation_id: onClientSessions
  summary: Client session notifications
- description: Channel for location update events from Mist indoor positioning. Triggered when SDK clients or BLE asset tags are detected and their location is calculated using the Mist vBLE antenna array. Provides X/Y coordinates on the floor plan map.
  name: /location
  operation: subscribe
  operation_id: onLocation
  summary: Location update notifications
- description: Channel for zone occupancy events. Triggered when clients enter or exit defined proximity zones on the floor plan. Zones enable location-aware engagement and occupancy analytics.
  name: /zone
  operation: subscribe
  operation_id: onZone
  summary: Zone occupancy notifications
- description: Channel for raw BLE asset tracking events. Triggered when BLE asset beacons are detected by Mist access points. Provides RSSI readings from multiple APs for real-time asset location.
  name: /asset-raw
  operation: subscribe
  operation_id: onAssetRaw
  summary: BLE asset tracking notifications
description: Juniper Mist delivers real-time webhook notifications for network events, device state changes, alarms, audits, and client activity. Webhooks are configured at the organization or site level through the Mist dashboard or API. When events occur, Mist sends HTTP POST requests with JSON payloads to registered webhook URLs. Webhook topics include device events, alarms, audits, client sessions, location updates, zone occupancy, asset tracking, and network anomalies detected by the Marvis AI engine. Each webhook delivery includes a topic header and a payload containing one or more events. Failed deliveries are retried with exponential backoff.
layout: asyncapi
messages:
- description: ''
  name: DeviceEventMessage
  summary: Webhook payload for device state change events including AP, switch, and gateway online/offline transitions, reboots, and upgrades.
  title: Device Event Webhook
- description: ''
  name: AlarmMessage
  summary: Webhook payload for alarm raise and clear events including device health, connectivity, and capacity alerts.
  title: Alarm Webhook
- description: ''
  name: AuditMessage
  summary: Webhook payload for administrative audit events including configuration changes and user actions.
  title: Audit Log Webhook
- description: ''
  name: ClientSessionMessage
  summary: Webhook payload for wireless client connect, disconnect, and roam events with session metrics.
  title: Client Session Webhook
- description: ''
  name: LocationMessage
  summary: Webhook payload for indoor location position updates calculated by the Mist vBLE location engine.
  title: Location Update Webhook
- description: ''
  name: ZoneMessage
  summary: Webhook payload for proximity zone enter and exit events.
  title: Zone Occupancy Webhook
- description: ''
  name: AssetRawMessage
  summary: Webhook payload for raw BLE beacon detection events from access points used for asset tracking.
  title: BLE Asset Raw Webhook
name: Juniper Mist Webhooks
provider_name: Juniper Networks
provider_slug: juniper-networks
servers:
- description: Your webhook endpoint URL registered in the Mist dashboard under Organization > Settings > Webhooks or via the API. The endpoint must accept POST requests with JSON payloads and return a 2xx status code within 30 seconds.
  name: webhook
  protocol: https
  url: '{webhookUrl}'
slug: juniper-networks-mist-webhooks-asyncapi
source_filename: juniper-networks-mist-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Juniper Mist Webhooks\n  version: '1.0'\n  description: >-\n    Juniper Mist delivers real-time webhook notifications for network events,\n    device state changes, alarms, audits, and client activity. Webhooks are\n    configured at the organization or site level through the Mist dashboard\n    or API. When events occur, Mist sends HTTP POST requests with JSON\n    payloads to registered webhook URLs. Webhook topics include device\n    events, alarms, audits, client sessions, location updates, zone\n    occupancy, asset tracking, and network anomalies detected by the\n    Marvis AI engine. Each webhook delivery includes a topic header and\n    a payload containing one or more events. Failed deliveries are retried\n    with exponential backoff.\n  contact:\n    name: Juniper Mist Developer Support\n    url: https://www.juniper.net/documentation/product/us/en/mist/\n  license:\n    name: Proprietary\n    url: https://www.juniper.net/us/en/legal-notices.html\n\
  servers:\n  webhook:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your webhook endpoint URL registered in the Mist dashboard under\n      Organization > Settings > Webhooks or via the API. The endpoint\n      must accept POST requests with JSON payloads and return a 2xx\n      status code within 30 seconds.\n    variables:\n      webhookUrl:\n        description: The URL of your registered webhook endpoint.\nchannels:\n  /device-events:\n    description: >-\n      Channel for device state change events. Triggered when access points,\n      switches, or gateways come online, go offline, or experience\n      configuration changes. Includes AP restarts, firmware upgrades,\n      and connectivity state transitions.\n    subscribe:\n      operationId: onDeviceEvents\n      summary: Device event notifications\n      message:\n        $ref: '#/components/messages/DeviceEventMessage'\n  /alarms:\n    description: >-\n      Channel for alarm notifications. Triggered\
  \ when new alarms are\n      raised or existing alarms are cleared. Alarm types include device\n      health, connectivity, configuration, capacity, and security events.\n    subscribe:\n      operationId: onAlarms\n      summary: Alarm notifications\n      message:\n        $ref: '#/components/messages/AlarmMessage'\n  /audits:\n    description: >-\n      Channel for audit log notifications. Triggered when administrative\n      actions are performed such as configuration changes, user logins,\n      device operations, and policy updates.\n    subscribe:\n      operationId: onAudits\n      summary: Audit log notifications\n      message:\n        $ref: '#/components/messages/AuditMessage'\n  /client-sessions:\n    description: >-\n      Channel for wireless client session events. Triggered when clients\n      connect, disconnect, or roam between access points. Includes\n      session duration, data usage, and connection quality metrics.\n    subscribe:\n      operationId: onClientSessions\n\
  \      summary: Client session notifications\n      message:\n        $ref: '#/components/messages/ClientSessionMessage'\n  /location:\n    description: >-\n      Channel for location update events from Mist indoor positioning.\n      Triggered when SDK clients or BLE asset tags are detected and their\n      location is calculated using the Mist vBLE antenna array. Provides\n      X/Y coordinates on the floor plan map.\n    subscribe:\n      operationId: onLocation\n      summary: Location update notifications\n      message:\n        $ref: '#/components/messages/LocationMessage'\n  /zone:\n    description: >-\n      Channel for zone occupancy events. Triggered when clients enter or\n      exit defined proximity zones on the floor plan. Zones enable\n      location-aware engagement and occupancy analytics.\n    subscribe:\n      operationId: onZone\n      summary: Zone occupancy notifications\n      message:\n        $ref: '#/components/messages/ZoneMessage'\n  /asset-raw:\n    description:\
  \ >-\n      Channel for raw BLE asset tracking events. Triggered when BLE\n      asset beacons are detected by Mist access points. Provides\n      RSSI readings from multiple APs for real-time asset location.\n    subscribe:\n      operationId: onAssetRaw\n      summary: BLE asset tracking notifications\n      message:\n        $ref: '#/components/messages/AssetRawMessage'\ncomponents:\n  messages:\n    DeviceEventMessage:\n      name: DeviceEventMessage\n      title: Device Event Webhook\n      summary: >-\n        Webhook payload for device state change events including AP, switch,\n        and gateway online/offline transitions, reboots, and upgrades.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          topic:\n            type: string\n            const: device-events\n            description: Webhook topic identifier.\n          events:\n            type: array\n            items:\n              type: object\n              properties:\n\
  \                org_id:\n                  type: string\n                  format: uuid\n                  description: Organization ID.\n                site_id:\n                  type: string\n                  format: uuid\n                  description: Site ID.\n                device_id:\n                  type: string\n                  format: uuid\n                  description: Device ID.\n                device_name:\n                  type: string\n                  description: Device name.\n                device_type:\n                  type: string\n                  enum:\n                    - ap\n                    - switch\n                    - gateway\n                  description: Device type.\n                mac:\n                  type: string\n                  description: Device MAC address.\n                type:\n                  type: string\n                  description: >-\n                    Event type (e.g., AP_CONNECTED, AP_DISCONNECTED,\n  \
  \                  AP_RESTARTED, AP_UPGRADED, SW_CONNECTED, GW_CONNECTED).\n                text:\n                  type: string\n                  description: Human-readable event description.\n                timestamp:\n                  type: number\n                  description: Event timestamp in epoch seconds.\n    AlarmMessage:\n      name: AlarmMessage\n      title: Alarm Webhook\n      summary: >-\n        Webhook payload for alarm raise and clear events including device\n        health, connectivity, and capacity alerts.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          topic:\n            type: string\n            const: alarms\n            description: Webhook topic identifier.\n          events:\n            type: array\n            items:\n              type: object\n              properties:\n                org_id:\n                  type: string\n                  format: uuid\n                site_id:\n    \
  \              type: string\n                  format: uuid\n                alarm_id:\n                  type: string\n                  format: uuid\n                  description: Alarm unique identifier.\n                type:\n                  type: string\n                  description: Alarm type identifier.\n                severity:\n                  type: string\n                  enum:\n                    - critical\n                    - warn\n                    - info\n                  description: Alarm severity.\n                group:\n                  type: string\n                  description: Alarm group category.\n                count:\n                  type: integer\n                  description: Occurrence count.\n                cleared:\n                  type: boolean\n                  description: Whether the alarm has been cleared.\n                timestamp:\n                  type: number\n                  description: Event timestamp in epoch seconds.\n\
  \    AuditMessage:\n      name: AuditMessage\n      title: Audit Log Webhook\n      summary: >-\n        Webhook payload for administrative audit events including\n        configuration changes and user actions.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          topic:\n            type: string\n            const: audits\n            description: Webhook topic identifier.\n          events:\n            type: array\n            items:\n              type: object\n              properties:\n                org_id:\n                  type: string\n                  format: uuid\n                site_id:\n                  type: string\n                  format: uuid\n                admin_name:\n                  type: string\n                  description: Name of the administrator who performed the action.\n                message:\n                  type: string\n                  description: Description of the action performed.\n\
  \                src_ip:\n                  type: string\n                  description: Source IP address of the admin session.\n                timestamp:\n                  type: number\n                  description: Event timestamp in epoch seconds.\n    ClientSessionMessage:\n      name: ClientSessionMessage\n      title: Client Session Webhook\n      summary: >-\n        Webhook payload for wireless client connect, disconnect, and\n        roam events with session metrics.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          topic:\n            type: string\n            const: client-sessions\n            description: Webhook topic identifier.\n          events:\n            type: array\n            items:\n              type: object\n              properties:\n                org_id:\n                  type: string\n                  format: uuid\n                site_id:\n                  type: string\n                  format:\
  \ uuid\n                ap:\n                  type: string\n                  description: AP MAC address.\n                mac:\n                  type: string\n                  description: Client MAC address.\n                ssid:\n                  type: string\n                  description: Connected SSID.\n                connect:\n                  type: number\n                  description: Session start timestamp.\n                disconnect:\n                  type: number\n                  description: Session end timestamp (0 if still connected).\n                duration:\n                  type: number\n                  description: Session duration in seconds.\n                rx_bytes:\n                  type: integer\n                  description: Bytes received during session.\n                tx_bytes:\n                  type: integer\n                  description: Bytes transmitted during session.\n                rssi:\n                  type: number\n   \
  \               description: Average RSSI during session.\n                band:\n                  type: string\n                  description: Radio band.\n                channel:\n                  type: integer\n                  description: Radio channel.\n                wlan_id:\n                  type: string\n                  format: uuid\n                  description: WLAN configuration ID.\n                timestamp:\n                  type: number\n                  description: Event timestamp in epoch seconds.\n    LocationMessage:\n      name: LocationMessage\n      title: Location Update Webhook\n      summary: >-\n        Webhook payload for indoor location position updates calculated\n        by the Mist vBLE location engine.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          topic:\n            type: string\n            const: location\n            description: Webhook topic identifier.\n          events:\n\
  \            type: array\n            items:\n              type: object\n              properties:\n                site_id:\n                  type: string\n                  format: uuid\n                map_id:\n                  type: string\n                  format: uuid\n                  description: Floor plan map ID.\n                mac:\n                  type: string\n                  description: Client or asset MAC address.\n                x:\n                  type: number\n                  description: X coordinate in meters from map origin.\n                'y':\n                  type: number\n                  description: Y coordinate in meters from map origin.\n                timestamp:\n                  type: number\n                  description: Location calculation timestamp.\n    ZoneMessage:\n      name: ZoneMessage\n      title: Zone Occupancy Webhook\n      summary: >-\n        Webhook payload for proximity zone enter and exit events.\n      contentType:\
  \ application/json\n      payload:\n        type: object\n        properties:\n          topic:\n            type: string\n            const: zone\n            description: Webhook topic identifier.\n          events:\n            type: array\n            items:\n              type: object\n              properties:\n                site_id:\n                  type: string\n                  format: uuid\n                map_id:\n                  type: string\n                  format: uuid\n                zone_id:\n                  type: string\n                  format: uuid\n                  description: Proximity zone ID.\n                mac:\n                  type: string\n                  description: Client or asset MAC address.\n                trigger:\n                  type: string\n                  enum:\n                    - enter\n                    - exit\n                  description: Zone transition direction.\n                timestamp:\n                  type:\
  \ number\n                  description: Event timestamp.\n    AssetRawMessage:\n      name: AssetRawMessage\n      title: BLE Asset Raw Webhook\n      summary: >-\n        Webhook payload for raw BLE beacon detection events from access\n        points used for asset tracking.\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          topic:\n            type: string\n            const: asset-raw\n            description: Webhook topic identifier.\n          events:\n            type: array\n            items:\n              type: object\n              properties:\n                site_id:\n                  type: string\n                  format: uuid\n                mac:\n                  type: string\n                  description: BLE beacon MAC address.\n                beam:\n                  type: integer\n                  description: vBLE antenna beam index.\n                rssi:\n                  type: number\n           \
  \       description: Received signal strength in dBm.\n                ap_mac:\n                  type: string\n                  description: Detecting AP MAC address.\n                ibeacon_uuid:\n                  type: string\n                  description: iBeacon UUID if applicable.\n                ibeacon_major:\n                  type: integer\n                  description: iBeacon major value.\n                ibeacon_minor:\n                  type: integer\n                  description: iBeacon minor value.\n                eddystone_uid_instance:\n                  type: string\n                  description: Eddystone UID instance ID if applicable.\n                eddystone_uid_namespace:\n                  type: string\n                  description: Eddystone UID namespace if applicable.\n                timestamp:\n                  type: number\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/juniper-networks/refs/heads/main/asyncapi/juniper-networks-mist-webhooks-asyncapi.yml
spec_file: asyncapi/juniper-networks-mist-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/juniper-networks/refs/heads/main/asyncapi/juniper-networks-mist-webhooks-asyncapi.yml
tags:
- Automation
- Cloud
- Data Center
- Enterprise
- Networking
- SDN
- Security
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
