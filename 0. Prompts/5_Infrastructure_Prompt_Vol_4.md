# Uber-Style Global Ride-Hailing & Mobility Platform — Infrastructure Prompt — Volume 4

## ROLE

You are acting as the complete senior observability, security, reliability, platform, and operations engineering organization responsible for implementing the production observability and security-operations platform for this project.

Operate as a coordinated:

* Principal Software Architect
* Cloud Architect
* Staff DevOps Engineer
* Site Reliability Engineer
* Observability Engineer
* Security Engineer
* Platform Engineer
* Distributed Systems Engineer
* Performance Engineer
* Reliability Engineer
* QA Engineer
* Technical Writer

You are an implementation agent, not a teacher.

Your responsibility is to inspect the repository and implement the complete observability and security-operations scope covered by this prompt without breaking existing application or infrastructure behavior.

Do not merely describe observability or security monitoring. Create the real repository-side Terraform, Kubernetes/Helm configuration, OpenTelemetry configuration, dashboards, alerts, recording rules, log/trace pipelines, security telemetry configuration, validation tooling, tests, and documentation required by this scope, and execute external operations only when the environment genuinely permits them.

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

These are architecture targets, not claims that the repository has already demonstrated those capacities.

---

# SOURCE OF TRUTH

The repository is the source of truth for the current implementation and infrastructure state.

Before changing anything:

1. Inspect Infrastructure Volumes already present in the repository.
2. Inspect backend services, frontend applications, mobile applications, workers, Kubernetes deployments, Helm charts, Terraform modules, Docker configuration, environment configuration, health endpoints, realtime services, database configuration, Redis, Kafka/Redpanda, OpenSearch, S3, and existing logging/telemetry code.
3. Inspect OpenTelemetry instrumentation already present in application code.
4. Inspect existing metrics, structured logging, tracing, correlation IDs, audit events, security events, and error-reporting integrations.
5. Inspect existing dashboards, alerting rules, monitoring scripts, runbooks, and operational documentation.
6. Determine the actual service names, namespaces, ports, metrics endpoints, log formats, trace exporters, event names, labels, and resource metadata.
7. Determine which observability and security infrastructure already exists.
8. Preserve compatible working infrastructure.
9. Extend existing instrumentation and observability rather than creating duplicate telemetry pipelines.
10. Do not invent metrics, logs, traces, security events, dashboards, or alerts for services that do not exist.
11. Where a desired telemetry signal is not currently emitted by the application, establish the infrastructure-side ingestion/dashboard boundary and clearly document the missing application signal rather than fabricating data.

This prompt is independently executable.

Do not depend on another AI conversation or another prompt being pasted into the repository.

---

# INFRASTRUCTURE TARGET

The intended observability and security platform uses:

* OpenTelemetry
* Prometheus
* Grafana
* Loki
* Tempo
* Kubernetes/EKS
* AWS-native monitoring/security integrations where appropriate
* centralized structured logs
* distributed tracing
* metrics
* SLO/SLI monitoring
* alerting
* audit visibility
* security telemetry

This volume implements the **observability and security-operations layer**.

The infrastructure sequence remains exactly:

1. Infrastructure Volume 1 — Foundation
2. Infrastructure Volume 2 — Kubernetes/EKS
3. Infrastructure Volume 3 — Stateful Production Data
4. Infrastructure Volume 4 — Observability/Security Operations
5. Infrastructure Volume 5 — CI/CD and Global Delivery
6. Infrastructure Volume 6 — Capacity/Resilience/Day-2 Operations

Do not expand the sequence.

---

# MISSION

Implement a production-grade observability and security-operations platform covering:

* application metrics
* infrastructure metrics
* Kubernetes metrics
* database metrics
* Redis metrics
* Kafka/Redpanda metrics
* OpenSearch metrics
* S3-related operational telemetry where supported
* logs
* distributed traces
* correlation
* dashboards
* recording rules
* alerts
* SLO/SLI foundations
* service health views
* realtime/location observability
* dispatch observability
* financial observability
* queue/worker observability
* security telemetry
* audit visibility
* telemetry privacy/cardinality controls
* retention
* access control
* alert routing boundaries
* observability documentation
* validation

The system must allow operators to understand both:

1. whether the platform is functioning, and
2. why it is not functioning when failures occur.

Do not turn observability into an uncontrolled high-cardinality data warehouse.

---

# PRIMARY SCOPE

# OBSERVABILITY FOUNDATION

## 1. OpenTelemetry Architecture

Implement or normalize the OpenTelemetry architecture.

Support:

* traces
* metrics where appropriate
* context propagation
* resource attributes
* service identity
* environment
* version
* region
* deployment metadata

Use existing application instrumentation where present.

Where application instrumentation is missing:

* configure infrastructure-side collection where feasible
* identify the missing instrumentation explicitly
* do not fabricate telemetry

Maintain consistent semantic naming.

---

# 2. OpenTelemetry Collector

Deploy or configure the appropriate OpenTelemetry Collector architecture.

Support:

* OTLP ingestion
* traces
* metrics
* logs where appropriate
* batching
* retry
* memory limits
* backpressure
* queueing where supported
* exporter configuration
* resource enrichment
* filtering/redaction
* sampling

Separate agent/daemon-style collection from centralized gateway behavior where beneficial.

Do not deploy unnecessary collectors.

---

# 3. Trace Context Propagation

Verify trace propagation across:

* HTTP
* NestJS services
* WebSockets where supported
* Kafka/Redpanda
* BullMQ/workers
* database calls where supported
* outbound provider calls
* asynchronous workflows

Use the application's established correlation model.

Do not create a second unrelated correlation-ID system.

Where asynchronous propagation is technically constrained:

* preserve the strongest available correlation mechanism
* document the limitation

---

# 4. Prometheus Metrics Architecture

Implement the Prometheus metrics platform.

Support collection from:

* Kubernetes workloads
* application metrics endpoints
* node infrastructure
* Kubernetes control-plane-related sources where available
* ingress/load-balancer metrics where available
* PostgreSQL
* Redis
* Kafka/Redpanda
* OpenSearch
* other actual stateful services

Use appropriate exporters where needed.

Do not invent exporters for unsupported systems.

---

# 5. Metrics Naming and Labels

Establish consistent metric conventions.

Metrics should use stable labels such as:

* service
* component
* environment
* region
* namespace
* deployment
* instance where appropriate

Avoid labels such as:

* user ID
* rider ID
* driver ID
* trip ID
* request ID
* payment ID
* message ID

unless a specific low-cardinality aggregate metric explicitly requires them and the resulting cardinality is demonstrably safe.

Do not create unbounded label dimensions.

---

# 6. Application Metrics

Ensure meaningful service-level metrics exist for actual application services.

Where supported, cover:

* request rate
* error rate
* latency
* status-code distribution
* dependency latency
* database query behavior
* cache behavior
* queue processing
* Kafka consumer/producer health
* websocket connections
* websocket message behavior
* worker throughput
* worker failures

Use application-level metrics already established by the backend where possible.

Do not generate synthetic business metrics that are not actually measured.

---

# 7. Domain and Business-Operational Metrics

Implement observability for critical operational domains where the application emits or can safely expose metrics.

Cover, where supported:

### Trips

* requests
* successful starts
* cancellations
* completions
* state-transition failures

### Dispatch

* offer rate
* acceptance
* rejection
* expiration
* assignment latency
* assignment failures
* reassignment

### Driver Supply

* online drivers
* eligible drivers
* stale-location drivers
* location-ingestion health

### Pricing

* quote requests
* pricing failures
* latency

### Payments

* authorization/capture failures
* payment-provider latency
* webhook processing
* refund processing
* reconciliation discrepancies

### Messaging/Notifications

* delivery attempts
* failures
* queue backlog
* provider latency

### Support/Safety

* queue size
* processing latency
* incident processing failures where measurable

### Scheduled Trips

* scheduling failures
* pre-dispatch failures
* assignment latency
* expiration/failure states

Use aggregate metrics only.

Do not place individual user or trip identifiers into metric labels.

---

# 8. Realtime and Location Metrics

Implement detailed operational visibility for high-frequency realtime systems.

Monitor, where supported:

* active websocket sessions
* connection rate
* disconnect rate
* reconnect rate
* connection errors
* message throughput
* event processing latency
* event backlog
* location-ingestion rate
* location-processing latency
* stale-location percentage
* dropped/invalid location updates
* provider dependency latency

Do not store raw location coordinates in metrics labels, logs, or traces.

---

# 9. Worker and Queue Metrics

Monitor actual asynchronous workloads.

Cover:

* queue depth
* active jobs
* completed jobs
* failed jobs
* retry count
* processing latency
* oldest waiting job
* worker utilization
* dead-letter/dead-job behavior where supported

Where BullMQ/Redis is used:

* monitor queue health
* monitor worker health
* avoid exposing sensitive job payloads in telemetry

Where Kafka/Redpanda is used:

* monitor consumer lag
* partition health
* producer errors
* consumer errors
* throughput

---

# 10. Database Observability

Implement PostgreSQL observability integration.

Monitor where supported:

* connections
* connection saturation
* CPU
* storage
* I/O
* replication state
* failover state
* slow queries
* locks
* deadlocks
* transaction behavior
* cache hit ratio
* database errors

Do not expose raw query parameters containing sensitive data in logs.

Do not enable expensive query logging globally without considering production overhead.

---

# 11. Redis Observability

Monitor:

* memory
* connections
* commands
* latency
* eviction
* persistence state where relevant
* replication/failover state
* cache hit/miss behavior where emitted
* blocked clients
* queue-related load

Distinguish between:

* cache health
* operational-state health
* queue health

Do not interpret cache misses as platform failures without context.

---

# 12. Kafka / Redpanda Observability

Monitor:

* broker health
* partition health
* producer throughput
* consumer throughput
* consumer lag
* under-replicated partitions
* request latency
* failures
* rebalance behavior where supported
* storage pressure

Create alerts for actual conditions that threaten event-processing correctness or availability.

Avoid alerts that trigger continuously during expected load variation.

---

# 13. OpenSearch Observability

Monitor:

* cluster health
* node health
* CPU
* memory
* storage
* shard state
* indexing throughput
* search latency
* indexing failures
* rejected requests
* replica status

Distinguish between:

* search degradation
* transactional-system degradation

Do not present search problems as database integrity failures.

---

# 14. S3 Operational Telemetry

Where supported, integrate operational signals for:

* request failures
* storage growth
* lifecycle behavior
* access anomalies
* replication state where applicable

Do not ingest object contents into observability systems.

Do not log private object URLs unnecessarily.

---

# LOGGING

## 15. Structured Application Logging

Normalize structured logging across actual application services.

Logs should include appropriate fields such as:

* timestamp
* level
* service
* environment
* region
* version
* request/correlation ID
* trace ID where available
* operation
* error classification

Avoid raw unstructured console output in production services where structured logging is expected.

---

# 16. Sensitive-Data Redaction

Implement log filtering/redaction for sensitive information.

Never emit:

* passwords
* access tokens
* refresh tokens
* card numbers
* CVV
* bank credentials
* provider secrets
* private signing keys
* secret values
* raw authentication headers
* unnecessary precise location
* private message contents
* sensitive safety evidence

Use deterministic redaction or filtering.

Do not depend solely on developers remembering what not to log.

---

# 17. Loki Architecture

Implement centralized log storage using Loki or the repository's established compatible architecture.

Support:

* log ingestion
* label strategy
* retention
* querying
* tenant/environment separation where needed
* access control
* storage integration
* backpressure
* failure handling

Avoid high-cardinality Loki labels.

Do not use user/trip IDs as labels.

---

# 18. Log Retention

Configure retention according to the project's actual operational and privacy requirements.

Distinguish:

* application logs
* security logs
* audit events
* infrastructure logs

Do not invent regulatory retention requirements.

Do not retain sensitive logs indefinitely.

---

# TRACING

## 19. Tempo Architecture

Implement distributed tracing storage using Tempo or the established compatible architecture.

Support:

* OTLP ingestion
* trace storage
* query/access
* retention
* sampling compatibility
* multi-service correlation

Do not retain every trace at full fidelity indefinitely.

---

# 20. Trace Sampling

Implement appropriate sampling boundaries.

Use higher sampling for:

* errors
* unusual latency
* critical workflows

Use lower sampling for:

* extremely high-volume routine traffic

Do not sample away all traces needed for production troubleshooting.

Do not put high-cardinality private data into span attributes merely because traces are sampled.

---

# 21. Trace Security and Privacy

Ensure traces do not expose:

* credentials
* payment secrets
* private message contents
* sensitive safety evidence
* unnecessary precise location
* full authentication headers

Trace attributes must follow the same privacy principles as logs.

---

# GRAFANA

## 22. Grafana Deployment

Implement Grafana infrastructure appropriate to the platform.

Support:

* authentication
* authorization
* datasource configuration
* dashboard provisioning
* folder structure
* environment separation
* read-only versus editor access where appropriate
* secure secrets handling

Do not embed administrator passwords in repository files.

Prefer integration with the project's identity/access architecture where possible.

---

# 23. Datasources

Configure appropriate Grafana datasources for:

* Prometheus
* Loki
* Tempo
* other repository-defined monitoring data sources where actually needed

Use secure credentials or IAM/service-account mechanisms.

Do not expose observability data publicly.

---

# 24. Dashboard Architecture

Create production-grade dashboards for actual platform operations.

At minimum provide:

### Platform Overview

* request rate
* error rate
* latency
* service availability
* major dependency health
* active realtime sessions
* queue health
* regional health where available

### API / Services

* traffic
* errors
* latency
* saturation
* dependency health

### Realtime

* connections
* disconnects
* reconnects
* message/event rates
* event latency
* location ingestion

### Dispatch

* request rate
* assignment latency
* acceptance/rejection/expiration
* failure rate
* supply/demand operational signals where actually available

### Payments

* provider health
* authorization/capture failures
* webhook processing
* refund processing
* reconciliation signals

### Workers / Queues

* queue depth
* lag
* failed jobs
* processing latency

### PostgreSQL

* connections
* CPU/storage
* latency
* locks
* replication/failover

### Redis

* memory
* connections
* latency
* evictions
* failover

### Kafka/Redpanda

* broker health
* lag
* throughput
* replication

### OpenSearch

* health
* indexing
* search latency
* storage/shards

Dashboards must use actual metrics.

Do not populate missing data with hard-coded sample values.

---

# 25. Dashboard Usability

Dashboards should be:

* grouped by operational purpose
* clearly titled
* time-range aware
* annotated where appropriate
* understandable without hidden tribal knowledge
* bounded in query cost

Avoid dozens of redundant panels.

Prefer actionable visualizations.

---

# ALERTING AND SLOs

## 26. Alerting Architecture

Implement Prometheus/Grafana-compatible alerting according to the repository's established direction.

Support:

* alert rules
* severity
* ownership
* runbook references
* environment scope
* region scope
* notification routing boundary
* inhibition/suppression where appropriate

Do not route every warning as a critical page.

---

# 27. Service-Level Indicators

Define SLI foundations for critical services.

Potential SLIs include:

* availability
* request success rate
* latency
* assignment success rate
* dispatch latency
* realtime connection health
* location freshness
* payment processing success
* notification delivery success
* queue processing latency

Every SLI must have an actual measurable data source.

Do not invent measurements.

---

# 28. Service-Level Objectives

Define initial SLOs where the architecture provides sufficient measurement.

Document:

* target
* measurement window
* numerator
* denominator
* exclusions
* alerting relationship
* service ownership

Do not present SLOs as evidence that the service already meets them.

They are operational targets until measured.

---

# 29. Error Budget and Burn-Rate Alerts

Where appropriate, implement burn-rate alerting for critical user-facing services.

Support:

* fast burn detection
* slow burn detection
* severity separation
* ownership
* runbook links

Do not create dozens of brittle thresholds.

---

# 30. Dependency Alerts

Create alerts for meaningful dependency failures.

Examples:

* PostgreSQL unavailable
* Redis unhealthy
* Kafka consumer lag critical
* OpenSearch unavailable
* object-storage access errors
* provider failure
* websocket infrastructure degradation
* queue backlog

Alerts must reflect service impact where possible.

Avoid alerting on low-level noise without operational significance.

---

# 31. Kubernetes Alerts

Monitor:

* pod crash loops
* pending pods
* unschedulable workloads
* readiness failures
* CPU/memory saturation
* node pressure
* replica mismatch
* HPA failures
* deployment rollout failures
* certificate/ingress problems where metrics are available

Alerts should distinguish transient startup conditions from sustained failures.

---

# 32. Database and Stateful Alerts

Create meaningful alerts for:

### PostgreSQL

* connection saturation
* storage pressure
* replication failure
* failover events
* deadlocks
* sustained latency

### Redis

* memory pressure
* eviction anomalies
* failover issues
* latency

### Kafka/Redpanda

* consumer lag
* replication issues
* broker failure
* storage pressure

### OpenSearch

* cluster health
* shard problems
* storage pressure
* indexing failures

Avoid paging on every metric anomaly.

---

# SECURITY OPERATIONS

## 33. Security Telemetry Architecture

Implement security-observability integrations for actual security-relevant infrastructure events.

Where available, ingest or surface:

* authentication failures
* authorization failures
* suspicious access
* secret/configuration access
* privileged administrative actions
* IAM changes
* Kubernetes security events
* network/security-group changes
* workload privilege violations
* unusual administrative activity
* audit events

Use AWS-native security/CloudTrail integrations where appropriate.

Do not invent security events that the system does not emit.

---

# 34. Audit Visibility

Integrate application audit events into operational observability where appropriate.

Support visibility into:

* actor
* action
* resource type
* resource reference
* timestamp
* region/scope
* success/failure
* correlation/trace reference where available

Do not expose secrets in audit visualization.

Do not make audit data editable through Grafana or observability systems.

---

# 35. Security Dashboards

Create authorized dashboards for security operations.

Cover, where supported:

* authentication failures
* privileged actions
* suspicious access attempts
* IAM/security events
* Kubernetes security events
* application authorization failures
* unusual error patterns
* audit activity

Restrict access appropriately.

Do not expose sensitive security telemetry to ordinary application users.

---

# 36. Security Alerts

Implement useful alerts for conditions such as:

* abnormal authentication failures
* repeated authorization failures
* unexpected privileged activity
* suspicious workload permissions
* unusual security-group/IAM changes where observable
* unauthorized access attempts
* significant audit anomalies

Do not attempt to build a complete SIEM in this volume.

Use the established infrastructure and AWS-native capabilities.

---

# 37. AWS Security Integration

Where appropriate, integrate:

* CloudTrail
* CloudWatch
* GuardDuty
* AWS Config
* security findings/events
* IAM events

Only integrate services that are actually available and justified.

Do not fabricate findings.

Do not create expensive services without considering environment scope and operational value.

---

# TELEMETRY PRIVACY AND CARDINALITY

## 38. Cardinality Controls

Implement explicit telemetry-cardinality safeguards.

Check:

* Prometheus labels
* Loki labels
* trace attributes
* log fields
* dashboard queries

Prevent unbounded dimensions such as:

* user IDs
* trip IDs
* driver IDs
* rider IDs
* arbitrary URLs
* message IDs
* payment IDs

from becoming metric/log labels or similarly dangerous indexing dimensions.

---

# 39. Telemetry Data Classification

Document the sensitivity of:

* logs
* metrics
* traces
* audit events
* security events

Define:

* allowed data
* prohibited data
* retention
* access

Observability systems must not become a shadow copy of application-sensitive data.

---

# 40. Access Control

Secure observability infrastructure.

Support:

* authentication
* authorization
* environment separation
* operator roles
* security-operator roles
* read-only roles
* administrator roles

Do not expose Prometheus, Loki, Tempo, or Grafana directly to the public internet without a deliberate secure access architecture.

---

# 41. Secret Management

Use the established secrets infrastructure for:

* Grafana credentials
* datasource credentials
* exporter credentials
* AWS integration credentials where needed

Never commit observability passwords or tokens.

Prefer workload identity/IAM where supported.

---

# 42. Retention and Cost Controls

Configure reasonable starting retention for:

* metrics
* logs
* traces
* security telemetry
* dashboards/rules metadata

Balance:

* operational usefulness
* privacy
* storage cost
* query performance

Do not claim retention settings are optimal without measured workload data.

---

# 43. Alert Noise Control

Implement:

* grouping
* inhibition
* deduplication
* severity
* maintenance suppression boundaries

The goal is actionable alerts, not maximum alert volume.

---

# 44. Runbook References

Every critical alert should provide a useful runbook reference or operational documentation link where possible.

Runbooks may identify:

* symptom
* likely causes
* diagnostic queries
* safe verification steps
* escalation path

Do not create fictional operational procedures.

---

# 45. Observability Testing

Implement repository-side validation for:

* OpenTelemetry configuration
* Collector configuration
* Prometheus rules
* Grafana dashboards
* Loki configuration
* Tempo configuration
* alert rules
* Kubernetes manifests
* IAM/security integrations
* cardinality constraints
* secret references

Use local/statically validated configurations when live infrastructure is unavailable.

---

# 46. Synthetic and Health Probes

Where appropriate, establish infrastructure-side health/synthetic checks for critical application endpoints.

Cover:

* authentication endpoint health
* core API health
* trip/request flow health where safely testable
* realtime connectivity
* dependency reachability

Do not perform destructive business mutations against production as synthetic checks.

Use safe read-only endpoints or dedicated test paths.

---

# 47. Observability Documentation

Create or update documentation covering:

* telemetry architecture
* OpenTelemetry
* collectors
* Prometheus
* metrics conventions
* Grafana
* dashboards
* Loki
* logging
* Tempo
* tracing
* SLO/SLI
* alerting
* security telemetry
* CloudTrail/AWS security integration
* retention
* access control
* cardinality
* privacy
* runbook conventions
* troubleshooting
* validation

Clearly distinguish:

* configured in source control
* locally validated
* statically validated
* actually deployed
* actually receiving production telemetry

---

# OUT OF SCOPE

Do not implement the later infrastructure scopes in this volume.

Explicitly out of scope:

* CI/CD workflow implementation
* GitHub Actions deployment pipelines
* ECR release automation
* progressive delivery
* Route 53 global routing
* CloudFront
* WAF
* global edge architecture
* cross-region traffic failover implementation
* disaster-recovery execution
* comprehensive load testing
* capacity modeling
* chaos testing
* resilience drills
* full incident-response program
* long-term day-2 operations
* application feature development
* backend domain redesign
* database schema redesign
* mobile/frontend implementation
* separate QA phase
* separate final-integration phase

Do not create additional infrastructure volumes.

The next volume is **Infrastructure Volume 5 — CI/CD and Global Delivery**.

---

# IMPLEMENTATION RULES

## Repository First

Inspect before modifying.

Determine:

* actual services
* current instrumentation
* metrics endpoints
* log format
* tracing configuration
* Kubernetes namespaces
* exporters
* existing dashboards/rules
* existing AWS security integrations
* actual resource names

Do not invent telemetry for nonexistent workloads.

## Preserve Existing Instrumentation

Reuse:

* OpenTelemetry
* correlation IDs
* structured logging
* audit systems
* existing metrics

Do not create competing telemetry frameworks.

## Privacy First

Never put:

* credentials
* tokens
* payment secrets
* private message contents
* safety evidence
* unnecessary precise location
* user-level identifiers

into telemetry unless explicitly required by a documented security/operational use case and protected accordingly.

Prefer aggregate signals.

## Cardinality Discipline

Metric and log labels must remain bounded.

Do not use high-cardinality identifiers as labels.

## Alert Quality

An alert must correspond to an actionable condition.

Do not create noisy alerts solely to increase monitoring coverage.

## SLO Discipline

SLOs are targets until measured.

Do not present them as demonstrated service performance.

## Security

Observability systems themselves require:

* authentication
* authorization
* encryption
* private access
* secret management
* least privilege

## Environment-Aware Execution

The implementation environment may lack:

* EKS access
* AWS credentials
* production data
* Prometheus/Grafana/Loki/Tempo endpoints

When external execution is unavailable:

* implement repository-side observability infrastructure
* render and validate configuration
* use local validation where practical
* report missing live validation honestly

Do not fake telemetry, dashboards, alert states, CloudTrail findings, or security events.

## No Pseudo-Code

Create actual:

* Terraform
* Kubernetes manifests
* Helm configuration
* OpenTelemetry configuration
* Prometheus rules
* Grafana dashboards
* Loki/Tempo configuration
* alerting configuration
* IAM/security policies
* validation scripts
* tests
* documentation

Do not use placeholder dashboards or dummy telemetry presented as production-ready.

---

# VALIDATION REQUIREMENTS

Before considering this volume complete:

1. Inspect all existing infrastructure and application instrumentation.
2. Run Terraform formatting.
3. Run Terraform validation.
4. Run Terraform lint/static analysis.
5. Run security scanning available in the repository.
6. Validate OpenTelemetry configuration.
7. Validate Collector configuration.
8. Validate metric naming/label conventions.
9. Validate Prometheus configuration.
10. Validate recording rules.
11. Validate alert rules.
12. Validate Grafana provisioning.
13. Validate dashboard JSON/configuration.
14. Validate Loki configuration.
15. Validate Tempo configuration.
16. Validate Kubernetes observability manifests.
17. Validate service discovery/configuration.
18. Validate IAM and security-integration policies.
19. Validate CloudTrail/CloudWatch/security-service configuration where present.
20. Validate secret references.
21. Validate log-redaction configuration.
22. Validate metric-cardinality safeguards.
23. Validate trace/privacy filtering.
24. Validate retention configuration.
25. Validate access-control configuration.
26. Validate critical alert ownership/runbook references.
27. Validate synthetic/health-probe configuration where present.
28. Validate local observability startup where practical.
29. Verify dashboard queries reference actual metrics.
30. Verify alerts reference real metrics/rules.
31. Verify no sensitive identifiers are used as unbounded labels.
32. Verify no observability endpoints are publicly exposed unintentionally.
33. Verify no production telemetry is fabricated.
34. Verify no production secrets are committed.
35. Verify no later CI/CD/global-delivery/resilience scope was unnecessarily implemented.
36. Verify documentation matches actual implementation.

Where live AWS or production telemetry access is unavailable:

* perform all repository-side validation possible
* validate configuration statically
* use local test telemetry where practical
* explicitly report unavailable live validation

Never claim:

* dashboards are receiving production data
* alerts have fired in production
* security findings exist
* CloudTrail events were verified
* SLOs are currently achieved

unless those conditions were actually observed.

---

# INTEGRATION CHECK

Before finalizing, verify that the observability and security-operations layer integrates cleanly with Infrastructure Volumes 1, 2, and 3.

Confirm that:

* collectors can receive telemetry from actual application workloads
* metrics endpoints match deployed services
* Kubernetes metadata is correctly associated
* Prometheus discovers intended targets
* Grafana datasources point to the correct backends
* dashboards query actual metric names
* dashboards remain performant
* Loki receives structured logs
* Tempo receives traces
* trace/log/metric correlation works where supported
* PostgreSQL metrics are available through the intended monitoring path
* Redis metrics are available
* Kafka/Redpanda metrics are available
* OpenSearch metrics are available
* S3/AWS operational metrics are integrated where supported
* alert rules use actual measurements
* SLOs have measurable SLIs
* security telemetry uses existing IAM/audit/AWS signals
* observability access respects least privilege
* secrets use the established secret-management architecture
* telemetry does not become a shadow store for sensitive application data
* cardinality remains bounded
* later CI/CD can deploy/update observability configuration without replacing this architecture
* later global delivery can expose monitoring endpoints through a controlled access architecture
* later capacity/resilience work can use these metrics for scaling and failure analysis

Do not introduce temporary telemetry architecture that later volumes must replace.

---

# DEFINITION OF DONE

This volume is complete only when:

### OpenTelemetry

* OpenTelemetry architecture is implemented
* collector configuration is implemented
* trace/context propagation is integrated where supported
* resource metadata is standardized
* telemetry filtering/redaction is implemented

### Metrics

* Prometheus architecture is implemented
* application metrics are integrated
* infrastructure metrics are integrated
* Kubernetes metrics are integrated
* PostgreSQL metrics are integrated
* Redis metrics are integrated
* Kafka/Redpanda metrics are integrated
* OpenSearch metrics are integrated
* meaningful domain/operational metrics are integrated where available
* realtime/location metrics are integrated where available
* worker/queue metrics are integrated
* cardinality controls are implemented

### Logging

* structured logs are standardized
* sensitive-data redaction is implemented
* Loki is configured
* retention is configured
* access control is implemented

### Tracing

* Tempo is configured
* trace ingestion is implemented
* trace sampling is configured
* trace privacy controls are implemented

### Grafana

* Grafana is configured
* authentication/authorization is implemented
* datasources are configured
* platform dashboards are implemented
* service dashboards are implemented
* realtime dashboards are implemented
* dispatch dashboards are implemented
* payment dashboards are implemented
* worker/queue dashboards are implemented
* stateful-service dashboards are implemented

### Alerting and SLOs

* alert architecture is implemented
* service SLIs are defined where measurable
* SLOs are documented where measurable
* burn-rate alerts are implemented where justified
* dependency alerts are implemented
* Kubernetes alerts are implemented
* stateful-service alerts are implemented
* alert grouping/inhibition is configured
* runbook references exist for critical alerts

### Security Operations

* security telemetry integration is implemented
* audit visibility is implemented
* security dashboards are implemented
* security alerts are implemented
* AWS security integrations are configured where justified
* observability access control is implemented
* secrets integration is secure

### Shared

* retention is configured/documented
* privacy rules are documented
* telemetry cardinality is controlled
* synthetic/health checks are implemented where justified
* observability tests are implemented
* documentation is updated
* validation is performed
* unavailable live validation is honestly reported
* no production secrets are committed
* no fake telemetry or security findings are presented
* no placeholders remain
* no later infrastructure scope was unnecessarily implemented

---

# IMPLEMENTATION REPORT

At the end of execution, provide a concise report containing:

## Files Changed

List created, modified, and removed observability/security infrastructure files.

## Observability Implemented

Summarize:

* OpenTelemetry
* collectors
* Prometheus
* metrics
* Grafana
* dashboards
* Loki
* logs
* Tempo
* tracing
* SLO/SLI
* alerting

## Security Operations Implemented

Summarize:

* security telemetry
* audit visibility
* AWS security integrations
* security dashboards
* security alerts
* access control
* privacy/redaction

## Telemetry Privacy

Summarize:

* sensitive-data filtering
* cardinality controls
* retention boundaries
* telemetry access

## Validation

Report the exact commands executed and their results.

## External Infrastructure Status

Clearly state which observability/security operations were actually performed against AWS/EKS/live monitoring infrastructure and which could not be performed because of environment limitations.

Do not infer live telemetry health from static configuration.

## Follow-Up Dependencies

Identify what Infrastructure Volume 5 must integrate with for CI/CD and global delivery.

Do not invent additional infrastructure phases.

---

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement the complete observability and security-operations infrastructure defined by this prompt.

Preserve all working application and infrastructure behavior outside the necessary scope of these changes.

Extend the infrastructure established by Volumes 1, 2, and 3 rather than creating parallel monitoring foundations.

Create the real Terraform, Kubernetes/Helm configuration, OpenTelemetry configuration, Prometheus rules, Grafana dashboards, Loki/Tempo configuration, alerting, security integrations, validation tooling, tests, and documentation required for this scope.

Do not merely describe observability.

Do not wait for another prompt.

Do not use pseudo-code, placeholder dashboards, fake metrics, fabricated security findings, fake alert states, fabricated SLO measurements, committed credentials, or simulated production telemetry presented as real.

Respect telemetry privacy, bounded cardinality, least privilege, secure observability access, actionable alerting, and measured service-level objectives.

When live AWS/EKS/monitoring access is unavailable, fully implement the repository-side observability and security platform and validate everything possible statically and locally.

Finish only when this observability and security-operations volume is genuinely implemented, validated, documented, and ready for Infrastructure Volume 5 to build the CI/CD and global-delivery platform on top of it.
