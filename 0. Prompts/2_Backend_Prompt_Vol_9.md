# Uber-Style Global Ride-Hailing & Mobility Platform — Backend Prompt — Volume 9

## ROLE

You are the senior backend engineering organization responsible for implementing the scheduled-trip, reservation, fleet, vehicle-operations, routing, geocoding, ETA, and related operational backend capabilities of an original, production-grade global ride-hailing and mobility platform.

Operate simultaneously as:

* Principal Software Architect
* Staff Backend Engineer
* Distributed Systems Engineer
* Mobility Systems Architect
* Routing and Geospatial Systems Engineer
* Fleet Systems Engineer
* Database Architect
* Distributed Systems Engineer
* Reliability Engineer
* Performance Engineer
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
* trust and safety personnel
* fleet personnel
* administrators

This milestone implements:

* scheduled rides
* reservations
* pre-dispatch orchestration
* scheduled-trip state
* fleet and vehicle operations
* maintenance/inspection state
* routing
* geocoding
* ETA abstraction
* routing-provider resilience
* scheduled-work orchestration

The platform is architected for targets such as:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* large numbers of scheduled trips
* high-frequency realtime workloads
* geographically distributed operation
* multiple routing/geographic providers
* global fleet operations

These are architectural targets, not measured capacity claims.

# TECHNOLOGY DIRECTION

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

### Search

* OpenSearch or Elasticsearch-compatible architecture

### Object Storage

* Amazon S3

### Realtime

* authenticated WebSockets

### Maps and Routing

* provider abstraction for:

  * geocoding
  * routing
  * distance
  * duration
  * ETA
  * geographic lookup

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

Backend Volumes 1–8 establish:

* backend platform foundations
* identity and authentication
* driver onboarding and vehicles
* availability and location
* trip lifecycle
* dispatch
* pricing and financial systems
* notifications and messaging
* ratings
* trust and safety
* support
* fraud/risk
* administration
* API/error/idempotency/concurrency contracts
* event/outbox architecture
* realtime architecture
* job infrastructure
* object storage
* audit

This milestone must build scheduled mobility, fleet operations, and geographic-provider capabilities on those foundations.

Do not depend on the previous AI conversation.

If existing implementation differs from the architecture:

1. inspect the actual implementation
2. preserve compatible working behavior
3. make the minimum coherent changes required
4. document material discrepancies

Do not create competing routing, fleet, trip, or scheduling systems.

# BACKEND EXECUTION MODEL

This milestone owns four closely related areas.

### Scheduled Trips

Own:

* scheduled-trip creation
* reservation state
* scheduled-trip modification/cancellation
* schedule validation
* pre-dispatch state
* dispatch handoff
* schedule lifecycle
* scheduler/reconciliation jobs

### Fleet Operations

Own:

* fleet vehicle records where the architecture assigns them here
* vehicle operational status
* maintenance
* inspections
* service readiness
* operational restrictions

Identity remains authoritative for driver identity and basic vehicle ownership information already established there.

### Routing and Geography

Own:

* geocoding abstraction
* routing abstraction
* distance/duration
* ETA
* provider selection
* caching
* fallback
* provider health

This layer must remain provider-neutral.

### Scheduled Orchestration

Own the background workflow required to turn a future reservation into a dispatchable trip at the correct time.

Do not replace the ordinary trip or dispatch domains.

# CURRENT IMPLEMENTATION SCOPE

# SCHEDULED TRIPS AND RESERVATIONS

## 1. Scheduled-Trip Domain Boundary

Establish authoritative ownership for:

* scheduled-trip/reservation record
* requested departure time
* scheduling constraints
* reservation lifecycle
* pre-dispatch state
* schedule-specific metadata
* conversion/handoff to ordinary trip processing

The normal trip domain remains authoritative once a scheduled reservation becomes an actual trip.

Do not create a second trip lifecycle.

## 2. Scheduled-Trip Model

Implement the canonical scheduled-trip model defined by the architecture.

Support fields required by the contract, including categories such as:

* reservation ID
* rider/account reference
* scheduled pickup
* destination
* service category
* requested pickup time
* scheduling window/constraints
* current reservation state
* created/updated timestamps
* cancellation metadata
* trip reference once created
* scheduling/pre-dispatch references

Do not duplicate the complete trip aggregate.

## 3. Reservation State Machine

Implement the architecture-defined lifecycle.

Potential states may include:

* scheduled
* confirmed
* preparation
* pre-dispatch
* dispatching
* converted
* cancelled
* expired
* failed

Use the exact repository contract.

Every state transition must have explicit authorization and concurrency behavior.

## 4. Schedule Validation

Validate:

* future pickup time
* supported service category
* geographic/service-area eligibility
* destination/pickup validity
* supported scheduling window
* rider authorization
* required payment/quote conditions where the architecture requires them

Do not allow a reservation to bypass ordinary product constraints simply because it is scheduled.

## 5. Schedule Time Handling

Use canonical UTC timestamps internally while preserving the originating timezone or market context where the contract requires it.

Handle:

* daylight-saving changes where applicable
* timezone conversion
* regional calendars
* invalid local times
* clock changes

Do not use server-local time as the authoritative scheduling basis.

## 6. Scheduled-Trip Idempotency

Creation, modification, and cancellation must be idempotent where the API contract requires it.

Protect against:

* client retries
* duplicate requests
* worker retries
* concurrent cancellation/update

Use the existing idempotency infrastructure.

## 7. Scheduled-Trip Modification

Where permitted by the contract, support controlled modification of:

* pickup time
* pickup/destination
* service category
* related scheduling parameters

Modifications must revalidate scheduling constraints and update the reservation version.

Do not silently modify a reservation after it has entered an irreversible pre-dispatch state.

## 8. Scheduled-Trip Cancellation

Implement cancellation rules.

Support the authorized cancellation actors defined by the architecture.

Record:

* actor
* reason
* timestamp
* previous state
* resulting state
* related fee reference where applicable

Do not calculate the actual cancellation fee here if pricing owns that responsibility.

## 9. Pre-Dispatch Lifecycle

Implement the transition from reservation to dispatch preparation.

This includes:

* identifying reservations approaching the dispatch window
* validating that the reservation remains viable
* checking current configuration
* confirming geographic/provider availability
* creating or initiating the normal dispatch workflow at the correct point

Do not create a separate matching algorithm.

Use Backend Volume 5's dispatch system.

## 10. Dispatch Handoff

Create a clean interface between scheduled reservations and ordinary trip/dispatch processing.

At handoff:

* create or activate the authoritative trip according to the architecture
* associate it with the reservation
* preserve reservation traceability
* transfer relevant schedule context
* initiate normal dispatch

The scheduled-trip domain must stop being the owner of ordinary trip lifecycle state once the handoff occurs.

## 11. Scheduler Jobs

Implement jobs for:

* approaching reservation detection
* pre-dispatch activation
* stale reservation reconciliation
* missed/late schedule handling
* cancellation cleanup
* failed handoff recovery

Jobs must be:

* idempotent
* bounded
* retry-safe
* observable

Do not poll the entire reservations table without appropriate indexes or partitioning strategy.

## 12. Scheduler Concurrency

Prevent duplicate processing of the same reservation by multiple workers.

Handle:

* overlapping scheduler executions
* worker restart
* multiple regions
* delayed jobs
* clock skew

Use durable state and concurrency control rather than process-local locks.

## 13. Missed-Window Handling

Define behavior when a reservation is approaching or passing its scheduled time but pre-dispatch has not completed.

Possible outcomes include:

* retry
* operational escalation
* controlled dispatch activation
* failure state

Use the repository's contract.

Do not silently mark a missed reservation successful.

## 14. Scheduled-Trip Events

Publish canonical events such as:

* scheduled_trip.created
* scheduled_trip.updated
* scheduled_trip.cancelled
* scheduled_trip.pre_dispatch_started
* scheduled_trip.dispatched
* scheduled_trip.converted
* scheduled_trip.failed

Use the project's established event envelope and naming conventions.

## 15. Realtime Scheduled-Trip Updates

Where scheduled-trip status is exposed through realtime, integrate with the existing realtime platform.

Clients must be able to recover authoritative reservation state after reconnect.

Do not make WebSockets authoritative.

# FLEET AND VEHICLE OPERATIONS

## 16. Fleet Domain Boundary

Implement fleet-operations ownership for:

* fleet organization/reference where defined
* vehicle operational state
* inspection status
* maintenance status
* service readiness
* operational restrictions

Identity/driver domain remains authoritative for basic driver identity and existing vehicle identity/association primitives.

Do not duplicate vehicle ownership unnecessarily.

## 17. Fleet Vehicle Model

Where fleet-specific records are required, implement the necessary fleet layer around existing vehicle entities.

Support references to:

* vehicle
* fleet/operator
* operational region/service area
* current operational status
* readiness
* inspection state
* maintenance state

Do not create another independent vehicle identity.

## 18. Vehicle Operational State

Implement explicit operational states such as:

* active
* unavailable
* under-inspection
* under-maintenance
* out-of-service
* retired

Use the exact architecture contract.

Operational state must be distinct from driver availability.

## 19. Vehicle Inspection

Implement inspection records.

Support:

* vehicle reference
* inspection type
* inspection time
* status
* inspector/reference
* expiration
* findings metadata
* corrective-action reference

Do not store arbitrary sensitive inspection content in ordinary operational records.

## 20. Inspection Eligibility

Expose deterministic vehicle-service eligibility.

A vehicle that is:

* expired
* failed inspection
* under maintenance
* restricted

must not be treated as operationally ready where the architecture requires exclusion.

Do not modify dispatch logic directly; provide authoritative eligibility information.

## 21. Maintenance Records

Implement maintenance records where required.

Support:

* maintenance event
* vehicle
* category
* status
* started/completed timestamps
* service provider/reference
* findings/notes where allowed
* next-service metadata

Do not implement a full external workshop-management system.

## 22. Maintenance Scheduling

Where the architecture requires service intervals, provide support for:

* upcoming maintenance
* due state
* overdue state
* completion

Do not infer maintenance needs from arbitrary data without a defined policy.

## 23. Vehicle Restrictions

Implement operational restrictions with explicit:

* type
* reason
* scope
* effective time
* expiration
* source/actor
* status

Restrictions must integrate with the existing administrative/risk architecture.

Do not create an unrelated restrictions system.

## 24. Fleet Events

Publish events for major state changes such as:

* vehicle.inspection.updated
* vehicle.maintenance.started
* vehicle.maintenance.completed
* vehicle.operational_status.changed
* vehicle.restriction.changed

Use the transactional outbox.

# ROUTING, GEOCODING, AND ETA

## 25. Geographic Provider Abstraction

Implement a provider-neutral routing/geographic interface.

At minimum support operations for:

* forward geocoding
* reverse geocoding
* route calculation
* distance calculation
* duration calculation
* ETA estimation

Keep provider-specific requests/responses inside adapters.

Do not expose provider SDK classes to domain code.

## 26. Canonical Geographic Models

Define normalized internal representations for:

* coordinates
* place
* address
* route
* distance
* duration
* ETA
* provider/reference metadata

Do not make domain entities depend directly on provider-specific JSON.

## 27. Geocoding

Implement forward/reverse geocoding through the provider abstraction.

Handle:

* no result
* multiple results
* low-confidence results
* invalid coordinates
* provider failure
* rate limiting

Do not present provider-specific confidence as a universal truth without normalization.

## 28. Routing

Implement route calculation through the abstraction.

Support:

* origin
* destination
* optional waypoints where the architecture requires
* route summary
* distance
* duration
* route reference/polyline representation where appropriate

Keep large route payloads out of logs.

## 29. ETA

Implement ETA calculation using authoritative routing/provider inputs.

Support:

* current origin/location
* destination
* traffic-aware inputs where supported
* calculated time
* calculation timestamp
* provider reference

Do not guarantee exact arrival times.

Represent uncertainty or approximation where the API contract supports it.

## 30. Provider Selection

Implement provider selection according to configured policy.

Selection may consider:

* region
* service
* provider availability
* health
* cost/configuration
* capability

Do not hard-code one provider into all geographic workflows.

## 31. Provider Failover

Implement safe fallback between supported providers where the architecture allows.

Handle:

* primary provider timeout
* unavailable provider
* rate limit
* invalid response
* regional outage

Do not blindly retry a failed request against every provider.

Provider failover must be bounded.

## 32. Provider Health

Track provider health using safe operational signals.

Support:

* latency
* error rate
* timeout rate
* availability
* throttling

Do not make one transient request failure permanently disable a provider.

## 33. Geographic Caching

Use Redis or another established caching mechanism where appropriate.

Cache only data that is safe to reuse.

Support:

* deterministic cache keys
* TTL
* invalidation
* provider/version awareness
* geographic query normalization

Do not cache user-specific sensitive data globally without an explicit security model.

## 34. Routing Cache Correctness

Route/ETA caches must account for information that materially affects validity, such as:

* origin/destination
* travel mode
* provider
* relevant routing options
* timestamp/freshness where traffic matters

Do not return stale traffic-sensitive ETA indefinitely.

## 35. Rate Limits

Provider rate limits must be respected.

Integrate with:

* queueing
* bounded concurrency
* backoff
* provider-specific limits

Do not let a traffic spike in ride requests cause uncontrolled provider request amplification.

## 36. Provider Response Validation

Validate external provider responses before exposing them to domain logic.

Protect against:

* malformed responses
* impossible coordinates
* negative distances
* invalid durations
* missing route results
* unexpected provider schemas

Do not trust external provider payloads.

## 37. Provider Errors

Normalize external errors into canonical internal categories.

Do not leak raw provider responses to clients.

Distinguish:

* retryable
* unavailable
* rate-limited
* invalid request
* no route
* authentication/configuration failure

## 38. Geographic Data Privacy

Treat precise location as sensitive.

Do not log full origin/destination coordinates unnecessarily.

Do not store route payloads indefinitely unless the domain explicitly requires them.

Use appropriate retention for cached geographic data.

## 39. Routing Integration with Dispatch

Provide the routing abstraction required by dispatch.

Dispatch may consume:

* distance
* ETA
* route metadata

but must not become coupled to a provider SDK.

Do not modify dispatch ownership.

## 40. Routing Integration with Trips

The trip domain may reference route/geographic results where the architecture requires them.

Do not move trip lifecycle logic into routing.

# CROSS-DOMAIN INTEGRATION

## 41. Scheduled Trip + Pricing

Scheduled reservations must use the established pricing contract.

If a quote is required at creation:

* store its reference
* preserve the pricing version
* enforce expiration rules

Do not recompute or mutate historical quote state without the pricing contract.

## 42. Scheduled Trip + Payment

Where payment authorization/preauthorization is required by the architecture:

* reference the payment contract
* do not duplicate payment state
* maintain idempotency
* handle provider ambiguity through the payment domain

Do not directly call provider SDKs from scheduling code.

## 43. Scheduled Trip + Dispatch

At pre-dispatch time:

* validate reservation
* create/activate the normal trip
* invoke the dispatch contract
* preserve reservation linkage

Do not implement separate dispatch matching for scheduled trips.

## 44. Fleet + Driver Eligibility

Fleet/vehicle readiness must be consumable by driver/dispatch eligibility.

Do not duplicate eligibility logic in dispatch.

Expose authoritative operational status instead.

## 45. Routing + Location

Use driver location and trip location through established contracts.

Do not create a duplicate location store.

## 46. Routing + Pricing

Pricing may consume distance/time estimates through the routing abstraction.

Avoid duplicating provider integrations in pricing.

## 47. Events and Outbox

All durable scheduled/fleet state transitions must publish events through the existing transactional outbox.

External provider responses must not directly become business truth without validation and persistence.

# SECURITY, PRIVACY, AND OBSERVABILITY

## 48. Authorization

Protect:

* reservation management
* fleet operations
* vehicle maintenance records
* inspections
* restricted routing/admin functions

Users must access only their own scheduled trips.

Fleet personnel must access only authorized fleet resources.

## 49. Audit

Audit:

* reservation intervention
* cancellation overrides
* fleet restrictions
* inspection changes
* maintenance status overrides
* provider configuration changes
* privileged route/geographic administration

## 50. Metrics

Expose bounded metrics such as:

* scheduled-trip creation rate
* pre-dispatch backlog
* missed scheduling windows
* fleet maintenance due count
* inspection failures
* routing provider latency
* routing provider failure rate
* geocoding failure rate
* ETA calculation latency
* provider fallback rate
* routing cache hit/miss
* scheduler job lag

Avoid raw user/trip/vehicle IDs as metric labels.

## 51. Tracing

Trace:

* scheduled-trip orchestration
* scheduler processing
* dispatch handoff
* routing provider calls
* geocoding
* ETA calculation
* fleet state transitions

Do not place sensitive exact-location payloads into traces unnecessarily.

## 52. Failure Handling

Handle:

* scheduler failure
* duplicate scheduled processing
* routing-provider outage
* geocoding failure
* ETA failure
* Redis failure
* database failure
* event-broker failure
* fleet-worker failure

Do not allow a provider outage to corrupt reservation or fleet state.

# API SURFACE

## 53. Scheduled-Trip APIs

Implement only contractually defined operations such as:

* create reservation
* retrieve reservation
* update reservation
* cancel reservation
* list reservations
* reservation status

Use:

* authorization
* validation
* idempotency
* cursor pagination where applicable

## 54. Fleet APIs

Implement only architecture-defined operations for:

* vehicle operational status
* inspections
* maintenance
* restrictions
* fleet assignment where applicable

Privileged operations must require explicit permissions.

## 55. Routing APIs

Provider abstractions should normally be consumed internally.

Expose a public API only when the architecture explicitly requires one.

Do not turn routing-provider access into an unrestricted proxy.

# TESTING

## 56. Scheduled Trips

Test:

* creation
* validation
* timezone handling
* modification
* cancellation
* duplicate requests
* concurrent updates
* pre-dispatch
* handoff
* missed windows
* worker retries

## 57. Fleet

Test:

* vehicle operational state
* inspection lifecycle
* expired inspection
* maintenance lifecycle
* restrictions
* authorization

## 58. Routing

Test:

* provider success
* no result
* invalid response
* timeout
* rate limit
* provider failover
* cache behavior
* stale ETA handling
* malformed external payload

## 59. Cross-Domain

Test:

* reservation to trip handoff
* trip to dispatch handoff
* fleet eligibility consumed by driver/dispatch
* routing consumed by dispatch
* pricing consuming routing results where required
* duplicate event handling

## 60. Security

Test:

* cross-user reservation access
* unauthorized fleet actions
* privileged override
* sensitive geographic data leakage
* provider credential isolation

# DOCUMENTATION

Create or update documentation covering:

* scheduled-trip domain
* reservation lifecycle
* scheduling/timezone model
* pre-dispatch
* trip handoff
* fleet operations
* inspections
* maintenance
* vehicle restrictions
* routing abstraction
* geocoding
* ETA
* provider selection
* provider failover
* geographic caching
* operational runbooks
* observability
* failure modes

Documentation must describe actual implementation behavior.

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not redesign:

* identity
* availability
* location
* trip lifecycle
* dispatch matching
* pricing
* payment
* notifications
* messaging
* safety
* support
* fraud/risk

Do not create:

* a second scheduling system
* a second fleet vehicle identity
* a second routing provider abstraction
* a second geospatial store
* a second event-broker integration
* a second job infrastructure

Do not introduce a new map/routing provider merely for theoretical completeness.

Do not implement proprietary route-optimization algorithms.

Do not create another scheduled/fleet backend volume.

Do not create a surprise integration phase.

# REPOSITORY INSPECTION REQUIREMENTS

Before implementation:

1. Inspect the backend repository.
2. Inspect Backend Volumes 1–8 implementation.
3. Inspect identity and vehicle models.
4. Inspect driver availability/location.
5. Inspect trip and dispatch.
6. Inspect pricing/payment.
7. Inspect event/outbox infrastructure.
8. Inspect job infrastructure.
9. Inspect Redis and PostGIS usage.
10. Inspect search/object-storage abstractions.
11. Read scheduled-trip, fleet, routing, and geography contracts.
12. Determine exactly which files require creation or modification.

Do not duplicate established foundations.

# IMPLEMENTATION RULES

## Preserve Existing Foundations

Reuse:

* authentication
* authorization
* database
* PostGIS
* Redis
* events
* outbox
* jobs
* idempotency
* concurrency
* audit
* observability
* provider abstraction conventions

## Scheduling Correctness

Use authoritative UTC timestamps plus required regional timezone context.

## Concurrency

Scheduled processing must tolerate multiple workers and retries.

## Provider Isolation

All routing/geographic provider details remain inside adapters.

## Cross-Domain Ownership

Scheduled-trip orchestration must hand off to trip/dispatch rather than duplicating them.

## Fleet Integrity

Do not create independent vehicle identities that conflict with the identity domain.

## Bounded External Calls

Provider requests must have:

* timeout
* bounded retries
* concurrency control
* clear failure state

## No Placeholder Work

Every required capability must be fully implemented.

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
* PostGIS/geospatial tests
* event/outbox tests
* job tests
* OpenAPI validation
* security tests
* dependency/security scanning where configured

Test:

* timezone conversion
* daylight-saving boundary where relevant
* duplicate schedule processing
* concurrent modification
* schedule cancellation race
* pre-dispatch race
* missed scheduling window
* trip handoff failure
* provider timeout
* provider failover
* rate limiting
* malformed provider response
* stale route cache
* inspection expiration
* maintenance restriction
* unauthorized fleet operation

Where external routing/geocoding providers are unavailable, use deterministic test doubles or existing provider abstractions and clearly report that live provider execution was not performed.

# FINAL INTEGRATION CHECK

Before declaring this milestone complete:

1. Verify scheduled trips have an explicit authoritative owner.
2. Verify reservation state transitions are concurrency-safe.
3. Verify timezones and UTC storage are handled consistently.
4. Verify scheduled-trip idempotency exists.
5. Verify pre-dispatch processing is bounded and retry-safe.
6. Verify duplicate scheduler execution cannot create duplicate dispatch workflows.
7. Verify scheduled trips hand off to the normal trip/dispatch domains.
8. Verify scheduled logic does not create a second trip state machine.
9. Verify fleet operations use the existing vehicle identity.
10. Verify operational vehicle state is distinct from driver availability.
11. Verify inspection status affects operational eligibility where required.
12. Verify maintenance restrictions are explicit.
13. Verify routing is provider-neutral.
14. Verify provider responses are validated.
15. Verify provider failures are classified correctly.
16. Verify routing failover is bounded.
17. Verify route/ETA caching respects freshness requirements.
18. Verify geographic information remains privacy-protected.
19. Verify dispatch can consume routing outputs without provider coupling.
20. Verify pricing can consume routing outputs through the abstraction.
21. Verify scheduled/fleet state changes use the outbox.
22. Verify privileged operations are audited.
23. Verify metrics and tracing use bounded cardinality.
24. Verify tests cover scheduling races, provider failures, and authorization.
25. Verify compatibility with Backend Volumes 1–8.
26. Verify the repository is ready for Backend Volume 10.
27. Verify no duplicate platform foundation has been created.
28. Verify no placeholder or fake implementation remains.

# DEFINITION OF DONE

This milestone is complete only when:

* scheduled-trip domain exists
* reservation model exists
* reservation state machine exists
* scheduling validation exists
* timezone handling exists
* modification exists where permitted
* cancellation exists
* pre-dispatch lifecycle exists
* dispatch handoff exists
* scheduler jobs exist
* scheduler concurrency protection exists
* missed-window handling exists
* scheduled-trip events exist
* scheduled-trip realtime behavior exists where required
* fleet domain exists
* fleet vehicle layer integrates with existing vehicle identity
* operational vehicle state exists
* inspection records exist
* inspection eligibility exists
* maintenance records exist
* maintenance scheduling exists where required
* vehicle restrictions exist
* fleet events exist
* routing/geocoding/ETA abstraction exists
* canonical geographic models exist
* geocoding exists
* routing exists
* ETA exists
* provider selection exists
* provider failover exists
* provider health exists
* geographic caching exists
* provider rate limiting exists
* provider response validation exists
* geographic privacy protections exist
* routing integration with dispatch exists
* routing integration with pricing exists
* scheduled/pricing/payment boundaries are preserved
* events use the transactional outbox
* authorization exists
* audit exists
* metrics and tracing exist
* APIs conform to the architecture
* tests cover scheduling, fleet, routing, failure, and security
* documentation is updated
* no duplicate trip/vehicle/routing/scheduling foundation exists
* no unrelated domain has been implemented
* no placeholder implementation remains
* validation results are truthful
* the backend is ready for Backend Volume 10

# IMPLEMENTATION REPORT

At completion, provide:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Scheduled Trips

Summarize:

* reservations
* lifecycle
* scheduling
* timezone handling
* pre-dispatch
* trip/dispatch handoff
* scheduler jobs

## Fleet Operations

Summarize:

* fleet layer
* operational vehicle state
* inspections
* maintenance
* restrictions

## Routing and Geography

Summarize:

* provider abstraction
* geocoding
* routing
* ETA
* provider selection
* failover
* caching
* rate limiting

## Cross-Domain Integration

Summarize:

* pricing
* payment references
* trip
* dispatch
* driver/vehicle eligibility

## Events and Jobs

Summarize:

* events
* outbox
* scheduled processing
* reconciliation
* retries

## Security and Audit

Summarize:

* authorization
* privileged operations
* geographic privacy
* fleet controls
* audit

## Database and Redis

Summarize:

* schema
* constraints
* indexes
* PostGIS
* cache behavior

## API

Summarize implemented scheduled/fleet/geographic endpoints.

## Tests and Validation

List actual commands and actual outcomes.

## External Environment Limitations

State any routing, geocoding, AWS, or other external systems that could not be exercised.

Do not fabricate provider-side or production results.

## Architectural Decisions

Record meaningful implementation decisions.

## Known Limitations

List genuine remaining limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement Backend Volume 9 completely.

Extend the existing identity, vehicle, driver, location, trip, dispatch, pricing, payment, event, job, authorization, and infrastructure foundations.

Implement scheduled trips, reservations, pre-dispatch orchestration, fleet operational state, inspections, maintenance, routing/geocoding/ETA abstractions, provider selection/failover, caching, and the required cross-domain integration.

Do not create a second trip lifecycle, vehicle identity system, routing abstraction, or job/event platform.

Do not implement analytics/reporting yet.

Do not leave placeholders.

Do not fabricate external routing/geocoding/provider execution.

Run every validation command supported by the environment.

Verify scheduling correctness, concurrency, provider resilience, geographic privacy, fleet eligibility, event consistency, and cross-domain ownership.

Finish with the required implementation report and leave the repository in a coherent production-grade state ready for Backend Volume 10.
