---
api_specs:
- filename: keda-metrics-api-openapi.yml
  format: yaml
  label: KEDA Metrics API
  slug: keda-metrics-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/keda/refs/heads/main/openapi/keda-metrics-api-openapi.yml
- filename: keda-cloud-events-asyncapi.yml
  format: yaml
  label: KEDA CloudEventSource API
  slug: keda-cloud-event-source-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/keda/refs/heads/main/asyncapi/keda-cloud-events-asyncapi.yml
channels:
- description: HTTP endpoint receiving CloudEvents emitted by KEDA. KEDA sends a POST request for each scaling event to the configured sink URL.
  name: /events
  operation: publish
  operation_id: receiveKedaCloudEvent
  summary: Receive a KEDA CloudEvent
description: KEDA emits CloudEvents to configured HTTP or Azure Event Grid destinations when scaling events occur. The CloudEventSource and ClusterCloudEventSource custom resources define the destination endpoint and filter which event types are delivered. Events follow the CloudEvents specification v1.0 and carry information about KEDA scaling actions including scale target changes, errors, and authentication failures. Consumers can use these events to trigger downstream workflows, populate dashboards, or audit scaling activity.
layout: asyncapi
messages:
- description: ''
  name: ScalerErrorEvent
  summary: A KEDA scaler encountered an error retrieving metrics
  title: Scaler Error
- description: ''
  name: ScaledObjectReadyEvent
  summary: A ScaledObject has been successfully created and is active
  title: ScaledObject Ready
- description: ''
  name: ScaledObjectDeletedEvent
  summary: A ScaledObject has been deleted
  title: ScaledObject Deleted
- description: ''
  name: ScaledJobReadyEvent
  summary: A ScaledJob has been successfully created and is active
  title: ScaledJob Ready
- description: ''
  name: ScaledJobDeletedEvent
  summary: A ScaledJob has been deleted
  title: ScaledJob Deleted
- description: ''
  name: AuthenticationFailedEvent
  summary: A TriggerAuthentication credential check failed
  title: Authentication Failed
name: KEDA CloudEvent Source
provider_name: KEDA
provider_slug: keda
servers:
- description: HTTP(S) endpoint configured in the CloudEventSource destination.http.uri field. KEDA POSTs CloudEvents to this URL as they occur.
  name: httpSink
  protocol: https
  url: '{sinkUrl}'
slug: keda-cloud-events-asyncapi
source_filename: keda-cloud-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: KEDA CloudEvent Source\n  description: >-\n    KEDA emits CloudEvents to configured HTTP or Azure Event Grid destinations\n    when scaling events occur. The CloudEventSource and ClusterCloudEventSource\n    custom resources define the destination endpoint and filter which event\n    types are delivered. Events follow the CloudEvents specification v1.0 and\n    carry information about KEDA scaling actions including scale target changes,\n    errors, and authentication failures. Consumers can use these events to\n    trigger downstream workflows, populate dashboards, or audit scaling activity.\n  version: '2.x'\n  contact:\n    name: KEDA Community\n    url: https://keda.sh/community/\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\nexternalDocs:\n  description: KEDA CloudEvent Support Documentation\n  url: https://keda.sh/docs/latest/operate/cloud-events/\nservers:\n  httpSink:\n    url: '{sinkUrl}'\n\
  \    protocol: https\n    description: >-\n      HTTP(S) endpoint configured in the CloudEventSource destination.http.uri\n      field. KEDA POSTs CloudEvents to this URL as they occur.\n    variables:\n      sinkUrl:\n        description: The full HTTPS URL of the CloudEvent sink endpoint.\n        default: https://your-sink.example.com/events\nchannels:\n  /events:\n    description: >-\n      HTTP endpoint receiving CloudEvents emitted by KEDA. KEDA sends a POST\n      request for each scaling event to the configured sink URL.\n    publish:\n      operationId: receiveKedaCloudEvent\n      summary: Receive a KEDA CloudEvent\n      description: >-\n        KEDA delivers a CloudEvent to this channel when a scaling-related event\n        occurs. The event type determines the specific scaling action that\n        triggered delivery. Consumers should inspect the type field to determine\n        how to process the event data.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/ScalerErrorEvent'\n\
  \          - $ref: '#/components/messages/ScaledObjectReadyEvent'\n          - $ref: '#/components/messages/ScaledObjectDeletedEvent'\n          - $ref: '#/components/messages/ScaledJobReadyEvent'\n          - $ref: '#/components/messages/ScaledJobDeletedEvent'\n          - $ref: '#/components/messages/AuthenticationFailedEvent'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: http\n      scheme: bearer\n      description: >-\n        Optional bearer token for authenticating CloudEvent delivery to the\n        sink, configured via a TriggerAuthentication reference on the\n        CloudEventSource.\n  messages:\n    ScalerErrorEvent:\n      name: ScalerError\n      title: Scaler Error\n      summary: A KEDA scaler encountered an error retrieving metrics\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KedaCloudEvent'\n      examples:\n        - name: scalerError\n          summary: Scaler failed to retrieve metrics\n          payload:\n\
  \            specversion: '1.0'\n            type: com.cloudeventsource.keda\n            source: /cluster-name/keda-namespace/keda\n            subject: /cluster-name/default/scaledobject/my-scaledobject\n            id: a1b2c3d4-e5f6-7890-abcd-ef1234567890\n            time: '2026-03-18T10:00:00Z'\n            datacontenttype: application/json\n            data:\n              reason: ScalerError\n              message: >-\n                Error when getting metric for trigger type kafka. Unable to\n                connect to broker at kafka-broker:9092\n\n    ScaledObjectReadyEvent:\n      name: ScaledObjectReady\n      title: ScaledObject Ready\n      summary: A ScaledObject has been successfully created and is active\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KedaCloudEvent'\n      examples:\n        - name: scaledObjectReady\n          payload:\n            specversion: '1.0'\n            type: com.cloudeventsource.keda\n           \
  \ source: /cluster-name/keda-namespace/keda\n            subject: /cluster-name/default/scaledobject/my-scaledobject\n            id: b2c3d4e5-f6a7-8901-bcde-f12345678901\n            time: '2026-03-18T10:01:00Z'\n            datacontenttype: application/json\n            data:\n              reason: ScaledObjectReady\n              message: ScaledObject my-scaledobject is ready for scaling\n\n    ScaledObjectDeletedEvent:\n      name: ScaledObjectDeleted\n      title: ScaledObject Deleted\n      summary: A ScaledObject has been deleted\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KedaCloudEvent'\n\n    ScaledJobReadyEvent:\n      name: ScaledJobReady\n      title: ScaledJob Ready\n      summary: A ScaledJob has been successfully created and is active\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KedaCloudEvent'\n\n    ScaledJobDeletedEvent:\n      name: ScaledJobDeleted\n      title: ScaledJob Deleted\n\
  \      summary: A ScaledJob has been deleted\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KedaCloudEvent'\n\n    AuthenticationFailedEvent:\n      name: AuthenticationFailed\n      title: Authentication Failed\n      summary: A TriggerAuthentication credential check failed\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/KedaCloudEvent'\n\n  schemas:\n    KedaCloudEvent:\n      type: object\n      description: >-\n        A CloudEvent (v1.0) emitted by KEDA when a scaling-related event occurs.\n        Follows the CloudEvents specification envelope with a KEDA-specific data\n        payload containing the reason and message for the event.\n      required:\n        - specversion\n        - type\n        - source\n        - subject\n        - id\n        - time\n        - datacontenttype\n        - data\n      properties:\n        specversion:\n          type: string\n          const: '1.0'\n          description:\
  \ CloudEvents specification version. Always 1.0.\n        type:\n          type: string\n          const: com.cloudeventsource.keda\n          description: >-\n            CloudEvent type identifier. Always com.cloudeventsource.keda for\n            events emitted by KEDA.\n        source:\n          type: string\n          description: >-\n            URI identifying the event source in the format\n            /{cluster-name}/{keda-namespace}/keda. The cluster-name is set\n            via the clusterName field in the CloudEventSource spec.\n          example: /my-cluster/keda/keda\n        subject:\n          type: string\n          description: >-\n            URI identifying the specific resource that generated the event in\n            the format /{cluster-name}/{namespace}/{object-type}/{object-name}.\n          example: /my-cluster/default/scaledobject/my-app-scaler\n        id:\n          type: string\n          format: uuid\n          description: Unique identifier for this event\
  \ instance.\n          example: a1b2c3d4-e5f6-7890-abcd-ef1234567890\n        time:\n          type: string\n          format: date-time\n          description: Timestamp of when the event occurred in ISO 8601 format.\n          example: '2026-03-18T10:00:00Z'\n        datacontenttype:\n          type: string\n          const: application/json\n          description: MIME type of the data field. Always application/json.\n        data:\n          $ref: '#/components/schemas/KedaEventData'\n\n    KedaEventData:\n      type: object\n      description: >-\n        The payload of a KEDA CloudEvent containing the reason code and\n        human-readable message describing the scaling event.\n      required:\n        - reason\n        - message\n      properties:\n        reason:\n          type: string\n          description: >-\n            Machine-readable reason code for the event. Corresponds to KEDA\n            Kubernetes event reasons such as ScalerError, ScaledObjectReady,\n         \
  \   ScaledObjectDeleted, ScaledJobReady, ScaledJobDeleted, or\n            AuthenticationFailed.\n          enum:\n            - ScalerError\n            - ScaledObjectReady\n            - ScaledObjectDeleted\n            - ScaledJobReady\n            - ScaledJobDeleted\n            - KEDAScalersStarted\n            - KEDAScalersStopped\n            - AuthenticationFailed\n          example: ScalerError\n        message:\n          type: string\n          description: >-\n            Human-readable description of the event, providing context about\n            what happened and which resource was affected.\n          example: >-\n            Error when getting metric for trigger type kafka. Unable to\n            connect to broker at kafka-broker:9092\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/keda/refs/heads/main/asyncapi/keda-cloud-events-asyncapi.yml
spec_file: asyncapi/keda-cloud-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/keda/refs/heads/main/asyncapi/keda-cloud-events-asyncapi.yml
tags:
- Autoscaling
- CNCF
- Event-Driven
- Graduated
- Kubernetes
- AsyncAPI
- Webhooks
- Events
version: 2.x
---
