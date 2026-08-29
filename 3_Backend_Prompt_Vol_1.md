You are operating in Senior Engineering Team Mode.

Build the production-ready backend foundation for an enterprise-scale global ride-hailing, mobility, transportation, and delivery platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

The backend must follow the approved Uber-like architecture, domain boundaries, service ownership, database architecture, geospatial architecture, dispatch architecture, matching architecture, pricing architecture, payment architecture, security model, event architecture, queue architecture, and Project Index.

Do not redesign the architecture.

Do not generate frontend code.

Do not generate mobile code.

Do not generate infrastructure implementation code.

Do not generate Terraform.

Do not generate Kubernetes manifests.

Do not generate CI/CD workflows.

────────────────────────────────────────

MISSION

Build the production-ready backend foundation required for:

• API Gateway
• Application bootstrap
• Configuration
• Request context
• Structured logging
• Error handling
• Validation
• Authentication foundation
• Authorization foundation
• PostgreSQL
• Prisma
• PostGIS
• Redis
• Kafka/Redpanda
• BullMQ
• WebSockets
• Socket.IO
• OpenTelemetry
• Metrics
• Health checks
• Graceful shutdown
• API contracts
• Event contracts
• Queue contracts
• Testing foundation
• Local development

This volume establishes the backend platform required by all later mobility domains.

The complete backend must eventually support:

• Riders
• Drivers
• Driver onboarding
• Driver verification
• Vehicles
• Availability
• Real-time location
• Geospatial matching
• Dispatch
• Ride requests
• Trips
• Scheduled rides
• Multi-stop trips
• Shared rides
• Pricing
• Surge
• Promotions
• Payments
• Wallets
• Earnings
• Incentives
• Payouts
• Ratings
• Messaging
• Notifications
• Safety
• Fraud
• Support
• Business accounts
• Analytics
• Administration
• Multi-region operation

────────────────────────────────────────

PRIMARY TECHNOLOGY STACK

Backend:

• Node.js
• NestJS
• TypeScript

Database:

• PostgreSQL
• Prisma ORM
• PostGIS

Cache:

• Redis

Event Streaming:

• Kafka or Redpanda

Background Processing:

• BullMQ

Real-Time:

• WebSockets
• Socket.IO

Maps:

• Google Maps Platform or approved provider abstraction

Payments:

• Stripe or approved payment abstraction

Notifications:

• Firebase Cloud Messaging
• Apple Push Notification Service
• Email/SMS provider abstractions

Object Storage:

• AWS S3-compatible storage

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

Testing:

• Jest
• Supertest
• Integration testing tools

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

Use safe timeout and retry policies.

Use idempotency where requests may be retried.

Use the established observability infrastructure.

────────────────────────────────────────

BACKEND ARCHITECTURE

Use:

• Clean Architecture
• Domain-Driven Design
• SOLID
• Repository Pattern
• Service Layer
• Dependency Injection
• Feature-first organization
• Explicit domain ownership
• CQRS where justified
• Event-driven communication where appropriate
• Transactional Outbox where appropriate
• Idempotent consumers
• Stateless services where possible

Do not create unnecessary microservices.

The implementation must permit future service extraction.

────────────────────────────────────────

MONOREPO BACKEND FOUNDATION

Create the backend structure required by the approved architecture.

Support:

apps/

• API Gateway

services/

Prepare service boundaries for:

• Identity
• Accounts
• Profiles
• Sessions
• Devices
• Riders
• Drivers
• Driver Onboarding
• Driver Verification
• Vehicles
• Availability
• Location
• Geospatial
• Maps
• Routing
• ETA
• Ride Requests
• Dispatch
• Matching
• Driver Offers
• Trips
• Scheduled Trips
• Shared Trips
• Pricing
• Surge
• Promotions
• Payments
• Wallets
• Refunds
• Earnings
• Incentives
• Payouts
• Ratings
• Messaging
• Notifications
• Safety
• Fraud
• Support
• Business Accounts
• Analytics
• Administration

workers/

• Background workers
• Scheduled jobs
• Event consumers

packages/

• Configuration
• Logging
• Errors
• Validation
• Database
• Redis
• Events
• Queues
• Observability
• API contracts
• Geospatial interfaces
• Maps interfaces
• Payment interfaces
• Testing utilities

────────────────────────────────────────

APPLICATION BOOTSTRAP

Implement NestJS application initialization.

Support:

• Environment loading
• Configuration
• Global validation
• Global exception handling
• Structured logging
• Request IDs
• Correlation IDs
• Trace IDs
• Secure headers
• CORS
• Request-size limits
• API versioning
• Graceful shutdown
• Health checks
• OpenAPI

Use production-safe defaults.

────────────────────────────────────────

CONFIGURATION

Implement centralized strongly typed configuration.

Support:

APPLICATION

• Environment
• Service name
• Version
• Host
• Port

POSTGRESQL

• Host
• Port
• Database
• Username
• Password
• SSL/TLS
• Connection pool

POSTGIS

• Spatial database configuration
• Geographic settings

REDIS

• Host
• Port
• Username
• Password
• TLS

KAFKA / REDPANDA

• Brokers
• Client ID
• Authentication
• TLS
• Consumer groups

BULLMQ

• Redis configuration
• Retry defaults
• Queue defaults

MAPS

• Provider
• API credentials
• Request timeout
• Regional provider configuration

PAYMENTS

• Provider configuration
• Webhook configuration

NOTIFICATIONS

• FCM
• APNS
• Email/SMS configuration

OBSERVABILITY

• Log level
• OpenTelemetry endpoint
• Metrics configuration

Never hard-code secrets.

Never access process.env throughout domain modules.

Validate all required configuration at startup.

Fail fast for invalid configuration.

────────────────────────────────────────

REQUEST CONTEXT

Implement reusable context containing:

• Request ID
• Correlation ID
• Trace ID
• Service
• Environment
• User ID
• Driver ID where authenticated
• Rider ID where authenticated
• Device ID
• Region
• City/service-area context where appropriate

Propagate context to:

• Logs
• Metrics
• Traces
• Kafka events
• Background jobs
• External requests

────────────────────────────────────────

LOGGING

Implement structured JSON logging.

Support:

• Timestamp
• Service
• Environment
• Log level
• Request ID
• Correlation ID
• Trace ID
• Operation
• Duration
• Result
• Safe error information

Never log:

• Passwords
• Access tokens
• Refresh tokens
• Payment secrets
• Private keys
• Database credentials
• Full payment information
• Unnecessary precise user location

────────────────────────────────────────

ERROR HANDLING

Implement centralized API error handling.

Define errors for:

• Validation
• Authentication
• Authorization
• Not found
• Conflict
• Rate limit
• Dependency unavailable
• External-provider failure
• Geospatial failure
• Dispatch failure
• Payment failure
• Internal error

Use a consistent error response:

• Error code
• Public-safe message
• Request ID
• Correlation ID
• Validation details where appropriate

Never expose stack traces in production responses.

────────────────────────────────────────

VALIDATION

Implement centralized validation for:

• Request bodies
• Query parameters
• Path parameters
• Headers
• Configuration
• Event payloads
• Queue payloads
• Webhook payloads
• Location coordinates

Validate geographic values:

• Latitude
• Longitude
• Accuracy
• Timestamp
• Speed where applicable
• Heading where applicable

Reject clearly impossible input.

────────────────────────────────────────

SECURITY FOUNDATION

Implement:

• Authentication guards
• Authorization guards
• RBAC foundation
• Permission foundation
• Rate limiting foundation
• Secure headers
• CORS
• Secret boundaries
• Audit hooks

Prepare for:

• Password authentication
• OAuth
• MFA
• Passkeys
• Device authentication
• Session management

Never store plaintext passwords.

────────────────────────────────────────

API FOUNDATION

Implement reusable REST API infrastructure.

Support:

• API versioning
• Request validation
• Response conventions
• Error conventions
• Pagination
• Cursor pagination
• Authentication
• Authorization
• Rate limiting
• OpenAPI
• Request tracing
• Timeout handling
• Cancellation
• Idempotency

Create reusable abstractions for:

• Idempotency keys
• Resource versioning
• Optimistic concurrency
• Safe retries

────────────────────────────────────────

DATABASE FOUNDATION

Implement PostgreSQL integration using Prisma.

Support:

• Prisma client lifecycle
• Connection handling
• Health checks
• Graceful shutdown
• Transactions
• Error translation
• Query logging controls
• Migration structure

Prepare for:

• PostgreSQL
• PostGIS
• Read replicas
• Connection pooling
• Partitioning

Do not create all domain models in this volume.

────────────────────────────────────────

PRISMA FOUNDATION

Define conventions for:

• IDs
• Timestamps
• Soft deletion where justified
• Optimistic concurrency
• Foreign keys
• Constraints
• Composite indexes
• Decimal monetary values

Prepare service/domain ownership boundaries.

Do not allow unrestricted cross-domain writes.

────────────────────────────────────────

POSTGIS FOUNDATION

Implement database-level PostGIS support.

Prepare utilities for:

• Point
• Polygon
• MultiPolygon
• Spatial reference system
• Distance queries
• Bounding boxes
• Spatial indexes

Define conventions for:

• WGS84 coordinates
• Geometry/geography usage
• Spatial indexes
• Precision

PostGIS is authoritative for durable geospatial entities such as:

• Service areas
• Geofences
• Airport zones
• Operational polygons

Do not use PostGIS as the high-frequency transient driver-location store.

────────────────────────────────────────

REDIS FOUNDATION

Implement reusable Redis infrastructure.

Support:

• Connection management
• TLS
• Authentication
• Health checks
• Graceful shutdown
• Namespaced keys
• Serialization
• TTL
• Cache abstraction
• Distributed short-lived lease abstraction
• Idempotency
• Geospatial primitives where appropriate

Prepare for:

• Driver availability
• Driver location
• Candidate pools
• ETA caching
• Rate limiting
• WebSocket coordination
• Dispatch state
• Notification deduplication

Redis must never be authoritative for:

• Trips
• Payments
• Wallets
• Earnings
• Payouts
• Driver identity
• Rider identity
• Historical financial data

────────────────────────────────────────

REDIS KEY CONVENTIONS

Create standardized key namespaces.

Examples:

• availability:
• location:
• dispatch:
• matching:
• trip:
• websocket:
• idempotency:
• rate-limit:
• notification:

Keys must include appropriate:

• Environment
• Region
• Entity scope

Define:

• TTL
• Serialization
• Invalidation
• Ownership

────────────────────────────────────────

KAFKA / REDPANDA FOUNDATION

Implement reusable event-streaming infrastructure.

Support:

• Producer lifecycle
• Consumer lifecycle
• Topic configuration
• Consumer groups
• Serialization
• Event IDs
• Event versions
• Correlation IDs
• Causation IDs where appropriate
• Retry
• Dead-letter handling
• Graceful shutdown

Event envelope:

• Event ID
• Event type
• Event version
• Aggregate type
• Aggregate ID
• Region
• Timestamp
• Correlation ID
• Causation ID where appropriate
• Producer
• Payload

Do not implement the full domain event catalog yet.

────────────────────────────────────────

TRANSACTIONAL OUTBOX

Implement reusable outbox infrastructure.

Support:

• Outbox ID
• Event type
• Event version
• Aggregate type
• Aggregate ID
• Region
• Payload
• Status
• Retry count
• Next retry timestamp
• Published timestamp
• Error information
• Created timestamp

Ensure domain transactions and event publication remain consistent.

Support recovery when:

• Database transaction succeeds
• Kafka publication fails

Publishing must be retryable and idempotent.

────────────────────────────────────────

BULLMQ FOUNDATION

Implement reusable asynchronous job infrastructure.

Support:

• Queue registration
• Producer
• Worker
• Job IDs
• Retry
• Exponential backoff
• Timeouts
• Concurrency
• Failure handling
• Dead-letter behavior
• Graceful shutdown
• Metrics

Prepare queues for:

• Driver verification
• Scheduled rides
• Notifications
• Receipts
• Payment reconciliation
• Payout processing
• Fraud analysis
• Support
• Analytics
• Cleanup

Do not implement full domain jobs in this volume.

────────────────────────────────────────

WEBSOCKET FOUNDATION

Implement production-ready WebSocket infrastructure.

Support:

• Connection establishment
• Authentication
• Authorization
• Heartbeats
• Reconnection
• Disconnect handling
• Connection metadata
• Region awareness
• Room/channel abstraction
• Rate limiting
• Backpressure

Prepare channels for:

• Driver location
• Trip tracking
• Dispatch offers
• Trip state
• Messaging
• Notifications

Do not implement full dispatch or location logic in this volume.

────────────────────────────────────────

SOCKET.IO FOUNDATION

Where Socket.IO is approved:

Implement:

• Gateway lifecycle
• Authentication middleware
• Connection tracking
• Room abstraction
• Event validation
• Error handling
• Heartbeats
• Rate limiting
• Graceful shutdown

Prepare horizontal scaling using Redis coordination.

────────────────────────────────────────

HEALTH CHECKS

Implement:

• Liveness
• Readiness
• Startup health where appropriate

Support checks for:

• PostgreSQL
• Redis
• Kafka
• BullMQ infrastructure
• PostGIS
• Maps dependency where appropriate

Do not make liveness depend on every external dependency.

Distinguish:

• Process alive
• Ready
• Dependency degraded

────────────────────────────────────────

GRACEFUL SHUTDOWN

Implement shutdown support for:

• HTTP server
• WebSocket gateways
• NestJS modules
• Prisma
• Redis
• Kafka producers
• Kafka consumers
• BullMQ workers

Stop accepting new work before closing dependencies.

Handle active requests and background jobs safely.

────────────────────────────────────────

OBSERVABILITY

Implement:

• Structured logging
• Metrics
• Distributed tracing
• Correlation IDs
• Request latency
• Error metrics
• Database metrics
• Redis metrics
• Kafka metrics
• Queue metrics
• WebSocket metrics

Use:

• OpenTelemetry
• Prometheus-compatible metrics

Prepare metrics for:

• API traffic
• WebSocket connections
• Location ingestion
• Dispatch
• Matching
• Trip state
• Payments
• Notifications

────────────────────────────────────────

MAP PROVIDER ABSTRACTION

Create interfaces for:

• Geocoding
• Reverse geocoding
• Places
• Directions
• Routes
• Distance
• ETA

Do not allow provider-specific response models to leak into domain entities.

Prepare:

• Google Maps implementation boundary
• Future alternative providers

Implement timeout and error normalization.

────────────────────────────────────────

PAYMENT PROVIDER ABSTRACTION

Create interfaces for:

• Payment method
• Authorization
• Capture
• Refund
• Provider status
• Webhooks

Do not couple the trip domain directly to Stripe-specific objects.

────────────────────────────────────────

NOTIFICATION PROVIDER ABSTRACTION

Create interfaces for:

• Push
• Email
• SMS where approved

Support:

• Provider response normalization
• Retry
• Error classification

────────────────────────────────────────

API CONTRACT FOUNDATION

Create shared conventions for:

• Resource naming
• Request DTOs
• Response DTOs
• Pagination
• Cursor pagination
• Errors
• Idempotency
• Versioning

Prepare contract packages for:

• Riders
• Drivers
• Vehicles
• Location
• Ride requests
• Dispatch
• Trips
• Pricing
• Payments
• Earnings
• Safety
• Support

Do not implement domain business logic in contract packages.

────────────────────────────────────────

EVENT CONTRACT FOUNDATION

Create reusable conventions for:

• Event naming
• Event versions
• Metadata
• Producer ownership
• Payload schemas
• Compatibility
• Correlation

Do not create the full event catalog yet.

────────────────────────────────────────

TESTING FOUNDATION

Implement:

• Jest configuration
• Unit-test utilities
• Integration-test utilities
• Database test helpers
• Redis test helpers
• Kafka test helpers
• BullMQ test helpers
• WebSocket test helpers
• API testing helpers
• Test fixtures
• Test factories

Support deterministic tests.

────────────────────────────────────────

LOCAL DEVELOPMENT

Provide local infrastructure supporting:

• PostgreSQL
• PostGIS
• Redis
• Kafka/Redpanda
• OpenSearch where required later
• S3-compatible object storage where useful

Use Docker Compose where appropriate.

No local environment should require production credentials.

────────────────────────────────────────

SECURITY TEST FOUNDATION

Prepare tests for:

• Authentication
• Authorization
• Rate limiting
• IDOR
• Input validation
• WebSocket authorization
• Geographic input validation
• Provider webhook verification
• Secret exposure

────────────────────────────────────────

DOCUMENTATION

Generate backend foundation documentation covering:

• Backend architecture
• Project structure
• Configuration
• API conventions
• Error handling
• Validation
• Database conventions
• Prisma
• PostGIS
• Redis
• Kafka/Redpanda
• BullMQ
• WebSockets
• Socket.IO
• Maps abstraction
• Payment abstraction
• Notifications
• Observability
• Testing
• Local development
• Security foundation

────────────────────────────────────────

PROJECT INDEX

Update the backend Project Index with:

• Backend applications
• Services
• Workers
• Shared packages
• Configuration
• Database foundation
• PostGIS foundation
• Redis foundation
• Kafka foundation
• BullMQ foundation
• WebSocket foundation
• Maps abstraction
• Payment abstraction
• Notification abstraction
• Observability
• Testing
• Local development
• Security
• Generated files
• Modified files
• Remaining work
• Current milestone
• Dependencies

────────────────────────────────────────

IMPLEMENTATION MILESTONES

BACKEND MILESTONE 1

Monorepo backend structure, NestJS application bootstrap, configuration, request context, logging, error handling, validation, security foundation, and API foundation.

BACKEND MILESTONE 2

PostgreSQL, Prisma, PostGIS, migrations, transaction utilities, connection management, and database health.

BACKEND MILESTONE 3

Redis infrastructure, key conventions, cache abstractions, TTL handling, short-lived leases, idempotency, and geospatial primitives.

BACKEND MILESTONE 4

Kafka/Redpanda, event envelopes, producers, consumers, serialization, retries, dead-letter infrastructure, and transactional outbox.

BACKEND MILESTONE 5

BullMQ, queue infrastructure, worker lifecycle, retries, backoff, timeouts, dead-letter handling, and background-job observability.

BACKEND MILESTONE 6

WebSocket and Socket.IO foundation, authentication, connection management, rooms, Redis coordination, heartbeats, and backpressure.

BACKEND MILESTONE 7

Maps provider abstraction, routing abstraction, ETA abstraction, payment abstraction, notification abstraction, and provider error normalization.

BACKEND MILESTONE 8

Observability, health checks, graceful shutdown, metrics, tracing, and centralized diagnostics.

BACKEND MILESTONE 9

Testing infrastructure, integration helpers, fixtures, factories, local development, and security test foundations.

BACKEND MILESTONE 10

Shared API/event contracts, documentation, hardening, architecture conformance, and Project Index completion.

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

This volume covers only backend foundations:

• Application bootstrap
• Configuration
• Request context
• Logging
• Error handling
• Validation
• Security foundation
• API foundation
• PostgreSQL
• Prisma
• PostGIS
• Redis
• Kafka/Redpanda
• Transactional outbox
• BullMQ
• WebSockets
• Socket.IO
• Maps abstraction
• Payment abstraction
• Notification abstraction
• Observability
• Health checks
• Graceful shutdown
• Testing foundation
• Local development
• Shared contracts

Do not implement complete:

• Riders
• Drivers
• Driver onboarding
• Driver verification
• Vehicles
• Availability
• Location service
• Dispatch
• Matching
• Ride requests
• Trips
• Scheduled rides
• Shared rides
• Pricing
• Surge
• Promotions
• Payments business logic
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
• Analytics
• Administration

Those belong to later backend implementation volumes.

────────────────────────────────────────

QUALITY BAR

Treat this backend foundation as critical infrastructure for a globally distributed mobility platform.

Assume:

• Hundreds of millions of riders
• Millions of drivers
• Tens of millions of concurrent mobile connections
• Massive location traffic
• Very high dispatch throughput
• Large payment volumes
• Large trip history
• Global operation
• Regional dispatch
• Strict financial correctness
• Strict location privacy
• High availability
• Disaster recovery

Prioritize:

• Correctness
• Low latency
• Security
• Reliability
• Scalability
• Clear ownership
• Observability
• Testability
• Future service extraction
• Production readiness
