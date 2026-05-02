---
api_specs:
- filename: kubernetes-services-openapi.yml
  format: yaml
  label: Kubernetes Services
  slug: kubernetes-services
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/kubernetes-services/refs/heads/main/openapi/kubernetes-services-openapi.yml
- filename: kubernetes-ingress-openapi.yml
  format: yaml
  label: Kubernetes Ingress
  slug: kubernetes-ingress
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/kubernetes-services/refs/heads/main/openapi/kubernetes-ingress-openapi.yml
- filename: kubernetes-gateway-api-openapi.yml
  format: yaml
  label: Kubernetes Gateway API
  slug: kubernetes-gateway-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/kubernetes-services/refs/heads/main/openapi/kubernetes-gateway-api-openapi.yml
- filename: kubernetes-endpoint-slices-openapi.yml
  format: yaml
  label: Kubernetes EndpointSlices
  slug: kubernetes-endpoint-slices
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/kubernetes-services/refs/heads/main/openapi/kubernetes-endpoint-slices-openapi.yml
- filename: kubernetes-network-policies-openapi.yml
  format: yaml
  label: Kubernetes Network Policies
  slug: kubernetes-network-policies
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/kubernetes-services/refs/heads/main/openapi/kubernetes-network-policies-openapi.yml
channels:
- description: Watch stream for Service objects in a namespace. Service changes include creation of new services, updates to port mappings or selectors, type changes (e.g. ClusterIP to LoadBalancer), and deletions.
  name: /api/v1/namespaces/{namespace}/services
  operation: subscribe
  operation_id: watchNamespacedServices
  summary: Watch Services in a namespace
- description: Watch stream for all Service objects across all namespaces in the cluster. Used for cluster-wide service discovery and monitoring.
  name: /api/v1/services
  operation: subscribe
  operation_id: watchAllServices
  summary: Watch all Services cluster-wide
- description: Watch stream for Ingress objects in a namespace. Ingress changes include new routing rules, TLS configuration updates, and load balancer status updates from the ingress controller.
  name: /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses
  operation: subscribe
  operation_id: watchNamespacedIngresses
  summary: Watch Ingresses in a namespace
- description: Watch stream for EndpointSlice objects in a namespace. EndpointSlice changes reflect pod readiness transitions, pod scheduling, and pod termination as pods backing a Service change state.
  name: /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices
  operation: subscribe
  operation_id: watchNamespacedEndpointSlices
  summary: Watch EndpointSlices in a namespace
- description: Watch stream for NetworkPolicy objects in a namespace. Network policy changes are monitored by CNI plugins to update their eBPF or iptables rules enforcing pod-level traffic restrictions.
  name: /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies
  operation: subscribe
  operation_id: watchNamespacedNetworkPolicies
  summary: Watch NetworkPolicies in a namespace
- description: Watch stream for Gateway objects in a namespace. Gateway changes include new listener configurations, TLS certificate updates, and status updates from the gateway controller.
  name: /apis/gateway.networking.k8s.io/v1/namespaces/{namespace}/gateways
  operation: subscribe
  operation_id: watchNamespacedGateways
  summary: Watch Gateways in a namespace
- description: Watch stream for HTTPRoute objects in a namespace. HTTPRoute changes reflect updates to routing rules, backend weights, and match conditions used by gateway controllers.
  name: /apis/gateway.networking.k8s.io/v1/namespaces/{namespace}/httproutes
  operation: subscribe
  operation_id: watchNamespacedHTTPRoutes
  summary: Watch HTTPRoutes in a namespace
description: The Kubernetes Services watch API provides streaming event notifications for networking resources including Services, Ingresses, EndpointSlices, NetworkPolicies, and Gateway API resources. Clients subscribe to resource watch streams and receive ADDED, MODIFIED, DELETED, and BOOKMARK events as networking configuration changes in the cluster. These streams are used by ingress controllers, load balancer operators, service mesh components, and observability tools to maintain synchronized state.
layout: asyncapi
messages:
- description: A watch event delivered when a Service is created, modified, or deleted in the cluster. The object field contains the current state of the Service, including its type, port mappings, selector, and load balancer status.
  name: ServiceWatchEvent
  summary: Change event for a Kubernetes Service resource
  title: Service Watch Event
- description: A watch event delivered when an Ingress is created, its routing rules are modified, or the ingress controller updates its load balancer status.
  name: IngressWatchEvent
  summary: Change event for a Kubernetes Ingress resource
  title: Ingress Watch Event
- description: A watch event delivered when an EndpointSlice is created, when pod readiness changes, when pods are added or removed from a Service's selector, or when topology hints are updated.
  name: EndpointSliceWatchEvent
  summary: Change event for a Kubernetes EndpointSlice resource
  title: EndpointSlice Watch Event
- description: A watch event delivered when a NetworkPolicy is created, its ingress or egress rules are modified, or the policy is deleted. CNI plugins consume these events to enforce the current network segmentation rules.
  name: NetworkPolicyWatchEvent
  summary: Change event for a Kubernetes NetworkPolicy resource
  title: NetworkPolicy Watch Event
- description: A watch event delivered when a Gateway is created, listener configurations change, TLS certificates are updated, or the gateway controller updates the assigned addresses in the status.
  name: GatewayWatchEvent
  summary: Change event for a Gateway API Gateway resource
  title: Gateway Watch Event
- description: A watch event delivered when an HTTPRoute is created, routing rules are modified, backend references change, or the gateway controller updates the route's accepted status.
  name: HTTPRouteWatchEvent
  summary: Change event for a Gateway API HTTPRoute resource
  title: HTTPRoute Watch Event
name: Kubernetes Services Watch Events
provider_name: Kubernetes Services
provider_slug: kubernetes-services
servers:
- description: In-cluster Kubernetes API server for watch streaming.
  name: kubernetesApiServer
  protocol: https
  url: https://kubernetes.default.svc
slug: kubernetes-services-watch-asyncapi
source_filename: kubernetes-services-watch-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Kubernetes Services Watch Events\n  description: >-\n    The Kubernetes Services watch API provides streaming event notifications\n    for networking resources including Services, Ingresses, EndpointSlices,\n    NetworkPolicies, and Gateway API resources. Clients subscribe to resource\n    watch streams and receive ADDED, MODIFIED, DELETED, and BOOKMARK events\n    as networking configuration changes in the cluster. These streams are\n    used by ingress controllers, load balancer operators, service mesh\n    components, and observability tools to maintain synchronized state.\n  version: v1.32.0\n  contact:\n    name: Kubernetes Community\n    url: https://kubernetes.io/community/\nexternalDocs:\n  description: Kubernetes API Concepts - Watch\n  url: https://kubernetes.io/docs/reference/using-api/api-concepts/\nservers:\n  kubernetesApiServer:\n    url: 'https://kubernetes.default.svc'\n    protocol: https\n    description: In-cluster Kubernetes\
  \ API server for watch streaming.\n    security:\n      - bearerAuth: []\n      - clientCertificate: []\nchannels:\n  /api/v1/namespaces/{namespace}/services:\n    description: >-\n      Watch stream for Service objects in a namespace. Service changes include\n      creation of new services, updates to port mappings or selectors, type\n      changes (e.g. ClusterIP to LoadBalancer), and deletions.\n    parameters:\n      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId: watchNamespacedServices\n      summary: Watch Services in a namespace\n      description: >-\n        Streams WatchEvent messages for all Service changes in the specified\n        namespace. Used by load balancer controllers to track service creation\n        and updates, and by kube-proxy to sync iptables/ipvs rules.\n      message:\n        $ref: '#/components/messages/ServiceWatchEvent'\n  /api/v1/services:\n    description: >-\n      Watch stream for all Service objects\
  \ across all namespaces in the\n      cluster. Used for cluster-wide service discovery and monitoring.\n    subscribe:\n      operationId: watchAllServices\n      summary: Watch all Services cluster-wide\n      description: >-\n        Streams WatchEvent messages for Service changes across all namespaces.\n        Useful for external DNS controllers and global load balancer\n        controllers that manage cluster-wide service exposure.\n      message:\n        $ref: '#/components/messages/ServiceWatchEvent'\n  /apis/networking.k8s.io/v1/namespaces/{namespace}/ingresses:\n    description: >-\n      Watch stream for Ingress objects in a namespace. Ingress changes include\n      new routing rules, TLS configuration updates, and load balancer\n      status updates from the ingress controller.\n    parameters:\n      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId: watchNamespacedIngresses\n      summary: Watch Ingresses in a namespace\n   \
  \   description: >-\n        Streams WatchEvent messages for Ingress changes in the specified\n        namespace. Ingress controllers watch this stream to reconfigure\n        their proxies when routing rules are added or modified.\n      message:\n        $ref: '#/components/messages/IngressWatchEvent'\n  /apis/discovery.k8s.io/v1/namespaces/{namespace}/endpointslices:\n    description: >-\n      Watch stream for EndpointSlice objects in a namespace. EndpointSlice\n      changes reflect pod readiness transitions, pod scheduling, and pod\n      termination as pods backing a Service change state.\n    parameters:\n      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId: watchNamespacedEndpointSlices\n      summary: Watch EndpointSlices in a namespace\n      description: >-\n        Streams WatchEvent messages for EndpointSlice changes. kube-proxy\n        and service mesh sidecars watch this stream to keep their endpoint\n        routing tables\
  \ synchronized with the current set of ready pods.\n      message:\n        $ref: '#/components/messages/EndpointSliceWatchEvent'\n  /apis/networking.k8s.io/v1/namespaces/{namespace}/networkpolicies:\n    description: >-\n      Watch stream for NetworkPolicy objects in a namespace. Network policy\n      changes are monitored by CNI plugins to update their eBPF or iptables\n      rules enforcing pod-level traffic restrictions.\n    parameters:\n      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId: watchNamespacedNetworkPolicies\n      summary: Watch NetworkPolicies in a namespace\n      description: >-\n        Streams WatchEvent messages for NetworkPolicy changes in the specified\n        namespace. CNI plugin agents watch this stream to enforce the latest\n        traffic rules for pods without requiring restarts.\n      message:\n        $ref: '#/components/messages/NetworkPolicyWatchEvent'\n  /apis/gateway.networking.k8s.io/v1/namespaces/{namespace}/gateways:\n\
  \    description: >-\n      Watch stream for Gateway objects in a namespace. Gateway changes include\n      new listener configurations, TLS certificate updates, and status\n      updates from the gateway controller.\n    parameters:\n      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId: watchNamespacedGateways\n      summary: Watch Gateways in a namespace\n      description: >-\n        Streams WatchEvent messages for Gateway resources. Gateway controllers\n        watch this stream to provision or update the underlying load balancer\n        or proxy infrastructure.\n      message:\n        $ref: '#/components/messages/GatewayWatchEvent'\n  /apis/gateway.networking.k8s.io/v1/namespaces/{namespace}/httproutes:\n    description: >-\n      Watch stream for HTTPRoute objects in a namespace. HTTPRoute changes\n      reflect updates to routing rules, backend weights, and match conditions\n      used by gateway controllers.\n    parameters:\n\
  \      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId: watchNamespacedHTTPRoutes\n      summary: Watch HTTPRoutes in a namespace\n      description: >-\n        Streams WatchEvent messages for HTTPRoute resources. Gateway controllers\n        watch this stream to update proxy routing configuration whenever\n        application teams modify traffic routing rules.\n      message:\n        $ref: '#/components/messages/HTTPRouteWatchEvent'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: httpApiKey\n      name: Authorization\n      in: header\n      description: Kubernetes service account or user bearer token.\n    clientCertificate:\n      type: X509\n      description: Client TLS certificate signed by the cluster CA.\n  parameters:\n    Namespace:\n      description: Namespace name to scope the watch stream.\n      schema:\n        type: string\n  messages:\n    ServiceWatchEvent:\n      name: ServiceWatchEvent\n      title:\
  \ Service Watch Event\n      summary: Change event for a Kubernetes Service resource\n      description: >-\n        A watch event delivered when a Service is created, modified, or deleted\n        in the cluster. The object field contains the current state of the\n        Service, including its type, port mappings, selector, and load balancer\n        status.\n      payload:\n        $ref: '#/components/schemas/WatchEvent'\n    IngressWatchEvent:\n      name: IngressWatchEvent\n      title: Ingress Watch Event\n      summary: Change event for a Kubernetes Ingress resource\n      description: >-\n        A watch event delivered when an Ingress is created, its routing rules\n        are modified, or the ingress controller updates its load balancer\n        status.\n      payload:\n        $ref: '#/components/schemas/WatchEvent'\n    EndpointSliceWatchEvent:\n      name: EndpointSliceWatchEvent\n      title: EndpointSlice Watch Event\n      summary: Change event for a Kubernetes EndpointSlice\
  \ resource\n      description: >-\n        A watch event delivered when an EndpointSlice is created, when pod\n        readiness changes, when pods are added or removed from a Service's\n        selector, or when topology hints are updated.\n      payload:\n        $ref: '#/components/schemas/WatchEvent'\n    NetworkPolicyWatchEvent:\n      name: NetworkPolicyWatchEvent\n      title: NetworkPolicy Watch Event\n      summary: Change event for a Kubernetes NetworkPolicy resource\n      description: >-\n        A watch event delivered when a NetworkPolicy is created, its ingress\n        or egress rules are modified, or the policy is deleted. CNI plugins\n        consume these events to enforce the current network segmentation rules.\n      payload:\n        $ref: '#/components/schemas/WatchEvent'\n    GatewayWatchEvent:\n      name: GatewayWatchEvent\n      title: Gateway Watch Event\n      summary: Change event for a Gateway API Gateway resource\n      description: >-\n        A watch event\
  \ delivered when a Gateway is created, listener\n        configurations change, TLS certificates are updated, or the gateway\n        controller updates the assigned addresses in the status.\n      payload:\n        $ref: '#/components/schemas/WatchEvent'\n    HTTPRouteWatchEvent:\n      name: HTTPRouteWatchEvent\n      title: HTTPRoute Watch Event\n      summary: Change event for a Gateway API HTTPRoute resource\n      description: >-\n        A watch event delivered when an HTTPRoute is created, routing rules\n        are modified, backend references change, or the gateway controller\n        updates the route's accepted status.\n      payload:\n        $ref: '#/components/schemas/WatchEvent'\n  schemas:\n    WatchEvent:\n      type: object\n      required:\n        - type\n        - object\n      description: >-\n        A watch event representing a state change to a Kubernetes networking\n        resource. The type indicates the change nature and the object contains\n        the full\
  \ resource state after the change.\n      properties:\n        type:\n          type: string\n          enum:\n            - ADDED\n            - MODIFIED\n            - DELETED\n            - BOOKMARK\n            - ERROR\n          description: >-\n            Type of change. ADDED on resource creation, MODIFIED on any\n            spec/status/metadata update, DELETED on removal. BOOKMARK\n            provides a resourceVersion checkpoint for resuming watches.\n            ERROR indicates a problem with the watch stream.\n        object:\n          type: object\n          description: >-\n            The Kubernetes resource at the time of the event. For BOOKMARK\n            events only metadata.resourceVersion is populated. For ERROR\n            events this is a Status object.\n          properties:\n            apiVersion:\n              type: string\n              description: API version of the resource.\n            kind:\n              type: string\n              description:\
  \ Kind of the resource (e.g. Service, Ingress, EndpointSlice).\n            metadata:\n              type: object\n              description: Object metadata including name, namespace, and resourceVersion.\n              properties:\n                name:\n                  type: string\n                  description: Name of the resource.\n                namespace:\n                  type: string\n                  description: Namespace of the resource.\n                uid:\n                  type: string\n                  description: Unique identifier of the resource.\n                resourceVersion:\n                  type: string\n                  description: Resource version for resuming watch streams.\n                generation:\n                  type: integer\n                  description: Generation of the resource spec.\n                creationTimestamp:\n                  type: string\n                  format: date-time\n                  description: Creation timestamp.\n\
  \                deletionTimestamp:\n                  type: string\n                  format: date-time\n                  description: Deletion timestamp when graceful deletion is pending.\n                labels:\n                  type: object\n                  additionalProperties:\n                    type: string\n                  description: Resource labels.\n                annotations:\n                  type: object\n                  additionalProperties:\n                    type: string\n                  description: Resource annotations.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/kubernetes-services/refs/heads/main/asyncapi/kubernetes-services-watch-asyncapi.yml
spec_file: asyncapi/kubernetes-services-watch-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/kubernetes-services/refs/heads/main/asyncapi/kubernetes-services-watch-asyncapi.yml
tags:
- Container Orchestration
- Kubernetes
- Load Balancing
- Networking
- Service Discovery
- AsyncAPI
- Webhooks
- Events
version: v1.32.0
---
