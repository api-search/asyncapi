---
api_specs:
- filename: swagger.json
  format: json
  label: Kubernetes API
  slug: kubernetes
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/kubernetes/kubernetes/master/api/openapi-spec/swagger.json
channels:
- description: Watch stream for Pod objects across all namespaces. Clients receive events for every pod creation, update, and deletion across the cluster.
  name: /api/v1/pods
  operation: subscribe
  operation_id: watchAllPods
  summary: Watch all pods cluster-wide
- description: Watch stream for Pod objects scoped to a single namespace. More efficient than cluster-wide watch when monitoring a specific application namespace.
  name: /api/v1/namespaces/{namespace}/pods
  operation: subscribe
  operation_id: watchNamespacedPods
  summary: Watch pods in a namespace
- description: Watch stream for Deployment objects in a namespace. Used by deployment controllers, GitOps tools, and monitoring systems to track rollout progress and configuration changes.
  name: /apis/apps/v1/namespaces/{namespace}/deployments
  operation: subscribe
  operation_id: watchNamespacedDeployments
  summary: Watch deployments in a namespace
- description: Watch stream for Service objects in a namespace. Service changes include creation, deletion, and updates to ports and selectors.
  name: /api/v1/namespaces/{namespace}/services
  operation: subscribe
  operation_id: watchNamespacedServices
  summary: Watch services in a namespace
- description: Watch stream for Node objects in the cluster. Node events include registration of new nodes, condition changes (Ready, MemoryPressure), and node deletions during scale-down or maintenance.
  name: /api/v1/nodes
  operation: subscribe
  operation_id: watchNodes
  summary: Watch all cluster nodes
- description: Watch stream for Namespace objects. Namespace events include creation of new namespaces, label updates, and termination when deleted.
  name: /api/v1/namespaces
  operation: subscribe
  operation_id: watchNamespaces
  summary: Watch all namespaces
- description: Watch stream for Event objects in a namespace. Events capture occurrences such as pod scheduling, container image pulls, restarts, and failures.
  name: /apis/events.k8s.io/v1/namespaces/{namespace}/events
  operation: subscribe
  operation_id: watchNamespacedEvents
  summary: Watch events in a namespace
description: The Kubernetes Watch API provides a streaming event interface for receiving real-time notifications about changes to cluster resources. Clients subscribe to resource types and receive a stream of ADDED, MODIFIED, DELETED, and BOOKMARK events as objects are created, changed, or removed. Watch is used by controllers, operators, and clients to maintain synchronized state without polling. The watch stream is delivered via HTTP chunked transfer encoding or WebSocket over the Kubernetes API server.
layout: asyncapi
messages:
- description: A WatchEvent is delivered to watch stream subscribers each time a watched resource changes. The type field indicates the nature of the change (ADDED, MODIFIED, DELETED, BOOKMARK, ERROR), and the object field contains the current state of the resource at the time of the event.
  name: WatchEvent
  summary: A single event in a Kubernetes watch stream
  title: Kubernetes Watch Event
name: Kubernetes Watch Events
provider_name: Kubernetes
provider_slug: kubernetes
servers:
- description: In-cluster Kubernetes API server. External access requires the cluster's API server endpoint, typically obtained via kubectl config view.
  name: kubernetesApiServer
  protocol: https
  url: https://kubernetes.default.svc
slug: kubernetes-watch-asyncapi
source_filename: kubernetes-watch-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Kubernetes Watch Events\n  description: >-\n    The Kubernetes Watch API provides a streaming event interface for receiving\n    real-time notifications about changes to cluster resources. Clients subscribe\n    to resource types and receive a stream of ADDED, MODIFIED, DELETED, and\n    BOOKMARK events as objects are created, changed, or removed. Watch is used\n    by controllers, operators, and clients to maintain synchronized state without\n    polling. The watch stream is delivered via HTTP chunked transfer encoding or\n    WebSocket over the Kubernetes API server.\n  version: v1.32.0\n  contact:\n    name: Kubernetes Community\n    url: https://kubernetes.io/community/\nexternalDocs:\n  description: Kubernetes API Concepts - Watch\n  url: https://kubernetes.io/docs/reference/using-api/api-concepts/\nservers:\n  kubernetesApiServer:\n    url: 'https://kubernetes.default.svc'\n    protocol: https\n    description: >-\n      In-cluster Kubernetes\
  \ API server. External access requires the cluster's\n      API server endpoint, typically obtained via kubectl config view.\n    security:\n      - bearerAuth: []\n      - clientCertificate: []\nchannels:\n  /api/v1/pods:\n    description: >-\n      Watch stream for Pod objects across all namespaces. Clients receive events\n      for every pod creation, update, and deletion across the cluster.\n    subscribe:\n      operationId: watchAllPods\n      summary: Watch all pods cluster-wide\n      description: >-\n        Opens a watch stream for all pods across all namespaces. The stream\n        produces WatchEvent messages each time a pod is created, modified,\n        deleted, or when a bookmark checkpoint is issued. Use ?watch=true query\n        parameter to activate streaming.\n      message:\n        $ref: '#/components/messages/WatchEvent'\n  /api/v1/namespaces/{namespace}/pods:\n    description: >-\n      Watch stream for Pod objects scoped to a single namespace. More efficient\n\
  \      than cluster-wide watch when monitoring a specific application namespace.\n    parameters:\n      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId: watchNamespacedPods\n      summary: Watch pods in a namespace\n      description: >-\n        Opens a watch stream for pods within the specified namespace. Produces\n        WatchEvent messages for pod lifecycle transitions and state changes\n        within the namespace scope.\n      message:\n        $ref: '#/components/messages/WatchEvent'\n  /apis/apps/v1/namespaces/{namespace}/deployments:\n    description: >-\n      Watch stream for Deployment objects in a namespace. Used by deployment\n      controllers, GitOps tools, and monitoring systems to track rollout\n      progress and configuration changes.\n    parameters:\n      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId: watchNamespacedDeployments\n      summary: Watch deployments\
  \ in a namespace\n      description: >-\n        Opens a watch stream for deployments in the specified namespace.\n        Produces WatchEvent messages when deployments are created, their\n        replica count changes, rollouts complete, or specs are updated.\n      message:\n        $ref: '#/components/messages/WatchEvent'\n  /api/v1/namespaces/{namespace}/services:\n    description: >-\n      Watch stream for Service objects in a namespace. Service changes\n      include creation, deletion, and updates to ports and selectors.\n    parameters:\n      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId: watchNamespacedServices\n      summary: Watch services in a namespace\n      description: >-\n        Opens a watch stream for services within the specified namespace.\n        Consumers receive WatchEvent messages when services are created,\n        their configuration is updated, or they are deleted.\n      message:\n        $ref: '#/components/messages/WatchEvent'\n\
  \  /api/v1/nodes:\n    description: >-\n      Watch stream for Node objects in the cluster. Node events include\n      registration of new nodes, condition changes (Ready, MemoryPressure),\n      and node deletions during scale-down or maintenance.\n    subscribe:\n      operationId: watchNodes\n      summary: Watch all cluster nodes\n      description: >-\n        Opens a watch stream for all nodes in the cluster. Produces WatchEvent\n        messages when nodes join or leave the cluster, or when node conditions\n        change, such as when a node transitions to NotReady.\n      message:\n        $ref: '#/components/messages/WatchEvent'\n  /api/v1/namespaces:\n    description: >-\n      Watch stream for Namespace objects. Namespace events include creation\n      of new namespaces, label updates, and termination when deleted.\n    subscribe:\n      operationId: watchNamespaces\n      summary: Watch all namespaces\n      description: >-\n        Opens a watch stream for all namespaces.\
  \ Consumers receive WatchEvent\n        messages when namespaces are created, modified, or enter the\n        Terminating phase prior to deletion.\n      message:\n        $ref: '#/components/messages/WatchEvent'\n  /apis/events.k8s.io/v1/namespaces/{namespace}/events:\n    description: >-\n      Watch stream for Event objects in a namespace. Events capture occurrences\n      such as pod scheduling, container image pulls, restarts, and failures.\n    parameters:\n      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId: watchNamespacedEvents\n      summary: Watch events in a namespace\n      description: >-\n        Opens a watch stream for Kubernetes events in the specified namespace.\n        Produces WatchEvent messages as the cluster records activity such as\n        scheduled pods, image pull completions, container crashes, and\n        resource quota violations.\n      message:\n        $ref: '#/components/messages/WatchEvent'\ncomponents:\n\
  \  securitySchemes:\n    bearerAuth:\n      type: httpApiKey\n      name: Authorization\n      in: header\n      description: >-\n        Kubernetes service account token or user token. Include in the\n        Authorization header as 'Bearer <token>'.\n    clientCertificate:\n      type: X509\n      description: >-\n        Client certificate authentication using a TLS certificate issued by\n        the cluster certificate authority.\n  parameters:\n    Namespace:\n      description: The namespace name to scope the watch stream to.\n      schema:\n        type: string\n  messages:\n    WatchEvent:\n      name: WatchEvent\n      title: Kubernetes Watch Event\n      summary: A single event in a Kubernetes watch stream\n      description: >-\n        A WatchEvent is delivered to watch stream subscribers each time a\n        watched resource changes. The type field indicates the nature of the\n        change (ADDED, MODIFIED, DELETED, BOOKMARK, ERROR), and the object\n        field contains\
  \ the current state of the resource at the time of\n        the event.\n      payload:\n        $ref: '#/components/schemas/WatchEvent'\n  schemas:\n    WatchEvent:\n      type: object\n      required:\n        - type\n        - object\n      description: >-\n        An event delivered over a Kubernetes watch stream representing a\n        state change to a resource. The object field contains the full\n        resource as it exists after the change.\n      properties:\n        type:\n          type: string\n          enum:\n            - ADDED\n            - MODIFIED\n            - DELETED\n            - BOOKMARK\n            - ERROR\n          description: >-\n            Type of change that triggered this event. ADDED when a resource\n            is created. MODIFIED when a resource's spec, status, or metadata\n            changes. DELETED when a resource is removed. BOOKMARK is a\n            periodic checkpoint containing only the resourceVersion, used\n            to allow clients\
  \ to resume watching from a known point.\n            ERROR indicates a watch stream error.\n        object:\n          type: object\n          description: >-\n            The Kubernetes resource object at the time of the event. For\n            BOOKMARK events, only the apiVersion, kind, and metadata\n            (with resourceVersion) are populated. For ERROR events, this\n            contains a Status object.\n          properties:\n            apiVersion:\n              type: string\n              description: API version of the resource.\n            kind:\n              type: string\n              description: Kind of the resource.\n            metadata:\n              type: object\n              description: Standard Kubernetes object metadata.\n              properties:\n                name:\n                  type: string\n                  description: Name of the resource.\n                namespace:\n                  type: string\n                  description: Namespace\
  \ of the resource.\n                uid:\n                  type: string\n                  description: Unique identifier for the resource.\n                resourceVersion:\n                  type: string\n                  description: >-\n                    Resource version at the time of this event. Used to\n                    resume a watch stream from this point.\n                generation:\n                  type: integer\n                  description: Generation of the resource spec.\n                creationTimestamp:\n                  type: string\n                  format: date-time\n                  description: Time the resource was created.\n                deletionTimestamp:\n                  type: string\n                  format: date-time\n                  description: >-\n                    Time at which the resource will be deleted. Present\n                    when the resource has been marked for deletion.\n                labels:\n                  type:\
  \ object\n                  additionalProperties:\n                    type: string\n                  description: Labels applied to the resource.\n                annotations:\n                  type: object\n                  additionalProperties:\n                    type: string\n                  description: Annotations applied to the resource.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/kubernetes/refs/heads/main/asyncapi/kubernetes-watch-asyncapi.yml
spec_file: asyncapi/kubernetes-watch-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/kubernetes/refs/heads/main/asyncapi/kubernetes-watch-asyncapi.yml
tags:
- Automation
- Cloud Native
- CNCF
- Containers
- Deployment
- Open Source
- Orchestration
- Scaling
- AsyncAPI
- Webhooks
- Events
version: v1.32.0
---
