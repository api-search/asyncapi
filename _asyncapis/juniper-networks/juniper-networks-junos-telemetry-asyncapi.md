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
- description: 'Channel for interface telemetry data. Provides real-time statistics for physical and logical interfaces including packet counts, byte counts, error counters, queue depths, and interface operational status. Sensor path: /junos/system/linecard/interface/'
  name: /interfaces
  operation: subscribe
  operation_id: onInterfaceStats
  summary: Interface statistics telemetry stream
- description: Channel for routing telemetry. Provides BGP session state changes, route count updates, and routing table modifications. Sensor paths include /junos/routing/ for Junos-native and OpenConfig BGP paths.
  name: /routing
  operation: subscribe
  operation_id: onRoutingTelemetry
  summary: Routing protocol telemetry stream
- description: 'Channel for system resource telemetry. Reports CPU utilization, memory usage, storage capacity, and routing engine temperature for capacity planning and health monitoring. Sensor path: /junos/system/'
  name: /system-resources
  operation: subscribe
  operation_id: onSystemResources
  summary: System resource utilization telemetry stream
- description: 'Channel for firewall filter counter telemetry. Provides real-time packet and byte counts for configured firewall filter terms. Sensor path: /junos/system/linecard/firewall/'
  name: /firewall
  operation: subscribe
  operation_id: onFirewallCounters
  summary: Firewall filter counter telemetry stream
- description: 'Channel for optical transceiver diagnostics. Reports real-time optical power levels, laser bias current, temperature, and voltage for SFP/QSFP transceivers. Used for proactive link failure detection. Sensor path: /junos/system/linecard/optics/'
  name: /optics
  operation: subscribe
  operation_id: onOpticsDiagnostics
  summary: Optical diagnostics telemetry stream
description: Junos Telemetry Interface provides real-time streaming telemetry from Juniper Networks devices using gRPC or UDP protocols. JTI pushes operational data from Junos devices at configured intervals, replacing traditional SNMP polling with high-frequency, model-driven telemetry. Supported data includes interface statistics, routing table changes, firewall filter counters, optics diagnostics, system resource utilization, and protocol-specific metrics. Data is encoded in Google Protocol Buffers (GPB) format or OpenConfig-modeled JSON/YANG. JTI supports both dial-out (device-initiated) and dial-in (collector-initiated via gNMI) modes. This specification covers the dial-out streaming model where Junos devices publish telemetry to configured collector endpoints.
layout: asyncapi
messages:
- description: ''
  name: InterfaceStatsMessage
  summary: Real-time interface counter data including ingress/egress packet and byte counts, error counters, and queue statistics. Published at the configured reporting rate (typically 2-30 seconds).
  title: Interface Statistics Telemetry
- description: ''
  name: RoutingMessage
  summary: BGP session state and route count telemetry data. Reports peer session transitions, received/advertised prefix counts, and route table summary statistics.
  title: Routing Protocol Telemetry
- description: ''
  name: SystemResourceMessage
  summary: System resource utilization data including CPU, memory, and temperature readings from routing engines and line cards.
  title: System Resource Telemetry
- description: ''
  name: FirewallMessage
  summary: Real-time firewall filter counter data for configured filter terms. Reports packet and byte match counts per filter term.
  title: Firewall Filter Counter Telemetry
- description: ''
  name: OpticsMessage
  summary: Optical transceiver diagnostic readings including power levels, bias current, temperature, and voltage for SFP/QSFP modules.
  title: Optical Transceiver Diagnostics Telemetry
name: Junos Telemetry Interface (JTI) Streaming
provider_name: Juniper Networks
provider_slug: juniper-networks
servers:
- description: gRPC telemetry collector endpoint. Junos devices establish a persistent gRPC stream to the collector and push telemetry data at the configured reporting interval. Configure the collector address on Junos devices under services analytics streaming-server.
  name: grpcCollector
  protocol: grpc
  url: '{collectorHost}:{collectorPort}'
- description: UDP telemetry collector for native GPB-encoded sensor data. Junos devices send UDP datagrams containing serialized Protocol Buffer messages to the collector. Configured under services analytics export-profile with transport udp.
  name: udpCollector
  protocol: udp
  url: '{collectorHost}:{collectorPort}'
slug: juniper-networks-junos-telemetry-asyncapi
source_filename: juniper-networks-junos-telemetry-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Junos Telemetry Interface (JTI) Streaming\n  version: '1.0'\n  description: >-\n    Junos Telemetry Interface provides real-time streaming telemetry from\n    Juniper Networks devices using gRPC or UDP protocols. JTI pushes\n    operational data from Junos devices at configured intervals, replacing\n    traditional SNMP polling with high-frequency, model-driven telemetry.\n    Supported data includes interface statistics, routing table changes,\n    firewall filter counters, optics diagnostics, system resource utilization,\n    and protocol-specific metrics. Data is encoded in Google Protocol Buffers\n    (GPB) format or OpenConfig-modeled JSON/YANG. JTI supports both dial-out\n    (device-initiated) and dial-in (collector-initiated via gNMI) modes.\n    This specification covers the dial-out streaming model where Junos\n    devices publish telemetry to configured collector endpoints.\n  contact:\n    name: Juniper Networks Support\n    url:\
  \ https://www.juniper.net/documentation/us/en/software/junos/interfaces-telemetry/index.html\n  license:\n    name: Proprietary\n    url: https://www.juniper.net/us/en/legal-notices.html\nservers:\n  grpcCollector:\n    url: '{collectorHost}:{collectorPort}'\n    protocol: grpc\n    description: >-\n      gRPC telemetry collector endpoint. Junos devices establish a persistent\n      gRPC stream to the collector and push telemetry data at the configured\n      reporting interval. Configure the collector address on Junos devices\n      under services analytics streaming-server.\n    variables:\n      collectorHost:\n        description: Hostname or IP of the telemetry collector.\n      collectorPort:\n        description: gRPC port on the collector.\n        default: '50051'\n  udpCollector:\n    url: '{collectorHost}:{collectorPort}'\n    protocol: udp\n    description: >-\n      UDP telemetry collector for native GPB-encoded sensor data. Junos\n      devices send UDP datagrams containing\
  \ serialized Protocol Buffer\n      messages to the collector. Configured under services analytics\n      export-profile with transport udp.\n    variables:\n      collectorHost:\n        description: Hostname or IP of the telemetry collector.\n      collectorPort:\n        description: UDP port on the collector.\n        default: '21000'\nchannels:\n  /interfaces:\n    description: >-\n      Channel for interface telemetry data. Provides real-time statistics\n      for physical and logical interfaces including packet counts, byte\n      counts, error counters, queue depths, and interface operational status.\n      Sensor path: /junos/system/linecard/interface/\n    subscribe:\n      operationId: onInterfaceStats\n      summary: Interface statistics telemetry stream\n      message:\n        $ref: '#/components/messages/InterfaceStatsMessage'\n  /routing:\n    description: >-\n      Channel for routing telemetry. Provides BGP session state changes,\n      route count updates, and routing\
  \ table modifications. Sensor paths\n      include /junos/routing/ for Junos-native and OpenConfig BGP paths.\n    subscribe:\n      operationId: onRoutingTelemetry\n      summary: Routing protocol telemetry stream\n      message:\n        $ref: '#/components/messages/RoutingMessage'\n  /system-resources:\n    description: >-\n      Channel for system resource telemetry. Reports CPU utilization,\n      memory usage, storage capacity, and routing engine temperature\n      for capacity planning and health monitoring.\n      Sensor path: /junos/system/\n    subscribe:\n      operationId: onSystemResources\n      summary: System resource utilization telemetry stream\n      message:\n        $ref: '#/components/messages/SystemResourceMessage'\n  /firewall:\n    description: >-\n      Channel for firewall filter counter telemetry. Provides real-time\n      packet and byte counts for configured firewall filter terms.\n      Sensor path: /junos/system/linecard/firewall/\n    subscribe:\n     \
  \ operationId: onFirewallCounters\n      summary: Firewall filter counter telemetry stream\n      message:\n        $ref: '#/components/messages/FirewallMessage'\n  /optics:\n    description: >-\n      Channel for optical transceiver diagnostics. Reports real-time\n      optical power levels, laser bias current, temperature, and voltage\n      for SFP/QSFP transceivers. Used for proactive link failure detection.\n      Sensor path: /junos/system/linecard/optics/\n    subscribe:\n      operationId: onOpticsDiagnostics\n      summary: Optical diagnostics telemetry stream\n      message:\n        $ref: '#/components/messages/OpticsMessage'\ncomponents:\n  messages:\n    InterfaceStatsMessage:\n      name: InterfaceStatsMessage\n      title: Interface Statistics Telemetry\n      summary: >-\n        Real-time interface counter data including ingress/egress packet\n        and byte counts, error counters, and queue statistics. Published\n        at the configured reporting rate (typically 2-30\
  \ seconds).\n      contentType: application/x-protobuf\n      payload:\n        type: object\n        properties:\n          system_id:\n            type: string\n            description: Device hostname or system identifier.\n          component_id:\n            type: integer\n            description: Line card slot number.\n          sensor_name:\n            type: string\n            description: Sensor resource path.\n          sequence_number:\n            type: integer\n            description: Monotonically increasing sequence number.\n          timestamp:\n            type: integer\n            description: Data collection timestamp in milliseconds since epoch.\n          interface_stats:\n            type: array\n            items:\n              type: object\n              properties:\n                if_name:\n                  type: string\n                  description: Interface name (e.g., et-0/0/0).\n                init_time:\n                  type: integer\n        \
  \          description: Interface initialization time.\n                snmp_if_index:\n                  type: integer\n                  description: SNMP interface index.\n                ingress_stats:\n                  type: object\n                  properties:\n                    if_pkts:\n                      type: integer\n                      description: Total ingress packets.\n                    if_octets:\n                      type: integer\n                      description: Total ingress bytes.\n                    if_ucast_pkts:\n                      type: integer\n                      description: Unicast packets received.\n                    if_mcast_pkts:\n                      type: integer\n                      description: Multicast packets received.\n                    if_errors:\n                      type: integer\n                      description: Ingress error count.\n                    if_discards:\n                      type: integer\n        \
  \              description: Ingress discard count.\n                egress_stats:\n                  type: object\n                  properties:\n                    if_pkts:\n                      type: integer\n                      description: Total egress packets.\n                    if_octets:\n                      type: integer\n                      description: Total egress bytes.\n                    if_ucast_pkts:\n                      type: integer\n                    if_mcast_pkts:\n                      type: integer\n                    if_errors:\n                      type: integer\n                    if_discards:\n                      type: integer\n                egress_queue_info:\n                  type: array\n                  items:\n                    type: object\n                    properties:\n                      queue_number:\n                        type: integer\n                      packets:\n                        type: integer\n          \
  \            bytes:\n                        type: integer\n                      tail_drop_packets:\n                        type: integer\n                      red_drop_packets:\n                        type: integer\n                  description: Per-queue egress statistics.\n                op_state:\n                  type: string\n                  enum:\n                    - up\n                    - down\n                  description: Interface operational state.\n    RoutingMessage:\n      name: RoutingMessage\n      title: Routing Protocol Telemetry\n      summary: >-\n        BGP session state and route count telemetry data. Reports peer\n        session transitions, received/advertised prefix counts, and\n        route table summary statistics.\n      contentType: application/x-protobuf\n      payload:\n        type: object\n        properties:\n          system_id:\n            type: string\n          timestamp:\n            type: integer\n          bgp_peers:\n      \
  \      type: array\n            items:\n              type: object\n              properties:\n                peer_address:\n                  type: string\n                  description: BGP peer IP address.\n                peer_as:\n                  type: integer\n                  description: BGP peer autonomous system number.\n                local_as:\n                  type: integer\n                  description: Local autonomous system number.\n                peer_state:\n                  type: string\n                  enum:\n                    - established\n                    - active\n                    - idle\n                    - connect\n                    - openconfirm\n                    - opensent\n                  description: BGP session state.\n                received_prefixes:\n                  type: integer\n                  description: Number of prefixes received from peer.\n                accepted_prefixes:\n                  type: integer\n \
  \                 description: Number of prefixes accepted from peer.\n                advertised_prefixes:\n                  type: integer\n                  description: Number of prefixes advertised to peer.\n                up_time:\n                  type: integer\n                  description: Session uptime in seconds.\n                last_error:\n                  type: string\n                  description: Last BGP notification error message.\n    SystemResourceMessage:\n      name: SystemResourceMessage\n      title: System Resource Telemetry\n      summary: >-\n        System resource utilization data including CPU, memory, and\n        temperature readings from routing engines and line cards.\n      contentType: application/x-protobuf\n      payload:\n        type: object\n        properties:\n          system_id:\n            type: string\n          timestamp:\n            type: integer\n          routing_engine:\n            type: array\n            items:\n         \
  \     type: object\n              properties:\n                slot:\n                  type: integer\n                  description: Routing engine slot number.\n                cpu_idle:\n                  type: number\n                  description: CPU idle percentage.\n                cpu_user:\n                  type: number\n                  description: CPU user-space percentage.\n                cpu_system:\n                  type: number\n                  description: CPU system percentage.\n                memory_total:\n                  type: integer\n                  description: Total memory in bytes.\n                memory_used:\n                  type: integer\n                  description: Used memory in bytes.\n                memory_buffer:\n                  type: integer\n                  description: Buffer memory in bytes.\n                temperature:\n                  type: number\n                  description: Routing engine temperature in Celsius.\n\
  \                uptime:\n                  type: integer\n                  description: Routing engine uptime in seconds.\n    FirewallMessage:\n      name: FirewallMessage\n      title: Firewall Filter Counter Telemetry\n      summary: >-\n        Real-time firewall filter counter data for configured filter terms.\n        Reports packet and byte match counts per filter term.\n      contentType: application/x-protobuf\n      payload:\n        type: object\n        properties:\n          system_id:\n            type: string\n          timestamp:\n            type: integer\n          firewall_stats:\n            type: array\n            items:\n              type: object\n              properties:\n                filter_name:\n                  type: string\n                  description: Firewall filter name.\n                counter_name:\n                  type: string\n                  description: Counter term name.\n                packets:\n                  type: integer\n \
  \                 description: Matched packet count.\n                bytes:\n                  type: integer\n                  description: Matched byte count.\n    OpticsMessage:\n      name: OpticsMessage\n      title: Optical Transceiver Diagnostics Telemetry\n      summary: >-\n        Optical transceiver diagnostic readings including power levels,\n        bias current, temperature, and voltage for SFP/QSFP modules.\n      contentType: application/x-protobuf\n      payload:\n        type: object\n        properties:\n          system_id:\n            type: string\n          timestamp:\n            type: integer\n          optics_diag:\n            type: array\n            items:\n              type: object\n              properties:\n                if_name:\n                  type: string\n                  description: Interface name.\n                module_temperature:\n                  type: number\n                  description: Module temperature in Celsius.\n          \
  \      module_voltage:\n                  type: number\n                  description: Module supply voltage in volts.\n                lanes:\n                  type: array\n                  items:\n                    type: object\n                    properties:\n                      lane_number:\n                        type: integer\n                      laser_output_power_dbm:\n                        type: number\n                        description: Laser output power in dBm.\n                      laser_rx_power_dbm:\n                        type: number\n                        description: Receiver input power in dBm.\n                      laser_bias_current_ma:\n                        type: number\n                        description: Laser bias current in milliamps.\n                      laser_output_power_high_alarm:\n                        type: boolean\n                      laser_rx_power_low_alarm:\n                        type: boolean\n                  description:\
  \ Per-lane optical diagnostics.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/juniper-networks/refs/heads/main/asyncapi/juniper-networks-junos-telemetry-asyncapi.yml
spec_file: asyncapi/juniper-networks-junos-telemetry-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/juniper-networks/refs/heads/main/asyncapi/juniper-networks-junos-telemetry-asyncapi.yml
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
