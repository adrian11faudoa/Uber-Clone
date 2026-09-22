# Uber-Style Global Ride-Hailing & Mobility Platform — Architecture Prompt — Volume 1

## ROLE

You are the principal architecture organization responsible for designing the foundational architecture of an original, production-grade global ride-hailing and mobility platform.

Operate simultaneously as:

* Principal Software Architect
* Distributed Systems Architect
* Backend Architect
* Database Architect
* Cloud Architect
* Security Architect
* Reliability Architect
* Platform Architect
* Realtime Systems Architect
* Data Architect
* Performance Architect
* Technical Writer

Your responsibility in this milestone is to create the foundational architectural source of truth for the project.

You are not implementing the application code yet.

You are designing the architecture artifacts that subsequent implementation milestones will use as their authoritative technical foundation.

Do not produce superficial architecture documentation.

Do not produce generic descriptions that could apply to any software system.

Make concrete architectural decisions appropriate for the product, its scale targets, its technology direction, and its operational requirements.

Where a decision intentionally remains configurable or provider-abstracted, document the boundary precisely.

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

The platform supports major mobility workflows including:

* rider registration and authentication
* driver onboarding and verification
* driver availability
* realtime driver location
* ride requesting
* dispatch and matching
* trip lifecycle
* pricing and fare estimation
* payments
* driver earnings and payouts
* notifications
* rider-driver messaging
* ratings and reviews
* trust and safety
* support
* scheduled rides
* fleet operations
* geographic service areas
* analytics and reporting

The product must be original.

Do not clone proprietary internal architecture, branding, proprietary algorithms, or private implementation details belonging to another company.

# SCALE TARGETS

The architecture must be suitable for targets such as:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* 100,000+ concurrent realtime sessions and higher at peak
* high-frequency driver location ingestion
* multi-region global deployment
* large event throughput
* geographically distributed operations
* high availability for critical mobility workflows

These are architectural targets.

They are not measured production results.

Do not claim that these capacities have been achieved merely because the architecture is designed for them.

# TECHNOLOGY DIRECTION

The architecture must be designed around the locked project stack.

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
* Prisma where compatible with the final architecture
* Redis

## Eventing

* Kafka or Redpanda

Use one coherent event-broker architecture.

## Background Processing

* BullMQ or equivalent queue architecture

## Search

* OpenSearch or Elasticsearch-compatible architecture

## Object Storage

* Amazon S3

## Payments

* provider abstraction with a Stripe-compatible implementation boundary

## Maps and Routing

Provider abstraction for:

* maps
* geocoding
* routing
* distance
* ETA
* related geographic services

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

# ARCHITECTURE OBJECTIVE

Create the foundational architecture documentation that defines how all major parts of the platform fit together.

This milestone must establish:

* system boundaries
* domain boundaries
* major components
* logical service/module boundaries
* deployment topology
* data ownership
* critical lifecycle models
* realtime architecture
* dispatch architecture
* geography/location architecture
* security architecture
* reliability architecture
* observability architecture
* scale strategy
* major architectural decisions

Architecture Volume 2 will later deepen the contracts.

Do not prematurely turn this volume into a complete API/event/schema contract catalog.

# SOURCE OF TRUTH

The architecture artifacts created by this milestone become the project's authoritative architectural source of truth.

The artifacts must be:

* internally consistent
* concrete
* implementation-oriented
* versionable
* understandable by backend, frontend, mobile, infrastructure, QA, security, and operations engineers

The architecture must not depend on undocumented assumptions.

Where an architectural decision affects later implementation, record it explicitly.

# REQUIRED ARCHITECTURE ARTIFACT SET

Create a coherent architecture documentation package under the repository's appropriate architecture-documentation location.

Inspect the repository first and preserve its existing documentation organization when possible.

At minimum, create or update the following artifacts.

## 1. Architecture Overview

Create a comprehensive architecture overview describing:

* product purpose
* scale targets
* major capabilities
* architectural style
* system boundaries
* deployment model
* major technology choices
* major reliability goals
* major security goals
* major architectural constraints

Explain why the architecture is appropriate for a global ride-hailing platform.

## 2. System Context

Document the system's external context.

Include:

* riders
* drivers
* operations
* support
* safety
* platform administrators
* payment providers
* mapping providers
* notification providers
* identity/verification providers where applicable
* fraud/risk providers where applicable
* AWS infrastructure
* observability systems
* external clients

Clearly distinguish:

* trusted internal systems
* authenticated clients
* third-party providers
* infrastructure dependencies

## 3. Container / Major Component Architecture

Define the major runtime components.

At minimum address the responsibilities of:

* public/API gateway layer
* identity/account capabilities
* rider capabilities
* driver capabilities
* trip capabilities
* dispatch capabilities
* location capabilities
* pricing capabilities
* payment capabilities
* earnings/payout capabilities
* notification capabilities
* messaging capabilities
* trust/safety capabilities
* support/operations capabilities
* fleet capabilities
* scheduled-trip capabilities
* routing/geography capabilities
* analytics/reporting capabilities
* event infrastructure
* background workers
* realtime gateway
* search
* object storage
* core data stores

Do not automatically make every domain a separate deployable microservice.

Explicitly distinguish:

* logical domain/module
* independently deployable service
* shared platform capability
* infrastructure dependency

## 4. Domain Boundary Model

Define the major business domains and their responsibilities.

For every major domain document:

* purpose
* owned responsibilities
* authoritative data
* commands it accepts
* events it produces
* events it consumes
* dependencies
* responsibilities explicitly excluded

At minimum cover:

* Identity
* Rider
* Driver
* Vehicle/Fleet
* Location/Presence
* Trip
* Dispatch
* Pricing
* Payment
* Earnings/Payout
* Notification
* Messaging
* Rating/Trust
* Safety
* Support/Operations
* Scheduled Trips
* Routing/Geography
* Analytics/Reporting

Avoid circular ownership.

A domain must not be simultaneously treated as the authoritative owner of the same business entity by multiple components.

## 5. Service and Module Boundary Strategy

Define when functionality belongs:

* inside one backend module
* inside a separate service
* inside a worker
* inside a platform component
* inside an infrastructure system

Use concrete criteria such as:

* independent scaling
* failure isolation
* data ownership
* lifecycle
* latency requirements
* security boundaries
* deployment independence
* operational complexity

Do not use microservices merely as a label.

Do not create a monolith merely because several domains are related.

The architecture must explain the selected balance.

## 6. Deployment Topology

Design the major deployment topology.

Document:

* web deployment
* mobile clients
* API workloads
* worker workloads
* realtime workloads
* event brokers
* Redis
* PostgreSQL/PostGIS
* OpenSearch
* S3
* observability
* ingress
* edge routing
* Kubernetes/EKS
* regional boundaries

Distinguish:

* client-side execution
* edge execution
* application runtime
* data infrastructure
* control-plane infrastructure

## 7. Request Flow Architecture

Document the major synchronous request flows.

At minimum cover:

* authentication
* rider requesting a ride
* driver becoming available
* trip creation
* dispatch initiation
* offer acceptance
* trip start
* trip completion
* payment authorization/capture
* cancellation
* refund
* support access

Show where:

* validation occurs
* authorization occurs
* transactions occur
* asynchronous work begins
* realtime notifications are generated
* external providers are called

## 8. Trip Lifecycle Architecture

Define the canonical trip lifecycle.

Document:

* trip creation
* estimate/quote
* requested
* dispatching
* driver assigned
* driver arriving
* driver arrived
* trip started
* trip completed
* cancelled states
* expired states
* exceptional states

Define:

* lifecycle ownership
* state-transition authority
* invalid transitions
* concurrency considerations
* event publication
* realtime propagation
* persistence expectations

Do not define every API contract in this volume.

Focus on architectural ownership and lifecycle semantics.

## 9. Driver Availability and Location Architecture

Define how the platform represents:

* driver availability
* work session
* current location
* location freshness
* geospatial indexing
* stale drivers
* location sequence/version
* regional ownership
* realtime propagation

Explain the distinction between:

* durable trip-associated location history
* ephemeral current location
* dispatch candidate state
* analytical location data

Define the responsibilities of:

* PostgreSQL/PostGIS
* Redis
* event infrastructure
* realtime gateway

for location-related workloads.

## 10. Dispatch Architecture

Define the high-level dispatch architecture.

Document:

* candidate discovery
* geographic filtering
* eligibility
* scoring/order
* offers
* acceptance
* winner selection
* race prevention
* timeout
* retry
* reassignment
* regional behavior

Define where correctness must be strongly enforced.

Do not invent a proprietary matching algorithm.

Describe the architectural extension points and invariants instead.

## 11. Pricing Architecture

Define the pricing subsystem boundaries.

Cover:

* fare estimates
* quote generation
* pricing versions
* dynamic pricing
* promotions
* cancellation fees
* final fare
* configuration
* rounding
* consistency between estimate and final charge

Define which values must be immutable once committed.

Separate pricing calculation from payment execution.

## 12. Payment and Financial Architecture

Define the financial architecture at a high level.

Cover:

* payment methods
* payment intent
* authorization
* capture
* refunds
* disputes
* tips
* earnings
* payouts
* reconciliation
* immutable financial ledger
* provider abstraction

Explicitly distinguish:

* payment-provider state
* internal financial state
* trip/fare state

Define the authoritative source of truth for each.

## 13. Realtime Architecture

Define the realtime system architecture.

Cover:

* WebSocket gateway
* authentication
* authorization
* connections
* subscriptions
* rider updates
* driver updates
* trip updates
* messaging
* notifications
* reconnect behavior
* presence
* fanout
* regional routing

Explain how realtime state is coordinated across horizontally scaled instances.

Do not depend on in-memory state for globally authoritative state.

## 14. Event-Driven Architecture

Define the role of Kafka or Redpanda.

Explain:

* domain events
* commands where appropriate
* event ownership
* producer/consumer boundaries
* durable asynchronous workflows
* outbox pattern
* retries
* dead letters
* replay
* ordering requirements
* idempotency

Do not define every event schema yet.

Architecture Volume 2 will establish detailed event contracts.

## 15. Background Job Architecture

Define the role of BullMQ or equivalent jobs.

Distinguish between:

* event-driven processing
* delayed jobs
* scheduled jobs
* retries
* operational jobs
* maintenance
* notifications
* exports
* reconciliation

Document worker isolation and scaling principles.

## 16. Data Architecture

Define the high-level data architecture.

Cover:

* PostgreSQL
* PostGIS
* Redis
* OpenSearch
* S3
* Kafka/Redpanda

For every major datastore explain:

* purpose
* authoritative versus derived status
* consistency expectations
* retention characteristics
* scale characteristics
* failure behavior

Define which system is authoritative for which categories of data.

## 17. Database Ownership

Create a clear data-ownership model.

For major entities identify:

* owning domain
* authoritative datastore
* primary identifier
* write ownership
* read access pattern
* derived copies

Avoid unrestricted cross-domain writes.

Do not permit one module to directly mutate another domain's authoritative data merely for convenience.

## 18. Caching Architecture

Define Redis responsibilities.

Include:

* cache
* ephemeral location
* presence
* rate limiting
* idempotency
* locks where justified
* short-lived operational state

Clearly distinguish:

* cache
* ephemeral state
* durable source of truth

Document behavior when Redis is unavailable.

## 19. Search Architecture

Define OpenSearch/Elasticsearch responsibilities.

Specify what data is indexed, such as:

* operational entities
* support cases
* fleet records
* geographic data where appropriate
* audit/searchable records
* reporting/search projections where required

Treat search as derived data.

Do not make search the authoritative system of record for transactional business state.

## 20. Object Storage Architecture

Define S3 responsibilities for:

* user files
* driver/vehicle verification documents
* safety evidence
* support attachments
* exports
* generated artifacts

Define high-level security boundaries.

Sensitive objects must remain private.

## 21. External Provider Architecture

Define provider abstraction boundaries for:

* payments
* maps
* routing
* geocoding
* notifications
* identity/verification
* fraud/risk

For each category document:

* abstraction boundary
* provider-specific adapter boundary
* timeout/failure concerns
* retry ownership
* fallback behavior
* data exchanged

Do not tightly couple domain models to provider-specific representations.

## 22. Security Architecture

Create the high-level security architecture.

Cover:

* authentication
* sessions
* authorization
* RBAC/permissions
* service identity
* workload identity
* secret management
* encryption
* network boundaries
* client security
* WebSocket security
* API security
* data protection
* auditability
* abuse prevention

Define security responsibilities at:

* client
* edge
* API
* domain
* data
* infrastructure

## 23. Privacy Architecture

Identify sensitive data categories including:

* identity
* contact information
* location
* payment-related data
* private messages
* safety information
* verification documents
* support information

Define high-level principles for:

* minimization
* access control
* retention
* deletion/anonymization boundaries
* audit
* regional handling
* derived-data treatment

Do not invent legal requirements.

## 24. Reliability Architecture

Define architectural reliability strategies for:

* service failure
* dependency failure
* network partitions
* Redis failure
* database failure
* event-broker failure
* external-provider failure
* regional failure
* stale realtime state
* duplicate events

Include:

* retries
* idempotency
* timeouts
* circuit-breaking boundaries
* graceful degradation
* recovery
* backpressure

Do not apply retries indiscriminately.

## 25. Consistency Model

Document where the platform requires:

* strong consistency
* transactional consistency
* optimistic concurrency
* eventual consistency
* asynchronous convergence

Explicitly identify critical consistency boundaries for:

* trip assignment
* trip state
* payment state
* financial ledger
* driver availability
* dispatch offers
* location freshness

## 26. Idempotency and Concurrency Strategy

At the architectural level, define where idempotency is required.

Cover operations such as:

* ride creation
* cancellation
* offer acceptance
* trip completion
* payment creation
* payment capture
* refund
* payout
* webhook handling
* event consumption
* job processing

Define concurrency-control principles without turning this volume into a detailed contract catalog.

## 27. API Architecture

Define the high-level API architecture.

Cover:

* REST
* versioning
* resource ownership
* authentication
* authorization
* pagination
* error model
* idempotency
* request tracing
* rate limiting

Architecture Volume 2 will specify the detailed API contract.

## 28. Frontend Architecture Boundary

Define how the web application communicates with backend systems.

Cover:

* API client boundary
* authentication/session management
* server/client responsibilities
* TanStack Query
* Zustand usage boundaries
* forms
* realtime
* maps
* caching
* error handling

Do not design every screen in this volume.

## 29. Mobile Architecture Boundary

Define the shared mobile architecture.

Cover:

* rider/driver application organization
* shared platform code
* navigation
* secure storage
* authentication
* API access
* realtime
* push notifications
* location
* background behavior
* connectivity/offline handling

Do not design every mobile screen in this volume.

## 30. Observability Architecture

Define:

* structured logging
* metrics
* traces
* correlation IDs
* domain observability
* infrastructure observability
* realtime observability
* event observability
* financial observability
* audit visibility

Explicitly identify data that must never appear in observability payloads.

## 31. Scale and Performance Architecture

Define high-level strategies for:

* horizontal scaling
* regional partitioning
* database scaling
* geospatial workload scaling
* Redis scaling
* event scaling
* WebSocket scaling
* search scaling
* worker scaling
* caching
* backpressure

Do not provide unsupported capacity numbers beyond the stated architectural targets.

## 32. Global and Multi-Region Architecture

Define:

* regional boundaries
* traffic routing
* data locality
* regional deployment
* cross-region dependencies
* failover
* disaster recovery
* regional health
* operational isolation

Explain which components are:

* region-local
* globally shared
* replicated
* asynchronously synchronized

Avoid creating unnecessary cross-region dependencies on critical request paths.

## 33. Environment Architecture

Define:

* local development
* test
* staging
* production
* disaster-recovery/secondary production environments where applicable

Explain configuration and secret separation.

Do not allow production data to leak into lower environments.

## 34. Architectural Risks

Create a documented architectural risk register.

Include risks such as:

* dispatch correctness
* location scale
* WebSocket scale
* database hotspots
* Redis memory pressure
* event backlog
* external-provider outages
* payment reconciliation
* regional failure
* privacy exposure
* operational complexity

For each risk provide:

* description
* impact
* likelihood category
* mitigation
* residual risk
* detection mechanism

Do not assign arbitrary numeric scores without a defined methodology.

## 35. Architectural Decision Records

Create ADRs for the most consequential decisions.

At minimum address decisions around:

* modular versus distributed service boundaries
* PostgreSQL ownership
* PostGIS usage
* Redis responsibilities
* Kafka/Redpanda role
* realtime WebSockets
* provider abstractions
* payment architecture
* global deployment
* event/outbox strategy
* observability architecture

Each ADR should include:

* context
* decision
* alternatives considered
* consequences

## 36. Architecture Diagrams

Create architecture diagrams appropriate to the repository's documentation conventions.

At minimum provide diagrams for:

* system context
* major runtime components
* domain boundaries
* primary rider trip flow
* driver availability/location flow
* dispatch flow
* payment flow
* event flow
* realtime flow
* deployment topology
* global/multi-region topology

Use maintainable diagram source formats such as Mermaid or another repository-supported format.

Do not rely only on rendered screenshots.

# ARCHITECTURAL INVARIANTS

The documentation must explicitly state invariants that later implementation prompts must preserve.

Examples include:

* Trip state has one authoritative owner.
* Financial ledger records are immutable.
* Payment-provider state and internal financial state are distinct.
* Current driver location is ephemeral operational state and is not the sole historical source of truth.
* Dispatch cannot assign one active driver to conflicting trips.
* Realtime delivery is not the source of transactional truth.
* Search indexes are derived.
* Redis is not the durable source of truth for transactional entities.
* External provider implementations are isolated behind adapters.
* Sensitive data is not emitted into ordinary logs or telemetry.
* Critical operations support idempotent execution.
* Domain ownership prevents arbitrary cross-domain writes.

The exact invariant set must reflect the final architecture.

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement production application code.

Do not implement:

* backend modules
* frontend screens
* mobile screens
* Terraform deployment
* Kubernetes manifests
* CI/CD workflows

Those belong to later implementation milestones.

Do not produce the complete detailed API specification.

Do not produce the complete event-schema catalog.

Do not create detailed Prisma schema files yet.

Do not create implementation-specific SQL migrations.

Do not invent specific cloud resource IDs.

Do not fabricate measured scalability results.

Do not create an unplanned Architecture Volume 3.

Do not create a surprise "final architecture" or "final integration" phase.

Do not introduce technologies outside the locked technology direction without a documented architectural necessity.

# REPOSITORY INSPECTION REQUIREMENTS

Before creating architecture artifacts:

1. Inspect the repository structure.
2. Identify existing source files.
3. Identify existing documentation.
4. Identify any existing architecture materials.
5. Identify existing infrastructure structure.
6. Identify current package/dependency configuration.
7. Identify any existing domain/module boundaries.
8. Identify existing database schema or migrations.
9. Identify current API conventions.
10. Identify existing event/realtime abstractions.
11. Identify existing configuration conventions.
12. Identify existing testing conventions.

Do not delete existing useful documentation.

Do not regenerate files unnecessarily.

If existing architectural artifacts are present, reconcile them with the project requirements instead of blindly replacing them.

# IMPLEMENTATION RULES

## Repository-First

The repository must be inspected before architectural decisions are finalized.

## Concrete Decisions

Avoid vague statements such as:

* "use scalable architecture"
* "ensure high availability"
* "secure the system appropriately"
* "use microservices as needed"

Every important architectural requirement must explain how it is achieved.

## No Unsupported Claims

Do not claim:

* production availability
* compliance
* capacity
* latency
* disaster recovery success
* fault tolerance validation

unless supported by evidence.

## Internal Consistency

Entity ownership, domain boundaries, diagrams, terminology, and architectural decisions must agree throughout all artifacts.

## Naming Consistency

Use the same canonical names for:

* domains
* major services
* entities
* stores
* events
* queues
* clients
* environments
* regions

Do not alternate between synonymous names for the same architectural concept.

## Documentation Quality

Documentation must be useful to engineers who will implement the system later.

Avoid marketing language.

Avoid vague architecture prose.

# VALIDATION REQUIREMENTS

After creating the architecture package:

1. Validate all documentation links.
2. Validate Mermaid or other diagram syntax where tooling is available.
3. Check for inconsistent terminology.
4. Check that every major domain has an identified owner.
5. Check that every major datastore has an explicit purpose.
6. Check that major external dependencies have architectural boundaries.
7. Check that critical flows are represented.
8. Check that architectural invariants are consistent with domain boundaries.
9. Check that the documented technology stack matches the project lock.
10. Check that no later implementation assumptions contradict the architecture.
11. Check that ADRs agree with the main architecture documents.
12. Check that architecture diagrams agree with written descriptions.

Do not merely check that files exist.

Review the architecture for internal contradictions.

# FINAL INTEGRATION CHECK

Before declaring Architecture Volume 1 complete, verify that:

1. The product scope is clearly defined.
2. The major domains are explicitly bounded.
3. Data ownership is explicit.
4. Major runtime components are identified.
5. Deployment topology is defined.
6. The trip lifecycle is architecturally coherent.
7. Driver availability and location architecture are coherent.
8. Dispatch ownership and correctness boundaries are explicit.
9. Pricing and payment responsibilities are separated.
10. Realtime is treated as distributed infrastructure rather than transactional truth.
11. Eventing and background jobs have distinct roles.
12. PostgreSQL/PostGIS, Redis, OpenSearch, S3, and Kafka/Redpanda have explicit responsibilities.
13. External providers are isolated behind abstractions.
14. Security and privacy boundaries are documented.
15. Reliability and degraded-mode principles are documented.
16. Consistency and concurrency expectations are explicit.
17. Web and mobile boundaries are defined.
18. Observability architecture is defined.
19. Multi-region architecture is defined.
20. Environment separation is defined.
21. Architectural risks are documented.
22. Important decisions have ADRs.
23. Required architecture diagrams exist and agree with the written architecture.
24. No implementation work has been prematurely introduced.
25. No unsupported claims have been made.
26. The architecture is detailed enough for the later implementation milestones to build against.
27. Nothing requires a nonexistent third architecture volume.

# DEFINITION OF DONE

Architecture Volume 1 is complete only when:

* the foundational architecture package exists
* domain boundaries are explicit
* ownership is explicit
* major runtime components are explicit
* deployment topology is explicit
* data architecture is explicit
* critical workflows are architecturally defined
* realtime architecture is defined
* dispatch architecture is defined
* pricing/payment architecture is defined
* security/privacy foundations are defined
* reliability foundations are defined
* observability foundations are defined
* global/multi-region architecture is defined
* architectural invariants are documented
* major risks are documented
* major ADRs exist
* architecture diagrams exist
* all artifacts are internally consistent
* documentation is implementation-oriented
* no major architectural dependency remains unexplained
* Volume 2 can deepen contracts without requiring this volume to be rewritten

# IMPLEMENTATION REPORT

At completion, provide a technically detailed report containing:

## Files Created

List every architecture file created.

## Files Modified

List every existing file modified.

## Architecture Decisions

Summarize the major architectural decisions established.

## Domain Boundaries

Summarize each major domain and its ownership.

## Data Ownership

Summarize authoritative stores and derived data boundaries.

## Runtime Architecture

Summarize major application, realtime, event, worker, and infrastructure components.

## Critical Flows

Summarize the major request, trip, dispatch, location, payment, event, and realtime flows documented.

## Diagrams

List the diagrams created and their source formats.

## ADRs

List the ADRs created.

## Validation Executed

List the actual validation commands or checks performed.

## Inconsistencies Found

Document any pre-existing repository/architecture contradictions discovered.

## Known Limitations

Document genuine architectural uncertainties or limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then create the complete Architecture Volume 1 documentation package.

Do not implement application code.

Do not create a third architecture volume.

Create concrete, internally consistent architectural artifacts that can serve as the source of truth for the later backend, frontend, mobile, and infrastructure milestones.

Do not leave required architecture as vague prose.

Do not invent unsupported technologies or measured capabilities.

Validate the complete documentation package before declaring the milestone complete.

Finish with the required implementation report and leave the repository with a coherent foundational architecture ready for Architecture Volume 2.
