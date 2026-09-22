# Uber-Style Global Ride-Hailing & Mobility Platform — Backend Prompt — Volume 4

## ROLE

You are the senior backend engineering organization responsible for implementing the canonical ride request and trip lifecycle domain of an original, production-grade global ride-hailing and mobility platform.

Operate simultaneously as:

* Principal Software Architect
* Staff Backend Engineer
* Distributed Systems Engineer
* Domain Architect
* Database Architect
* Reliability Engineer
* Performance Engineer
* Security Engineer
* Realtime Systems Engineer
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

This milestone implements the authoritative ride-request and trip lifecycle domain.

The platform is architected for targets such as:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* 100,000+ concurrent realtime sessions and higher during peak
* high-frequency driver location ingestion
* global multi-region operation
* high availability for critical mobility workflows

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
* PostGIS
* Prisma where compatible with the architecture

### Cache and Ephemeral State

* Redis

### Events

* Kafka or Redpanda

### Background Jobs

* BullMQ or equivalent

### Realtime

* authenticated WebSockets

### Observability

* OpenTelemetry
* Prometheus-compatible metrics
* structured logs
* Loki-compatible logging
* Tempo-compatible tracing

# SOURCE OF TRUTH

The repository is the implementation source of truth.

Inspect the repository before making changes.

Use the architecture artifacts already present in the repository as the authoritative architecture and contract reference.

Backend Volumes 1–3 establish:

* backend platform foundations
* identity and account ownership
* authentication and authorization
* driver onboarding and vehicles
* driver operational state
* driver location and freshness
* Redis current-location state
* PostGIS foundations
* realtime foundations
* canonical identifiers
* API/error/idempotency/concurrency contracts
* event and outbox contracts
* trip lifecycle architecture
* dispatch integration boundaries

Do not depend on the previous AI conversation.

If existing implementation differs from the architecture:

1. inspect the actual implementation
2. preserve compatible working behavior
3. make the minimum coherent changes required
4. document material discrepancies

Do not create competing implementations of the same platform capability.

# BACKEND EXECUTION MODEL

This milestone owns the authoritative trip domain.

Implement:

* ride requests
* trip creation
* trip aggregate/state
* trip state machine
* trip cancellation
* trip expiration
* trip assignment reference handling
* trip timestamps
* trip history
* trip concurrency
* trip idempotency
* trip events
* trip realtime updates
* trip-related authorization
* trip recovery/reconciliation
* trip observability
* foundational interfaces required by dispatch

Do not implement the matching algorithm or driver-offer system in this milestone.

The trip domain must expose clear contracts for Backend Volume 5 to implement dispatch against.

# CURRENT IMPLEMENTATION SCOPE

## 1. Trip Domain Ownership

Establish authoritative ownership of the trip aggregate.

The trip domain owns:

* trip identity
* rider association
* assigned-driver reference
* requested service category
* pickup and destination references
* lifecycle state
* timestamps
* cancellation metadata
* completion metadata
* lifecycle history
* state-transition authority

Do not allow dispatch, pricing, payment, or frontend code to become the authoritative owner of trip lifecycle state.

## 2. Trip Aggregate Model

Implement the canonical trip representation defined by the architecture.

The model should include only fields required by the repository contract.

Potential categories include:

* trip ID
* rider ID
* assigned driver ID where applicable
* vehicle/category reference where applicable
* pickup location/reference
* destination location/reference
* trip state
* request time
* assignment time
* arrival time
* start time
* completion time
* cancellation information
* expiration information
* pricing/quote references
* region/service-area context
* version/concurrency metadata

Do not duplicate the entire pricing or payment model inside the trip table.

Use domain references to those systems.

## 3. Trip State Machine

Implement the canonical trip state machine from Architecture Volume 2.

The implementation must define and enforce:

* legal states
* legal transitions
* transition preconditions
* transition ownership
* transition timestamps
* invalid-transition behavior

The exact state names must match the repository's architecture.

Potential lifecycle concepts include:

* requested
* dispatching
* assigned
* driver arriving
* driver arrived
* in progress
* completed
* cancelled
* expired

Do not add states merely for implementation convenience.

## 4. Transition Invariants

Enforce important trip invariants.

Examples:

* a trip cannot be completed before it starts
* a cancelled trip cannot later become active
* an expired trip cannot be assigned normally
* assignment must reference an eligible/authorized driver
* active trip transitions must be serialized correctly
* terminal states remain terminal

Use the repository's precise contract rather than relying only on examples.

## 5. Trip Creation

Implement the canonical trip-request flow.

Validate:

* authenticated rider
* rider account state
* request schema
* service category
* pickup/destination validity
* idempotency requirements
* region/service-area constraints defined by the architecture
* required pricing/quote reference where the contract requires one

Create the trip atomically.

Do not perform dispatch matching inside trip creation.

## 6. Trip Creation Idempotency

Integrate trip creation with the shared idempotency infrastructure.

Handle:

* first request
* duplicate identical request
* same key with different request
* concurrent requests
* retried requests after partial infrastructure failure

A client retry must not create multiple equivalent trips.

Do not use a simple in-memory deduplication mechanism.

## 7. Request Validation

Validate all trip-request fields defined by the contract.

At minimum account for:

* pickup information
* destination information
* service category
* quote/pricing reference
* optional metadata allowed by the architecture

Reject malformed or contradictory requests.

Do not trust client-provided internal references without authorization and validation.

## 8. Pickup and Destination Model

Implement the canonical representation for trip origin and destination.

Use the architecture's chosen representation for:

* coordinates
* place references
* formatted address
* geographic context

Avoid storing redundant representations unless there is a defined purpose.

Treat exact location data as sensitive.

## 9. Trip Region and Service Context

Associate the trip with the relevant geographic context where the architecture requires it.

The context may include:

* region
* country/market
* service area
* currency
* service category

Do not duplicate global geography logic from the location domain.

## 10. Trip Versioning and Concurrency

Use optimistic concurrency/versioning as defined by Architecture Volume 2.

Every state-changing operation must protect against:

* concurrent cancellation
* concurrent assignment
* duplicate driver-arrival transitions
* concurrent start
* concurrent completion
* administrative intervention

Do not use unconditional updates for state transitions when multiple actors can race.

## 11. Transactional State Transitions

Trip state transitions must be atomic.

A transition must ensure that:

* the expected current state is correct
* all required fields are updated together
* transition history is persisted consistently
* required outbox events are created in the same transaction

Do not publish a trip event before the authoritative database transaction commits.

## 12. Trip History

Implement an append-oriented trip state history where required.

Record:

* transition identity
* trip ID
* previous state
* new state
* actor/context
* timestamp
* reason where applicable
* request/correlation ID
* relevant metadata

History must remain useful for:

* customer support
* operational investigation
* reconciliation
* analytics
* incident analysis

Do not make history dependent on application logs.

## 13. Cancellation

Implement trip cancellation according to the architecture.

Support the cancellation actors actually defined by the project, potentially including:

* rider
* driver
* operations
* system

Define:

* permitted states
* authorization
* cancellation reason
* timestamps
* resulting state
* event publication
* interaction with dispatch

Do not implement the full cancellation-fee pricing calculation here.

Store the information pricing will need.

## 14. Cancellation Concurrency

Cancellation must be safe when it races with:

* driver acceptance/assignment
* driver arrival
* trip start
* system expiration
* operator intervention

Use the canonical concurrency mechanism.

A cancelled trip must not later transition into a normal active-trip state.

## 15. Expiration

Implement trip expiration where the architecture requires it.

Support:

* expiration deadline
* expiration state transition
* scheduled/background processing
* race protection
* event publication
* operational observability

Expiration processing must be idempotent.

Do not allow an expired request to remain indefinitely dispatchable.

## 16. Expiration Job

Use the shared BullMQ infrastructure for expiration work where appropriate.

The job must:

* verify the trip is still eligible for expiration
* perform the transition transactionally
* avoid racing with valid assignment/transition
* publish the required event
* record failure
* retry safely

Do not mark an already-assigned or active trip as expired merely because a stale job executes.

## 17. Assignment Reference Boundary

Implement the trip-side representation of assignment.

The trip domain must be capable of recording:

* assigned driver
* assignment time
* assignment source/reference
* assignment version where required

But dispatch itself remains outside this milestone.

Do not implement:

* candidate search
* matching
* offer ranking
* offer lifecycle

Backend Volume 5 owns those capabilities.

## 18. Assignment Concurrency Invariant

Enforce the trip-side invariant that a trip has at most one authoritative active assignment at a time.

Support safe handling of:

* competing dispatch workers
* duplicate assignment messages
* reassignment
* stale assignment attempts
* cancellation racing with assignment

Do not create a second assignment authority.

## 19. Assignment Integration Contract

Expose an internal contract for dispatch to request or apply assignment.

The contract must include the architectural prerequisites for:

* verifying trip state
* verifying assignment eligibility
* atomically committing assignment
* returning conflict information
* generating the required event

Do not embed dispatch scoring logic here.

## 20. Trip Commands

Implement the trip commands defined by the architecture.

These may include:

* create trip
* cancel trip
* assign trip
* transition trip state
* mark arrival
* start trip
* complete trip
* expire trip

Only implement commands actually defined by the repository contracts.

Every command must have:

* authorization
* validation
* idempotency/concurrency handling where applicable
* state-transition rules
* event behavior

## 21. Driver Actions

Where the trip contract requires driver actions, implement only their trip-side state transitions.

Examples:

* acknowledge assignment
* driver arriving
* driver arrived
* trip started
* trip completed
* driver-initiated cancellation

Do not implement dispatch-offer acceptance here.

That remains part of the dispatch milestone.

## 22. Rider Actions

Implement trip-side rider actions defined by the contract:

* trip request
* cancellation
* status retrieval
* trip history retrieval where applicable

Do not implement frontend-specific behavior.

## 23. Trip Authorization

Implement resource authorization.

Riders must only access their own trips.

Drivers must only access trips they are authorized to participate in.

Operators/support/safety personnel must use the appropriate privileged scopes.

Do not expose arbitrary trip access based solely on knowing a trip ID.

## 24. Trip Retrieval

Implement the contractually defined trip retrieval APIs.

Support appropriate:

* authorization
* resource lookup
* error behavior
* response shaping

Do not return internal infrastructure metadata to clients.

Do not expose other participants' sensitive information beyond the contract.

## 25. Trip History Queries

Where trip history is part of this backend milestone, implement repository-compatible access patterns for:

* rider trip history
* authorized driver trip history where applicable
* operational lookup where defined

Use cursor pagination for high-volume histories.

Do not implement operational full-text search here.

That belongs to the support/operations/search milestone.

## 26. Trip Event Model

Publish the canonical trip events required by the architecture.

Potential events include:

* trip.created
* trip.dispatching
* trip.assigned
* trip.arriving
* trip.arrived
* trip.started
* trip.completed
* trip.cancelled
* trip.expired

Use the exact event naming convention defined in Architecture Volume 2.

Events must represent committed domain facts.

## 27. Transactional Outbox Integration

All durable trip-domain events that correspond to database state changes must be created through the shared transactional outbox.

A database transition and its corresponding event record must commit atomically.

Do not publish directly to Kafka inside the transaction.

## 28. Trip Event Payload Discipline

Include the minimum information required by consumers.

Do not put:

* passwords
* tokens
* unnecessary personal data
* private messages
* sensitive operational details

into trip events.

Use identifiers and references instead of duplicating entire domain records.

## 29. Realtime Trip Updates

Integrate trip state changes with the established realtime architecture.

Authorized participants should receive appropriate trip updates for:

* state changes
* assignment
* driver arrival
* trip start
* trip completion
* cancellation

Realtime propagation must originate from authoritative state/events rather than becoming the source of truth.

## 30. Realtime Recovery

Ensure clients can recover from:

* reconnect
* missed messages
* out-of-order delivery
* duplicate delivery
* temporary gateway failure

Provide enough authoritative trip state for clients to resynchronize.

Do not depend on receiving every individual realtime message.

## 31. Trip Read Model and Realtime State

Where a lightweight Redis-backed realtime representation is useful, keep it derived from the authoritative trip database/event stream.

Do not make Redis authoritative for trip state.

Define TTL/invalidation behavior for any trip-related ephemeral data.

## 32. Pricing Boundary

Integrate with the pricing contract without implementing pricing logic.

The trip domain may store:

* quote reference
* pricing version/reference
* currency
* fare commitment reference

But pricing calculation remains owned by the pricing domain.

Do not recalculate fares in the trip module.

## 33. Payment Boundary

Integrate with future payment functionality without implementing payment processing.

The trip domain may expose:

* financial status references
* fare commitment reference
* completion event
* cancellation reason

Payment state remains owned by the payment domain.

Do not write payment-provider calls from trip handlers.

## 34. Location Boundary

Trip state must integrate with driver-location information without becoming its owner.

Use the existing location/realtime contracts for:

* driver position
* freshness
* arrival context where required

Do not duplicate the driver-location storage system.

## 35. Dispatch Boundary

Trip APIs and internal commands must expose the state information required by dispatch.

Dispatch must later be able to determine:

* dispatchable state
* expiration
* service category
* pickup
* destination
* region
* assignment status

Do not implement matching here.

## 36. Data Constraints and Indexes

Create database constraints and indexes based on actual trip query patterns.

Support:

* rider history
* driver history
* active-trip lookup
* state filtering
* assignment lookup
* expiration lookup
* recent-trip retrieval
* trip history ordering

Avoid indexing every field.

Consider write volume and retention.

## 37. State-Transition Integrity

Enforce state transitions at a layer that prevents arbitrary direct mutation.

Domain code must use explicit transition functions/services.

Do not allow generic repository updates to bypass trip lifecycle invariants.

## 38. Administrative Intervention

Where the architecture permits operator intervention, create controlled internal capabilities for:

* cancellation
* state correction where explicitly authorized
* investigation metadata

Administrative corrections must be:

* authorized
* audited
* explicit
* traceable

Do not provide an unrestricted "set any trip state" endpoint.

## 39. Audit

Audit security-sensitive or exceptional trip operations such as:

* administrative cancellation
* administrative state correction
* privileged trip access
* exceptional assignment correction

Do not create audit records for every normal realtime location update.

## 40. Background Jobs and Reconciliation

Implement jobs for:

* trip expiration
* stale-state reconciliation where required
* transition consistency checks
* outbox/reconciliation support where appropriate

Jobs must be:

* idempotent
* bounded
* retry-safe
* observable

Do not build a parallel scheduling system.

## 41. Failure Handling

Handle:

* database conflict
* duplicate commands
* out-of-order operations
* Redis outage
* Kafka/outbox failure
* worker failure
* realtime gateway failure

A temporary event-broker failure must not cause the trip transaction itself to become inconsistent.

## 42. Metrics

Expose bounded metrics such as:

* trip creation rate
* trip creation failures
* active trips
* transition failures
* cancellation rate
* expiration count
* assignment-conflict count
* state-transition latency
* trip event backlog
* realtime propagation failures

Do not use raw trip IDs as metric labels.

## 43. Tracing

Trace representative flows through:

* API
* validation
* authorization
* transaction
* outbox creation
* event publication
* background expiration
* realtime propagation

Do not attach sensitive pickup/destination payloads unnecessarily to traces.

## 44. API Layer

Implement the architecture-defined trip APIs.

Only implement endpoints actually defined by the repository contract.

Do not invent frontend-specific endpoints.

Apply:

* authentication
* authorization
* validation
* idempotency
* concurrency
* error contract
* pagination where applicable

## 45. Testing

Create comprehensive tests covering:

### Trip Creation

* valid request
* invalid request
* unauthorized rider
* duplicate request
* idempotency conflict
* transaction failure

### State Machine

* valid transitions
* invalid transitions
* terminal-state protection
* concurrent transitions

### Cancellation

* permitted cancellation
* unauthorized cancellation
* duplicate cancellation
* cancellation races

### Expiration

* eligible expiration
* already-assigned trip
* already-cancelled trip
* worker retry
* duplicate expiration

### Assignment Boundary

* valid assignment
* stale assignment
* competing assignment
* assignment after cancellation
* duplicate assignment

### Authorization

* rider ownership
* driver participation
* privileged operator access

### Events

* outbox creation
* event publication
* duplicate processing
* event failure/retry

### Realtime

* authorized trip updates
* reconnect/resynchronization
* duplicate messages
* out-of-order messages

## 46. Documentation

Create or update documentation covering:

* trip domain ownership
* state machine
* state-transition invariants
* request lifecycle
* cancellation
* expiration
* assignment boundary
* events
* outbox
* realtime
* authorization
* operational intervention
* reconciliation
* observability

Documentation must describe the actual implementation.

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement:

* dispatch candidate search
* dispatch scoring
* driver offers
* offer acceptance
* dispatch ranking
* pricing calculation
* dynamic pricing
* payment processing
* payment provider calls
* driver earnings
* payouts
* notifications
* messaging
* ratings
* safety incidents
* support cases
* fleet maintenance
* scheduled-trip workflows
* analytics/reporting pipelines

Do not implement a proprietary dispatch algorithm.

Do not move trip state authority into Redis.

Do not make realtime messages authoritative.

Do not duplicate location storage.

Do not duplicate authentication/authorization foundations.

Do not create another trip lifecycle backend volume.

Do not create a surprise integration phase.

# REPOSITORY INSPECTION REQUIREMENTS

Before implementation:

1. Inspect the backend repository.
2. Inspect Backend Volumes 1–3 implementation.
3. Inspect Prisma schema and migrations.
4. Inspect identity/account models.
5. Inspect driver and vehicle models.
6. Inspect Redis abstractions.
7. Inspect event/outbox infrastructure.
8. Inspect background jobs.
9. Inspect realtime infrastructure.
10. Inspect API conventions.
11. Inspect idempotency and concurrency utilities.
12. Inspect audit infrastructure.
13. Inspect location/availability contracts and implementation.
14. Read the trip, dispatch, pricing, and payment contracts from the architecture artifacts.
15. Determine exactly which files require changes.

Do not duplicate existing platform infrastructure.

# IMPLEMENTATION RULES

## Preserve Existing Foundations

Reuse:

* configuration
* database
* Redis
* errors
* request context
* authorization
* idempotency
* concurrency
* outbox
* events
* jobs
* realtime
* audit
* observability

## State Machine Integrity

All trip state changes must pass through explicit transition logic.

## Transactional Correctness

A state transition and its required outbox records must commit atomically.

## Idempotency

Trip creation and other retryable mutations must behave deterministically under duplicate requests.

## Concurrency

Use optimistic concurrency/version checks or appropriate transactional techniques.

Do not rely on process-local state.

## Authorization

Never authorize a user merely because they know a trip ID.

## Event Discipline

Emit committed business facts only.

## Realtime Discipline

Realtime must reflect authoritative trip state.

## External Providers

Do not call payment or mapping providers from the trip domain unless the architecture explicitly assigns that responsibility here.

## No Placeholder Work

Every required feature must be implemented completely.

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
* Redis integration tests
* event/outbox tests
* job tests
* realtime tests
* OpenAPI validation
* security tests
* dependency/security scanning where configured

Test:

* duplicate trip creation
* idempotency conflict
* invalid state transitions
* concurrent transitions
* cancellation races
* assignment races
* expiration races
* terminal-state protection
* authorization failures
* event publication failure
* worker restart
* Redis outage behavior
* realtime reconnect
* duplicate/out-of-order realtime messages
* administrative authorization

Do not claim production-scale capacity without actual load-testing evidence.

# FINAL INTEGRATION CHECK

Before declaring this milestone complete:

1. Verify trip state has one authoritative owner.
2. Verify the complete trip state machine matches the architecture contract.
3. Verify invalid transitions are rejected.
4. Verify terminal states remain terminal.
5. Verify trip creation is idempotent.
6. Verify state transitions are concurrency-safe.
7. Verify transition history is durable.
8. Verify cancellations are authorization-protected and race-safe.
9. Verify expiration cannot override valid assignment or active state.
10. Verify the trip-side assignment boundary is ready for dispatch.
11. Verify no dispatch matching logic has been introduced.
12. Verify outbox records are committed transactionally with trip changes.
13. Verify event payloads are minimal and privacy-safe.
14. Verify realtime updates originate from authoritative state.
15. Verify clients can recover after missed realtime messages.
16. Verify pricing and payment remain separate domain authorities.
17. Verify location remains owned by the location domain.
18. Verify privileged operational changes are audited.
19. Verify indexes match actual trip query patterns.
20. Verify reconciliation/expiration jobs are retry-safe.
21. Verify metrics and traces have bounded cardinality.
22. Verify tests cover concurrency and failure scenarios.
23. Verify compatibility with Backend Volumes 1–3.
24. Verify the repository is ready for Backend Volume 5.
25. Verify no placeholder or fake implementation remains.

# DEFINITION OF DONE

This milestone is complete only when:

* trip aggregate exists
* trip state machine exists
* legal transitions are enforced
* state-transition invariants exist
* trip creation exists
* trip creation idempotency exists
* pickup/destination representation exists
* geographic context exists where required
* concurrency/versioning exists
* transactional state transitions exist
* trip history exists
* cancellation exists
* cancellation concurrency protection exists
* expiration exists
* expiration jobs exist
* assignment reference boundary exists
* assignment concurrency invariant exists
* trip commands exist
* rider trip actions exist
* driver trip actions exist where contractually required
* trip authorization exists
* trip retrieval exists
* history retrieval exists where in scope
* trip events exist
* transactional outbox integration exists
* realtime trip updates exist
* realtime recovery exists
* pricing boundary exists
* payment boundary exists
* location boundary exists
* dispatch integration boundary exists
* database constraints/indexes exist
* administrative interventions are controlled and audited
* reconciliation jobs exist where required
* failure handling exists
* metrics and tracing exist
* APIs conform to the architecture
* tests cover correctness, races, and failure modes
* documentation is updated
* no dispatch algorithm has been implemented prematurely
* no unrelated domain has been implemented
* no placeholder implementation remains
* validation results are truthful
* the backend is ready for Backend Volume 5

# IMPLEMENTATION REPORT

At completion, provide:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Trip Domain

Summarize:

* aggregate
* state machine
* lifecycle
* cancellation
* expiration
* history

## Concurrency and Idempotency

Summarize:

* idempotency
* versioning
* state-transition concurrency
* assignment conflicts

## Events and Realtime

Summarize:

* trip events
* outbox
* realtime propagation
* recovery

## Domain Boundaries

Summarize:

* dispatch boundary
* pricing boundary
* payment boundary
* location boundary

## Security and Authorization

Summarize:

* rider access
* driver access
* operational access
* audit

## Database

Summarize:

* schema changes
* constraints
* indexes
* transactions
* migrations

## Jobs

Summarize:

* expiration
* reconciliation
* retries

## API

Summarize implemented trip endpoints.

## Tests and Validation

List actual commands and outcomes.

## External Environment Limitations

State any external systems that could not be exercised.

Do not fabricate production execution or scale results.

## Architectural Decisions

Record meaningful implementation decisions.

## Known Limitations

List genuine remaining limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement Backend Volume 4 completely.

Extend the existing platform, identity, driver, availability, and location foundations.

Implement the authoritative trip lifecycle, including creation, state transitions, cancellation, expiration, assignment boundaries, history, events, realtime updates, concurrency, and idempotency.

Do not implement dispatch matching yet.

Do not implement pricing or payment processing yet.

Do not leave placeholders.

Do not move authoritative trip state into Redis or realtime.

Run every validation command supported by the environment.

Verify concurrency, authorization, state-machine correctness, event consistency, realtime recovery, and failure handling.

Finish with the required implementation report and leave the repository in a coherent production-grade state ready for Backend Volume 5.
