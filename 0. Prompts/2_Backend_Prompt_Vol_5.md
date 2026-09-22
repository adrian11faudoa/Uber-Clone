# Uber-Style Global Ride-Hailing & Mobility Platform — Backend Prompt — Volume 5

## ROLE

You are the senior backend engineering organization responsible for implementing the dispatch, matching, driver-offer, and assignment orchestration domain of an original, production-grade global ride-hailing and mobility platform.

Operate simultaneously as:

* Principal Software Architect
* Staff Backend Engineer
* Distributed Systems Engineer
* Dispatch Systems Architect
* Distributed Systems Engineer
* Geospatial Systems Engineer
* Database Architect
* Realtime Systems Engineer
* Performance Engineer
* Reliability Engineer
* Security Engineer
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

This milestone implements the backend dispatch and matching system that connects dispatchable ride requests with eligible drivers.

The platform is architected for targets such as:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* 100,000+ concurrent realtime sessions and higher during peak
* high-frequency driver location ingestion
* multi-region production operation
* high-throughput asynchronous processing

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

Backend Volumes 1–4 establish:

* backend platform foundations
* identity and account ownership
* authentication and authorization
* driver onboarding and vehicles
* driver availability and work sessions
* location ingestion and freshness
* Redis current-location state
* PostGIS foundations
* realtime foundations
* canonical API and event contracts
* idempotency and concurrency
* trip ownership and lifecycle
* trip-side assignment boundaries

Do not depend on the previous AI conversation.

If existing implementation differs from the architecture:

1. inspect the actual implementation
2. preserve compatible working behavior
3. make the minimum coherent changes required
4. document material discrepancies

Do not create competing dispatch or matching systems.

# BACKEND EXECUTION MODEL

This milestone owns dispatch and matching.

Implement:

* dispatch orchestration
* candidate discovery
* eligibility filtering
* spatial candidate selection
* candidate ordering
* dispatch attempts
* driver offers
* offer expiration
* driver acceptance/rejection
* single-winner assignment
* competing-offer protection
* retry and reassignment
* dispatch timeouts
* dispatch cancellation
* dispatch state
* dispatch events
* dispatch realtime behavior
* dispatch observability
* reconciliation

The trip domain remains authoritative for trip lifecycle state.

The driver/location domain remains authoritative for driver operational state and location.

Dispatch coordinates those domains; it does not replace them.

# CURRENT IMPLEMENTATION SCOPE

## 1. Dispatch Domain Boundary

Establish dispatch as the orchestration domain responsible for finding and offering eligible drivers for dispatchable trips.

Dispatch owns:

* dispatch attempt
* candidate set
* candidate ordering
* offer lifecycle
* offer expiration
* dispatch attempt status
* dispatch retry/reassignment
* dispatch outcome
* correlation between trip and offer workflows

Dispatch does not own:

* canonical trip state
* driver account state
* driver current location
* pricing calculations
* payment state

## 2. Dispatch Lifecycle

Implement the canonical dispatch lifecycle defined by the architecture.

The lifecycle must support the actual states in the repository contract, including concepts such as:

* pending
* searching
* offering
* accepted
* rejected
* expired
* cancelled
* exhausted
* completed
* failed

Do not invent states that contradict Architecture Volume 2.

Define valid state transitions and terminal states.

## 3. Dispatch Initiation

Implement dispatch initiation when a trip enters the state that makes it dispatchable.

Validate:

* trip exists
* trip is in a dispatchable state
* trip is not expired
* trip is not cancelled
* trip does not already have a valid active dispatch workflow
* required geographic/service information exists
* required service category exists

Use idempotency so repeated dispatch initiation cannot create uncontrolled duplicate workflows.

## 4. Candidate Discovery

Implement candidate discovery using the location architecture established by Backend Volume 3.

Candidate discovery must consider, as required by the architecture:

* current location
* location freshness
* driver operational availability
* work-session state
* account/driver eligibility
* vehicle/service category
* service area
* operational restrictions
* trip geographic context

Use PostGIS and/or Redis according to the architecture.

Do not make PostgreSQL perform an unbounded full-table scan for every dispatch attempt.

## 5. Spatial Candidate Selection

Implement bounded geographic candidate selection.

Support:

* search radius
* service-area boundaries
* geographic partitioning where appropriate
* expansion strategy
* candidate limits

The implementation must be capable of gradually widening the search when no suitable driver is available, according to the architecture.

Do not create an unbounded search radius.

Do not assume a fixed global radius is appropriate for every market.

## 6. Driver Eligibility

Implement deterministic driver eligibility checks.

Eligibility may consider:

* driver active status
* onboarding/verification status
* vehicle eligibility
* vehicle category
* work-session state
* operational availability
* location freshness
* service area
* account restrictions
* temporary operational blocks
* existing conflicting assignments

Do not duplicate identity ownership logic.

Use the authoritative domain APIs/services established by earlier milestones.

## 7. Candidate Filtering

Filter candidates before creating offers.

Reject candidates that are:

* offline
* stale
* unavailable
* suspended
* already committed
* missing required vehicle capability
* outside required geographic constraints
* otherwise ineligible according to domain contracts

Filtering must be deterministic and observable.

## 8. Candidate Ordering

Implement the candidate-ordering abstraction.

Candidate ordering may incorporate architecture-approved factors such as:

* estimated distance
* estimated arrival time
* vehicle/service compatibility
* operational eligibility
* market-specific configured rules
* fairness or rotation mechanisms where explicitly defined

Do not implement a proprietary hidden algorithm.

Keep the scoring/ordering strategy modular so it can evolve without rewriting dispatch orchestration.

## 9. Estimated Arrival / Routing Boundary

Dispatch may consume ETA/distance data from the routing/geography abstraction.

Do not directly bind dispatch to a specific map provider.

Define timeout and failure behavior for routing dependencies.

If routing data is temporarily unavailable, follow the architecture's documented degraded-mode behavior rather than fabricating precise ETAs.

## 10. Candidate Reservation

Protect candidates from race conditions between:

* multiple dispatch workers
* multiple trips
* retries
* stale candidate lists
* competing offers

Use appropriate short-lived reservation or concurrency mechanisms.

Do not create long-lived locks that can permanently block drivers.

Reservations must have bounded expiration and recovery behavior.

## 11. Driver Offer Model

Implement the canonical driver-offer representation.

An offer should include only data required by the architecture, potentially:

* offer ID
* trip reference
* driver reference
* dispatch attempt reference
* offered-at timestamp
* expiration timestamp
* status
* candidate rank/decision metadata where appropriate
* correlation metadata

Do not place sensitive rider data into offer records unnecessarily.

## 12. Offer Lifecycle

Implement the offer state machine.

Support the contractually required states, such as:

* pending
* accepted
* rejected
* expired
* cancelled
* superseded

Enforce legal transitions.

An expired or rejected offer must not later become accepted.

## 13. Offer Expiration

Implement bounded offer expiration.

Use the shared background-job infrastructure where appropriate.

Expiration must be concurrency-safe with acceptance.

If an offer expires at the same time a driver accepts it, exactly one outcome must win according to the canonical concurrency contract.

Do not allow a stale acceptance to create an inconsistent assignment.

## 14. Driver Offer Acceptance

Implement the driver-side acceptance flow.

Validate:

* authenticated driver
* active session
* offer ownership
* offer status
* expiration
* driver operational eligibility
* trip state
* conflicting assignment state

Acceptance must be atomic with the single-winner assignment decision.

Do not trust a driver ID supplied by the client without authorization.

## 15. Driver Offer Rejection

Implement rejection behavior.

Support:

* authorized rejection
* already-terminal offer
* duplicate rejection
* rejection reason where contractually supported

Rejection must not accidentally cancel the trip itself.

Dispatch may subsequently offer the trip to another driver.

## 16. Single-Winner Assignment

Implement the critical invariant:

> At most one eligible driver may become the authoritative assignment for a dispatchable trip.

Protect this invariant against:

* multiple driver acceptances
* duplicate accept requests
* multiple dispatch workers
* event duplication
* retry
* network timeouts
* concurrent reassignment

Use transactional/concurrency mechanisms rather than in-memory locks alone.

## 17. Trip Assignment Integration

Use the trip domain's assignment contract from Backend Volume 4.

Dispatch must request or apply assignment through the authoritative trip boundary.

Do not directly manipulate unrelated trip internals.

The assignment operation must verify that:

* trip state remains assignable
* no conflicting assignment has won
* driver remains eligible
* offer remains valid

## 18. Driver Availability Integration

Use the driver availability domain rather than duplicating it.

Before final assignment, verify current operational availability.

After a successful assignment, ensure the driver's operational state reflects the assignment according to the established cross-domain contract.

Do not create a second source of truth for driver availability.

## 19. Candidate Reservation Release

Reservations must be released when:

* offer is accepted
* offer rejected
* offer expires
* trip is cancelled
* dispatch attempt fails
* dispatch completes
* reservation TTL expires

Release must be idempotent.

Do not allow abandoned reservations to permanently reduce driver supply.

## 20. Dispatch Retries

Implement retry/reassignment behavior.

When an offer fails because of:

* rejection
* expiration
* transient infrastructure failure
* driver becoming unavailable

dispatch should be able to continue according to the architecture.

Bound retry attempts.

Do not retry indefinitely.

## 21. Search Expansion

Where no suitable driver is available, implement the architecture-defined search expansion strategy.

Expansion may vary by:

* region
* service category
* trip type
* supply state
* configuration

Keep policy configurable.

Do not hard-code business policy that belongs in the configuration/control-plane architecture.

## 22. Dispatch Timeouts

Implement bounded dispatch timeouts.

Define behavior when:

* candidate discovery takes too long
* all offers expire
* no driver accepts
* trip expires
* provider dependencies are unavailable

Dispatch must eventually reach a deterministic terminal or retryable state.

Do not leave dispatch attempts indefinitely pending.

## 23. Dispatch Cancellation

When the trip is cancelled or otherwise no longer dispatchable, terminate active dispatch work.

Handle:

* trip cancellation
* expiration
* administrative intervention
* duplicate cancellation
* worker race

Cancel outstanding offers according to the contract.

## 24. Dispatch Reconciliation

Implement reconciliation capabilities for inconsistent states such as:

* trip dispatchable but no active dispatch
* active dispatch for a terminal trip
* accepted offer without assignment
* reservation without active offer
* stale pending offer
* driver assignment state mismatch

Reconciliation must not silently mutate arbitrary state.

It must use explicit safe correction rules and record anomalies.

## 25. Dispatch Events

Publish canonical dispatch events through the established event infrastructure.

Potential events include:

* dispatch.started
* dispatch.candidate.selected
* dispatch.offer.created
* dispatch.offer.accepted
* dispatch.offer.rejected
* dispatch.offer.expired
* dispatch.assignment.confirmed
* dispatch.reassignment.started
* dispatch.completed
* dispatch.exhausted
* dispatch.failed

Use exact repository naming conventions.

Do not emit internal debugging events as domain contracts.

## 26. Transactional Outbox

Use the shared outbox infrastructure for durable dispatch events that represent committed state changes.

Dispatch state changes and corresponding outbox records must commit atomically.

Do not publish critical dispatch events directly before the transaction commits.

## 27. Event Consumption

Dispatch may consume events such as:

* trip became dispatchable
* driver availability changed
* location freshness changed
* driver became unavailable
* trip cancelled
* trip expired

Consumers must be:

* idempotent
* concurrency-safe
* observable
* retry-safe

Do not assume event delivery exactly once.

## 28. Location Event Handling

Do not copy the complete driver-location system into dispatch.

Instead, consume the authoritative location information required for candidate discovery.

If dispatch maintains a derived spatial index or candidate cache, clearly document it as derived.

Ensure stale data can never silently remain dispatch-eligible beyond the defined freshness policy.

## 29. Realtime Dispatch Offers

Integrate driver offers with the authenticated realtime system.

Send offers only to the authorized driver.

Support:

* offer delivery
* expiration
* acceptance/rejection
* reconnect/recovery
* duplicate messages
* out-of-order messages

Realtime delivery is not proof that the offer is still valid.

The backend must validate the offer state when the driver responds.

## 30. Offer Recovery After Reconnect

When a driver reconnects:

* determine active valid offers from authoritative state
* exclude expired/terminal offers
* return the correct current state
* avoid recreating duplicate offers unnecessarily

Do not rely on in-memory WebSocket state for offer ownership.

## 31. Push/Offline Boundary

If the architecture supports push fallback, expose the required integration event/contract for future notification infrastructure.

Do not implement the entire notification domain here.

The dispatch system must remain correct when the driver is temporarily offline.

An undelivered realtime offer must eventually expire or follow the defined fallback path.

## 32. Dispatch Priority

Where multiple dispatchable trips or candidate opportunities compete for processing resources, define deterministic dispatch scheduling.

Prioritization may consider:

* trip age
* scheduled deadlines
* operational urgency
* configured service priority

Do not invent an arbitrary ranking policy.

Implement only the contractually defined priority rules.

## 33. Database Model and Indexing

Create database structures for dispatch state.

Support queries for:

* active dispatch attempts
* active offers
* offer expiration
* trip dispatch state
* driver offers
* reconciliation
* historical dispatch records

Use indexes based on actual access patterns.

Do not create a database row for every transient location sample.

## 34. Redis Usage

Use Redis for appropriate ephemeral dispatch state such as:

* short-lived candidate/reservation state
* offer TTL support
* distributed coordination where justified
* derived candidate caches

Do not make Redis the only authoritative source of assignment.

Critical assignment state must remain durable.

## 35. Concurrency Strategy

Dispatch correctness must remain safe under:

* multiple workers
* multiple regions where applicable
* duplicate events
* retried API requests
* driver races
* trip cancellation races
* stale cache entries

Use explicit transactional and optimistic concurrency controls.

Do not depend on process-local mutexes for cross-instance correctness.

## 36. Regional Dispatch

Respect the existing regional architecture.

Dispatch should prefer regional drivers and resources according to the configured geography.

Avoid unnecessary cross-region candidate queries on normal critical paths.

Define behavior when a region becomes degraded.

Do not automatically route every dispatch operation through a global coordination point.

## 37. Dispatch Degraded Modes

Define behavior for failures of:

* Redis
* PostgreSQL
* PostGIS
* Kafka/Redpanda
* routing provider
* realtime gateway
* driver-location freshness system

Dispatch must fail safely.

Do not assign drivers based on known-stale critical data merely because it is available.

## 38. Security and Authorization

Protect dispatch operations.

Only authorized:

* drivers
* internal dispatch workers
* operational roles

may execute the applicable commands.

Drivers must only accept their own offers.

Operators must only access dispatch controls permitted by their authorization scope.

Do not expose candidate lists or sensitive driver-location data through ordinary rider APIs.

## 39. Audit

Audit privileged dispatch operations such as:

* administrative dispatch override
* manual assignment
* forced cancellation of dispatch
* exceptional reassignment

Do not audit every candidate-evaluation operation as an individual human action.

## 40. Observability

Expose bounded metrics such as:

* dispatch attempts
* candidate-search latency
* candidate counts
* offer creation rate
* offer acceptance rate
* offer expiration rate
* dispatch success rate
* dispatch exhaustion
* assignment conflicts
* reservation conflicts
* dispatch retry count
* dispatch latency
* stale-candidate rate
* realtime offer failures

Avoid high-cardinality labels containing:

* trip IDs
* driver IDs
* rider IDs
* exact coordinates

Use aggregate dimensions such as:

* region
* service category
* outcome
* error class

## 41. Tracing

Trace representative dispatch flows through:

* trip-triggered dispatch
* candidate discovery
* geospatial query
* eligibility
* reservation
* offer creation
* offer acceptance
* assignment
* outbox
* realtime notification

Do not attach full rider or driver data to traces.

## 42. Failure Monitoring

Detect:

* high offer expiration
* high rejection
* excessive candidate shortages
* candidate-search latency
* assignment conflicts
* reservation leaks
* dispatch backlog
* reconciliation anomalies
* regional dispatch degradation

Alerts must be actionable.

## 43. APIs

Implement the contractually defined dispatch APIs/internal commands.

Potential operations include:

* initiate dispatch
* retrieve dispatch status
* accept offer
* reject offer
* cancel dispatch
* operational inspection where authorized

Only expose the actual API surface defined by the architecture.

Do not create rider-facing candidate APIs.

## 44. Testing

Create comprehensive tests for:

### Candidate Discovery

* eligible driver
* stale driver
* offline driver
* wrong service category
* wrong service area
* suspended driver
* conflicting assignment

### Offers

* creation
* delivery state
* acceptance
* rejection
* expiration
* duplicate acceptance
* acceptance after expiration

### Single Winner

* two drivers accept concurrently
* duplicate acceptance
* multiple workers
* retry races

Only one driver may win.

### Trip Races

* cancellation versus acceptance
* expiration versus acceptance
* assignment versus cancellation
* reassignment versus stale acceptance

### Reservations

* acquisition
* release
* expiration
* duplicate release
* abandoned reservation recovery

### Events

* duplicate delivery
* out-of-order delivery where applicable
* retry
* dead-letter

### Reconnect

* valid active offer
* expired offer
* duplicate offer
* missed realtime message

### Failures

* Redis failure
* database failure
* PostGIS failure
* event-broker failure
* routing-provider failure
* worker restart

## 45. Documentation

Create or update documentation covering:

* dispatch ownership
* candidate discovery
* eligibility
* ordering
* reservations
* offers
* single-winner guarantees
* expiration
* retries
* reassignment
* reconciliation
* realtime offers
* regional behavior
* degraded modes
* observability
* operator controls

Documentation must describe actual implementation behavior.

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not redesign the trip state machine.

Do not implement pricing calculations.

Do not implement payment processing.

Do not implement notification delivery infrastructure.

Do not implement rider-driver messaging.

Do not implement ratings.

Do not implement safety incidents.

Do not implement support workflows.

Do not implement fleet maintenance.

Do not implement scheduled-trip orchestration beyond ordinary dispatch interfaces.

Do not replace the location system.

Do not create a second driver-availability system.

Do not implement a proprietary matching algorithm.

Do not expose raw candidate lists to riders.

Do not create another dispatch volume.

Do not create a surprise integration phase.

# REPOSITORY INSPECTION REQUIREMENTS

Before implementation:

1. Inspect the backend repository.
2. Inspect Backend Volumes 1–4 implementation.
3. Inspect trip lifecycle implementation.
4. Inspect driver availability implementation.
5. Inspect location and PostGIS implementation.
6. Inspect Redis usage.
7. Inspect event/outbox infrastructure.
8. Inspect job infrastructure.
9. Inspect realtime implementation.
10. Inspect authentication and authorization.
11. Inspect pricing boundary contracts.
12. Inspect payment boundary contracts.
13. Read dispatch-related architecture artifacts.
14. Determine exactly which files require creation or modification.

Do not create competing foundations.

# IMPLEMENTATION RULES

## Preserve Existing Foundations

Reuse:

* trip lifecycle
* driver availability
* location
* Redis
* PostGIS
* events
* outbox
* jobs
* realtime
* authorization
* audit
* observability

## Single-Winner Correctness

Assignment correctness must be enforced by durable concurrency controls.

Never rely solely on:

* WebSocket timing
* Redis locks
* in-memory state
* client behavior

## Stale Data

Stale location or eligibility state must never silently become a valid assignment basis.

## Idempotency

All retryable dispatch mutations must behave deterministically.

## Bounded Operations

Candidate search, retries, offers, and reconciliation must have bounded limits.

## Failure Safety

If critical dependencies are unavailable, dispatch must fail safely rather than making unsafe assignments.

## Security

Driver offers and dispatch controls must be authenticated and authorized.

## No Placeholder Work

Every required dispatch capability must be fully implemented.

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
* Redis tests
* PostGIS tests
* event/outbox tests
* job tests
* realtime tests
* OpenAPI validation
* security tests
* dependency/security scanning where configured

Test:

* candidate eligibility
* stale-location exclusion
* service-category matching
* service-area filtering
* offer creation
* offer expiration
* concurrent acceptance
* single-winner assignment
* cancellation/acceptance race
* expiration/acceptance race
* reassignment
* reservation expiration
* duplicate events
* replay
* realtime reconnect
* Redis failure
* database failure
* PostGIS failure
* broker failure
* routing-provider failure

Do not claim measured dispatch throughput or latency without actual benchmark/load-test evidence.

# FINAL INTEGRATION CHECK

Before declaring this milestone complete:

1. Verify dispatch owns only orchestration and offer state.
2. Verify trip state remains authoritative in the trip domain.
3. Verify driver availability remains authoritative in the driver domain.
4. Verify location remains authoritative in the location domain.
5. Verify candidate discovery uses bounded, current-enough data.
6. Verify stale drivers cannot be assigned.
7. Verify candidate eligibility is deterministic.
8. Verify offer state transitions are explicit.
9. Verify offer expiration is race-safe.
10. Verify single-winner assignment is transactionally/concurrently protected.
11. Verify competing workers cannot assign the same trip incorrectly.
12. Verify trip cancellation can safely race with dispatch.
13. Verify reassignment handles stale attempts.
14. Verify reservations have bounded lifetimes and cleanup.
15. Verify dispatch retries are bounded.
16. Verify realtime offers are authorization-controlled.
17. Verify reconnect behavior restores authoritative offer state.
18. Verify dispatch events use the outbox.
19. Verify Redis is not the authoritative assignment store.
20. Verify regional dispatch avoids unnecessary global coordination.
21. Verify degraded modes fail safely.
22. Verify operational overrides are authorized and audited.
23. Verify metrics and traces use bounded cardinality.
24. Verify reconciliation detects important inconsistent states.
25. Verify tests cover driver races and trip races.
26. Verify no pricing, payment, notification, or unrelated business logic has been implemented prematurely.
27. Verify compatibility with Backend Volumes 1–4.
28. Verify the repository is ready for Backend Volume 6.
29. Verify no placeholder or fake implementation remains.

# DEFINITION OF DONE

This milestone is complete only when:

* dispatch domain exists
* dispatch lifecycle exists
* dispatch initiation exists
* candidate discovery exists
* spatial candidate selection exists
* driver eligibility filtering exists
* candidate ordering abstraction exists
* routing boundary exists
* candidate reservation exists
* driver offers exist
* offer lifecycle exists
* offer expiration exists
* driver acceptance exists
* driver rejection exists
* single-winner assignment exists
* trip assignment integration exists
* availability integration exists
* reservation release exists
* retry/reassignment exists
* search expansion exists where required
* dispatch timeouts exist
* dispatch cancellation exists
* reconciliation exists
* dispatch events exist
* transactional outbox integration exists
* required event consumers exist
* location-event integration exists
* realtime offers exist
* reconnect/recovery exists
* regional dispatch behavior exists
* degraded modes exist
* security and authorization exist
* audit for privileged dispatch actions exists
* metrics and traces exist
* APIs conform to the architecture
* tests cover concurrency and failure
* documentation is updated
* no proprietary matching algorithm has been invented
* no later payment/pricing implementation has been introduced
* no duplicate availability/location/trip authority exists
* no placeholder implementation remains
* validation results are truthful
* the backend is ready for Backend Volume 6

# IMPLEMENTATION REPORT

At completion, provide:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Dispatch Domain

Summarize:

* dispatch lifecycle
* candidate discovery
* eligibility
* ordering
* reservations
* offers
* assignment
* retry/reassignment

## Concurrency and Correctness

Summarize:

* single-winner enforcement
* offer races
* cancellation/assignment races
* expiration/acceptance races
* reservation safety

## Events and Realtime

Summarize:

* dispatch events
* outbox
* event consumers
* realtime offers
* reconnect behavior

## Integration Boundaries

Summarize:

* trip
* driver availability
* location
* routing

## Security and Audit

Summarize:

* authorization
* privileged operations
* audit

## Database and Redis

Summarize:

* dispatch schema
* indexes
* reservations
* ephemeral state
* failure behavior

## Jobs

Summarize:

* offer expiration
* retries
* reconciliation

## API

Summarize implemented dispatch/offer endpoints.

## Tests and Validation

List actual commands and actual outcomes.

## External Environment Limitations

State any external services that could not be exercised.

Do not fabricate production or scale results.

## Architectural Decisions

Record meaningful dispatch implementation decisions.

## Known Limitations

List genuine remaining limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement Backend Volume 5 completely.

Extend the existing trip, driver-availability, location, realtime, event, and backend foundations.

Implement dispatch orchestration, candidate discovery, eligibility, ordering, reservations, offers, acceptance, single-winner assignment, retries, reassignment, expiration, reconciliation, events, and realtime offer behavior.

Keep trip state, driver availability, and driver location authoritative in their existing domains.

Do not implement pricing, payment, notifications, or unrelated business domains.

Do not invent a proprietary dispatch algorithm.

Do not leave placeholders.

Run every validation command supported by the environment.

Verify the system under concurrent driver acceptance, cancellation races, expiration races, stale location, duplicate events, reconnects, and dependency failures.

Finish with the required implementation report and leave the repository in a coherent production-grade state ready for Backend Volume 6.
