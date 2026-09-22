# Uber-Style Global Ride-Hailing & Mobility Platform — Backend Prompt — Volume 2

## ROLE

You are the senior backend engineering organization responsible for implementing the identity, account, authentication, driver onboarding, vehicle, role, permission, and ownership foundation of an original, production-grade global ride-hailing and mobility platform.

Operate simultaneously as:

* Principal Software Architect
* Staff Backend Engineer
* Distributed Systems Engineer
* Database Architect
* Security Engineer
* Identity and Access Engineer
* Reliability Engineer
* Performance Engineer
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
* safety personnel
* fleet personnel
* administrators

This milestone establishes the backend identity and account foundation required by the rest of the platform.

The architecture targets:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* large concurrent session volumes
* global multi-region operation
* strong authentication and authorization requirements

These are architectural targets, not measured capacity claims.

## Technology Direction

Use the locked project stack:

### Runtime

* Node.js
* TypeScript

### Framework

* NestJS

### Database

* PostgreSQL
* PostGIS where geographic data is relevant
* Prisma where compatible with the architecture

### Cache and Ephemeral State

* Redis

### Events

* Kafka or Redpanda

### Background Jobs

* BullMQ or equivalent

### Object Storage

* Amazon S3 where later identity/verification workflows require object references

### Realtime

* authenticated WebSockets through the established platform foundation

### Observability

* OpenTelemetry
* Prometheus-compatible metrics
* structured logs
* Loki-compatible logging
* Tempo-compatible tracing

# SOURCE OF TRUTH

The repository is the implementation source of truth.

Inspect the repository before making changes.

Use the architecture artifacts already present in the repository as the authoritative architectural and contractual reference.

This milestone implements the identity/account architecture defined by those artifacts.

Do not depend on the previous AI conversation.

If the repository already contains identity or authentication implementation:

1. inspect it
2. determine what is already working
3. preserve compatible behavior
4. extend rather than duplicate it
5. document meaningful conflicts

Do not blindly regenerate existing files.

# BACKEND EXECUTION MODEL

This milestone owns the identity and account domain foundation.

Implement:

* account identities
* rider profiles
* driver profiles
* authentication credentials
* sessions
* devices
* refresh-token/session management
* account lifecycle
* account status
* roles
* permissions
* resource ownership primitives
* driver onboarding state
* verification metadata
* vehicles
* vehicle categories
* service-area associations
* security-sensitive identity events
* identity-related jobs
* identity auditing

Do not implement trip, dispatch, pricing, payment, notification, messaging, safety, support, fleet operations, scheduled trips, or analytics business logic beyond the identity/driver/vehicle data required by this milestone.

# CURRENT IMPLEMENTATION SCOPE

## 1. Domain Boundary

Establish clear backend ownership for:

* Account
* Rider Profile
* Driver Profile
* Session
* Device
* Credential
* Role
* Permission
* Driver Onboarding
* Driver Verification Metadata
* Vehicle
* Vehicle Category
* Driver-Vehicle association
* Service-area association where required

The identity/account domain must own the authoritative state for these entities.

Do not allow later domains to directly mutate identity-owned records without an explicit contract.

## 2. Account Model

Implement the canonical account representation.

The model must support, according to the architecture:

* stable account identifier
* account type/persona where required
* status
* creation timestamp
* update timestamp
* lifecycle state
* identity metadata references
* security metadata
* region or service-area context where required

Do not store unnecessary personal data in the root account record.

Separate authentication/security state from business-profile state where the architecture requires it.

## 3. Account Lifecycle

Implement explicit account lifecycle behavior.

Support states appropriate to the architecture, such as:

* pending
* active
* restricted
* suspended
* deactivated

The exact state model must follow the repository architecture.

Define legal transitions.

Do not permit arbitrary state mutation.

Distinguish:

* temporary restriction
* security suspension
* voluntary deactivation
* administrative deactivation

where the architecture requires different behavior.

## 4. Rider Profile

Implement the rider profile domain owned by the account system.

Support the fields actually defined by the architecture.

Examples may include:

* display name
* contact references
* locale
* preferences that belong to the identity domain
* profile state

Do not move payment methods, trip history, ratings, or support data into the rider profile merely because they relate to riders.

Those remain owned by their respective domains.

## 5. Driver Profile

Implement the driver profile foundation.

Support:

* driver identity
* onboarding status
* driver status
* verification status
* service-area eligibility references
* vehicle association
* profile metadata

Do not implement driver availability or realtime location here.

Those belong to the location/availability milestone.

## 6. Authentication Credentials

Implement secure credential storage and management appropriate to the architecture.

Support the authentication methods actually selected by the repository.

Where password authentication is used:

* never store plaintext passwords
* use a modern password-hashing strategy
* use appropriate work factors/configuration
* protect against credential enumeration
* validate password requirements
* provide secure credential replacement

Where passwordless or provider-based identity is used, preserve the architecture rather than introducing unnecessary password storage.

Never log credentials.

## 7. Authentication Flows

Implement the backend foundation for supported authentication flows.

At minimum establish the actual flow required by the architecture for:

* account registration
* authentication
* session creation
* token issuance
* refresh
* logout
* credential failure
* account restriction/suspension

Do not add multiple authentication mechanisms merely for completeness.

Implement only the mechanisms established by the project's architecture.

## 8. Password Security

If password authentication exists, implement:

* hashing
* verification
* password-change flow
* secure password replacement
* failed-attempt handling
* credential invalidation after security-sensitive changes

Do not return information that reveals whether an account exists when the contract requires anti-enumeration behavior.

Do not store password-reset tokens permanently in plaintext.

## 9. Session Model

Implement a durable session model.

Support:

* session identifier
* account identifier
* device identifier
* creation time
* last-used time
* expiration
* revocation
* authentication metadata
* session status

Define which state is durable and which ephemeral information may live in Redis.

A session must remain auditable.

## 10. Access and Refresh Token Strategy

Implement the project's canonical token strategy.

Support:

* short-lived access credentials
* refresh-session mechanism
* rotation where required
* revocation
* expiration
* token reuse detection where required

Do not use an indefinitely valid access token.

Do not store raw refresh tokens in the database when the architecture calls for hashed representations.

## 11. Refresh-Token Rotation

Where refresh rotation is part of the architecture, implement it correctly.

Handle:

* rotation
* previous-token invalidation
* replay detection
* concurrent refresh attempts
* session revocation
* expiration

A reused revoked refresh token must not silently create a new valid session.

## 12. Device Model

Implement device/session association.

Support:

* device identifier
* platform
* application version where required
* push capability metadata where appropriate
* device status
* last activity
* account association

Do not collect unnecessary device identifiers.

Do not expose internal device-security metadata to ordinary clients.

## 13. Session Revocation

Implement explicit session revocation.

Support:

* single-session logout
* all-session logout
* administrator/security revocation
* account suspension
* credential compromise response

Ensure revocation propagates to active authentication checks according to the architecture.

Where access tokens are self-contained and short-lived, document the security tradeoff and use session/revocation state where necessary for high-risk checks.

## 14. Authentication Rate Limiting

Integrate authentication operations with the shared rate-limiting infrastructure.

Protect:

* login
* registration
* credential changes
* token refresh
* verification attempts

Use appropriate identity and device/IP dimensions.

Do not create a second unrelated rate-limiter implementation.

## 15. Credential Security Events

Publish and audit security-relevant events such as:

* account registered
* authentication succeeded
* authentication failed
* session created
* session revoked
* credential changed
* credential reset where applicable
* suspicious refresh reuse
* account suspended
* account reactivated

Use the canonical event envelope.

Do not include raw credentials in events.

## 16. Role Model

Implement the foundational role model.

Support the roles explicitly required by the architecture, such as:

* rider
* driver
* support
* operations
* safety
* fleet
* administrator

Do not hard-code role checks throughout unrelated modules.

Roles must integrate with the shared authorization infrastructure.

## 17. Permission Model

Implement permission primitives.

Permissions should be explicit and machine-readable.

Support:

* resource
* action
* role association
* permission evaluation

Do not make an unrestricted administrator role the only way to implement privileged workflows.

## 18. Authorization Integration

Connect the identity model with the authorization foundation created in Backend Volume 1.

Support:

* authenticated principal
* roles
* permissions
* account status
* session status

Authorization failures must use the canonical error model.

Do not allow suspended accounts to continue normal authenticated access merely because a token remains technically valid.

## 19. Resource Ownership

Implement reusable ownership concepts for identity-owned entities.

Support authorization checks such as:

* account owns profile
* account owns session
* driver owns driver profile
* driver controls authorized vehicle association
* privileged operator has explicit administrative scope

Do not implement arbitrary cross-domain ownership rules here.

## 20. Driver Onboarding State

Implement the driver's onboarding lifecycle.

Support the architecture's actual states, potentially including:

* not started
* started
* information submitted
* verification pending
* verification failed
* approved
* rejected
* suspended

Define legal transitions.

Do not mark a driver operationally eligible merely because onboarding records exist.

Driver availability eligibility will be handled by later domain logic.

## 21. Driver Verification Metadata

Implement storage for verification state and references.

Support metadata for:

* verification provider/reference
* verification type
* status
* submitted-at
* reviewed-at
* expiration where applicable
* failure reason category
* evidence reference

Do not store sensitive document contents directly in identity tables when S3/object-storage architecture is intended.

Do not store raw third-party verification secrets.

## 22. Verification Provider Boundary

Create the backend abstraction required for future identity/verification providers.

The interface must isolate:

* provider-specific IDs
* provider-specific statuses
* provider-specific errors

Do not hard-code a provider-specific status model into the domain.

Do not implement a fictional external verification provider.

## 23. Verification Webhooks or Callbacks

Where the architecture requires provider callbacks, establish the identity-domain boundary for them.

Support:

* signature/authentication validation
* idempotency
* event versioning
* provider-reference lookup
* state transition validation
* auditability

Do not trust callback payloads solely because they arrive at a known endpoint.

## 24. Vehicle Model

Implement vehicle ownership data.

Support the fields established by architecture, such as:

* vehicle identifier
* driver association
* category
* make/model metadata
* model year where required
* license/registration references
* status
* verification status

Do not implement maintenance workflows yet.

Those belong to the fleet milestone.

## 25. Vehicle Categories

Implement canonical vehicle/service categories needed by later trip and dispatch domains.

Categories must have:

* stable identifier
* name/code
* status
* capacity/configuration metadata where appropriate

Avoid encoding business logic through arbitrary strings.

## 26. Driver-Vehicle Association

Implement the relationship between a driver and authorized vehicles.

Support:

* association
* disassociation
* primary/active designation where required
* validity periods where required
* status

Enforce ownership and authorization constraints.

A driver must not be able to arbitrarily associate with a vehicle owned by another driver unless the architecture explicitly allows shared/fleet ownership.

## 27. Service-Area Associations

Implement the identity-owned relationship necessary to associate drivers with service areas where the architecture requires it.

Support:

* service-area reference
* driver association
* status
* validity

Do not implement full geographic dispatch logic.

Do not duplicate PostGIS matching behavior that belongs to the location/dispatch domains.

## 28. Database Constraints

Use database-level constraints for important identity invariants.

Enforce as appropriate:

* unique identifiers
* unique active session relationships where required
* unique credential constraints
* valid foreign keys
* valid role/permission relations
* driver/vehicle relationship integrity

Do not rely exclusively on application checks for invariants that PostgreSQL can enforce safely.

## 29. Indexing

Create indexes based on actual query patterns.

Consider:

* account lookup
* credential lookup
* session lookup
* active session retrieval
* driver status lookup
* onboarding status
* verification status
* vehicle lookup
* driver-vehicle association

Do not create indexes merely on every column.

Account for write cost and expected cardinality.

## 30. Transactions

Use transactions for identity operations that require atomic changes.

Examples:

* account registration plus credential initialization
* session creation plus security-state updates
* credential rotation plus session revocation
* driver/vehicle association changes
* onboarding state transitions

Keep transaction scope bounded.

Do not hold transactions open across external provider calls.

## 31. Identity Cache Usage

Use Redis only for appropriate identity-related ephemeral state.

Potential uses include:

* short-lived authentication attempt state
* rate limits
* session acceleration
* revocation/cache lookups where justified
* temporary verification workflow state

Do not make Redis the authoritative account database.

## 32. Security-Sensitive Caching

Do not cache sensitive authentication information indefinitely.

For any cached identity/security state define:

* key scope
* TTL
* invalidation
* stale behavior
* failure behavior

Do not allow stale authorization or suspension state to remain active indefinitely.

## 33. Authentication Audit

Use the audit foundation from Backend Volume 1.

Audit important actions such as:

* account creation
* credential changes
* login security events
* session revocation
* role changes
* permission changes
* driver approval/rejection
* vehicle authorization
* administrative account actions

Do not log passwords, raw tokens, private documents, or sensitive verification payloads.

## 34. Administrative Authorization

Protect privileged identity operations.

Administrative actions must require the appropriate role/permission and resource scope.

Examples:

* suspending an account
* changing roles
* approving identity verification
* modifying driver status
* associating a vehicle

Do not create hidden administrative bypasses.

## 35. Events and Outbox Integration

Publish domain events through the shared transactional outbox.

Potential events include:

* account.created
* account.status.changed
* rider.profile.updated
* driver.created
* driver.onboarding.updated
* driver.verification.updated
* vehicle.created
* vehicle.updated
* driver.vehicle.association.changed
* session.created
* session.revoked
* security.authentication.failed

Use the exact naming conventions established by Architecture Volume 2.

Do not emit events for every internal implementation detail.

## 36. Identity Event Idempotency

Ensure consumers can safely process identity events more than once.

Events must contain:

* event ID
* entity ID
* event type/version
* occurred-at
* correlation/causation metadata

Do not rely on consumers receiving exactly one event.

## 37. Background Jobs

Use the shared job infrastructure for identity-related asynchronous work where required.

Potential jobs include:

* expired-session cleanup
* stale credential/security-state cleanup
* verification timeout processing
* document/reference cleanup
* onboarding reminders where explicitly part of the architecture

Do not implement notification-specific business workflows in this milestone.

## 38. Security and Privacy

Protect identity data through:

* least-privilege database access
* field minimization
* safe serialization
* secure logging
* secure error responses
* encrypted secret handling
* strict authorization

Never expose:

* password hashes
* refresh-token hashes
* security secrets
* internal verification credentials
* sensitive provider data

through standard API responses.

## 39. API Layer

Implement the identity endpoints defined by the architecture.

Depending on the repository's exact contract, these may cover:

* registration
* authentication
* token refresh
* logout
* session management
* account profile
* driver onboarding
* verification state
* vehicle management
* authorized role/permission operations

Only implement routes actually defined by the repository contract.

Do not invent an incompatible API surface.

## 40. API Validation

Validate:

* request schemas
* authentication state
* authorization
* account status
* identifier formats
* pagination where applicable
* idempotency where required

Return the canonical error contract.

## 41. Security Against Enumeration

Protect endpoints where account existence must remain private.

Use consistent responses and timing-aware design where appropriate.

Do not reveal:

* whether an email/phone belongs to an account
* whether a credential is valid
* internal verification details

unless the contract explicitly permits disclosure.

## 42. Testing

Create comprehensive tests for:

### Account

* creation
* duplicate identity handling
* lifecycle transitions
* profile authorization

### Authentication

* valid login
* invalid credentials
* rate limits
* session creation
* refresh
* rotation
* replay detection
* logout
* revocation
* account suspension

### Authorization

* role permissions
* resource ownership
* privileged actions
* denied access

### Driver

* onboarding transitions
* verification states
* unauthorized changes

### Vehicles

* creation
* updates
* association
* ownership restrictions
* invalid transitions

### Events

* outbox creation
* event publication
* duplicate delivery handling

### Security

* secret leakage prevention
* enumeration resistance
* invalid token behavior

## 43. Documentation

Create or update backend documentation for:

* account model
* authentication
* sessions
* devices
* authorization
* roles
* permissions
* driver onboarding
* verification boundaries
* vehicle ownership
* service-area associations
* security events
* operational procedures

Documentation must reflect actual implementation.

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement:

* driver online/offline availability
* driver work sessions
* realtime driver location
* location ingestion
* dispatch
* trip state
* pricing
* payment processing
* earnings
* payouts
* notifications
* messaging
* ratings
* safety incidents
* support case workflows
* scheduled rides
* fleet maintenance
* analytics/reporting

Do not implement detailed map matching.

Do not implement dispatch candidate search.

Do not introduce a separate identity microservice unless the repository architecture explicitly requires one.

Do not replace the established authentication/session foundation with a competing mechanism.

Do not create a surprise integration phase.

Do not create another identity/account backend volume covering the same scope.

# REPOSITORY INSPECTION REQUIREMENTS

Before implementation:

1. Inspect the backend repository.
2. Inspect the foundational backend modules created by Volume 1.
3. Inspect Prisma schema and migrations.
4. Inspect API conventions.
5. Inspect authentication foundations.
6. Inspect authorization foundations.
7. Inspect request context.
8. Inspect error handling.
9. Inspect Redis abstractions.
10. Inspect rate-limiting infrastructure.
11. Inspect idempotency infrastructure.
12. Inspect outbox/event infrastructure.
13. Inspect job infrastructure.
14. Inspect audit infrastructure.
15. Inspect architecture contract artifacts.
16. Determine exactly which files must be created or modified.

Preserve existing foundations.

# IMPLEMENTATION RULES

## Preserve Existing Infrastructure

Extend the foundational modules.

Do not duplicate:

* configuration
* database integration
* Redis clients
* rate limiting
* idempotency
* event publishing
* job infrastructure
* audit infrastructure
* logging
* telemetry

## Secure Defaults

Identity and authentication behavior must fail securely.

Do not default to permissive authorization.

## Credential Safety

Never log raw credentials.

Never return credential secrets to clients.

Never store plaintext passwords.

## Session Safety

Session invalidation must be deterministic.

Token rotation and revocation must handle concurrency correctly.

## Database Integrity

Use PostgreSQL constraints and transactions for identity invariants.

## External Providers

Keep verification provider-specific details behind the provider abstraction.

Never fake verification success.

## Events

Use the shared transactional outbox.

Do not publish identity events directly before the authoritative database transaction is committed.

## Idempotency

Critical identity mutations must be safe under retries.

## Authorization

Every privileged mutation must perform explicit authorization.

## Testing

Tests must exercise both successful and adversarial paths.

# VALIDATION REQUIREMENTS

Execute all validation supported by the repository.

At minimum:

* TypeScript compilation
* linting
* formatting
* unit tests
* API integration tests
* Prisma validation
* migration validation
* authentication tests
* authorization tests
* Redis-dependent tests
* outbox/event tests
* job tests
* OpenAPI validation
* security tests
* dependency/security scanning where configured

Validate failure scenarios including:

* duplicate account registration
* invalid credentials
* expired access token
* refresh-token replay
* revoked session
* suspended account
* insufficient permission
* unauthorized vehicle association
* invalid onboarding transition
* verification callback duplication
* event publication failure
* database transaction failure
* race conditions in credential/session updates

Do not claim successful external provider verification unless a real provider is available and actually exercised.

# FINAL INTEGRATION CHECK

Before declaring this milestone complete:

1. Verify account ownership is explicit.
2. Verify authentication and account lifecycle are distinct but integrated.
3. Verify sessions are durable and revocable.
4. Verify refresh-token behavior is secure.
5. Verify authentication rate limiting uses the shared infrastructure.
6. Verify role and permission models integrate with the authorization foundation.
7. Verify privileged actions are authorization-protected.
8. Verify driver onboarding state transitions are explicit.
9. Verify verification-provider details remain abstracted.
10. Verify vehicle ownership and associations are integrity-protected.
11. Verify service-area associations do not implement dispatch logic prematurely.
12. Verify PostgreSQL constraints protect important identity invariants.
13. Verify sensitive authentication data is absent from logs and normal responses.
14. Verify identity events use the outbox infrastructure.
15. Verify event consumers can tolerate duplicate delivery.
16. Verify identity background jobs are retry-safe.
17. Verify security-sensitive actions are auditable.
18. Verify enumeration-sensitive APIs do not reveal account existence improperly.
19. Verify tests cover concurrency and adversarial cases.
20. Verify no later backend domain was implemented prematurely.
21. Verify the implementation remains compatible with Backend Volume 1.
22. Verify the repository remains ready for Backend Volume 3.
23. Verify no placeholder or fake provider implementation remains.

# DEFINITION OF DONE

This milestone is complete only when:

* account model exists
* account lifecycle exists
* rider profile exists
* driver profile exists
* authentication credentials are secure
* authentication flows are implemented according to the architecture
* session management exists
* token refresh/revocation behavior exists
* device/session association exists
* authentication rate limiting is integrated
* roles exist
* permissions exist
* authorization integration exists
* resource ownership primitives exist
* driver onboarding exists
* verification metadata exists
* verification provider abstraction exists
* required callbacks/webhooks are protected
* vehicle model exists
* vehicle categories exist
* driver-vehicle associations exist
* service-area associations exist where required
* database constraints and indexes exist
* transactions protect critical mutations
* Redis is used only for appropriate identity-related ephemeral state
* audit events exist for sensitive actions
* identity events use the transactional outbox
* background cleanup/verification jobs exist where required
* security controls are implemented
* identity APIs conform to the established contracts
* tests cover normal and adversarial flows
* documentation is updated
* no placeholder implementation remains
* no unrelated domain has been implemented
* validation results are truthful
* the backend remains ready for the driver availability/location milestone

# IMPLEMENTATION REPORT

At completion, provide:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Identity and Account Implementation

Summarize:

* accounts
* riders
* drivers
* sessions
* devices
* credentials
* roles
* permissions

## Driver Onboarding

Summarize:

* lifecycle
* verification state
* provider abstraction
* events

## Vehicle and Ownership

Summarize:

* vehicles
* categories
* driver associations
* service-area associations

## Security

Summarize:

* authentication
* session security
* authorization
* rate limiting
* enumeration protection
* audit

## Events and Jobs

Summarize:

* identity events
* outbox usage
* background jobs
* retry behavior

## Database

Summarize:

* schema changes
* constraints
* indexes
* transactions
* migrations

## API

Summarize implemented identity/account endpoints.

## Tests and Validation

List actual commands and actual outcomes.

## External Environment Limitations

Identify any external verification or infrastructure integration that could not be executed.

Do not claim successful provider or cloud execution when unavailable.

## Architectural Decisions

Record important decisions made during implementation.

## Known Limitations

List genuine remaining limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement Backend Volume 2 completely.

Extend the foundational backend platform rather than duplicating it.

Implement the identity, account, authentication, session, authorization, driver onboarding, verification metadata, vehicle, and ownership capabilities defined by this milestone.

Keep all later trip, dispatch, pricing, payment, notification, messaging, safety, fleet, scheduled-trip, and analytics domains out of scope.

Do not leave placeholders.

Do not fabricate identity-provider or external verification results.

Run every validation command supported by the environment.

Verify security, data integrity, authorization, concurrency, event publication, and session behavior.

Finish with the required implementation report and leave the repository in a coherent production-grade state ready for Backend Volume 3.
