---
api_specs:
- filename: openapi.json
  format: json
  label: Temenos Transact API
  slug: temenos-transact-api
  spec_type: OpenAPI
  url: https://developer.temenos.com/transact/openapi.json
- filename: openapi.json
  format: json
  label: Temenos Infinity API
  slug: temenos-infinity-api
  spec_type: OpenAPI
  url: https://developer.temenos.com/infinity/openapi.json
- filename: openapi.json
  format: json
  label: Temenos Payments API
  slug: temenos-payments-api
  spec_type: OpenAPI
  url: https://developer.temenos.com/payments/openapi.json
- filename: openapi.json
  format: json
  label: Temenos Fund Administration API
  slug: temenos-fund-administration-api
  spec_type: OpenAPI
  url: https://developer.temenos.com/funds/openapi.json
- filename: openapi.json
  format: json
  label: Temenos Financial Crime Mitigation API
  slug: temenos-financial-crime-mitigation-api
  spec_type: OpenAPI
  url: https://developer.temenos.com/fcm/openapi.json
- filename: temenos-data-hub-openapi.yml
  format: yaml
  label: Temenos Transact Data Hub API
  slug: temenos-transact-data-hub-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-data-hub-openapi.yml
- filename: temenos-wealth-openapi.yml
  format: yaml
  label: Temenos Wealth API
  slug: temenos-wealth-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-wealth-openapi.yml
- filename: temenos-enterprise-product-pricing-openapi.yml
  format: yaml
  label: Temenos Enterprise Product and Pricing API
  slug: temenos-enterprise-product-and-pricing-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-enterprise-product-pricing-openapi.yml
- filename: temenos-cloud-banking-openapi.yml
  format: yaml
  label: Temenos Cloud Banking (CMB) API
  slug: temenos-cloud-banking-cmb-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-cloud-banking-openapi.yml
- filename: temenos-journey-manager-openapi.yml
  format: yaml
  label: Temenos Journey Manager API
  slug: temenos-journey-manager-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-journey-manager-openapi.yml
- filename: temenos-microservices-openapi.yml
  format: yaml
  label: Temenos Transact Microservices API
  slug: temenos-transact-microservices-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-microservices-openapi.yml
- filename: temenos-bnpl-openapi.yml
  format: yaml
  label: Temenos Buy Now Pay Later API
  slug: temenos-buy-now-pay-later-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/openapi/temenos-bnpl-openapi.yml
channels:
- description: Account lifecycle events including creation, closure, status changes, and balance updates for all account types.
  name: temenos.events.account
  operation: publish
  operation_id: onAccountEvent
  summary: Account event published
- description: Payment processing events including order acceptance, execution confirmation, clearing status updates, and payment failures.
  name: temenos.events.payment
  operation: publish
  operation_id: onPaymentEvent
  summary: Payment event published
- description: Customer lifecycle events including onboarding, profile updates, KYC status changes, and relationship modifications.
  name: temenos.events.customer
  operation: publish
  operation_id: onCustomerEvent
  summary: Customer event published
- description: Transaction events published when financial transactions are committed to the system including debits, credits, and transfers.
  name: temenos.events.transaction
  operation: publish
  operation_id: onTransactionEvent
  summary: Transaction event published
- description: Compliance and financial crime events including sanctions screening alerts, AML monitoring alerts, and risk score changes.
  name: temenos.events.compliance
  operation: publish
  operation_id: onComplianceEvent
  summary: Compliance event published
- description: Data replication events captured from memory when transactions are committed to the system. Used for populating the Analytics Data Store and Operational Data Store through real-time ETL processing.
  name: temenos.data.replication
  operation: publish
  operation_id: onDataReplicationEvent
  summary: Data replication event published
- description: System-level events including service health changes, configuration updates, and platform operational events.
  name: temenos.events.system
  operation: publish
  operation_id: onSystemEvent
  summary: System event published
description: Event-driven architecture for Temenos banking platform providing asynchronous integration through business and system events published to Apache Kafka topics. Enables loose coupling of Packaged Business Capabilities (PBCs) with support for both JMS point-to-point messaging for guaranteed once-and-only-once delivery and Kafka publish-subscribe for at-least-once delivery of data events. Events are published in JSON format with adapter support for XML and Avro transformation.
layout: asyncapi
messages:
- description: ''
  name: AccountCreated
  summary: Published when a new account is created
  title: Account Created
- description: ''
  name: AccountClosed
  summary: Published when an account is closed
  title: Account Closed
- description: ''
  name: AccountStatusChanged
  summary: Published when an account status changes
  title: Account Status Changed
- description: ''
  name: PaymentOrderAccepted
  summary: Published when a payment order is accepted for processing
  title: Payment Order Accepted
- description: ''
  name: PaymentOrderConfirmed
  summary: Published when a payment order is confirmed and booked
  title: Payment Order Confirmed
- description: ''
  name: PaymentOrderFailed
  summary: Published when a payment order fails processing
  title: Payment Order Failed
- description: ''
  name: CustomerOnboarded
  summary: Published when a new customer is onboarded
  title: Customer Onboarded
- description: ''
  name: CustomerUpdated
  summary: Published when customer details are updated
  title: Customer Updated
- description: ''
  name: KycStatusChanged
  summary: Published when a customer KYC status changes
  title: KYC Status Changed
- description: ''
  name: TransactionCommitted
  summary: Published when a financial transaction is committed
  title: Transaction Committed
- description: ''
  name: SanctionAlertRaised
  summary: Published when a sanctions screening alert is generated
  title: Sanction Alert Raised
- description: ''
  name: RiskScoreChanged
  summary: Published when a customer risk score is updated
  title: Risk Score Changed
- description: ''
  name: DataReplicationEvent
  summary: Published for data replication when transactions are committed
  title: Data Replication Event
- description: ''
  name: SystemEvent
  summary: Published for system-level operational events
  title: System Event
name: Temenos Banking Events
provider_name: Temenos
provider_slug: temenos
servers:
- description: Temenos Kafka cluster for event streaming. Apache Kafka serves as the distributed event streaming platform for publishing and subscribing to banking events.
  name: kafka
  protocol: kafka
  url: kafka.temenos.com:9092
- description: JMS message broker for point-to-point event delivery with guaranteed once-and-only-once delivery semantics.
  name: jms
  protocol: jms
  url: jms.temenos.com:61616
slug: temenos-events-asyncapi
source_filename: temenos-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Temenos Banking Events\n  description: >-\n    Event-driven architecture for Temenos banking platform providing\n    asynchronous integration through business and system events published\n    to Apache Kafka topics. Enables loose coupling of Packaged Business\n    Capabilities (PBCs) with support for both JMS point-to-point messaging\n    for guaranteed once-and-only-once delivery and Kafka publish-subscribe\n    for at-least-once delivery of data events. Events are published in\n    JSON format with adapter support for XML and Avro transformation.\n  version: '1.0.0'\n  contact:\n    name: Temenos Developer Support\n    url: https://developer.temenos.com/\n    email: api.support@temenos.com\n  license:\n    name: Temenos Terms of Service\n    url: https://www.temenos.com/legal-information/website-terms-and-conditions/\nservers:\n  kafka:\n    url: kafka.temenos.com:9092\n    protocol: kafka\n    description: >-\n      Temenos Kafka cluster\
  \ for event streaming. Apache Kafka serves as the\n      distributed event streaming platform for publishing and subscribing\n      to banking events.\n    security:\n      - sasl: []\n  jms:\n    url: jms.temenos.com:61616\n    protocol: jms\n    description: >-\n      JMS message broker for point-to-point event delivery with guaranteed\n      once-and-only-once delivery semantics.\n    security:\n      - userPassword: []\nchannels:\n  temenos.events.account:\n    description: >-\n      Account lifecycle events including creation, closure, status changes,\n      and balance updates for all account types.\n    publish:\n      operationId: onAccountEvent\n      summary: Account event published\n      description: >-\n        Receive notifications for account lifecycle events when accounts\n        are created, modified, closed, or have significant balance changes.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/AccountCreated'\n          - $ref: '#/components/messages/AccountClosed'\n\
  \          - $ref: '#/components/messages/AccountStatusChanged'\n  temenos.events.payment:\n    description: >-\n      Payment processing events including order acceptance, execution\n      confirmation, clearing status updates, and payment failures.\n    publish:\n      operationId: onPaymentEvent\n      summary: Payment event published\n      description: >-\n        Receive notifications for payment lifecycle events when payment\n        orders are accepted, confirmed, cleared, or fail processing.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/PaymentOrderAccepted'\n          - $ref: '#/components/messages/PaymentOrderConfirmed'\n          - $ref: '#/components/messages/PaymentOrderFailed'\n  temenos.events.customer:\n    description: >-\n      Customer lifecycle events including onboarding, profile updates,\n      KYC status changes, and relationship modifications.\n    publish:\n      operationId: onCustomerEvent\n      summary: Customer event published\n\
  \      description: >-\n        Receive notifications for customer lifecycle events when customers\n        are onboarded, updated, or have KYC status changes.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/CustomerOnboarded'\n          - $ref: '#/components/messages/CustomerUpdated'\n          - $ref: '#/components/messages/KycStatusChanged'\n  temenos.events.transaction:\n    description: >-\n      Transaction events published when financial transactions are\n      committed to the system including debits, credits, and transfers.\n    publish:\n      operationId: onTransactionEvent\n      summary: Transaction event published\n      description: >-\n        Receive notifications when financial transactions are committed\n        including debit, credit, and transfer operations.\n      message:\n        $ref: '#/components/messages/TransactionCommitted'\n  temenos.events.compliance:\n    description: >-\n      Compliance and financial crime events including sanctions\
  \ screening\n      alerts, AML monitoring alerts, and risk score changes.\n    publish:\n      operationId: onComplianceEvent\n      summary: Compliance event published\n      description: >-\n        Receive notifications for compliance events including new\n        screening alerts and risk rating changes.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/SanctionAlertRaised'\n          - $ref: '#/components/messages/RiskScoreChanged'\n  temenos.data.replication:\n    description: >-\n      Data replication events captured from memory when transactions are\n      committed to the system. Used for populating the Analytics Data Store\n      and Operational Data Store through real-time ETL processing.\n    publish:\n      operationId: onDataReplicationEvent\n      summary: Data replication event published\n      description: >-\n        Receive data change events for replicating committed transaction\n        data to downstream data stores and analytics systems.\n\
  \      message:\n        $ref: '#/components/messages/DataReplicationEvent'\n  temenos.events.system:\n    description: >-\n      System-level events including service health changes, configuration\n      updates, and platform operational events.\n    publish:\n      operationId: onSystemEvent\n      summary: System event published\n      description: >-\n        Receive notifications for system-level operational events.\n      message:\n        $ref: '#/components/messages/SystemEvent'\ncomponents:\n  securitySchemes:\n    sasl:\n      type: scramSha256\n      description: SASL/SCRAM-SHA-256 authentication for Kafka\n    userPassword:\n      type: userPassword\n      description: Username/password authentication for JMS\n  messages:\n    AccountCreated:\n      name: AccountCreated\n      title: Account Created\n      summary: Published when a new account is created\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AccountEvent'\n      headers:\n\
  \        type: object\n        properties:\n          eventType:\n            type: string\n            const: account.created\n          correlationId:\n            type: string\n          timestamp:\n            type: string\n            format: date-time\n    AccountClosed:\n      name: AccountClosed\n      title: Account Closed\n      summary: Published when an account is closed\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AccountEvent'\n      headers:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: account.closed\n    AccountStatusChanged:\n      name: AccountStatusChanged\n      title: Account Status Changed\n      summary: Published when an account status changes\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AccountEvent'\n      headers:\n        type: object\n        properties:\n          eventType:\n            type: string\n\
  \            const: account.status.changed\n    PaymentOrderAccepted:\n      name: PaymentOrderAccepted\n      title: Payment Order Accepted\n      summary: Published when a payment order is accepted for processing\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentEvent'\n      headers:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: payment.order.accepted\n    PaymentOrderConfirmed:\n      name: PaymentOrderConfirmed\n      title: Payment Order Confirmed\n      summary: Published when a payment order is confirmed and booked\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentEvent'\n      headers:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: payment.order.confirmed\n    PaymentOrderFailed:\n      name: PaymentOrderFailed\n      title: Payment Order Failed\n      summary:\
  \ Published when a payment order fails processing\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PaymentEvent'\n      headers:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: payment.order.failed\n    CustomerOnboarded:\n      name: CustomerOnboarded\n      title: Customer Onboarded\n      summary: Published when a new customer is onboarded\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CustomerEvent'\n      headers:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: customer.onboarded\n    CustomerUpdated:\n      name: CustomerUpdated\n      title: Customer Updated\n      summary: Published when customer details are updated\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CustomerEvent'\n      headers:\n        type: object\n        properties:\n\
  \          eventType:\n            type: string\n            const: customer.updated\n    KycStatusChanged:\n      name: KycStatusChanged\n      title: KYC Status Changed\n      summary: Published when a customer KYC status changes\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CustomerEvent'\n      headers:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: customer.kyc.changed\n    TransactionCommitted:\n      name: TransactionCommitted\n      title: Transaction Committed\n      summary: Published when a financial transaction is committed\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TransactionEvent'\n    SanctionAlertRaised:\n      name: SanctionAlertRaised\n      title: Sanction Alert Raised\n      summary: Published when a sanctions screening alert is generated\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ComplianceEvent'\n\
  \      headers:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: compliance.sanction.alert\n    RiskScoreChanged:\n      name: RiskScoreChanged\n      title: Risk Score Changed\n      summary: Published when a customer risk score is updated\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ComplianceEvent'\n      headers:\n        type: object\n        properties:\n          eventType:\n            type: string\n            const: compliance.risk.changed\n    DataReplicationEvent:\n      name: DataReplicationEvent\n      title: Data Replication Event\n      summary: Published for data replication when transactions are committed\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DataReplication'\n    SystemEvent:\n      name: SystemEvent\n      title: System Event\n      summary: Published for system-level operational events\n      contentType: application/json\n\
  \      payload:\n        $ref: '#/components/schemas/SystemEventPayload'\n  schemas:\n    AccountEvent:\n      type: object\n      description: Account lifecycle event payload\n      properties:\n        eventId:\n          type: string\n          description: Unique event identifier\n        eventType:\n          type: string\n          description: Event type classification\n        accountId:\n          type: string\n          description: Account identifier\n        customerId:\n          type: string\n          description: Associated customer identifier\n        accountType:\n          type: string\n          description: Account type\n        currency:\n          type: string\n          description: Account currency\n        status:\n          type: string\n          description: Account status after event\n        previousStatus:\n          type: string\n          description: Account status before event\n        timestamp:\n          type: string\n          format: date-time\n\
  \          description: Event timestamp\n        source:\n          type: string\n          description: Source application\n    PaymentEvent:\n      type: object\n      description: Payment lifecycle event payload\n      properties:\n        eventId:\n          type: string\n          description: Unique event identifier\n        eventType:\n          type: string\n          description: Event type classification\n        paymentOrderId:\n          type: string\n          description: Payment order identifier\n        debitAccountId:\n          type: string\n          description: Debit account\n        creditAccountId:\n          type: string\n          description: Credit account\n        amount:\n          type: number\n          format: double\n          description: Payment amount\n        currency:\n          type: string\n          description: Payment currency\n        paymentType:\n          type: string\n          description: Payment type\n        bookingStatus:\n         \
  \ type: string\n          description: Booking status\n        failureReason:\n          type: string\n          description: Failure reason if applicable\n        timestamp:\n          type: string\n          format: date-time\n          description: Event timestamp\n    CustomerEvent:\n      type: object\n      description: Customer lifecycle event payload\n      properties:\n        eventId:\n          type: string\n          description: Unique event identifier\n        eventType:\n          type: string\n          description: Event type classification\n        customerId:\n          type: string\n          description: Customer identifier\n        customerType:\n          type: string\n          description: Customer type\n        kycStatus:\n          type: string\n          description: Current KYC status\n        previousKycStatus:\n          type: string\n          description: Previous KYC status\n        timestamp:\n          type: string\n          format: date-time\n    \
  \      description: Event timestamp\n    TransactionEvent:\n      type: object\n      description: Financial transaction event payload\n      properties:\n        eventId:\n          type: string\n          description: Unique event identifier\n        transactionId:\n          type: string\n          description: Transaction identifier\n        accountId:\n          type: string\n          description: Account identifier\n        transactionType:\n          type: string\n          description: Transaction type\n        amount:\n          type: number\n          format: double\n          description: Transaction amount\n        currency:\n          type: string\n          description: Currency\n        debitOrCredit:\n          type: string\n          description: Debit or credit indicator\n          enum:\n            - DEBIT\n            - CREDIT\n        bookingDate:\n          type: string\n          format: date\n          description: Booking date\n        valueDate:\n          type:\
  \ string\n          format: date\n          description: Value date\n        timestamp:\n          type: string\n          format: date-time\n          description: Event timestamp\n    ComplianceEvent:\n      type: object\n      description: Compliance event payload\n      properties:\n        eventId:\n          type: string\n          description: Unique event identifier\n        eventType:\n          type: string\n          description: Event type\n        customerId:\n          type: string\n          description: Customer identifier\n        alertId:\n          type: string\n          description: Alert identifier if applicable\n        severity:\n          type: string\n          description: Event severity\n          enum:\n            - HIGH\n            - MEDIUM\n            - LOW\n        riskScore:\n          type: number\n          format: double\n          description: Risk score if applicable\n        previousRiskScore:\n          type: number\n          format: double\n\
  \          description: Previous risk score\n        details:\n          type: string\n          description: Event details\n        timestamp:\n          type: string\n          format: date-time\n          description: Event timestamp\n    DataReplication:\n      type: object\n      description: Data replication event payload\n      properties:\n        eventId:\n          type: string\n          description: Unique event identifier\n        entityType:\n          type: string\n          description: Entity type being replicated\n        entityId:\n          type: string\n          description: Entity identifier\n        operation:\n          type: string\n          description: Operation type\n          enum:\n            - CREATE\n            - UPDATE\n            - DELETE\n        data:\n          type: object\n          description: Entity data payload\n          additionalProperties: true\n        timestamp:\n          type: string\n          format: date-time\n          description:\
  \ Commit timestamp\n    SystemEventPayload:\n      type: object\n      description: System event payload\n      properties:\n        eventId:\n          type: string\n          description: Event identifier\n        eventType:\n          type: string\n          description: System event type\n        source:\n          type: string\n          description: Source service\n        severity:\n          type: string\n          description: Event severity\n          enum:\n            - INFO\n            - WARNING\n            - ERROR\n            - CRITICAL\n        message:\n          type: string\n          description: Event message\n        timestamp:\n          type: string\n          format: date-time\n          description: Event timestamp\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/asyncapi/temenos-events-asyncapi.yml
spec_file: asyncapi/temenos-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/temenos/refs/heads/main/asyncapi/temenos-events-asyncapi.yml
tags:
- Banking
- Cloud Banking
- Core Banking
- Digital Banking
- Financial Services
- Fintech
- Open Banking
- Payments
- Wealth Management
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
