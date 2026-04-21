---
channels:
- description: The merchant's webhook endpoint that receives HTTP POST notifications from Braintree. All event types are delivered to the same configured URL. The bt_payload contains a Base64-encoded, signed XML document with the event details. Merchants must verify the bt_signature against the payload using their private API key before processing.
  name: /webhook
  operation: publish
  operation_id: receiveBraintreeWebhook
  summary: Receive a Braintree webhook notification
description: Braintree Webhooks deliver automated HTTP POST notifications to a merchant-configured destination URL when specific events occur within the payment gateway. Webhook notifications are triggered by transaction settlements, subscription lifecycle changes, dispute events, disbursements, sub-merchant account updates, and other gateway events. Each notification payload is sent as a form-encoded POST with a bt_signature field and a bt_payload field, where the payload is a Base64-encoded signed XML document. Merchants must verify the signature using their API keys before processing the payload. Webhooks are configured in the Braintree Control Panel by specifying a destination URL and selecting the event types to monitor.
layout: asyncapi
messages:
- description: Sent when a subscription advances to its next billing cycle and the associated transaction is successfully authorized. Also sent when a mid-cycle upgrade generates a prorated charge. The notification payload includes the full subscription object with up to 20 recent transactions.
  name: SubscriptionChargedSuccessfully
  summary: A subscription billing cycle completed with a successful charge.
  title: Subscription Charged Successfully
- description: Sent when a subscription billing cycle charge fails, such as when the customer's payment method is declined. The subscription transitions to Past Due status. The notification includes the subscription object with the failed transaction.
  name: SubscriptionChargedUnsuccessfully
  summary: A subscription billing cycle charge attempt failed.
  title: Subscription Charged Unsuccessfully
- description: Sent when a subscription's first authorized transaction is created, or when a subscription transitions from Past Due back to Active status. Indicates the subscription is in good standing and billing normally.
  name: SubscriptionWentActive
  summary: A subscription transitioned to Active status.
  title: Subscription Went Active
- description: Sent when a subscription fails to charge successfully and moves from Active to Past Due status. Merchants should use this event to notify customers and prompt them to update their payment method.
  name: SubscriptionWentPastDue
  summary: A subscription transitioned from Active to Past Due status.
  title: Subscription Went Past Due
- description: Sent when a subscription completes all of its configured billing cycles and expires. The subscription status transitions to Expired. No further charges will be made. Merchants may create a new subscription to continue billing.
  name: SubscriptionExpired
  summary: A subscription reached its configured number of billing cycles.
  title: Subscription Expired
- description: Sent when a subscription is canceled either by the merchant via the API or Control Panel. The subscription status transitions to Canceled and no further charges will be made.
  name: SubscriptionCanceled
  summary: A subscription was canceled.
  title: Subscription Canceled
- description: Sent when a subscription's trial period concludes. This event fires before the first billing charge occurs, allowing merchants to send advance notice to customers that billing is about to begin.
  name: SubscriptionTrialEnded
  summary: A subscription's trial period ended.
  title: Subscription Trial Ended
- description: Sent when a subscription's billing cycle is skipped because the customer has a credit balance from previous add-ons or discounts that covers the entire cost of the subscription for that cycle.
  name: SubscriptionBillingSkipped
  summary: A subscription billing cycle was skipped due to a zero or negative balance.
  title: Subscription Billing Skipped
- description: Sent when an ACH or SEPA Direct Debit transaction completes settlement. This webhook fires after the funds have moved. Applicable specifically to ACH and SEPA Direct Debit sale and refund transactions where settlement is asynchronous.
  name: TransactionSettled
  summary: A transaction settled successfully.
  title: Transaction Settled
- description: Sent when settlement is declined for an ACH or SEPA Direct Debit transaction. May also fire after a transaction_settled event if the customer's bank returns the funds after initial settlement. The original transaction status updates to settlement_declined.
  name: TransactionSettlementDeclined
  summary: Settlement for a transaction was declined.
  title: Transaction Settlement Declined
- description: Sent when a cardholder or issuing bank initiates a chargeback or retrieval against one of the merchant's transactions. The notification includes the dispute object with the associated transaction, disputed amount, reason, and reply-by deadline.
  name: DisputeOpened
  summary: A new dispute was opened against a transaction.
  title: Dispute Opened
- description: Sent when a dispute is resolved in the merchant's favor, meaning the funds are returned to the merchant. The dispute status transitions to Won.
  name: DisputeWon
  summary: A dispute was resolved in the merchant's favor.
  title: Dispute Won
- description: Sent when a dispute is resolved in the cardholder's favor, meaning the merchant loses the disputed funds. The dispute status transitions to Lost.
  name: DisputeLost
  summary: A dispute was resolved in the cardholder's favor.
  title: Dispute Lost
- description: Sent when a merchant explicitly accepts a dispute without contesting it. The dispute status transitions to Accepted and the funds are surrendered to the cardholder.
  name: DisputeAccepted
  summary: A dispute was accepted by the merchant.
  title: Dispute Accepted
- description: Sent when a dispute is automatically accepted because the reply-by deadline passed without the merchant submitting a response or evidence. The dispute status transitions to Accepted.
  name: DisputeAutoAccepted
  summary: A dispute was automatically accepted after the reply deadline passed.
  title: Dispute Auto-Accepted
- description: Sent when the merchant submits evidence to contest a dispute and the dispute transitions to the Disputed status, indicating it is being reviewed by the card network.
  name: DisputeDisputed
  summary: Evidence was submitted and the dispute is under review.
  title: Dispute Disputed
- description: Sent when a dispute expires without being resolved or responded to within the allowed timeframe. The dispute status transitions to Expired.
  name: DisputeExpired
  summary: A dispute expired without resolution.
  title: Dispute Expired
- description: Sent when a dispute enters an internal review state with PayPal. This status indicates Braintree or PayPal is actively investigating the dispute before it is presented to the card network.
  name: DisputeUnderReview
  summary: A dispute is under internal review with PayPal.
  title: Dispute Under Review
- description: Sent once per merchant account per day when Braintree sends a disbursement to the merchant's bank account. Applicable only to Braintree-funded merchant accounts. The notification includes a disbursement object with the total amount and transaction count.
  name: Disbursement
  summary: Funds were disbursed to the merchant's bank account.
  title: Disbursement
- description: Deprecated. Sent when a transaction is marked for disbursement from Braintree's bank account to the merchant. This event type is superseded by the Disbursement event and is only sent for legacy Braintree-funded merchant accounts.
  name: TransactionDisbursed
  summary: A transaction was marked for disbursement. Deprecated in favor of the Disbursement event.
  title: Transaction Disbursed
- description: Sent when a sub-merchant account created through the Braintree Marketplace API completes underwriting review and is approved for payment processing. The notification includes the merchant account object for the approved sub-merchant.
  name: SubMerchantAccountApproved
  summary: A Braintree Marketplace sub-merchant account was approved.
  title: Sub-Merchant Account Approved
- description: Sent when a sub-merchant account created through the Braintree Marketplace API is declined during underwriting review. The notification includes the merchant account object and the reason for the decline.
  name: SubMerchantAccountDeclined
  summary: A Braintree Marketplace sub-merchant account application was declined.
  title: Sub-Merchant Account Declined
name: Braintree Webhooks
provider_name: braintree
provider_slug: braintree
servers:
- description: The merchant-configured HTTPS endpoint that receives webhook notifications from Braintree. The URL is set in the Braintree Control Panel and must be publicly accessible.
  name: merchantServer
  protocol: https
  url: '{webhookDestinationUrl}'
slug: braintree-webhooks-asyncapi
spec_file: asyncapi/braintree-webhooks-asyncapi.yml
spec_url: https://raw.githubusercontent.com/api-evangelist/braintree/refs/heads/main/asyncapi/braintree-webhooks-asyncapi.yml
tags:
- AsyncAPI
- Webhooks
- Events
version: '1.0'
---
