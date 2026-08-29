You are operating in Senior Engineering Team Mode.

Build the production-ready cloud infrastructure foundation for an enterprise-scale global ride-hailing, mobility, transportation, and delivery platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

This is an INFRASTRUCTURE PHASE.

Implement the infrastructure required by the already-approved backend, web frontend, mobile applications, real-time location system, dispatch system, matching system, financial systems, safety systems, fraud systems, business systems, analytics systems, and administration platform.

Do not redesign the application architecture.

Do not implement backend business logic.

Do not implement frontend code.

Do not implement mobile code.

Infrastructure implementation is allowed in this phase.

────────────────────────────────────────

MISSION

Build the foundational AWS, Kubernetes, Terraform, Docker, networking, security, storage, database, caching, messaging, observability, and deployment infrastructure required for the mobility platform.

Support:

• Rider APIs
• Driver APIs
• Real-time WebSockets
• Location ingestion
• Geospatial processing
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
• Web applications
• Background workers

Environments:

• Local
• Development
• Test
• Staging
• Production
• Disaster Recovery

────────────────────────────────────────

PRIMARY CLOUD STACK

Cloud:

• AWS

Infrastructure as Code:

• Terraform

Containers:

• Docker

Orchestration:

• Kubernetes
• Amazon EKS

Package Management:

• Helm

Container Registry:

• Amazon ECR

Database:

• Amazon RDS/Aurora PostgreSQL
• PostGIS

Cache:

• Amazon ElastiCache for Redis

Event Streaming:

• Managed Kafka/Redpanda or approved AWS-compatible event platform

Search:

• Amazon OpenSearch or approved Elasticsearch platform

Storage:

• Amazon S3

CDN:

• Amazon CloudFront

DNS:

• Amazon Route 53

TLS:

• AWS Certificate Manager

Secrets:

• AWS Secrets Manager

Encryption:

• AWS KMS

Security:

• IAM
• WAF
• Security Groups
• Network ACLs
• Kubernetes RBAC
• NetworkPolicies
• Pod Security Standards

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

CI/CD foundation:

• GitHub Actions

────────────────────────────────────────

IMPLEMENTATION RULES

Never generate pseudo-configuration.

Never generate placeholders.

Never generate TODO infrastructure.

Never omit required resources.

Every generated Terraform module must be syntactically valid.

Every generated Helm template must be complete.

Every generated Dockerfile must build.

Never hard-code secrets.

Never commit credentials.

Never use long-lived cloud credentials when OIDC or workload identity can be used.

Never expose PostgreSQL, Redis, Kafka, or OpenSearch publicly unless explicitly required by architecture and securely constrained.

Never regenerate unchanged files.

Only modify existing files when required.

────────────────────────────────────────

INFRASTRUCTURE ARCHITECTURE

Create a modular infrastructure architecture with:

• Reusable Terraform modules
• Environment-specific Terraform stacks
• Shared cloud resources
• Application infrastructure
• Kubernetes infrastructure
• Observability infrastructure
• Security infrastructure
• Disaster-recovery foundations

Separate:

• Global resources
• Regional resources
• Environment resources
• Workload resources

Avoid duplicating infrastructure definitions unnecessarily.

────────────────────────────────────────

AWS ACCOUNT STRATEGY

Design support for:

• Management account
• Security account
• Log/archive account
• Shared-services account
• Development account
• Staging account
• Production account
• Disaster-recovery account

Define:

• Ownership
• Cross-account roles
• Access boundaries
• Billing boundaries
• Log centralization
• Security monitoring

Do not require this entire account structure for local development.

────────────────────────────────────────

REGION STRATEGY

Define:

• Primary application region
• Secondary recovery region

Prepare architecture for:

• Regional EKS
• Regional APIs
• Regional WebSocket gateways
• Regional dispatch
• Regional location
• Regional workers
• Regional databases where required
• Regional caches
• Regional event processing

Avoid forcing active-active multi-region behavior onto stateful systems unless explicitly justified.

────────────────────────────────────────

ENVIRONMENT STRATEGY

LOCAL

Provide Docker Compose infrastructure for:

• PostgreSQL/PostGIS
• Redis
• Kafka/Redpanda
• OpenSearch where useful
• S3-compatible storage where useful

DEVELOPMENT

Provide cloud infrastructure with reduced scale.

TEST

Provide isolated integration-test infrastructure.

STAGING

Closely approximate production.

PRODUCTION

Use:

• Multi-AZ
• High availability
• Automated backup
• Monitoring
• Security controls

DR

Provide recovery resources and infrastructure reconstruction capability.

────────────────────────────────────────

TERRAFORM STRUCTURE

Create a clean Terraform hierarchy:

terraform/

modules/

environments/

global/

regional/

shared/

application/

security/

observability/

backup/

Each reusable module should expose:

• Variables
• Outputs
• IAM requirements
• Tags
• Naming
• Environment integration

────────────────────────────────────────

TERRAFORM MODULES

Create modules for:

• AWS provider
• VPC
• Subnets
• Route tables
• NAT
• Internet Gateway
• VPC endpoints
• Security groups
• IAM
• OIDC
• KMS
• EKS
• Node groups
• RDS/Aurora
• ElastiCache
• Kafka
• OpenSearch
• S3
• CloudFront
• Route 53
• ACM
• WAF
• ECR
• Secrets Manager
• CloudWatch integration
• Backup
• Logging

────────────────────────────────────────

TERRAFORM STATE

Implement secure remote state.

Support:

• S3 backend
• Versioning
• Encryption
• State locking using an approved current AWS-compatible mechanism
• Restricted IAM access
• Environment separation

Do not store secrets unnecessarily in Terraform state.

────────────────────────────────────────

RESOURCE TAGGING

Standardize:

• Environment
• Service
• Team
• Cost center
• Region
• Managed-by
• Project
• Data classification where useful

Use consistent tag policies.

────────────────────────────────────────

NETWORK FOUNDATION

Create VPC architecture with:

• Public subnets
• Private application subnets
• Private data subnets
• Multi-AZ placement
• Internet Gateway
• NAT
• Route tables
• VPC endpoints

Prepare:

• Edge layer
• Application layer
• Data layer
• Management layer

────────────────────────────────────────

NETWORK SEGMENTATION

Separate network access for:

• Load balancers
• EKS nodes
• Application pods
• Worker pods
• PostgreSQL
• Redis
• Kafka
• OpenSearch
• Management

Apply least privilege.

Do not allow unrestricted east-west traffic.

────────────────────────────────────────

SECURITY GROUPS

Create dedicated security groups for:

• ALB/NLB
• EKS
• PostgreSQL
• Redis
• Kafka
• OpenSearch
• Bastion/management tooling where needed

Allow only required ports and sources.

Avoid 0.0.0.0/0 access to internal resources.

────────────────────────────────────────

VPC ENDPOINTS

Use private connectivity for AWS services where appropriate:

• S3
• ECR
• Secrets Manager
• KMS
• CloudWatch-related services
• STS where required
• Other required AWS APIs

Reduce public internet dependency for private workloads.

────────────────────────────────────────

EKS FOUNDATION

Create Amazon EKS architecture.

Support:

• Multi-AZ cluster
• Private worker networking
• Cluster logging
• IAM Roles for Service Accounts / EKS Pod Identity as appropriate
• Kubernetes RBAC
• NetworkPolicies
• Pod Security Standards
• Managed node groups

Prepare namespaces for:

• Applications
• Workers
• Media
• Observability
• Ingress
• Security
• Operations

────────────────────────────────────────

NODE GROUPS

Create workload-specific node pools:

GENERAL

• API services
• Web workloads

COMPUTE

• CPU-heavy services
• Dispatch
• Matching

MEMORY

• Memory-intensive workers

MEDIA

• Media processing if required

ANALYTICS

• Batch processing

OBSERVABILITY

• Monitoring/logging where justified

Define:

• Instance types
• Scaling bounds
• Labels
• Taints
• Tolerations
• Affinity
• Anti-affinity
• Topology spread

────────────────────────────────────────

KUBERNETES GOVERNANCE

Configure:

• ResourceQuota
• LimitRange
• Resource requests
• Resource limits
• PodDisruptionBudgets
• ServiceAccounts
• RBAC
• NetworkPolicies
• Pod Security

Prevent:

• Unbounded resource usage
• Privilege escalation
• Cross-namespace access
• Noisy-neighbor failures

────────────────────────────────────────

KUBERNETES INGRESS

Design ingress for:

• Public APIs
• Web application
• Driver APIs
• Rider APIs
• WebSocket gateways
• Administrative APIs

Support:

• TLS
• HTTP health checks
• WebSocket upgrade
• Timeouts
• Connection draining
• Rate limiting integration

────────────────────────────────────────

LOAD BALANCERS

Use appropriate AWS load-balancing resources.

Support:

• Application Load Balancer
• Network Load Balancer where real-time traffic requires it

Configure:

• TLS
• Health checks
• Idle timeouts
• Access logs
• Security controls

────────────────────────────────────────

POSTGRESQL

Create managed production PostgreSQL infrastructure.

Support:

• Multi-AZ
• Encryption
• TLS
• Automated backups
• PITR
• Parameter groups
• Monitoring
• Maintenance windows
• Read replicas where required
• Storage scaling

Database must remain private.

────────────────────────────────────────

POSTGRESQL OPERATIONAL CONFIGURATION

Prepare:

• Connection limits
• Parameter tuning
• Logging
• Slow query monitoring
• Backup retention
• Performance Insights where appropriate

Prepare external pooling such as PgBouncer if required by architecture.

────────────────────────────────────────

ELASTICACHE REDIS

Create production Redis infrastructure.

Support:

• Multi-AZ
• Replication
• Automatic failover
• Encryption at rest
• TLS
• Authentication
• Parameter groups
• Monitoring

Prepare workloads for:

• Location
• Availability
• Dispatch
• Matching
• Rate limiting
• Idempotency
• WebSocket coordination
• Caching

────────────────────────────────────────

KAFKA / REDPANDA

Create event infrastructure.

Support:

• Multi-broker deployment
• Multi-AZ placement
• Replication
• Persistent storage
• TLS
• Authentication
• Monitoring
• Topic lifecycle

Prepare for:

• Location events
• Dispatch events
• Trip events
• Financial events
• Notification events
• Fraud events
• Safety events
• Analytics events

────────────────────────────────────────

OPENSEARCH

Create production search infrastructure.

Support:

• Multi-node
• Multi-AZ
• Encryption
• Access policies
• Shards
• Replicas
• Snapshots
• Monitoring

Keep search rebuildable from authoritative data.

────────────────────────────────────────

S3

Create secure S3 architecture for:

• Driver documents
• Verification documents where required
• Receipts
• Reports
• Generated artifacts
• Analytics exports
• Other approved objects

Support:

• Versioning
• Encryption
• Lifecycle rules
• Bucket policies
• Block public access
• Access logging where needed
• Cross-region replication where appropriate

────────────────────────────────────────

CLOUDFRONT

Prepare CDN for:

• Web static assets
• Public assets
• Secure temporary content where approved

Configure:

• Origins
• Cache policies
• Origin access control
• TLS
• Compression
• WAF association

Do not expose private objects publicly.

────────────────────────────────────────

ROUTE 53

Support:

• Public application domain
• API domain
• Admin domain
• Regional routing
• Health checks
• Failover
• Weighted routing where appropriate

────────────────────────────────────────

ACM

Configure TLS certificates for:

• Web
• API
• Admin
• CDN
• Regional endpoints where appropriate

Automate renewal.

────────────────────────────────────────

WAF

Protect:

• Web
• Public APIs
• Admin endpoints
• Webhooks

Support:

• AWS managed rules
• Rate-based rules
• IP restrictions
• Request-size limits
• Bot controls where appropriate

Administrative APIs require stricter rules.

────────────────────────────────────────

IAM

Create least-privilege roles for:

• Terraform
• GitHub Actions
• EKS
• Application pods
• Workers
• Media processors
• Analytics workers
• Notification workers
• Backup jobs
• Observability

Prefer:

• OIDC
• EKS Pod Identity
• Short-lived credentials

────────────────────────────────────────

KMS

Create and manage KMS keys for:

• S3
• RDS
• Redis
• EBS
• Secrets
• Logs
• Backups
• Terraform state where applicable

Define:

• Key policy
• Rotation
• Access
• Environment isolation

────────────────────────────────────────

SECRETS

Use AWS Secrets Manager for:

• PostgreSQL credentials
• Redis credentials
• Kafka credentials
• Payment provider credentials
• Maps credentials
• Notification credentials
• OAuth secrets
• Webhook secrets
• External provider credentials

Integrate securely with Kubernetes.

Never place secrets in:

• Git
• Docker images
• Helm values committed to source
• Terraform variables with plaintext secrets

────────────────────────────────────────

DOCKER

Create production Docker standards for:

• API services
• Workers
• Web application
• Media workers

Use:

• Multi-stage builds
• Minimal runtime images
• Non-root user
• Read-only filesystem where possible
• Health checks
• Signal handling
• Dependency pinning

Images must be reproducible.

────────────────────────────────────────

ECR

Create ECR repositories for:

• API
• Web
• Workers
• Media workers
• Search workers
• Analytics workers
• Notification workers

Support:

• Image scanning
• Lifecycle rules
• Immutable tags where appropriate
• Access controls

────────────────────────────────────────

LOCAL DOCKER ENVIRONMENT

Create Docker Compose for local development.

Services:

• PostgreSQL
• PostGIS
• Redis
• Kafka/Redpanda
• OpenSearch
• S3-compatible object storage

Provide:

• Persistent development volumes
• Health checks
• Environment variables
• Safe local credentials
• Network configuration

Never use production secrets locally.

────────────────────────────────────────

OBSERVABILITY FOUNDATION

Create infrastructure for:

• OpenTelemetry Collector
• Prometheus
• Grafana
• Loki
• Tempo

Prepare:

• Cluster metrics
• Node metrics
• Pod metrics
• Application metrics
• Redis metrics
• PostgreSQL metrics
• Kafka metrics
• OpenSearch metrics
• Load-balancer metrics

────────────────────────────────────────

HEALTH CHECKS

Configure Kubernetes probes:

• Startup
• Readiness
• Liveness

Do not make liveness fail because an external dependency is temporarily unavailable.

Readiness should reflect whether the workload can safely receive traffic.

────────────────────────────────────────

AUTOSCALING FOUNDATION

Prepare:

• Horizontal Pod Autoscaler
• Cluster Autoscaler/Karpenter where approved
• Queue-based scaling
• Kafka-lag-based scaling

Scaling signals:

• CPU
• Memory
• Request rate
• Queue depth
• Consumer lag
• WebSocket connections
• Location throughput

────────────────────────────────────────

BACKUP FOUNDATION

Configure:

• RDS automated backups
• PITR
• S3 versioning
• S3 replication where required
• OpenSearch snapshots
• Terraform state protection
• Critical configuration backup

Support:

• Encryption
• Retention
• Monitoring

────────────────────────────────────────

DISASTER-RECOVERY FOUNDATION

Prepare for:

• AZ failure
• PostgreSQL failure
• Redis failure
• Kafka failure
• OpenSearch failure
• EKS failure
• Region failure

Define:

• Recovery dependencies
• Restoration order
• Backup sources
• Infrastructure reconstruction

────────────────────────────────────────

SECURITY BASELINE

Implement baseline controls for:

• IAM least privilege
• Encryption
• Private networking
• WAF
• Security groups
• NetworkPolicies
• Pod security
• Secrets management
• Container security
• Audit logging
• CloudTrail integration

────────────────────────────────────────

CLOUD AUDIT

Enable and centralize:

• CloudTrail
• EKS audit logs
• AWS Config where appropriate
• Security findings integration where appropriate

Keep logs protected from unauthorized modification.

────────────────────────────────────────

INFRASTRUCTURE TESTING

Validate:

• Terraform fmt
• Terraform validate
• Terraform plan
• Module tests
• Helm lint
• Kubernetes schema validation
• Docker builds
• Container scanning
• IAM policy validation
• Network policy validation
• Security group validation

────────────────────────────────────────

DOCUMENTATION

Generate:

• AWS architecture
• Account strategy
• Region strategy
• Environment strategy
• Terraform architecture
• VPC architecture
• Network segmentation
• IAM
• KMS
• EKS
• Kubernetes
• PostgreSQL
• Redis
• Kafka
• OpenSearch
• S3
• CloudFront
• Route 53
• ACM
• WAF
• Secrets
• Docker
• ECR
• Observability
• Backup
• Disaster recovery
• Local development
• Infrastructure testing

────────────────────────────────────────

PROJECT INDEX

Update the infrastructure Project Index with:

• AWS accounts
• Regions
• Environments
• VPCs
• Subnets
• Route tables
• NAT gateways
• VPC endpoints
• Security groups
• IAM roles
• OIDC
• KMS keys
• EKS clusters
• Node groups
• Namespaces
• Terraform modules
• Helm structure
• Dockerfiles
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
• Secrets Manager
• Observability
• Backups
• Disaster recovery
• Infrastructure tests
• Generated files
• Modified files
• Remaining work
• Current milestone
• Dependencies

────────────────────────────────────────

IMPLEMENTATION MILESTONES

INFRASTRUCTURE MILESTONE 1

Terraform foundation, remote state, providers, naming, tagging, reusable modules, environment structure, and global/regional separation.

INFRASTRUCTURE MILESTONE 2

AWS networking: VPC, subnets, routing, NAT, security groups, network ACLs, VPC endpoints, and network segmentation.

INFRASTRUCTURE MILESTONE 3

IAM, OIDC, EKS identity, KMS, Secrets Manager, ECR, CloudTrail, and security foundations.

INFRASTRUCTURE MILESTONE 4

EKS cluster, node groups, namespaces, RBAC, NetworkPolicies, Pod Security, resource governance, and load-balancer integration.

INFRASTRUCTURE MILESTONE 5

PostgreSQL/PostGIS, backups, monitoring, failover, connection-management foundation, and database security.

INFRASTRUCTURE MILESTONE 6

Redis, Kafka/Redpanda, OpenSearch, encryption, monitoring, persistence, and operational configuration.

INFRASTRUCTURE MILESTONE 7

S3, CloudFront, Route 53, ACM, WAF, secure object access, and edge networking.

INFRASTRUCTURE MILESTONE 8

Docker, Docker Compose, ECR, container hardening, health checks, and local-development infrastructure.

INFRASTRUCTURE MILESTONE 9

Observability foundation, OpenTelemetry Collector, Prometheus, Grafana, Loki, Tempo, metrics, logs, traces, and health checks.

INFRASTRUCTURE MILESTONE 10

Autoscaling foundation, backup validation, disaster-recovery foundation, infrastructure testing, documentation, security validation, and Project Index completion.

Each milestone should contain approximately 20–40 files where practical.

Every milestone must pass infrastructure validation before proceeding.

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

This volume covers infrastructure foundations:

• AWS
• Terraform
• Networking
• IAM
• OIDC
• KMS
• Secrets Manager
• EKS
• Kubernetes foundations
• PostgreSQL/PostGIS
• Redis
• Kafka/Redpanda
• OpenSearch
• S3
• CloudFront
• Route 53
• ACM
• WAF
• Docker
• ECR
• Local development
• Observability foundation
• Backup foundation
• Disaster-recovery foundation
• Infrastructure security
• Infrastructure testing

Do not implement:

• Backend business logic
• Frontend business logic
• Mobile business logic
• Dispatch logic
• Matching logic
• Pricing logic
• Payment logic
• Fraud logic
• Safety logic

Those already belong to the application layers.

────────────────────────────────────────

QUALITY BAR

Treat this infrastructure as the foundation of a globally distributed mobility platform.

Assume:

• Hundreds of millions of riders
• Millions of drivers
• Millions of active vehicles
• Massive GPS traffic
• Large WebSocket traffic
• High dispatch throughput
• High payment volume
• Large analytics workloads
• Multiple regions
• High availability
• Strict security requirements
• Strict privacy requirements
• Disaster recovery requirements

Prioritize:

• Security
• Availability
• Scalability
• Reliability
• Private networking
• Least privilege
• Observability
• Disaster recovery
• Cost awareness
• Automation
• Maintainability
• Production readiness
