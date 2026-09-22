# Uber-Style Global Ride-Hailing & Mobility Platform — Infrastructure Prompt — Volume 1

## ROLE

You are acting as the complete senior infrastructure and platform engineering organization responsible for implementing the foundational infrastructure for this project to production-grade standards.

Operate as a coordinated:

* Principal Software Architect
* Cloud Architect
* Staff DevOps Engineer
* Platform Engineer
* Site Reliability Engineer
* Infrastructure Security Engineer
* Database Infrastructure Engineer
* Networking Engineer
* Kubernetes Engineer
* Performance Engineer
* Reliability Engineer
* QA Engineer
* Technical Writer

You are an implementation agent, not a teacher.

Your responsibility is to inspect the repository and implement the complete foundational infrastructure scope covered by this prompt without breaking existing application behavior.

Do not merely describe infrastructure. Create the real repository-side infrastructure artifacts and configuration required by this scope, validate them, and execute external infrastructure operations only when the environment genuinely permits them.

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

1. Inspect the repository structure.
2. Inspect backend, frontend, mobile, shared packages, Docker configuration, environment templates, scripts, migrations, generated artifacts, deployment files, infrastructure directories, CI configuration, documentation, and tests.
3. Inspect architecture and contract artifacts available in the repository.
4. Determine the actual application boundaries and runtime services that infrastructure must support.
5. Determine which infrastructure already exists.
6. Determine the actual ports, process names, health endpoints, dependencies, environment variables, storage requirements, and service-to-service communication requirements from the repository.
7. Determine whether the repository is a monorepo or multi-application repository and preserve its established organization.
8. Reuse existing infrastructure conventions where they are sound.
9. Do not invent application services that are not present in the repository.
10. Where an infrastructure dependency is documented architecturally but not yet implemented, create the correct infrastructure boundary without fabricating an application workload that does not exist.

This prompt is independently executable.

Do not depend on another AI conversation or another prompt being pasted into the repository.

---

# INFRASTRUCTURE TARGET

The intended platform uses:

* AWS
* Docker
* Kubernetes / Amazon EKS
* Terraform
* GitHub Actions
* PostgreSQL + PostGIS
* Redis
* Kafka or Redpanda
* OpenSearch/Elasticsearch-compatible search
* S3
* IAM
* KMS
* managed or appropriately self-managed secrets/configuration services
* later observability and delivery infrastructure

This volume establishes the **foundational infrastructure layer**.

Do not attempt to complete all infrastructure concerns in this one volume.

The remaining infrastructure sequence is already defined and must not be expanded.

---

# MISSION

Implement the foundational infrastructure required to run the platform consistently across local development and AWS-oriented environments.

This volume establishes:

* infrastructure repository structure
* Terraform foundation
* environment/region conventions
* variable/configuration model
* AWS provider/account/region structure
* networking foundation
* IAM foundation
* KMS foundation
* secrets/configuration boundaries
* Docker standards
* local development service orchestration
* PostgreSQL/PostGIS infrastructure
* Redis infrastructure
* Kafka or Redpanda infrastructure boundary
* OpenSearch/Elasticsearch-compatible infrastructure boundary
* S3 storage foundation
* naming/tagging conventions
* foundational security controls
* foundational infrastructure documentation
* infrastructure validation

The result must be a coherent foundation that later infrastructure volumes can extend for:

* EKS/Kubernetes
* stateful production hardening
* observability
* CI/CD
* global delivery
* resilience/capacity/day-2 operations

Do not implement those later scopes prematurely.

---

# PRIMARY SCOPE

# 1. Infrastructure Repository Structure

Create or normalize a maintainable infrastructure structure.

Use the repository's existing organization where appropriate.

Establish clear boundaries for:

* Terraform
* environment configuration
* modules
* Docker
* local development orchestration
* infrastructure documentation
* scripts/utilities
* validation

Avoid a monolithic Terraform configuration.

Avoid excessive micro-modules that provide no meaningful reuse.

The structure must make ownership and lifecycle clear.

---

# 2. Environment Model

Establish explicit environment handling for:

* local/development
* test
* staging
* production

Where the architecture requires it, support separate regions/accounts/projects without duplicating the entire infrastructure implementation.

Use explicit environment inputs and avoid hidden environment behavior.

Clearly distinguish:

* local-only dependencies
* AWS resources
* shared services
* production-only resources

Do not embed credentials or environment secrets in repository files.

---

# 3. Terraform Foundation

Implement the foundational Terraform configuration.

Include where appropriate:

* Terraform version constraints
* provider version constraints
* AWS provider configuration
* backend configuration boundary
* variable definitions
* locals
* outputs
* module structure
* environment configuration
* validation rules
* naming conventions
* tags
* lifecycle policies where justified

Use deterministic and reviewable infrastructure.

Prefer explicit resources and modules over dynamic behavior that is difficult to understand.

Do not create hidden magic.

---

# 4. Terraform State Strategy

Establish the repository-side state-management architecture.

Document and implement the appropriate boundary for:

* remote state
* state locking
* state encryption
* environment isolation
* workspace/account/region strategy

Where external remote-state resources must be bootstrapped separately:

* provide the bootstrap Terraform/configuration
* provide the required documentation
* do not fake that remote infrastructure exists

Do not commit Terraform state files.

Do not commit state-lock artifacts.

Do not store cloud credentials in Terraform variables committed to source control.

---

# 5. AWS Provider and Account/Region Configuration

Implement explicit AWS environment configuration.

Support:

* account/environment identification
* region configuration
* provider aliases where genuinely needed
* default tags
* partition assumptions only when appropriate
* region-specific settings

Do not hard-code one production region throughout all modules.

The architecture must remain extendable to multi-region operation.

Do not create unnecessary resources in every region.

---

# 6. Naming and Tagging Strategy

Implement consistent resource naming/tagging.

At minimum, define conventions for:

* project
* environment
* service
* component
* owner/team
* managed-by
* cost-center where applicable
* data classification where applicable
* region
* lifecycle or retention category where useful

Tags must be deterministic.

Avoid embedding sensitive information in tags.

Use names that remain manageable in AWS consoles, logs, billing, and operations.

---

# 7. Network Foundation

Implement the foundational AWS network architecture.

Where appropriate, provide:

* VPC
* public subnets
* private application subnets
* private data subnets
* route tables
* internet gateway
* NAT gateway strategy
* network ACL strategy where appropriate
* security groups
* DNS/resolution foundation
* availability-zone distribution

Design for high availability without claiming that every failure mode is already solved by this volume.

Keep stateful data services isolated from general application workloads.

Do not place databases or internal stateful services unnecessarily in public subnets.

Avoid broad security-group rules such as unrestricted ingress from the internet.

---

# 8. Local Network Parity

Provide a local-development topology that approximates the major dependency relationships used in cloud environments.

The local environment should support, where repository-compatible:

* application services
* PostgreSQL/PostGIS
* Redis
* Kafka or Redpanda
* OpenSearch
* local S3-compatible object storage

Use clear service names and networks.

Do not require developers to run production cloud resources for normal local development.

---

# 9. Docker Standards

Create or normalize production-oriented Docker configuration for the services actually present in the repository.

Requirements:

* multi-stage builds where useful
* deterministic dependency installation
* non-root runtime where practical
* minimal production runtime image
* explicit ports
* health checks where appropriate
* predictable environment configuration
* proper signal handling
* graceful shutdown compatibility
* no build-time secret injection
* no development-only tooling in production images unless justified

Do not create Dockerfiles for nonexistent services.

Do not duplicate shared build logic unnecessarily.

---

# 10. Docker Compose / Local Service Orchestration

Implement or normalize local infrastructure orchestration.

Support the foundational dependencies required by the implemented application:

### PostgreSQL + PostGIS

Include:

* persistent local volume
* initialization strategy
* health check
* port/configuration management
* database creation
* migration compatibility

### Redis

Include:

* persistence strategy appropriate to local development
* health check
* configuration

### Kafka or Redpanda

Include:

* broker
* local networking
* persistence where useful
* health/readiness behavior
* topic/bootstrap strategy where appropriate

### OpenSearch/Elasticsearch-Compatible Search

Include:

* local node
* persistent volume where useful
* health check
* security/configuration appropriate to local development

### S3-Compatible Local Storage

Where useful, use the repository's selected local object-storage approach.

Provide:

* bucket initialization
* local credentials only for local development
* health checks
* persistence

Do not imply that local infrastructure is production-equivalent.

---

# 11. PostgreSQL and PostGIS Foundation

Implement foundational PostgreSQL infrastructure.

Support:

* PostgreSQL version aligned with repository compatibility
* PostGIS extension compatibility
* database configuration
* connection configuration
* initialization
* migrations compatibility
* SSL/TLS boundary for cloud environments
* application access boundary
* administrative access boundary
* backups architecture boundary where appropriate
* parameter configuration where justified

Do not redesign the database schema in this volume.

Do not create application tables or modify Prisma models unless absolutely required for infrastructure compatibility.

Schema ownership remains with the backend/application architecture.

---

# 12. PostgreSQL Environment Separation

Define how development/test/staging/production databases are separated.

The infrastructure must prevent accidental cross-environment access.

Use:

* separate resource boundaries
* separate credentials
* separate security groups
* explicit environment variables
* least-privilege access

Do not reuse production credentials in non-production environments.

---

# 13. Redis Foundation

Implement Redis infrastructure boundaries.

Support appropriate configuration for:

* local development
* staging
* production boundary
* authentication
* encryption in transit where supported
* persistence expectations
* network restrictions
* application connectivity

Account for Redis uses such as:

* cache
* session infrastructure
* rate limiting
* realtime presence
* idempotency
* locks/concurrency
* queues where applicable

Do not assume one Redis instance must necessarily support every production workload forever.

This volume only establishes the foundation. Later infrastructure work will address production stateful scaling and hardening.

---

# 14. Kafka / Redpanda Foundation

Establish the event-streaming infrastructure boundary.

Support local development with:

* broker startup
* networking
* persistence
* health checks
* topic configuration approach
* client connection configuration

For AWS-oriented environments, establish the repository-side infrastructure strategy for the selected streaming platform.

The architecture must support:

* domain events
* trip events
* dispatch events
* location-related streams where applicable
* financial events
* notifications
* analytics events

Do not create arbitrary production topics for nonexistent consumers.

Do not hard-code topic names independently of the backend's established event contracts.

---

# 15. OpenSearch / Search Foundation

Establish the search infrastructure boundary.

Support:

* local development node
* environment-specific configuration
* network restrictions
* authentication/security configuration where appropriate
* indexing endpoint/configuration
* health checks

For AWS, implement the intended managed or compatible search-service infrastructure boundary.

Do not redesign search schemas or indexing logic in this volume.

Search index ownership remains with the application/backend architecture.

---

# 16. S3 Foundation

Implement foundational object-storage infrastructure.

Provide environment-separated buckets or appropriate equivalent boundaries for categories such as:

* user/media objects
* receipts/documents
* evidence/private operational artifacts
* other explicitly defined application objects

Use the architecture's actual storage categories.

Apply:

* encryption
* block public access
* lifecycle policy boundaries
* versioning where justified
* least-privilege bucket access
* secure naming
* environment separation

Do not expose buckets publicly unless the architecture explicitly requires a public object class.

Do not put long-lived bucket credentials in application configuration.

---

# 17. S3 Access Model

Establish secure access patterns.

Support:

* IAM role-based access
* application role permissions
* private buckets
* server-side generated access mechanisms
* environment separation

The infrastructure should support application-generated authorized access rather than distributing permanent object-storage credentials.

Do not implement direct public access as a shortcut.

---

# 18. IAM Foundation

Implement foundational AWS IAM structure.

Support roles/policies for categories such as:

* Terraform/deployment identity boundary
* application workloads
* data services where applicable
* CI/CD identity boundary
* read-only operational access
* break-glass/admin boundary

Use least privilege.

Avoid wildcard permissions unless the specific AWS service genuinely requires them and the scope is explicitly bounded.

Do not hard-code human users into application IAM policies unnecessarily.

Prefer role-based access.

---

# 19. IAM for Workloads

Design the infrastructure so later EKS workloads can assume scoped AWS roles.

Where the EKS implementation will later use:

* IRSA
* EKS Pod Identity
* equivalent workload identity

prepare the IAM policy/module boundaries without requiring the Kubernetes layer to be implemented yet.

Policies may cover controlled access to:

* S3
* Secrets Manager
* KMS
* messaging where applicable
* other explicitly required AWS services

Do not attach broad account-level permissions to application workloads.

---

# 20. KMS Foundation

Implement foundational encryption-key architecture.

Support appropriate keys for:

* secrets
* S3
* data services where required
* infrastructure/state where required

Provide:

* key policies
* rotation settings
* aliases
* environment boundaries
* least-privilege usage

Do not expose key material.

Do not create an excessive number of keys without clear separation requirements.

---

# 21. Secrets and Configuration Boundary

Establish the infrastructure strategy for:

* Secrets Manager and/or SSM Parameter Store
* non-secret configuration
* environment-specific values
* rotation boundaries
* application consumption
* least privilege

Clearly separate:

* secrets
* configuration
* public runtime configuration

Do not commit actual production secrets.

Do not generate fake secret values and present them as deployment-ready credentials.

For local development, use explicitly non-production credentials or documented local secrets.

---

# 22. Application Configuration Contract

Create the infrastructure-side configuration structure needed to provide:

* database connection
* Redis connection
* streaming connection
* search connection
* object storage configuration
* service URLs
* environment identification
* region identification
* runtime feature/configuration references

Do not duplicate application configuration definitions that already belong to the backend.

Infrastructure should supply values; applications should own their own typed configuration schemas.

---

# 23. Network Security

Implement foundational network security.

Requirements:

* private data services
* restricted ingress
* least-privilege security-group rules
* no unrestricted database access from the internet
* controlled administrative access
* internal-only service communication where appropriate
* encrypted transport where supported
* separation between public and private layers

Do not expose:

* PostgreSQL
* Redis
* Kafka
* OpenSearch

directly to the public internet.

---

# 24. Environment Safety

Implement protections against accidental destructive operations.

Where appropriate:

* Terraform lifecycle protections
* explicit environment naming
* production safeguards
* deletion protection
* confirmation requirements
* restricted credentials
* separate state

Do not make all infrastructure immutable if that prevents legitimate lifecycle management.

Use protections where data loss or service destruction would be especially costly.

---

# 25. Cost and Resource Defaults

Establish reasonable defaults without over-optimizing for a development environment at the expense of production architecture.

Clearly distinguish:

* local-development sizes
* non-production AWS sizes
* production target classes

Do not claim those sizes are capacity-tested.

Avoid accidentally deploying expensive production-grade infrastructure as part of ordinary local development.

---

# 26. Infrastructure Validation

Implement infrastructure validation tools and scripts.

Support:

* Terraform formatting
* Terraform validation
* linting
* static analysis
* security scanning where compatible
* Dockerfile validation
* Compose validation
* configuration validation

Use repository-supported tooling where available.

Do not introduce an unnecessary toolchain solely for cosmetic purposes.

---

# 27. Documentation

Create or update infrastructure documentation covering:

* architecture
* environment model
* Terraform structure
* state management
* AWS account/region strategy
* networking
* IAM
* KMS
* secrets/configuration
* Docker
* local development
* PostgreSQL/PostGIS
* Redis
* Kafka/Redpanda
* OpenSearch
* S3
* environment separation
* security expectations
* prerequisites
* validation
* external-infrastructure limitations

Documentation must distinguish repository configuration from actual deployed infrastructure.

---

# 28. Environment Bootstrap Documentation

Provide explicit, actionable instructions for infrastructure bootstrapping.

Document:

* prerequisites
* AWS authentication expectations
* Terraform initialization
* required variables
* backend/state bootstrap
* plan/apply flow
* local development startup
* database migration handoff
* verification commands
* cleanup/destruction procedures appropriate to each environment

Do not embed personal credentials or account identifiers.

Do not provide destructive production commands without clear safeguards/context.

---

# 29. Infrastructure Testing

Implement meaningful infrastructure tests where practical.

Cover:

* Terraform validation
* module input/output behavior
* policy syntax
* security-group rule intent
* environment separation
* resource naming/tagging
* Docker build
* Compose startup
* local service health
* configuration rendering

Where actual AWS access is unavailable:

* validate Terraform statically
* validate plans where credentials are genuinely available
* use local emulation/mocks only where appropriate
* explicitly report what could not be executed

Do not fabricate successful cloud provisioning.

---

# 30. Compatibility with Application Runtime

Verify that the foundational infrastructure can support the actual application runtime.

Confirm:

* backend can obtain required configuration
* database migration process can connect correctly
* Redis configuration matches application expectations
* Kafka/Redpanda connection parameters match application clients
* search configuration matches backend clients
* S3 configuration matches object-storage abstractions
* local Docker networking resolves service names correctly
* health checks use actual service endpoints
* graceful shutdown remains compatible with container execution

Do not modify application behavior merely to make infrastructure validation easier unless the change is genuinely required for integration.

---

# OUT OF SCOPE

Do not implement the later infrastructure scopes in this volume.

Explicitly out of scope:

* complete Kubernetes/EKS cluster implementation
* Kubernetes manifests/Helm application deployments
* ingress/load-balancer implementation
* pod disruption budgets
* HPA/autoscaling configuration
* network policies at Kubernetes level
* production observability stack
* Prometheus
* Grafana
* Loki
* Tempo
* complete OpenTelemetry deployment
* CI/CD workflows
* GitHub Actions deployment pipelines
* ECR delivery pipelines
* global edge/Route53/WAF delivery architecture
* multi-region failover implementation
* disaster-recovery execution
* production load testing
* capacity testing
* resilience drills
* day-2 operational runbooks beyond foundational bootstrap documentation
* backend code
* database schema redesign
* application-level search/indexing implementation
* application-level event-schema redesign
* separate final-integration phase

Do not create additional infrastructure volumes.

The remaining infrastructure sequence must remain exactly:

1. Infrastructure Volume 1 — Foundation
2. Infrastructure Volume 2 — Kubernetes/EKS
3. Infrastructure Volume 3 — Stateful Production Data
4. Infrastructure Volume 4 — Observability/Security Operations
5. Infrastructure Volume 5 — CI/CD and Global Delivery
6. Infrastructure Volume 6 — Capacity/Resilience/Day-2 Operations

---

# IMPLEMENTATION RULES

## Repository First

Inspect before modifying.

Determine the actual:

* infrastructure structure
* application services
* Docker strategy
* environment variables
* runtime ports
* database requirements
* Redis usage
* event-streaming usage
* search usage
* object-storage usage
* existing Terraform
* existing local orchestration

Do not invent nonexistent workloads.

## Infrastructure as Code First

Repository-side infrastructure must be fully represented in code.

Do not rely on manual console configuration for foundational resources unless a service explicitly requires a documented bootstrap step that cannot reasonably be codified.

Where manual external operations are unavoidable:

* document them
* provide the corresponding repository-side configuration
* do not claim they were executed if they were not

## Environment-Aware Execution

Infrastructure agents commonly run in environments without:

* AWS credentials
* cloud network access
* Terraform state backends
* EKS access
* external managed services

When external execution is unavailable:

* create correct repository artifacts
* validate syntax and plans where possible
* use local infrastructure for local dependencies
* clearly report unavailable external validation
* never fake successful provisioning

## Security

Never commit:

* production credentials
* access keys
* secret values
* private certificates
* state files containing secrets

Use least privilege.

## No Public Stateful Services

Do not expose databases, Redis, Kafka, or OpenSearch to the public internet.

## Docker

Images must be production-oriented.

Avoid:

* root runtime where practical
* unnecessary packages
* embedded secrets
* mutable "latest" assumptions in production-oriented configuration

## Terraform

Use deterministic modules and explicit inputs.

Do not use broad wildcard permissions or dangerous lifecycle behavior without justification.

## No Pseudo-Code

Create actual Terraform, Docker, Compose, configuration, scripts, tests, and documentation.

Do not use:

* placeholders presented as finished infrastructure
* TODO-only modules
* fake AWS resources
* fake cloud outputs
* fabricated deployment success
* omitted configuration
* “implement similarly”

---

# VALIDATION REQUIREMENTS

Before considering this volume complete:

1. Inspect the entire infrastructure repository.
2. Run Terraform formatting checks.
3. Run Terraform validation.
4. Run Terraform lint/static analysis available in the repository.
5. Run infrastructure security scanning available in the repository.
6. Validate variable and environment schemas.
7. Validate naming/tagging conventions.
8. Validate IAM policy syntax and intended scope.
9. Validate KMS configuration syntax.
10. Validate security-group rules.
11. Validate Dockerfiles.
12. Build relevant Docker images where the environment permits.
13. Validate Docker Compose configuration.
14. Start local foundational services where feasible.
15. Verify PostgreSQL/PostGIS health.
16. Verify Redis health.
17. Verify Kafka/Redpanda health.
18. Verify OpenSearch health.
19. Verify S3-compatible local storage where used.
20. Verify application-to-dependency networking where practical.
21. Verify environment separation configuration.
22. Verify no production secrets are present.
23. Verify no Terraform state artifacts are committed.
24. Verify documentation commands remain accurate.
25. Verify no later infrastructure scope has been unintentionally implemented here.
26. Verify no duplicate or conflicting infrastructure definitions were introduced.

Where AWS credentials, cloud access, or external managed services are unavailable:

* perform every repository-side validation possible
* validate Terraform syntax/plan behavior to the extent available
* validate local infrastructure
* explicitly report what could not be executed

Never claim that AWS resources were created, updated, or verified unless the environment actually performed and returned evidence of those operations.

---

# INTEGRATION CHECK

Before finalizing, verify that the foundational infrastructure integrates cleanly with the application repository and prepares the exact base required by later infrastructure volumes.

Confirm that:

* backend runtime configuration can consume the environment structure
* PostgreSQL/PostGIS connectivity matches application expectations
* Redis connectivity matches application expectations
* Kafka/Redpanda connectivity matches application expectations
* OpenSearch connectivity matches application expectations
* S3/object-storage configuration matches the application abstraction
* Docker containers can resolve required dependencies
* local development can reproduce the foundational dependency graph
* infrastructure environments are clearly separated
* IAM is prepared for later workload identity
* KMS is prepared for later encrypted services
* secrets/configuration boundaries are prepared for later EKS and CI/CD integration
* naming/tagging remains consistent
* Terraform modules can be extended by later infrastructure volumes without restructuring this foundation

Do not create temporary infrastructure that later volumes will need to replace.

The infrastructure produced by this volume must combine cleanly with the Kubernetes, stateful-data, observability, CI/CD/global-delivery, and resilience work that follows.

---

# DEFINITION OF DONE

This volume is complete only when:

* infrastructure repository structure is established
* environment model is established
* Terraform foundation is implemented
* Terraform state strategy is documented/implemented at repository level
* AWS provider/account/region configuration is implemented
* naming/tagging strategy is implemented
* VPC/network foundation is implemented
* public/private subnet architecture is defined
* security-group foundation is implemented
* local development network is implemented
* Docker standards are implemented
* local container orchestration is implemented
* PostgreSQL/PostGIS foundation is implemented
* Redis foundation is implemented
* Kafka/Redpanda foundation is implemented
* OpenSearch foundation is implemented
* S3 foundation is implemented
* S3 access model is implemented
* IAM foundation is implemented
* workload-identity-ready IAM boundaries are implemented
* KMS foundation is implemented
* secrets/configuration boundary is implemented
* application configuration contract is established
* environment-safety controls are implemented
* cost/resource defaults are documented
* infrastructure validation is implemented
* local foundational services are validated where possible
* infrastructure documentation is updated
* bootstrap documentation is complete
* integration with the application runtime is verified as far as the environment allows
* no production secrets are committed
* no public exposure of stateful services exists
* no fake cloud provisioning is reported
* no placeholders remain
* no later infrastructure scope was unnecessarily implemented

---

# IMPLEMENTATION REPORT

At the end of execution, provide a concise report containing:

## Files Changed

List created, modified, and removed infrastructure files.

## Infrastructure Implemented

Summarize:

* Terraform
* networking
* IAM
* KMS
* secrets/configuration
* Docker
* local orchestration
* PostgreSQL/PostGIS
* Redis
* Kafka/Redpanda
* OpenSearch
* S3

## Environments

Explain the implemented local/development/test/staging/production boundaries.

## Validation

Report the exact commands executed and their results.

## External Infrastructure Status

Clearly state which AWS/cloud operations were actually performed and which could not be performed because of environment limitations.

Do not claim deployment when only code validation occurred.

## Follow-Up Dependencies

Identify the infrastructure components that the next volumes will extend.

Do not invent additional infrastructure phases.

---

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement the complete foundational infrastructure scope defined by this prompt.

Preserve all working application and infrastructure behavior that is outside the scope of necessary changes.

Use the repository's actual architecture, runtime requirements, and existing infrastructure as the source of truth.

Create the real Terraform, Docker, local-orchestration, configuration, IAM, KMS, storage, networking, validation, and documentation artifacts required for this scope.

Do not merely describe infrastructure.

Do not wait for another prompt.

Do not use pseudo-code, fake AWS resources, fabricated outputs, fake cloud success, placeholder modules, committed secrets, or omitted implementation.

When cloud access is unavailable, fully implement the repository-side infrastructure and validate everything possible locally and statically.

Respect least privilege, environment isolation, secure networking, encrypted storage, workload identity, and production-oriented container practices.

Finish only when this foundational infrastructure volume is genuinely implemented, validated, documented, and ready for the subsequent infrastructure volumes to extend.
