---
api_specs:
- filename: adobe-analytics-api-openapi.yml
  format: yaml
  label: Adobe Analytics API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-analytics/refs/heads/main/openapi/adobe-analytics-api-openapi.yml
- filename: adobe-analytics-bulk-data-insertion-api-openapi.yml
  format: yaml
  label: Adobe Analytics Bulk Data Insertion API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-analytics/refs/heads/main/openapi/adobe-analytics-bulk-data-insertion-api-openapi.yml
- filename: adobe-analytics-livestream-asyncapi.yml
  format: yaml
  label: Adobe Analytics Livestream API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-analytics/refs/heads/main/asyncapi/adobe-analytics-livestream-asyncapi.yml
- filename: adobe-analytics-data-repair-api-openapi.yml
  format: yaml
  label: Adobe Analytics Data Repair API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-analytics/refs/heads/main/openapi/adobe-analytics-data-repair-api-openapi.yml
channels:
- description: Persistent streaming channel for receiving real-time Analytics hit data. The client maintains a long-lived HTTPS connection and receives a continuous stream of newline-delimited JSON objects, one per Analytics hit, as they are processed.
  name: /{endpointName}
  operation: subscribe
  operation_id: receiveAnalyticsHit
  summary: Receive real-time Analytics hit data
description: The Adobe Analytics Livestream API delivers real-time analytics hit data to a connected client as each hit is processed by Adobe Analytics servers. Data is streamed in line-delimited JSON format compressed with gzip, reflecting traffic being collected by a report suite at the time it is processed. Clients connect to a named streaming endpoint provisioned by Adobe and maintain a persistent connection to receive the continuous data stream.
layout: asyncapi
messages:
- description: Represents one processed Analytics hit as received from a visitor's browser or server-side data collection. Contains all variables set during the hit including page information, visitor identifiers, eVars, props, and events.
  name: AnalyticsHit
  summary: A single Analytics data collection hit
  title: Analytics Hit
- description: An Analytics hit that includes additional geolocation information derived from the visitor's IP address, such as country, region, city, and DMA code.
  name: AnalyticsHitWithGeolocation
  summary: An Analytics hit enriched with geolocation data
  title: Analytics Hit With Geolocation
name: Adobe Analytics Livestream API
provider_name: Adobe Analytics
provider_slug: adobe-analytics
servers:
- description: Adobe Analytics Livestream endpoint. The endpoint name is provisioned by Adobe and corresponds to one or more report suites.
  name: adobeLivestream
  protocol: https
  url: https://livestream.adobe.net/api/1/stream/{endpointName}
slug: adobe-analytics-livestream-asyncapi
source_filename: adobe-analytics-livestream-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Adobe Analytics Livestream API\n  description: >-\n    The Adobe Analytics Livestream API delivers real-time analytics hit data\n    to a connected client as each hit is processed by Adobe Analytics servers.\n    Data is streamed in line-delimited JSON format compressed with gzip,\n    reflecting traffic being collected by a report suite at the time it is\n    processed. Clients connect to a named streaming endpoint provisioned by\n    Adobe and maintain a persistent connection to receive the continuous\n    data stream.\n  version: '1.0'\n  contact:\n    name: Adobe Analytics Support\n    url: https://developer.adobe.com/analytics-apis/docs/2.0/support/\n  termsOfService: https://www.adobe.com/legal/terms.html\nexternalDocs:\n  description: Adobe Analytics Livestream API Documentation\n  url: https://developer.adobe.com/analytics-apis/docs/2.0/guides/endpoints/livestream/\nservers:\n  adobeLivestream:\n    url: 'https://livestream.adobe.net/api/1/stream/{endpointName}'\n\
  \    protocol: https\n    description: >-\n      Adobe Analytics Livestream endpoint. The endpoint name is provisioned\n      by Adobe and corresponds to one or more report suites.\n    variables:\n      endpointName:\n        description: >-\n          The livestream endpoint name provided by Adobe Customer Care,\n          associated with your report suite(s)\n    security:\n      - oauth2: []\nchannels:\n  /{endpointName}:\n    description: >-\n      Persistent streaming channel for receiving real-time Analytics hit data.\n      The client maintains a long-lived HTTPS connection and receives a\n      continuous stream of newline-delimited JSON objects, one per Analytics\n      hit, as they are processed.\n    parameters:\n      endpointName:\n        description: The provisioned livestream endpoint name\n        schema:\n          type: string\n    subscribe:\n      operationId: receiveAnalyticsHit\n      summary: Receive real-time Analytics hit data\n      description: >-\n       \
  \ Receive a continuous stream of Analytics hit records as they are\n        processed. Each message is a newline-delimited JSON object\n        representing a single Analytics hit, including visitor information,\n        page data, eVars, props, events, and other variables collected\n        during the hit.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/AnalyticsHit'\n          - $ref: '#/components/messages/AnalyticsHitWithGeolocation'\ncomponents:\n  securitySchemes:\n    oauth2:\n      type: oauth2\n      description: OAuth 2.0 access token from Adobe IMS\n      flows:\n        clientCredentials:\n          tokenUrl: https://ims-na1.adobelogin.com/ims/token/v3\n          scopes:\n            openid: Required\n  messages:\n    AnalyticsHit:\n      name: AnalyticsHit\n      title: Analytics Hit\n      summary: A single Analytics data collection hit\n      description: >-\n        Represents one processed Analytics hit as received from a visitor's\n        browser\
  \ or server-side data collection. Contains all variables set\n        during the hit including page information, visitor identifiers,\n        eVars, props, and events.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AnalyticsHit'\n    AnalyticsHitWithGeolocation:\n      name: AnalyticsHitWithGeolocation\n      title: Analytics Hit With Geolocation\n      summary: An Analytics hit enriched with geolocation data\n      description: >-\n        An Analytics hit that includes additional geolocation information\n        derived from the visitor's IP address, such as country, region,\n        city, and DMA code.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AnalyticsHitWithGeolocation'\n  schemas:\n    AnalyticsHit:\n      type: object\n      description: A single processed Analytics data collection hit\n      properties:\n        hitIdHigh:\n          type: integer\n          description: High 64 bits of\
  \ the unique hit identifier\n        hitIdLow:\n          type: integer\n          description: Low 64 bits of the unique hit identifier\n        acceptLanguage:\n          type: string\n          description: The Accept-Language header value from the visitor's browser\n        browserHeight:\n          type: integer\n          description: Browser viewport height in pixels\n        browserWidth:\n          type: integer\n          description: Browser viewport width in pixels\n        connectionType:\n          type: integer\n          description: Visitor connection type code\n        currencyCode:\n          type: string\n          description: Currency code used for the hit\n        customVisId:\n          type: string\n          description: Custom visitor ID set by the implementation\n        dateTime:\n          type: string\n          format: date-time\n          description: Timestamp when the hit was received and processed by Adobe\n        domain:\n          type: string\n \
  \         description: Internet domain derived from the visitor's IP address\n        eVar1:\n          type: string\n          description: eVar1 conversion variable value\n        eVar2:\n          type: string\n          description: eVar2 conversion variable value\n        eVar3:\n          type: string\n          description: eVar3 conversion variable value\n        eVar4:\n          type: string\n          description: eVar4 conversion variable value\n        eVar5:\n          type: string\n          description: eVar5 conversion variable value\n        events:\n          type: string\n          description: Comma-separated list of events fired on this hit\n        excludeHit:\n          type: integer\n          description: Flag indicating if the hit should be excluded from reporting\n        hitSource:\n          type: integer\n          description: Hit source type code indicating how the hit was submitted\n        ipAddress:\n          type: string\n          description: Visitor\
  \ IP address (may be obfuscated)\n        javaEnabled:\n          type: boolean\n          description: Whether Java is enabled in the visitor's browser\n        javaScriptVersion:\n          type: string\n          description: JavaScript version supported by the visitor's browser\n        language:\n          type: integer\n          description: Visitor browser language code\n        mcVisId:\n          type: string\n          description: Marketing Cloud Visitor ID (Experience Cloud ID)\n        mobileDeviceName:\n          type: string\n          description: Name of the mobile device if the visit is from a mobile device\n        os:\n          type: integer\n          description: Operating system code\n        pageName:\n          type: string\n          description: Page name variable value\n        pageURL:\n          type: string\n          description: URL of the page on which the hit was fired\n        pagetype:\n          type: string\n          description: Page type variable\
  \ value\n        prop1:\n          type: string\n          description: prop1 traffic variable value\n        prop2:\n          type: string\n          description: prop2 traffic variable value\n        prop3:\n          type: string\n          description: prop3 traffic variable value\n        purchaseId:\n          type: string\n          description: Purchase ID for deduplication of purchase events\n        referrer:\n          type: string\n          description: Referring URL for the visit\n        reportSuite:\n          type: string\n          description: The report suite ID that collected this hit\n        screenHeight:\n          type: integer\n          description: Visitor's screen height in pixels\n        screenWidth:\n          type: integer\n          description: Visitor's screen width in pixels\n        userAgent:\n          type: string\n          description: Browser user agent string\n        visIdHigh:\n          type: integer\n          description: High 64 bits\
  \ of the Analytics visitor ID\n        visIdLow:\n          type: integer\n          description: Low 64 bits of the Analytics visitor ID\n        visIdType:\n          type: integer\n          description: Visitor ID type code indicating the source of the visitor ID\n        visitNum:\n          type: integer\n          description: Visit number for this visitor\n        visitPageNum:\n          type: integer\n          description: Page number within the current visit\n    AnalyticsHitWithGeolocation:\n      allOf:\n        - $ref: '#/components/schemas/AnalyticsHit'\n        - type: object\n          description: Additional geolocation fields derived from IP address\n          properties:\n            countryCode:\n              type: string\n              description: Two-letter ISO country code for the visitor's location\n            region:\n              type: integer\n              description: Region code for the visitor's geographic region\n            city:\n              type:\
  \ integer\n              description: City code for the visitor's city\n            zip:\n              type: string\n              description: Postal code for the visitor's location\n            latitude:\n              type: number\n              description: Latitude coordinate of the visitor's location\n            longitude:\n              type: number\n              description: Longitude coordinate of the visitor's location\n            dmaCode:\n              type: integer\n              description: Designated Market Area code for US visitors\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/adobe-analytics/refs/heads/main/asyncapi/adobe-analytics-livestream-asyncapi.yml
spec_file: asyncapi/adobe-analytics-livestream-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/adobe-analytics/refs/heads/main/asyncapi/adobe-analytics-livestream-asyncapi.yml
tags:
- Adobe
- Analytics
- Business Intelligence
- Customer Intelligence
- Digital Marketing
- Marketing
- Web Analytics
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
