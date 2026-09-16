# UBER-STYLE RIDE-HAILING PLATFORM — BACKEND PROMPT — VOLUME 2

## ROLE

You are the senior backend engineering organization responsible for implementing the core ride marketplace, dispatch, realtime trip execution, geospatial processing, pricing, and asynchronous orchestration capabilities of a production-grade ride-hailing platform comparable in product depth and operational sophistication to Uber.

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

You are not creating a tutorial, prototype, simulation, mock dispatch system, or simplified demonstration.

Implement complete, connected backend functionality with real persistence, real concurrency handling, real realtime behavior, real geospatial processing, real state transitions, real failure handling, real tests, and production-grade observability.

The repository is the source of truth for what currently exists.

Do not assume that another AI prompt or previous conversation is available.

---

# PROJECT

Implement the core transactional and distributed backend capabilities required to turn the foundational platform into a functioning ride-hailing marketplace.

This volume is responsible for:

* ride estimates
* ride request creation
* ride request lifecycle
* geospatial driver location
* driver discovery
* dispatch candidate selection
* ride offers
* driver acceptance
* dispatch assignment
* reassignment
* dispatch recovery
* trip lifecycle
* realtime trip communication
* driver location streaming
* rider driver-location visibility
* pickup workflow
* trip start
* trip progress
* trip completion
* cancellation
* scheduled-ride foundations
* ETA integration
* map/routing provider abstraction
* pricing foundation
* fare estimation
* surge/dynamic pricing foundation
* transactional outbox integration for relevant workflows
* Kafka event publishing and consumption needed by these domains
* BullMQ jobs required by these workflows
* distributed concurrency protection
* idempotency
* observability
* automated testing

Do not implement full payment settlement, driver payouts, advanced fraud systems, complete notification provider orchestration, or administrative analytics merely because later systems will consume the trip events created here.

Create stable contracts for those domains instead.

---

# SOURCE OF TRUTH

Before changing code:

Inspect the repository thoroughly.

Determine:

* current NestJS modules
* Prisma schema and migrations
* user/rider/driver foundations
* vehicle and compliance implementation
* availability model
* Redis infrastructure
* BullMQ infrastructure
* Kafka/event infrastructure
* outbox implementation
* WebSocket implementation
* authentication and authorization
* API conventions
* error handling
* observability
* external integration abstractions
* test conventions
* frontend/mobile API consumers
* existing geographic utilities

Preserve compatible implementations.

Do not build parallel versions of:

* authentication
* authorization
* Redis
* event envelopes
* queue infrastructure
* database connection management
* logging
* tracing
* validation

Extend the existing repository foundations.

Do not regenerate unchanged files.

---

# BACKEND SCOPE

This prompt owns the following domains:

* Location
* Ride Estimate
* Ride Request
* Dispatch
* Ride Offer
* Trip
* Route/ETA
* Pricing
* Geographic Configuration
* Realtime Trip Communication
* Scheduled Ride Foundation

It also extends the foundational:

* event infrastructure
* outbox infrastructure
* BullMQ processing
* Redis usage
* observability
* auditability

---

# DOMAIN RESPONSIBILITIES

The implementation must maintain explicit ownership.

## LOCATION

Own:

* current driver location
* location freshness
* geospatial lookup state
* location ingestion rules
* location privacy boundaries

Do not make Location the owner of trip state.

## RIDE REQUEST

Own:

* rider request
* pickup
* destination
* requested product
* request lifecycle
* request cancellation before active trip execution
* estimate reference
* dispatch initiation

Do not make Ride Request the authoritative source for active trip execution.

## DISPATCH

Own:

* candidate discovery
* eligibility evaluation
* offer creation
* offer expiration
* acceptance race
* assignment
* reassignment
* dispatch retry/recovery

Do not duplicate driver profiles or vehicle records as independent truth.

## TRIP

Own:

* accepted ride execution
* pickup
* arrival
* start
* active trip
* completion
* trip cancellation
* trip-level location association
* trip lifecycle events

## PRICING

Own:

* estimate calculation
* pricing configuration
* dynamic pricing modifiers
* quote creation
* final fare calculation inputs

Payment capture remains a separate later domain.

---

# RIDE PRODUCT MODEL

The backend must support a generic ride-product abstraction.

A ride product must be extensible to represent capabilities such as:

* standard
* premium
* larger-capacity
* accessibility-oriented
* scheduled
* airport-oriented

The domain must not scatter product-specific conditionals through controllers.

Use explicit product configuration and policy abstractions.

A ride product must define or reference:

* eligibility
* capacity
* vehicle requirements
* pricing behavior
* geographic availability
* scheduling support
* operational constraints

---

# GEOGRAPHIC CONFIGURATION

Implement a foundation for geographic operating configuration.

Support entities or equivalent concepts for:

* market
* city
* service zone
* airport zone
* restricted zone
* geofence

Define:

* identifiers
* boundaries
* active/inactive state
* market association
* supported ride products
* pricing configuration references
* operational rules

Where the repository supports PostGIS, use proper geospatial types/indexes.

Do not calculate complex polygon containment by loading all polygons into application memory.

---

# LOCATION INGESTION

Implement production-grade driver location ingestion.

The backend must:

1. Authenticate the driver.
2. Validate the submitted coordinates.
3. Validate the timestamp.
4. Validate request freshness.
5. Validate driver/session relationship.
6. Apply rate limiting.
7. Normalize the location representation.
8. Update ephemeral driver-location state.
9. Update freshness metadata.
10. Publish relevant realtime/domain signals where necessary.
11. Emit observability telemetry.

High-frequency updates must not create unbounded PostgreSQL writes.

Use Redis/geospatial infrastructure for live location where appropriate.

---

# LOCATION VALIDATION

Reject:

* latitude below -90 or above 90
* longitude below -180 or above 180
* NaN/infinite values
* missing required timestamps
* timestamps far in the future
* timestamps outside the accepted staleness window
* malformed driver/session identity
* unauthorized driver updates

Do not blindly trust device timestamps.

Server receipt time must be recorded.

---

# LOCATION FRESHNESS

Define a reusable freshness calculation.

At minimum distinguish:

* fresh
* stale
* expired

Dispatch must use freshness as an eligibility input.

A driver with an expired location must not remain dispatch-eligible merely because the driver is marked online.

The system must expose enough metadata for operators and dispatch workflows to understand stale-location conditions.

---

# LOCATION UPDATE ORDERING

Driver location packets may arrive:

* late
* duplicated
* out of order

Do not overwrite a newer location with an older packet.

Use appropriate comparison semantics based on server-recognized timestamps and sequence information where available.

If device timestamps cannot be trusted sufficiently, use controlled server-side sequencing.

---

# LOCATION RATE LIMITING

Enforce location update limits appropriate to driver operation.

The rate limit must protect:

* API capacity
* Redis capacity
* WebSocket fan-out
* downstream processing

Do not simply reject all high-frequency traffic without preserving sufficient movement fidelity.

Make the accepted frequency configurable.

---

# EPHEMERAL GEOLOCATION STATE

Use Redis geospatial facilities or the repository's equivalent for nearby-driver discovery where appropriate.

Define key namespaces for:

* driver location
* driver freshness
* operational driver state
* geographic partition

All ephemeral state must have lifecycle management.

Expired drivers must be removed or treated as unavailable.

Do not rely on stale Redis entries indefinitely.

---

# LOCATION PRIVACY

A driver's exact live location may be returned only to authorized clients during appropriate active ride states.

Do not expose:

* exact driver location before assignment unless product rules permit it
* historical driver location to arbitrary riders
* rider location to unrelated drivers
* unrestricted precise location to ordinary support staff

All exact-location access must pass authorization.

---

# RIDE ESTIMATE

Implement an estimate workflow that can calculate an expected fare before a ride request is created.

The estimate must consider:

* pickup
* destination
* ride product
* market
* route distance
* expected duration
* pricing configuration
* dynamic pricing modifier
* applicable fees
* applicable promotion references where supported

Estimate results must include enough metadata to be traceable without exposing internal implementation details.

---

# ESTIMATE CONSISTENCY

An estimate is not the final authoritative fare.

Record or return a pricing configuration version/reference so that the backend can later determine what pricing rules were used.

Do not allow clients to modify:

* fare
* dynamic pricing multiplier
* distance
* duration
* market
* pricing version

The server must derive these values.

---

# ROUTING PROVIDER ABSTRACTION

Implement a provider-independent routing abstraction.

The abstraction must support:

* geocoding
* reverse geocoding
* route calculation
* travel time
* travel distance
* ETA
* route matrix where required for dispatch

Create internal request/response models.

Do not expose the provider's response types throughout the domain.

---

# ROUTING PROVIDER FAILURE

Define timeout and retry behavior.

If the provider is temporarily unavailable:

* do not block unrelated user operations indefinitely
* return a controlled dependency-unavailable response where route data is essential
* use bounded fallback/caching where appropriate
* emit structured telemetry

Do not retry indefinitely.

Do not perform multiple expensive provider calls for the same request without justification.

---

# ROUTE CACHING

Cache route results only where useful.

Every cache entry must define:

* key
* TTL
* invalidation strategy
* acceptable staleness
* provider metadata
* fallback

Never use cached route data as authoritative trip state.

---

# DISPATCH ENGINE

Implement the core dispatch orchestration.

The dispatch system must:

1. Receive a ride request.
2. Determine the applicable market/zone.
3. Determine the requested ride product.
4. Identify eligible drivers.
5. Filter stale/unavailable/ineligible drivers.
6. Calculate/rank candidates.
7. Create offers.
8. Track offer expiration.
9. Process acceptance/rejection/timeout.
10. Commit a unique assignment.
11. Start the trip workflow when appropriate.
12. Recover failed attempts.
13. Emit domain events.
14. Remain observable.

Dispatch must be asynchronous where doing so reduces coupling without making user-visible behavior unreliable.

---

# DRIVER ELIGIBILITY FOR DISPATCH

A driver may be considered dispatch-eligible only when all required conditions are satisfied.

Evaluate:

* account state
* compliance state
* vehicle eligibility
* active availability state
* current trip state
* location freshness
* service-zone eligibility
* requested ride-product compatibility
* temporary operational restrictions

Do not duplicate full driver/compliance records into Redis.

Load only the minimum authoritative information necessary.

---

# DISPATCH CANDIDATE SEARCH

Use geospatial lookup to produce a bounded candidate set.

Do not:

* scan every online driver
* fetch unbounded candidate lists
* perform sequential database queries for each candidate

Candidate discovery should use:

* geographic partition
* radius/area search
* bounded candidate count
* freshness
* operational state

Only after candidate discovery should the system perform deeper eligibility and ranking checks.

---

# DISPATCH RANKING

Implement dispatch ranking as an explicit component.

The first production ranking implementation may use deterministic policy rules based on factors such as:

* ETA
* distance
* location freshness
* ride-product compatibility
* geographic restrictions
* driver operational state

The ranking component must be replaceable.

Do not embed ranking logic inside a NestJS controller.

---

# DISPATCH OFFERS

A ride offer must contain a unique identifier and explicit lifecycle.

Support states equivalent to:

* created
* offered
* accepted
* rejected
* expired
* canceled
* superseded

Persist authoritative offer state as required for race prevention and auditing.

Ephemeral display state may live in Redis, but final acceptance must be backed by authoritative persistence.

---

# OFFER EXPIRATION

Every dispatch offer must have an expiration timestamp.

Expired offers must:

* reject late acceptance
* become eligible for reassignment
* release temporary driver reservation
* emit an observable state transition where appropriate

Do not rely solely on a mobile timer.

The backend must enforce expiration.

---

# ACCEPTANCE RACE

Multiple drivers may attempt to accept the same ride.

Guarantee that only one valid assignment succeeds.

Use:

* database constraints
* transactions
* optimistic concurrency
* unique active-assignment constraints
* compare-and-set semantics

where appropriate.

The operation must remain correct if:

* two requests arrive simultaneously
* network retries duplicate an acceptance
* two dispatch workers act concurrently
* the driver mobile app submits the same acceptance twice

---

# ACCEPTANCE IDEMPOTENCY

Driver acceptance must support idempotency.

A repeated acceptance request with the same valid idempotency key must return the same logical result without creating a duplicate assignment.

A stale or conflicting acceptance must produce a deterministic conflict result.

---

# DRIVER RESERVATION

If the architecture uses temporary driver reservation before final assignment, implement it with explicit expiration.

Reservation must:

* identify the ride
* identify the driver
* have a TTL
* have an owner
* be safely released
* never override authoritative database assignment

Do not use indefinite locks.

---

# DISPATCH REASSIGNMENT

When a driver:

* rejects
* times out
* becomes unreachable
* loses eligibility
* cancels

the ride must become eligible for reassignment when product rules permit.

Do not manually mutate the ride to "searching" without preserving the prior assignment history.

Record enough state to explain what happened.

---

# DISPATCH RETRY

Retries must be bounded.

Define retry behavior for:

* candidate discovery
* offer delivery
* provider lookup
* event processing
* worker failures

Do not retry a business operation after it has already reached a valid terminal state.

---

# DISPATCH RECOVERY

Implement recoverability when workers crash.

If a dispatch worker dies after:

* creating an offer
* reserving a driver
* accepting an offer
* committing an assignment
* emitting an event

the system must be able to determine durable state and continue correctly.

Use transactional state, outbox/event recovery, and reconciliation jobs where required.

---

# DISPATCH EVENTS

Emit explicit events for meaningful transitions such as:

* ride request created
* dispatch started
* offer created
* offer accepted
* offer rejected
* offer expired
* driver assigned
* assignment canceled
* dispatch exhausted
* dispatch reassigned

Do not publish every internal ranking calculation as a public domain event.

---

# TRIP CREATION

When a driver assignment becomes authoritative, create or activate the trip through a controlled state transition.

The trip must reference:

* rider
* driver
* vehicle
* ride request
* ride product
* pickup
* destination
* pricing estimate/reference
* market
* assignment metadata

Do not copy unnecessary mutable user/profile information into the trip as an uncontrolled duplicate source of truth.

---

# TRIP STATE MACHINE

Implement an explicit trip state machine.

Support appropriate states equivalent to:

* assigned
* driver_en_route
* driver_arrived
* start_pending
* in_progress
* completed
* canceled
* terminated

The exact state names may follow repository conventions.

Every transition must validate:

* actor
* current state
* authorization
* required data
* idempotency
* concurrency

---

# DRIVER ARRIVAL

Implement the driver-arrived transition.

Validate:

* trip ownership
* active trip
* appropriate proximity or route policy where required
* current state
* cancellation state

Do not make geographic proximity the only security mechanism.

---

# TRIP START

Implement the trip-start workflow.

Require the correct driver/trip relationship.

Where a verification mechanism is used, validate it server-side.

Possible mechanisms include:

* trip PIN
* confirmation code
* QR-equivalent verification

The backend must prevent:

* unauthorized trip start
* trip start after cancellation
* duplicate trip starts
* stale verification reuse

---

# ACTIVE TRIP

An active trip must have one authoritative lifecycle.

Support:

* current state
* latest known driver location
* route progress where available
* started timestamp
* completion timestamp
* cancellation metadata
* final route/fare references

Do not use Redis as the authoritative trip state.

---

# TRIP LOCATION STREAM

During an active trip:

* receive driver locations
* validate them
* update ephemeral live state
* distribute authorized realtime updates
* optionally persist sampled route history if required
* preserve location privacy

Do not synchronously write every location packet into the trip record.

---

# RIDER DRIVER TRACKING

Authorized riders with an active relevant ride may receive driver location.

Implement:

* authenticated WebSocket connection
* authorized subscription
* location updates
* reconnect
* missed-state recovery
* disconnect cleanup

After the trip becomes inactive, stop live location exposure unless another explicitly authorized workflow requires it.

---

# WEBSOCKET ARCHITECTURE

Implement or extend the realtime gateway.

Support:

* authentication
* connection lifecycle
* heartbeat
* subscription authorization
* active-trip channels
* driver offer channels
* driver operational channels where needed
* disconnect handling
* reconnect
* horizontal scaling through the repository's realtime infrastructure

Do not trust arbitrary client-selected channel identifiers.

---

# REALTIME SUBSCRIPTION SECURITY

Before a client subscribes to an active trip channel, verify:

* authenticated identity
* relationship to the trip
* current access rights
* active status where required

A rider must not subscribe to another rider's trip.

A driver must not subscribe to another driver's offer channel.

Administrative access must use separate authorization rules.

---

# REALTIME RECOVERY

Clients may miss events.

Implement a recovery path where a reconnecting client can obtain authoritative current state.

The backend must not require event delivery to have been perfect.

Support:

* last-known state/version where practical
* authoritative REST snapshot
* current trip
* current offer
* current driver location where authorized

---

# EVENT ORDERING

Do not assume global ordering.

For a single ride/trip, preserve meaningful entity-level ordering where necessary.

Clients should use:

* state version
* server timestamp
* sequence number

where appropriate to prevent older updates from overwriting newer state.

---

# TRIP CANCELLATION

Implement controlled cancellation workflows.

Support appropriate actors:

* rider
* driver
* authorized operations/support
* automated system rules

For each cancellation path define:

* valid states
* cancellation reason
* actor
* timing
* applicable fee reference
* emitted events
* assignment cleanup
* notification trigger

Cancellation must be idempotent.

---

# CANCELLATION RACES

Explicitly handle:

* rider cancellation vs driver acceptance
* rider cancellation vs driver arrival
* rider cancellation vs trip start
* driver cancellation vs rider cancellation
* administrative cancellation vs active trip

Define deterministic state precedence.

Do not allow two terminal outcomes to be persisted for one lifecycle.

---

# NO-SHOW FOUNDATIONS

Implement architecture for no-show handling where product rules require it.

Examples:

* driver arrives and rider does not appear
* rider waits beyond configured threshold
* driver leaves too early

Do not hardcode local-market timings into controllers.

Use configurable policies.

---

# SCHEDULED RIDE FOUNDATIONS

Implement backend structures needed for scheduled rides.

Support:

* scheduled pickup time
* timezone
* market
* requested ride product
* scheduling eligibility
* cancellation
* reminder metadata
* dispatch preparation metadata

Do not execute scheduled rides by holding one HTTP request open.

Use persistent state and scheduled jobs.

---

# SCHEDULED RIDE PROCESSING

Use BullMQ scheduled/delayed processing where appropriate.

Jobs must be:

* idempotent
* recoverable
* observable
* bounded

The scheduled job must re-check current ride state before taking action.

A canceled ride must not become dispatch-active merely because an old scheduled job fires.

---

# ETA SERVICES

Implement backend ETA services using the map-provider abstraction.

Support:

* rider-to-destination estimate
* driver-to-pickup ETA
* active-trip ETA
* route recalculation

ETA must be treated as derived, non-authoritative information.

Do not block critical trip transitions on an ETA provider response.

---

# ETA CACHING

Use bounded caching where repeated identical route requests would otherwise overload the provider.

Cache keys should incorporate appropriate:

* origin bucket
* destination bucket
* ride product if relevant
* market
* route configuration

Avoid caching precise user coordinates indefinitely.

---

# PRICING FOUNDATION

Implement a pricing domain capable of producing:

* fare estimates
* pricing snapshots/references
* final fare inputs

At minimum support:

* base fare
* distance component
* duration component
* ride product
* market
* fees
* minimum fare
* dynamic pricing modifier

Taxes and promotions may use extension points if their complete later domains are not yet implemented.

Do not hardcode a single universal fare formula into a controller.

---

# PRICING CONFIGURATION

Pricing configuration must be stored or represented through a validated server-side configuration model.

Support:

* market
* ride product
* version
* effective time
* base amount
* per-distance amount
* per-duration amount
* minimum fare
* fee configuration
* dynamic modifier boundaries

Configurations must be immutable once referenced by an authoritative quote or final fare, or must otherwise be versioned so historical calculations remain reproducible.

---

# MONEY REPRESENTATION

Use exact monetary representation.

Do not calculate authoritative fare amounts with floating-point JavaScript numbers.

Use:

* integer minor units
* PostgreSQL numeric/decimal
* or another exact representation consistent with the repository architecture

Every monetary value must have an explicit currency.

---

# ROUNDING

Define deterministic rounding.

Rounding must occur only at specified domain boundaries.

Do not repeatedly round intermediate calculations.

Different currencies may require different fractional precision.

---

# DYNAMIC PRICING FOUNDATION

Implement a replaceable dynamic pricing policy.

It may consume:

* configured market multipliers
* supply-demand signals
* geographic zone
* time window
* product category

The first implementation may use a deterministic configuration-driven multiplier.

The domain must remain extensible so future demand/supply calculation can be introduced without rewriting ride-request orchestration.

---

# DYNAMIC PRICING SAFETY

Enforce:

* minimum modifier
* maximum modifier
* valid currency/fare constraints
* configuration version
* effective period
* market applicability

Invalid configuration must be rejected before affecting an authoritative estimate.

Do not allow clients to provide arbitrary surge multipliers.

---

# PRICING AUDITABILITY

A quote must retain or reference enough information to answer:

* which market
* which ride product
* which pricing configuration version
* which dynamic pricing modifier
* which route distance
* which route duration
* which timestamp
* which currency

was used to generate it.

---

# FARE ESTIMATE API

Implement an authenticated estimate endpoint appropriate to the repository.

The estimate flow must:

1. Validate rider.
2. Validate pickup.
3. Validate destination.
4. Resolve market/zone.
5. Resolve ride product.
6. Obtain route/distance/time.
7. Resolve pricing configuration.
8. Calculate dynamic modifier.
9. Calculate fare.
10. Return a structured quote.
11. Record necessary traceability metadata.

Do not trust any client-supplied route distance or duration.

---

# RIDE REQUEST CREATION

Implement ride-request creation with idempotency.

Validate:

* authenticated rider
* pickup
* destination
* ride product
* market eligibility
* account state
* applicable scheduling rules
* duplicate request conditions
* payment-readiness contract if the repository has the required payment foundation

Create the authoritative ride-request record before dispatch begins.

---

# RIDE REQUEST STATE

Support explicit states such as:

* pending
* requested
* dispatching
* matched
* canceled
* expired
* completed-via-trip

The exact state model must follow the repository conventions, but it must distinguish request lifecycle from active trip lifecycle.

---

# RIDE REQUEST IDEMPOTENCY

A duplicate request caused by:

* mobile retry
* network timeout
* user double tap
* API retry

must not create multiple active ride requests when the client intends one operation.

Use idempotency keys and authoritative constraints.

---

# ACTIVE RIDE UNIQUENESS

Where product policy permits only one active ride request per rider, enforce the invariant at the authoritative persistence layer.

Do not rely solely on:

* frontend button disabling
* Redis locks
* application memory

to prevent duplicates.

---

# RIDE REQUEST CANCELLATION

Implement cancellation of eligible ride requests before active trip execution.

The backend must:

* validate current state
* authorize rider
* terminate dispatch offers where necessary
* release driver reservations
* stop or invalidate scheduled work
* emit appropriate event
* preserve cancellation reason

---

# EVENT INTEGRATION

Integrate Kafka/outbox with the implemented ride lifecycle.

Publish events for meaningful transitions such as:

* ride requested
* ride canceled
* dispatch started
* offer created
* offer expired
* driver assigned
* trip started
* trip completed
* trip canceled
* pricing quote created where appropriate

Events must contain:

* event ID
* event type
* version
* aggregate/entity ID
* timestamp
* producer
* correlation metadata

Never put access tokens or sensitive credentials into events.

---

# CONSUMER IDEMPOTENCY

Any consumers created in this volume must tolerate duplicate event delivery.

Use:

* durable processing state
* unique event identifiers
* idempotent writes
* transactional processing

Do not assume Kafka delivers exactly once to business state.

---

# BULLMQ WORKFLOWS

Create jobs where appropriate for:

* offer expiration
* dispatch recovery
* scheduled ride activation
* stale-driver cleanup
* route recalculation
* event-driven asynchronous work

Every job must define:

* timeout
* retry
* backoff
* concurrency
* idempotency
* terminal failure handling
* observability

Do not use background jobs for operations that require an immediate transactional response when a direct transaction is safer.

---

# STALE DRIVER CLEANUP

Create a recoverable mechanism for marking/removing stale drivers from dispatch candidate pools.

It must:

* respect freshness thresholds
* not corrupt authoritative driver state
* remove expired ephemeral location
* emit metrics
* recover after worker failure

Do not permanently mark a driver offline solely because one cleanup job failed.

---

# RECONCILIATION

Implement reconciliation logic where asynchronous dispatch/realtime state can diverge from PostgreSQL.

At minimum detect conditions such as:

* offer exists without valid ride state
* reservation exists after offer expiration
* ride is dispatching without active dispatch work
* driver availability says available while an authoritative active assignment exists
* stale location remains indexed
* terminal trip still has active ephemeral state

Reconciliation must be safe and observable.

---

# DATABASE DESIGN

Implement or update persistence for:

* ride requests
* ride products
* pricing quotes/snapshots
* dispatch offers
* assignments
* trips
* relevant location metadata
* geographic configuration
* scheduled ride metadata

Use appropriate:

* foreign keys
* uniqueness
* indexes
* state constraints
* timestamps
* version fields

High-volume tables must have indexes matching actual access patterns.

---

# DATABASE CONCURRENCY

Use transactions and constraints for critical operations.

At minimum protect:

* duplicate ride request
* driver acceptance
* assignment uniqueness
* cancellation
* trip state transition
* scheduled-ride activation

Test the race conditions with concurrent requests where practical.

---

# ACTIVE ASSIGNMENT CONSTRAINTS

Ensure the database cannot represent two simultaneous authoritative active assignments for the same ride.

Likewise, enforce the appropriate business invariant preventing one driver from holding incompatible concurrent active trips.

Use the strongest database-level representation supported by PostgreSQL and repository conventions.

---

# TRIP INDEXING

Optimize database queries for:

* rider active trip
* driver active trip
* ride request by rider
* ride request state
* dispatch offers by driver
* active assignment
* trip by ride request
* trip by driver
* trip by rider
* scheduled rides by activation window

Avoid querying large historical datasets for every active-trip operation.

---

# REALTIME FAN-OUT

Implement controlled WebSocket fan-out.

Do not broadcast every location update to:

* all connected riders
* all drivers
* all administrators

Only authorized subscribers should receive the update.

Use appropriate throttling/sampling to balance:

* user experience
* mobile battery
* network bandwidth
* gateway load
* Redis load

---

# REALTIME DUPLICATES

Clients may receive duplicate messages.

Include sufficient event metadata for clients to detect duplicates or reconcile state.

Do not assume a WebSocket event is delivered exactly once.

---

# ACTIVE TRIP RECOVERY API

Provide an authoritative API for retrieving:

* current ride request
* current dispatch/assignment state
* active trip
* driver summary
* latest authorized location
* current estimated arrival information
* current lifecycle state

This API must allow clients to recover after:

* app restart
* WebSocket disconnect
* missed events
* stale cache

---

# SECURITY

Review every new endpoint and operation for:

* authentication
* authorization
* ownership
* IDOR
* rate limiting
* input validation
* sensitive-data exposure
* WebSocket authorization
* replay
* duplicate requests

Specific requirements:

* riders must not request another rider's trip
* drivers must not accept another driver's offers
* drivers must not submit location for another driver
* clients must not modify pricing
* clients must not modify assignment
* clients must not force trip state transitions without authorization
* clients must not manipulate dynamic pricing

---

# PRIVACY

Protect:

* pickup coordinates
* destination coordinates
* driver live coordinates
* trip route
* historical location
* rider/driver relationships

Avoid storing high-frequency route data unless there is a documented reason.

Where route history is stored, define:

* retention
* access
* deletion/anonymization
* audit

---

# OBSERVABILITY

Instrument:

* ride-request latency
* estimate latency
* map-provider latency
* dispatch latency
* candidate counts
* offer creation
* offer expiration
* acceptance rate
* assignment conflicts
* reassignment rate
* trip state transitions
* location update rate
* stale-driver rate
* WebSocket connections
* WebSocket disconnects
* realtime delivery errors
* queue depth
* Kafka lag
* reconciliation findings
* pricing errors

Every critical workflow must preserve:

* request ID
* correlation ID
* trace ID
* entity ID
* safe actor ID where appropriate

---

# BUSINESS METRICS

Measure at least:

* ride-request creation success
* dispatch success
* dispatch time
* match rate
* driver acceptance rate
* rider cancellation rate
* driver cancellation rate
* trip start rate
* trip completion rate
* stale location percentage
* route provider errors
* pricing calculation failures
* active trips
* active drivers
* active WebSocket connections

These metrics must be separated from infrastructure health metrics.

---

# PERFORMANCE

Optimize:

* nearby-driver lookup
* dispatch candidate filtering
* assignment transaction
* active trip reads
* location ingestion
* WebSocket fan-out
* pricing calculation
* route provider calls

Prevent:

* unbounded candidate lists
* N+1 candidate lookups
* per-driver sequential database queries
* synchronous processing of noncritical dispatch side effects
* unbounded event payloads
* excessive location persistence
* excessive route-provider calls

---

# FAILURE HANDLING

Define and implement controlled behavior for:

## REDIS FAILURE

The system must:

* avoid corrupting authoritative trip state
* reject or degrade operations that genuinely require ephemeral location
* preserve durable ride/trip state
* recover ephemeral state

## KAFKA FAILURE

The system must:

* preserve transactional business state
* retain outbox records where applicable
* retry publishing
* expose lag/backlog metrics

## BULLMQ FAILURE

The system must:

* preserve durable scheduling/work state where necessary
* recover scheduled/retryable operations
* avoid duplicate side effects

## MAP PROVIDER FAILURE

The system must:

* time out
* avoid unbounded retries
* provide controlled failure/degradation
* preserve existing trip state

## WEBSOCKET FAILURE

The system must:

* preserve authoritative state
* allow reconnect
* provide recovery API
* avoid considering notification delivery authoritative

---

# RESILIENCE

Critical state must remain correct through:

* duplicate requests
* duplicate events
* worker crashes
* driver reconnect
* rider reconnect
* delayed packets
* stale location
* database retries
* partial provider failures

Use:

* transactions
* unique constraints
* idempotency
* bounded retries
* explicit states
* reconciliation
* outbox
* observability

---

# TESTING REQUIREMENTS

Write comprehensive automated tests.

## RIDE REQUEST TESTS

Test:

* valid creation
* duplicate idempotency
* invalid coordinates
* invalid product
* unavailable market
* unauthorized rider
* cancellation
* active-request uniqueness

## DISPATCH TESTS

Test:

* candidate discovery
* stale-driver filtering
* vehicle compatibility
* eligibility filtering
* ranking
* offer creation
* offer expiration
* rejection
* acceptance
* concurrent acceptance
* reassignment
* exhausted dispatch
* worker recovery

## TRIP TESTS

Test:

* assignment
* arrival
* start
* progress
* completion
* cancellation
* invalid transitions
* duplicate commands
* cancellation races
* concurrent transition attempts

## LOCATION TESTS

Test:

* valid updates
* malformed coordinates
* stale timestamps
* future timestamps
* out-of-order packets
* duplicate packets
* unauthorized driver IDs
* rate limits
* stale-driver expiration

## REALTIME TESTS

Test:

* authentication
* subscription authorization
* active-trip location delivery
* duplicate events
* reconnect
* missed state recovery
* unauthorized subscriptions

## PRICING TESTS

Test:

* base fare
* distance
* duration
* ride products
* market configuration
* dynamic multiplier
* currency
* rounding
* configuration version
* invalid configuration

## SCHEDULED RIDE TESTS

Test:

* scheduling
* cancellation before activation
* delayed job execution
* duplicate activation
* expired schedule
* timezone behavior

---

# CONCURRENT TESTING

Explicitly test races involving concurrent requests.

At minimum:

* two driver acceptances
* rider cancellation during acceptance
* driver cancellation during rider cancellation
* duplicate ride request
* duplicate trip-start request
* duplicate trip-completion request
* duplicate location update
* duplicate scheduled activation
* duplicate event consumer processing

The tests must prove that database invariants prevent contradictory state.

---

# INTEGRATION TESTING

Validate integration among:

* PostgreSQL
* Prisma
* Redis
* BullMQ
* Kafka/event infrastructure
* WebSocket gateway
* map-provider abstraction

Use realistic integration environments where available.

Do not mock every dependency in every test.

---

# MIGRATION TESTING

For every database change:

* apply migration to clean database
* apply against representative existing data where possible
* verify constraints
* verify indexes
* verify rollback/deployment strategy
* verify Prisma client behavior

Do not manually synchronize production schemas.

---

# API CONTRACT TESTING

Verify all newly added API surfaces for:

* validation
* authorization
* pagination where relevant
* idempotency
* response schema
* error semantics
* ownership
* security headers where relevant

Ensure Swagger/OpenAPI documentation matches runtime behavior.

---

# REALTIME CONTRACT TESTING

Validate:

* socket authentication
* room/channel authorization
* event payload schema
* state-version behavior
* reconnect
* stale-message handling
* unsubscribe/disconnect cleanup

---

# PERFORMANCE VALIDATION

Measure or benchmark, where practical:

* driver location ingestion
* nearby-driver query
* dispatch candidate generation
* assignment transaction
* active-trip retrieval
* WebSocket update fan-out

Identify:

* latency
* throughput
* database load
* Redis operations
* event throughput

Do not claim load-test success without actually running the relevant tests.

---

# BACKWARD COMPATIBILITY

Before changing existing contracts, inspect current consumers.

Pay particular attention to:

* mobile applications
* web application
* existing WebSocket clients
* authentication
* existing rider/driver endpoints

Prefer additive changes.

Where a contract must change:

* document it
* update consumers
* provide compatibility where necessary
* test the migration path

---

# DOCUMENTATION

Update repository documentation for:

* ride request lifecycle
* dispatch
* trip lifecycle
* pricing
* location
* WebSockets
* map provider configuration
* scheduled rides
* Kafka events
* BullMQ jobs
* Redis keys
* operational troubleshooting

Documentation must reflect actual implementation.

---

# IMPLEMENTATION DISCIPLINE

Before modifying files:

1. Inspect the repository.
2. Identify existing foundational implementation.
3. Map the required scope to existing modules.
4. Preserve compatible contracts.
5. Implement the ride marketplace functionality completely.
6. Add database models and migrations.
7. Implement concurrency controls.
8. Implement idempotency.
9. Implement Redis/geospatial processing.
10. Implement dispatch.
11. Implement trip lifecycle.
12. Implement realtime behavior.
13. Implement pricing.
14. Implement routing/ETA abstraction.
15. Implement required events/jobs.
16. Implement observability.
17. Add comprehensive tests.
18. Validate migrations.
19. Run formatting/linting/type checks.
20. Run relevant tests and runtime validation.
21. Review security/privacy/reliability.
22. Update documentation.
23. Produce the required completion report.

Do not rewrite unrelated repository code.

---

# PRODUCTION COMPLETENESS

The implementation must contain real working functionality.

Never leave:

* fake dispatch
* fake location
* fake pricing
* hardcoded ETAs
* hardcoded drivers
* simulated offers
* placeholder trip state
* fake WebSocket messages
* TODO implementation gaps
* pseudo-code
* omitted race handling

Do not claim dispatch is implemented if it does not enforce authoritative assignment uniqueness.

Do not claim realtime support if clients cannot recover after a disconnect.

Do not claim pricing is production-ready if monetary calculations are unsafe or configuration is not auditable.

---

# PROHIBITED PRACTICES

Never:

* trust client-provided fare
* trust client-provided assignment
* trust client-provided driver identity
* expose exact location without authorization
* store every location update synchronously in PostgreSQL by default
* use Redis as authoritative trip state
* use WebSockets as authoritative business state
* accept an expired offer
* allow two drivers to own one ride
* allow stale drivers to remain indefinitely dispatchable
* rely only on frontend cancellation
* perform unlimited map-provider retries
* publish secrets into events
* process duplicate financial/ride commands as independent operations
* use floating-point money
* create unbounded dispatch queries
* leave concurrency behavior undefined

---

# IMPLEMENTATION BOUNDARIES

This prompt implements the core ride marketplace and trip execution layer.

It establishes the backend behavior consumed later by:

* payment
* earnings
* payout
* notifications
* safety
* fraud
* support
* administration
* analytics

Do not implement those domains comprehensively here.

Emit stable events and create integration points so those later domains can consume the ride lifecycle without redesigning the core trip architecture.

---

# REQUIRED IMPLEMENTATION DELIVERABLES

Implement or update:

## LOCATION

* driver location ingestion
* freshness
* geospatial state
* validation
* privacy

## RIDE REQUESTS

* estimates
* creation
* state
* cancellation
* idempotency

## DISPATCH

* candidate discovery
* filtering
* ranking
* offers
* expiration
* acceptance
* assignment
* reassignment
* recovery

## TRIPS

* assignment
* arrival
* start
* progress
* completion
* cancellation
* lifecycle events

## REALTIME

* WebSockets
* authorization
* trip channels
* driver offers
* reconnect/recovery

## PRICING

* configuration
* quote
* exact money handling
* dynamic pricing foundation
* auditability

## ROUTING

* provider abstraction
* route
* ETA
* failure handling

## SCHEDULED RIDES

* persistence foundation
* scheduling
* delayed processing
* cancellation/recovery

## DISTRIBUTED INFRASTRUCTURE

* outbox integration
* Kafka events
* BullMQ jobs
* Redis geospatial state
* reconciliation

## OBSERVABILITY

* logs
* metrics
* traces
* business telemetry
* dispatch telemetry

---

# REQUIRED API SURFACES

Implement appropriate authenticated endpoints for:

* fare estimate
* ride creation
* ride retrieval
* ride cancellation
* active ride
* driver location submission
* driver offer retrieval where required
* offer acceptance
* offer rejection
* driver arrival
* trip start
* trip completion
* trip cancellation
* route/ETA retrieval where appropriate
* scheduled ride creation/retrieval/cancellation

Exact route structure must follow repository conventions.

Every endpoint must enforce:

* authentication
* authorization
* validation
* idempotency where required
* observability
* error semantics
* tests

---

# REQUIRED WEBSOCKET SURFACES

Implement the realtime channels needed for:

* driver offers
* active ride state
* active driver location
* trip state changes

Every subscription must be authorized.

Every client must have a recovery path through authoritative backend state.

---

# DATABASE VALIDATION

After implementation:

* apply migrations
* verify ride uniqueness
* verify assignment uniqueness
* verify trip relationships
* verify state/version constraints
* verify pricing references
* verify scheduled-ride indexing
* verify active-record lookup indexes
* verify location-related metadata indexes where used

Test concurrent transactions against real PostgreSQL where practical.

---

# RUNTIME VALIDATION

Verify:

* application startup
* Redis connections
* Kafka/event publishing
* queue workers
* WebSocket gateway
* ride estimate
* ride creation
* dispatch
* offer acceptance
* trip state transitions
* cancellation
* pricing
* location updates
* reconnect/recovery

Do not report functionality as working when it was not exercised.

---

# COMPLETION REPORT REQUIREMENTS

When implementation is complete, report:

## FILES CREATED

List every new file.

## FILES MODIFIED

List every modified file.

## MAJOR FUNCTIONALITY

Describe:

* ride requests
* dispatch
* offers
* trips
* location
* realtime
* pricing
* routing
* scheduled rides

## DATABASE CHANGES

Report:

* Prisma schema
* migrations
* indexes
* constraints
* concurrency protections

## API CHANGES

Report all ride, dispatch, trip, pricing, location, and scheduling endpoints.

## WEBSOCKET CHANGES

Report:

* channels
* authentication
* authorization
* events
* recovery behavior

## EVENT CHANGES

Report:

* event types
* versions
* producers
* consumers
* outbox changes

## QUEUE CHANGES

Report:

* jobs
* workers
* retries
* scheduling
* dead-letter behavior
* reconciliation

## REDIS CHANGES

Report:

* key namespaces
* geospatial structures
* TTLs
* rate limits
* ephemeral state

## SECURITY CHANGES

Report:

* authorization
* IDOR protections
* rate limiting
* realtime authorization
* location protections
* sensitive-data handling

## OBSERVABILITY CHANGES

Report:

* logs
* metrics
* traces
* dashboards/alerts if added

## TESTS

List tests added or changed and what behavior they verify.

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
* WebSocket tests
* runtime verification
* performance testing where performed

## COMPATIBILITY

Identify:

* web consumers
* mobile consumers
* API compatibility
* event compatibility
* database compatibility

## UNRESOLVED ISSUES

List only genuine remaining issues.

Do not claim completion if a mandatory ride, dispatch, trip, pricing, location, or realtime capability remains incomplete or unverified.

---

# FINAL ENGINEERING PRINCIPLE

The ride marketplace backend must behave as one coherent distributed system.

Ride requests, driver location, dispatch, offers, assignments, trips, pricing, realtime state, asynchronous processing, persistence, and events must preserve their business invariants under:

* concurrency
* duplicate requests
* duplicate events
* stale location
* driver disconnects
* rider disconnects
* worker crashes
* infrastructure degradation
* external provider failure
* high demand

Prioritize:

* assignment correctness
* transactional integrity
* deterministic state transitions
* idempotency
* realtime recovery
* location privacy
* financial safety
* observability
* scalability
* graceful degradation
* maintainability

The repository remains the implementation source of truth.

Every later backend capability must be able to consume the ride lifecycle through stable API, event, and data contracts without creating a second source of truth or requiring the core marketplace to be redesigned.
