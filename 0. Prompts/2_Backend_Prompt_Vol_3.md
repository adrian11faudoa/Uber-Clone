# Uber-Style Global Ride-Hailing & Mobility Platform — Backend Prompt — Volume 3

## ROLE

You are the senior backend engineering organization responsible for implementing the driver availability, work-session, location, presence, geospatial, and realtime-location foundation of an original, production-grade global ride-hailing and mobility platform.

Operate simultaneously as:

* Principal Software Architect
* Staff Backend Engineer
* Distributed Systems Engineer
* Geospatial Systems Engineer
* Realtime Systems Engineer
* Database Architect
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

This milestone establishes the backend foundation for driver operational state and high-frequency geospatial location.

The platform is architected for targets such as:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* 100,000+ concurrent realtime sessions and higher during peak
* high-frequency driver location ingestion
* multi-region production operation

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

Backend Volumes 1 and 2 establish:

* backend platform foundations
* identity/account ownership
* authentication and sessions
* authorization
* canonical identifiers
* API behavior
* idempotency
* concurrency
* event envelopes
* outbox/inbox behavior
* realtime contracts
* location contracts
* driver availability concepts

Do not depend on the previous AI conversation.

If existing implementation differs from the architecture:

1. inspect the actual implementation
2. preserve compatible working behavior
3. make the minimum coherent changes required
4. document material discrepancies

Do not create competing implementations of the same platform capability.

# BACKEND EXECUTION MODEL

This milestone owns driver operational state and location infrastructure.

Implement:

* driver work sessions
* operational availability
* location ingestion
* location validation
* sequence/order handling
* freshness tracking
* Redis-backed current-location state
* PostGIS geospatial support
* driver presence
* stale-driver cleanup
* location events
* location-related realtime propagation
* location observability
* foundational dispatch-consumer integration points

Do not implement full dispatch matching in this milestone.

Do not implement trip state.

Do not implement pricing or payments.

# CURRENT IMPLEMENTATION SCOPE

## 1. Driver Operational State Boundary

Establish the backend ownership of driver operational state.

Clearly distinguish:

* account status
* onboarding/verification status
* operational availability
* current work session
* current location
* active assignment state, which belongs to later trip/dispatch domains

A verified driver is not automatically an available driver.

An authenticated driver is not automatically operationally eligible.

## 2. Work Session Model

Implement driver work-session state.

A work session should support, according to the architecture:

* session identifier
* driver identifier
* start time
* end time
* current operational state
* device/session context where required
* region/service-area context
* last activity
* lifecycle status

Work sessions must be auditable and concurrency-safe.

## 3. Availability State Machine

Implement the driver availability state machine established by the architecture.

Use the repository's canonical states.

At minimum, support the appropriate distinctions between:

* offline
* online/unavailable
* available
* temporarily unavailable
* ended session

Do not introduce state names that contradict Architecture Volume 2.

Every state transition must validate:

* authenticated driver
* account state
* onboarding/verification eligibility
* active work session
* conflicting existing state
* required location readiness where the architecture requires it

## 4. Availability Concurrency

Prevent conflicting simultaneous availability transitions.

Handle:

* duplicate requests
* concurrent enable/disable requests
* multiple devices
* reconnects
* process retries

Use the established idempotency and concurrency infrastructure.

Do not depend on in-memory state for correctness.

## 5. Operational Eligibility

Create the backend checks required to determine whether a driver may become dispatch-eligible.

The eligibility foundation may include:

* account active state
* driver onboarding approved state
* required vehicle association
* required service-area association
* valid work session
* sufficiently fresh location
* operational restrictions

Do not implement the actual dispatch candidate-ranking algorithm.

Return or expose deterministic eligibility reasons for internal consumers.

## 6. Location Ingestion Endpoint

Implement the canonical location-ingestion contract.

Accept the location payload defined by Architecture Volume 2, including only fields actually required by the repository.

Handle:

* latitude
* longitude
* timestamp
* accuracy
* heading where supported
* speed where supported
* sequence/version
* device/session reference where required
* source metadata where required

Validate all values.

Reject:

* invalid coordinates
* impossible ranges
* malformed timestamps
* invalid sequence data
* payloads exceeding defined size constraints

## 7. Location Authentication and Authorization

Only authorized driver/device sessions may publish driver location.

Validate that:

* the authenticated principal is a driver where required
* the driver may publish for the referenced session/device
* the session is valid
* the account is not suspended
* the driver is not impersonating another driver
* stale/revoked sessions cannot continue publishing

Do not trust a driver ID supplied by the client as sufficient authorization.

## 8. Location Ordering

Implement sequence/order protection.

The system must identify and safely handle:

* duplicate location messages
* delayed messages
* out-of-order updates
* reconnects
* device clock anomalies

Use the canonical sequence/version model from Architecture Volume 2.

Do not allow an older update to overwrite a newer authoritative current-location state.

## 9. Timestamp Handling

Distinguish:

* device-observed timestamp
* server-received timestamp
* server-accepted timestamp where applicable

Do not assume client clocks are perfectly synchronized.

Define stale and future-skew behavior.

Reject or quarantine obviously invalid timestamps according to the contract.

Do not silently rewrite all timestamps without preserving the original event metadata.

## 10. Location Freshness

Implement a canonical freshness model.

Provide:

* last accepted location
* last accepted timestamp
* server receipt time
* freshness status
* stale threshold
* unavailable/stale transition

Freshness must be available to downstream dispatch and operational consumers.

Do not let a driver remain dispatch-eligible indefinitely merely because the last known location exists.

## 11. Current Location Storage

Use Redis for appropriate ephemeral current-location state.

Store only the data required by the operational architecture.

Define:

* deterministic keys
* TTL
* update semantics
* invalidation
* stale detection
* region/service-area scope

Do not store unbounded historical location streams in Redis.

Redis must not become the durable historical source of truth.

## 12. Location TTL and Expiration

Every ephemeral current-location record must have explicit expiration semantics.

Handle:

* normal refresh
* location silence
* session termination
* driver logout
* availability termination
* Redis expiration
* regional failover

Expiration must not silently make the driver appear healthy.

## 13. PostGIS Location Support

Implement the durable/geospatial database structures actually required by the architecture.

Where historical trip-associated or operational location records are required:

* use appropriate PostGIS types
* choose proper SRID
* create useful spatial indexes
* preserve timestamp/indexing strategy
* avoid unnecessary high-frequency writes when the architecture only requires ephemeral state

Do not blindly persist every high-frequency location sample to PostgreSQL if the architecture does not require it.

## 14. Geospatial Indexing

Implement spatial indexes appropriate to expected query patterns.

Validate that index strategy supports operations such as:

* nearby-driver discovery foundations
* service-area checks
* geographic containment
* operational location lookup

Do not implement the complete dispatch candidate search algorithm.

Avoid excessive indexes that create unacceptable write overhead.

## 15. Location History Boundary

If the architecture requires durable location history, clearly separate:

* operational current location
* trip-associated location history
* analytics-derived location data

Only implement the durable location history required by this milestone.

Do not create a second historical storage system outside the architecture.

## 16. Presence Model

Implement driver presence state where required.

Presence should represent whether the platform has recent operational connectivity for the driver.

Support:

* connected/active
* stale
* disconnected
* explicitly offline

The exact canonical states must match Architecture Volume 2.

Presence must not be equated automatically with dispatch eligibility.

## 17. Realtime Location Propagation

Integrate accepted location updates with the realtime foundation.

Support authorized propagation to appropriate consumers such as:

* active-trip participants
* operational clients
* authorized internal services

Do not broadcast driver location globally.

Do not expose one driver's precise location to unauthorized riders or other drivers.

## 18. Realtime Location Authorization

Enforce resource and purpose authorization before emitting location updates.

Examples:

* rider may see the assigned driver's appropriate location during an authorized trip
* driver may see authorized trip-related information
* operations may access location according to role and scope
* unrelated riders must not receive arbitrary driver locations

Do not let WebSocket subscription identifiers bypass authorization.

## 19. Location Event Publication

Publish accepted location events through the established event infrastructure where the architecture requires them.

Events must include the canonical envelope and appropriate location metadata.

Do not publish every internal Redis mutation as a domain event.

Only publish events required by the architectural contract.

## 20. Location Event Volume Controls

High-frequency location traffic must be treated differently from ordinary business events.

Implement appropriate controls for:

* batching where contractually safe
* sampling where explicitly permitted
* backpressure
* event-size limits
* producer configuration
* consumer isolation

Do not silently drop business-critical state updates merely to reduce event volume.

## 21. Stale-Driver Detection

Implement background processing for stale driver state.

Support:

* detecting drivers whose location exceeded the freshness threshold
* updating presence/freshness
* removing dispatch eligibility
* expiring ephemeral location
* producing required events

The job must be:

* idempotent
* bounded
* observable
* safe to retry

## 22. Session and Location Cleanup

When a driver:

* logs out
* ends a work session
* becomes suspended
* loses authorization
* becomes stale

ensure location/presence state follows the architecture's rules.

Do not leave stale location data indefinitely active.

## 23. Multi-Device Handling

Handle drivers using more than one authorized device/session where the architecture permits it.

Define:

* active location source
* source precedence
* sequence behavior
* device revocation
* conflicting location streams

Do not let two devices race to overwrite current state without deterministic rules.

## 24. Mobile Location Characteristics

The backend must tolerate realistic mobile behavior:

* intermittent connectivity
* delayed uploads
* background throttling
* duplicate batches
* temporary offline operation
* reconnection
* changing GPS accuracy
* inaccurate device timestamps

Do not assume constant connectivity or perfectly sampled locations.

## 25. Location Accuracy and Quality

Store or propagate location-quality metadata where defined by the contract.

Use accuracy and timestamp information appropriately.

Do not treat every coordinate as equally trustworthy.

Do not implement hidden business rules that reject valid locations merely because the GPS accuracy is imperfect unless the architecture defines the threshold.

## 26. Geographic Boundary Validation

Validate that coordinates and geographic references are plausible.

Where service-area validation belongs to this milestone, provide the foundational capability.

Do not hard-code worldwide assumptions that conflict with configured operational regions.

## 27. Driver Eligibility Re-evaluation

Availability changes and location freshness changes must be able to trigger re-evaluation of operational eligibility.

Provide a reusable eligibility result or internal contract.

Do not couple this directly to future dispatch-ranking algorithms.

## 28. Dispatch Integration Boundary

Expose the information later dispatch implementation will need, including:

* driver operational state
* current location
* freshness
* eligibility
* service-area context
* vehicle/category context where already available

Do not implement:

* candidate ranking
* offer generation
* offer acceptance
* dispatch winner selection

Those belong to Backend Volume 5.

## 29. Database Constraints and Indexes

Implement database-level constraints for:

* driver/session relationships
* active work-session uniqueness where required
* valid location references
* valid ownership
* valid state representations

Add indexes based on actual location and operational query patterns.

## 30. Redis Failure Behavior

Define and implement behavior when Redis is unavailable.

Because current location is operationally important, the system must not silently report fresh location when it cannot maintain freshness state.

Do not make PostgreSQL absorb unlimited high-frequency writes merely because Redis is temporarily unavailable.

Follow the architecture's degraded-mode strategy.

## 31. PostGIS Failure Behavior

If PostGIS/database geospatial queries are unavailable:

* do not fabricate location answers
* expose appropriate degraded behavior
* preserve transactional correctness
* avoid silently treating all geographic checks as successful

## 32. Security and Privacy

Treat driver location as highly sensitive operational data.

Do not log:

* exact coordinates unnecessarily
* full location histories
* private trip routes
* unauthorized driver locations

Use redacted/summarized telemetry.

Protect location APIs and realtime channels through authentication and authorization.

## 33. Audit

Audit sensitive operational actions such as:

* changing driver availability
* forcing operational status changes
* administrative access to location where required
* location-access exceptions

Do not create audit records for every high-frequency GPS point unless the architecture explicitly requires it.

## 34. Metrics

Provide bounded metrics such as:

* location ingestion rate
* accepted location rate
* rejected location rate
* stale-driver count
* freshness lag
* Redis update failures
* geospatial query latency
* location event publication failures
* presence transitions
* availability transitions

Do not use raw driver IDs as metric labels.

## 35. Tracing

Trace representative location and availability operations through:

* API
* validation
* Redis
* PostgreSQL/PostGIS where used
* events
* background cleanup
* realtime propagation

Do not attach full coordinate histories to traces.

## 36. API Layer

Implement the architecture-defined endpoints for:

* driver availability
* work-session control
* current-location ingestion
* presence/state where externally exposed

Only implement actual routes defined by repository contracts.

Do not invent arbitrary driver-operations APIs.

## 37. Idempotency

Use the shared idempotency system where required for:

* starting a work session
* ending a work session
* availability transitions

High-frequency location updates should use the sequence/version contract rather than creating unnecessarily expensive idempotency records for every sample unless the architecture explicitly requires it.

## 38. Background Jobs

Implement required jobs for:

* stale-driver detection
* presence cleanup
* expired location cleanup
* work-session reconciliation

Jobs must have:

* bounded concurrency
* retry behavior
* metrics
* tracing
* safe restart behavior

## 39. Testing

Create comprehensive tests for:

### Availability

* valid transitions
* invalid transitions
* duplicate requests
* concurrent requests
* suspended driver
* missing work session

### Work Sessions

* start
* end
* duplicate start
* duplicate end
* concurrent session creation
* forced revocation

### Location

* valid coordinates
* invalid coordinates
* stale timestamp
* future timestamp
* duplicate sequence
* out-of-order sequence
* newer sequence
* device mismatch
* unauthorized driver
* revoked session

### Redis

* current state
* TTL
* expiration
* stale handling
* failure behavior

### PostGIS

* coordinate persistence where required
* geospatial indexing
* containment/nearby foundations where applicable

### Realtime

* authorized propagation
* unauthorized subscription
* reconnect
* stale state

### Events

* event publication
* duplicate delivery tolerance
* publication failure

### Jobs

* stale cleanup
* retries
* idempotency
* restart

## 40. Documentation

Create or update documentation covering:

* driver availability
* work sessions
* location ingestion
* freshness
* ordering
* Redis state
* PostGIS responsibilities
* presence
* stale cleanup
* privacy/security
* realtime location
* dispatch integration boundary
* operational troubleshooting

Documentation must describe actual implementation.

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement:

* trip creation
* trip lifecycle
* dispatch matching
* dispatch offers
* offer acceptance
* dispatch ranking
* pricing
* payments
* earnings
* payouts
* notifications
* messaging
* ratings
* safety incidents
* support cases
* scheduled trips
* fleet maintenance
* analytics pipelines

Do not implement a proprietary matching algorithm.

Do not implement full rider-facing live-trip screens.

Do not implement the frontend or mobile applications.

Do not redesign authentication or account models from Backend Volume 2.

Do not create another location architecture phase.

Do not create a surprise backend integration phase.

# REPOSITORY INSPECTION REQUIREMENTS

Before implementation:

1. Inspect the backend.
2. Inspect identity/account implementation.
3. Inspect Prisma schema and migrations.
4. Inspect Redis integration.
5. Inspect event infrastructure.
6. Inspect outbox/inbox infrastructure.
7. Inspect realtime foundation.
8. Inspect authentication and authorization.
9. Inspect rate limiting.
10. Inspect idempotency infrastructure.
11. Inspect audit infrastructure.
12. Inspect health/readiness infrastructure.
13. Inspect architecture contracts for location and availability.
14. Inspect any existing PostGIS configuration.
15. Determine exactly which files require changes.

Do not duplicate foundational infrastructure.

# IMPLEMENTATION RULES

## Preserve Existing Foundations

Reuse:

* request context
* authentication
* authorization
* errors
* database
* Redis
* idempotency
* events
* jobs
* audit
* telemetry

Do not create parallel infrastructure.

## Location Correctness

Never allow an older location update to overwrite a newer accepted location.

## Privacy

Treat precise driver location as sensitive data.

Do not expose it beyond authorized contexts.

## High Throughput

Do not build the location path around expensive synchronous database writes when ephemeral Redis state and asynchronous persistence are the architecture's intended pattern.

## Bounded Storage

Do not create unbounded location-history growth.

## Failure Safety

Do not report a driver as fresh when freshness cannot actually be established.

## Concurrency

Availability and work-session transitions must remain safe under concurrent requests.

## Events

Publish location/availability events through the established event infrastructure and transactional patterns where required.

## No Placeholder Work

Every required capability must be implemented completely.

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
* PostGIS tests where available
* event tests
* realtime tests
* job tests
* security tests
* OpenAPI validation
* dependency/security scanning where configured

Test:

* invalid coordinates
* stale locations
* out-of-order locations
* duplicate locations
* device conflicts
* unauthorized location submission
* concurrent availability changes
* concurrent session creation
* Redis outage behavior
* database outage behavior
* stale cleanup
* realtime authorization
* event publication failure
* worker restart
* job retry

Do not claim successful production-scale location throughput without load-test evidence.

# FINAL INTEGRATION CHECK

Before declaring this milestone complete:

1. Verify driver availability is owned by this domain.
2. Verify work sessions are concurrency-safe.
3. Verify account/onboarding state controls operational eligibility.
4. Verify location ingestion validates all contract requirements.
5. Verify sequence ordering prevents stale overwrites.
6. Verify freshness semantics are explicit.
7. Verify Redis current-location state uses bounded TTLs.
8. Verify durable location storage is used only where required.
9. Verify PostGIS indexes match actual geospatial needs.
10. Verify presence is distinct from dispatch eligibility.
11. Verify stale-driver cleanup is implemented.
12. Verify session/logout/revocation behavior cleans operational state appropriately.
13. Verify multi-device behavior is deterministic.
14. Verify realtime location propagation is authorization-controlled.
15. Verify location events use the canonical event system.
16. Verify high-volume location traffic is protected from uncontrolled amplification.
17. Verify Redis failure does not produce false freshness.
18. Verify security-sensitive location data is protected from logs and unauthorized access.
19. Verify operational actions are auditable.
20. Verify observability has bounded cardinality.
21. Verify tests cover ordering, concurrency, failure, and authorization.
22. Verify no dispatch algorithm or trip logic has been implemented prematurely.
23. Verify compatibility with Backend Volumes 1 and 2.
24. Verify the repository is ready for Backend Volume 4.
25. Verify no placeholder implementation remains.

# DEFINITION OF DONE

This milestone is complete only when:

* driver work sessions exist
* availability state management exists
* availability concurrency is safe
* operational eligibility foundation exists
* location ingestion exists
* location validation exists
* location ordering exists
* timestamp/freshness handling exists
* Redis current-location state exists
* explicit TTL/expiration exists
* PostGIS support exists where required
* geospatial indexes exist where required
* presence exists
* realtime location propagation exists
* realtime authorization exists
* location events exist where required
* stale-driver cleanup exists
* session/revocation cleanup exists
* multi-device behavior is defined and tested where applicable
* dispatch integration boundaries exist
* database constraints/indexes exist
* Redis/database failure behavior is implemented
* privacy and security controls exist
* audit requirements are implemented
* metrics and tracing exist
* APIs conform to architecture contracts
* background jobs exist where required
* tests cover correctness and adversarial cases
* documentation is updated
* no dispatch/trip business logic outside this milestone exists
* no placeholder implementation remains
* validation results are truthful
* the backend is ready for Backend Volume 4

# IMPLEMENTATION REPORT

At completion, provide:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Availability and Work Sessions

Summarize:

* state machine
* session handling
* concurrency
* eligibility

## Location System

Summarize:

* ingestion
* validation
* ordering
* freshness
* Redis state
* PostGIS
* persistence boundaries

## Presence and Realtime

Summarize:

* presence
* WebSocket propagation
* authorization
* reconnect behavior

## Events and Jobs

Summarize:

* location/availability events
* stale cleanup
* reconciliation jobs
* retries

## Security and Privacy

Summarize:

* authentication
* authorization
* location protection
* audit
* logging redaction

## Database and Redis

Summarize:

* schema
* constraints
* indexes
* TTLs
* failure behavior

## API

Summarize implemented endpoints.

## Tests and Validation

List actual commands and outcomes.

## External Environment Limitations

State any external systems that could not be exercised.

Do not claim successful live-scale or production infrastructure validation when unavailable.

## Architectural Decisions

Record meaningful implementation decisions.

## Known Limitations

List genuine remaining limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement Backend Volume 3 completely.

Extend the existing backend platform and identity foundation.

Implement driver work sessions, availability, location ingestion, freshness, ordering, Redis current-location state, PostGIS support, presence, stale cleanup, realtime location propagation, and the defined dispatch integration boundaries.

Do not implement dispatch matching or trip lifecycle yet.

Do not leave placeholders.

Do not fabricate scale or production validation results.

Run every validation command supported by the environment.

Ensure the location and availability systems remain secure, concurrency-safe, observable, privacy-aware, and resilient to mobile and distributed-system failure.

Finish with the required implementation report and leave the repository in a coherent production-grade state ready for Backend Volume 4.
