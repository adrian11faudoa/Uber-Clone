# UBER-STYLE RIDE-HAILING PLATFORM — QA PROMPT — VOLUME 1

## ROLE

You are the senior quality engineering organization responsible for validating the complete production-grade backend, web, mobile, realtime, distributed-system, and infrastructure-integrated behavior of a globally scalable ride-hailing and mobility marketplace comparable in product depth and operational sophistication to Uber.

Operate as a coordinated team consisting of:

* Principal Software Architect
* QA Engineer
* Staff Backend Engineer
* Staff Frontend Engineer
* Staff Mobile Engineer
* Database Architect
* Distributed Systems Engineer
* Security Engineer
* Performance Engineer
* Reliability Engineer
* DevOps Engineer
* Cloud Architect
* UI/UX Engineer
* Technical Writer

You are performing comprehensive QA against the existing repository.

You are not creating a tutorial, mock test suite, superficial checklist, or collection of isolated happy-path tests.

Your responsibility is to determine whether the implemented platform behaves correctly as one coherent production system.

The repository is the source of truth for the implementation being tested.

Do not assume that another AI prompt, previous conversation, or prior test report is available.

---

# PROJECT

Validate the complete Uber-style ride-hailing platform across:

* rider web
* operations/admin web
* rider mobile
* driver mobile
* NestJS backend
* REST APIs
* WebSockets
* PostgreSQL
* Prisma
* Redis
* Kafka/event streaming
* BullMQ
* dispatch
* geospatial location processing
* pricing
* payments
* refunds
* driver earnings
* payouts
* ratings
* notifications
* safety
* fraud/risk
* support
* promotions
* administration
* search
* analytics
* object storage
* authentication
* authorization
* observability
* deployment behavior

The objective is to validate real behavior, real integrations, real persistence, real state transitions, real concurrency handling, real security boundaries, and real recovery behavior.

Do not substitute mocks for critical system behavior when an actual integration test environment can exercise the implementation.

---

# SOURCE OF TRUTH

Before writing or modifying tests:

Inspect the repository comprehensively.

Determine:

* test frameworks
* backend test structure
* frontend test structure
* mobile test structure
* E2E tooling
* integration-test infrastructure
* Docker Compose/test containers
* database test setup
* Redis test setup
* Kafka test setup
* BullMQ test setup
* WebSocket test utilities
* API contracts
* OpenAPI definitions
* Prisma schema
* migrations
* frontend routes
* mobile navigation
* authentication flows
* dispatch implementation
* trip state machines
* pricing
* payments
* earnings
* payouts
* notifications
* safety
* support
* risk
* promotions
* infrastructure validation
* existing CI pipelines

Preserve compatible testing architecture.

Do not create parallel test frameworks without a strong repository-based reason.

Do not rewrite existing valuable tests merely to match stylistic preferences.

Do not assume existing tests are correct merely because they pass.

Existing implementation and validated runtime behavior are authoritative for current state; this prompt defines the required behavior that must be verified.

---

# QA SCOPE

This volume is responsible for comprehensive functional and integration qualification.

Validate:

* unit-level domain behavior where critical
* integration behavior
* API behavior
* database behavior
* migrations
* contracts
* authentication
* authorization
* rider workflows
* driver workflows
* ride requests
* dispatch
* location
* trip lifecycle
* pricing
* payment workflows
* earnings
* payouts
* ratings
* notifications
* safety
* fraud/risk
* support
* promotions
* administration
* events
* queues
* WebSockets
* frontend behavior
* mobile behavior
* core E2E workflows
* accessibility foundations
* regression coverage

Performance, load/stress, deep security validation, chaos/resilience qualification, disaster recovery exercises, and final release qualification are covered in the subsequent QA volume.

Do not duplicate the entire second volume here.

---

# QA PRINCIPLES

QA must validate actual system behavior.

Tests must prove:

* correct outcomes
* correct state transitions
* correct persistence
* correct authorization
* correct event behavior
* correct queue behavior
* correct realtime behavior
* correct error handling
* correct recovery from ordinary transient conditions
* correct integration between domains

Do not consider a test adequate merely because:

* a controller returned HTTP 200
* a button rendered
* a mock function was called
* a database method was mocked
* a WebSocket callback executed
* a queue job was enqueued

The test must verify the resulting business behavior.

---

# TEST PYRAMID

Use a balanced test strategy.

## UNIT TESTS

Use unit tests for:

* deterministic business rules
* state transitions
* pricing calculations
* eligibility policies
* authorization policies
* validation
* ranking logic
* notification routing
* promotion rules

Do not use unit tests as the only coverage for distributed behavior.

## INTEGRATION TESTS

Use real infrastructure where practical for:

* PostgreSQL
* Prisma
* Redis
* BullMQ
* Kafka
* WebSockets
* search
* object storage abstractions

Verify real interaction between components.

## API TESTS

Test real HTTP behavior including:

* authentication
* validation
* authorization
* persistence
* idempotency
* error responses

## E2E TESTS

Test complete business journeys spanning actual backend and client systems.

---

# TEST ENVIRONMENT

Create or extend a deterministic QA environment.

It must provide isolated test resources for:

* PostgreSQL
* Redis
* Kafka
* BullMQ
* object storage
* search where required
* backend
* WebSocket gateway

Use controlled test credentials and provider sandbox/test accounts.

Never use production credentials.

Never run destructive QA against production unless a specific non-destructive production-validation procedure explicitly exists.

---

# TEST DATA

Build deterministic test fixtures/factories for:

* riders
* drivers
* vehicles
* compliance records
* ride products
* pricing configurations
* geographic zones
* ride requests
* offers
* trips
* payment methods
* payment records
* refunds
* earnings
* payouts
* notifications
* support cases
* safety incidents
* risk signals
* promotions
* administrative roles

Fixtures must be isolated between tests.

Do not share mutable global test state.

---

# TEST DATA SECURITY

Never use real personal data.

Never use:

* production payment credentials
* real identity documents
* real passwords copied from production
* production tokens
* production provider secrets

Synthetic test data must be clearly identifiable.

---

# DATABASE TESTING

Validate PostgreSQL behavior using the actual database layer.

Test:

* constraints
* foreign keys
* uniqueness
* indexes
* state persistence
* transactions
* rollback
* concurrency
* pagination
* query filtering
* deletion/anonymization
* migration behavior

Do not mock Prisma for tests whose purpose is to prove database correctness.

---

# MIGRATION TESTING

Every migration must be tested against:

* a clean database
* the expected previous schema version
* representative existing data where applicable

Verify:

* migration succeeds
* constraints are preserved
* indexes exist
* data is not unintentionally lost
* application behavior remains compatible

Test migrations as part of CI where practical.

---

# AUTHENTICATION TESTING

Validate:

* registration
* login
* logout
* token expiration
* refresh
* refresh-token rotation where implemented
* revoked sessions
* account recovery
* disabled account
* suspended account
* restricted account
* malformed token
* invalid signature
* invalid audience/issuer where applicable
* session invalidation after sensitive account changes

Verify authentication is enforced consistently across:

* REST
* WebSockets
* administrative APIs

---

# AUTHORIZATION TESTING

Test every critical resource boundary.

Verify that:

* rider A cannot access rider B's rides
* rider A cannot access rider B's payment methods
* driver A cannot access driver B's offers
* driver A cannot submit driver B's location
* driver A cannot access driver B's earnings
* support users cannot execute administrator-only commands
* ordinary operators cannot execute financial-only operations
* safety personnel cannot access unrestricted data outside permission scope
* administrators cannot bypass domain-level validation

Test authorization against direct API calls, not only UI behavior.

---

# IDOR TESTING

Explicitly test insecure direct object reference scenarios.

For every externally addressable resource:

1. authenticate as user A
2. obtain a valid resource identifier belonging to user B
3. request the resource through every relevant endpoint
4. attempt mutation where applicable
5. verify access is denied or safely hidden

Include:

* users
* rides
* trips
* vehicles
* payments
* refunds
* payouts
* ratings
* support cases
* safety incidents
* promotions
* administrative resources

---

# API TESTING

Validate all major API families.

For each endpoint test:

* valid request
* malformed request
* missing required field
* invalid type
* invalid range
* unauthorized
* forbidden
* not found
* conflict
* rate limit
* dependency failure where applicable
* idempotent retry where applicable

Verify:

* HTTP status
* response schema
* error schema
* persisted state
* emitted events
* queued jobs
* authorization

---

# API CONTRACT TESTING

Compare implementation against established OpenAPI and typed contracts.

Validate:

* field names
* data types
* nullability
* required properties
* error structures
* pagination
* enums/status values
* authentication requirements

Contract tests must detect accidental breaking changes.

---

# RIDER FUNCTIONAL TESTING

Validate the rider journey end to end.

At minimum test:

1. registration/login
2. profile
3. location selection
4. destination selection
5. ride-product selection
6. fare estimate
7. promotion
8. payment method
9. ride creation
10. dispatch
11. driver assignment
12. driver location
13. driver arrival
14. trip start
15. active trip
16. completion
17. final fare
18. payment
19. receipt
20. rating
21. history
22. support
23. safety

Each stage must use real backend state.

---

# RIDER EDGE CASES

Test:

* invalid pickup
* invalid destination
* unsupported market
* unavailable product
* expired quote
* stale pricing
* no drivers
* dispatch timeout
* rider cancellation
* cancellation race
* driver cancellation
* payment-method failure
* WebSocket disconnect
* app/browser refresh
* duplicate ride creation
* network timeout after ride creation

Verify the UI and API converge on authoritative state.

---

# DRIVER FUNCTIONAL TESTING

Validate:

1. registration
2. onboarding
3. compliance submission
4. vehicle registration
5. eligibility
6. availability
7. location
8. dispatch offer
9. acceptance
10. navigation/pickup
11. arrival
12. rider verification
13. trip start
14. active trip
15. completion
16. earnings
17. payout state
18. history
19. support
20. safety

---

# DRIVER EDGE CASES

Test:

* incomplete onboarding
* expired compliance
* ineligible vehicle
* location permission denied
* stale location
* network loss
* offer expiration
* offer rejection
* duplicate acceptance
* another driver winning the ride
* trip-start conflict
* cancellation
* app restart
* background/resume
* logout while online

Verify driver state remains consistent.

---

# LOCATION TESTING

Validate:

* valid coordinates
* invalid coordinates
* impossible coordinates
* stale timestamp
* future timestamp
* duplicate update
* out-of-order update
* high-frequency updates
* unauthorized driver
* rate limiting
* stale-driver detection
* location expiration
* privacy access controls

Verify older packets cannot overwrite newer accepted state.

---

# LOCATION PRIVACY TESTING

Verify:

* rider sees only authorized driver location
* driver cannot access unrelated rider location
* ordinary support users cannot obtain unrestricted historical location
* expired ride access is revoked where required
* deleted/anonymized account data is removed or appropriately anonymized from derived systems

---

# GEOSPATIAL TESTING

Validate:

* nearby-driver discovery
* service-zone boundaries
* restricted zones
* airport zones
* market detection
* ride-product geographic eligibility
* boundary conditions

Test points:

* inside boundary
* exactly on boundary where meaningful
* outside boundary
* overlapping zones
* no matching zone

---

# DISPATCH TESTING

Validate:

* candidate discovery
* eligibility filtering
* stale-location filtering
* vehicle compatibility
* ride-product compatibility
* geographic constraints
* ranking
* offer generation
* expiration
* acceptance
* rejection
* reassignment
* exhausted candidate pool
* recovery after worker restart

---

# DISPATCH CONCURRENCY TESTING

Run actual concurrent scenarios.

At minimum:

## TWO DRIVERS ACCEPT

Two eligible drivers attempt to accept the same offer/ride at approximately the same time.

Expected:

* exactly one authoritative assignment
* one successful acceptance
* one deterministic conflict
* no duplicate trip
* no inconsistent driver availability

## ACCEPT VS CANCELLATION

Driver acceptance races against rider cancellation.

Expected:

* deterministic final state
* no duplicate assignment
* no contradictory terminal state

## DUPLICATE ACCEPTANCE

The same driver submits the same acceptance multiple times.

Expected:

* idempotent logical result
* no duplicate assignment
* no duplicate event side effect

---

# RIDE REQUEST IDEMPOTENCY

Test duplicate ride creation caused by:

* double tap
* client retry
* request timeout
* reconnect
* app/browser refresh

Verify only the intended ride request is created.

---

# RIDE STATE MACHINE TESTING

For each legal transition:

* verify success
* verify persistence
* verify event
* verify authorization
* verify idempotency

For each illegal transition:

* verify rejection
* verify state remains unchanged
* verify no incorrect event is emitted

---

# TRIP STATE MACHINE TESTING

Validate:

* assigned
* driver en route
* driver arrived
* start pending
* in progress
* completed
* canceled
* terminated

Test illegal transitions such as:

* completed → active
* canceled → started
* completed → canceled
* unrelated driver → start
* unrelated rider → cancel

---

# TRIP CONCURRENCY TESTING

Test:

* start vs cancellation
* completion vs cancellation
* duplicate start
* duplicate completion
* driver restart during transition
* rider restart during transition

Verify exactly one authoritative result.

---

# REALTIME WEBSOCKET TESTING

Validate:

* authentication
* authorization
* connection
* subscription
* unsubscribe
* heartbeat
* disconnect
* reconnect
* duplicate event
* stale event
* malformed event
* unauthorized subscription

---

# REALTIME RECOVERY TESTING

Simulate:

1. active rider trip
2. WebSocket connection lost
3. backend state changes while disconnected
4. client reconnects
5. client retrieves authoritative current state
6. client resumes live updates

Expected:

* no lost critical state
* no duplicate lifecycle transition
* no stale UI remaining permanently

---

# REALTIME AUTHORIZATION TESTING

Attempt:

* rider subscribing to another rider's trip
* rider subscribing to unrelated driver channel
* driver subscribing to another driver's offer
* logged-out user reconnecting with stale credentials
* revoked session using an existing socket

All unauthorized access must fail.

---

# EVENT TESTING

Validate event contracts for:

* type
* version
* entity ID
* event ID
* timestamp
* correlation
* trace context where applicable

Test:

* producer
* consumer
* duplicate delivery
* replay
* invalid schema
* out-of-order events where relevant
* consumer failure
* dead-letter routing

---

# EVENT IDEMPOTENCY TESTING

Deliver the same event multiple times.

Verify:

* state changes only once
* financial effects occur only once
* notification deduplication works
* search indexing remains correct
* analytics do not double-count

---

# OUTBOX TESTING

Validate:

1. business transaction succeeds
2. outbox record is created atomically
3. publisher processes event
4. consumer receives event

Also test:

* database commit with publisher failure
* publisher restart
* duplicate publish
* retry
* stale outbox records
* dead-letter handling

The business transaction must not become inconsistent with the event stream because of a publisher failure.

---

# QUEUE TESTING

Validate BullMQ jobs for:

* creation
* payload validation
* retry
* timeout
* backoff
* concurrency
* deduplication
* dead letter
* worker restart
* graceful shutdown

Test business idempotency separately from queue retry behavior.

---

# QUEUE RECOVERY TESTING

Test:

* worker crash during processing
* worker restart
* Redis interruption where test infrastructure supports it
* job timeout
* duplicate delivery
* stale delayed job

Verify critical work is neither silently lost nor applied twice.

---

# PRICING TESTING

Validate exact pricing behavior for:

* base fare
* distance
* duration
* product
* market
* fees
* minimum fare
* dynamic pricing
* promotion
* currency
* rounding
* quote expiration

Use deterministic expected values.

Do not allow floating-point precision errors to alter authoritative money.

---

# PRICING CONFIGURATION TESTING

Test:

* active configuration
* future configuration
* expired configuration
* invalid configuration
* market override
* product override
* version preservation

Verify historical quotes remain tied to the correct configuration version.

---

# PAYMENT TESTING

Use provider sandbox/test facilities where available.

Test:

* payment method creation
* payment intent
* authorization
* capture
* decline
* timeout
* unknown provider outcome
* webhook
* duplicate webhook
* refund
* partial refund
* reconciliation

Do not use real payment credentials.

---

# PAYMENT CONCURRENCY TESTING

Test:

* duplicate capture
* capture vs cancellation
* duplicate refund
* provider timeout + retry
* webhook vs API response
* reconciliation during pending payment

Verify no duplicate financial effect.

---

# EARNINGS TESTING

Validate:

* completed trip → earning
* platform fee
* adjustments
* refund impact
* duplicate earning event
* payout eligibility

Verify historical financial records remain auditable.

---

# PAYOUT TESTING

Use sandbox/test provider behavior where available.

Test:

* payout eligibility
* payout creation
* duplicate request
* provider timeout
* provider failure
* webhook
* reconciliation
* reversal/failure

Verify no duplicate payout effect.

---

# RATING TESTING

Validate:

* completed-trip eligibility
* actor relationship
* rating constraints
* duplicate rating
* review text validation
* moderation
* aggregation

A rating must never be accepted for an unrelated trip.

---

# NOTIFICATION TESTING

Test:

* event → notification
* channel selection
* user preferences
* transactional notifications
* safety notifications
* duplicate event
* retry
* permanent failure
* dead-letter
* provider callback

Verify notification failure does not roll back the underlying ride/payment/trip transaction.

---

# SAFETY TESTING

Validate:

* safety incident creation
* authorization
* trip linkage
* trusted contacts
* trip sharing
* expiration
* revocation
* escalation

Safety incident creation must remain independently functional from analytics/search systems.

---

# FRAUD/RISK TESTING

Validate:

* risk signal creation
* signal deduplication
* severity
* expiration
* assessment
* controlled enforcement
* authorization
* asynchronous processing

Verify a risk worker cannot arbitrarily mutate unrelated domain state.

---

# PROMOTION TESTING

Validate:

* eligibility
* expiration
* market
* product
* usage limits
* per-user limits
* discount caps
* duplicate application
* concurrent usage

Test concurrency around usage limits.

---

# SUPPORT TESTING

Validate:

* case creation
* role access
* lifecycle
* assignment
* linked ride/trip/payment
* customer-visible content
* internal notes
* authorized domain commands

Verify support cannot bypass domain authorization.

---

# ADMINISTRATION TESTING

Test:

* authentication
* permissions
* role-based navigation
* operational search
* investigation
* refund
* driver restriction
* compliance action
* payout investigation
* safety action
* configuration change
* feature-flag change
* audit generation

Every privileged mutation must create the expected audit trail.

---

# AUDIT TESTING

Verify audit records include appropriate:

* actor
* action
* target
* timestamp
* result
* reason
* correlation/request ID

Verify sensitive secrets are absent.

Verify unauthorized users cannot read privileged audit data.

---

# SEARCH TESTING

Validate:

* index creation
* indexing
* update
* deletion
* eventual consistency
* permission filtering
* stale-result behavior
* reindex
* rebuild

Before mutation:

* use search result
* retrieve authoritative state
* execute domain command

Verify stale search cannot cause an invalid administrative action.

---

# ANALYTICS TESTING

Validate:

* event ingestion
* aggregation
* deduplication
* event replay
* time windows
* market filters
* product filters

Verify analytics cannot alter transactional state.

---

# DATA PRIVACY TESTING

Validate:

* account deletion
* anonymization
* session revocation
* cache invalidation
* search cleanup
* notification cleanup
* derived-data cleanup
* export authorization
* export expiration

Confirm retained financial/audit information follows the defined policy without unnecessary private-data exposure.

---

# DATA EXPORT TESTING

Test:

* authorization
* scope
* asynchronous job
* private object storage
* expiration
* repeated request
* download authorization
* account-deletion interaction

Do not expose permanent public URLs.

---

# FRONTEND TESTING

Validate the web application using real backend contracts.

Test:

* route protection
* authentication
* booking
* estimates
* ride request
* dispatch
* active trip
* realtime
* history
* payments
* notifications
* support
* safety
* scheduled rides
* operations
* administrative search
* configuration
* audit

Verify loading, empty, error, conflict, and recovery states.

---

# FRONTEND STATE TESTING

Verify server-state synchronization after:

* mutation
* realtime event
* reconnect
* refresh
* logout
* account switch

Verify stale data cannot remain indefinitely after authoritative mutation.

---

# FRONTEND SECURITY TESTING

Test:

* unauthorized routes
* direct URL access
* IDOR through route parameters
* open redirects
* unsafe rich text
* cache isolation
* token exposure
* sensitive analytics payloads
* privileged route access

Do not consider route hiding sufficient.

---

# MOBILE TESTING

Validate actual rider and driver mobile applications.

Test:

* authentication
* secure storage
* navigation
* booking
* active trip
* driver offer
* driver acceptance
* trip lifecycle
* push notifications
* deep links
* app restart
* background/resume
* offline
* reconnect
* location permissions
* driver background location
* earnings
* payouts
* support
* safety

Use real backend contracts.

---

# MOBILE ACCOUNT ISOLATION

Test:

1. authenticate account A
2. populate active state
3. logout
4. authenticate account B
5. verify no account A state remains

Include:

* query caches
* navigation
* push data
* WebSocket subscriptions
* local state
* active-trip state

---

# MOBILE LOCATION TESTING

On real or controlled devices test:

* permission granted
* denied
* revoked
* foreground
* background
* locked device
* app restart
* network loss
* network recovery
* logout
* driver offline

Verify location stops when it should.

---

# PUSH AND DEEP-LINK TESTING

Test:

* token registration
* token refresh
* logout/unregistration
* foreground notification
* background notification
* duplicate notification
* notification tap
* authenticated deep link
* unauthorized deep link
* expired resource
* malformed link

---

# ACCESSIBILITY TESTING

Validate the actual user interfaces for:

* keyboard navigation
* screen readers
* forms
* dialogs
* live status
* error messages
* tables
* charts
* mobile dynamic text
* touch targets
* reduced motion

Critical workflows include:

* booking
* active trip
* driver offer
* support
* safety
* administrative operations

---

# CROSS-CLIENT CONSISTENCY

Validate that a state change made through one client is correctly reflected in other authorized clients.

Examples:

* rider cancels via web → mobile reflects canceled state
* driver accepts via mobile → rider web reflects assignment
* admin cancels ride → rider/driver clients reconcile
* payment completes via webhook → web/mobile reflect final state
* compliance approval changes → driver app reflects eligibility

Do not require a client refresh manually where realtime/invalidations should provide the update.

---

# REGRESSION TESTING

Establish regression suites around business-critical flows.

At minimum preserve automated coverage for:

* authentication
* ride creation
* dispatch
* assignment
* trip lifecycle
* payment
* payout
* notifications
* safety
* driver availability
* location

Every production bug discovered during QA must result in:

* a regression test
* a documented failure mode
* remediation where required

---

# TEST FLAKINESS

Do not hide flaky tests.

For every flaky test:

* identify root cause
* distinguish application race from test race
* make synchronization deterministic
* remove timing assumptions
* avoid arbitrary sleeps

Do not mark tests as skipped simply because they are inconvenient.

A test may be skipped only for a documented environmental limitation with an explicit remediation path.

---

# TEST ISOLATION

Tests must:

* reset state
* use isolated identifiers
* avoid ordering dependency
* avoid shared mutable fixtures
* clean temporary files
* clean queues/topics where practical
* clean database state

Do not rely on tests executing in a specific order unless the test framework explicitly models the dependency.

---

# DETERMINISTIC TESTING

Avoid:

* real-time sleeps
* uncontrolled random values
* current-time dependence without injection
* external production services
* nondeterministic provider responses

Use controllable:

* clocks
* IDs
* provider responses
* queue scheduling
* geographic fixtures

where appropriate.

---

# TEST OBSERVABILITY

Test infrastructure itself must produce actionable diagnostics.

On failure capture, where appropriate:

* request/correlation ID
* relevant logs
* database state
* queue state
* event identifiers
* screenshots
* mobile/device logs
* browser console
* trace references

Do not capture secrets.

---

# TEST REPORTING

Generate machine-readable and human-readable test results.

Include:

* test suite
* environment
* commit/revision
* start/end
* passed
* failed
* skipped
* flaky
* duration

Failed tests must identify the affected domain.

---

# CI TEST GATES

Establish appropriate CI gates.

At minimum:

* formatting
* linting
* type checking
* unit tests
* integration tests
* API tests
* contract tests
* frontend tests
* mobile tests where CI environment permits
* E2E smoke tests

Do not make every expensive stress/DR test a mandatory per-commit gate if it would make the development loop impractical; separate execution frequency appropriately while preserving coverage.

---

# TEST ENVIRONMENT CLEANUP

Ensure automated test runs do not leave:

* orphaned containers
* test databases
* unbounded queues
* temporary object files
* leaked credentials
* stale Kubernetes resources

Cleanup must execute even after test failure.

---

# QUALITY GATES

Before considering this QA volume complete, verify:

* critical unit coverage exists
* database integration tests pass
* API tests pass
* contract tests pass
* event tests pass
* queue tests pass
* WebSocket tests pass
* rider E2E passes
* driver E2E passes
* frontend critical flows pass
* mobile critical flows pass
* accessibility baseline passes
* migration tests pass
* regression suite passes

A test suite passing is not sufficient if it proves only mocked behavior.

---

# DEFECT MANAGEMENT

For each discovered defect record:

* unique identifier
* severity
* affected component
* affected environment
* reproduction steps
* expected result
* actual result
* evidence
* related test
* remediation status

Critical correctness/security defects must block release qualification unless explicitly accepted through a documented production decision process.

Do not hide defects by weakening the test.

---

# SEVERITY MODEL

Use a consistent severity model based on actual impact.

Examples:

## CRITICAL

* double charge
* duplicate payout
* duplicate ride assignment
* authentication bypass
* unauthorized private-data access
* active-trip state corruption

## HIGH

* core ride flow unavailable
* dispatch broadly failing
* driver location unavailable during active trips
* payment processing broadly failing
* safety workflow unavailable

## MEDIUM

* significant noncritical workflow degradation
* incorrect nonauthoritative display
* limited administrative functionality

## LOW

* cosmetic issue
* noncritical usability issue
* minor documentation/UI inconsistency

Do not reduce severity simply because reproduction is difficult.

---

# RELEASE BLOCKERS

The following must block production qualification unless formally resolved or explicitly accepted by authorized stakeholders:

* duplicate financial effects
* duplicate active ride assignment
* authorization bypass
* sensitive-data exposure
* broken trip state machine
* unrecoverable active-trip state
* unsafe migration
* unverified payment uncertainty handling
* critical safety workflow failure
* widespread notification of incorrect trip state
* data corruption
* unrecoverable queue/event loss

---

# QA IMPLEMENTATION DISCIPLINE

Before changing tests:

1. Inspect the repository.
2. Identify current test coverage.
3. Identify coverage gaps.
4. Build deterministic fixtures.
5. Add missing unit tests.
6. Add integration tests.
7. Add API tests.
8. Add contract tests.
9. Add database/migration tests.
10. Add event tests.
11. Add queue tests.
12. Add WebSocket tests.
13. Add frontend tests.
14. Add mobile tests.
15. Add critical E2E tests.
16. Add accessibility coverage.
17. Add regression tests.
18. Validate CI execution.
19. Analyze failures.
20. Fix actual defects discovered.
21. Re-run affected and regression suites.
22. Document remaining defects.
23. Produce the required QA report.

Do not modify production code merely to make tests pass without understanding the underlying defect.

---

# PRODUCTION CODE DEFECTS

When QA discovers a real production-code defect:

* identify the root cause
* implement the smallest correct fix within the appropriate repository boundary
* add a regression test
* validate related workflows
* review for compatibility

Do not:

* weaken assertions
* remove the test
* hardcode test-specific behavior
* add hidden test bypasses

---

# PROHIBITED TEST PRACTICES

Never:

* mock away the behavior under test
* treat a successful HTTP status as proof of business correctness
* skip concurrency tests for critical invariants
* use production credentials
* use real customer data
* disable security validation
* ignore flaky tests
* use arbitrary sleeps as synchronization
* make tests depend on execution order
* silently skip failing suites
* declare recovery functionality tested when only configuration was checked
* claim load/resilience behavior from unit tests
* certify functionality that remains simulated

---

# IMPLEMENTATION BOUNDARIES

This volume performs comprehensive functional and integration qualification.

It does not constitute the final performance, security, resilience, disaster-recovery, or release-qualification phase.

The next QA volume will perform:

* performance
* load
* stress
* security
* resilience
* failure
* backup/restore
* disaster recovery
* deployment validation
* production-release qualification

Do not create an additional unplanned QA phase beyond the established QA sequence.

---

# REQUIRED QA DELIVERABLES

Implement or update:

## TEST INFRASTRUCTURE

* deterministic test environment
* fixtures/factories
* test containers/services
* cleanup
* test configuration
* reporting

## BACKEND

* unit
* integration
* API
* database
* migration
* contract
* event
* queue
* WebSocket

## CORE BUSINESS FLOWS

* rider
* driver
* dispatch
* trip
* pricing
* payment
* earnings
* payout
* rating
* notifications
* safety
* risk
* support
* promotions
* administration

## CLIENTS

* frontend
* rider mobile
* driver mobile

## END-TO-END

* rider journey
* driver journey
* cross-client synchronization
* critical recovery flows

## QUALITY

* accessibility
* regression
* defect tracking
* CI gates
* diagnostics

---

# REQUIRED VALIDATION

Execute and report, as applicable:

* unit tests
* integration tests
* API tests
* contract tests
* database tests
* migration tests
* event tests
* queue tests
* WebSocket tests
* frontend tests
* mobile tests
* E2E tests
* accessibility tests
* regression suite

Do not report a suite as passed if it was not actually executed.

---

# REQUIRED COMPLETION STANDARD

This QA volume is complete only when:

* critical user journeys execute successfully
* critical backend invariants are tested
* database constraints are verified
* API contracts are verified
* event and queue behavior is verified
* realtime recovery is verified
* rider flows are verified
* driver flows are verified
* frontend critical flows are verified
* mobile critical flows are verified
* accessibility baseline is verified
* regression coverage is established
* discovered critical defects are resolved or explicitly reported
* the test environment is reproducible
* CI integration is validated

A green test pipeline alone does not prove quality.

The tests must provide meaningful evidence that the actual platform behavior is correct.

---

# COMPLETION REPORT REQUIREMENTS

When QA work is complete, report:

## FILES CREATED

List every new test file, fixture, factory, utility, configuration, or QA document.

## FILES MODIFIED

List every modified test, application, configuration, or documentation file.

## TEST INFRASTRUCTURE

Report:

* test environments
* fixtures
* factories
* containers
* service dependencies
* cleanup strategy
* reporting

## BACKEND TESTING

Report:

* unit
* integration
* API
* database
* migration
* contract
* event
* queue
* WebSocket

## RIDER VALIDATION

Report the complete rider workflows tested.

## DRIVER VALIDATION

Report the complete driver workflows tested.

## DISPATCH AND TRIP

Report:

* candidate selection
* offers
* concurrency
* assignment
* state transitions
* cancellation
* recovery

## FINANCIAL

Report:

* pricing
* payment
* refund
* earnings
* payout
* idempotency
* webhook/reconciliation coverage

## CLIENT VALIDATION

Report:

* web
* rider mobile
* driver mobile
* realtime
* push
* deep links
* account isolation

## ACCESSIBILITY

Report:

* web accessibility
* mobile accessibility
* critical workflow validation

## REGRESSION

Report:

* regression suites
* production defects converted to regression tests
* recurring test execution

## CI

Report:

* gates
* test commands
* artifacts
* reports
* environment setup

## DEFECTS

Report:

* critical
* high
* medium
* low
* resolved
* unresolved
* release blockers

## VALIDATION

Report:

* tests actually executed
* pass/fail counts
* skipped tests
* flaky tests
* execution environments
* representative browser/device coverage

Do not claim success for tests that were not executed.

## UNRESOLVED ISSUES

List only genuine remaining QA issues or test-environment limitations.

---

# FINAL ENGINEERING PRINCIPLE

QA must establish evidence that the ride-hailing platform works as one system rather than as a collection of individually passing components.

The highest priority is validating the business invariants that cannot be compromised:

* one ride cannot be assigned to two drivers
* one driver cannot hold conflicting active assignments
* duplicate commands cannot create duplicate business effects
* financial operations cannot execute twice
* unauthorized users cannot access private data
* stale or out-of-order location cannot corrupt current state
* trip state cannot transition illegally
* realtime disconnects cannot permanently lose authoritative state
* queue/event replay cannot duplicate critical effects
* account deletion cannot expose retained private data
* safety workflows must remain independently usable
* clients must converge on backend-authoritative state

Test actual integrations.

Test actual persistence.

Test actual concurrency.

Test actual authorization.

Test actual recovery from ordinary failures.

Test the rider and driver experiences end to end.

Do not certify behavior that is represented only by mocks or placeholders.

The repository remains the implementation source of truth.

The next QA volume must build on this functional/integration qualification and focus exclusively on advanced non-functional, resilience, security, performance, disaster-recovery, and production-release validation.
