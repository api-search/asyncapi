---
api_specs:
- filename: upvest-investment-api-openapi.yml
  format: yaml
  label: Upvest Investment API
  slug: investment-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/upvest/refs/heads/main/openapi/upvest-investment-api-openapi.yml
channels:
- description: The webhook delivery channel. Upvest sends HTTPS POST requests to your registered endpoint containing one or more events. Events within a single request are ordered by created_at in ascending order. There are no ordering guarantees across separate requests.
  name: /webhook
  operation: publish
  operation_id: receiveWebhookEvents
  summary: Receive webhook event notifications
description: The Upvest Investment API uses an asynchronous, event-driven architecture where events represent state changes within the system. Webhook subscriptions allow your application to receive real-time notifications about user onboarding, order lifecycle changes, portfolio rebalancing, payment processing, and other investment operations. Events are delivered via HTTPS POST requests with at-least-once delivery semantics, meaning your handler must be idempotent.
layout: asyncapi
messages:
- description: ''
  name: UserEvent
  summary: Events related to user lifecycle changes including creation, updates, and status transitions.
  title: User Event
- description: ''
  name: UserCheckEvent
  summary: Events related to user compliance and verification check outcomes.
  title: User Check Event
- description: ''
  name: AccountEvent
  summary: Events related to investment account lifecycle changes including opening, closing, and status updates.
  title: Account Event
- description: ''
  name: AccountGroupEvent
  summary: Events related to account group changes.
  title: Account Group Event
- description: ''
  name: OrderEvent
  summary: Events related to the order lifecycle including placement, processing, filling, and rejection. Every order status change emits a webhook event.
  title: Order Event
- description: ''
  name: OrderCancellationEvent
  summary: Events related to order cancellation requests and their outcomes.
  title: Order Cancellation Event
- description: ''
  name: ExecutionEvent
  summary: Events related to order execution fills. Every execution associated with an order has its own set of statuses, and every status change emits a webhook event.
  title: Execution Event
- description: ''
  name: PositionEvent
  summary: Events related to changes in holdings and positions within accounts.
  title: Position Event
- description: ''
  name: CashBalanceEvent
  summary: Events related to changes in account cash balances.
  title: Cash Balance Event
- description: ''
  name: PortfolioEvent
  summary: Events related to portfolio creation, updates, and allocation changes.
  title: Portfolio Event
- description: ''
  name: RebalancingEvent
  summary: Events related to portfolio rebalancing execution and completion.
  title: Rebalancing Event
- description: ''
  name: SavingsPlanEvent
  summary: Events related to savings plan creation, execution, and status changes.
  title: Savings Plan Event
- description: ''
  name: DirectDebitEvent
  summary: Events related to direct debit funding operations and their status transitions.
  title: Direct Debit Event
- description: ''
  name: WithdrawalEvent
  summary: Events related to cash withdrawal processing and completion.
  title: Withdrawal Event
- description: ''
  name: MandateEvent
  summary: Events related to direct debit mandate creation and revocation.
  title: Mandate Event
- description: ''
  name: SecuritiesTransferEvent
  summary: Events related to inbound and outbound securities transfer operations.
  title: Securities Transfer Event
- description: ''
  name: AccountTransferEvent
  summary: Events related to account transfer operations between entities.
  title: Account Transfer Event
- description: ''
  name: CorporateActionEvent
  summary: Events related to corporate actions on held securities such as dividends, splits, and mergers.
  title: Corporate Action Event
- description: ''
  name: LiquidationEvent
  summary: Events related to account liquidation operations.
  title: Liquidation Event
- description: ''
  name: ReportEvent
  summary: Events related to report generation completion.
  title: Report Event
- description: ''
  name: FeeEvent
  summary: Events related to fee charges on accounts.
  title: Fee Event
name: Upvest Investment Events
provider_name: Upvest
provider_slug: upvest
servers:
- description: Your registered webhook endpoint. Must use HTTPS with TLS 1.2 or higher. The host must be a DNS name, not an IP address.
  name: production
  protocol: https
  url: '{webhookUrl}'
slug: upvest-investment-events-asyncapi
source_filename: upvest-investment-events-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Upvest Investment Events\n  description: >-\n    The Upvest Investment API uses an asynchronous, event-driven architecture\n    where events represent state changes within the system. Webhook\n    subscriptions allow your application to receive real-time notifications\n    about user onboarding, order lifecycle changes, portfolio rebalancing,\n    payment processing, and other investment operations. Events are delivered\n    via HTTPS POST requests with at-least-once delivery semantics, meaning\n    your handler must be idempotent.\n  version: '1.0.0'\n  contact:\n    name: Upvest Support\n    url: https://upvest.co/\n  externalDocs:\n    description: Upvest Webhooks Documentation\n    url: https://docs.upvest.co/documentation/concepts/api_concepts/webhooks\nservers:\n  production:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your registered webhook endpoint. Must use HTTPS with TLS 1.2 or\n      higher. The host\
  \ must be a DNS name, not an IP address.\n    variables:\n      webhookUrl:\n        description: >-\n          The HTTPS URL registered as your webhook endpoint.\n    security:\n      - httpSignature: []\nchannels:\n  /webhook:\n    description: >-\n      The webhook delivery channel. Upvest sends HTTPS POST requests to your\n      registered endpoint containing one or more events. Events within a\n      single request are ordered by created_at in ascending order. There are\n      no ordering guarantees across separate requests.\n    publish:\n      operationId: receiveWebhookEvents\n      summary: Receive webhook event notifications\n      description: >-\n        Receive one or more event notifications from the Upvest Investment\n        API. Each request contains a payload array with event objects. Your\n        handler should return a 2xx status code to acknowledge receipt.\n        Events may be delivered more than once, so implement idempotent\n        processing using the event\
  \ id field.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/UserEvent'\n          - $ref: '#/components/messages/UserCheckEvent'\n          - $ref: '#/components/messages/AccountEvent'\n          - $ref: '#/components/messages/AccountGroupEvent'\n          - $ref: '#/components/messages/OrderEvent'\n          - $ref: '#/components/messages/OrderCancellationEvent'\n          - $ref: '#/components/messages/ExecutionEvent'\n          - $ref: '#/components/messages/PositionEvent'\n          - $ref: '#/components/messages/CashBalanceEvent'\n          - $ref: '#/components/messages/PortfolioEvent'\n          - $ref: '#/components/messages/RebalancingEvent'\n          - $ref: '#/components/messages/SavingsPlanEvent'\n          - $ref: '#/components/messages/DirectDebitEvent'\n          - $ref: '#/components/messages/WithdrawalEvent'\n          - $ref: '#/components/messages/MandateEvent'\n          - $ref: '#/components/messages/SecuritiesTransferEvent'\n          -\
  \ $ref: '#/components/messages/AccountTransferEvent'\n          - $ref: '#/components/messages/CorporateActionEvent'\n          - $ref: '#/components/messages/LiquidationEvent'\n          - $ref: '#/components/messages/ReportEvent'\n          - $ref: '#/components/messages/FeeEvent'\ncomponents:\n  securitySchemes:\n    httpSignature:\n      type: httpApiKey\n      name: Signature\n      in: header\n      description: >-\n        Upvest signs webhook requests using HTTP message signatures. Your\n        handler should verify the signature to ensure the request originated\n        from Upvest and was not tampered with in transit.\n  messages:\n    UserEvent:\n      name: UserEvent\n      title: User Event\n      summary: >-\n        Events related to user lifecycle changes including creation, updates,\n        and status transitions.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n      examples:\n        - name: UserCreated\n \
  \         payload:\n            payload:\n              - id: fbecea50-2f35-4969-96af-342271da9eca\n                created_at: '2024-01-15T14:10:00.000Z'\n                event_type: USER.CREATED\n                object:\n                  id: 83d83ec2-d2ca-49ff-bbea-b92b5c3be202\n                  type: USER\n                webhook_id: 091915d8-7b4b-4d25-8208-f8e2d4b30070\n    UserCheckEvent:\n      name: UserCheckEvent\n      title: User Check Event\n      summary: >-\n        Events related to user compliance and verification check outcomes.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    AccountEvent:\n      name: AccountEvent\n      title: Account Event\n      summary: >-\n        Events related to investment account lifecycle changes including\n        opening, closing, and status updates.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    AccountGroupEvent:\n\
  \      name: AccountGroupEvent\n      title: Account Group Event\n      summary: >-\n        Events related to account group changes.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    OrderEvent:\n      name: OrderEvent\n      title: Order Event\n      summary: >-\n        Events related to the order lifecycle including placement, processing,\n        filling, and rejection. Every order status change emits a webhook\n        event.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    OrderCancellationEvent:\n      name: OrderCancellationEvent\n      title: Order Cancellation Event\n      summary: >-\n        Events related to order cancellation requests and their outcomes.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    ExecutionEvent:\n      name: ExecutionEvent\n      title: Execution Event\n      summary:\
  \ >-\n        Events related to order execution fills. Every execution associated\n        with an order has its own set of statuses, and every status change\n        emits a webhook event.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    PositionEvent:\n      name: PositionEvent\n      title: Position Event\n      summary: >-\n        Events related to changes in holdings and positions within accounts.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    CashBalanceEvent:\n      name: CashBalanceEvent\n      title: Cash Balance Event\n      summary: >-\n        Events related to changes in account cash balances.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    PortfolioEvent:\n      name: PortfolioEvent\n      title: Portfolio Event\n      summary: >-\n        Events related to portfolio creation, updates,\
  \ and allocation changes.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    RebalancingEvent:\n      name: RebalancingEvent\n      title: Rebalancing Event\n      summary: >-\n        Events related to portfolio rebalancing execution and completion.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    SavingsPlanEvent:\n      name: SavingsPlanEvent\n      title: Savings Plan Event\n      summary: >-\n        Events related to savings plan creation, execution, and status changes.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    DirectDebitEvent:\n      name: DirectDebitEvent\n      title: Direct Debit Event\n      summary: >-\n        Events related to direct debit funding operations and their status\n        transitions.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n\
  \    WithdrawalEvent:\n      name: WithdrawalEvent\n      title: Withdrawal Event\n      summary: >-\n        Events related to cash withdrawal processing and completion.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    MandateEvent:\n      name: MandateEvent\n      title: Mandate Event\n      summary: >-\n        Events related to direct debit mandate creation and revocation.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    SecuritiesTransferEvent:\n      name: SecuritiesTransferEvent\n      title: Securities Transfer Event\n      summary: >-\n        Events related to inbound and outbound securities transfer operations.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    AccountTransferEvent:\n      name: AccountTransferEvent\n      title: Account Transfer Event\n      summary: >-\n        Events related\
  \ to account transfer operations between entities.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    CorporateActionEvent:\n      name: CorporateActionEvent\n      title: Corporate Action Event\n      summary: >-\n        Events related to corporate actions on held securities such as\n        dividends, splits, and mergers.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    LiquidationEvent:\n      name: LiquidationEvent\n      title: Liquidation Event\n      summary: >-\n        Events related to account liquidation operations.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n    ReportEvent:\n      name: ReportEvent\n      title: Report Event\n      summary: >-\n        Events related to report generation completion.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n\
  \    FeeEvent:\n      name: FeeEvent\n      title: Fee Event\n      summary: >-\n        Events related to fee charges on accounts.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WebhookPayload'\n  schemas:\n    WebhookPayload:\n      type: object\n      description: >-\n        The top-level webhook request payload containing a list of event\n        objects. Events within a request are ordered by created_at in\n        ascending order.\n      required:\n        - payload\n      properties:\n        payload:\n          type: array\n          description: >-\n            A list of event objects, each representing a state change.\n          items:\n            $ref: '#/components/schemas/WebhookEvent'\n    WebhookEvent:\n      type: object\n      description: >-\n        An individual event record representing a state change within the\n        Upvest Investment API.\n      required:\n        - id\n        - created_at\n        - event_type\n \
  \       - object\n        - webhook_id\n      properties:\n        id:\n          type: string\n          format: uuid\n          description: >-\n            The unique identifier of the event. Use this for idempotent\n            processing.\n        created_at:\n          type: string\n          format: date-time\n          description: >-\n            The timestamp when the event occurred.\n        event_type:\n          type: string\n          description: >-\n            The event type in CATEGORY.ACTION format. The category corresponds\n            to the resource type, and the action describes what changed.\n          examples:\n            - USER.CREATED\n            - USER.UPDATED\n            - USER_CHECK.PASSED\n            - USER_CHECK.FAILED\n            - ACCOUNT.OPENED\n            - ACCOUNT.CLOSED\n            - ORDER.NEW\n            - ORDER.PROCESSING\n            - ORDER.FILLED\n            - ORDER.CANCELLED\n            - ORDER.REJECTED\n            - ORDER_CANCELLATION.CONFIRMED\n\
  \            - ORDER_CANCELLATION.REJECTED\n            - EXECUTION.NEW\n            - EXECUTION.SETTLED\n            - EXECUTION.CANCELLED\n            - POSITION.UPDATED\n            - CASH_BALANCE.UPDATED\n            - PORTFOLIO.CREATED\n            - PORTFOLIO.UPDATED\n            - REBALANCING.COMPLETED\n            - REBALANCING.FAILED\n            - SAVINGS_PLAN.EXECUTED\n            - DIRECT_DEBIT.COMPLETED\n            - DIRECT_DEBIT.FAILED\n            - WITHDRAWAL.COMPLETED\n            - WITHDRAWAL.FAILED\n            - SECURITIES_TRANSFER.COMPLETED\n            - CORPORATE_ACTION.PROCESSED\n            - LIQUIDATION.COMPLETED\n            - REPORT.READY\n            - FEE.CHARGED\n        object:\n          $ref: '#/components/schemas/EventObject'\n        webhook_id:\n          type: string\n          format: uuid\n          description: >-\n            The identifier of the webhook subscription that triggered this\n            delivery.\n    EventObject:\n      type: object\n\
  \      description: >-\n        A reference to the resource that changed.\n      required:\n        - id\n        - type\n      properties:\n        id:\n          type: string\n          format: uuid\n          description: >-\n            The unique identifier of the affected resource.\n        type:\n          type: string\n          description: >-\n            The resource type.\n          enum:\n            - USER\n            - USER_CHECK\n            - ACCOUNT\n            - ACCOUNT_GROUP\n            - ORDER\n            - ORDER_CANCELLATION\n            - EXECUTION\n            - POSITION\n            - CASH_BALANCE\n            - PORTFOLIO\n            - REBALANCING\n            - SAVINGS_PLAN\n            - DIRECT_DEBIT\n            - WITHDRAWAL\n            - MANDATE\n            - SECURITIES_TRANSFER\n            - ACCOUNT_TRANSFER\n            - CORPORATE_ACTION\n            - LIQUIDATION\n            - REPORT\n            - FEE\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/upvest/refs/heads/main/asyncapi/upvest-investment-events-asyncapi.yml
spec_file: asyncapi/upvest-investment-events-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/upvest/refs/heads/main/asyncapi/upvest-investment-events-asyncapi.yml
tags:
- Banking Infrastructure
- Fintech
- Investments
- Securities
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
