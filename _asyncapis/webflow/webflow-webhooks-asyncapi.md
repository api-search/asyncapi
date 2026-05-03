---
api_specs:
- filename: webflow-data-api-openapi.yml
  format: yaml
  label: Webflow Data API
  slug: data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-data-api-openapi.yml
- filename: webflow-meta-openapi.yml
  format: yaml
  label: Webflow Meta API
  slug: meta-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-meta-openapi.yml
- filename: webflow-sites-openapi.yml
  format: yaml
  label: Webflow Sites API
  slug: sites-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-sites-openapi.yml
- filename: webflow-pages-openapi.yml
  format: yaml
  label: Webflow Pages API
  slug: pages-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-pages-openapi.yml
- filename: webflow-collections-openapi.yml
  format: yaml
  label: Webflow Collections API
  slug: collections-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-collections-openapi.yml
- filename: webflow-items-openapi.yml
  format: yaml
  label: Webflow CMS Items API
  slug: items-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-items-openapi.yml
- filename: webflow-components-openapi.yml
  format: yaml
  label: Webflow Components API
  slug: components-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-components-openapi.yml
- filename: webflow-assets-openapi.yml
  format: yaml
  label: Webflow Assets API
  slug: assets-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-assets-openapi.yml
- filename: webflow-forms-openapi.yml
  format: yaml
  label: Webflow Forms API
  slug: forms-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-forms-openapi.yml
- filename: webflow-products-openapi.yml
  format: yaml
  label: Webflow Products and SKUs API
  slug: products-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-products-openapi.yml
- filename: webflow-orders-openapi.yml
  format: yaml
  label: Webflow Orders API
  slug: orders-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-orders-openapi.yml
- filename: webflow-inventory-openapi.yml
  format: yaml
  label: Webflow Inventory API
  slug: inventory-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-inventory-openapi.yml
- filename: webflow-ecommerce-settings-openapi.yml
  format: yaml
  label: Webflow Ecommerce Settings API
  slug: ecommerce-settings-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-ecommerce-settings-openapi.yml
- filename: webflow-webhooks-openapi.yml
  format: yaml
  label: Webflow Webhooks API
  slug: webhooks-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-webhooks-openapi.yml
- filename: webflow-custom-code-openapi.yml
  format: yaml
  label: Webflow Custom Code API
  slug: custom-code-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-custom-code-openapi.yml
- filename: webflow-comments-openapi.yml
  format: yaml
  label: Webflow Comments API
  slug: comments-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/openapi/webflow-comments-openapi.yml
channels:
- description: Triggered when a visitor submits a form on a Webflow site.
  name: form_submission
  operation: publish
  operation_id: receiveFormSubmission
  summary: Receive a form submission event.
- description: Triggered when a Webflow site is published.
  name: site_publish
  operation: publish
  operation_id: receiveSitePublish
  summary: Receive a site publish event.
- description: Triggered when a new page is created in the Webflow Designer.
  name: page_created
  operation: publish
  operation_id: receivePageCreated
  summary: Receive a page created event.
- description: Triggered when page metadata (title, description, OG tags, etc.) is updated.
  name: page_metadata_updated
  operation: publish
  operation_id: receivePageMetadataUpdated
  summary: Receive a page metadata updated event.
- description: Triggered when a page is deleted from a Webflow site.
  name: page_deleted
  operation: publish
  operation_id: receivePageDeleted
  summary: Receive a page deleted event.
- description: Triggered when a new e-commerce order is placed.
  name: ecomm_new_order
  operation: publish
  operation_id: receiveEcommNewOrder
  summary: Receive a new e-commerce order event.
- description: Triggered when an existing e-commerce order is updated (status change, fulfillment, etc.).
  name: ecomm_order_changed
  operation: publish
  operation_id: receiveEcommOrderChanged
  summary: Receive an e-commerce order changed event.
- description: Triggered when inventory quantities change for an e-commerce product.
  name: ecomm_inventory_changed
  operation: publish
  operation_id: receiveEcommInventoryChanged
  summary: Receive an e-commerce inventory changed event.
- description: Triggered when a new CMS collection item is created.
  name: collection_item_created
  operation: publish
  operation_id: receiveCollectionItemCreated
  summary: Receive a collection item created event.
- description: Triggered when a CMS collection item is updated.
  name: collection_item_changed
  operation: publish
  operation_id: receiveCollectionItemChanged
  summary: Receive a collection item changed event.
- description: Triggered when a CMS collection item is deleted.
  name: collection_item_deleted
  operation: publish
  operation_id: receiveCollectionItemDeleted
  summary: Receive a collection item deleted event.
- description: Triggered when a CMS collection item is published (made live).
  name: collection_item_published
  operation: publish
  operation_id: receiveCollectionItemPublished
  summary: Receive a collection item published event.
- description: Triggered when a CMS collection item is unpublished (taken offline).
  name: collection_item_unpublished
  operation: publish
  operation_id: receiveCollectionItemUnpublished
  summary: Receive a collection item unpublished event.
- description: Triggered when a comment is added in the Webflow Designer.
  name: comment_created
  operation: publish
  operation_id: receiveCommentCreated
  summary: Receive a comment created event.
description: 'AsyncAPI specification for Webflow webhook events. Webflow delivers webhook payloads via HTTP POST to a URL you register through the Webflow API. Each payload includes a signature header (`X-Webflow-Signature`) that lets you verify the request originated from Webflow. ## Webhook Registration Register a webhook by sending a POST request to: POST https://api.webflow.com/v2/sites/{site_id}/webhooks with a JSON body containing `triggerType` and `url`. A Bearer token is required in the `Authorization` header. ## Signature Validation Every webhook delivery includes an `X-Webflow-Signature` header containing an HMAC-SHA256 digest of the request body, computed with the secret returned when the webhook was created. Compare this value against your own HMAC computation to verify authenticity.'
layout: asyncapi
messages:
- description: ''
  name: FormSubmission
  summary: A visitor submitted a form on the Webflow site.
  title: Form Submission
- description: ''
  name: SitePublish
  summary: The Webflow site was published.
  title: Site Publish
- description: ''
  name: PageCreated
  summary: A new page was created in the Webflow Designer.
  title: Page Created
- description: ''
  name: PageMetadataUpdated
  summary: Page metadata was updated.
  title: Page Metadata Updated
- description: ''
  name: PageDeleted
  summary: A page was deleted from the Webflow site.
  title: Page Deleted
- description: ''
  name: EcommNewOrder
  summary: A new e-commerce order was placed.
  title: New E-Commerce Order
- description: ''
  name: EcommOrderChanged
  summary: An existing e-commerce order was updated.
  title: E-Commerce Order Changed
- description: ''
  name: EcommInventoryChanged
  summary: Inventory quantities changed for a product.
  title: E-Commerce Inventory Changed
- description: ''
  name: CollectionItemCreated
  summary: A new CMS collection item was created.
  title: Collection Item Created
- description: ''
  name: CollectionItemChanged
  summary: A CMS collection item was updated.
  title: Collection Item Changed
- description: ''
  name: CollectionItemDeleted
  summary: A CMS collection item was deleted.
  title: Collection Item Deleted
- description: ''
  name: CollectionItemPublished
  summary: A CMS collection item was published.
  title: Collection Item Published
- description: ''
  name: CollectionItemUnpublished
  summary: A CMS collection item was unpublished.
  title: Collection Item Unpublished
- description: ''
  name: CommentCreated
  summary: A comment was added in the Webflow Designer.
  title: Comment Created
name: Webflow Webhooks
provider_name: Webflow
provider_slug: webflow
servers:
- description: The HTTPS endpoint you provide when registering a webhook. Webflow delivers event payloads here via POST.
  name: webhookDelivery
  protocol: https
  url: https://{yourDomain}
- description: Webflow REST API used to register, list, and delete webhooks.
  name: webflowApi
  protocol: https
  url: https://api.webflow.com/v2
slug: webflow-webhooks-asyncapi
source_filename: webflow-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\n\ninfo:\n  title: Webflow Webhooks\n  version: 2.0.0\n  description: |\n    AsyncAPI specification for Webflow webhook events. Webflow delivers\n    webhook payloads via HTTP POST to a URL you register through the\n    Webflow API. Each payload includes a signature header\n    (`X-Webflow-Signature`) that lets you verify the request originated\n    from Webflow.\n\n    ## Webhook Registration\n\n    Register a webhook by sending a POST request to:\n\n        POST https://api.webflow.com/v2/sites/{site_id}/webhooks\n\n    with a JSON body containing `triggerType` and `url`. A Bearer token\n    is required in the `Authorization` header.\n\n    ## Signature Validation\n\n    Every webhook delivery includes an `X-Webflow-Signature` header\n    containing an HMAC-SHA256 digest of the request body, computed with\n    the secret returned when the webhook was created. Compare this value\n    against your own HMAC computation to verify authenticity.\n  contact:\n  \
  \  name: Webflow Developer Platform\n    url: https://developers.webflow.com\n  license:\n    name: Apache 2.0\n    url: https://www.apache.org/licenses/LICENSE-2.0\n\nservers:\n  webhookDelivery:\n    url: https://{yourDomain}\n    protocol: https\n    description: |\n      The HTTPS endpoint you provide when registering a webhook. Webflow\n      delivers event payloads here via POST.\n    variables:\n      yourDomain:\n        description: The domain of the URL you registered to receive webhooks.\n        default: example.com\n    security:\n      - webhookSignature: []\n\n  webflowApi:\n    url: https://api.webflow.com/v2\n    protocol: https\n    description: |\n      Webflow REST API used to register, list, and delete webhooks.\n    security:\n      - bearerToken: []\n\nchannels:\n  form_submission:\n    description: Triggered when a visitor submits a form on a Webflow site.\n    publish:\n      operationId: receiveFormSubmission\n      summary: Receive a form submission event.\n\
  \      message:\n        $ref: '#/components/messages/FormSubmission'\n\n  site_publish:\n    description: Triggered when a Webflow site is published.\n    publish:\n      operationId: receiveSitePublish\n      summary: Receive a site publish event.\n      message:\n        $ref: '#/components/messages/SitePublish'\n\n  page_created:\n    description: Triggered when a new page is created in the Webflow Designer.\n    publish:\n      operationId: receivePageCreated\n      summary: Receive a page created event.\n      message:\n        $ref: '#/components/messages/PageCreated'\n\n  page_metadata_updated:\n    description: Triggered when page metadata (title, description, OG tags, etc.) is updated.\n    publish:\n      operationId: receivePageMetadataUpdated\n      summary: Receive a page metadata updated event.\n      message:\n        $ref: '#/components/messages/PageMetadataUpdated'\n\n  page_deleted:\n    description: Triggered when a page is deleted from a Webflow site.\n    publish:\n\
  \      operationId: receivePageDeleted\n      summary: Receive a page deleted event.\n      message:\n        $ref: '#/components/messages/PageDeleted'\n\n  ecomm_new_order:\n    description: Triggered when a new e-commerce order is placed.\n    publish:\n      operationId: receiveEcommNewOrder\n      summary: Receive a new e-commerce order event.\n      message:\n        $ref: '#/components/messages/EcommNewOrder'\n\n  ecomm_order_changed:\n    description: Triggered when an existing e-commerce order is updated (status change, fulfillment, etc.).\n    publish:\n      operationId: receiveEcommOrderChanged\n      summary: Receive an e-commerce order changed event.\n      message:\n        $ref: '#/components/messages/EcommOrderChanged'\n\n  ecomm_inventory_changed:\n    description: Triggered when inventory quantities change for an e-commerce product.\n    publish:\n      operationId: receiveEcommInventoryChanged\n      summary: Receive an e-commerce inventory changed event.\n      message:\n\
  \        $ref: '#/components/messages/EcommInventoryChanged'\n\n  collection_item_created:\n    description: Triggered when a new CMS collection item is created.\n    publish:\n      operationId: receiveCollectionItemCreated\n      summary: Receive a collection item created event.\n      message:\n        $ref: '#/components/messages/CollectionItemCreated'\n\n  collection_item_changed:\n    description: Triggered when a CMS collection item is updated.\n    publish:\n      operationId: receiveCollectionItemChanged\n      summary: Receive a collection item changed event.\n      message:\n        $ref: '#/components/messages/CollectionItemChanged'\n\n  collection_item_deleted:\n    description: Triggered when a CMS collection item is deleted.\n    publish:\n      operationId: receiveCollectionItemDeleted\n      summary: Receive a collection item deleted event.\n      message:\n        $ref: '#/components/messages/CollectionItemDeleted'\n\n  collection_item_published:\n    description: Triggered\
  \ when a CMS collection item is published (made live).\n    publish:\n      operationId: receiveCollectionItemPublished\n      summary: Receive a collection item published event.\n      message:\n        $ref: '#/components/messages/CollectionItemPublished'\n\n  collection_item_unpublished:\n    description: Triggered when a CMS collection item is unpublished (taken offline).\n    publish:\n      operationId: receiveCollectionItemUnpublished\n      summary: Receive a collection item unpublished event.\n      message:\n        $ref: '#/components/messages/CollectionItemUnpublished'\n\n  comment_created:\n    description: Triggered when a comment is added in the Webflow Designer.\n    publish:\n      operationId: receiveCommentCreated\n      summary: Receive a comment created event.\n      message:\n        $ref: '#/components/messages/CommentCreated'\n\ncomponents:\n  securitySchemes:\n    bearerToken:\n      type: http\n      scheme: bearer\n      bearerFormat: JWT\n      description:\
  \ |\n        Bearer token issued by Webflow. Required when registering,\n        listing, or deleting webhooks via the Webflow API.\n\n    webhookSignature:\n      type: httpApiKey\n      name: X-Webflow-Signature\n      in: header\n      description: |\n        HMAC-SHA256 signature of the request body, computed with the\n        webhook secret returned at registration time. Verify this header\n        to confirm the payload was sent by Webflow.\n\n  schemas:\n    WebhookEnvelope:\n      type: object\n      description: Common fields present in every Webflow webhook payload.\n      properties:\n        _id:\n          type: string\n          description: Unique identifier for the webhook event.\n        triggerType:\n          type: string\n          description: The event trigger type.\n        siteId:\n          type: string\n          description: The Webflow site ID associated with this event.\n        createdOn:\n          type: string\n          format: date-time\n          description:\
  \ Timestamp when the event was created.\n      required:\n        - _id\n        - triggerType\n        - siteId\n        - createdOn\n\n    FormSubmissionPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEnvelope'\n        - type: object\n          properties:\n            triggerType:\n              type: string\n              enum:\n                - form_submission\n            data:\n              type: object\n              description: The form submission data.\n              properties:\n                formId:\n                  type: string\n                  description: Identifier of the form that was submitted.\n                formName:\n                  type: string\n                  description: Display name of the form.\n                submissionId:\n                  type: string\n                  description: Unique identifier for this submission.\n                fields:\n                  type: object\n                  additionalProperties:\n\
  \                    type: string\n                  description: Key-value pairs of submitted form field names and values.\n                dateSubmitted:\n                  type: string\n                  format: date-time\n                  description: Timestamp of the submission.\n\n    SitePublishPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEnvelope'\n        - type: object\n          properties:\n            triggerType:\n              type: string\n              enum:\n                - site_publish\n            data:\n              type: object\n              description: Details about the site publish event.\n              properties:\n                siteId:\n                  type: string\n                  description: The site that was published.\n                publishedBy:\n                  type: object\n                  properties:\n                    userId:\n                      type: string\n                    displayName:\n           \
  \           type: string\n                publishedOn:\n                  type: string\n                  format: date-time\n                  description: Timestamp of the publish action.\n                domains:\n                  type: array\n                  items:\n                    type: string\n                  description: The domains the site was published to.\n\n    PagePayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEnvelope'\n        - type: object\n          properties:\n            data:\n              type: object\n              description: Page data.\n              properties:\n                pageId:\n                  type: string\n                  description: Unique identifier for the page.\n                title:\n                  type: string\n                  description: The page title.\n                slug:\n                  type: string\n                  description: URL slug for the page.\n                parentId:\n         \
  \         type: string\n                  description: Identifier of the parent page, if any.\n                createdOn:\n                  type: string\n                  format: date-time\n                updatedOn:\n                  type: string\n                  format: date-time\n\n    PageCreatedPayload:\n      allOf:\n        - $ref: '#/components/schemas/PagePayload'\n        - type: object\n          properties:\n            triggerType:\n              type: string\n              enum:\n                - page_created\n\n    PageMetadataUpdatedPayload:\n      allOf:\n        - $ref: '#/components/schemas/PagePayload'\n        - type: object\n          properties:\n            triggerType:\n              type: string\n              enum:\n                - page_metadata_updated\n            data:\n              type: object\n              properties:\n                pageId:\n                  type: string\n                title:\n                  type: string\n            \
  \    description:\n                  type: string\n                  description: The page meta description.\n                openGraphTitle:\n                  type: string\n                openGraphDescription:\n                  type: string\n                openGraphImage:\n                  type: string\n                  format: uri\n\n    PageDeletedPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEnvelope'\n        - type: object\n          properties:\n            triggerType:\n              type: string\n              enum:\n                - page_deleted\n            data:\n              type: object\n              properties:\n                pageId:\n                  type: string\n                  description: Identifier of the deleted page.\n                deletedOn:\n                  type: string\n                  format: date-time\n\n    EcommOrderPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEnvelope'\n        - type: object\n\
  \          properties:\n            data:\n              type: object\n              description: E-commerce order data.\n              properties:\n                orderId:\n                  type: string\n                  description: Unique order identifier.\n                status:\n                  type: string\n                  description: Current order status.\n                  enum:\n                    - pending\n                    - fulfilled\n                    - refunded\n                    - disputed\n                    - cancelled\n                acceptedOn:\n                  type: string\n                  format: date-time\n                customerInfo:\n                  type: object\n                  properties:\n                    fullName:\n                      type: string\n                    email:\n                      type: string\n                      format: email\n                totalPrice:\n                  type: object\n                 \
  \ properties:\n                    value:\n                      type: number\n                    unit:\n                      type: string\n                      description: ISO 4217 currency code.\n                purchasedItems:\n                  type: array\n                  items:\n                    type: object\n                    properties:\n                      productId:\n                        type: string\n                      productName:\n                        type: string\n                      variantId:\n                        type: string\n                      quantity:\n                        type: integer\n                      price:\n                        type: object\n                        properties:\n                          value:\n                            type: number\n                          unit:\n                            type: string\n\n    EcommNewOrderPayload:\n      allOf:\n        - $ref: '#/components/schemas/EcommOrderPayload'\n\
  \        - type: object\n          properties:\n            triggerType:\n              type: string\n              enum:\n                - ecomm_new_order\n\n    EcommOrderChangedPayload:\n      allOf:\n        - $ref: '#/components/schemas/EcommOrderPayload'\n        - type: object\n          properties:\n            triggerType:\n              type: string\n              enum:\n                - ecomm_order_changed\n\n    EcommInventoryChangedPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEnvelope'\n        - type: object\n          properties:\n            triggerType:\n              type: string\n              enum:\n                - ecomm_inventory_changed\n            data:\n              type: object\n              description: Inventory change details.\n              properties:\n                productId:\n                  type: string\n                  description: Identifier of the product whose inventory changed.\n                productName:\n  \
  \                type: string\n                variantId:\n                  type: string\n                  description: Identifier of the specific variant, if applicable.\n                previousQuantity:\n                  type: integer\n                  description: Inventory count before the change.\n                newQuantity:\n                  type: integer\n                  description: Inventory count after the change.\n                updatedOn:\n                  type: string\n                  format: date-time\n\n    CollectionItemPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEnvelope'\n        - type: object\n          properties:\n            data:\n              type: object\n              description: CMS collection item data.\n              properties:\n                collectionId:\n                  type: string\n                  description: Identifier of the CMS collection.\n                collectionName:\n                  type: string\n\
  \                itemId:\n                  type: string\n                  description: Unique identifier of the collection item.\n                slug:\n                  type: string\n                  description: URL slug for the item.\n                name:\n                  type: string\n                  description: Display name of the item.\n                fields:\n                  type: object\n                  additionalProperties: true\n                  description: Dynamic field data for the collection item.\n                createdOn:\n                  type: string\n                  format: date-time\n                updatedOn:\n                  type: string\n                  format: date-time\n\n    CollectionItemCreatedPayload:\n      allOf:\n        - $ref: '#/components/schemas/CollectionItemPayload'\n        - type: object\n          properties:\n            triggerType:\n              type: string\n              enum:\n                - collection_item_created\n\
  \n    CollectionItemChangedPayload:\n      allOf:\n        - $ref: '#/components/schemas/CollectionItemPayload'\n        - type: object\n          properties:\n            triggerType:\n              type: string\n              enum:\n                - collection_item_changed\n\n    CollectionItemDeletedPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEnvelope'\n        - type: object\n          properties:\n            triggerType:\n              type: string\n              enum:\n                - collection_item_deleted\n            data:\n              type: object\n              properties:\n                collectionId:\n                  type: string\n                itemId:\n                  type: string\n                deletedOn:\n                  type: string\n                  format: date-time\n\n    CollectionItemPublishedPayload:\n      allOf:\n        - $ref: '#/components/schemas/CollectionItemPayload'\n        - type: object\n          properties:\n\
  \            triggerType:\n              type: string\n              enum:\n                - collection_item_published\n\n    CollectionItemUnpublishedPayload:\n      allOf:\n        - $ref: '#/components/schemas/CollectionItemPayload'\n        - type: object\n          properties:\n            triggerType:\n              type: string\n              enum:\n                - collection_item_unpublished\n\n    CommentCreatedPayload:\n      allOf:\n        - $ref: '#/components/schemas/WebhookEnvelope'\n        - type: object\n          properties:\n            triggerType:\n              type: string\n              enum:\n                - comment_created\n            data:\n              type: object\n              description: Comment details.\n              properties:\n                commentId:\n                  type: string\n                  description: Unique identifier for the comment.\n                author:\n                  type: object\n                  properties:\n \
  \                   userId:\n                      type: string\n                    displayName:\n                      type: string\n                body:\n                  type: string\n                  description: The comment text.\n                pageId:\n                  type: string\n                  description: The page the comment was left on.\n                itemId:\n                  type: string\n                  description: The element or item the comment refers to, if applicable.\n                createdOn:\n                  type: string\n                  format: date-time\n\n    WebhookRegistrationRequest:\n      type: object\n      description: Request body for registering a new webhook.\n      required:\n        - triggerType\n        - url\n      properties:\n        triggerType:\n          type: string\n          description: The event type to subscribe to.\n          enum:\n            - form_submission\n            - site_publish\n            - page_created\n\
  \            - page_metadata_updated\n            - page_deleted\n            - ecomm_new_order\n            - ecomm_order_changed\n            - ecomm_inventory_changed\n            - collection_item_created\n            - collection_item_changed\n            - collection_item_deleted\n            - collection_item_published\n            - collection_item_unpublished\n            - comment_created\n        url:\n          type: string\n          format: uri\n          description: The HTTPS URL that will receive webhook POST requests.\n        filter:\n          type: object\n          additionalProperties: true\n          description: Optional filter criteria to narrow which events trigger this webhook.\n\n    WebhookRegistrationResponse:\n      type: object\n      description: Response returned after successfully registering a webhook.\n      properties:\n        _id:\n          type: string\n          description: Unique identifier for the registered webhook.\n        triggerType:\n\
  \          type: string\n        url:\n          type: string\n          format: uri\n        siteId:\n          type: string\n        createdOn:\n          type: string\n          format: date-time\n        secret:\n          type: string\n          description: |\n            The HMAC secret used to compute the X-Webflow-Signature header.\n            Store this securely; it is only returned once at creation time.\n\n  messages:\n    FormSubmission:\n      name: FormSubmission\n      title: Form Submission\n      summary: A visitor submitted a form on the Webflow site.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/FormSubmissionPayload'\n\n    SitePublish:\n      name: SitePublish\n      title: Site Publish\n      summary: The Webflow site was published.\n\
  \      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/SitePublishPayload'\n\n    PageCreated:\n      name: PageCreated\n      title: Page Created\n      summary: A new page was created in the Webflow Designer.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/PageCreatedPayload'\n\n    PageMetadataUpdated:\n      name: PageMetadataUpdated\n      title: Page Metadata Updated\n      summary: Page metadata was updated.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n\
  \            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/PageMetadataUpdatedPayload'\n\n    PageDeleted:\n      name: PageDeleted\n      title: Page Deleted\n      summary: A page was deleted from the Webflow site.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/PageDeletedPayload'\n\n    EcommNewOrder:\n      name: EcommNewOrder\n      title: New E-Commerce Order\n      summary: A new e-commerce order was placed.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n       \
  \ $ref: '#/components/schemas/EcommNewOrderPayload'\n\n    EcommOrderChanged:\n      name: EcommOrderChanged\n      title: E-Commerce Order Changed\n      summary: An existing e-commerce order was updated.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/EcommOrderChangedPayload'\n\n    EcommInventoryChanged:\n      name: EcommInventoryChanged\n      title: E-Commerce Inventory Changed\n      summary: Inventory quantities changed for a product.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/EcommInventoryChangedPayload'\n\n    CollectionItemCreated:\n\
  \      name: CollectionItemCreated\n      title: Collection Item Created\n      summary: A new CMS collection item was created.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/CollectionItemCreatedPayload'\n\n    CollectionItemChanged:\n      name: CollectionItemChanged\n      title: Collection Item Changed\n      summary: A CMS collection item was updated.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/CollectionItemChangedPayload'\n\n    CollectionItemDeleted:\n      name: CollectionItemDeleted\n      title: Collection Item Deleted\n\
  \      summary: A CMS collection item was deleted.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/CollectionItemDeletedPayload'\n\n    CollectionItemPublished:\n      name: CollectionItemPublished\n      title: Collection Item Published\n      summary: A CMS collection item was published.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/CollectionItemPublishedPayload'\n\n    CollectionItemUnpublished:\n      name: CollectionItemUnpublished\n      title: Collection Item Unpublished\n      summary: A CMS collection item was unpublished.\n\
  \      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/CollectionItemUnpublishedPayload'\n\n    CommentCreated:\n      name: CommentCreated\n      title: Comment Created\n      summary: A comment was added in the Webflow Designer.\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-Webflow-Signature:\n            type: string\n            description: HMAC-SHA256 signature for payload verification.\n      payload:\n        $ref: '#/components/schemas/CommentCreatedPayload'\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/asyncapi/webflow-webhooks-asyncapi.yml
spec_file: asyncapi/webflow-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/webflow/refs/heads/main/asyncapi/webflow-webhooks-asyncapi.yml
tags:
- CMS
- Ecommerce
- No-Code
- Web Development
- AsyncAPI
- Webhooks
- Events
version: 2.0.0
---
