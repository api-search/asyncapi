---
api_specs:
- filename: sap-business-one-service-layer-openapi.yml
  format: yaml
  label: SAP Business One Service Layer API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap/refs/heads/main/openapi/sap-business-one-service-layer-openapi.yml
- filename: sap-s4hana-cloud-business-partner-openapi.yml
  format: yaml
  label: SAP S/4HANA Cloud API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap/refs/heads/main/openapi/sap-s4hana-cloud-business-partner-openapi.yml
- filename: sap-event-mesh-asyncapi.yml
  format: yaml
  label: SAP Event Mesh API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap/refs/heads/main/asyncapi/sap-event-mesh-asyncapi.yml
- filename: sap-ai-core-openapi.yml
  format: yaml
  label: SAP AI Core API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap/refs/heads/main/openapi/sap-ai-core-openapi.yml
channels:
- description: Event emitted when a new business partner is created in SAP S/4HANA.
  name: sap/s4/beh/businesspartner/v1/BusinessPartner/Created/v1
  operation: publish
  operation_id: onBusinessPartnerCreated
  summary: Business Partner Created
- description: Event emitted when an existing business partner is modified in SAP S/4HANA.
  name: sap/s4/beh/businesspartner/v1/BusinessPartner/Changed/v1
  operation: publish
  operation_id: onBusinessPartnerChanged
  summary: Business Partner Changed
- description: Event emitted when a new sales order is created in SAP S/4HANA.
  name: sap/s4/beh/salesorder/v1/SalesOrder/Created/v1
  operation: publish
  operation_id: onSalesOrderCreated
  summary: Sales Order Created
- description: Event emitted when a sales order is modified in SAP S/4HANA.
  name: sap/s4/beh/salesorder/v1/SalesOrder/Changed/v1
  operation: publish
  operation_id: onSalesOrderChanged
  summary: Sales Order Changed
- description: Event emitted when a new purchase order is created in SAP S/4HANA.
  name: sap/s4/beh/purchaseorder/v1/PurchaseOrder/Created/v1
  operation: publish
  operation_id: onPurchaseOrderCreated
  summary: Purchase Order Created
- description: Event emitted when a material document (goods receipt, goods issue) is posted in SAP S/4HANA.
  name: sap/s4/beh/materialDocument/v1/MaterialDocument/Created/v1
  operation: publish
  operation_id: onMaterialDocumentCreated
  summary: Material Document Created
description: Event-driven messaging API for SAP Business Technology Platform supporting AMQP, MQTT, and REST protocols. Enables publish/subscribe patterns for business events across SAP and third-party applications.
layout: asyncapi
messages:
- description: ''
  name: BusinessPartnerCreated
  summary: ''
  title: Business Partner Created Event
- description: ''
  name: BusinessPartnerChanged
  summary: ''
  title: Business Partner Changed Event
- description: ''
  name: SalesOrderCreated
  summary: ''
  title: Sales Order Created Event
- description: ''
  name: SalesOrderChanged
  summary: ''
  title: Sales Order Changed Event
- description: ''
  name: PurchaseOrderCreated
  summary: ''
  title: Purchase Order Created Event
- description: ''
  name: MaterialDocumentCreated
  summary: ''
  title: Material Document Created Event
name: SAP Event Mesh Events
provider_name: SAP
provider_slug: sap
servers:
- description: SAP Event Mesh REST API endpoint
  name: restServer
  protocol: https
  url: https://enterprise-messaging-pubsub.cfapps.{region}.hana.ondemand.com
- description: SAP Event Mesh MQTT endpoint
  name: mqttServer
  protocol: mqtts
  url: mqtts://enterprise-messaging-messaging-mqtts.cfapps.{region}.hana.ondemand.com:443
- description: SAP Event Mesh AMQP endpoint
  name: amqpServer
  protocol: amqps
  url: amqps://enterprise-messaging-messaging-amqps.cfapps.{region}.hana.ondemand.com:443
slug: sap-event-mesh-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: SAP Event Mesh Events\n  description: >-\n    Event-driven messaging API for SAP Business Technology Platform supporting\n    AMQP, MQTT, and REST protocols. Enables publish/subscribe patterns for\n    business events across SAP and third-party applications.\n  version: '1.0'\n  contact:\n    name: SAP Support\n    url: https://support.sap.com/\n  termsOfService: https://www.sap.com/about/legal/terms-of-use.html\n  externalDocs:\n    description: SAP Event Mesh Documentation\n    url: https://help.sap.com/docs/event-mesh\nservers:\n  restServer:\n    url: https://enterprise-messaging-pubsub.cfapps.{region}.hana.ondemand.com\n    protocol: https\n    description: SAP Event Mesh REST API endpoint\n    variables:\n      region:\n        description: SAP BTP region identifier\n        default: eu10\n    security:\n      - oauth2: []\n  mqttServer:\n    url: mqtts://enterprise-messaging-messaging-mqtts.cfapps.{region}.hana.ondemand.com:443\n    protocol:\
  \ mqtts\n    description: SAP Event Mesh MQTT endpoint\n    variables:\n      region:\n        default: eu10\n    security:\n      - oauth2: []\n  amqpServer:\n    url: amqps://enterprise-messaging-messaging-amqps.cfapps.{region}.hana.ondemand.com:443\n    protocol: amqps\n    description: SAP Event Mesh AMQP endpoint\n    variables:\n      region:\n        default: eu10\n    security:\n      - oauth2: []\nchannels:\n  sap/s4/beh/businesspartner/v1/BusinessPartner/Created/v1:\n    description: >-\n      Event emitted when a new business partner is created in SAP S/4HANA.\n    publish:\n      operationId: onBusinessPartnerCreated\n      summary: Business Partner Created\n      message:\n        $ref: '#/components/messages/BusinessPartnerCreated'\n  sap/s4/beh/businesspartner/v1/BusinessPartner/Changed/v1:\n    description: >-\n      Event emitted when an existing business partner is modified in SAP S/4HANA.\n    publish:\n      operationId: onBusinessPartnerChanged\n      summary: Business\
  \ Partner Changed\n      message:\n        $ref: '#/components/messages/BusinessPartnerChanged'\n  sap/s4/beh/salesorder/v1/SalesOrder/Created/v1:\n    description: >-\n      Event emitted when a new sales order is created in SAP S/4HANA.\n    publish:\n      operationId: onSalesOrderCreated\n      summary: Sales Order Created\n      message:\n        $ref: '#/components/messages/SalesOrderCreated'\n  sap/s4/beh/salesorder/v1/SalesOrder/Changed/v1:\n    description: >-\n      Event emitted when a sales order is modified in SAP S/4HANA.\n    publish:\n      operationId: onSalesOrderChanged\n      summary: Sales Order Changed\n      message:\n        $ref: '#/components/messages/SalesOrderChanged'\n  sap/s4/beh/purchaseorder/v1/PurchaseOrder/Created/v1:\n    description: >-\n      Event emitted when a new purchase order is created in SAP S/4HANA.\n    publish:\n      operationId: onPurchaseOrderCreated\n      summary: Purchase Order Created\n      message:\n        $ref: '#/components/messages/PurchaseOrderCreated'\n\
  \  sap/s4/beh/materialDocument/v1/MaterialDocument/Created/v1:\n    description: >-\n      Event emitted when a material document (goods receipt, goods issue) is\n      posted in SAP S/4HANA.\n    publish:\n      operationId: onMaterialDocumentCreated\n      summary: Material Document Created\n      message:\n        $ref: '#/components/messages/MaterialDocumentCreated'\ncomponents:\n  securitySchemes:\n    oauth2:\n      type: oauth2\n      flows:\n        clientCredentials:\n          tokenUrl: https://{subdomain}.authentication.{region}.hana.ondemand.com/oauth/token\n          scopes: {}\n  messages:\n    BusinessPartnerCreated:\n      name: BusinessPartnerCreated\n      title: Business Partner Created Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BusinessPartnerEvent'\n    BusinessPartnerChanged:\n      name: BusinessPartnerChanged\n      title: Business Partner Changed Event\n      contentType: application/json\n      payload:\n  \
  \      $ref: '#/components/schemas/BusinessPartnerEvent'\n    SalesOrderCreated:\n      name: SalesOrderCreated\n      title: Sales Order Created Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SalesOrderEvent'\n    SalesOrderChanged:\n      name: SalesOrderChanged\n      title: Sales Order Changed Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SalesOrderEvent'\n    PurchaseOrderCreated:\n      name: PurchaseOrderCreated\n      title: Purchase Order Created Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PurchaseOrderEvent'\n    MaterialDocumentCreated:\n      name: MaterialDocumentCreated\n      title: Material Document Created Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/MaterialDocumentEvent'\n  schemas:\n    BusinessPartnerEvent:\n      type: object\n      properties:\n        BusinessPartner:\n\
  \          type: string\n          description: Business partner number\n        BusinessPartnerFullName:\n          type: string\n          description: Full name of the business partner\n        BusinessPartnerCategory:\n          type: string\n          description: Category (1=Organization, 2=Person)\n    SalesOrderEvent:\n      type: object\n      properties:\n        SalesOrder:\n          type: string\n          description: Sales order number\n        SalesOrderType:\n          type: string\n          description: Sales document type\n        SoldToParty:\n          type: string\n          description: Sold-to party business partner number\n        CreationDate:\n          type: string\n          format: date\n          description: Document creation date\n        TotalNetAmount:\n          type: number\n          description: Total net value of the order\n    PurchaseOrderEvent:\n      type: object\n      properties:\n        PurchaseOrder:\n          type: string\n          description:\
  \ Purchase order number\n        PurchaseOrderType:\n          type: string\n          description: Purchase order type\n        Supplier:\n          type: string\n          description: Supplier business partner number\n        CreationDate:\n          type: string\n          format: date\n    MaterialDocumentEvent:\n      type: object\n      properties:\n        MaterialDocument:\n          type: string\n          description: Material document number\n        MaterialDocumentYear:\n          type: string\n          description: Material document year\n        GoodsMovementType:\n          type: string\n          description: Goods movement type code\n        PostingDate:\n          type: string\n          format: date\n          description: Posting date\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sap/refs/heads/main/asyncapi/sap-event-mesh-asyncapi.yml
spec_file: asyncapi/sap-event-mesh-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/sap/refs/heads/main/asyncapi/sap-event-mesh-asyncapi.yml
tags:
- AI
- BTP
- Business Applications
- Cloud
- Data Management
- Enterprise
- ERP
- Integration
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
