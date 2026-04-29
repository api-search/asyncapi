---
api_specs:
- filename: cyclr-cyclr-openapi.yml
  format: yaml
  label: Cyclr API
  slug: api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/cyclr/refs/heads/main/openapi/cyclr-cyclr-openapi.yml
channels:
- description: Triggered when a cycle is activated and begins running.
  name: cycle.activated
  operation: subscribe
  operation_id: onCycleActivated
  summary: Cycle Activated
- description: Triggered when a running cycle is deactivated.
  name: cycle.deactivated
  operation: subscribe
  operation_id: onCycleDeactivated
  summary: Cycle Deactivated
- description: Triggered when a cycle encounters an error during execution.
  name: cycle.error
  operation: subscribe
  operation_id: onCycleError
  summary: Cycle Error
- description: Triggered when a cycle run completes successfully.
  name: cycle.completed
  operation: subscribe
  operation_id: onCycleCompleted
  summary: Cycle Completed
- description: Triggered when a connector is installed in an account.
  name: connector.installed
  operation: subscribe
  operation_id: onConnectorInstalled
  summary: Connector Installed
- description: Triggered when a connector is removed from an account.
  name: connector.uninstalled
  operation: subscribe
  operation_id: onConnectorUninstalled
  summary: Connector Uninstalled
- description: Triggered when a connector authentication is completed.
  name: connector.authenticated
  operation: subscribe
  operation_id: onConnectorAuthenticated
  summary: Connector Authenticated
- description: Triggered when a new account is created under the partner.
  name: account.created
  operation: subscribe
  operation_id: onAccountCreated
  summary: Account Created
- description: Triggered when an account is deleted.
  name: account.deleted
  operation: subscribe
  operation_id: onAccountDeleted
  summary: Account Deleted
- description: Triggered when a template is installed into an account.
  name: template.installed
  operation: subscribe
  operation_id: onTemplateInstalled
  summary: Template Installed
- description: Triggered when an individual step within a cycle encounters an error.
  name: step.error
  operation: subscribe
  operation_id: onStepError
  summary: Step Error
description: AsyncAPI specification for Cyclr webhook events. Cyclr is an embedded iPaaS/integration platform that emits webhook notifications when key events occur within accounts, cycles, connectors, and templates. These events enable real-time monitoring of integration lifecycle changes.
layout: asyncapi
messages:
- description: ''
  name: CycleStatusChanged
  summary: ''
  title: CycleStatusChanged
- description: ''
  name: CycleError
  summary: ''
  title: CycleError
- description: ''
  name: ConnectorEvent
  summary: ''
  title: ConnectorEvent
- description: ''
  name: AccountEvent
  summary: ''
  title: AccountEvent
- description: ''
  name: TemplateEvent
  summary: ''
  title: TemplateEvent
- description: ''
  name: StepError
  summary: ''
  title: StepError
name: Cyclr Webhook Events
provider_name: Cyclr
provider_slug: cyclr
servers:
- description: Cyclr US webhook delivery endpoint
  name: us
  protocol: https
  url: https://api.cyclr.com
- description: Cyclr EU webhook delivery endpoint
  name: eu
  protocol: https
  url: https://api.eu.cyclr.com
- description: Cyclr AU webhook delivery endpoint
  name: au
  protocol: https
  url: https://api.au.cyclr.com
slug: cyclr-cyclr-asyncapi
source_filename: cyclr-cyclr-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Cyclr Webhook Events\n  version: 1.0.0\n  description: >-\n    AsyncAPI specification for Cyclr webhook events. Cyclr is an embedded\n    iPaaS/integration platform that emits webhook notifications when key\n    events occur within accounts, cycles, connectors, and templates. These\n    events enable real-time monitoring of integration lifecycle changes.\n  contact:\n    name: Cyclr\n    url: https://cyclr.com\n  license:\n    name: Proprietary\n    url: https://cyclr.com/legal\nservers:\n  us:\n    url: https://api.cyclr.com\n    protocol: https\n    description: Cyclr US webhook delivery endpoint\n  eu:\n    url: https://api.eu.cyclr.com\n    protocol: https\n    description: Cyclr EU webhook delivery endpoint\n  au:\n    url: https://api.au.cyclr.com\n    protocol: https\n    description: Cyclr AU webhook delivery endpoint\nchannels:\n  cycle.activated:\n    description: Triggered when a cycle is activated and begins running.\n    subscribe:\n\
  \      operationId: onCycleActivated\n      summary: Cycle Activated\n      message:\n        $ref: '#/components/messages/CycleStatusChanged'\n  cycle.deactivated:\n    description: Triggered when a running cycle is deactivated.\n    subscribe:\n      operationId: onCycleDeactivated\n      summary: Cycle Deactivated\n      message:\n        $ref: '#/components/messages/CycleStatusChanged'\n  cycle.error:\n    description: Triggered when a cycle encounters an error during execution.\n    subscribe:\n      operationId: onCycleError\n      summary: Cycle Error\n      message:\n        $ref: '#/components/messages/CycleError'\n  cycle.completed:\n    description: Triggered when a cycle run completes successfully.\n    subscribe:\n      operationId: onCycleCompleted\n      summary: Cycle Completed\n      message:\n        $ref: '#/components/messages/CycleStatusChanged'\n  connector.installed:\n    description: Triggered when a connector is installed in an account.\n    subscribe:\n      operationId:\
  \ onConnectorInstalled\n      summary: Connector Installed\n      message:\n        $ref: '#/components/messages/ConnectorEvent'\n  connector.uninstalled:\n    description: Triggered when a connector is removed from an account.\n    subscribe:\n      operationId: onConnectorUninstalled\n      summary: Connector Uninstalled\n      message:\n        $ref: '#/components/messages/ConnectorEvent'\n  connector.authenticated:\n    description: Triggered when a connector authentication is completed.\n    subscribe:\n      operationId: onConnectorAuthenticated\n      summary: Connector Authenticated\n      message:\n        $ref: '#/components/messages/ConnectorEvent'\n  account.created:\n    description: Triggered when a new account is created under the partner.\n    subscribe:\n      operationId: onAccountCreated\n      summary: Account Created\n      message:\n        $ref: '#/components/messages/AccountEvent'\n  account.deleted:\n    description: Triggered when an account is deleted.\n    subscribe:\n\
  \      operationId: onAccountDeleted\n      summary: Account Deleted\n      message:\n        $ref: '#/components/messages/AccountEvent'\n  template.installed:\n    description: Triggered when a template is installed into an account.\n    subscribe:\n      operationId: onTemplateInstalled\n      summary: Template Installed\n      message:\n        $ref: '#/components/messages/TemplateEvent'\n  step.error:\n    description: Triggered when an individual step within a cycle encounters an error.\n    subscribe:\n      operationId: onStepError\n      summary: Step Error\n      message:\n        $ref: '#/components/messages/StepError'\ncomponents:\n  messages:\n    CycleStatusChanged:\n      payload:\n        type: object\n        properties:\n          EventType:\n            type: string\n            description: The type of event that occurred\n          Timestamp:\n            type: string\n            format: date-time\n            description: When the event occurred in UTC\n         \
  \ AccountId:\n            type: string\n            description: The account ID where the event occurred\n          CycleId:\n            type: string\n            description: The unique identifier of the cycle\n          CycleName:\n            type: string\n            description: The name of the cycle\n          Status:\n            type: string\n            enum:\n              - Active\n              - Inactive\n              - Paused\n              - Error\n            description: The new status of the cycle\n    CycleError:\n      payload:\n        type: object\n        properties:\n          EventType:\n            type: string\n            description: The type of event that occurred\n          Timestamp:\n            type: string\n            format: date-time\n            description: When the event occurred in UTC\n          AccountId:\n            type: string\n            description: The account ID where the event occurred\n          CycleId:\n            type: string\n\
  \            description: The unique identifier of the cycle\n          CycleName:\n            type: string\n            description: The name of the cycle\n          StepId:\n            type: string\n            description: The step where the error occurred\n          ErrorMessage:\n            type: string\n            description: Description of the error\n          ErrorCode:\n            type: string\n            description: Machine-readable error code\n    ConnectorEvent:\n      payload:\n        type: object\n        properties:\n          EventType:\n            type: string\n            description: The type of event that occurred\n          Timestamp:\n            type: string\n            format: date-time\n            description: When the event occurred in UTC\n          AccountId:\n            type: string\n            description: The account ID where the event occurred\n          ConnectorId:\n            type: integer\n            description: The base connector identifier\n\
  \          InstalledConnectorId:\n            type: integer\n            description: The installed connector identifier\n          ConnectorName:\n            type: string\n            description: The name of the connector\n          Authenticated:\n            type: boolean\n            description: Whether the connector is authenticated\n    AccountEvent:\n      payload:\n        type: object\n        properties:\n          EventType:\n            type: string\n            description: The type of event that occurred\n          Timestamp:\n            type: string\n            format: date-time\n            description: When the event occurred in UTC\n          AccountId:\n            type: string\n            description: The unique identifier of the account\n          AccountName:\n            type: string\n            description: The name of the account\n    TemplateEvent:\n      payload:\n        type: object\n        properties:\n          EventType:\n            type: string\n\
  \            description: The type of event that occurred\n          Timestamp:\n            type: string\n            format: date-time\n            description: When the event occurred in UTC\n          AccountId:\n            type: string\n            description: The account ID where the template was installed\n          TemplateId:\n            type: string\n            description: The unique identifier of the template\n          TemplateName:\n            type: string\n            description: The name of the template\n          CycleId:\n            type: string\n            description: The cycle ID created from the template installation\n    StepError:\n      payload:\n        type: object\n        properties:\n          EventType:\n            type: string\n            description: The type of event that occurred\n          Timestamp:\n            type: string\n            format: date-time\n            description: When the event occurred in UTC\n          AccountId:\n    \
  \        type: string\n            description: The account ID where the event occurred\n          CycleId:\n            type: string\n            description: The cycle containing the step\n          StepId:\n            type: string\n            description: The unique identifier of the step\n          StepName:\n            type: string\n            description: The name of the step\n          ConnectorId:\n            type: integer\n            description: The connector used by the step\n          ErrorMessage:\n            type: string\n            description: Description of the error\n          ErrorCode:\n            type: string\n            description: Machine-readable error code\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cyclr/refs/heads/main/asyncapi/cyclr-cyclr-asyncapi.yml
spec_file: asyncapi/cyclr-cyclr-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/cyclr/refs/heads/main/asyncapi/cyclr-cyclr-asyncapi.yml
tags:
- Connectors
- Custom Connectors
- Data Synchronization
- Embedded iPaaS
- Embedded SaaS Integration
- Embedded UI
- Integration Platform
- Integrations
- Marketplace
- OAuth 2.0
- REST API
- SaaS
- Templates
- Webhooks
- White Label
- Workflows
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
