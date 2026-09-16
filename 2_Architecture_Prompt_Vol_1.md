# UBER-STYLE RIDE-HAILING PLATFORM — ARCHITECTURE PROMPT — VOLUME 1

## ROLE

You are the senior architecture organization responsible for defining the production architecture of a globally scalable ride-hailing and mobility marketplace comparable in product depth and operational sophistication to Uber.

Operate as a coordinated team consisting of:

* Principal Software Architect
* Staff Backend Engineer
* Database Architect
* Distributed Systems Engineer
* Security Engineer
* Cloud Architect
* DevOps Engineer
* Performance Engineer
* Reliability Engineer
* QA Engineer
* Staff Frontend Engineer
* Staff Mobile Engineer
* Technical Writer

You are not implementing the application in this prompt.

You are producing the detailed architecture blueprint that will govern implementation of the platform.

The architecture must be concrete enough for experienced engineering agents to implement directly, while remaining focused on architectural decisions, boundaries, contracts, data ownership, failure behavior, and infrastructure relationships rather than writing application code.

The repository is the source of truth for what already exists.

Do not assume that another AI prompt, prior conversation, or previous architecture document exists.

---

# PROJECT

Define the production architecture for an Uber-style ride-hailing platform supporting riders, drivers, transportation products, dispatch, trips, pricing, payments, earnings, safety, notifications, administration, analytics, and operational infrastructure.

The platform must support:

* web clients
* rider mobile applications
* driver mobile applications
* backend services and domain modules
* PostgreSQL
* Redis
* Kafka-compatible event streaming
* BullMQ background processing
* geospatial processing
* map/routing provider integrations
* payment provider integrations
* notification providers
* object storage
* search infrastructure where justified
* centralized observability
* AWS infrastructure
* Kubernetes
* CI/CD
* multi-environment deployment
* regional scaling
* disaster recovery

The architecture must support a commercially realistic platform rather than a demonstration application.

---

# SOURCE OF TRUTH

Before defining architecture, inspect the repository thoroughly.

Establish:

* repository structure
* existing applications
* existing packages
* existing services
* existing modules
* current NestJS architecture
* current Next.js architecture
* current React Native/Expo architecture
* current PostgreSQL/Prisma schema
* current Redis usage
* current queue implementation
* current event infrastructure
* current API conventions
* current authentication implementation
* current infrastructure
* current CI/CD
* current testing conventions
* current observability implementation
* existing external integrations
* existing naming conventions

Treat already implemented repository contracts as authoritative unless they are demonstrably incorrect, insecure, incompatible with the project requirements, or structurally incapable of supporting the required scale.

Do not redesign working repository components merely for stylistic preference.

Where the repository is incomplete, define the missing architecture required by this prompt.

Do not refer to any previous AI-generated prompt as an architectural dependency.

---

# ARCHITECTURAL OBJECTIVES

The architecture must provide:

* clear domain ownership
* clear data ownership
* explicit service and module boundaries
* scalable ride dispatch
* high-frequency geospatial processing
* resilient realtime communication
* transactional financial correctness
* secure authentication and authorization
* strong privacy controls
* reliable asynchronous processing
* observable distributed workflows
* horizontal scalability
* geographic scalability
* graceful degradation
* recoverability
* operational visibility
* independently testable domains
* long-term extensibility

Architectural decisions must favor correctness and operational reliability over unnecessary abstraction.

---

# SYSTEM ARCHITECTURE

Define the overall logical architecture of the platform.

At minimum, identify and describe the responsibilities and boundaries for:

* edge/API ingress
* authentication and identity
* rider domain
* driver domain
* driver onboarding/compliance
* vehicle domain
* availability and presence
* location ingestion
* ride request management
* dispatch
* trip management
* pricing
* payments
* earnings
* payouts
* ratings
* notifications
* safety
* fraud/risk
* support
* administration
* analytics
* search
* media/object storage
* event streaming
* background jobs
* observability

Determine which responsibilities should initially exist as:

* modular components inside a NestJS application
* independently deployable services
* infrastructure-managed capabilities

Do not split services merely because they can theoretically be separate.

Service boundaries must be justified by factors such as:

* independent scaling
* operational isolation
* data ownership
* failure isolation
* deployment independence
* security boundaries
* workload characteristics
* team ownership
* lifecycle differences

Avoid both extremes:

* one uncontrolled monolith with shared mutable state everywhere
* unnecessary microservice fragmentation that creates excessive distributed-system complexity

---

# DOMAIN BOUNDARIES

Define bounded contexts and ownership boundaries.

At minimum, establish explicit ownership for:

## IDENTITY AND ACCESS

Responsible for:

* user identity
* authentication
* sessions
* credential lifecycle
* authorization primitives
* role/permission relationships
* account security state

It must not own ride, payment, or dispatch business state.

## RIDER

Responsible for:

* rider profile
* rider preferences
* rider-related settings
* rider-facing account state

It must not become the source of truth for trip execution.

## DRIVER AND COMPLIANCE

Separate:

* driver identity/profile
* driver onboarding
* compliance requirements
* eligibility state
* document verification
* operational suspension/blocking

Driver authentication must not automatically imply dispatch eligibility.

## VEHICLE

Responsible for:

* vehicle identity
* vehicle attributes
* category eligibility
* registration metadata
* compliance relationships
* active/inactive state

Define how vehicle eligibility interacts with driver eligibility without creating circular ownership.

## DRIVER AVAILABILITY AND PRESENCE

Responsible for:

* online/offline state
* driver operational state
* current availability
* ephemeral presence
* readiness for dispatch

Define how this domain interacts with:

* current trip state
* location
* compliance
* vehicle eligibility
* dispatch

## LOCATION

Responsible for high-frequency location ingestion and geospatial operational state.

Separate:

* ephemeral live location
* durable location information required for business or legal purposes
* historical trip location
* geographic service boundaries

Define retention and privacy boundaries.

## RIDE REQUEST

Responsible for:

* rider request creation
* ride product
* pickup
* destination
* request lifecycle
* rider cancellation
* request metadata

Do not allow ride-request state to become a substitute for trip state.

## DISPATCH

Responsible for:

* candidate driver discovery
* eligibility filtering
* offer generation
* offer expiration
* assignment
* reassignment
* concurrency control
* matching state

Dispatch must not own authoritative rider identity, payment accounts, or driver compliance records.

## TRIP

Responsible for:

* accepted ride execution
* pickup phase
* arrival
* trip start
* trip progress
* trip completion
* trip cancellation/termination
* trip state transitions

Define a clear boundary between dispatch assignment and trip execution.

## PRICING

Responsible for:

* fare calculation
* market configuration
* pricing rules
* surge/dynamic pricing
* fees
* taxes where applicable
* promotions
* cancellation charges
* final fare

Pricing must produce auditable results.

## PAYMENTS

Responsible for:

* payment methods through the provider abstraction
* payment intents
* authorization
* capture
* refunds
* provider webhooks
* reconciliation
* payment state

Do not allow trip services to directly manipulate provider APIs outside the payment boundary.

## EARNINGS AND PAYOUTS

Responsible for:

* driver earnings
* platform fee accounting
* adjustments
* payout eligibility
* payout records
* payout provider interactions

Separate rider payment state from driver payout state.

## NOTIFICATIONS

Responsible for:

* notification creation
* channel selection
* delivery orchestration
* retry
* provider integration
* notification status

Notifications are not the authoritative source for trip or payment state.

## SAFETY

Responsible for:

* safety incidents
* emergency workflows
* trusted-contact capabilities
* incident escalation
* safety-related audit access

## FRAUD AND RISK

Responsible for:

* risk signals
* fraud assessments
* abuse detection
* account/rider/driver risk states
* promotional abuse controls
* payment abuse indicators

Risk services must not become a mandatory synchronous dependency for every non-risk-critical action if that would introduce unnecessary availability coupling.

## SUPPORT

Responsible for:

* support cases
* support interactions
* case state
* issue categorization
* escalation

Support must reference operational entities without owning their underlying truth.

## ADMINISTRATION

Responsible for:

* operational controls
* administrative workflows
* privileged actions
* configuration management
* audit access

Administrative actions must not bypass domain-level authorization.

---

# DOMAIN DEPENDENCY MODEL

Define the allowed dependency direction between domains.

Prevent:

* cyclic domain dependencies
* unrestricted database access
* direct mutation of another domain's tables
* arbitrary internal service calls
* hidden shared mutable state

Prefer:

* domain-owned persistence
* explicit application interfaces
* domain events
* asynchronous workflows
* controlled synchronous calls for operations that genuinely require immediate responses

For every cross-domain dependency, classify it as one of:

* synchronous query
* synchronous command
* asynchronous event
* background job
* shared infrastructure capability

Document why that interaction type is appropriate.

---

# DATA OWNERSHIP

Define exactly which domain owns each major category of durable data.

At minimum clarify ownership for:

* users
* credentials/session state
* rider profiles
* drivers
* driver compliance
* vehicles
* vehicle eligibility
* driver availability
* ride requests
* dispatch assignments/offers
* trips
* trip locations
* pricing configurations
* fare calculations
* payments
* refunds
* driver earnings
* payouts
* ratings
* notifications
* safety cases
* support cases
* promotions
* fraud signals
* administrative actions
* audit records

No domain may write another domain's authoritative records directly unless a clearly documented architectural exception exists.

---

# POSTGRESQL ARCHITECTURE

Define the PostgreSQL architecture supporting transactional business state.

Specify:

* database ownership model
* schema organization
* table ownership
* transaction boundaries
* indexing principles
* foreign-key strategy
* uniqueness strategy
* state-transition constraints
* migration strategy
* connection management
* read/write behavior
* replication strategy
* backup strategy
* archival strategy
* high-volume table strategy

Determine where a modular monolith can safely share one PostgreSQL deployment and where independent service ownership requires stronger isolation.

Do not prematurely introduce separate databases when a shared transactional database with strict logical ownership provides a more reliable initial architecture.

Where multiple services require separate persistence, define:

* authoritative owner
* synchronization mechanism
* eventual-consistency implications
* recovery strategy
* rebuild strategy

---

# GEOSPATIAL ARCHITECTURE

Define the geospatial strategy for:

* rider pickup coordinates
* destination coordinates
* driver live location
* nearby-driver discovery
* city service zones
* geofencing
* airport zones
* restricted areas
* vehicle/ride-product geographic eligibility

Use durable geospatial storage for authoritative geographic configuration and short-lived high-performance mechanisms for live driver discovery.

Define:

* coordinate precision
* update frequency
* retention
* indexing
* radius search
* geographic partitioning
* location freshness
* stale-driver detection

Establish how the system handles a driver whose location is old, missing, invalid, or inconsistent.

---

# DRIVER LOCATION PIPELINE

Design the complete driver-location flow.

Define:

1. Mobile location acquisition.
2. Client-side sampling/batching.
3. Secure transport.
4. Gateway/API ingestion.
5. Validation.
6. Rate limiting.
7. Ephemeral location update.
8. Dispatch visibility.
9. Realtime fan-out to authorized riders where applicable.
10. Optional durable persistence.
11. Metrics and tracing.
12. Expiration/staleness handling.

Define the maximum acceptable load and behavior during demand spikes.

Do not persist every location update synchronously to the primary transactional database by default.

Define how location updates remain useful when:

* Redis is degraded
* clients reconnect
* packets arrive late
* packets arrive out of order
* a driver rapidly changes state
* a mobile device sends malformed coordinates

---

# RIDER REQUEST ARCHITECTURE

Define the architecture for ride creation.

The request path must establish:

* authenticated rider
* pickup
* destination
* ride category
* pricing estimate
* geographic validity
* rider eligibility
* payment readiness where required
* request idempotency
* ride request creation
* dispatch initiation

Separate estimate generation from authoritative final fare calculation.

Define how duplicate requests are prevented.

Define how the system responds when dispatch, pricing, maps, or payment dependencies are temporarily unavailable.

---

# DISPATCH ARCHITECTURE

Dispatch is one of the most important distributed-system components.

Define:

* dispatch ownership
* candidate search
* eligibility filters
* geographic partitioning
* ranking criteria
* offer generation
* offer expiration
* concurrent offers
* acceptance
* rejection
* timeout
* reassignment
* cancellation
* retry
* idempotency
* race-condition prevention
* stale-location handling
* driver state validation

Establish whether dispatch should use a city/region partitioning model.

A dispatch worker must not blindly issue multiple simultaneous offers that can create contradictory assignments.

Define how assignment uniqueness is protected under concurrency.

Specify the authoritative transaction or compare-and-set mechanism that ultimately commits driver assignment.

---

# DISPATCH CANDIDATE MODEL

Define what information dispatch needs to evaluate a driver.

Potential inputs include:

* driver eligibility
* vehicle eligibility
* online state
* current trip state
* current location
* location freshness
* ride category
* geographic restrictions
* estimated distance
* estimated arrival time
* driver cooldown or temporary restrictions
* risk restrictions where appropriate

Separate immutable or durable eligibility information from rapidly changing ephemeral state.

Do not duplicate entire driver profiles into dispatch storage unless justified.

---

# RIDE OFFER STATE

Design an explicit ride-offer lifecycle.

Define valid states such as:

* created
* offered
* acknowledged
* accepted
* rejected
* expired
* canceled
* superseded

Define:

* offer TTL
* assignment uniqueness
* duplicate offer handling
* driver reconnect behavior
* client acknowledgment
* acceptance race handling

An expired offer must not be accepted later due to stale mobile state.

---

# TRIP ARCHITECTURE

Define trip lifecycle ownership independently from ride-request and dispatch systems.

At minimum define:

* accepted
* driver en route
* driver arrived
* rider verification
* started
* in progress
* completed
* canceled
* terminated due to exceptional circumstances

Every transition must define:

* authorized actor
* valid source state
* valid destination state
* concurrency rules
* idempotency
* emitted events
* audit behavior
* failure handling

The trip domain must remain authoritative for actual trip execution state.

---

# REALTIME ARCHITECTURE

Define realtime communication for:

* driver location to active rider
* ride request state
* dispatch offer state
* trip state
* notifications
* driver operational state
* support/safety events where appropriate

Use WebSockets where realtime delivery materially improves behavior.

Define:

* connection lifecycle
* authentication
* authorization
* topic/channel model
* subscription rules
* connection limits
* heartbeat
* reconnect behavior
* missed-event recovery
* duplicate messages
* ordering assumptions
* horizontal scaling
* connection routing
* fan-out architecture

Do not require all realtime events to be globally ordered.

Define ordering guarantees per entity where needed.

---

# REALTIME AUTHORIZATION

The server must verify authorization for every realtime subscription and sensitive realtime message.

Examples:

* a rider may observe only their own active trip and permitted driver location
* a driver may receive only offers assigned to that driver
* an administrator may access only permissions explicitly granted
* support users may access data according to case permissions

Never rely on an opaque room/channel name as the security boundary.

---

# OFFLINE AND RECONNECTION MODEL

Define the recovery model when:

* rider loses connectivity
* driver loses connectivity
* WebSocket disconnects
* mobile application backgrounding occurs
* application restarts
* client receives events out of order
* client misses events
* device clock differs from server time

The server remains authoritative.

Clients must reconcile with server state after reconnecting.

Define recovery APIs or synchronization mechanisms for active rides.

---

# PRICING ARCHITECTURE

Define a pricing subsystem capable of supporting:

* base fare
* time
* distance
* ride product
* local rules
* taxes
* fees
* promotions
* minimum fares
* cancellation charges
* surge/dynamic pricing

Define separate concepts for:

* estimate
* authorization amount
* actual measured trip
* final fare
* adjustments
* refund

Pricing calculations must be deterministic for the same authoritative inputs and configuration version.

Record enough information to reconstruct why a fare was produced.

---

# DYNAMIC PRICING ARCHITECTURE

Define an architecture for surge/dynamic pricing without embedding demand calculation into the transactional trip service.

Consider:

* geographic zones
* active demand
* available driver supply
* supply/demand ratios
* pricing configuration
* minimum/maximum modifiers
* update frequency
* cache lifetime
* auditability
* stale configuration
* regional overrides

Dynamic pricing calculations must degrade safely if the pricing-signal pipeline becomes unavailable.

Never allow malformed external or operational configuration to produce invalid pricing.

---

# PAYMENT ARCHITECTURE

Define the payment domain boundary.

The architecture must include:

* payment-method abstraction
* provider abstraction
* payment intent lifecycle
* authorization
* capture
* refund
* failure
* retry
* webhook handling
* reconciliation
* idempotency
* provider reference identifiers

Separate:

* ride/trip state
* fare state
* payment state
* payout state

These lifecycles must not be collapsed into one status field.

---

# FINANCIAL CONSISTENCY

Define how the system handles:

* duplicate requests
* duplicate webhooks
* delayed webhooks
* provider timeout after unknown outcome
* capture failure
* refund failure
* partial operational failure
* reconciliation discrepancies

Financial operations must not rely on distributed locks alone.

Use durable state transitions and provider references to recover from uncertain outcomes.

---

# EARNINGS ARCHITECTURE

Define the relationship between:

* fare
* rider payment
* platform fees
* promotions
* adjustments
* driver earnings
* payout eligibility
* payout execution

Driver earnings must not be inferred from current ride state after the fact without authoritative financial records.

Define an immutable or append-oriented accounting approach where appropriate for financial auditability.

---

# EVENT ARCHITECTURE

Define the event backbone.

At minimum establish event domains for:

* driver
* vehicle
* ride request
* dispatch
* trip
* pricing
* payment
* earnings
* payout
* notification
* safety
* support
* fraud/risk

Define event envelope metadata including:

* event ID
* event type
* event version
* aggregate/entity ID
* producer
* event timestamp
* correlation ID
* trace context

Define:

* topic naming
* partitioning strategy
* retention
* schema evolution
* consumer group strategy
* retry
* dead-letter handling
* replay strategy
* privacy controls

---

# TRANSACTIONAL OUTBOX

Define where transactional outbox patterns are required.

At minimum evaluate use for state transitions where:

* PostgreSQL transaction commits business state
* an event must reliably become visible to downstream consumers

Specify:

* outbox ownership
* transaction boundary
* publishing mechanism
* delivery state
* retry
* deduplication
* cleanup/retention
* monitoring

Do not implement dual writes to PostgreSQL and Kafka without a recovery strategy.

---

# BACKGROUND PROCESSING

Define BullMQ job domains and responsibilities.

Potential job groups include:

* notifications
* receipts
* payment retry/reconciliation
* payout processing
* compliance processing
* fraud analysis
* cleanup
* analytics enrichment
* scheduled operations

Every job category must define:

* source
* payload
* retry
* timeout
* backoff
* concurrency
* idempotency
* dead-letter behavior
* observability
* shutdown behavior

Do not put long-running CPU-heavy workloads into latency-sensitive API processes.

---

# EXTERNAL INTEGRATION ARCHITECTURE

Define stable internal abstractions around:

* mapping
* routing
* geocoding
* payments
* push notifications
* email
* SMS
* identity/compliance providers
* fraud providers
* analytics providers where appropriate

External providers must not leak their proprietary error models throughout the application.

Map provider-specific failures into stable internal domain errors.

Every external integration must define:

* timeout
* retry policy
* rate-limit policy
* authentication
* observability
* fallback
* failure isolation
* contract testing strategy

---

# AUTHENTICATION ARCHITECTURE

Define authentication architecture for:

* web
* rider mobile
* driver mobile
* administrative users
* internal services

Specify:

* identity lifecycle
* access token model
* refresh mechanism
* revocation
* session/device management
* password handling if applicable
* MFA extension points
* suspicious-login handling
* credential recovery
* account lock/rate limiting

Administrative authentication must have stronger security controls than ordinary rider authentication.

---

# AUTHORIZATION ARCHITECTURE

Define a centralized permission model supporting:

* rider permissions
* driver permissions
* support permissions
* operations permissions
* administrator permissions
* service-to-service permissions

Authorization must consider resource ownership.

Examples:

* riders may access only their own ride data
* drivers may access only rides assigned or offered to them
* support personnel may access data associated with authorized support cases
* administrators may access according to explicit privilege

Avoid a single coarse "admin" permission covering every administrative operation.

---

# DRIVER ONBOARDING ARCHITECTURE

Define lifecycle states for driver compliance.

Example categories may include:

* pending
* information required
* submitted
* under review
* approved
* rejected
* suspended
* expired

Separate:

* authentication status
* compliance status
* operational eligibility
* vehicle eligibility

A driver should not become dispatch-eligible solely because account registration succeeded.

---

# VEHICLE ARCHITECTURE

Define vehicle data ownership and eligibility.

Support:

* vehicle registration
* vehicle attributes
* ride-product category
* compliance documents
* active/inactive state
* driver association
* regional eligibility

Define how vehicle eligibility is evaluated at dispatch time without requiring large synchronous joins across unrelated services.

---

# SAFETY ARCHITECTURE

Define:

* emergency event flow
* safety incident model
* trusted-contact model
* trip sharing
* incident reporting
* escalation
* audit access
* retention
* privacy controls

Safety workflows must remain available even when nonessential services are degraded.

---

# ADMINISTRATIVE ARCHITECTURE

Define an isolated administrative surface and backend authorization model.

Administrative functionality should support:

* user lookup
* driver lookup
* trip investigation
* payment investigation
* compliance review
* support workflows
* fraud review
* geographic configuration
* pricing configuration
* operational metrics
* audit-log access

Privileged mutations must require explicit authorization and produce audit events.

---

# ANALYTICS ARCHITECTURE

Separate operational transactions from analytics workloads.

Define how analytics events move from transactional systems into analytics/storage infrastructure without putting analytical query load on the primary transactional database.

Consider:

* Kafka events
* event enrichment
* analytical consumers
* aggregation
* dashboards
* operational reporting
* data retention

Analytics must not become a synchronous dependency for trip execution.

---

# SEARCH ARCHITECTURE

Where OpenSearch/Elasticsearch is used, define appropriate indexed entities such as:

* users
* drivers
* vehicles
* trips
* support cases
* administrative records

Search indexes must be derived from authoritative data.

Define:

* indexing events
* reindexing
* consistency expectations
* index versioning
* failure recovery
* access control

---

# MEDIA ARCHITECTURE

Define secure object-storage flows for:

* driver compliance documents
* identity artifacts
* receipts
* support attachments

Use pre-signed or controlled upload/download mechanisms where appropriate.

The application should not proxy large files through API servers unnecessarily.

Define:

* upload authorization
* content validation
* private/public boundary
* lifecycle
* deletion
* retention
* audit access

---

# SECURITY ARCHITECTURE

Define platform-wide security boundaries.

At minimum address:

* authentication
* authorization
* service-to-service authentication
* secret management
* TLS
* network boundaries
* API rate limits
* WebSocket abuse
* upload security
* webhook verification
* administrative security
* audit logging
* sensitive-data handling
* encryption
* key management
* dependency security

Define which controls belong at:

* edge
* application
* domain
* database
* infrastructure

Do not rely on a single layer.

---

# PRIVACY ARCHITECTURE

Define privacy boundaries for:

* user identity
* driver identity
* exact location
* trip history
* payment information
* compliance documents
* support conversations
* safety incidents

Define:

* data minimization
* access control
* retention
* deletion/anonymization
* privileged access auditing
* regional compliance extensibility

---

# FAILURE MODEL

Explicitly define expected behavior for failure of:

* PostgreSQL
* Redis
* Kafka
* BullMQ workers
* mapping provider
* payment provider
* notification provider
* object storage
* search
* WebSocket gateway
* external compliance provider

For each critical dependency determine:

* timeout
* retry
* fallback
* circuit breaking where appropriate
* stale-data tolerance
* user-visible behavior
* recovery process

The failure of one noncritical dependency must not unnecessarily take down the complete ride lifecycle.

---

# CONSISTENCY MODEL

For each major domain, classify data as requiring:

* strong consistency
* transactional consistency
* eventual consistency
* best-effort freshness

At minimum evaluate:

* ride assignment
* trip state
* payment state
* driver location
* driver availability
* pricing configuration
* search index
* analytics
* notifications

Do not use eventual consistency where it can create financial loss or duplicate ride assignment.

---

# CONCURRENCY MODEL

Define concurrency controls for:

* duplicate ride requests
* driver acceptance race
* multiple dispatch workers
* cancellation versus acceptance
* trip start versus cancellation
* completion versus cancellation
* payment capture retries
* refund retries
* duplicate webhooks
* driver status updates
* compliance status changes

Use appropriate mechanisms such as:

* database transactions
* unique constraints
* optimistic concurrency
* compare-and-set semantics
* state-version checks
* idempotency keys

Do not make Redis locks the sole protection for authoritative business invariants.

---

# API ARCHITECTURE

Define the major REST resource boundaries and responsibility.

At minimum identify resource families for:

* authentication
* users
* rider profiles
* drivers
* vehicles
* compliance
* ride estimates
* ride requests
* dispatch/driver offers
* trips
* locations where exposed
* payments
* payment methods
* earnings
* payouts
* ratings
* notifications
* safety
* support
* administration

Define:

* authentication requirements
* authorization requirements
* pagination
* filtering
* idempotency
* error structure
* versioning strategy
* OpenAPI ownership

Do not prescribe every endpoint implementation here; establish stable architectural contracts and ownership.

---

# CLIENT ARCHITECTURE

Define the high-level relationship between:

* Next.js web
* rider mobile application
* driver mobile application
* backend API
* realtime gateway

Establish that:

* clients are not authoritative
* client state may become stale
* server state must be recoverable
* realtime events supplement API state
* authorization remains server-side
* sensitive business rules execute on trusted backend components

Define high-level client responsibilities without turning this prompt into a frontend or mobile implementation plan.

---

# OBSERVABILITY ARCHITECTURE

Define platform-wide observability.

Establish requirements for:

* structured logs
* metrics
* traces
* request correlation
* event correlation
* queue correlation
* business metrics
* infrastructure metrics
* alerts

At minimum trace critical flows end-to-end:

* ride request → dispatch → acceptance → trip → completion
* trip → pricing → payment
* driver earnings → payout
* compliance submission → verification → eligibility

Never include secrets or unnecessary private data in telemetry.

---

# RELIABILITY ARCHITECTURE

Define reliability objectives for critical capabilities.

Identify appropriate SLO categories for:

* API availability
* ride-request creation
* dispatch latency
* realtime trip updates
* payment processing
* notification delivery
* driver location ingestion

Define degradation priorities.

For example:

* preserving authoritative trip state is more important than realtime visual freshness
* preserving payment correctness is more important than immediate UI confirmation
* preserving driver assignment correctness is more important than minimizing dispatch latency by a few milliseconds

---

# CAPACITY AND SCALING MODEL

Define which workloads scale independently.

At minimum consider independent scaling for:

* HTTP API
* WebSocket gateways
* location ingestion
* dispatch workers
* BullMQ workers
* Kafka consumers
* notification workers
* payment workers
* analytics consumers
* search ingestion

Define likely bottlenecks and protection mechanisms.

Do not design all traffic through a single synchronous backend process.

---

# MULTI-REGION DIRECTION

Define the long-term regional architecture.

Determine:

* regional data ownership
* routing strategy
* geographic affinity
* city/market partitioning
* global identity considerations
* cross-region events
* disaster recovery
* failover boundaries

The architecture must distinguish between:

* data that can be regional
* data that must be global
* data that may be replicated asynchronously

Do not introduce active-active global writes for every table without a clear consistency model.

---

# ARCHITECTURAL DECISION RECORDS

Document major decisions and their rationale.

At minimum record decisions about:

* modular monolith versus service decomposition
* PostgreSQL ownership
* Redis role
* Kafka role
* BullMQ role
* geospatial architecture
* dispatch partitioning
* realtime architecture
* payment boundaries
* location retention
* event delivery
* transactional outbox
* multi-region strategy
* search architecture
* object-storage security

Each decision must explain:

* problem
* chosen approach
* alternatives considered
* rationale
* operational implications
* scaling implications
* failure implications

---

# IMPLEMENTATION BOUNDARIES

This architecture volume defines the system's foundational architecture.

Do not use it to implement the entire application.

Do not produce superficial placeholder code merely to demonstrate architecture.

Focus on defining:

* domains
* responsibilities
* service boundaries
* data ownership
* major APIs
* event boundaries
* queue boundaries
* infrastructure relationships
* consistency models
* failure behavior
* security boundaries
* scaling strategy

Implementation agents must later be able to use this architecture as a blueprint while still inspecting the actual repository before changing code.

---

# REQUIRED ARCHITECTURE DELIVERABLES

Produce complete architectural documentation in the repository appropriate to the project's established documentation conventions.

At minimum document:

## SYSTEM CONTEXT

Describe:

* users
* clients
* platform
* external providers
* infrastructure dependencies
* major data flows

## CONTAINER/SERVICE VIEW

Describe:

* applications
* backend components
* workers
* databases
* caches
* event infrastructure
* search
* object storage
* external systems

## DOMAIN MODEL

Describe bounded contexts and responsibilities.

## DATA OWNERSHIP MODEL

Identify the authoritative owner of every major business entity.

## API BOUNDARY MODEL

Document major resource families and ownership.

## EVENT MODEL

Document event categories, ownership, envelope requirements, and consumers.

## QUEUE MODEL

Document background job families, ownership, retry behavior, and operational requirements.

## REALTIME MODEL

Document WebSocket responsibilities, authorization, subscriptions, reconnect behavior, and recovery.

## GEOLOCATION MODEL

Document location ingestion, storage, freshness, geospatial indexing, and privacy.

## DISPATCH MODEL

Document candidate discovery, ranking inputs, offer lifecycle, concurrency, assignment, and recovery.

## FINANCIAL MODEL

Document pricing, payment, earnings, payout boundaries, state transitions, and reconciliation.

## SECURITY MODEL

Document authentication, authorization, trust boundaries, secret management, and privileged operations.

## PRIVACY MODEL

Document sensitive data boundaries, retention, deletion, and access controls.

## RELIABILITY MODEL

Document failure handling, degradation, recovery, and disaster-recovery direction.

## SCALING MODEL

Document major scaling units, bottlenecks, partitioning, and capacity considerations.

## OBSERVABILITY MODEL

Document logs, metrics, traces, business telemetry, and critical end-to-end flows.

---

# VALIDATION REQUIREMENTS

After producing the architecture, validate it against the repository.

Verify that:

* referenced technologies match the repository where already established
* existing contracts are identified
* proposed boundaries do not create impossible dependency cycles
* data ownership is unambiguous
* critical transactional operations have authoritative persistence
* dispatch assignment has a concurrency strategy
* payment state has an idempotency strategy
* realtime communication has reconnect/recovery behavior
* location processing has a scale and retention strategy
* asynchronous workflows have retry/recovery behavior
* external integrations have failure handling
* security boundaries are explicit
* privacy-sensitive data has defined access controls
* observability covers critical workflows
* scaling boundaries are identified
* infrastructure responsibilities are identifiable
* disaster-recovery implications are documented

Do not declare the architecture complete if critical ownership or consistency decisions remain ambiguous.

---

# IMPLEMENTATION READINESS

The resulting architecture must be detailed enough that implementation engineers can determine:

* where a feature belongs
* which component owns the data
* which API boundary should expose it
* whether the interaction is synchronous or asynchronous
* which system is authoritative
* how state transitions are protected
* how failures are handled
* how retries work
* how realtime state is synchronized
* how the feature is observed
* how the feature scales
* how privacy and authorization are enforced

Do not leave architectural ownership to guesswork.

---

# IMPLEMENTATION DISCIPLINE

Before making repository changes:

1. Inspect the repository.
2. Identify existing architecture and contracts.
3. Preserve compatible implementation.
4. Identify architecture that must be corrected for security, correctness, scalability, or consistency.
5. Document architectural decisions clearly.
6. Do not rewrite unrelated implementation.
7. Do not introduce unnecessary technologies.
8. Do not create duplicate sources of truth.
9. Keep architecture aligned with the defined technology direction.
10. Validate all documented relationships against the actual repository.

---

# PROHIBITED ARCHITECTURAL PRACTICES

Never design the platform around:

* a single globally mutable application state
* direct cross-domain table mutation without justification
* Redis as durable business truth
* Kafka as current transactional truth
* client state as authoritative
* WebSocket delivery as authoritative
* payment provider callbacks without idempotency
* unlimited retries
* synchronous dependency on every external integration
* uncontrolled microservice proliferation
* uncontrolled shared database access
* undocumented privileged administrative access
* permanent high-frequency location retention without justification
* financial calculations based on unsafe floating point
* architecture dependent on a previous AI response

---

# FINAL ARCHITECTURE REVIEW

Before considering this architecture volume complete, verify that the blueprint can support the complete ride-hailing lifecycle:

Rider:

* authenticate
* select pickup
* select destination
* obtain estimate
* request ride
* wait for dispatch
* receive driver
* observe driver
* complete trip
* pay
* receive receipt
* rate
* review history
* use support and safety features

Driver:

* authenticate
* onboard
* complete compliance
* register vehicle
* become eligible
* go online
* send location
* receive offer
* accept
* navigate to pickup
* arrive
* start trip
* complete trip
* receive earnings
* receive payout
* use support and safety features

Platform:

* authenticate users
* authorize access
* discover drivers
* dispatch correctly
* maintain trip state
* calculate pricing
* process payment
* account for earnings
* deliver notifications
* process events
* process background jobs
* provide operational administration
* detect abuse
* maintain observability
* recover from partial failures
* scale geographically

Every one of these flows must have a clear architectural owner and source of truth.

---

# COMPLETION REPORT REQUIREMENTS

When the architecture work is complete, report:

## FILES CREATED

List every architectural document created.

## FILES MODIFIED

List every repository file modified.

## ARCHITECTURAL DECISIONS

Summarize the major architectural decisions established.

## DOMAIN OWNERSHIP

Summarize domain and data ownership boundaries.

## API CONTRACTS

Summarize major API ownership and interaction patterns.

## EVENT CONTRACTS

Summarize event categories and delivery strategy.

## QUEUE CONTRACTS

Summarize queue/job categories and reliability behavior.

## DATA ARCHITECTURE

Summarize PostgreSQL, Redis, geospatial, search, and object-storage responsibilities.

## REALTIME ARCHITECTURE

Summarize WebSocket architecture and recovery behavior.

## DISPATCH ARCHITECTURE

Summarize matching, assignment, concurrency, and recovery strategy.

## FINANCIAL ARCHITECTURE

Summarize pricing, payments, earnings, payouts, reconciliation, and idempotency.

## SECURITY

Summarize trust boundaries, authentication, authorization, privileged operations, and sensitive-data protections.

## PRIVACY

Summarize location and identity privacy controls, retention, and access boundaries.

## RELIABILITY

Summarize failure handling, degradation, recovery, and disaster-recovery architecture.

## SCALABILITY

Summarize scaling boundaries, regional partitioning, and anticipated bottlenecks.

## OBSERVABILITY

Summarize logs, metrics, traces, alerts, and critical flow instrumentation.

## VALIDATION

Report:

* repository inspection performed
* architectural consistency validation
* dependency/cycle review
* data ownership review
* concurrency review
* security review
* privacy review
* reliability review
* scalability review

## UNRESOLVED ISSUES

List only genuine architectural uncertainties or blockers that require resolution before implementation.

Do not claim architectural completeness when critical ownership, consistency, or failure behavior remains undefined.

---

# FINAL ENGINEERING PRINCIPLE

The architecture must define one coherent ride-hailing platform rather than a collection of independent features.

The rider experience, driver experience, dispatch engine, trip lifecycle, pricing, financial systems, realtime systems, location infrastructure, event processing, infrastructure, and operational tooling must fit together through explicit contracts and authoritative ownership.

Prioritize:

* correctness
* clear ownership
* transactional integrity
* concurrency safety
* reliability
* security
* privacy
* observability
* scalability
* recoverability
* maintainability

The repository remains the implementation source of truth.

This architecture volume defines the foundational system structure that implementation work must follow while still requiring every implementation agent to inspect and respect the actual repository state before making changes.
