# Uber-Style Global Ride-Hailing & Mobility Platform — Backend Prompt — Volume 6

## ROLE

You are the senior backend engineering organization responsible for implementing the pricing, fare, promotion, payment, refund, financial-ledger, earnings, payout, and reconciliation foundation of an original, production-grade global ride-hailing and mobility platform.

Operate simultaneously as:

* Principal Software Architect
* Staff Backend Engineer
* Financial Systems Architect
* Payments Engineer
* Database Architect
* Distributed Systems Engineer
* Security Engineer
* Reliability Engineer
* Performance Engineer
* QA Engineer
* Observability Engineer
* Technical Writer

You are implementing production software, not demonstrating concepts.

Do not act as a teacher.

Do not provide pseudo-code.

Do not provide incomplete examples instead of implementation.

Do not leave TODO or FIXME placeholders for required work.

Do not omit implementations with statements such as:

* "implement similarly"
* "remaining code omitted"
* "for brevity"
* "left as an exercise"

Every required file must contain a real implementation.

# PROJECT

## Project Identity

Build an original global ride-hailing and mobility platform supporting:

* riders
* drivers
* operations personnel
* support personnel
* safety personnel
* fleet personnel
* administrators

This milestone implements the platform's financial domain foundation, covering fare calculation through internal financial records and payout state.

The platform is architected for targets such as:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* high-volume payment processing
* large numbers of concurrent financial operations
* multi-region operation
* strong correctness and audit requirements

These are architectural targets, not measured capacity claims.

## Technology Direction

Use the locked project stack:

### Runtime

* Node.js
* TypeScript

### Framework

* NestJS

### Database

* PostgreSQL
* PostGIS where applicable
* Prisma where compatible with the architecture

### Cache and Ephemeral State

* Redis

### Events

* Kafka or Redpanda

### Background Jobs

* BullMQ or equivalent

### Payments

* provider abstraction with a Stripe-compatible implementation boundary

### Object Storage

* Amazon S3 where required for financial artifacts or reconciliation exports

### Observability

* OpenTelemetry
* Prometheus-compatible metrics
* structured logs
* Loki-compatible logging
* Tempo-compatible tracing

# SOURCE OF TRUTH

The repository is the implementation source of truth.

Inspect the repository before making changes.

Use the architecture artifacts already present in the repository as the authoritative architecture and financial-contract reference.

Backend Volumes 1–5 establish:

* backend platform foundations
* identity and authorization
* driver availability and location
* trip lifecycle
* dispatch and assignment
* canonical API/error/idempotency/concurrency contracts
* event/outbox infrastructure
* realtime foundations

This milestone must build financial behavior around those established boundaries.

Do not depend on the previous AI conversation.

If existing implementation differs from the architecture:

1. inspect the actual implementation
2. preserve compatible working behavior
3. make the minimum coherent changes required
4. document material discrepancies

Do not create competing payment or financial authorities.

# BACKEND EXECUTION MODEL

This milestone owns:

* fare estimates
* quotes
* pricing versions
* dynamic pricing
* promotions
* cancellation fees
* final fare calculation
* payment-provider abstraction
* payment intents
* authorization
* capture
* refunds
* payment webhooks
* payment reconciliation
* disputes
* immutable financial ledger
* driver earnings
* tips
* bonuses/adjustments where defined
* payout state
* payout provider integration boundary
* financial holds
* financial audit/reconciliation
* financial events

The trip domain remains authoritative for trip lifecycle.

Dispatch remains authoritative for driver assignment.

This milestone must consume those domain facts rather than taking ownership of them.

# FINANCIAL PRINCIPLES

The implementation must treat financial correctness as a first-class invariant.

At minimum:

* monetary values must use exact representations
* currency must be explicit
* historical financial records must be immutable
* financial corrections must use compensating entries rather than mutation
* provider state must remain distinct from internal financial state
* payment operations must be idempotent
* provider webhooks must be authenticated and idempotent
* reconciliation must identify mismatches
* retries must not duplicate charges or payouts
* external provider failure must not corrupt internal financial state

Never use floating-point numbers as the authoritative representation of money.

# CURRENT IMPLEMENTATION SCOPE

## 1. Pricing Domain Boundary

Establish authoritative ownership for pricing.

Pricing owns:

* fare calculation
* quote generation
* pricing configuration references
* pricing version
* promotions
* cancellation-fee calculation
* final fare composition

Pricing does not own:

* trip lifecycle
* driver assignment
* payment-provider state
* payout-provider state

## 2. Money Representation

Implement a canonical monetary representation.

Support:

* integer minor units or the architecture's equivalent exact representation
* ISO currency code
* explicit precision
* exact arithmetic
* deterministic rounding
* serialization rules

Do not use JavaScript floating-point arithmetic for authoritative money calculations.

Create reusable money utilities or value objects rather than duplicating monetary arithmetic across modules.

## 3. Currency Handling

Implement currency validation according to the architecture.

Support:

* currency code
* supported currency configuration
* currency compatibility with market/service area
* explicit rounding behavior

Do not infer currency from client locale.

Use authoritative regional/service configuration.

## 4. Pricing Version

Every committed quote/fare must identify the pricing version or configuration revision used.

Pricing versions must be:

* immutable once referenced by a committed financial record
* auditable
* reproducible

A later pricing-configuration change must not silently alter an already committed fare.

## 5. Fare Estimate

Implement the fare-estimate flow defined by the architecture.

It may use:

* service category
* route/distance estimates
* time estimates
* base fare
* distance/time components
* configured fees
* dynamic pricing
* promotions where applicable

The estimate must clearly identify that it is an estimate rather than a captured financial charge.

Do not call the payment provider during ordinary fare estimation.

## 6. Quote

Implement the canonical quote model.

A quote should contain the authoritative information required by the contract, including:

* quote ID
* trip/request context
* pricing version
* currency
* component breakdown
* subtotal
* discounts
* fees
* estimated total
* expiration
* calculation metadata where required

Quotes must be immutable after issuance.

## 7. Quote Expiration

Implement quote expiration.

Expired quotes must not be silently reused for new financial commitments.

Handle:

* expiration
* client retry
* duplicate quote request
* pricing-version changes
* service/configuration changes

Quote expiration must be explicit and observable.

## 8. Fare Calculation

Implement deterministic fare calculation.

Separate individual components such as:

* base fare
* distance component
* time component
* minimum fare
* booking/service fees
* tolls where supported
* taxes/fees where contractually defined
* dynamic pricing multiplier/adjustment
* discounts
* cancellation fee
* tip exclusion/inclusion according to the contract

Do not invent jurisdiction-specific tax logic absent an explicit project requirement.

## 9. Pricing Configuration

Load pricing configuration through the established configuration architecture.

Configuration should support:

* versioning
* effective time
* market/service-area scope
* service category
* currency
* bounded numeric values
* auditability

Do not hard-code production pricing values into business logic.

## 10. Dynamic Pricing

Implement the architecture's dynamic-pricing boundary.

Support:

* pricing multiplier or adjustment
* market/service-area scope
* effective period
* configuration version
* validation

Keep dynamic pricing policy separated from the low-level fare calculator.

Do not invent a proprietary surge algorithm.

Use a deterministic configured input or explicit strategy abstraction.

## 11. Promotion Model

Implement promotions according to the architecture.

Support:

* promotion identity
* eligibility
* validity period
* usage constraints
* scope
* discount type
* maximum discount where applicable
* application status

Do not make promotion redemption dependent on client-side validation.

## 12. Promotion Idempotency

Ensure repeated requests cannot consume the same promotion incorrectly.

Protect against:

* concurrent redemption
* duplicate trip creation
* retry
* cancellation/repricing scenarios

Promotion usage must remain consistent with the final committed fare.

## 13. Final Fare

Implement final fare calculation after the trip completes or reaches the architecture-defined billing point.

The final fare must be based on:

* actual trip facts
* authoritative pricing version
* applicable adjustments
* valid promotions
* cancellation/other applicable fees

Do not modify an already committed fare silently.

## 14. Fare Adjustment Model

Where the architecture supports post-trip adjustments, implement explicit adjustment records.

Examples may include:

* toll correction
* authorized manual adjustment
* provider correction
* support-approved adjustment

Adjustments must be:

* explicit
* auditable
* attributable
* separately represented

Do not mutate the original fare to hide a correction.

## 15. Cancellation Fees

Implement the pricing side of cancellation fees.

Determine:

* applicable state
* applicable policy
* fee amount
* pricing version
* reason/reference

Do not implement trip cancellation authorization here.

Consume the trip's authoritative cancellation facts.

## 16. Pricing/Trip Integration

Consume trip events and state as the authoritative source for:

* completed trip
* cancelled trip
* trip timing
* service category
* geographic context

Do not directly modify trip lifecycle state from pricing.

## 17. Payment Domain Boundary

Establish authoritative ownership for internal payment state.

The payment domain owns:

* payment intent
* payment operation
* provider reference
* payment state
* authorization
* capture
* refund
* dispute
* reconciliation state

Trip and pricing domains do not own provider payment state.

## 18. Payment Provider Abstraction

Implement a provider-neutral interface.

The abstraction must support operations such as:

* create payment intent
* retrieve payment intent
* authorize
* capture
* cancel
* refund
* retrieve charge/payment state
* reconcile
* verify webhook
* handle provider events

Provider-specific APIs and response models must remain inside the adapter.

## 19. Stripe-Compatible Adapter Boundary

Implement the provider adapter required by the repository architecture without leaking provider-specific details into domain models.

Provider-specific concepts must be mapped into canonical internal states.

Do not make the rest of the application depend directly on SDK classes.

## 20. Payment State Machine

Implement the internal payment state machine.

Support the contractually defined states, potentially including:

* pending
* requires-action
* authorized
* captured
* failed
* cancelled
* partially-refunded
* refunded
* disputed
* reconciliation-required

Use the exact architecture terminology.

State transitions must be explicit and protected by concurrency controls.

## 21. Payment Intent

Implement the canonical internal payment-intent record.

It should reference:

* internal payment ID
* trip/fare reference
* rider/account
* currency
* amount
* provider
* provider reference
* current internal state
* timestamps
* version

Do not store sensitive payment credentials.

## 22. Payment Idempotency

Every provider-changing payment operation must have robust idempotency.

Protect:

* payment creation
* authorization
* capture
* refund
* payout

against retries and concurrent execution.

Use provider idempotency capabilities where available, plus internal safeguards.

Never assume a network timeout means the provider did nothing.

## 23. Authorization

Implement payment authorization flow.

The sequence must clearly handle:

* internal intent creation
* provider request
* provider response
* internal state update
* event publication

A timeout or ambiguous provider response must enter a recoverable/reconciliation state rather than blindly retrying a charge.

## 24. Capture

Implement capture according to the architecture.

Capture must be linked to:

* internal payment ID
* authorized amount
* final fare
* provider reference

Prevent double capture.

If the final amount differs from the authorized amount, follow the contractually supported adjustment flow.

## 25. Payment Failure

Classify payment failures.

Distinguish:

* retryable provider failure
* customer-action-required
* permanent payment failure
* fraud/risk decline
* configuration failure
* ambiguous provider outcome

Do not expose raw provider error details to clients.

## 26. Refunds

Implement refund state and workflow.

Support:

* full refund
* partial refund where allowed
* refund reason
* original payment reference
* provider refund reference
* idempotency
* asynchronous completion

Do not mutate the original captured payment record to represent a refund.

## 27. Refund Concurrency

Prevent:

* duplicate refunds
* refund exceeding captured amount
* concurrent refund races
* retries creating additional refunds

Use database constraints and explicit refund-total calculations.

## 28. Payment Webhooks

Implement authenticated provider webhook handling.

Support:

* signature verification
* event parsing
* event version
* provider event ID
* idempotency
* state transition validation
* reconciliation
* safe retry

Never trust webhook payloads solely because the endpoint is private or obscure.

## 29. Webhook Event Ordering

Provider webhooks may be duplicated or delivered out of order.

Use provider event identifiers, timestamps, internal versioning, and reconciliation logic as appropriate.

Do not blindly apply an older webhook state over a newer authoritative internal state.

## 30. Financial Ledger

Implement the immutable internal financial ledger.

The ledger must represent financial facts separately from operational payment-provider state.

Implement:

* ledger account/reference
* entry identity
* transaction/reference ID
* debit/credit semantics as defined
* amount
* currency
* source
* timestamp
* immutable metadata

Do not update historical ledger entries in place.

## 31. Double-Entry or Equivalent Integrity

Use the architecture's defined accounting model.

If the architecture uses double-entry accounting, enforce balanced entries.

Financial transactions must have deterministic total debits and credits.

A transaction must not be considered committed if its required ledger entries are incomplete.

## 32. Financial Corrections

Never edit historical financial entries to correct an error.

Implement compensating or adjustment entries.

Corrections must include:

* reason
* original reference
* actor/source
* timestamp
* authorization where required

## 33. Earnings

Implement the driver-earnings domain.

Support:

* trip earnings
* applicable fees
* tips
* bonuses
* adjustments
* holds
* available balance
* pending balance

Earnings must derive from committed financial facts.

Do not directly calculate driver earnings from mutable trip fields during payout execution.

## 34. Tips

Where tips are supported, implement explicit tip records.

Support:

* amount
* currency
* trip
* rider
* driver
* creation time
* modification window where the architecture permits
* financial/ledger references

Protect against duplicate tip creation.

## 35. Payout Domain Boundary

Implement internal payout state but preserve abstraction over payout providers.

Support:

* payout request
* amount
* currency
* destination reference
* provider
* provider reference
* status
* timestamps
* failure reason
* reconciliation state

Do not store bank credentials or other sensitive provider data unnecessarily.

## 36. Payout Idempotency

Prevent duplicate payouts.

Use:

* unique payout references
* idempotency
* database constraints
* provider idempotency where available
* explicit state transitions

A network timeout must not cause a blind second payout.

## 37. Payout Holds

Implement financial holds where the architecture requires them.

Possible causes include:

* fraud/risk review
* account restriction
* payout reconciliation
* dispute
* operational investigation

Do not allow ordinary user flows to bypass a hold.

## 38. Reconciliation

Implement internal reconciliation workflows for:

* payment-provider state versus internal payment state
* refunds
* captures
* payouts
* ledger totals
* earnings

Reconciliation should identify:

* missing provider operation
* duplicate operation
* mismatched amount
* mismatched currency
* mismatched status
* unknown provider reference

Do not silently auto-correct financial mismatches without a defined safe reconciliation policy.

## 39. Reconciliation Jobs

Use the shared background-job infrastructure for scheduled reconciliation where appropriate.

Jobs must be:

* idempotent
* bounded
* resumable
* observable
* retry-safe

Large historical reconciliation must support pagination/batching.

## 40. Financial Events

Publish canonical financial events such as:

* quote.created
* fare.committed
* payment.created
* payment.authorized
* payment.captured
* payment.failed
* refund.created
* refund.completed
* payment.disputed
* ledger.transaction.committed
* earnings.updated
* payout.created
* payout.completed
* payout.failed

Use the exact project event naming conventions.

Do not expose sensitive payment credentials or provider secrets in events.

## 41. Transactional Boundaries

Financial state changes and their required outbox records must be atomic.

Examples:

* payment-state transition plus payment event
* ledger transaction plus financial event
* earnings update plus earnings event
* payout-state transition plus payout event

Do not rely on eventual repair for ordinary transaction integrity.

## 42. Financial Authorization and Privileged Actions

Protect:

* manual refunds
* manual adjustments
* payout intervention
* holds/release
* reconciliation corrections

with explicit permissions.

Sensitive actions must be auditable.

Do not provide an unrestricted financial-admin endpoint.

## 43. Database Constraints

Implement database-level protection for:

* unique provider references
* unique webhook event IDs
* ledger entry integrity
* payout idempotency
* refund limits
* valid foreign keys
* valid state values
* currency consistency

Application validation must be backed by database constraints where appropriate.

## 44. Financial Precision and Rounding

Centralize all financial calculations.

Define:

* rounding mode
* scale
* currency precision
* tax/fee rounding behavior
* component-sum rules
* final-total calculation

Ensure the displayed and persisted totals remain consistent.

## 45. Security and Privacy

Never store:

* raw card numbers
* CVV
* provider secret keys
* authentication credentials
* raw bank credentials

Use provider references/tokens according to the payment-provider abstraction.

Financial API responses must expose only the permitted information.

## 46. Logs and Telemetry

Do not log:

* payment credentials
* authorization headers
* full provider webhook secrets
* sensitive banking information
* raw payment instrument details

Metrics must avoid high-cardinality financial identifiers.

Traces should contain safe payment-operation metadata without sensitive payloads.

## 47. Financial Audit

Audit:

* manual refunds
* manual adjustments
* payout changes
* financial holds
* ledger corrections
* privileged reconciliation actions
* administrative financial access

Financial audit records must remain protected and traceable.

## 48. Failure and Recovery

Handle:

* provider timeout
* provider outage
* ambiguous provider result
* database failure
* event-broker failure
* duplicate webhook
* out-of-order webhook
* Redis failure
* job worker failure

An ambiguous payment operation must become reconcilable, not automatically duplicated.

## 49. APIs

Implement only the financial APIs defined by the architecture.

Potential capabilities include:

* fare estimate
* quote retrieval
* promotion application
* payment method references
* payment status
* refund status
* earnings
* payout status

Do not expose internal ledger mechanics through ordinary customer APIs.

## 50. Testing

Create comprehensive tests for:

### Pricing

* deterministic calculations
* rounding
* quote expiration
* configuration versioning
* promotion eligibility
* promotion concurrency
* final fare
* cancellation fee

### Payments

* intent creation
* authorization
* capture
* provider failure
* timeout
* idempotent retry
* duplicate operation
* webhook signature
* duplicate webhook
* out-of-order webhook

### Refunds

* full refund
* partial refund
* duplicate refund
* refund race
* over-refund prevention

### Ledger

* balanced transaction
* immutability
* correction entries
* currency consistency

### Earnings and Payouts

* earnings calculation
* tip
* adjustment
* hold
* payout creation
* duplicate payout
* payout failure
* reconciliation

### Security

* unauthorized financial action
* privileged action enforcement
* sensitive-data redaction

### Jobs

* reconciliation
* retry
* worker restart
* duplicate execution

## 51. Documentation

Create or update documentation covering:

* pricing model
* quote lifecycle
* pricing versions
* promotions
* final fares
* payment provider abstraction
* payment state machine
* refunds
* webhooks
* ledger
* earnings
* tips
* payouts
* holds
* reconciliation
* financial audit
* security and privacy
* operational procedures

Documentation must describe actual implementation behavior.

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not redesign trip lifecycle.

Do not implement dispatch matching.

Do not implement driver location.

Do not implement notification delivery.

Do not implement rider-driver messaging.

Do not implement ratings.

Do not implement safety cases.

Do not implement support workflows.

Do not implement fleet maintenance.

Do not implement analytics/reporting pipelines beyond financial events required here.

Do not hard-code a proprietary surge algorithm.

Do not expose provider SDK types throughout the application.

Do not store payment credentials.

Do not create a second financial ledger.

Do not create another payment volume covering the same responsibilities.

Do not create a surprise integration phase.

# REPOSITORY INSPECTION REQUIREMENTS

Before implementation:

1. Inspect the backend repository.
2. Inspect Backend Volumes 1–5 implementation.
3. Inspect trip and dispatch implementations.
4. Inspect database schema and migrations.
5. Inspect money/currency utilities if already present.
6. Inspect event/outbox infrastructure.
7. Inspect job infrastructure.
8. Inspect authentication/authorization.
9. Inspect audit infrastructure.
10. Inspect configuration infrastructure.
11. Inspect provider abstractions already present.
12. Read the pricing/payment/earnings/payout contracts.
13. Determine exactly which files require creation or modification.

Do not duplicate existing financial infrastructure.

# IMPLEMENTATION RULES

## Preserve Existing Foundations

Reuse:

* database
* transactions
* idempotency
* concurrency
* events
* outbox
* jobs
* authorization
* audit
* observability
* configuration

## Financial Immutability

Never mutate committed ledger history.

Never silently modify captured payment history.

Use explicit adjustment/refund/correction records.

## Provider Isolation

All provider-specific behavior must remain behind the payment/provider adapter.

## Idempotency

Provider-changing actions must be safe to retry.

## Reconciliation

Ambiguous provider states must be recoverable through reconciliation.

## Exact Money

Never use floating-point arithmetic for authoritative amounts.

## Security

Never expose payment credentials or financial secrets.

## No Fake Provider Execution

Do not report a successful external payment, payout, or webhook execution unless a real provider environment was available and actually tested.

# VALIDATION REQUIREMENTS

Execute all supported validation.

At minimum:

* TypeScript compilation
* linting
* formatting
* unit tests
* API integration tests
* Prisma validation
* migration validation
* event/outbox tests
* job tests
* security tests
* OpenAPI validation
* dependency/security scanning where configured

Test:

* money precision
* rounding
* quote expiration
* promotion races
* final fare
* payment idempotency
* provider timeout
* provider ambiguous result
* duplicate webhook
* out-of-order webhook
* capture race
* duplicate refund
* refund limits
* ledger balancing
* ledger immutability
* payout idempotency
* payout failure
* holds
* reconciliation
* unauthorized financial operations

Where a real payment provider is unavailable, use deterministic test doubles or the repository's existing provider abstraction and clearly report that external execution was not performed.

Do not fabricate provider-side results.

# FINAL INTEGRATION CHECK

Before declaring this milestone complete:

1. Verify pricing owns fare calculation and pricing versions.
2. Verify quotes are immutable and expire correctly.
3. Verify monetary arithmetic is exact.
4. Verify currency is explicit.
5. Verify promotions are concurrency-safe.
6. Verify final fare uses authoritative trip facts.
7. Verify payment state is separate from trip state.
8. Verify provider-specific details remain inside adapters.
9. Verify payment creation is idempotent.
10. Verify authorization/capture cannot duplicate.
11. Verify ambiguous provider outcomes are reconcilable.
12. Verify webhooks are authenticated and idempotent.
13. Verify webhook ordering cannot regress internal state incorrectly.
14. Verify refunds cannot exceed refundable amounts.
15. Verify the ledger is immutable.
16. Verify financial corrections use explicit compensating entries.
17. Verify earnings derive from committed financial facts.
18. Verify tips are represented explicitly.
19. Verify payouts cannot duplicate.
20. Verify payout holds are enforced.
21. Verify reconciliation detects meaningful mismatches.
22. Verify financial events use the outbox.
23. Verify privileged financial operations are audited.
24. Verify sensitive financial data is absent from logs/traces.
25. Verify database constraints enforce important financial invariants.
26. Verify failure recovery is implemented.
27. Verify tests cover races and retries.
28. Verify compatibility with Backend Volumes 1–5.
29. Verify the repository is ready for Backend Volume 7.
30. Verify no placeholder or fake payment implementation remains.

# DEFINITION OF DONE

This milestone is complete only when:

* money representation exists
* currency handling exists
* pricing versioning exists
* fare estimates exist
* immutable quotes exist
* quote expiration exists
* deterministic fare calculation exists
* pricing configuration exists
* dynamic-pricing boundary exists
* promotions exist
* promotion idempotency exists
* final fare calculation exists
* fare adjustments exist
* cancellation-fee pricing exists
* payment domain exists
* provider abstraction exists
* Stripe-compatible adapter boundary exists
* payment state machine exists
* payment intents exist
* payment idempotency exists
* authorization exists
* capture exists
* payment failure handling exists
* refunds exist
* webhook handling exists
* webhook idempotency exists
* financial ledger exists
* ledger integrity exists
* financial corrections exist
* driver earnings exist
* tips exist
* payout state exists
* payout idempotency exists
* holds exist
* reconciliation exists
* reconciliation jobs exist
* financial events exist
* transactional outbox integration exists
* privileged financial authorization exists
* financial audit exists
* exact arithmetic and rounding rules exist
* sensitive financial data is protected
* failure/recovery behavior exists
* APIs conform to the architecture
* tests cover normal and adversarial financial flows
* documentation is updated
* no payment credentials are stored
* no duplicate financial authority exists
* no unrelated domain has been implemented
* no placeholder implementation remains
* validation results are truthful
* the backend is ready for Backend Volume 7

# IMPLEMENTATION REPORT

At completion, provide:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Pricing

Summarize:

* money model
* currency
* quotes
* pricing versions
* fare calculation
* dynamic pricing
* promotions
* final fares
* cancellation fees

## Payments

Summarize:

* provider abstraction
* payment state
* authorization
* capture
* refunds
* webhooks
* idempotency

## Financial Ledger

Summarize:

* ledger model
* integrity
* immutability
* corrections
* reconciliation

## Earnings and Payouts

Summarize:

* earnings
* tips
* adjustments
* holds
* payouts

## Security and Audit

Summarize:

* authorization
* privileged operations
* sensitive-data protection
* audit

## Events and Jobs

Summarize:

* financial events
* outbox
* reconciliation jobs
* retries

## Database

Summarize:

* schema
* constraints
* indexes
* transactions
* migrations

## API

Summarize implemented financial endpoints.

## Tests and Validation

List actual commands and actual outcomes.

## External Environment Limitations

State any payment, payout, webhook, or cloud services that could not be exercised.

Do not fabricate provider-side or production financial results.

## Architectural Decisions

Record meaningful financial implementation decisions.

## Known Limitations

List genuine remaining limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement Backend Volume 6 completely.

Extend the existing trip, dispatch, identity, location, event, transaction, and backend foundations.

Implement pricing, quotes, promotions, final fares, payment-provider abstraction, payment state, authorization, capture, refunds, webhooks, immutable financial records, earnings, tips, payouts, holds, reconciliation, events, security, and audit.

Keep trip, dispatch, location, and provider-specific implementation responsibilities properly separated.

Never use floating-point arithmetic for authoritative money.

Never store raw payment credentials.

Never mutate historical financial facts to correct an error.

Do not fabricate external payment-provider execution.

Run every validation command supported by the environment.

Verify idempotency, concurrency, reconciliation, financial integrity, security, and failure recovery.

Finish with the required implementation report and leave the repository in a coherent production-grade state ready for Backend Volume 7.
