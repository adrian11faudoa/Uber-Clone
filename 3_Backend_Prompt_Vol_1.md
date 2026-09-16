# UBER-STYLE RIDE-HAILING PLATFORM — BACKEND PROMPT — VOLUME 1

## ROLE

You are the senior backend engineering organization responsible for implementing the foundational backend platform for a production-grade ride-hailing and mobility marketplace comparable in product depth and operational sophistication to Uber.

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

You are not creating a tutorial, prototype, mock backend, or educational example.

Implement complete, connected, production-grade backend functionality using the project's established architecture, contracts, conventions, and technology direction.

The repository is the source of truth for what currently exists.

Do not assume that another AI prompt or previous conversation is available.

---

# PROJECT

Implement the foundational backend platform for an Uber-style ride-hailing system using:

* NestJS
* TypeScript
* PostgreSQL
* Prisma
* Redis
* BullMQ
* Kafka or compatible event streaming
* REST APIs
* WebSockets where required
* OpenAPI/Swagger
* OpenTelemetry-compatible observability

The backend must provide the durable foundation for:

* identity
* authentication
* authorization
* riders
* drivers
* driver onboarding
* compliance
* vehicles
* availability
* foundational geolocation
* ride requests
* trip lifecycle
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
* asynchronous processing
* events
* observability

This volume is responsible for establishing the backend application foundation, shared infrastructure, identity/security foundations, rider and driver domains, vehicle/compliance foundations, and the durable primitives required by later backend functionality.

Do not implement unrelated later-domain functionality merely because it is mentioned in the project scope.

---

# SOURCE OF TRUTH

Before changing code:

Inspect the repository comprehensively.

Determine:

* workspace/package structure
* backend application location
* NestJS modules
* Prisma schema
* existing migrations
* Redis integration
* BullMQ integration
* Kafka/event integration
* authentication implementation
* authorization implementation
* API conventions
* WebSocket implementation
* shared libraries
* error handling
* configuration
* logging
* observability
* testing
* CI/CD
* existing infrastructure
* existing frontend/mobile contracts

Preserve existing working behavior.

Reuse compatible infrastructure rather than creating parallel implementations.

Do not regenerate unchanged files.

Do not replace established repository patterns solely for stylistic preference.

If foundational backend functionality is missing, implement it completely.

If an existing implementation is insecure, incorrect, or incompatible with the project's architecture, correct it as part of the relevant scope and document the compatibility impact.

---

# BACKEND SCOPE

This prompt is responsible for implementing:

* NestJS backend foundation
* configuration architecture
* database integration
* Redis integration
* common request/error infrastructure
* authentication
* session/token lifecycle
* authorization
* user accounts
* rider profiles
* driver profiles
* driver onboarding state
* driver compliance foundations
* compliance evidence metadata
* vehicle management
* vehicle eligibility foundations
* driver availability foundations
* initial geolocation infrastructure contracts
* audit infrastructure
* foundational event infrastructure
* foundational queue infrastructure
* backend observability
* rate limiting foundations
* security middleware/guards
* automated tests for all implemented functionality

This prompt does not own the full dispatch engine, full ride-matching algorithm, complete payment orchestration, advanced pricing engine, full trip orchestration, or production infrastructure deployment unless the repository already places a required foundational component inside this scope.

Those later systems must consume the contracts established here rather than creating incompatible parallel foundations.

---

# ARCHITECTURAL RESPONSIBILITIES

The backend must enforce clear domain boundaries.

At minimum establish independent modules or equivalent boundaries for:

* Identity
* Authentication
* Authorization
* Users
* Riders
* Drivers
* Compliance
* Vehicles
* Availability
* Location
* Audit
* Infrastructure

The exact physical module structure must follow the repository where a compatible implementation already exists.

Do not create an artificial microservice topology solely for organizational purposes.

The immediate goal is a clean backend foundation that can scale into the complete distributed system without requiring uncontrolled rewrites.

---

# APPLICATION FOUNDATION

Establish or preserve a production NestJS application foundation including:

* application bootstrap
* environment configuration
* configuration validation
* module composition
* global validation
* global exception handling
* request correlation
* structured logging
* security middleware
* health/readiness architecture
* graceful shutdown
* dependency injection conventions
* API versioning where applicable
* OpenAPI integration
* test infrastructure

Global infrastructure must not hide domain logic.

---

# CONFIGURATION

Create a strongly typed configuration system.

Configuration must distinguish:

* application settings
* database settings
* Redis settings
* Kafka settings
* queue settings
* authentication settings
* token settings
* rate limits
* external provider configuration
* observability settings
* environment metadata

Validate configuration on application startup.

Invalid production-critical configuration must cause a controlled startup failure rather than allowing the service to start with unsafe defaults.

Do not hardcode:

* credentials
* API keys
* signing secrets
* database passwords
* provider secrets
* encryption keys

Provide safe local-development defaults only for non-secret infrastructure where appropriate.

---

# DATABASE FOUNDATION

Implement the PostgreSQL/Prisma persistence foundation.

Requirements:

* Prisma client integration
* controlled connection lifecycle
* transaction support
* safe shutdown
* migration integration
* database health checks
* query instrumentation
* consistent error mapping
* test database strategy

Configure the Prisma client to prevent uncontrolled connection growth.

Do not create a new database connection per request.

Support transaction boundaries explicitly in application services.

---

# DATABASE ENGINEERING

Create or evolve models for foundational entities as required by the repository architecture.

At minimum support durable data for:

* users
* authentication/session state where durable storage is required
* rider profiles
* driver profiles
* driver compliance state
* compliance evidence metadata
* vehicles
* vehicle eligibility
* availability state where durable representation is required
* audit records
* idempotency records where applicable

Use:

* primary keys
* foreign keys
* uniqueness constraints
* appropriate check constraints where Prisma/PostgreSQL support the required semantics
* indexes based on actual query patterns
* created/updated timestamps
* explicit state fields
* appropriate soft-delete/anonymization strategy

Do not introduce unrestricted JSON blobs where normalized fields are required for transactional behavior.

---

# USER IDENTITY MODEL

Implement a canonical user identity model.

A user must represent the authenticated account independently from product-specific role data.

Support appropriate attributes for:

* identity identifier
* email where applicable
* phone where applicable
* account status
* verification state
* locale
* timezone
* created timestamp
* updated timestamp
* deletion/anonymization state

Do not duplicate credentials into rider and driver tables.

The user identity must be reusable by:

* rider
* driver
* support
* operations
* administrator

while authorization determines actual privileges.

---

# ACCOUNT STATES

Implement explicit account security/availability states as required.

Examples may include:

* active
* pending verification
* restricted
* suspended
* disabled
* deleted/anonymized

Define legal transitions.

Sensitive administrative state changes must be auditable.

A disabled user must not be able to authenticate merely because an old access token remains technically valid.

---

# AUTHENTICATION

Implement secure authentication for the backend.

The implementation must support the credential mechanisms established by the repository and must provide a clean architecture for:

* registration
* login
* logout
* access-token issuance
* refresh
* revocation
* account recovery
* credential rotation
* session/device management where applicable

Use secure password hashing when passwords are part of the selected authentication method.

Never store plaintext passwords.

Never place secrets or raw credentials into logs.

---

# TOKEN ARCHITECTURE

If JWT-based authentication is used, implement a secure lifecycle for:

* short-lived access tokens
* protected refresh tokens
* token rotation where appropriate
* revocation
* replay detection where required
* issuer/audience validation
* expiration
* signing-key configuration

Do not trust decoded token claims without signature and validity verification.

Do not place unnecessary sensitive information into tokens.

The backend must enforce authorization independently of frontend/mobile claims.

---

# SESSION AND DEVICE SECURITY

Where session storage is used, establish a durable or controlled representation for:

* session identifier
* user
* device/client context
* issued time
* expiration
* revocation
* last-use metadata as appropriate

Support:

* logout from current session
* revocation of compromised sessions
* controlled session expiration

Do not create unbounded session records without retention policies.

---

# ACCOUNT RECOVERY

Implement secure account recovery architecture.

Requirements include:

* expiring recovery tokens
* one-time use
* secure token storage or hashing
* rate limiting
* generic user-facing responses where enumeration would be harmful
* auditability
* session invalidation after sensitive credential reset where appropriate

Do not expose whether an arbitrary email or phone belongs to an account unless product requirements explicitly justify it.

---

# AUTHORIZATION MODEL

Implement server-side authorization foundations.

Support role and permission concepts appropriate to:

* rider
* driver
* support
* operations
* administrator
* internal service

Authorization must include resource ownership.

Examples:

* rider access must be limited to the rider's own resources
* driver access must be limited to the driver's own resources and explicitly assigned resources
* support access must require appropriate case/operational permission
* administrative privileges must be explicit

Do not implement a single uncontrolled `isAdmin` boolean as the complete authorization system.

---

# AUTHORIZATION GUARDS

Create reusable authorization mechanisms for NestJS such as:

* authentication guards
* role/permission guards
* resource ownership checks
* service-level authorization helpers

Controller guards alone are insufficient when business logic can be invoked through other application pathways.

Critical authorization decisions must also exist inside appropriate application services/domain boundaries.

---

# USER ENUMERATION PROTECTION

Protect authentication and recovery flows against account enumeration.

Responses must not unnecessarily disclose whether:

* an email exists
* a phone exists
* an account is disabled
* a driver exists

when the operation does not require that disclosure.

Internal logs may contain controlled diagnostic context subject to privacy rules.

---

# RATE LIMITING FOUNDATION

Implement reusable Redis-backed rate limiting for security-sensitive APIs.

At minimum support limits for:

* registration
* login
* password reset
* verification attempts
* token refresh
* sensitive profile mutations
* administrative authentication

The rate-limit implementation must define:

* key strategy
* TTL
* maximum attempts
* response behavior
* identity/IP combination where appropriate
* Redis failure behavior

Do not disable rate limits silently because Redis is unavailable.

Where Redis is unavailable, choose an explicit safe failure/degradation strategy suitable to the operation.

---

# REQUEST CORRELATION

Every HTTP request should have a correlation/request identifier.

Implement middleware/interceptors that:

* accept a validated client request ID where safe
* otherwise generate one
* propagate it through application logging
* attach it to responses
* integrate it with tracing
* propagate it to relevant asynchronous jobs/events

Do not trust arbitrary trace identifiers without validation.

---

# ERROR MODEL

Create a consistent backend error model.

Errors must distinguish appropriate categories such as:

* validation
* authentication
* authorization
* not found
* conflict
* business rule violation
* rate limiting
* dependency failure
* timeout
* internal error

Responses must not leak:

* stack traces
* SQL statements
* internal hostnames
* secrets
* provider credentials
* sensitive personal information

Map lower-level errors to stable API semantics.

---

# VALIDATION

Use server-side validation for all external input.

Validate:

* request bodies
* query parameters
* path parameters
* headers where business-critical
* pagination
* identifiers
* dates
* timezones
* coordinates
* uploaded metadata where applicable

Reject unexpected fields where strict validation is appropriate.

Do not depend on frontend validation for security.

---

# PAGINATION

Establish consistent pagination utilities.

For potentially large collections, prefer cursor-based pagination when appropriate.

Prevent:

* unbounded result sets
* unrestricted sort fields
* arbitrary database expressions
* expensive unrestricted offset queries on high-volume tables

Allow only approved sortable/filterable fields.

---

# USERS MODULE

Implement the user domain foundation.

Required capabilities include:

* retrieving the authenticated user
* profile retrieval
* safe account updates
* account status inspection
* controlled account deletion/deactivation
* privacy-conscious output mapping

Do not return internal fields or security metadata unnecessarily.

Separate internal persistence entities from public response DTOs.

---

# RIDER DOMAIN

Implement the rider profile foundation.

Support:

* rider profile creation
* profile retrieval
* profile update
* preferences where appropriate
* locale/timezone
* accessibility preferences where relevant
* notification preferences where appropriate

Rider profile data must remain separate from:

* authentication credentials
* ride state
* payment state
* driver state

Do not allow rider profile updates to mutate unrelated domains.

---

# DRIVER DOMAIN

Implement the driver profile foundation.

Support:

* driver creation
* driver profile retrieval
* profile update
* driver operational status
* regional information
* eligibility relationship
* account restrictions

A driver profile must not automatically imply:

* compliance approval
* vehicle eligibility
* dispatch eligibility
* online availability

These are separate concepts.

---

# DRIVER ONBOARDING

Implement explicit onboarding state.

The backend must support workflow stages appropriate to the repository and project architecture.

Examples:

* started
* information_required
* submitted
* under_review
* approved
* rejected
* suspended

Separate onboarding progress from final operational eligibility.

State changes must validate:

* authorized actor
* current state
* required information
* transition rules

---

# COMPLIANCE DOMAIN

Implement foundational compliance models and service boundaries.

Support metadata for:

* requirement type
* jurisdiction/market
* document/evidence type
* submission status
* verification status
* expiration
* reviewer or provider reference where appropriate
* rejection reason
* timestamps

Do not store sensitive document binary content directly in PostgreSQL when object storage is more appropriate.

Persist metadata and secure object references.

---

# COMPLIANCE STATE

Compliance must have explicit state.

Example conceptual states:

* not_started
* required
* submitted
* under_review
* approved
* rejected
* expired
* suspended

The exact repository conventions may differ, but state transitions must be explicit and auditable.

Do not encode compliance with uncontrolled booleans such as:

`isVerified = true`

without preserving the underlying workflow state and evidence context.

---

# COMPLIANCE AUTHORIZATION

Only authorized actors may:

* submit compliance evidence
* review evidence
* approve
* reject
* suspend
* reinstate

Driver self-service actions must never be able to set final approval states.

Administrative changes must generate audit records.

---

# VEHICLE DOMAIN

Implement vehicle management.

Support:

* vehicle creation
* vehicle retrieval
* vehicle update
* vehicle activation/deactivation
* driver association where appropriate
* ride-category metadata
* market eligibility metadata
* compliance relationships

Prevent unauthorized users from accessing another driver's vehicles.

Enforce ownership at the application/domain boundary.

---

# VEHICLE ELIGIBILITY

Separate vehicle existence from vehicle eligibility.

Eligibility may depend on:

* vehicle type
* model/year rules
* jurisdiction
* compliance documents
* active state
* driver relationship

Create an explicit service boundary for eligibility decisions so dispatch can later consume it without embedding vehicle rules into dispatch logic.

---

# DRIVER-VEHICLE RELATIONSHIP

Define whether:

* one driver may own multiple vehicles
* one vehicle may be assigned to one driver at a time
* temporary vehicle assignments are supported

The implementation must enforce the repository's selected invariant at the database level where practical.

Do not allow concurrent application requests to produce impossible relationships.

---

# DRIVER AVAILABILITY FOUNDATION

Implement the durable model and service boundary needed for driver operational availability.

Support state concepts such as:

* offline
* available
* unavailable
* restricted
* on_trip

The exact active-trip state may remain owned by the future trip domain, but the availability abstraction must be designed so later dispatch and trip functionality can integrate without redesigning it.

Do not treat a simple `online = true` flag as sufficient for the complete driver state.

---

# LOCATION FOUNDATION

Implement the foundational location boundary without building the complete dispatch system.

At minimum define and validate:

* latitude
* longitude
* location timestamp
* driver identity
* source/device context where required
* coordinate validity
* timestamp sanity
* location freshness representation

Create an internal contract that future dispatch/location services can consume.

Do not synchronously persist every high-frequency driver coordinate into PostgreSQL merely because the database exists.

Design the abstraction for high-frequency ephemeral location.

---

# LOCATION SECURITY

Location submission must verify:

* authenticated driver
* ownership of the location identity
* valid coordinate ranges
* reasonable timestamp
* rate limits
* active session/device where required

Reject:

* NaN coordinates
* out-of-range latitude/longitude
* impossible timestamps
* malformed identifiers

Do not accept an arbitrary driver ID supplied by the client as proof of identity.

---

# AUDIT INFRASTRUCTURE

Implement reusable audit infrastructure for security-sensitive and operationally significant actions.

Audit records should include:

* actor
* actor type
* action
* target type
* target ID
* timestamp
* request/correlation ID
* result
* reason where required
* structured metadata where safe

Do not place sensitive credentials or private document contents into audit records.

Audit storage must be protected by authorization.

---

# EVENT INFRASTRUCTURE

Implement foundational event infrastructure for the backend.

Create a consistent event envelope containing appropriate fields such as:

* event ID
* event type
* event version
* entity/aggregate ID
* producer
* timestamp
* correlation ID
* trace ID where appropriate
* payload

Do not publish arbitrary ORM entities directly as event payloads.

Events must be explicit contracts.

---

# EVENT VERSIONING

Every event contract must include a version.

The implementation must support additive evolution.

Consumers must not depend on undocumented field ordering or ORM serialization.

Do not publish database-specific internal structures that make schema evolution impossible.

---

# OUTBOX FOUNDATION

Where the repository architecture uses transactional outbox, implement the foundational persistence and publishing abstraction required for reliable event delivery.

The outbox design must support:

* event ID
* type
* version
* aggregate/entity ID
* serialized payload
* creation time
* publishing state where appropriate
* retry metadata
* error metadata where safe

The outbox write must participate in the same database transaction as the state change that requires the event.

Do not implement an unreliable pattern that commits PostgreSQL and Kafka independently without recovery semantics.

---

# QUEUE FOUNDATION

Implement BullMQ infrastructure that supports:

* named queues
* typed job payloads
* worker registration
* retry configuration
* exponential backoff
* timeout
* concurrency configuration
* graceful worker shutdown
* structured job logging
* job correlation
* failure reporting

Do not create a single unbounded queue for every background task.

Foundational queue infrastructure must allow later domains to define isolated workload classes.

---

# QUEUE IDEMPOTENCY

Create utilities/patterns that allow later job implementations to safely achieve idempotency.

Where possible support:

* deterministic job IDs
* deduplication
* attempt tracking
* safe retry
* result recording where required

Do not claim that BullMQ's built-in retry behavior automatically makes a business operation idempotent.

Business operations must remain responsible for preventing duplicate effects.

---

# REDIS FOUNDATION

Implement a reusable Redis integration.

Provide:

* connection management
* health monitoring
* namespacing
* structured key builders where appropriate
* TTL helpers
* safe serialization
* error handling
* graceful shutdown

Do not scatter raw Redis connection handling across domain modules.

---

# REDIS FAILURE BEHAVIOR

Redis must not become a hidden single point of failure for durable operations.

Where Redis supports:

* rate limiting
* cache
* ephemeral presence
* future location state

define explicit failure behavior.

Critical durable user/account operations must continue using PostgreSQL as the authority.

Do not convert temporary Redis failures into data corruption.

---

# CACHING FOUNDATION

Create cache utilities only where repository requirements justify them.

Every cache should define:

* key
* TTL
* owner
* serialization format
* invalidation
* stale behavior
* fallback to authoritative storage

Do not introduce caching for every repository read automatically.

Avoid caching highly mutable security state without carefully defined invalidation.

---

# DATABASE TRANSACTION UTILITIES

Provide an application-level transaction mechanism that allows domain services to execute atomic database operations where appropriate.

Transactions must remain bounded and avoid:

* external network calls inside long-lived transactions
* unbounded loops
* queue waits
* user interaction
* provider API calls

External side effects should use appropriate outbox/event/job patterns.

---

# DISTRIBUTED CONCURRENCY FOUNDATIONS

Provide reusable mechanisms for:

* optimistic concurrency
* unique constraints
* state-version checking
* idempotency
* conflict detection

Do not introduce distributed locking abstractions without an actual business need.

Where locks are necessary, document:

* key
* TTL
* ownership
* release behavior
* failure mode

Never rely solely on Redis locks to enforce database invariants.

---

# HEALTH AND READINESS

Implement health/readiness endpoints appropriate to the backend architecture.

Distinguish:

* process liveness
* application readiness
* critical dependency readiness

Do not cause a temporary optional dependency failure to make the entire platform appear dead unless that dependency is genuinely required for safe startup/operation.

Health endpoints must not leak credentials or internal infrastructure information.

---

# GRACEFUL SHUTDOWN

Implement graceful application shutdown.

The application must:

* stop accepting new work
* complete or safely terminate in-flight requests
* disconnect WebSockets where applicable
* stop background workers
* finish safe queue acknowledgements
* flush telemetry where appropriate
* close database connections
* close Redis connections
* close Kafka connections

Do not terminate workers while claiming their jobs were successfully processed.

---

# API DOCUMENTATION

Integrate OpenAPI/Swagger consistently.

Document:

* authentication
* request/response schemas
* validation
* errors
* pagination
* idempotency
* major rider/driver endpoints

Do not expose internal admin endpoints publicly without appropriate documentation and authorization.

API documentation must reflect actual implementation.

---

# SECURITY HEADERS AND HTTP HARDENING

Apply appropriate HTTP protections including, where applicable:

* secure headers
* CORS policy
* request size limits
* content-type validation
* trusted proxy configuration
* transport security assumptions

CORS must not use insecure wildcard configurations for credentialed production APIs.

---

# CORS

Define explicit origin configuration.

Support environment-specific allowed origins.

Do not use:

* `*` with credentialed requests
* unrestricted arbitrary origins

unless a specific endpoint is intentionally public and does not use credentials.

---

# CSRF CONSIDERATIONS

Choose the CSRF posture based on the authentication mechanism.

If cookies are used for authenticated browser requests, implement appropriate CSRF protection.

If bearer-token authentication is used and tokens are not automatically attached by the browser, document the different threat model and still protect all browser-sensitive operations appropriately.

Do not claim CSRF is irrelevant without considering the actual transport mechanism.

---

# SECURITY-SENSITIVE LOGGING

Implement structured logs while enforcing redaction.

Never log:

* passwords
* access tokens
* refresh tokens
* session secrets
* payment credentials
* raw compliance documents
* private keys
* provider secrets

Avoid unnecessarily logging:

* exact rider location
* exact driver historical location
* sensitive identity information

Provide centralized redaction utilities where practical.

---

# OBSERVABILITY FOUNDATION

Integrate OpenTelemetry-compatible tracing and metrics.

Instrument:

* HTTP requests
* database calls
* Redis calls
* queue jobs
* Kafka producers/consumers where present
* authentication operations
* important domain commands

Every trace should preserve:

* request/correlation ID
* trace ID
* operation name
* relevant safe entity identifiers

---

# BUSINESS METRICS FOUNDATION

Create reusable metrics infrastructure for later domains.

Foundational metrics should support:

* request count
* request latency
* error rate
* authentication failures
* authorization failures
* rate-limit events
* database latency
* Redis latency
* queue depth
* job failures
* event publishing failures

Avoid creating meaningless metrics for every method.

Metrics should support real operational decisions.

---

# SECURITY AUDIT EVENTS

Emit audit events for operations such as:

* login
* logout where appropriate
* credential changes
* account recovery
* role/permission changes
* driver compliance review
* driver suspension
* vehicle eligibility change
* administrative profile modification

Do not create audit records for every insignificant read.

Focus on security-sensitive and materially consequential actions.

---

# PRIVACY CONTROLS

Implement foundational privacy rules.

At minimum:

* limit user data returned in DTOs
* avoid exposing internal identifiers unnecessarily
* restrict exact location access
* protect compliance metadata
* support account deactivation/deletion architecture
* prevent unauthorized historical-data access

Do not allow an authenticated user to query another user's data by changing a URL parameter.

Every resource query must perform appropriate ownership/permission checks.

---

# DATA DELETION FOUNDATION

Design account deletion/anonymization service boundaries.

Distinguish between:

* data that may be deleted
* data that must be retained for financial/legal reasons
* data requiring anonymization
* derived/cache data
* asynchronous deletion tasks

Do not physically delete financial/audit records simply because a user requested account deletion if retention is required.

---

# TESTING REQUIREMENTS

Write automated tests for every implemented backend capability.

At minimum cover:

## AUTHENTICATION

* registration
* successful login
* invalid credentials
* disabled accounts
* expired tokens
* refresh rotation/revocation
* logout
* recovery
* rate limiting

## AUTHORIZATION

* correct-role access
* incorrect-role access
* resource ownership
* administrative permissions
* suspended-account behavior

## RIDERS

* profile creation
* retrieval
* update
* unauthorized access
* validation failures

## DRIVERS

* profile creation
* retrieval
* update
* unauthorized access
* state validation

## COMPLIANCE

* onboarding transitions
* evidence submission
* review authorization
* invalid transitions
* expiration state

## VEHICLES

* creation
* update
* ownership
* eligibility
* concurrent relationship constraints

## AVAILABILITY

* state changes
* authorization
* invalid transitions
* consistency with driver restrictions

## LOCATION

* coordinate validation
* timestamp validation
* ownership
* rate limiting
* malformed input

## AUDIT

* required actions produce audit records
* unauthorized actors cannot create privileged audit events
* sensitive data is redacted

## INFRASTRUCTURE

* Redis failure behavior
* database connection failure handling
* queue startup/shutdown
* event envelope validation

Tests must exercise real repository behavior rather than mock every dependency.

---

# INTEGRATION TESTING

Add integration tests that validate:

* PostgreSQL persistence
* Prisma transactions
* unique constraints
* authorization against real persisted data
* Redis-backed security controls
* queue registration
* event publishing where infrastructure is available

Use realistic test environments.

Do not disable database constraints merely to simplify tests.

---

# MIGRATION TESTING

Every schema change must be validated.

Verify:

* migration applies cleanly
* schema matches Prisma expectations
* indexes exist
* constraints exist
* fresh database initialization works
* existing-data migration behavior is safe where relevant

Do not manually edit production data as a substitute for migration design.

---

# API CONTRACT TESTING

Verify:

* validation
* response schemas
* errors
* authentication
* authorization
* pagination
* resource ownership

Where OpenAPI is used, ensure documented behavior reflects actual runtime behavior.

---

# BACKWARD COMPATIBILITY

Inspect current repository consumers before changing:

* endpoints
* request structures
* response structures
* authentication behavior
* database fields
* event names
* queue payloads

Prefer additive migration.

If a breaking change is required, document:

* affected consumers
* migration path
* compatibility strategy
* removal conditions

Do not break mobile clients casually because they may remain on older versions after backend deployment.

---

# PERFORMANCE

Benchmark or reason explicitly about:

* authentication lookup
* authorization lookup
* user retrieval
* driver retrieval
* vehicle retrieval
* compliance lookup
* location-write handling
* Redis operations
* database connection usage

Prevent:

* N+1 queries
* unbounded list queries
* repeated expensive permission lookups
* unnecessary serialization
* excessive database transactions
* per-request initialization of infrastructure clients

---

# SECURITY REVIEW

Before declaring the implementation complete, review for:

* IDOR
* authentication bypass
* authorization bypass
* privilege escalation
* user enumeration
* brute-force vulnerability
* token leakage
* session replay
* insecure password handling
* SQL injection through raw queries
* unsafe deserialization
* mass assignment
* insecure file references
* sensitive logging
* CORS errors
* CSRF exposure where relevant
* SSRF exposure through future integration boundaries

Fix actual issues discovered during implementation.

Do not leave known critical security defects unresolved while declaring the foundational backend complete.

---

# IMPLEMENTATION DISCIPLINE

Before modifying files:

1. Inspect the repository.
2. Identify existing compatible implementation.
3. Identify the exact scope of this prompt.
4. Preserve working functionality.
5. Implement the foundational backend capabilities completely.
6. Integrate all modules into the actual NestJS application.
7. Create or update Prisma migrations.
8. Add tests.
9. Add observability.
10. Add security controls.
11. Validate APIs.
12. Validate database operations.
13. Validate application startup and shutdown.
14. Run linting/formatting.
15. Run type checking.
16. Run relevant automated tests.
17. Validate migrations.
18. Review compatibility.
19. Update documentation.
20. Produce the required implementation report.

Do not rewrite the entire repository.

---

# PRODUCTION COMPLETENESS

A module is not complete merely because its controller exists.

Every implemented backend capability must include, where applicable:

* DTOs
* validation
* service/application logic
* domain rules
* persistence
* database constraints
* authorization
* error handling
* observability
* tests
* documentation
* integration into module composition

Do not leave routes connected to placeholders.

Do not return hardcoded data.

Do not create fake provider integrations.

Do not leave TODO/FIXME implementation gaps.

Do not use comments such as:

* "implement later"
* "similar to above"
* "omitted for brevity"

as substitutes for implementation.

---

# PROHIBITED PRACTICES

Never:

* hardcode credentials
* hardcode JWT secrets
* trust client role claims without server verification
* trust client driver IDs
* trust client ownership claims
* store plaintext passwords
* place access tokens in logs
* use Redis as the only source of durable identity data
* implement privileged operations only in controllers without service authorization
* allow unrestricted account queries
* accept arbitrary database sort/filter expressions
* perform unbounded database reads
* use distributed locks as the only business invariant protection
* treat queue retries as idempotency
* publish raw ORM entities as durable public events
* bypass database constraints because application validation exists
* silently swallow provider/infrastructure failures
* disable tests to achieve a passing build
* create duplicate identity systems

---

# IMPLEMENTATION BOUNDARIES

This prompt establishes the production backend foundation.

Implement only the scope defined in this document and necessary integration work.

Do not implement the entire Uber-style marketplace in one backend pass.

Do not build a second parallel architecture.

Do not redesign future dispatch, payment, or pricing systems prematurely.

Instead, create stable foundations that those future domains can consume through explicit interfaces and contracts.

---

# REQUIRED IMPLEMENTATION DELIVERABLES

Implement or update the repository with the appropriate backend components for:

## APPLICATION FOUNDATION

* NestJS bootstrap
* configuration
* validation
* exception handling
* request correlation
* health/readiness
* graceful shutdown
* API documentation

## IDENTITY

* user model
* authentication
* sessions/tokens where applicable
* account states
* recovery mechanisms
* rate limits

## AUTHORIZATION

* roles
* permissions
* authentication guards
* authorization guards
* ownership enforcement

## RIDER

* rider profile
* profile APIs
* validation
* authorization

## DRIVER

* driver profile
* driver state foundations
* profile APIs
* authorization

## COMPLIANCE

* onboarding state
* compliance state
* evidence metadata
* authorized review actions
* auditability

## VEHICLES

* vehicle model
* CRUD operations
* ownership
* eligibility foundation
* concurrency constraints

## AVAILABILITY

* state model
* transition service
* authorization
* persistence as required

## LOCATION

* validation
* authenticated driver association
* rate limiting
* high-frequency ingestion contract
* freshness representation

## PLATFORM INFRASTRUCTURE

* PostgreSQL/Prisma
* Redis
* BullMQ
* event envelope
* outbox foundation where appropriate
* OpenTelemetry
* structured logging
* metrics

## SECURITY

* hardened HTTP
* secure authentication
* authorization
* rate limiting
* sensitive-data redaction
* audit

---

# REQUIRED API SURFACES

Implement the appropriate authenticated API boundaries for the foundational domains.

At minimum, support concepts equivalent to:

* authentication
* current user
* rider profile
* driver profile
* driver onboarding/compliance
* vehicles
* availability
* driver location submission

Exact routes, versioning, and naming must follow repository conventions.

Do not invent duplicate route families where compatible ones already exist.

Every endpoint must define:

* authentication requirement
* authorization requirement
* request validation
* response DTO
* error semantics
* observability
* tests

---

# DATABASE VALIDATION

After implementation:

* apply migrations in a clean database
* validate Prisma schema
* validate indexes
* validate uniqueness
* validate foreign keys
* verify transaction behavior
* test account and ownership constraints
* test driver/vehicle relationship rules
* test state-transition constraints where implemented

Do not claim database readiness if migrations are not reproducible.

---

# RUNTIME VALIDATION

Verify:

* application startup
* configuration loading
* database connectivity
* Redis connectivity
* queue initialization
* health endpoints
* graceful shutdown
* authentication flows
* authorization flows
* rider APIs
* driver APIs
* compliance flows
* vehicle flows
* availability flows
* location validation

Use actual repository commands and environments.

Do not report tests as passed if they were not executed.

---

# DOCUMENTATION

Update repository documentation for:

* backend setup
* required environment variables
* authentication flow
* database migrations
* Redis requirements
* queue requirements
* local development
* API documentation
* security-sensitive operational settings
* testing commands

Documentation must describe the actual implemented system.

Never document nonexistent behavior.

---

# COMPLETION REPORT REQUIREMENTS

When implementation is complete, report:

## FILES CREATED

List every new file.

## FILES MODIFIED

List every modified file.

## MAJOR FUNCTIONALITY

Describe the completed backend foundation.

## DATABASE CHANGES

Report:

* Prisma schema changes
* migrations
* constraints
* indexes
* relationship changes

## API CHANGES

Report:

* authentication endpoints
* user endpoints
* rider endpoints
* driver endpoints
* compliance endpoints
* vehicle endpoints
* availability endpoints
* location endpoints
* other affected endpoints

## EVENT CHANGES

Report:

* event infrastructure
* event envelopes
* event types
* outbox changes

## QUEUE CHANGES

Report:

* queue infrastructure
* worker changes
* retry configuration
* graceful shutdown

## INFRASTRUCTURE CHANGES

Report:

* Redis
* PostgreSQL
* observability
* configuration
* environment changes

## SECURITY CHANGES

Report:

* authentication
* authorization
* rate limiting
* token/session security
* redaction
* audit logging

## OBSERVABILITY CHANGES

Report:

* logs
* metrics
* traces
* health checks
* correlation IDs

## TESTS

List tests added or changed and the behavior they verify.

## VALIDATION

Report:

* formatting
* linting
* type checking
* builds
* migrations
* unit tests
* integration tests
* API tests
* runtime verification

## COMPATIBILITY

Identify:

* existing consumers affected
* API compatibility considerations
* database compatibility
* mobile/web implications
* migration considerations

## UNRESOLVED ISSUES

List only genuine remaining issues.

Do not claim completion if required foundational functionality is missing or unverified.

---

# FINAL ENGINEERING PRINCIPLE

The backend foundation must become the trusted execution layer for the complete ride-hailing platform.

Authentication, authorization, user identity, rider state, driver state, compliance, vehicles, availability, location, persistence, events, queues, security, and observability must be implemented as real production functionality with explicit ownership and stable contracts.

Prioritize:

* correctness
* secure authorization
* durable persistence
* concurrency safety
* idempotency
* observability
* privacy
* maintainability
* scalability
* compatibility

The repository remains the implementation source of truth.

Every implementation decision must preserve the ability for later ride, dispatch, pricing, payment, notification, safety, and administrative backend capabilities to integrate cleanly without creating conflicting sources of truth or requiring an unnecessary rewrite.
