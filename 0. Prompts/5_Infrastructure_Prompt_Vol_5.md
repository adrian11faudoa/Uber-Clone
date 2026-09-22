# Uber-Style Global Ride-Hailing & Mobility Platform — Infrastructure Prompt — Volume 5

## ROLE

You are acting as the complete senior cloud delivery, DevOps, platform engineering, security, release engineering, networking, and reliability organization responsible for implementing the project's CI/CD and global production-delivery platform to production-grade standards.

Operate as a coordinated:

* Principal Software Architect
* Cloud Architect
* Staff DevOps Engineer
* Platform Engineer
* Site Reliability Engineer
* Release Engineer
* CI/CD Engineer
* Infrastructure Security Engineer
* Networking Engineer
* Kubernetes Engineer
* Performance Engineer
* Reliability Engineer
* QA Engineer
* Technical Writer

You are an implementation agent, not a teacher.

Your responsibility is to inspect the repository and implement the complete CI/CD and global-delivery infrastructure covered by this prompt without breaking existing application or infrastructure behavior.

Do not merely describe pipelines or cloud delivery. Create the real repository-side GitHub Actions, Terraform, Helm/release configuration, container registry integration, deployment policies, environment promotion configuration, AWS edge/networking configuration, health/failover boundaries, security controls, validation tooling, tests, and documentation required by this scope, and execute external operations only when the environment genuinely permits them.

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

The repository is the source of truth for the current application and infrastructure delivery state.

Before changing anything:

1. Inspect the entire repository relevant to application delivery.
2. Inspect:

   * backend services
   * frontend
   * mobile
   * Dockerfiles
   * Docker Compose
   * Terraform
   * Helm charts
   * Kubernetes manifests
   * environment configuration
   * application package/workspace structure
   * tests
   * build scripts
   * current GitHub Actions workflows
   * deployment scripts
   * versioning/release configuration
   * observability configuration
   * health/readiness endpoints
   * graceful-shutdown behavior
3. Inspect infrastructure from the previous volumes:

   * AWS accounts/regions
   * VPC/networking
   * IAM
   * KMS
   * EKS
   * stateful services
   * observability
   * secret/configuration architecture
4. Determine the actual buildable/deployable services.
5. Determine which container images are required.
6. Determine actual ports, health endpoints, startup commands, migration requirements, worker types, and environment dependencies.
7. Determine how the existing repository expects releases to be versioned and promoted.
8. Determine whether infrastructure is monorepo-based or split into workspaces/packages and preserve the actual repository conventions.
9. Determine what delivery infrastructure already exists.
10. Preserve compatible working CI/CD and infrastructure.
11. Do not invent deployable services, environments, repositories, domains, certificates, accounts, or regions that are not part of the established architecture.
12. Do not fabricate external credentials or infrastructure identifiers.

This prompt is independently executable.

Do not depend on another AI conversation or on another prompt being pasted into the repository.

---

# INFRASTRUCTURE TARGET

The intended delivery platform uses:

* GitHub Actions
* Docker
* Amazon ECR
* Amazon EKS
* Terraform
* Helm
* AWS IAM
* OIDC-based GitHub-to-AWS authentication
* AWS Route 53
* CloudFront where appropriate
* AWS WAF where appropriate
* TLS/ACM
* health checks
* controlled environment promotion
* global/multi-region delivery boundaries
* infrastructure and application deployment automation

This volume implements **CI/CD and global production delivery**.

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

Implement a secure and auditable delivery platform capable of taking verified repository changes through:

* validation
* build
* test
* security checks
* containerization
* artifact publication
* environment deployment
* controlled promotion
* rollback
* infrastructure changes
* global routing/delivery
* health-aware traffic management

Establish:

* GitHub Actions workflow architecture
* reusable CI components
* application build pipelines
* test pipelines
* container image build/publish
* ECR repositories
* image provenance and signing where practical
* dependency/security scanning
* OIDC-based AWS authentication
* deployment identities
* Terraform CI/CD
* Helm deployment automation
* environment promotion
* deployment gates
* rollback mechanisms
* migration sequencing
* Route 53 DNS
* ACM certificate integration
* CloudFront where appropriate
* WAF
* global/multi-region routing boundaries
* health checks
* failover configuration
* release/version management
* secrets handling
* branch/protected-environment controls
* pipeline observability
* deployment documentation

The resulting platform must support safe evolution of a large distributed system.

Do not confuse automated deployment with proven production resilience.

---

# PRIMARY SCOPE

# CI FOUNDATION

## 1. GitHub Actions Architecture

Implement or normalize the repository's GitHub Actions architecture.

Use clear workflow boundaries for:

* pull-request validation
* continuous integration
* application build
* container build
* infrastructure validation
* security validation
* deployment
* promotion
* rollback/manual operations where justified

Avoid one giant workflow with unrelated responsibilities.

Avoid unnecessary duplicated workflow logic.

Use reusable workflows/actions where they materially reduce repetition.

---

# 2. Pull Request Validation

Implement appropriate pull-request validation for actual repository components.

Cover where applicable:

* formatting
* lint
* TypeScript/type checking
* unit tests
* component tests
* integration tests
* frontend build
* mobile validation/build checks appropriate to repository capabilities
* backend build
* Terraform validation
* Terraform lint/security checks
* Helm lint
* Kubernetes manifest validation
* Dockerfile validation
* dependency/security checks

The exact matrix must match the actual repository.

Do not require a production deployment for ordinary pull requests.

---

# 3. Monorepo / Workspace Awareness

Where the repository contains multiple packages/applications:

* detect changed components where practical
* avoid rebuilding unrelated components unnecessarily
* preserve dependency ordering
* retain a full-project validation path

Do not optimize CI by sacrificing cross-package correctness.

Where change detection is unsafe or too complex, prefer deterministic broader validation rather than fragile heuristics.

---

# 4. Build Reproducibility

Implement deterministic builds.

Support:

* pinned tool versions where appropriate
* lockfile enforcement
* reproducible package installation
* deterministic Docker builds where practical
* explicit build arguments
* environment separation
* artifact versioning

Do not rely on mutable `latest` tags for release identity.

---

# 5. Dependency Caching

Use CI caching where safe for:

* package managers
* Docker layers
* Terraform providers/modules
* other supported tooling

Cache keys must include relevant lockfile/toolchain inputs.

Do not allow stale caches to conceal dependency changes.

Do not cache secrets.

---

# 6. Build Artifacts

Define artifact handling for:

* build outputs
* test reports
* coverage
* generated manifests
* container metadata
* release metadata

Artifacts must be attributable to:

* commit
* branch/tag
* build
* version

Do not upload sensitive runtime secrets as artifacts.

---

# CONTAINER DELIVERY

## 7. ECR Architecture

Implement Amazon ECR repositories for actual deployable container images.

Support:

* one repository per appropriate application/workload boundary
* environment-independent image identity where appropriate
* immutable release tags
* lifecycle policies
* encryption
* scan-on-push where available
* repository access policies
* image retention

Do not create ECR repositories for nonexistent services.

Do not use mutable `latest` as a production release identifier.

---

# 8. Container Tagging

Implement deterministic image tagging.

Useful tags may include:

* immutable commit SHA
* semantic/version release
* build identifier

Production deployment references should resolve to immutable artifacts.

Do not rely solely on human-readable mutable tags.

---

# 9. Image Scanning

Implement container security scanning.

Cover:

* OS vulnerabilities
* package vulnerabilities
* dependency vulnerabilities
* secret detection
* malware/security checks supported by the chosen tooling

Define severity thresholds appropriate to the project.

Do not automatically block every low-severity advisory without considering exploitability and operational context.

Do not allow known critical issues into production silently.

---

# 10. Image Provenance and Signing

Where practical, establish:

* SBOM generation
* provenance metadata
* image signing
* signature verification at deployment or admission boundaries where compatible

Use repository-supported tooling.

Do not create an elaborate supply-chain system that cannot be maintained.

Document which guarantees are actually enforced versus merely generated.

---

# 11. Registry Lifecycle

Configure ECR lifecycle policies to control:

* old image retention
* untagged image cleanup
* development-image cleanup
* release retention

Do not delete images still referenced by active production deployments.

Use retention values as operational starting points, not capacity-tested claims.

---

# AWS AUTHENTICATION AND SECURITY

## 12. GitHub OIDC

Implement GitHub Actions OIDC federation to AWS.

Use:

* IAM OIDC provider
* scoped trust policies
* repository/organization conditions
* branch/tag/environment constraints where appropriate

Do not store long-lived AWS access keys in GitHub secrets.

---

# 13. CI/CD IAM Roles

Create separate IAM roles for appropriate responsibilities, such as:

* Terraform plan
* Terraform apply
* image publication
* staging deployment
* production deployment
* read-only verification

Apply least privilege.

Do not grant every workflow administrator privileges.

---

# 14. Environment Deployment Permissions

Protect staging/production roles with:

* branch restrictions
* environment restrictions
* approval requirements where justified
* repository conditions
* tag constraints
* explicit trust policies

Production deployment must not be reachable by arbitrary pull requests.

---

# 15. Secret Handling in CI

Use:

* GitHub environment secrets only where necessary
* AWS Secrets Manager/SSM references
* OIDC
* ephemeral credentials

Never:

* print secrets
* persist secrets into artifacts
* embed secrets in Docker images
* commit secrets
* pass secrets through unprotected shell output

Ensure workflow logs redact sensitive values.

---

# 16. Supply-Chain Security

Implement appropriate controls for:

* dependency integrity
* lockfile changes
* third-party GitHub Actions
* Docker base images
* Terraform providers
* Helm charts
* artifact provenance

Pin third-party actions where practical rather than following floating branches.

Do not introduce supply-chain dependencies without justification.

---

# TERRAFORM DELIVERY

## 17. Infrastructure Pipeline

Implement CI workflows for Terraform.

Support:

* formatting
* validation
* linting
* security scanning
* plan
* plan artifact
* controlled apply

Plans must be reviewable before production application.

---

# 18. Terraform Plan/Apply Separation

Separate:

* validation
* planning
* approval
* apply

Do not automatically apply every pull request to production.

For pull requests:

* run validation
* generate plans for relevant environments where appropriate
* publish reviewable results safely

For production:

* use protected deployment environments
* explicit approval where required
* apply only the intended plan

---

# 19. Terraform State Safety

Use the established remote-state architecture.

Support:

* state locking
* encrypted state
* environment separation
* scoped CI credentials

Do not expose state contents in logs.

Remember that Terraform state can contain sensitive values.

---

# 20. Drift and Plan Visibility

Make infrastructure changes visible.

Support:

* plan artifacts
* resource summaries
* approval boundaries
* drift-detection boundary where appropriate

Do not build a separate continuous drift system if it belongs naturally in the later operational scope.

---

# HELM / KUBERNETES DELIVERY

## 21. Helm Deployment Pipeline

Implement automated Helm deployment for actual application workloads.

Support:

* chart validation
* template rendering
* environment values
* immutable image references
* namespace selection
* release naming
* timeout
* wait behavior
* atomic rollout where appropriate
* rollback-compatible release history

Do not silently continue after failed Kubernetes rollouts.

---

# 22. Deployment Ordering

Define safe application deployment ordering.

Account for dependencies such as:

* database-compatible application changes
* migrations
* backend API
* workers
* realtime services
* frontend
* supporting consumers

Do not create an ordering that violates application compatibility.

---

# 23. Database Migration Delivery

Establish a production-safe migration mechanism.

Support, according to actual backend architecture:

* migration image/job
* explicit execution
* migration status
* failure visibility
* sequencing relative to application rollout

Avoid automatically running destructive migrations as an incidental side effect of every pod startup.

Do not run multiple competing migration processes simultaneously unless the architecture explicitly supports it.

---

# 24. Deployment Strategy

Use appropriate Kubernetes rollout mechanisms.

Support:

* rolling updates
* readiness gates
* safe termination
* replica availability
* rollback
* deployment timeout

Do not claim zero downtime under all failure modes.

Where a workload needs special rollout handling, encode it explicitly.

---

# 25. Rollback

Implement practical rollback procedures.

Support:

* application rollback
* Helm release rollback
* immutable image selection
* previous-release identification
* deployment failure detection

Document database migration rollback limitations.

Do not imply that every database migration is automatically reversible.

---

# 26. Promotion Model

Implement a controlled promotion path such as:

**Validation → Build → Staging → Verification → Production**

Use the project's actual environment model.

Production should promote known artifacts rather than rebuilding a materially different image.

Do not rebuild images independently in each environment and assume they are identical.

---

# 27. Deployment Gates

Define automated gates using actual measurable signals.

Potential gates:

* tests pass
* security scan thresholds pass
* image exists and is immutable
* Helm rendering succeeds
* rollout succeeds
* readiness passes
* smoke checks pass
* key health endpoints respond
* deployment error budget conditions where appropriate

Do not create gates that depend on fabricated or unavailable measurements.

---

# 28. Post-Deployment Verification

Implement safe post-deployment verification.

Use:

* health checks
* readiness checks
* version/build endpoint where available
* read-only smoke tests
* key service checks

Avoid destructive business actions in production smoke tests.

---

# 29. Deployment Observability

Integrate deployments with the existing observability system.

Record:

* version
* commit
* deployment time
* environment
* region
* release
* actor/workflow
* result

Make deployments visible in dashboards/annotations where practical.

Do not leak secrets into deployment metadata.

---

# GLOBAL DELIVERY

## 30. Domain and DNS Architecture

Implement Route 53 infrastructure for actual production domains configured by the repository/environment.

Support:

* hosted zones where appropriate
* records
* aliases
* environment separation
* health-check integration
* region-aware routing

Do not invent production domain names.

Use variables/inputs for deployment-specific domains.

---

# 31. TLS / ACM

Implement ACM certificate architecture.

Support:

* certificate resources or references
* DNS validation
* appropriate regional certificate placement
* renewal behavior
* environment/region separation

Where CloudFront is used, remember that certificates are region-sensitive.

Do not fabricate certificate ARNs.

---

# 32. CloudFront

Where the architecture benefits from a global edge layer, implement CloudFront appropriately.

Possible uses:

* frontend/static web delivery
* global API edge where explicitly designed
* caching of safe public assets
* TLS termination
* origin failover

Do not cache authenticated/private API responses indiscriminately.

Do not place mutable/private trip/payment responses into public caches.

---

# 33. CloudFront Origin Architecture

Configure origins according to actual workloads.

Support appropriate origins such as:

* application ingress
* object storage for public/static assets where applicable
* other explicitly documented origins

Configure:

* HTTPS
* origin timeouts
* protocol policy
* caching behavior
* compression
* headers
* cookies/query-string forwarding only where required

Do not forward every header/cookie/query parameter unnecessarily.

---

# 34. WebSocket / Realtime Edge Delivery

Ensure the chosen edge/load-balancer architecture supports realtime workloads appropriately.

Where CloudFront is used or bypassed:

* document the websocket path
* configure supported origin behavior
* preserve authenticated headers/cookies required by the application
* avoid incompatible caching
* use appropriate timeout behavior

Do not route realtime traffic through a caching policy designed for static content.

---

# 35. AWS WAF

Implement WAF where appropriate for internet-facing workloads.

Use managed protections and sensible custom controls for:

* common web attacks
* abusive traffic
* rate limiting
* suspicious requests

Do not deploy unlimited aggressive rate rules that can block legitimate riders/drivers.

Where rate-limiting rules are configured, document their intended scope.

---

# 36. WAF Logging and Monitoring

Integrate WAF signals with the observability/security platform.

Support:

* blocked requests
* sampled/allowed requests where useful
* rule matches
* rate-limit events
* associated operational visibility

Do not log sensitive request bodies unnecessarily.

---

# 37. Global Traffic Management

Implement the repository-side global routing architecture.

Where supported, establish:

* region-aware endpoints
* Route 53 latency/weighted/failover/geolocation policy as architecturally appropriate
* health-check-driven routing
* region weights
* explicit primary/secondary boundaries

Do not implement arbitrary geographic routing unrelated to service architecture.

---

# 38. Multi-Region Application Delivery

Prepare application deployment for multiple AWS regions.

Support:

* region-specific infrastructure
* environment/region variables
* immutable artifacts
* independent cluster releases where appropriate
* global DNS
* health checks

Do not assume that deploying the same Helm chart to two regions automatically creates a functioning globally consistent system.

---

# 39. Regional Health

Integrate global routing with real service health.

Health checks must reflect meaningful availability.

Avoid using superficial TCP success where the application is actually unavailable.

Where appropriate, use read-only application health endpoints.

---

# 40. Failover Configuration Boundary

Implement automated infrastructure-level failover boundaries where appropriate.

Support:

* primary/secondary region definition
* Route 53 failover policies
* health checks
* origin failover where applicable
* documented operator override

Do not claim full disaster recovery merely because DNS failover is configured.

Detailed resilience and failover testing belongs to Infrastructure Volume 6.

---

# 41. Frontend Global Delivery

Where the web architecture uses static/edge delivery:

* configure global caching
* immutable asset handling
* compression
* cache invalidation/versioning where required
* secure custom domains

Do not cache private authenticated application data at the edge without an explicit safe design.

---

# 42. Mobile Distribution Boundary

Where repository-side mobile release automation is appropriate, implement the delivery boundary for:

* build metadata
* environment selection
* release artifacts
* signing configuration references
* staged release configuration

Do not commit signing certificates or private keys.

Do not fabricate Apple/Google credentials.

If app-store publishing is outside current environment access, implement the repository-side workflow and clearly document the external credential boundary.

---

# RELEASE MANAGEMENT

## 43. Versioning

Implement consistent application/release versioning across:

* package versions where applicable
* container tags
* Helm releases
* deployment metadata
* mobile builds where applicable

Avoid version drift between artifact and deployed workload identity.

---

# 44. Release Provenance

Each production deployment must be traceable to:

* source commit
* build
* artifact/image digest
* workflow
* environment
* region
* deployment time

Prefer image digests over mutable tags for deployment identity.

---

# 45. Protected Production Releases

Implement production release controls.

Support where appropriate:

* protected GitHub environments
* approval requirements
* release tags
* branch restrictions
* explicit production IAM role
* concurrency control

Prevent simultaneous conflicting production deployments.

---

# 46. Deployment Concurrency

Protect against concurrent runs targeting the same environment.

Use workflow concurrency controls where appropriate.

Do not cancel a currently safe deployment merely because a new commit arrived unless the desired policy explicitly calls for it.

For production, prefer deliberate serialization or another safe deployment policy.

---

# 47. Rollout Failure Handling

When deployment fails:

* surface the failure
* preserve logs/artifacts
* stop promotion
* retain the previous healthy release
* provide rollback path
* do not automatically perform risky remediation without explicit policy

---

# 48. Artifact Retention

Configure retention for:

* workflow artifacts
* test reports
* deployment reports
* manifests
* SBOMs
* provenance
* release metadata

Retention should be sufficient for troubleshooting without becoming uncontrolled storage growth.

---

# 49. CI/CD Security and Audit

Ensure pipeline activity is attributable.

Record:

* actor
* workflow
* commit
* environment
* approval
* deployment result

Integrate with the security/audit architecture where appropriate.

Do not expose secret values in audit events.

---

# 50. Delivery Documentation

Create or update deployment documentation covering:

* GitHub Actions
* OIDC
* IAM
* ECR
* image tagging
* image scanning
* SBOM/provenance/signing
* Terraform pipeline
* Helm pipeline
* migration strategy
* promotion
* smoke verification
* rollback
* DNS
* ACM
* CloudFront
* WAF
* websocket delivery
* global routing
* multi-region deployment
* mobile release boundary
* production approvals
* deployment troubleshooting

Clearly distinguish:

* configured in source control
* validated in CI
* deployed to staging
* deployed to production
* externally configured but not executable from the current environment

---

# 51. Pipeline Testing

Implement meaningful CI/CD tests and validation.

Cover:

* workflow syntax
* YAML validity
* action references
* Terraform plan/validation
* Helm rendering
* Kubernetes validation
* Docker build
* ECR configuration
* IAM trust policies
* release metadata
* environment protections
* deployment scripts
* smoke-test configuration
* DNS/TLS configuration
* WAF/CloudFront/Route 53 configuration

Where actual deployment is unavailable:

* validate workflow configuration statically
* run local builds
* render manifests
* validate Terraform
* test scripts with mocks/dry-run modes
* report cloud limitations honestly

---

# 52. Local / Non-Production Deployment Path

Provide a practical path for:

* local development
* test
* staging

The staging path should resemble production sufficiently to expose:

* deployment failures
* configuration problems
* networking mistakes
* readiness issues
* migration problems

Do not require local developers to possess production AWS permissions.

---

# 53. Environment Promotion Consistency

Ensure that environment differences are deliberate.

Avoid:

* hidden configuration drift
* hand-edited production manifests
* different application builds per environment
* undocumented production-only patches

Use environment-specific configuration over one immutable artifact.

---

# 54. Security Gates

Integrate appropriate security gates into CI/CD.

Potential checks:

* dependency vulnerabilities
* container vulnerabilities
* secrets
* IaC security
* Kubernetes security
* license policies where required
* artifact provenance

Set actionable thresholds.

Do not blindly reject every theoretical advisory.

---

# 55. Deployment Rollback Documentation

Document safe rollback procedures for:

* application
* Helm
* image
* infrastructure
* DNS/global routing where applicable

Explicitly identify irreversible or dangerous operations.

Do not document impossible rollback procedures.

---

# OUT OF SCOPE

Do not implement the final infrastructure volume's capacity, resilience, and day-2 operations program here.

Explicitly out of scope:

* comprehensive load testing
* scale/capacity benchmarking
* autoscaling capacity tuning based on production measurements
* chaos engineering
* disaster-recovery drills
* backup restore drills
* regional failure exercises
* incident-response program
* operational maintenance runbooks beyond CI/CD/global-delivery procedures
* long-term infrastructure cost optimization
* comprehensive service upgrade lifecycle program
* full production data migration program
* backend application feature development
* frontend feature development
* mobile feature development
* database schema redesign
* dispatch redesign
* observability redesign
* separate QA phase
* separate final-integration phase
* a new infrastructure volume

The next and final infrastructure volume is **Infrastructure Volume 6 — Capacity, Resilience, and Day-2 Operations**.

---

# IMPLEMENTATION RULES

## Repository First

Inspect before modifying.

Determine actual:

* build commands
* tests
* containers
* deployable services
* workflow structure
* Terraform structure
* Helm charts
* health endpoints
* environment boundaries
* domain configuration
* AWS resources
* mobile build/release capabilities

Do not invent pipelines for nonexistent workloads.

## Immutable Artifacts

Production deployments should reference immutable:

* image digests
* verified artifacts
* identifiable commits/releases

Do not rely on mutable `latest`.

## OIDC Over Long-Lived Keys

Use GitHub OIDC to AWS.

Do not create long-lived AWS access keys for CI.

## Least Privilege

Separate:

* build
* registry
* Terraform
* staging deploy
* production deploy
* verification

Use narrowly scoped IAM roles.

## Promotion Discipline

Promote known artifacts.

Do not rebuild independently for production.

## Migration Discipline

Treat database migrations as a first-class release concern.

Do not hide them inside arbitrary application startup.

## Production Protection

Use:

* protected environments
* approvals
* branch/tag restrictions
* deployment concurrency
* explicit IAM boundaries

## Security

Do not:

* print credentials
* store signing keys in git
* commit secrets
* expose private origin infrastructure unnecessarily
* publish sensitive deployment artifacts

## Global Delivery

Use health-aware routing.

Do not claim global resilience merely because DNS/edge resources exist.

## Cloud-Access Reality

The implementation environment may lack:

* AWS credentials
* GitHub repository administration access
* ECR access
* Route 53 access
* ACM access
* CloudFront access
* WAF access
* EKS access
* mobile signing credentials

When external access is unavailable:

* implement repository-side configuration
* validate workflows statically
* run local build/tests
* validate Terraform
* render Helm/Kubernetes
* use dry-run/mock paths
* document exactly what was not executed

Do not fabricate deployments or DNS/certificate state.

## No Pseudo-Code

Create actual:

* GitHub Actions workflows
* Terraform
* Helm configuration
* Kubernetes deployment configuration
* IAM policies
* ECR configuration
* DNS/TLS/edge infrastructure
* WAF rules
* scripts
* tests
* documentation

Do not use placeholder workflows presented as production-ready.

---

# VALIDATION REQUIREMENTS

Before considering this volume complete:

1. Inspect all current application and infrastructure delivery configuration.
2. Validate GitHub Actions workflow syntax.
3. Validate action references/pinning strategy.
4. Validate pull-request CI.
5. Validate full-build CI.
6. Validate test workflows.
7. Validate Docker builds.
8. Validate image tagging.
9. Validate ECR configuration.
10. Validate image lifecycle rules.
11. Validate vulnerability/scanning configuration.
12. Validate SBOM/provenance/signing configuration where implemented.
13. Validate GitHub OIDC trust policies.
14. Validate CI/CD IAM roles.
15. Validate production environment protections.
16. Validate Terraform CI.
17. Validate Terraform plan/apply boundaries.
18. Validate Helm deployment workflows.
19. Validate rendered Kubernetes manifests.
20. Validate deployment ordering.
21. Validate migration-job configuration.
22. Validate deployment rollback behavior/configuration.
23. Validate promotion configuration.
24. Validate deployment gates.
25. Validate post-deployment health checks.
26. Validate deployment observability metadata.
27. Validate Route 53 configuration.
28. Validate ACM certificate configuration.
29. Validate CloudFront configuration where used.
30. Validate websocket edge behavior configuration where applicable.
31. Validate WAF configuration.
32. Validate WAF/edge observability integration.
33. Validate global routing policy.
34. Validate regional health checks.
35. Validate multi-region deployment configuration.
36. Validate mobile release configuration where repository-supported.
37. Validate release/version metadata.
38. Validate deployment concurrency protection.
39. Validate artifact retention.
40. Validate CI/CD audit metadata.
41. Validate workflow secrets handling.
42. Verify no long-lived AWS credentials were introduced for CI.
43. Verify no production secrets or signing keys are committed.
44. Verify no mutable `latest` production dependency exists.
45. Verify no private stateful service was unnecessarily exposed publicly.
46. Verify no later capacity/resilience/day-2 scope was unnecessarily implemented.
47. Verify documentation matches actual implementation.

Where external GitHub/AWS access is unavailable:

* perform all static/repository-side validation possible
* run local builds/tests
* validate Terraform
* render Helm/Kubernetes manifests
* validate workflow syntax and configuration
* exercise dry-run/mock deployment logic where possible
* explicitly report unavailable external validation

Never claim:

* GitHub production workflow execution
* ECR image publication
* AWS deployment
* DNS propagation
* certificate issuance
* CloudFront propagation
* WAF activation
* multi-region failover
* mobile-store publication

unless actually performed and verified.

---

# INTEGRATION CHECK

Before finalizing, verify that the CI/CD and global-delivery platform integrates cleanly with Infrastructure Volumes 1–4.

Confirm that:

* GitHub OIDC uses the established AWS IAM architecture
* CI roles use least privilege
* ECR repositories match actual deployable workloads
* immutable images are compatible with EKS deployments
* Helm charts from Infrastructure Volume 2 can be deployed directly by CI
* environment configuration uses the existing secrets model
* Terraform pipelines use the existing remote-state architecture
* database migrations are compatible with the PostgreSQL infrastructure
* deployment health checks use the application's actual health endpoints
* observability annotations/metadata integrate with the existing monitoring stack
* deployment events can be correlated with metrics/logs/traces
* Route 53 routes to the intended regional entry points
* ACM certificates cover actual configured domains
* CloudFront does not cache private/authenticated application data incorrectly
* websocket traffic remains functional
* WAF does not interfere with legitimate authenticated/API/realtime traffic by design
* global routing uses meaningful health signals
* regional environments can run the same immutable application artifacts
* production promotion cannot accidentally use pull-request code without the intended controls
* rollback remains possible for application releases
* infrastructure changes remain reviewable
* the final capacity/resilience volume can build on the resulting deployment and global-routing architecture without replacing it

Do not introduce temporary delivery architecture that Infrastructure Volume 6 must replace.

---

# DEFINITION OF DONE

This volume is complete only when:

### CI/CD

* GitHub Actions architecture is implemented
* pull-request validation is implemented
* full build/test validation is implemented
* monorepo/workspace handling is implemented where needed
* reproducible builds are implemented
* dependency caching is implemented where justified
* artifact handling is implemented
* release metadata is implemented

### Container Delivery

* ECR repositories are implemented for actual workloads
* immutable image tags/digests are supported
* image scanning is configured
* SBOM/provenance/signing are implemented where justified
* registry lifecycle policies are implemented

### AWS CI Security

* GitHub OIDC is implemented
* CI/CD IAM roles are implemented
* environment deployment permissions are protected
* secret handling is secure
* supply-chain controls are implemented

### Terraform Delivery

* Terraform CI is implemented
* plan/apply separation is implemented
* state access is secured
* reviewable plan flow exists
* drift visibility boundary is established

### Kubernetes Delivery

* Helm deployment automation is implemented
* deployment ordering is defined
* database migration delivery is implemented where applicable
* rollout strategy is implemented
* rollback is implemented/documented
* environment promotion is implemented
* deployment gates are implemented
* post-deployment verification is implemented
* deployment observability metadata is implemented

### Global Delivery

* Route 53 architecture is implemented
* ACM is implemented
* CloudFront is implemented where appropriate
* websocket edge behavior is configured where applicable
* WAF is implemented where appropriate
* WAF observability is integrated
* global routing is implemented
* regional health checks are implemented
* multi-region delivery boundary is implemented
* failover configuration boundary is implemented
* frontend edge delivery is implemented where applicable
* mobile release boundary is implemented where repository-supported

### Release and Operations

* versioning is consistent
* release provenance is implemented
* production releases are protected
* deployment concurrency is controlled
* rollout failures stop promotion
* artifact retention is configured
* CI/CD audit metadata is implemented
* deployment documentation is complete
* tests/validation are implemented
* external infrastructure status is honestly reported
* no production credentials/signing keys are committed
* no fake deployment success is reported
* no placeholders remain
* no later capacity/resilience/day-2 scope was unnecessarily implemented

---

# IMPLEMENTATION REPORT

At the end of execution, provide a concise report containing:

## Files Changed

List created, modified, and removed delivery/infrastructure files.

## CI/CD Implemented

Summarize:

* GitHub Actions
* validation
* build
* testing
* Docker
* ECR
* scanning
* SBOM/provenance/signing
* OIDC
* IAM
* Terraform delivery
* Helm deployment
* promotion
* rollback
* release management

## Global Delivery Implemented

Summarize:

* Route 53
* ACM
* CloudFront
* WAF
* websocket edge behavior
* global routing
* regional health
* multi-region deployment
* failover boundary
* mobile release boundary where applicable

## Security Controls

Summarize:

* OIDC
* least-privilege CI roles
* production protection
* secret handling
* supply-chain controls
* artifact integrity

## Validation

Report the exact commands/workflows/tests executed and their results.

## External Infrastructure Status

Clearly state which GitHub/AWS/cloud operations were actually performed and which could not be performed due to environment limitations.

Do not infer deployment from repository configuration alone.

## Follow-Up Dependencies

Identify what Infrastructure Volume 6 needs to use for:

* capacity modeling
* load testing
* resilience testing
* failover validation
* day-2 operations

Do not invent additional infrastructure phases.

---

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement the complete CI/CD and global-delivery infrastructure defined by this prompt.

Preserve all working application and infrastructure behavior outside the necessary scope of these changes.

Extend the infrastructure established by Volumes 1–4 rather than creating parallel delivery, IAM, observability, or Kubernetes foundations.

Create the real GitHub Actions workflows, Terraform, Helm/release configuration, ECR infrastructure, OIDC/IAM policies, release controls, Route 53, ACM, CloudFront, WAF, global-routing configuration, validation tooling, tests, and documentation required for this scope.

Do not merely describe pipelines or global delivery.

Do not wait for another prompt.

Do not use pseudo-code, placeholder workflows, fake image publications, fake AWS deployments, fabricated domains/certificates, fabricated DNS state, fake failover validation, committed credentials, long-lived CI access keys, or simulated production success.

Promote immutable, verified artifacts.

Protect production with appropriate approvals and IAM boundaries.

Treat migrations, rollback, websocket delivery, authenticated/private data, and regional health as first-class concerns.

When external GitHub/AWS access is unavailable, fully implement and validate the repository-side delivery platform and report unavailable live execution honestly.

Finish only when this CI/CD and global-delivery volume is genuinely implemented, validated, documented, and ready for Infrastructure Volume 6 to perform the final capacity, resilience, and day-2 operational engineering work.
