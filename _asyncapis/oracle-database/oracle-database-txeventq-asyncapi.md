---
api_specs:
- filename: openapi.yaml
  format: yaml
  label: Oracle REST Data Services (ORDS)
  slug: oracle-rest-data-services-ords
  spec_type: OpenAPI
  url: https://docs.oracle.com/en/database/oracle/oracle-rest-data-services/
- filename: openapi.yaml
  format: yaml
  label: Oracle Cloud Infrastructure Database API
  slug: oracle-cloud-infrastructure-database-api
  spec_type: OpenAPI
  url: https://docs.oracle.com/iaas/api/#/en/database/
- filename: oracle-database-soda-openapi.yml
  format: yaml
  label: Oracle SODA (Simple Oracle Document Access)
  slug: oracle-soda-simple-oracle-document-access
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/oracle-database/refs/heads/main/openapi/oracle-database-soda-openapi.yml
- filename: oracle-database-txeventq-asyncapi.yml
  format: yaml
  label: Oracle Transactional Event Queues (TxEventQ)
  slug: oracle-transactional-event-queues-txeventq
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/oracle-database/refs/heads/main/asyncapi/oracle-database-txeventq-asyncapi.yml
channels:
- description: A TxEventQ topic represents an ordered, partitioned event stream stored in Oracle Database. Topics support multiple producers and consumer groups with exactly-once delivery semantics backed by database transactions.
  name: database/txeventq/topics/{topicName}
  operation: publish
  operation_id: produceMessage
  summary: Produce a message to a topic
- description: Topic management channel for listing all available TxEventQ topics
  name: database/txeventq/topics
  operation: subscribe
  operation_id: listTopics
  summary: List all TxEventQ topics
- description: Cluster-scoped topic management channel
  name: database/txeventq/clusters/{clusterId}/topics
  operation: publish
  operation_id: createTopic
  summary: Create a new topic
- description: Consumer group management channel
  name: database/txeventq/clusters/{clusterId}/consumer-groups/{consumerGroupId}
  operation: publish
  operation_id: createConsumerGroup
  summary: Create a consumer group
- description: Message consumption endpoint for fetching messages from a consumer instance
  name: database/txeventq/consumers/{groupName}/instances/{instanceId}/records
  operation: subscribe
  operation_id: fetchMessages
  summary: Fetch messages from consumer instance
- description: Topic partition information channel
  name: database/txeventq/topics/{topicName}/partitions
  operation: subscribe
  operation_id: getPartitions
  summary: Get topic partitions
description: Oracle Transactional Event Queues provide Kafka-compatible event streaming and message queuing capabilities built into Oracle Database. TxEventQ enables event-driven architectures with transactional guarantees, supporting publish-subscribe patterns, consumer groups, partitioned topics, and exactly-once message delivery semantics. Accessible through ORDS REST endpoints and native Kafka protocol compatibility.
layout: asyncapi
messages:
- description: ''
  name: ProduceMessage
  summary: A message to be published to a TxEventQ topic
  title: Produce Message
- description: ''
  name: ConsumeMessage
  summary: A message consumed from a TxEventQ topic
  title: Consumed Message
- description: ''
  name: TopicList
  summary: List of available TxEventQ topics
  title: Topic List
- description: ''
  name: CreateTopicRequest
  summary: Request to create a new TxEventQ topic
  title: Create Topic Request
- description: ''
  name: CreateConsumerGroupRequest
  summary: Request to create a new consumer group
  title: Create Consumer Group Request
- description: ''
  name: FetchedMessages
  summary: Messages fetched from a consumer instance
  title: Fetched Messages
- description: ''
  name: PartitionList
  summary: List of partitions for a topic
  title: Partition List
name: Oracle Transactional Event Queues (TxEventQ) API
provider_name: Oracle Database
provider_slug: oracle-database
servers:
- description: ORDS REST endpoint for TxEventQ management and message operations
  name: ords
  protocol: https
  url: https://{host}:{port}/ords/{schema}
- description: Kafka-compatible protocol endpoint for native Kafka client connectivity. Oracle TxEventQ supports the Apache Kafka protocol, allowing standard Kafka producers and consumers to interact with Oracle Database event queues.
  name: kafka
  protocol: kafka
  url: '{host}:{port}'
slug: oracle-database-txeventq-asyncapi
source_filename: oracle-database-txeventq-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Oracle Transactional Event Queues (TxEventQ) API\n  description: >-\n    Oracle Transactional Event Queues provide Kafka-compatible event streaming\n    and message queuing capabilities built into Oracle Database. TxEventQ enables\n    event-driven architectures with transactional guarantees, supporting\n    publish-subscribe patterns, consumer groups, partitioned topics, and exactly-once\n    message delivery semantics. Accessible through ORDS REST endpoints and native\n    Kafka protocol compatibility.\n  version: 25.4.0\n  contact:\n    name: Oracle Support\n    url: https://support.oracle.com\n    email: support@oracle.com\n  license:\n    name: Oracle Technology Network License\n    url: https://www.oracle.com/downloads/licenses/standard-license.html\n  termsOfService: https://www.oracle.com/legal/terms.html\n  externalDocs:\n    description: Oracle Transactional Event Queues Documentation\n    url: https://docs.oracle.com/en/database/oracle/oracle-database/23/adque/\n\
  servers:\n  ords:\n    url: https://{host}:{port}/ords/{schema}\n    protocol: https\n    description: ORDS REST endpoint for TxEventQ management and message operations\n    variables:\n      host:\n        default: localhost\n        description: ORDS server hostname\n      port:\n        default: '8443'\n        description: ORDS server port\n      schema:\n        default: myschema\n        description: Database schema\n  kafka:\n    url: '{host}:{port}'\n    protocol: kafka\n    description: >-\n      Kafka-compatible protocol endpoint for native Kafka client connectivity.\n      Oracle TxEventQ supports the Apache Kafka protocol, allowing standard\n      Kafka producers and consumers to interact with Oracle Database event queues.\n    variables:\n      host:\n        default: localhost\n        description: Kafka protocol endpoint hostname\n      port:\n        default: '9092'\n        description: Kafka protocol endpoint port\ndefaultContentType: application/json\nchannels:\n  database/txeventq/topics/{topicName}:\n\
  \    description: >-\n      A TxEventQ topic represents an ordered, partitioned event stream stored\n      in Oracle Database. Topics support multiple producers and consumer groups\n      with exactly-once delivery semantics backed by database transactions.\n    parameters:\n      topicName:\n        description: The name of the TxEventQ topic\n        schema:\n          type: string\n    publish:\n      operationId: produceMessage\n      summary: Produce a message to a topic\n      description: >-\n        Publishes a message to the specified TxEventQ topic. Messages are\n        durably stored in Oracle Database with transactional guarantees.\n        Supports key-based partitioning for ordered delivery within partitions.\n      message:\n        $ref: '#/components/messages/ProduceMessage'\n      bindings:\n        kafka:\n          groupId:\n            type: string\n    subscribe:\n      operationId: consumeMessages\n      summary: Consume messages from a topic\n      description:\
  \ >-\n        Subscribes to messages from the specified TxEventQ topic via a\n        consumer group. Supports at-least-once and exactly-once delivery\n        semantics. Consumer instances within a group share partition assignments.\n      message:\n        $ref: '#/components/messages/ConsumeMessage'\n      bindings:\n        kafka:\n          groupId:\n            type: string\n            description: Consumer group identifier\n\n  database/txeventq/topics:\n    description: Topic management channel for listing all available TxEventQ topics\n    subscribe:\n      operationId: listTopics\n      summary: List all TxEventQ topics\n      description: Returns a list of all available TxEventQ topics in the schema.\n      message:\n        $ref: '#/components/messages/TopicList'\n\n  database/txeventq/clusters/{clusterId}/topics:\n    description: Cluster-scoped topic management channel\n    parameters:\n      clusterId:\n        description: The TxEventQ cluster identifier\n        schema:\n\
  \          type: string\n    publish:\n      operationId: createTopic\n      summary: Create a new topic\n      description: >-\n        Creates a new TxEventQ topic in the specified cluster with the given\n        configuration including partition count, retention policy, and replication settings.\n      message:\n        $ref: '#/components/messages/CreateTopicRequest'\n\n  database/txeventq/clusters/{clusterId}/consumer-groups/{consumerGroupId}:\n    description: Consumer group management channel\n    parameters:\n      clusterId:\n        description: The TxEventQ cluster identifier\n        schema:\n          type: string\n      consumerGroupId:\n        description: The consumer group identifier\n        schema:\n          type: string\n    publish:\n      operationId: createConsumerGroup\n      summary: Create a consumer group\n      description: >-\n        Creates a new consumer group within the specified cluster.\n        Consumer groups enable parallel processing of topic messages\n\
  \        with automatic partition assignment.\n      message:\n        $ref: '#/components/messages/CreateConsumerGroupRequest'\n\n  database/txeventq/consumers/{groupName}/instances/{instanceId}/records:\n    description: Message consumption endpoint for fetching messages from a consumer instance\n    parameters:\n      groupName:\n        description: The consumer group name\n        schema:\n          type: string\n      instanceId:\n        description: The consumer instance identifier\n        schema:\n          type: string\n    subscribe:\n      operationId: fetchMessages\n      summary: Fetch messages from consumer instance\n      description: >-\n        Retrieves available messages for a specific consumer instance\n        within a consumer group. Returns messages from assigned partitions\n        with offset tracking.\n      message:\n        $ref: '#/components/messages/FetchedMessages'\n\n  database/txeventq/topics/{topicName}/partitions:\n    description: Topic partition\
  \ information channel\n    parameters:\n      topicName:\n        description: The name of the TxEventQ topic\n        schema:\n          type: string\n    subscribe:\n      operationId: getPartitions\n      summary: Get topic partitions\n      description: Returns partition information for the specified topic.\n      message:\n        $ref: '#/components/messages/PartitionList'\n\ncomponents:\n  messages:\n    ProduceMessage:\n      name: ProduceMessage\n      title: Produce Message\n      summary: A message to be published to a TxEventQ topic\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ProduceMessagePayload'\n\n    ConsumeMessage:\n      name: ConsumeMessage\n      title: Consumed Message\n      summary: A message consumed from a TxEventQ topic\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ConsumedMessagePayload'\n\n    TopicList:\n      name: TopicList\n      title: Topic List\n      summary: List\
  \ of available TxEventQ topics\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/TopicListPayload'\n\n    CreateTopicRequest:\n      name: CreateTopicRequest\n      title: Create Topic Request\n      summary: Request to create a new TxEventQ topic\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CreateTopicPayload'\n\n    CreateConsumerGroupRequest:\n      name: CreateConsumerGroupRequest\n      title: Create Consumer Group Request\n      summary: Request to create a new consumer group\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CreateConsumerGroupPayload'\n\n    FetchedMessages:\n      name: FetchedMessages\n      title: Fetched Messages\n      summary: Messages fetched from a consumer instance\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/FetchedMessagesPayload'\n\n    PartitionList:\n      name: PartitionList\n   \
  \   title: Partition List\n      summary: List of partitions for a topic\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PartitionListPayload'\n\n  schemas:\n    ProduceMessagePayload:\n      type: object\n      properties:\n        key:\n          type: string\n          description: >-\n            Message key used for partition assignment. Messages with the same\n            key are guaranteed to be delivered to the same partition in order.\n        value:\n          description: The message payload content\n        headers:\n          type: object\n          additionalProperties:\n            type: string\n          description: Optional message headers for metadata\n        partition:\n          type: integer\n          description: Optional explicit partition number\n        timestamp:\n          type: string\n          format: date-time\n          description: Message timestamp (defaults to current time)\n      required:\n        - value\n\
  \n    ConsumedMessagePayload:\n      type: object\n      properties:\n        key:\n          type: string\n          description: Message key\n        value:\n          description: The message payload content\n        headers:\n          type: object\n          additionalProperties:\n            type: string\n        topic:\n          type: string\n          description: Source topic name\n        partition:\n          type: integer\n          description: Partition number the message was consumed from\n        offset:\n          type: integer\n          format: int64\n          description: Message offset within the partition\n        timestamp:\n          type: string\n          format: date-time\n          description: Message timestamp\n        timestampType:\n          type: string\n          enum:\n            - CREATE_TIME\n            - LOG_APPEND_TIME\n\n    TopicListPayload:\n      type: object\n      properties:\n        items:\n          type: array\n          items:\n  \
  \          $ref: '#/components/schemas/TopicSummary'\n\n    TopicSummary:\n      type: object\n      properties:\n        name:\n          type: string\n          description: Topic name\n        partitionCount:\n          type: integer\n          description: Number of partitions\n        replicationFactor:\n          type: integer\n          description: Replication factor\n        retentionMs:\n          type: integer\n          format: int64\n          description: Message retention period in milliseconds\n\n    CreateTopicPayload:\n      type: object\n      required:\n        - name\n      properties:\n        name:\n          type: string\n          description: Topic name\n        partitionCount:\n          type: integer\n          description: Number of partitions\n          default: 1\n        retentionMs:\n          type: integer\n          format: int64\n          description: Message retention time in milliseconds\n          default: 604800000\n        config:\n          type:\
  \ object\n          additionalProperties:\n            type: string\n          description: Additional topic configuration properties\n\n    CreateConsumerGroupPayload:\n      type: object\n      required:\n        - groupId\n      properties:\n        groupId:\n          type: string\n          description: Consumer group identifier\n        autoOffsetReset:\n          type: string\n          enum:\n            - earliest\n            - latest\n          default: latest\n          description: Where to start consuming if no committed offset exists\n        enableAutoCommit:\n          type: boolean\n          default: true\n          description: Whether offsets are automatically committed\n\n    FetchedMessagesPayload:\n      type: object\n      properties:\n        items:\n          type: array\n          items:\n            $ref: '#/components/schemas/ConsumedMessagePayload'\n        count:\n          type: integer\n          description: Number of messages returned\n\n    PartitionListPayload:\n\
  \      type: object\n      properties:\n        items:\n          type: array\n          items:\n            $ref: '#/components/schemas/PartitionInfo'\n\n    PartitionInfo:\n      type: object\n      properties:\n        partitionId:\n          type: integer\n          description: Partition identifier\n        leader:\n          type: string\n          description: Leader node for this partition\n        beginOffset:\n          type: integer\n          format: int64\n          description: Earliest available offset\n        endOffset:\n          type: integer\n          format: int64\n          description: Latest offset (next offset to be assigned)\n\n    ConsumerLag:\n      type: object\n      properties:\n        topic:\n          type: string\n        partition:\n          type: integer\n        currentOffset:\n          type: integer\n          format: int64\n          description: Current consumer offset\n        logEndOffset:\n          type: integer\n          format: int64\n\
  \          description: Latest offset in the partition\n        lag:\n          type: integer\n          format: int64\n          description: Number of messages behind\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/oracle-database/refs/heads/main/asyncapi/oracle-database-txeventq-asyncapi.yml
spec_file: asyncapi/oracle-database-txeventq-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/oracle-database/refs/heads/main/asyncapi/oracle-database-txeventq-asyncapi.yml
tags:
- Cloud
- Database
- Enterprise
- Oracle
- REST API
- SQL
- AsyncAPI
- Webhooks
- Events
version: 25.4.0
---
