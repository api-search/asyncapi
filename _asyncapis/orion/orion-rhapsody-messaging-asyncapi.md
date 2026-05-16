---
api_specs:
- filename: orion-fhir-openapi.yml
  format: yaml
  label: Orion Health FHIR API
  slug: orion-health-fhir-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/orion/refs/heads/main/openapi/orion-fhir-openapi.yml
- filename: orion-population-health-openapi.yml
  format: yaml
  label: Orion Health Population Health API
  slug: orion-health-population-health-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/orion/refs/heads/main/openapi/orion-population-health-openapi.yml
- filename: orion-hie-openapi.yml
  format: yaml
  label: Orion Health HIE API
  slug: orion-health-hie-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/orion/refs/heads/main/openapi/orion-hie-openapi.yml
- filename: orion-rhapsody-openapi.yml
  format: yaml
  label: Orion Health Rhapsody Integration API
  slug: orion-health-rhapsody-integration-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/orion/refs/heads/main/openapi/orion-rhapsody-openapi.yml
channels:
- description: Patient admission events (HL7v2 ADT^A01). Triggered when a patient is admitted to a healthcare facility. Contains patient demographics, visit information, attending provider, and insurance details.
  name: adt/patient-admit
  operation: publish
  operation_id: sendPatientAdmit
  summary: Send a patient admission event
- description: Patient discharge events (HL7v2 ADT^A03). Triggered when a patient is discharged from a healthcare facility. Contains discharge disposition, diagnosis codes, and follow-up instructions.
  name: adt/patient-discharge
  operation: publish
  operation_id: sendPatientDischarge
  summary: Send a patient discharge event
- description: Patient transfer events (HL7v2 ADT^A02). Triggered when a patient is transferred between locations or units within a facility.
  name: adt/patient-transfer
  operation: publish
  operation_id: sendPatientTransfer
  summary: Send a patient transfer event
- description: Patient registration events (HL7v2 ADT^A04). Triggered when a patient is registered for outpatient services.
  name: adt/patient-registration
  operation: publish
  operation_id: sendPatientRegistration
  summary: Send a patient registration event
- description: Patient demographics update events (HL7v2 ADT^A08). Triggered when patient demographic information is updated in the source system.
  name: adt/patient-update
  operation: publish
  operation_id: sendPatientUpdate
  summary: Send a patient update event
- description: Patient merge events (HL7v2 ADT^A40). Triggered when duplicate patient records are merged in the source system.
  name: adt/patient-merge
  operation: subscribe
  operation_id: onPatientMerge
  summary: Receive patient merge events
- description: New order events (HL7v2 ORM^O01). Triggered when a new clinical order is placed, such as laboratory, radiology, or pharmacy orders.
  name: orders/new-order
  operation: publish
  operation_id: sendNewOrder
  summary: Send a new order event
- description: Order update events. Triggered when an existing order is modified, cancelled, or its status changes.
  name: orders/order-update
  operation: subscribe
  operation_id: onOrderUpdate
  summary: Receive order update events
- description: Observation result events (HL7v2 ORU^R01). Triggered when clinical results are available, including laboratory results, radiology reports, and other diagnostic findings.
  name: results/observation-result
  operation: publish
  operation_id: sendObservationResult
  summary: Send an observation result event
- description: Scheduling notification events (HL7v2 SIU^S12-S17). Triggered when appointments are created, modified, or cancelled.
  name: scheduling/appointment-notification
  operation: subscribe
  operation_id: onAppointmentNotification
  summary: Receive appointment notification events
- description: FHIR Subscription notification events. Triggered when FHIR resources matching a subscription criteria are created or updated, delivered as FHIR Bundle notifications over HTTPS.
  name: fhir/subscription-notification
  operation: subscribe
  operation_id: onFhirSubscriptionNotification
  summary: Receive FHIR subscription notifications
- description: Clinical document events (HL7v2 MDM^T02). Triggered when clinical documents such as discharge summaries, progress notes, or consult notes are created or updated.
  name: documents/clinical-document
  operation: publish
  operation_id: sendClinicalDocument
  summary: Send a clinical document event
description: The Orion Health Rhapsody Integration Engine processes healthcare messages in real-time across connected healthcare systems. This specification describes the event-driven messaging patterns supported by Rhapsody, including HL7v2 ADT (Admit/Discharge/Transfer) events, order messages (ORM/OML), result messages (ORU), and FHIR subscription notifications. Rhapsody acts as a healthcare message broker, routing and transforming messages between clinical systems using MLLP, TCP, HTTP, and other transport protocols.
layout: asyncapi
messages:
- description: ''
  name: ADT_A01
  summary: HL7v2 ADT^A01 patient admission message
  title: Patient Admission
- description: ''
  name: ADT_A02
  summary: HL7v2 ADT^A02 patient transfer message
  title: Patient Transfer
- description: ''
  name: ADT_A03
  summary: HL7v2 ADT^A03 patient discharge message
  title: Patient Discharge
- description: ''
  name: ADT_A04
  summary: HL7v2 ADT^A04 patient registration message
  title: Patient Registration
- description: ''
  name: ADT_A08
  summary: HL7v2 ADT^A08 patient information update message
  title: Patient Demographics Update
- description: ''
  name: ADT_A40
  summary: HL7v2 ADT^A40 patient merge message
  title: Patient Merge
- description: ''
  name: ORM_O01
  summary: HL7v2 ORM^O01 general order message
  title: New Order
- description: ''
  name: ORU_R01
  summary: HL7v2 ORU^R01 observation result message
  title: Observation Result
- description: ''
  name: SIU_S12
  summary: HL7v2 SIU^S12 scheduling notification message
  title: Appointment Notification
- description: ''
  name: FHIRSubscriptionNotification
  summary: FHIR R4 subscription notification bundle
  title: FHIR Subscription Notification
- description: ''
  name: MDM_T02
  summary: HL7v2 MDM^T02 document notification with content
  title: Clinical Document Notification
name: Orion Health Rhapsody Messaging Events
provider_name: Orion Health
provider_slug: orion
servers:
- description: Production MLLP endpoint for HL7v2 messaging
  name: production
  protocol: mllp
  url: mllp://integration.orionhealth.com:2575
- description: Production HTTPS endpoint for FHIR and REST messaging
  name: production-http
  protocol: https
  url: https://integration.orionhealth.com/messaging
- description: Sandbox MLLP endpoint
  name: sandbox
  protocol: mllp
  url: mllp://sandbox-integration.orionhealth.com:2575
- description: Sandbox HTTPS endpoint
  name: sandbox-http
  protocol: https
  url: https://sandbox-integration.orionhealth.com/messaging
slug: orion-rhapsody-messaging-asyncapi
source_filename: orion-rhapsody-messaging-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Orion Health Rhapsody Messaging Events\n  version: 1.0.0\n  description: >-\n    The Orion Health Rhapsody Integration Engine processes healthcare messages\n    in real-time across connected healthcare systems. This specification\n    describes the event-driven messaging patterns supported by Rhapsody,\n    including HL7v2 ADT (Admit/Discharge/Transfer) events, order messages\n    (ORM/OML), result messages (ORU), and FHIR subscription notifications.\n    Rhapsody acts as a healthcare message broker, routing and transforming\n    messages between clinical systems using MLLP, TCP, HTTP, and other\n    transport protocols.\n  contact:\n    name: Orion Health API Support\n    email: apisupport@orionhealth.com\n    url: https://www.orionhealth.com/support\n  license:\n    name: Proprietary\n    url: https://www.orionhealth.com/terms-of-service\nservers:\n  production:\n    url: mllp://integration.orionhealth.com:2575\n    protocol: mllp\n    description:\
  \ Production MLLP endpoint for HL7v2 messaging\n  production-http:\n    url: https://integration.orionhealth.com/messaging\n    protocol: https\n    description: Production HTTPS endpoint for FHIR and REST messaging\n  sandbox:\n    url: mllp://sandbox-integration.orionhealth.com:2575\n    protocol: mllp\n    description: Sandbox MLLP endpoint\n  sandbox-http:\n    url: https://sandbox-integration.orionhealth.com/messaging\n    protocol: https\n    description: Sandbox HTTPS endpoint\ndefaultContentType: application/json\nchannels:\n  adt/patient-admit:\n    description: >-\n      Patient admission events (HL7v2 ADT^A01). Triggered when a patient\n      is admitted to a healthcare facility. Contains patient demographics,\n      visit information, attending provider, and insurance details.\n    subscribe:\n      operationId: onPatientAdmit\n      summary: Receive patient admission events\n      message:\n        $ref: '#/components/messages/ADT_A01'\n    publish:\n      operationId: sendPatientAdmit\n\
  \      summary: Send a patient admission event\n      message:\n        $ref: '#/components/messages/ADT_A01'\n  adt/patient-discharge:\n    description: >-\n      Patient discharge events (HL7v2 ADT^A03). Triggered when a patient\n      is discharged from a healthcare facility. Contains discharge\n      disposition, diagnosis codes, and follow-up instructions.\n    subscribe:\n      operationId: onPatientDischarge\n      summary: Receive patient discharge events\n      message:\n        $ref: '#/components/messages/ADT_A03'\n    publish:\n      operationId: sendPatientDischarge\n      summary: Send a patient discharge event\n      message:\n        $ref: '#/components/messages/ADT_A03'\n  adt/patient-transfer:\n    description: >-\n      Patient transfer events (HL7v2 ADT^A02). Triggered when a patient\n      is transferred between locations or units within a facility.\n    subscribe:\n      operationId: onPatientTransfer\n      summary: Receive patient transfer events\n      message:\n\
  \        $ref: '#/components/messages/ADT_A02'\n    publish:\n      operationId: sendPatientTransfer\n      summary: Send a patient transfer event\n      message:\n        $ref: '#/components/messages/ADT_A02'\n  adt/patient-registration:\n    description: >-\n      Patient registration events (HL7v2 ADT^A04). Triggered when a\n      patient is registered for outpatient services.\n    subscribe:\n      operationId: onPatientRegistration\n      summary: Receive patient registration events\n      message:\n        $ref: '#/components/messages/ADT_A04'\n    publish:\n      operationId: sendPatientRegistration\n      summary: Send a patient registration event\n      message:\n        $ref: '#/components/messages/ADT_A04'\n  adt/patient-update:\n    description: >-\n      Patient demographics update events (HL7v2 ADT^A08). Triggered when\n      patient demographic information is updated in the source system.\n    subscribe:\n      operationId: onPatientUpdate\n      summary: Receive patient\
  \ update events\n      message:\n        $ref: '#/components/messages/ADT_A08'\n    publish:\n      operationId: sendPatientUpdate\n      summary: Send a patient update event\n      message:\n        $ref: '#/components/messages/ADT_A08'\n  adt/patient-merge:\n    description: >-\n      Patient merge events (HL7v2 ADT^A40). Triggered when duplicate\n      patient records are merged in the source system.\n    subscribe:\n      operationId: onPatientMerge\n      summary: Receive patient merge events\n      message:\n        $ref: '#/components/messages/ADT_A40'\n  orders/new-order:\n    description: >-\n      New order events (HL7v2 ORM^O01). Triggered when a new clinical\n      order is placed, such as laboratory, radiology, or pharmacy orders.\n    subscribe:\n      operationId: onNewOrder\n      summary: Receive new order events\n      message:\n        $ref: '#/components/messages/ORM_O01'\n    publish:\n      operationId: sendNewOrder\n      summary: Send a new order event\n      message:\n\
  \        $ref: '#/components/messages/ORM_O01'\n  orders/order-update:\n    description: >-\n      Order update events. Triggered when an existing order is modified,\n      cancelled, or its status changes.\n    subscribe:\n      operationId: onOrderUpdate\n      summary: Receive order update events\n      message:\n        $ref: '#/components/messages/ORM_O01'\n  results/observation-result:\n    description: >-\n      Observation result events (HL7v2 ORU^R01). Triggered when clinical\n      results are available, including laboratory results, radiology\n      reports, and other diagnostic findings.\n    subscribe:\n      operationId: onObservationResult\n      summary: Receive observation result events\n      message:\n        $ref: '#/components/messages/ORU_R01'\n    publish:\n      operationId: sendObservationResult\n      summary: Send an observation result event\n      message:\n        $ref: '#/components/messages/ORU_R01'\n  scheduling/appointment-notification:\n    description:\
  \ >-\n      Scheduling notification events (HL7v2 SIU^S12-S17). Triggered when\n      appointments are created, modified, or cancelled.\n    subscribe:\n      operationId: onAppointmentNotification\n      summary: Receive appointment notification events\n      message:\n        $ref: '#/components/messages/SIU_S12'\n  fhir/subscription-notification:\n    description: >-\n      FHIR Subscription notification events. Triggered when FHIR resources\n      matching a subscription criteria are created or updated, delivered\n      as FHIR Bundle notifications over HTTPS.\n    subscribe:\n      operationId: onFhirSubscriptionNotification\n      summary: Receive FHIR subscription notifications\n      message:\n        $ref: '#/components/messages/FHIRSubscriptionNotification'\n  documents/clinical-document:\n    description: >-\n      Clinical document events (HL7v2 MDM^T02). Triggered when clinical\n      documents such as discharge summaries, progress notes, or consult\n      notes are created\
  \ or updated.\n    subscribe:\n      operationId: onClinicalDocument\n      summary: Receive clinical document events\n      message:\n        $ref: '#/components/messages/MDM_T02'\n    publish:\n      operationId: sendClinicalDocument\n      summary: Send a clinical document event\n      message:\n        $ref: '#/components/messages/MDM_T02'\ncomponents:\n  messages:\n    ADT_A01:\n      name: ADT_A01\n      title: Patient Admission\n      summary: HL7v2 ADT^A01 patient admission message\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ADTEvent'\n      headers:\n        type: object\n        properties:\n          messageType:\n            type: string\n            const: ADT^A01\n            description: HL7 message type\n          messageControlId:\n            type: string\n            description: Unique message identifier\n          sendingFacility:\n            type: string\n          receivingFacility:\n            type: string\n      \
  \    timestamp:\n            type: string\n            format: date-time\n    ADT_A02:\n      name: ADT_A02\n      title: Patient Transfer\n      summary: HL7v2 ADT^A02 patient transfer message\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ADTTransferEvent'\n      headers:\n        type: object\n        properties:\n          messageType:\n            type: string\n            const: ADT^A02\n          messageControlId:\n            type: string\n          sendingFacility:\n            type: string\n          receivingFacility:\n            type: string\n          timestamp:\n            type: string\n            format: date-time\n    ADT_A03:\n      name: ADT_A03\n      title: Patient Discharge\n      summary: HL7v2 ADT^A03 patient discharge message\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ADTDischargeEvent'\n      headers:\n        type: object\n        properties:\n          messageType:\n\
  \            type: string\n            const: ADT^A03\n          messageControlId:\n            type: string\n          sendingFacility:\n            type: string\n          receivingFacility:\n            type: string\n          timestamp:\n            type: string\n            format: date-time\n    ADT_A04:\n      name: ADT_A04\n      title: Patient Registration\n      summary: HL7v2 ADT^A04 patient registration message\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ADTEvent'\n      headers:\n        type: object\n        properties:\n          messageType:\n            type: string\n            const: ADT^A04\n          messageControlId:\n            type: string\n          sendingFacility:\n            type: string\n          receivingFacility:\n            type: string\n          timestamp:\n            type: string\n            format: date-time\n    ADT_A08:\n      name: ADT_A08\n      title: Patient Demographics Update\n      summary:\
  \ HL7v2 ADT^A08 patient information update message\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ADTEvent'\n      headers:\n        type: object\n        properties:\n          messageType:\n            type: string\n            const: ADT^A08\n          messageControlId:\n            type: string\n          sendingFacility:\n            type: string\n          receivingFacility:\n            type: string\n          timestamp:\n            type: string\n            format: date-time\n    ADT_A40:\n      name: ADT_A40\n      title: Patient Merge\n      summary: HL7v2 ADT^A40 patient merge message\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ADTMergeEvent'\n      headers:\n        type: object\n        properties:\n          messageType:\n            type: string\n            const: ADT^A40\n          messageControlId:\n            type: string\n          sendingFacility:\n            type: string\n\
  \          receivingFacility:\n            type: string\n          timestamp:\n            type: string\n            format: date-time\n    ORM_O01:\n      name: ORM_O01\n      title: New Order\n      summary: HL7v2 ORM^O01 general order message\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/OrderEvent'\n      headers:\n        type: object\n        properties:\n          messageType:\n            type: string\n            const: ORM^O01\n          messageControlId:\n            type: string\n          sendingFacility:\n            type: string\n          receivingFacility:\n            type: string\n          timestamp:\n            type: string\n            format: date-time\n    ORU_R01:\n      name: ORU_R01\n      title: Observation Result\n      summary: HL7v2 ORU^R01 observation result message\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ResultEvent'\n      headers:\n        type: object\n   \
  \     properties:\n          messageType:\n            type: string\n            const: ORU^R01\n          messageControlId:\n            type: string\n          sendingFacility:\n            type: string\n          receivingFacility:\n            type: string\n          timestamp:\n            type: string\n            format: date-time\n    SIU_S12:\n      name: SIU_S12\n      title: Appointment Notification\n      summary: HL7v2 SIU^S12 scheduling notification message\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SchedulingEvent'\n      headers:\n        type: object\n        properties:\n          messageType:\n            type: string\n            description: SIU^S12 through SIU^S17\n          messageControlId:\n            type: string\n          sendingFacility:\n            type: string\n          receivingFacility:\n            type: string\n          timestamp:\n            type: string\n            format: date-time\n    FHIRSubscriptionNotification:\n\
  \      name: FHIRSubscriptionNotification\n      title: FHIR Subscription Notification\n      summary: FHIR R4 subscription notification bundle\n      contentType: application/fhir+json\n      payload:\n        $ref: '#/components/schemas/FHIRNotificationEvent'\n    MDM_T02:\n      name: MDM_T02\n      title: Clinical Document Notification\n      summary: HL7v2 MDM^T02 document notification with content\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/DocumentEvent'\n      headers:\n        type: object\n        properties:\n          messageType:\n            type: string\n            const: MDM^T02\n          messageControlId:\n            type: string\n          sendingFacility:\n            type: string\n          receivingFacility:\n            type: string\n          timestamp:\n            type: string\n            format: date-time\n  schemas:\n    ADTEvent:\n      type: object\n      properties:\n        messageHeader:\n          $ref:\
  \ '#/components/schemas/MessageHeader'\n        eventType:\n          type: string\n          description: ADT event type code\n        patient:\n          $ref: '#/components/schemas/PatientIdentification'\n        visit:\n          $ref: '#/components/schemas/PatientVisit'\n        attendingDoctor:\n          $ref: '#/components/schemas/Provider'\n        diagnosis:\n          type: array\n          items:\n            $ref: '#/components/schemas/Diagnosis'\n        insurance:\n          type: array\n          items:\n            $ref: '#/components/schemas/Insurance'\n    ADTTransferEvent:\n      type: object\n      properties:\n        messageHeader:\n          $ref: '#/components/schemas/MessageHeader'\n        eventType:\n          type: string\n          const: A02\n        patient:\n          $ref: '#/components/schemas/PatientIdentification'\n        visit:\n          $ref: '#/components/schemas/PatientVisit'\n        priorLocation:\n          $ref: '#/components/schemas/Location'\n\
  \        newLocation:\n          $ref: '#/components/schemas/Location'\n    ADTDischargeEvent:\n      type: object\n      properties:\n        messageHeader:\n          $ref: '#/components/schemas/MessageHeader'\n        eventType:\n          type: string\n          const: A03\n        patient:\n          $ref: '#/components/schemas/PatientIdentification'\n        visit:\n          $ref: '#/components/schemas/PatientVisit'\n        dischargeDisposition:\n          type: string\n          description: Discharge disposition code\n        dischargeDateTime:\n          type: string\n          format: date-time\n        diagnosis:\n          type: array\n          items:\n            $ref: '#/components/schemas/Diagnosis'\n    ADTMergeEvent:\n      type: object\n      properties:\n        messageHeader:\n          $ref: '#/components/schemas/MessageHeader'\n        eventType:\n          type: string\n          const: A40\n        survivingPatient:\n          $ref: '#/components/schemas/PatientIdentification'\n\
  \        mergedPatient:\n          $ref: '#/components/schemas/PatientIdentification'\n        mergeReason:\n          type: string\n    OrderEvent:\n      type: object\n      properties:\n        messageHeader:\n          $ref: '#/components/schemas/MessageHeader'\n        patient:\n          $ref: '#/components/schemas/PatientIdentification'\n        visit:\n          $ref: '#/components/schemas/PatientVisit'\n        orderControl:\n          type: string\n          description: Order control code (NW=New, CA=Cancel, XO=Change)\n          enum:\n            - NW\n            - CA\n            - XO\n            - DC\n            - HD\n            - RL\n            - SC\n        order:\n          type: object\n          properties:\n            placerOrderNumber:\n              type: string\n            fillerOrderNumber:\n              type: string\n            orderDateTime:\n              type: string\n              format: date-time\n            orderingProvider:\n              $ref:\
  \ '#/components/schemas/Provider'\n            orderCode:\n              type: string\n              description: Code identifying the ordered service\n            orderCodeSystem:\n              type: string\n              description: Coding system (LOINC, CPT, local)\n            orderCodeText:\n              type: string\n            priority:\n              type: string\n              enum:\n                - S\n                - A\n                - R\n                - T\n              description: 'S=Stat, A=ASAP, R=Routine, T=Timed'\n            specimenSource:\n              type: string\n            clinicalInformation:\n              type: string\n    ResultEvent:\n      type: object\n      properties:\n        messageHeader:\n          $ref: '#/components/schemas/MessageHeader'\n        patient:\n          $ref: '#/components/schemas/PatientIdentification'\n        visit:\n          $ref: '#/components/schemas/PatientVisit'\n        order:\n          type: object\n       \
  \   properties:\n            placerOrderNumber:\n              type: string\n            fillerOrderNumber:\n              type: string\n            orderCode:\n              type: string\n            orderCodeText:\n              type: string\n            resultStatus:\n              type: string\n              enum:\n                - F\n                - P\n                - C\n                - X\n              description: 'F=Final, P=Preliminary, C=Corrected, X=Cancelled'\n        observations:\n          type: array\n          items:\n            type: object\n            properties:\n              observationId:\n                type: string\n              observationCode:\n                type: string\n              observationCodeText:\n                type: string\n              value:\n                type: string\n              units:\n                type: string\n              referenceRange:\n                type: string\n              abnormalFlag:\n                type:\
  \ string\n                enum:\n                  - N\n                  - L\n                  - H\n                  - LL\n                  - HH\n                  - A\n                description: 'N=Normal, L=Low, H=High, LL=Critical Low, HH=Critical High, A=Abnormal'\n              resultStatus:\n                type: string\n              observationDateTime:\n                type: string\n                format: date-time\n    SchedulingEvent:\n      type: object\n      properties:\n        messageHeader:\n          $ref: '#/components/schemas/MessageHeader'\n        eventType:\n          type: string\n          description: Scheduling event type (S12-S17)\n        patient:\n          $ref: '#/components/schemas/PatientIdentification'\n        appointment:\n          type: object\n          properties:\n            appointmentId:\n              type: string\n            startDateTime:\n              type: string\n              format: date-time\n            endDateTime:\n    \
  \          type: string\n              format: date-time\n            duration:\n              type: integer\n              description: Duration in minutes\n            appointmentType:\n              type: string\n            appointmentReason:\n              type: string\n            status:\n              type: string\n              enum:\n                - booked\n                - cancelled\n                - rescheduled\n                - no-show\n                - completed\n            provider:\n              $ref: '#/components/schemas/Provider'\n            location:\n              $ref: '#/components/schemas/Location'\n    FHIRNotificationEvent:\n      type: object\n      properties:\n        resourceType:\n          type: string\n          const: Bundle\n        type:\n          type: string\n          const: history\n        timestamp:\n          type: string\n          format: date-time\n        entry:\n          type: array\n          items:\n            type: object\n\
  \            properties:\n              fullUrl:\n                type: string\n                format: uri\n              resource:\n                type: object\n                properties:\n                  resourceType:\n                    type: string\n                  id:\n                    type: string\n              request:\n                type: object\n                properties:\n                  method:\n                    type: string\n                    enum:\n                      - POST\n                      - PUT\n                      - DELETE\n                  url:\n                    type: string\n        subscription:\n          type: object\n          properties:\n            id:\n              type: string\n            criteria:\n              type: string\n            channel:\n              type: object\n              properties:\n                type:\n                  type: string\n                  enum:\n                    - rest-hook\n      \
  \              - websocket\n                    - email\n                endpoint:\n                  type: string\n                  format: uri\n    DocumentEvent:\n      type: object\n      properties:\n        messageHeader:\n          $ref: '#/components/schemas/MessageHeader'\n        patient:\n          $ref: '#/components/schemas/PatientIdentification'\n        document:\n          type: object\n          properties:\n            documentId:\n              type: string\n            documentType:\n              type: string\n              description: Document type code\n            documentTypeText:\n              type: string\n            activityDateTime:\n              type: string\n              format: date-time\n            author:\n              $ref: '#/components/schemas/Provider'\n            authenticator:\n              $ref: '#/components/schemas/Provider'\n            contentType:\n              type: string\n              description: MIME type of the document content\n\
  \            content:\n              type: string\n              description: Base64-encoded document content\n    MessageHeader:\n      type: object\n      properties:\n        messageControlId:\n          type: string\n          description: Unique message identifier\n        messageType:\n          type: string\n          description: HL7 message type (e.g., ADT^A01)\n        triggerEvent:\n          type: string\n          description: Trigger event code\n        sendingApplication:\n          type: string\n        sendingFacility:\n          type: string\n        receivingApplication:\n          type: string\n        receivingFacility:\n          type: string\n        messageDateTime:\n          type: string\n          format: date-time\n        processingId:\n          type: string\n          enum:\n            - P\n            - T\n            - D\n          description: 'P=Production, T=Training, D=Debugging'\n        versionId:\n          type: string\n          description: HL7\
  \ version (e.g., 2.5.1)\n    PatientIdentification:\n      type: object\n      properties:\n        patientId:\n          type: string\n          description: Internal patient identifier\n        mrn:\n          type: string\n          description: Medical record number\n        externalIds:\n          type: array\n          items:\n            type: object\n            properties:\n              id:\n                type: string\n              assigningAuthority:\n                type: string\n              idType:\n                type: string\n        familyName:\n          type: string\n        givenName:\n          type: string\n        middleName:\n          type: string\n        dateOfBirth:\n          type: string\n          format: date\n        gender:\n          type: string\n          enum:\n            - M\n            - F\n            - O\n            - U\n        ssn:\n          type: string\n        address:\n          type: object\n          properties:\n            streetAddress:\n\
  \              type: string\n            city:\n              type: string\n            state:\n              type: string\n            postalCode:\n              type: string\n            country:\n              type: string\n        phone:\n          type: string\n        email:\n          type: string\n    PatientVisit:\n      type: object\n      properties:\n        visitNumber:\n          type: string\n        patientClass:\n          type: string\n          enum:\n            - I\n            - O\n            - E\n            - P\n          description: 'I=Inpatient, O=Outpatient, E=Emergency, P=Preadmit'\n        assignedLocation:\n          $ref: '#/components/schemas/Location'\n        admitDateTime:\n          type: string\n          format: date-time\n        dischargeDateTime:\n          type: string\n          format: date-time\n        admitReason:\n          type: string\n        admitSource:\n          type: string\n        visitType:\n          type: string\n    Location:\n\
  \      type: object\n      properties:\n        pointOfCare:\n          type: string\n          description: Ward or clinic\n        room:\n          type: string\n        bed:\n          type: string\n        facility:\n          type: string\n        building:\n          type: string\n        floor:\n          type: string\n    Provider:\n      type: object\n      properties:\n        id:\n          type: string\n        npi:\n          type: string\n        familyName:\n          type: string\n        givenName:\n          type: string\n        prefix:\n          type: string\n        specialty:\n          type: string\n    Diagnosis:\n      type: object\n      properties:\n        code:\n          type: string\n        codingSystem:\n          type: string\n          description: Coding system (ICD-10, SNOMED)\n        description:\n          type: string\n        type:\n          type: string\n          enum:\n            - admitting\n            - final\n            - working\n \
  \       dateTime:\n          type: string\n          format: date-time\n    Insurance:\n      type: object\n      properties:\n        planId:\n          type: string\n        planName:\n          type: string\n        groupNumber:\n          type: string\n        policyNumber:\n          type: string\n        subscriberName:\n          type: string\n        relationship:\n          type: string\n        coordinationOfBenefits:\n          type: integer\n          description: 'Priority order (1=Primary, 2=Secondary)'\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/orion/refs/heads/main/asyncapi/orion-rhapsody-messaging-asyncapi.yml
spec_file: asyncapi/orion-rhapsody-messaging-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/orion/refs/heads/main/asyncapi/orion-rhapsody-messaging-asyncapi.yml
tags:
- EHR
- FHIR
- Health IT
- Healthcare
- HIE
- HL7
- Integration
- Interoperability
- Population Health
- AsyncAPI
- Webhooks
- Events
version: 1.0.0
---
