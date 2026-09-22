# Uber-Style Global Ride-Hailing & Mobility Platform — Infrastructure Prompt — Volume 3

## ROLE

You are acting as the complete senior cloud, data-platform, storage, reliability, and infrastructure engineering organization responsible for implementing the production stateful-data platform for this project.

Operate as a coordinated:

* Principal Software Architect
* Cloud Architect
* Database Architect
* Staff DevOps Engineer
* Database Infrastructure Engineer
* Distributed Systems Engineer
* Site Reliability Engineer
* Storage Engineer
* Infrastructure Security Engineer
* Networking Engineer
* Performance Engineer
* Reliability Engineer
* QA Engineer
* Technical Writer

You are an implementation agent, not a teacher.

Your responsibility is to inspect the repository and implement the complete production stateful-data infrastructure covered by this prompt without breaking existing application or infrastructure behavior.

Do not merely describe the data platform. Create the real repository-side Terraform, configuration, policies, storage architecture, backup/recovery configuration, validation tooling, tests, and documentation required by this scope, and perform external cloud operations only when the environment genuinely permits them.

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

The repository is the source of truth for the current infrastructure implementation state.

Before changing anything:

1. Inspect Infrastructure Volumes already present in the repository.
2. Inspect backend services, Prisma configuration, migration strategy, database usage, Redis usage, Kafka/Redpanda usage, OpenSearch/search usage, S3/object-storage usage, worker processes, environment variables, connection settings, health checks, and application contracts.
3. Inspect Terraform modules, Helm charts, Kubernetes configuration, Docker configuration, environment files, scripts, CI configuration, tests, and infrastructure documentation.
4. Determine the actual persistence and infrastructure requirements of each application component.
5. Determine the existing:

   * PostgreSQL/PostGIS configuration
   * Redis topology
   * Kafka/Redpanda assumptions
   * OpenSearch assumptions
   * S3 bucket structure
   * encryption model
   * credentials/secrets boundary
   * backup requirements
   * retention requirements
   * connection requirements
6. Determine which stateful infrastructure already exists.
7. Preserve compatible working infrastructure.
8. Extend the existing infrastructure rather than creating parallel data platforms.
9. Do not invent data stores that are not required by the application architecture.
10. Do not redesign the application's logical database schema in this infrastructure volume.

This prompt is independently executable.

Do not depend on another AI conversation or on another prompt being pasted into the repository.

---

# INFRASTRUCTURE TARGET

The intended stateful platform uses infrastructure appropriate to:

* AWS
* PostgreSQL + PostGIS
* Redis
* Kafka or Redpanda
* OpenSearch/Elasticsearch-compatible search
* S3
* KMS
* private networking
* encrypted transport and storage
* environment separation
* automated backup and recovery
* high availability
* controlled retention
* monitoring hooks for later observability infrastructure

This volume implements the **production stateful-data platform**.

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

Implement production-grade persistent infrastructure for:

* PostgreSQL/PostGIS
* Redis
* Kafka or Redpanda
* OpenSearch/Elasticsearch-compatible search
* S3/object storage

Establish:

* high-availability architecture
* encryption
* private networking
* authentication
* authorization
* backup
* point-in-time recovery where supported
* retention
* replication
* failover boundaries
* maintenance policies
* storage lifecycle
* recovery configuration
* environment isolation
* connection/security configuration
* capacity starting points
* data durability guarantees and limitations
* application integration contracts
* validation and recovery verification

The implementation must distinguish clearly between:

* source-of-truth transactional data
* ephemeral/cache data
* durable event-stream data
* derived search data
* immutable/private object artifacts

Do not treat all stateful systems as interchangeable.

---

# PRIMARY SCOPE

# POSTGRESQL / POSTGIS

## 1. Production PostgreSQL Architecture

Implement the production PostgreSQL infrastructure appropriate to the application's transactional workload.

Where AWS-managed PostgreSQL is the established architecture, use an appropriate managed service such as:

* Amazon RDS for PostgreSQL
* Amazon Aurora PostgreSQL

Use the repository's existing architectural direction rather than arbitrarily replacing it.

The implementation must provide:

* production instance/cluster boundary
* storage configuration
* subnet placement
* security groups
* encryption
* parameter configuration
* availability strategy
* backup configuration
* maintenance configuration
* deletion protection where justified
* monitoring hooks for later observability

Do not assume that a particular database class is capacity-tested.

Document it as an initial production sizing assumption.

---

# 2. PostgreSQL High Availability

Configure high availability appropriate to the selected AWS database architecture.

Support, where applicable:

* multi-AZ deployment
* synchronous standby/failover behavior
* automatic failover
* backup retention
* maintenance behavior
* controlled upgrade path

Clearly distinguish:

* failover capability
* read scaling
* disaster recovery

These are different concerns.

Do not claim multi-region disaster recovery merely because multi-AZ failover is enabled.

---

# 3. PostgreSQL Storage and Encryption

Configure:

* encrypted storage
* KMS integration
* storage sizing
* autoscaling where appropriate
* IOPS/throughput assumptions where supported
* snapshot encryption
* secure deletion behavior where appropriate

Do not expose encryption keys.

Do not hard-code storage values that will silently become unsafe as data volume grows.

---

# 4. PostgreSQL Backups

Implement automated backups.

Support:

* backup retention
* automated snapshots
* backup window
* maintenance window
* point-in-time recovery where the selected service supports it
* snapshot tagging
* backup encryption
* cross-environment separation

The backup configuration must be explicit.

Do not claim that backup success has been tested merely because a Terraform resource exists.

---

# 5. PostgreSQL Recovery Strategy

Establish repository-side recovery configuration and documentation.

Document:

* recovery objectives
* restore process
* point-in-time recovery process
* snapshot restoration
* application reconnection
* migration compatibility
* rollback considerations

Where actual recovery execution is not possible:

* provide the repository-side configuration
* provide verification procedures
* do not fake recovery execution

Detailed recovery drills belong to the final infrastructure volume.

---

# 6. PostgreSQL Parameter Configuration

Configure only parameters justified by the application architecture.

Consider:

* connection management
* statement/time limits
* logging boundaries
* SSL enforcement
* timezone behavior
* extension configuration
* memory/workload-related parameters where supported

Do not blindly copy generic PostgreSQL tuning guides.

Document non-default settings and why they exist.

---

# 7. PostgreSQL Extensions

Ensure the infrastructure supports required extensions, especially:

* PostGIS
* any additional extension explicitly required by the repository

Do not modify the logical schema here.

Do not introduce arbitrary extensions merely because they are available.

---

# 8. PostgreSQL Connection Architecture

Integrate application connectivity with the production database.

Support:

* private endpoints
* TLS/SSL
* credential retrieval through the existing secret system
* connection-string generation/reference
* connection limits
* application/workload separation
* migration access boundary

Where a connection pooler such as PgBouncer is required by the architecture, establish the infrastructure boundary without inventing it where the repository does not support it.

The later capacity/resilience volume may refine connection scaling.

---

# 9. PostgreSQL Security

Implement:

* private networking
* least-privilege security groups
* encryption at rest
* encryption in transit
* restricted administrative access
* separate application credentials
* restricted migration/administrative credentials
* secret rotation boundary where supported

Do not expose PostgreSQL directly to the internet.

Do not hard-code passwords in Terraform.

---

# 10. PostgreSQL Migration Compatibility

Ensure the production database infrastructure is compatible with the repository's Prisma migration process.

Do not run destructive schema modifications from this infrastructure volume.

Do not automatically reset production databases.

Provide the configuration and documented execution boundary required for:

* migration jobs
* deployment-time migration
* controlled migration execution

Actual CI/CD orchestration belongs to Infrastructure Volume 5.

---

# REDIS

## 11. Production Redis Architecture

Implement the production Redis architecture appropriate to the platform's actual uses.

Redis may support:

* caching
* session infrastructure
* rate limiting
* idempotency
* locks/concurrency
* presence
* realtime coordination
* BullMQ/worker workloads

Do not assume all workloads must share a single Redis cluster permanently.

Where workload isolation is necessary, establish appropriate deployment boundaries based on actual usage.

---

# 12. Redis High Availability

Use an appropriate managed Redis architecture, such as an AWS-managed Redis service compatible with the project's requirements.

Support, where applicable:

* replication
* automatic failover
* multi-AZ deployment
* cluster/shard configuration
* node groups
* maintenance behavior

Clearly distinguish:

* high availability
* horizontal partitioning
* persistence
* disaster recovery

---

# 13. Redis Persistence

Configure persistence based on the actual role of each Redis workload.

Do not assume every Redis key is equally important.

Classify workloads according to whether data is:

* cache/rebuildable
* operational state
* session-related
* idempotency-related
* queue-related
* coordination-related

Apply durability settings appropriate to the classification.

Do not blindly optimize Redis for persistence if a workload is intentionally ephemeral.

---

# 14. Redis Encryption and Security

Implement:

* encryption at rest
* encryption in transit
* authentication
* private networking
* restricted security groups
* KMS where applicable

Do not expose Redis publicly.

Do not place Redis passwords in source control.

---

# 15. Redis Configuration

Configure only parameters justified by application requirements.

Consider:

* eviction policy
* timeout behavior
* connection limits
* TLS behavior
* persistence
* maintenance
* failover
* memory boundaries

Do not select eviction behavior that could silently destroy authoritative operational state.

When different Redis workloads require different eviction semantics, maintain explicit workload separation.

---

# 16. Redis Application Integration

Ensure the Kubernetes/application configuration can consume the correct production Redis endpoints securely.

Support:

* secret references
* endpoint references
* TLS parameters
* authentication
* connection configuration
* environment separation

Do not embed permanent credentials in Helm values or ConfigMaps.

---

# KAFKA / REDPANDA

## 17. Production Streaming Architecture

Implement the production event-streaming platform using the repository's selected architecture:

* Amazon-managed Kafka-compatible service where appropriate
* or the selected Redpanda architecture

Do not arbitrarily switch technologies if the application already depends on one.

Support the platform's event-streaming requirements for:

* trip events
* dispatch events
* location-related events where applicable
* financial events
* notifications
* analytics
* operational events

Do not redesign application event contracts.

---

# 18. Streaming High Availability

Configure:

* multi-AZ broker placement
* replication
* controlled partition placement
* fault tolerance
* broker availability
* storage durability

Do not claim that a replication factor alone guarantees application-level exactly-once behavior.

---

# 19. Kafka Topic and Partition Infrastructure

Establish repository-side topic infrastructure only for actual documented event domains.

Where topic creation is infrastructure-managed, define:

* topic names
* partitions
* replication factor
* retention
* cleanup policy
* compression where appropriate
* configuration boundaries

Respect the application's existing event contracts.

Do not create dozens of speculative topics.

Do not silently rename existing topic contracts.

---

# 20. Event Retention

Configure retention based on the actual semantics of the event stream.

Distinguish between:

* short-lived operational streams
* replayable domain events
* analytics streams
* audit-related streams

Retention must be explicit and documented.

Do not treat Kafka as the permanent system of record for transactional data unless the architecture says so.

---

# 21. Streaming Security

Implement:

* private networking
* TLS
* authentication
* authorization/ACL boundary
* encryption at rest
* KMS integration where applicable
* restricted client access

Applications should receive only the stream permissions they require.

Do not give all services cluster-wide administrative access.

---

# 22. Consumer/Producer Connectivity

Ensure production application workloads can consume the stream platform through secure configuration.

Support:

* broker endpoints
* TLS configuration
* authentication
* topic permissions
* consumer-group permissions
* producer permissions

Do not hard-code broker credentials.

Do not expose Kafka brokers publicly.

---

# 23. Streaming Durability and Recovery

Document:

* replication
* retention
* recovery behavior
* topic restoration
* producer/consumer reconnect expectations
* offset handling
* consumer-group recovery

Actual failure/recovery drills belong to Infrastructure Volume 6.

Do not claim that a recovery procedure has been tested merely because it is documented.

---

# OPENSEARCH / SEARCH

## 24. Production Search Architecture

Implement the production search infrastructure required by the application.

Use the repository's selected OpenSearch/Elasticsearch-compatible architecture.

Support:

* dedicated search domain/cluster
* private networking
* multiple nodes where justified
* storage configuration
* encryption
* access policy
* endpoint configuration
* environment separation

Search is a derived data system unless architecture explicitly defines otherwise.

---

# 25. Search High Availability

Configure:

* multi-node deployment
* availability-zone distribution where supported
* shard/replica architecture
* automated failure handling where supported
* durable storage

Do not claim search availability equals transactional-data availability.

---

# 26. Search Storage and Lifecycle

Configure:

* encrypted storage
* storage sizing
* rollover/lifecycle strategy where appropriate
* snapshot strategy where supported
* retention boundaries
* index management controls

Search data must remain rebuildable from canonical sources where architecture requires that property.

---

# 27. Search Security

Implement:

* private network access
* authentication
* authorization
* encryption at rest
* encryption in transit
* KMS where applicable
* restricted service access

Do not expose the search cluster directly to the public internet.

Do not embed admin credentials in source control.

---

# 28. Search Integration

Provide secure configuration for application workloads to reach the search service.

Support:

* endpoint references
* TLS
* credentials/secrets
* environment separation
* workload access policies

Do not duplicate the search-indexing application logic in infrastructure.

---

# S3 / OBJECT STORAGE

## 29. Production Object-Storage Architecture

Implement production S3 storage according to the repository's actual object categories.

Possible classes include:

* user/media assets
* receipts
* private safety evidence
* documents
* exports
* other explicitly documented application objects

Do not create arbitrary buckets unrelated to application requirements.

---

# 30. S3 Security

Every production bucket must use, where appropriate:

* block public access
* encryption
* least-privilege bucket policy
* environment isolation
* versioning where justified
* secure transport enforcement
* controlled access logging/monitoring integration boundary

Do not expose private application data through public buckets.

---

# 31. S3 Encryption

Implement:

* server-side encryption
* KMS integration where appropriate
* key access restrictions
* encryption-aware bucket policies

Do not expose KMS permissions broadly.

---

# 32. S3 Lifecycle Management

Implement lifecycle policies appropriate to each object class.

Consider:

* transition
* expiration
* noncurrent-version expiration
* incomplete multipart-upload cleanup
* legal/retention requirements where applicable

Do not automatically expire safety/evidence or financial artifacts without checking the repository's retention policy.

Do not invent retention periods.

Use the architecture's documented retention requirements.

---

# 33. S3 Versioning

Enable versioning where durability or auditability requires it.

Avoid enabling indefinite version retention without a lifecycle strategy.

Where versioning is enabled:

* define noncurrent-version cleanup
* ensure storage growth is controlled
* document the rationale

---

# 34. S3 Access Architecture

Use:

* workload IAM
* role-based access
* private buckets
* application-generated authorized access mechanisms
* environment-specific policies

Do not distribute permanent access keys to application services.

Do not grant broad `s3:*` access unless specifically justified and scoped.

---

# 35. S3 Replication and Disaster-Recovery Boundary

Where the architecture requires multi-region durability, establish the repository-side design for:

* cross-region replication
* replication roles
* destination buckets
* encryption compatibility
* replication filters
* recovery documentation

Do not claim disaster recovery is operational merely because replication Terraform exists.

Detailed resilience testing belongs to Infrastructure Volume 6.

---

# DATA CLASSIFICATION AND RETENTION

## 36. Stateful Data Classification

Create or update infrastructure documentation that categorizes platform state into:

### Transactional

Examples:

* users
* drivers
* trips
* payments
* ledger records
* scheduled trips

PostgreSQL is the canonical transactional store unless the architecture states otherwise.

### Operational/ephemeral

Examples:

* cache
* presence
* transient coordination
* short-lived state

Redis may host these where appropriate.

### Event-stream

Examples:

* domain events
* asynchronous events
* analytics events

Kafka/Redpanda is the streaming transport, not automatically the transactional source of truth.

### Search

Examples:

* searchable projections
* indexed entities
* operational search

OpenSearch is derived/search-oriented unless architecture explicitly states otherwise.

### Object

Examples:

* media
* receipts
* documents
* evidence
* exports

S3 is the object-storage system.

Do not allow one system to become an accidental source of truth for another domain.

---

# 37. Retention Boundaries

Implement or document infrastructure-compatible retention for:

* database backups
* Redis persistence where applicable
* Kafka/Redpanda topics
* OpenSearch indices
* S3 objects
* snapshots

Retention must follow the project's documented data lifecycle.

Do not invent arbitrary legal or regulatory retention requirements.

---

# 38. Encryption Standardization

Ensure consistent encryption across stateful infrastructure.

Cover:

* PostgreSQL
* Redis
* Kafka/Redpanda
* OpenSearch
* S3
* backups/snapshots

Use the established KMS strategy.

Do not create unnecessary duplicated key hierarchies.

---

# 39. Private Connectivity

Ensure all production stateful services remain private.

Applications running in EKS should access them through:

* private AWS endpoints
* private subnets
* security groups
* controlled routing

No production database, Redis, search, or broker endpoint should be publicly exposed.

---

# 40. Secrets Integration

Integrate stateful credentials with the previously established:

* AWS Secrets Manager
* SSM Parameter Store
* workload identity
* Kubernetes secret integration

Do not put passwords directly into:

* Terraform source
* Helm values
* ConfigMaps
* Docker images
* application repositories

Where a managed service supports secret rotation, establish the infrastructure boundary for it.

---

# 41. Environment Isolation

Ensure stateful services are isolated by:

* environment
* account/project
* credentials
* network
* encryption
* backup lifecycle
* endpoint configuration

Do not allow staging workloads to connect to production stateful systems.

Do not reuse production credentials elsewhere.

---

# 42. Database and Search Data Seeding Boundaries

Production infrastructure must not depend on development seed scripts.

Distinguish:

* schema migrations
* application test data
* local seed data
* production data

Do not automatically inject sample records into production services.

---

# 43. Backup Metadata and Tagging

Apply consistent metadata to backups/snapshots where supported.

Include useful information such as:

* project
* environment
* service
* data classification
* retention class
* managed-by
* owner

Do not include secrets or sensitive business data in metadata.

---

# 44. Maintenance and Upgrade Boundaries

Configure or document safe maintenance practices for:

* PostgreSQL
* Redis
* Kafka/Redpanda
* OpenSearch
* S3-related infrastructure

Support:

* maintenance windows
* version pinning
* controlled upgrades
* compatibility considerations
* rollback limitations

Do not automatically upgrade production stateful services to latest versions.

---

# 45. Data Integrity and Application Contracts

Verify infrastructure supports application guarantees such as:

* transactional consistency
* idempotency state
* event durability
* queue durability where required
* financial record persistence
* trip state persistence
* geographic queries through PostGIS
* search projection rebuildability
* object authorization

Do not move consistency logic into Terraform or Kubernetes.

---

# 46. Connection and Quota Awareness

For each stateful service, document relevant infrastructure boundaries around:

* connections
* clients
* throughput
* storage
* partitions
* shards
* memory
* request rates
* API quotas

These are starting constraints, not claims of tested maximum capacity.

Detailed capacity testing belongs to Infrastructure Volume 6.

---

# 47. Stateful Data Validation

Implement repository-side validation for all stateful infrastructure.

Support:

* Terraform formatting
* Terraform validation
* linting
* security scanning
* policy validation
* configuration checks
* endpoint/configuration consistency checks
* backup configuration validation

Use repository-supported tooling where available.

---

# 48. Local Parity

Maintain appropriate local-development equivalents established by Infrastructure Volume 1.

Ensure production infrastructure changes do not unnecessarily break:

* local PostgreSQL/PostGIS
* local Redis
* local Kafka/Redpanda
* local OpenSearch
* local S3-compatible storage

Do not require developers to connect to production-managed services for normal local development.

---

# 49. Recovery Validation

Where actual managed-service access is available, validate as much as safely possible:

* backup status
* service health
* connectivity
* encryption settings
* endpoint access
* replica/HA configuration

Do not perform destructive recovery tests against production merely to satisfy this prompt.

Where real recovery cannot be tested:

* validate configuration
* validate documented restore procedures
* report the limitation honestly

---

# 50. Documentation

Create or update detailed stateful-infrastructure documentation.

Document:

* PostgreSQL architecture
* PostGIS
* backups
* PITR
* restore
* HA
* Redis topology
* Redis durability classification
* Kafka/Redpanda architecture
* topics/retention
* OpenSearch architecture
* index/search durability
* S3 buckets
* lifecycle
* replication
* encryption
* IAM
* secrets
* environment isolation
* maintenance
* connection limits
* data classification
* retention
* recovery procedures
* local development
* validation
* actual deployment status

Documentation must clearly distinguish:

* configured
* locally validated
* statically validated
* actually deployed
* actually tested

---

# 51. Stateful Infrastructure Testing

Implement meaningful infrastructure tests where practical.

## PostgreSQL

Validate:

* network placement
* encryption
* backups
* retention
* parameter configuration
* PostGIS compatibility
* environment separation

## Redis

Validate:

* topology
* authentication
* encryption
* private connectivity
* persistence behavior
* eviction configuration

## Kafka/Redpanda

Validate:

* broker configuration
* replication settings
* topic definitions
* retention
* ACL intent
* secure connectivity

## OpenSearch

Validate:

* node topology
* storage
* encryption
* private networking
* access policy
* lifecycle configuration

## S3

Validate:

* bucket encryption
* public-access block
* lifecycle
* versioning
* access policy
* replication configuration where applicable

Use static/mocked validation when cloud access is unavailable.

Do not claim live service behavior without live validation.

---

# 52. Application Integration Validation

Where environment access permits, verify that the application configuration can reach:

* PostgreSQL/PostGIS
* Redis
* Kafka/Redpanda
* OpenSearch
* S3

Validate:

* DNS
* network reachability
* credentials retrieval
* TLS
* ports
* endpoint references
* environment separation

Do not modify application code to bypass security.

---

# OUT OF SCOPE

Do not implement the later infrastructure scopes in this volume.

Explicitly out of scope:

* Prometheus
* Grafana
* Loki
* Tempo
* centralized OpenTelemetry collector deployment
* security-monitoring dashboards
* centralized alerting
* GitHub Actions deployment pipeline
* ECR build/release pipeline
* Route 53 global traffic management
* CloudFront
* WAF
* global edge routing
* complete multi-region traffic failover
* comprehensive disaster-recovery drills
* load testing
* capacity testing
* chaos testing
* incident-response runbooks
* day-2 operations
* backend database schema redesign
* Prisma schema redesign
* backend application code
* frontend code
* mobile code
* Kubernetes redesign
* a separate QA phase
* a separate final-integration phase

Do not create additional infrastructure volumes.

The next volume is **Infrastructure Volume 4 — Observability/Security Operations**.

---

# IMPLEMENTATION RULES

## Repository First

Inspect before modifying.

Determine actual:

* database architecture
* Redis usage
* event-streaming platform
* search platform
* object-storage categories
* existing backup strategy
* existing secrets architecture
* existing network/security architecture
* actual application dependencies

Do not invent infrastructure that the application does not use.

## Preserve Previous Infrastructure

Extend:

* VPC/networking
* IAM
* KMS
* Terraform
* EKS
* Helm
* secret/configuration boundaries

Do not create conflicting stateful resources.

## Source-of-Truth Discipline

Respect the distinction between:

* transactional
* operational
* event-stream
* search
* object data

Do not create hidden duplicate sources of truth.

## Security

Use:

* private networking
* encryption
* least privilege
* secure authentication
* workload identity
* protected backups
* controlled administrative access

Do not expose stateful services publicly.

## Backup Discipline

Backups must be configured explicitly.

Do not equate configuration with tested recoverability.

## Retention Discipline

Use architecture-defined retention.

Do not invent regulatory requirements or arbitrary expiration periods.

## Capacity Discipline

Document starting capacity assumptions without presenting them as tested limits.

## No Destructive Shortcuts

Do not:

* reset production databases
* destroy stateful resources for convenience
* disable encryption
* disable access controls
* expose services publicly
* commit credentials

## Infrastructure as Code

Represent infrastructure through Terraform and repository configuration.

Manual console configuration may only exist where unavoidable and must be documented.

## Environment-Aware Execution

The implementation environment may lack:

* AWS credentials
* database access
* Redis access
* Kafka/Redpanda access
* OpenSearch access
* S3 access

When external execution is unavailable:

* implement repository-side infrastructure
* validate configuration statically
* validate local equivalents
* report unavailable live validation honestly

Do not fake cloud-service health.

## No Pseudo-Code

Create actual:

* Terraform
* policies
* configuration
* lifecycle rules
* backup settings
* IAM
* validation scripts
* tests
* documentation

Do not use placeholders presented as finished infrastructure.

---

# VALIDATION REQUIREMENTS

Before considering this volume complete:

1. Inspect the full repository and existing infrastructure.
2. Run Terraform formatting.
3. Run Terraform validation.
4. Run Terraform lint/static analysis.
5. Run security scanning available in the repository.
6. Validate PostgreSQL architecture.
7. Validate PostGIS support.
8. Validate PostgreSQL encryption.
9. Validate PostgreSQL backup configuration.
10. Validate PITR configuration where supported.
11. Validate PostgreSQL network security.
12. Validate PostgreSQL credential/secrets integration.
13. Validate PostgreSQL maintenance settings.
14. Validate Redis topology.
15. Validate Redis encryption.
16. Validate Redis authentication.
17. Validate Redis persistence configuration.
18. Validate Redis eviction semantics against workload classification.
19. Validate Kafka/Redpanda broker architecture.
20. Validate topic definitions.
21. Validate topic retention.
22. Validate replication configuration.
23. Validate stream access policies.
24. Validate secure producer/consumer connectivity configuration.
25. Validate OpenSearch topology.
26. Validate OpenSearch storage.
27. Validate OpenSearch encryption.
28. Validate OpenSearch access policy.
29. Validate search lifecycle configuration.
30. Validate S3 bucket encryption.
31. Validate S3 public-access block.
32. Validate S3 lifecycle policies.
33. Validate S3 versioning where required.
34. Validate S3 access policies.
35. Validate S3 replication configuration where applicable.
36. Validate stateful environment isolation.
37. Validate KMS integration.
38. Validate secret/configuration integration.
39. Validate local-development parity.
40. Validate application endpoint/configuration consistency.
41. Validate documentation commands.
42. Verify no stateful production service is publicly exposed.
43. Verify no production credentials are committed.
44. Verify no Terraform state artifacts are committed.
45. Verify no later observability/delivery/resilience scope was unnecessarily implemented.

Where live AWS/service access is available, validate non-destructively as much as practical.

Where live access is unavailable:

* perform all repository-side validation possible
* validate local equivalents
* verify Terraform/resource intent statically
* explicitly report what could not be executed

Never claim:

* backup completion
* restore success
* failover success
* live replication
* live database health
* live Redis health
* live Kafka/Redpanda health
* live OpenSearch health
* live S3 replication

unless actually verified.

---

# INTEGRATION CHECK

Before finalizing, verify that the stateful-data platform integrates cleanly with Infrastructure Volumes 1 and 2.

Confirm that:

* PostgreSQL uses the established VPC and private subnet architecture
* Redis uses the established private network and security model
* Kafka/Redpanda uses the established network and IAM/security model
* OpenSearch uses the established private connectivity architecture
* S3 uses the established KMS/IAM/environment conventions
* application workloads in EKS can consume the correct private endpoints
* Kubernetes secrets/configuration can obtain the required credentials safely
* workload IAM policies are least privilege
* financial/trip/user data remains in the intended transactional source of truth
* Redis is not accidentally used as a permanent transactional store
* Kafka/Redpanda is not treated as the canonical transactional database
* OpenSearch remains derived/search-oriented where intended
* S3 objects remain private and authorization-controlled
* backup and retention policies match application data classes
* environment isolation prevents staging/test from touching production state
* later observability can instrument these systems
* later CI/CD can deploy/update them without redesign
* later resilience/capacity work can extend the stateful infrastructure without replacing its architecture

Do not introduce a temporary stateful architecture that later infrastructure volumes must replace.

---

# DEFINITION OF DONE

This volume is complete only when:

### PostgreSQL / PostGIS

* production PostgreSQL architecture is implemented
* HA configuration is implemented
* encrypted storage is implemented
* KMS integration is implemented
* backups are implemented
* PITR is configured where supported
* recovery configuration/documentation is implemented
* parameter configuration is implemented
* PostGIS compatibility is established
* secure connectivity is implemented
* least-privilege database access is implemented
* migration compatibility is documented

### Redis

* production Redis architecture is implemented
* HA/failover is implemented where appropriate
* persistence semantics are defined
* encryption is implemented
* authentication is implemented
* private connectivity is implemented
* workload classification is documented
* eviction configuration is appropriate
* application integration is configured

### Kafka / Redpanda

* production streaming architecture is implemented
* HA/replication is implemented
* required documented topics are configured
* retention is configured
* security/access control is implemented
* secure application connectivity is implemented
* durability/recovery boundaries are documented

### OpenSearch

* production search infrastructure is implemented
* HA topology is implemented
* storage is configured
* encryption is implemented
* private access is implemented
* access control is implemented
* lifecycle configuration is implemented
* application integration is configured

### S3

* production bucket architecture is implemented
* encryption is implemented
* public-access block is enabled
* lifecycle policies are implemented
* versioning is configured where appropriate
* access policies are least privilege
* replication boundary is implemented where required

### Shared

* data classification is documented
* retention boundaries are documented/implemented
* environment isolation is enforced
* secrets integration is implemented
* private connectivity is enforced
* validation is implemented
* tests are present where practical
* documentation is updated
* actual cloud validation status is honestly reported
* no production credentials are committed
* no stateful services are publicly exposed
* no fake recovery/health/failover claims are made
* no placeholders remain
* no later infrastructure scope was unnecessarily implemented

---

# IMPLEMENTATION REPORT

At the end of execution, provide a concise report containing:

## Files Changed

List created, modified, and removed infrastructure files.

## Stateful Infrastructure Implemented

Summarize:

* PostgreSQL/PostGIS
* Redis
* Kafka/Redpanda
* OpenSearch
* S3
* backups
* encryption
* retention
* replication
* recovery configuration

## Data Classification

Summarize how transactional, operational, event-stream, search, and object data are separated.

## Validation

Report the exact commands executed and their results.

## External Infrastructure Status

Clearly state which AWS/stateful-service operations were actually performed and which could not be performed because of environment limitations.

Do not infer live service health from static Terraform validation.

## Follow-Up Dependencies

Identify what Infrastructure Volume 4 needs to instrument and secure operationally.

Do not invent additional infrastructure phases.

---

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement the complete production stateful-data infrastructure defined by this prompt.

Preserve all working application and infrastructure behavior outside the necessary scope of these changes.

Extend the infrastructure established by Volumes 1 and 2 rather than creating parallel foundations.

Create the real Terraform, policies, configuration, backup/lifecycle settings, storage definitions, validation tooling, tests, and documentation required for:

* PostgreSQL/PostGIS
* Redis
* Kafka/Redpanda
* OpenSearch
* S3

Do not merely describe the data platform.

Do not wait for another prompt.

Do not use pseudo-code, placeholder resources, fake endpoints, fake health results, fake backup success, fake failover success, fabricated credentials, or simulated cloud validation.

When live cloud access is unavailable, fully implement the repository-side stateful infrastructure and validate everything possible statically and locally.

Respect private networking, encryption, least privilege, data classification, backup integrity, environment isolation, retention, durability, and recovery boundaries.

Finish only when this stateful-data infrastructure volume is genuinely implemented, validated, documented, and ready for Infrastructure Volume 4 to build the observability and security-operations layer on top of it.
