---
api_specs:
- filename: reference
  format: yaml
  label: Twitch API
  slug: ''
  spec_type: OpenAPI
  url: https://dev.twitch.tv/docs/api/reference
- filename: twitch-eventsub-asyncapi.yml
  format: yaml
  label: Twitch EventSub
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/asyncapi/twitch-eventsub-asyncapi.yml
- filename: twitch-extensions-openapi.yml
  format: yaml
  label: Twitch Extensions API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/openapi/twitch-extensions-openapi.yml
- filename: twitch-drops-openapi.yml
  format: yaml
  label: Twitch Drops API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/openapi/twitch-drops-openapi.yml
- filename: twitch-video-broadcast-openapi.yml
  format: yaml
  label: Twitch Video Broadcast API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/openapi/twitch-video-broadcast-openapi.yml
- filename: twitch-insights-analytics-openapi.yml
  format: yaml
  label: Twitch Insights and Analytics API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/openapi/twitch-insights-analytics-openapi.yml
- filename: twitch-igdb-openapi.yml
  format: yaml
  label: IGDB API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/openapi/twitch-igdb-openapi.yml
channels:
- description: A broadcaster updates their channel properties.
  name: channel.update
  operation: subscribe
  operation_id: onChannelUpdate
  summary: Channel Update
- description: A user follows the specified broadcaster.
  name: channel.follow
  operation: subscribe
  operation_id: onChannelFollow
  summary: Channel Follow
- description: A user subscribes to the specified broadcaster.
  name: channel.subscribe
  operation: subscribe
  operation_id: onChannelSubscribe
  summary: Channel Subscribe
- description: A subscription to the specified broadcaster expires.
  name: channel.subscription.end
  operation: subscribe
  operation_id: onChannelSubscriptionEnd
  summary: Channel Subscription End
- description: A user gifts a subscription to one or more viewers.
  name: channel.subscription.gift
  operation: subscribe
  operation_id: onChannelSubscriptionGift
  summary: Channel Subscription Gift
- description: A user sends a resubscription chat message.
  name: channel.subscription.message
  operation: subscribe
  operation_id: onChannelSubscriptionMessage
  summary: Channel Subscription Message
- description: A user cheers Bits in the specified channel.
  name: channel.cheer
  operation: subscribe
  operation_id: onChannelCheer
  summary: Channel Cheer
- description: A broadcaster raids another broadcaster's channel.
  name: channel.raid
  operation: subscribe
  operation_id: onChannelRaid
  summary: Channel Raid
- description: A viewer is banned or timed out from a channel.
  name: channel.ban
  operation: subscribe
  operation_id: onChannelBan
  summary: Channel Ban
- description: A viewer is unbanned from a channel.
  name: channel.unban
  operation: subscribe
  operation_id: onChannelUnban
  summary: Channel Unban
- description: A moderator is added to a channel.
  name: channel.moderator.add
  operation: subscribe
  operation_id: onChannelModeratorAdd
  summary: Channel Moderator Add
- description: A moderator is removed from a channel.
  name: channel.moderator.remove
  operation: subscribe
  operation_id: onChannelModeratorRemove
  summary: Channel Moderator Remove
- description: A custom channel points reward is added to a channel.
  name: channel.channel_points_custom_reward.add
  operation: subscribe
  operation_id: onChannelPointsCustomRewardAdd
  summary: Channel Points Custom Reward Add
- description: A viewer redeems a custom channel points reward.
  name: channel.channel_points_custom_reward_redemption.add
  operation: subscribe
  operation_id: onChannelPointsRedemptionAdd
  summary: Channel Points Redemption Add
- description: A poll begins on a channel.
  name: channel.poll.begin
  operation: subscribe
  operation_id: onChannelPollBegin
  summary: Channel Poll Begin
- description: A poll ends on a channel.
  name: channel.poll.end
  operation: subscribe
  operation_id: onChannelPollEnd
  summary: Channel Poll End
- description: A prediction begins on a channel.
  name: channel.prediction.begin
  operation: subscribe
  operation_id: onChannelPredictionBegin
  summary: Channel Prediction Begin
- description: A prediction ends on a channel.
  name: channel.prediction.end
  operation: subscribe
  operation_id: onChannelPredictionEnd
  summary: Channel Prediction End
- description: A Hype Train begins on a channel.
  name: channel.hype_train.begin
  operation: subscribe
  operation_id: onHypeTrainBegin
  summary: Hype Train Begin
- description: A Hype Train makes progress on a channel.
  name: channel.hype_train.progress
  operation: subscribe
  operation_id: onHypeTrainProgress
  summary: Hype Train Progress
- description: A Hype Train ends on a channel.
  name: channel.hype_train.end
  operation: subscribe
  operation_id: onHypeTrainEnd
  summary: Hype Train End
- description: A user donates to a charity campaign on a channel.
  name: channel.charity_campaign.donate
  operation: subscribe
  operation_id: onCharityDonation
  summary: Charity Campaign Donate
- description: A creator goal begins on a channel.
  name: channel.goal.begin
  operation: subscribe
  operation_id: onGoalBegin
  summary: Goal Begin
- description: A creator goal makes progress.
  name: channel.goal.progress
  operation: subscribe
  operation_id: onGoalProgress
  summary: Goal Progress
- description: A creator goal ends on a channel.
  name: channel.goal.end
  operation: subscribe
  operation_id: onGoalEnd
  summary: Goal End
- description: A chat message is sent in a channel.
  name: channel.chat.message
  operation: subscribe
  operation_id: onChatMessage
  summary: Chat Message
- description: A chat notification is sent in a channel (sub, raid, etc.).
  name: channel.chat.notification
  operation: subscribe
  operation_id: onChatNotification
  summary: Chat Notification
- description: The specified broadcaster starts a stream.
  name: stream.online
  operation: subscribe
  operation_id: onStreamOnline
  summary: Stream Online
- description: The specified broadcaster stops a stream.
  name: stream.offline
  operation: subscribe
  operation_id: onStreamOffline
  summary: Stream Offline
- description: A user's authorization is granted for an application.
  name: user.authorization.grant
  operation: subscribe
  operation_id: onUserAuthorizationGrant
  summary: User Authorization Grant
- description: A user's authorization is revoked for an application.
  name: user.authorization.revoke
  operation: subscribe
  operation_id: onUserAuthorizationRevoke
  summary: User Authorization Revoke
- description: A user updates their account.
  name: user.update
  operation: subscribe
  operation_id: onUserUpdate
  summary: User Update
- description: A Drops entitlement is granted to a user.
  name: drop.entitlement.grant
  operation: subscribe
  operation_id: onDropEntitlementGrant
  summary: Drop Entitlement Grant
description: EventSub is Twitch's event-driven subscription service for receiving real-time notifications about events on Twitch. Supports webhook, WebSocket, and conduit transport methods. Subscribe to events such as stream changes, channel updates, chat messages, subscriptions, follows, raids, bans, and more.
layout: asyncapi
messages:
- description: ''
  name: ChannelUpdateEvent
  summary: ''
  title: Channel Update Event
- description: ''
  name: ChannelFollowEvent
  summary: ''
  title: Channel Follow Event
- description: ''
  name: ChannelSubscribeEvent
  summary: ''
  title: Channel Subscribe Event
- description: ''
  name: ChannelSubscriptionEndEvent
  summary: ''
  title: Channel Subscription End Event
- description: ''
  name: ChannelSubscriptionGiftEvent
  summary: ''
  title: Channel Subscription Gift Event
- description: ''
  name: ChannelSubscriptionMessageEvent
  summary: ''
  title: Channel Subscription Message Event
- description: ''
  name: ChannelCheerEvent
  summary: ''
  title: Channel Cheer Event
- description: ''
  name: ChannelRaidEvent
  summary: ''
  title: Channel Raid Event
- description: ''
  name: ChannelBanEvent
  summary: ''
  title: Channel Ban Event
- description: ''
  name: ChannelUnbanEvent
  summary: ''
  title: Channel Unban Event
- description: ''
  name: ChannelModeratorAddEvent
  summary: ''
  title: Channel Moderator Add Event
- description: ''
  name: ChannelModeratorRemoveEvent
  summary: ''
  title: Channel Moderator Remove Event
- description: ''
  name: ChannelPointsCustomRewardEvent
  summary: ''
  title: Channel Points Custom Reward Event
- description: ''
  name: ChannelPointsRedemptionEvent
  summary: ''
  title: Channel Points Redemption Event
- description: ''
  name: ChannelPollEvent
  summary: ''
  title: Channel Poll Event
- description: ''
  name: ChannelPredictionEvent
  summary: ''
  title: Channel Prediction Event
- description: ''
  name: HypeTrainEvent
  summary: ''
  title: Hype Train Event
- description: ''
  name: HypeTrainEndEvent
  summary: ''
  title: Hype Train End Event
- description: ''
  name: CharityDonationEvent
  summary: ''
  title: Charity Donation Event
- description: ''
  name: GoalEvent
  summary: ''
  title: Goal Event
- description: ''
  name: ChatMessageEvent
  summary: ''
  title: Chat Message Event
- description: ''
  name: ChatNotificationEvent
  summary: ''
  title: Chat Notification Event
- description: ''
  name: StreamOnlineEvent
  summary: ''
  title: Stream Online Event
- description: ''
  name: StreamOfflineEvent
  summary: ''
  title: Stream Offline Event
- description: ''
  name: UserAuthorizationGrantEvent
  summary: ''
  title: User Authorization Grant Event
- description: ''
  name: UserAuthorizationRevokeEvent
  summary: ''
  title: User Authorization Revoke Event
- description: ''
  name: UserUpdateEvent
  summary: ''
  title: User Update Event
- description: ''
  name: DropEntitlementGrantEvent
  summary: ''
  title: Drop Entitlement Grant Event
name: Twitch EventSub
provider_name: Twitch
provider_slug: twitch
servers:
- description: Webhook transport - Twitch sends HTTP POST notifications to your registered callback URL
  name: webhook
  protocol: https
  url: '{callbackUrl}'
- description: WebSocket transport - Connect to receive events over a persistent WebSocket connection
  name: websocket
  protocol: wss
  url: wss://eventsub.wss.twitch.tv/ws
slug: twitch-eventsub-asyncapi
source_filename: twitch-eventsub-asyncapi.yml
source_heading: AsyncAPI Specification
source_yaml: "asyncapi: 2.6.0\ninfo:\n  title: Twitch EventSub\n  version: '1.0'\n  description: >-\n    EventSub is Twitch's event-driven subscription service for receiving\n    real-time notifications about events on Twitch. Supports webhook,\n    WebSocket, and conduit transport methods. Subscribe to events such as\n    stream changes, channel updates, chat messages, subscriptions,\n    follows, raids, bans, and more.\n  contact:\n    name: Twitch Developer Support\n    url: https://dev.twitch.tv/support/\n  termsOfService: https://www.twitch.tv/p/legal/terms-of-service/\n  externalDocs:\n    description: Twitch EventSub Documentation\n    url: https://dev.twitch.tv/docs/eventsub\nservers:\n  webhook:\n    url: '{callbackUrl}'\n    protocol: https\n    description: >-\n      Webhook transport - Twitch sends HTTP POST notifications to your\n      registered callback URL\n    variables:\n      callbackUrl:\n        description: Your HTTPS callback endpoint\n  websocket:\n    url: wss://eventsub.wss.twitch.tv/ws\n\
  \    protocol: wss\n    description: >-\n      WebSocket transport - Connect to receive events over a persistent\n      WebSocket connection\ndefaultContentType: application/json\nchannels:\n  channel.update:\n    description: A broadcaster updates their channel properties.\n    subscribe:\n      operationId: onChannelUpdate\n      summary: Channel Update\n      message:\n        $ref: '#/components/messages/ChannelUpdateEvent'\n  channel.follow:\n    description: A user follows the specified broadcaster.\n    subscribe:\n      operationId: onChannelFollow\n      summary: Channel Follow\n      message:\n        $ref: '#/components/messages/ChannelFollowEvent'\n  channel.subscribe:\n    description: A user subscribes to the specified broadcaster.\n    subscribe:\n      operationId: onChannelSubscribe\n      summary: Channel Subscribe\n      message:\n        $ref: '#/components/messages/ChannelSubscribeEvent'\n  channel.subscription.end:\n    description: A subscription to the specified\
  \ broadcaster expires.\n    subscribe:\n      operationId: onChannelSubscriptionEnd\n      summary: Channel Subscription End\n      message:\n        $ref: '#/components/messages/ChannelSubscriptionEndEvent'\n  channel.subscription.gift:\n    description: A user gifts a subscription to one or more viewers.\n    subscribe:\n      operationId: onChannelSubscriptionGift\n      summary: Channel Subscription Gift\n      message:\n        $ref: '#/components/messages/ChannelSubscriptionGiftEvent'\n  channel.subscription.message:\n    description: A user sends a resubscription chat message.\n    subscribe:\n      operationId: onChannelSubscriptionMessage\n      summary: Channel Subscription Message\n      message:\n        $ref: '#/components/messages/ChannelSubscriptionMessageEvent'\n  channel.cheer:\n    description: A user cheers Bits in the specified channel.\n    subscribe:\n      operationId: onChannelCheer\n      summary: Channel Cheer\n      message:\n        $ref: '#/components/messages/ChannelCheerEvent'\n\
  \  channel.raid:\n    description: A broadcaster raids another broadcaster's channel.\n    subscribe:\n      operationId: onChannelRaid\n      summary: Channel Raid\n      message:\n        $ref: '#/components/messages/ChannelRaidEvent'\n  channel.ban:\n    description: A viewer is banned or timed out from a channel.\n    subscribe:\n      operationId: onChannelBan\n      summary: Channel Ban\n      message:\n        $ref: '#/components/messages/ChannelBanEvent'\n  channel.unban:\n    description: A viewer is unbanned from a channel.\n    subscribe:\n      operationId: onChannelUnban\n      summary: Channel Unban\n      message:\n        $ref: '#/components/messages/ChannelUnbanEvent'\n  channel.moderator.add:\n    description: A moderator is added to a channel.\n    subscribe:\n      operationId: onChannelModeratorAdd\n      summary: Channel Moderator Add\n      message:\n        $ref: '#/components/messages/ChannelModeratorAddEvent'\n  channel.moderator.remove:\n    description: A moderator\
  \ is removed from a channel.\n    subscribe:\n      operationId: onChannelModeratorRemove\n      summary: Channel Moderator Remove\n      message:\n        $ref: '#/components/messages/ChannelModeratorRemoveEvent'\n  channel.channel_points_custom_reward.add:\n    description: A custom channel points reward is added to a channel.\n    subscribe:\n      operationId: onChannelPointsCustomRewardAdd\n      summary: Channel Points Custom Reward Add\n      message:\n        $ref: '#/components/messages/ChannelPointsCustomRewardEvent'\n  channel.channel_points_custom_reward_redemption.add:\n    description: A viewer redeems a custom channel points reward.\n    subscribe:\n      operationId: onChannelPointsRedemptionAdd\n      summary: Channel Points Redemption Add\n      message:\n        $ref: '#/components/messages/ChannelPointsRedemptionEvent'\n  channel.poll.begin:\n    description: A poll begins on a channel.\n    subscribe:\n      operationId: onChannelPollBegin\n      summary: Channel Poll\
  \ Begin\n      message:\n        $ref: '#/components/messages/ChannelPollEvent'\n  channel.poll.end:\n    description: A poll ends on a channel.\n    subscribe:\n      operationId: onChannelPollEnd\n      summary: Channel Poll End\n      message:\n        $ref: '#/components/messages/ChannelPollEvent'\n  channel.prediction.begin:\n    description: A prediction begins on a channel.\n    subscribe:\n      operationId: onChannelPredictionBegin\n      summary: Channel Prediction Begin\n      message:\n        $ref: '#/components/messages/ChannelPredictionEvent'\n  channel.prediction.end:\n    description: A prediction ends on a channel.\n    subscribe:\n      operationId: onChannelPredictionEnd\n      summary: Channel Prediction End\n      message:\n        $ref: '#/components/messages/ChannelPredictionEvent'\n  channel.hype_train.begin:\n    description: A Hype Train begins on a channel.\n    subscribe:\n      operationId: onHypeTrainBegin\n      summary: Hype Train Begin\n      message:\n\
  \        $ref: '#/components/messages/HypeTrainEvent'\n  channel.hype_train.progress:\n    description: A Hype Train makes progress on a channel.\n    subscribe:\n      operationId: onHypeTrainProgress\n      summary: Hype Train Progress\n      message:\n        $ref: '#/components/messages/HypeTrainEvent'\n  channel.hype_train.end:\n    description: A Hype Train ends on a channel.\n    subscribe:\n      operationId: onHypeTrainEnd\n      summary: Hype Train End\n      message:\n        $ref: '#/components/messages/HypeTrainEndEvent'\n  channel.charity_campaign.donate:\n    description: A user donates to a charity campaign on a channel.\n    subscribe:\n      operationId: onCharityDonation\n      summary: Charity Campaign Donate\n      message:\n        $ref: '#/components/messages/CharityDonationEvent'\n  channel.goal.begin:\n    description: A creator goal begins on a channel.\n    subscribe:\n      operationId: onGoalBegin\n      summary: Goal Begin\n      message:\n        $ref: '#/components/messages/GoalEvent'\n\
  \  channel.goal.progress:\n    description: A creator goal makes progress.\n    subscribe:\n      operationId: onGoalProgress\n      summary: Goal Progress\n      message:\n        $ref: '#/components/messages/GoalEvent'\n  channel.goal.end:\n    description: A creator goal ends on a channel.\n    subscribe:\n      operationId: onGoalEnd\n      summary: Goal End\n      message:\n        $ref: '#/components/messages/GoalEvent'\n  channel.chat.message:\n    description: A chat message is sent in a channel.\n    subscribe:\n      operationId: onChatMessage\n      summary: Chat Message\n      message:\n        $ref: '#/components/messages/ChatMessageEvent'\n  channel.chat.notification:\n    description: A chat notification is sent in a channel (sub, raid, etc.).\n    subscribe:\n      operationId: onChatNotification\n      summary: Chat Notification\n      message:\n        $ref: '#/components/messages/ChatNotificationEvent'\n  stream.online:\n    description: The specified broadcaster starts\
  \ a stream.\n    subscribe:\n      operationId: onStreamOnline\n      summary: Stream Online\n      message:\n        $ref: '#/components/messages/StreamOnlineEvent'\n  stream.offline:\n    description: The specified broadcaster stops a stream.\n    subscribe:\n      operationId: onStreamOffline\n      summary: Stream Offline\n      message:\n        $ref: '#/components/messages/StreamOfflineEvent'\n  user.authorization.grant:\n    description: A user's authorization is granted for an application.\n    subscribe:\n      operationId: onUserAuthorizationGrant\n      summary: User Authorization Grant\n      message:\n        $ref: '#/components/messages/UserAuthorizationGrantEvent'\n  user.authorization.revoke:\n    description: A user's authorization is revoked for an application.\n    subscribe:\n      operationId: onUserAuthorizationRevoke\n      summary: User Authorization Revoke\n      message:\n        $ref: '#/components/messages/UserAuthorizationRevokeEvent'\n  user.update:\n    description:\
  \ A user updates their account.\n    subscribe:\n      operationId: onUserUpdate\n      summary: User Update\n      message:\n        $ref: '#/components/messages/UserUpdateEvent'\n  drop.entitlement.grant:\n    description: A Drops entitlement is granted to a user.\n    subscribe:\n      operationId: onDropEntitlementGrant\n      summary: Drop Entitlement Grant\n      message:\n        $ref: '#/components/messages/DropEntitlementGrantEvent'\ncomponents:\n  messages:\n    ChannelUpdateEvent:\n      name: ChannelUpdateEvent\n      title: Channel Update Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChannelFollowEvent:\n      name: ChannelFollowEvent\n      title: Channel Follow Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChannelSubscribeEvent:\n      name: ChannelSubscribeEvent\n      title: Channel Subscribe Event\n      contentType:\
  \ application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChannelSubscriptionEndEvent:\n      name: ChannelSubscriptionEndEvent\n      title: Channel Subscription End Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChannelSubscriptionGiftEvent:\n      name: ChannelSubscriptionGiftEvent\n      title: Channel Subscription Gift Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChannelSubscriptionMessageEvent:\n      name: ChannelSubscriptionMessageEvent\n      title: Channel Subscription Message Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChannelCheerEvent:\n      name: ChannelCheerEvent\n      title: Channel Cheer Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n\
  \    ChannelRaidEvent:\n      name: ChannelRaidEvent\n      title: Channel Raid Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChannelBanEvent:\n      name: ChannelBanEvent\n      title: Channel Ban Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChannelUnbanEvent:\n      name: ChannelUnbanEvent\n      title: Channel Unban Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChannelModeratorAddEvent:\n      name: ChannelModeratorAddEvent\n      title: Channel Moderator Add Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChannelModeratorRemoveEvent:\n      name: ChannelModeratorRemoveEvent\n      title: Channel Moderator Remove Event\n      contentType: application/json\n      payload:\n        $ref:\
  \ '#/components/schemas/EventSubNotification'\n    ChannelPointsCustomRewardEvent:\n      name: ChannelPointsCustomRewardEvent\n      title: Channel Points Custom Reward Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChannelPointsRedemptionEvent:\n      name: ChannelPointsRedemptionEvent\n      title: Channel Points Redemption Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChannelPollEvent:\n      name: ChannelPollEvent\n      title: Channel Poll Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChannelPredictionEvent:\n      name: ChannelPredictionEvent\n      title: Channel Prediction Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    HypeTrainEvent:\n      name: HypeTrainEvent\n      title:\
  \ Hype Train Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    HypeTrainEndEvent:\n      name: HypeTrainEndEvent\n      title: Hype Train End Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    CharityDonationEvent:\n      name: CharityDonationEvent\n      title: Charity Donation Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    GoalEvent:\n      name: GoalEvent\n      title: Goal Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChatMessageEvent:\n      name: ChatMessageEvent\n      title: Chat Message Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    ChatNotificationEvent:\n      name: ChatNotificationEvent\n      title: Chat Notification\
  \ Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    StreamOnlineEvent:\n      name: StreamOnlineEvent\n      title: Stream Online Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    StreamOfflineEvent:\n      name: StreamOfflineEvent\n      title: Stream Offline Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    UserAuthorizationGrantEvent:\n      name: UserAuthorizationGrantEvent\n      title: User Authorization Grant Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    UserAuthorizationRevokeEvent:\n      name: UserAuthorizationRevokeEvent\n      title: User Authorization Revoke Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    UserUpdateEvent:\n\
  \      name: UserUpdateEvent\n      title: User Update Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n    DropEntitlementGrantEvent:\n      name: DropEntitlementGrantEvent\n      title: Drop Entitlement Grant Event\n      contentType: application/json\n      payload:\n        $ref: '#/components/schemas/EventSubNotification'\n  schemas:\n    EventSubNotification:\n      type: object\n      description: Standard EventSub notification envelope\n      properties:\n        subscription:\n          type: object\n          properties:\n            id:\n              type: string\n              description: Unique subscription ID\n            status:\n              type: string\n              description: Subscription status\n            type:\n              type: string\n              description: The subscription event type\n            version:\n              type: string\n              description: Version of the subscription\
  \ type\n            condition:\n              type: object\n              additionalProperties:\n                type: string\n              description: Conditions the subscription was created with\n            transport:\n              type: object\n              properties:\n                method:\n                  type: string\n                  enum: [webhook, websocket, conduit]\n                callback:\n                  type: string\n            cost:\n              type: integer\n            created_at:\n              type: string\n              format: date-time\n        event:\n          type: object\n          description: The event-specific payload (varies by subscription type)\n          additionalProperties: true\n    ChannelUpdatePayload:\n      type: object\n      properties:\n        broadcaster_user_id:\n          type: string\n        broadcaster_user_login:\n          type: string\n        broadcaster_user_name:\n          type: string\n        title:\n       \
  \   type: string\n        language:\n          type: string\n        category_id:\n          type: string\n        category_name:\n          type: string\n        content_classification_labels:\n          type: array\n          items:\n            type: string\n    ChannelFollowPayload:\n      type: object\n      properties:\n        user_id:\n          type: string\n        user_login:\n          type: string\n        user_name:\n          type: string\n        broadcaster_user_id:\n          type: string\n        broadcaster_user_login:\n          type: string\n        broadcaster_user_name:\n          type: string\n        followed_at:\n          type: string\n          format: date-time\n    ChannelSubscribePayload:\n      type: object\n      properties:\n        user_id:\n          type: string\n        user_login:\n          type: string\n        user_name:\n          type: string\n        broadcaster_user_id:\n          type: string\n        broadcaster_user_login:\n          type:\
  \ string\n        broadcaster_user_name:\n          type: string\n        tier:\n          type: string\n          enum: ['1000', '2000', '3000']\n        is_gift:\n          type: boolean\n    ChannelCheerPayload:\n      type: object\n      properties:\n        is_anonymous:\n          type: boolean\n        user_id:\n          type: string\n          nullable: true\n        user_login:\n          type: string\n          nullable: true\n        user_name:\n          type: string\n          nullable: true\n        broadcaster_user_id:\n          type: string\n        broadcaster_user_login:\n          type: string\n        broadcaster_user_name:\n          type: string\n        message:\n          type: string\n        bits:\n          type: integer\n    ChannelRaidPayload:\n      type: object\n      properties:\n        from_broadcaster_user_id:\n          type: string\n        from_broadcaster_user_login:\n          type: string\n        from_broadcaster_user_name:\n          type: string\n\
  \        to_broadcaster_user_id:\n          type: string\n        to_broadcaster_user_login:\n          type: string\n        to_broadcaster_user_name:\n          type: string\n        viewers:\n          type: integer\n    ChannelBanPayload:\n      type: object\n      properties:\n        user_id:\n          type: string\n        user_login:\n          type: string\n        user_name:\n          type: string\n        broadcaster_user_id:\n          type: string\n        broadcaster_user_login:\n          type: string\n        broadcaster_user_name:\n          type: string\n        moderator_user_id:\n          type: string\n        moderator_user_login:\n          type: string\n        moderator_user_name:\n          type: string\n        reason:\n          type: string\n        banned_at:\n          type: string\n          format: date-time\n        ends_at:\n          type: string\n          format: date-time\n          nullable: true\n        is_permanent:\n          type: boolean\n\
  \    StreamOnlinePayload:\n      type: object\n      properties:\n        id:\n          type: string\n        broadcaster_user_id:\n          type: string\n        broadcaster_user_login:\n          type: string\n        broadcaster_user_name:\n          type: string\n        type:\n          type: string\n          enum: [live, playlist, watch_party, premiere, rerun]\n        started_at:\n          type: string\n          format: date-time\n    StreamOfflinePayload:\n      type: object\n      properties:\n        broadcaster_user_id:\n          type: string\n        broadcaster_user_login:\n          type: string\n        broadcaster_user_name:\n          type: string\n    DropEntitlementGrantPayload:\n      type: object\n      properties:\n        id:\n          type: string\n        data:\n          type: array\n          items:\n            type: object\n            properties:\n              organization_id:\n                type: string\n              category_id:\n            \
  \    type: string\n              category_name:\n                type: string\n              campaign_id:\n                type: string\n              user_id:\n                type: string\n              user_name:\n                type: string\n              user_login:\n                type: string\n              entitlement_id:\n                type: string\n              benefit_id:\n                type: string\n              created_at:\n                type: string\n                format: date-time\n    WebSocketSessionMessage:\n      type: object\n      description: WebSocket session welcome message\n      properties:\n        metadata:\n          type: object\n          properties:\n            message_id:\n              type: string\n            message_type:\n              type: string\n              enum: [session_welcome, session_keepalive, notification, session_reconnect, revocation]\n            message_timestamp:\n              type: string\n              format: date-time\n\
  \        payload:\n          type: object\n          properties:\n            session:\n              type: object\n              properties:\n                id:\n                  type: string\n                status:\n                  type: string\n                connected_at:\n                  type: string\n                  format: date-time\n                keepalive_timeout_seconds:\n                  type: integer\n                reconnect_url:\n                  type: string\n                  nullable: true\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/asyncapi/twitch-eventsub-asyncapi.yml
spec_file: asyncapi/twitch-eventsub-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/twitch/refs/heads/main/asyncapi/twitch-eventsub-asyncapi.yml
tags:
- Entertainment
- Gaming
- Live Video
- Streaming
- Video
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
