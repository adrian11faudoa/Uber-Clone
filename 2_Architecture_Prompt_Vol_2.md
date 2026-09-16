# UBER-STYLE RIDE-HAILING PLATFORM — ARCHITECTURE PROMPT — VOLUME 2

## ROLE

You are the senior architecture organization responsible for completing the production architecture of a globally scalable ride-hailing and mobility marketplace comparable in product depth and operational sophistication to Uber.

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

You are completing the detailed implementation architecture for the platform.

This volume focuses on the deeper contracts, operational models, persistence structures, distributed workflows, deployment boundaries, security controls, resilience behavior, and implementation-level architectural decisions required for engineers to build the system correctly.

The repository is the source of truth for what already exists.

Do not assume that another AI prompt, previous conversation, or previous architecture document exists.

---

# PROJECT

Define the detailed architecture for a production-grade Uber-style ride-hailing platform supporting:

* riders
* drivers
* driver onboarding and compliance
* vehicles
* driver availability
* driver location
* ride requests
* dispatch
* ride offers
* trips
* pricing
* dynamic pricing
* payments
* refunds
* driver earnings
* payouts
* ratings
* notifications
* safety
* fraud/risk
* support
* administration
* analytics
* search
* object storage
* realtime communication
* asynchronous jobs
* event streaming
* geospatial processing
* observability
* AWS infrastructure
* Kubernetes
* CI/CD
* disaster recovery

The platform must support high-volume concurrent workloads, geographically distributed users, frequent realtime state changes, financial transactions, and partial infrastructure failures.

---

# SOURCE OF TRUTH

Before defining or modifying architecture:

Inspect the repository and determine:

* current applications
* package/workspace structure
* backend services
* domain modules
* database models
* migrations
* Redis integrations
* queues
* event infrastructure
* API contracts
* realtime infrastructure
* mobile architecture
* web architecture
* infrastructure code
* environment configuration
* CI/CD
* tests
* observability
* existing integrations

Preserve working compatible architecture.

Do not redesign existing systems simply to make the architecture look cleaner.

If repository implementation conflicts with the requirements of this architecture and the conflict affects security, correctness, scalability, reliability, or compatibility, document the required architectural correction and its migration implications.

The repository remains authoritative for current implemented state.

This prompt is independently executable and must not rely on another AI-generated document.

---

# ARCHITECTURE OBJECTIVE

This volume establishes the detailed contracts and operational behavior required to convert the platform architecture into implementation-ready engineering boundaries.

The architecture must answer, with minimal ambiguity:

* what data is authoritative
* which component owns it
* which database transaction commits it
* which events are emitted
* which consumers process those events
* which operations are synchronous
* which operations are asynchronous
* how idempotency works
* how concurrency is controlled
* how state is reconstructed
* how clients recover from realtime failures
* how geographic workloads partition
* how services scale
* how privileged access is controlled
* how incidents are investigated
* how deployments fail safely
* how the system recovers after infrastructure loss

---

# DOMAIN CONTRACT MODEL

Every major domain must have explicit contracts.

For each domain define:

* purpose
* authoritative entities
* commands
* queries
* state transitions
* API ownership
* event ownership
* queue ownership
* persistence ownership
* authorization responsibility
* observability responsibility
* failure boundary

Use consistent domain vocabulary.

At minimum define these domains:

* Identity
* Rider
* Driver
* Compliance
* Vehicle
* Availability
* Location
* Ride Request
* Dispatch
* Trip
* Pricing
* Payment
* Earnings
* Payout
* Rating
* Notification
* Safety
* Fraud/Risk
* Support
* Administration
* Analytics

Do not allow domain names to mean different things in different parts of the system.

---

# CANONICAL ENTITY MODEL

Define the conceptual relationships among:

* User
* Rider Profile
* Driver Profile
* Driver Compliance Profile
* Compliance Requirement
* Compliance Evidence
* Vehicle
* Vehicle Eligibility
* Driver Availability State
* Driver Location
* Ride Request
* Ride Offer
* Dispatch Assignment
* Trip
* Trip Location
* Pricing Quote
* Pricing Configuration
* Fare
* Payment Method
* Payment Intent
* Payment Transaction
* Refund
* Driver Earning
* Payout
* Rating
* Notification
* Safety Incident
* Support Case
* Fraud/Risk Signal
* Promotion
* Administrative Action
* Audit Record

For each entity establish:

* owning domain
* identity strategy
* lifecycle
* immutable fields
* mutable fields
* state field where appropriate
* timestamps
* tenant/region relationship where appropriate
* deletion policy
* privacy classification

Do not create duplicate concepts representing the same business fact.

---

# IDENTIFIER STRATEGY

Define identifier principles for:

* users
* drivers
* riders
* vehicles
* rides
* offers
* trips
* payments
* payouts
* events
* jobs
* support cases
* audit records

Identifiers must be:

* globally safe
* non-guessable for externally exposed resources where appropriate
* stable
* immutable
* suitable for distributed systems

Do not expose sequential internal database identifiers as public authorization controls where doing so increases IDOR or enumeration risk.

Where internal and external identifiers differ, define the reason and mapping strategy.

---

# TIMESTAMP AND TIME-ZONE MODEL

Establish that authoritative timestamps use a consistent server-side representation.

Define handling for:

* created time
* updated time
* state-transition time
* event time
* scheduled ride time
* payment provider time
* compliance expiration
* location timestamp
* audit timestamp

Store machine timestamps in UTC unless an existing repository standard requires otherwise.

Preserve market-local timezone semantics for:

* scheduled rides
* operational schedules
* pricing windows
* airport rules
* promotions
* compliance deadlines

Never rely on mobile device clocks for authoritative lifecycle decisions.

---

# MONEY AND CURRENCY MODEL

Define a canonical representation for:

* fare amounts
* taxes
* platform fees
* promotions
* refunds
* driver earnings
* payout amounts

Requirements:

* no floating-point authoritative money values
* explicit currency
* deterministic rounding
* currency-specific precision
* consistent arithmetic rules
* immutable financial event references
* auditable adjustment history

Define how multi-currency operations behave.

The architecture must permit regional currency configuration without changing financial storage semantics.

---

# STATE-MACHINE ARCHITECTURE

Every critical lifecycle must have a formally defined state machine.

At minimum:

* account security state
* driver compliance state
* vehicle eligibility state
* driver availability state
* ride-request state
* ride-offer state
* dispatch assignment state
* trip state
* payment state
* refund state
* payout state
* support case state
* safety incident state
* promotion state

For every transition define:

* source state
* destination state
* actor
* authorization
* command
* persistence behavior
* emitted event
* idempotency semantics
* concurrency protection
* failure handling
* audit requirement

Invalid transitions must fail deterministically.

---

# STATE-VERSIONING MODEL

Define optimistic concurrency or equivalent version control for entities where concurrent mutations are realistic.

Evaluate versioning for:

* ride requests
* dispatch assignments
* ride offers
* trips
* payment records
* payout records
* compliance records

The architecture must prevent:

* two drivers accepting the same ride
* cancellation after a successful final assignment without correct arbitration
* trip completion racing with cancellation
* duplicate payout execution
* stale administrative writes overwriting newer state

---

# IDEMPOTENCY ARCHITECTURE

Define a reusable idempotency model.

Support idempotency for operations such as:

* ride request creation
* cancellation commands
* trip state transitions
* payment creation
* payment capture
* refunds
* payouts
* webhook handling
* important administrative mutations

Define:

* idempotency-key source
* scope
* storage
* TTL
* result replay
* collision behavior
* security considerations
* cleanup

Do not reuse one global idempotency namespace for unrelated business operations.

---

# REQUEST CORRELATION MODEL

Define correlation identifiers across:

* HTTP requests
* WebSocket actions
* background jobs
* Kafka events
* database-triggered outbox records
* external API requests

At minimum support:

* request ID
* correlation ID
* trace ID

Correlation must survive asynchronous boundaries.

A rider request that becomes a dispatch operation, trip transition, payment operation, notification job, and event should remain traceable as one business workflow without requiring sensitive data in logs.

---

# API CONTRACT MODEL

Define common HTTP API conventions.

Establish:

* route naming
* resource naming
* pagination
* cursor strategy where appropriate
* filtering
* sorting
* validation
* error envelope
* request IDs
* correlation IDs
* idempotency headers
* authentication
* authorization
* rate-limit response semantics
* versioning

Use stable error categories rather than exposing framework exceptions directly.

Error responses must not leak:

* stack traces
* SQL errors
* provider credentials
* internal topology
* secrets
* unnecessary personal information

---

# HTTP ERROR MODEL

Define canonical categories such as:

* validation error
* authentication error
* authorization error
* resource not found
* conflict
* rate limit exceeded
* dependency unavailable
* timeout
* business rule violation
* internal error

Specify how clients distinguish:

* retryable errors
* non-retryable errors
* authentication recovery
* idempotent command replay

Do not force clients to interpret arbitrary framework error strings.

---

# RATE-LIMITING ARCHITECTURE

Define limits for:

* authentication
* password recovery
* ride requests
* fare estimation
* location updates
* WebSocket actions
* notification operations
* payment operations
* administrative APIs
* support actions
* upload requests

Rate limits must account for:

* authenticated identity
* IP
* device/session
* API route
* region
* driver/rider state

Critical operations require stronger abuse protection than ordinary read APIs.

Redis-based distributed rate limiting must fail safely and must not silently grant unlimited access when Redis is unavailable.

---

# ABUSE-PREVENTION MODEL

Define protection against:

* credential stuffing
* ride-request spam
* cancellation abuse
* fake-driver activity
* location spoofing
* promotion abuse
* payment abuse
* payout abuse
* WebSocket flooding
* API enumeration
* support abuse
* document upload abuse

Separate:

* preventive controls
* detection controls
* investigative controls
* enforcement controls

Ensure fraud/risk systems can operate asynchronously where synchronous enforcement would threaten platform availability.

---

# DRIVER AVAILABILITY STATE

Define an authoritative operational state model such as:

* offline
* available
* offered
* en route to pickup
* at pickup
* on trip
* temporarily unavailable
* suspended

Separate the durable interpretation of driver state from fast-changing ephemeral presence.

The driver must not become dispatch-eligible solely because a mobile client reports an online flag.

Eligibility must combine:

* account state
* compliance
* vehicle eligibility
* current operational state
* geographic eligibility
* location freshness
* platform restrictions

---

# LOCATION FRESHNESS MODEL

Define thresholds for:

* fresh location
* stale location
* expired location

Architect the system so dispatch can make decisions based on known freshness.

An old location must never silently appear current.

Define behavior for:

* GPS disabled
* missing timestamps
* implausible movement
* invalid coordinates
* device clock skew
* duplicate location points
* out-of-order updates

---

# LOCATION PRIVACY MODEL

Exact driver and rider location must be treated as sensitive.

Define:

* who may access live coordinates
* who may access historical coordinates
* when access is permitted
* retention windows
* masking/generalization where appropriate
* administrative access
* audit requirements

A rider should not receive unnecessary driver location after a trip is no longer active.

Operational personnel should not automatically receive unrestricted historical location.

---

# GEO PARTITION MODEL

Define a geographic partitioning abstraction suitable for:

* countries
* regions
* cities
* service zones
* airports
* restricted areas

The dispatch engine should work against a bounded operational geography.

Partitioning should reduce:

* candidate search size
* event fan-out
* cache contention
* worker contention
* operational blast radius

Define how drivers and rides behave when crossing zone boundaries.

---

# DISPATCH RANKING ARCHITECTURE

Define dispatch ranking as a replaceable decision component.

Possible ranking inputs include:

* ETA
* distance
* driver availability
* vehicle compatibility
* location freshness
* trip context
* market rules
* driver constraints
* scheduled trip requirements

The architecture must not permanently embed ranking logic in controller code.

Define an interface allowing future ranking models or policies without replacing the dispatch orchestration layer.

Do not introduce machine-learning infrastructure unless the repository actually requires it; keep the contract extensible.

---

# DISPATCH FAIRNESS AND STARVATION

Architecture must address:

* repeated rejection
* driver starvation
* rider starvation
* geographically isolated drivers
* high-demand zones
* low-demand zones
* dispatch monopolization by a small set of drivers

If fairness mechanisms are used, define them as explicit policy components.

Do not allow undocumented heuristics to become hidden product behavior.

---

# DISPATCH FAILURE RECOVERY

If a dispatch worker crashes during assignment:

* no ride may become permanently invisible
* no driver may become permanently blocked
* no duplicate assignment may be created
* the ride must be recoverable from durable state

Define reconciliation or timeout workflows.

The same principle applies to:

* worker restarts
* Kafka consumer rebalance
* Redis outage
* API timeout after successful DB commit
* client disconnect during acceptance

---

# ACCEPTANCE RACE MODEL

Explicitly design the race in which two drivers attempt to accept the same ride.

The architecture must guarantee exactly one valid assignment.

Use the authoritative transactional mechanism required by the repository and database architecture.

A successful response to one driver must correspond to durable assignment state.

The losing driver must receive a deterministic conflict result and the system must remain consistent.

Do not depend on client-side timing.

---

# CANCELLATION RACE MODEL

Define races such as:

* rider cancellation vs driver acceptance
* rider cancellation vs trip start
* driver cancellation vs rider cancellation
* support/admin cancellation vs active trip
* payment failure vs completion
* completion vs duplicate completion

Each race must have:

* precedence rules
* authoritative state transition
* idempotency
* event semantics
* client-visible outcome

---

# SCHEDULED RIDES

Define architecture for scheduled rides even if implementation is phased.

Support:

* scheduled pickup time
* rider timezone
* advance reservation
* driver assignment window
* cancellation rules
* pricing snapshot rules
* reminder notifications
* dispatch preparation
* no-show behavior

Scheduled rides must not compromise the simpler immediate-dispatch path.

---

# TRIP VERIFICATION

Define mechanisms for verifying that the correct rider and driver begin a trip.

Architecture may support:

* trip PIN
* QR or equivalent verification
* trusted device/session checks
* driver/rider confirmation

Any verification method must protect against:

* accidental wrong rider pickup
* malicious trip start
* replay
* stale verification codes

Do not rely solely on visual confirmation when stronger verification is required.

---

# TRIP LOCATION MODEL

Define:

* location sampling
* route progression
* trip start location
* trip completion location
* optional historical route
* retention
* privacy
* accuracy
* storage strategy

Separate operational realtime location from long-term historical data.

Define how the system handles route gaps without falsely claiming continuous tracking.

---

# ETA ARCHITECTURE

ETA must be treated as an estimate rather than an authoritative promise.

Define:

* input data
* map-provider dependency
* driver location freshness
* caching
* update frequency
* timeout
* fallback
* stale-data labeling

ETA calculations must not block critical trip state transitions.

---

# MAP PROVIDER ABSTRACTION

Define interfaces for:

* geocoding
* reverse geocoding
* route calculation
* matrix/nearby travel estimates
* ETA

Define provider-independent internal models.

A map provider outage must have a defined fallback or degraded behavior.

Provider-specific response formats must not propagate into domain entities.

---

# PAYMENT STATE MODEL

Define separate lifecycle stages for:

* payment method
* payment intent
* authorization
* capture
* refund
* provider reconciliation

Example conceptual states may include:

* pending
* requires_action
* authorized
* capture_pending
* captured
* failed
* canceled
* refunded
* partially_refunded

Do not force all providers into a single exact lifecycle if provider semantics differ; create a stable internal abstraction and preserve provider-specific details behind integration boundaries.

---

# PAYMENT WEBHOOK MODEL

Every provider webhook must include:

* authentication/signature verification
* event ID
* provider event type
* provider object ID
* received timestamp
* processing state
* idempotency handling

Webhook processing must:

* verify authenticity
* persist receipt where appropriate
* deduplicate
* update authoritative internal state
* emit internal events when needed
* retry safely

Do not perform arbitrary long-running business workflows directly inside the HTTP webhook request.

---

# PAYMENT RECONCILIATION

Define scheduled and event-driven reconciliation.

Reconciliation must detect:

* provider records missing internally
* internal records missing provider confirmation
* unexpected provider states
* refund mismatches
* capture mismatches
* payout mismatches

Reconciliation must be observable and produce operational alerts.

It must never silently rewrite financial history.

---

# EARNINGS LEDGER MODEL

Design driver earnings so that historical financial records remain auditable.

Consider representing financial movements as immutable records or append-oriented entries.

Define how:

* earnings are generated
* fees are applied
* adjustments occur
* refunds impact earnings
* corrections are recorded
* payout eligibility is calculated

Do not overwrite old financial amounts merely to "fix" historical data.

Corrections should preserve audit history.

---

# PAYOUT ARCHITECTURE

Define:

* payout eligibility
* payout batching
* payout scheduling
* provider abstraction
* payout execution
* provider webhook handling
* failed payout recovery
* retry
* reconciliation

Payout execution must use strong idempotency protections.

A worker restart must never create an unintended duplicate payout.

---

# PROMOTION ARCHITECTURE

Define promotion ownership and lifecycle.

Promotions may include:

* percentage discounts
* fixed discounts
* capped discounts
* market-specific campaigns
* eligibility rules
* expiration
* usage limits
* rider-specific or cohort-specific eligibility

Promotions must not directly mutate payment records.

Discount decisions must become part of the authoritative fare computation.

---

# RATING ARCHITECTURE

Define:

* who may rate whom
* timing
* one-rating-per-trip rules
* rating visibility
* moderation
* abuse protection
* aggregation

Ratings must be tied to completed valid trips.

Administrative overrides must be audited.

---

# NOTIFICATION ARCHITECTURE

Define:

* notification intent
* template
* channel
* recipient
* delivery provider
* delivery status
* retry state

Separate:

* business event
* notification job
* provider delivery

A failed SMS provider must not cause trip state failure.

---

# PUSH NOTIFICATION SECURITY

Push payloads must avoid unnecessary sensitive information.

Do not place:

* full payment information
* authentication tokens
* private documents
* unnecessary exact coordinates

inside notification payloads.

Use notifications as wakeup/notification mechanisms and retrieve authoritative sensitive information through authenticated APIs where needed.

---

# SUPPORT ARCHITECTURE

Define support case structure around references to:

* user
* ride
* trip
* payment
* driver
* safety incident

Support agents must access only information required for the case.

Support workflows must not directly mutate arbitrary domain state.

Operational actions must invoke domain-authorized commands.

---

# ADMIN COMMAND ARCHITECTURE

Administrative operations should use explicit commands rather than arbitrary database editing.

Examples:

* suspend driver
* reinstate driver
* cancel ride
* refund payment
* override compliance status
* alter pricing configuration
* disable promotion
* restrict account

Each command must have:

* permission
* validation
* authorization
* audit event
* reason
* affected entity
* idempotency where necessary

---

# AUDIT ARCHITECTURE

Define audit logging for security and operationally significant actions.

Audit records should capture:

* actor
* actor type
* action
* target
* timestamp
* request/correlation ID
* source
* result
* before/after data or structured delta where appropriate

Do not place sensitive raw payloads into audit logs indiscriminately.

Audit data should have restricted access and appropriate retention.

---

# CONFIGURATION ARCHITECTURE

Separate runtime configuration from deploy-time secrets.

Configuration categories include:

* market configuration
* ride-product configuration
* pricing rules
* surge settings
* cancellation rules
* service zones
* notification settings
* rate limits
* operational feature flags

Define:

* configuration ownership
* versioning
* validation
* rollout
* rollback
* auditability
* regional overrides

Invalid configuration must be rejected before becoming active.

---

# FEATURE-FLAG ARCHITECTURE

Feature flags may be used for controlled rollout.

Define:

* flag ownership
* scope
* targeting
* default
* rollback
* audit

Do not use feature flags to hide incomplete code forever.

Critical financial and safety rules should not depend on mutable client-side flags.

---

# SECRET MANAGEMENT

Define production secret handling through AWS or an appropriate managed secret solution.

Secrets include:

* database credentials
* provider API keys
* payment secrets
* OAuth credentials
* signing keys
* webhook secrets
* encryption keys

Secrets must:

* never be committed
* never be logged
* be injected through secure runtime mechanisms
* have rotation strategies
* have access policies
* be auditable

---

# SERVICE-TO-SERVICE SECURITY

Define authenticated communication between backend components.

Where appropriate use:

* workload identities
* short-lived credentials
* mTLS
* signed service tokens
* IAM-backed authorization

Avoid unrestricted internal network trust.

A compromised internal service must not automatically gain access to every domain.

---

# NETWORK ARCHITECTURE

Define AWS network boundaries.

At minimum architect:

* VPC
* public ingress
* private application networks
* worker networks
* database subnets
* cache subnets
* event infrastructure
* controlled egress
* administrative access paths

Databases and internal infrastructure must not be publicly reachable.

---

# KUBERNETES ARCHITECTURE

Define the Kubernetes workload model for:

* API services
* WebSocket gateways
* dispatch workers
* queue workers
* event consumers
* notification workers
* scheduled workloads

Specify:

* deployments
* services
* ingress
* horizontal pod autoscaling
* pod disruption budgets
* readiness probes
* liveness probes
* startup probes
* resource requests
* resource limits
* graceful termination
* topology spreading
* secrets integration

Do not scale all workloads identically.

Location ingestion, dispatch, WebSockets, APIs, and asynchronous workers have different scaling profiles.

---

# DATABASE HIGH AVAILABILITY

Define production PostgreSQL architecture with consideration for:

* primary/standby
* automated backups
* point-in-time recovery
* replicas
* connection pooling
* failover
* maintenance
* migration safety

Determine which workloads may use read replicas.

Never route strongly consistent writes to replicas.

Do not assume replicas are instantly consistent.

---

# REDIS HIGH AVAILABILITY

Define Redis topology appropriate for:

* caching
* rate limiting
* presence
* dispatch state
* ephemeral location

Document:

* failure behavior
* failover
* key expiration
* cache warmup
* loss of ephemeral state
* rebuild behavior

The architecture must remain correct if Redis loses non-authoritative state.

---

# EVENT STREAMING ARCHITECTURE

Define Kafka topology concepts:

* topics
* partitions
* replication
* consumer groups
* retention
* replay
* dead-letter topics
* schema registry or equivalent schema governance

Partitioning should preserve required entity ordering without creating severe hot partitions.

Examples requiring careful ordering may include:

* trip events
* payment events
* driver state events

Do not require global ordering.

---

# EVENT VERSIONING

Every domain event should support schema evolution.

Define:

* version field
* compatibility policy
* optional versus required fields
* deprecation
* consumer migration
* replay compatibility

Consumers must not break simply because an additive event field is introduced.

---

# EVENT PRIVACY

Do not publish unnecessary sensitive data into broad event topics.

Where possible publish:

* identifiers
* state changes
* minimal business metadata

Consumers that require sensitive details should obtain them through authorized channels rather than receiving excessive personal information in every event.

---

# OUTBOX PROCESSING

Define operational behavior for the transactional outbox:

* polling or CDC strategy
* batch size
* retry
* lock strategy
* publishing state
* deduplication
* failed message handling
* cleanup
* lag monitoring

Outbox processing must not create unbounded backlog without alerts.

---

# QUEUE TOPOLOGY

Define logical queue groups for:

* notifications
* receipts
* payment reconciliation
* payout processing
* compliance
* fraud/risk
* scheduled rides
* cleanup
* analytics enrichment
* support operations

Separate critical jobs from low-priority jobs to prevent noisy-neighbor behavior.

---

# DEAD-LETTER ARCHITECTURE

Every retryable asynchronous workflow must have a defined terminal failure path.

Dead-letter handling must specify:

* payload preservation
* reason
* retry count
* original timestamps
* correlation ID
* operator visibility
* replay mechanism
* retention

Dead letters must be operationally actionable.

---

# MOBILE ARCHITECTURE CONSIDERATIONS

Define high-level production architecture for rider and driver mobile clients.

The architecture must support:

* secure credential storage
* authenticated API communication
* WebSockets
* network retries
* reconnection
* background location for drivers where permitted
* app lifecycle
* push notifications
* deep links
* secure local storage
* offline-tolerant UI
* state reconciliation
* platform permissions

Driver background location is particularly sensitive and must follow platform requirements and privacy controls.

---

# MOBILE LOCATION SECURITY

Driver location updates must:

* authenticate the session
* validate coordinates
* validate timestamps
* enforce rate limits
* detect impossible values
* bind updates to the authenticated driver/device/session
* reject unauthorized location submissions

Do not allow arbitrary clients to submit location for another driver.

---

# WEB ARCHITECTURE CONSIDERATIONS

The web client must separate:

* server state
* local UI state
* authenticated identity
* realtime state
* cached reads

Critical actions must always be validated server-side.

The web application must not contain authoritative business rules that are absent from the backend.

Administrative surfaces must use distinct permission boundaries.

---

# MULTI-CLIENT CONTRACT MODEL

The same backend platform may serve:

* rider web
* rider mobile
* driver mobile
* operations web
* support tooling

Contracts must remain stable across clients.

Avoid creating subtly different business semantics for different clients unless the product intentionally requires it.

---

# BACKWARD COMPATIBILITY

API changes must consider:

* older mobile versions
* rolling deployments
* multiple server versions
* delayed event consumers
* cached configuration
* partial client upgrades

Prefer additive changes where feasible.

Where breaking changes are unavoidable:

* introduce a migration period
* version appropriately
* maintain compatibility windows
* remove obsolete behavior only after safe migration

---

# DEPLOYMENT ARCHITECTURE

Define the production deployment lifecycle:

1. Build.
2. Test.
3. Security validation.
4. Container image creation.
5. Artifact publication.
6. Infrastructure validation.
7. Staging deployment.
8. Smoke/E2E validation.
9. Production rollout.
10. Health verification.
11. Rollback capability.

Deployments must account for:

* database migrations
* API compatibility
* event schema compatibility
* worker compatibility
* WebSocket versioning
* mobile client compatibility

---

# DATABASE MIGRATION STRATEGY

Use expand-and-contract principles where necessary.

Dangerous migrations include:

* dropping columns immediately
* changing data meaning in place
* rebuilding huge indexes synchronously during peak load
* making new constraints before cleaning existing data
* introducing incompatible enum/state changes

Define safe migration sequencing.

Database migrations must be:

* versioned
* reviewable
* repeatable
* observable
* tested before production

---

# DISASTER-RECOVERY ARCHITECTURE

Define targets for:

* RPO
* RTO

at least for critical domains.

Classify systems by recovery importance:

* identity
* active trips
* payments
* driver earnings
* dispatch
* notifications
* analytics
* search

Define restoration order.

Active-trip recovery must preserve authoritative trip state even if ephemeral location or realtime connection state is lost.

---

# BACKUP ARCHITECTURE

Define backups for:

* PostgreSQL
* object storage metadata/configuration where appropriate
* infrastructure state
* critical configuration
* audit records

Backups must be:

* encrypted
* access-controlled
* monitored
* retention-managed
* restoration-tested

A backup that has never been restored must not be treated as proven recovery capability.

---

# RESILIENCE TESTING ARCHITECTURE

Plan for controlled testing of:

* Redis loss
* Kafka consumer failure
* queue-worker crash
* API pod termination
* database failover
* external map outage
* payment provider timeout
* notification outage
* WebSocket gateway failure
* node failure
* regional degradation

The platform must maintain its most critical invariants during these scenarios.

---

# SLO AND ALERT ARCHITECTURE

Define actionable alerts around:

* API availability
* elevated latency
* dispatch backlog
* dispatch assignment latency
* stale-driver location ratio
* trip state-processing failures
* payment failures
* payout failures
* queue backlog
* dead letters
* Kafka consumer lag
* database saturation
* Redis saturation
* WebSocket disconnect rates
* notification failures

Do not alert on every low-level metric.

Alerts should map to actionable operational conditions.

---

# CAPACITY PLANNING

Define capacity dimensions for:

* API requests per second
* WebSocket connections
* location updates per second
* dispatch requests
* active trips
* database writes
* Redis operations
* Kafka events
* queue jobs
* payment volume

Identify likely bottlenecks.

Define scaling signals and safeguards.

The architecture must be capable of surviving major demand spikes without uncontrolled cascading failure.

---

# LOAD-SHEDDING AND BACKPRESSURE

Define mechanisms for protecting the system during overload.

Potential controls:

* API rate limiting
* admission control
* bounded queues
* concurrency caps
* prioritized workloads
* stale-cache fallback
* degraded noncritical features
* location sampling reduction
* asynchronous processing

Critical trip and payment correctness must be protected before nonessential features.

---

# GRACEFUL DEGRADATION

Define degraded states for:

* map provider unavailable
* search unavailable
* notification provider unavailable
* analytics unavailable
* fraud service delayed
* Redis degraded
* Kafka lagging
* payment provider degraded

Examples:

* analytics may lag without stopping rides
* notification delivery may be delayed without changing trip truth
* search may be unavailable while transactional workflows continue
* realtime visual updates may become less frequent while authoritative trip state remains correct

Never silently degrade financial correctness or assignment uniqueness.

---

# SECURITY THREAT MODEL

Perform a structured threat analysis for:

* rider account
* driver account
* administrative account
* mobile client
* web client
* API gateway
* WebSocket gateway
* dispatch
* location pipeline
* payment system
* file uploads
* provider webhooks
* event system
* queues
* Kubernetes
* CI/CD
* secrets
* databases

For each major threat identify:

* asset
* attacker
* attack surface
* control
* detection
* response

---

# SUPPLY-CHAIN SECURITY

Define controls for:

* npm dependencies
* Docker base images
* container scanning
* dependency vulnerability scanning
* secret scanning
* SBOM generation where appropriate
* signed artifacts where applicable
* CI permissions
* Terraform/Kubernetes configuration review

CI/CD credentials must have least privilege.

---

# DATA CLASSIFICATION

Define data classes such as:

* public
* internal
* confidential
* highly sensitive

Map examples:

* public product information
* internal operational metrics
* confidential support information
* highly sensitive identity/payment/location/compliance information

Use classification to drive:

* encryption
* logging restrictions
* access control
* retention
* auditing

---

# DATA RETENTION MODEL

Define retention categories for:

* active ride data
* historical trip data
* location data
* payment records
* payout records
* compliance evidence
* support cases
* safety incidents
* audit records
* analytics events
* logs
* traces

Retention must balance:

* operational requirements
* legal obligations
* fraud investigation
* privacy
* cost

Do not retain data indefinitely without justification.

---

# DELETION AND ACCOUNT CLOSURE

Define the architecture for account deletion requests.

Distinguish:

* directly deletable data
* data requiring anonymization
* legally/financially retained records
* audit records
* derived analytics data
* backups

Account deletion must not corrupt financial history or audit integrity.

Define asynchronous deletion jobs where appropriate.

---

# DATA EXPORT

Where privacy requirements require it, support export of user-owned data.

Exports should:

* be authenticated
* be authorized
* be asynchronous for large datasets
* have expiration
* be securely stored
* be auditable
* avoid exposing other users' data

---

# OPERATIONAL RUNBOOK ARCHITECTURE

Define the required operational runbooks for:

* database failover
* Redis recovery
* Kafka backlog
* queue backlog
* dispatch degradation
* payment provider outage
* map provider outage
* notification outage
* suspicious fraud spike
* location pipeline degradation
* WebSocket degradation
* production rollback
* security incident
* compromised credentials

Runbooks must identify:

* symptoms
* dashboards
* decision points
* safe actions
* rollback
* communication
* verification

---

# ARCHITECTURAL TESTABILITY

Every critical architectural component must have a test strategy.

Define tests for:

* state machines
* dispatch races
* idempotency
* event processing
* outbox
* queue retries
* payment webhooks
* geospatial queries
* authorization
* realtime recovery
* failure handling
* migrations

Architecture that cannot be meaningfully tested is not complete.

---

# ARCHITECTURAL ANTI-PATTERNS

Explicitly reject:

* shared mutable domain state without ownership
* direct cross-domain SQL writes
* business rules hidden in controllers
* event-driven workflows without idempotency
* background jobs without retry/terminal failure handling
* provider APIs called from arbitrary modules
* client-controlled financial state
* client-controlled authorization
* Redis-only business truth
* globally ordered event streams
* infinite event retries
* synchronous analytics on critical trip paths
* synchronous notifications on critical trip paths
* unbounded location persistence
* unrestricted admin access
* undocumented feature flags
* database edits as ordinary operational workflows

---

# ARCHITECTURAL IMPLEMENTATION MAP

Create a detailed implementation map showing where the architecture should live in the repository.

The map should identify, where appropriate:

* backend application boundaries
* domain modules
* infrastructure modules
* shared libraries
* API contracts
* event schemas
* worker applications
* database schema organization
* WebSocket gateways
* mobile applications
* web applications
* Terraform modules
* Helm charts
* Kubernetes manifests
* observability configuration
* documentation

Do not force a folder structure that contradicts the repository.

The implementation map must show responsibilities rather than merely naming directories.

---

# CROSS-DOMAIN CONTRACT MATRIX

Create a matrix describing the main cross-domain interactions.

At minimum include relationships among:

* Rider → Ride Request
* Ride Request → Pricing
* Ride Request → Dispatch
* Dispatch → Driver Availability
* Dispatch → Location
* Dispatch → Trip
* Trip → Pricing
* Trip → Payment
* Trip → Earnings
* Trip → Notification
* Trip → Rating
* Trip → Safety
* Payment → Earnings
* Payment → Refund
* Driver Compliance → Dispatch Eligibility
* Vehicle Eligibility → Dispatch
* Fraud/Risk → Account/Trip/Payment
* Administration → Every privileged domain

For each interaction specify:

* caller
* callee
* command/query/event/job
* consistency requirement
* failure behavior
* authorization requirement

---

# BUSINESS-CRITICAL INVARIANTS

Define invariants that must never be violated.

At minimum:

* a ride cannot be assigned to two active drivers
* a driver cannot have conflicting active trip assignments
* a completed trip cannot revert to an earlier active state without an explicit controlled correction workflow
* a captured payment must map to the correct financial record
* a payout must not execute twice for the same payout intent
* a rider cannot access another rider's trip
* a driver cannot receive another driver's private ride offer
* an ineligible driver cannot become dispatch-eligible
* invalid pricing configuration cannot produce an authoritative fare
* administrative actions must be auditable
* deleted/anonymized accounts must not expose private data through search or caches

---

# FAILURE AND RECOVERY MATRIX

Create a matrix for major dependency failures.

At minimum include:

| Dependency     | Failure     | Impact               | Immediate Behavior                      | Recovery                   | Data Risk  |
| -------------- | ----------- | -------------------- | --------------------------------------- | -------------------------- | ---------- |
| PostgreSQL     | unavailable | transactional writes | reject/degrade safely                   | failover/recovery          | high       |
| Redis          | unavailable | ephemeral state      | use defined fallback                    | rebuild                    | medium     |
| Kafka          | unavailable | events delayed       | preserve transactional state            | replay/outbox              | medium     |
| BullMQ         | unavailable | async work delayed   | persist work where required             | worker recovery            | medium     |
| Maps           | unavailable | ETA/routes           | degraded behavior                       | provider recovery/fallback | low/medium |
| Payments       | unavailable | payment operations   | controlled pending/failure              | retry/reconcile            | high       |
| Notifications  | unavailable | user alerts          | queue/retry                             | provider recovery          | low/medium |
| Search         | unavailable | operational lookup   | transactional APIs remain authoritative | reindex                    | low        |
| Object storage | unavailable | uploads/documents    | reject or queue safely                  | provider recovery          | medium     |
| WebSockets     | unavailable | realtime freshness   | clients use API recovery                | gateway recovery           | low        |

Adapt the matrix to actual repository architecture.

---

# ARCHITECTURAL VALIDATION

Validate the completed architecture for:

## CORRECTNESS

Verify:

* authoritative ownership
* valid state transitions
* concurrency controls
* financial consistency
* idempotency
* event reliability

## SECURITY

Verify:

* trust boundaries
* authentication
* authorization
* secret handling
* webhook verification
* upload security
* administrative controls

## PRIVACY

Verify:

* location access
* identity exposure
* retention
* deletion
* privileged access

## PERFORMANCE

Verify:

* dispatch scalability
* location throughput
* WebSocket fan-out
* database hot paths
* event throughput

## RELIABILITY

Verify:

* timeouts
* retries
* backpressure
* degradation
* failover
* recovery

## OPERABILITY

Verify:

* metrics
* logs
* traces
* dashboards
* alerts
* runbooks

## DEPLOYABILITY

Verify:

* container boundaries
* migration strategy
* rolling deployments
* backward compatibility
* infrastructure automation
* rollback

---

# IMPLEMENTATION BOUNDARIES

This volume completes the detailed architecture and operational contract model.

Do not use this prompt to implement every feature.

Focus on documenting:

* canonical entities
* state machines
* contracts
* concurrency
* idempotency
* domain interaction
* location architecture
* dispatch architecture
* financial architecture
* security architecture
* privacy
* event and queue semantics
* deployment
* resilience
* disaster recovery
* operational behavior

Implementation must follow the repository's actual state and must not depend on the existence of an earlier AI prompt.

---

# REQUIRED ARCHITECTURE DELIVERABLES

Create or update the appropriate repository documentation to capture:

## CANONICAL DOMAIN MODEL

Document:

* domains
* entities
* ownership
* lifecycle

## STATE MACHINES

Document:

* valid states
* transitions
* authorization
* concurrency
* events

## API CONTRACT MODEL

Document:

* resource conventions
* errors
* pagination
* idempotency
* authorization

## EVENT CONTRACT MODEL

Document:

* event envelope
* topics
* partitions
* versions
* consumers
* replay

## QUEUE CONTRACT MODEL

Document:

* jobs
* payloads
* retries
* dead letters
* recovery

## DISPATCH MODEL

Document:

* geo partitions
* candidate discovery
* ranking
* offer lifecycle
* acceptance race
* cancellation race
* recovery

## LOCATION MODEL

Document:

* ingestion
* freshness
* ephemeral state
* retention
* privacy
* geospatial processing

## FINANCIAL MODEL

Document:

* money representation
* pricing
* payments
* refunds
* earnings
* payouts
* reconciliation

## REALTIME MODEL

Document:

* WebSockets
* authentication
* authorization
* reconnect
* synchronization
* recovery

## SECURITY MODEL

Document:

* trust zones
* authentication
* service authentication
* permissions
* secret management
* threat model

## PRIVACY MODEL

Document:

* classification
* retention
* deletion
* data access

## INFRASTRUCTURE MODEL

Document:

* AWS
* networking
* Kubernetes
* databases
* Redis
* Kafka
* object storage
* observability

## RESILIENCE MODEL

Document:

* failure modes
* degradation
* backpressure
* recovery
* DR

## OPERATIONS MODEL

Document:

* SLOs
* dashboards
* alerts
* runbooks
* incident workflows

---

# VALIDATION REQUIREMENTS

After documenting the architecture:

1. Inspect the repository again.
2. Compare the architecture against current implementation.
3. Identify incompatible assumptions.
4. Identify missing integration boundaries.
5. Identify duplicate sources of truth.
6. Verify data ownership.
7. Verify state-machine correctness.
8. Verify concurrency protections.
9. Verify idempotency requirements.
10. Verify event and queue recovery.
11. Verify location scalability.
12. Verify dispatch scalability.
13. Verify payment correctness.
14. Verify security boundaries.
15. Verify privacy controls.
16. Verify infrastructure assumptions.
17. Verify disaster-recovery behavior.
18. Verify backwards compatibility.
19. Verify testability.
20. Update documentation so the architecture represents the actual intended implementation.

Do not leave critical contradictions unresolved without explicitly reporting them.

---

# PROHIBITED PRACTICES

Never:

* assume a previous AI architecture exists
* create unexplained duplicate entities
* allow direct cross-domain database mutation
* use Redis as durable business truth
* use events as the sole current state source
* allow duplicate driver assignment
* trust client clocks
* trust client payment state
* trust client authorization
* create payment operations without idempotency
* allow webhook duplication to change financial results twice
* use unlimited retries
* retain location indefinitely by default
* expose precise location without authorization
* provide unrestricted administrator data access
* make analytics synchronous with trip execution
* make notification delivery a critical trip dependency
* allow a failed search index to invalidate transactional truth
* make provider-specific models the domain contract
* create public access to private compliance documents
* introduce architecture without documenting failure behavior

---

# FINAL ARCHITECTURE REVIEW

The completed architecture must demonstrate how the platform maintains its core invariants through:

* normal operation
* high traffic
* driver and rider churn
* duplicate requests
* duplicate events
* stale location
* concurrent acceptance
* cancellation races
* payment uncertainty
* provider outages
* Redis loss
* queue failure
* Kafka lag
* WebSocket disconnects
* worker crashes
* rolling deployments
* database failover
* regional incidents

The architecture must remain coherent under these conditions.

---

# COMPLETION REPORT REQUIREMENTS

When the architecture work is complete, report:

## FILES CREATED

List every new architecture document.

## FILES MODIFIED

List every modified repository file.

## DOMAIN MODEL

Summarize canonical entities and ownership.

## STATE MACHINES

Summarize major lifecycles and transition safeguards.

## API CONTRACTS

Summarize API conventions, errors, idempotency, and authorization.

## DATA MODEL

Summarize PostgreSQL, Redis, geospatial, search, and object-storage architecture.

## DISPATCH

Summarize:

* partitioning
* candidate discovery
* ranking
* offer lifecycle
* race prevention
* recovery

## REALTIME

Summarize WebSocket architecture, authorization, and reconnect behavior.

## LOCATION

Summarize ingestion, freshness, privacy, retention, and scaling.

## FINANCIAL SYSTEMS

Summarize pricing, payment, refund, earnings, payout, and reconciliation architecture.

## EVENTS

Summarize event envelope, topics, versioning, outbox behavior, replay, and consumers.

## QUEUES

Summarize job types, retries, dead letters, and recovery.

## SECURITY

Summarize:

* authentication
* authorization
* service security
* secrets
* threat model
* administrative controls

## PRIVACY

Summarize data classification, retention, deletion, and access controls.

## INFRASTRUCTURE

Summarize AWS, networking, Kubernetes, database, Redis, Kafka, and deployment architecture.

## RELIABILITY

Summarize:

* SLOs
* degradation
* failure handling
* recovery
* disaster recovery

## OPERATIONS

Summarize:

* observability
* dashboards
* alerts
* runbooks
* incident response

## VALIDATION

Report:

* repository inspection
* architecture consistency review
* dependency review
* state-machine review
* concurrency review
* security review
* privacy review
* performance review
* reliability review
* deployment review
* disaster-recovery review

## UNRESOLVED ISSUES

List only genuine blockers or architectural uncertainties that remain.

Do not claim completion if critical architecture decisions remain undefined.

---

# FINAL ENGINEERING PRINCIPLE

The platform must be architected as one coherent distributed system whose business invariants survive concurrency, failures, scale, regional growth, and continuous deployment.

The most important architectural properties are:

* explicit ownership
* deterministic state transitions
* strong transactional boundaries
* safe concurrency
* robust idempotency
* recoverable asynchronous workflows
* secure realtime communication
* controlled location processing
* financially auditable operations
* least-privilege access
* privacy by design
* observable critical paths
* graceful degradation
* reliable deployment
* tested recovery

The repository remains the implementation source of truth.

Every implementation team must be able to inspect the repository, map its existing implementation to this architecture, preserve compatible behavior, and make incremental production-grade changes without relying on any previous AI response.

This architecture volume completes the detailed system contracts, operational semantics, and resilience model required for implementation.
