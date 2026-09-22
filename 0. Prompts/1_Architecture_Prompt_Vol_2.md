# Uber-Style Global Ride-Hailing & Mobility Platform — Architecture Prompt — Volume 2

## ROLE

You are the principal architecture and systems-contract organization responsible for completing the detailed contractual architecture of an original, production-grade global ride-hailing and mobility platform.

Operate simultaneously as:

* Principal Software Architect
* Distributed Systems Architect
* Backend Architect
* Database Architect
* API Architect
* Realtime Systems Architect
* Event-Driven Systems Architect
* Security Architect
* Reliability Architect
* Data Architect
* Platform Architect
* Performance Architect
* QA Architect
* Technical Writer

Your responsibility in this milestone is to create the detailed contracts and architectural rules required for implementation.

You are not implementing the application code yet.

You are extending the foundational architecture with concrete contracts that backend, frontend, mobile, infrastructure, QA, security, and operations implementations can consume consistently.

Do not produce generic documentation.

Do not merely restate Architecture Volume 1.

Convert the foundational architecture into explicit, implementation-ready contracts.

# PROJECT

## Project Identity

Build an original global ride-hailing and mobility platform serving:

* riders
* drivers
* operations teams
* customer-support teams
* trust and safety teams
* fleet teams
* platform administrators

The platform supports:

* rider registration and authentication
* driver onboarding
* driver availability and location
* ride requesting
* dispatch and matching
* trip lifecycle
* pricing
* payments
* driver earnings and payouts
* notifications
* rider-driver messaging
* ratings and reviews
* safety and incidents
* support
* scheduled trips
* fleet operations
* geographic service areas
* analytics and reporting

The product must remain original.

Do not reproduce proprietary internal implementations, private algorithms, branding, or protected assets belonging to another company.

# SCALE TARGETS

The architecture is designed for targets such as:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* 100,000+ simultaneous realtime sessions and higher during peaks
* high-frequency driver location ingestion
* global multi-region operation
* high-volume asynchronous processing
* high availability for critical mobility workflows

These are architectural targets rather than measured claims.

# TECHNOLOGY DIRECTION

Use the locked project technology direction:

## Web

* Next.js
* React
* TypeScript
* Tailwind CSS
* shadcn/ui
* TanStack Query
* React Hook Form
* Zod
* Zustand where justified

## Mobile

* React Native
* Expo
* TypeScript

## Backend

* Node.js
* TypeScript
* NestJS

## Data

* PostgreSQL
* PostGIS
* Prisma where compatible
* Redis

## Eventing

* Kafka or Redpanda

## Background Jobs

* BullMQ or equivalent

## Search

* OpenSearch or Elasticsearch-compatible architecture

## Object Storage

* Amazon S3

## Payments

* provider abstraction with a Stripe-compatible implementation boundary

## Maps and Routing

* provider abstraction for:

  * maps
  * geocoding
  * routing
  * distance
  * ETA

## Realtime

* authenticated WebSockets

## Infrastructure

* AWS
* Docker
* Kubernetes
* Amazon EKS
* Terraform
* GitHub Actions

## Observability

* OpenTelemetry
* Prometheus
* Grafana
* Loki
* Tempo

# SOURCE OF TRUTH

The repository and Architecture Volume 1 artifacts are the architectural context available to this milestone.

Inspect the repository before creating or changing artifacts.

Architecture Volume 1 established:

* system boundaries
* domains
* ownership
* major components
* deployment topology
* data architecture
* trip lifecycle
* dispatch architecture
* realtime architecture
* eventing principles
* security foundations
* reliability principles
* global architecture
* architectural invariants

This volume must deepen those decisions into explicit contracts.

Do not contradict Volume 1.

If implementation files already exist, inspect them and record meaningful divergence.

Do not make later implementation prompts dependent on an AI conversation.

All important contracts created here must exist as repository artifacts.

# ARCHITECTURE OBJECTIVE

Create the detailed contract layer for the project.

This milestone must establish explicit, implementation-ready rules for:

* identifiers
* API behavior
* errors
* pagination
* idempotency
* concurrency
* authentication
* authorization
* commands
* events
* outbox/inbox processing
* background jobs
* realtime channels
* location
* trip/dispatch interactions
* pricing
* payments
* earnings/payouts
* notifications
* messaging
* media/object access
* search
* configuration
* retention
* audit
* reliability
* schema evolution
* client contracts
* operations
* architectural traceability

Do not implement production code.

Do not create detailed implementation code merely to illustrate a contract.

Use concrete examples only where they make the contract unambiguous.

# REQUIRED ARCHITECTURE ARTIFACT SET

Inspect the repository's documentation conventions and create the contract artifacts in the appropriate architecture location.

At minimum create or update the following.

## 1. Identifier and Time Model

Define canonical rules for:

* entity IDs
* request IDs
* correlation IDs
* idempotency keys
* event IDs
* job IDs
* timestamps
* timezone handling
* ordering fields
* version fields

Specify:

* format
* uniqueness expectations
* scope
* serialization
* persistence rules
* client exposure

Distinguish business identity from internal database identity where appropriate.

Define a canonical time representation for APIs, events, database records, and clients.

## 2. API Contract

Define the canonical API conventions for:

* HTTP methods
* paths
* versioning
* content types
* authentication
* authorization
* request IDs
* correlation IDs
* idempotency
* errors
* pagination
* filtering
* sorting
* conditional requests where applicable
* concurrency
* response envelopes where justified

Specify naming conventions.

Do not leave critical conventions to individual services.

## 3. Error Contract

Define the canonical application error model.

Include:

* stable error code
* human-readable message
* machine-readable details
* request/correlation ID
* retryability
* field validation errors where applicable
* domain versus infrastructure errors
* HTTP mapping
* event/worker error mapping

Do not expose:

* stack traces
* secrets
* database internals
* provider credentials
* internal infrastructure topology

Define which errors clients may safely display.

## 4. Pagination and Query Contract

Define:

* cursor pagination
* cursor encoding
* stable ordering
* page limits
* maximum page sizes
* filtering
* sorting
* consistency expectations
* handling of deleted or updated records

Cursor pagination must be the default for high-volume collections where appropriate.

Define when offset pagination is permitted.

## 5. Idempotency Contract

Define idempotency requirements for operations including:

* ride creation
* cancellation
* offer acceptance
* trip completion
* payment creation
* payment capture
* refunds
* payouts
* notification dispatch
* webhook handling
* background jobs
* event consumers

Define:

* key scope
* storage
* expiration
* response replay
* conflict behavior
* concurrency
* cleanup
* failure behavior

## 6. Concurrency and Versioning Contract

Define canonical mechanisms for:

* optimistic concurrency
* entity versioning
* compare-and-set behavior
* locking where justified
* transactional boundaries
* conflict detection
* retry semantics

Explicitly define concurrency-sensitive operations such as:

* dispatch assignment
* offer acceptance
* trip transitions
* payment transitions
* driver availability

Do not use distributed locks by default when transactional or optimistic techniques are sufficient.

## 7. Authentication and Session Contract

Define:

* access-token model
* refresh-token model
* session lifecycle
* device/session registration
* token expiration
* revocation
* logout
* account suspension
* credential rotation
* WebSocket authentication

Define how clients recover from expired sessions.

Do not put long-lived secrets in client-accessible storage.

## 8. Authorization Contract

Define authorization layers:

* authentication
* role permissions
* resource ownership
* contextual authorization
* operational privileges
* safety privileges
* administrative privileges

Specify authorization expectations for:

* riders
* drivers
* support personnel
* safety personnel
* operations personnel
* administrators
* automated workers
* internal services

Define service-to-service authorization separately from end-user authorization.

## 9. Command Contract

Define how important commands are represented.

Distinguish:

* synchronous API commands
* asynchronous commands
* domain events
* operational commands

Commands must identify:

* actor
* target
* request ID
* idempotency information
* timestamp
* version
* authorization context

Do not confuse commands with events.

## 10. Event Contract

Define the common event envelope.

At minimum establish:

* event ID
* event type
* event version
* aggregate/entity ID
* producer
* occurred-at timestamp
* correlation ID
* causation ID where appropriate
* region
* schema version
* payload
* metadata

Define event naming conventions.

Define whether events represent facts rather than requests.

## 11. Event Delivery Semantics

Define:

* at-least-once behavior
* ordering expectations
* duplicate handling
* retry
* dead-letter behavior
* replay
* consumer idempotency

Do not claim exactly-once semantics unless the complete application processing path supports them.

## 12. Outbox and Inbox Contract

Define the architectural contract for:

* transactional outbox
* event publication
* consumer inbox/deduplication
* transaction boundaries
* publication status
* retry
* cleanup
* reconciliation

Clarify which domains require an outbox.

Define how event publication relates to database transactions.

## 13. Background Job Contract

Define canonical job metadata:

* job ID
* job type
* version
* correlation ID
* actor/context where relevant
* scheduled time
* attempt count
* retry policy
* priority
* timeout
* cancellation
* result state

Define job idempotency and retry requirements.

## 14. Realtime Contract

Define the canonical WebSocket model.

Specify:

* connection handshake
* authentication
* authorization
* connection identity
* channels/subscriptions
* message envelope
* sequence/version metadata
* acknowledgments where applicable
* heartbeat
* reconnect
* replay/recovery
* disconnect semantics
* authorization failures

Define what realtime messages represent.

Realtime must not become the authoritative source of transactional state.

## 15. Location Contract

Define location-specific contracts for:

* latitude/longitude
* accuracy
* heading
* speed
* timestamp
* sequence
* source
* freshness
* device/session
* region

Define stale-data semantics.

Define which location data is:

* ephemeral
* operational
* durable
* analytical

Define ordering and duplicate handling.

## 16. Driver Availability Contract

Define explicit states and transitions for driver availability/work sessions.

Include concepts such as:

* offline
* online
* available
* assigned
* temporarily unavailable
* suspended where relevant

Define concurrency guarantees.

Define how availability interacts with:

* location freshness
* dispatch
* active trips
* session state

## 17. Trip Contract

Define the canonical trip aggregate and lifecycle contract.

Specify:

* trip identifier
* rider
* driver
* pickup
* destination
* service category
* pricing reference
* state
* timestamps
* cancellation metadata
* completion metadata
* assignment metadata

Define legal state transitions and invalid transitions.

## 18. Dispatch Contract

Define detailed dispatch boundaries.

Specify:

* candidate criteria
* eligibility
* candidate ordering
* offer identity
* offer expiration
* driver acceptance
* single-winner enforcement
* conflict behavior
* reassignment
* retry
* dispatch failure
* cancellation interaction

Define the invariant that one driver cannot be simultaneously committed to conflicting active assignments.

## 19. Pricing Contract

Define contracts for:

* fare estimate
* quote
* dynamic pricing
* promotions
* cancellation fees
* final fare
* pricing version
* currency
* rounding

Define which data becomes immutable after quote or fare commitment.

Separate:

* price calculation
* financial authorization
* payment execution

## 20. Payment Contract

Define the internal payment state machine.

Cover:

* payment method reference
* payment intent
* authorization
* capture
* failure
* refund
* dispute
* reconciliation
* provider webhook
* provider state mismatch

Clearly distinguish provider IDs from internal IDs.

Define webhook idempotency.

## 21. Financial Ledger Contract

Define the immutable financial-record model at the architecture level.

Cover:

* debit/credit semantics where used
* ledger entry identity
* source reference
* monetary precision
* currency
* immutability
* correction strategy
* reconciliation

Corrections must not mutate immutable historical entries.

## 22. Earnings and Payout Contract

Define:

* driver earnings
* tips
* bonuses
* adjustments
* holds
* payout requests
* payout state
* provider references
* reconciliation

Define separation between:

* trip fare
* platform financial state
* driver earnings
* payout provider state

## 23. Notification Contract

Define common notification behavior for:

* push
* email
* SMS
* in-app/realtime notification

Specify:

* notification identity
* recipient
* category
* template/version
* locale
* delivery state
* retry
* provider response
* deduplication

## 24. Messaging Contract

Define rider-driver messaging contracts.

Cover:

* conversation identity
* participant authorization
* message identity
* sender
* ordering
* delivery
* read state
* retries
* reconnect
* attachment references
* retention boundaries

Do not expose private conversations through broad search or administrative access.

## 25. Media and Object Contract

Define how applications reference S3 objects.

Specify:

* object identity
* owner
* purpose
* access scope
* object state
* upload lifecycle
* download authorization
* expiration
* deletion
* derived objects

Do not expose long-lived public object URLs for sensitive content.

## 26. Search Contract

Define search as a derived-data capability.

Specify:

* indexed entities
* indexing triggers
* projection ownership
* eventual-consistency expectations
* search pagination
* filtering
* authorization filtering
* rebuild behavior
* stale-index handling

Search must never become the authoritative transactional source.

## 27. Configuration Contract

Define:

* static configuration
* secrets
* runtime configuration
* feature flags
* environment scope
* regional scope
* versioning
* validation
* rollout
* rollback

Do not allow feature flags to bypass security or immutable financial invariants.

## 28. Retention and Data Lifecycle Contract

Define architectural lifecycle categories for:

* transactional records
* location data
* Redis state
* events
* search indexes
* object storage
* logs
* audit
* backups
* exports
* analytics data

Do not invent legal retention durations.

Define where retention is:

* domain-controlled
* infrastructure-controlled
* configurable
* immutable

## 29. Audit Contract

Define the canonical audit event model.

Include:

* actor
* actor type
* action
* target
* scope
* timestamp
* request/correlation ID
* previous state reference where appropriate
* resulting state/reference
* outcome

Define which actions require audit records.

Do not place secrets or full sensitive payloads into audit records.

## 30. Security Event Contract

Define events or telemetry for significant security activity such as:

* authentication failure
* session revocation
* privilege changes
* suspicious activity
* sensitive administrative action
* credential lifecycle changes

Distinguish security telemetry from ordinary business events.

## 31. API/Web/Mobile Client Contract

Define shared client-facing expectations for:

* authentication
* API versioning
* errors
* pagination
* idempotency
* optimistic updates
* realtime recovery
* localization
* timestamps
* money
* permissions

Ensure web and mobile clients use compatible semantics.

## 32. Money and Currency Contract

Define canonical handling of:

* monetary values
* currency
* precision
* rounding
* display amounts
* stored amounts
* provider amounts

Never use floating-point arithmetic as the authoritative representation for monetary values.

## 33. Geography Contract

Define canonical representation for:

* coordinates
* service areas
* geofences
* distances
* route references
* region identifiers
* city/service-area identifiers

Specify coordinate-system assumptions.

Do not duplicate competing geographic identifiers across domains.

## 34. Reliability Contract

Define common expectations for:

* timeouts
* retries
* backoff
* idempotency
* circuit breaking
* bulkheading
* degraded modes
* dependency health
* graceful shutdown

Specify that retries must have an owner.

Avoid independently retrying the same failed operation at every architectural layer.

## 35. API and Event Schema Evolution

Define compatibility policy.

Cover:

* additive changes
* deprecated fields
* versioning
* migration windows
* producer/consumer compatibility
* mobile-version compatibility
* web-version compatibility
* database schema evolution

Define how breaking changes are handled.

## 36. Operational Contract

Define operational metadata and conventions for:

* service ownership
* deployment ownership
* alerts
* SLOs
* runbooks
* incident references
* maintenance
* emergency controls
* environment/region identification

## 37. Traceability Matrix

Create a traceability artifact mapping:

* product capability
* domain
* authoritative data
* API contract
* event contract
* realtime contract
* implementation phase
* observability
* security responsibility

This should make it possible to determine where every major capability is implemented later.

# ARCHITECTURAL INVARIANTS TO PRESERVE

The detailed contracts must preserve invariants established in Volume 1, including where applicable:

* one authoritative owner for each critical business entity
* immutable financial records
* payment-provider state separate from internal financial state
* realtime delivery separate from transactional truth
* search as derived data
* Redis not serving as durable transactional truth
* external providers isolated behind adapters
* sensitive information excluded from ordinary telemetry
* critical operations idempotent
* concurrency explicitly controlled
* domain boundaries preventing arbitrary cross-domain writes
* regional architecture avoiding unnecessary critical cross-region dependencies

Add any additional invariant discovered to be necessary during this milestone.

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement production backend code.

Do not implement frontend code.

Do not implement mobile code.

Do not implement Terraform, Kubernetes, Helm, or CI/CD.

Do not create a complete Prisma schema.

Do not create database migrations.

Do not implement actual API controllers or handlers.

Do not create application services merely to demonstrate the contracts.

Do not create Architecture Volume 3.

Do not create a surprise final architecture phase.

Do not add technologies outside the locked stack without a clearly documented architectural necessity.

# REPOSITORY INSPECTION REQUIREMENTS

Before creating artifacts:

1. Inspect existing architecture documentation.
2. Read the Volume 1 artifacts.
3. Inspect existing backend contracts if any exist.
4. Inspect existing API conventions.
5. Inspect existing database schemas or migrations.
6. Inspect existing event definitions.
7. Inspect realtime abstractions.
8. Inspect authentication/session implementation if present.
9. Inspect infrastructure naming conventions.
10. Inspect testing and documentation conventions.

Use the actual repository state when resolving naming or compatibility questions.

# IMPLEMENTATION RULES

## Contract Precision

Every critical contract must define enough detail that an implementation team does not need to invent incompatible semantics.

## No Contradictions

Check all artifacts against Volume 1.

Do not define one identifier, state, or ownership model in one document and another model elsewhere.

## Stable Naming

Use consistent names for:

* entities
* states
* events
* commands
* IDs
* fields
* domains
* services
* resources

## No Fake Guarantees

Do not claim:

* exactly-once delivery
* zero downtime
* instantaneous consistency
* guaranteed cross-region continuity

unless the architecture genuinely establishes those guarantees.

## Implementation-Aware Design

Contracts must be realistic for:

* NestJS
* PostgreSQL/PostGIS
* Redis
* Kafka/Redpanda
* BullMQ
* OpenSearch
* S3
* WebSockets
* Next.js
* React Native

Do not define abstractions impossible or impractical for the locked stack.

# VALIDATION REQUIREMENTS

After creating the contract package:

1. Verify all artifacts are internally consistent.
2. Verify identifiers use one canonical model.
3. Verify timestamp conventions are consistent.
4. Verify API errors are consistent with authorization and validation behavior.
5. Verify idempotency rules cover critical operations.
6. Verify trip states agree with dispatch states.
7. Verify payment states agree with financial states.
8. Verify event envelopes are consistent.
9. Verify realtime messages correspond to actual domain events/state changes.
10. Verify location semantics agree with the Volume 1 location architecture.
11. Verify retention contracts do not contradict data ownership.
12. Verify audit contracts do not expose prohibited sensitive information.
13. Verify client contracts are compatible with web and mobile phases.
14. Verify schema-evolution rules support future application releases.
15. Verify the traceability matrix covers all major product domains.
16. Validate diagram or contract source formats where tooling exists.

# FINAL INTEGRATION CHECK

Before declaring Architecture Volume 2 complete:

1. Verify every major domain has identifiable API and event boundaries.
2. Verify critical state machines have explicit legal transitions.
3. Verify idempotency exists for critical mutation operations.
4. Verify concurrency rules exist for dispatch, trips, payments, and availability.
5. Verify authentication and authorization contracts are explicit.
6. Verify event delivery and replay semantics are explicit.
7. Verify outbox/inbox responsibilities are explicit.
8. Verify realtime authentication and subscription authorization are explicit.
9. Verify location ordering and freshness rules are explicit.
10. Verify pricing and financial state boundaries are explicit.
11. Verify payment-provider and internal-financial state are separated.
12. Verify messaging authorization and ordering are explicit.
13. Verify object access is authorization-controlled.
14. Verify search is explicitly derived.
15. Verify data lifecycle responsibilities are explicit.
16. Verify audit requirements are explicit.
17. Verify schema evolution is explicit.
18. Verify client compatibility requirements are explicit.
19. Verify operational ownership and traceability are explicit.
20. Verify all contracts agree with Architecture Volume 1.
21. Verify the artifacts are sufficient for the later implementation phases.
22. Verify no third architecture volume is required.

# DEFINITION OF DONE

Architecture Volume 2 is complete only when:

* canonical identifiers are defined
* time conventions are defined
* API contracts are defined
* error contracts are defined
* pagination is defined
* idempotency is defined
* concurrency is defined
* authentication is defined
* authorization is defined
* command/event distinction is defined
* event envelope is defined
* delivery semantics are defined
* outbox/inbox architecture is defined
* job contract is defined
* realtime contract is defined
* location contract is defined
* availability contract is defined
* trip contract is defined
* dispatch contract is defined
* pricing contract is defined
* payment contract is defined
* financial ledger contract is defined
* earnings/payout contract is defined
* notification contract is defined
* messaging contract is defined
* object/media contract is defined
* search contract is defined
* configuration contract is defined
* retention/lifecycle contract is defined
* audit contract is defined
* security-event contract is defined
* client contract is defined
* money/currency contract is defined
* geography contract is defined
* reliability contract is defined
* schema-evolution contract is defined
* operational contract is defined
* traceability exists
* all artifacts agree with Volume 1
* no implementation code has been prematurely introduced
* no unsupported guarantees have been documented
* the architecture is ready for Backend Volume 1

# IMPLEMENTATION REPORT

At completion, provide a technically detailed report containing:

## Files Created

List every new contract artifact.

## Files Modified

List every existing artifact modified.

## Contracts Established

Summarize the major contracts created.

## Critical State Machines

Summarize trip, dispatch, availability, payment, payout, and other critical state models.

## Event Architecture

Summarize event envelope, delivery semantics, idempotency, outbox/inbox, retry, dead-letter, and replay rules.

## API Architecture

Summarize API, error, pagination, concurrency, and idempotency conventions.

## Realtime Architecture

Summarize connection, subscription, authentication, authorization, ordering, and recovery rules.

## Data and Lifecycle

Summarize retention, audit, object, search, location, and derived-data contracts.

## Traceability

Summarize how major capabilities map to implementation responsibilities.

## Validation Executed

List actual validation checks and results.

## Inconsistencies Found

Document any pre-existing implementation or documentation conflicts discovered.

## Known Limitations

Document genuine limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Read and reconcile the Architecture Volume 1 artifacts.

Then create the complete Architecture Volume 2 contract package.

Do not implement application code.

Do not create a third architecture volume.

Do not duplicate Volume 1 without adding concrete contractual detail.

Create explicit, internally consistent, implementation-ready contracts for APIs, events, realtime behavior, state machines, data ownership, security, reliability, lifecycle, and client integration.

Validate the complete contract package against Volume 1 and the repository.

Do not invent unsupported guarantees.

Finish with the required implementation report and leave the repository with a complete two-volume architecture foundation ready for Backend Volume 1.
