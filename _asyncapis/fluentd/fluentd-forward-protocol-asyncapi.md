---
api_specs:
- filename: fluentd-forward-protocol-asyncapi.yml
  format: yaml
  label: Fluentd Forward Protocol
  slug: fluentd-forward-protocol
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/fluentd/refs/heads/main/asyncapi/fluentd-forward-protocol-asyncapi.yml
- filename: fluentd-http-input-openapi.yml
  format: yaml
  label: Fluentd HTTP Input API
  slug: fluentd-http-input
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/fluentd/refs/heads/main/openapi/fluentd-http-input-openapi.yml
channels:
- description: The Forward Protocol channel transports Fluentd event streams from upstream forwarders or agents to a downstream Fluentd aggregator. Messages are serialized as MessagePack arrays and sent over a persistent TCP connection.
  name: /forward
  operation: publish
  operation_id: forwardEvents
  summary: Forward one or more log events to a Fluentd aggregator
- description: UDP heartbeat channel used for keepalive and connection health checking between a forwarder and its upstream aggregator.
  name: /heartbeat
  operation: publish
  operation_id: sendHeartbeat
  summary: Send a heartbeat packet
description: The Fluentd Forward Protocol is a binary MessagePack-based protocol used to transport event streams between Fluentd nodes, Fluent Bit agents, and compatible forwarders over TCP or TLS. It supports multiple transport modes including Message, Forward, PackedForward, and CompressedPackedForward, as well as optional SASL-style authentication and heartbeat mechanisms for connection health checking.
layout: asyncapi
messages:
- description: 'The simplest Forward Protocol message. Encodes a single event as a 3-element or 4-element MessagePack array: [tag, time, record] or [tag, time, record, option]. Used when the sender has one event to transmit.'
  name: MessageMode
  summary: A single log event with tag, timestamp, and record
  title: Message Mode Event
- description: 'Encodes multiple events under one tag as a 3-element or 4-element MessagePack array: [tag, entries, option]. Each entry is a 2-element array [time, record]. Efficient when the sender batches many events for the same tag before flushing.'
  name: ForwardMode
  summary: A batch of log events sharing a single tag
  title: Forward Mode Event
- description: Encodes events as a 3-element or 4-element array [tag, entries, option] where entries is a raw binary blob of concatenated MessagePack [time, record] pairs. This avoids double-encoding overhead and is the default mode used by Fluentd's out_forward plugin.
  name: PackedForwardMode
  summary: A batch of pre-serialized log events as a raw MessagePack byte stream
  title: Packed Forward Mode Event
- description: The same as PackedForwardMode but the entries binary blob is additionally gzip-compressed. The option map must include {"compressed":"gzip"} to signal the encoding to the receiver. Reduces bandwidth for high-volume log pipelines.
  name: CompressedPackedForwardMode
  summary: A gzip-compressed packed forward batch
  title: Compressed Packed Forward Mode Event
- description: 'A single null byte (0x00) sent over UDP by a forwarder to the aggregator''s heartbeat port (default: same as TCP port). The aggregator echoes the packet back to confirm reachability.'
  name: Heartbeat
  summary: A UDP keepalive packet
  title: Heartbeat Packet
name: Fluentd Forward Protocol
provider_name: Fluentd
provider_slug: fluentd
servers:
- description: Default Fluentd forward input listener. TLS variants use the same port with a TLS-wrapped connection when tls_enable is set to true in the in_forward plugin configuration.
  name: fluentd
  protocol: tcp
  url: tcp://localhost:24224
slug: fluentd-forward-protocol-asyncapi
source_filename: fluentd-forward-protocol-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Fluentd Forward Protocol\n  description: >-\n    The Fluentd Forward Protocol is a binary MessagePack-based protocol used\n    to transport event streams between Fluentd nodes, Fluent Bit agents, and\n    compatible forwarders over TCP or TLS. It supports multiple transport\n    modes including Message, Forward, PackedForward, and\n    CompressedPackedForward, as well as optional SASL-style authentication\n    and heartbeat mechanisms for connection health checking.\n  version: '1.0.0'\n  contact:\n    name: Fluentd Community\n    url: https://www.fluentd.org/community/\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\nexternalDocs:\n  description: Forward Protocol Specification v1\n  url: https://github.com/fluent/fluentd/wiki/Forward-Protocol-Specification-v1\nservers:\n  fluentd:\n    url: 'tcp://localhost:24224'\n    protocol: tcp\n    description: >-\n      Default Fluentd forward input listener. TLS\
  \ variants use the same port\n      with a TLS-wrapped connection when tls_enable is set to true in the\n      in_forward plugin configuration.\nchannels:\n  /forward:\n    description: >-\n      The Forward Protocol channel transports Fluentd event streams from\n      upstream forwarders or agents to a downstream Fluentd aggregator.\n      Messages are serialized as MessagePack arrays and sent over a persistent\n      TCP connection.\n    publish:\n      operationId: forwardEvents\n      summary: Forward one or more log events to a Fluentd aggregator\n      description: >-\n        Sends log events from a Fluentd forwarder or Fluent Bit agent to an\n        aggregating Fluentd instance. The message format depends on the\n        transport mode selected by the sender. The Mode mode sends a single\n        event; Forward mode sends multiple events sharing a tag; PackedForward\n        sends events pre-serialized as a MessagePack byte stream;\n        CompressedPackedForward adds gzip compression\
  \ on top of PackedForward.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/MessageMode'\n          - $ref: '#/components/messages/ForwardMode'\n          - $ref: '#/components/messages/PackedForwardMode'\n          - $ref: '#/components/messages/CompressedPackedForwardMode'\n  /heartbeat:\n    description: >-\n      UDP heartbeat channel used for keepalive and connection health checking\n      between a forwarder and its upstream aggregator.\n    publish:\n      operationId: sendHeartbeat\n      summary: Send a heartbeat packet\n      description: >-\n        A forwarder periodically sends a UDP heartbeat packet (a single null\n        byte) to the aggregator. The aggregator echoes it back to confirm the\n        connection is alive.\n      message:\n        $ref: '#/components/messages/Heartbeat'\ncomponents:\n  securitySchemes:\n    sharedKeyAuth:\n      type: httpApiKey\n      in: header\n      name: Authorization\n      description: >-\n        Optional SASL-style\
  \ shared key authentication. The forwarder presents\n        a nonce-based HMAC challenge response derived from a pre-shared key\n        configured in both the out_forward and in_forward plugins.\n  messages:\n    MessageMode:\n      name: MessageMode\n      title: Message Mode Event\n      summary: A single log event with tag, timestamp, and record\n      description: >-\n        The simplest Forward Protocol message. Encodes a single event as a\n        3-element or 4-element MessagePack array: [tag, time, record] or\n        [tag, time, record, option]. Used when the sender has one event to\n        transmit.\n      contentType: application/msgpack\n      payload:\n        $ref: '#/components/schemas/MessageModePayload'\n    ForwardMode:\n      name: ForwardMode\n      title: Forward Mode Event\n      summary: A batch of log events sharing a single tag\n      description: >-\n        Encodes multiple events under one tag as a 3-element or 4-element\n        MessagePack array: [tag,\
  \ entries, option]. Each entry is a 2-element\n        array [time, record]. Efficient when the sender batches many events\n        for the same tag before flushing.\n      contentType: application/msgpack\n      payload:\n        $ref: '#/components/schemas/ForwardModePayload'\n    PackedForwardMode:\n      name: PackedForwardMode\n      title: Packed Forward Mode Event\n      summary: >-\n        A batch of pre-serialized log events as a raw MessagePack byte stream\n      description: >-\n        Encodes events as a 3-element or 4-element array [tag, entries,\n        option] where entries is a raw binary blob of concatenated MessagePack\n        [time, record] pairs. This avoids double-encoding overhead and is the\n        default mode used by Fluentd's out_forward plugin.\n      contentType: application/msgpack\n      payload:\n        $ref: '#/components/schemas/PackedForwardModePayload'\n    CompressedPackedForwardMode:\n      name: CompressedPackedForwardMode\n      title: Compressed\
  \ Packed Forward Mode Event\n      summary: A gzip-compressed packed forward batch\n      description: >-\n        The same as PackedForwardMode but the entries binary blob is\n        additionally gzip-compressed. The option map must include\n        {\"compressed\":\"gzip\"} to signal the encoding to the receiver.\n        Reduces bandwidth for high-volume log pipelines.\n      contentType: application/msgpack\n      payload:\n        $ref: '#/components/schemas/CompressedPackedForwardModePayload'\n    Heartbeat:\n      name: Heartbeat\n      title: Heartbeat Packet\n      summary: A UDP keepalive packet\n      description: >-\n        A single null byte (0x00) sent over UDP by a forwarder to the\n        aggregator's heartbeat port (default: same as TCP port). The\n        aggregator echoes the packet back to confirm reachability.\n      contentType: application/octet-stream\n      payload:\n        type: string\n        description: Single null byte heartbeat payload.\n  schemas:\n\
  \    MessageModePayload:\n      type: array\n      description: >-\n        A MessagePack array representing a single Fluentd event in Message\n        mode: [tag, time, record] or [tag, time, record, option].\n      prefixItems:\n        - type: string\n          description: The Fluentd routing tag.\n        - $ref: '#/components/schemas/EventTime'\n        - $ref: '#/components/schemas/Record'\n        - $ref: '#/components/schemas/OptionMap'\n      minItems: 3\n      maxItems: 4\n    ForwardModePayload:\n      type: array\n      description: >-\n        A MessagePack array representing a batch of Fluentd events in Forward\n        mode: [tag, entries, option].\n      prefixItems:\n        - type: string\n          description: The Fluentd routing tag shared by all events in the batch.\n        - type: array\n          description: Array of [time, record] entry pairs.\n          items:\n            $ref: '#/components/schemas/Entry'\n        - $ref: '#/components/schemas/OptionMap'\n\
  \      minItems: 2\n      maxItems: 3\n    PackedForwardModePayload:\n      type: array\n      description: >-\n        A MessagePack array representing a packed batch: [tag, entries_bytes,\n        option]. entries_bytes is a raw binary sequence of MessagePack-encoded\n        [time, record] pairs.\n      prefixItems:\n        - type: string\n          description: The Fluentd routing tag.\n        - type: string\n          contentEncoding: binary\n          description: >-\n            Raw binary blob of concatenated MessagePack-encoded [time, record]\n            pairs.\n        - $ref: '#/components/schemas/OptionMap'\n      minItems: 2\n      maxItems: 3\n    CompressedPackedForwardModePayload:\n      type: array\n      description: >-\n        Same as PackedForwardModePayload but the entries binary blob is\n        gzip-compressed. The option map must contain {\"compressed\":\"gzip\"}.\n      prefixItems:\n        - type: string\n          description: The Fluentd routing tag.\n\
  \        - type: string\n          contentEncoding: binary\n          description: Gzip-compressed binary blob of packed MessagePack entries.\n        - $ref: '#/components/schemas/OptionMap'\n      minItems: 2\n      maxItems: 3\n    Entry:\n      type: array\n      description: A single event entry consisting of a timestamp and a record.\n      prefixItems:\n        - $ref: '#/components/schemas/EventTime'\n        - $ref: '#/components/schemas/Record'\n      minItems: 2\n      maxItems: 2\n    EventTime:\n      description: >-\n        Event timestamp. Can be a Unix epoch integer (seconds) or a Fluentd\n        EventTime MessagePack extension type that carries both seconds and\n        nanoseconds for sub-second precision.\n      oneOf:\n        - type: integer\n          description: Unix epoch time in seconds.\n          example: 1700000000\n        - type: object\n          description: >-\n            Fluentd EventTime extension (MessagePack ext type 0). Contains\n            seconds\
  \ and nanoseconds fields for nanosecond-precision timestamps.\n          properties:\n            seconds:\n              type: integer\n              description: Seconds since Unix epoch.\n            nanoseconds:\n              type: integer\n              description: Nanosecond component of the timestamp.\n    Record:\n      type: object\n      description: >-\n        The log record payload. An arbitrary key-value map where keys are\n        strings and values can be any MessagePack-compatible type. The fields\n        are defined by the emitting application or plugin.\n      additionalProperties: true\n    OptionMap:\n      type: object\n      description: >-\n        Optional metadata map attached to a Forward Protocol message. Can\n        carry acknowledgement chunk IDs, compression hints, and size hints.\n      properties:\n        chunk:\n          type: string\n          description: >-\n            A unique base64-encoded identifier for this message batch used for\n     \
  \       at-least-once acknowledgement. The receiver sends back {\"ack\":chunk}\n            to confirm delivery.\n        compressed:\n          type: string\n          description: >-\n            Indicates the compression algorithm applied to packed entries.\n            Currently only 'gzip' is supported.\n          enum:\n            - gzip\n        size:\n          type: integer\n          description: >-\n            The number of records in the batch. Used as a hint by the receiver\n            to pre-allocate buffers.\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/fluentd/refs/heads/main/asyncapi/fluentd-forward-protocol-asyncapi.yml
spec_file: asyncapi/fluentd-forward-protocol-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/fluentd/refs/heads/main/asyncapi/fluentd-forward-protocol-asyncapi.yml
tags:
- Data Collection
- Logging
- Open Source
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
