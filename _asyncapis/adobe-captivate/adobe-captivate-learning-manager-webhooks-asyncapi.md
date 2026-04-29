---
api_specs:
- filename: adobe-captivate-prime-api-openapi.yml
  format: yaml
  label: Adobe Captivate Prime API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-captivate/refs/heads/main/openapi/adobe-captivate-prime-api-openapi.yml
- filename: adobe-captivate-learning-manager-webhooks-asyncapi.yml
  format: yaml
  label: Adobe Learning Manager Webhooks API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/adobe-captivate/refs/heads/main/asyncapi/adobe-captivate-learning-manager-webhooks-asyncapi.yml
channels:
- description: Events triggered when a learner enrolls in a course, learning program, certification, or job aid. Includes both self-enrollment and manager/admin-initiated enrollments.
  name: /learner-enrollment
  operation: subscribe
  operation_id: onLearnerEnrollment
  summary: Learner enrollment event
- description: Events triggered when a learner completes a course, learning program, or certification module. Includes completion status, score, and timestamp information.
  name: /learner-completion
  operation: subscribe
  operation_id: onLearnerCompletion
  summary: Learner completion event
- description: Events triggered when a learner's progress in a course or module is updated. Tracks incremental progress changes.
  name: /learner-progress
  operation: subscribe
  operation_id: onLearnerProgress
  summary: Learner progress update event
- description: Events triggered when a learner is unenrolled from a course, learning program, or certification.
  name: /learner-unenrollment
  operation: subscribe
  operation_id: onLearnerUnenrollment
  summary: Learner unenrollment event
- description: Events triggered when a new course or learning object is created in the Learning Manager account.
  name: /course-created
  operation: subscribe
  operation_id: onCourseCreated
  summary: Course creation event
- description: Events triggered when an existing course or learning object is modified, including content updates, metadata changes, and state transitions.
  name: /course-updated
  operation: subscribe
  operation_id: onCourseUpdated
  summary: Course update event
- description: Events triggered when a badge is awarded to a learner upon achieving a specific milestone or completing a learning objective.
  name: /badge-awarded
  operation: subscribe
  operation_id: onBadgeAwarded
  summary: Badge awarded event
- description: Events triggered when a learner completes a certification, including initial certification and recertification cycles.
  name: /certification-completed
  operation: subscribe
  operation_id: onCertificationCompleted
  summary: Certification completion event
- description: Events triggered when a learner achieves a new skill level through course completions or skill credit assignments.
  name: /skill-achieved
  operation: subscribe
  operation_id: onSkillAchieved
  summary: Skill achievement event
- description: Events triggered when a new user is created in the Learning Manager account, either through self-registration, admin creation, or bulk import.
  name: /user-created
  operation: subscribe
  operation_id: onUserCreated
  summary: User creation event
- description: Events triggered when a user's profile or state is updated, including role changes, group assignments, and status changes.
  name: /user-updated
  operation: subscribe
  operation_id: onUserUpdated
  summary: User update event
- description: Events triggered when a user is deleted or purged from the Learning Manager account.
  name: /user-deleted
  operation: subscribe
  operation_id: onUserDeleted
  summary: User deletion event
- description: Events triggered when a bulk import or export job completes, including status and result details.
  name: /job-completed
  operation: subscribe
  operation_id: onJobCompleted
  summary: Job completion event
description: The Adobe Learning Manager Webhooks API enables real-time event notifications for learning management activities. When configured, Adobe Learning Manager sends HTTP POST requests to registered webhook URLs whenever significant events occur, such as learner enrollments, course completions, certification achievements, badge awards, and administrative changes. Webhooks support real-time integration with external systems, enabling automated workflows for learner management, reporting, and compliance tracking. Events are delivered as JSON payloads with retry logic for failed deliveries.
layout: asyncapi
messages:
- description: ''
  name: LearnerEnrollmentEvent
  summary: Notification when a learner enrolls in a learning object
  title: Learner Enrollment Event
- description: ''
  name: LearnerCompletionEvent
  summary: Notification when a learner completes a learning object
  title: Learner Completion Event
- description: ''
  name: LearnerProgressEvent
  summary: Notification when learner progress is updated
  title: Learner Progress Event
- description: ''
  name: LearnerUnenrollmentEvent
  summary: Notification when a learner is unenrolled
  title: Learner Unenrollment Event
- description: ''
  name: CourseCreatedEvent
  summary: Notification when a new course is created
  title: Course Created Event
- description: ''
  name: CourseUpdatedEvent
  summary: Notification when a course is updated
  title: Course Updated Event
- description: ''
  name: BadgeAwardedEvent
  summary: Notification when a badge is awarded to a learner
  title: Badge Awarded Event
- description: ''
  name: CertificationCompletedEvent
  summary: Notification when a learner completes a certification
  title: Certification Completed Event
- description: ''
  name: SkillAchievedEvent
  summary: Notification when a learner achieves a new skill level
  title: Skill Achieved Event
- description: ''
  name: UserCreatedEvent
  summary: Notification when a new user is created
  title: User Created Event
- description: ''
  name: UserUpdatedEvent
  summary: Notification when a user is updated
  title: User Updated Event
- description: ''
  name: UserDeletedEvent
  summary: Notification when a user is deleted
  title: User Deleted Event
- description: ''
  name: JobCompletedEvent
  summary: Notification when a bulk job completes
  title: Job Completed Event
name: Adobe Learning Manager Webhooks API
provider_name: Adobe Captivate
provider_slug: adobe-captivate
servers:
- description: Your webhook receiver endpoint. Adobe Learning Manager sends HTTP POST requests to this URL when events occur. The URL must be HTTPS and publicly accessible.
  name: webhookReceiver
  protocol: https
  url: '{webhookUrl}'
slug: adobe-captivate-learning-manager-webhooks-asyncapi
source_filename: adobe-captivate-learning-manager-webhooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Adobe Learning Manager Webhooks API\n  description: >-\n    The Adobe Learning Manager Webhooks API enables real-time event\n    notifications for learning management activities. When configured,\n    Adobe Learning Manager sends HTTP POST requests to registered webhook\n    URLs whenever significant events occur, such as learner enrollments,\n    course completions, certification achievements, badge awards, and\n    administrative changes. Webhooks support real-time integration with\n    external systems, enabling automated workflows for learner management,\n    reporting, and compliance tracking. Events are delivered as JSON\n    payloads with retry logic for failed deliveries.\n  version: '1.0'\n  contact:\n    name: Adobe Learning Manager Support\n    url: https://helpx.adobe.com/learning-manager/kb/helpdesk.html\n  termsOfService: https://www.adobe.com/legal/terms.html\nexternalDocs:\n  description: Adobe Learning Manager Webhooks Documentation\n\
  \  url: https://experienceleague.adobe.com/docs/learning-manager/using/integration/feature-summary/webhooks.html\nservers:\n  webhookReceiver:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your webhook receiver endpoint. Adobe Learning Manager sends HTTP\n      POST requests to this URL when events occur. The URL must be HTTPS\n      and publicly accessible.\n    variables:\n      webhookUrl:\n        description: >-\n          The HTTPS URL of your webhook endpoint registered in Adobe\n          Learning Manager\n    security:\n    - hmacSignature: []\nchannels:\n  /learner-enrollment:\n    description: >-\n      Events triggered when a learner enrolls in a course, learning program,\n      certification, or job aid. Includes both self-enrollment and\n      manager/admin-initiated enrollments.\n    subscribe:\n      operationId: onLearnerEnrollment\n      summary: Learner enrollment event\n      description: >-\n        Fired when a learner is enrolled in a\
  \ learning object. The event\n        payload contains the learner details, the learning object they\n        enrolled in, and the enrollment metadata including enrollment type\n        and date.\n      message:\n        $ref: '#/components/messages/LearnerEnrollmentEvent'\n  /learner-completion:\n    description: >-\n      Events triggered when a learner completes a course, learning program,\n      or certification module. Includes completion status, score, and\n      timestamp information.\n    subscribe:\n      operationId: onLearnerCompletion\n      summary: Learner completion event\n      description: >-\n        Fired when a learner completes a learning object. The event payload\n        contains completion details including score, pass/fail status,\n        and completion timestamp.\n      message:\n        $ref: '#/components/messages/LearnerCompletionEvent'\n  /learner-progress:\n    description: >-\n      Events triggered when a learner's progress in a course or module\n    \
  \  is updated. Tracks incremental progress changes.\n    subscribe:\n      operationId: onLearnerProgress\n      summary: Learner progress update event\n      description: >-\n        Fired when a learner's progress in a learning object changes.\n        The payload includes the old and new progress percentage.\n      message:\n        $ref: '#/components/messages/LearnerProgressEvent'\n  /learner-unenrollment:\n    description: >-\n      Events triggered when a learner is unenrolled from a course,\n      learning program, or certification.\n    subscribe:\n      operationId: onLearnerUnenrollment\n      summary: Learner unenrollment event\n      description: >-\n        Fired when a learner is removed from a learning object enrollment.\n        Includes the reason for unenrollment and who initiated it.\n      message:\n        $ref: '#/components/messages/LearnerUnenrollmentEvent'\n  /course-created:\n    description: >-\n      Events triggered when a new course or learning object is\
  \ created\n      in the Learning Manager account.\n    subscribe:\n      operationId: onCourseCreated\n      summary: Course creation event\n      description: >-\n        Fired when a new learning object (course, learning program,\n        certification, or job aid) is created by an author or admin.\n      message:\n        $ref: '#/components/messages/CourseCreatedEvent'\n  /course-updated:\n    description: >-\n      Events triggered when an existing course or learning object is\n      modified, including content updates, metadata changes, and state\n      transitions.\n    subscribe:\n      operationId: onCourseUpdated\n      summary: Course update event\n      description: >-\n        Fired when a learning object's content, metadata, or state is\n        updated. Includes details about what changed.\n      message:\n        $ref: '#/components/messages/CourseUpdatedEvent'\n  /badge-awarded:\n    description: >-\n      Events triggered when a badge is awarded to a learner upon\n  \
  \    achieving a specific milestone or completing a learning objective.\n    subscribe:\n      operationId: onBadgeAwarded\n      summary: Badge awarded event\n      description: >-\n        Fired when a learner earns a badge. The payload contains the\n        badge details and the achievement that triggered the award.\n      message:\n        $ref: '#/components/messages/BadgeAwardedEvent'\n  /certification-completed:\n    description: >-\n      Events triggered when a learner completes a certification, including\n      initial certification and recertification cycles.\n    subscribe:\n      operationId: onCertificationCompleted\n      summary: Certification completion event\n      description: >-\n        Fired when a learner completes a certification program. Includes\n        certification validity dates and recertification deadlines.\n      message:\n        $ref: '#/components/messages/CertificationCompletedEvent'\n  /skill-achieved:\n    description: >-\n      Events triggered when\
  \ a learner achieves a new skill level through\n      course completions or skill credit assignments.\n    subscribe:\n      operationId: onSkillAchieved\n      summary: Skill achievement event\n      description: >-\n        Fired when a learner achieves a new level for a skill. Includes\n        the skill name, level achieved, and credits earned.\n      message:\n        $ref: '#/components/messages/SkillAchievedEvent'\n  /user-created:\n    description: >-\n      Events triggered when a new user is created in the Learning Manager\n      account, either through self-registration, admin creation, or bulk\n      import.\n    subscribe:\n      operationId: onUserCreated\n      summary: User creation event\n      description: >-\n        Fired when a new user account is created. Includes user profile\n        details and the creation method.\n      message:\n        $ref: '#/components/messages/UserCreatedEvent'\n  /user-updated:\n    description: >-\n      Events triggered when a user's\
  \ profile or state is updated,\n      including role changes, group assignments, and status changes.\n    subscribe:\n      operationId: onUserUpdated\n      summary: User update event\n      description: >-\n        Fired when a user's profile information, role, or state is\n        changed. Includes the updated fields.\n      message:\n        $ref: '#/components/messages/UserUpdatedEvent'\n  /user-deleted:\n    description: >-\n      Events triggered when a user is deleted or purged from the Learning\n      Manager account.\n    subscribe:\n      operationId: onUserDeleted\n      summary: User deletion event\n      description: >-\n        Fired when a user account is deleted. Includes the user ID and\n        deletion timestamp.\n      message:\n        $ref: '#/components/messages/UserDeletedEvent'\n  /job-completed:\n    description: >-\n      Events triggered when a bulk import or export job completes,\n      including status and result details.\n    subscribe:\n      operationId:\
  \ onJobCompleted\n      summary: Job completion event\n      description: >-\n        Fired when a bulk job (user import, transcript export, etc.)\n        finishes processing. Includes job status and download URL for\n        export jobs.\n      message:\n        $ref: '#/components/messages/JobCompletedEvent'\ncomponents:\n  securitySchemes:\n    hmacSignature:\n      type: httpApiKey\n      name: X-ALM-Webhook-Signature\n      in: header\n      description: >-\n        HMAC-SHA256 signature of the webhook payload, computed using the\n        shared secret configured during webhook registration. Receivers\n        should validate this signature to verify the authenticity of\n        incoming events.\n  schemas:\n    WebhookEventBase:\n      type: object\n      description: Base schema for all webhook event payloads\n      required:\n      - eventType\n      - eventId\n      - accountId\n      - timestamp\n      properties:\n        eventType:\n          type: string\n          description:\
  \ The type of event that triggered this webhook\n        eventId:\n          type: string\n          format: uuid\n          description: Unique identifier for this event instance\n        accountId:\n          type: string\n          description: The Learning Manager account ID\n        timestamp:\n          type: string\n          format: date-time\n          description: ISO 8601 timestamp when the event occurred\n        source:\n          type: string\n          description: The system component that generated the event\n          enum:\n          - learner\n          - admin\n          - manager\n          - system\n          - api\n    LearnerReference:\n      type: object\n      description: Reference to a learner involved in an event\n      properties:\n        userId:\n          type: string\n          description: Unique user identifier\n        name:\n          type: string\n          description: Learner's full name\n        email:\n          type: string\n          format:\
  \ email\n          description: Learner's email address\n    LearningObjectReference:\n      type: object\n      description: Reference to a learning object involved in an event\n      properties:\n        loId:\n          type: string\n          description: Learning object identifier\n        loType:\n          type: string\n          description: Type of learning object\n          enum:\n          - course\n          - learningProgram\n          - certification\n          - jobAid\n        name:\n          type: string\n          description: Learning object name\n        instanceId:\n          type: string\n          description: Learning object instance identifier\n    LearnerEnrollmentPayload:\n      allOf:\n      - $ref: '#/components/schemas/WebhookEventBase'\n      - type: object\n        properties:\n          eventType:\n            const: LEARNER_ENROLLMENT\n          learner:\n            $ref: '#/components/schemas/LearnerReference'\n          learningObject:\n          \
  \  $ref: '#/components/schemas/LearningObjectReference'\n          enrollmentId:\n            type: string\n            description: Unique enrollment identifier\n          enrollmentType:\n            type: string\n            description: How the enrollment was initiated\n            enum:\n            - selfEnrolled\n            - managerNominated\n            - adminEnrolled\n            - autoEnrolled\n          dateEnrolled:\n            type: string\n            format: date-time\n            description: Enrollment timestamp\n    LearnerCompletionPayload:\n      allOf:\n      - $ref: '#/components/schemas/WebhookEventBase'\n      - type: object\n        properties:\n          eventType:\n            const: LEARNER_COMPLETION\n          learner:\n            $ref: '#/components/schemas/LearnerReference'\n          learningObject:\n            $ref: '#/components/schemas/LearningObjectReference'\n          enrollmentId:\n            type: string\n            description: Enrollment\
  \ identifier\n          completedOn:\n            type: string\n            format: date-time\n            description: Completion timestamp\n          hasPassed:\n            type: boolean\n            description: Whether the learner passed\n          score:\n            type: number\n            description: Score achieved\n          progressPercent:\n            type: integer\n            description: Final progress percentage\n            const: 100\n    LearnerProgressPayload:\n      allOf:\n      - $ref: '#/components/schemas/WebhookEventBase'\n      - type: object\n        properties:\n          eventType:\n            const: LEARNER_PROGRESS\n          learner:\n            $ref: '#/components/schemas/LearnerReference'\n          learningObject:\n            $ref: '#/components/schemas/LearningObjectReference'\n          enrollmentId:\n            type: string\n            description: Enrollment identifier\n          progressPercent:\n            type: integer\n            description:\
  \ Current progress percentage\n            minimum: 0\n            maximum: 100\n    LearnerUnenrollmentPayload:\n      allOf:\n      - $ref: '#/components/schemas/WebhookEventBase'\n      - type: object\n        properties:\n          eventType:\n            const: LEARNER_UNENROLLMENT\n          learner:\n            $ref: '#/components/schemas/LearnerReference'\n          learningObject:\n            $ref: '#/components/schemas/LearningObjectReference'\n          enrollmentId:\n            type: string\n            description: Enrollment identifier\n          unenrolledBy:\n            type: string\n            description: Who initiated the unenrollment\n            enum:\n            - learner\n            - manager\n            - admin\n            - system\n          dateUnenrolled:\n            type: string\n            format: date-time\n            description: Unenrollment timestamp\n    CourseCreatedPayload:\n      allOf:\n      - $ref: '#/components/schemas/WebhookEventBase'\n\
  \      - type: object\n        properties:\n          eventType:\n            const: COURSE_CREATED\n          learningObject:\n            $ref: '#/components/schemas/LearningObjectReference'\n          createdBy:\n            type: string\n            description: User ID of the creator\n          dateCreated:\n            type: string\n            format: date-time\n            description: Creation timestamp\n    CourseUpdatedPayload:\n      allOf:\n      - $ref: '#/components/schemas/WebhookEventBase'\n      - type: object\n        properties:\n          eventType:\n            const: COURSE_UPDATED\n          learningObject:\n            $ref: '#/components/schemas/LearningObjectReference'\n          updatedBy:\n            type: string\n            description: User ID of who made the update\n          updatedFields:\n            type: array\n            description: List of fields that were modified\n            items:\n              type: string\n          dateUpdated:\n     \
  \       type: string\n            format: date-time\n            description: Update timestamp\n    BadgeAwardedPayload:\n      allOf:\n      - $ref: '#/components/schemas/WebhookEventBase'\n      - type: object\n        properties:\n          eventType:\n            const: BADGE_AWARDED\n          learner:\n            $ref: '#/components/schemas/LearnerReference'\n          badge:\n            type: object\n            properties:\n              badgeId:\n                type: string\n                description: Badge identifier\n              name:\n                type: string\n                description: Badge name\n              imageUrl:\n                type: string\n                format: uri\n                description: Badge image URL\n          dateAwarded:\n            type: string\n            format: date-time\n            description: Award timestamp\n    CertificationCompletedPayload:\n      allOf:\n      - $ref: '#/components/schemas/WebhookEventBase'\n      - type:\
  \ object\n        properties:\n          eventType:\n            const: CERTIFICATION_COMPLETED\n          learner:\n            $ref: '#/components/schemas/LearnerReference'\n          certification:\n            type: object\n            properties:\n              certificationId:\n                type: string\n                description: Certification identifier\n              name:\n                type: string\n                description: Certification name\n              instanceId:\n                type: string\n                description: Certification instance identifier\n          completedOn:\n            type: string\n            format: date-time\n            description: Completion timestamp\n          validUntil:\n            type: string\n            format: date-time\n            description: Certification validity expiration date\n          recertificationDeadline:\n            type: string\n            format: date-time\n            description: Deadline for recertification\n\
  \    SkillAchievedPayload:\n      allOf:\n      - $ref: '#/components/schemas/WebhookEventBase'\n      - type: object\n        properties:\n          eventType:\n            const: SKILL_ACHIEVED\n          learner:\n            $ref: '#/components/schemas/LearnerReference'\n          skill:\n            type: object\n            properties:\n              skillId:\n                type: string\n                description: Skill identifier\n              name:\n                type: string\n                description: Skill name\n              levelName:\n                type: string\n                description: Skill level name achieved\n              credits:\n                type: number\n                description: Skill credits earned\n          dateAchieved:\n            type: string\n            format: date-time\n            description: Achievement timestamp\n    UserCreatedPayload:\n      allOf:\n      - $ref: '#/components/schemas/WebhookEventBase'\n      - type: object\n\
  \        properties:\n          eventType:\n            const: USER_CREATED\n          user:\n            type: object\n            properties:\n              userId:\n                type: string\n                description: User identifier\n              name:\n                type: string\n                description: User's full name\n              email:\n                type: string\n                format: email\n                description: User's email address\n              roles:\n                type: array\n                items:\n                  type: string\n              userType:\n                type: string\n                enum:\n                - Internal\n                - External\n          creationMethod:\n            type: string\n            description: How the user was created\n            enum:\n            - selfRegistration\n            - adminCreated\n            - csvImport\n            - apiCreated\n            - ssoProvisioned\n    UserUpdatedPayload:\n\
  \      allOf:\n      - $ref: '#/components/schemas/WebhookEventBase'\n      - type: object\n        properties:\n          eventType:\n            const: USER_UPDATED\n          user:\n            type: object\n            properties:\n              userId:\n                type: string\n                description: User identifier\n              name:\n                type: string\n                description: User's full name\n              email:\n                type: string\n                format: email\n          updatedFields:\n            type: array\n            description: Fields that were modified\n            items:\n              type: string\n    UserDeletedPayload:\n      allOf:\n      - $ref: '#/components/schemas/WebhookEventBase'\n      - type: object\n        properties:\n          eventType:\n            const: USER_DELETED\n          user:\n            type: object\n            properties:\n              userId:\n                type: string\n                description:\
  \ Deleted user identifier\n              email:\n                type: string\n                format: email\n          dateDeleted:\n            type: string\n            format: date-time\n            description: Deletion timestamp\n    JobCompletedPayload:\n      allOf:\n      - $ref: '#/components/schemas/WebhookEventBase'\n      - type: object\n        properties:\n          eventType:\n            const: JOB_COMPLETED\n          job:\n            type: object\n            properties:\n              jobId:\n                type: string\n                description: Job identifier\n              jobType:\n                type: string\n                description: Type of bulk operation\n                enum:\n                - userImport\n                - learnerTranscriptExport\n                - trainingReportExport\n              status:\n                type: string\n                description: Final job status\n                enum:\n                - Completed\n          \
  \      - Failed\n              downloadUrl:\n                type: string\n                format: uri\n                description: URL to download results (for export jobs)\n              recordsProcessed:\n                type: integer\n                description: Number of records processed\n              recordsFailed:\n                type: integer\n                description: Number of records that failed\n          dateCompleted:\n            type: string\n            format: date-time\n            description: Job completion timestamp\n  messages:\n    LearnerEnrollmentEvent:\n      name: LearnerEnrollmentEvent\n      title: Learner Enrollment Event\n      summary: Notification when a learner enrolls in a learning object\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/LearnerEnrollmentPayload'\n      examples:\n      - name: LearnerEnrollmentEventDefaultExample\n        summary: Default LearnerEnrollmentEvent example payload\n      \
  \  x-microcks-default: true\n        payload: {}\n    LearnerCompletionEvent:\n      name: LearnerCompletionEvent\n      title: Learner Completion Event\n      summary: Notification when a learner completes a learning object\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/LearnerCompletionPayload'\n      examples:\n      - name: LearnerCompletionEventDefaultExample\n        summary: Default LearnerCompletionEvent example payload\n        x-microcks-default: true\n        payload: {}\n    LearnerProgressEvent:\n      name: LearnerProgressEvent\n      title: Learner Progress Event\n      summary: Notification when learner progress is updated\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/LearnerProgressPayload'\n      examples:\n      - name: LearnerProgressEventDefaultExample\n        summary: Default LearnerProgressEvent example payload\n        x-microcks-default: true\n        payload: {}\n    LearnerUnenrollmentEvent:\n\
  \      name: LearnerUnenrollmentEvent\n      title: Learner Unenrollment Event\n      summary: Notification when a learner is unenrolled\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/LearnerUnenrollmentPayload'\n      examples:\n      - name: LearnerUnenrollmentEventDefaultExample\n        summary: Default LearnerUnenrollmentEvent example payload\n        x-microcks-default: true\n        payload: {}\n    CourseCreatedEvent:\n      name: CourseCreatedEvent\n      title: Course Created Event\n      summary: Notification when a new course is created\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CourseCreatedPayload'\n      examples:\n      - name: CourseCreatedEventDefaultExample\n        summary: Default CourseCreatedEvent example payload\n        x-microcks-default: true\n        payload: {}\n    CourseUpdatedEvent:\n      name: CourseUpdatedEvent\n      title: Course Updated Event\n      summary: Notification\
  \ when a course is updated\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/CourseUpdatedPayload'\n      examples:\n      - name: CourseUpdatedEventDefaultExample\n        summary: Default CourseUpdatedEvent example payload\n        x-microcks-default: true\n        payload: {}\n    BadgeAwardedEvent:\n      name: BadgeAwardedEvent\n      title: Badge Awarded Event\n      summary: Notification when a badge is awarded to a learner\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BadgeAwardedPayload'\n      examples:\n      - name: BadgeAwardedEventDefaultExample\n        summary: Default BadgeAwardedEvent example payload\n        x-microcks-default: true\n        payload: {}\n    CertificationCompletedEvent:\n      name: CertificationCompletedEvent\n      title: Certification Completed Event\n      summary: Notification when a learner completes a certification\n      contentType: application/json\n      payload:\n\
  \        $ref: '#/components/schemas/CertificationCompletedPayload'\n      examples:\n      - name: CertificationCompletedEventDefaultExample\n        summary: Default CertificationCompletedEvent example payload\n        x-microcks-default: true\n        payload: {}\n    SkillAchievedEvent:\n      name: SkillAchievedEvent\n      title: Skill Achieved Event\n      summary: Notification when a learner achieves a new skill level\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/SkillAchievedPayload'\n      examples:\n      - name: SkillAchievedEventDefaultExample\n        summary: Default SkillAchievedEvent example payload\n        x-microcks-default: true\n        payload: {}\n    UserCreatedEvent:\n      name: UserCreatedEvent\n      title: User Created Event\n      summary: Notification when a new user is created\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/UserCreatedPayload'\n      examples:\n      -\
  \ name: UserCreatedEventDefaultExample\n        summary: Default UserCreatedEvent example payload\n        x-microcks-default: true\n        payload: {}\n    UserUpdatedEvent:\n      name: UserUpdatedEvent\n      title: User Updated Event\n      summary: Notification when a user is updated\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/UserUpdatedPayload'\n      examples:\n      - name: UserUpdatedEventDefaultExample\n        summary: Default UserUpdatedEvent example payload\n        x-microcks-default: true\n        payload: {}\n    UserDeletedEvent:\n      name: UserDeletedEvent\n      title: User Deleted Event\n      summary: Notification when a user is deleted\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/UserDeletedPayload'\n      examples:\n      - name: UserDeletedEventDefaultExample\n        summary: Default UserDeletedEvent example payload\n        x-microcks-default: true\n        payload:\
  \ {}\n    JobCompletedEvent:\n      name: JobCompletedEvent\n      title: Job Completed Event\n      summary: Notification when a bulk job completes\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/JobCompletedPayload'\n      examples:\n      - name: JobCompletedEventDefaultExample\n        summary: Default JobCompletedEvent example payload\n        x-microcks-default: true\n        payload: {}\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/adobe-captivate/refs/heads/main/asyncapi/adobe-captivate-learning-manager-webhooks-asyncapi.yml
spec_file: asyncapi/adobe-captivate-learning-manager-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/adobe-captivate/refs/heads/main/asyncapi/adobe-captivate-learning-manager-webhooks-asyncapi.yml
tags:
- Authoring
- Education
- eLearning
- LMS
- SCORM
- Training
- xAPI
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
