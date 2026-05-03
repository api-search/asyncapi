---
api_specs:
- filename: uniblock-unified-api-openapi.yml
  format: yaml
  label: Uniblock Unified API
  slug: unified-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uniblock/refs/heads/main/openapi/uniblock-unified-api-openapi.yml
- filename: uniblock-direct-api-openapi.yml
  format: yaml
  label: Uniblock Direct API
  slug: direct-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uniblock/refs/heads/main/openapi/uniblock-direct-api-openapi.yml
- filename: uniblock-json-rpc-api-openapi.yml
  format: yaml
  label: Uniblock JSON-RPC API
  slug: json-rpc-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uniblock/refs/heads/main/openapi/uniblock-json-rpc-api-openapi.yml
channels:
- description: Notifications triggered when a tracked address sends or receives transactions, including native token transfers and token activity. Provides real-time insights into portfolio changes and wallet movements.
  name: /webhook/address-activity
  operation: publish
  operation_id: onAddressActivity
  summary: Address activity event
- description: Notifications triggered when fungible token transfers occur involving tracked addresses or contracts, including ERC-20 transfers, approvals, and swap events.
  name: /webhook/token-transfer
  operation: publish
  operation_id: onTokenTransfer
  summary: Token transfer event
- description: Notifications triggered when NFT transfers occur involving tracked addresses or collections, including mints, sales, and transfers.
  name: /webhook/nft-transfer
  operation: publish
  operation_id: onNftTransfer
  summary: NFT transfer event
- description: Notifications triggered when a specific pending transaction is confirmed and included in a mined block.
  name: /webhook/mined-transaction
  operation: publish
  operation_id: onMinedTransaction
  summary: Mined transaction event
description: Uniblock webhooks enable real-time notifications for blockchain events without the need to poll endpoints. By configuring webhooks through the Uniblock dashboard or API, developers can receive HTTP callbacks whenever specific on-chain activities occur, such as address activity, token transfers, NFT transfers, and mined transactions. Webhook payloads include detailed event data and are signed for authentication.
layout: asyncapi
messages:
- description: ''
  name: AddressActivityEvent
  summary: Notification of transaction activity involving a tracked address.
  title: Address Activity Event
- description: ''
  name: TokenTransferEvent
  summary: Notification of a fungible token transfer matching configured filters.
  title: Token Transfer Event
- description: ''
  name: NftTransferEvent
  summary: Notification of an NFT transfer matching configured filters.
  title: NFT Transfer Event
- description: ''
  name: MinedTransactionEvent
  summary: Notification that a monitored transaction has been mined and confirmed.
  title: Mined Transaction Event
name: Uniblock Webhook Events
provider_name: Uniblock
provider_slug: uniblock
servers:
- description: Your application's webhook endpoint URL configured in the Uniblock dashboard. Uniblock sends HTTP POST requests to this URL when matching blockchain events are detected.
  name: webhookServer
  protocol: https
  url: '{webhookUrl}'
slug: uniblock-webhooks-asyncapi
source_filename: uniblock-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Uniblock Webhook Events\n  description: >-\n    Uniblock webhooks enable real-time notifications for blockchain events\n    without the need to poll endpoints. By configuring webhooks through the\n    Uniblock dashboard or API, developers can receive HTTP callbacks whenever\n    specific on-chain activities occur, such as address activity, token\n    transfers, NFT transfers, and mined transactions. Webhook payloads include\n    detailed event data and are signed for authentication.\n  version: '1.0'\n  contact:\n    name: Uniblock Support\n    url: https://docs.uniblock.dev\n  externalDocs:\n    description: Uniblock Webhook Documentation\n    url: https://docs.uniblock.dev/docs/event-trigger-types\nservers:\n  webhookServer:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your application's webhook endpoint URL configured in the Uniblock\n      dashboard. Uniblock sends HTTP POST requests to this URL when matching\n\
  \      blockchain events are detected.\n    variables:\n      webhookUrl:\n        description: >-\n          The HTTPS URL of your webhook endpoint that will receive event\n          notifications.\n    security:\n      - webhookSignature: []\nchannels:\n  /webhook/address-activity:\n    description: >-\n      Notifications triggered when a tracked address sends or receives\n      transactions, including native token transfers and token activity.\n      Provides real-time insights into portfolio changes and wallet movements.\n    publish:\n      operationId: onAddressActivity\n      summary: Address activity event\n      description: >-\n        Triggered when a monitored blockchain address has any inbound or\n        outbound transaction activity, including native token sends and\n        receives.\n      message:\n        $ref: '#/components/messages/AddressActivityEvent'\n  /webhook/token-transfer:\n    description: >-\n      Notifications triggered when fungible token transfers occur\
  \ involving\n      tracked addresses or contracts, including ERC-20 transfers, approvals,\n      and swap events.\n    publish:\n      operationId: onTokenTransfer\n      summary: Token transfer event\n      description: >-\n        Triggered when a fungible token transfer occurs that matches the\n        configured filter criteria, such as specific sender or receiver\n        addresses or token contract addresses.\n      message:\n        $ref: '#/components/messages/TokenTransferEvent'\n  /webhook/nft-transfer:\n    description: >-\n      Notifications triggered when NFT transfers occur involving tracked\n      addresses or collections, including mints, sales, and transfers.\n    publish:\n      operationId: onNftTransfer\n      summary: NFT transfer event\n      description: >-\n        Triggered when an NFT transfer event occurs that matches the\n        configured filter criteria, including ERC-721 and ERC-1155 transfers.\n      message:\n        $ref: '#/components/messages/NftTransferEvent'\n\
  \  /webhook/mined-transaction:\n    description: >-\n      Notifications triggered when a specific pending transaction is\n      confirmed and included in a mined block.\n    publish:\n      operationId: onMinedTransaction\n      summary: Mined transaction event\n      description: >-\n        Triggered when a transaction that was being monitored has been\n        successfully mined and confirmed on the blockchain.\n      message:\n        $ref: '#/components/messages/MinedTransactionEvent'\ncomponents:\n  securitySchemes:\n    webhookSignature:\n      type: httpApiKey\n      name: x-uniblock-signature\n      in: header\n      description: >-\n        HMAC signature used to verify that webhook payloads originate from\n        Uniblock. Computed using the webhook secret key configured in the\n        Uniblock dashboard.\n  messages:\n    AddressActivityEvent:\n      name: AddressActivityEvent\n      title: Address Activity Event\n      summary: >-\n        Notification of transaction activity\
  \ involving a tracked address.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AddressActivityPayload'\n    TokenTransferEvent:\n      name: TokenTransferEvent\n      title: Token Transfer Event\n      summary: >-\n        Notification of a fungible token transfer matching configured filters.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TokenTransferPayload'\n    NftTransferEvent:\n      name: NftTransferEvent\n      title: NFT Transfer Event\n      summary: >-\n        Notification of an NFT transfer matching configured filters.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/NftTransferPayload'\n    MinedTransactionEvent:\n      name: MinedTransactionEvent\n      title: Mined Transaction Event\n      summary: >-\n        Notification that a monitored transaction has been mined and confirmed.\n      contentType: application/json\n      payload:\n        $ref:\
  \ '#/components/schemas/MinedTransactionPayload'\n  schemas:\n    WebhookMetadata:\n      type: object\n      description: >-\n        Common metadata included in all webhook event payloads.\n      properties:\n        webhookId:\n          type: string\n          description: >-\n            The unique identifier of the webhook subscription that triggered\n            this notification.\n        eventType:\n          type: string\n          description: >-\n            The type of event that triggered the webhook.\n          enum:\n            - ADDRESS_ACTIVITY\n            - TOKEN_TRANSFER\n            - NFT_TRANSFER\n            - MINED_TRANSACTION\n        chain:\n          type: string\n          description: >-\n            The blockchain network on which the event occurred.\n        timestamp:\n          type: string\n          format: date-time\n          description: >-\n            The timestamp when the event was detected by Uniblock.\n    AddressActivityPayload:\n      type:\
  \ object\n      description: >-\n        Payload delivered when transaction activity is detected for a\n        monitored address.\n      properties:\n        metadata:\n          $ref: '#/components/schemas/WebhookMetadata'\n        data:\n          type: object\n          description: >-\n            Address activity event data.\n          properties:\n            address:\n              type: string\n              description: >-\n                The monitored address involved in the activity.\n            direction:\n              type: string\n              description: >-\n                Whether the address was the sender or receiver.\n              enum:\n                - inbound\n                - outbound\n            transactionHash:\n              type: string\n              description: >-\n                The hash of the transaction.\n            from:\n              type: string\n              description: >-\n                The sender address.\n            to:\n     \
  \         type: string\n              description: >-\n                The recipient address.\n            value:\n              type: string\n              description: >-\n                The value transferred in the native token's smallest unit.\n            blockNumber:\n              type: integer\n              description: >-\n                The block number containing the transaction.\n            blockTimestamp:\n              type: string\n              format: date-time\n              description: >-\n                The timestamp of the block.\n    TokenTransferPayload:\n      type: object\n      description: >-\n        Payload delivered when a token transfer event is detected.\n      properties:\n        metadata:\n          $ref: '#/components/schemas/WebhookMetadata'\n        data:\n          type: object\n          description: >-\n            Token transfer event data.\n          properties:\n            transactionHash:\n              type: string\n              description:\
  \ >-\n                The hash of the transaction containing the transfer.\n            from:\n              type: string\n              description: >-\n                The sender address.\n            to:\n              type: string\n              description: >-\n                The recipient address.\n            contractAddress:\n              type: string\n              description: >-\n                The smart contract address of the transferred token.\n            tokenName:\n              type: string\n              description: >-\n                The name of the transferred token.\n            tokenSymbol:\n              type: string\n              description: >-\n                The symbol of the transferred token.\n            value:\n              type: string\n              description: >-\n                The amount transferred in the token's smallest unit.\n            decimals:\n              type: integer\n              description: >-\n                The number of\
  \ decimal places for the token.\n            blockNumber:\n              type: integer\n              description: >-\n                The block number containing the transfer.\n            blockTimestamp:\n              type: string\n              format: date-time\n              description: >-\n                The timestamp of the block.\n    NftTransferPayload:\n      type: object\n      description: >-\n        Payload delivered when an NFT transfer event is detected.\n      properties:\n        metadata:\n          $ref: '#/components/schemas/WebhookMetadata'\n        data:\n          type: object\n          description: >-\n            NFT transfer event data.\n          properties:\n            transactionHash:\n              type: string\n              description: >-\n                The hash of the transaction containing the transfer.\n            from:\n              type: string\n              description: >-\n                The sender address.\n            to:\n        \
  \      type: string\n              description: >-\n                The recipient address.\n            contractAddress:\n              type: string\n              description: >-\n                The smart contract address of the NFT collection.\n            tokenId:\n              type: string\n              description: >-\n                The token ID of the transferred NFT.\n            tokenType:\n              type: string\n              description: >-\n                The token standard type.\n              enum:\n                - ERC-721\n                - ERC-1155\n            quantity:\n              type: integer\n              description: >-\n                The number of tokens transferred (relevant for ERC-1155).\n            blockNumber:\n              type: integer\n              description: >-\n                The block number containing the transfer.\n            blockTimestamp:\n              type: string\n              format: date-time\n              description:\
  \ >-\n                The timestamp of the block.\n    MinedTransactionPayload:\n      type: object\n      description: >-\n        Payload delivered when a monitored transaction has been mined.\n      properties:\n        metadata:\n          $ref: '#/components/schemas/WebhookMetadata'\n        data:\n          type: object\n          description: >-\n            Mined transaction event data.\n          properties:\n            transactionHash:\n              type: string\n              description: >-\n                The hash of the mined transaction.\n            from:\n              type: string\n              description: >-\n                The sender address.\n            to:\n              type: string\n              description: >-\n                The recipient address.\n            value:\n              type: string\n              description: >-\n                The value transferred in the native token's smallest unit.\n            status:\n              type: string\n \
  \             description: >-\n                The execution status of the transaction.\n              enum:\n                - success\n                - failed\n            blockNumber:\n              type: integer\n              description: >-\n                The block number in which the transaction was mined.\n            blockTimestamp:\n              type: string\n              format: date-time\n              description: >-\n                The timestamp of the block.\n            gasUsed:\n              type: string\n              description: >-\n                The amount of gas consumed by the transaction.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/uniblock/refs/heads/main/asyncapi/uniblock-webhooks-asyncapi.yml
spec_file: asyncapi/uniblock-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/uniblock/refs/heads/main/asyncapi/uniblock-webhooks-asyncapi.yml
tags:
- Blockchain
- Web3
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
