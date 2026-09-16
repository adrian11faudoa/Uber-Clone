# UBER-STYLE RIDE-HAILING PLATFORM — INFRASTRUCTURE PROMPT — VOLUME 2

## ROLE

You are the senior infrastructure, cloud, reliability, security, performance, and platform engineering organization responsible for completing the production infrastructure of a globally scalable ride-hailing and mobility marketplace comparable in product depth and operational sophistication to Uber.

Operate as a coordinated team consisting of:

* Principal Software Architect
* Cloud Architect
* DevOps Engineer
* Site Reliability Engineer
* Security Engineer
* Database Architect
* Distributed Systems Engineer
* Performance Engineer
* QA Engineer
* Staff Backend Engineer
* Technical Writer

You are implementing production infrastructure against the existing repository.

You are not creating a tutorial, proof of concept, generic Kubernetes configuration, or infrastructure checklist.

Implement complete, operationally realistic infrastructure that supports high availability, horizontal scaling, secure operations, observability, disaster recovery, controlled releases, capacity growth, resilience testing, and production incident response.

The repository is the source of truth for what currently exists.

Do not assume that another AI prompt or previous conversation is available.

---

# PROJECT

Complete the production infrastructure for the Uber-style ride-hailing platform.

The infrastructure must support:

* rider web
* operations/admin web
* rider mobile
* driver mobile
* NestJS backend
* WebSocket gateways
* dispatch workers
* BullMQ workers
* Kafka consumers/producers
* PostgreSQL
* Redis
* search
* object storage
* CDN
* payment integrations
* mapping integrations
* notification providers
* analytics
* observability
* administration
* high availability
* regional expansion
* disaster recovery
* secure CI/CD
* capacity scaling
* operational resilience

Use the infrastructure foundation already present in the repository.

This volume focuses on:

* comprehensive observability
* alerting
* SLO/SLA support
* advanced autoscaling
* workload-specific scaling
* database resilience
* Redis resilience
* Kafka resilience
* backup and restore
* disaster recovery
* multi-region readiness
* security hardening
* compliance-oriented controls
* production capacity planning
* resilience testing
* deployment safety
* incident-response infrastructure
* cost governance
* operational runbooks
* infrastructure validation

Do not create a parallel cloud architecture.

---

# SOURCE OF TRUTH

Before modifying infrastructure, inspect:

* Terraform
* Kubernetes
* Helm
* AWS resources
* CI/CD
* EKS configuration
* node pools
* load balancing
* DNS
* certificates
* WAF
* PostgreSQL
* Redis
* Kafka
* search
* S3
* CloudFront
* secrets
* IAM
* existing observability
* application health endpoints
* metrics
* logs
* traces
* backend deployment profiles
* worker deployment profiles
* mobile release infrastructure

Preserve compatible infrastructure.

Do not replace working managed services without a documented operational reason.

Do not duplicate infrastructure resources.

Do not regenerate unchanged files.

---

# INFRASTRUCTURE SCOPE

This volume is responsible for:

* OpenTelemetry infrastructure integration
* Prometheus
* Grafana
* Loki
* Tempo
* CloudWatch integration
* centralized dashboards
* alerting
* SLO/SLA telemetry
* production autoscaling
* workload-specific scaling
* queue-based scaling
* Kafka-consumer scaling
* WebSocket scaling
* PostgreSQL resilience
* Redis resilience
* Kafka resilience
* search resilience
* S3 durability controls
* backup strategy
* restore procedures
* disaster recovery
* regional architecture readiness
* multi-region routing foundations
* security hardening
* compliance-oriented infrastructure controls
* infrastructure auditability
* vulnerability management
* capacity planning
* cost controls
* chaos/resilience testing
* deployment safety
* rollback automation
* operational runbooks
* incident-response support
* production validation

---

# OBSERVABILITY ARCHITECTURE

Implement a production-wide observability architecture covering:

* metrics
* logs
* traces
* infrastructure state
* business metrics
* Kubernetes
* AWS-managed services
* application workloads
* background jobs
* Kafka
* Redis
* PostgreSQL
* WebSockets
* external providers

Use:

* OpenTelemetry
* Prometheus
* Grafana
* Loki
* Tempo
* CloudWatch

where consistent with the existing repository.

Do not create multiple competing telemetry systems for the same signal.

---

# TELEMETRY FLOW

Define and implement the telemetry path from:

* application
* Kubernetes
* AWS infrastructure

into centralized observability systems.

Support:

* traces
* metrics
* logs

without sending excessive duplicate telemetry.

Production observability must remain useful during elevated load.

---

# TRACE ARCHITECTURE

Trace critical workflows end-to-end.

At minimum:

* ride request
* dispatch
* driver acceptance
* trip start
* trip completion
* payment
* refund
* earnings
* payout
* notification
* driver location ingestion
* scheduled ride
* support command
* administrative command

Trace context must cross:

* HTTP
* WebSocket
* PostgreSQL
* Redis
* BullMQ
* Kafka
* external providers

---

# TRACE SAMPLING

Use adaptive or policy-driven sampling where appropriate.

Always preserve:

* errors
* high-latency requests
* security-sensitive operations
* critical financial operations
* critical trip transitions

Do not sample all high-frequency location telemetry at full volume.

The trace system must remain operationally affordable at scale.

---

# METRICS ARCHITECTURE

Collect infrastructure and application metrics.

Infrastructure examples:

* CPU
* memory
* disk
* network
* pod health
* node capacity
* load balancer traffic
* database utilization
* Redis utilization
* Kafka lag
* object storage activity

Application examples:

* API latency
* request rate
* error rate
* active WebSocket connections
* location ingestion rate
* dispatch latency
* queue depth
* worker failures
* payment failures
* payout failures
* notification failures

Business metrics must use the backend definitions already established by the application.

---

# PROMETHEUS

Implement Prometheus-compatible metrics collection with production retention and scrape configuration.

Support:

* Kubernetes workloads
* backend services
* worker services
* infrastructure exporters where appropriate

Avoid cardinality explosions.

Do not label metrics with:

* user IDs
* trip IDs
* request IDs
* arbitrary coordinates

as high-cardinality Prometheus labels.

---

# GRAFANA

Create dashboards appropriate for:

## PLATFORM

* cluster health
* node capacity
* application availability
* API latency
* error rate

## RIDES

* ride requests
* dispatch latency
* match rate
* active trips
* cancellation

## REALTIME

* WebSocket connections
* connection errors
* location throughput
* stale-location ratio

## FINANCIAL

* payment success/failure
* refund backlog
* payout success/failure
* reconciliation discrepancies

## ASYNC

* queue depth
* job failure
* Kafka lag
* outbox lag
* dead letters

## DATA

* PostgreSQL connections
* CPU
* storage
* replication health
* Redis memory
* Redis evictions
* search health

Dashboards must use consistent naming and environment filters.

---

# LOKI

Centralize structured logs through Loki or the repository's established logging stack.

Logs must include:

* timestamp
* level
* service
* environment
* pod/workload
* request/correlation ID
* trace ID where available
* operation

Logs must be searchable by:

* service
* environment
* severity
* correlation ID
* trace ID
* relevant entity reference where safe

Do not log secrets.

---

# TEMPO

Integrate distributed traces using Tempo or the repository's established tracing backend.

Ensure trace/span metadata remains compatible with OpenTelemetry.

Do not store full sensitive payloads in traces.

---

# CLOUDWATCH

Integrate AWS service telemetry.

Capture appropriate metrics/logs for:

* ALB
* CloudFront
* WAF
* EKS
* RDS/Aurora
* ElastiCache
* Kafka/managed streaming
* S3
* Route 53
* IAM/security events where appropriate

Do not duplicate every CloudWatch metric into Prometheus without a reason.

---

# SLO ARCHITECTURE

Define measurable SLOs for critical workloads.

At minimum establish measurement support for:

* API availability
* API latency
* ride-request success
* dispatch latency
* realtime delivery
* location-ingestion availability
* payment processing
* payout processing
* notification delivery

Each SLO must specify:

* service
* indicator
* target
* measurement window
* error-budget interpretation

Do not create targets that cannot be measured reliably.

---

# ERROR BUDGETS

Where the repository supports error-budget tracking, expose:

* current budget
* consumption rate
* burn rate
* affected service

Production release policy may use burn-rate thresholds for deployment decisions.

Do not automatically block every deployment because of one isolated error without considering severity and scope.

---

# ALERTING

Create actionable alerts for:

* service outage
* elevated API latency
* high error rate
* dispatch degradation
* stale driver location
* payment failures
* payout failures
* queue backlog
* Kafka lag
* outbox lag
* dead-letter growth
* database saturation
* Redis memory pressure
* WebSocket failure
* search failure
* backup failure
* replication lag
* certificate expiration
* unusual WAF activity
* node capacity exhaustion

Alerts must include:

* severity
* affected service
* environment
* region
* metric/condition
* likely operational impact
* dashboard/runbook link where appropriate

---

# ALERT FATIGUE

Do not create alerts for every metric threshold.

Alerts must be:

* actionable
* deduplicated
* appropriately scoped
* severity-aware

Prefer composite conditions for incidents requiring multiple signals.

---

# ESCALATION

Define escalation levels for:

* warning
* critical
* security incident
* data-integrity incident
* financial incident

Do not build notification escalation that requires application code changes to modify operational recipients.

Use infrastructure/configuration mechanisms where practical.

---

# WORKLOAD-SPECIFIC AUTOSCALING

Different workloads must scale independently.

At minimum support independent scaling for:

* HTTP API
* WebSocket gateway
* location ingestion
* dispatch workers
* BullMQ workers
* Kafka consumers
* notification workers
* payment/reconciliation workers
* search/index workers
* analytics consumers

Do not use one global replica count.

---

# API AUTOSCALING

Scale API workloads based on appropriate signals such as:

* request rate
* CPU
* memory
* latency
* saturation

Use HPA or the repository's selected autoscaling mechanism.

Avoid scaling only from CPU when requests are primarily network-bound.

---

# WEBSOCKET AUTOSCALING

WebSocket gateway scaling must consider:

* connection count
* connections per pod
* message rate
* CPU
* memory

Use connection-aware telemetry.

Ensure clients can reconnect after pod termination.

Do not use a scaling configuration that causes aggressive connection churn.

---

# LOCATION SCALING

Driver location ingestion is a high-volume workload.

Scale based on:

* incoming update rate
* CPU
* Redis operation rate
* queue/backlog where used

Use backpressure.

Do not allow location spikes to exhaust the main API capacity.

---

# DISPATCH SCALING

Dispatch workers must scale based on:

* waiting dispatch operations
* assignment latency
* CPU
* geographic backlog

Do not allow one noisy geographic region to starve all other regions.

Where applicable, isolate workloads by region or shard.

---

# QUEUE AUTOSCALING

Scale BullMQ workers using queue depth/lag.

Different queues should have independent scaling where workload priorities differ.

Critical queues must not be starved by:

* analytics
* cleanup
* low-priority notifications

---

# KAFKA CONSUMER SCALING

Scale consumers based on:

* partition count
* consumer lag
* processing latency

Do not create more consumers than useful partitions.

Monitor rebalance behavior.

---

# DATABASE SCALING

Plan PostgreSQL scaling around:

* CPU
* memory
* connection usage
* IOPS
* storage
* replica lag
* query latency

Use read replicas only for workloads that tolerate eventual consistency.

Do not use replicas for authoritative state transitions.

---

# DATABASE HIGH AVAILABILITY

Ensure:

* multi-AZ primary/standby
* automated failover
* backups
* point-in-time recovery
* monitoring
* maintenance strategy

Applications must tolerate connection interruption and reconnect.

---

# DATABASE FAILOVER

Validate that:

* API retries safe reads
* transactions fail cleanly
* connection pools recover
* workers reconnect
* Kafka/outbox processing recovers
* no partial financial state is silently acknowledged

Do not blindly replay non-idempotent transactions after a database failover.

---

# READ REPLICAS

Where used, define explicit workloads.

Appropriate candidates may include:

* operational reporting
* large historical reads
* analytics preparation
* search/index backfills

Do not use replicas for:

* ride assignment
* payment authorization
* final trip state
* payout execution

when strong consistency is required.

---

# DATABASE BACKUPS

Configure:

* automated backups
* point-in-time recovery
* backup retention
* encryption
* monitoring
* cross-region backup strategy where appropriate

Backup failures must produce alerts.

---

# RESTORE PROCEDURES

Create documented and testable restoration procedures for PostgreSQL.

At minimum define:

1. Identify target recovery point.
2. Provision restore target.
3. Restore backup.
4. Validate schema.
5. Validate data integrity.
6. Rebuild derived systems as required.
7. Reconnect workloads in controlled order.
8. Verify critical business invariants.
9. Record recovery outcome.

Do not declare backup readiness without restore validation.

---

# REDIS RESILIENCE

Use a production highly available Redis architecture.

Support:

* replication
* failover
* encryption
* controlled maintenance
* monitoring

Redis loss must not corrupt authoritative business state.

---

# REDIS RECOVERY

Define which Redis state can be:

* rebuilt
* repopulated
* discarded

Examples:

* cache → rebuildable
* live location → recover from active drivers
* rate-limit counters → temporary
* durable financial state → must not be Redis-only

---

# KAFKA RESILIENCE

Configure:

* replication
* retention
* monitoring
* consumer recovery
* producer acknowledgment
* encryption
* authentication

Do not assume Kafka is infinitely durable.

---

# KAFKA RECOVERY

Define:

* topic recovery
* consumer offset recovery
* replay
* dead-letter handling
* schema compatibility

Critical domain events must remain recoverable from durable source state or appropriate event retention.

---

# KAFKA PARTITIONING

Review partitioning for:

* trip events
* payment events
* driver state
* ride requests

Use entity/aggregate keys where ordering is required.

Avoid:

* globally ordered single partitions
* hot keys
* random keys that destroy needed ordering

---

# SEARCH RESILIENCE

Search infrastructure must support:

* replication
* health checks
* snapshot/backup strategy where supported
* index versioning
* rebuild
* controlled failover

Search loss must not affect transactional truth.

---

# S3 DURABILITY

Protect critical S3 data with:

* encryption
* versioning where appropriate
* lifecycle
* restricted access
* object-lock/retention where legally required and supported
* replication where justified

Classify objects by importance.

---

# CDN RESILIENCE

CDN configuration must tolerate origin degradation where appropriate.

Do not cache:

* private user data
* active-trip dynamic state
* payment-sensitive responses

Configure cache invalidation for immutable assets.

---

# DISASTER RECOVERY MODEL

Define recovery architecture for:

* regional failure
* availability-zone failure
* database failure
* Redis failure
* Kafka failure
* Kubernetes cluster failure
* object storage issues
* credential compromise
* application-wide bad deployment

Classify workloads by recovery priority.

---

# RECOVERY PRIORITY

Critical systems include:

1. identity/authentication
2. active rides/trips
3. dispatch
4. payments
5. driver earnings/payouts
6. notifications
7. support
8. analytics
9. search

Recovery procedures must prioritize preserving authoritative business state.

---

# RPO AND RTO

Define realistic RPO/RTO targets for:

* PostgreSQL
* object storage
* Kafka
* Redis
* search
* application services

Targets must correspond to actual architecture and costs.

Do not claim zero RPO/RTO without infrastructure capable of providing it.

---

# MULTI-REGION READINESS

Design infrastructure modules so a second AWS region can be introduced.

Avoid region-specific assumptions in:

* naming
* state
* modules
* DNS
* certificates
* networking

Do not duplicate stateful systems into multiple active regions without a documented consistency strategy.

---

# REGIONAL TRAFFIC MANAGEMENT

Where multi-region is implemented or prepared, define:

* DNS routing
* health-based routing
* regional affinity
* failover
* TLS
* API endpoints
* WebSocket endpoints

Traffic routing must not split users arbitrarily when regional data locality matters.

---

# REGIONAL DATA OWNERSHIP

Identify which data is:

* global
* regional
* asynchronously replicated

Active trip and dispatch state should remain geographically coherent.

Do not design simultaneous unrestricted writes to the same trip from multiple regions.

---

# CROSS-REGION EVENTS

If Kafka/event replication is used:

* define replication scope
* avoid event loops
* preserve event IDs
* maintain traceability
* handle duplicate cross-region events

---

# MULTI-REGION FAILOVER

A regional failover must define:

* traffic redirection
* service availability
* state recovery
* event processing
* database accessibility
* cache rebuild
* WebSocket reconnection
* mobile endpoint behavior

Do not assume existing client connections survive a regional transition.

---

# SECURITY HARDENING

Perform infrastructure-wide security hardening.

Review:

* IAM
* Kubernetes RBAC
* service accounts
* network policies
* security groups
* WAF
* TLS
* secrets
* CI/CD
* images
* dependencies
* S3
* databases
* Redis
* Kafka
* administrative access

---

# KUBERNETES NETWORK POLICIES

Implement network policies restricting which namespaces/workloads can communicate.

At minimum distinguish:

* public ingress
* application
* worker
* observability
* system

Do not allow every pod to contact every other pod.

---

# POD SECURITY

Enforce secure pod defaults where compatible.

Use:

* non-root
* read-only filesystem where practical
* dropped Linux capabilities
* seccomp defaults
* restricted privilege escalation
* bounded resources

Do not require privileged containers unless a specific component genuinely needs them.

---

# RBAC

Create least-privilege Kubernetes RBAC.

Separate:

* deployment automation
* application workloads
* operations
* observability

Do not grant cluster-admin to application service accounts.

---

# SECRETS ACCESS AUDIT

Audit which workloads can access:

* database
* Redis
* Kafka
* payment
* map
* notification
* signing
* storage secrets

Remove unused access.

---

# IMAGE SECURITY

Require:

* vulnerability scanning
* trusted registries
* pinned base-image strategy
* image provenance where available
* non-root runtime

Block production deployment when critical image policy violations exceed defined thresholds.

Do not automatically block every low-severity dependency alert.

---

# SUPPLY-CHAIN SECURITY

Harden:

* GitHub Actions
* Terraform providers
* Helm dependencies
* npm dependencies
* Docker base images

Support:

* dependency scanning
* SBOM
* provenance/signing where practical
* secret scanning
* branch protection
* environment protection

---

# CI/CD SECURITY

Separate permissions for:

* pull request
* test
* staging deployment
* production deployment

Production deployment must require appropriate protected environment controls.

Use short-lived AWS authentication.

---

# DEPLOYMENT STRATEGIES

Support safe deployment strategies such as:

* rolling
* canary
* blue/green where justified

Choose based on workload.

Financial and trip-critical services need stronger deployment safeguards than stateless UI components.

---

# CANARY DEPLOYMENT

Where used:

* route a controlled percentage of traffic
* monitor error/SLO/burn-rate signals
* compare key business metrics
* abort on defined thresholds
* promote only after validation

Do not perform silent production experiments without observability and rollback.

---

# ROLLBACK

Every application deployment must have a defined rollback path.

Rollback must consider:

* container version
* database migrations
* event schemas
* queue schemas
* configuration versions
* mobile client compatibility

Do not blindly rollback an application after a destructive schema migration.

Use backward-compatible migration strategy.

---

# DATABASE MIGRATION SAFETY

Use:

* expand
* migrate
* contract

where required.

Production migrations must support rolling application versions.

Do not deploy schema changes that make currently-running application versions fail.

---

# CONFIGURATION ROLLBACK

Configuration changes must be independently reversible where practical.

A bad pricing/configuration rollout should not require rebuilding application binaries.

---

# INCIDENT-RESPONSE INFRASTRUCTURE

Provide infrastructure support for incident investigation.

Operators should be able to correlate:

* deployment
* pod
* service
* trace
* log
* metric
* event
* queue
* database state

through common timestamps and correlation metadata.

---

# INCIDENT TIMELINE

Ensure infrastructure logs enough metadata to reconstruct:

* when problem began
* which deployment occurred
* which region
* which service
* which dependency
* what traffic changed
* what mitigation occurred

Do not rely on manually assembled evidence.

---

# OPERATIONAL ACCESS

Production access must be controlled.

Use:

* SSO/federated identity where available
* MFA
* short-lived credentials
* role-based access
* audited administrative access

Do not share persistent administrator credentials.

---

# BREAK-GLASS ACCESS

Where supported, define emergency access that:

* is time-limited
* requires elevated authorization
* is audited
* is reviewed afterward

Do not create undocumented permanent backdoors.

---

# COST GOVERNANCE

Track infrastructure cost by:

* environment
* service
* region
* data platform
* major workload

Monitor for:

* unexpected EKS scaling
* Kafka growth
* Redis overprovisioning
* database overprovisioning
* excessive NAT usage
* CloudWatch/log ingestion spikes
* S3 growth
* CDN transfer spikes

Cost controls must not weaken critical reliability.

---

# CAPACITY PLANNING

Maintain capacity models for:

* requests per second
* WebSocket connections
* location updates per second
* dispatch operations
* Kafka events
* queue jobs
* database writes
* Redis commands
* object storage
* network bandwidth

For each identify:

* baseline
* peak
* scale trigger
* maximum safe capacity
* known bottleneck

---

# LOAD SHEDDING

Implement infrastructure-level protections for overload.

Potential controls:

* API rate limits
* WAF rate rules
* autoscaling
* connection limits
* queue backpressure
* priority classes
* bounded worker concurrency

Critical workloads must remain protected from low-priority workload storms.

---

# PRIORITY CLASSES

Where Kubernetes priority classes are appropriate, classify workloads such as:

* critical API
* WebSocket
* dispatch
* payment
* standard workers
* analytics
* cleanup

Do not allow low-priority workloads to evict critical services.

---

# RESILIENCE TESTING

Implement infrastructure tests or controlled exercises for:

* pod termination
* node failure
* API scaling
* Redis failover
* database failover
* Kafka consumer restart
* queue-worker crash
* WebSocket reconnect
* external provider outage
* certificate renewal
* deployment rollback

Tests must validate actual business invariants.

---

# CHAOS TESTING

Introduce controlled chaos testing where the repository/environment can safely support it.

Possible scenarios:

* random API pod termination
* worker interruption
* Redis failover
* network latency
* Kafka consumer delay
* database connection interruption

Never run destructive experiments directly in production without explicit controlled safeguards.

---

# BACKUP RESTORE TESTING

Regularly test:

* database restore
* object recovery
* configuration restoration
* infrastructure-state restoration

Record:

* recovery duration
* data validation
* discrepancies
* remediation

---

# DISASTER-RECOVERY EXERCISES

Conduct controlled DR exercises.

Validate:

* traffic failover
* service startup
* database recovery
* event recovery
* cache rebuilding
* mobile reconnection
* active-trip state recovery
* payment reconciliation

A DR process is incomplete until it has been exercised.

---

# OPERATIONAL RUNBOOKS

Create or update runbooks for:

* API outage
* WebSocket outage
* dispatch degradation
* location-ingestion overload
* payment provider outage
* payout outage
* Kafka lag
* queue backlog
* Redis failure
* PostgreSQL failover
* search outage
* S3 outage
* certificate issue
* bad deployment
* security incident
* regional outage

Each runbook must include:

* symptoms
* dashboards
* likely causes
* immediate actions
* safe mitigations
* rollback
* recovery verification
* escalation

---

# SECURITY INCIDENT RESPONSE

Provide infrastructure support for:

* credential compromise
* malicious deployment
* exposed secret
* suspicious IAM activity
* WAF attack
* container compromise
* database access anomaly

Support:

* credential rotation
* access revocation
* traffic blocking
* workload isolation
* forensic log retention
* incident audit

---

# COMPLIANCE SUPPORT

Where applicable, infrastructure must support compliance controls for:

* encryption
* access logging
* retention
* auditability
* least privilege
* secret management
* backup
* change history

Do not claim legal compliance merely because technical controls exist.

Document which controls are implemented and which require organizational/legal processes.

---

# CHANGE MANAGEMENT

Infrastructure changes must be traceable.

Require:

* pull request
* review
* automated validation
* plan output
* controlled approval
* deployment record

Emergency changes must still be auditable afterward.

---

# INFRASTRUCTURE DRIFT

Detect and manage drift between:

* Terraform
* AWS
* Kubernetes
* Helm

Do not permit manual production changes to become the permanent source of truth.

Where emergency changes occur, reconcile them into infrastructure code.

---

# TESTING REQUIREMENTS

Write or configure automated infrastructure tests for:

## TERRAFORM

* validation
* formatting
* plan
* policy checks
* module tests where available

## KUBERNETES

* manifest rendering
* schema validation
* security policy validation
* resource validation
* probe validation

## NETWORK

* connectivity
* restricted ingress
* restricted egress
* TLS

## IAM

* least privilege
* workload access
* secret access

## DATA

* PostgreSQL connectivity
* Redis connectivity
* Kafka connectivity
* S3 access

## CI/CD

* build
* image
* scan
* deployment
* rollback

---

# RESILIENCE TESTING

Verify that:

* API scales horizontally
* WebSockets reconnect
* workers terminate gracefully
* queues recover
* Kafka consumers recover
* Redis failover works
* PostgreSQL failover works
* search can be rebuilt
* object access remains secure
* backup restore succeeds

---

# PERFORMANCE TESTING

Measure:

* API scaling
* WebSocket connection capacity
* location ingestion capacity
* dispatch worker capacity
* queue throughput
* Kafka consumer throughput
* database throughput
* Redis throughput

Use representative production-like workloads.

---

# DOCUMENTATION

Update documentation for:

* observability
* dashboards
* alerts
* SLOs
* scaling
* database HA
* Redis HA
* Kafka resilience
* backup/restore
* disaster recovery
* multi-region
* security
* incident response
* runbooks
* capacity planning
* cost controls
* chaos testing
* deployment rollback

Documentation must describe actual infrastructure and actual tested behavior.

---

# IMPLEMENTATION DISCIPLINE

Before modifying files:

1. Inspect the repository infrastructure.
2. Identify existing observability.
3. Identify current scaling mechanisms.
4. Preserve compatible infrastructure.
5. Implement comprehensive telemetry.
6. Implement dashboards and alerts.
7. Implement workload-specific autoscaling.
8. Harden PostgreSQL.
9. Harden Redis.
10. Harden Kafka.
11. Harden search.
12. Implement backup and restore support.
13. Implement disaster-recovery architecture.
14. Prepare multi-region capabilities.
15. Harden Kubernetes security.
16. Harden CI/CD.
17. Implement capacity controls.
18. Implement resilience testing.
19. Implement operational runbooks.
20. Validate staging.
21. Validate production deployment safety.
22. Update documentation.
23. Produce the required completion report.

Do not rewrite unrelated infrastructure.

---

# PRODUCTION COMPLETENESS

Never leave:

* dashboards disconnected from real telemetry
* fake alerts
* nonfunctional SLO calculations
* untested backups
* undocumented failover
* missing restore procedures
* unrestricted production access
* broad IAM roles
* privileged containers without justification
* unbounded autoscaling
* uncontrolled costs
* incomplete rollback strategy
* unsafe database migrations
* TODO/FIXME infrastructure gaps
* pseudo-code

Infrastructure is complete only when operators can observe, scale, recover, secure, and validate the platform.

---

# PROHIBITED PRACTICES

Never:

* claim HA without testing failover
* claim DR without restore/failover exercises
* autoscale critical services from one weak signal
* expose database services publicly
* grant cluster-admin to workloads
* store secrets in Git
* ignore certificate expiry
* create alerts without operational meaning
* flood Prometheus with high-cardinality labels
* log sensitive payment/location content indiscriminately
* deploy destructive database migrations in rolling production
* use mutable image tags as the only release reference
* bypass infrastructure-as-code ownership
* make manual production changes permanent without reconciliation

---

# IMPLEMENTATION BOUNDARIES

This volume completes the production reliability, observability, security, scaling, and disaster-recovery infrastructure around the existing cloud foundation.

Do not create:

* a second AWS environment model
* a second Kubernetes cluster architecture without regional justification
* another CI/CD platform
* another observability stack
* duplicate database infrastructure

All subsequent infrastructure changes must extend the established platform.

---

# REQUIRED IMPLEMENTATION DELIVERABLES

Implement or update:

## OBSERVABILITY

* OpenTelemetry
* Prometheus
* Grafana
* Loki
* Tempo
* CloudWatch
* dashboards
* alerts
* SLO support

## SCALING

* HPA
* workload-specific scaling
* queue scaling
* Kafka consumer scaling
* WebSocket scaling
* node scaling

## DATA RESILIENCE

* PostgreSQL HA
* backups
* restore
* Redis HA
* Kafka resilience
* search resilience
* S3 resilience

## DISASTER RECOVERY

* RPO/RTO
* recovery architecture
* regional readiness
* failover
* restore
* replay

## SECURITY

* Kubernetes RBAC
* network policies
* pod security
* image security
* secret-access review
* CI/CD hardening
* operational access

## OPERATIONS

* runbooks
* incident support
* capacity planning
* cost governance
* drift management
* change management

## RESILIENCE

* chaos testing
* failover testing
* restore testing
* deployment rollback testing

---

# REQUIRED OBSERVABILITY CONTRACTS

Every production workload must expose or integrate with:

* health
* readiness
* metrics
* logs
* traces

Critical workflows must be traceable across:

* API
* database
* Redis
* queues
* Kafka
* external providers

---

# REQUIRED SCALING CONTRACTS

For each workload document:

* baseline replicas
* minimum replicas
* maximum replicas
* scaling metric
* scale-up threshold
* scale-down threshold
* cooldown
* resource request
* resource limit

Do not use the same values blindly for every workload.

---

# REQUIRED RECOVERY CONTRACTS

For every critical service define:

* failure mode
* detection
* automatic recovery
* manual recovery
* data authority
* RPO
* RTO
* validation after recovery

---

# REQUIRED RUNTIME VALIDATION

Verify:

* dashboards
* alerts
* SLOs
* autoscaling
* database failover
* Redis failover
* Kafka recovery
* queue recovery
* WebSocket scaling
* backup restore
* search rebuild
* S3 access
* deployment rollback
* security controls
* operational access
* regional readiness where implemented

Do not report success for mechanisms that were only configured but never validated.

---

# COMPLETION REPORT REQUIREMENTS

When implementation is complete, report:

## FILES CREATED

List every new infrastructure file.

## FILES MODIFIED

List every modified infrastructure/application deployment file.

## OBSERVABILITY

Report:

* OpenTelemetry
* Prometheus
* Grafana
* Loki
* Tempo
* CloudWatch
* dashboards
* alerts
* SLOs

## SCALING

Report:

* API
* WebSocket
* location
* dispatch
* BullMQ
* Kafka
* database
* node scaling

## DATA RESILIENCE

Report:

* PostgreSQL HA
* Redis HA
* Kafka resilience
* search resilience
* S3 resilience
* backups
* restore

## DISASTER RECOVERY

Report:

* RPO
* RTO
* regional architecture
* failover
* recovery testing
* replay

## SECURITY

Report:

* RBAC
* network policies
* pod security
* IAM
* secret access
* image security
* CI/CD security
* operational access

## RESILIENCE TESTING

Report:

* chaos tests
* failover tests
* restore tests
* deployment rollback tests

## OPERATIONS

Report:

* runbooks
* incident response
* capacity planning
* cost controls
* drift detection
* change management

## VALIDATION

Report:

* Terraform
* Helm
* Kubernetes
* security
* performance
* scaling
* backup/restore
* resilience
* staging deployment
* production deployment readiness

## COMPATIBILITY

Identify:

* application deployment implications
* database implications
* event implications
* regional implications
* mobile release implications

## UNRESOLVED ISSUES

List only genuine remaining infrastructure issues.

Do not claim infrastructure completion if critical observability, scaling, recovery, security, or deployment-safety capabilities remain incomplete or unverified.

---

# FINAL ENGINEERING PRINCIPLE

The production platform must remain observable, scalable, secure, and recoverable when individual components fail, workloads spike, deployments go wrong, or an entire availability region becomes impaired.

The infrastructure must provide:

* measurable reliability
* workload-specific autoscaling
* strong database durability
* recoverable asynchronous processing
* resilient realtime infrastructure
* controlled multi-region growth
* secure operations
* verified backup/restore
* tested failover
* actionable observability
* disciplined deployment
* controlled costs
* auditable infrastructure changes

Authoritative transactional state remains in the appropriate durable systems.

Caches remain rebuildable.

Search remains reconstructible.

Queues remain recoverable.

Events remain replayable under controlled safeguards.

Infrastructure remains defined as code.

Production access remains least-privilege and audited.

Disaster recovery remains a tested capability rather than a theoretical document.

The repository remains the implementation source of truth.

The Uber-style ride-hailing platform infrastructure is complete only when the deployed system can be observed, scaled, secured, operated, and recovered using reproducible engineering processes.
