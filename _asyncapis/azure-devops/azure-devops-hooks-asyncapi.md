---
channels:
- description: Published when a work item is created in Azure Boards.
  name: workitem.created
  operation: subscribe
  operation_id: onWorkItemCreated
  summary: Work item created
- description: Published when a work item is updated in Azure Boards.
  name: workitem.updated
  operation: subscribe
  operation_id: onWorkItemUpdated
  summary: Work item updated
- description: Published when a build pipeline run completes.
  name: build.complete
  operation: subscribe
  operation_id: onBuildComplete
  summary: Build completed
- description: Published when code is pushed to a repository.
  name: git.push
  operation: subscribe
  operation_id: onGitPush
  summary: Code pushed to repository
- description: Published when a pull request is created.
  name: git.pullrequest.created
  operation: subscribe
  operation_id: onPullRequestCreated
  summary: Pull request created
- description: Published when a pull request is merged.
  name: git.pullrequest.merged
  operation: subscribe
  operation_id: onPullRequestMerged
  summary: Pull request merged
- description: Published when a release deployment completes.
  name: release.deployment.completed
  operation: subscribe
  operation_id: onReleaseDeploymentCompleted
  summary: Release deployment completed
description: Azure DevOps Service Hooks deliver event notifications for work item changes, build completions, pull request events, code pushes, and release deployments. Service hooks are configured in Azure DevOps settings and delivered via HTTPS POST to registered consumer endpoints.
layout: asyncapi
messages:
- description: ''
  name: WorkItemCreatedEvent
  summary: ''
  title: Work Item Created
- description: ''
  name: WorkItemUpdatedEvent
  summary: ''
  title: Work Item Updated
- description: ''
  name: BuildCompleteEvent
  summary: ''
  title: Build Complete
- description: ''
  name: GitPushEvent
  summary: ''
  title: Git Push
- description: ''
  name: PullRequestEvent
  summary: ''
  title: Pull Request Event
- description: ''
  name: ReleaseDeploymentEvent
  summary: ''
  title: Release Deployment Completed
name: Azure DevOps Service Hooks (Webhooks)
provider_name: Azure DevOps
provider_slug: azure-devops
servers:
- description: Your registered HTTPS consumer endpoint for Azure DevOps service hooks
  name: consumer
  protocol: https
  url: https://your-consumer.example.com/hooks/azure-devops
slug: azure-devops-hooks-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Azure DevOps Service Hooks (Webhooks)\n  description: >-\n    Azure DevOps Service Hooks deliver event notifications for work item changes,\n    build completions, pull request events, code pushes, and release deployments.\n    Service hooks are configured in Azure DevOps settings and delivered via HTTPS POST\n    to registered consumer endpoints.\n  version: \"7.2\"\n  contact:\n    name: Microsoft Azure DevOps\n    url: https://learn.microsoft.com/en-us/azure/devops/service-hooks/\n\nservers:\n  consumer:\n    url: https://your-consumer.example.com/hooks/azure-devops\n    protocol: https\n    description: Your registered HTTPS consumer endpoint for Azure DevOps service hooks\n\nchannels:\n  workitem.created:\n    description: Published when a work item is created in Azure Boards.\n    subscribe:\n      operationId: onWorkItemCreated\n      summary: Work item created\n      description: Receive notifications when a new work item is created.\n\
  \      tags:\n        - name: WorkItems\n      message:\n        $ref: '#/components/messages/WorkItemCreatedEvent'\n\n  workitem.updated:\n    description: Published when a work item is updated in Azure Boards.\n    subscribe:\n      operationId: onWorkItemUpdated\n      summary: Work item updated\n      description: Receive notifications when a work item field is changed.\n      tags:\n        - name: WorkItems\n      message:\n        $ref: '#/components/messages/WorkItemUpdatedEvent'\n\n  build.complete:\n    description: Published when a build pipeline run completes.\n    subscribe:\n      operationId: onBuildComplete\n      summary: Build completed\n      description: Receive notifications when a CI/CD pipeline build finishes.\n      tags:\n        - name: Builds\n      message:\n        $ref: '#/components/messages/BuildCompleteEvent'\n\n  git.push:\n    description: Published when code is pushed to a repository.\n    subscribe:\n      operationId: onGitPush\n      summary: Code\
  \ pushed to repository\n      description: Receive notifications when commits are pushed to an Azure Repos Git repository.\n      tags:\n        - name: Git\n      message:\n        $ref: '#/components/messages/GitPushEvent'\n\n  git.pullrequest.created:\n    description: Published when a pull request is created.\n    subscribe:\n      operationId: onPullRequestCreated\n      summary: Pull request created\n      description: Receive notifications when a new pull request is opened.\n      tags:\n        - name: PullRequests\n      message:\n        $ref: '#/components/messages/PullRequestEvent'\n\n  git.pullrequest.merged:\n    description: Published when a pull request is merged.\n    subscribe:\n      operationId: onPullRequestMerged\n      summary: Pull request merged\n      description: Receive notifications when a pull request is completed and merged.\n      tags:\n        - name: PullRequests\n      message:\n        $ref: '#/components/messages/PullRequestEvent'\n\n  release.deployment.completed:\n\
  \    description: Published when a release deployment completes.\n    subscribe:\n      operationId: onReleaseDeploymentCompleted\n      summary: Release deployment completed\n      description: Receive notifications when a release pipeline stage deployment finishes.\n      tags:\n        - name: Releases\n      message:\n        $ref: '#/components/messages/ReleaseDeploymentEvent'\n\ncomponents:\n  messages:\n    WorkItemCreatedEvent:\n      name: WorkItemCreatedEvent\n      title: Work Item Created\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WorkItemEventPayload'\n\n    WorkItemUpdatedEvent:\n      name: WorkItemUpdatedEvent\n      title: Work Item Updated\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/WorkItemUpdatedPayload'\n\n    BuildCompleteEvent:\n      name: BuildCompleteEvent\n      title: Build Complete\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/BuildEventPayload'\n\
  \n    GitPushEvent:\n      name: GitPushEvent\n      title: Git Push\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/GitPushPayload'\n\n    PullRequestEvent:\n      name: PullRequestEvent\n      title: Pull Request Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/PullRequestPayload'\n\n    ReleaseDeploymentEvent:\n      name: ReleaseDeploymentEvent\n      title: Release Deployment Completed\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/ReleaseDeploymentPayload'\n\n  schemas:\n    ServiceHookEnvelope:\n      type: object\n      required: [id, eventType, publisherId, resource]\n      properties:\n        id:\n          type: string\n          description: Service hook event ID (UUID)\n        eventType:\n          type: string\n        publisherId:\n          type: string\n        message:\n          type: object\n          properties:\n            text:\n\
  \              type: string\n            html:\n              type: string\n        resourceVersion:\n          type: string\n        resourceContainers:\n          type: object\n          properties:\n            collection:\n              type: object\n              properties:\n                id:\n                  type: string\n            account:\n              type: object\n              properties:\n                id:\n                  type: string\n            project:\n              type: object\n              properties:\n                id:\n                  type: string\n        createdDate:\n          type: string\n          format: date-time\n\n    WorkItemEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/ServiceHookEnvelope'\n        - type: object\n          properties:\n            eventType:\n              type: string\n              enum: [\"workitem.created\", \"workitem.updated\", \"workitem.deleted\"]\n            resource:\n              type:\
  \ object\n              properties:\n                id:\n                  type: integer\n                rev:\n                  type: integer\n                fields:\n                  type: object\n                  additionalProperties: true\n                url:\n                  type: string\n\n    WorkItemUpdatedPayload:\n      allOf:\n        - $ref: '#/components/schemas/ServiceHookEnvelope'\n        - type: object\n          properties:\n            resource:\n              type: object\n              properties:\n                id:\n                  type: integer\n                workItemId:\n                  type: integer\n                revisedBy:\n                  type: object\n                  properties:\n                    name:\n                      type: string\n                revisedDate:\n                  type: string\n                  format: date-time\n                fields:\n                  type: object\n                  description: Changed fields\
  \ with old and new values\n                  additionalProperties:\n                    type: object\n                    properties:\n                      oldValue:\n                        description: Previous value\n                      newValue:\n                        description: New value\n\n    BuildEventPayload:\n      allOf:\n        - $ref: '#/components/schemas/ServiceHookEnvelope'\n        - type: object\n          properties:\n            resource:\n              type: object\n              properties:\n                id:\n                  type: integer\n                buildNumber:\n                  type: string\n                status:\n                  type: string\n                  enum: [succeeded, failed, canceled, partiallySucceeded]\n                result:\n                  type: string\n                startTime:\n                  type: string\n                  format: date-time\n                finishTime:\n                  type: string\n         \
  \         format: date-time\n                definition:\n                  type: object\n                  properties:\n                    id:\n                      type: integer\n                    name:\n                      type: string\n\n    GitPushPayload:\n      allOf:\n        - $ref: '#/components/schemas/ServiceHookEnvelope'\n        - type: object\n          properties:\n            resource:\n              type: object\n              properties:\n                pushId:\n                  type: integer\n                date:\n                  type: string\n                  format: date-time\n                pushedBy:\n                  type: object\n                  properties:\n                    displayName:\n                      type: string\n                    uniqueName:\n                      type: string\n                commits:\n                  type: array\n                  items:\n                    type: object\n                    properties:\n  \
  \                    commitId:\n                        type: string\n                      comment:\n                        type: string\n                      author:\n                        type: object\n                        properties:\n                          name:\n                            type: string\n                          email:\n                            type: string\n                repository:\n                  type: object\n                  properties:\n                    id:\n                      type: string\n                    name:\n                      type: string\n                refUpdates:\n                  type: array\n                  items:\n                    type: object\n                    properties:\n                      name:\n                        type: string\n                      oldObjectId:\n                        type: string\n                      newObjectId:\n                        type: string\n\n    PullRequestPayload:\n\
  \      allOf:\n        - $ref: '#/components/schemas/ServiceHookEnvelope'\n        - type: object\n          properties:\n            resource:\n              type: object\n              properties:\n                pullRequestId:\n                  type: integer\n                title:\n                  type: string\n                status:\n                  type: string\n                  enum: [active, abandoned, completed]\n                createdBy:\n                  type: object\n                  properties:\n                    displayName:\n                      type: string\n                sourceRefName:\n                  type: string\n                targetRefName:\n                  type: string\n                mergeStatus:\n                  type: string\n                repository:\n                  type: object\n                  properties:\n                    id:\n                      type: string\n                    name:\n                      type: string\n\
  \n    ReleaseDeploymentPayload:\n      allOf:\n        - $ref: '#/components/schemas/ServiceHookEnvelope'\n        - type: object\n          properties:\n            resource:\n              type: object\n              properties:\n                release:\n                  type: object\n                  properties:\n                    id:\n                      type: integer\n                    name:\n                      type: string\n                environment:\n                  type: object\n                  properties:\n                    id:\n                      type: integer\n                    name:\n                      type: string\n                    status:\n                      type: string\n                      enum: [succeeded, failed, canceled, partiallySucceeded]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/azure-devops/refs/heads/main/asyncapi/azure-devops-hooks-asyncapi.yml
spec_file: asyncapi/azure-devops-hooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/azure-devops/refs/heads/main/asyncapi/azure-devops-hooks-asyncapi.yml
tags:
- Azure
- CI/CD
- DevOps
- Pipelines
- Work Items
- AsyncAPI
- Webhooks
- Events
version: '7.2'
---
