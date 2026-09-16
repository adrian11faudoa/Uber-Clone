# UBER-STYLE RIDE-HAILING PLATFORM — INFRASTRUCTURE PROMPT — VOLUME 1

## ROLE

You are the senior infrastructure and platform engineering organization responsible for implementing the production cloud foundation for a globally scalable ride-hailing and mobility marketplace comparable in product depth and operational sophistication to Uber.

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
* Staff Mobile Engineer
* Technical Writer

You are implementing production infrastructure against the existing repository.

You are not creating a tutorial, infrastructure demonstration, toy Kubernetes cluster, or deployment checklist.

Implement complete, secure, reproducible, observable, scalable, and operationally realistic infrastructure that can run the existing backend, web applications, mobile build systems, asynchronous workers, realtime gateways, event consumers, databases, caches, and supporting services.

The repository is the source of truth for what currently exists.

Do not assume that another AI prompt or previous conversation is available.

---

# PROJECT

Implement the AWS-based production infrastructure foundation for the Uber-style ride-hailing platform.

The platform must support:

* web applications
* rider web
* operations/admin web
* rider mobile build/release pipelines
* driver mobile build/release pipelines
* NestJS backend services
* WebSocket gateways
* dispatch workers
* BullMQ workers
* Kafka consumers/producers
* PostgreSQL
* Redis
* OpenSearch/Elasticsearch where already established
* object storage
* CDN
* external provider integrations
* observability
* CI/CD
* secrets
* IAM
* WAF
* DNS
* TLS
* multiple environments
* horizontal scaling
* high availability
* disaster recovery foundations

Use:

* AWS
* Docker
* Kubernetes
* Helm
* Terraform
* GitHub Actions

where consistent with the repository.

Do not replace already-established repository infrastructure technology without a documented technical reason.

---

# SOURCE OF TRUTH

Before changing infrastructure:

Inspect:

* repository structure
* backend deployment configuration
* Dockerfiles
* Docker Compose/local infrastructure
* Kubernetes manifests
* Helm charts
* Terraform modules
* GitHub Actions workflows
* environment definitions
* secrets/configuration conventions
* frontend deployment
* mobile EAS/build configuration
* PostgreSQL configuration
* Redis configuration
* Kafka configuration
* search configuration
* S3/object-storage usage
* CDN configuration
* observability
* health endpoints
* readiness probes
* application resource expectations

Preserve compatible implementation.

Do not create parallel infrastructure that conflicts with existing deployment conventions.

Do not regenerate unchanged files.

Identify which infrastructure already exists and extend it.

---

# INFRASTRUCTURE SCOPE

This volume is responsible for:

* AWS account/environment structure
* Terraform foundation
* networking
* VPC
* subnets
* routing
* security groups
* IAM foundations
* Kubernetes cluster foundation
* node pools
* load balancing
* ingress
* TLS
* DNS
* WAF foundation
* container registry
* object storage foundation
* environment separation
* secret-management foundation
* baseline autoscaling
* availability zones
* baseline monitoring integration
* CI/CD foundation
* deployment conventions
* backend/web container deployment foundations
* production environment configuration
* infrastructure validation

This volume establishes the cloud platform on which later infrastructure work can build.

Do not implement advanced disaster-recovery execution, multi-region active-active architecture, complete observability dashboards, or exhaustive resilience testing unless required to establish the foundational infrastructure boundaries.

---

# ENVIRONMENTS

Support isolated environments for:

* local development
* test
* staging
* production

The infrastructure must prevent accidental cross-environment access.

Production must not share:

* database credentials
* Redis credentials
* Kafka credentials
* payment secrets
* signing keys
* storage buckets

with development or test environments.

---

# TERRAFORM ARCHITECTURE

Use modular Terraform.

Organize infrastructure around reusable concerns such as:

* network
* IAM
* ECR
* EKS
* load balancing
* DNS
* certificates
* WAF
* S3
* secrets
* observability integration
* environment configuration

The exact module structure must follow repository conventions.

Avoid one giant Terraform file containing the entire platform.

Avoid excessive module fragmentation that makes dependencies difficult to understand.

---

# TERRAFORM STATE

Implement secure remote Terraform state.

Requirements include:

* remote state storage
* state locking
* encryption
* restricted access
* environment isolation
* versioning where supported
* recovery considerations

Terraform state may contain sensitive resource metadata.

Never commit Terraform state files to source control.

---

# AWS ACCOUNT BOUNDARIES

Where the repository and organization structure permit, establish clear separation between environments/accounts.

At minimum prevent production resources from being accidentally provisioned with development configuration.

Use naming/tagging conventions that clearly identify:

* environment
* service
* region
* owner/team
* cost center/project
* data classification where useful

---

# AWS REGION STRATEGY

Choose a primary AWS region appropriate to the repository's deployment configuration.

The architecture must be region-aware so later regional expansion does not require rewriting Terraform modules.

Do not hardcode a single-region design into resource naming, application configuration, or assumptions that make future regional deployment impossible.

---

# NETWORK ARCHITECTURE

Implement a production VPC.

Include, as appropriate:

* public subnets
* private application subnets
* private data subnets
* controlled NAT/egress
* route tables
* internet gateway where required
* network ACLs where justified
* VPC endpoints where beneficial

Databases, Redis, Kafka, and internal services must not be publicly reachable.

---

# AVAILABILITY ZONES

Spread production-critical workloads across multiple availability zones.

At minimum evaluate:

* EKS worker capacity
* load balancers
* PostgreSQL
* Redis
* Kafka
* NAT/egress dependencies

Avoid single-AZ production bottlenecks.

---

# SUBNET DESIGN

Separate network responsibilities clearly.

Example categories:

* public ingress
* private application/compute
* private data
* optional dedicated integration subnet

Do not expose internal services directly to the public internet merely because they need outbound access.

---

# NAT AND EGRESS

Provide controlled outbound access for:

* container workloads
* package/provider integrations
* map providers
* payment providers
* notification providers

Evaluate NAT gateway topology and cost.

Where AWS VPC endpoints are appropriate, prefer private connectivity for AWS-managed services to reduce unnecessary public egress.

---

# NETWORK SECURITY GROUPS

Create least-privilege security groups.

Rules must explicitly define:

* source
* destination
* port
* protocol
* reason

Do not use broad:

* `0.0.0.0/0`
* all ports
* all protocols

rules for internal services.

---

# INTERNAL SERVICE NETWORKING

EKS workloads should communicate through controlled Kubernetes/AWS networking.

Databases and infrastructure services must accept connections only from authorized security groups/subnets/workloads.

Do not rely on obscurity of hostnames as a security mechanism.

---

# DNS

Implement Route 53 architecture for:

* web applications
* API
* realtime endpoint
* administrative application
* environment-specific domains

Use environment-safe naming.

Do not expose internal service hostnames publicly.

---

# TLS

Use AWS Certificate Manager or the repository's established certificate architecture.

TLS must protect:

* public web traffic
* APIs
* WebSockets
* administrative interfaces

Certificates must:

* renew automatically
* be monitored
* use strong defaults
* avoid hardcoded private keys

---

# LOAD BALANCING

Deploy appropriate load balancing for:

* web applications
* HTTP APIs
* WebSockets

Ensure long-lived WebSocket connections are compatible with the chosen load-balancing architecture.

Define:

* health checks
* idle timeout
* connection behavior
* TLS termination
* ingress rules
* security groups

Do not use arbitrary default timeouts for active-trip realtime workloads without validating their suitability.

---

# WEB APPLICATION DELIVERY

For Next.js applications, use the repository's selected deployment model.

If containerized:

* build production images
* use non-root containers where practical
* expose health endpoints where appropriate
* configure resource requests/limits
* deploy behind the appropriate load balancer/CDN

If a managed AWS hosting service is already established, preserve that architecture instead of duplicating web hosting inside Kubernetes.

---

# CONTAINER REGISTRY

Use Amazon ECR or repository-established equivalent.

Implement:

* repository naming
* image tagging
* lifecycle policies
* vulnerability scanning where available
* immutable release references where practical
* access control

Do not use mutable `latest` as the only production deployment identifier.

---

# DOCKER SECURITY

Production containers must:

* use minimal appropriate base images
* run as non-root where feasible
* avoid unnecessary packages
* have predictable entrypoints
* receive configuration at runtime
* contain no credentials
* use health checks where useful

Pin base-image strategy appropriately.

Do not bake environment secrets into images.

---

# KUBERNETES FOUNDATION

Implement the EKS foundation.

Support workloads such as:

* API
* WebSocket gateway
* dispatch workers
* BullMQ workers
* Kafka consumers
* notification workers
* scheduled jobs
* administrative backend components where applicable

Use production namespaces and conventions.

---

# KUBERNETES NAMESPACES

Separate workloads logically.

At minimum distinguish:

* application
* workers
* observability/system workloads

Use labels and annotations consistently.

Do not place every workload into one undifferentiated namespace when operational boundaries require separation.

---

# NODE POOLS

Define node groups appropriate to:

* general API workloads
* compute/background workloads
* high-throughput or specialized workers where justified

Do not create unnecessary node pools.

Resource profiles should reflect workload characteristics.

---

# RESOURCE REQUESTS AND LIMITS

Every production Kubernetes workload must define appropriate:

* CPU requests
* memory requests
* CPU limits where justified
* memory limits

Do not assign arbitrary identical resources to every deployment.

Worker workloads and API workloads have different resource patterns.

---

# POD DISRUPTION

Use:

* PodDisruptionBudgets
* topology spreading
* anti-affinity where justified

to maintain service availability during:

* node replacement
* cluster maintenance
* rolling deployment

Do not configure disruption policies that prevent routine cluster maintenance entirely.

---

# HEALTH PROBES

Use:

* startup probes
* readiness probes
* liveness probes

where appropriate.

Readiness must represent actual ability to receive traffic.

Do not use liveness probes that restart healthy but temporarily busy workers.

---

# GRACEFUL TERMINATION

Configure Kubernetes termination behavior to match application graceful shutdown.

Allow:

* request drain
* WebSocket disconnect handling
* queue-worker shutdown
* Kafka consumer shutdown
* database connection closure

Do not terminate active workers before giving them sufficient opportunity to stop safely.

---

# HORIZONTAL AUTOSCALING

Implement HPA for appropriate workloads.

Consider:

* CPU
* memory
* request rate
* queue depth
* worker backlog
* Kafka consumer lag

Do not autoscale every workload solely on CPU.

Location, dispatch, API, and asynchronous workers require workload-specific signals.

---

# CLUSTER AUTOSCALING

Provide node scaling appropriate to workload demands.

Prevent:

* unschedulable production pods
* runaway scale-out
* insufficient capacity during deployment

Use defined resource classes.

---

# APPLICATION CONFIGURATION

Separate:

* secrets
* runtime configuration
* environment configuration

Use:

* Kubernetes ConfigMaps for non-sensitive configuration
* AWS Secrets Manager/SSM or another approved secret system for sensitive values

Do not commit production secrets to Helm values or Kubernetes manifests.

---

# SECRET MANAGEMENT

Integrate Kubernetes workloads with AWS-managed secrets.

Support secure access to:

* database credentials
* Redis credentials
* Kafka credentials
* JWT/signing secrets
* payment provider secrets
* map provider secrets
* notification provider secrets
* webhook secrets
* encryption keys

Use least privilege.

Do not grant every workload access to every secret.

---

# IAM

Implement least-privilege IAM.

Use workload-specific identities where possible.

Separate permissions for:

* API
* workers
* notification workers
* storage access
* deployment system
* operations

Do not attach broad administrator permissions to production application workloads.

---

# SERVICE ACCOUNT SECURITY

Use Kubernetes service accounts tied to appropriate AWS identities where the selected architecture supports it.

Applications should receive only required AWS permissions.

Examples:

* receipt worker → S3 write
* compliance service → restricted object storage access
* application → read selected secrets
* deployment agent → deployment permissions

Do not use one universal AWS role for all pods.

---

# OBJECT STORAGE

Create secure S3 foundations for:

* compliance evidence
* receipts
* support attachments
* export files
* other private artifacts

Buckets must be private by default.

Enable:

* encryption
* versioning where useful
* lifecycle policies
* access logging/monitoring where appropriate
* controlled IAM access

---

# S3 ACCESS

Applications should use:

* pre-signed upload
* pre-signed download
* IAM-backed service access

as appropriate.

Do not make private compliance or support objects publicly readable.

---

# S3 LIFECYCLE

Define lifecycle rules where appropriate for:

* temporary uploads
* expired exports
* transient processing artifacts
* old derived objects

Do not delete records that are required for compliance or financial retention.

---

# CDN

Use CloudFront or repository-established CDN architecture for appropriate web/static/media workloads.

Configure:

* TLS
* origins
* caching
* invalidation strategy
* compression
* access control where needed

Private objects must not become publicly cacheable.

---

# WAF

Implement AWS WAF protection for public entry points.

Protect against:

* common web attacks
* request flooding
* abusive patterns
* known malicious traffic

Tune rules to avoid breaking:

* APIs
* WebSockets
* legitimate ride traffic

Do not rely exclusively on WAF for application authorization.

---

# API EDGE SECURITY

Public API entry should have:

* TLS
* WAF where appropriate
* rate-limit integration
* request-size limits
* access logs
* health checks

Application-level authorization remains mandatory.

---

# WEBSOCKET INFRASTRUCTURE

Ensure Kubernetes/load-balancer configuration supports production WebSockets.

Validate:

* connection timeout
* idle timeout
* keepalive
* connection draining
* horizontal scaling
* client reconnect behavior

WebSocket gateways must not become single-node infrastructure.

---

# KAFKA INFRASTRUCTURE FOUNDATION

If Kafka/Redpanda is managed inside AWS infrastructure, implement the foundational connectivity and security model.

Support:

* private networking
* authentication
* encryption
* topic configuration
* security groups
* monitoring hooks

If the repository already uses a managed Kafka provider, integrate with that rather than provisioning a duplicate cluster.

---

# REDIS INFRASTRUCTURE FOUNDATION

Use a production-compatible Redis service such as ElastiCache where appropriate.

Support:

* subnet groups
* private networking
* encryption
* authentication
* high availability
* failover configuration
* monitoring

Redis infrastructure must not be publicly accessible.

---

# POSTGRESQL INFRASTRUCTURE FOUNDATION

Use managed PostgreSQL such as Amazon RDS/Aurora where appropriate.

Support:

* multi-AZ
* encryption
* backup configuration
* maintenance windows
* parameter configuration
* monitoring
* private networking
* connection security

Do not expose the database directly to the internet.

---

# DATABASE ACCESS

Only authorized application workloads may access PostgreSQL.

Separate:

* application connectivity
* migration access
* administrative access

Do not grant every Kubernetes pod direct database credentials.

---

# DATABASE BACKUPS

Enable production-appropriate:

* automated backups
* point-in-time recovery
* backup retention
* encryption
* monitoring

Actual recovery testing belongs to the appropriate later resilience/DR scope but the foundation must support it.

---

# DATABASE PARAMETERIZATION

Configure PostgreSQL parameters only when justified by:

* workload
* connection profile
* query behavior
* operational requirements

Do not copy arbitrary tuning values without validating them.

---

# CONNECTION POOLING

Infrastructure must account for connections from:

* API replicas
* workers
* Kafka consumers
* admin workloads
* migration processes

Avoid cluster autoscaling creating more database connections than the database can safely sustain.

---

# ECR/GITHUB ACTIONS TRUST

CI/CD should use short-lived AWS authentication such as GitHub Actions OIDC where appropriate.

Do not store long-lived AWS access keys in GitHub repository secrets when OIDC can provide safer federation.

---

# CI/CD FOUNDATION

Implement GitHub Actions workflows for:

* lint
* test
* type check
* build
* security scans where appropriate
* container build
* image scan
* artifact publication
* infrastructure validation
* deployment promotion

Separate:

* pull-request validation
* staging deployment
* production deployment

---

# CI SECURITY

CI workflows must use:

* least-privilege permissions
* pinned/reviewed actions
* secret isolation
* environment protection
* OIDC
* artifact integrity controls

Do not give every workflow production deployment access.

---

# ENVIRONMENT PROMOTION

Promotion should follow:

1. Build.
2. Validate.
3. Test.
4. Publish immutable artifact.
5. Deploy to test/staging.
6. Run smoke validation.
7. Require appropriate production authorization.
8. Deploy production.
9. Verify health.

Do not rebuild different artifacts for every environment if doing so could produce untraceable differences.

---

# IMAGE VERSIONING

Production deployments should identify images by immutable:

* digest
* commit SHA
* release identifier

Do not rely only on mutable tags.

---

# HELM

Use Helm for Kubernetes application packaging where appropriate.

Define:

* values
* environments
* resources
* secrets/config references
* ingress
* autoscaling
* service accounts
* probes
* disruption policies

Avoid duplicating entire manifests for every environment.

---

# HELM SECURITY

Do not place production secret values directly into Helm values.

Ensure templates cannot accidentally render secrets into logs or public ConfigMaps.

Validate rendered manifests in CI.

---

# TERRAFORM/HELM DEPENDENCY MANAGEMENT

Define clean boundaries:

Terraform owns infrastructure.

Helm/Kubernetes owns application deployment.

CI/CD coordinates the sequence.

Do not have Terraform and Helm simultaneously manage the same Kubernetes application resources without an explicit reason.

---

# ENVIRONMENT CONFIGURATION

Use separate configuration for:

* local
* test
* staging
* production

Configuration should define:

* environment name
* AWS region
* API endpoints
* WebSocket endpoints
* storage locations
* observability configuration
* provider references

Secrets remain in secure secret stores.

---

# RESOURCE TAGGING

Apply consistent AWS tags to all supported resources:

* project
* environment
* service
* owner
* cost-center
* managed-by
* data-classification where useful

Tagging must support cost and operational analysis.

---

# COST CONTROLS

Infrastructure must be commercially realistic.

Consider:

* NAT gateway costs
* EKS node costs
* load balancers
* storage
* CloudWatch ingestion
* Kafka
* Redis
* PostgreSQL
* data transfer
* CDN

Do not optimize cost by weakening:

* security
* availability
* backups
* observability

---

# CAPACITY BASELINES

Define initial production capacity assumptions for:

* API replicas
* WebSocket replicas
* worker replicas
* node pools
* database capacity
* Redis capacity
* event capacity
* storage

The baseline must be adjustable through infrastructure configuration.

Do not hardcode assumptions that prevent scaling.

---

# SECURITY BASELINE

Infrastructure must enforce:

* encryption in transit
* encryption at rest
* least privilege
* private data services
* secrets management
* restricted admin access
* audit logging
* vulnerability scanning
* controlled ingress/egress

---

# LOGGING

Enable centralized infrastructure/application log collection appropriate to the repository.

Ensure logs support:

* service
* environment
* pod/workload
* request/correlation ID
* severity
* timestamp

Do not collect sensitive data indiscriminately.

---

# CLOUDWATCH / OBSERVABILITY INTEGRATION

Integrate AWS/Kubernetes infrastructure with the repository's observability architecture.

Capture relevant:

* load balancer metrics
* EKS health
* node metrics
* PostgreSQL health
* Redis health
* storage metrics
* network errors
* deployment events

The complete dashboards/alert design may belong to later infrastructure scope, but this foundation must expose the required telemetry.

---

# HEALTH INTEGRATION

Infrastructure health checks must map correctly to application:

* liveness
* readiness
* startup

Do not route traffic to pods that cannot safely serve requests.

---

# DEPLOYMENT SAFETY

Production rollouts must account for:

* database migrations
* API compatibility
* event-schema compatibility
* worker compatibility
* WebSocket compatibility
* rolling deployment
* health validation
* rollback

Do not allow deployment sequencing to break existing clients.

---

# DATABASE MIGRATION DEPLOYMENT

Migrations must be separated from application startup when required for production safety.

Use a controlled migration mechanism.

Do not allow multiple replicas to race on schema migration.

Do not perform destructive migrations without expand-and-contract compatibility.

---

# ROLLING DEPLOYMENTS

Configure Kubernetes deployments to avoid:

* all replicas restarting simultaneously
* insufficient capacity during rollout
* routing to unready pods
* event consumers duplicating unsafe work

Use:

* readiness probes
* max surge
* max unavailable
* graceful termination

appropriate to each workload.

---

# WORKER DEPLOYMENT

Workers require different rollout behavior from APIs.

Ensure:

* graceful job completion/termination
* Kafka consumer shutdown
* retry-safe job handling
* no abrupt loss of active processing

Do not treat all worker workloads like stateless HTTP deployments.

---

# MOBILE BUILD INFRASTRUCTURE

Where the repository uses Expo/EAS, configure CI/CD foundations for:

* rider iOS builds
* rider Android builds
* driver iOS builds
* driver Android builds

Support:

* environment-specific configuration
* signing integration
* build profiles
* release artifacts
* protected production credentials

Do not commit signing credentials to source control.

---

# SECRET ROTATION FOUNDATION

Infrastructure must support rotation of:

* database credentials
* Redis credentials
* provider secrets
* webhook secrets
* signing keys
* API keys

Application deployments must tolerate controlled secret rotation.

Do not require source-code changes to rotate a secret.

---

# BACKEND ENVIRONMENT INJECTION

Applications must receive runtime configuration securely.

Do not bake:

* database URLs
* signing secrets
* payment secrets
* provider API keys

into Docker images.

---

# INFRASTRUCTURE VALIDATION

CI must validate:

* Terraform formatting
* Terraform syntax
* Terraform plan
* Helm template rendering
* Kubernetes manifest validation
* Docker builds
* image scanning
* policy checks where configured

Production deployment must not occur from an unvalidated infrastructure change.

---

# POLICY VALIDATION

Where repository tooling permits, enforce policies such as:

* public S3 bucket denial
* public database denial
* unrestricted security groups denied
* unencrypted storage denied
* privileged service accounts denied
* missing resource limits denied

Do not introduce policy checks that make legitimate deployment impossible without documenting exceptions.

---

# BACKUP AND RECOVERY FOUNDATIONS

Configure:

* database backups
* object-storage versioning where appropriate
* infrastructure state backup
* secret recovery strategy
* registry artifact retention

Disaster-recovery execution and full failover testing belong to the appropriate later scope, but this infrastructure must make recovery possible.

---

# INFRASTRUCTURE TESTING

Test:

* Terraform plan
* Terraform validation
* Helm rendering
* Kubernetes manifests
* Docker images
* health checks
* network connectivity
* secret injection
* IAM permissions
* TLS
* DNS
* load balancing

Use isolated test/staging resources where appropriate.

---

# SECURITY TESTING

Validate:

* public exposure
* security groups
* IAM policies
* S3 access
* secret access
* TLS
* WAF
* Kubernetes RBAC
* pod security
* image vulnerabilities
* CI permissions

Do not skip security validation because the infrastructure is internal.

---

# PERFORMANCE AND CAPACITY TESTING

At this stage validate basic infrastructure capacity and deployment behavior.

Measure where practical:

* pod startup
* API scaling
* WebSocket scaling
* worker startup
* database connection behavior
* Redis connectivity
* load-balancer behavior

Full production load/stress testing belongs to later infrastructure work but this foundation must support it.

---

# DOCUMENTATION

Update infrastructure documentation for:

* AWS environment structure
* Terraform
* Kubernetes
* Helm
* networking
* secrets
* IAM
* ECR
* PostgreSQL
* Redis
* Kafka
* S3
* CDN
* WAF
* DNS
* TLS
* CI/CD
* mobile build infrastructure
* environment variables
* operational access

Documentation must describe actual infrastructure.

---

# IMPLEMENTATION DISCIPLINE

Before modifying files:

1. Inspect the repository.
2. Identify existing infrastructure.
3. Preserve compatible architecture.
4. Establish Terraform foundation.
5. Establish network.
6. Establish IAM/security boundaries.
7. Establish ECR.
8. Establish EKS/Kubernetes foundation.
9. Establish load balancing/ingress.
10. Establish DNS/TLS.
11. Establish WAF.
12. Establish database/cache/event connectivity.
13. Establish object storage.
14. Establish secrets.
15. Establish CI/CD.
16. Establish application deployment foundations.
17. Establish mobile build infrastructure.
18. Add infrastructure validation.
19. Add security validation.
20. Add documentation.
21. Validate staging deployment.
22. Produce the required completion report.

Do not rewrite unrelated application code.

---

# PRODUCTION COMPLETENESS

Never leave:

* open security groups
* public databases
* public private-storage buckets
* hardcoded production secrets
* unprotected state files
* mutable production-only image references
* unvalidated Helm charts
* unvalidated Terraform
* missing health probes
* uncontrolled service accounts
* unrestricted CI credentials
* placeholder infrastructure resources
* TODO/FIXME infrastructure gaps
* pseudo-code

Infrastructure is not complete merely because Terraform can create resources.

The deployed system must be able to operate securely and predictably.

---

# PROHIBITED PRACTICES

Never:

* commit AWS credentials
* commit Terraform state
* expose PostgreSQL publicly
* expose Redis publicly
* expose Kafka publicly without deliberate secure architecture
* use `0.0.0.0/0` for internal database/Redis ingress
* use universal administrator IAM roles for application workloads
* bake secrets into Docker images
* store production secrets in Git
* use mutable `latest` as the sole production deployment identifier
* deploy without health checks
* run database migrations independently from deployment safety requirements
* terminate workers without graceful shutdown
* allow unrestricted CI production access
* create duplicate infrastructure stacks for the same service

---

# IMPLEMENTATION BOUNDARIES

This volume establishes the AWS/Kubernetes/Terraform/CI foundation.

Later infrastructure work must extend these foundations for:

* comprehensive observability
* advanced autoscaling
* multi-region
* disaster recovery
* backup/restore testing
* resilience engineering
* production load testing
* advanced security/compliance
* operational runbooks

Do not create duplicate VPCs, clusters, registries, or environment systems merely because later infrastructure requirements exist.

---

# REQUIRED IMPLEMENTATION DELIVERABLES

Implement or update:

## TERRAFORM

* state backend
* provider configuration
* modules
* environments
* tagging
* validation

## NETWORKING

* VPC
* subnets
* routing
* NAT/egress
* security groups
* private connectivity

## SECURITY

* IAM
* service identities
* secrets integration
* TLS
* WAF
* network controls

## COMPUTE

* EKS
* node pools
* namespaces
* workload foundations
* autoscaling basics
* probes
* disruption policies

## APPLICATION DELIVERY

* ECR
* Docker
* Helm
* ingress
* load balancing
* DNS

## DATA

* PostgreSQL connectivity
* Redis connectivity
* Kafka connectivity
* S3

## CI/CD

* GitHub Actions
* OIDC
* build
* test
* scan
* publish
* deploy

## MOBILE

* EAS build/release foundations
* environment configuration
* protected signing integration

## VALIDATION

* Terraform
* Helm
* Kubernetes
* Docker
* security
* deployment

---

# REQUIRED INFRASTRUCTURE CONTRACTS

Establish stable deployment contracts for:

* API
* WebSocket gateway
* dispatch worker
* BullMQ workers
* Kafka consumers
* web applications
* migration jobs
* scheduled jobs

Each workload must define:

* image
* port if applicable
* health probes
* resource profile
* environment/configuration
* secret requirements
* IAM requirements
* scaling behavior
* deployment strategy

---

# REQUIRED NETWORK CONTRACTS

Document and implement intended communication paths among:

* internet → load balancer
* load balancer → web/API
* API → PostgreSQL
* API → Redis
* API → Kafka
* workers → PostgreSQL
* workers → Redis
* workers → Kafka
* workloads → S3
* workloads → external providers

No communication path should depend on undocumented firewall exceptions.

---

# REQUIRED ENVIRONMENT VALIDATION

For staging, verify:

* DNS
* TLS
* ingress
* API
* WebSocket
* database
* Redis
* Kafka
* S3
* secrets
* CI/CD deployment
* health checks

Do not claim successful deployment if any required dependency was not validated.

---

# COMPLETION REPORT REQUIREMENTS

When implementation is complete, report:

## FILES CREATED

List every new infrastructure file.

## FILES MODIFIED

List every modified infrastructure/application deployment file.

## TERRAFORM

Report:

* modules
* state
* environments
* providers
* validation

## NETWORKING

Report:

* VPC
* subnets
* routes
* NAT
* security groups
* private connectivity

## KUBERNETES

Report:

* EKS
* node pools
* namespaces
* deployments
* services
* ingress
* probes
* autoscaling
* disruption policies

## SECURITY

Report:

* IAM
* workload identities
* secrets
* TLS
* WAF
* security groups
* encryption

## DATA SERVICES

Report:

* PostgreSQL
* Redis
* Kafka
* S3
* CDN

## CI/CD

Report:

* GitHub Actions
* OIDC
* image build
* scanning
* registry
* staging deployment
* production promotion controls

## MOBILE

Report:

* EAS/build profiles
* signing integration
* environment configuration

## VALIDATION

Report:

* Terraform validation
* Terraform plan
* Helm rendering
* Kubernetes validation
* Docker builds
* security scans
* deployment tests
* runtime health verification

## COMPATIBILITY

Identify:

* application deployment compatibility
* database migration implications
* WebSocket implications
* mobile build implications
* environment changes

## UNRESOLVED ISSUES

List only genuine remaining infrastructure issues.

Do not claim infrastructure foundation completion if critical networking, identity, secret, deployment, or connectivity requirements remain incomplete or unverified.

---

# FINAL ENGINEERING PRINCIPLE

The infrastructure must become a secure and reproducible platform for the complete ride-hailing system.

Infrastructure must provide:

* private-by-default networking
* least-privilege identity
* secure secret delivery
* highly available compute
* controlled deployment
* scalable workloads
* reliable data connectivity
* secure object storage
* production TLS
* protected public entry points
* reproducible infrastructure
* traceable releases
* safe environment separation

Terraform is the authoritative infrastructure definition.

Kubernetes/Helm is the authoritative application deployment definition.

GitHub Actions is the controlled delivery mechanism.

AWS managed services are used where they improve reliability and reduce unnecessary operational burden.

The repository remains the implementation source of truth.

All subsequent infrastructure work must extend these foundations without creating duplicate environments, competing deployment systems, or conflicting infrastructure ownership.
