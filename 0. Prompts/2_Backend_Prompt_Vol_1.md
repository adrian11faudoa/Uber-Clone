# Uber-Style Global Ride-Hailing & Mobility Platform — Backend Prompt — Volume 1

## ROLE

You are the senior backend engineering organization responsible for implementing the foundational backend platform for an original, production-grade global ride-hailing and mobility system.

Operate simultaneously as:

* Principal Software Architect
* Staff Backend Engineer
* Distributed Systems Engineer
* Database Architect
* Security Engineer
* Performance Engineer
* Reliability Engineer
* Platform Engineer
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

Every required file must contain real implementation.

# PROJECT

## Project Identity

Build an original global ride-hailing and mobility backend supporting:

* riders
* drivers
* operations
* support
* safety
* fleet
* administrators

The platform is architected for targets such as:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* 100,000+ concurrent realtime sessions and higher during peak
* high-frequency driver location ingestion
* multi-region production operation
* high-volume asynchronous processing

These are architectural targets, not claims that this implementation has already demonstrated those capacities.

## Technology Direction

Implement the backend using the locked project stack:

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

* OpenSearch or Elasticsearch-compatible architecture where already required by the architecture

### Object Storage

* Amazon S3

### Realtime

* authenticated WebSockets

### Payments

* internal payment abstraction with a Stripe-compatible provider boundary

### Maps and Routing

* provider abstraction

### Observability

* OpenTelemetry
* Prometheus-compatible metrics
* structured logs compatible with Loki
* traces compatible with Tempo

# SOURCE OF TRUTH

The repository is the implementation source of truth.

Inspect the repository before making any change.

Architecture Volume 1 and Architecture Volume 2 define the project's architectural and contractual direction.

Use them as repository artifacts when available, but do not depend on the previous AI conversation.

If the repository already contains implementation work, preserve it and extend it.

If repository code conflicts with the architectural artifacts:

1. inspect the existing implementation
2. determine whether the conflict is intentional or accidental
3. preserve working behavior where possible
4. make the smallest coherent change necessary
5. document material discrepancies in the implementation report

Do not blindly regenerate existing files.

# BACKEND EXECUTION MODEL

This milestone establishes the reusable backend platform foundation.

Implement the infrastructure required by later business domains without implementing those domains yet.

This milestone owns:

* NestJS application foundation
* configuration
* environment validation
* API infrastructure
* request context
* errors
* security middleware/guards/interceptors
* PostgreSQL integration
* Prisma integration
* Redis integration
* cache foundations
* rate limiting foundations
* idempotency infrastructure
* transaction boundaries/helpers
* outbox foundations
* event publishing foundations
* event-consumer foundations
* background-job foundations
* health/readiness
* audit foundations
* OpenAPI
* telemetry
* testing infrastructure
* developer-facing backend documentation

Do not implement rider, driver, trip, dispatch, pricing, payment, messaging, safety, fleet, or analytics business logic in this milestone.

# CURRENT IMPLEMENTATION SCOPE

## 1. Repository Inspection and Backend Structure

Before implementation:

* inspect the repository
* inspect existing backend directories
* inspect package configuration
* inspect TypeScript configuration
* inspect lint and formatting configuration
* inspect test configuration
* inspect environment configuration
* inspect architecture documentation
* inspect database configuration
* inspect existing infrastructure integration points

Determine the correct backend application structure.

Prefer a modular structure that can later contain the established domains without requiring a structural rewrite.

Do not create an unnecessarily distributed set of applications if the current architecture is a modular NestJS backend.

## 2. NestJS Application Bootstrap

Create or complete the backend application bootstrap.

Implement:

* NestJS application initialization
* global configuration initialization
* global validation
* global exception handling
* request-context initialization
* OpenAPI bootstrap where appropriate
* security middleware
* graceful shutdown
* process-level error handling

Bootstrap code must be deterministic.

Do not hide initialization failures.

If a critical dependency fails to initialize, behavior must match the architecture's startup/readiness contract.

## 3. Application Configuration

Implement centralized configuration loading.

Separate:

* environment configuration
* runtime configuration
* secrets
* non-secret defaults

Configuration must be:

* typed
* validated
* explicit
* environment-aware

Validate required configuration at startup.

Reject invalid values such as:

* malformed URLs
* invalid ports
* invalid booleans
* unsupported environment names
* invalid durations
* malformed database configuration
* malformed Redis configuration
* malformed event-broker configuration

Do not silently fall back to unsafe values.

## 4. Environment Validation

Create a strongly typed environment/configuration schema.

Support required environments such as:

* local
* test
* staging
* production

Do not hard-code production credentials.

Do not log secret values during validation.

Validation errors must identify the invalid configuration key without exposing sensitive values.

## 5. Request Context

Implement a canonical request context.

The context should support, where appropriate:

* request ID
* correlation ID
* authenticated principal
* actor type
* tenant/region context if required by the architecture
* locale where appropriate
* start timestamp
* trace/span linkage

Define how the context is propagated into:

* logs
* database operations where useful
* events
* jobs
* outbound provider calls
* audit records

Do not use mutable global process state for request-specific information.

## 6. Request and Correlation IDs

Implement the architecture's canonical identifier behavior.

Support:

* client-supplied request ID only within validated rules where allowed
* server-generated request IDs
* correlation IDs
* propagation to downstream operations

Ensure IDs are available in error responses where contractually appropriate.

Do not trust arbitrary client-supplied identifiers as authenticated identities.

## 7. Global Validation

Implement consistent request validation.

Support:

* body validation
* query validation
* path-parameter validation
* type transformation where appropriate
* strict unknown-field handling according to the contract

Use the repository's established Zod/class-validator strategy consistently.

Do not create multiple competing validation frameworks.

Validation must prevent unsafe values from reaching business logic.

## 8. Error Handling

Implement the canonical error infrastructure from Architecture Volume 2.

Support:

* stable application error codes
* HTTP status mapping
* safe messages
* structured details
* request/correlation IDs
* retryability metadata where applicable
* field-level validation errors
* domain errors
* infrastructure errors
* provider errors

Do not expose:

* stack traces
* SQL statements
* internal hostnames
* secrets
* provider credentials
* Redis internals
* Kafka internals

Detailed internal error information must remain in appropriately protected logs.

## 9. Exception Mapping

Create consistent translation between:

* validation failures
* authentication failures
* authorization failures
* not-found conditions
* conflict conditions
* rate-limit failures
* database failures
* Redis failures
* event infrastructure failures
* unexpected exceptions

Do not convert every failure to HTTP 500.

Do not expose infrastructure failure details to clients.

## 10. Logging Foundation

Implement structured application logging.

The logging system must support:

* timestamp
* level
* service/application identity
* environment
* region where known
* request ID
* correlation ID
* trace ID
* actor metadata only where safe
* event/error code
* duration where useful

Implement appropriate redaction.

Never log:

* access tokens
* refresh tokens
* passwords
* payment credentials
* sensitive document contents
* private message contents
* secrets
* full authorization headers

Avoid high-cardinality or unnecessary sensitive log fields.

## 11. OpenTelemetry Foundation

Integrate the backend with OpenTelemetry.

Instrument:

* inbound HTTP requests
* database operations where appropriate
* Redis operations where appropriate
* outbound provider calls
* event publication
* event consumption
* background jobs
* important internal operations

Preserve trace/context propagation across:

* HTTP
* events
* jobs
* WebSockets where supported

Do not insert sensitive payloads into spans.

Avoid unbounded span attributes.

## 12. Metrics Foundation

Expose application metrics suitable for Prometheus-compatible collection.

At minimum provide infrastructure for:

* request count
* request duration
* request errors
* dependency failures
* database latency
* Redis latency
* event publish failures
* event consumption failures
* queue/job metrics
* active WebSocket connections where applicable

Use bounded metric labels.

Do not use raw user IDs, email addresses, phone numbers, trip IDs, or arbitrary resource identifiers as metric labels.

## 13. Database Module

Implement the PostgreSQL integration layer.

Provide:

* connection configuration
* connection lifecycle
* graceful shutdown
* health checks
* transaction support
* connection configuration
* environment-specific configuration
* safe error handling

Use Prisma according to the architecture.

Do not allow uncontrolled per-request database client creation.

## 14. Prisma Integration

Create the foundation for a maintainable Prisma integration.

Implement:

* Prisma client lifecycle
* dependency injection
* graceful disconnect
* logging configuration
* transaction helper boundaries where appropriate

Do not create all business-domain models in this milestone.

Only create foundational database artifacts required by the platform itself.

## 15. Database Transaction Utilities

Provide reusable transaction infrastructure.

Support:

* interactive transactions where needed
* transaction-scoped database access
* correct transaction lifecycle
* rollback on failure
* bounded transaction duration where practical

Do not hide all database operations inside an abstraction so generic that transaction semantics become unclear.

Transactions must remain visible at important business boundaries.

## 16. Database Error Translation

Create safe translation for common database failure categories such as:

* unique constraint conflict
* foreign key conflict
* serialization/deadlock failure
* connection failure
* timeout
* unavailable database

Map them into appropriate internal application errors.

Do not expose raw database exceptions to API clients.

## 17. Redis Module

Implement a reusable Redis integration.

Support:

* connection configuration
* lifecycle management
* graceful shutdown
* health checks
* retry behavior appropriate to the architecture
* bounded connection configuration

Do not make Redis startup failure behave identically to PostgreSQL failure when a specific application mode can safely run without Redis.

The dependency criticality must follow the architecture.

## 18. Cache Abstraction

Create a coherent cache abstraction for later domains.

Support:

* key generation
* TTL
* get/set
* deletion
* serialization
* cache misses
* cache errors
* invalidation

Define cache behavior when Redis is unavailable.

Do not silently treat stale cache data as authoritative transactional state.

## 19. Redis Namespace Conventions

Establish deterministic Redis key conventions.

They must support:

* environment isolation
* domain isolation
* entity scope
* versioning where needed
* predictable expiration

Prevent arbitrary user-supplied strings from becoming dangerous unbounded key namespaces.

## 20. Rate Limiting Foundation

Implement shared rate-limiting infrastructure.

The design must support dimensions such as:

* IP
* authenticated actor
* device/session
* route
* operation

Use Redis-backed distributed coordination where appropriate.

Rate limiting must be configurable.

Do not create separate incompatible rate-limit implementations for every future domain.

## 21. Rate-Limit Failure Behavior

Define behavior when the rate-limiting dependency is unavailable.

For security-sensitive endpoints, fail according to the architecture's protective posture.

For less sensitive endpoints, a controlled degraded mode may be possible.

The behavior must be explicit.

Do not accidentally convert a Redis outage into either:

* unrestricted abuse
* total application unavailability

without an architectural reason.

## 22. Idempotency Infrastructure

Implement shared idempotency support according to Architecture Volume 2.

Support:

* idempotency key extraction
* scope
* request fingerprinting where appropriate
* persistence
* in-progress handling
* completed-response reuse
* conflict handling
* expiration
* cleanup

Idempotency records must distinguish:

* same key/same request
* same key/different request
* in-progress request
* successfully completed request
* failed request

Do not store sensitive request payloads unnecessarily.

## 23. Idempotency Storage

Use the architecture's appropriate durable/ephemeral storage for idempotency records.

For operations where correctness must survive process restarts, do not rely solely on in-memory state.

Implement indexes/constraints required to prevent race conditions.

## 24. Concurrency Utilities

Create reusable infrastructure for optimistic concurrency and compare-and-set style operations where required.

Support future domain code in enforcing:

* version checks
* update conditions
* conflict detection

Do not implement generic distributed locking unless a real platform requirement exists.

## 25. Outbox Infrastructure

Implement the foundational transactional outbox pattern.

Provide:

* outbox record representation
* event metadata
* persistence
* transaction integration
* publication state
* retry metadata
* correlation/causation identifiers
* timestamps

The outbox must be written transactionally with the authoritative database change it represents.

Do not publish directly to Kafka before the database transaction can guarantee the state change.

## 26. Outbox Publisher

Implement the background mechanism that publishes pending outbox records.

Support:

* bounded batching
* retry
* exponential/backoff behavior where appropriate
* failure tracking
* successful publication
* safe process restart
* duplicate-publication tolerance

Do not mark an event successfully published before the broker confirms the required delivery semantics.

## 27. Outbox Recovery

Implement recovery for:

* process interruption
* broker outage
* duplicate publisher execution
* stale outbox records
* partial publication failure

Provide observability for:

* outbox backlog
* oldest pending event
* publish failures
* retry counts

## 28. Event Publishing Abstraction

Create a reusable event-publishing abstraction.

Support:

* canonical event envelope
* schema/version metadata
* correlation
* causation
* producer identity
* region
* event timestamp

Keep domain-specific event construction out of the generic infrastructure.

## 29. Event Consumer Foundation

Implement a reusable consumer foundation for later backend domains.

Support:

* consumer configuration
* consumer-group identity
* graceful shutdown
* message deserialization
* event validation
* tracing
* error classification
* retry integration
* dead-letter handling hooks
* idempotent processing hooks

Do not implement domain-specific consumers yet.

## 30. Event Consumer Error Handling

Distinguish between:

* transient infrastructure failures
* malformed events
* validation failures
* permanent business failures
* dependency failures

Provide a deterministic mechanism for later consumers to choose:

* retry
* dead-letter
* ignore
* manual review

Do not silently discard invalid events.

## 31. Background Job Module

Implement shared BullMQ or equivalent infrastructure.

Support:

* connection lifecycle
* queue creation
* worker registration
* job metadata
* retries
* backoff
* concurrency
* timeout
* graceful shutdown
* structured logging
* tracing

Do not create business-specific queues yet unless required by foundational infrastructure tests.

## 32. Job Execution Context

Propagate:

* job ID
* correlation ID
* actor context where appropriate
* trace context
* attempt count
* job version

into worker execution.

Workers must not depend on HTTP request context being present.

## 33. Job Failure Handling

Define shared handling for:

* transient failure
* permanent failure
* malformed payload
* timeout
* cancellation
* exhausted retries

Support dead-letter or terminal-failure recording where appropriate.

Do not retry permanently invalid jobs indefinitely.

## 34. Health Checks

Implement health endpoints according to the architecture.

Distinguish:

* process liveness
* readiness
* dependency health

Provide checks for relevant dependencies such as:

* PostgreSQL
* Redis
* event broker
* job infrastructure

Do not make liveness depend on every external dependency.

A degraded dependency should affect readiness only when the service cannot safely serve its intended function.

## 35. Graceful Shutdown

Implement graceful shutdown for:

* HTTP server
* WebSocket layer foundation
* PostgreSQL
* Redis
* event consumers
* outbox publisher
* job workers

Shutdown must:

* stop accepting new work
* allow bounded in-flight work to complete
* stop consumers safely
* close connections
* flush required telemetry
* exit deterministically

Do not wait indefinitely for unhealthy dependencies.

## 36. Security Foundation

Implement backend security infrastructure including:

* secure headers where appropriate
* request-size limits
* validation
* authentication guard foundations
* authorization guard foundations
* service identity hooks
* secure error handling
* secret-safe logging

Do not implement complete account authentication flows yet.

Create reusable boundaries for later identity work.

## 37. Authentication Context Foundation

Create the backend abstraction that later authentication modules can populate.

It should support:

* authenticated principal
* principal type
* subject identifier
* session identifier
* roles/permissions
* authentication method metadata where needed

Do not fabricate authenticated users.

Unauthenticated requests must be represented explicitly.

## 38. Authorization Foundation

Create reusable infrastructure for:

* route guards
* permission checks
* resource authorization hooks
* service authorization hooks

Do not hard-code rider/driver business permissions that belong in the identity milestone.

The infrastructure should allow later domain-specific authorization to plug into it.

## 39. Audit Foundation

Implement the base audit infrastructure.

Support:

* actor identity
* actor type
* action
* target type
* target ID
* timestamp
* request/correlation ID
* result
* metadata

Ensure sensitive values are not logged indiscriminately.

Create the infrastructure needed by later business domains to record audited actions.

## 40. OpenAPI and API Documentation

Implement the backend's OpenAPI foundation.

Ensure:

* generated schema support
* authentication schemes
* error models
* request/response documentation
* version metadata
* consistent operation identifiers

Do not document endpoints that do not yet exist.

The generated specification must accurately reflect implemented routes.

## 41. API Versioning

Implement the architecture's API versioning mechanism.

Use a consistent strategy compatible with future web and mobile releases.

Do not introduce multiple versioning mechanisms.

## 42. Request Limits and Abuse Protection

Implement foundational controls for:

* request body size
* URL/query size where appropriate
* header limits where configurable
* malformed request protection
* basic abuse throttling

Do not allow unbounded request payloads.

## 43. Database Migration Foundation

Establish safe migration execution conventions.

Provide:

* development migration workflow
* test database setup
* migration validation
* deployment-safe migration principles

Do not introduce domain schema beyond foundational infrastructure.

Do not create destructive production migration behavior merely to simplify local development.

## 44. Test Infrastructure

Create the backend testing foundation.

Support:

* unit tests
* module-level integration tests
* database integration tests where practical
* Redis integration tests where practical
* event infrastructure tests
* job infrastructure tests
* API infrastructure tests

Provide deterministic setup/teardown.

Avoid tests that depend on inaccessible production infrastructure.

## 45. Local Development Infrastructure Integration

Make the backend capable of running against the repository's local infrastructure.

Support:

* PostgreSQL/PostGIS
* Redis
* Kafka/Redpanda
* object storage abstraction where required

Use existing Docker/Compose/local infrastructure when available.

Do not create a competing local-development stack.

## 46. Dependency Injection and Module Boundaries

Structure NestJS modules so foundational infrastructure has clear boundaries.

At minimum separate concerns for:

* configuration
* database
* Redis
* cache
* events
* jobs
* idempotency
* rate limiting
* audit
* observability
* API/platform utilities

Prevent cyclic dependencies.

Do not create a giant "CommonModule" containing every unrelated concern.

## 47. Backend Error and Dependency Telemetry

Instrument foundational infrastructure failures.

Expose metrics/logs for:

* database failures
* Redis failures
* rate-limit failures
* idempotency conflicts
* outbox backlog
* event publish failures
* event consumer failures
* queue failures
* job retries
* health degradation

Do not include sensitive payloads.

## 48. Documentation

Create or update backend documentation covering:

* application structure
* module boundaries
* configuration
* database access
* Redis
* caching
* rate limiting
* idempotency
* outbox
* events
* jobs
* health
* shutdown
* security foundations
* audit
* OpenAPI
* testing
* local development

Documentation must describe the implementation actually created.

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement:

* rider domain logic
* driver domain logic
* vehicle/fleet domain logic
* location business logic
* dispatch
* trips
* pricing
* payments
* earnings
* notifications
* messaging
* ratings
* safety
* support
* scheduled trips
* routing/geocoding business logic
* analytics/reporting

Those belong to later backend milestones.

Do not implement the frontend.

Do not implement mobile applications.

Do not implement production AWS/Terraform/Kubernetes infrastructure.

Do not create infrastructure-domain implementations merely to demonstrate later functionality.

Do not redesign the architecture established by Volumes 1 and 2 unless a concrete repository conflict requires it.

Do not create a surprise backend integration phase.

Do not create another foundational backend volume covering the same responsibilities.

# REPOSITORY INSPECTION REQUIREMENTS

Before implementation:

1. Inspect the repository.
2. Locate the backend application.
3. Inspect package.json.
4. Inspect TypeScript configuration.
5. Inspect NestJS bootstrap/application modules.
6. Inspect existing Prisma configuration.
7. Inspect database migrations.
8. Inspect Redis integration.
9. Inspect Kafka/Redpanda integration.
10. Inspect BullMQ/job infrastructure.
11. Inspect OpenTelemetry/logging infrastructure.
12. Inspect environment configuration.
13. Inspect test configuration.
14. Inspect Docker/local infrastructure.
15. Inspect existing API conventions.
16. Inspect the architecture artifacts created by the project.
17. Determine exactly which files require changes.

Do not blindly overwrite the backend.

# IMPLEMENTATION RULES

## Preserve Existing Behavior

If foundational backend code already exists:

* preserve working behavior
* extend it
* avoid unnecessary rewrites
* preserve API compatibility
* preserve established naming where compatible

## No Placeholders

Do not leave:

* TODO
* FIXME
* stubbed methods
* fake repositories
* fake clients
* fake event publishers
* dummy health checks

## Real Error Handling

Handle failures explicitly.

Do not swallow exceptions.

Do not log and ignore failures that affect correctness.

## Security

Never log:

* passwords
* tokens
* secrets
* payment credentials
* private message contents
* sensitive document contents

## Configuration

Never hard-code:

* credentials
* secret keys
* production endpoints
* environment-specific identifiers

## Database

Use proper connection lifecycle management.

Do not create unbounded connections.

## Redis

Treat Redis according to its architectural role.

Do not make it the durable source of truth for transactional entities.

## Events

Do not publish domain events directly from business transactions without the outbox boundary.

Ensure consumers are written for duplicate delivery.

## Jobs

Jobs must be retry-safe.

Do not create infinite retries.

## Observability

Use bounded-cardinality metrics.

Do not put arbitrary entity IDs into Prometheus labels.

## Testing

Tests must validate behavior rather than merely increase coverage counts.

# VALIDATION REQUIREMENTS

Execute all validation commands supported by the repository.

At minimum perform applicable checks for:

* dependency installation/verification
* TypeScript compilation
* linting
* formatting
* unit tests
* backend integration tests
* Prisma validation
* database migration validation
* Redis integration tests
* Kafka/Redpanda infrastructure tests where available
* job/queue tests
* OpenAPI generation/validation
* configuration-schema tests
* security scanning
* dependency vulnerability scanning where configured

Test failure behavior for:

* invalid environment configuration
* database unavailable
* Redis unavailable
* broker unavailable
* invalid requests
* duplicate idempotency keys
* conflicting idempotency keys
* transaction failure
* outbox publication failure
* consumer failure
* job retry exhaustion
* graceful shutdown

Do not claim tests passed unless they actually executed successfully.

# FINAL INTEGRATION CHECK

Before declaring this milestone complete:

1. Verify the NestJS application starts correctly.
2. Verify configuration validation occurs before normal application operation.
3. Verify request context is propagated consistently.
4. Verify global validation is active.
5. Verify error responses follow the architectural error contract.
6. Verify sensitive information is redacted from logs.
7. Verify tracing and metrics are integrated.
8. Verify PostgreSQL/Prisma lifecycle is correct.
9. Verify Redis lifecycle is correct.
10. Verify cache behavior is explicit.
11. Verify distributed rate limiting is implemented consistently.
12. Verify idempotency is durable and race-safe.
13. Verify transaction utilities preserve transactional boundaries.
14. Verify the outbox is transactional with database changes.
15. Verify outbox publication handles retry and restart safely.
16. Verify event consumer foundations handle validation, tracing, retries, and dead letters.
17. Verify job infrastructure is retry-safe and observable.
18. Verify health and readiness semantics are separated.
19. Verify graceful shutdown is implemented.
20. Verify authentication and authorization foundations are reusable.
21. Verify audit infrastructure is safe and usable by later domains.
22. Verify OpenAPI reflects actual implemented routes.
23. Verify migration and testing infrastructure works.
24. Verify local development remains compatible with repository infrastructure.
25. Verify no business-domain functionality has been prematurely implemented.
26. Verify no placeholder implementation remains.
27. Verify no fake validation result is reported.
28. Verify documentation matches the actual repository state.
29. Verify the backend foundation is ready for Backend Volume 2 without requiring architectural restructuring.

# DEFINITION OF DONE

This milestone is complete only when:

* the backend application foundation is implemented
* configuration is typed and validated
* request context exists
* global validation exists
* canonical error handling exists
* structured logging exists
* OpenTelemetry integration exists
* metrics infrastructure exists
* PostgreSQL/Prisma integration exists
* transaction utilities exist
* Redis integration exists
* cache abstraction exists
* rate limiting infrastructure exists
* idempotency infrastructure exists
* concurrency utilities exist
* transactional outbox exists
* outbox publisher exists
* event publisher foundation exists
* event consumer foundation exists
* retry/dead-letter hooks exist
* background-job infrastructure exists
* job failure handling exists
* health/readiness checks exist
* graceful shutdown exists
* security foundations exist
* authentication context foundation exists
* authorization foundation exists
* audit foundation exists
* OpenAPI foundation exists
* API versioning exists
* request-size/abuse controls exist
* database migration conventions exist
* test infrastructure exists
* local development integration exists
* module boundaries are coherent
* observability covers foundational dependencies
* documentation is updated
* no domain-specific business logic outside this milestone has been introduced
* no TODO or placeholder implementation remains
* validation results are truthful
* the backend is ready for the identity/account milestone

# IMPLEMENTATION REPORT

At completion, provide:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Backend Foundation Implemented

Summarize:

* NestJS bootstrap
* configuration
* request context
* validation
* errors
* logging
* observability

## Persistence Foundation

Summarize:

* PostgreSQL
* Prisma
* transactions
* migrations

## Redis Foundation

Summarize:

* connection management
* cache
* namespaces
* rate limiting
* idempotency

## Event Foundation

Summarize:

* outbox
* publisher
* consumer framework
* error handling
* tracing

## Job Foundation

Summarize:

* queues
* workers
* retries
* backoff
* shutdown

## Security Foundation

Summarize:

* authentication context
* authorization hooks
* request controls
* secret-safe logging

## API Foundation

Summarize:

* error contract
* validation
* versioning
* OpenAPI
* request context

## Test and Validation Results

List actual commands and actual outcomes.

## External Environment Limitations

Explicitly state which external services could not be exercised because the environment lacked access.

Do not claim successful execution against infrastructure that was unavailable.

## Architectural Decisions

Record meaningful implementation decisions.

## Known Limitations

List actual remaining limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement Backend Volume 1 completely.

Build the reusable backend platform foundation described by this prompt.

Do not implement later business domains.

Do not redesign the established architecture without a concrete reason.

Do not leave placeholders.

Do not fake external infrastructure execution.

Run every validation command supported by the environment.

Ensure the resulting backend foundation is secure, observable, testable, maintainable, and ready for Backend Volume 2.

Finish with the required implementation report and leave the repository in a coherent production-grade state.
