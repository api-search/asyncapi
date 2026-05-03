---
api_specs:
- filename: spire-workload-asyncapi.yml
  format: yaml
  label: SPIRE Workload API
  slug: spire-workload-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/spire/refs/heads/main/asyncapi/spire-workload-asyncapi.yml
- filename: spire-health-openapi.yml
  format: yaml
  label: SPIRE Agent API
  slug: spire-agent-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spire/refs/heads/main/openapi/spire-health-openapi.yml
- filename: spire-oidc-discovery-openapi.yml
  format: yaml
  label: SPIRE OIDC Discovery API
  slug: spire-oidc-discovery-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spire/refs/heads/main/openapi/spire-oidc-discovery-openapi.yml
channels:
- description: Streaming channel through which SPIRE Agent delivers X.509-SVIDs to workloads. After attestation, the agent sends the initial set of X.509-SVIDs the workload is authorized to hold, then proactively re-delivers updated SVIDs before each certificate expires. The stream remains open indefinitely and workloads should reconnect automatically if disconnected.
  name: /spiffe.workload.SpiffeWorkloadAPI/FetchX509SVID
  operation: subscribe
  operation_id: receiveX509SVIDs
  summary: Receive streaming X.509-SVID updates
- description: Streaming channel for receiving X.509 trust bundles for all trust domains the workload needs to validate peer identities. Delivers the local trust domain bundle and all federated trust domain bundles configured on the SPIRE Server.
  name: /spiffe.workload.SpiffeWorkloadAPI/FetchX509Bundles
  operation: subscribe
  operation_id: receiveX509Bundles
  summary: Receive streaming X.509 trust bundle updates
- description: Unary-style channel for requesting JWT-SVIDs for a specific audience. The workload requests a JWT for a target service and receives a short-lived token. JWT-SVIDs have a TTL of typically 5 minutes and must be fetched immediately before use.
  name: /spiffe.workload.SpiffeWorkloadAPI/FetchJWTSVID
  operation: subscribe
  operation_id: receiveJWTSVID
  summary: Receive a JWT-SVID for a target audience
- description: Streaming channel for receiving JWT trust bundles (JWKS) for all configured trust domains. Used by services that need to validate incoming JWT-SVIDs from workloads in the local or federated trust domains.
  name: /spiffe.workload.SpiffeWorkloadAPI/FetchJWTBundles
  operation: subscribe
  operation_id: receiveJWTBundles
  summary: Receive streaming JWT trust bundle updates
- description: Unary channel for delegating JWT-SVID validation to the SPIRE Agent. Services can send incoming JWT-SVIDs to the Agent for validation rather than implementing token validation themselves.
  name: /spiffe.workload.SpiffeWorkloadAPI/ValidateJWTSVID
  operation: subscribe
  operation_id: receiveJWTValidationResult
  summary: Receive JWT-SVID validation result
description: The SPIRE Workload API is a gRPC streaming interface exposed by the SPIRE Agent on each node, through which workloads request and receive SPIFFE Verifiable Identity Documents (SVIDs) and trust bundle updates. Workloads connect to the Agent's Unix domain socket and subscribe to streaming RPCs that deliver X.509-SVIDs, JWT-SVIDs, and trust bundles. The Agent continuously monitors SVID expiry and re-issues certificates before they expire, streaming updated SVIDs to all connected workloads. This AsyncAPI document describes the streaming event channels of the SPIRE Workload API as implemented by SPIRE Agent.
layout: asyncapi
messages:
- description: A streaming response from the SPIRE Agent containing all X.509-SVIDs the workload is currently authorized to hold, plus the trust bundles needed to validate peer identities. Delivered on initial connection and re-delivered on every SVID rotation or authorization change.
  name: X509SVIDResponse
  summary: Batch of X.509-SVIDs and trust bundles for the workload
  title: X.509 SVID Response
- description: A streaming response containing X.509 trust bundles for the local and all federated trust domains. Re-delivered whenever any trust bundle is updated.
  name: X509BundlesResponse
  summary: Complete set of X.509 trust bundles
  title: X.509 Bundles Response
- description: A response containing JWT-SVIDs for all SPIFFE IDs the workload is authorized to hold, each signed with the requested audience claim(s).
  name: JWTSVIDResponse
  summary: JWT-SVIDs for the requested audience
  title: JWT-SVID Response
- description: A streaming response containing JWKS documents for validating JWT-SVIDs from all configured trust domains. Re-delivered on JWT signing key rotation.
  name: JWTBundlesResponse
  summary: JWT trust bundles for all trust domains
  title: JWT Bundles Response
- description: Returns the SPIFFE ID and claims from a validated JWT-SVID. The Agent returns an error status if the token is expired, has an invalid signature, or has an incorrect audience.
  name: ValidateJWTSVIDResponse
  summary: Result of JWT-SVID validation
  title: Validate JWT-SVID Response
name: SPIRE Workload API Events
provider_name: SPIRE
provider_slug: spire
servers:
- description: SPIRE Agent Unix domain socket for the SPIFFE Workload API. The socket path is configurable via the SPIRE Agent socket_path configuration parameter. Workloads connect to this socket to receive their identities.
  name: spireAgent
  protocol: grpc
  url: unix:///tmp/spire-agent/public/api.sock
slug: spire-workload-asyncapi
source_filename: spire-workload-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: SPIRE Workload API Events\n  description: >-\n    The SPIRE Workload API is a gRPC streaming interface exposed by the SPIRE\n    Agent on each node, through which workloads request and receive SPIFFE\n    Verifiable Identity Documents (SVIDs) and trust bundle updates. Workloads\n    connect to the Agent's Unix domain socket and subscribe to streaming RPCs\n    that deliver X.509-SVIDs, JWT-SVIDs, and trust bundles. The Agent\n    continuously monitors SVID expiry and re-issues certificates before they\n    expire, streaming updated SVIDs to all connected workloads. This AsyncAPI\n    document describes the streaming event channels of the SPIRE Workload API\n    as implemented by SPIRE Agent.\n  version: '1.2'\n  contact:\n    name: SPIFFE Community\n    url: https://spiffe.io/community/\nexternalDocs:\n  description: SPIRE Workload API Documentation\n  url: https://spiffe.io/docs/latest/spire-about/spire-concepts/\nservers:\n  spireAgent:\n\
  \    url: 'unix:///tmp/spire-agent/public/api.sock'\n    protocol: grpc\n    description: >-\n      SPIRE Agent Unix domain socket for the SPIFFE Workload API. The socket\n      path is configurable via the SPIRE Agent socket_path configuration\n      parameter. Workloads connect to this socket to receive their identities.\nchannels:\n  /spiffe.workload.SpiffeWorkloadAPI/FetchX509SVID:\n    description: >-\n      Streaming channel through which SPIRE Agent delivers X.509-SVIDs to\n      workloads. After attestation, the agent sends the initial set of\n      X.509-SVIDs the workload is authorized to hold, then proactively\n      re-delivers updated SVIDs before each certificate expires. The stream\n      remains open indefinitely and workloads should reconnect automatically\n      if disconnected.\n    subscribe:\n      operationId: receiveX509SVIDs\n      summary: Receive streaming X.509-SVID updates\n      description: >-\n        Subscribes to a stream of X.509-SVID bundles from the\
  \ SPIRE Agent.\n        The first response delivers all current X.509-SVIDs the workload\n        is authorized to hold. Subsequent responses are triggered by SVID\n        rotation (before expiry), workload registration changes, or trust\n        bundle updates. Each response is a complete replacement of the\n        workload's SVID set. Workloads should use the svids list from the\n        latest response and discard previous SVIDs.\n      message:\n        $ref: '#/components/messages/X509SVIDResponse'\n  /spiffe.workload.SpiffeWorkloadAPI/FetchX509Bundles:\n    description: >-\n      Streaming channel for receiving X.509 trust bundles for all trust\n      domains the workload needs to validate peer identities. Delivers\n      the local trust domain bundle and all federated trust domain bundles\n      configured on the SPIRE Server.\n    subscribe:\n      operationId: receiveX509Bundles\n      summary: Receive streaming X.509 trust bundle updates\n      description: >-\n        Subscribes\
  \ to a stream of X.509 trust bundle updates from the SPIRE\n        Agent. The first response delivers the complete set of trust bundles.\n        Subsequent responses are triggered by trust bundle rotation events\n        on any trust domain in the federation set. Validators should replace\n        their full trust bundle set with each received response.\n      message:\n        $ref: '#/components/messages/X509BundlesResponse'\n  /spiffe.workload.SpiffeWorkloadAPI/FetchJWTSVID:\n    description: >-\n      Unary-style channel for requesting JWT-SVIDs for a specific audience.\n      The workload requests a JWT for a target service and receives a\n      short-lived token. JWT-SVIDs have a TTL of typically 5 minutes and\n      must be fetched immediately before use.\n    subscribe:\n      operationId: receiveJWTSVID\n      summary: Receive a JWT-SVID for a target audience\n      description: >-\n        Returns JWT-SVIDs for all SPIFFE IDs the workload holds, signed with\n        the requested\
  \ audience claim(s). The token should be fetched\n        immediately before being passed to the target service in an HTTP\n        Authorization header or similar mechanism. Do not cache JWT-SVIDs\n        between requests as they have short TTLs.\n      message:\n        $ref: '#/components/messages/JWTSVIDResponse'\n  /spiffe.workload.SpiffeWorkloadAPI/FetchJWTBundles:\n    description: >-\n      Streaming channel for receiving JWT trust bundles (JWKS) for all\n      configured trust domains. Used by services that need to validate\n      incoming JWT-SVIDs from workloads in the local or federated trust domains.\n    subscribe:\n      operationId: receiveJWTBundles\n      summary: Receive streaming JWT trust bundle updates\n      description: >-\n        Subscribes to a stream of JWT trust bundle updates containing JWKS\n        (JSON Web Key Sets) for all trust domains. New responses are pushed\n        whenever a JWT signing key is rotated in any trust domain. Services\n        that\
  \ validate JWT-SVIDs should use the keys from this stream rather\n        than caching static public keys.\n      message:\n        $ref: '#/components/messages/JWTBundlesResponse'\n  /spiffe.workload.SpiffeWorkloadAPI/ValidateJWTSVID:\n    description: >-\n      Unary channel for delegating JWT-SVID validation to the SPIRE Agent.\n      Services can send incoming JWT-SVIDs to the Agent for validation\n      rather than implementing token validation themselves.\n    subscribe:\n      operationId: receiveJWTValidationResult\n      summary: Receive JWT-SVID validation result\n      description: >-\n        Returns the validation result for a provided JWT-SVID token. The\n        SPIRE Agent verifies the token signature using the appropriate trust\n        bundle, checks the audience claim against the expected value, and\n        returns the validated SPIFFE ID and token claims on success.\n      message:\n        $ref: '#/components/messages/ValidateJWTSVIDResponse'\ncomponents:\n  messages:\n\
  \    X509SVIDResponse:\n      name: X509SVIDResponse\n      title: X.509 SVID Response\n      summary: Batch of X.509-SVIDs and trust bundles for the workload\n      description: >-\n        A streaming response from the SPIRE Agent containing all X.509-SVIDs\n        the workload is currently authorized to hold, plus the trust bundles\n        needed to validate peer identities. Delivered on initial connection\n        and re-delivered on every SVID rotation or authorization change.\n      contentType: application/protobuf\n      payload:\n        $ref: '#/components/schemas/X509SVIDResponse'\n    X509BundlesResponse:\n      name: X509BundlesResponse\n      title: X.509 Bundles Response\n      summary: Complete set of X.509 trust bundles\n      description: >-\n        A streaming response containing X.509 trust bundles for the local\n        and all federated trust domains. Re-delivered whenever any trust\n        bundle is updated.\n      contentType: application/protobuf\n      payload:\n\
  \        $ref: '#/components/schemas/X509BundlesResponse'\n    JWTSVIDResponse:\n      name: JWTSVIDResponse\n      title: JWT-SVID Response\n      summary: JWT-SVIDs for the requested audience\n      description: >-\n        A response containing JWT-SVIDs for all SPIFFE IDs the workload\n        is authorized to hold, each signed with the requested audience claim(s).\n      contentType: application/protobuf\n      payload:\n        $ref: '#/components/schemas/JWTSVIDResponse'\n    JWTBundlesResponse:\n      name: JWTBundlesResponse\n      title: JWT Bundles Response\n      summary: JWT trust bundles for all trust domains\n      description: >-\n        A streaming response containing JWKS documents for validating JWT-SVIDs\n        from all configured trust domains. Re-delivered on JWT signing key rotation.\n      contentType: application/protobuf\n      payload:\n        $ref: '#/components/schemas/JWTBundlesResponse'\n    ValidateJWTSVIDResponse:\n      name: ValidateJWTSVIDResponse\n\
  \      title: Validate JWT-SVID Response\n      summary: Result of JWT-SVID validation\n      description: >-\n        Returns the SPIFFE ID and claims from a validated JWT-SVID. The\n        Agent returns an error status if the token is expired, has an\n        invalid signature, or has an incorrect audience.\n      contentType: application/protobuf\n      payload:\n        $ref: '#/components/schemas/ValidateJWTSVIDResponse'\n  schemas:\n    X509SVID:\n      type: object\n      description: >-\n        An X.509-SVID issued by SPIRE containing the DER-encoded certificate\n        chain, private key, and the trust bundle for the issuing trust domain.\n      required:\n        - spiffe_id\n        - x509_svid\n        - x509_svid_key\n        - bundle\n      properties:\n        spiffe_id:\n          type: string\n          description: SPIFFE ID encoded in the certificate's Subject Alternative Name URI field\n          pattern: '^spiffe://[^/]+/.+$'\n        x509_svid:\n          type:\
  \ string\n          description: DER-encoded X.509 certificate chain as base64. Leaf certificate first, followed by intermediates.\n          contentEncoding: base64\n        x509_svid_key:\n          type: string\n          description: DER-encoded PKCS#8 private key for the leaf certificate as base64\n          contentEncoding: base64\n        bundle:\n          type: string\n          description: DER-encoded trust bundle for the issuing trust domain as base64\n          contentEncoding: base64\n        hint:\n          type: string\n          description: Optional hint to help workloads distinguish between multiple SVIDs\n    X509SVIDResponse:\n      type: object\n      description: Streaming response containing all X.509-SVIDs and federated trust bundles\n      required:\n        - svids\n      properties:\n        svids:\n          type: array\n          description: Complete list of X.509-SVIDs the workload is authorized to hold\n          items:\n            $ref: '#/components/schemas/X509SVID'\n\
  \        federated_bundles:\n          type: object\n          description: Map from trust domain name to DER-encoded trust bundle for federated trust domains\n          additionalProperties:\n            type: string\n            contentEncoding: base64\n    X509BundlesResponse:\n      type: object\n      description: Streaming response containing X.509 trust bundles for all trust domains\n      required:\n        - bundles\n      properties:\n        bundles:\n          type: object\n          description: Map from trust domain name to DER-encoded X.509 trust bundle\n          additionalProperties:\n            type: string\n            contentEncoding: base64\n    JWTSVID:\n      type: object\n      description: A JWT-SVID issued by SPIRE as a signed JSON Web Token\n      required:\n        - token\n        - spiffe_id\n      properties:\n        token:\n          type: string\n          description: Compact JWS representation of the JWT-SVID\n          pattern: '^[A-Za-z0-9_-]+\\.[A-Za-z0-9_-]+\\\
  .[A-Za-z0-9_-]+$'\n        spiffe_id:\n          type: string\n          description: SPIFFE ID encoded in the token's sub claim\n          pattern: '^spiffe://[^/]+/.+$'\n        expiry_time:\n          type: integer\n          description: Unix timestamp when this JWT-SVID expires\n          minimum: 0\n        hint:\n          type: string\n          description: Optional hint to help workloads distinguish between multiple SVIDs\n    JWTSVIDResponse:\n      type: object\n      description: Response containing JWT-SVIDs for the requested audience\n      required:\n        - svids\n      properties:\n        svids:\n          type: array\n          description: JWT-SVIDs for all SPIFFE IDs the workload holds, signed for the requested audience\n          items:\n            $ref: '#/components/schemas/JWTSVID'\n    JWTBundlesResponse:\n      type: object\n      description: Streaming response containing JWT trust bundles (JWKS) for all trust domains\n      required:\n        - bundles\n\
  \      properties:\n        bundles:\n          type: object\n          description: Map from trust domain name to serialized JWKS JSON for validating JWT-SVIDs\n          additionalProperties:\n            type: string\n            description: Serialized JWKS JSON document\n    ValidateJWTSVIDResponse:\n      type: object\n      description: Result of JWT-SVID validation performed by the SPIRE Agent\n      required:\n        - spiffe_id\n      properties:\n        spiffe_id:\n          type: string\n          description: The SPIFFE ID extracted from the validated JWT-SVID\n          pattern: '^spiffe://[^/]+/.+$'\n        claims:\n          type: object\n          description: Full set of JWT claims from the validated token\n          additionalProperties: true\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spire/refs/heads/main/asyncapi/spire-workload-asyncapi.yml
spec_file: asyncapi/spire-workload-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/spire/refs/heads/main/asyncapi/spire-workload-asyncapi.yml
tags:
- Authentication
- Cloud Native
- Graduated
- Identity
- Security
- Zero Trust
- AsyncAPI
- Webhooks
- Events
version: '1.2'
---
