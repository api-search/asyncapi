---
channels:
- description: Fired before processing any admin resource request. Scripts can inspect or modify the request before it reaches the handler.
  name: system.admin.pre_process
  operation: subscribe
  operation_id: onAdminPreProcess
  summary: Admin resource pre-process event
- description: Fired after processing any admin resource request. Scripts can inspect or modify the response before it is returned to the client.
  name: system.admin.post_process
  operation: subscribe
  operation_id: onAdminPostProcess
  summary: Admin resource post-process event
- description: Fired before processing any app resource request.
  name: system.app.pre_process
  operation: subscribe
  operation_id: onAppPreProcess
  summary: App resource pre-process event
- description: Fired after processing any app resource request.
  name: system.app.post_process
  operation: subscribe
  operation_id: onAppPostProcess
  summary: App resource post-process event
- description: Fired before processing any role resource request.
  name: system.role.pre_process
  operation: subscribe
  operation_id: onRolePreProcess
  summary: Role resource pre-process event
- description: Fired after processing any role resource request.
  name: system.role.post_process
  operation: subscribe
  operation_id: onRolePostProcess
  summary: Role resource post-process event
- description: Fired before processing any service resource request.
  name: system.service.pre_process
  operation: subscribe
  operation_id: onServicePreProcess
  summary: Service resource pre-process event
- description: Fired after processing any service resource request.
  name: system.service.post_process
  operation: subscribe
  operation_id: onServicePostProcess
  summary: Service resource post-process event
- description: Fired before processing any user resource request.
  name: system.user.pre_process
  operation: subscribe
  operation_id: onUserPreProcess
  summary: User resource pre-process event
- description: Fired after processing any user resource request.
  name: system.user.post_process
  operation: subscribe
  operation_id: onUserPostProcess
  summary: User resource post-process event
description: Asynchronous event model for the DreamFactory System API. DreamFactory provides a comprehensive event scripting system that fires events before and after every API call, allowing server-side scripts (PHP, Python, Node.js, or V8js) to intercept, modify, or augment request and response processing. Events follow the pattern {service}.{resource}.{verb} with pre-process and post-process variants.
layout: asyncapi
messages:
- description: ''
  name: SystemEvent
  summary: An event payload delivered to server-side scripts during pre-process or post-process phases of a system API call.
  title: DreamFactory System Event
name: DreamFactory System API Events
provider_name: DreamFactory
provider_slug: dreamfactory
servers: []
slug: dreamfactory-system-api-asyncapi
source_filename: dreamfactory-system-api-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: DreamFactory System API Events\n  version: 2.0.0\n  description: >-\n    Asynchronous event model for the DreamFactory System API. DreamFactory\n    provides a comprehensive event scripting system that fires events before\n    and after every API call, allowing server-side scripts (PHP, Python,\n    Node.js, or V8js) to intercept, modify, or augment request and response\n    processing. Events follow the pattern {service}.{resource}.{verb} with\n    pre-process and post-process variants.\n  contact:\n    name: DreamFactory Support\n    url: https://www.dreamfactory.com/support\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\n  termsOfService: https://www.dreamfactory.com/terms-of-use\nexternalDocs:\n  description: DreamFactory Event Scripting Documentation\n  url: https://guide.dreamfactory.com/docs/event-scripting/\ndefaultContentType: application/json\nchannels:\n  system.admin.pre_process:\n    description:\
  \ >-\n      Fired before processing any admin resource request. Scripts can\n      inspect or modify the request before it reaches the handler.\n    subscribe:\n      operationId: onAdminPreProcess\n      summary: Admin resource pre-process event\n      message:\n        $ref: '#/components/messages/SystemEvent'\n  system.admin.post_process:\n    description: >-\n      Fired after processing any admin resource request. Scripts can\n      inspect or modify the response before it is returned to the client.\n    subscribe:\n      operationId: onAdminPostProcess\n      summary: Admin resource post-process event\n      message:\n        $ref: '#/components/messages/SystemEvent'\n  system.app.pre_process:\n    description: >-\n      Fired before processing any app resource request.\n    subscribe:\n      operationId: onAppPreProcess\n      summary: App resource pre-process event\n      message:\n        $ref: '#/components/messages/SystemEvent'\n  system.app.post_process:\n    description: >-\n\
  \      Fired after processing any app resource request.\n    subscribe:\n      operationId: onAppPostProcess\n      summary: App resource post-process event\n      message:\n        $ref: '#/components/messages/SystemEvent'\n  system.role.pre_process:\n    description: >-\n      Fired before processing any role resource request.\n    subscribe:\n      operationId: onRolePreProcess\n      summary: Role resource pre-process event\n      message:\n        $ref: '#/components/messages/SystemEvent'\n  system.role.post_process:\n    description: >-\n      Fired after processing any role resource request.\n    subscribe:\n      operationId: onRolePostProcess\n      summary: Role resource post-process event\n      message:\n        $ref: '#/components/messages/SystemEvent'\n  system.service.pre_process:\n    description: >-\n      Fired before processing any service resource request.\n    subscribe:\n      operationId: onServicePreProcess\n      summary: Service resource pre-process event\n  \
  \    message:\n        $ref: '#/components/messages/SystemEvent'\n  system.service.post_process:\n    description: >-\n      Fired after processing any service resource request.\n    subscribe:\n      operationId: onServicePostProcess\n      summary: Service resource post-process event\n      message:\n        $ref: '#/components/messages/SystemEvent'\n  system.user.pre_process:\n    description: >-\n      Fired before processing any user resource request.\n    subscribe:\n      operationId: onUserPreProcess\n      summary: User resource pre-process event\n      message:\n        $ref: '#/components/messages/SystemEvent'\n  system.user.post_process:\n    description: >-\n      Fired after processing any user resource request.\n    subscribe:\n      operationId: onUserPostProcess\n      summary: User resource post-process event\n      message:\n        $ref: '#/components/messages/SystemEvent'\ncomponents:\n  messages:\n    SystemEvent:\n      name: SystemEvent\n      title: DreamFactory\
  \ System Event\n      summary: >-\n        An event payload delivered to server-side scripts during\n        pre-process or post-process phases of a system API call.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventPayload'\n  schemas:\n    EventPayload:\n      type: object\n      properties:\n        request:\n          type: object\n          description: The inbound HTTP request details.\n          properties:\n            method:\n              type: string\n              description: HTTP method (GET, POST, PUT, PATCH, DELETE).\n            uri:\n              type: string\n              description: Request URI path.\n            headers:\n              type: object\n              description: HTTP request headers.\n              additionalProperties:\n                type: string\n            parameters:\n              type: object\n              description: Query parameters.\n              additionalProperties: true\n            payload:\n\
  \              type: object\n              description: Request body payload.\n              additionalProperties: true\n        response:\n          type: object\n          description: >-\n            The outbound HTTP response (available in post-process events\n            and modifiable by scripts).\n          properties:\n            status_code:\n              type: integer\n              description: HTTP status code.\n            headers:\n              type: object\n              description: HTTP response headers.\n              additionalProperties:\n                type: string\n            content:\n              description: Response body content.\n        resource:\n          type: string\n          description: The system resource being acted upon.\n        event_name:\n          type: string\n          description: >-\n            Full event name in the format\n            {service}.{resource}.{verb}.{process_type}.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/dreamfactory/refs/heads/main/asyncapi/dreamfactory-system-api-asyncapi.yml
spec_file: asyncapi/dreamfactory-system-api-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/dreamfactory/refs/heads/main/asyncapi/dreamfactory-system-api-asyncapi.yml
tags:
- Automation
- Deployment
- Documentation
- Generation
- Security
- AsyncAPI
- Webhooks
- Events
version: 2.0.0
---
