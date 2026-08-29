You are operating in Senior Engineering Team Mode.

Complete the production-grade infrastructure, DevOps, CI/CD, multi-region deployment, autoscaling, observability, security operations, disaster recovery, backup validation, cost optimization, incident response, operational tooling, and production-release infrastructure for an enterprise-scale global ride-hailing and mobility platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

Use the previously approved infrastructure architecture as the source of truth.

Do not redesign the application architecture.

Do not implement backend business logic.

Do not implement frontend code.

Do not implement mobile code.

────────────────────────────────────────

MISSION

Complete the infrastructure required for:

• Production application deployment
• Rider APIs
• Driver APIs
• Web applications
• Real-time WebSocket gateways
• Location services
• Dispatch
• Matching
• Trip services
• Pricing
• Payments
• Notifications
• Safety
• Fraud
• Support
• Business accounts
• Analytics
• Administration
• Background workers
• Media/identity document processing
• Search infrastructure
• Multi-region deployment
• Global routing
• Continuous delivery
• Automated rollback
• Observability
• Security operations
• Disaster recovery
• Capacity management
• Cost optimization
• Incident response
• Production certification

────────────────────────────────────────

PRIMARY TECHNOLOGY STACK

Cloud:

• AWS

Infrastructure as Code:

• Terraform

Containers:

• Docker
• Amazon ECR

Orchestration:

• Kubernetes
• Amazon EKS

Packaging:

• Helm

CI/CD:

• GitHub Actions

Database:

• Amazon RDS/Aurora PostgreSQL
• PostGIS

Cache:

• Amazon ElastiCache for Redis

Event streaming:

• Kafka/Redpanda or approved managed equivalent

Search:

• Amazon OpenSearch or approved managed equivalent

Storage:

• Amazon S3

CDN:

• Amazon CloudFront

DNS:

• Amazon Route 53

TLS:

• AWS Certificate Manager

Security:

• IAM
• KMS
• WAF
• Security Groups
• Network ACLs
• Kubernetes RBAC
• NetworkPolicies
• Pod Security Standards

Secrets:

• AWS Secrets Manager

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

────────────────────────────────────────

IMPLEMENTATION RULES

Never generate pseudo-configuration.

Never generate placeholders.

Never generate TODO infrastructure.

Never omit required configuration.

Every Terraform file must be syntactically valid.

Every Helm template must be complete.

Every Dockerfile must build.

Every GitHub Actions workflow must be complete and security-conscious.

Never hard-code:

• AWS credentials
• API keys
• Payment secrets
• Database passwords
• Certificates
• Private keys

Never commit secrets.

Prefer:

• OIDC
• Short-lived credentials
• Workload identity
• Managed services
• Immutable image references

Never regenerate unchanged files.

Only modify existing files when necessary.

────────────────────────────────────────

KUBERNETES PRODUCTION ARCHITECTURE

Complete Kubernetes deployments for:

• API gateway
• Rider-facing APIs
• Driver-facing APIs
• Dispatch
• Matching
• Trip services
• Location services
• Pricing
• Payments
• Notifications
• Safety
• Fraud
• Support
• Business services
• Administration
• Web application
• General background workers
• Location workers
• Dispatch workers
• Analytics workers
• Notification workers
• Reconciliation workers

For every workload define:

• Deployment
• Service
• ServiceAccount
• ConfigMap where appropriate
• Secret reference
• Readiness probe
• Liveness probe
• Startup probe
• Resource requests
• Resource limits
• HorizontalPodAutoscaler
• PodDisruptionBudget
• NetworkPolicy
• Topology spread
• Affinity
• Anti-affinity

────────────────────────────────────────

HELM ARCHITECTURE

Complete reusable Helm charts.

Support chart patterns for:

• API services
• Real-time gateways
• Dispatch
• Matching
• Workers
• Web
• CronJobs
• Internal tools

Values must support:

• Development
• Test
• Staging
• Production

Do not duplicate templates unnecessarily.

Separate:

• Common defaults
• Environment configuration
• Region configuration
• Workload-specific values

────────────────────────────────────────

DEPLOYMENT STRATEGIES

Support:

• Rolling deployment
• Canary
• Blue-green where justified

Define strategy by service class.

STANDARD SERVICES:

• Rolling deployment

HIGH-RISK SERVICES:

• Canary or controlled rollout

CRITICAL FINANCIAL SERVICES:

• Strong release gates
• Backward-compatible migrations
• Automated rollback validation

REAL-TIME SERVICES:

• Connection draining
• Graceful shutdown
• Session reconnection support

────────────────────────────────────────

ZERO-DOWNTIME REQUIREMENTS

Ensure:

• Multiple replicas
• PDB
• Readiness probes
• Startup probes
• Graceful termination
• Connection draining
• Backward-compatible schema
• Deployment surge limits

Do not terminate all pods simultaneously.

────────────────────────────────────────

APPLICATION CONFIGURATION

Use:

• ConfigMaps for non-sensitive configuration
• AWS Secrets Manager for secrets
• Approved external-secrets integration

Configuration must be:

• Environment-specific
• Region-aware where necessary
• Versioned
• Auditable

Never put secret values into Helm values committed to Git.

────────────────────────────────────────

AUTOSCALING

Implement:

• HPA
• Cluster Autoscaler or Karpenter where approved
• Queue-based worker scaling
• Kafka-lag scaling
• WebSocket connection scaling

Scale using:

• CPU
• Memory
• Request rate
• Queue depth
• Kafka consumer lag
• Concurrent connections
• Location ingestion rate

Define safe minimum and maximum replicas.

────────────────────────────────────────

DISPATCH AUTOSCALING

Scale dispatch/matching resources according to:

• Ride-request rate
• Candidate-search rate
• Match latency
• CPU
• Queue depth
• Regional demand

Avoid scaling based only on CPU.

────────────────────────────────────────

LOCATION AUTOSCALING

Scale location services according to:

• Driver GPS update rate
• Concurrent connections
• Message throughput
• CPU
• Network saturation

Use regional deployment.

────────────────────────────────────────

WEBSOCKET SCALING

Support:

• Horizontal WebSocket gateways
• Connection affinity where required
• Redis-based coordination
• Health-aware routing
• Graceful connection drain
• Reconnect handling

Do not keep authoritative trip state only in WebSocket process memory.

────────────────────────────────────────

GLOBAL TRAFFIC MANAGEMENT

Configure:

• Route 53 latency routing
• Route 53 health checks
• Failover routing
• Weighted traffic shifting

Support:

• Region draining
• Controlled failover
• Failback

Do not automatically send traffic to a region that is not fully healthy.

────────────────────────────────────────

CLOUDFRONT

Complete CloudFront for:

• Web assets
• Public assets
• Documentation where appropriate
• Secure object access where approved

Configure:

• Origin access control
• Cache policies
• Response headers
• Compression
• TLS
• WAF
• Logging
• Regional failover where applicable

────────────────────────────────────────

ALB / NLB

Configure load balancing for:

• HTTP APIs
• Web applications
• WebSocket traffic
• Internal high-throughput traffic where appropriate

Support:

• TLS
• Health checks
• Idle timeouts
• Connection draining
• Access logs

────────────────────────────────────────

NETWORK SECURITY

Complete:

• Security Groups
• Network ACLs
• Kubernetes NetworkPolicies
• Private subnets
• VPC endpoints

Use explicit allow rules.

Minimize lateral movement.

────────────────────────────────────────

POD SECURITY

Enforce:

• Non-root
• Read-only filesystem where possible
• Dropped Linux capabilities
• Seccomp
• No privileged containers
• Restricted Pod Security Standards
• ServiceAccount isolation

Prevent workloads from accessing unnecessary Kubernetes or cloud resources.

────────────────────────────────────────

IAM / WORKLOAD IDENTITY

Use:

• GitHub Actions OIDC
• EKS Pod Identity or IRSA
• Least-privilege IAM policies

Create distinct roles for:

• API
• Dispatch
• Matching
• Location
• Payments
• Workers
• Analytics
• Notifications
• Media
• Backup
• Observability

Avoid broad wildcard permissions.

────────────────────────────────────────

CONTAINER SECURITY

Implement:

• Minimal base images
• Multi-stage builds
• Non-root
• Dependency pinning
• Vulnerability scanning
• SBOM
• Image signing
• Immutable release references

Block releases according to approved severity thresholds.

────────────────────────────────────────

ECR

Complete:

• Repository policy
• Scan-on-push
• Lifecycle policies
• Immutable tags
• Retention
• Access controls
• Cross-region replication where appropriate

Use:

• Git SHA
• Semantic release
• Environment metadata

Avoid mutable "latest" as the production deployment reference.

────────────────────────────────────────

CI/CD

Create GitHub Actions workflows for:

PULL REQUEST

• Formatting
• Linting where applicable
• Unit tests
• Integration tests
• Security scanning
• Secret scanning
• Dependency scanning
• Docker build
• Terraform validation
• Helm lint
• Kubernetes validation

BUILD

• Docker build
• SBOM
• Image scan
• Image signing
• ECR push
• Artifact metadata

DEPLOY

• Development
• Test
• Staging
• Production

────────────────────────────────────────

CI/CD SECURITY

Use:

• OIDC
• Minimal GitHub permissions
• Protected environments
• Required approvals
• Branch protection
• Signed commits/releases where adopted
• Environment-specific IAM roles

Production deployment must not use developer AWS credentials.

────────────────────────────────────────

PROMOTION PIPELINE

Use:

Development
→ Test
→ Staging
→ Production

Promotion should verify:

• Build artifact identity
• Test results
• Security status
• Infrastructure state
• Required approval

Promote the exact same immutable image artifact between environments whenever practical.

────────────────────────────────────────

ROLLBACK

Support:

• Application rollback
• Helm rollback
• Traffic rollback
• Canary rollback
• Database-safe rollback procedures

Do not automatically roll back database schema changes that are not reversible.

Use expand-and-contract.

────────────────────────────────────────

DATABASE OPERATIONS

Complete infrastructure for PostgreSQL.

Support:

• Multi-AZ
• Read replicas
• Automated backups
• PITR
• Encryption
• TLS
• Monitoring
• Failover
• Maintenance windows
• Performance monitoring

Monitor:

• CPU
• Memory
• Storage
• IOPS
• Connections
• Query latency
• Locks
• Deadlocks
• Replica lag

────────────────────────────────────────

DATABASE MIGRATION OPERATIONS

Define deployment integration for:

• Expand migration
• Application rollout
• Backfill
• Contract migration

Ensure old and new application versions can coexist where necessary.

────────────────────────────────────────

REDIS OPERATIONS

Complete:

• Multi-AZ
• Replication
• Automatic failover
• Encryption
• TLS
• Authentication
• Monitoring

Monitor:

• Memory
• Evictions
• Connections
• Command latency
• Replication
• Hot keys

────────────────────────────────────────

KAFKA / REDPANDA OPERATIONS

Complete:

• Multi-broker
• Multi-AZ
• Replication
• TLS
• Authentication
• Monitoring
• Retention

Monitor:

• Consumer lag
• Broker health
• Disk usage
• Partition distribution
• Under-replicated partitions
• Throughput

────────────────────────────────────────

OPENSEARCH OPERATIONS

Complete:

• Multi-node
• Multi-AZ
• Encryption
• Access policy
• Shards
• Replicas
• Snapshots
• Monitoring

Monitor:

• JVM
• CPU
• Memory
• Disk
• Search latency
• Indexing latency
• Cluster health

────────────────────────────────────────

S3 OPERATIONS

Configure:

• Versioning
• Encryption
• Block public access
• Lifecycle
• Replication
• Access logging where required

Buckets may include:

• Driver documents
• Verification assets
• Receipts
• Reports
• Exports
• Backups

────────────────────────────────────────

SECRETS ROTATION

Automate or operationally support rotation of:

• Database credentials
• Redis credentials
• Kafka credentials
• Payment secrets
• Maps credentials
• Notification credentials
• Verification-provider credentials
• OAuth secrets
• Webhook secrets

Applications must support safe credential rotation.

────────────────────────────────────────

OBSERVABILITY

Complete:

• OpenTelemetry Collector
• Prometheus
• Grafana
• Loki
• Tempo

Build dashboards for:

PLATFORM

• Requests
• Latency
• Errors
• Saturation

RIDER

• Ride requests
• Booking failures
• Trip failures

DRIVER

• Online drivers
• Location freshness
• Offer rate

DISPATCH

• Request rate
• Match rate
• Match latency
• Offer latency
• Assignment failures

LOCATION

• Update rate
• Staleness
• WebSocket connections
• Message rate

FINANCE

• Payment success
• Refunds
• Payouts

SAFETY

• Incidents
• Escalations

FRAUD

• Risk evaluations
• Fraud cases

INFRASTRUCTURE

• EKS
• Nodes
• Pods
• Database
• Redis
• Kafka
• OpenSearch

────────────────────────────────────────

SLO / SLI

Define SLOs for:

• API availability
• Booking
• Matching
• Location freshness
• WebSocket availability
• Trip-state propagation
• Fare estimation
• Payment processing
• Payout processing
• Notifications
• Support
• Analytics ingestion

For each define:

• SLI
• Measurement
• Target
• Error budget
• Alert threshold

────────────────────────────────────────

ALERTING

Create alerts for:

• API availability
• High error rate
• High latency
• Matching degradation
• Location staleness
• WebSocket connection drops
• Payment failures
• Payout failures
• Queue backlog
• Kafka lag
• Database health
• Redis health
• Search health
• Backup failures
• Certificate expiration
• Region degradation
• Security anomalies

Use severity:

• Warning
• Critical
• Emergency

────────────────────────────────────────

BACKUP

Complete backups for:

• PostgreSQL
• S3
• OpenSearch
• Terraform state
• Critical configurations

Support:

• Encryption
• Retention
• Cross-region recovery
• Monitoring

────────────────────────────────────────

RESTORE VALIDATION

Regularly validate:

• PostgreSQL PITR
• PostgreSQL full restore
• S3 object restoration
• OpenSearch snapshot restore
• Terraform state recovery
• Configuration restoration

A backup is not considered valid until restoration succeeds.

────────────────────────────────────────

DISASTER RECOVERY

Support recovery from:

• Pod failure
• Node failure
• AZ failure
• Database failure
• Redis failure
• Kafka failure
• OpenSearch failure
• S3 disruption
• Region failure

Define:

• Detection
• Failover
• Recovery
• Validation
• Reconciliation
• Failback

────────────────────────────────────────

MULTI-REGION

Complete regional infrastructure for:

• EKS
• APIs
• WebSockets
• Dispatch
• Location
• Workers
• Observability
• Data replication

Keep active trips regionally owned.

Avoid unnecessary cross-region synchronous requests.

────────────────────────────────────────

REGIONAL FAILOVER

Implement:

• Health evaluation
• Traffic draining
• Traffic redirection
• State recovery
• Reconciliation
• Failback

Prevent split-brain dispatch and trip ownership.

────────────────────────────────────────

CAPACITY PLANNING

Model capacity for:

• Riders
• Drivers
• Online drivers
• Ride requests
• Active trips
• GPS updates
• WebSocket connections
• API requests
• Matching operations
• Payment transactions
• Notifications
• Analytics events

For each define:

• Baseline
• Peak
• Burst
• Headroom
• Scaling threshold
• Expansion procedure

────────────────────────────────────────

COST OPTIMIZATION

Evaluate:

• EKS node right-sizing
• Autoscaling
• Karpenter
• Spot instances for safe non-critical workloads
• Reserved capacity
• Savings Plans
• Database sizing
• Redis sizing
• Search sizing
• S3 lifecycle
• CloudFront caching
• NAT Gateway costs
• Log retention
• Cross-region data transfer

Do not reduce:

• Financial integrity
• Safety
• Disaster recovery
• Required availability

solely for cost savings.

────────────────────────────────────────

INCIDENT RESPONSE

Define operational procedures for:

• API outage
• Booking outage
• Dispatch outage
• Location outage
• Payment outage
• Database outage
• Redis outage
• Kafka outage
• Search outage
• Region outage
• Security incident
• Credential compromise

Each incident process must include:

• Detection
• Severity
• Assignment
• Containment
• Communication
• Mitigation
• Recovery
• Validation
• Postmortem
• Corrective actions

────────────────────────────────────────

RUNBOOKS

Create runbooks for:

• Failed deployment
• Rollback
• Database failover
• Database restore
• Redis failover
• Kafka broker failure
• Search failure
• Location backlog
• Dispatch backlog
• Notification backlog
• Secret rotation
• Certificate renewal
• Region failover
• Region recovery
• Backup failure
• EKS outage

Each runbook must contain:

• Symptoms
• Detection
• Diagnosis
• Immediate mitigation
• Recovery
• Validation
• Escalation

────────────────────────────────────────

SECURITY OPERATIONS

Complete:

• IAM access review
• Permission review
• KMS review
• Secrets review
• Security-group review
• NetworkPolicy review
• Container scanning
• Dependency scanning
• Image-signature verification
• WAF review
• CloudTrail review
• Kubernetes audit review

────────────────────────────────────────

COMPLIANCE PREPARATION

Prepare infrastructure evidence and controls for:

• SOC 2
• ISO 27001
• GDPR
• PCI DSS scope minimization

Do not claim compliance certification without formal assessment.

────────────────────────────────────────

PRODUCTION SMOKE TESTING

After every production deployment validate:

• Web
• API
• Authentication
• Rider booking
• Driver availability
• Dispatch
• Matching
• Trip state
• Payment-provider connectivity
• Notifications
• Business APIs
• Admin APIs

Use safe, non-destructive testing.

────────────────────────────────────────

INFRASTRUCTURE VALIDATION

Automate validation for:

• Terraform fmt
• Terraform validate
• Terraform plan
• Terraform policy checks
• Helm lint
• Kubernetes schema
• Kubernetes security
• Docker build
• Container scan
• IAM policy validation
• Security-group validation
• NetworkPolicy validation
• WAF rules
• Backup policies

────────────────────────────────────────

RELEASE READINESS

A production release requires:

• Successful automated tests
• Security checks
• Infrastructure validation
• Image verification
• Health checks
• Observability
• Backup health
• Rollback readiness
• Required approvals
• Smoke-test success
• Known-risk documentation

────────────────────────────────────────

DOCUMENTATION

Generate:

• Production deployment guide
• Helm operations guide
• Terraform operations guide
• GitHub Actions guide
• EKS operations
• Autoscaling guide
• Global routing guide
• Multi-region guide
• PostgreSQL operations
• Redis operations
• Kafka operations
• OpenSearch operations
• S3 operations
• CloudFront operations
• WAF operations
• Secrets rotation guide
• Backup/restore guide
• Disaster-recovery guide
• Observability guide
• SLO/SLI guide
• Incident-response guide
• Runbooks
• Capacity-planning guide
• Cost-management guide
• Security-operations guide
• Production-release guide

────────────────────────────────────────

PROJECT INDEX

Update the infrastructure Project Index with:

• AWS accounts
• Regions
• Environments
• VPCs
• Network components
• Security groups
• IAM roles
• OIDC
• KMS
• Secrets
• EKS
• Node groups
• Namespaces
• Helm charts
• Terraform modules
• Docker images
• ECR repositories
• PostgreSQL
• Redis
• Kafka/Redpanda
• OpenSearch
• S3
• CloudFront
• Route 53
• ACM
• WAF
• CI/CD
• Autoscaling
• Observability
• Dashboards
• Alerts
• SLOs
• Backups
• Disaster recovery
• Runbooks
• Incident procedures
• Security operations
• Cost controls
• Infrastructure tests
• Smoke tests
• Generated files
• Modified files
• Remaining work
• Known risks
• Current milestone
• Production-readiness status

────────────────────────────────────────

IMPLEMENTATION MILESTONES

INFRASTRUCTURE MILESTONE 11

Production Helm charts, application deployments, worker deployments, health probes, PDBs, NetworkPolicies, service accounts, resource policies, and environment configuration.

INFRASTRUCTURE MILESTONE 12

Autoscaling, Karpenter or Cluster Autoscaler, queue-driven worker scaling, regional dispatch scaling, location scaling, WebSocket scaling, and capacity controls.

INFRASTRUCTURE MILESTONE 13

Load balancing, ingress, CloudFront, Route 53, ACM, WAF, global routing, regional traffic management, and failover.

INFRASTRUCTURE MILESTONE 14

GitHub Actions, OIDC, build pipelines, ECR, SBOM, vulnerability scanning, image signing, promotion, deployment, smoke testing, and rollback.

INFRASTRUCTURE MILESTONE 15

Multi-region EKS, regional services, regional dispatch, regional location, database recovery, S3 replication, search recovery, and regional failover.

INFRASTRUCTURE MILESTONE 16

OpenTelemetry, Prometheus, Grafana, Loki, Tempo, dashboards, alerts, SLOs, SLIs, trace propagation, and observability validation.

INFRASTRUCTURE MILESTONE 17

PostgreSQL operations, Redis operations, Kafka operations, OpenSearch operations, backup automation, restore testing, and reconciliation infrastructure.

INFRASTRUCTURE MILESTONE 18

Secrets rotation, IAM reviews, KMS operations, WAF hardening, container security, CloudTrail, Kubernetes audit, security scanning, and compliance preparation.

INFRASTRUCTURE MILESTONE 19

Disaster recovery, chaos/resilience procedures, capacity planning, cost optimization, incident response, operational runbooks, and recovery drills.

INFRASTRUCTURE MILESTONE 20

Production smoke testing, release certification, rollback validation, disaster-recovery validation, final documentation, infrastructure audit, and Project Index completion.

Each milestone should contain approximately 20–40 files where practical.

Every milestone must be validated before proceeding.

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never truncate files.

Never summarize infrastructure configuration instead of generating it.

Never generate pseudo-configuration.

Never generate placeholders.

Never generate TODO implementations.

When modifying an existing file:

1. Provide the exact file path.
2. State why it must change.
3. Provide the complete updated file.

Never regenerate unchanged files.

────────────────────────────────────────

SCOPE RESTRICTION

This volume completes the production infrastructure and DevOps implementation.

It covers:

• Kubernetes production workloads
• Helm
• Autoscaling
• Global traffic management
• Multi-region deployment
• CI/CD
• GitHub Actions
• ECR
• Container security
• Database operations
• Redis operations
• Kafka operations
• OpenSearch operations
• S3
• CloudFront
• Route 53
• ACM
• WAF
• Secrets rotation
• Observability
• SLO/SLI
• Alerts
• Backups
• Disaster recovery
• Capacity planning
• Cost optimization
• Incident response
• Runbooks
• Security operations
• Compliance preparation
• Infrastructure testing
• Production smoke testing
• Release certification

Do not implement:

• Backend business logic
• Frontend application logic
• Mobile application logic
• Domain features

────────────────────────────────────────

QUALITY BAR

Treat this infrastructure as mission-critical global transportation infrastructure supporting:

• Hundreds of millions of riders
• Millions of drivers
• Millions of active vehicles
• Massive GPS traffic
• Massive WebSocket traffic
• High ride-request throughput
• Low-latency dispatch
• High payment volume
• Large notification volume
• Multiple regions
• High availability
• Disaster recovery
• Continuous deployment
• Strict security
• Strict privacy

Prioritize:

• Availability
• Security
• Reliability
• Scalability
• Recoverability
• Observability
• Zero-downtime deployment
• Automation
• Operational simplicity
• Cost awareness
• Maintainability
• Production readiness
