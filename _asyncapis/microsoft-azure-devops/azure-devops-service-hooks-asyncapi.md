---
api_specs:
- filename: openapi.yaml
  format: yaml
  label: Azure DevOps Services REST API
  slug: ''
  spec_type: OpenAPI
  url: https://learn.microsoft.com/en-us/rest/api/azure/devops/
- filename: azure-devops-work-items-api-openapi.yml
  format: yaml
  label: Azure DevOps Boards API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/microsoft-azure-devops/refs/heads/main/openapi/azure-devops-work-items-api-openapi.yml
- filename: azure-devops-git-api-openapi.yml
  format: yaml
  label: Azure DevOps Repos API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/microsoft-azure-devops/refs/heads/main/openapi/azure-devops-git-api-openapi.yml
- filename: azure-devops-pipelines-api-openapi.yml
  format: yaml
  label: Azure DevOps Pipelines API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/microsoft-azure-devops/refs/heads/main/openapi/azure-devops-pipelines-api-openapi.yml
- filename: azure-devops-builds-api-openapi.yml
  format: yaml
  label: Azure DevOps Build API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/microsoft-azure-devops/refs/heads/main/openapi/azure-devops-builds-api-openapi.yml
- filename: azure-devops-releases-api-openapi.yml
  format: yaml
  label: Azure DevOps Release API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/microsoft-azure-devops/refs/heads/main/openapi/azure-devops-releases-api-openapi.yml
- filename: azure-devops-test-plans-api-openapi.yml
  format: yaml
  label: Azure DevOps Test Plans API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/microsoft-azure-devops/refs/heads/main/openapi/azure-devops-test-plans-api-openapi.yml
- filename: azure-devops-artifacts-api-openapi.yml
  format: yaml
  label: Azure DevOps Artifacts API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/microsoft-azure-devops/refs/heads/main/openapi/azure-devops-artifacts-api-openapi.yml
- filename: azure-devops-service-hooks-api-openapi.yml
  format: yaml
  label: Azure DevOps Service Hooks API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/microsoft-azure-devops/refs/heads/main/openapi/azure-devops-service-hooks-api-openapi.yml
- filename: azure-devops-wiki-api-openapi.yml
  format: yaml
  label: Azure DevOps Wiki API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/microsoft-azure-devops/refs/heads/main/openapi/azure-devops-wiki-api-openapi.yml
channels:
- description: Triggered when a new work item is created in Azure Boards. The resource in the payload contains the full work item with all its fields.
  name: workitem/created
  operation: subscribe
  operation_id: onWorkItemCreated
  summary: Receive work item created events
- description: Triggered when any field of a work item is updated, including state changes, assignment changes, field value updates, and relation additions or removals.
  name: workitem/updated
  operation: subscribe
  operation_id: onWorkItemUpdated
  summary: Receive work item updated events
- description: Triggered when a work item is deleted (moved to the recycle bin or permanently deleted). The payload contains the work item as it was before deletion.
  name: workitem/deleted
  operation: subscribe
  operation_id: onWorkItemDeleted
  summary: Receive work item deleted events
- description: Triggered when a comment is added to a work item. The payload contains the work item and the new comment.
  name: workitem/commented
  operation: subscribe
  operation_id: onWorkItemCommented
  summary: Receive work item commented events
- description: Triggered when one or more commits are pushed to a Git repository branch. The payload includes the repository, branch, and list of commits pushed.
  name: git/push
  operation: subscribe
  operation_id: onGitPush
  summary: Receive git push events
- description: Triggered when a new pull request is created in a Git repository. The payload contains the full pull request details including source and target branches, title, description, and assigned reviewers.
  name: git/pullrequest/created
  operation: subscribe
  operation_id: onPullRequestCreated
  summary: Receive pull request created events
- description: Triggered when an existing pull request is updated, such as when reviewers are added, the PR is approved, the merge status changes, or the title or description is modified.
  name: git/pullrequest/updated
  operation: subscribe
  operation_id: onPullRequestUpdated
  summary: Receive pull request updated events
- description: Triggered when a pull request is merged (completed) into the target branch. The payload includes the merge commit and the completed pull request details.
  name: git/pullrequest/merged
  operation: subscribe
  operation_id: onPullRequestMerged
  summary: Receive pull request merged events
- description: Triggered when a build completes (succeeds, fails, is canceled, or partially succeeds). The payload includes the build details, result, and links to logs and artifacts.
  name: build/complete
  operation: subscribe
  operation_id: onBuildComplete
  summary: Receive build completed events
- description: Triggered when a new release is created from a release definition. The payload includes the release details, artifacts, and environments.
  name: ms.vss-release.release-created-event
  operation: subscribe
  operation_id: onReleaseCreated
  summary: Receive release created events
- description: Triggered when a deployment to an environment requires manual approval. The payload includes the release, environment, and approval request details.
  name: ms.vss-release.deployment-approval-pending-event
  operation: subscribe
  operation_id: onDeploymentApprovalPending
  summary: Receive deployment approval pending events
- description: Triggered when a deployment to an environment is completed, regardless of whether it succeeded or failed. The payload includes the release, environment, deployment result, and timing information.
  name: ms.vss-release.deployment-completed-event
  operation: subscribe
  operation_id: onDeploymentCompleted
  summary: Receive deployment completed events
description: AsyncAPI specification for Azure DevOps Service Hooks (webhooks and event subscriptions). Azure DevOps delivers event notifications via HTTP POST requests to subscriber endpoints when events occur such as work item changes, git pushes, pull request updates, build completions, and release deployments. Subscribers configure webhooks through the Service Hooks REST API or the Azure DevOps portal. Each subscription specifies the event type, optional filter conditions, and the target consumer endpoint. Azure DevOps signs each delivery with an HMAC-SHA1 signature in the X-AzureDevOps-Signature header, allowing subscribers to verify message authenticity.
layout: asyncapi
messages:
- description: ''
  name: WorkItemCreatedEvent
  summary: A new work item was created in Azure Boards
  title: Work item created
- description: ''
  name: WorkItemUpdatedEvent
  summary: A work item was updated in Azure Boards
  title: Work item updated
- description: ''
  name: WorkItemDeletedEvent
  summary: A work item was deleted from Azure Boards
  title: Work item deleted
- description: ''
  name: WorkItemCommentedEvent
  summary: A comment was added to a work item
  title: Work item comment added
- description: ''
  name: GitPushEvent
  summary: Commits were pushed to a Git repository
  title: Git push
- description: ''
  name: PullRequestCreatedEvent
  summary: A new pull request was opened
  title: Pull request created
- description: ''
  name: PullRequestUpdatedEvent
  summary: A pull request was updated (reviewer added, approved, etc.)
  title: Pull request updated
- description: ''
  name: PullRequestMergedEvent
  summary: A pull request was completed and merged
  title: Pull request merged
- description: ''
  name: BuildCompleteEvent
  summary: A build finished executing
  title: Build complete
- description: ''
  name: ReleaseCreatedEvent
  summary: A new release was created from a release definition
  title: Release created
- description: ''
  name: DeploymentApprovalPendingEvent
  summary: A deployment is waiting for manual approval
  title: Deployment approval pending
- description: ''
  name: DeploymentCompletedEvent
  summary: A deployment to an environment finished executing
  title: Deployment completed
name: Azure DevOps Service Hooks AsyncAPI
provider_name: Azure DevOps
provider_slug: microsoft-azure-devops
servers:
- description: 'The HTTPS endpoint configured by the webhook subscriber to receive event notifications. This URL is specified when creating a service hook subscription via the Azure DevOps Service Hooks API (POST /hooks/subscriptions with consumerId: ''webHooks'' and consumerActionId: ''httpRequest'').'
  name: subscriber-endpoint
  protocol: https
  url: '{subscriberUrl}'
slug: azure-devops-service-hooks-asyncapi
source_filename: azure-devops-service-hooks-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Azure DevOps Service Hooks AsyncAPI\n  version: '7.1'\n  description: >\n    AsyncAPI specification for Azure DevOps Service Hooks (webhooks and event subscriptions).\n    Azure DevOps delivers event notifications via HTTP POST requests to subscriber endpoints\n    when events occur such as work item changes, git pushes, pull request updates, build\n    completions, and release deployments.\n\n    Subscribers configure webhooks through the Service Hooks REST API or the Azure DevOps\n    portal. Each subscription specifies the event type, optional filter conditions, and the\n    target consumer endpoint.\n\n    Azure DevOps signs each delivery with an HMAC-SHA1 signature in the\n    X-AzureDevOps-Signature header, allowing subscribers to verify message authenticity.\n  contact:\n    name: Microsoft Azure DevOps\n    url: https://learn.microsoft.com/en-us/azure/devops/service-hooks/overview?view=azure-devops\n  license:\n    name: MIT\n    url:\
  \ https://opensource.org/licenses/MIT\n  x-publisher:\n    name: Azure DevOps\n    id: tfs\n    description: >\n      The primary Azure DevOps event publisher. All events described in this spec\n      are produced by the 'tfs' publisher.\n\ndefaultContentType: application/json\n\nservers:\n  subscriber-endpoint:\n    url: '{subscriberUrl}'\n    protocol: https\n    description: >\n      The HTTPS endpoint configured by the webhook subscriber to receive event\n      notifications. This URL is specified when creating a service hook subscription\n      via the Azure DevOps Service Hooks API (POST /hooks/subscriptions with\n      consumerId: 'webHooks' and consumerActionId: 'httpRequest').\n    variables:\n      subscriberUrl:\n        description: The full HTTPS URL of the subscriber endpoint\n\nchannels:\n  workitem/created:\n    description: >\n      Triggered when a new work item is created in Azure Boards. The resource\n      in the payload contains the full work item with all its fields.\n\
  \    subscribe:\n      operationId: onWorkItemCreated\n      summary: Receive work item created events\n      description: >\n        Subscribe to this channel to receive notifications whenever a new work item\n        is created in any project (or in a specific project and area path based on\n        subscription filters). The event payload includes the complete work item.\n      tags:\n        - name: Work Items\n        - name: Azure Boards\n      bindings:\n        http:\n          method: POST\n      message:\n        $ref: '#/components/messages/WorkItemCreatedEvent'\n\n  workitem/updated:\n    description: >\n      Triggered when any field of a work item is updated, including state changes,\n      assignment changes, field value updates, and relation additions or removals.\n    subscribe:\n      operationId: onWorkItemUpdated\n      summary: Receive work item updated events\n      description: >\n        Subscribe to receive notifications when work items are modified. The payload\n\
  \        includes both the updated work item and details of what changed. Filter by\n        specific field changes using the subscription's publisherInputs.\n      tags:\n        - name: Work Items\n        - name: Azure Boards\n      bindings:\n        http:\n          method: POST\n      message:\n        $ref: '#/components/messages/WorkItemUpdatedEvent'\n\n  workitem/deleted:\n    description: >\n      Triggered when a work item is deleted (moved to the recycle bin or permanently\n      deleted). The payload contains the work item as it was before deletion.\n    subscribe:\n      operationId: onWorkItemDeleted\n      summary: Receive work item deleted events\n      description: >\n        Subscribe to receive notifications when work items are deleted. Useful for\n        maintaining external systems in sync with Azure Boards.\n      tags:\n        - name: Work Items\n        - name: Azure Boards\n      bindings:\n        http:\n          method: POST\n      message:\n        $ref:\
  \ '#/components/messages/WorkItemDeletedEvent'\n\n  workitem/commented:\n    description: >\n      Triggered when a comment is added to a work item. The payload contains the\n      work item and the new comment.\n    subscribe:\n      operationId: onWorkItemCommented\n      summary: Receive work item commented events\n      description: >\n        Subscribe to receive notifications when comments are added to work items.\n        Useful for triggering notifications or integrations based on team discussions.\n      tags:\n        - name: Work Items\n        - name: Azure Boards\n      bindings:\n        http:\n          method: POST\n      message:\n        $ref: '#/components/messages/WorkItemCommentedEvent'\n\n  git/push:\n    description: >\n      Triggered when one or more commits are pushed to a Git repository branch.\n      The payload includes the repository, branch, and list of commits pushed.\n    subscribe:\n      operationId: onGitPush\n      summary: Receive git push events\n\
  \      description: >\n        Subscribe to receive notifications when code is pushed to a repository.\n        Can be filtered to specific repositories or branches via subscription\n        publisherInputs. Useful for triggering CI processes or code reviews.\n      tags:\n        - name: Git\n        - name: Azure Repos\n      bindings:\n        http:\n          method: POST\n      message:\n        $ref: '#/components/messages/GitPushEvent'\n\n  git/pullrequest/created:\n    description: >\n      Triggered when a new pull request is created in a Git repository. The payload\n      contains the full pull request details including source and target branches,\n      title, description, and assigned reviewers.\n    subscribe:\n      operationId: onPullRequestCreated\n      summary: Receive pull request created events\n      description: >\n        Subscribe to receive notifications when new pull requests are opened.\n        Useful for triggering automated code review processes, notifications,\n\
  \        or external workflow systems.\n      tags:\n        - name: Git\n        - name: Pull Requests\n        - name: Azure Repos\n      bindings:\n        http:\n          method: POST\n      message:\n        $ref: '#/components/messages/PullRequestCreatedEvent'\n\n  git/pullrequest/updated:\n    description: >\n      Triggered when an existing pull request is updated, such as when reviewers\n      are added, the PR is approved, the merge status changes, or the title or\n      description is modified.\n    subscribe:\n      operationId: onPullRequestUpdated\n      summary: Receive pull request updated events\n      description: >\n        Subscribe to receive notifications on pull request changes. The payload\n        includes the updated pull request with the most recent status and reviewer votes.\n      tags:\n        - name: Git\n        - name: Pull Requests\n        - name: Azure Repos\n      bindings:\n        http:\n          method: POST\n      message:\n        $ref: '#/components/messages/PullRequestUpdatedEvent'\n\
  \n  git/pullrequest/merged:\n    description: >\n      Triggered when a pull request is merged (completed) into the target branch.\n      The payload includes the merge commit and the completed pull request details.\n    subscribe:\n      operationId: onPullRequestMerged\n      summary: Receive pull request merged events\n      description: >\n        Subscribe to receive notifications when pull requests are completed and\n        merged into the target branch. Useful for triggering deployment workflows\n        or updating external project tracking systems.\n      tags:\n        - name: Git\n        - name: Pull Requests\n        - name: Azure Repos\n      bindings:\n        http:\n          method: POST\n      message:\n        $ref: '#/components/messages/PullRequestMergedEvent'\n\n  build/complete:\n    description: >\n      Triggered when a build completes (succeeds, fails, is canceled, or partially\n      succeeds). The payload includes the build details, result, and links to logs\n\
  \      and artifacts.\n    subscribe:\n      operationId: onBuildComplete\n      summary: Receive build completed events\n      description: >\n        Subscribe to receive notifications when builds finish executing. Can be\n        filtered by definition ID and build status. Useful for triggering downstream\n        deployments or notifying teams about build results.\n      tags:\n        - name: Builds\n        - name: Azure Pipelines\n      bindings:\n        http:\n          method: POST\n      message:\n        $ref: '#/components/messages/BuildCompleteEvent'\n\n  ms.vss-release.release-created-event:\n    description: >\n      Triggered when a new release is created from a release definition. The payload\n      includes the release details, artifacts, and environments.\n    subscribe:\n      operationId: onReleaseCreated\n      summary: Receive release created events\n      description: >\n        Subscribe to receive notifications when releases are created. Useful for\n        triggering\
  \ external workflow systems or sending release announcements.\n      tags:\n        - name: Releases\n        - name: Azure Pipelines\n      bindings:\n        http:\n          method: POST\n      message:\n        $ref: '#/components/messages/ReleaseCreatedEvent'\n\n  ms.vss-release.deployment-approval-pending-event:\n    description: >\n      Triggered when a deployment to an environment requires manual approval.\n      The payload includes the release, environment, and approval request details.\n    subscribe:\n      operationId: onDeploymentApprovalPending\n      summary: Receive deployment approval pending events\n      description: >\n        Subscribe to receive notifications when deployments are waiting for manual\n        approval before proceeding. Useful for notifying approvers through external\n        channels or triggering approval workflow integrations.\n      tags:\n        - name: Releases\n        - name: Deployments\n        - name: Azure Pipelines\n      bindings:\n\
  \        http:\n          method: POST\n      message:\n        $ref: '#/components/messages/DeploymentApprovalPendingEvent'\n\n  ms.vss-release.deployment-completed-event:\n    description: >\n      Triggered when a deployment to an environment is completed, regardless of\n      whether it succeeded or failed. The payload includes the release, environment,\n      deployment result, and timing information.\n    subscribe:\n      operationId: onDeploymentCompleted\n      summary: Receive deployment completed events\n      description: >\n        Subscribe to receive notifications when deployments finish. Useful for\n        auditing deployment activity, updating external dashboards, or triggering\n        post-deployment testing workflows.\n      tags:\n        - name: Releases\n        - name: Deployments\n        - name: Azure Pipelines\n      bindings:\n        http:\n          method: POST\n      message:\n        $ref: '#/components/messages/DeploymentCompletedEvent'\n\ncomponents:\n\
  \  messages:\n    WorkItemCreatedEvent:\n      name: WorkItemCreatedEvent\n      title: Work item created\n      summary: A new work item was created in Azure Boards\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-AzureDevOps-Signature:\n            type: string\n            description: >\n              HMAC-SHA1 signature of the request body using the subscription's\n              shared secret. Format: sha1={signature}\n            example: 'sha1=7a3f9b2c4d5e6f8a9b0c1d2e3f4a5b6c7d8e9f0a'\n          Content-Type:\n            type: string\n            enum: ['application/json']\n      payload:\n        $ref: '#/components/schemas/ServiceHookEventEnvelope'\n      examples:\n        - name: BasicWorkItemCreated\n          summary: Example of a work item created event payload\n          payload:\n            subscriptionId: 'c0cc6f6a-b2b3-4c4e-b1b0-2c5d7e6f8a9b'\n            notificationId: 1\n            id: 'a1b2c3d4-e5f6-a1b2-c3d4-e5f6a1b2c3d4'\n\
  \            eventType: 'workitem.created'\n            publisherId: 'tfs'\n            message:\n              text: 'Bug #42 (Fix login alignment) created by John Doe'\n              html: '<a href=\"https://dev.azure.com/myorg/myproject/_workitems/edit/42\">Bug #42</a> (Fix login alignment) created by John Doe'\n              markdown: '[Bug #42](https://dev.azure.com/myorg/myproject/_workitems/edit/42) (Fix login alignment) created by John Doe'\n            detailedMessage:\n              text: 'Bug #42 (Fix login alignment) created by John Doe in Sprint 5'\n              html: '<a href=\"https://dev.azure.com/myorg/myproject/_workitems/edit/42\">Bug #42</a> (Fix login alignment) created by John Doe in Sprint 5'\n              markdown: '[Bug #42](https://dev.azure.com/myorg/myproject/_workitems/edit/42) (Fix login alignment) created by John Doe in Sprint 5'\n            resource:\n              id: 42\n              rev: 1\n              fields:\n                System.Id: 42\n  \
  \              System.Title: 'Fix login alignment'\n                System.WorkItemType: 'Bug'\n                System.State: 'New'\n                System.CreatedBy:\n                  displayName: 'John Doe'\n                  uniqueName: 'john.doe@example.com'\n                System.CreatedDate: '2024-03-15T10:30:00Z'\n                System.TeamProject: 'myproject'\n                System.AreaPath: 'myproject'\n                System.IterationPath: 'myproject\\\\Sprint 5'\n              url: 'https://dev.azure.com/myorg/myproject/_apis/wit/workItems/42'\n              _links:\n                self:\n                  href: 'https://dev.azure.com/myorg/myproject/_apis/wit/workItems/42'\n            resourceVersion: '1.0'\n            resourceContainers:\n              collection:\n                id: 'myorg-collection-id'\n                baseUrl: 'https://dev.azure.com/myorg'\n              account:\n                id: 'myorg-account-id'\n                baseUrl: 'https://dev.azure.com/myorg'\n\
  \              project:\n                id: 'a1b2c3d4-e5f6-a1b2-c3d4-e5f6a1b2c3d4'\n                baseUrl: 'https://dev.azure.com/myorg/myproject'\n            createdDate: '2024-03-15T10:30:00Z'\n\n    WorkItemUpdatedEvent:\n      name: WorkItemUpdatedEvent\n      title: Work item updated\n      summary: A work item was updated in Azure Boards\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-AzureDevOps-Signature:\n            type: string\n            description: HMAC-SHA1 signature of the request body\n      payload:\n        $ref: '#/components/schemas/ServiceHookEventEnvelope'\n\n    WorkItemDeletedEvent:\n      name: WorkItemDeletedEvent\n      title: Work item deleted\n      summary: A work item was deleted from Azure Boards\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-AzureDevOps-Signature:\n            type: string\n            description: HMAC-SHA1\
  \ signature of the request body\n      payload:\n        $ref: '#/components/schemas/ServiceHookEventEnvelope'\n\n    WorkItemCommentedEvent:\n      name: WorkItemCommentedEvent\n      title: Work item comment added\n      summary: A comment was added to a work item\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-AzureDevOps-Signature:\n            type: string\n            description: HMAC-SHA1 signature of the request body\n      payload:\n        $ref: '#/components/schemas/ServiceHookEventEnvelope'\n\n    GitPushEvent:\n      name: GitPushEvent\n      title: Git push\n      summary: Commits were pushed to a Git repository\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-AzureDevOps-Signature:\n            type: string\n            description: HMAC-SHA1 signature of the request body\n      payload:\n        $ref: '#/components/schemas/ServiceHookEventEnvelope'\n\
  \      examples:\n        - name: BasicGitPush\n          summary: Example of a git push event payload\n          payload:\n            subscriptionId: 'd1e2f3a4-b5c6-d7e8-f9a0-b1c2d3e4f5a6'\n            notificationId: 2\n            id: 'b2c3d4e5-f6a1-b2c3-d4e5-f6a1b2c3d4e5'\n            eventType: 'git.push'\n            publisherId: 'tfs'\n            message:\n              text: 'John Doe pushed to main in myproject/my-application'\n              html: 'John Doe pushed to <a href=\"https://dev.azure.com/myorg/myproject/_git/my-application/commits?itemVersion=GBmain\">main</a> in <a href=\"https://dev.azure.com/myorg/myproject/_git/my-application\">myproject/my-application</a>'\n              markdown: 'John Doe pushed to [main](https://dev.azure.com/myorg/myproject/_git/my-application) in [my-application](https://dev.azure.com/myorg/myproject/_git/my-application)'\n            resource:\n              commits:\n                - commitId: 'a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2'\n\
  \                  author:\n                    name: 'John Doe'\n                    email: 'john.doe@example.com'\n                    date: '2024-03-15T10:30:00Z'\n                  committer:\n                    name: 'John Doe'\n                    email: 'john.doe@example.com'\n                    date: '2024-03-15T10:30:00Z'\n                  comment: 'Fix login button alignment'\n                  url: 'https://dev.azure.com/myorg/myproject/_git/my-application/commit/a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2'\n              refUpdates:\n                - name: 'refs/heads/main'\n                  oldObjectId: '0000000000000000000000000000000000000000'\n                  newObjectId: 'a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2'\n              repository:\n                id: 'repo-guid-here'\n                name: 'my-application'\n                url: 'https://dev.azure.com/myorg/myproject/_git/my-application'\n                project:\n                  id: 'proj-guid-here'\n \
  \                 name: 'myproject'\n              pushedBy:\n                displayName: 'John Doe'\n                uniqueName: 'john.doe@example.com'\n              pushId: 12345\n              date: '2024-03-15T10:30:00Z'\n              url: 'https://dev.azure.com/myorg/myproject/_git/my-application/pushes/12345'\n            resourceVersion: '1.0'\n            resourceContainers:\n              collection:\n                id: 'collection-id'\n                baseUrl: 'https://dev.azure.com/myorg'\n              account:\n                id: 'account-id'\n                baseUrl: 'https://dev.azure.com/myorg'\n              project:\n                id: 'proj-guid-here'\n                baseUrl: 'https://dev.azure.com/myorg/myproject'\n            createdDate: '2024-03-15T10:30:01Z'\n\n    PullRequestCreatedEvent:\n      name: PullRequestCreatedEvent\n      title: Pull request created\n      summary: A new pull request was opened\n      contentType: application/json\n      headers:\n\
  \        type: object\n        properties:\n          X-AzureDevOps-Signature:\n            type: string\n            description: HMAC-SHA1 signature of the request body\n      payload:\n        $ref: '#/components/schemas/ServiceHookEventEnvelope'\n\n    PullRequestUpdatedEvent:\n      name: PullRequestUpdatedEvent\n      title: Pull request updated\n      summary: A pull request was updated (reviewer added, approved, etc.)\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-AzureDevOps-Signature:\n            type: string\n            description: HMAC-SHA1 signature of the request body\n      payload:\n        $ref: '#/components/schemas/ServiceHookEventEnvelope'\n\n    PullRequestMergedEvent:\n      name: PullRequestMergedEvent\n      title: Pull request merged\n      summary: A pull request was completed and merged\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-AzureDevOps-Signature:\n\
  \            type: string\n            description: HMAC-SHA1 signature of the request body\n      payload:\n        $ref: '#/components/schemas/ServiceHookEventEnvelope'\n\n    BuildCompleteEvent:\n      name: BuildCompleteEvent\n      title: Build complete\n      summary: A build finished executing\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-AzureDevOps-Signature:\n            type: string\n            description: HMAC-SHA1 signature of the request body\n      payload:\n        $ref: '#/components/schemas/ServiceHookEventEnvelope'\n      examples:\n        - name: BuildSucceeded\n          summary: Example of a build complete event payload (succeeded)\n          payload:\n            subscriptionId: 'e3f4a5b6-c7d8-e9f0-a1b2-c3d4e5f6a7b8'\n            notificationId: 5\n            id: 'c4d5e6f7-a8b9-c0d1-e2f3-a4b5c6d7e8f9'\n            eventType: 'build.complete'\n            publisherId: 'tfs'\n            message:\n\
  \              text: 'Build CI-Pipeline 20240315.1 succeeded'\n              html: 'Build <a href=\"https://dev.azure.com/myorg/myproject/_build/results?buildId=1234\">CI-Pipeline 20240315.1</a> succeeded'\n              markdown: 'Build [CI-Pipeline 20240315.1](https://dev.azure.com/myorg/myproject/_build/results?buildId=1234) succeeded'\n            resource:\n              id: 1234\n              buildNumber: '20240315.1'\n              status: 'completed'\n              result: 'succeeded'\n              queueTime: '2024-03-15T10:00:00Z'\n              startTime: '2024-03-15T10:01:00Z'\n              finishTime: '2024-03-15T10:15:00Z'\n              url: 'https://dev.azure.com/myorg/myproject/_apis/build/Builds/1234'\n              definition:\n                id: 5\n                name: 'CI-Pipeline'\n                url: 'https://dev.azure.com/myorg/myproject/_apis/build/Definitions/5'\n              sourceBranch: 'refs/heads/main'\n              sourceVersion: 'a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2'\n\
  \              requestedBy:\n                displayName: 'John Doe'\n                uniqueName: 'john.doe@example.com'\n              project:\n                id: 'proj-guid-here'\n                name: 'myproject'\n            resourceVersion: '1.0'\n            resourceContainers:\n              collection:\n                id: 'collection-id'\n                baseUrl: 'https://dev.azure.com/myorg'\n              account:\n                id: 'account-id'\n                baseUrl: 'https://dev.azure.com/myorg'\n              project:\n                id: 'proj-guid-here'\n                baseUrl: 'https://dev.azure.com/myorg/myproject'\n            createdDate: '2024-03-15T10:15:01Z'\n\n    ReleaseCreatedEvent:\n      name: ReleaseCreatedEvent\n      title: Release created\n      summary: A new release was created from a release definition\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-AzureDevOps-Signature:\n         \
  \   type: string\n            description: HMAC-SHA1 signature of the request body\n      payload:\n        $ref: '#/components/schemas/ServiceHookEventEnvelope'\n\n    DeploymentApprovalPendingEvent:\n      name: DeploymentApprovalPendingEvent\n      title: Deployment approval pending\n      summary: A deployment is waiting for manual approval\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-AzureDevOps-Signature:\n            type: string\n            description: HMAC-SHA1 signature of the request body\n      payload:\n        $ref: '#/components/schemas/ServiceHookEventEnvelope'\n\n    DeploymentCompletedEvent:\n      name: DeploymentCompletedEvent\n      title: Deployment completed\n      summary: A deployment to an environment finished executing\n      contentType: application/json\n      headers:\n        type: object\n        properties:\n          X-AzureDevOps-Signature:\n            type: string\n            description:\
  \ HMAC-SHA1 signature of the request body\n      payload:\n        $ref: '#/components/schemas/ServiceHookEventEnvelope'\n\n  schemas:\n    ServiceHookEventEnvelope:\n      type: object\n      description: >\n        The standard envelope for all Azure DevOps Service Hook event notifications.\n        Delivered via HTTP POST to the configured subscriber endpoint.\n      required:\n        - subscriptionId\n        - notificationId\n        - id\n        - eventType\n        - publisherId\n        - resource\n        - resourceVersion\n        - resourceContainers\n        - createdDate\n      properties:\n        subscriptionId:\n          type: string\n          format: uuid\n          description: GUID of the service hook subscription that triggered this notification\n          example: 'c0cc6f6a-b2b3-4c4e-b1b0-2c5d7e6f8a9b'\n        notificationId:\n          type: integer\n          description: Sequential notification ID within the subscription\n          example: 42\n        id:\n\
  \          type: string\n          format: uuid\n          description: Unique GUID identifier for this specific notification event instance\n          example: 'a1b2c3d4-e5f6-a1b2-c3d4-e5f6a1b2c3d4'\n        eventType:\n          type: string\n          description: >\n            The type of event that triggered this notification. Identifies the\n            channel/event category.\n          enum:\n            - workitem.created\n            - workitem.updated\n            - workitem.deleted\n            - workitem.commented\n            - git.push\n            - git.pullrequest.created\n            - git.pullrequest.updated\n            - git.pullrequest.merged\n            - build.complete\n            - ms.vss-release.release-created-event\n            - ms.vss-release.deployment-approval-pending-event\n            - ms.vss-release.deployment-completed-event\n          example: 'workitem.created'\n        publisherId:\n          type: string\n          description: Identifier of\
  \ the publisher that produced this event\n          example: 'tfs'\n        message:\n          $ref: '#/components/schemas/FormattedEventMessage'\n        detailedMessage:\n          $ref: '#/components/schemas/FormattedEventMessage'\n        resource:\n          type: object\n          description: >\n            The primary resource affected by the event. The schema of this object\n            varies by eventType:\n            - Work item events: contains the work item fields (id, rev, fields, relations)\n            - Git push: contains commits, refUpdates, repository, pushedBy\n            - Pull request events: contains the full pull request object\n            - Build events: contains the build object (id, buildNumber, status, result)\n            - Release events: contains the release or deployment object\n          additionalProperties: true\n        resourceVersion:\n          type: string\n          description: Version of the resource schema used in this event payload\n   \
  \       example: '1.0'\n        resourceContainers:\n          $ref: '#/components/schemas/ResourceContainers'\n        createdDate:\n          type: string\n          format: date-time\n          description: Date and time the event was created (ISO 8601 UTC)\n          example: '2024-03-15T10:30:00Z'\n\n    FormattedEventMessage:\n      type: object\n      description: An event message rendered in multiple formats for different use cases\n      properties:\n        text:\n          type: string\n          description: Plain text version of the event message\n          example: 'Bug #42 (Fix login alignment) created by John Doe'\n        html:\n          type: string\n          description: HTML version with hyperlinks to relevant Azure DevOps resources\n          example: '<a href=\"https://dev.azure.com/myorg/myproject/_workitems/edit/42\">Bug #42</a> (Fix login alignment) created by John Doe'\n        markdown:\n          type: string\n          description: Markdown version of the\
  \ event message with links\n          example: '[Bug #42](https://dev.azure.com/myorg/myproject/_workitems/edit/42) (Fix login alignment) created by John Doe'\n\n    ResourceContainers:\n      type: object\n      description: >\n        Context about the Azure DevOps organization, account, and project in which\n        the event occurred. Useful for routing events in multi-tenant scenarios.\n      properties:\n        collection:\n          $ref: '#/components/schemas/ResourceContainer'\n        account:\n          $ref: '#/components/schemas/ResourceContainer'\n        project:\n          $ref: '#/components/schemas/ResourceContainer'\n\n    ResourceContainer:\n      type: object\n      description: An Azure DevOps resource container (collection, account, or project)\n      properties:\n        id:\n          type: string\n          description: GUID identifier for this container\n          example: 'a1b2c3d4-e5f6-a1b2-c3d4-e5f6a1b2c3d4'\n        baseUrl:\n          type: string\n   \
  \       format: uri\n          description: Base URL for accessing this container\n          example: 'https://dev.azure.com/myorganization'\n        name:\n          type: string\n          description: Display name of the container\n          example: 'myorganization'\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/microsoft-azure-devops/refs/heads/main/asyncapi/azure-devops-service-hooks-asyncapi.yml
spec_file: asyncapi/azure-devops-service-hooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/microsoft-azure-devops/refs/heads/main/asyncapi/azure-devops-service-hooks-asyncapi.yml
tags:
- Agile
- CI/CD
- DevOps
- Project Management
- Version Control
- AsyncAPI
- Webhooks
- Events
version: '7.1'
---
