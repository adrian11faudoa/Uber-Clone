# UBER-STYLE RIDE-HAILING PLATFORM — QA PROMPT — VOLUME 2

## ROLE

You are the senior quality engineering organization responsible for performing the final non-functional, security, resilience, performance, disaster-recovery, deployment, and production-release qualification of a globally scalable ride-hailing and mobility marketplace comparable in product depth and operational sophistication to Uber.

Operate as a coordinated team consisting of:

* Principal Software Architect
* QA Engineer
* Staff Backend Engineer
* Staff Frontend Engineer
* Staff Mobile Engineer
* Database Architect
* Distributed Systems Engineer
* Security Engineer
* DevOps Engineer
* Cloud Architect
* Performance Engineer
* Reliability Engineer
* UI/UX Engineer
* Technical Writer

You are performing production qualification against the existing repository and the actual deployed test/staging infrastructure.

You are not creating a tutorial, theoretical performance report, simulated security review, or checklist that merely claims resilience.

The objective is to produce measurable evidence that the complete platform can withstand realistic production workloads, malicious inputs, dependency failures, infrastructure failures, deployment changes, data recovery operations, and regional incidents while preserving its critical business invariants.

The repository is the source of truth for the implementation being qualified.

Do not assume another AI prompt, previous conversation, or previous QA report is available.

---

# PROJECT

Perform advanced production qualification of the complete Uber-style ride-hailing platform across:

* rider web
* operations/admin web
* rider mobile
* driver mobile
* NestJS backend
* REST APIs
* WebSockets
* PostgreSQL
* Redis
* Kafka/event streaming
* BullMQ
* dispatch
* geospatial processing
* pricing
* payments
* refunds
* earnings
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
* AWS infrastructure
* Kubernetes
* Terraform
* Helm
* CI/CD
* observability
* backup and restore
* disaster recovery

This volume is responsible for:

* performance testing
* load testing
* stress testing
* spike testing
* soak testing
* concurrency validation
* resilience testing
* failure injection
* security testing
* penetration-oriented validation
* abuse testing
* accessibility hardening validation
* backup/restore testing
* disaster-recovery testing
* deployment validation
* rollback validation
* infrastructure qualification
* mobile device qualification
* release qualification
* production readiness assessment

Do not repeat the functional/integration testing strategy already established in the previous QA volume except where a functional assertion is required to prove a non-functional property.

---

# SOURCE OF TRUTH

Before executing advanced QA:

Inspect:

* current test suites
* CI/CD workflows
* Docker and Kubernetes configuration
* Terraform
* Helm
* AWS staging/test infrastructure
* production-like database sizing
* Redis configuration
* Kafka configuration
* BullMQ workers
* WebSocket gateways
* API replicas
* frontend build/deployment
* mobile builds
* observability
* dashboards
* alerts
* SLO definitions
* backup configuration
* restoration procedures
* security controls
* network policies
* IAM
* WAF
* secrets management
* certificates
* DNS
* autoscaling

Use actual deployed configuration for qualification.

Do not certify production behavior based solely on static configuration review.

---

# QA SCOPE

This volume owns:

* non-functional validation
* security validation
* scalability validation
* availability validation
* resilience validation
* recovery validation
* deployment validation
* production-release qualification

It must validate the interaction among:

* application
* database
* cache
* event streaming
* queues
* realtime
* infrastructure
* external dependencies
* clients

The tests must be representative of realistic production behavior.

---

# TEST ENVIRONMENT

Use a controlled staging or dedicated production-like environment.

The environment must provide:

* realistic topology
* representative application replicas
* production-like database configuration
* production-like Redis
* production-like Kafka
* production-like queue workers
* production-like WebSocket topology
* production-like observability
* realistic network paths
* safe test provider accounts

Do not use production customer data.

Do not execute destructive experiments in production unless a specific production-safe exercise has been authorized and technically isolated.

---

# TEST DATA SCALE

Generate realistic synthetic datasets for:

* users
* riders
* drivers
* vehicles
* active locations
* ride requests
* trips
* historical trips
* payments
* payouts
* notifications
* support cases
* risk signals
* promotions

The dataset must be large enough to expose:

* indexing problems
* memory problems
* connection saturation
* queue growth
* Kafka lag
* hot keys
* pagination failures
* search degradation

Do not use unrealistic single-record fixtures for capacity testing.

---

# PERFORMANCE TESTING PRINCIPLES

Measure actual system behavior.

For every major test record:

* workload
* concurrency
* throughput
* latency
* p50
* p95
* p99
* error rate
* saturation
* resource utilization
* queue/event lag
* database behavior
* Redis behavior

Do not report only average latency.

A system may have acceptable average performance while severe tail latency affects users.

---

# PERFORMANCE BASELINES

Establish baseline measurements for:

* authentication
* rider profile
* fare estimate
* ride creation
* nearby-driver discovery
* dispatch
* driver acceptance
* active-trip retrieval
* location ingestion
* WebSocket messaging
* trip transitions
* payment initiation
* payment webhook processing
* earnings queries
* payout queries
* notification processing
* administrative search

Record the environment and configuration used for the baseline.

---

# API LOAD TESTING

Load test critical API paths independently.

At minimum:

* authentication
* rider profile
* fare estimate
* ride creation
* active trip
* location ingestion
* driver offer
* offer acceptance
* trip transitions
* payment endpoints
* notification endpoints
* search
* administrative APIs

The workload must include realistic read/write ratios.

Do not overload only one endpoint while claiming the platform was load tested.

---

# RIDE REQUEST LOAD

Simulate realistic marketplace demand.

Include:

* normal demand
* commuting peaks
* geographic demand concentration
* sudden demand increases
* uneven city activity

Measure:

* request latency
* dispatch backlog
* match latency
* database load
* Redis load
* Kafka throughput
* queue depth

Verify low-demand regions are not starved by high-demand regions.

---

# DISPATCH LOAD TESTING

Simulate:

* large online driver populations
* high rider request volume
* stale drivers
* rejected offers
* expired offers
* driver churn
* geographic hotspots

Measure:

* candidate discovery latency
* ranking latency
* assignment latency
* offers per second
* acceptance throughput
* worker utilization
* Redis operations
* PostgreSQL contention

Verify dispatch continues to enforce assignment uniqueness under load.

---

# LOCATION LOAD TESTING

Generate realistic driver-location traffic.

Test:

* normal sampling
* elevated update frequency
* dense city center
* large active fleet
* sudden fleet concentration
* reconnect storms

Measure:

* ingestion throughput
* latency
* Redis CPU/memory
* network bandwidth
* dropped/rejected updates
* stale-location rate

Verify location traffic does not exhaust core API capacity.

---

# WEBSOCKET LOAD TESTING

Test:

* thousands to large numbers of concurrent connections appropriate to the staging environment
* driver offer fan-out
* rider active-trip updates
* driver location updates
* reconnect storms
* pod termination
* gateway scaling

Measure:

* connection count
* connection churn
* message latency
* message throughput
* CPU
* memory
* event-loop latency
* reconnect success

Verify horizontal scaling does not produce inconsistent subscriptions or duplicate state.

---

# MOBILE NETWORK CONDITIONS

Test mobile behavior under:

* high latency
* packet loss
* intermittent connectivity
* airplane mode
* Wi-Fi/mobile-network transitions
* bandwidth constraints

Verify:

* safe mutation handling
* reconnect
* state reconciliation
* location recovery
* push behavior
* active-trip recovery

Do not assume reliable mobile connectivity.

---

# DATABASE LOAD TESTING

Test PostgreSQL under realistic production-like workloads.

Measure:

* transactions per second
* query latency
* connection count
* CPU
* memory
* IOPS
* lock contention
* deadlocks
* replication lag
* storage growth

Focus on hot paths:

* active rides
* dispatch assignments
* trip transitions
* payments
* payouts
* location metadata
* administrative search references

---

# DATABASE CONCURRENCY TESTING

Run high-concurrency transactions around:

* ride creation
* driver acceptance
* rider cancellation
* trip start
* trip completion
* payment capture
* refund
* payout
* promotion usage

Verify:

* no duplicate business effects
* no lost updates
* no invalid states
* bounded lock contention
* acceptable latency

---

# REDIS LOAD TESTING

Test:

* location operations
* geospatial queries
* rate limiting
* cache operations
* ephemeral state
* connection pressure

Measure:

* operations/second
* latency
* memory
* evictions
* hot keys
* CPU
* connection count

Verify high-frequency location traffic cannot starve authentication/rate-limit/cache operations.

---

# KAFKA LOAD TESTING

Test:

* event production
* event consumption
* replay
* high-volume location/operational events where applicable
* financial event processing

Measure:

* throughput
* partition utilization
* consumer lag
* rebalance duration
* processing latency
* dead-letter volume

Verify consumers maintain correctness when lag increases.

---

# QUEUE LOAD TESTING

Test BullMQ under:

* normal traffic
* backlog
* burst load
* slow providers
* worker scaling
* worker failure

Measure:

* queue depth
* oldest job age
* throughput
* retry amplification
* worker utilization
* dead letters

Ensure critical queues remain isolated from low-priority work.

---

# SEARCH LOAD TESTING

Test:

* administrative search
* concurrent search users
* large result sets
* complex but supported filters
* reindexing
* index failure/recovery

Measure:

* latency
* throughput
* cluster health
* shard utilization
* index lag

Verify transactional operations remain healthy while search is degraded.

---

# EXTERNAL PROVIDER LOAD PROTECTION

Validate behavior when:

* map provider latency increases
* payment provider latency increases
* notification provider latency increases
* payout provider latency increases

Verify:

* bounded concurrency
* timeouts
* backpressure
* retries
* circuit-breaking where applicable
* queue protection

Do not allow an external provider to exhaust all application worker capacity.

---

# SPIKE TESTING

Simulate abrupt demand changes such as:

* major commute start
* event ending
* severe weather-style demand spike
* large fleet reconnect
* mass application reconnect
* push-notification storm
* WebSocket reconnect storm

Measure:

* autoscaling response
* queue backlog
* API latency
* dispatch degradation
* recovery time

The system must fail predictably rather than collapse through cascading overload.

---

# STRESS TESTING

Increase workload beyond expected normal peak until a controlled capacity boundary is identified.

Determine:

* first bottleneck
* saturation point
* failure mode
* graceful-degradation behavior
* maximum safe throughput
* recovery behavior

Do not simply continue until the system crashes without monitoring.

---

# SOAK TESTING

Run representative workload continuously for an extended period sufficient to reveal:

* memory leaks
* connection leaks
* queue drift
* Kafka lag accumulation
* database growth
* Redis fragmentation
* resource exhaustion
* telemetry overload
* degraded latency

Compare beginning and ending system state.

---

# AUTOSCALING VALIDATION

Verify scaling behavior for:

* API
* WebSocket
* location ingestion
* dispatch
* BullMQ
* Kafka consumers
* notification workers

Measure:

* scale-up trigger
* scale-up duration
* new-capacity readiness
* scale-down
* workload recovery
* connection stability

Do not accept autoscaling that causes oscillation or excessive churn.

---

# CAPACITY LIMITS

For each critical workload determine:

* sustained throughput
* peak throughput
* safe operating range
* hard saturation point
* scaling ceiling

Document assumptions and environment.

Do not present staging capacity as exact production capacity without qualification.

---

# SECURITY TESTING PRINCIPLES

Perform security testing against the actual deployed application and APIs.

Test:

* authentication
* authorization
* IDOR
* injection
* XSS
* CSRF where applicable
* SSRF boundaries
* file upload
* webhook security
* rate limiting
* session management
* token handling
* administrative access
* WebSocket authorization
* abuse controls

Use safe test payloads.

Do not perform destructive exploitation.

---

# AUTHENTICATION SECURITY

Test:

* brute-force resistance
* credential-stuffing resistance
* rate limits
* session fixation
* session revocation
* refresh-token replay
* token expiration
* malformed tokens
* algorithm confusion where applicable
* issuer/audience validation
* account enumeration

Verify security controls remain effective under concurrent attack traffic.

---

# AUTHORIZATION SECURITY

Test horizontal and vertical escalation.

Examples:

* rider → rider
* rider → driver
* rider → admin
* driver → driver
* support → finance
* operations → administrator

Attempt direct API and WebSocket access.

Authorization must remain server-enforced.

---

# INJECTION TESTING

Test relevant inputs for:

* SQL injection
* NoSQL injection where applicable
* command injection
* template injection
* header injection
* log injection
* path traversal

Include:

* search
* administrative filters
* support fields
* uploaded filenames
* webhook data
* user-generated content

---

# XSS TESTING

Test:

* profile fields
* support messages
* reviews
* administrative notes
* promotion fields
* notification content

Verify browser output remains safely encoded/sanitized.

---

# CSRF TESTING

Where browser authentication relies on cookies, validate:

* CSRF tokens/defenses
* origin checks
* same-site configuration

Verify state-changing operations cannot be triggered cross-origin.

---

# SSRF TESTING

Identify backend functionality that accepts URLs or fetches remote content.

Test against:

* internal addresses
* metadata endpoints
* loopback
* private IP ranges
* unexpected protocols

Verify network egress protections complement application validation.

---

# FILE-UPLOAD SECURITY

Test:

* MIME spoofing
* malicious extensions
* oversized files
* corrupt files
* archive abuse
* path traversal
* executable content
* malicious metadata

Verify:

* authorization
* size limits
* content validation
* malware controls where implemented
* private object storage

---

# WEBHOOK SECURITY

Test:

* invalid signature
* replay
* malformed payload
* duplicate event
* unexpected event type
* altered provider identifier
* oversized body
* timing anomalies where applicable

Verify invalid webhooks cannot mutate financial state.

---

# WEBSOCKET SECURITY

Test:

* unauthenticated connection
* expired token
* revoked token
* unauthorized subscription
* subscription enumeration
* message flooding
* oversized messages
* malformed messages
* reconnect abuse
* cross-user channel access

Verify rate limits and connection controls.

---

# RATE-LIMIT TESTING

Test limits under:

* normal traffic
* attack traffic
* distributed requests
* multiple devices
* authenticated and unauthenticated sources

Validate that rate-limit bypass is not possible through simple changes to:

* IP
* headers
* user identifier
* device identifier
* endpoint aliases

Do not over-block legitimate high-volume location traffic without preserving operational requirements.

---

# ABUSE TESTING

Test:

* ride spam
* cancellation spam
* promotion abuse
* login abuse
* notification abuse
* support abuse
* payout abuse
* location spoof indicators
* enumeration

Verify controls are observable and do not create unauthorized state changes.

---

# PAYMENT SECURITY TESTING

Validate:

* payment authorization boundaries
* amount manipulation
* currency manipulation
* payment IDOR
* duplicate captures
* refund authorization
* webhook forgery
* provider reference manipulation

A client must never be able to change the authoritative amount of a payment.

---

# PAYOUT SECURITY TESTING

Test:

* driver ownership
* payout account authorization
* amount manipulation
* duplicate payout
* admin privilege boundaries
* provider-reference substitution

Verify no client-controlled value can create an unauthorized payout.

---

# DATA EXPOSURE TESTING

Search responses, logs, traces, analytics, mobile storage, and notifications for:

* tokens
* passwords
* payment credentials
* private documents
* unnecessary exact location
* internal risk scores
* support notes
* sensitive administrative data

Use automated secret/data scanning where appropriate.

---

# MOBILE SECURITY VALIDATION

Test real applications for:

* insecure token storage
* debug builds in production configuration
* sensitive data in logs
* deep-link bypass
* screenshot leakage where protected
* clipboard exposure
* exported Android components
* insecure iOS/Android permissions
* unsafe WebView behavior where used

Do not treat source-code review as the only mobile security validation.

---

# SECURITY PERFORMANCE

Security controls must remain effective under load.

Validate:

* auth rate limits
* WAF behavior
* API limits
* WebSocket limits
* upload controls

Do not allow protection mechanisms to become trivial denial-of-service targets.

---

# RESILIENCE TESTING PRINCIPLES

Inject controlled failures into non-production environments.

For every failure test verify:

* detection
* containment
* graceful degradation
* state integrity
* recovery
* observability

The most important invariant is preservation of authoritative state.

---

# POD FAILURE

Terminate application pods during:

* ride request
* dispatch
* active trip
* payment
* worker processing

Verify:

* Kubernetes replaces capacity
* clients reconnect where applicable
* transactions recover
* jobs are retried safely
* no duplicate business effect occurs

---

# NODE FAILURE

Simulate node loss for:

* API
* WebSocket
* workers

Verify:

* workloads reschedule
* traffic continues
* capacity returns
* active sockets reconnect

---

# WORKER FAILURE

Terminate workers while processing:

* notification
* payment reconciliation
* payout
* dispatch
* scheduled ride
* analytics

Verify:

* jobs recover
* duplicate effects are prevented
* state remains consistent

---

# REDIS FAILURE

Simulate failover or temporary unavailability.

Verify:

* authoritative PostgreSQL state remains intact
* caches rebuild
* location can recover
* rate limiting degrades according to design
* dispatch does not create duplicate assignments
* active trips remain authoritative

---

# POSTGRESQL FAILOVER

Execute a controlled managed-database failover.

Verify:

* application detects connection failure
* safe requests recover
* connection pools reconnect
* workers reconnect
* event/outbox processing resumes
* no duplicate financial effects occur

Record recovery time.

---

# KAFKA FAILURE

Simulate:

* broker interruption where safe
* consumer restart
* consumer lag
* producer failure

Verify:

* transactional state remains intact
* outbox backlog grows safely
* consumers recover
* replay works
* no duplicate financial side effects occur

---

# QUEUE FAILURE

Test:

* Redis-backed worker interruption
* worker restart
* delayed-job recovery
* failed jobs
* dead letters

Verify critical work is not silently lost.

---

# SEARCH FAILURE

Simulate:

* index unavailable
* node failure
* indexing backlog

Verify:

* transactional APIs remain available
* admin workflows clearly indicate search degradation
* indexes rebuild successfully
* stale search cannot cause harmful mutations

---

# OBJECT STORAGE FAILURE

Test upload/download failures.

Verify:

* private data remains private
* temporary failures do not corrupt transactional state
* retries are bounded
* user-facing behavior is clear
* cleanup/recovery works

---

# EXTERNAL PROVIDER FAILURE

Simulate:

* maps unavailable
* payment timeout
* notification outage
* payout outage

Verify:

* timeout
* controlled degradation
* queueing where appropriate
* reconciliation
* alerting
* no cascading failure

---

# CASCADING FAILURE TESTING

Test combinations such as:

* Redis degradation + high location load
* map latency + high dispatch load
* payment latency + trip completion spike
* Kafka lag + queue backlog
* database saturation + admin search load

Verify the platform sheds noncritical work before compromising critical business state.

---

# BACKPRESSURE VALIDATION

Verify:

* bounded queues
* worker concurrency
* provider request limits
* location sampling behavior
* API rate limits
* graceful degradation

The system must not convert overload into unbounded memory growth.

---

# DATA CORRUPTION TESTING

Use controlled fault injection to verify detection of:

* orphaned records
* invalid state combinations
* missing events
* stale indexes
* inconsistent derived state

Verify reconciliation detects rather than silently ignores inconsistencies.

---

# BACKUP TESTING

Test restoration of:

* PostgreSQL
* required object storage data
* configuration
* infrastructure state where applicable

Verify:

* data integrity
* schema compatibility
* application connectivity
* authorization
* derived-system rebuild

---

# POSTGRESQL RESTORE TEST

Perform an actual restore into an isolated environment.

Validate:

1. backup selected
2. restore completed
3. schema validated
4. expected data present
5. indexes present
6. application connects
7. critical queries execute
8. financial records remain consistent
9. audit data remains available

Record actual recovery time.

---

# OBJECT STORAGE RESTORE TEST

Restore/version-recover representative:

* compliance artifacts
* receipts
* support attachments
* exports

Verify:

* access controls
* encryption
* object integrity
* lifecycle policy behavior

---

# DISASTER RECOVERY TESTING

Execute controlled regional or environment-level recovery exercises where infrastructure permits.

Validate:

* traffic failover
* application startup
* database access
* cache rebuild
* Kafka recovery
* queue recovery
* object storage
* DNS
* TLS
* WebSocket reconnection
* mobile reconnection
* active-trip state recovery
* payment reconciliation

---

# REGIONAL FAILURE

Where a multi-region architecture exists or a DR environment is available, simulate loss of the primary region.

Verify:

* routing changes
* service startup
* state recovery
* event recovery
* cache recovery
* client behavior
* operational visibility

Do not claim active-active recovery unless concurrent regional writes have actually been validated.

---

# ACTIVE-TRIP RECOVERY

The most important DR functional scenario is an active trip.

Test:

1. rider has active trip
2. driver has active trip
3. primary service/region fails
4. recovery environment becomes authoritative
5. rider reconnects
6. driver reconnects
7. current trip state is recovered
8. location resumes
9. trip can continue or terminate safely
10. final financial state remains correct

---

# FINANCIAL DISASTER RECOVERY

Validate:

* payment state
* refund state
* earnings
* payout state
* reconciliation

after recovery.

Verify no financial transaction is duplicated during replay/recovery.

---

# DISASTER-RECOVERY RPO/RTO

Measure actual:

* RPO
* RTO

for each critical system.

Compare results against defined targets.

Do not mark a target as satisfied merely because the architecture claims to support it.

---

# DEPLOYMENT VALIDATION

Test production-style releases.

Validate:

* rolling deployment
* canary where configured
* readiness
* graceful shutdown
* database compatibility
* event compatibility
* worker compatibility
* WebSocket compatibility
* mobile compatibility

---

# ZERO-DOWNTIME DEPLOYMENT TESTING

Where zero/minimal downtime is claimed:

1. maintain active traffic
2. deploy new version
3. observe old/new version coexistence
4. execute critical workflows
5. verify no failed requests beyond accepted thresholds
6. verify WebSocket reconnection behavior
7. verify jobs continue safely

---

# DATABASE MIGRATION DEPLOYMENT TESTING

Test:

* expand migration
* mixed-version application
* deployment
* backfill where relevant
* contract compatibility
* contract removal

Verify older application replicas remain functional during safe migration phases.

---

# ROLLBACK TESTING

Perform an actual rollback.

Validate:

* application rollback
* configuration rollback
* traffic restoration
* WebSocket behavior
* worker recovery
* event compatibility
* database compatibility

Do not perform unsafe database rollback merely to satisfy a test.

For irreversible schema changes, validate forward recovery/compensating migration instead.

---

# BAD-RELEASE TESTING

Introduce a controlled defect into a staging release.

Verify:

* monitoring detects it
* alert triggers
* rollback works
* business state remains correct
* incident evidence is available

---

# MOBILE RELEASE VALIDATION

Validate:

* production build configuration
* signing
* push
* deep links
* API endpoints
* WebSockets
* permissions
* background location
* staged rollout compatibility

Verify older mobile versions remain compatible with supported backend compatibility windows.

---

# ACCESSIBILITY FINAL VALIDATION

Perform comprehensive accessibility validation across:

* rider web
* operations web
* rider mobile
* driver mobile

Validate:

* keyboard
* screen readers
* dynamic text
* touch targets
* focus
* error communication
* charts
* tables
* live trip status
* safety controls

Critical transportation workflows must remain accessible.

---

# PERFORMANCE REGRESSION

Compare new/current builds against established baselines.

Flag regressions in:

* API p95/p99
* database latency
* Redis latency
* location ingestion
* dispatch
* WebSocket
* app startup
* frontend bundle
* mobile startup
* memory
* battery

A statistically meaningful regression must be investigated.

---

# LOAD-SHEDDING VALIDATION

Under overload verify priority order.

Noncritical work should degrade before:

* authentication
* active rides
* dispatch assignment
* authoritative trip state
* payment correctness
* safety

Do not sacrifice correctness to maximize throughput.

---

# PRODUCTION READINESS REVIEW

Before release qualification, inspect evidence for:

* tests
* performance
* security
* resilience
* recovery
* deployment
* observability
* backups
* DR
* accessibility

Every critical claim must reference actual test evidence.

---

# RELEASE QUALIFICATION GATES

Production release requires, at minimum:

* no unresolved critical defects
* no unresolved high-severity security vulnerabilities without explicit acceptance
* critical E2E journeys passing
* concurrency invariants passing
* payment/payout correctness validated
* performance within approved thresholds
* backup restore validated
* disaster-recovery exercise completed
* rollback validated
* observability functioning
* alerts functioning
* deployment validation passed
* accessibility baseline passed

Do not mark release-ready merely because CI is green.

---

# TEST EVIDENCE

Every major advanced QA activity must produce evidence such as:

* benchmark output
* load-test reports
* latency distributions
* resource graphs
* security findings
* failure-injection results
* recovery timestamps
* backup-restore results
* deployment results
* screenshots/videos where appropriate
* trace references
* logs/metrics references

Do not create fabricated evidence.

---

# DEFECT TRIAGE

For every advanced test failure record:

* severity
* impact
* affected system
* reproduction
* evidence
* root cause
* remediation
* regression coverage
* release impact

Distinguish:

* product defect
* infrastructure defect
* test-environment defect
* test-design defect
* capacity limitation
* external-provider limitation

Do not incorrectly attribute infrastructure failures to application code.

---

# TEST FLAKINESS

Advanced QA tests are often timing-sensitive.

Do not use arbitrary waits to make them pass.

Use:

* explicit readiness
* condition polling
* event synchronization
* deterministic clocks where possible
* trace correlation

A flaky resilience test is not evidence of resilience.

---

# QA CI/CD INTEGRATION

Integrate appropriate advanced tests into CI/CD according to cost and risk.

Per-commit:

* unit
* integration
* contract
* smoke

Pre-release:

* E2E
* accessibility
* security suites
* performance smoke
* deployment validation

Scheduled:

* full load
* soak
* chaos
* backup/restore
* DR exercises

Do not run massive tests on every pull request if they materially prevent productive development.

---

# SECURITY FINDING MANAGEMENT

For security findings record:

* vulnerability
* severity
* affected endpoint/component
* exploitability
* evidence
* remediation
* retest
* residual risk

Critical exploitable vulnerabilities must block release unless formally accepted by authorized stakeholders.

---

# PERFORMANCE ACCEPTANCE

Define project-specific thresholds based on measured baselines and production requirements.

At minimum review:

* API p95/p99
* dispatch latency
* location latency
* WebSocket delivery
* database latency
* queue age
* Kafka lag
* mobile startup
* frontend performance

Do not invent arbitrary universal thresholds if the workload or environment requires a different target.

Document chosen thresholds and rationale.

---

# CAPACITY REPORTING

Produce a capacity model showing:

* tested sustained rate
* tested peak
* saturation point
* autoscaling behavior
* resource bottleneck
* safe headroom
* expected production scaling factor

Clearly distinguish:

* measured capacity
* projected capacity
* untested assumptions

---

# FINAL QA DECISION

The final QA assessment must classify each major area as:

* validated
* validated with limitations
* failed
* not tested

Do not assign an overall numeric score.

Do not hide limitations.

The final assessment must be evidence-based.

---

# IMPLEMENTATION DISCIPLINE

Before executing final qualification:

1. Inspect the current repository and deployment state.
2. Verify functional QA prerequisites.
3. Establish production-like test environment.
4. Establish test-data scale.
5. Establish measurable baselines.
6. Execute load tests.
7. Execute stress tests.
8. Execute spike tests.
9. Execute soak tests.
10. Execute security tests.
11. Execute abuse tests.
12. Execute resilience/failure tests.
13. Execute backup/restore tests.
14. Execute disaster-recovery tests.
15. Execute deployment/rollback tests.
16. Execute mobile device qualification.
17. Execute accessibility qualification.
18. Compare performance regressions.
19. Triage defects.
20. Re-test remediations.
21. Validate release gates.
22. Produce the final QA evidence package.
23. Produce the required completion report.

Do not alter production code simply to make a test pass without identifying the underlying defect.

---

# PROHIBITED QA PRACTICES

Never:

* fabricate performance results
* fabricate disaster-recovery results
* claim backup restoration without actually restoring
* claim chaos validation from unit tests
* call security testing complete after a static checklist
* ignore high-severity security findings
* weaken assertions
* skip failing resilience tests without documentation
* use production credentials in load tests
* use real customer data
* create destructive production experiments without explicit controls
* report theoretical RPO/RTO as measured recovery
* certify capacity using a tiny test environment without qualification
* hide performance regressions through changed measurement windows

---

# IMPLEMENTATION BOUNDARIES

This volume completes advanced QA qualification.

It does not create another QA volume afterward.

It covers:

* functional/non-functional release evidence
* performance
* load
* stress
* resilience
* security
* failure
* backup/restore
* disaster recovery
* deployment
* rollback
* accessibility
* mobile/device qualification
* production readiness

When this volume is complete, the planned QA phase is complete.

Do not invent another "final integration" or "production readiness" prompt.

---

# REQUIRED QA DELIVERABLES

Produce:

## PERFORMANCE PACKAGE

* baselines
* load results
* stress results
* spike results
* soak results
* capacity model

## SECURITY PACKAGE

* authentication testing
* authorization testing
* injection
* XSS/CSRF
* SSRF
* file upload
* webhook
* WebSocket
* abuse
* mobile security
* findings/remediation

## RESILIENCE PACKAGE

* pod failure
* node failure
* worker failure
* Redis failure
* PostgreSQL failover
* Kafka failure
* queue failure
* search failure
* provider failure
* cascading failure

## RECOVERY PACKAGE

* database restore
* object restore
* backup validation
* disaster recovery
* regional failover where supported
* active-trip recovery
* financial recovery

## DEPLOYMENT PACKAGE

* rolling deployment
* zero/minimal downtime validation
* migration compatibility
* canary/blue-green where applicable
* rollback

## CLIENT QUALIFICATION

* web
* rider mobile
* driver mobile
* device matrix
* accessibility
* network degradation

## RELEASE PACKAGE

* defect inventory
* performance regression
* security findings
* SLO evidence
* recovery measurements
* release gates
* final qualification status

---

# REQUIRED FINAL VALIDATION

Execute and report actual results for:

* performance
* load
* stress
* spike
* soak
* security
* abuse
* concurrency
* resilience
* failure injection
* backup restore
* disaster recovery
* deployment
* rollback
* accessibility
* mobile/device validation

Do not report a test as passed unless it was actually executed.

---

# COMPLETION REPORT REQUIREMENTS

When QA qualification is complete, report:

## FILES CREATED

List every new test, configuration, fixture, benchmark, report, runbook, or QA artifact.

## FILES MODIFIED

List every modified test, application, infrastructure, or configuration file.

## PERFORMANCE

Report:

* baseline
* load
* stress
* spike
* soak
* capacity
* p50/p95/p99
* saturation points

## SECURITY

Report:

* tested attack surfaces
* findings
* severity
* remediation
* retest status
* residual risk

## RESILIENCE

Report:

* failures injected
* impact
* detection
* recovery
* state integrity
* measured recovery time

## BACKUP/RESTORE

Report:

* backup type
* restore tested
* data validation
* actual recovery duration

## DISASTER RECOVERY

Report:

* scenario
* region/environment
* RPO
* RTO
* measured result
* active-trip recovery
* financial recovery

## DEPLOYMENT

Report:

* deployment strategy
* mixed-version validation
* migration validation
* rollback
* zero/minimal downtime evidence

## CLIENT QUALIFICATION

Report:

* browsers
* iOS devices/versions
* Android devices/versions
* network conditions
* accessibility

## DEFECTS

Report:

* critical
* high
* medium
* low
* fixed
* open
* deferred
* release blockers

## SLO VALIDATION

Report:

* SLO
* measurement
* target
* observed result
* pass/limitation/failure

## CAPACITY

Report:

* measured sustained capacity
* measured peak
* bottleneck
* safe operating range
* scaling behavior
* assumptions

## FINAL QA ASSESSMENT

For each major area report one of:

* validated
* validated with limitations
* failed
* not tested

Do not provide a numeric quality score or arbitrary overall ranking.

## UNRESOLVED ISSUES

List only genuine remaining QA issues, limitations, or environmental constraints.

---

# FINAL ENGINEERING PRINCIPLE

The platform is not production-ready because unit tests pass.

Production readiness requires evidence that the complete system remains correct and recoverable under realistic scale, attack, dependency failure, deployment change, data recovery, and regional failure conditions.

The most important invariants remain:

* no duplicate ride assignment
* no duplicate financial effects
* no unauthorized data access
* no illegal trip state transition
* no silent loss of critical asynchronous work
* no permanent loss of active-trip state
* no unsafe deployment-induced corruption
* no unrecoverable backup failure
* no hidden critical security vulnerability
* no uncontrolled cascading failure

Performance results must be measured.

Security findings must be tested and retested.

Recovery must be executed, not merely documented.

Backup restoration must be performed.

RPO/RTO must be measured.

Deployment rollback must be exercised.

Mobile background/location behavior must be tested on representative devices.

Accessibility must be validated on the actual clients.

Capacity limitations must be documented honestly.

The repository remains the implementation source of truth.

Upon completion of this volume, the dedicated QA phase is complete and the planned project prompt sequence is complete.
