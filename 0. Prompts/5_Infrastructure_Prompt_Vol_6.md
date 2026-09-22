# Uber-Style Global Ride-Hailing & Mobility Platform — Infrastructure Prompt — Volume 6

## ROLE

You are acting as the complete senior infrastructure, site reliability, performance, resilience, security, cloud operations, release, and technical documentation organization responsible for implementing the project's final infrastructure engineering scope.

Operate as a coordinated:

* Principal Software Architect
* Cloud Architect
* Staff Platform Engineer
* Staff DevOps Engineer
* Site Reliability Engineer
* Performance Engineer
* Distributed Systems Engineer
* Infrastructure Security Engineer
* Database Reliability Engineer
* Kubernetes Engineer
* Networking Engineer
* Capacity Engineer
* Resilience Engineer
* QA Engineer
* Technical Writer

You are an implementation agent, not a teacher.

Your responsibility is to inspect the repository and implement the complete **capacity, resilience, disaster-recovery validation, operational hardening, maintenance, and day-2 operations** scope covered by this prompt without breaking existing application or infrastructure behavior.

Do not merely describe how the platform should scale or recover. Create the real repository-side infrastructure configuration, automation, tests, load/resilience tooling, capacity models, operational documentation, maintenance mechanisms, and runbooks required by this scope, and execute live operations only when the environment genuinely permits them.

This is the final infrastructure implementation volume.

Do not create another infrastructure volume, final-integration volume, hidden QA phase, or surprise production-readiness phase.

---

# PROJECT

## Project

**Uber-Style Global Ride-Hailing & Mobility Platform**

## Product

A production-grade global ride-hailing and mobility platform supporting:

* riders
* drivers
* dispatch
* realtime communication
* payments
* earnings
* scheduled trips
* safety
* support
* fleet operations
* analytics
* global geographic operations

## Scale Target

The architecture targets:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* 100,000+ concurrent realtime sessions and higher
* high-frequency driver-location ingestion
* global and multi-region operation

These are architecture targets, not claims that this repository has already demonstrated those capacities.

All capacity estimates in this volume must be clearly identified as:

* architectural targets
* modeled estimates
* benchmark results
* or production-observed measurements

Do not represent modeled or assumed capacity as tested capacity.

---

# SOURCE OF TRUTH

The repository is the source of truth for the current implementation and infrastructure state.

Before changing anything:

1. Inspect the complete repository.
2. Inspect:

   * backend
   * frontend
   * mobile
   * shared libraries
   * Docker
   * Terraform
   * Helm
   * Kubernetes
   * GitHub Actions
   * deployment scripts
   * environment configuration
   * observability
   * security configuration
   * database configuration
   * Redis
   * Kafka/Redpanda
   * OpenSearch
   * S3
3. Inspect existing:

   * autoscaling
   * resource requests/limits
   * PDBs
   * topology constraints
   * multi-region configuration
   * DNS/failover configuration
   * backups
   * retention
   * monitoring
   * alerts
   * SLOs
   * deployment controls
   * health endpoints
   * rollback procedures
4. Inspect application metrics and telemetry already implemented.
5. Inspect infrastructure documentation and existing runbooks.
6. Determine the actual workload architecture and current deployment topology.
7. Determine which services are:

   * stateless
   * stateful
   * realtime
   * location-heavy
   * queue/worker-driven
   * read-heavy
   * write-heavy
   * latency-sensitive
   * batch/analytics-oriented
8. Determine the existing failure domains:

   * pod
   * node
   * availability zone
   * region
   * dependency
   * provider
9. Determine what resilience/capacity tooling already exists.
10. Preserve compatible working behavior.
11. Extend existing infrastructure instead of creating parallel operational systems.
12. Do not invent workloads, dependencies, traffic levels, SLIs, or operational guarantees that are not supported by repository evidence or explicitly stated architectural requirements.
13. Where a desired validation depends on infrastructure that is unavailable, implement the repository-side test/automation and document exactly what could not be executed.

This prompt is independently executable.

Do not depend on another AI conversation or another prompt being pasted into the repository.

---

# INFRASTRUCTURE TARGET

The platform is intended to operate across:

* AWS
* Amazon EKS
* multiple availability zones
* potentially multiple regions
* Kubernetes
* PostgreSQL/PostGIS
* Redis
* Kafka or Redpanda
* OpenSearch
* S3
* Route 53
* CloudFront where applicable
* WAF
* GitHub Actions
* OpenTelemetry
* Prometheus
* Grafana
* Loki
* Tempo
* automated deployments
* backup/recovery systems

The previous infrastructure volumes established:

1. Foundational infrastructure
2. Kubernetes/EKS
3. Stateful production data
4. Observability/security operations
5. CI/CD and global delivery

This volume completes the infrastructure engineering program with:

* capacity modeling
* performance testing
* scaling validation
* resilience testing
* failover validation
* disaster-recovery validation
* operational hardening
* cost controls
* maintenance procedures
* upgrade safety
* drift detection boundaries
* incident response
* runbooks
* day-2 operations
* lifecycle management

No additional infrastructure volume may be created.

---

# MISSION

Implement and validate the operational engineering needed to keep the platform reliable under:

* normal load
* peak load
* burst load
* dependency degradation
* instance/node failure
* pod failure
* availability-zone failure
* region failure
* queue backlog
* consumer lag
* database pressure
* Redis pressure
* search pressure
* provider failures
* network degradation
* partial outages
* deployment failures
* certificate/domain issues
* observability failures
* backup/restore scenarios

Establish:

* explicit capacity models
* measurable performance budgets
* load-test tooling
* stress-test tooling
* concurrency-test tooling
* realtime load testing
* location-ingestion load testing
* dispatch throughput testing
* database-load testing
* event-stream testing
* queue/backlog testing
* autoscaling validation
* resource-rightsizing methodology
* failure-injection tooling where safe
* AZ resilience validation
* node resilience validation
* pod disruption validation
* dependency-failure validation
* regional failover procedures
* backup/restore validation
* disaster-recovery procedures
* RTO/RPO validation boundaries
* cost visibility
* cost guardrails
* maintenance procedures
* upgrade procedures
* infrastructure drift detection
* incident response
* operational runbooks
* service ownership
* lifecycle and decommissioning procedures

The goal is not merely to prove that the platform can survive every possible failure.

The goal is to establish a repeatable engineering system for measuring, validating, recovering from, and operating the platform under realistic conditions.

---

# CAPACITY ENGINEERING

## 1. Capacity Model

Create a repository-side capacity model for the actual platform architecture.

Model, where supported:

* requests per second
* trips per second
* trips per day
* driver-location updates per second
* websocket connections
* websocket message throughput
* dispatch candidate evaluations
* dispatch offers
* payment operations
* notification throughput
* messaging throughput
* support/safety event throughput
* Kafka/Redpanda event rate
* worker job throughput
* PostgreSQL transactions/second
* database connections
* Redis operations/second
* Redis memory
* OpenSearch indexing rate
* OpenSearch query rate
* S3 object throughput

Document assumptions.

Do not fabricate traffic distributions.

Where real product measurements do not exist, use explicit modeled assumptions.

---

# 2. Capacity Targets Versus Observed Capacity

For each critical workload, distinguish:

* architectural target
* modeled requirement
* local benchmark
* staging benchmark
* production observation

Never claim:

> "supports 100 million riders"

solely because the architecture document states that as a target.

Capacity must be evidence-based.

---

# 3. Performance Budgets

Establish measurable performance budgets for key services.

Potential measurements:

* API p50/p95/p99 latency
* dispatch latency
* fare-quote latency
* payment operation latency
* websocket message latency
* location-ingestion latency
* notification-delivery processing latency
* queue processing latency
* database latency
* search latency

Use existing SLO/SLI architecture.

Do not invent numbers without documented rationale.

When a target is unavailable, establish a clearly labeled initial budget and document that it requires validation.

---

# 4. Workload Profiles

Define realistic test profiles for:

* normal
* peak
* burst
* sustained high load
* recovery after burst
* degraded dependency
* high websocket concurrency
* high location-ingestion rate
* high dispatch demand
* high scheduled-trip demand
* high messaging activity

Keep workload mixes configurable.

Do not bake one unrealistic synthetic workload into every test.

---

# 5. Test Data Strategy

Create realistic but synthetic test data generation for load testing.

Support:

* riders
* drivers
* vehicles
* trips
* locations
* dispatch requests
* scheduled trips
* payment states
* messages
* notifications

Requirements:

* synthetic identifiers
* controlled geographic distributions
* reproducibility
* deterministic seeds where useful
* cleanup
* no production PII
* no production payment credentials

Do not copy real production customer data into test environments.

---

# LOAD AND PERFORMANCE TESTING

## 6. API Load Testing

Implement load tests for actual high-value API paths.

Prioritize:

* authentication/session flows where safe
* trip creation
* quote/fare requests
* trip status retrieval
* dispatch-related endpoints
* trip history
* payment-related read operations
* scheduled-trip operations
* support/safety reads
* operational APIs

Use the repository's actual API contracts.

Do not create load tests against fictional endpoints.

---

# 7. Realtime Load Testing

Implement realistic websocket load testing.

Measure:

* connection establishment rate
* concurrent connections
* message throughput
* subscription behavior
* reconnect behavior
* connection lifetime
* event delivery latency
* server resource consumption

Target the architecture's 100,000+ concurrent-session goal only as a test target.

Do not claim achievement until a reproducible benchmark demonstrates it.

---

# 8. Driver Location Load Testing

Create a dedicated location-ingestion load profile.

Model:

* active drivers
* update frequency
* geographic distribution
* stale clients
* reconnects
* burst behavior
* duplicate updates
* out-of-order updates
* temporary network loss

Measure:

* ingestion rate
* processing latency
* Redis load
* database/PostGIS load where applicable
* event-stream load
* websocket propagation
* dropped/invalid updates

Do not use real user location data.

---

# 9. Dispatch Load Testing

Test the dispatch system under realistic demand.

Measure:

* request arrival rate
* candidate lookup
* assignment latency
* offer throughput
* offer expiration
* rejection
* reassignment
* contention
* geographic hot spots
* supply shortages
* demand bursts

Validate that infrastructure scaling does not create pathological dispatch behavior.

Do not claim dispatch quality metrics beyond what can actually be measured.

---

# 10. Database Load Testing

Test PostgreSQL/PostGIS against representative workloads.

Cover:

* trip writes
* trip reads
* location/spatial queries
* rider/driver lookups
* dispatch spatial queries
* payment/ledger writes
* scheduled-trip queries
* support/safety queries
* concurrent transactions

Measure:

* query latency
* CPU
* memory
* storage I/O
* connections
* lock contention
* deadlocks
* replication behavior

Use representative indexed workloads.

Do not run destructive stress tests against production.

---

# 11. Redis Load Testing

Test actual Redis workload classes.

Cover:

* cache reads/writes
* idempotency
* locks
* rate limiting
* presence
* location state
* queue operations where applicable

Measure:

* operations/sec
* latency
* memory
* eviction
* connections
* replication/failover behavior

Test critical Redis workloads separately where their durability/eviction semantics differ.

---

# 12. Kafka / Redpanda Load Testing

Test event-stream workloads.

Cover:

* producer throughput
* consumer throughput
* partition distribution
* consumer lag
* burst traffic
* rebalance behavior
* backlog recovery

Measure:

* events/sec
* bytes/sec
* latency
* lag
* storage
* replication behavior

Do not claim exactly-once business semantics merely because transport-level performance is good.

---

# 13. OpenSearch Load Testing

Test:

* indexing
* search
* aggregation where actually used
* concurrent queries
* shard distribution
* indexing bursts
* recovery after degraded nodes

Measure:

* indexing latency
* search latency
* CPU
* memory
* storage
* rejected requests
* queue depth

Do not make OpenSearch the source of truth in performance tests if it is architecturally a derived system.

---

# 14. S3 Performance and Lifecycle Validation

Validate relevant S3 workloads such as:

* media upload
* receipt/object retrieval
* private evidence access
* exports

Where applicable, test:

* throughput
* request rate
* authorization
* lifecycle behavior
* replication state

Do not upload real private data into non-production test environments.

---

# 15. End-to-End Performance Tests

Create representative end-to-end scenarios.

Examples:

### Rider Request

* rider authentication
* location
* quote
* trip request
* dispatch
* driver assignment
* realtime tracking

### Driver Workflow

* driver authentication
* online transition
* location stream
* offer
* acceptance
* pickup
* active trip
* completion

### Financial Workflow

* quote
* payment authorization
* completion
* capture
* receipt
* earnings

### Scheduled Trip

* creation
* pre-dispatch
* assignment
* active trip
* completion

Measure latency and failure rates at each significant stage.

---

# AUTOSCALING AND RESOURCE VALIDATION

## 16. HPA Validation

Validate actual autoscaling behavior.

Test:

* scale-up
* scale-down
* burst response
* stabilization
* minimum replicas
* maximum replicas
* workload recovery

Use actual application metrics where possible.

Do not use synthetic CPU load alone to claim application scalability.

---

# 17. Worker Scaling

Validate scaling of:

* BullMQ workers
* Kafka consumers
* asynchronous processors
* notification workers
* analytics consumers

Measure:

* backlog
* processing rate
* recovery time

Do not scale consumers beyond what underlying partitions/queue semantics can usefully support.

---

# 18. Database Connection Scaling

Validate:

* connection limits
* pool sizes
* pod scaling
* migration processes
* worker connection usage

Identify connection-exhaustion thresholds.

Do not increase connection counts indefinitely as a substitute for capacity engineering.

---

# 19. Resource Right-Sizing

Use load-test evidence to identify:

* underprovisioned workloads
* overprovisioned workloads
* memory leaks
* CPU bottlenecks
* connection bottlenecks
* I/O bottlenecks

Update repository-side starting configuration only where justified by measured evidence.

Do not optimize based solely on theoretical assumptions.

---

# RESILIENCE ENGINEERING

## 20. Pod Failure

Validate recovery from:

* pod termination
* crash loops
* readiness loss
* abrupt process termination

Verify:

* traffic shifts
* Kubernetes restarts
* realtime reconnection
* queue consumers recover
* no duplicate destructive processing occurs

---

# 21. Node Failure

Validate behavior after worker-node loss.

Verify:

* pod rescheduling
* PDB behavior
* topology distribution
* service availability
* worker recovery
* realtime session impact
* observability continuity

Do not claim zero connection loss for realtime sessions unless demonstrated.

---

# 22. Availability-Zone Failure

Where environment access permits, test AZ-level degradation/failure.

Validate:

* workload redistribution
* load balancer behavior
* database failover
* Redis failover
* Kafka/Redpanda availability
* application availability
* SLO impact

Document which components are:

* AZ-resilient
* AZ-sensitive
* region-sensitive

Do not claim AZ resilience solely from multi-AZ configuration.

---

# 23. Database Failover

Validate the database failover procedure where safe.

Test:

* failover initiation where supported
* connection recovery
* application retry behavior
* transaction behavior
* worker behavior
* stale connection recovery

Do not perform destructive production failover tests.

---

# 24. Redis Failover

Validate:

* failover
* client reconnect
* transient errors
* cache recovery
* operational state recovery
* queue behavior if Redis is used for queues

Distinguish recoverable cache loss from loss of operationally important state.

---

# 25. Kafka / Redpanda Failure

Test:

* broker failure
* partition unavailability
* consumer reconnect
* producer retry
* lag recovery
* duplicate/replayed messages

Verify idempotent consumers where required.

---

# 26. OpenSearch Failure

Test:

* node degradation
* shard relocation
* indexing backlog
* search failure
* recovery

Verify that search degradation does not corrupt canonical transactional workflows.

---

# 27. External Provider Failure

Where provider abstraction exists, test degraded behavior for:

* maps/routing
* payment provider
* notification provider
* other actual external providers

Validate:

* timeout
* retry
* fallback
* circuit behavior where implemented
* user-facing degradation
* alerting
* recovery

Do not claim fallback works unless a real test or deterministic simulation demonstrates it.

---

# 28. Network Degradation

Test realistic network conditions:

* latency injection
* packet loss
* transient disconnect
* DNS failure where safely simulated
* partial dependency loss

Focus on:

* API calls
* websocket sessions
* driver location
* dispatch
* payment
* messaging

Do not create unsafe network tests against shared production environments.

---

# 29. Deployment Failure

Validate behavior when:

* pod startup fails
* readiness fails
* image is invalid
* rollout stalls
* migration job fails
* dependency becomes unavailable during rollout

Confirm:

* rollout stops
* previous healthy release remains available where possible
* alerts fire
* rollback procedure works
* no hidden partial deployment state remains

---

# DISASTER RECOVERY

## 30. RTO / RPO Validation

For critical services, document and validate:

* recovery point objective
* recovery time objective
* actual observed recovery time
* actual observed data-loss window

Do not label an RTO/RPO as achieved unless tested.

If only architecture-level objectives exist, identify them as targets.

---

# 31. PostgreSQL Recovery Test

Perform non-destructive recovery testing where environment permits.

Validate:

* backup availability
* snapshot restoration
* PITR
* DNS/endpoint update where required
* application reconnection
* migration compatibility
* data-integrity checks

Do not overwrite production systems during a recovery drill.

---

# 32. Redis Recovery

Validate the documented recovery process appropriate to the Redis workload.

For rebuildable cache:

* verify clean rebuild

For operational state:

* verify durability/recovery assumptions

Do not claim zero data loss for inherently ephemeral Redis data.

---

# 33. Kafka / Redpanda Recovery

Validate:

* broker recovery
* topic availability
* offset behavior
* consumer-group recovery
* backlog catch-up

Where cross-region replication exists:

* validate replication health
* validate recovery path
* document lag limitations

---

# 34. OpenSearch Recovery

Validate:

* snapshot availability
* restore path
* shard restoration
* application reconnection
* rebuild path from canonical sources

Search recovery must not require corruption of the transactional system.

---

# 35. S3 Recovery

Validate:

* object version recovery where enabled
* replication recovery where configured
* lifecycle behavior
* private access after restoration

---

# 36. Regional Disaster Recovery

Where the architecture supports multiple regions, implement and document the regional recovery procedure.

Cover:

* regional application deployment
* stateful dependency recovery/replication
* global DNS/edge failover
* secrets/configuration
* observability
* data consistency implications
* rollback to primary region

Do not claim active-active global consistency unless the architecture actually provides it.

Distinguish:

* active-active
* active-passive
* warm standby
* cold recovery

---

# 37. Disaster-Recovery Runbooks

Create actionable runbooks for:

* regional outage
* database outage
* Redis outage
* Kafka/Redpanda outage
* OpenSearch outage
* major application outage
* provider outage
* certificate failure
* DNS failure
* compromised deployment
* failed migration
* unexpected data corruption

Runbooks must include:

* prerequisites
* detection
* verification
* safe actions
* escalation
* rollback
* recovery verification

Do not create fictional commands.

---

# COST AND FINANCIAL OPERATIONS

## 38. Cost Visibility

Implement repository-side infrastructure/cost metadata sufficient to identify major spend categories.

Cover:

* EKS
* EC2/node capacity
* RDS/Aurora
* Redis
* Kafka/Redpanda
* OpenSearch
* S3
* CloudFront
* data transfer
* observability storage

Use existing tags.

Do not claim exact monthly cost without current pricing/usage data.

---

# 39. Cost Guardrails

Implement where appropriate:

* non-production sizing defaults
* resource limits
* ECR cleanup
* log/trace retention
* S3 lifecycle
* idle-resource cleanup boundaries
* autoscaling ceilings
* environment shutdown procedures

Do not cripple production availability merely to minimize cost.

---

# 40. Capacity-to-Cost Analysis

Document the major scaling cost drivers.

Examples:

* realtime connections
* driver-location volume
* database I/O
* event throughput
* search indexing
* telemetry volume
* cross-region traffic

Use measured data where available.

Otherwise clearly mark assumptions.

---

# DAY-2 OPERATIONS

## 41. Operational Ownership

Establish ownership metadata/documentation for major services.

For each operational component document:

* owner/team
* criticality
* dependencies
* SLO
* dashboards
* alerts
* runbooks
* escalation path

Do not invent team names that are not established by the project. Use placeholders only for organizational ownership fields that genuinely cannot be assigned, and clearly identify them as configuration inputs rather than pretending they are actual owners.

---

# 42. Incident Response

Create an actionable incident-response framework.

Cover:

* detection
* severity
* triage
* mitigation
* communication
* escalation
* recovery
* verification
* post-incident review

Integrate with:

* alerts
* dashboards
* logs
* traces
* audit events
* deployment history

Do not build a fictional external incident-management integration when none exists.

---

# 43. Operational Runbooks

Create runbooks for the most important operational scenarios.

At minimum cover:

* API degradation
* realtime degradation
* location-ingestion overload
* dispatch degradation
* database saturation
* Redis pressure
* Kafka lag
* OpenSearch pressure
* provider outage
* deployment rollback
* failed migration
* certificate issue
* DNS issue
* regional failover

Runbooks must reference actual repository paths, commands, dashboards, and configuration.

---

# 44. Maintenance Windows

Document and, where infrastructure supports it, configure maintenance boundaries for:

* Kubernetes
* EKS nodes
* PostgreSQL
* Redis
* Kafka/Redpanda
* OpenSearch
* observability systems

Avoid scheduling incompatible maintenance operations simultaneously.

---

# 45. Upgrade Strategy

Establish safe upgrade procedures for:

* Kubernetes/EKS
* node images
* PostgreSQL versions
* Redis versions
* Kafka/Redpanda
* OpenSearch
* Helm
* Terraform providers
* application runtime dependencies

Cover:

* compatibility checks
* staging validation
* backup/recovery verification
* rollout
* rollback limitations

Do not automatically upgrade production dependencies without validation.

---

# 46. Infrastructure Drift

Implement practical drift-detection boundaries.

Support:

* Terraform plan checks
* scheduled plan/diff where appropriate
* configuration comparison
* Kubernetes drift awareness

Do not create a second infrastructure-management system.

---

# 47. Certificate Lifecycle

Operationalize certificate monitoring.

Support:

* expiration visibility
* renewal validation
* alarms where appropriate
* dependency tracking
* emergency replacement procedure

Do not wait for certificate expiry to discover renewal failures.

---

# 48. Secret Rotation

Operationalize secrets rotation where supported.

Document:

* rotation source
* consumers
* reload/restart behavior
* validation
* rollback

Do not rotate credentials automatically if consumers cannot safely handle rotation.

---

# 49. Backup Monitoring

Create monitoring and operational checks for:

* backup existence
* backup age
* backup failure
* replication failure
* retention compliance

Do not treat "backup resource configured" as equivalent to "recoverable backup."

---

# 50. Recovery Verification

After recovery operations:

* verify application health
* verify data integrity where applicable
* verify queues/consumers
* verify search projections
* verify object access
* verify realtime
* verify alerts
* verify global routing
* verify user-facing functionality

Recovery is not complete merely because infrastructure is running.

---

# 51. Scheduled Operational Checks

Implement or document recurring checks for:

* certificates
* backups
* replication
* infrastructure drift
* unused resources
* ECR lifecycle
* stale deployments
* failed jobs
* consumer lag
* storage pressure
* expired credentials
* unhealthy regions

Use automation where safe.

---

# 52. Capacity Review Process

Document a recurring capacity-review procedure.

Review:

* traffic growth
* realtime sessions
* location rate
* dispatch volume
* DB utilization
* Redis utilization
* Kafka throughput
* OpenSearch utilization
* observability costs
* regional distribution

Capacity changes should be evidence-driven.

---

# 53. Scaling Runbooks

Create runbooks for scaling:

* API workloads
* realtime workloads
* dispatch workloads
* workers
* database capacity
* Redis
* Kafka/Redpanda
* OpenSearch

Document safe scaling steps and rollback.

---

# 54. Data Lifecycle Operations

Operationalize:

* retention
* archival
* expiration
* object lifecycle
* search index lifecycle
* event retention
* backup retention

Ensure operational lifecycle actions match architecture-defined retention.

---

# 55. Decommissioning

Document safe decommissioning for:

* retired services
* old Helm releases
* unused infrastructure
* old ECR images
* old dashboards
* stale DNS
* obsolete secrets
* deprecated Kafka topics
* retired search indices

Require explicit dependency verification before destruction.

---

# 56. Operational Access Review

Document recurring access reviews for:

* AWS IAM
* EKS
* Grafana
* observability systems
* databases
* security systems

Use least privilege.

Remove stale access.

Do not create shared permanent administrator credentials.

---

# 57. Security Hardening Review

Create recurring checks for:

* privileged containers
* broad IAM permissions
* public endpoints
* expired certificates
* exposed secrets
* outdated images
* vulnerable dependencies
* insecure Kubernetes configuration
* WAF changes
* security-group drift

Do not duplicate the entire security program from Infrastructure Volume 4; operationalize the existing controls.

---

# RESILIENCE AUTOMATION

## 58. Safe Failure-Injection Tooling

Where appropriate, create controlled failure-injection tooling for:

* pod deletion
* worker termination
* network delay/loss
* dependency unavailability
* queue backlog
* broker/node failure simulation
* application process termination

Requirements:

* explicit environment guardrails
* production blocking by default
* confirmation
* clear target selection
* logging/audit
* cleanup/recovery

Never make destructive failure injection accidentally runnable against production.

---

# 59. Chaos-Test Boundaries

Where chaos tooling is introduced:

* scope it to non-production by default
* define blast radius
* define abort criteria
* define expected outcome
* capture metrics
* capture recovery time
* document findings

Do not introduce a complex chaos platform merely for appearance.

---

# 60. Resilience Test Matrix

Create a matrix covering:

* failure
* affected component
* expected behavior
* measurable SLO impact
* recovery mechanism
* observed result
* remaining gap

This matrix must reflect actual tested scenarios.

Do not mark scenarios "passed" without evidence.

---

# PERFORMANCE AND RESILIENCE RESULTS

## 61. Benchmark Reporting

Create machine-readable and human-readable benchmark results where practical.

Include:

* test version
* commit
* environment
* workload
* duration
* concurrency
* throughput
* latency
* errors
* resource utilization
* bottleneck observations

Do not overwrite previous benchmark history without preserving comparison ability.

---

# 62. Regression Thresholds

Establish automated performance-regression boundaries where justified.

Examples:

* latency regression
* throughput regression
* error-rate regression
* resource-utilization regression

Avoid brittle thresholds that make CI unusable.

Use baseline comparisons only where measurements are repeatable.

---

# 63. Performance Result Traceability

Each benchmark result should be traceable to:

* source commit
* infrastructure version
* test version
* configuration
* environment

Do not compare incomparable environments without clearly stating the difference.

---

# 64. Capacity Gaps

Document known capacity gaps such as:

* untested scale targets
* single-region dependencies
* provider bottlenecks
* database limits
* websocket constraints
* location-ingestion limits
* cost ceilings
* recovery gaps

Do not present unresolved gaps as completed work.

---

# AUTOMATION AND OPERATIONAL TOOLING

## 65. Operational Scripts

Create safe scripts/utilities for repeatable operations such as:

* health verification
* deployment verification
* rollback checks
* backup verification
* connectivity checks
* queue checks
* consumer-lag checks
* certificate checks
* drift checks
* capacity report generation

Scripts must:

* fail safely
* have explicit environment targeting
* avoid destructive defaults
* provide useful output
* return meaningful exit codes

---

# 66. Environment Guardrails

For every potentially destructive operational script:

* require explicit environment
* reject production by default for destructive actions
* require an explicit confirmation mechanism where appropriate
* validate target account/region
* print the intended target before execution

Do not rely solely on human caution.

---

# 67. Operational Configuration

Centralize safe operational parameters where practical.

Do not scatter production thresholds across scripts.

Configuration must be:

* typed/validated where appropriate
* documented
* environment-aware

---

# 68. Runbook Command Accuracy

Every command referenced in a runbook must correspond to:

* an actual script
* an actual Terraform target
* an actual Helm command
* an actual AWS/Kubernetes command
* or an explicitly documented manual action

Do not document commands that were invented but never validated.

---

# 69. Operational Logs and Auditability

Operational scripts/actions should produce:

* timestamp
* operator identity where available
* environment
* region
* target
* action
* result

Do not log secrets.

---

# 70. Documentation Index

Create a discoverable operations documentation index linking:

* dashboards
* alerts
* runbooks
* recovery procedures
* deployment procedures
* scaling procedures
* maintenance procedures
* benchmark results
* resilience tests
* ownership
* escalation guidance

The operations team should not need to search the entire repository to find the correct runbook.

---

# OUT OF SCOPE

This is the final infrastructure volume.

Do not create another infrastructure phase.

Explicitly out of scope:

* new application product functionality
* backend domain redesign
* frontend feature development
* mobile feature development
* new database schemas
* new dispatch architecture
* new payment architecture
* new messaging architecture
* unrelated security products
* speculative infrastructure for services not present in the repository
* rebuilding the Kubernetes platform from scratch
* replacing the observability platform
* redesigning CI/CD
* creating another global-delivery architecture
* a separate QA-only phase
* a separate final-integration or production-readiness phase

Do not invent a "final cleanup", "final integration", "post-production readiness", or "Volume 7".

This volume is the terminal infrastructure milestone.

---

# IMPLEMENTATION RULES

## Evidence-Based Capacity

Do not state that a target has been achieved without benchmark evidence.

Always distinguish:

* target
* assumption
* modeled value
* measured value
* production observation

## Safe Testing

Never run destructive performance or resilience experiments against production merely to satisfy a prompt.

Use:

* local
* test
* staging
* isolated environments

where practical.

Production validation must be non-destructive unless there is an explicitly approved operational procedure.

## Production Guardrails

Destructive scripts must:

* require explicit targeting
* reject production by default
* validate account/region
* provide confirmation
* produce audit output

## Preserve Existing Architecture

Extend:

* Terraform
* EKS
* Helm
* stateful infrastructure
* observability
* CI/CD
* global delivery

Do not create competing platforms.

## No Fake Results

Do not mark a:

* benchmark
* failover
* restore
* chaos test
* scaling test
* recovery

as successful unless evidence exists.

## External-Access Reality

The implementation environment may lack:

* AWS credentials
* EKS access
* production services
* staging services
* sufficient load-generation infrastructure
* access to external providers

When live testing is unavailable:

* implement the test/tooling infrastructure
* run all local/static tests possible
* produce dry-run or configuration validation where appropriate
* clearly state what was not executed
* do not fabricate results

## Data Safety

Use synthetic test data.

Never load real production PII, payment credentials, messages, precise locations, or safety evidence into load-test fixtures.

## No Pseudo-Code

Create actual:

* load-test programs
* benchmark scripts
* Terraform
* Helm/Kubernetes configuration
* resilience tooling
* recovery scripts
* operational scripts
* runbooks
* documentation
* test harnesses
* validation utilities

Do not use placeholder scripts presented as complete.

---

# VALIDATION REQUIREMENTS

Before considering this volume complete:

## Repository and Configuration

1. Inspect the entire repository.
2. Validate Terraform formatting.
3. Validate Terraform syntax.
4. Run Terraform static analysis.
5. Validate Helm charts.
6. Render Kubernetes manifests.
7. Validate infrastructure security controls.
8. Validate environment guardrails.
9. Validate operational script syntax.
10. Validate documentation links/references where tooling permits.

## Performance

11. Execute API load tests where infrastructure permits.
12. Execute websocket load tests where infrastructure permits.
13. Execute driver-location load tests where infrastructure permits.
14. Execute dispatch load tests where infrastructure permits.
15. Execute database load tests where infrastructure permits.
16. Execute Redis load tests where infrastructure permits.
17. Execute Kafka/Redpanda load tests where infrastructure permits.
18. Execute OpenSearch load tests where infrastructure permits.
19. Execute relevant S3 performance/lifecycle tests where appropriate.
20. Execute representative end-to-end performance tests where feasible.
21. Capture throughput, latency, errors, and resource utilization.
22. Preserve benchmark artifacts/results.
23. Compare against defined performance budgets where repeatable.
24. Identify bottlenecks and document them.

## Scaling

25. Validate HPA behavior where possible.
26. Validate worker scaling.
27. Validate database connection behavior.
28. Validate resource limits.
29. Validate topology distribution.
30. Validate scale-down recovery.
31. Document measured scaling limits and untested targets.

## Resilience

32. Validate pod failure.
33. Validate node failure where possible.
34. Validate AZ resilience where safely possible.
35. Validate database failover where safely possible.
36. Validate Redis failover where safely possible.
37. Validate Kafka/Redpanda failure handling.
38. Validate OpenSearch failure/recovery.
39. Validate external-provider degradation where provider simulation is possible.
40. Validate network degradation.
41. Validate deployment failure.
42. Validate application recovery.
43. Preserve evidence for each resilience test.
44. Do not mark unexecuted tests as passed.

## Disaster Recovery

45. Validate PostgreSQL backup/PITR recovery where safe.
46. Validate Redis recovery assumptions.
47. Validate Kafka/Redpanda recovery.
48. Validate OpenSearch recovery/rebuild.
49. Validate S3 recovery.
50. Validate regional failover procedure where infrastructure permits.
51. Record observed recovery times.
52. Compare observed recovery with RTO/RPO targets.
53. Clearly document gaps.

## Day-2 Operations

54. Validate critical runbooks against real repository commands.
55. Validate backup monitoring.
56. Validate certificate monitoring.
57. Validate drift checks.
58. Validate maintenance procedures.
59. Validate upgrade procedures in non-production where possible.
60. Validate scaling scripts.
61. Validate operational script environment guardrails.
62. Validate incident-response references.
63. Validate ownership/documentation metadata.
64. Verify no destructive production-default operation exists.

## Security and Data Protection

65. Verify no production PII is present in test fixtures.
66. Verify no production secrets are present.
67. Verify load-test tools cannot accidentally target production without explicit overrides.
68. Verify destructive failure-injection tools are blocked from production by default.
69. Verify operational logs do not expose secrets.
70. Verify benchmark artifacts do not contain sensitive data.

## Final Quality

71. Verify no TODO/placeholder implementation was introduced.
72. Verify no fake benchmark result exists.
73. Verify no fake disaster-recovery result exists.
74. Verify no fake failover result exists.
75. Verify no fake production-capacity claim exists.
76. Verify no duplicate infrastructure platform was introduced.
77. Verify documentation matches actual implementation.
78. Verify the complete six-volume infrastructure architecture remains coherent.
79. Verify no additional infrastructure phase has been introduced.

Where a validation step cannot run due to environment limitations, perform every feasible repository-side or local validation and explicitly report the limitation.

---

# INTEGRATION CHECK

Before finalizing, verify that the completed platform integrates coherently across all infrastructure concerns.

Confirm that:

* capacity models reference actual services
* performance tests exercise actual APIs or explicitly documented test boundaries
* websocket tests use the deployed realtime architecture
* location tests use the real location-ingestion boundary
* dispatch tests use canonical dispatch contracts
* database tests reflect the actual PostgreSQL/PostGIS architecture
* Redis tests reflect actual workload classes
* event tests reflect Kafka/Redpanda contracts
* search tests reflect OpenSearch architecture
* S3 tests reflect real object categories
* HPA settings are consistent with observed workload behavior
* resource configurations are informed by evidence where available
* observability measures the same workloads being benchmarked
* alerts can identify the failures tested by resilience scenarios
* deployment metadata allows benchmark and outage results to be correlated with releases
* backups/recovery procedures align with the stateful infrastructure
* global failover procedures align with the CI/CD and routing architecture
* operational runbooks reference actual dashboards, scripts, resources, and commands
* maintenance procedures respect availability and recovery requirements
* destructive tools cannot accidentally target production
* lifecycle/decommissioning procedures do not destroy active dependencies
* capacity and cost controls do not silently undermine SLOs
* the final infrastructure state remains compatible with the completed backend, frontend, mobile, and application architecture

The complete infrastructure must function as one coherent operational system.

Do not leave conflicting duplicate operational systems behind.

---

# DEFINITION OF DONE

This final infrastructure volume is complete only when:

## Capacity

* capacity model is implemented
* assumptions are documented
* capacity targets are distinguished from measured capacity
* performance budgets are defined
* workload profiles are implemented
* synthetic test-data generation is implemented
* API load tests are implemented
* websocket load tests are implemented
* driver-location load tests are implemented
* dispatch load tests are implemented
* database load tests are implemented
* Redis load tests are implemented
* Kafka/Redpanda load tests are implemented
* OpenSearch load tests are implemented
* S3 testing is implemented where relevant
* end-to-end performance tests are implemented where feasible
* benchmark reporting is implemented
* regression thresholds are implemented where justified
* capacity bottlenecks are documented

## Scaling

* HPA behavior is validated where possible
* worker scaling is validated
* database connections are validated
* resource sizing is evidence-informed
* scale-up/down behavior is documented
* untested scale limits are explicit

## Resilience

* pod failure is tested
* node failure is tested where possible
* AZ resilience is tested where safely possible
* database failover is tested where safely possible
* Redis failover is tested where safely possible
* Kafka/Redpanda failure is tested
* OpenSearch failure/recovery is tested
* provider degradation is tested where possible
* network degradation is tested
* deployment failure is tested
* recovery behavior is documented

## Disaster Recovery

* RTO/RPO targets are documented
* observed recovery metrics are recorded where tested
* PostgreSQL recovery is tested where possible
* Redis recovery is documented/tested according to workload class
* Kafka/Redpanda recovery is tested
* OpenSearch recovery is tested
* S3 recovery is tested where applicable
* regional recovery is documented and tested where possible
* actual recovery gaps are documented

## Cost and Operations

* cost visibility metadata is implemented
* cost guardrails are implemented
* capacity-to-cost drivers are documented
* ownership metadata is documented
* incident-response framework is implemented
* critical runbooks are implemented
* maintenance procedures are documented
* upgrade procedures are documented
* drift detection is implemented/documented
* certificate lifecycle monitoring is implemented
* secret-rotation procedures are documented
* backup monitoring is implemented
* recovery verification is documented
* recurring operational checks are implemented/documented
* capacity-review process is documented
* scaling runbooks are implemented
* data-lifecycle procedures are documented
* decommissioning procedures are documented
* access-review procedures are documented
* security-hardening operational checks are documented
* safe failure-injection tooling is implemented where justified
* resilience test matrix is implemented
* operational documentation index is implemented

## Safety and Quality

* production destructive operations are guarded
* synthetic data is used for load testing
* no sensitive production data is present in tests
* no fake test results are reported
* no fake capacity claims are reported
* no fake failover/recovery claims are reported
* no placeholders remain
* no duplicate infrastructure systems were introduced
* all six infrastructure volumes remain coherent
* documentation matches actual implementation
* no seventh phase exists

---

# IMPLEMENTATION REPORT

At the end of execution, provide a concise but evidence-based report containing:

## Files Changed

List created, modified, and removed files.

## Capacity Engineering

Report:

* workload models
* load-test tooling
* benchmark tooling
* actual tests executed
* measured throughput/latency
* major bottlenecks
* untested targets

Do not report modeled capacity as measured capacity.

## Scaling

Report:

* HPA/worker scaling validation
* resource behavior
* connection behavior
* observed scaling limits

## Resilience

For each executed scenario, report:

* scenario
* environment
* target
* expected behavior
* observed behavior
* recovery result
* measured recovery time
* remaining gap

Do not list unexecuted scenarios as successful.

## Disaster Recovery

Report:

* backup/restore validation
* PITR validation
* stateful-service recovery
* regional recovery
* observed RTO/RPO
* remaining gaps

## Cost and Day-2 Operations

Report:

* cost metadata/guardrails
* runbooks
* maintenance procedures
* upgrade procedures
* drift checks
* certificate/secret rotation boundaries
* incident-response procedures
* decommissioning/lifecycle procedures

## Validation

Report the exact validation commands, test commands, benchmark commands, and results.

## External Infrastructure Status

Clearly state which operations were actually executed against:

* AWS
* EKS
* managed database services
* Redis
* Kafka/Redpanda
* OpenSearch
* S3
* Route 53
* CloudFront
* WAF
* live observability systems
* staging/production environments

and which could not be executed because of environment limitations.

Never infer live resilience or capacity from static configuration alone.

## Known Gaps

Report genuine remaining gaps such as:

* untested target scale
* unavailable external services
* unavailable device/load-generator infrastructure
* provider-specific limits
* unvalidated regional recovery paths

Do not hide limitations.

Do not invent additional project phases.

---

# FINAL EXECUTION DIRECTIVE

Inspect the entire repository first.

Then implement the complete final infrastructure engineering scope defined by this prompt.

Preserve all working application and infrastructure behavior outside the necessary scope of these changes.

Extend the six-volume infrastructure architecture already established rather than creating parallel operational platforms.

Create the real capacity models, load tests, realtime tests, location tests, dispatch tests, stateful-service tests, scaling validation, resilience tooling, recovery procedures, operational scripts, guardrails, runbooks, maintenance procedures, cost controls, benchmark reporting, and documentation required by this scope.

Do not merely describe how the platform could scale or recover.

Do not wait for another prompt.

Do not create another infrastructure volume.

Do not create a separate final-integration or production-readiness phase.

Do not use pseudo-code, placeholder test harnesses, fabricated benchmarks, fake failover results, fake disaster-recovery results, fake capacity claims, fabricated AWS state, or simulated production success presented as real.

Use synthetic data only for load and resilience testing.

Protect production with explicit environment guardrails.

Measure and report actual results where testing is possible.

Where live infrastructure access is unavailable, fully implement the repository-side tooling and validate everything possible locally and statically while clearly reporting what remains untested.

Treat performance, capacity, resilience, recovery, security, cost, maintainability, operational safety, and day-2 ownership as measurable engineering concerns rather than assumptions.

Finish only when the complete six-volume infrastructure program is genuinely implemented, validated to the extent the environment permits, documented, and operationally coherent with the rest of the project.
