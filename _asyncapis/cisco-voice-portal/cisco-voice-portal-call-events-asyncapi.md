---
api_specs:
- filename: cisco-voice-portal-call-control-openapi.yml
  format: yaml
  label: Cisco Voice Portal Call Control API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/cisco-voice-portal/refs/heads/main/openapi/cisco-voice-portal-call-control-openapi.yml
- filename: cisco-voice-portal-reporting-openapi.yml
  format: yaml
  label: Cisco Voice Portal Reporting API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/cisco-voice-portal/refs/heads/main/openapi/cisco-voice-portal-reporting-openapi.yml
- filename: cisco-voice-portal-administration-openapi.yml
  format: yaml
  label: Cisco Voice Portal Administration API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/cisco-voice-portal/refs/heads/main/openapi/cisco-voice-portal-administration-openapi.yml
- filename: cisco-voice-portal-vxml-services-openapi.yml
  format: yaml
  label: Cisco Voice Portal VXML Services API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/cisco-voice-portal/refs/heads/main/openapi/cisco-voice-portal-vxml-services-openapi.yml
- filename: cisco-voice-portal-call-events-asyncapi.yml
  format: yaml
  label: Cisco Voice Portal Call Events API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/cisco-voice-portal/refs/heads/main/asyncapi/cisco-voice-portal-call-events-asyncapi.yml
channels:
- description: Published when a new call is received by the CVP Call Server. This event is generated after the initial SIP INVITE is processed and a call GUID is assigned.
  name: cvp/calls/started
  operation: subscribe
  operation_id: onCallStarted
  summary: Receive call started events
- description: Published when a call is terminated. Includes the final call disposition, duration, and summary of the call treatment.
  name: cvp/calls/ended
  operation: subscribe
  operation_id: onCallEnded
  summary: Receive call ended events
- description: Published when a call is transferred to another destination, such as an agent queue, external number, or another application.
  name: cvp/calls/transferred
  operation: subscribe
  operation_id: onCallTransferred
  summary: Receive call transfer events
- description: Published when a call enters a queue waiting for an agent. This event is generated when ICM/UCCE routes the call to a skill group and the call is placed in queue.
  name: cvp/calls/queued
  operation: subscribe
  operation_id: onCallQueued
  summary: Receive call queued events
- description: Published when a VXML application is invoked to handle a call. This occurs when the Call Server sends the call to a VXML Server for self-service treatment.
  name: cvp/calls/application-invoked
  operation: subscribe
  operation_id: onApplicationInvoked
  summary: Receive application invocation events
- description: Published when a call processing error occurs, such as a SIP failure, VXML application error, or ICM communication failure.
  name: cvp/calls/error
  operation: subscribe
  operation_id: onCallError
  summary: Receive call error events
- description: Published when the status of a managed CVP device changes, such as transitioning from online to offline or entering maintenance mode.
  name: cvp/system/device-status-changed
  operation: subscribe
  operation_id: onDeviceStatusChanged
  summary: Receive device status change events
- description: Published when a monitored system threshold is exceeded, such as concurrent call limits, CPU usage, memory usage, or disk space. These events correspond to SNMP traps that CVP generates.
  name: cvp/system/threshold-exceeded
  operation: subscribe
  operation_id: onThresholdExceeded
  summary: Receive threshold exceeded alerts
- description: Published when a CVP service starts, stops, or encounters an error. Monitors service health across the deployment.
  name: cvp/system/service-state-changed
  operation: subscribe
  operation_id: onServiceStateChanged
  summary: Receive service state change events
- description: Published when a configuration deployment operation completes, either successfully or with errors.
  name: cvp/deployment/config-deployed
  operation: subscribe
  operation_id: onConfigDeployed
  summary: Receive deployment completion events
description: The Cisco Unified Customer Voice Portal (CVP) generates real-time events during call processing that can be consumed for monitoring, analytics, and integration purposes. CVP publishes call lifecycle events, system alerts, and operational notifications through multiple channels including JMS messaging, SNMP traps, and syslog. This specification documents the event-driven interfaces for consuming CVP call processing events and system notifications.
layout: asyncapi
messages:
- description: ''
  name: CallStartedEvent
  summary: A new call has been received by CVP
  title: Call Started
- description: ''
  name: CallEndedEvent
  summary: A call has been terminated
  title: Call Ended
- description: ''
  name: CallTransferredEvent
  summary: A call has been transferred to a new destination
  title: Call Transferred
- description: ''
  name: CallQueuedEvent
  summary: A call has been placed in an agent queue
  title: Call Queued
- description: ''
  name: ApplicationInvokedEvent
  summary: A VXML application has been invoked to handle a call
  title: Application Invoked
- description: ''
  name: CallErrorEvent
  summary: A call processing error has occurred
  title: Call Error
- description: ''
  name: DeviceStatusChangedEvent
  summary: A managed device status has changed
  title: Device Status Changed
- description: ''
  name: ThresholdExceededEvent
  summary: A system monitoring threshold has been exceeded
  title: Threshold Exceeded
- description: ''
  name: ServiceStateChangedEvent
  summary: A CVP service has changed state
  title: Service State Changed
- description: ''
  name: ConfigDeployedEvent
  summary: A configuration deployment operation has completed
  title: Configuration Deployed
name: Cisco Voice Portal Call Events API
provider_name: Cisco Voice Portal
provider_slug: cisco-voice-portal
servers:
- description: CVP JMS message broker for call event notifications. The CVP Call Server and VXML Server publish events to JMS topics that can be consumed by external applications.
  name: jms
  protocol: jms
  url: tcp://{cvp-server}:61616
- description: Syslog endpoint for receiving CVP system events and alerts. CVP components forward structured syslog messages for operational events.
  name: syslog
  protocol: syslog
  url: udp://{syslog-server}:514
slug: cisco-voice-portal-call-events-asyncapi
source_filename: cisco-voice-portal-call-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Cisco Voice Portal Call Events API\n  version: 12.6.0\n  description: >-\n    The Cisco Unified Customer Voice Portal (CVP) generates real-time events\n    during call processing that can be consumed for monitoring, analytics, and\n    integration purposes. CVP publishes call lifecycle events, system alerts,\n    and operational notifications through multiple channels including JMS\n    messaging, SNMP traps, and syslog. This specification documents the\n    event-driven interfaces for consuming CVP call processing events and\n    system notifications.\n  contact:\n    name: Cisco Developer Support\n    url: https://developer.cisco.com/\n  license:\n    name: Cisco DevNet\n    url: https://developer.cisco.com/site/license/\nservers:\n  jms:\n    url: tcp://{cvp-server}:61616\n    protocol: jms\n    description: >-\n      CVP JMS message broker for call event notifications. The CVP Call Server\n      and VXML Server publish events to JMS topics\
  \ that can be consumed by\n      external applications.\n    variables:\n      cvp-server:\n        default: cvp-callserver.example.com\n        description: Hostname or IP of the CVP server running the JMS broker\n  syslog:\n    url: udp://{syslog-server}:514\n    protocol: syslog\n    description: >-\n      Syslog endpoint for receiving CVP system events and alerts. CVP\n      components forward structured syslog messages for operational events.\n    variables:\n      syslog-server:\n        default: syslog.example.com\n        description: Hostname or IP of the syslog receiver\nchannels:\n  cvp/calls/started:\n    description: >-\n      Published when a new call is received by the CVP Call Server. This\n      event is generated after the initial SIP INVITE is processed and a\n      call GUID is assigned.\n    subscribe:\n      operationId: onCallStarted\n      summary: Receive call started events\n      message:\n        $ref: '#/components/messages/CallStartedEvent'\n  cvp/calls/ended:\n\
  \    description: >-\n      Published when a call is terminated. Includes the final call\n      disposition, duration, and summary of the call treatment.\n    subscribe:\n      operationId: onCallEnded\n      summary: Receive call ended events\n      message:\n        $ref: '#/components/messages/CallEndedEvent'\n  cvp/calls/transferred:\n    description: >-\n      Published when a call is transferred to another destination, such as\n      an agent queue, external number, or another application.\n    subscribe:\n      operationId: onCallTransferred\n      summary: Receive call transfer events\n      message:\n        $ref: '#/components/messages/CallTransferredEvent'\n  cvp/calls/queued:\n    description: >-\n      Published when a call enters a queue waiting for an agent. This event\n      is generated when ICM/UCCE routes the call to a skill group and the\n      call is placed in queue.\n    subscribe:\n      operationId: onCallQueued\n      summary: Receive call queued events\n    \
  \  message:\n        $ref: '#/components/messages/CallQueuedEvent'\n  cvp/calls/application-invoked:\n    description: >-\n      Published when a VXML application is invoked to handle a call. This\n      occurs when the Call Server sends the call to a VXML Server for\n      self-service treatment.\n    subscribe:\n      operationId: onApplicationInvoked\n      summary: Receive application invocation events\n      message:\n        $ref: '#/components/messages/ApplicationInvokedEvent'\n  cvp/calls/error:\n    description: >-\n      Published when a call processing error occurs, such as a SIP failure,\n      VXML application error, or ICM communication failure.\n    subscribe:\n      operationId: onCallError\n      summary: Receive call error events\n      message:\n        $ref: '#/components/messages/CallErrorEvent'\n  cvp/system/device-status-changed:\n    description: >-\n      Published when the status of a managed CVP device changes, such as\n      transitioning from online to offline\
  \ or entering maintenance mode.\n    subscribe:\n      operationId: onDeviceStatusChanged\n      summary: Receive device status change events\n      message:\n        $ref: '#/components/messages/DeviceStatusChangedEvent'\n  cvp/system/threshold-exceeded:\n    description: >-\n      Published when a monitored system threshold is exceeded, such as\n      concurrent call limits, CPU usage, memory usage, or disk space.\n      These events correspond to SNMP traps that CVP generates.\n    subscribe:\n      operationId: onThresholdExceeded\n      summary: Receive threshold exceeded alerts\n      message:\n        $ref: '#/components/messages/ThresholdExceededEvent'\n  cvp/system/service-state-changed:\n    description: >-\n      Published when a CVP service starts, stops, or encounters an error.\n      Monitors service health across the deployment.\n    subscribe:\n      operationId: onServiceStateChanged\n      summary: Receive service state change events\n      message:\n        $ref: '#/components/messages/ServiceStateChangedEvent'\n\
  \  cvp/deployment/config-deployed:\n    description: >-\n      Published when a configuration deployment operation completes,\n      either successfully or with errors.\n    subscribe:\n      operationId: onConfigDeployed\n      summary: Receive deployment completion events\n      message:\n        $ref: '#/components/messages/ConfigDeployedEvent'\ncomponents:\n  messages:\n    CallStartedEvent:\n      name: CallStartedEvent\n      title: Call Started\n      summary: A new call has been received by CVP\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: call.started\n          timestamp:\n            type: string\n            format: date-time\n          callGuid:\n            type: string\n            description: Globally unique call identifier\n          callingNumber:\n            type: string\n            description: Caller ANI\n          calledNumber:\n            type:\
  \ string\n            description: Called DNIS\n          callServerHostname:\n            type: string\n            description: Call Server handling the call\n          sipCallId:\n            type: string\n            description: SIP Call-ID\n          ingressGateway:\n            type: string\n            description: SIP endpoint that sent the call to CVP\n          matchedPattern:\n            type: string\n            description: Dialed number pattern that matched\n        required:\n          - eventType\n          - timestamp\n          - callGuid\n          - callingNumber\n          - calledNumber\n    CallEndedEvent:\n      name: CallEndedEvent\n      title: Call Ended\n      summary: A call has been terminated\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: call.ended\n          timestamp:\n            type: string\n            format: date-time\n         \
  \ callGuid:\n            type: string\n          callingNumber:\n            type: string\n          calledNumber:\n            type: string\n          callResult:\n            type: string\n            enum:\n              - completed\n              - abandoned\n              - transferred\n              - error\n          callDuration:\n            type: integer\n            description: Total call duration in seconds\n          selfServiceDuration:\n            type: integer\n            description: Self-service IVR duration in seconds\n          queueDuration:\n            type: integer\n            description: Queue wait time in seconds\n          applicationName:\n            type: string\n          terminationReason:\n            type: string\n            description: Reason the call ended\n          sipResponseCode:\n            type: integer\n            description: Final SIP response code\n        required:\n          - eventType\n          - timestamp\n          - callGuid\n\
  \          - callResult\n    CallTransferredEvent:\n      name: CallTransferredEvent\n      title: Call Transferred\n      summary: A call has been transferred to a new destination\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: call.transferred\n          timestamp:\n            type: string\n            format: date-time\n          callGuid:\n            type: string\n          callingNumber:\n            type: string\n          calledNumber:\n            type: string\n          transferDestination:\n            type: string\n            description: Transfer target number or URI\n          transferType:\n            type: string\n            enum:\n              - blind\n              - consultation\n          icmLabel:\n            type: string\n            description: ICM routing label for the transfer\n          skillGroup:\n            type: string\n            description:\
  \ Target skill group if agent-bound\n        required:\n          - eventType\n          - timestamp\n          - callGuid\n          - transferDestination\n    CallQueuedEvent:\n      name: CallQueuedEvent\n      title: Call Queued\n      summary: A call has been placed in an agent queue\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: call.queued\n          timestamp:\n            type: string\n            format: date-time\n          callGuid:\n            type: string\n          callingNumber:\n            type: string\n          calledNumber:\n            type: string\n          skillGroup:\n            type: string\n            description: Skill group the call is queued for\n          estimatedWaitTime:\n            type: integer\n            description: Estimated wait time in seconds (if available)\n          queuePosition:\n            type: integer\n           \
  \ description: Position in the queue\n          queueApplication:\n            type: string\n            description: Queue treatment application being played\n        required:\n          - eventType\n          - timestamp\n          - callGuid\n    ApplicationInvokedEvent:\n      name: ApplicationInvokedEvent\n      title: Application Invoked\n      summary: A VXML application has been invoked to handle a call\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: call.application_invoked\n          timestamp:\n            type: string\n            format: date-time\n          callGuid:\n            type: string\n          applicationName:\n            type: string\n            description: Name of the invoked VXML application\n          vxmlServerHostname:\n            type: string\n            description: VXML Server executing the application\n          sessionId:\n       \
  \     type: string\n            description: VXML session identifier\n        required:\n          - eventType\n          - timestamp\n          - callGuid\n          - applicationName\n    CallErrorEvent:\n      name: CallErrorEvent\n      title: Call Error\n      summary: A call processing error has occurred\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: call.error\n          timestamp:\n            type: string\n            format: date-time\n          callGuid:\n            type: string\n          errorCode:\n            type: string\n            description: CVP error code\n          errorMessage:\n            type: string\n            description: Human-readable error description\n          errorCategory:\n            type: string\n            enum:\n              - sip_failure\n              - vxml_error\n              - icm_communication\n              - application_error\n\
  \              - timeout\n              - system_error\n          serverHostname:\n            type: string\n            description: Server where the error occurred\n          sipResponseCode:\n            type: integer\n            description: SIP response code if applicable\n        required:\n          - eventType\n          - timestamp\n          - errorCode\n          - errorCategory\n    DeviceStatusChangedEvent:\n      name: DeviceStatusChangedEvent\n      title: Device Status Changed\n      summary: A managed device status has changed\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: system.device_status_changed\n          timestamp:\n            type: string\n            format: date-time\n          deviceId:\n            type: string\n          hostname:\n            type: string\n          deviceType:\n            type: string\n            enum:\n             \
  \ - CallServer\n              - VXMLServer\n              - ReportingServer\n              - MediaServer\n          previousStatus:\n            type: string\n            enum:\n              - online\n              - offline\n              - maintenance\n              - error\n          currentStatus:\n            type: string\n            enum:\n              - online\n              - offline\n              - maintenance\n              - error\n          reason:\n            type: string\n            description: Reason for the status change\n        required:\n          - eventType\n          - timestamp\n          - deviceId\n          - previousStatus\n          - currentStatus\n    ThresholdExceededEvent:\n      name: ThresholdExceededEvent\n      title: Threshold Exceeded\n      summary: A system monitoring threshold has been exceeded\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventType:\n            type: string\n\
  \            const: system.threshold_exceeded\n          timestamp:\n            type: string\n            format: date-time\n          deviceId:\n            type: string\n          hostname:\n            type: string\n          metric:\n            type: string\n            enum:\n              - concurrent_calls\n              - cpu_usage\n              - memory_usage\n              - disk_usage\n              - call_error_rate\n              - sip_response_time\n            description: Metric that exceeded the threshold\n          thresholdValue:\n            type: number\n            description: Configured threshold value\n          currentValue:\n            type: number\n            description: Current metric value\n          severity:\n            type: string\n            enum:\n              - warning\n              - critical\n        required:\n          - eventType\n          - timestamp\n          - metric\n          - thresholdValue\n          - currentValue\n       \
  \   - severity\n    ServiceStateChangedEvent:\n      name: ServiceStateChangedEvent\n      title: Service State Changed\n      summary: A CVP service has changed state\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: system.service_state_changed\n          timestamp:\n            type: string\n            format: date-time\n          deviceId:\n            type: string\n          hostname:\n            type: string\n          serviceName:\n            type: string\n            description: Name of the CVP service\n          previousState:\n            type: string\n            enum:\n              - running\n              - stopped\n              - error\n          currentState:\n            type: string\n            enum:\n              - running\n              - stopped\n              - error\n          message:\n            type: string\n        required:\n          - eventType\n\
  \          - timestamp\n          - serviceName\n          - previousState\n          - currentState\n    ConfigDeployedEvent:\n      name: ConfigDeployedEvent\n      title: Configuration Deployed\n      summary: A configuration deployment operation has completed\n      contentType: application/json\n      payload:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: deployment.config_deployed\n          timestamp:\n            type: string\n            format: date-time\n          operationId:\n            type: string\n          status:\n            type: string\n            enum:\n              - success\n              - partial_success\n              - failed\n          targetDevices:\n            type: array\n            items:\n              type: object\n              properties:\n                deviceId:\n                  type: string\n                hostname:\n                  type: string\n                status:\n\
  \                  type: string\n                  enum:\n                    - success\n                    - failed\n                message:\n                  type: string\n          initiatedBy:\n            type: string\n            description: Username of the administrator who initiated the deployment\n        required:\n          - eventType\n          - timestamp\n          - operationId\n          - status\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cisco-voice-portal/refs/heads/main/asyncapi/cisco-voice-portal-call-events-asyncapi.yml
spec_file: asyncapi/cisco-voice-portal-call-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/cisco-voice-portal/refs/heads/main/asyncapi/cisco-voice-portal-call-events-asyncapi.yml
tags:
- Contact Center
- IVR
- Telephony
- Voice
- VXML
- AsyncAPI
- Webhooks
- Events
version: 12.6.0
---
