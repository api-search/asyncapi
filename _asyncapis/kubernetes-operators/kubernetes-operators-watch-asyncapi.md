---
api_specs:
- filename: kubernetes-operators-watch-asyncapi.yml
  format: yaml
  label: Kubernetes Operators
  slug: kubernetes-operators
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/kubernetes-operators/refs/heads/main/asyncapi/kubernetes-operators-watch-asyncapi.yml
- filename: kubernetes-crd-openapi.yml
  format: yaml
  label: Kubernetes Custom Resource Definitions
  slug: custom-resource-definitions
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/kubernetes-operators/refs/heads/main/openapi/kubernetes-crd-openapi.yml
- filename: kubernetes-olm-openapi.yml
  format: yaml
  label: Operator Lifecycle Manager
  slug: operator-lifecycle-manager
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/kubernetes-operators/refs/heads/main/openapi/kubernetes-olm-openapi.yml
channels:
- description: Watch stream for CustomResourceDefinition objects cluster-wide. CRD events are generated when new custom resource types are registered, their schemas are updated, or they are deleted. Operator controllers watch this channel to react to CRD establishment before starting their reconciliation loops.
  name: /apis/apiextensions.k8s.io/v1/customresourcedefinitions
  operation: subscribe
  operation_id: watchCustomResourceDefinitions
  summary: Watch all CustomResourceDefinitions
- description: Watch stream for CatalogSource objects in a namespace. OLM's catalog operator watches this stream to start, update, or stop catalog registry pods when catalog sources change.
  name: /apis/operators.coreos.com/v1alpha1/namespaces/{namespace}/catalogsources
  operation: subscribe
  operation_id: watchNamespacedCatalogSources
  summary: Watch CatalogSources in a namespace
- description: Watch stream for Subscription objects in a namespace. OLM watches subscriptions to detect when new operator installs are requested or existing subscriptions need to be reconciled.
  name: /apis/operators.coreos.com/v1alpha1/namespaces/{namespace}/subscriptions
  operation: subscribe
  operation_id: watchNamespacedSubscriptions
  summary: Watch Subscriptions in a namespace
- description: Watch stream for InstallPlan objects in a namespace. Used to monitor operator installation progress and detect when Manual approval plans are awaiting administrator approval.
  name: /apis/operators.coreos.com/v1alpha1/namespaces/{namespace}/installplans
  operation: subscribe
  operation_id: watchNamespacedInstallPlans
  summary: Watch InstallPlans in a namespace
- description: Watch stream for ClusterServiceVersion objects in a namespace. Operators and administrative tools watch CSVs to track installation progress, upgrades completing, and operator failures.
  name: /apis/operators.coreos.com/v1alpha1/namespaces/{namespace}/clusterserviceversions
  operation: subscribe
  operation_id: watchNamespacedClusterServiceVersions
  summary: Watch ClusterServiceVersions in a namespace
description: The Kubernetes Operators watch API provides streaming event notifications for operator-related resources including CustomResourceDefinitions, OLM resources (CatalogSources, Subscriptions, InstallPlans, ClusterServiceVersions, OperatorGroups), and custom resources managed by operators. Operators are built on the Kubernetes watch mechanism — controllers start informers that subscribe to watch streams for their owned resource types and trigger reconciliation loops when objects change. These same streams are used by cluster administrators to monitor operator installation progress and CRD lifecycle events.
layout: asyncapi
messages:
- description: A watch event delivered when a CustomResourceDefinition is created, its schema or versions are updated, or it is deleted. The status Established condition transitions to True when the API endpoint is live and ready for custom resource instances.
  name: CRDWatchEvent
  summary: Change event for a Kubernetes CRD resource
  title: CustomResourceDefinition Watch Event
- description: A watch event delivered when a CatalogSource is added, its image reference or update interval changes, or it is removed from the cluster.
  name: CatalogSourceWatchEvent
  summary: Change event for an OLM CatalogSource resource
  title: CatalogSource Watch Event
- description: A watch event delivered when an operator Subscription is created, its channel or approval mode changes, or it is deleted. Subscription creation triggers OLM to generate an InstallPlan.
  name: SubscriptionWatchEvent
  summary: Change event for an OLM Subscription resource
  title: Subscription Watch Event
- description: A watch event delivered when an InstallPlan is created by OLM or when its phase transitions. For Manual plans, this event fires when the plan is awaiting approval and again when an admin approves it.
  name: InstallPlanWatchEvent
  summary: Change event for an OLM InstallPlan resource
  title: InstallPlan Watch Event
- description: A watch event delivered when a ClusterServiceVersion is installed, transitions between phases (Pending, Installing, Succeeded, Failed), or is deleted during an upgrade or uninstall.
  name: CSVWatchEvent
  summary: Change event for an OLM ClusterServiceVersion resource
  title: ClusterServiceVersion Watch Event
name: Kubernetes Operators Watch Events
provider_name: Kubernetes Operators
provider_slug: kubernetes-operators
servers:
- description: In-cluster Kubernetes API server for watch streaming.
  name: kubernetesApiServer
  protocol: https
  url: https://kubernetes.default.svc
slug: kubernetes-operators-watch-asyncapi
source_filename: kubernetes-operators-watch-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Kubernetes Operators Watch Events\n  description: >-\n    The Kubernetes Operators watch API provides streaming event notifications\n    for operator-related resources including CustomResourceDefinitions, OLM\n    resources (CatalogSources, Subscriptions, InstallPlans, ClusterServiceVersions,\n    OperatorGroups), and custom resources managed by operators. Operators are\n    built on the Kubernetes watch mechanism — controllers start informers that\n    subscribe to watch streams for their owned resource types and trigger\n    reconciliation loops when objects change. These same streams are used by\n    cluster administrators to monitor operator installation progress and CRD\n    lifecycle events.\n  version: v1.32.0\n  contact:\n    name: Operator Framework Community\n    url: https://github.com/operator-framework/operator-lifecycle-manager\nexternalDocs:\n  description: Kubernetes API Concepts - Watch\n  url: https://kubernetes.io/docs/reference/using-api/api-concepts/\n\
  servers:\n  kubernetesApiServer:\n    url: 'https://kubernetes.default.svc'\n    protocol: https\n    description: In-cluster Kubernetes API server for watch streaming.\n    security:\n      - bearerAuth: []\n      - clientCertificate: []\nchannels:\n  /apis/apiextensions.k8s.io/v1/customresourcedefinitions:\n    description: >-\n      Watch stream for CustomResourceDefinition objects cluster-wide. CRD events\n      are generated when new custom resource types are registered, their schemas\n      are updated, or they are deleted. Operator controllers watch this channel\n      to react to CRD establishment before starting their reconciliation loops.\n    subscribe:\n      operationId: watchCustomResourceDefinitions\n      summary: Watch all CustomResourceDefinitions\n      description: >-\n        Streams WatchEvent messages for CRD lifecycle events. Fires on CRD\n        creation (ADDED), schema or version changes (MODIFIED), and deletion\n        (DELETED). The Established condition in\
  \ the status indicates when the\n        API endpoint is ready to serve requests.\n      message:\n        $ref: '#/components/messages/CRDWatchEvent'\n  /apis/operators.coreos.com/v1alpha1/namespaces/{namespace}/catalogsources:\n    description: >-\n      Watch stream for CatalogSource objects in a namespace. OLM's catalog\n      operator watches this stream to start, update, or stop catalog registry\n      pods when catalog sources change.\n    parameters:\n      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId: watchNamespacedCatalogSources\n      summary: Watch CatalogSources in a namespace\n      description: >-\n        Streams WatchEvent messages for CatalogSource changes. Fires when\n        catalog sources are added, their image or address is updated, or\n        they are deleted. Used by OLM to maintain catalog registry availability.\n      message:\n        $ref: '#/components/messages/CatalogSourceWatchEvent'\n  /apis/operators.coreos.com/v1alpha1/namespaces/{namespace}/subscriptions:\n\
  \    description: >-\n      Watch stream for Subscription objects in a namespace. OLM watches\n      subscriptions to detect when new operator installs are requested or\n      existing subscriptions need to be reconciled.\n    parameters:\n      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId: watchNamespacedSubscriptions\n      summary: Watch Subscriptions in a namespace\n      description: >-\n        Streams WatchEvent messages for Subscription changes. Fires when\n        subscriptions are created (triggering InstallPlan generation), their\n        channel changes, or upgrade approval mode is toggled.\n      message:\n        $ref: '#/components/messages/SubscriptionWatchEvent'\n  /apis/operators.coreos.com/v1alpha1/namespaces/{namespace}/installplans:\n    description: >-\n      Watch stream for InstallPlan objects in a namespace. Used to monitor\n      operator installation progress and detect when Manual approval plans\n      are\
  \ awaiting administrator approval.\n    parameters:\n      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId: watchNamespacedInstallPlans\n      summary: Watch InstallPlans in a namespace\n      description: >-\n        Streams WatchEvent messages for InstallPlan lifecycle events. Fires\n        when new plans are created, when they transition between Installing\n        and Complete phases, or when approval is granted by an administrator.\n      message:\n        $ref: '#/components/messages/InstallPlanWatchEvent'\n  /apis/operators.coreos.com/v1alpha1/namespaces/{namespace}/clusterserviceversions:\n    description: >-\n      Watch stream for ClusterServiceVersion objects in a namespace. Operators\n      and administrative tools watch CSVs to track installation progress,\n      upgrades completing, and operator failures.\n    parameters:\n      namespace:\n        $ref: '#/components/parameters/Namespace'\n    subscribe:\n      operationId:\
  \ watchNamespacedClusterServiceVersions\n      summary: Watch ClusterServiceVersions in a namespace\n      description: >-\n        Streams WatchEvent messages for CSV lifecycle events. Fires when\n        an operator's CSV transitions through Pending, Installing, Succeeded,\n        and Failed phases, enabling automated monitoring and alerting of\n        operator health.\n      message:\n        $ref: '#/components/messages/CSVWatchEvent'\ncomponents:\n  securitySchemes:\n    bearerAuth:\n      type: httpApiKey\n      name: Authorization\n      in: header\n      description: Kubernetes service account or user bearer token.\n    clientCertificate:\n      type: X509\n      description: Client TLS certificate signed by the cluster CA.\n  parameters:\n    Namespace:\n      description: Namespace name to scope the watch stream.\n      schema:\n        type: string\n  messages:\n    CRDWatchEvent:\n      name: CRDWatchEvent\n      title: CustomResourceDefinition Watch Event\n      summary:\
  \ Change event for a Kubernetes CRD resource\n      description: >-\n        A watch event delivered when a CustomResourceDefinition is created,\n        its schema or versions are updated, or it is deleted. The status\n        Established condition transitions to True when the API endpoint is\n        live and ready for custom resource instances.\n      payload:\n        $ref: '#/components/schemas/WatchEvent'\n    CatalogSourceWatchEvent:\n      name: CatalogSourceWatchEvent\n      title: CatalogSource Watch Event\n      summary: Change event for an OLM CatalogSource resource\n      description: >-\n        A watch event delivered when a CatalogSource is added, its image\n        reference or update interval changes, or it is removed from the cluster.\n      payload:\n        $ref: '#/components/schemas/WatchEvent'\n    SubscriptionWatchEvent:\n      name: SubscriptionWatchEvent\n      title: Subscription Watch Event\n      summary: Change event for an OLM Subscription resource\n   \
  \   description: >-\n        A watch event delivered when an operator Subscription is created,\n        its channel or approval mode changes, or it is deleted. Subscription\n        creation triggers OLM to generate an InstallPlan.\n      payload:\n        $ref: '#/components/schemas/WatchEvent'\n    InstallPlanWatchEvent:\n      name: InstallPlanWatchEvent\n      title: InstallPlan Watch Event\n      summary: Change event for an OLM InstallPlan resource\n      description: >-\n        A watch event delivered when an InstallPlan is created by OLM or\n        when its phase transitions. For Manual plans, this event fires when\n        the plan is awaiting approval and again when an admin approves it.\n      payload:\n        $ref: '#/components/schemas/WatchEvent'\n    CSVWatchEvent:\n      name: CSVWatchEvent\n      title: ClusterServiceVersion Watch Event\n      summary: Change event for an OLM ClusterServiceVersion resource\n      description: >-\n        A watch event delivered when\
  \ a ClusterServiceVersion is installed,\n        transitions between phases (Pending, Installing, Succeeded, Failed),\n        or is deleted during an upgrade or uninstall.\n      payload:\n        $ref: '#/components/schemas/WatchEvent'\n  schemas:\n    WatchEvent:\n      type: object\n      required:\n        - type\n        - object\n      description: >-\n        A watch event representing a state change to a Kubernetes operator\n        resource. The type field indicates the change and the object field\n        contains the full resource state after the change.\n      properties:\n        type:\n          type: string\n          enum:\n            - ADDED\n            - MODIFIED\n            - DELETED\n            - BOOKMARK\n            - ERROR\n          description: >-\n            Type of change. ADDED on creation, MODIFIED on any update,\n            DELETED on removal. BOOKMARK provides a resourceVersion checkpoint.\n        object:\n          type: object\n          description:\
  \ The resource at the time of the event.\n          properties:\n            apiVersion:\n              type: string\n              description: API version of the resource.\n            kind:\n              type: string\n              description: >-\n                Kind of the resource (e.g. CustomResourceDefinition,\n                CatalogSource, Subscription, InstallPlan, ClusterServiceVersion).\n            metadata:\n              type: object\n              description: Object metadata.\n              properties:\n                name:\n                  type: string\n                  description: Resource name.\n                namespace:\n                  type: string\n                  description: Resource namespace.\n                uid:\n                  type: string\n                  description: Unique identifier.\n                resourceVersion:\n                  type: string\n                  description: Resource version for watch resumption.\n              \
  \  generation:\n                  type: integer\n                  description: Spec generation.\n                creationTimestamp:\n                  type: string\n                  format: date-time\n                  description: Creation timestamp.\n                labels:\n                  type: object\n                  additionalProperties:\n                    type: string\n                annotations:\n                  type: object\n                  additionalProperties:\n                    type: string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/kubernetes-operators/refs/heads/main/asyncapi/kubernetes-operators-watch-asyncapi.yml
spec_file: asyncapi/kubernetes-operators-watch-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/kubernetes-operators/refs/heads/main/asyncapi/kubernetes-operators-watch-asyncapi.yml
tags:
- Automation
- Cloud Native
- DevOps
- Infrastructure
- Kubernetes
- AsyncAPI
- Webhooks
- Events
version: v1.32.0
---
