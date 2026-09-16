# UBER-STYLE RIDE-HAILING PLATFORM — BACKEND PROMPT — VOLUME 4

## ROLE

You are the senior backend engineering organization responsible for completing the production backend platform for a globally scalable ride-hailing and mobility marketplace comparable in product depth and operational sophistication to Uber.

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

You are not creating a tutorial, prototype, benchmark-only implementation, or simplified demonstration.

This volume is responsible for completing the backend's operational intelligence, analytics ingestion, administrative search, data lifecycle controls, privacy operations, reliability automation, reconciliation framework, and backend-wide production hardening required after the core marketplace, financial, safety, support, and risk capabilities have been implemented.

The repository is the source of truth for what currently exists.

Do not assume that another AI prompt or previous conversation is available.

---

# PROJECT

Complete the production backend capabilities required to operate the ride-hailing marketplace at commercial scale.

The backend now must provide a coherent operational platform around:

* riders
* drivers
* vehicles
* compliance
* locations
* ride requests
* dispatch
* trips
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
* analytics
* auditability
* data lifecycle
* privacy operations
* reconciliation
* reliability automation
* observability

This volume must not introduce a new product architecture.

Instead, complete the operational backend layer around the existing domains and harden the system for high-volume production operation.

---

# SOURCE OF TRUTH

Before modifying the repository, inspect:

* NestJS applications and modules
* Prisma schema and migrations
* PostgreSQL indexes and constraints
* Redis usage
* Kafka topics and consumers
* outbox processing
* BullMQ queues and workers
* WebSocket infrastructure
* ride/trip/dispatch domains
* pricing
* payments
* earnings/payouts
* notifications
* safety
* fraud/risk
* support
* promotions
* administrative APIs
* audit infrastructure
* existing search implementation
* analytics/event consumers
* privacy/deletion workflows
* logging/metrics/tracing
* tests
* existing frontend/mobile consumers
* deployment configuration

Preserve compatible behavior.

Extend existing implementations instead of creating duplicate infrastructure.

Do not regenerate unchanged files.

---

# BACKEND SCOPE

This prompt owns:

* operational analytics ingestion
* business-event analytics processing
* administrative search
* operational dashboards data APIs
* reconciliation framework
* data-retention automation
* privacy deletion/anonymization workflows
* data-export workflows where applicable
* cache/index invalidation infrastructure
* event replay tooling
* dead-letter management
* queue recovery tooling
* outbox monitoring
* event consumer health
* operational configuration services
* feature-flag backend support where applicable
* production backend hardening
* backend-wide resilience validation
* database performance hardening
* API protection hardening
* audit retention
* compliance-oriented operational controls
* backend integration tests
* production readiness verification

Do not implement cloud infrastructure deployment in this volume.

Do not implement frontend or mobile applications.

---

# DOMAIN OWNERSHIP

Maintain the existing authoritative domain boundaries.

Analytics must not become the source of truth for:

* rides
* trips
* payments
* earnings
* payouts
* users
* drivers

Search indexes must remain derived representations.

Operational dashboards must consume derived telemetry/analytics rather than querying transactional tables indiscriminately.

Privacy workflows may orchestrate deletion/anonymization but must not violate financial, audit, or legal retention requirements.

Administrative tooling must invoke domain-approved commands rather than directly editing domain persistence.

---

# ANALYTICS ARCHITECTURE

Implement the backend-side analytics ingestion architecture needed to observe marketplace behavior without placing analytical workloads on transactional PostgreSQL.

Use domain events already emitted by the platform.

Relevant analytics domains include:

* ride demand
* driver supply
* dispatch performance
* trip completion
* cancellation
* pricing
* payments
* earnings
* payouts
* notifications
* safety
* fraud/risk
* support
* promotions

Analytics processing must be asynchronous.

Do not add synchronous analytics work to the ride-request or trip-critical paths.

---

# ANALYTICS EVENTS

Create or extend event consumers that transform operational domain events into analytics records.

Analytics events should contain only necessary information.

Do not publish or retain:

* authentication credentials
* payment credentials
* secrets
* unnecessary precise historical location
* unnecessary sensitive identity information

Where aggregate metrics are sufficient, prefer aggregate/event metadata over raw sensitive records.

---

# ANALYTICS IDEMPOTENCY

Analytics consumers must tolerate:

* duplicate events
* replay
* consumer restart
* Kafka rebalance
* delayed events

Use deterministic event identifiers and durable processing state where required.

Do not double-count:

* rides
* completed trips
* payment outcomes
* payouts
* cancellations
* notification deliveries

---

# BUSINESS METRICS PIPELINE

Support derived operational metrics such as:

* ride requests
* match rate
* dispatch latency
* driver acceptance rate
* rider cancellation rate
* driver cancellation rate
* trip completion rate
* average trip duration
* supply availability
* stale-location rate
* ETA accuracy signals
* payment success rate
* refund rate
* payout success rate
* notification delivery rate
* safety incident rate
* support backlog
* promotion utilization
* risk-signal volume

Metrics must have clear definitions.

Do not allow multiple modules to calculate the same business metric differently without an explicit reason.

---

# ANALYTICS TIME MODEL

Analytics must preserve event time separately from processing time where required.

Use UTC for event storage unless market-local time is explicitly required for reporting.

Support aggregation windows such as:

* minute
* hour
* day
* market
* city
* service zone
* ride product

Do not rely solely on application server processing time when measuring marketplace behavior.

---

# OPERATIONAL DASHBOARD APIS

Implement secure backend APIs supporting authorized operational dashboards.

Dashboards may consume metrics such as:

* active riders
* active drivers
* active trips
* dispatch backlog
* location freshness
* payment failures
* payout failures
* notification failures
* queue backlog
* event lag
* dead-letter count
* safety incidents
* support cases

Dashboard APIs must use pre-aggregated or purpose-built data where necessary.

Do not allow administrators to execute arbitrary analytical queries against the production transactional database.

---

# ADMINISTRATIVE SEARCH

Implement controlled operational search for entities such as:

* users
* drivers
* vehicles
* rides
* trips
* payments
* payouts
* support cases
* safety incidents
* promotions
* risk signals

Search may use OpenSearch/Elasticsearch or an existing repository search architecture.

Search must never become authoritative state.

---

# SEARCH INDEXING

Index transactional records through events or other reliable asynchronous mechanisms.

Support:

* index creation
* update
* deletion
* retry
* dead-letter handling
* reindexing
* index versioning

Index documents must contain only information appropriate for their audience.

Do not expose fields merely because they happen to exist in PostgreSQL.

---

# SEARCH CONSISTENCY

Search is eventually consistent.

Administrative workflows must distinguish:

* search result
* authoritative record

Before executing a privileged mutation:

1. resolve the target from the search result
2. verify authorization
3. retrieve authoritative state
4. validate the current state
5. execute a domain command

Never mutate based solely on stale search results.

---

# SEARCH REBUILD

Implement a safe reindex/rebuild strategy.

The system must support rebuilding indexes from authoritative data without corrupting the active index.

Where practical use:

* new index version
* backfill
* validation
* alias/switch
* old-index cleanup

Do not require production downtime for routine index reconstruction.

---

# DEAD-LETTER MANAGEMENT

Implement an operational backend for inspecting and safely replaying dead-letter records.

Support:

* queue/job dead letters
* Kafka/event dead letters
* outbox failures
* notification failures
* search-index failures

Every replay operation must:

* require authorization
* record operator identity
* preserve original failure metadata
* re-check current authoritative state
* be idempotent where applicable
* create an audit record

Do not provide an unrestricted "replay everything" operation.

---

# EVENT REPLAY

Implement a controlled event-replay abstraction.

Replay must support:

* selected event IDs
* selected event ranges
* selected event types
* selected aggregate/entity IDs where feasible

Before replaying:

* verify operator permissions
* verify consumer compatibility
* verify event schema version
* prevent unsafe side effects
* preserve correlation metadata

Replay of a financial event must never blindly execute a second financial side effect.

Consumers must identify whether an event represents:

* informational analytics
* derived index state
* notification
* financial command

and apply appropriate safeguards.

---

# OUTBOX MONITORING

Implement monitoring around the transactional outbox.

Track:

* backlog size
* oldest unpublished event age
* publish success
* publish failure
* retry count
* dead-letter count
* publishing throughput

Provide operational APIs/metrics sufficient to detect when event propagation is falling behind.

---

# EVENT CONSUMER MONITORING

Track for important consumers:

* consumer lag
* processing latency
* processing failures
* retry count
* dead letters
* throughput
* last successful processing timestamp

Consumers that stop processing must become operationally visible.

---

# QUEUE OPERATIONS

Provide operational controls for BullMQ workloads.

Support controlled inspection of:

* waiting jobs
* active jobs
* failed jobs
* delayed jobs
* completed jobs where retained

Where operational replay is allowed:

* require authorization
* preserve job identity
* prevent unintended duplicate effects
* verify current domain state

Do not create an administrative endpoint that permits arbitrary job payload modification.

---

# RECONCILIATION FRAMEWORK

Create a reusable reconciliation framework for domains that already require it.

At minimum support reconciliation around:

* payments
* refunds
* payouts
* trip/dispatch state
* location state
* notification delivery
* search indexing
* event propagation

A reconciliation task must produce:

* reconciliation run ID
* domain
* scope
* start time
* end time
* records examined
* discrepancies found
* corrections applied
* corrections rejected
* unresolved discrepancies

---

# RECONCILIATION SAFETY

Reconciliation must not become a hidden second business engine.

The framework must:

* compare authoritative sources
* identify discrepancies
* execute only explicitly approved correction rules
* preserve audit history
* support dry-run mode where appropriate
* avoid destructive history rewriting

Financial reconciliation must preserve existing financial records and use adjustments where corrections are necessary.

---

# DATA RETENTION

Implement backend retention workflows according to defined domain policies.

Potential data categories:

* transient location
* historical location
* notification delivery history
* logs
* traces
* analytics events
* support attachments
* safety metadata
* risk signals
* search documents
* session records
* idempotency records
* audit records

Retention must be explicit.

Do not blindly delete records solely based on age.

---

# LOCATION RETENTION

Treat exact historical location separately from operational live location.

Implement:

* TTL for ephemeral live location
* controlled retention for historical trip location
* deletion/anonymization where required
* access controls
* auditability

Do not retain every high-frequency driver location indefinitely.

---

# ACCOUNT DELETION

Implement the production account-deletion workflow.

The workflow must:

1. Authenticate the requesting user.
2. Authorize ownership.
3. Determine which data is deletable.
4. Determine which data is legally/financially retained.
5. Anonymize/delete eligible personal data.
6. Invalidate active sessions where required.
7. invalidate ephemeral caches.
8. remove or anonymize search documents.
9. enqueue asynchronous cleanup.
10. preserve required audit/financial records.
11. record completion state.

Do not delete financial/audit records that must legally remain while still exposing unnecessary personal identifiers.

---

# ACCOUNT DELETION ASYNCHRONOUS PROCESSING

Large deletion workflows must use background jobs.

Jobs must be:

* idempotent
* resumable
* observable
* retryable
* permission-aware

A worker restart must not leave the account in an unknowable intermediate state.

---

# DATA EXPORT

Where supported by the product/privacy model, implement a secure data-export workflow.

The export must:

* be requested by an authenticated user
* include only authorized data
* run asynchronously for large datasets
* use private object storage
* expire automatically
* have access logging
* prevent cross-user access

Do not expose raw database dumps to users.

---

# PRIVACY DELETION FROM DERIVED SYSTEMS

Account deletion must address derived data such as:

* Redis keys
* search indexes
* notification preferences
* analytics where personal identifiers exist
* caches
* derived views

Use deletion/anonymization events and asynchronous processing.

Do not assume deleting PostgreSQL records automatically removes derived data.

---

# CACHE INVALIDATION

Implement or strengthen consistent cache invalidation for mutable entities.

At minimum consider:

* user profile
* driver profile
* vehicle state
* pricing configuration
* promotion configuration
* operational configuration

Cache invalidation must occur after the authoritative write succeeds.

Do not invalidate before a transaction that later rolls back.

Where transactionally reliable invalidation is required, use outbox/event-driven invalidation.

---

# FEATURE-FLAG BACKEND

Implement a server-side feature-flag abstraction where the repository requires feature-controlled rollout.

Flags must support:

* identifier
* default
* environment
* activation state
* target scope
* rollout rules where needed
* audit
* expiration/cleanup metadata

Feature evaluation must be deterministic.

Critical security and financial invariants must not depend solely on mutable feature flags.

---

# OPERATIONAL CONFIGURATION

Implement configuration entities for business-operational values such as:

* market availability
* ride-product availability
* pricing settings
* cancellation rules
* service zones
* rate limits
* notification settings
* feature controls
* safety settings

Configuration changes must support:

* validation
* authorization
* versioning
* activation
* rollback
* audit

---

# CONFIGURATION VERSIONING

When configuration affects a historical business decision, preserve the configuration version/reference used at decision time.

Do not allow changing a configuration record to silently change the meaning of an old ride estimate or financial calculation.

---

# CONFIGURATION ROLLBACK

Implement controlled rollback where configuration changes materially affect operations.

A rollback must:

* restore a previously validated configuration
* create an audit record
* preserve the history
* invalidate relevant caches
* propagate changes to derived services

---

# ADMINISTRATIVE SEARCH SECURITY

Administrative search must enforce data classification.

For example:

* ordinary support users receive minimal rider information
* privileged financial users receive financial records needed for authorized workflows
* safety investigators receive safety data under explicit permissions
* risk investigators receive risk signals according to permission
* unrestricted historical location is not exposed by default

Search field visibility must be permission-aware.

---

# AUDIT RETENTION

Audit records for:

* authentication security
* administrative actions
* financial corrections
* compliance decisions
* safety actions
* data deletion
* privacy access
* risk enforcement

must have defined retention.

Do not silently purge critical audit evidence.

---

# SECURITY EVENT PROCESSING

Create or extend security events for:

* suspicious authentication
* repeated login failures
* privilege changes
* session revocation
* administrative access
* unusual data export
* excessive location access
* repeated payment failures
* suspicious payout changes

Security events must be observable and auditable.

---

# API SECURITY HARDENING

Review all backend APIs for:

* authentication
* authorization
* resource ownership
* rate limiting
* pagination
* input validation
* output filtering
* request-size controls
* error handling
* CORS
* security headers

Pay particular attention to:

* list endpoints
* search endpoints
* export endpoints
* administrative APIs
* support APIs
* financial endpoints

---

# MASS-ASSIGNMENT PROTECTION

Ensure request DTOs cannot directly set privileged/internal fields such as:

* account status
* role
* permissions
* compliance approval
* payment state
* payout state
* trip state
* administrative flags

Use explicit DTOs and command models.

Do not bind arbitrary request objects directly into Prisma update operations.

---

# SQL AND QUERY SAFETY

Review raw SQL usage.

Every raw query must:

* parameterize user input
* use controlled identifiers
* avoid dynamic SQL from untrusted data
* have a clear reason for existing

Do not accept arbitrary SQL expressions through API parameters.

---

# DATABASE PERFORMANCE HARDENING

Review production query paths for:

* N+1 patterns
* missing indexes
* unbounded queries
* inefficient joins
* hot rows
* excessive transactions
* oversized selected columns
* poor pagination
* unnecessary serialization

Use query plans where practical.

Add indexes only where justified by actual access patterns.

Do not create redundant indexes that unnecessarily increase write cost.

---

# DATABASE CONNECTION MANAGEMENT

Verify:

* connection pool sizing
* worker-specific connection behavior
* request concurrency
* background job concurrency
* transaction duration
* shutdown handling

Do not allow worker scaling to overwhelm PostgreSQL with uncontrolled connections.

---

# REDIS PERFORMANCE HARDENING

Review:

* key cardinality
* TTL coverage
* hot keys
* large values
* serialization size
* command patterns
* geographic lookup load
* rate-limit load

Avoid:

* giant Redis values
* permanent keys
* unbounded lists/sets
* global locks with high contention

---

# EVENT PERFORMANCE HARDENING

Review Kafka usage for:

* partition balance
* consumer concurrency
* message size
* topic retention
* consumer lag
* hot partitions
* retry behavior
* dead-letter behavior

Do not create globally ordered topics when entity-level ordering is sufficient.

---

# QUEUE PERFORMANCE HARDENING

Review BullMQ workloads for:

* concurrency
* retry amplification
* job payload size
* delayed-job volume
* queue starvation
* dead-letter growth
* worker resource consumption

Separate critical and noncritical workloads.

---

# BACKPRESSURE

Implement or strengthen backpressure for:

* location ingestion
* notification generation
* analytics ingestion
* event consumers
* search indexing
* reconciliation
* bulk exports

The system must fail predictably under overload.

---

# GRACEFUL DEGRADATION

Validate that failure of:

* search
* analytics
* notification providers
* risk analysis
* noncritical configuration services

does not unnecessarily stop:

* active trips
* authoritative ride state
* financial correctness
* emergency incident creation

---

# DISASTER RECOVERY BACKEND SUPPORT

Implement the backend-side mechanisms needed for recovery.

Support:

* replayable events
* rebuildable search indexes
* reconstructible caches
* recoverable queue jobs
* reconciliation
* database backup verification hooks
* idempotent startup/reprocessing

Do not depend on ephemeral state being preserved through a disaster.

---

# RECOVERY FROM REDIS LOSS

Ensure that after Redis data loss:

* authoritative PostgreSQL records remain valid
* caches can be rebuilt
* ephemeral driver/location state can recover from active clients
* active-trip authoritative state remains available
* rate-limit state can safely reset according to defined policy
* distributed ephemeral state does not become permanent corruption

---

# RECOVERY FROM KAFKA LOSS OR REBUILD

Ensure event-driven derived systems can be reconstructed from authoritative state or durable event history.

Where a downstream consumer depends on a Kafka topic, define:

* replay strategy
* initial synchronization
* schema compatibility
* duplicate handling

---

# RECOVERY FROM SEARCH LOSS

Search indexes must be rebuildable.

The loss of search must not destroy:

* users
* trips
* payments
* payouts
* support cases

Transactional APIs remain authoritative.

---

# RECOVERY FROM QUEUE LOSS

Critical asynchronous work must have enough durable source state to be regenerated or reconciled.

Do not rely solely on an ephemeral queue entry as proof that critical work should happen.

---

# OBSERVABILITY HARDENING

Ensure tracing crosses:

* HTTP
* PostgreSQL
* Redis
* BullMQ
* Kafka
* WebSockets
* external providers

Every asynchronous boundary should preserve correlation context.

---

# TRACE SAMPLING

High-volume paths such as driver location must not produce unbounded telemetry volume.

Use appropriate sampling while preserving:

* errors
* slow operations
* important business transactions
* security-sensitive operations

Do not sample away every trace needed for incident investigation.

---

# LOGGING HARDENING

Review logs for:

* secrets
* tokens
* passwords
* payment credentials
* exact location
* private support content
* raw compliance documents
* raw risk signals

Implement redaction centrally where possible.

---

# ALERTING SIGNALS

Create or document alerts for:

* API error spikes
* dispatch backlog
* stale driver location
* payment failures
* payout failures
* webhook backlog
* Kafka consumer lag
* outbox lag
* queue backlog
* dead letters
* database saturation
* Redis failures
* WebSocket degradation
* search indexing failures
* reconciliation discrepancies
* unusual safety events
* suspicious risk spikes

Alerts must be actionable.

---

# SLO SUPPORT

Expose metrics necessary to evaluate SLOs for:

* API availability
* ride request success
* dispatch latency
* realtime delivery
* payment processing
* payout processing
* notification delivery
* location ingestion

Do not create an SLO that cannot be measured reliably.

---

# OPERATIONAL RUNBOOK DATA

Backend APIs/metrics should expose enough information to execute operational runbooks.

Operators should be able to determine:

* what failed
* when it failed
* affected domain
* affected region/market
* current backlog
* last successful processing
* safe recovery action

Do not expose operational mutation endpoints to ordinary users.

---

# DATA QUALITY

Implement validation/monitoring for:

* impossible state combinations
* orphaned records
* missing foreign relationships
* duplicate financial references
* stale driver state
* invalid pricing configuration
* orphaned search documents
* out-of-date aggregates

Data-quality checks must be observable.

---

# DATA INTEGRITY RECONCILIATION

Implement periodic checks for invariants such as:

* active rides have valid lifecycle states
* assignments map to valid trips
* drivers do not hold contradictory active assignments
* payments map to valid financial references
* payouts map to valid earnings
* promotions do not exceed usage rules
* ratings reference valid completed trips

Detected violations must produce alerts and safe investigation records.

Do not silently "fix" data without a documented correction pathway.

---

# BULK OPERATIONS

Administrative bulk operations must be carefully bounded.

Examples:

* suspend a set of accounts
* reindex a set of records
* reprocess a bounded event range
* migrate configuration

Every bulk operation must support:

* authorization
* explicit scope
* bounded batch size
* progress
* cancellation
* audit
* idempotency
* failure reporting

Never provide unrestricted arbitrary bulk SQL through an API.

---

# DATA EXPORT SAFETY

Exports must:

* enforce authorization
* limit data scope
* run asynchronously
* expire
* encrypt at rest
* use private storage
* create access audits
* prevent predictable URLs

Do not place exports in public object storage.

---

# BACKEND-WIDE SECURITY REVIEW

Perform a complete review covering:

* authentication
* authorization
* IDOR
* mass assignment
* SQL injection
* SSRF boundaries
* webhook security
* file access
* rate limiting
* token handling
* admin authorization
* support authorization
* privacy controls
* location protection
* payment security
* payout security
* audit protection
* secret handling

Fix issues discovered within scope.

---

# BACKEND-WIDE RELIABILITY REVIEW

Verify:

* graceful shutdown
* retry bounds
* idempotency
* transaction boundaries
* outbox recovery
* queue recovery
* Kafka replay
* search rebuild
* cache rebuild
* reconciliation
* provider timeouts
* dependency isolation
* overload protection

---

# TESTING REQUIREMENTS

Add comprehensive tests.

## ANALYTICS

Test:

* event ingestion
* deduplication
* event replay
* aggregation
* event-time handling

## SEARCH

Test:

* indexing
* update
* deletion
* eventual consistency
* reindex
* permission filtering

## RECONCILIATION

Test:

* discrepancy detection
* dry-run
* safe correction
* audit
* idempotent rerun

## PRIVACY

Test:

* account deletion
* anonymization
* session invalidation
* cache cleanup
* search cleanup
* data export authorization
* export expiration

## ADMINISTRATION

Test:

* permission checks
* bulk operation boundaries
* replay permissions
* dead-letter permissions
* configuration changes
* audit

## RESILIENCE

Test:

* Redis loss
* Kafka consumer restart
* queue failure
* search failure
* provider outage
* duplicate event
* worker restart
* database reconnect

---

# CONCURRENT TESTING

Verify correctness under:

* concurrent reconciliation
* repeated event replay
* simultaneous administrative actions
* duplicate export requests
* concurrent configuration updates
* reindexing while records are changing
* cache invalidation races
* queue retry races

---

# INTEGRATION TESTING

Use realistic infrastructure where practical.

Validate:

* PostgreSQL
* Redis
* Kafka/outbox
* BullMQ
* search
* object storage
* existing provider abstractions
* observability integrations

Do not claim integration coverage when infrastructure was not actually exercised.

---

# PERFORMANCE VALIDATION

Measure, where practical:

* administrative search
* analytics consumers
* event throughput
* queue throughput
* reconciliation throughput
* account deletion throughput
* export throughput
* database query latency
* Redis operations
* Kafka consumer lag

Identify bottlenecks and document the observed limits.

---

# MIGRATION VALIDATION

Every schema change must:

* apply cleanly
* preserve required data
* preserve financial precision
* preserve auditability
* preserve indexes
* support rolling deployment where required

Do not use destructive migration shortcuts on production data.

---

# API CONTRACT VALIDATION

Review existing APIs for:

* pagination
* authorization
* output filtering
* error semantics
* rate limits
* sensitive fields
* backwards compatibility

Do not expose newly added operational fields through ordinary client APIs unintentionally.

---

# DOCUMENTATION

Update documentation for:

* analytics
* search
* replay
* dead letters
* reconciliation
* privacy deletion
* data export
* operational configuration
* feature flags
* recovery
* data retention
* backend security
* performance considerations

Documentation must describe real implementation and operational behavior.

---

# IMPLEMENTATION DISCIPLINE

Before changing files:

1. Inspect the repository.
2. Map existing operational infrastructure.
3. Preserve compatible implementation.
4. Implement analytics ingestion.
5. Implement operational search.
6. Implement reconciliation framework.
7. Implement privacy workflows.
8. Implement data retention.
9. Implement controlled replay and dead-letter operations.
10. Implement operational configuration.
11. Harden cache/index/event processing.
12. Harden APIs and database performance.
13. Add observability improvements.
14. Add resilience controls.
15. Add comprehensive tests.
16. Validate migrations.
17. Run formatting/linting/type checks.
18. Run integration/runtime validation.
19. Perform backend-wide security/reliability review.
20. Update documentation.
21. Produce the required completion report.

Do not rewrite unrelated features.

---

# PRODUCTION COMPLETENESS

Never leave:

* fake analytics
* fake reconciliation
* unrestricted admin queries
* placeholder deletion logic
* irreversible replay operations
* unaudited administrative mutations
* unbounded export functionality
* undocumented configuration changes
* unsafe bulk operations
* TODO/FIXME implementation gaps
* pseudo-code

Do not claim operational readiness if reconciliation cannot safely detect or report discrepancies.

---

# PROHIBITED PRACTICES

Never:

* query production transactional tables for arbitrary analytics
* expose raw SQL administration
* replay financial events without safeguards
* permanently store high-frequency location without policy
* delete required financial/audit records
* expose private exports publicly
* permit support users to bypass domain authorization
* use search as authoritative state
* use analytics as authoritative state
* use feature flags to bypass authorization
* let a failed derived system corrupt transactional truth
* silently repair inconsistent data
* create infinite retry loops
* allow unbounded bulk operations
* expose secrets in operational tooling

---

# IMPLEMENTATION BOUNDARIES

This volume completes the backend operational and production-hardening layer.

It must integrate with all previously implemented domains without creating alternate versions.

Do not implement:

* frontend
* mobile UI
* cloud infrastructure deployment

unless a minimal repository integration change is required for backend functionality.

Do not redesign the core ride, trip, payment, or identity domains.

---

# REQUIRED IMPLEMENTATION DELIVERABLES

Implement or update:

## ANALYTICS

* event consumers
* business metrics
* aggregation
* analytics persistence/transport where required

## SEARCH

* index management
* indexing consumers
* permission-aware search
* rebuild/reindex

## RECONCILIATION

* reusable framework
* domain reconciliation jobs
* discrepancy tracking
* safe correction

## PRIVACY

* account deletion
* anonymization
* data export
* derived-system cleanup

## OPERATIONS

* dead-letter inspection
* controlled replay
* queue operations
* outbox monitoring
* configuration management
* feature flags where applicable

## DATA LIFECYCLE

* retention
* cleanup
* cache invalidation
* derived-data cleanup

## HARDENING

* API security
* database performance
* Redis performance
* event performance
* queue performance
* backpressure
* resilience

## OBSERVABILITY

* operational metrics
* lag metrics
* reconciliation metrics
* audit telemetry
* recovery metrics

---

# REQUIRED OPERATIONAL APIs

Implement appropriately authorized APIs or internal administrative mechanisms for:

* business metrics
* operational search
* dead-letter inspection
* controlled replay
* reconciliation status
* reconciliation execution
* queue inspection
* configuration
* feature flags where applicable
* data-export status
* privacy deletion status

Do not expose internal operational controls to riders or drivers.

---

# REQUIRED DATABASE VALIDATION

After implementation:

* apply migrations
* inspect query plans for important new queries
* verify indexes
* verify retention constraints
* verify deletion/anonymization behavior
* verify audit relationships
* verify reconciliation records
* verify export records
* verify configuration versioning

---

# RUNTIME VALIDATION

Verify:

* analytics consumers
* search indexing
* search rebuild
* reconciliation
* dead-letter operations
* event replay safeguards
* queue operations
* account deletion
* data export
* cache invalidation
* configuration changes
* feature flags
* observability
* graceful degradation

Do not report a recovery workflow as implemented unless it was actually exercised.

---

# COMPLETION REPORT REQUIREMENTS

When implementation is complete, report:

## FILES CREATED

List every new file.

## FILES MODIFIED

List every modified file.

## ANALYTICS

Report:

* event consumers
* aggregates
* metrics
* deduplication
* replay behavior

## SEARCH

Report:

* indexes
* indexing consumers
* permissions
* reindexing
* rebuild strategy

## RECONCILIATION

Report:

* domains covered
* discrepancy types
* corrections
* audit behavior
* dry-run behavior

## PRIVACY

Report:

* deletion
* anonymization
* export
* cache cleanup
* search cleanup

## OPERATIONS

Report:

* dead-letter tooling
* replay
* queue controls
* outbox monitoring
* configuration
* feature flags

## DATABASE

Report:

* schema changes
* indexes
* performance changes
* retention support

## SECURITY

Report:

* API hardening
* admin controls
* bulk-operation controls
* privacy authorization
* export security

## OBSERVABILITY

Report:

* logs
* metrics
* traces
* alerts
* lag monitoring
* reconciliation telemetry

## TESTS

List tests added or modified and the behaviors they verify.

## VALIDATION

Report:

* formatting
* linting
* type checking
* builds
* migrations
* unit tests
* integration tests
* resilience tests
* performance tests
* operational-workflow validation

## COMPATIBILITY

Identify:

* API compatibility
* database compatibility
* event compatibility
* operational migration considerations

## UNRESOLVED ISSUES

List only genuine remaining issues.

Do not claim production readiness if required operational controls or recovery behavior remain incomplete or unverified.

---

# FINAL ENGINEERING PRINCIPLE

The backend must not merely execute successful requests; it must remain understandable, recoverable, auditable, and operationally controllable when the system is under stress or partially failing.

The final backend layer must provide:

* observable business behavior
* safe operational tooling
* rebuildable derived systems
* controlled data lifecycle
* privacy-preserving deletion
* secure data export
* recoverable asynchronous processing
* reliable reconciliation
* bounded bulk operations
* measurable SLO support
* hardened persistence
* resilient event and queue infrastructure

Transactional systems remain authoritative.

Analytics, search, caches, queues, and derived stores remain reconstructible.

Administrative operations remain authorized and audited.

Privacy operations remain compatible with financial and audit retention.

Recovery operations remain idempotent and bounded.

The repository remains the implementation source of truth.

All subsequent client and infrastructure work must consume the completed backend through stable APIs, events, and operational contracts without introducing alternate backend behavior.
