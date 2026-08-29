You are operating in Senior Engineering Team Mode.

Build the production-ready backend for pricing, fare calculation, surge pricing, promotions, coupons, payments, wallets, refunds, receipts, driver earnings, incentives, and driver payouts for an enterprise-scale global ride-hailing and mobility platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

The backend must follow the approved Uber-like architecture, domain boundaries, database ownership, trip architecture, dispatch architecture, driver architecture, location architecture, payment architecture, security model, event architecture, queue architecture, and Project Index.

Do not redesign the architecture.

Do not generate frontend code.

Do not generate mobile code.

Do not generate infrastructure implementation code.

Do not generate Terraform.

Do not generate Kubernetes manifests.

Do not generate CI/CD workflows.

────────────────────────────────────────

MISSION

Implement the production-ready backend required for:

• Fare estimation
• Fare calculation
• Pricing rules
• Pricing versions
• Surge pricing
• Dynamic pricing
• Promotions
• Coupon codes
• Discount eligibility
• Payment methods
• Payment authorization
• Payment capture
• Payment failure
• Payment retries
• Refunds
• Partial refunds
• Wallets
• Promotional credits
• Trip receipts
• Driver earnings
• Driver incentives
• Bonuses
• Tips
• Driver balances
• Driver payouts
• Payout status
• Financial reconciliation

The implementation must support:

• Hundreds of millions of riders
• Millions of drivers
• Large trip volumes
• Multiple currencies
• Multiple regions
• Regional pricing rules
• High payment traffic
• High payout volume
• Large promotion campaigns
• Strong financial correctness
• Full auditability
• Idempotent financial operations

────────────────────────────────────────

TECHNOLOGY STACK

Backend:

• Node.js
• NestJS
• TypeScript

Database:

• PostgreSQL
• Prisma ORM

Cache:

• Redis

Event Streaming:

• Kafka or Redpanda

Background Processing:

• BullMQ

Payments:

• Stripe or approved payment abstraction

Object Storage:

• AWS S3-compatible storage for receipts/reports where appropriate

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

Testing:

• Jest
• Supertest
• Integration and financial-consistency testing tools

────────────────────────────────────────

IMPLEMENTATION RULES

Never generate pseudo-code.

Never generate placeholders.

Never generate TODO comments.

Never omit implementations.

Never say:

- "implement similarly"
- "left as an exercise"
- "for brevity"
- "remaining code omitted"

Every generated file must be complete.

Every generated file must compile.

Never regenerate unchanged files.

Only modify existing files when required.

Use strict TypeScript.

Use dependency injection.

Keep controllers thin.

Keep financial business logic outside controllers.

Use repositories for persistence.

Use DTOs for API contracts.

Use centralized validation.

Use centralized error handling.

Use structured logging.

Every financial mutation must be idempotent.

Every financial state transition must be auditable.

Never use floating-point arithmetic for monetary calculations.

────────────────────────────────────────

DOMAIN OWNERSHIP

Maintain explicit boundaries between:

• Pricing
• Fare calculation
• Surge
• Promotions
• Payments
• Wallet
• Refunds
• Receipts
• Driver earnings
• Incentives
• Payouts

Do not combine:

• Trip state with payment state
• Payment state with driver payout state
• Promotion state with wallet ledger
• Surge state with final fare records
• Redis state with financial truth

────────────────────────────────────────

PRICING DOMAIN

Implement configurable pricing.

Support:

• Base fare
• Distance rate
• Time rate
• Minimum fare
• Booking/service fee
• Tolls
• Taxes
• Category surcharge
• Accessibility-related pricing where legally permitted
• Surge multiplier
• Promotions
• Other regional fees

Pricing must be versioned.

────────────────────────────────────────

PRICING RULES

Create configurable pricing rules based on:

• Region
• City
• Ride category
• Time
• Distance
• Demand conditions
• Special events
• Vehicle type
• Regulatory constraints

Rules must be:

• Versioned
• Effective-dated
• Auditable
• Testable

Do not hard-code city pricing directly in application logic.

────────────────────────────────────────

PRICING VERSION

Every fare calculation must reference:

• Pricing version
• Region
• Category
• Currency
• Calculation timestamp
• Applied rules

Historical trips must remain reconstructable even after pricing changes.

────────────────────────────────────────

FARE ESTIMATION

Implement:

• Estimate request
• Route context
• Distance
• Duration
• Pricing rules
• Surge
• Promotions
• Taxes where applicable

Return:

• Estimated minimum
• Estimated maximum where appropriate
• Currency
• Fare components
• Pricing version
• Expiration

Do not guarantee an estimate will equal the final fare when trip conditions change.

────────────────────────────────────────

FARE CALCULATION

At trip completion:

• Determine actual distance
• Determine actual duration
• Apply pricing rules
• Apply applicable surge
• Apply promotions
• Apply tolls
• Apply taxes
• Apply adjustments

Generate a deterministic final fare.

────────────────────────────────────────

FARE SNAPSHOT

Persist:

• Pricing version
• Base fare
• Time component
• Distance component
• Fees
• Tolls
• Taxes
• Surge multiplier
• Promotion discounts
• Credits
• Final amount
• Currency
• Calculation timestamp

The resulting fare must remain immutable except through auditable adjustment workflows.

────────────────────────────────────────

MONEY HANDLING

Use integer minor units or an approved decimal strategy.

Never use JavaScript floating-point numbers as the source of truth for money.

Define:

• Currency
• Minor-unit precision
• Rounding mode
• Tax rounding
• Discount rounding

Ensure calculations are deterministic.

────────────────────────────────────────

SURGE PRICING

Implement dynamic surge pricing architecture.

Inputs may include:

• Active requests
• Available drivers
• Supply/demand ratio
• Service area
• Time
• Ride category
• Special events

Output:

• Surge multiplier
• Effective area
• Effective time
• Pricing version
• Confidence metadata where useful

────────────────────────────────────────

SURGE STABILITY

Prevent unstable surge fluctuations.

Support:

• Minimum duration
• Update intervals
• Smoothing
• Hysteresis
• Floor
• Ceiling
• Regional caps
• Regulatory constraints

Do not allow rapid oscillation based on noisy inputs.

────────────────────────────────────────

SURGE ZONES

Define:

• Surge zone
• Region
• Spatial boundary
• Category
• Multiplier
• Effective time

Use PostGIS for durable spatial definitions.

Use Redis or derived state for low-latency operational lookup.

────────────────────────────────────────

SURGE EVENTS

Publish:

• SurgeCreated
• SurgeUpdated
• SurgeExpired
• PricingRuleChanged

Consumers must be idempotent.

────────────────────────────────────────

PROMOTIONS

Implement:

• Campaigns
• Promo codes
• Eligibility
• Redemption
• Usage limits
• Customer limits
• Region
• Category
• Start/end date
• Minimum fare
• Maximum discount

Support promotion states:

• Draft
• Active
• Paused
• Expired
• Exhausted
• Archived

────────────────────────────────────────

PROMOTION ELIGIBILITY

Evaluate:

• User eligibility
• Region
• Ride category
• First-ride status
• Usage count
• Campaign status
• Time window
• Minimum fare
• Maximum discount

Do not rely only on frontend eligibility.

────────────────────────────────────────

PROMOTION REDEMPTION

Ensure:

• Single-use or configured-use rules
• Atomic redemption
• Duplicate-request protection
• Idempotency
• Race-condition safety

A promotion must not be redeemed twice because of concurrent requests.

────────────────────────────────────────

PROMOTION STACKING

Define explicit policies for:

• Multiple promotions
• Coupon + wallet
• Promotion + tip
• Promotion + surge

Prevent unapproved discount combinations.

────────────────────────────────────────

PAYMENT METHODS

Support a payment abstraction for:

• Cards
• Wallet
• Business payment
• Cash where supported

Store provider references rather than unnecessary raw payment data.

────────────────────────────────────────

PAYMENT FLOW

Implement:

Ride Request
→ Payment Method Validation
→ Authorization/Pre-Authorization
→ Trip
→ Final Fare
→ Capture
→ Receipt

Handle:

• Authorization failure
• Authentication required
• Provider timeout
• Capture failure
• Retry
• Reconciliation

────────────────────────────────────────

PAYMENT STATE MACHINE

Support states:

• Created
• Requires Action
• Authorized
• Processing
• Capturing
• Captured
• Failed
• Canceled
• Partially Refunded
• Refunded
• Disputed

Define all valid and invalid transitions.

────────────────────────────────────────

PAYMENT IDEMPOTENCY

Every externally triggered payment operation must support:

• Idempotency key
• Operation scope
• Stored result
• Replay behavior
• Conflict handling

Prevent:

• Duplicate authorization
• Duplicate capture
• Duplicate refund

────────────────────────────────────────

STRIPE ABSTRACTION

Implement a provider-neutral payment interface.

Support provider operations:

• Customer
• Payment method
• Payment authorization
• Capture
• Refund
• Payment status
• Webhook

Core domains must not depend directly on Stripe-specific classes.

────────────────────────────────────────

PAYMENT WEBHOOKS

Implement:

• Signature verification
• Event persistence
• Provider event ID uniqueness
• Duplicate detection
• Idempotent handling
• Retry
• Error recording
• Reconciliation

Never trust client-side payment state as final.

────────────────────────────────────────

REFUNDS

Implement:

• Full refund
• Partial refund
• Cancellation refund
• Support refund
• Promotion-adjusted refund

Support refund states:

• Requested
• Processing
• Succeeded
• Failed
• Canceled

Track:

• Amount
• Currency
• Reason
• Actor
• Provider reference
• Timestamp

────────────────────────────────────────

REFUND RULES

A refund cannot:

• Exceed captured amount
• Be duplicated
• Produce invalid wallet balance
• Create unsupported negative financial balances

Use transactions for internal state.

Use provider references for external operations.

────────────────────────────────────────

WALLET DOMAIN

Implement wallet architecture supporting:

• Promotional credits
• Refund credits
• Business credits
• Stored-value credits where legally supported

Use an immutable ledger.

────────────────────────────────────────

WALLET LEDGER

Each entry should include:

• Entry ID
• Wallet ID
• Type
• Amount
• Currency
• Direction
• Source
• Reference
• Expiration
• Created timestamp

Never update historical ledger entries.

Create compensating entries for corrections.

────────────────────────────────────────

WALLET BALANCE

Support:

• Available balance
• Pending balance
• Expiring balance

Balance may be projected from ledger data and optionally cached.

The ledger remains authoritative.

────────────────────────────────────────

WALLET CONCURRENCY

Prevent:

• Double-spending
• Concurrent negative balances
• Duplicate credit
• Duplicate debit

Use:

• Database transactions
• Row/version checks
• Idempotency

────────────────────────────────────────

RECEIPTS

Generate receipts for completed trips.

Include:

• Trip ID
• Date/time
• Pickup
• Dropoff
• Driver
• Vehicle
• Fare components
• Surge
• Promotions
• Taxes
• Tip
• Payment method
• Total
• Currency

Receipt data must remain consistent with the final financial record.

────────────────────────────────────────

RECEIPT GENERATION

Support:

• Synchronous metadata retrieval
• Asynchronous document generation
• Secure storage
• Download authorization
• Expiration
• Regeneration

Use BullMQ for expensive document generation.

Do not expose public S3 object URLs unnecessarily.

────────────────────────────────────────

DRIVER EARNINGS

Implement:

• Trip earnings
• Base earnings
• Driver adjustments
• Tips
• Incentives
• Bonuses
• Fees
• Refund effects

Create an immutable earnings ledger.

────────────────────────────────────────

EARNINGS CALCULATION

Define a deterministic earnings calculation.

Inputs may include:

• Final fare
• Driver compensation rule
• Category
• Region
• Incentive
• Tip
• Adjustments

Persist the calculation version.

Do not depend on mutable future pricing rules to reconstruct old earnings.

────────────────────────────────────────

DRIVER INCENTIVES

Support:

• Trip-count incentives
• Time-window incentives
• Geographic incentives
• Guaranteed earnings
• Bonus campaigns

Define:

• Eligibility
• Progress
• Completion
• Expiration
• Payout amount
• Campaign version

────────────────────────────────────────

INCENTIVE PROGRESS

Track progress without requiring expensive transactional writes for every event.

Use event-driven aggregation where practical.

Ensure final qualification is authoritative and reproducible.

────────────────────────────────────────

DRIVER BALANCES

Separate:

• Pending earnings
• Available earnings
• Paid earnings
• Held amounts
• Adjustments

Do not use a cached Redis balance as financial truth.

────────────────────────────────────────

PAYOUTS

Implement:

• Payout creation
• Scheduled payouts
• Instant payouts where supported
• Payout provider reference
• Payout state
• Failure
• Retry
• Reversal
• Reconciliation

Payout states:

• Requested
• Pending
• Processing
• Succeeded
• Failed
• Reversed
• Canceled

────────────────────────────────────────

PAYOUT ELIGIBILITY

Before payout validate:

• Available driver balance
• Driver status
• Payout method
• Risk holds
• Minimum payout
• Regional eligibility

Prevent payout of:

• Pending earnings
• Held earnings
• Already-paid earnings

────────────────────────────────────────

PAYOUT IDEMPOTENCY

Every payout request must include:

• Idempotency key
• Driver
• Amount
• Currency
• Payout method reference

Prevent duplicate payouts.

────────────────────────────────────────

PAYOUT RECONCILIATION

Compare:

• Internal payout
• Provider payout
• Driver balance
• Earnings ledger

Detect:

• Missing payout
• Duplicate payout
• Incorrect provider status
• Amount mismatch

Reconciliation must be safe and auditable.

────────────────────────────────────────

TIPS

Support:

• Tip amount
• Tip eligibility
• Tip window
• Driver allocation
• Tip receipt
• Tip payout

Prevent duplicate tips.

Tip records must remain associated with the originating trip.

────────────────────────────────────────

FINANCIAL EVENTS

Publish:

• FareEstimated
• FareCalculated
• PricingSnapshotCreated
• SurgeUpdated
• PromotionCreated
• PromotionRedeemed
• PaymentAuthorized
• PaymentCaptureRequested
• PaymentCaptured
• PaymentFailed
• PaymentDisputed
• RefundRequested
• RefundSucceeded
• RefundFailed
• WalletCreditCreated
• WalletDebitCreated
• DriverEarningCreated
• IncentiveProgressUpdated
• IncentiveCompleted
• PayoutRequested
• PayoutSucceeded
• PayoutFailed
• PayoutReversed
• TipCreated
• ReceiptGenerated

All financially relevant consumers must be idempotent.

────────────────────────────────────────

BACKGROUND JOBS

Implement BullMQ jobs for:

• Payment reconciliation
• Refund reconciliation
• Payout processing
• Payout reconciliation
• Promotion expiration
• Promotion campaign cleanup
• Surge expiration
• Incentive settlement
• Receipt generation
• Receipt regeneration
• Wallet expiration
• Financial reconciliation

Every job must support:

• Retry
• Backoff
• Timeout
• Idempotency
• Dead-letter handling
• Metrics
• Structured logging

────────────────────────────────────────

DATABASE

Implement Prisma models and migrations for:

• PricingRule
• PricingVersion
• FareEstimate
• Fare
• FareComponent
• SurgeZone
• SurgeSnapshot
• PromotionCampaign
• PromotionCode
• PromotionRedemption
• PaymentMethodReference
• Payment
• PaymentAttempt
• PaymentWebhookEvent
• Refund
• Wallet
• WalletLedgerEntry
• Receipt
• ReceiptGenerationJob
• DriverEarning
• DriverEarningLedgerEntry
• IncentiveCampaign
• IncentiveEligibility
• IncentiveProgress
• DriverBalance
• DriverPayout
• PayoutAttempt
• FinancialReconciliationReference
• Tip

Use:

• Primary keys
• Foreign keys
• Unique constraints
• Composite indexes
• Version fields
• Currency fields
• Amount in minor units or approved decimal representation
• Timestamps

────────────────────────────────────────

DATABASE TRANSACTIONS

Use transactions for:

• Promotion redemption
• Wallet debit/credit
• Earnings creation
• Balance changes
• Payout state transitions
• Refund state transitions
• Final fare creation
• Payment-internal state transitions

Do not use database transactions across external payment-provider calls.

Use:

• Idempotency
• Outbox
• Reconciliation

────────────────────────────────────────

API

Implement production-ready APIs.

PRICING

• Fare estimate
• Pricing details
• Available categories

PROMOTIONS

• Validate promo
• Redeem
• Get promotion status

PAYMENTS

• List payment methods
• Add payment method reference
• Remove payment method
• Create payment authorization
• Get payment state

REFUNDS

• Request refund where authorized
• Get refund state

WALLET

• Get balance
• Get ledger
• Redeem credit where allowed

RECEIPTS

• Get receipt
• Generate receipt
• Download receipt

DRIVER EARNINGS

• Get earnings
• Get earnings breakdown
• Get balance
• Get incentives

PAYOUTS

• Create payout
• Get payout
• List payouts
• Get payout methods where supported

ADMIN

• Pricing rules
• Surge configuration
• Promotions
• Payments
• Refunds
• Wallet adjustments
• Earnings adjustments
• Payout investigation

Every endpoint must implement:

• Authentication
• Authorization
• Validation
• Rate limiting
• Idempotency where appropriate
• OpenAPI
• Consistent errors
• Audit where required

────────────────────────────────────────

SECURITY

Protect against:

• Payment manipulation
• Duplicate charging
• Duplicate refunds
• Wallet double-spending
• Promotion abuse
• Payout fraud
• Driver balance manipulation
• Unauthorized financial adjustments
• Webhook spoofing
• Financial record tampering
• Admin privilege escalation

Sensitive financial operations require strong authorization.

────────────────────────────────────────

AUDIT

Audit:

• Pricing changes
• Surge changes
• Promotion changes
• Payment adjustments
• Refunds
• Wallet adjustments
• Earnings adjustments
• Payout actions
• Administrative financial operations

Audit records must be immutable.

────────────────────────────────────────

OBSERVABILITY

Instrument:

• Fare estimation
• Fare calculation
• Surge updates
• Promotion validation
• Payment authorization
• Payment capture
• Refunds
• Wallet operations
• Earnings
• Incentives
• Payouts
• Receipt generation
• Reconciliation

Track:

• Fare latency
• Payment success
• Payment failure
• Refund success
• Promotion redemption rate
• Wallet errors
• Payout success
• Payout failure
• Reconciliation mismatch
• Queue depth

Never log:

• Full card data
• Payment credentials
• Provider secrets
• Sensitive wallet data unnecessarily

────────────────────────────────────────

TESTING

UNIT TESTS

Test:

• Pricing rules
• Fare calculation
• Rounding
• Surge calculation
• Promotion eligibility
• Promotion stacking
• Wallet ledger
• Wallet balance
• Earnings calculation
• Incentive qualification
• Payout eligibility
• Refund rules
• Payment state machine

FINANCIAL TESTS

Test exact monetary arithmetic.

Test:

• Currency conversion boundaries where applicable
• Rounding
• Tax calculation
• Discounts
• Surge
• Refunds
• Wallet credits
• Wallet debits

INTEGRATION TESTS

Test:

• PostgreSQL
• Redis
• Kafka
• BullMQ
• Payment provider abstraction
• Object storage

PAYMENT TESTS

Test:

• Authorization
• Capture
• Failure
• Retry
• Webhook duplicate
• Out-of-order webhook
• Refund
• Partial refund
• Reconciliation

WALLET TESTS

Test:

• Concurrent debit
• Concurrent credit
• Double-spend
• Duplicate request
• Expiration
• Compensating entries

PROMOTION TESTS

Test:

• Concurrent redemption
• Usage limits
• Customer limits
• Expiration
• Stacking

PAYOUT TESTS

Test:

• Duplicate payout
• Insufficient balance
• Provider failure
• Provider timeout
• Reconciliation
• Reversal

CONCURRENCY TESTS

Test:

• Two refunds
• Two promotion redemptions
• Two wallet debits
• Two payouts
• Concurrent fare finalization

SECURITY TESTS

Test:

• Financial IDOR
• Unauthorized refunds
• Unauthorized wallet access
• Promotion abuse
• Payout manipulation
• Webhook spoofing
• Admin escalation

PERFORMANCE TESTS

Test:

• Fare estimation
• Payment creation
• Wallet lookup
• Earnings retrieval
• Payout processing
• Promotion validation

────────────────────────────────────────

DOCUMENTATION

Generate:

• Pricing architecture
• Fare engine
• Pricing versioning
• Surge architecture
• Promotion architecture
• Payment architecture
• Payment state machine
• Webhooks
• Refunds
• Wallet architecture
• Wallet ledger
• Receipts
• Driver earnings
• Incentives
• Payouts
• Reconciliation
• Financial event catalog
• Financial queue catalog
• API contracts
• Database schema
• Security model
• Audit model
• Testing strategy

────────────────────────────────────────

PROJECT INDEX

Update the backend Project Index with:

• Pricing modules
• Fare modules
• Surge modules
• Promotion modules
• Payment modules
• Refund modules
• Wallet modules
• Receipt modules
• Earnings modules
• Incentive modules
• Payout modules
• Financial reconciliation
• Database objects
• Migrations
• API endpoints
• Events
• Queues
• Workers
• Redis usage
• External provider integrations
• Audit
• Security
• Tests
• Generated files
• Remaining work
• Current milestone
• Dependencies

────────────────────────────────────────

IMPLEMENTATION MILESTONES

BACKEND MILESTONE 41

Pricing rules, pricing versions, fare estimation, fare components, and deterministic money calculations.

BACKEND MILESTONE 42

Final fare calculation, fare snapshots, trip-completion integration, taxes, tolls, and financial auditability.

BACKEND MILESTONE 43

Surge pricing, surge zones, surge snapshots, dynamic updates, smoothing, caps, and regional rules.

BACKEND MILESTONE 44

Promotion campaigns, promo codes, eligibility, redemption, usage limits, stacking, and abuse protection.

BACKEND MILESTONE 45

Payment methods, payment intents, authorization, capture, payment state machine, and provider abstraction.

BACKEND MILESTONE 46

Payment webhooks, retries, idempotency, refunds, partial refunds, disputes, and reconciliation.

BACKEND MILESTONE 47

Wallets, immutable ledger, wallet concurrency, promotional credits, refund credits, and expiration.

BACKEND MILESTONE 48

Driver earnings, tips, incentives, driver balances, compensation rules, and earnings ledger.

BACKEND MILESTONE 49

Driver payouts, payout provider integration, payout reconciliation, receipts, financial background jobs, and audit.

BACKEND MILESTONE 50

Financial security hardening, concurrency testing, monetary-accuracy testing, reconciliation testing, performance testing, and production readiness.

Each milestone should contain approximately 20–40 files where practical.

Every milestone must compile before proceeding.

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never truncate code.

Never summarize source code instead of generating it.

Never generate pseudo-code.

Never generate placeholders.

Never generate TODO implementations.

When modifying an existing file:

1. Provide the exact file path.
2. State why it must change.
3. Provide the complete updated file.

Never regenerate unchanged files.

────────────────────────────────────────

SCOPE RESTRICTION

This volume covers:

• Pricing
• Fare estimates
• Fare calculation
• Pricing versions
• Surge
• Surge zones
• Promotions
• Coupon codes
• Payment methods
• Payment authorization
• Payment capture
• Payment webhooks
• Refunds
• Wallets
• Wallet ledger
• Receipts
• Driver earnings
• Tips
• Driver incentives
• Driver balances
• Driver payouts
• Financial reconciliation
• Financial events
• Related queues and workers

Do not implement complete:

• Ratings
• Reviews
• Messaging
• Notifications business logic
• Safety
• Fraud platform
• Support
• Business accounts
• Analytics platform
• Administration UI
• Frontend
• Mobile
• Infrastructure

Those belong to later implementation volumes.

────────────────────────────────────────

QUALITY BAR

Treat all financial systems as mission-critical.

Assume:

• Hundreds of millions of riders
• Millions of drivers
• Large trip volumes
• High payment traffic
• High payout traffic
• Large promotion campaigns
• Multiple currencies
• Multiple regions
• Regional tax and pricing rules
• Strict financial audit requirements
• Strict security requirements

Prioritize:

• Financial correctness
• Idempotency
• Auditability
• Deterministic calculations
• Exact monetary arithmetic
• Concurrency safety
• Reconciliation
• Security
• Reliability
• Scalability
• Observability
• Production readiness
