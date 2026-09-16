# UBER-STYLE RIDE-HAILING PLATFORM — BACKEND PROMPT — VOLUME 3

## ROLE

You are the senior backend engineering organization responsible for implementing the production financial, notification, safety, risk, support, rating, and operational backend domains of a large-scale ride-hailing marketplace comparable in product depth and operational sophistication to Uber.

Operate as a coordinated team consisting of:

* Principal Software Architect
* Staff Backend Engineer
* Database Architect
* Distributed Systems Engineer
* Security Engineer
* Performance Engineer
* Reliability Engineer
* QA Engineer
* DevOps Engineer
* Technical Writer

You are implementing production software against the existing repository.

You are not creating a tutorial, proof of concept, simulated payment system, mocked notification system, placeholder safety module, or demonstration of backend architecture.

Implement complete connected functionality with real persistence, real provider integration boundaries, real idempotency, real transactional behavior, real authorization, real asynchronous processing, real auditability, real observability, and comprehensive automated testing.

The repository is the source of truth for what currently exists.

Do not assume that another AI prompt or previous conversation is available.

---

# PROJECT

Implement the backend domains that complete the commercial operational layer surrounding the core ride-hailing marketplace.

This volume is responsible for:

* payment methods
* payment intent lifecycle
* payment provider integration
* payment webhooks
* payment capture
* refunds
* reconciliation
* pricing-to-payment handoff
* driver earnings
* earnings adjustments
* payout foundation
* payout provider abstraction
* payout execution
* payout webhooks
* payout reconciliation
* ratings
* notifications
* push/email/SMS abstraction
* safety workflows
* trusted contacts
* incident reporting
* fraud/risk foundation
* abuse signals
* support cases
* support operations APIs
* promotions foundation
* administrative operational commands
* audit extensions
* financial events
* notification jobs
* payout jobs
* reconciliation jobs
* risk-processing jobs
* observability
* automated testing

The implementation must integrate with the existing rider, driver, vehicle, ride, dispatch, trip, pricing, Redis, queue, event, and observability foundations already present in the repository.

Do not create parallel ride, pricing, dispatch, identity, or trip systems.

---

# SOURCE OF TRUTH

Before changing code, inspect:

* current NestJS module structure
* Prisma schema
* ride/trip entities
* pricing implementation
* event infrastructure
* outbox implementation
* BullMQ queues
* Redis integration
* authentication
* authorization
* audit infrastructure
* WebSocket implementation
* current frontend/mobile consumers
* existing external-provider abstractions
* test infrastructure
* observability
* infrastructure configuration

Preserve compatible behavior.

Extend existing abstractions rather than creating duplicates.

Do not regenerate unchanged files.

Do not arbitrarily rename existing contracts.

Where current implementation is insecure, financially unsafe, or incompatible with the project's architecture, correct it within the relevant scope and document compatibility implications.

---

# BACKEND SCOPE

This prompt owns the following domains:

* Payments
* Refunds
* Financial Reconciliation
* Driver Earnings
* Payouts
* Ratings
* Notifications
* Safety
* Fraud/Risk
* Support
* Promotions
* Operational Administration
* Financial/Audit extensions

It also extends:

* Kafka events
* transactional outbox
* BullMQ processing
* Redis
* authorization
* observability
* auditability

---

# DOMAIN OWNERSHIP

Maintain explicit boundaries.

## PAYMENTS

Own:

* payment methods
* payment intents
* provider references
* authorization
* capture
* payment failures
* refunds
* provider webhook processing
* payment reconciliation

Do not own trip state.

## EARNINGS

Own:

* driver earnings
* platform fees
* adjustments
* financial allocation from completed rides

Do not become a second payment ledger.

## PAYOUTS

Own:

* payout eligibility
* payout requests
* payout execution
* payout provider references
* payout failures
* payout reconciliation

## RATINGS

Own:

* rating eligibility
* rating creation
* aggregation
* rating moderation

## NOTIFICATIONS

Own:

* notification intents
* templates
* delivery orchestration
* delivery state
* provider integrations

Notifications are not authoritative business state.

## SAFETY

Own:

* safety incidents
* trusted contacts
* safety reporting
* escalation metadata
* safety audit access

## FRAUD/RISK

Own:

* risk signals
* risk assessments
* abuse indicators
* enforcement recommendations
* risk-related asynchronous processing

Risk systems must not silently mutate financial or trip state without explicit domain commands.

## SUPPORT

Own:

* support cases
* case categories
* case lifecycle
* case interactions
* escalation metadata

Support must invoke explicit domain commands when changing another domain's authoritative state.

## ADMINISTRATION

Own:

* operational commands
* administrative configuration
* privileged workflows
* administrative search and investigation

Administrative operations must never become unrestricted direct database editing.

---

# FINANCIAL ARCHITECTURE

Implement financial correctness as a first-class requirement.

The platform must distinguish:

* fare
* payment
* refund
* platform fee
* driver earning
* adjustment
* payout

Do not collapse these into one monetary record or one generic status.

Every authoritative monetary record must include:

* amount
* currency
* lifecycle state
* created timestamp
* updated timestamp
* business reference
* provider reference where applicable
* correlation/reference information
* auditability

Use exact monetary representations only.

Never use JavaScript floating-point arithmetic for authoritative financial calculations.

---

# PAYMENT METHODS

Implement secure payment-method management appropriate to the selected provider architecture.

Support:

* adding a payment method through provider-compatible mechanisms
* listing authorized payment methods
* setting a default method
* removing a method where allowed
* payment-method state
* provider reference
* rider ownership

Do not store raw card numbers, security codes, or other prohibited payment credentials.

Use provider tokens/references.

---

# PAYMENT METHOD AUTHORIZATION

Every payment-method operation must verify:

* authenticated rider
* resource ownership
* supported provider state
* account eligibility

A rider must never access or modify another rider's payment method by changing a resource identifier.

Apply appropriate rate limits to sensitive payment operations.

---

# PAYMENT INTENTS

Implement a payment-intent domain abstraction.

A payment intent must represent the platform's authoritative understanding of an attempted customer charge.

Support states equivalent to:

* created
* requires_action
* requires_payment_method
* authorized
* capture_pending
* captured
* failed
* canceled
* partially_refunded
* refunded

Map provider-specific lifecycle states into the internal model without losing necessary provider metadata.

---

# PAYMENT CREATION

Payment creation must:

1. Validate the authenticated rider.
2. Validate the ride/trip relationship.
3. Validate the authoritative fare.
4. Resolve currency.
5. Resolve the payment method.
6. Generate an idempotency key.
7. Create the internal payment record.
8. Invoke the provider through the payment abstraction.
9. Persist the provider reference.
10. Handle known/unknown provider outcomes safely.
11. Emit relevant events.
12. Return a controlled response.

The client must never determine the authoritative charge amount.

---

# PAYMENT IDEMPOTENCY

All externally meaningful payment operations must support idempotency.

At minimum:

* payment intent creation
* authorization
* capture
* refund
* payout execution
* webhook processing

Idempotency must distinguish:

* same operation repeated
* same key used with different parameters
* previously completed operation
* previous operation with unknown outcome

Never execute the provider operation a second time simply because the first network response was lost.

---

# UNKNOWN PAYMENT OUTCOME

Design for:

1. Client requests capture.
2. Provider processes capture.
3. Network times out.
4. Backend does not know whether capture succeeded.

The system must not blindly retry.

Use:

* provider reference lookup
* idempotency
* reconciliation
* durable pending state

to resolve the outcome.

---

# PAYMENT WEBHOOKS

Implement secure provider webhook handling.

Requirements:

* signature verification
* provider event ID
* provider event type
* provider object ID
* received timestamp
* durable receipt/processing state
* deduplication
* authorization of webhook processing logic
* internal event emission
* retry-safe processing

Never trust a webhook solely because it reaches the webhook endpoint.

Never use webhook request bodies directly to authorize user actions.

---

# WEBHOOK PROCESSING

Webhook processing must be asynchronous where appropriate.

The webhook endpoint should:

* verify signature
* validate structure
* record the incoming event
* acknowledge valid receipt
* hand processing to reliable background infrastructure

Long-running payment workflows must not execute synchronously inside the HTTP webhook request when that threatens timeout/retry correctness.

---

# PAYMENT CAPTURE

Capture must verify:

* payment intent state
* trip/fare relationship
* idempotency
* current financial state

Do not capture an arbitrary client-provided amount.

Use the authoritative final fare.

Where the provider supports incremental authorization or related mechanisms, isolate those semantics behind the payment provider abstraction.

---

# FARE ADJUSTMENT

If final fare differs from the original estimate:

* preserve the estimate
* preserve the final fare
* preserve the reason for the difference
* apply the correct payment behavior
* emit an auditable state transition

Do not overwrite the original quote.

---

# REFUNDS

Implement controlled refund workflows.

Support:

* full refund
* partial refund
* refund reason
* provider reference
* refund state
* retry
* webhook reconciliation

Refund requests must be idempotent.

A repeated refund command must not accidentally refund the same amount twice.

---

# REFUND STATES

Use an explicit lifecycle such as:

* requested
* pending
* processing
* succeeded
* failed
* partially_completed

The repository may use different names, but the state machine must support uncertain provider outcomes.

---

# PAYMENT RECONCILIATION

Implement reconciliation jobs that compare internal payment records with provider state.

Detect:

* missing provider confirmation
* unknown outcomes
* incorrect status
* unexpected amount
* unexpected currency
* duplicate events
* missing refunds
* partial refunds
* provider-side changes not reflected internally

Reconciliation must produce:

* structured findings
* metrics
* alerts
* operator-visible state

Do not silently rewrite financial history.

---

# FINANCIAL AUDITABILITY

Do not update financial history destructively merely to correct an error.

When a financial correction is required, preserve:

* original record
* correction reason
* adjustment amount
* actor/system source
* timestamp
* correlation identifier

Use append-oriented adjustments where appropriate.

---

# DRIVER EARNINGS

Implement driver earnings derived from authoritative completed-trip financial outcomes.

Support:

* gross fare
* platform fee
* applicable deductions
* driver earning
* adjustments
* promotional subsidies where applicable
* refund impacts
* earning state

Do not calculate current historical earnings from mutable ride state alone.

---

# EARNINGS ALLOCATION

When a trip is financially finalized:

1. Resolve authoritative final fare.
2. Resolve platform fee.
3. Resolve applicable adjustments.
4. Create the driver earning record.
5. Preserve the financial references.
6. Emit an earning-created event.
7. Make the earning available to payout eligibility logic.

This workflow must be idempotent.

---

# EARNINGS CORRECTIONS

Support controlled corrections.

Examples:

* support adjustment
* fee correction
* refund impact
* promotional subsidy
* operational correction

Corrections must not silently alter previously reported history.

Use explicit adjustment records.

---

# DRIVER EARNINGS QUERIES

Implement APIs for drivers to retrieve:

* available earnings
* pending earnings
* historical earnings
* adjustments
* payout status

Use pagination.

Do not return unbounded historical financial data.

Do not expose internal financial metadata unnecessarily.

---

# PAYOUT FOUNDATION

Implement a payout domain abstraction.

Support:

* payout account/provider reference
* payout eligibility
* payout request
* payout batching where appropriate
* payout processing
* payout state
* provider reference
* failure handling
* reconciliation

Do not transfer money automatically merely because an earnings record exists unless the payout rules explicitly allow it.

---

# PAYOUT STATE MACHINE

Support states such as:

* pending
* eligible
* processing
* submitted
* paid
* failed
* reversed
* canceled

The exact naming may follow repository conventions.

Payout state must remain separate from driver earning state.

---

# PAYOUT IDEMPOTENCY

A payout must never execute twice because of:

* worker retries
* API retries
* process restarts
* duplicate webhook events
* operator retries

Use:

* internal payout identifier
* provider idempotency key
* transactionally persisted state
* provider reconciliation

---

# PAYOUT PROVIDER ABSTRACTION

Implement a provider-independent interface supporting:

* account readiness
* payout creation
* payout lookup
* status retrieval
* provider webhook verification

Provider-specific models must remain inside the integration boundary.

Do not leak provider SDK types throughout the domain.

---

# PAYOUT RECONCILIATION

Detect:

* payout submitted internally but absent at provider
* provider-paid payout still pending internally
* payout failed at provider but marked successful internally
* duplicate provider events
* payout reversal

Reconciliation must be retryable and observable.

---

# RATINGS

Implement a rating domain tied to completed trips.

Support:

* rider-to-driver ratings
* driver-to-rider ratings where product policy permits
* one rating per eligible relationship
* rating validation
* optional review text
* moderation metadata
* aggregate rating calculation

A rating must reference a valid completed trip.

---

# RATING ELIGIBILITY

Enforce:

* correct trip relationship
* completed/eligible trip state
* authorized actor
* one-rating-per-side-per-trip where applicable
* rating window if configured

Do not allow arbitrary users to create ratings for unrelated users.

---

# RATING MODERATION

Support controlled moderation states where required.

Potential states:

* visible
* pending_review
* hidden
* removed

Administrative moderation actions must be auditable.

Do not allow arbitrary administrative deletion without preserving an audit record.

---

# RATING AGGREGATION

Use an aggregation strategy appropriate to scale.

Avoid recalculating millions of ratings on every profile request.

Where denormalized aggregate fields are used, define:

* authoritative rating records
* aggregate update mechanism
* reconciliation/rebuild strategy

---

# NOTIFICATION ARCHITECTURE

Implement a notification domain that separates:

1. Business event.
2. Notification intent.
3. Delivery job.
4. Provider delivery.
5. Delivery result.

This separation is mandatory for reliability.

Do not let notification-provider availability directly determine transactional ride/payment success.

---

# NOTIFICATION CHANNELS

Create abstractions for:

* push
* email
* SMS
* in-app notifications

A specific provider may be used through an adapter.

Do not embed provider-specific SDK calls into arbitrary business services.

---

# NOTIFICATION EVENTS

Integrate notification creation with relevant domain events, including where appropriate:

* ride requested
* driver assigned
* driver arriving
* trip started
* trip completed
* payment result
* payout result
* safety event
* support update

Not every event must generate every channel.

Channel selection must be policy-driven.

---

# NOTIFICATION PREFERENCES

Implement user preferences for:

* channel
* category
* locale
* optional marketing communications where applicable

Transactional and safety-critical notifications must not be disabled by ordinary marketing preferences.

---

# NOTIFICATION TEMPLATES

Use a versioned template abstraction.

Templates must support:

* locale
* channel
* event type
* variables
* version

Do not construct large notification strings inside arbitrary service methods.

---

# PUSH NOTIFICATION SECURITY

Push payloads must contain the minimum necessary information.

Do not place:

* passwords
* tokens
* payment details
* private documents
* unnecessary precise coordinates

into notification payloads.

Clients should retrieve sensitive details through authenticated APIs.

---

# NOTIFICATION RETRIES

Define:

* timeout
* retry count
* exponential backoff
* provider-specific retry classification
* dead-letter handling
* delivery metrics

Do not retry permanent provider failures indefinitely.

---

# NOTIFICATION DEDUPLICATION

Where repeated events could create duplicate user notifications, implement deterministic deduplication.

Examples:

* repeated driver-arrival event
* duplicated payment webhook
* replayed trip event

Duplicate domain events must not necessarily generate duplicate user notifications.

---

# SAFETY DOMAIN

Implement a dedicated safety domain.

Support:

* safety incidents
* incident categories
* severity
* trip reference
* reporter
* incident state
* escalation
* notes/metadata
* timestamps
* audit access

Safety state must not be embedded inside ordinary support tickets.

---

# EMERGENCY WORKFLOWS

Support the architecture for emergency actions such as:

* emergency event creation
* trip reference
* rider/driver reference
* trusted contacts
* operational escalation
* safety notification

Safety-critical operations must be designed to remain available during partial platform degradation.

Do not make analytics or recommendation systems a prerequisite for emergency reporting.

---

# TRUSTED CONTACTS

Implement a controlled trusted-contact model supporting:

* contact creation
* contact verification
* ownership
* activation/deactivation
* notification permissions

A rider must only control their own trusted contacts.

Do not expose the trusted contact's private information unnecessarily.

---

# TRIP SHARING

Where supported, implement a secure trip-sharing mechanism.

The design must prevent:

* unauthorized trip viewing
* indefinite access
* token reuse
* cross-user enumeration

Shared access must have:

* explicit scope
* expiration
* revocation
* auditability

---

# INCIDENT REPORTING

Users must be able to report:

* safety incidents
* driver issues
* rider issues
* trip issues
* payment concerns
* other supported categories

The reporting system must create a durable support/safety reference rather than simply sending an email.

---

# FRAUD/RISK FOUNDATION

Implement a risk-domain foundation that can consume operational signals.

Potential signals include:

* repeated failed payments
* abnormal cancellation
* duplicate accounts
* unusual device/IP behavior
* promotion abuse
* suspicious payout activity
* impossible location movement
* unusual trip patterns

Risk signals must be durable enough for investigation but must not become an uncontrolled duplicate user/trip database.

---

# RISK SIGNAL MODEL

A risk signal should contain:

* signal ID
* category
* subject type
* subject ID
* severity
* source
* confidence/score where used
* created timestamp
* expiration where applicable
* status
* related entity references

Do not store unnecessary raw sensitive telemetry.

---

# RISK ASSESSMENT

Implement an extensible assessment abstraction.

It may classify:

* low risk
* review
* restricted
* blocked

These are internal operational states, not user-facing accusations.

A risk assessment must have:

* reason/reference
* source
* timestamp
* expiration/review time where appropriate

---

# RISK ENFORCEMENT

Risk controls must use explicit domain commands.

Examples:

* require additional verification
* temporarily restrict action
* suspend payout
* require payment review
* block promotion use

Do not allow a risk worker to directly update arbitrary tables.

---

# LOCATION ANOMALY FOUNDATION

Use safe, explainable signals for suspicious location behavior such as:

* impossible movement
* inconsistent timestamps
* implausible distance/time
* repeated location spoofing indicators

These signals should inform risk workflows.

Do not treat one anomalous GPS reading as conclusive evidence.

---

# PROMOTIONS

Implement a promotion foundation.

Support:

* promotion code
* eligibility
* start/end
* usage limit
* per-user usage limit
* discount type
* discount amount/rate
* cap
* market
* ride-product applicability
* active state

Promotion application must occur within authoritative fare calculation.

---

# PROMOTION VALIDATION

Validate:

* expiration
* market
* rider eligibility
* usage count
* product
* maximum discount
* one-time constraints

Do not trust a discount amount supplied by the client.

---

# PROMOTION IDEMPOTENCY

A promotion must not be consumed twice because of:

* duplicate ride requests
* pricing retries
* payment retries
* event replay

Use durable usage records and appropriate uniqueness constraints.

---

# SUPPORT DOMAIN

Implement support-case management.

Support cases should reference:

* user
* rider/driver where applicable
* ride
* trip
* payment
* payout
* safety incident

Support cases must have explicit lifecycle states.

Potential states include:

* open
* assigned
* waiting_for_user
* escalated
* resolved
* closed

---

# SUPPORT AUTHORIZATION

Support staff must have controlled permissions.

Do not allow every support agent to:

* refund arbitrary amounts
* suspend arbitrary drivers
* reveal private location history
* alter pricing
* modify compliance approval

Use fine-grained operational permissions.

Sensitive actions should require stronger authorization.

---

# SUPPORT DOMAIN COMMANDS

Support must invoke domain commands for actions such as:

* cancel ride
* issue refund
* restrict account
* reopen payout review
* request compliance review

Do not allow support code to directly mutate another domain's database models.

---

# ADMINISTRATION

Implement the backend foundations for authorized operations staff.

Support:

* operational search
* user lookup
* driver lookup
* trip investigation
* payment investigation
* payout investigation
* support case management
* safety investigation
* risk review
* configuration workflows

Search results must respect access permissions and data classification.

---

# ADMINISTRATIVE COMMANDS

Implement auditable commands for actions such as:

* suspend user
* restrict driver
* reinstate driver
* cancel ride
* issue refund
* suspend payout
* disable promotion
* alter operational configuration

Every command must validate:

* permission
* target state
* reason where appropriate
* idempotency
* audit

---

# ADMIN AUDIT

Every privileged mutation must create an audit record containing:

* actor
* permission context
* action
* target
* timestamp
* request/correlation ID
* result
* reason
* safe before/after state where appropriate

Do not log sensitive secrets into audit data.

---

# FINANCIAL EVENT MODEL

Emit explicit events for:

* payment created
* payment authorized
* payment captured
* payment failed
* refund requested
* refund completed
* earnings created
* earnings adjusted
* payout requested
* payout submitted
* payout completed
* payout failed

Event payloads must contain only necessary financial metadata.

Never emit:

* card numbers
* security codes
* authentication tokens
* provider secrets

---

# EVENT CONSUMPTION

Use events from the ride/trip/pricing domains to trigger:

* payment workflows
* earnings
* notifications
* ratings eligibility
* support references
* analytics signals
* risk signals

Every consumer must be idempotent.

---

# BULLMQ JOBS

Implement jobs for:

* payment reconciliation
* refund reconciliation
* payout processing
* payout reconciliation
* notification delivery
* notification retry
* safety escalation where asynchronous
* risk analysis
* promotion cleanup
* rating aggregation where required
* support automation
* data retention/cleanup
* administrative reconciliation

Every job must specify:

* job ID
* payload
* retry policy
* backoff
* timeout
* concurrency
* idempotency
* terminal failure handling
* metrics

---

# DEAD-LETTER PROCESSING

Jobs that exhaust retries must enter an operationally visible terminal state.

Dead-letter records must include:

* job identifier
* job type
* related business entity
* error category
* attempt count
* timestamps
* correlation ID

Provide a safe replay mechanism.

Replay must re-check current authoritative business state before executing.

---

# RECONCILIATION ARCHITECTURE

Create reconciliation jobs for:

* payments
* refunds
* payouts
* notification delivery
* event processing
* rating aggregates
* promotion usage
* risk state where needed

Reconciliation must be read-mostly and correction-oriented.

Do not silently mutate historical records without preserving the reason and audit trail.

---

# SECURITY

Review all new domains for:

* IDOR
* privilege escalation
* sensitive financial data exposure
* webhook forgery
* payment replay
* duplicate refund
* duplicate payout
* support abuse
* admin abuse
* notification abuse
* trusted-contact abuse
* promotion abuse
* fraud-worker overreach

All sensitive actions must be:

* authenticated
* authorized
* validated
* idempotent where appropriate
* audited

---

# PAYMENT DATA PRIVACY

Never expose:

* full card numbers
* CVV/security codes
* raw provider secrets
* private payment credentials

Only expose safe payment-method metadata needed by clients.

---

# LOCATION PRIVACY IN OPERATIONS

Support staff and ordinary administrators must not automatically have unrestricted access to exact historical location.

Where operational access is required:

* enforce permission
* log access
* minimize returned detail
* respect retention policies

---

# FINANCIAL ACCESS CONTROL

Drivers may access:

* their own earnings
* their own payout records

Riders may access:

* their own payment methods
* their own payment records
* their own refunds

Support/operations access must be permission-based.

Do not expose full financial datasets through generic user endpoints.

---

# OBSERVABILITY

Instrument:

* payment creation
* payment provider latency
* payment failures
* webhook latency
* webhook duplicates
* reconciliation findings
* refund processing
* earnings creation
* payout execution
* payout failures
* notification delivery
* notification failures
* safety incidents
* risk signals
* support cases
* administrative commands

Every important workflow must preserve:

* request ID
* correlation ID
* trace ID
* entity ID
* provider reference where safe

Never log secrets or unnecessary financial/private content.

---

# BUSINESS METRICS

Track:

* payment success rate
* payment failure rate
* unknown payment outcomes
* refund success rate
* refund backlog
* earnings generation rate
* payout success rate
* payout failure rate
* payout backlog
* notification delivery rate
* notification failure rate
* safety incidents
* risk signal rate
* promotion usage
* rating completion rate
* support case backlog
* average support resolution time

Do not mix these metrics with generic infrastructure counters.

---

# RELIABILITY

The implementation must tolerate:

* duplicate provider webhooks
* provider timeout after successful operation
* worker restart
* queue retry
* Kafka replay
* duplicate domain events
* notification provider outage
* payment provider outage
* payout provider outage
* Redis outage
* database failover
* partial support-system failure

Financial correctness must survive retries and unknown external outcomes.

---

# PAYMENT PROVIDER FAILURE

When the provider is unavailable:

* do not silently mark payment successful
* do not retry blindly
* preserve pending/unknown state as required
* expose controlled client behavior
* queue reconciliation
* alert operations

---

# PAYOUT PROVIDER FAILURE

When payout execution times out:

* preserve a pending/unknown state
* do not execute another payout blindly
* reconcile provider status
* retain idempotency keys
* alert when uncertainty exceeds threshold

---

# NOTIFICATION PROVIDER FAILURE

If a notification provider is unavailable:

* retain the notification job
* apply bounded retry
* move permanently failed jobs to dead-letter state
* do not fail the underlying ride/payment transaction

---

# SAFETY FAILURE

Safety incident creation should have a minimal critical path.

Do not make:

* analytics
* ratings
* recommendation
* search

prerequisites for creating a safety incident.

---

# FRAUD FAILURE

Fraud/risk processing may be delayed.

The platform must define safe fallback behavior rather than blocking every ride/payment operation indefinitely.

Critical enforcement must be explicit.

---

# PERFORMANCE

Optimize:

* payment database lookups
* webhook processing
* earnings creation
* payout eligibility queries
* notification queue throughput
* support searches
* rating aggregation
* promotion validation

Prevent:

* unbounded financial queries
* repeated provider calls
* synchronous provider calls inside large database transactions
* unbounded notification fan-out
* unbounded support search
* recalculating aggregates on every read

---

# DATABASE DESIGN

Implement or update persistence for:

* payment methods
* payment intents
* payment transactions
* refunds
* financial adjustments
* earnings
* payouts
* ratings
* notification intents
* notification deliveries
* safety incidents
* trusted contacts
* trusted sharing where applicable
* risk signals
* risk assessments
* promotions
* promotion usage
* support cases
* support actions
* administrative commands/audit extensions

Use:

* foreign keys
* uniqueness
* appropriate indexes
* exact monetary types
* state/version fields
* timestamps
* provider references

High-volume historical tables must have appropriate indexing and retention considerations.

---

# DATABASE CONCURRENCY

Protect:

* payment creation
* payment capture
* refund creation
* payout execution
* promotion consumption
* rating uniqueness
* notification deduplication
* administrative mutations

Use:

* unique constraints
* transactions
* optimistic concurrency
* explicit state checks
* idempotency records

where appropriate.

---

# FINANCIAL DATABASE INVARIANTS

Enforce invariants such as:

* one authoritative payment intent per intended charge
* one idempotent capture effect
* one authoritative refund effect per refund command
* one payout execution per payout intent
* one promotion usage per defined usage key
* one rating per eligible actor/trip relationship

These invariants must survive concurrent requests.

---

# API SURFACES

Implement authenticated and appropriately authorized APIs for:

* payment methods
* payments
* refunds where user-facing
* driver earnings
* driver payouts
* ratings
* notification preferences
* safety incidents
* trusted contacts
* support cases
* promotions
* administrative operations

Exact route naming must follow repository conventions.

Every endpoint must include:

* validation
* authorization
* ownership
* error semantics
* idempotency where required
* observability
* automated tests

---

# PAYMENT WEBHOOK SURFACE

Implement the provider-specific webhook endpoint through the repository's integration architecture.

It must:

* verify signatures
* reject malformed requests
* record provider event identity
* safely acknowledge valid events
* avoid duplicate processing
* enqueue long-running work
* emit internal events when appropriate

---

# NOTIFICATION WEBHOOKS

Where notification providers require callbacks:

* verify authenticity
* map provider status to internal state
* deduplicate
* preserve delivery history
* avoid retry loops
* emit delivery metrics

---

# PAYOUT WEBHOOKS

Where payout providers require callbacks:

* verify authenticity
* deduplicate
* update payout state safely
* emit internal events
* trigger reconciliation if state is unexpected

---

# SUPPORT SEARCH

Support and administrative search must avoid exposing unrestricted arbitrary database access.

Allow only approved:

* fields
* filters
* sort orders
* resource relationships

Apply authorization before returning records.

Do not allow SQL-like arbitrary search syntax from clients.

---

# ADMIN API SECURITY

Administrative endpoints must be separately protected with:

* strong authentication
* fine-grained permissions
* rate limits
* audit logging
* explicit action confirmation for destructive operations where appropriate

Do not reuse ordinary rider authorization rules for administrator operations.

---

# DATA RETENTION

Define retention policies for:

* payment records
* financial adjustments
* payout records
* notification history
* safety incidents
* risk signals
* support cases
* audit records
* promotion usage
* location references included in incidents

Do not delete records merely because they are old if they are required for legal/financial auditability.

---

# PRIVACY

Protect:

* financial information
* identity information
* safety information
* support conversations
* fraud signals
* trusted-contact information

Never expose internal risk scores directly to riders or drivers unless the product explicitly requires a safe user-facing representation.

Do not expose support notes to users unless explicitly intended.

---

# TESTING REQUIREMENTS

Write comprehensive tests.

## PAYMENTS

Test:

* payment creation
* provider success
* provider decline
* timeout
* unknown outcome
* capture
* duplicate capture
* duplicate webhook
* invalid webhook signature
* partial refund
* full refund
* duplicate refund
* reconciliation

## EARNINGS

Test:

* completed-trip earnings
* platform fee
* adjustment
* refund impact
* duplicate event
* historical query
* pagination

## PAYOUTS

Test:

* eligibility
* payout creation
* duplicate payout
* provider timeout
* webhook
* reconciliation
* failure/retry
* reversal

## RATINGS

Test:

* eligible rating
* unauthorized rating
* duplicate rating
* incomplete trip
* aggregation
* moderation

## NOTIFICATIONS

Test:

* event-to-notification mapping
* preference selection
* provider success
* retry
* permanent failure
* dead-letter
* deduplication
* channel selection

## SAFETY

Test:

* incident creation
* authorization
* trusted contacts
* trip sharing
* expiration/revocation
* escalation

## FRAUD/RISK

Test:

* signal creation
* idempotent processing
* expiration
* controlled enforcement
* access control

## PROMOTIONS

Test:

* eligibility
* expiration
* usage limit
* duplicate consumption
* market/product rules
* discount cap

## SUPPORT

Test:

* case creation
* authorization
* assignment
* state transitions
* domain commands
* privileged actions

## ADMINISTRATION

Test:

* permissions
* command validation
* audit
* idempotency
* unauthorized access

---

# CONCURRENT TESTING

Explicitly test:

* duplicate payment creation
* concurrent payment captures
* duplicate refund requests
* duplicate payout attempts
* simultaneous promotion usage
* duplicate webhook processing
* duplicate notification jobs
* concurrent rating creation
* concurrent administrative commands

Tests must prove that database constraints and idempotency prevent duplicate financial effects.

---

# INTEGRATION TESTING

Validate real integration behavior for:

* PostgreSQL
* Prisma
* Redis
* BullMQ
* Kafka/outbox
* payment provider abstraction
* notification providers where test environments exist
* payout provider abstraction
* WebSocket-triggered notification flows where applicable

Do not mock the database in every test.

---

# MIGRATION TESTING

For every financial or operational schema change:

* apply clean migration
* apply migration against representative existing data where practical
* validate exact monetary columns
* validate uniqueness
* validate foreign keys
* validate indexes
* verify Prisma client generation
* verify rollback/deployment strategy

---

# PERFORMANCE TESTING

Measure where practical:

* payment webhook throughput
* notification queue throughput
* payout processing throughput
* earnings query latency
* support search latency
* rating aggregation throughput
* promotion validation latency

Identify database and provider bottlenecks.

Do not claim performance validation without measurements.

---

# SECURITY REVIEW

Perform a security review for:

* payment IDOR
* refund authorization
* payout authorization
* admin privilege escalation
* support privilege escalation
* webhook forgery
* replay
* duplicate financial effect
* secret leakage
* provider credential exposure
* risk-data exposure
* safety-data exposure
* trusted-contact exposure
* promotion abuse

Fix discovered vulnerabilities within scope.

---

# BACKWARD COMPATIBILITY

Inspect existing consumers before changing:

* trip completion contracts
* pricing contracts
* payment endpoints
* event payloads
* notification contracts
* driver earnings APIs
* mobile responses

Prefer additive changes.

If a breaking change is required:

* identify consumers
* update consumers
* document migration
* preserve compatibility during rollout where practical

---

# DOCUMENTATION

Update repository documentation for:

* payment provider configuration
* webhook setup
* payment reconciliation
* refunds
* earnings
* payouts
* notification providers
* notification jobs
* safety workflows
* risk workflows
* support permissions
* administrative permissions
* promotions
* audit requirements
* financial troubleshooting
* operational recovery

Documentation must describe actual implementation.

---

# IMPLEMENTATION DISCIPLINE

Before changing files:

1. Inspect the repository.
2. Identify existing financial/domain foundations.
3. Map this scope to existing modules.
4. Preserve compatible contracts.
5. Implement payment methods.
6. Implement payment lifecycle.
7. Implement refunds and reconciliation.
8. Implement earnings.
9. Implement payouts.
10. Implement ratings.
11. Implement notifications.
12. Implement safety.
13. Implement risk foundations.
14. Implement support.
15. Implement promotions.
16. Implement administrative commands.
17. Extend audit infrastructure.
18. Add required events and jobs.
19. Add observability.
20. Add tests.
21. Validate migrations.
22. Run linting/formatting/type checks.
23. Run integration and runtime validation.
24. Perform security/privacy review.
25. Update documentation.
26. Produce the required completion report.

Do not rewrite unrelated parts of the repository.

---

# PRODUCTION COMPLETENESS

Never leave:

* simulated payment success
* fake payout processing
* fake notification delivery
* fake refunds
* hardcoded earnings
* placeholder safety workflows
* incomplete administrative commands
* TODO/FIXME implementation gaps
* pseudo-code
* unverified provider callbacks

Do not claim financial functionality is complete without idempotency and reconciliation.

Do not claim safety functionality is complete if unauthorized users can access incidents.

Do not claim notification reliability if failed deliveries disappear without retry or terminal handling.

---

# PROHIBITED PRACTICES

Never:

* store raw payment credentials
* trust client payment amounts
* trust client payout amounts
* execute duplicate financial effects
* treat webhooks as automatically trusted
* retry uncertain financial outcomes blindly
* use floating-point money
* expose risk scores without authorization
* expose support notes arbitrarily
* let support directly mutate financial tables
* let administration bypass domain authorization
* make notification delivery required for transactional correctness
* make fraud analysis an uncontrolled single point of failure
* allow safety incidents to be silently discarded
* allow duplicate promotion consumption
* create unrestricted administrative APIs
* store secrets in logs/events
* use event replay as an excuse for non-idempotent consumers

---

# IMPLEMENTATION BOUNDARIES

This prompt implements the financial and operational backend layer surrounding the completed ride marketplace.

It must integrate with:

* riders
* drivers
* rides
* trips
* pricing
* dispatch
* location
* events
* queues
* authorization
* audit

Do not implement frontend or mobile UI.

Do not implement infrastructure deployment unless changes are strictly necessary for the backend functionality and repository conventions require them.

Do not create a second API/event architecture.

---

# REQUIRED IMPLEMENTATION DELIVERABLES

Implement or update:

## PAYMENTS

* payment methods
* payment intent
* provider abstraction
* authorization/capture
* webhooks
* refunds
* reconciliation

## EARNINGS

* earning creation
* fee allocation
* adjustments
* historical queries

## PAYOUTS

* payout eligibility
* payout execution
* provider abstraction
* webhook processing
* reconciliation

## RATINGS

* rating creation
* eligibility
* moderation
* aggregation

## NOTIFICATIONS

* notification intents
* provider adapters
* preferences
* templates
* jobs
* retry/dead-letter

## SAFETY

* incidents
* trusted contacts
* trip sharing where supported
* escalation

## FRAUD/RISK

* signals
* assessments
* asynchronous processing
* controlled enforcement

## SUPPORT

* cases
* lifecycle
* domain-command integration
* authorization

## PROMOTIONS

* configuration
* eligibility
* application
* usage tracking

## ADMINISTRATION

* operational search
* privileged commands
* audit

## OBSERVABILITY

* financial metrics
* notification metrics
* risk metrics
* safety metrics
* support metrics
* audit telemetry

---

# REQUIRED EVENTS

Implement appropriate events such as:

* payment-intent-created
* payment-authorized
* payment-captured
* payment-failed
* refund-requested
* refund-completed
* earning-created
* earning-adjusted
* payout-requested
* payout-submitted
* payout-completed
* payout-failed
* rating-created
* notification-requested
* notification-delivered
* notification-failed
* safety-incident-created
* support-case-created
* risk-signal-created
* promotion-applied
* promotion-rejected
* administrative-action-executed

Event names must follow the repository's established conventions.

---

# REQUIRED QUEUES

Implement appropriate jobs/queues for:

* payment reconciliation
* refund reconciliation
* payout processing
* payout reconciliation
* notification delivery
* notification retry
* rating aggregation
* risk analysis
* promotion maintenance
* safety escalation where applicable
* support automation where applicable
* retention/cleanup

Every queue must define:

* payload
* retry
* timeout
* backoff
* concurrency
* idempotency
* terminal failure
* observability

---

# REQUIRED DATABASE VALIDATION

After implementation:

* apply migrations
* verify financial precision
* verify unique payment/payout invariants
* verify refund constraints
* verify rating uniqueness
* verify promotion usage constraints
* verify support relationships
* verify audit relationships
* verify indexes
* verify foreign keys
* verify state/version fields

Test concurrent operations against PostgreSQL where practical.

---

# RUNTIME VALIDATION

Verify:

* payment creation
* webhook processing
* capture
* refund
* reconciliation
* earnings generation
* payout processing
* rating
* notification jobs
* safety incident creation
* risk signal processing
* support case lifecycle
* promotion validation
* administrative commands

Do not report provider integration as functional unless the configured provider/test environment was actually exercised.

---

# COMPLETION REPORT REQUIREMENTS

When implementation is complete, report:

## FILES CREATED

List every new file.

## FILES MODIFIED

List every modified file.

## MAJOR FUNCTIONALITY

Describe:

* payments
* refunds
* earnings
* payouts
* ratings
* notifications
* safety
* fraud/risk
* support
* promotions
* administration

## DATABASE CHANGES

Report:

* Prisma schema
* migrations
* indexes
* constraints
* financial precision
* concurrency protections

## API CHANGES

Report:

* payment methods
* payments
* refunds
* earnings
* payouts
* ratings
* notifications
* safety
* support
* promotions
* administrative operations

## WEBHOOK CHANGES

Report:

* payment provider
* payout provider
* notification provider callbacks where applicable
* signature verification
* deduplication
* async processing

## EVENT CHANGES

Report:

* events
* versions
* producers
* consumers
* outbox changes

## QUEUE CHANGES

Report:

* queues
* jobs
* retry
* reconciliation
* dead letters

## SECURITY CHANGES

Report:

* financial authorization
* admin permissions
* support permissions
* webhook verification
* sensitive-data protection
* fraud/risk access control

## AUDIT CHANGES

Report:

* administrative audit
* financial audit
* safety audit
* security actions

## OBSERVABILITY CHANGES

Report:

* logs
* metrics
* traces
* alerts
* business telemetry

## TESTS

List tests added or modified and the behaviors they verify.

## VALIDATION

Report:

* formatting
* linting
* type checking
* builds
* migrations
* unit tests
* integration tests
* concurrency tests
* API tests
* webhook tests
* queue tests
* runtime validation
* performance validation where performed

## COMPATIBILITY

Identify:

* existing clients affected
* API compatibility
* mobile compatibility
* event compatibility
* database compatibility
* provider migration considerations

## UNRESOLVED ISSUES

List only genuine remaining issues.

Do not claim financial or operational readiness if mandatory functionality remains incomplete or unverified.

---

# FINAL ENGINEERING PRINCIPLE

Financial correctness, safety, and operational control must be treated as first-class system invariants.

Payments must remain correct under unknown provider outcomes.

Payouts must remain correct under retries and worker crashes.

Notifications must remain recoverable without becoming transactional dependencies.

Safety workflows must remain accessible during partial failures.

Risk systems must be extensible without becoming uncontrolled sources of truth.

Support and administration must operate through explicit, authorized domain commands.

Promotions must remain deterministic and resistant to replay.

Ratings must remain tied to real completed trips.

Every financial, safety, administrative, and security-sensitive action must be observable and auditable.

Prioritize:

* financial correctness
* idempotency
* security
* privacy
* auditability
* reliability
* recoverability
* operational clarity
* scalability
* maintainability

The repository remains the implementation source of truth.

All later client and infrastructure work must consume these backend contracts without creating alternate payment, earnings, notification, safety, support, or administrative sources of truth.
