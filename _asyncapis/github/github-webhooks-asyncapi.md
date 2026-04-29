---
channels:
- description: The endpoint that receives all GitHub webhook event deliveries. The specific event type is identified by the X-GitHub-Event header.
  name: /webhook
  operation: publish
  operation_id: receiveWebhookEvent
  summary: Receive a GitHub webhook event
description: GitHub Webhooks deliver HTTP POST payloads to a configured URL whenever specified events occur on GitHub, such as pushes, pull requests, issues, releases, and more. Webhooks can be configured at the repository, organization, or GitHub App level. Each delivery includes headers for event identification, delivery tracking, and HMAC signature verification.
layout: asyncapi
messages:
- description: Triggered when one or more commits are pushed to a repository branch or tag. This is one of the most common webhook events and includes details about all commits in the push.
  name: push
  summary: Commits pushed to a repository branch or tag.
  title: Push Event
- description: Triggered when a pull request is assigned, auto-merge enabled/disabled, closed, converted to draft, demilestoned, dequeued, edited, enqueued, labeled, locked, milestoned, opened, ready for review, reopened, review requested, review request removed, synchronized, unassigned, unlabeled, or unlocked.
  name: pull_request
  summary: Pull request opened, closed, merged, or updated.
  title: Pull Request Event
- description: Triggered when an issue is opened, edited, deleted, pinned, unpinned, closed, reopened, assigned, unassigned, labeled, unlabeled, locked, unlocked, transferred, milestoned, or demilestoned.
  name: issues
  summary: Issue opened, edited, closed, or updated.
  title: Issues Event
- description: ''
  name: issue_comment
  summary: Comment on issue or pull request created, edited, or deleted.
  title: Issue Comment Event
- description: Triggered when a Git branch or tag is created. This event does not include an action property.
  name: create
  summary: Branch or tag created.
  title: Create Event
- description: Triggered when a Git branch or tag is deleted. This event does not include an action property.
  name: delete
  summary: Branch or tag deleted.
  title: Delete Event
- description: ''
  name: release
  summary: Release created, published, edited, or deleted.
  title: Release Event
- description: Triggered when a user forks a repository. This event does not include an action property.
  name: fork
  summary: Repository forked.
  title: Fork Event
- description: Triggered when someone stars a repository. This is a legacy event name that fires on star activity. The star event was added later as the correctly named equivalent.
  name: watch
  summary: User starred a repository (legacy naming).
  title: Watch Event
- description: ''
  name: star
  summary: Repository starred or unstarred.
  title: Star Event
- description: ''
  name: check_run
  summary: Check run created, completed, or rerequested.
  title: Check Run Event
- description: ''
  name: check_suite
  summary: Check suite completed, requested, or rerequested.
  title: Check Suite Event
- description: ''
  name: commit_comment
  summary: Commit comment created.
  title: Commit Comment Event
- description: ''
  name: deployment
  summary: Deployment created.
  title: Deployment Event
- description: ''
  name: deployment_status
  summary: Deployment status updated.
  title: Deployment Status Event
- description: ''
  name: discussion
  summary: Discussion created, edited, answered, or updated.
  title: Discussion Event
- description: ''
  name: discussion_comment
  summary: Discussion comment created, edited, or deleted.
  title: Discussion Comment Event
- description: ''
  name: workflow_run
  summary: Workflow run requested, completed, or in progress.
  title: Workflow Run Event
- description: ''
  name: workflow_job
  summary: Workflow job queued, in progress, completed, or waiting.
  title: Workflow Job Event
- description: ''
  name: workflow_dispatch
  summary: Workflow manually triggered.
  title: Workflow Dispatch Event
- description: ''
  name: repository
  summary: Repository created, deleted, archived, or updated.
  title: Repository Event
- description: Triggered by a POST to the repository dispatch endpoint, allowing external systems to trigger GitHub Actions workflows with custom event payloads.
  name: repository_dispatch
  summary: Custom event triggered via the API.
  title: Repository Dispatch Event
- description: ''
  name: pull_request_review
  summary: Pull request review submitted, edited, or dismissed.
  title: Pull Request Review Event
- description: ''
  name: pull_request_review_comment
  summary: Pull request review comment created, edited, or deleted.
  title: Pull Request Review Comment Event
- description: ''
  name: pull_request_review_thread
  summary: Pull request review thread resolved or unresolved.
  title: Pull Request Review Thread Event
- description: ''
  name: code_scanning_alert
  summary: Code scanning alert created, fixed, or appeared in branch.
  title: Code Scanning Alert Event
- description: ''
  name: dependabot_alert
  summary: Dependabot alert activity.
  title: Dependabot Alert Event
- description: ''
  name: secret_scanning_alert
  summary: Secret scanning alert created, resolved, or reopened.
  title: Secret Scanning Alert Event
- description: ''
  name: security_advisory
  summary: Security advisory published, updated, or withdrawn.
  title: Security Advisory Event
- description: ''
  name: branch_protection_rule
  summary: Branch protection rule created, edited, or deleted.
  title: Branch Protection Rule Event
- description: ''
  name: branch_protection_configuration
  summary: Branch protection configuration enabled or disabled.
  title: Branch Protection Configuration Event
- description: ''
  name: member
  summary: Collaborator added, removed, or permissions edited.
  title: Member Event
- description: ''
  name: membership
  summary: Team membership added or removed.
  title: Membership Event
- description: ''
  name: organization
  summary: Organization membership changes.
  title: Organization Event
- description: ''
  name: team
  summary: Team created, deleted, edited, or child team changes.
  title: Team Event
- description: ''
  name: team_add
  summary: Repository added to a team.
  title: Team Add Event
- description: ''
  name: label
  summary: Label created, edited, or deleted.
  title: Label Event
- description: ''
  name: milestone
  summary: Milestone created, closed, opened, edited, or deleted.
  title: Milestone Event
- description: ''
  name: project_card
  summary: Project (classic) card activity.
  title: Project Card Event
- description: ''
  name: project
  summary: Project (classic) created, edited, closed, or updated.
  title: Project Event
- description: ''
  name: project_column
  summary: Project (classic) column activity.
  title: Project Column Event
- description: ''
  name: projects_v2
  summary: Projects v2 created, edited, closed, or updated.
  title: Projects V2 Event
- description: ''
  name: projects_v2_item
  summary: Projects v2 item activity.
  title: Projects V2 Item Event
- description: ''
  name: page_build
  summary: GitHub Pages build attempted.
  title: Page Build Event
- description: ''
  name: package
  summary: GitHub Package published or updated.
  title: Package Event
- description: ''
  name: public
  summary: Private repository made public.
  title: Public Event
- description: Triggered when a wiki page is created or updated. The event name gollum is a long-standing GitHub tradition derived from the Lord of the Rings character.
  name: gollum
  summary: Wiki page created or updated.
  title: Wiki Event
- description: ''
  name: installation
  summary: GitHub App installed, uninstalled, or permissions changed.
  title: Installation Event
- description: ''
  name: installation_repositories
  summary: Repositories added or removed from GitHub App installation.
  title: Installation Repositories Event
- description: ''
  name: github_app_authorization
  summary: GitHub App authorization revoked.
  title: GitHub App Authorization Event
- description: ''
  name: marketplace_purchase
  summary: GitHub Marketplace purchase activity.
  title: Marketplace Purchase Event
- description: ''
  name: merge_group
  summary: Merge group checks requested or destroyed.
  title: Merge Group Event
- description: Triggered when the webhook configuration that is receiving this event is deleted. This allows the receiver to clean up any state associated with the webhook.
  name: meta
  summary: The webhook itself is deleted.
  title: Meta Event
- description: ''
  name: org_block
  summary: Organization blocked or unblocked a user.
  title: Organization Block Event
- description: Sent when a new webhook is created to verify the endpoint is reachable. This is a connectivity test and is not subscribable as a regular event.
  name: ping
  summary: Test event sent when a webhook is first created.
  title: Ping Event
- description: ''
  name: deploy_key
  summary: Deploy key created or deleted.
  title: Deploy Key Event
- description: ''
  name: deployment_protection_rule
  summary: Deployment protection rule requested.
  title: Deployment Protection Rule Event
- description: ''
  name: deployment_review
  summary: Deployment review approved, rejected, or requested.
  title: Deployment Review Event
- description: ''
  name: status
  summary: Commit status updated.
  title: Status Event
- description: ''
  name: sponsorship
  summary: Sponsorship created, edited, tier changed, or cancelled.
  title: Sponsorship Event
- description: ''
  name: repository_advisory
  summary: Repository security advisory published or reported.
  title: Repository Advisory Event
- description: ''
  name: repository_ruleset
  summary: Repository ruleset created, edited, or deleted.
  title: Repository Ruleset Event
- description: ''
  name: repository_vulnerability_alert
  summary: Vulnerability alert created, dismissed, or resolved.
  title: Repository Vulnerability Alert Event
- description: ''
  name: personal_access_token_request
  summary: Fine-grained PAT request created, approved, or denied.
  title: Personal Access Token Request Event
- description: ''
  name: custom_property
  summary: Custom property created, updated, or deleted.
  title: Custom Property Event
- description: ''
  name: custom_property_values
  summary: Custom property values changed for a repository.
  title: Custom Property Values Event
- description: ''
  name: security_and_analysis
  summary: Code security or analysis features enabled or disabled.
  title: Security and Analysis Event
- description: ''
  name: secret_scanning_alert_location
  summary: Secret scanning alert location detected.
  title: Secret Scanning Alert Location Event
- description: ''
  name: sub_issues
  summary: Sub-issue added or removed.
  title: Sub Issues Event
- description: ''
  name: repository_import
  summary: Repository import activity.
  title: Repository Import Event
- description: ''
  name: registry_package
  summary: Registry package published or updated.
  title: Registry Package Event
- description: ''
  name: installation_target
  summary: Installation target renamed.
  title: Installation Target Event
- description: ''
  name: projects_v2_status_update
  summary: Projects v2 status update activity.
  title: Projects V2 Status Update Event
- description: ''
  name: issue_dependencies
  summary: Issue dependency added or removed.
  title: Issue Dependencies Event
- description: ''
  name: secret_scanning_scan
  summary: Secret scanning scan completed.
  title: Secret Scanning Scan Event
name: GitHub Webhooks
provider_name: GitHub
provider_slug: github
servers:
- description: Your webhook receiver endpoint. GitHub sends POST requests to this URL when subscribed events occur.
  name: webhook-receiver
  protocol: https
  url: '{webhookUrl}'
slug: github-webhooks-asyncapi
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: GitHub Webhooks\n  description: >-\n    GitHub Webhooks deliver HTTP POST payloads to a configured URL whenever\n    specified events occur on GitHub, such as pushes, pull requests, issues,\n    releases, and more. Webhooks can be configured at the repository,\n    organization, or GitHub App level. Each delivery includes headers for\n    event identification, delivery tracking, and HMAC signature verification.\n  version: '2022-11-28'\n  contact:\n    name: GitHub Support\n    url: https://support.github.com/\n  license:\n    name: GitHub Terms of Service\n    url: https://docs.github.com/en/site-policy/github-terms/github-terms-of-service\n  externalDocs:\n    description: GitHub Webhooks Documentation\n    url: https://docs.github.com/en/webhooks\nservers:\n  webhook-receiver:\n    url: '{webhookUrl}'\n    protocol: https\n    description: >-\n      Your webhook receiver endpoint. GitHub sends POST requests to this URL\n      when subscribed\
  \ events occur.\n    variables:\n      webhookUrl:\n        description: The URL configured to receive webhook deliveries.\n    security:\n      - hmacSignature: []\nchannels:\n  /webhook:\n    description: >-\n      The endpoint that receives all GitHub webhook event deliveries. The\n      specific event type is identified by the X-GitHub-Event header.\n    publish:\n      operationId: receiveWebhookEvent\n      summary: Receive a GitHub webhook event\n      description: >-\n        GitHub delivers webhook events as HTTP POST requests with JSON payloads.\n        Each delivery includes identifying headers and an HMAC signature for\n        verification. The maximum payload size is 25 MB.\n      bindings:\n        http:\n          type: request\n          method: POST\n          headers:\n            type: object\n            properties:\n              X-GitHub-Event:\n                type: string\n                description: The name of the event that triggered the delivery.\n      \
  \        X-GitHub-Delivery:\n                type: string\n                format: uuid\n                description: A GUID to uniquely identify the delivery.\n              X-GitHub-Hook-ID:\n                type: string\n                description: Unique identifier for the webhook configuration.\n              X-Hub-Signature-256:\n                type: string\n                description: >-\n                  HMAC-SHA256 hex digest of the payload body, prefixed with\n                  sha256=. Used for verifying payload authenticity.\n              X-GitHub-Hook-Installation-Target-Type:\n                type: string\n                enum:\n                  - repository\n                  - organization\n                  - business\n                  - app\n                description: The type of resource the webhook is installed on.\n              X-GitHub-Hook-Installation-Target-ID:\n                type: string\n                description: The unique identifier of the resource\
  \ the webhook is installed on.\n              User-Agent:\n                type: string\n                description: Always prefixed with GitHub-Hookshot/.\n      message:\n        oneOf:\n          - $ref: '#/components/messages/push'\n          - $ref: '#/components/messages/pull_request'\n          - $ref: '#/components/messages/issues'\n          - $ref: '#/components/messages/issue_comment'\n          - $ref: '#/components/messages/create'\n          - $ref: '#/components/messages/delete'\n          - $ref: '#/components/messages/release'\n          - $ref: '#/components/messages/fork'\n          - $ref: '#/components/messages/watch'\n          - $ref: '#/components/messages/star'\n          - $ref: '#/components/messages/check_run'\n          - $ref: '#/components/messages/check_suite'\n          - $ref: '#/components/messages/commit_comment'\n          - $ref: '#/components/messages/deployment'\n          - $ref: '#/components/messages/deployment_status'\n          - $ref: '#/components/messages/discussion'\n\
  \          - $ref: '#/components/messages/discussion_comment'\n          - $ref: '#/components/messages/workflow_run'\n          - $ref: '#/components/messages/workflow_job'\n          - $ref: '#/components/messages/workflow_dispatch'\n          - $ref: '#/components/messages/repository'\n          - $ref: '#/components/messages/repository_dispatch'\n          - $ref: '#/components/messages/pull_request_review'\n          - $ref: '#/components/messages/pull_request_review_comment'\n          - $ref: '#/components/messages/pull_request_review_thread'\n          - $ref: '#/components/messages/code_scanning_alert'\n          - $ref: '#/components/messages/dependabot_alert'\n          - $ref: '#/components/messages/secret_scanning_alert'\n          - $ref: '#/components/messages/security_advisory'\n          - $ref: '#/components/messages/branch_protection_rule'\n          - $ref: '#/components/messages/branch_protection_configuration'\n          - $ref: '#/components/messages/member'\n  \
  \        - $ref: '#/components/messages/membership'\n          - $ref: '#/components/messages/organization'\n          - $ref: '#/components/messages/team'\n          - $ref: '#/components/messages/team_add'\n          - $ref: '#/components/messages/label'\n          - $ref: '#/components/messages/milestone'\n          - $ref: '#/components/messages/project_card'\n          - $ref: '#/components/messages/project'\n          - $ref: '#/components/messages/project_column'\n          - $ref: '#/components/messages/projects_v2'\n          - $ref: '#/components/messages/projects_v2_item'\n          - $ref: '#/components/messages/page_build'\n          - $ref: '#/components/messages/package'\n          - $ref: '#/components/messages/public'\n          - $ref: '#/components/messages/gollum'\n          - $ref: '#/components/messages/installation'\n          - $ref: '#/components/messages/installation_repositories'\n          - $ref: '#/components/messages/github_app_authorization'\n          -\
  \ $ref: '#/components/messages/marketplace_purchase'\n          - $ref: '#/components/messages/merge_group'\n          - $ref: '#/components/messages/meta'\n          - $ref: '#/components/messages/org_block'\n          - $ref: '#/components/messages/ping'\n          - $ref: '#/components/messages/deploy_key'\n          - $ref: '#/components/messages/deployment_protection_rule'\n          - $ref: '#/components/messages/deployment_review'\n          - $ref: '#/components/messages/status'\n          - $ref: '#/components/messages/sponsorship'\n          - $ref: '#/components/messages/repository_advisory'\n          - $ref: '#/components/messages/repository_ruleset'\n          - $ref: '#/components/messages/repository_vulnerability_alert'\n          - $ref: '#/components/messages/personal_access_token_request'\n          - $ref: '#/components/messages/custom_property'\n          - $ref: '#/components/messages/custom_property_values'\n          - $ref: '#/components/messages/security_and_analysis'\n\
  \          - $ref: '#/components/messages/secret_scanning_alert_location'\n          - $ref: '#/components/messages/sub_issues'\n          - $ref: '#/components/messages/repository_import'\n          - $ref: '#/components/messages/registry_package'\n          - $ref: '#/components/messages/installation_target'\n          - $ref: '#/components/messages/projects_v2_status_update'\n          - $ref: '#/components/messages/issue_dependencies'\n          - $ref: '#/components/messages/secret_scanning_scan'\ncomponents:\n  securitySchemes:\n    hmacSignature:\n      type: httpApiKey\n      name: X-Hub-Signature-256\n      in: header\n      description: >-\n        HMAC-SHA256 signature of the payload using the webhook secret. The value\n        is prefixed with sha256=. Use constant-time comparison to validate.\n  messages:\n    push:\n      name: push\n      title: Push Event\n      summary: Commits pushed to a repository branch or tag.\n      description: >-\n        Triggered when one or\
  \ more commits are pushed to a repository branch or\n        tag. This is one of the most common webhook events and includes details\n        about all commits in the push.\n      payload:\n        $ref: '#/components/schemas/PushEvent'\n    pull_request:\n      name: pull_request\n      title: Pull Request Event\n      summary: Pull request opened, closed, merged, or updated.\n      description: >-\n        Triggered when a pull request is assigned, auto-merge enabled/disabled,\n        closed, converted to draft, demilestoned, dequeued, edited, enqueued,\n        labeled, locked, milestoned, opened, ready for review, reopened,\n        review requested, review request removed, synchronized, unassigned,\n        unlabeled, or unlocked.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    issues:\n      name: issues\n      title: Issues Event\n      summary: Issue opened, edited, closed, or updated.\n      description: >-\n        Triggered when an issue is opened, edited,\
  \ deleted, pinned, unpinned,\n        closed, reopened, assigned, unassigned, labeled, unlabeled, locked,\n        unlocked, transferred, milestoned, or demilestoned.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    issue_comment:\n      name: issue_comment\n      title: Issue Comment Event\n      summary: Comment on issue or pull request created, edited, or deleted.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    create:\n      name: create\n      title: Create Event\n      summary: Branch or tag created.\n      description: >-\n        Triggered when a Git branch or tag is created. This event does not\n        include an action property.\n      payload:\n        $ref: '#/components/schemas/RefEvent'\n    delete:\n      name: delete\n      title: Delete Event\n      summary: Branch or tag deleted.\n      description: >-\n        Triggered when a Git branch or tag is deleted. This event does not\n        include an action property.\n      payload:\n\
  \        $ref: '#/components/schemas/RefEvent'\n    release:\n      name: release\n      title: Release Event\n      summary: Release created, published, edited, or deleted.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    fork:\n      name: fork\n      title: Fork Event\n      summary: Repository forked.\n      description: >-\n        Triggered when a user forks a repository. This event does not include\n        an action property.\n      payload:\n        $ref: '#/components/schemas/BaseEvent'\n    watch:\n      name: watch\n      title: Watch Event\n      summary: User starred a repository (legacy naming).\n      description: >-\n        Triggered when someone stars a repository. This is a legacy event name\n        that fires on star activity. The star event was added later as the\n        correctly named equivalent.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    star:\n      name: star\n      title: Star Event\n      summary: Repository\
  \ starred or unstarred.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    check_run:\n      name: check_run\n      title: Check Run Event\n      summary: Check run created, completed, or rerequested.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    check_suite:\n      name: check_suite\n      title: Check Suite Event\n      summary: Check suite completed, requested, or rerequested.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    commit_comment:\n      name: commit_comment\n      title: Commit Comment Event\n      summary: Commit comment created.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    deployment:\n      name: deployment\n      title: Deployment Event\n      summary: Deployment created.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    deployment_status:\n      name: deployment_status\n      title: Deployment Status Event\n      summary: Deployment status updated.\n    \
  \  payload:\n        $ref: '#/components/schemas/ActionEvent'\n    discussion:\n      name: discussion\n      title: Discussion Event\n      summary: Discussion created, edited, answered, or updated.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    discussion_comment:\n      name: discussion_comment\n      title: Discussion Comment Event\n      summary: Discussion comment created, edited, or deleted.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    workflow_run:\n      name: workflow_run\n      title: Workflow Run Event\n      summary: Workflow run requested, completed, or in progress.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    workflow_job:\n      name: workflow_job\n      title: Workflow Job Event\n      summary: Workflow job queued, in progress, completed, or waiting.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    workflow_dispatch:\n      name: workflow_dispatch\n      title: Workflow Dispatch\
  \ Event\n      summary: Workflow manually triggered.\n      payload:\n        $ref: '#/components/schemas/BaseEvent'\n    repository:\n      name: repository\n      title: Repository Event\n      summary: Repository created, deleted, archived, or updated.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    repository_dispatch:\n      name: repository_dispatch\n      title: Repository Dispatch Event\n      summary: Custom event triggered via the API.\n      description: >-\n        Triggered by a POST to the repository dispatch endpoint, allowing\n        external systems to trigger GitHub Actions workflows with custom\n        event payloads.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    pull_request_review:\n      name: pull_request_review\n      title: Pull Request Review Event\n      summary: Pull request review submitted, edited, or dismissed.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    pull_request_review_comment:\n\
  \      name: pull_request_review_comment\n      title: Pull Request Review Comment Event\n      summary: Pull request review comment created, edited, or deleted.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    pull_request_review_thread:\n      name: pull_request_review_thread\n      title: Pull Request Review Thread Event\n      summary: Pull request review thread resolved or unresolved.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    code_scanning_alert:\n      name: code_scanning_alert\n      title: Code Scanning Alert Event\n      summary: Code scanning alert created, fixed, or appeared in branch.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    dependabot_alert:\n      name: dependabot_alert\n      title: Dependabot Alert Event\n      summary: Dependabot alert activity.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    secret_scanning_alert:\n      name: secret_scanning_alert\n      title: Secret\
  \ Scanning Alert Event\n      summary: Secret scanning alert created, resolved, or reopened.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    security_advisory:\n      name: security_advisory\n      title: Security Advisory Event\n      summary: Security advisory published, updated, or withdrawn.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    branch_protection_rule:\n      name: branch_protection_rule\n      title: Branch Protection Rule Event\n      summary: Branch protection rule created, edited, or deleted.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    branch_protection_configuration:\n      name: branch_protection_configuration\n      title: Branch Protection Configuration Event\n      summary: Branch protection configuration enabled or disabled.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    member:\n      name: member\n      title: Member Event\n      summary: Collaborator added, removed,\
  \ or permissions edited.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    membership:\n      name: membership\n      title: Membership Event\n      summary: Team membership added or removed.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    organization:\n      name: organization\n      title: Organization Event\n      summary: Organization membership changes.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    team:\n      name: team\n      title: Team Event\n      summary: Team created, deleted, edited, or child team changes.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    team_add:\n      name: team_add\n      title: Team Add Event\n      summary: Repository added to a team.\n      payload:\n        $ref: '#/components/schemas/BaseEvent'\n    label:\n      name: label\n      title: Label Event\n      summary: Label created, edited, or deleted.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n\
  \    milestone:\n      name: milestone\n      title: Milestone Event\n      summary: Milestone created, closed, opened, edited, or deleted.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    project_card:\n      name: project_card\n      title: Project Card Event\n      summary: Project (classic) card activity.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    project:\n      name: project\n      title: Project Event\n      summary: Project (classic) created, edited, closed, or updated.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    project_column:\n      name: project_column\n      title: Project Column Event\n      summary: Project (classic) column activity.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    projects_v2:\n      name: projects_v2\n      title: Projects V2 Event\n      summary: Projects v2 created, edited, closed, or updated.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n\
  \    projects_v2_item:\n      name: projects_v2_item\n      title: Projects V2 Item Event\n      summary: Projects v2 item activity.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    page_build:\n      name: page_build\n      title: Page Build Event\n      summary: GitHub Pages build attempted.\n      payload:\n        $ref: '#/components/schemas/BaseEvent'\n    package:\n      name: package\n      title: Package Event\n      summary: GitHub Package published or updated.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    public:\n      name: public\n      title: Public Event\n      summary: Private repository made public.\n      payload:\n        $ref: '#/components/schemas/BaseEvent'\n    gollum:\n      name: gollum\n      title: Wiki Event\n      summary: Wiki page created or updated.\n      description: >-\n        Triggered when a wiki page is created or updated. The event name gollum\n        is a long-standing GitHub tradition derived from\
  \ the Lord of the Rings\n        character.\n      payload:\n        $ref: '#/components/schemas/BaseEvent'\n    installation:\n      name: installation\n      title: Installation Event\n      summary: GitHub App installed, uninstalled, or permissions changed.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    installation_repositories:\n      name: installation_repositories\n      title: Installation Repositories Event\n      summary: Repositories added or removed from GitHub App installation.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    github_app_authorization:\n      name: github_app_authorization\n      title: GitHub App Authorization Event\n      summary: GitHub App authorization revoked.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    marketplace_purchase:\n      name: marketplace_purchase\n      title: Marketplace Purchase Event\n      summary: GitHub Marketplace purchase activity.\n      payload:\n        $ref:\
  \ '#/components/schemas/ActionEvent'\n    merge_group:\n      name: merge_group\n      title: Merge Group Event\n      summary: Merge group checks requested or destroyed.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    meta:\n      name: meta\n      title: Meta Event\n      summary: The webhook itself is deleted.\n      description: >-\n        Triggered when the webhook configuration that is receiving this event\n        is deleted. This allows the receiver to clean up any state associated\n        with the webhook.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    org_block:\n      name: org_block\n      title: Organization Block Event\n      summary: Organization blocked or unblocked a user.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    ping:\n      name: ping\n      title: Ping Event\n      summary: Test event sent when a webhook is first created.\n      description: >-\n        Sent when a new webhook is created\
  \ to verify the endpoint is reachable.\n        This is a connectivity test and is not subscribable as a regular event.\n      payload:\n        $ref: '#/components/schemas/PingEvent'\n    deploy_key:\n      name: deploy_key\n      title: Deploy Key Event\n      summary: Deploy key created or deleted.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    deployment_protection_rule:\n      name: deployment_protection_rule\n      title: Deployment Protection Rule Event\n      summary: Deployment protection rule requested.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    deployment_review:\n      name: deployment_review\n      title: Deployment Review Event\n      summary: Deployment review approved, rejected, or requested.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    status:\n      name: status\n      title: Status Event\n      summary: Commit status updated.\n      payload:\n        $ref: '#/components/schemas/BaseEvent'\n\
  \    sponsorship:\n      name: sponsorship\n      title: Sponsorship Event\n      summary: Sponsorship created, edited, tier changed, or cancelled.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    repository_advisory:\n      name: repository_advisory\n      title: Repository Advisory Event\n      summary: Repository security advisory published or reported.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    repository_ruleset:\n      name: repository_ruleset\n      title: Repository Ruleset Event\n      summary: Repository ruleset created, edited, or deleted.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    repository_vulnerability_alert:\n      name: repository_vulnerability_alert\n      title: Repository Vulnerability Alert Event\n      summary: Vulnerability alert created, dismissed, or resolved.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    personal_access_token_request:\n      name: personal_access_token_request\n\
  \      title: Personal Access Token Request Event\n      summary: Fine-grained PAT request created, approved, or denied.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    custom_property:\n      name: custom_property\n      title: Custom Property Event\n      summary: Custom property created, updated, or deleted.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    custom_property_values:\n      name: custom_property_values\n      title: Custom Property Values Event\n      summary: Custom property values changed for a repository.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    security_and_analysis:\n      name: security_and_analysis\n      title: Security and Analysis Event\n      summary: Code security or analysis features enabled or disabled.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    secret_scanning_alert_location:\n      name: secret_scanning_alert_location\n      title: Secret Scanning Alert\
  \ Location Event\n      summary: Secret scanning alert location detected.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    sub_issues:\n      name: sub_issues\n      title: Sub Issues Event\n      summary: Sub-issue added or removed.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    repository_import:\n      name: repository_import\n      title: Repository Import Event\n      summary: Repository import activity.\n      payload:\n        $ref: '#/components/schemas/BaseEvent'\n    registry_package:\n      name: registry_package\n      title: Registry Package Event\n      summary: Registry package published or updated.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    installation_target:\n      name: installation_target\n      title: Installation Target Event\n      summary: Installation target renamed.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    projects_v2_status_update:\n      name: projects_v2_status_update\n\
  \      title: Projects V2 Status Update Event\n      summary: Projects v2 status update activity.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    issue_dependencies:\n      name: issue_dependencies\n      title: Issue Dependencies Event\n      summary: Issue dependency added or removed.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n    secret_scanning_scan:\n      name: secret_scanning_scan\n      title: Secret Scanning Scan Event\n      summary: Secret scanning scan completed.\n      payload:\n        $ref: '#/components/schemas/ActionEvent'\n  schemas:\n    BaseEvent:\n      type: object\n      description: >-\n        Common properties shared by all GitHub webhook event payloads.\n      properties:\n        sender:\n          $ref: '#/components/schemas/User'\n        repository:\n          $ref: '#/components/schemas/Repository'\n        organization:\n          $ref: '#/components/schemas/Organization'\n        enterprise:\n          type:\
  \ object\n          description: The enterprise account, present for enterprise-level events.\n        installation:\n          type: object\n          description: >-\n            The GitHub App installation, present when the delivery is to a\n            GitHub App.\n          properties:\n            id:\n              type: integer\n              description: The installation ID.\n            node_id:\n              type: string\n              description: The node ID for the installation.\n    ActionEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseEvent'\n        - type: object\n          properties:\n            action:\n              type: string\n              description: >-\n                The action that was performed. This is the primary discriminator\n                for determining what happened within an event type.\n    PushEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseEvent'\n        - type: object\n          required:\n            - ref\n\
  \            - commits\n          properties:\n            ref:\n              type: string\n              description: >-\n                The full git ref that was pushed, e.g. refs/heads/main or\n                refs/tags/v1.0.\n            before:\n              type: string\n              description: The SHA of the most recent commit before the push.\n            after:\n              type: string\n              description: The SHA of the most recent commit after the push.\n            created:\n              type: boolean\n              description: Whether this push created the ref.\n            deleted:\n              type: boolean\n              description: Whether this push deleted the ref.\n            forced:\n              type: boolean\n              description: Whether this was a force push.\n            head_commit:\n              $ref: '#/components/schemas/Commit'\n            commits:\n              type: array\n              description: The list of pushed commits.\n\
  \              items:\n                $ref: '#/components/schemas/Commit'\n            compare:\n              type: string\n              format: uri\n              description: URL comparing the before and after commits.\n            pusher:\n              type: object\n              description: The user who pushed the commits.\n              properties:\n                name:\n                  type: string\n                email:\n                  type: string\n                  format: email\n    RefEvent:\n      allOf:\n        - $ref: '#/components/schemas/BaseEvent'\n        - type: object\n          required:\n            - ref\n            - ref_type\n          properties:\n            ref:\n              type: string\n              description: The git ref name (branch or tag name).\n            ref_type:\n              type: string\n              enum:\n                - branch\n                - tag\n              description: The type of git ref object created or deleted.\n\
  \            master_branch:\n              type: string\n              description: The name of the repository's default branch.\n            description:\n              type: string\n              description: The repository description.\n    PingEvent:\n      type: object\n      description: >-\n        Sent when a webhook is first created to verify the endpoint is reachable.\n      properties:\n        zen:\n          type: string\n          description: A random string from the Zen of GitHub.\n        hook_id:\n          type: integer\n          description: The ID of the webhook that triggered the ping.\n        hook:\n          type: object\n          description: The webhook configuration.\n          properties:\n            type:\n              type: string\n            id:\n              type: integer\n            name:\n              type: string\n            active:\n              type: boolean\n            events:\n              type: array\n              items:\n         \
  \       type: string\n            config:\n              type: object\n              properties:\n                content_type:\n                  type: string\n                url:\n                  type: string\n                  format: uri\n                insecure_ssl:\n                  type: string\n        sender:\n          $ref: '#/components/schemas/User'\n        repository:\n          $ref: '#/components/schemas/Repository'\n    User:\n      type: object\n      description: A GitHub user account.\n      properties:\n        login:\n          type: string\n          description: The username of the user.\n        id:\n          type: integer\n          description: The unique identifier for the user.\n        node_id:\n          type: string\n          description: The node ID for GraphQL.\n        avatar_url:\n          type: string\n          format: uri\n          description: URL to the user's avatar image.\n        html_url:\n          type: string\n          format:\
  \ uri\n          description: URL to the user's GitHub profile.\n        type:\n          type: string\n          enum:\n            - User\n            - Organization\n            - Bot\n          description: The type of account.\n        site_admin:\n          type: boolean\n          description: Whether the user is a GitHub site administrator.\n    Repository:\n      type: object\n      description: A GitHub repository.\n      properties:\n        id:\n          type: integer\n          description: The unique identifier for the repository.\n        node_id:\n          type: string\n          description: The node ID for GraphQL.\n        name:\n          type: string\n          description: The name of the repository.\n        full_name:\n          type: string\n          description: The full name of the repository (owner/name).\n        private:\n          type: boolean\n          description: Whether the repository is private.\n        owner:\n          $ref: '#/components/schemas/User'\n\
  \        html_url:\n          type: string\n          format: uri\n          description: URL to the repository on GitHub.\n        description:\n          type: string\n          description: The repository description.\n        fork:\n          type: boolean\n          description: Whether the repository is a fork.\n        url:\n          type: string\n          format: uri\n          description: API URL for the repository.\n        default_branch:\n          type: string\n          description: The default branch of the repository.\n        visibility:\n          type: string\n          enum:\n            - public\n            - private\n            - internal\n          description: The visibility of the repository.\n    Organization:\n      type: object\n      description: A GitHub organization.\n      properties:\n        login:\n          type: string\n          description: The organization's login name.\n        id:\n          type: integer\n          description: The unique\
  \ identifier for the organization.\n        node_id:\n          type: string\n          description: The node ID for GraphQL.\n        url:\n          type: string\n          format: uri\n          description: API URL for the organization.\n        avatar_url:\n          type: string\n          format: uri\n          description: URL to the organization's avatar image.\n        description:\n          type: string\n          description: The organization's description.\n    Commit:\n      type: object\n      description: A Git commit included in a push eve\n\n# --- truncated at 32 KB (33 KB total) ---\n# Full source: https://raw.githubusercontent.com/api-evangelist/github/refs/heads/main/asyncapi/github-webhooks-asyncapi.yml\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/github/refs/heads/main/asyncapi/github-webhooks-asyncapi.yml
spec_file: asyncapi/github-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/github/refs/heads/main/asyncapi/github-webhooks-asyncapi.yml
tags:
- Code
- Pipelines
- Platform
- Software Development
- Source Control
- T1
- AsyncAPI
- Webhooks
- Events
version: '2022-11-28'
---
