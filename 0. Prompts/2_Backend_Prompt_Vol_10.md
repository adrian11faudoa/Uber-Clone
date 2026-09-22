# Uber-Style Global Ride-Hailing & Mobility Platform — Backend Prompt — Volume 10

## ROLE

You are the senior backend engineering organization responsible for implementing the analytics, reporting, metric-definition, projection, data-quality, freshness, and export backend of an original, production-grade global ride-hailing and mobility platform.

Operate simultaneously as:

* Principal Software Architect
* Staff Backend Engineer
* Distributed Systems Engineer
* Data Architect
* Analytics Systems Engineer
* Distributed Systems Engineer
* Database Architect
* Event-Streaming Engineer
* Performance Engineer
* Reliability Engineer
* Security Engineer
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
* trust and safety personnel
* fleet personnel
* administrators

This milestone implements the backend analytics and reporting platform required to transform authoritative domain events and operational data into reliable, queryable business and operational metrics.

The platform is architected for targets such as:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* high-volume event streams
* large analytical datasets
* multi-region operation
* operational dashboards
* financial and marketplace reporting
* historical trend analysis

These are architectural targets, not measured capacity claims.

# TECHNOLOGY DIRECTION

Use the locked project stack:

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

* Redis where genuinely useful for bounded report/cache workloads

### Events

* Kafka or Redpanda

### Background Jobs

* BullMQ or equivalent

### Search

* OpenSearch or Elasticsearch-compatible architecture where already selected by the project

### Object Storage

* Amazon S3

### Observability

* OpenTelemetry
* Prometheus-compatible metrics
* structured logs
* Loki-compatible logging
* Tempo-compatible tracing

# SOURCE OF TRUTH

The repository is the implementation source of truth.

Inspect the repository before making changes.

Use the architecture artifacts already present in the repository as the authoritative architecture and analytics-contract reference.

Backend Volumes 1–9 establish:

* backend platform foundations
* identity and accounts
* driver onboarding and vehicles
* availability and location
* trip lifecycle
* dispatch
* pricing and financial systems
* notifications and messaging
* trust/safety/support/risk
* scheduled trips
* fleet operations
* routing/geography
* canonical API/error/idempotency/concurrency contracts
* event/outbox infrastructure
* jobs
* object storage
* audit
* observability

This milestone must consume those authoritative systems rather than replacing them.

Do not depend on the previous AI conversation.

If existing implementation differs from the architecture:

1. inspect the actual implementation
2. preserve compatible working behavior
3. make the minimum coherent changes required
4. document material discrepancies

Do not create competing sources of truth.

# BACKEND EXECUTION MODEL

This milestone owns the analytical backend layer.

It must support:

* canonical metric definitions
* analytics event ingestion
* normalized analytical events
* projection consumers
* time-bucket aggregation
* trip analytics
* dispatch analytics
* supply/demand analytics
* pricing analytics
* payment/earnings analytics
* ratings analytics
* notification analytics
* messaging analytics
* safety analytics
* support analytics
* fleet analytics
* scheduled-trip analytics
* data-quality checks
* late-event handling
* projection rebuilds
* projection freshness
* analytical query APIs
* report generation
* exports

The analytical layer is downstream of operational domain ownership.

It must not become the authoritative source for transactional business state.

# ANALYTICS PRINCIPLES

The implementation must preserve these principles:

* source domains remain authoritative
* analytical projections are derived
* metric definitions are explicit and versioned
* event processing is idempotent
* late events are handled explicitly
* duplicate events do not inflate metrics
* analytical queries do not overload transactional workloads
* financial analytics do not mutate financial records
* sensitive data is minimized
* report access is authorization-controlled
* exported data is private and expires according to the data-lifecycle architecture

Do not confuse:

* operational metrics
* analytical metrics
* observability metrics

They may share infrastructure but have different ownership and semantics.

# CURRENT IMPLEMENTATION SCOPE

## 1. Analytics Domain Boundary

Establish authoritative ownership for:

* metric definitions
* analytical event processing
* derived projections
* analytical aggregates
* report definitions
* report execution state
* export metadata
* data-quality state
* freshness state

The analytics domain does not own source-domain transactional entities.

## 2. Metric Definition Model

Implement a canonical metric-definition model.

Each metric should have:

* stable metric identifier
* name
* description
* owner
* version
* definition
* dimensions
* time semantics
* aggregation method
* source domain/event
* effective status

Definitions must be versioned.

Do not silently change the meaning of a metric while preserving the same identifier/version.

## 3. Metric Semantics

Document and implement exact semantics for:

* count
* distinct count
* sum
* average
* rate
* ratio
* percentile/quantile where supported
* duration
* time-to-event
* utilization

For every important metric, define:

* numerator
* denominator
* inclusion criteria
* exclusion criteria
* time basis
* timezone semantics
* handling of duplicates
* handling of late events

Avoid ambiguous metrics such as "active drivers" without defining the exact observation rule.

## 4. Event Ingestion for Analytics

Implement the analytics event-consumption layer from Kafka/Redpanda.

Consumers must support:

* schema validation
* event-version compatibility
* idempotency
* correlation metadata
* partition-aware processing
* retry
* dead-letter behavior
* metrics/tracing

Do not directly consume arbitrary application logs as the primary analytics source when domain events are available.

## 5. Canonical Analytical Event Model

Where the analytical layer needs normalization across domains, implement a canonical internal event representation.

Preserve:

* source event ID
* source event type
* source version
* source domain
* entity ID
* occurred-at
* processed-at
* region
* correlation/causation metadata
* payload/reference metadata

Do not duplicate complete sensitive source records unnecessarily.

## 6. Event Idempotency

Prevent analytical double counting.

Use durable deduplication keyed by a stable event identifier and appropriate source context.

Handle:

* duplicate delivery
* replay
* consumer restart
* partition reassignment

Do not assume Kafka/Redpanda delivers an event exactly once to the analytics consumer.

## 7. Late and Out-of-Order Events

Implement explicit handling for events that arrive after the expected time window.

Support:

* event-time processing
* processing-time tracking
* bounded lateness
* correction/recomputation where required
* freshness status

Do not silently assign all late events to the current time bucket.

## 8. Time-Bucket Architecture

Implement reusable aggregation by time bucket.

Support the granularity required by the architecture, such as:

* minute
* hour
* day
* week
* month

Ensure consistent bucket boundaries.

Define whether analytical reporting uses:

* UTC
* market-local time
* configured reporting timezone

Do not let individual reports implement their own incompatible time semantics.

## 9. Trip Analytics

Implement projections/aggregates for relevant trip metrics such as:

* trip requests
* successful trips
* cancellations
* expirations
* completion rate
* trip duration
* wait time where authoritative data exists
* distance where authoritative data exists
* trip volume by region/service category
* rider/driver activity aggregates where permitted

Derived metrics must reference authoritative trip facts.

## 10. Dispatch Analytics

Implement dispatch analytics such as:

* dispatch attempts
* candidate counts
* offers
* offer acceptance
* offer rejection
* offer expiration
* dispatch success
* time to assignment
* reassignment
* dispatch exhaustion
* regional/service-category trends

Do not rebuild dispatch state from guesses if canonical dispatch events exist.

## 11. Supply and Demand Analytics

Implement analytical projections for:

* available driver supply
* requested rides
* completed rides
* supply-demand ratios
* unmet demand indicators
* regional trends
* service-category trends
* scheduled versus on-demand demand

Clearly define observation windows and denominators.

Do not expose internal driver-level sensitive location data through aggregate reports unless explicitly required.

## 12. Pricing Analytics

Implement analytics for:

* fare estimates
* final fares
* average fare
* fare components
* promotions
* discounts
* dynamic-pricing usage
* cancellation fees
* pricing-version usage

Do not mutate the pricing domain.

Use committed financial/pricing facts.

## 13. Payment Analytics

Implement derived reporting for:

* payment attempts
* authorization success/failure
* capture volume
* refunds
* refund rates
* payment failures
* disputes
* reconciliation anomalies

Do not expose sensitive payment-instrument information.

Use internal financial state as authoritative.

## 14. Earnings and Payout Analytics

Support:

* driver earnings
* tips
* bonuses
* adjustments
* payout volume
* payout failures
* payout latency
* holds
* reconciliation anomalies

Analytics must remain downstream of the immutable financial domain.

Do not calculate official balances in analytics.

## 15. Ratings Analytics

Provide projections for:

* rating counts
* average ratings
* rating distributions
* rating trends
* review volume
* moderation outcomes where appropriate

Do not expose private review content through aggregate analytics unless explicitly authorized.

## 16. Notification Analytics

Support:

* notification creation
* channel usage
* send success
* delivery success where provider semantics allow
* failures
* invalid-token trends
* retry volume
* category-level notification trends

Do not treat provider acknowledgement as user engagement unless the metric definition explicitly says so.

## 17. Messaging Analytics

Support aggregate metrics such as:

* conversations created
* messages sent
* delivery latency
* read latency
* active messaging volume

Do not store or expose message bodies for analytics.

Do not use message content as an analytical signal unless an explicit architecture contract exists.

## 18. Safety Analytics

Support appropriate aggregate safety reporting such as:

* incident volume
* incident categories
* response/resolution duration
* escalations
* restrictions
* safety workflow throughput

Minimize personally identifying information.

Do not expose sensitive case details through ordinary reports.

## 19. Support Analytics

Support:

* case volume
* category distribution
* assignment time
* resolution time
* reopen rate
* escalation volume
* backlog
* SLA-related measurements where defined

Internal notes and private case contents must not become ordinary analytical data.

## 20. Fleet Analytics

Support:

* vehicle counts
* operational status
* inspection rates
* maintenance volume
* downtime
* readiness
* restriction rates

Use authoritative fleet events.

## 21. Scheduled-Trip Analytics

Support:

* scheduled reservations
* confirmation rates
* cancellation rates
* pre-dispatch timing
* dispatch conversion
* missed schedule windows
* completion outcomes

Distinguish scheduled trips from ordinary trips using explicit definitions.

## 22. Regional and Market Dimensions

Analytical models must support dimensions such as:

* region
* country/market
* city/service area
* service category
* device/client platform where appropriate
* customer type where authorized

Do not expose raw coordinates as ordinary report dimensions.

## 23. Dimension Governance

Define controlled dimensions.

Do not let arbitrary user-provided values become analytical dimensions.

Dimensions must be:

* bounded
* versioned where necessary
* validated
* documented

Avoid cardinality explosions.

## 24. Projection Architecture

Implement derived projections appropriate to the project's scale.

Separate:

* raw analytical event state
* operational aggregates
* historical reporting aggregates
* report-specific projections

Do not build one enormous "analytics table" containing every domain metric.

## 25. Projection Freshness

Track projection freshness.

Every projection should expose, where appropriate:

* latest processed event time
* latest processing time
* backlog/lag
* last successful update
* freshness status

Consumers and operators must be able to determine whether a report is current.

## 26. Projection Rebuilds

Implement controlled rebuild mechanisms.

Support:

* full rebuild
* bounded rebuild
* date-range rebuild
* source-domain rebuild
* versioned projection rebuild

Rebuilds must not overwrite authoritative operational state.

Do not run unbounded rebuilds through normal realtime workers without throttling.

## 27. Backfill and Reprocessing

Support safe reprocessing of historical events.

Provide:

* scope
* time range
* metric/projection selection
* checkpointing
* progress
* cancellation
* retry
* idempotency

Do not create an unrestricted production "reprocess everything" command.

## 28. Data Quality Framework

Implement analytical data-quality checks.

Detect conditions such as:

* missing expected events
* duplicate events
* impossible counts
* negative financial aggregates
* orphan references
* unexpected nulls
* inconsistent totals
* stale projections
* broken dimensions

Quality failures must be observable and actionable.

## 29. Reconciliation

Where analytical projections should reconcile with authoritative systems, implement explicit checks.

Examples include:

* completed trips versus trip projections
* captured payments versus financial aggregates
* payout totals versus ledger
* scheduled-trip counts versus source records

Do not silently change source data to make analytics reconcile.

## 30. Report Definition Model

Implement report definitions where the architecture requires reusable reports.

A report definition should specify:

* report ID
* version
* owner
* permissions
* metrics
* dimensions
* filters
* time semantics
* freshness requirement

Do not allow arbitrary SQL from ordinary clients.

## 31. Reporting Query API

Implement controlled reporting APIs.

Support:

* authorization
* date/time filters
* region/service filters
* pagination where required
* aggregation
* freshness metadata
* validation of supported dimensions

The API must use safe parameterization.

Do not expose direct database query execution.

## 32. Operational Reporting

Support reports needed by operations, such as:

* trip volume
* supply/demand
* dispatch performance
* driver operational metrics
* support backlog
* safety workflow throughput
* fleet readiness
* scheduled-trip health

Respect role-based access.

## 33. Financial Reporting

Support authorized reporting on:

* fare totals
* refunds
* captures
* earnings
* payouts
* reconciliation

Do not expose raw payment credentials.

Do not make analytics the source of official financial balances.

## 34. Report Performance

Protect transactional databases from expensive analytical queries.

Use appropriate:

* projections
* aggregate tables
* caching
* pagination
* precomputed summaries
* query timeouts

Do not run unrestricted historical aggregation over primary transactional tables for every report.

## 35. Report Caching

Where safe, cache repeatable report results.

Cache keys must account for:

* report version
* filter set
* time range
* region
* permissions/scope
* freshness requirements

Do not allow one user's privileged report to be returned to another user through shared caching.

## 36. Exports

Implement report/export jobs where required.

Support:

* CSV or other repository-approved formats
* asynchronous generation
* scoped filters
* authorization
* progress/state
* S3 storage
* expiration
* secure download

Do not generate large exports synchronously inside API request workers.

## 37. Export Security

Exports must:

* remain private
* use authorization-controlled access
* expire
* avoid public object URLs
* record creator/requester
* be auditable

Do not place secrets or unnecessary sensitive fields into exports.

## 38. Export Lifecycle

Integrate report exports with the existing object-lifecycle architecture.

Support:

* automatic expiration
* incomplete-generation cleanup
* failed-export cleanup
* retry
* storage monitoring

Do not leave historical exports indefinitely.

## 39. Analytics Authorization

Analytics access must respect:

* user role
* organization/market scope where defined
* support/safety privilege
* financial privilege
* operational privilege

A user authorized to view trips does not automatically become authorized to view financial or safety analytics.

## 40. Privacy Controls

Analytics must minimize sensitive data.

Avoid ordinary report dimensions containing:

* raw user IDs
* phone numbers
* email addresses
* payment identifiers
* private message content
* exact location coordinates
* internal risk scores

Where pseudonymous identifiers are truly required, follow the security/privacy architecture.

## 41. Retention

Use the established data-lifecycle architecture.

Define retention separately for:

* raw analytical events
* projections
* aggregates
* report outputs
* exports
* quality records

Do not invent legal retention requirements.

## 42. Events

Publish analytics lifecycle events where the architecture requires them, such as:

* projection.updated
* projection.rebuilt
* report.generated
* report.failed
* export.created
* export.completed
* data_quality.alerted

Do not publish every analytical row mutation as a global domain event.

## 43. Background Jobs

Implement jobs for:

* event projection
* aggregate rollups
* projection maintenance
* rebuilds
* reconciliation
* quality checks
* report generation
* export generation
* export cleanup

Jobs must be:

* idempotent
* bounded
* retry-safe
* observable
* cancellable where appropriate

## 44. Queue Isolation

Separate workloads where necessary:

* realtime event projection
* historical backfill
* report generation
* export generation
* reconciliation
* data-quality checks

A large export must not starve near-realtime analytical projections.

## 45. Analytics Observability

Expose metrics such as:

* event-consumer lag
* projection freshness
* projection failures
* rebuild duration
* report latency
* export queue depth
* export duration
* data-quality failures
* reconciliation mismatches

Avoid high-cardinality labels.

## 46. Tracing

Trace:

* event ingestion
* projection processing
* rollups
* report queries
* exports
* reconciliation
* rebuilds

Do not place sensitive raw event payloads into traces.

## 47. API and Event Security

Protect analytics and reporting interfaces using the established authentication and authorization system.

Do not create a parallel analytics authentication system.

## 48. Testing

Create comprehensive tests for:

### Metric Definitions

* versioning
* deterministic semantics
* filtering
* aggregation

### Event Processing

* valid event
* duplicate event
* late event
* out-of-order event
* malformed event
* replay

### Projections

* correct aggregation
* incremental update
* rebuild
* backfill
* freshness

### Data Quality

* duplicate detection
* missing-event detection
* inconsistent totals
* stale projection

### Reporting

* authorization
* filter correctness
* aggregation correctness
* pagination
* timeout behavior

### Exports

* authorization
* generation
* failure
* retry
* private storage
* expiration

### Reconciliation

* matching data
* mismatch detection
* non-destructive behavior

# SECURITY AND PRIVACY

## 49. Sensitive Financial Data

Do not expose:

* payment credentials
* bank information
* provider secrets
* security tokens

Analytics may expose aggregate financial figures only to authorized roles.

## 50. Safety and Risk Data

Do not expose:

* raw safety evidence
* internal risk scores
* fraud rules
* private case notes

outside authorized operational contexts.

## 51. Messaging Privacy

Analytics must not require storing or indexing message contents.

## 52. Location Privacy

Use geographic aggregates rather than exact coordinates wherever possible.

Do not make precise driver-location history a general reporting dimension.

## 53. Audit

Audit:

* privileged report access where required
* financial report access
* safety/risk report access
* export creation
* export download where required
* report-definition changes
* projection administrative operations

# FAILURE AND RECOVERY

## 54. Event-Broker Failure

Analytics consumers must recover from Kafka/Redpanda failure without corrupting projection state.

## 55. Database Failure

Projection/reporting failures must not corrupt source-domain state.

## 56. Backlog

When analytical lag grows:

* expose freshness degradation
* throttle optional workloads
* preserve critical projection processing
* avoid unbounded worker scaling

## 57. Projection Corruption

Provide rebuild/reconciliation mechanisms rather than silently serving known-corrupt results.

## 58. Export Failure

A failed export must:

* enter a deterministic failure state
* be retryable where appropriate
* clean temporary objects
* remain auditable

# API SURFACE

## 59. Analytics APIs

Implement only repository-defined analytics/reporting APIs.

Potential operations include:

* metric definitions
* operational dashboards
* report execution
* report status
* historical aggregates
* export creation
* export status
* authorized export access

Do not expose arbitrary SQL.

## 60. Administrative Analytics APIs

Privileged users may receive broader reporting capabilities according to the authorization model.

Every such capability must be explicitly permissioned.

# DOCUMENTATION

Create or update documentation covering:

* metric definitions
* event ingestion
* analytical event model
* projections
* time buckets
* late events
* trip/dispatch/supply-demand analytics
* pricing/payment/earnings analytics
* ratings/notification/messaging analytics
* safety/support/fleet/scheduled-trip analytics
* data quality
* freshness
* rebuilds
* backfills
* reconciliation
* reporting APIs
* exports
* authorization
* privacy
* retention
* operational runbooks

Documentation must describe actual implementation behavior.

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not create a new data warehouse or lakehouse platform.

Do not replace PostgreSQL, Kafka/Redpanda, S3, OpenSearch, or existing project infrastructure.

Do not turn analytics into the transactional source of truth.

Do not expose arbitrary SQL execution.

Do not create a second reporting engine.

Do not create a separate authentication system for analytics.

Do not store message content merely for analytics.

Do not expose exact location history as a general-purpose reporting dataset.

Do not invent legal retention periods.

Do not create another backend analytics volume.

Do not create a surprise integration phase.

# REPOSITORY INSPECTION REQUIREMENTS

Before implementation:

1. Inspect the backend repository.
2. Inspect Backend Volumes 1–9 implementation.
3. Inspect all domain event definitions.
4. Inspect Kafka/Redpanda consumers and topic conventions.
5. Inspect database and projection patterns.
6. Inspect OpenSearch projections if already present.
7. Inspect S3/export infrastructure.
8. Inspect job/queue infrastructure.
9. Inspect authorization and audit.
10. Inspect data-lifecycle conventions.
11. Read the analytics/reporting contracts.
12. Determine exactly which files require creation or modification.

Do not create a competing analytics foundation.

# IMPLEMENTATION RULES

## Preserve Existing Foundations

Reuse:

* event infrastructure
* database
* jobs
* object storage
* authorization
* audit
* observability
* configuration
* lifecycle management

## Source-of-Truth Discipline

Analytics must never silently become authoritative for operational state.

## Metric Versioning

Do not change metric meaning without changing the metric version.

## Idempotency

Projection processing and report jobs must be safe under retries.

## Event-Time Correctness

Late events must follow explicit event-time semantics.

## Query Safety

No arbitrary client SQL.

## Privacy

Minimize sensitive analytical data.

## Bounded Work

Backfills, reports, and exports must be bounded and cancellable.

## No Placeholder Work

Every required capability must be implemented completely.

# VALIDATION REQUIREMENTS

Execute all supported validation.

At minimum:

* TypeScript compilation
* linting
* formatting
* unit tests
* API integration tests
* Prisma validation
* migration validation
* Kafka/Redpanda event-consumer tests
* projection tests
* job tests
* S3/export tests where available
* OpenAPI validation
* authorization tests
* privacy/security tests
* dependency/security scanning where configured

Test:

* duplicate event
* late event
* out-of-order event
* malformed event
* projection rebuild
* replay
* freshness tracking
* metric versioning
* reconciliation mismatch
* report authorization
* filter correctness
* report timeout
* export authorization
* export retry
* export expiration
* queue isolation
* consumer restart

Do not claim measured analytical throughput or freshness without actual test evidence.

# FINAL INTEGRATION CHECK

Before declaring this milestone complete:

1. Verify analytics remains downstream of authoritative domains.
2. Verify metric definitions are explicit and versioned.
3. Verify event ingestion validates schemas.
4. Verify duplicates do not inflate aggregates.
5. Verify late/out-of-order events are handled according to event time.
6. Verify time buckets are consistent.
7. Verify trip analytics use authoritative trip facts.
8. Verify dispatch analytics use authoritative dispatch events.
9. Verify supply/demand definitions are explicit.
10. Verify financial analytics use authoritative financial facts.
11. Verify earnings/payout analytics do not become the balance source of truth.
12. Verify ratings/notification/messaging analytics protect private data.
13. Verify safety/support/risk analytics are appropriately restricted.
14. Verify fleet/scheduled-trip analytics use authoritative domain events.
15. Verify projections expose freshness.
16. Verify rebuilds and backfills are safe and bounded.
17. Verify data-quality checks detect important anomalies.
18. Verify reconciliation is non-destructive.
19. Verify reports cannot execute arbitrary SQL.
20. Verify exports are private and expire.
21. Verify analytics authorization is separate from ordinary user access.
22. Verify sensitive data is excluded from telemetry.
23. Verify workload isolation protects near-realtime projections.
24. Verify failure/recovery behavior is implemented.
25. Verify audit exists for privileged analytics operations.
26. Verify tests cover duplicates, lateness, rebuilds, authorization, and exports.
27. Verify compatibility with Backend Volumes 1–9.
28. Verify this completes the planned backend sequence.
29. Verify no placeholder or competing analytics implementation remains.

# DEFINITION OF DONE

This milestone is complete only when:

* analytics domain exists
* metric definitions exist
* metric versioning exists
* analytics event ingestion exists
* canonical analytical event model exists
* event deduplication exists
* late/out-of-order handling exists
* time-bucket aggregation exists
* trip analytics exist
* dispatch analytics exist
* supply/demand analytics exist
* pricing analytics exist
* payment analytics exist
* earnings/payout analytics exist
* ratings analytics exist
* notification analytics exist
* messaging analytics exist without storing message content unnecessarily
* safety analytics exist
* support analytics exist
* fleet analytics exist
* scheduled-trip analytics exist
* regional/market dimensions exist
* dimension governance exists
* projection architecture exists
* projection freshness exists
* rebuilds exist
* backfills exist
* data-quality checks exist
* reconciliation exists
* report definitions exist
* reporting APIs exist
* report performance controls exist
* report caching exists where appropriate
* export jobs exist
* export security exists
* export lifecycle exists
* analytics authorization exists
* retention integration exists
* analytics events exist where required
* background jobs exist
* queue isolation exists
* analytics observability exists
* tracing exists
* security/privacy controls exist
* audit exists
* APIs conform to the architecture
* tests cover normal, adversarial, and recovery flows
* documentation is updated
* no new warehouse/lakehouse has been unnecessarily introduced
* analytics remains derived rather than authoritative
* no placeholder implementation remains
* validation results are truthful
* the backend sequence is complete

# IMPLEMENTATION REPORT

At completion, provide:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Analytics Architecture

Summarize:

* event ingestion
* metric definitions
* projection architecture
* time buckets
* freshness

## Domain Analytics

Summarize:

* trips
* dispatch
* supply/demand
* pricing
* payments
* earnings/payouts
* ratings
* notifications
* messaging
* safety
* support
* fleet
* scheduled trips

## Data Quality and Reconciliation

Summarize:

* validation
* late-event handling
* duplicate detection
* reconciliation
* rebuilds
* backfills

## Reporting

Summarize:

* metric/report definitions
* APIs
* filters
* authorization
* caching
* performance controls

## Exports

Summarize:

* generation
* S3 storage
* security
* expiration
* cleanup

## Security and Privacy

Summarize:

* access control
* financial restrictions
* safety/risk restrictions
* location privacy
* audit

## Events and Jobs

Summarize:

* consumers
* projection jobs
* rebuild jobs
* quality checks
* reconciliation
* export jobs

## Database and Storage

Summarize:

* projections
* indexes
* aggregates
* Redis use
* OpenSearch use where applicable
* S3 exports

## API

Summarize implemented analytics/reporting endpoints.

## Tests and Validation

List actual commands and actual outcomes.

## External Environment Limitations

State any external Kafka, AWS, object-storage, or production analytics infrastructure that could not be exercised.

Do not fabricate production-scale or freshness results.

## Architectural Decisions

Record meaningful analytics implementation decisions.

## Known Limitations

List genuine remaining limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement Backend Volume 10 completely.

Extend the existing backend, event, database, job, object-storage, authorization, audit, and observability foundations.

Implement metric definitions, analytics ingestion, projections, time-bucket aggregation, late-event handling, trip/dispatch/supply-demand/pricing/payment/earnings/ratings/notification/messaging/safety/support/fleet/scheduled-trip analytics, data-quality checks, freshness, rebuilds, reconciliation, reporting APIs, and secure exports.

Keep every source domain authoritative for its own operational state.

Do not introduce a new warehouse/lakehouse or competing analytics platform.

Do not expose arbitrary SQL.

Do not store sensitive message content or precise location history unnecessarily.

Do not leave placeholders.

Do not fabricate analytical throughput, freshness, or production results.

Run every validation command supported by the environment.

Verify analytical correctness, idempotency, late-event handling, authorization, privacy, reconciliation, rebuild safety, report performance, export security, and failure recovery.

Finish with the required implementation report and leave the repository in a coherent production-grade state with the planned backend phase complete.
