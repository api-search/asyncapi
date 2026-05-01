---
api_specs:
- filename: openapi
  format: yaml
  label: Red Hat OpenShift API
  slug: ''
  spec_type: OpenAPI
  url: https://api.openshift.com/api/clusters_mgmt/v1/openapi
- filename: openapi
  format: yaml
  label: Red Hat OpenShift Cluster Manager API
  slug: ''
  spec_type: OpenAPI
  url: https://api.openshift.com/api/clusters_mgmt/v1/openapi
- filename: red-hat-ansible-automation-platform-openapi.yml
  format: yaml
  label: Red Hat Ansible Automation Platform API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/openapi/red-hat-ansible-automation-platform-openapi.yml
- filename: discovery
  format: yaml
  label: Red Hat Quay API
  slug: ''
  spec_type: OpenAPI
  url: https://quay.io/api/v1/discovery
- filename: red-hat-insights-openapi.yml
  format: yaml
  label: Red Hat Insights API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/openapi/red-hat-insights-openapi.yml
- filename: red-hat-satellite-openapi.yml
  format: yaml
  label: Red Hat Satellite API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/openapi/red-hat-satellite-openapi.yml
- filename: red-hat-keycloak-admin-openapi.yml
  format: yaml
  label: Red Hat Build of Keycloak Admin REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/openapi/red-hat-keycloak-admin-openapi.yml
- filename: red-hat-kafka-bridge-asyncapi.yml
  format: yaml
  label: Red Hat Streams for Apache Kafka Bridge API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/asyncapi/red-hat-kafka-bridge-asyncapi.yml
- filename: red-hat-notifications-webhooks-asyncapi.yml
  format: yaml
  label: Red Hat Notifications API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/asyncapi/red-hat-notifications-webhooks-asyncapi.yml
- filename: openapi
  format: yaml
  label: Red Hat Assisted Installer API
  slug: ''
  spec_type: OpenAPI
  url: https://api.openshift.com/api/assisted-install/v2/openapi
channels:
- description: Triggered when the Advisor service identifies a new recommendation for one or more registered RHEL systems based on rule evaluation.
  name: advisor.newRecommendation
  operation: subscribe
  operation_id: onAdvisorNewRecommendation
  summary: New advisor recommendation
- description: Triggered when an Advisor recommendation is resolved on systems, either through remediation or configuration change.
  name: advisor.resolvedRecommendation
  operation: subscribe
  operation_id: onAdvisorResolvedRecommendation
  summary: Advisor recommendation resolved
- description: Triggered when a new CVE is detected affecting registered systems through the Vulnerability service.
  name: vulnerability.newCve
  operation: subscribe
  operation_id: onVulnerabilityNewCve
  summary: New CVE detected
- description: Triggered when the severity rating of a CVE affecting registered systems changes.
  name: vulnerability.cveSeverityChange
  operation: subscribe
  operation_id: onVulnerabilityCveSeverityChange
  summary: CVE severity changed
- description: Triggered when a system fails compliance against an assigned SCAP policy profile.
  name: compliance.policyViolation
  operation: subscribe
  operation_id: onCompliancePolicyViolation
  summary: Compliance policy violation
- description: Triggered when new errata advisories become applicable to registered systems through the Patch service.
  name: patch.newAdvisory
  operation: subscribe
  operation_id: onPatchNewAdvisory
  summary: New patch advisory
- description: Triggered when a new system is registered with Red Hat Insights through the Inventory service.
  name: inventory.systemRegistered
  operation: subscribe
  operation_id: onInventorySystemRegistered
  summary: System registered
- description: Triggered when a registered system becomes stale after failing to check in within the configured stale period.
  name: inventory.systemBecameStale
  operation: subscribe
  operation_id: onInventorySystemBecameStale
  summary: System became stale
description: The Red Hat Hybrid Cloud Console notifications service delivers event-driven notifications when significant events occur across Insights services, including advisor recommendations, vulnerability alerts, compliance changes, patch advisories, and inventory updates. Events can be forwarded via webhook integrations to third-party applications, email notifications, or integration endpoints such as Splunk, ServiceNow, and PagerDuty.
layout: asyncapi
messages:
- description: Payload delivered when the Advisor service identifies a new recommendation for one or more registered RHEL systems.
  name: AdvisorRecommendationEvent
  summary: A new Advisor recommendation was identified for systems.
  title: Advisor New Recommendation Event
- description: ''
  name: AdvisorResolvedEvent
  summary: An Advisor recommendation was resolved.
  title: Advisor Recommendation Resolved Event
- description: ''
  name: VulnerabilityNewCveEvent
  summary: A new CVE was detected affecting systems.
  title: New CVE Detected Event
- description: ''
  name: VulnerabilitySeverityChangeEvent
  summary: A CVE severity rating was changed.
  title: CVE Severity Change Event
- description: ''
  name: CompliancePolicyViolationEvent
  summary: A compliance policy violation was detected.
  title: Compliance Policy Violation Event
- description: ''
  name: PatchNewAdvisoryEvent
  summary: New patch advisories are available for systems.
  title: New Patch Advisory Event
- description: ''
  name: InventorySystemRegisteredEvent
  summary: A new system was registered with Insights.
  title: System Registered Event
- description: ''
  name: InventorySystemStaleEvent
  summary: A system became stale after missing check-ins.
  title: System Became Stale Event
name: Red Hat Hybrid Cloud Console Notifications Events
provider_name: Red Hat
provider_slug: red-hat
servers:
- description: Red Hat Hybrid Cloud Console notifications service. Events are delivered as HTTP POST requests to configured webhook endpoints when subscribed events occur across Insights services.
  name: hybridCloudConsole
  protocol: https
  url: https://console.redhat.com
slug: red-hat-notifications-webhooks-asyncapi
source_filename: red-hat-notifications-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Red Hat Hybrid Cloud Console Notifications Events\n  description: >-\n    The Red Hat Hybrid Cloud Console notifications service delivers event-driven\n    notifications when significant events occur across Insights services,\n    including advisor recommendations, vulnerability alerts, compliance changes,\n    patch advisories, and inventory updates. Events can be forwarded via\n    webhook integrations to third-party applications, email notifications,\n    or integration endpoints such as Splunk, ServiceNow, and PagerDuty.\n  version: '1.0'\n  contact:\n    name: Red Hat Support\n    url: https://access.redhat.com/support\n  license:\n    name: Red Hat Terms of Use\n    url: https://www.redhat.com/en/about/terms-use\nservers:\n  hybridCloudConsole:\n    url: https://console.redhat.com\n    protocol: https\n    description: >-\n      Red Hat Hybrid Cloud Console notifications service. Events are delivered\n      as HTTP POST requests to configured\
  \ webhook endpoints when subscribed\n      events occur across Insights services.\n    security:\n      - bearerAuth: []\ndefaultContentType: application/json\nchannels:\n  advisor.newRecommendation:\n    description: >-\n      Triggered when the Advisor service identifies a new recommendation for\n      one or more registered RHEL systems based on rule evaluation.\n    subscribe:\n      operationId: onAdvisorNewRecommendation\n      summary: New advisor recommendation\n      description: >-\n        Receives a notification when a new Advisor recommendation becomes active\n        for registered systems, indicating a configuration risk, security\n        issue, or performance concern.\n      tags:\n        - name: Advisor\n        - name: Insights Events\n      message:\n        $ref: '#/components/messages/AdvisorRecommendationEvent'\n  advisor.resolvedRecommendation:\n    description: >-\n      Triggered when an Advisor recommendation is resolved on systems, either\n      through remediation\
  \ or configuration change.\n    subscribe:\n      operationId: onAdvisorResolvedRecommendation\n      summary: Advisor recommendation resolved\n      description: >-\n        Receives a notification when a previously active Advisor recommendation\n        is resolved on one or more systems.\n      tags:\n        - name: Advisor\n        - name: Insights Events\n      message:\n        $ref: '#/components/messages/AdvisorResolvedEvent'\n  vulnerability.newCve:\n    description: >-\n      Triggered when a new CVE is detected affecting registered systems\n      through the Vulnerability service.\n    subscribe:\n      operationId: onVulnerabilityNewCve\n      summary: New CVE detected\n      description: >-\n        Receives a notification when the Vulnerability service identifies a\n        new CVE affecting one or more registered RHEL systems.\n      tags:\n        - name: Vulnerability\n        - name: Insights Events\n      message:\n        $ref: '#/components/messages/VulnerabilityNewCveEvent'\n\
  \  vulnerability.cveSeverityChange:\n    description: >-\n      Triggered when the severity rating of a CVE affecting registered\n      systems changes.\n    subscribe:\n      operationId: onVulnerabilityCveSeverityChange\n      summary: CVE severity changed\n      description: >-\n        Receives a notification when the severity of an existing CVE is\n        updated by Red Hat security.\n      tags:\n        - name: Vulnerability\n        - name: Insights Events\n      message:\n        $ref: '#/components/messages/VulnerabilitySeverityChangeEvent'\n  compliance.policyViolation:\n    description: >-\n      Triggered when a system fails compliance against an assigned SCAP\n      policy profile.\n    subscribe:\n      operationId: onCompliancePolicyViolation\n      summary: Compliance policy violation\n      description: >-\n        Receives a notification when a system's compliance scan results\n        indicate a policy violation against an assigned SCAP profile.\n      tags:\n    \
  \    - name: Compliance\n        - name: Insights Events\n      message:\n        $ref: '#/components/messages/CompliancePolicyViolationEvent'\n  patch.newAdvisory:\n    description: >-\n      Triggered when new errata advisories become applicable to registered\n      systems through the Patch service.\n    subscribe:\n      operationId: onPatchNewAdvisory\n      summary: New patch advisory\n      description: >-\n        Receives a notification when new security, bugfix, or enhancement\n        advisories become applicable to registered systems.\n      tags:\n        - name: Patch\n        - name: Insights Events\n      message:\n        $ref: '#/components/messages/PatchNewAdvisoryEvent'\n  inventory.systemRegistered:\n    description: >-\n      Triggered when a new system is registered with Red Hat Insights through\n      the Inventory service.\n    subscribe:\n      operationId: onInventorySystemRegistered\n      summary: System registered\n      description: >-\n        Receives a\
  \ notification when a new RHEL system registers with\n        Red Hat Insights.\n      tags:\n        - name: Inventory\n        - name: Insights Events\n      message:\n        $ref: '#/components/messages/InventorySystemRegisteredEvent'\n  inventory.systemBecameStale:\n    description: >-\n      Triggered when a registered system becomes stale after failing to\n      check in within the configured stale period.\n    subscribe:\n      operationId: onInventorySystemBecameStale\n      summary: System became stale\n      description: >-\n        Receives a notification when a registered system has not checked\n        in and is now considered stale.\n      tags:\n        - name: Inventory\n        - name: Insights Events\n      message:\n        $ref: '#/components/messages/InventorySystemStaleEvent'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: http\n      scheme: bearer\n      description: >-\n        OAuth 2.0 Bearer token for managing notification preferences and\n \
  \       integration configurations through the Hybrid Cloud Console API.\n  messages:\n    AdvisorRecommendationEvent:\n      name: AdvisorRecommendationEvent\n      title: Advisor New Recommendation Event\n      summary: A new Advisor recommendation was identified for systems.\n      description: >-\n        Payload delivered when the Advisor service identifies a new\n        recommendation for one or more registered RHEL systems.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AdvisorRecommendationPayload'\n      examples:\n        - name: NewRecommendation\n          payload:\n            id: evt-abc123\n            bundle: rhel\n            application: advisor\n            event_type: new-recommendation\n            timestamp: '2024-06-15T10:30:00Z'\n            org_id: '12345'\n            events:\n              - metadata: {}\n                payload:\n                  rule_id: network_tcp_keepalive|NETWORK_TCP_KEEPALIVE\n             \
  \     rule_description: TCP keepalive not configured optimally\n                  total_risk: 3\n                  affected_systems: 5\n    AdvisorResolvedEvent:\n      name: AdvisorResolvedEvent\n      title: Advisor Recommendation Resolved Event\n      summary: An Advisor recommendation was resolved.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AdvisorResolvedPayload'\n    VulnerabilityNewCveEvent:\n      name: VulnerabilityNewCveEvent\n      title: New CVE Detected Event\n      summary: A new CVE was detected affecting systems.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/VulnerabilityNewCvePayload'\n      examples:\n        - name: NewCveDetected\n          payload:\n            id: evt-def456\n            bundle: rhel\n            application: vulnerability\n            event_type: new-cve\n            timestamp: '2024-06-15T14:00:00Z'\n            org_id: '12345'\n            events:\n     \
  \         - metadata: {}\n                payload:\n                  cve_id: CVE-2024-1234\n                  severity: Important\n                  affected_systems: 12\n                  synopsis: Buffer overflow in kernel module\n    VulnerabilitySeverityChangeEvent:\n      name: VulnerabilitySeverityChangeEvent\n      title: CVE Severity Change Event\n      summary: A CVE severity rating was changed.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/VulnerabilitySeverityChangePayload'\n    CompliancePolicyViolationEvent:\n      name: CompliancePolicyViolationEvent\n      title: Compliance Policy Violation Event\n      summary: A compliance policy violation was detected.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CompliancePolicyViolationPayload'\n    PatchNewAdvisoryEvent:\n      name: PatchNewAdvisoryEvent\n      title: New Patch Advisory Event\n      summary: New patch advisories are available\
  \ for systems.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PatchNewAdvisoryPayload'\n    InventorySystemRegisteredEvent:\n      name: InventorySystemRegisteredEvent\n      title: System Registered Event\n      summary: A new system was registered with Insights.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/InventorySystemRegisteredPayload'\n    InventorySystemStaleEvent:\n      name: InventorySystemStaleEvent\n      title: System Became Stale Event\n      summary: A system became stale after missing check-ins.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/InventorySystemStalePayload'\n  schemas:\n    NotificationEventBase:\n      type: object\n      description: >-\n        Base structure shared by all Hybrid Cloud Console notification\n        event payloads.\n      required:\n        - id\n        - bundle\n        - application\n        - event_type\n\
  \        - timestamp\n        - org_id\n        - events\n      properties:\n        id:\n          type: string\n          description: Unique identifier for this notification event.\n        bundle:\n          type: string\n          description: The product bundle that generated the event.\n          example: rhel\n        application:\n          type: string\n          description: The Insights application that generated the event.\n          example: advisor\n        event_type:\n          type: string\n          description: The specific event type identifier.\n        timestamp:\n          type: string\n          format: date-time\n          description: The ISO 8601 timestamp when the event occurred.\n        org_id:\n          type: string\n          description: The Red Hat organization ID associated with the event.\n        context:\n          type: object\n          description: Additional context metadata for the event.\n          additionalProperties: true\n        events:\n\
  \          type: array\n          description: The list of sub-events in this notification.\n          items:\n            type: object\n            properties:\n              metadata:\n                type: object\n                additionalProperties: true\n              payload:\n                type: object\n                additionalProperties: true\n    AdvisorRecommendationPayload:\n      allOf:\n        - $ref: '#/components/schemas/NotificationEventBase'\n        - type: object\n          description: Payload for new Advisor recommendation events.\n          properties:\n            events:\n              type: array\n              items:\n                type: object\n                properties:\n                  payload:\n                    type: object\n                    properties:\n                      rule_id:\n                        type: string\n                        description: The Advisor rule identifier.\n                      rule_description:\n         \
  \               type: string\n                        description: A description of what the rule detects.\n                      total_risk:\n                        type: integer\n                        description: The total risk score (1-4).\n                      affected_systems:\n                        type: integer\n                        description: The number of affected systems.\n    AdvisorResolvedPayload:\n      allOf:\n        - $ref: '#/components/schemas/NotificationEventBase'\n        - type: object\n          description: Payload for resolved Advisor recommendation events.\n          properties:\n            events:\n              type: array\n              items:\n                type: object\n                properties:\n                  payload:\n                    type: object\n                    properties:\n                      rule_id:\n                        type: string\n                      resolved_systems:\n                        type: integer\n\
  \    VulnerabilityNewCvePayload:\n      allOf:\n        - $ref: '#/components/schemas/NotificationEventBase'\n        - type: object\n          description: Payload for new CVE detection events.\n          properties:\n            events:\n              type: array\n              items:\n                type: object\n                properties:\n                  payload:\n                    type: object\n                    properties:\n                      cve_id:\n                        type: string\n                        description: The CVE identifier.\n                      severity:\n                        type: string\n                        description: The severity rating.\n                        enum:\n                          - Critical\n                          - Important\n                          - Moderate\n                          - Low\n                      affected_systems:\n                        type: integer\n                      synopsis:\n       \
  \                 type: string\n                        description: A brief description of the vulnerability.\n    VulnerabilitySeverityChangePayload:\n      allOf:\n        - $ref: '#/components/schemas/NotificationEventBase'\n        - type: object\n          description: Payload for CVE severity change events.\n          properties:\n            events:\n              type: array\n              items:\n                type: object\n                properties:\n                  payload:\n                    type: object\n                    properties:\n                      cve_id:\n                        type: string\n                      previous_severity:\n                        type: string\n                      new_severity:\n                        type: string\n    CompliancePolicyViolationPayload:\n      allOf:\n        - $ref: '#/components/schemas/NotificationEventBase'\n        - type: object\n          description: Payload for compliance policy violation events.\n\
  \          properties:\n            events:\n              type: array\n              items:\n                type: object\n                properties:\n                  payload:\n                    type: object\n                    properties:\n                      policy_name:\n                        type: string\n                        description: The name of the compliance policy.\n                      policy_id:\n                        type: string\n                      system_id:\n                        type: string\n                        format: uuid\n                      compliance_score:\n                        type: number\n                        description: The compliance score as a percentage.\n    PatchNewAdvisoryPayload:\n      allOf:\n        - $ref: '#/components/schemas/NotificationEventBase'\n        - type: object\n          description: Payload for new patch advisory events.\n          properties:\n            events:\n              type: array\n   \
  \           items:\n                type: object\n                properties:\n                  payload:\n                    type: object\n                    properties:\n                      advisory_id:\n                        type: string\n                        description: The advisory identifier (e.g., RHSA-2024:1234).\n                      advisory_type:\n                        type: string\n                        enum:\n                          - security\n                          - bugfix\n                          - enhancement\n                      severity:\n                        type: string\n                      affected_systems:\n                        type: integer\n                      synopsis:\n                        type: string\n    InventorySystemRegisteredPayload:\n      allOf:\n        - $ref: '#/components/schemas/NotificationEventBase'\n        - type: object\n          description: Payload for system registration events.\n          properties:\n\
  \            events:\n              type: array\n              items:\n                type: object\n                properties:\n                  payload:\n                    type: object\n                    properties:\n                      system_id:\n                        type: string\n                        format: uuid\n                      display_name:\n                        type: string\n                      rhel_version:\n                        type: string\n    InventorySystemStalePayload:\n      allOf:\n        - $ref: '#/components/schemas/NotificationEventBase'\n        - type: object\n          description: Payload for system stale events.\n          properties:\n            events:\n              type: array\n              items:\n                type: object\n                properties:\n                  payload:\n                    type: object\n                    properties:\n                      system_id:\n                        type: string\n    \
  \                    format: uuid\n                      display_name:\n                        type: string\n                      last_seen:\n                        type: string\n                        format: date-time\n                      stale_since:\n                        type: string\n                        format: date-time\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/asyncapi/red-hat-notifications-webhooks-asyncapi.yml
spec_file: asyncapi/red-hat-notifications-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/red-hat/refs/heads/main/asyncapi/red-hat-notifications-webhooks-asyncapi.yml
tags:
- Cloud
- Containers
- Enterprise
- Hybrid Cloud
- Kubernetes
- Linux
- Open Source
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
