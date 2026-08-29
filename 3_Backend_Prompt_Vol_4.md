You are operating in Senior Engineering Team Mode.

Build the production-ready backend for ride requests, dispatch, driver matching, driver offers, trip lifecycle, scheduled rides, multi-stop trips, shared rides, and real-time trip state for an enterprise-scale global ride-hailing and mobility platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

The backend must follow the approved Uber-like architecture, domain boundaries, database ownership, PostGIS strategy, Redis strategy, real-time architecture, maps abstraction, driver-availability architecture, security model, event architecture, queue architecture, and Project Index.

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

• Ride requests
• Fare-estimate integration
• Pickup and dropoff validation
• Ride-category selection
• Driver candidate retrieval
• Dispatch
• Matching
• Driver offers
• Assignment
• Reassignment
• Driver acceptance
• Driver rejection
• Offer expiration
• Trip lifecycle
• Driver en-route state
• Driver arrival
• Trip start
• Trip progress
• Trip completion
• Trip cancellation
• Multi-stop trips
• Scheduled rides
• Shared rides
• Airport trip constraints
• Real-time trip-state propagation
• Rider trip tracking
• Driver trip-state synchronization
• Dispatch recovery
• Assignment consistency

The implementation must support:

• Hundreds of millions of riders
• Millions of drivers
• Large numbers of simultaneous ride requests
• Millions of active trips
• Massive real-time traffic
• Regional dispatch
• Very low assignment latency
• Strong trip-state correctness
• High availability

────────────────────────────────────────

TECHNOLOGY STACK

Backend:

• Node.js
• NestJS
• TypeScript

Database:

• PostgreSQL
• Prisma ORM
• PostGIS

Transient state:

• Redis

Event streaming:

• Kafka or Redpanda

Background processing:

• BullMQ

Real-time:

• WebSockets
• Socket.IO

Maps:

• Google Maps Platform or approved provider abstraction

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

Testing:

• Jest
• Supertest
• Integration and performance testing tools

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

Keep domain logic outside controllers.

Use repositories for persistence.

Use DTOs for external contracts.

Use centralized validation.

Use centralized error handling.

Use structured logging.

Use idempotency for ride requests, offers, assignments, cancellations, and state transitions where required.

Use optimistic concurrency for trip state where appropriate.

Use short-lived leases for dispatch resources.

Never use a long-lived distributed lock for the entire trip.

────────────────────────────────────────

DOMAIN OWNERSHIP

Maintain explicit boundaries between:

• Ride requests
• Dispatch
• Matching
• Driver offers
• Trip lifecycle
• Scheduled rides
• Multi-stop trips
• Shared rides
• Airport operations
• Driver availability
• Location
• Pricing

Do not combine:

• Ride request with completed trip
• Driver availability with permanent driver state
• Matching with payment
• Trip state with location storage
• Scheduled ride with active-trip ownership

────────────────────────────────────────

RIDE REQUEST DOMAIN

Implement:

• Create ride request
• Pickup location
• Destination
• Stops
• Ride category
• Passenger count
• Accessibility requirements
• Scheduled time
• Promotion reference
• Payment method reference
• Fare estimate reference

Ride-request states:

• Created
• Validating
• Searching
• Match Found
• Assigned
• Canceled
• Failed
• Expired

Define valid transitions.

────────────────────────────────────────

REQUEST VALIDATION

Validate:

• Rider authorization
• Pickup coordinates
• Destination coordinates
• Service-area coverage
• Ride category
• Passenger capacity
• Accessibility requirements
• Scheduled-time constraints
• Payment-method availability

Do not trust client-computed:

• Distance
• ETA
• Fare
• Service-area membership

────────────────────────────────────────

PICKUP AND DROPOFF

Support:

• Exact coordinates
• Place references
• Address metadata
• Pickup instructions
• Landmark
• Terminal
• Designated pickup zone

Normalize location data before dispatch.

────────────────────────────────────────

RIDE CATEGORY

Support configurable categories such as:

• Economy
• Standard
• Premium
• XL
• Accessible
• Electric

Category eligibility depends on:

• Region
• Vehicle
• Driver
• Passenger count
• Accessibility

Do not hard-code categories into dispatch logic.

────────────────────────────────────────

DISPATCH ARCHITECTURE

Implement regional dispatch.

Flow:

Ride Request
→ Validation
→ Service Area
→ Candidate Query
→ Eligibility
→ ETA
→ Scoring
→ Driver Offer
→ Response
→ Reservation
→ Assignment

Dispatch must be:

• Region-aware
• Low latency
• Horizontally scalable
• Idempotent
• Recoverable

────────────────────────────────────────

DISPATCH SHARDING

Partition dispatch by:

• Region
• City
• Operational zone
• Spatial cell

A request should have a dispatch owner.

Define:

• Dispatch partition key
• Ownership
• Rebalancing
• Failover
• Cross-cell expansion

Avoid a single global dispatch process.

────────────────────────────────────────

CANDIDATE GENERATION

Use the established geospatial architecture.

Candidate sources:

• Nearby available drivers
• Neighboring cells
• Appropriate vehicle category
• Active driver eligibility

Filter by:

• Driver state
• Vehicle state
• Service area
• Accessibility
• Passenger capacity
• Current assignment state
• Driver restrictions
• Regulatory constraints

Never broadcast a ride request to every nearby driver.

────────────────────────────────────────

MATCHING

Implement an extensible matching engine.

Separate:

1. Candidate generation
2. Hard eligibility
3. ETA
4. Scoring
5. Offer strategy
6. Driver response
7. Reservation
8. Assignment

Scoring may consider:

• Pickup ETA
• Distance
• Driver availability
• Vehicle category
• Accessibility
• Trip direction
• Driver preferences
• Service requirements
• Supply balancing
• Configurable quality signals

Do not hard-code one algorithm.

────────────────────────────────────────

MATCHING FAIRNESS

Provide architecture for configurable fairness constraints.

Consider:

• Driver opportunity
• Supply distribution
• Service quality
• Acceptance behavior
• Regional requirements

Matching should be operationally explainable.

────────────────────────────────────────

DRIVER OFFER

Implement:

• Offer creation
• Offer delivery
• Offer receipt
• Offer viewed
• Accept
• Reject
• Expire
• Cancel

Offer states:

• Created
• Sent
• Delivered
• Viewed
• Accepted
• Rejected
• Expired
• Canceled

────────────────────────────────────────

OFFER TIMEOUT

Offer expiration must be server-authoritative.

Support:

• Configurable timeout
• Region-specific policies
• Vehicle-category policies
• Retry
• Reassignment

A late acceptance must return a deterministic result.

────────────────────────────────────────

DUPLICATE OFFERS

Prevent:

• Same request offered repeatedly unintentionally
• Same driver receiving incompatible concurrent offers
• Multiple drivers being assigned simultaneously

Use:

• Offer IDs
• Idempotency keys
• Short-lived reservation state
• Atomic transitions

────────────────────────────────────────

DRIVER RESERVATION

Before assignment, create a short-lived reservation/lease.

Support:

• Reservation ID
• Driver ID
• Ride request ID
• Expiration
• Status

Possible statuses:

• Held
• Confirmed
• Released
• Expired

Do not reserve drivers indefinitely.

────────────────────────────────────────

ASSIGNMENT CONSISTENCY

The system must prevent:

• One driver receiving two confirmed trips
• Two drivers owning one trip
• A canceled trip being assigned
• A stale offer becoming assignment authority
• A driver being assigned while ineligible

Use database state transitions plus short-lived distributed coordination where appropriate.

────────────────────────────────────────

TRIP DOMAIN

Implement:

• Trip creation
• Driver assignment
• Driver en-route
• Driver arrival
• Trip start
• Stop reached
• Trip progress
• Trip completion
• Cancellation
• Dispute state reference

Trip states:

• Requested
• Searching
• Assigned
• Driver En Route
• Driver Arrived
• Trip Started
• Trip In Progress
• Stop Reached
• Trip Completed
• Rider Canceled
• Driver Canceled
• System Canceled
• Disputed

────────────────────────────────────────

TRIP STATE MACHINE

Define every valid transition.

Examples:

Requested
→ Searching

Searching
→ Assigned
→ Canceled
→ Failed

Assigned
→ Driver En Route
→ Rider Canceled
→ Driver Canceled
→ System Canceled

Driver En Route
→ Driver Arrived
→ Driver Canceled
→ Rider Canceled

Driver Arrived
→ Trip Started
→ Rider Canceled
→ Driver Canceled

Trip Started
→ Trip In Progress
→ Stop Reached
→ Trip Completed

Trip In Progress
→ Stop Reached
→ Trip Completed
→ Disputed

No invalid transition may be accepted.

────────────────────────────────────────

TRIP STATE VERSIONING

Implement optimistic concurrency.

Every trip state mutation should support:

• Expected version
• Mutation ID
• Actor
• Timestamp

Reject stale mutations.

Do not silently overwrite newer state.

────────────────────────────────────────

TRIP EVENT HISTORY

Record important transitions:

• Previous state
• New state
• Actor
• Timestamp
• Reason
• Request ID
• Region
• Mutation ID

Trip event history must be auditable.

────────────────────────────────────────

DRIVER STATE DURING TRIP

Integrate with driver availability.

The driver transitions appropriately:

Available
→ Offered
→ Assigned
→ En Route
→ Arrived
→ On Trip
→ Available

Do not make availability and trip state one shared aggregate.

Define synchronization rules.

────────────────────────────────────────

REAL-TIME TRIP STATE

Publish trip updates through WebSockets.

Support:

• Driver status
• Driver arrival
• Trip start
• Trip progress
• Stop reached
• Trip completion
• Cancellation
• ETA updates

Authorize subscribers.

────────────────────────────────────────

RIDER TRACKING

During an active trip, authorized riders may receive:

• Driver location
• Driver status
• Vehicle
• ETA
• Route state
• Trip status

Access must expire after the trip according to privacy policy.

────────────────────────────────────────

DRIVER TRIP VIEW

Drivers should receive:

• Pickup
• Destination
• Stop sequence
• Rider information permitted by policy
• Trip state
• Navigation context
• Fare information according to driver policy

Do not expose unnecessary personal data.

────────────────────────────────────────

SCHEDULED RIDES

Implement:

• Create scheduled ride
• Update where allowed
• Cancel
• Reminder
• Pre-dispatch
• Driver assignment
• Reassignment
• Expiration

States:

• Scheduled
• Preparing
• Dispatching
• Assigned
• Active
• Canceled
• Expired
• Failed

Use background scheduling.

────────────────────────────────────────

SCHEDULED-RIDE DISPATCH

Define:

• Pre-dispatch window
• Driver candidate preparation
• Driver assignment strategy
• Driver replacement
• Rider notification
• Failure handling

Do not hold a driver from going online for an unlimited period.

────────────────────────────────────────

MULTI-STOP TRIPS

Support:

• Multiple stops
• Stop sequence
• Add stop
• Remove stop
• Reorder stop
• Stop arrival
• Stop completion

Every mutation must be authorized and versioned.

────────────────────────────────────────

ROUTE UPDATES

When stops change:

• Recalculate route
• Recalculate ETA
• Recalculate fare when required
• Update driver/rider views

Use the approved maps and ETA abstractions.

────────────────────────────────────────

SHARED RIDES

Implement architecture for shared trips.

Support:

• Multiple riders
• Shared vehicle
• Capacity
• Pickup order
• Dropoff order
• Detour limits
• Fare allocation
• Trip participant state

Keep shared-trip orchestration separate from the standard trip path where possible.

────────────────────────────────────────

SHARED-RIDE MATCHING

Candidate matching should consider:

• Existing route
• Pickup detour
• Dropoff detour
• Vehicle capacity
• Current trip state
• Maximum allowed delay

Reject candidates exceeding configured limits.

────────────────────────────────────────

AIRPORT TRIPS

Integrate airport zones.

Support:

• Terminal
• Pickup zone
• Dropoff zone
• Driver staging
• Queue zone
• Restricted zone

Dispatch must respect airport-specific operational constraints.

────────────────────────────────────────

TRIP CANCELLATION

Support:

• Rider cancellation
• Driver cancellation
• System cancellation
• Timeout
• Safety cancellation

Record:

• Actor
• Reason
• Timestamp
• Trip state
• Financial implications reference

Do not calculate final financial adjustments here if the payment/fare domain owns those calculations.

────────────────────────────────────────

DISPATCH FAILURE RECOVERY

When dispatch fails:

• Preserve ride request
• Do not incorrectly cancel active trips
• Rebuild candidate pool
• Retry
• Reassign dispatch ownership if needed

A dispatch-worker failure must not imply a trip failure.

────────────────────────────────────────

TRIP RECOVERY

When a service crashes:

• Reload authoritative trip state
• Reconstruct transient state
• Resume appropriate processing
• Avoid duplicate offers
• Avoid duplicate transitions

Use database state plus event history and idempotency.

────────────────────────────────────────

REDIS

Use Redis for:

• Dispatch partitions
• Candidate pools
• Driver reservations
• Offer state
• Dispatch coordination
• Trip real-time state cache
• WebSocket coordination
• Idempotency

Use TTL for transient state.

Redis must never be authoritative for:

• Trip history
• Final trip state
• Driver ownership
• Financial outcomes

────────────────────────────────────────

DATABASE

Implement Prisma models and migrations for:

• RideRequest
• RideRequestStop
• DriverOffer
• DriverOfferAttempt
• DriverReservation
• Trip
• TripParticipant
• TripStop
• TripStateTransition
• TripAssignment
• ScheduledRide
• SharedRide
• SharedRideParticipant
• DispatchRequest
• DispatchAttempt
• DispatchLease
• AirportTripReference where appropriate

Use:

• Primary keys
• Foreign keys
• Composite indexes
• Unique constraints
• State constraints
• Version fields
• Timestamps
• Region identifiers

Partition high-growth trip/event tables where appropriate.

────────────────────────────────────────

DATABASE CONSISTENCY

Use transactions for:

• Ride creation
• Assignment
• Reservation confirmation
• Trip-state transition
• Cancellation
• Stop-state changes

Use optimistic concurrency.

Use short-lived distributed coordination only for resources such as active driver reservations.

────────────────────────────────────────

EVENTS

Publish:

RIDE REQUEST

• RideRequested
• RideValidationFailed
• RideSearchingStarted
• RideSearchExpanded
• RideMatched
• RideAssignmentChanged
• RideCanceled

DRIVER OFFERS

• DriverOfferCreated
• DriverOfferSent
• DriverOfferViewed
• DriverOfferAccepted
• DriverOfferRejected
• DriverOfferExpired
• DriverOfferCanceled

TRIPS

• TripCreated
• DriverAssigned
• DriverEnRoute
• DriverArrived
• TripStarted
• TripStopReached
• TripCompleted
• TripCanceled
• TripDisputed

SCHEDULED

• ScheduledRideCreated
• ScheduledRidePreparing
• ScheduledRideDispatchStarted
• ScheduledRideAssigned
• ScheduledRideCanceled
• ScheduledRideExpired

SHARED

• SharedRideCreated
• SharedRideParticipantAdded
• SharedRideParticipantRemoved
• SharedRideRouteUpdated

Events must be:

• Versioned
• Idempotently consumable
• Minimal
• Region-aware where required

────────────────────────────────────────

BACKGROUND JOBS

Implement queues for:

• Offer expiration
• Dispatch retry
• Scheduled-ride preparation
• Scheduled reminders
• Driver reservation expiration
• Trip-state reconciliation
• Stale dispatch cleanup
• Shared-ride recalculation
• Trip-event archival

Every job must support:

• Retry
• Exponential backoff
• Timeout
• Idempotency
• Dead-letter handling
• Metrics
• Structured logs

────────────────────────────────────────

API

Implement production-ready REST APIs.

RIDE REQUESTS

• Create ride request
• Get ride request
• Cancel ride request
• Estimate route context
• Get request state

DISPATCH

• Internal dispatch request
• Candidate discovery
• Driver offer creation
• Assignment confirmation

DRIVER OFFERS

• List offers
• Get offer
• Accept offer
• Reject offer

TRIPS

• Get trip
• Get trip state
• Cancel trip
• Driver arrived
• Start trip
• Reach stop
• Complete trip
• Update trip state

SCHEDULED

• Create scheduled ride
• Get scheduled ride
• Update
• Cancel

SHARED RIDE

• Create
• Add participant
• Remove participant
• Get shared-trip state

Every public API must support:

• Authentication
• Authorization
• Validation
• Rate limiting
• Idempotency
• Versioning
• OpenAPI
• Consistent errors

Internal dispatch APIs must also enforce service authentication and authorization.

────────────────────────────────────────

REAL-TIME API

Implement WebSocket events for:

• Ride search status
• Driver offer
• Driver assignment
• Driver location
• ETA
• Trip state
• Stop state
• Cancellation

Clients may receive only data they are authorized to receive.

────────────────────────────────────────

SECURITY

Protect against:

• Fake ride requests
• Request flooding
• Offer manipulation
• Offer replay
• Assignment hijacking
• Driver impersonation
• Trip IDOR
• Location leakage
• Unauthorized trip cancellation
• Stale-state replay
• Duplicate state transitions

Use:

• Authentication
• Authorization
• Resource ownership
• Rate limiting
• Idempotency
• Version checks
• Audit

────────────────────────────────────────

OBSERVABILITY

Instrument:

• Ride requests
• Dispatch
• Candidate generation
• Matching
• Offers
• Assignment
• Trip-state transitions
• Scheduled rides
• Shared rides
• WebSocket events

Track:

• Request-to-match latency
• Candidate-generation latency
• Match success rate
• Offer delivery latency
• Offer acceptance rate
• Assignment conflict rate
• Reassignment rate
• Cancellation rate
• Trip completion
• State-transition failures
• Dispatch queue depth
• Regional capacity

Define alerts for:

• Matching degradation
• Offer backlog
• Assignment conflicts
• High cancellation
• Trip-state inconsistency
• Region saturation

────────────────────────────────────────

TESTING

UNIT TESTS

Test:

• Ride-request validation
• Matching filters
• Matching scoring
• Offer state machine
• Reservation state
• Trip state machine
• Scheduled-ride transitions
• Multi-stop rules
• Shared-ride rules
• Cancellation rules

INTEGRATION TESTS

Test:

• PostgreSQL
• PostGIS
• Redis
• Kafka
• BullMQ
• WebSockets
• Maps integration

CONCURRENCY TESTS

Test:

• Two drivers accept one offer
• One driver accepts two trips
• Duplicate offer response
• Late offer acceptance
• Concurrent cancellation
• Concurrent trip-state mutations
• Scheduled dispatch race
• Multi-stop edits

RECOVERY TESTS

Test:

• Dispatch-worker crash
• Redis restart
• Kafka interruption
• Database failover
• WebSocket disconnect
• Region failover

PERFORMANCE TESTS

Test:

• Ride-request throughput
• Candidate generation
• Matching throughput
• Offer throughput
• Assignment latency
• Active trip count
• WebSocket traffic

SECURITY TESTS

Test:

• Trip IDOR
• Driver impersonation
• Unauthorized cancellation
• Offer replay
• Assignment hijacking
• WebSocket authorization

────────────────────────────────────────

DOCUMENTATION

Generate:

• Ride-request architecture
• Dispatch architecture
• Dispatch partitioning
• Matching architecture
• Matching constraints
• Driver-offer lifecycle
• Reservation/lease architecture
• Trip state machine
• Scheduled-ride architecture
• Multi-stop architecture
• Shared-ride architecture
• Airport integration
• Real-time trip-state architecture
• Recovery architecture
• API contracts
• WebSocket contracts
• Event contracts
• Queue definitions
• Database schema
• Redis key catalog
• Security model
• Testing strategy

────────────────────────────────────────

PROJECT INDEX

Update the backend Project Index with:

• Ride-request modules
• Dispatch modules
• Matching modules
• Driver-offer modules
• Reservation modules
• Trip modules
• Trip-state machine
• Scheduled-ride modules
• Multi-stop modules
• Shared-ride modules
• Airport integration
• WebSocket trip streams
• Database objects
• Migrations
• Redis keys
• API endpoints
• WebSocket events
• Kafka topics
• BullMQ queues
• Workers
• Tests
• Observability
• Security controls
• Generated files
• Remaining work
• Current milestone
• Dependencies

────────────────────────────────────────

IMPLEMENTATION MILESTONES

BACKEND MILESTONE 31

Ride requests, validation, request state machine, ride categories, pickup/dropoff normalization, and APIs.

BACKEND MILESTONE 32

Dispatch partitions, candidate generation, spatial expansion, eligibility filtering, and dispatch orchestration.

BACKEND MILESTONE 33

Matching engine, scoring abstractions, fairness controls, ETA integration, and matching recovery.

BACKEND MILESTONE 34

Driver offers, offer lifecycle, timeout, retries, reservations, leases, and assignment consistency.

BACKEND MILESTONE 35

Trip aggregate, trip state machine, optimistic concurrency, trip-event history, and trip APIs.

BACKEND MILESTONE 36

Real-time trip-state WebSockets, rider tracking, driver trip state, disconnect/reconnect handling, and fan-out.

BACKEND MILESTONE 37

Scheduled rides, pre-dispatch, reminders, assignment, reassignment, expiration, and reconciliation.

BACKEND MILESTONE 38

Multi-stop trips, route updates, ETA recalculation, fare-recalculation integration, and stop state.

BACKEND MILESTONE 39

Shared rides, airport integrations, Redis optimization, events, queues, recovery, and observability.

BACKEND MILESTONE 40

Concurrency, dispatch, trip-state, WebSocket, performance, resilience, security, and production-hardening tests.

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

• Ride requests
• Ride-request validation
• Dispatch
• Dispatch partitioning
• Candidate generation
• Matching
• Matching scoring
• Matching fairness
• Driver offers
• Offer lifecycle
• Driver reservations
• Assignment
• Trip lifecycle
• Trip state machine
• Trip-event history
• Real-time trip state
• Scheduled rides
• Multi-stop trips
• Shared rides
• Airport-trip integration
• Dispatch recovery
• Assignment consistency

Do not implement complete:

• Pricing
• Surge
• Promotions
• Payments
• Wallets
• Earnings
• Payouts
• Ratings
• Messaging business logic
• Notifications business logic
• Safety
• Fraud
• Support
• Business accounts
• Analytics platform
• Administration UI
• Infrastructure
• Frontend
• Mobile

Those belong to later implementation volumes.

────────────────────────────────────────

QUALITY BAR

Treat dispatch, matching, assignment, and trip state as mission-critical systems.

Assume:

• Millions of online drivers
• Millions of active trips
• Large ride-request bursts
• Tens of millions of concurrent client connections
• Regional dispatch
• High location update volume
• Very low matching latency
• Strict trip consistency

Prioritize:

• Low dispatch latency
• Correct assignment
• Strong trip-state correctness
• Idempotency
• Concurrency safety
• Regional isolation
• Graceful recovery
• Horizontal scalability
• Real-time reliability
• Observability
• Security
• Production readiness
