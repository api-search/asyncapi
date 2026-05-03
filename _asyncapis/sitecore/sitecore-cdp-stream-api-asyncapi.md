---
api_specs:
- filename: sitecore-xm-cloud-rest-api-openapi.yml
  format: yaml
  label: Sitecore XM Cloud REST API
  slug: xm-cloud-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/openapi/sitecore-xm-cloud-rest-api-openapi.yml
- filename: sitecore-cdp-rest-api-openapi.yml
  format: yaml
  label: Sitecore CDP REST API
  slug: cdp-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/openapi/sitecore-cdp-rest-api-openapi.yml
- filename: sitecore-cdp-stream-api-asyncapi.yml
  format: yaml
  label: Sitecore CDP Stream API
  slug: cdp-stream-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/asyncapi/sitecore-cdp-stream-api-asyncapi.yml
- filename: sitecore-personalize-rest-api-openapi.yml
  format: yaml
  label: Sitecore Personalize REST API
  slug: personalize-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/openapi/sitecore-personalize-rest-api-openapi.yml
- filename: sitecore-content-hub-rest-api-openapi.yml
  format: yaml
  label: Sitecore Content Hub REST API
  slug: content-hub-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/openapi/sitecore-content-hub-rest-api-openapi.yml
- filename: sitecore-ordercloud-api-openapi.yml
  format: yaml
  label: Sitecore OrderCloud API
  slug: ordercloud-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/openapi/sitecore-ordercloud-api-openapi.yml
- filename: sitecore-discover-api-openapi.yml
  format: yaml
  label: Sitecore Discover API
  slug: discover-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/openapi/sitecore-discover-api-openapi.yml
channels:
- description: The primary channel for submitting all behavioral and transactional events to Sitecore CDP. Each event payload must include the channel, type, browser ID, and session identifier along with event-specific data.
  name: /v1.2/event/create.json
  operation: publish
  operation_id: sendEvent
  summary: Send a behavioral or transactional event
description: 'The Sitecore CDP Stream API enables applications to send real-time behavioral and transactional events about users to the Sitecore Customer Data Platform. It is designed for high-throughput event ingestion from web, mobile, and server-side applications, capturing interactions such as page views, product views, identity events, and purchases. Events sent through the Stream API update guest profiles in near real-time, powering personalization and segmentation use cases. The API consists of two components: the Browser API for managing browser cookies and guest identification, and the Event API for transmitting structured event payloads. The target endpoint is environment-specific and must be configured based on the Sitecore CDP instance region.'
layout: asyncapi
messages:
- description: A VIEW event is sent whenever a guest views a page in the application. It captures the URL, page type, and contextual information about the visit. VIEW events trigger every time a webpage loads and are used to build session profiles and behavioral segments.
  name: ViewEvent
  summary: Captures a guest's page view interaction
  title: Page View Event
- description: An IDENTITY event links session activity to a known guest by providing identifying information such as email address, name, and other profile attributes. This event triggers identity resolution and merges anonymous session data with the guest's persistent profile.
  name: IdentityEvent
  summary: Associates a guest profile with identifying information
  title: Guest Identity Event
- description: An ORDER_CHECKOUT event captures a completed or confirmed purchase including order totals, items, and payment information. This event is used to build order history in the guest profile and enables purchase behavior-based segmentation.
  name: OrderCheckoutEvent
  summary: Records a completed purchase transaction
  title: Order Checkout Event
- description: An ADD event captures a guest adding a product to their shopping cart. These events feed into cart abandonment tracking and product affinity modeling within Sitecore CDP.
  name: AddEvent
  summary: Records a product being added to the shopping cart
  title: Add to Cart Event
- description: A SEARCH event captures search queries performed by guests within the application. These events contribute to interest modeling and can be used to trigger relevant personalization rules.
  name: SearchEvent
  summary: Records a search query performed by the guest
  title: Search Event
- description: A CUSTOM event allows organizations to send application-specific behavioral events with a custom event name and arbitrary data in the ext extension object. Custom event names must not conflict with reserved Sitecore CDP event names.
  name: CustomEvent
  summary: Records a custom application-defined event
  title: Custom Event
name: Sitecore CDP Stream API
provider_name: sitecore
provider_slug: sitecore
servers:
- description: EU Production Stream Server
  name: eu
  protocol: https
  url: https://api-engage-eu.sitecorecloud.io
- description: US Production Stream Server
  name: us
  protocol: https
  url: https://api-engage-us.sitecorecloud.io
- description: Asia-Pacific Production Stream Server
  name: ap
  protocol: https
  url: https://api-engage-ap.sitecorecloud.io
- description: Japan Production Stream Server
  name: jp
  protocol: https
  url: https://api-engage-jpe.sitecorecloud.io
slug: sitecore-cdp-stream-api-asyncapi
source_filename: sitecore-cdp-stream-api-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Sitecore CDP Stream API\n  description: >-\n    The Sitecore CDP Stream API enables applications to send real-time behavioral\n    and transactional events about users to the Sitecore Customer Data Platform.\n    It is designed for high-throughput event ingestion from web, mobile, and\n    server-side applications, capturing interactions such as page views, product\n    views, identity events, and purchases. Events sent through the Stream API update\n    guest profiles in near real-time, powering personalization and segmentation\n    use cases. The API consists of two components: the Browser API for managing\n    browser cookies and guest identification, and the Event API for transmitting\n    structured event payloads. The target endpoint is environment-specific and must\n    be configured based on the Sitecore CDP instance region.\n  version: '2.1'\n  contact:\n    name: Sitecore Support\n    url: https://www.sitecore.com/support\nservers:\n\
  \  eu:\n    url: 'https://api-engage-eu.sitecorecloud.io'\n    protocol: https\n    description: EU Production Stream Server\n    security:\n      - basicAuth: []\n  us:\n    url: 'https://api-engage-us.sitecorecloud.io'\n    protocol: https\n    description: US Production Stream Server\n    security:\n      - basicAuth: []\n  ap:\n    url: 'https://api-engage-ap.sitecorecloud.io'\n    protocol: https\n    description: Asia-Pacific Production Stream Server\n    security:\n      - basicAuth: []\n  jp:\n    url: 'https://api-engage-jpe.sitecorecloud.io'\n    protocol: https\n    description: Japan Production Stream Server\n    security:\n      - basicAuth: []\nchannels:\n  /v1.2/event/create.json:\n    description: >-\n      The primary channel for submitting all behavioral and transactional events\n      to Sitecore CDP. Each event payload must include the channel, type, browser\n      ID, and session identifier along with event-specific data.\n    publish:\n      operationId: sendEvent\n\
  \      summary: Send a behavioral or transactional event\n      description: >-\n        Publishes a single event to Sitecore CDP representing a guest interaction.\n        Events are processed asynchronously and update guest profiles in near\n        real-time. The event type determines the required and optional fields.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/ViewEvent'\n          - $ref: '#/components/messages/IdentityEvent'\n          - $ref: '#/components/messages/OrderCheckoutEvent'\n          - $ref: '#/components/messages/AddEvent'\n          - $ref: '#/components/messages/SearchEvent'\n          - $ref: '#/components/messages/CustomEvent'\n\ncomponents:\n  securitySchemes:\n    basicAuth:\n      type: httpApiKey\n      name: Authorization\n      in: header\n      description: >-\n        HTTP Basic authentication using the client key as username and API token\n        as password. Credentials are obtained from Sitecore CDP Settings > API access.\n\
  \n  messages:\n    ViewEvent:\n      name: VIEW\n      title: Page View Event\n      summary: Captures a guest's page view interaction\n      description: >-\n        A VIEW event is sent whenever a guest views a page in the application.\n        It captures the URL, page type, and contextual information about the\n        visit. VIEW events trigger every time a webpage loads and are used to\n        build session profiles and behavioral segments.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ViewEventPayload'\n\n    IdentityEvent:\n      name: IDENTITY\n      title: Guest Identity Event\n      summary: Associates a guest profile with identifying information\n      description: >-\n        An IDENTITY event links session activity to a known guest by providing\n        identifying information such as email address, name, and other profile\n        attributes. This event triggers identity resolution and merges anonymous\n        session data with\
  \ the guest's persistent profile.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/IdentityEventPayload'\n\n    OrderCheckoutEvent:\n      name: ORDER_CHECKOUT\n      title: Order Checkout Event\n      summary: Records a completed purchase transaction\n      description: >-\n        An ORDER_CHECKOUT event captures a completed or confirmed purchase\n        including order totals, items, and payment information. This event is\n        used to build order history in the guest profile and enables purchase\n        behavior-based segmentation.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderCheckoutEventPayload'\n\n    AddEvent:\n      name: ADD\n      title: Add to Cart Event\n      summary: Records a product being added to the shopping cart\n      description: >-\n        An ADD event captures a guest adding a product to their shopping cart.\n        These events feed into cart abandonment tracking and\
  \ product affinity\n        modeling within Sitecore CDP.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/AddEventPayload'\n\n    SearchEvent:\n      name: SEARCH\n      title: Search Event\n      summary: Records a search query performed by the guest\n      description: >-\n        A SEARCH event captures search queries performed by guests within the\n        application. These events contribute to interest modeling and can be\n        used to trigger relevant personalization rules.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SearchEventPayload'\n\n    CustomEvent:\n      name: CUSTOM\n      title: Custom Event\n      summary: Records a custom application-defined event\n      description: >-\n        A CUSTOM event allows organizations to send application-specific\n        behavioral events with a custom event name and arbitrary data in the\n        ext extension object. Custom event names must not\
  \ conflict with reserved\n        Sitecore CDP event names.\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CustomEventPayload'\n\n  schemas:\n    BaseEventPayload:\n      type: object\n      description: Base fields shared by all Sitecore CDP Stream API events\n      required:\n        - channel\n        - type\n        - browser_id\n        - session_id\n        - pos\n        - currency\n      properties:\n        channel:\n          type: string\n          description: The channel from which the event originates\n          enum:\n            - WEB\n            - MOBILE_WEB\n            - MOBILE_APP\n            - SERVER_SIDE\n        type:\n          type: string\n          description: The type identifier for the event\n        browser_id:\n          type: string\n          description: >-\n            The unique identifier for the guest's browser session, set by the\n            CDP Browser API cookie\n        session_id:\n          type:\
  \ string\n          description: >-\n            The unique identifier for the current session, generated by the\n            client and consistent within a single visit\n        pos:\n          type: string\n          description: >-\n            The point of sale identifier that maps to the brand or channel\n            configured in the Sitecore CDP instance\n        currency:\n          type: string\n          description: The ISO 4217 currency code for monetary values in this event\n          example: USD\n        language:\n          type: string\n          description: The ISO 639-1 language code for the session\n          example: EN\n        page:\n          type: string\n          description: The URL of the page where the event occurred\n          format: uri\n        ext:\n          type: object\n          description: >-\n            Custom extension data for the event. Only one ext object is supported\n            per event and its name must match the configured data extension\
  \ name.\n          additionalProperties: true\n\n    ViewEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseEventPayload'\n        - type: object\n          description: Payload for a VIEW event capturing page view interactions\n          properties:\n            type:\n              type: string\n              description: Event type identifier, must be VIEW\n              const: VIEW\n            page:\n              type: string\n              description: The URL of the page being viewed\n              format: uri\n\n    IdentityEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseEventPayload'\n        - type: object\n          description: Payload for an IDENTITY event associating a guest with known identifiers\n          required:\n            - email\n          properties:\n            type:\n              type: string\n              description: Event type identifier, must be IDENTITY\n              const: IDENTITY\n            email:\n  \
  \            type: string\n              description: The email address of the guest being identified\n              format: email\n            firstname:\n              type: string\n              description: The guest's first name\n            lastname:\n              type: string\n              description: The guest's last name\n            date_of_birth:\n              type: string\n              description: The guest's date of birth in YYYY-MM-DD format\n              format: date\n            gender:\n              type: string\n              description: The guest's gender\n              enum:\n                - Male\n                - Female\n                - Other\n                - Unknown\n            phone:\n              type: string\n              description: The guest's phone number\n\n    OrderCheckoutEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseEventPayload'\n        - type: object\n          description: Payload for an ORDER_CHECKOUT event\
  \ recording a completed purchase\n          required:\n            - reference_id\n            - total_price\n          properties:\n            type:\n              type: string\n              description: Event type identifier, must be ORDER_CHECKOUT\n              const: ORDER_CHECKOUT\n            reference_id:\n              type: string\n              description: The external order reference identifier\n            status:\n              type: string\n              description: The order status\n              enum:\n                - CONFIRMED\n                - PENDING\n                - CANCELED\n            total_price:\n              type: number\n              description: The total price of the order\n              format: float\n            payment_type:\n              type: string\n              description: The payment method used\n              enum:\n                - CREDIT_CARD\n                - DEBIT_CARD\n                - PAYPAL\n                - GIFT_CARD\n  \
  \              - OTHER\n            ordered_at:\n              type: string\n              description: The ISO 8601 timestamp when the order was placed\n              format: date-time\n            items:\n              type: array\n              description: The products included in the order\n              items:\n                $ref: '#/components/schemas/OrderItem'\n\n    AddEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseEventPayload'\n        - type: object\n          description: Payload for an ADD event recording a product added to cart\n          required:\n            - product\n          properties:\n            type:\n              type: string\n              description: Event type identifier, must be ADD\n              const: ADD\n            product:\n              $ref: '#/components/schemas/ProductReference'\n\n    SearchEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseEventPayload'\n        - type: object\n          description:\
  \ Payload for a SEARCH event recording a guest search query\n          required:\n            - search_term\n          properties:\n            type:\n              type: string\n              description: Event type identifier, must be SEARCH\n              const: SEARCH\n            search_term:\n              type: string\n              description: The search query entered by the guest\n            num_results:\n              type: integer\n              description: The number of results returned for the search query\n              minimum: 0\n\n    CustomEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/BaseEventPayload'\n        - type: object\n          description: Payload for a custom application-defined event\n          required:\n            - type\n          properties:\n            type:\n              type: string\n              description: >-\n                The custom event type name defined by the organization. Must not\n                conflict with\
  \ reserved Sitecore CDP event names.\n              minLength: 1\n              maxLength: 50\n\n    OrderItem:\n      type: object\n      description: A product line item within an order checkout event\n      required:\n        - sku\n        - quantity\n        - price\n      properties:\n        sku:\n          type: string\n          description: The product SKU or identifier\n        name:\n          type: string\n          description: The product display name\n        quantity:\n          type: integer\n          description: The quantity of the product purchased\n          minimum: 1\n        price:\n          type: number\n          description: The unit price of the product\n          format: float\n        category:\n          type: string\n          description: The product category\n\n    ProductReference:\n      type: object\n      description: A reference to a product in a behavioral event\n      required:\n        - sku\n      properties:\n        sku:\n          type:\
  \ string\n          description: The product SKU or identifier\n        name:\n          type: string\n          description: The product display name\n        price:\n          type: number\n          description: The unit price of the product\n          format: float\n        category:\n          type: string\n          description: The product category\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/asyncapi/sitecore-cdp-stream-api-asyncapi.yml
spec_file: asyncapi/sitecore-cdp-stream-api-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/asyncapi/sitecore-cdp-stream-api-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '2.1'
---
