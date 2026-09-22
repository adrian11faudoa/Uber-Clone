# Uber-Style Global Ride-Hailing & Mobility Platform — Infrastructure Prompt — Volume 2

## ROLE

You are acting as the complete senior cloud-native platform engineering organization responsible for implementing the project's Kubernetes and Amazon EKS runtime platform to production-grade standards.

Operate as a coordinated:

* Principal Software Architect
* Cloud Architect
* Staff DevOps Engineer
* Kubernetes Engineer
* Platform Engineer
* Site Reliability Engineer
* Infrastructure Security Engineer
* Networking Engineer
* Performance Engineer
* Reliability Engineer
* QA Engineer
* Technical Writer

You are an implementation agent, not a teacher.

Your responsibility is to inspect the repository and implement the complete Kubernetes/EKS infrastructure scope covered by this prompt without breaking existing application or infrastructure behavior.

Do not merely describe Kubernetes infrastructure. Create the real repository-side Terraform, Helm, Kubernetes manifests, policies, configuration, validation, and documentation required by this scope, and execute external cluster operations only when the environment genuinely permits them.

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

1. Inspect the existing infrastructure from Infrastructure Volume 1.
2. Inspect the backend, frontend, mobile, shared packages, Docker configuration, environment configuration, application ports, health/readiness endpoints, startup/shutdown behavior, existing Terraform modules, Helm/manifests, scripts, CI configuration, tests, and documentation.
3. Inspect the architecture and backend contracts available in the repository.
4. Determine the actual deployable application services and their dependencies.
5. Determine each service's:

   * runtime command
   * container image
   * port
   * health endpoint
   * readiness endpoint
   * resource requirements
   * environment variables
   * secret/configuration requirements
   * startup dependencies
   * shutdown behavior
   * scaling characteristics
6. Determine which Kubernetes/EKS resources already exist.
7. Preserve compatible working infrastructure.
8. Reuse the foundational networking, IAM, KMS, environment, and naming conventions already established.
9. Do not invent application workloads that do not exist in the repository.
10. Do not redesign application architecture in this task.

This prompt is independently executable.

Do not depend on another AI conversation or on another prompt being pasted into the repository.

---

# INFRASTRUCTURE TARGET

The intended platform uses:

* AWS
* Amazon EKS
* Kubernetes
* Docker
* Terraform
* Helm
* GitHub Actions
* IAM workload identity
* private application networking
* AWS load balancing
* TLS
* containerized backend services
* supporting infrastructure established by the project architecture

This volume implements the **Kubernetes/EKS runtime platform**.

It does not complete all stateful data, observability, CI/CD/global delivery, or resilience work.

The infrastructure sequence remains exactly:

1. Infrastructure Volume 1 — Foundation
2. Infrastructure Volume 2 — Kubernetes/EKS
3. Infrastructure Volume 3 — Stateful Production Data
4. Infrastructure Volume 4 — Observability/Security Operations
5. Infrastructure Volume 5 — CI/CD and Global Delivery
6. Infrastructure Volume 6 — Capacity/Resilience/Day-2 Operations

---

# MISSION

Implement the production-grade Kubernetes/EKS platform required to run the application's containerized workloads.

This volume establishes:

* EKS cluster infrastructure
* cluster networking integration
* node infrastructure
* workload identity
* namespaces
* service accounts
* Helm chart structure
* application deployments
* services
* configuration and secrets wiring
* ingress/load-balancer boundary
* TLS boundary
* health/readiness/liveness behavior
* graceful shutdown
* pod disruption budgets
* resource requests/limits
* horizontal autoscaling foundations
* topology/availability controls
* Kubernetes network policies
* security contexts
* workload isolation
* service discovery
* deployment configuration
* release values
* cluster validation
* Kubernetes documentation

Do not implement the later centralized observability stack, complete CI/CD delivery pipelines, or the later resilience/capacity program here.

---

# PRIMARY SCOPE

## 1. EKS Cluster Architecture

Implement the EKS cluster infrastructure using Terraform and repository-compatible modules.

Establish:

* EKS cluster
* cluster IAM role
* control-plane configuration
* private cluster networking as appropriate
* Kubernetes version aligned with application/library compatibility
* control-plane logging configuration boundary where appropriate
* cluster endpoint access policy
* encryption configuration for Kubernetes secrets where appropriate
* cluster tags
* environment and region association

Do not hard-code a single environment or production region.

The configuration must support later extension to multiple environments and regions.

---

# 2. EKS Networking Integration

Integrate EKS with the foundational VPC from the previous infrastructure volume.

Support:

* private worker subnets
* appropriate public subnets for load-balancer-related resources where required by AWS architecture
* subnet tagging required by EKS/AWS load-balancing behavior
* security groups
* cluster/control-plane communication
* node-to-control-plane communication
* pod/service networking

Avoid broad unrestricted network access.

Do not expose the Kubernetes API publicly unless there is a documented operational reason and appropriate access controls.

Prefer private cluster access where the environment and deployment model permit it.

---

# 3. EKS Node Architecture

Implement worker-node infrastructure appropriate for the application.

Support:

* managed node groups and/or another repository-appropriate managed compute strategy
* architecture/instance-class configuration
* autoscaling boundaries
* node labels
* node taints where justified
* availability-zone distribution
* node IAM role
* security groups
* bootstrap configuration
* upgrade strategy boundaries

Separate workloads by meaningful characteristics when necessary, such as:

* general API workloads
* realtime/high-connection workloads
* asynchronous workers
* scheduled/background jobs

Do not create excessive node pools merely for categorization.

Do not claim a particular node count is capacity-tested.

---

# 4. Workload Identity

Implement secure AWS workload identity for Kubernetes workloads.

Use the repository's chosen mechanism, such as:

* EKS Pod Identity
* IRSA

Provide the foundation for workloads requiring controlled access to:

* S3
* Secrets Manager
* SSM Parameter Store
* KMS
* other AWS services explicitly required by application contracts

Use least-privilege IAM policies.

Do not attach broad account-level permissions to Kubernetes service accounts.

Do not distribute AWS access keys to pods.

---

# 5. Kubernetes Namespaces

Create clear namespace boundaries.

At minimum, establish a coherent pattern for:

* application workloads
* background workers/jobs
* platform components where required

Use separate namespaces where security, lifecycle, or operational isolation genuinely benefits from it.

Do not create a namespace per microservice unless the architecture specifically justifies it.

---

# 6. Service Accounts

Implement Kubernetes service accounts with:

* explicit names
* workload-specific IAM identity where required
* least privilege
* automount behavior consciously configured
* ownership labels

Do not allow unnecessary service-account token exposure.

Do not use the default service account for production workloads unless there is a deliberate reason.

---

# 7. Helm Architecture

Create or normalize Helm charts for the application's Kubernetes workloads.

Use a maintainable structure for:

* chart metadata
* values
* templates
* helpers
* environment overrides
* secrets/config references
* resource definitions
* deployment strategies

Avoid a single giant chart that cannot be maintained.

Avoid excessive chart duplication.

Use shared helpers for:

* labels
* naming
* annotations
* selectors
* common environment configuration

Do not make application charts depend on undocumented manual edits.

---

# 8. Environment Values

Establish explicit Helm values/configuration for:

* development
* test
* staging
* production

Where appropriate, define:

* image references
* replicas
* resources
* environment
* service type
* ingress behavior
* autoscaling boundaries
* topology settings
* security settings

Never commit actual production secrets.

Do not use one mutable values file that silently changes behavior between environments.

---

# 9. Application Deployments

Create Kubernetes Deployments or appropriate workload resources for the actual backend services in the repository.

For each service, configure:

* container image
* container port
* environment
* config references
* secret references
* resources
* security context
* probes
* lifecycle
* termination behavior
* rolling-update strategy
* replica configuration

Do not deploy services that do not exist.

Do not create fake placeholder services solely to demonstrate Kubernetes structure.

---

# 10. Background Workers and Jobs

Where the repository contains workers consuming:

* BullMQ
* Kafka/Redpanda
* scheduled jobs
* asynchronous workloads

deploy them using appropriate Kubernetes workload types.

Distinguish:

* long-running workers
* one-time jobs
* scheduled jobs

Use concurrency/resource settings compatible with actual application behavior.

Do not accidentally run a job as an endlessly replicated Deployment.

Do not create duplicate consumers without checking the application's consumer model.

---

# 11. Kubernetes Services

Create internal Services for application workloads.

Use appropriate service types:

* ClusterIP for internal services
* LoadBalancer only where explicitly required
* other types only when justified

Support:

* stable DNS names
* correct ports
* selectors
* readiness-aware traffic routing

Do not expose internal services publicly without a documented requirement.

---

# 12. Ingress and Load-Balancer Boundary

Implement the Kubernetes ingress/load-balancing architecture appropriate to the AWS environment.

Where repository-compatible, use:

* AWS Load Balancer Controller
* Application Load Balancer and/or Network Load Balancer
* Ingress resources
* target-group configuration

The architecture must support:

* HTTP/HTTPS routing
* service routing
* websocket traffic where required
* health checks
* connection behavior appropriate to realtime workloads

Do not hard-code production hostnames unless they are configuration inputs.

Do not attempt to complete the global DNS/WAF/edge architecture here; that belongs to a later infrastructure volume.

---

# 13. TLS Boundary

Establish the Kubernetes-side TLS architecture.

Where appropriate, support:

* ACM certificate references
* HTTPS listener configuration
* TLS termination
* secure redirects
* internal versus external TLS boundaries

Do not commit private certificates or private keys.

Do not fabricate certificate ARNs.

Use configuration inputs/references.

---

# 14. WebSocket Support

Ensure Kubernetes networking supports the platform's authenticated realtime workloads.

Configure where required:

* websocket upgrade
* load-balancer behavior
* connection timeouts
* service routing
* graceful termination
* readiness handling
* sufficient connection capacity

Do not treat websocket traffic exactly like ordinary short-lived HTTP requests.

Do not claim high concurrent connection capacity without testing it.

---

# 15. Health Checks

Configure Kubernetes health probes based on the actual application's health contracts.

Use:

* startup probes where application startup can be long
* readiness probes for traffic eligibility
* liveness probes only for genuine process-health conditions

Do not use arbitrary fixed sleep commands as health checks.

Probes must not create restart loops during legitimate dependency degradation.

Distinguish:

* process alive
* ready to receive traffic
* dependency healthy

according to application semantics.

---

# 16. Graceful Shutdown

Implement Kubernetes lifecycle behavior compatible with the application's graceful shutdown implementation.

Support:

* termination grace period
* pre-stop behavior where necessary
* connection draining
* websocket/session draining
* worker shutdown
* in-flight request completion
* queue-consumer shutdown

Do not use unnecessarily long or short termination windows without considering workload behavior.

Deployment configuration must avoid sending new traffic to pods that are shutting down.

---

# 17. Pod Disruption Budgets

Implement PodDisruptionBudgets for workloads where availability requires protection during:

* node drains
* cluster maintenance
* rolling upgrades
* voluntary disruptions

Use sensible availability constraints.

Do not create PDBs so restrictive that normal cluster maintenance becomes impossible.

---

# 18. Resource Requests and Limits

Define CPU/memory requests and limits for workloads based on actual application characteristics and documented starting assumptions.

Separate:

* baseline requested resources
* maximum resources
* environment-specific values

Do not use unlimited resources.

Do not pretend that these resource sizes are capacity-tested.

Document that production resource values may require tuning after measured load.

---

# 19. Horizontal Pod Autoscaling Foundation

Implement HPA where application workloads are suitable for horizontal scaling.

Support:

* minimum replicas
* maximum replicas
* CPU/memory metrics where appropriate
* behavior/stabilization settings
* scale-up limits
* scale-down controls

For services whose real scaling depends on:

* connection count
* queue depth
* Kafka lag
* custom metrics

establish a clear extension boundary rather than inventing unsupported metrics.

Do not blindly autoscale stateful or singleton workloads.

---

# 20. Topology and Availability

Configure workload placement to improve availability.

Where appropriate use:

* topology spread constraints
* pod anti-affinity
* zone-aware scheduling
* node selectors
* tolerations

Ensure replicas can distribute across availability zones when the node architecture supports it.

Do not force impossible scheduling constraints for development environments.

---

# 21. Kubernetes Network Policies

Implement NetworkPolicy controls where supported by the selected CNI/environment.

Use least-privilege communication.

Define intended communication paths for:

* ingress to public APIs
* API-to-database dependencies
* API-to-Redis
* API-to-Kafka/Redpanda
* API-to-search
* worker-to-queue infrastructure
* worker-to-storage/services
* internal service-to-service communication

Default-deny patterns may be used where compatible, followed by explicit allowed traffic.

Do not create policies that accidentally block required DNS or cluster-critical traffic.

---

# 22. Security Contexts

Apply production security contexts.

Where compatible:

* non-root user
* non-root group
* read-only root filesystem where practical
* drop unnecessary Linux capabilities
* seccomp profile
* privilege escalation disabled
* filesystem permissions appropriate to the runtime

Do not force read-only filesystems onto applications that genuinely require writable temporary storage without providing an approved ephemeral location.

---

# 23. Pod-Level Security

Implement Kubernetes pod security controls appropriate to the environment.

Support:

* Pod Security Standards or equivalent
* namespace security labels where applicable
* restricted security posture where compatible
* controlled exception boundaries for workloads that genuinely require elevated permissions

Do not disable Kubernetes security enforcement simply to make a workload start.

If a workload requires an exception, document the reason.

---

# 24. Secrets and Configuration Integration

Integrate workloads with the secrets/configuration architecture established previously.

Where appropriate use:

* Secrets Manager
* SSM Parameter Store
* External Secrets-compatible architecture
* Kubernetes Secrets only when necessary and appropriately protected

Do not place secret values in:

* Helm values committed to git
* Docker images
* ConfigMaps
* source code
* Terraform outputs unnecessarily

Separate sensitive values from ordinary configuration.

---

# 25. ConfigMaps and Non-Secret Configuration

Use ConfigMaps or equivalent configuration mechanisms for non-sensitive runtime configuration.

Possible values:

* environment
* service URLs
* feature/config references
* logging level
* public provider settings
* operational limits

Do not place credentials or tokens in ConfigMaps.

Avoid embedding large configuration documents unnecessarily.

---

# 26. Service Discovery and Dependency Configuration

Use Kubernetes DNS/service discovery appropriately.

Ensure application configuration can reference:

* internal services
* namespace-qualified services where required
* external AWS service endpoints
* database endpoints
* Redis endpoints
* Kafka/Redpanda endpoints
* search endpoints

Do not hard-code dynamically created cluster IP addresses.

---

# 27. Deployment Strategy

Implement safe rolling deployment defaults.

Support:

* max unavailable
* max surge
* readiness-aware rollout
* revision history
* rollback-compatible configuration
* image pull behavior

Do not introduce zero-downtime claims without ensuring:

* sufficient replicas
* readiness correctness
* compatible termination
* application backward compatibility

Deployment configuration must be consistent with application behavior.

---

# 28. Image Pull and Registry Integration

Prepare Kubernetes workloads to pull images securely from the repository's selected registry.

Where AWS-native:

* Amazon ECR integration boundary
* appropriate node/workload IAM
* image references
* pull policies

Do not hard-code credentials into Kubernetes manifests.

Do not create fake images.

---

# 29. Cluster Add-On Boundaries

Establish only the cluster add-ons required by this scope.

Potential components include:

* AWS Load Balancer Controller
* External Secrets integration
* metrics-server or equivalent metrics provider required by HPA
* EBS/EFS CSI drivers where actual workloads require them
* other foundational components explicitly required by the application

For each:

* pin a compatible version
* configure securely
* define ownership
* document why it is required

Do not install every available Kubernetes add-on.

---

# 30. Stateful Application Boundary

The application workloads must connect to stateful services such as:

* PostgreSQL
* Redis
* Kafka/Redpanda
* OpenSearch

Use external/managed service endpoints as appropriate.

Do not create production StatefulSets for these systems in this volume when the architecture has an infrastructure-managed or managed-service strategy.

The detailed production stateful-data infrastructure belongs to Infrastructure Volume 3.

---

# 31. Namespaces, Labels, and Ownership

Apply consistent metadata to Kubernetes resources.

At minimum include appropriate:

* app
* component
* service
* environment
* version
* managed-by
* owner/team
* region where useful

Ensure selectors remain stable across releases.

Do not put sensitive information into labels or annotations.

---

# 32. Runtime Security

Configure runtime security appropriate to the workload.

Consider:

* non-root execution
* read-only filesystem
* capability dropping
* seccomp
* network policies
* service-account restrictions
* resource quotas where appropriate
* namespace-level controls

Do not use privileged containers unless explicitly required and documented.

---

# 33. Namespace Resource Governance

Where justified, implement:

* ResourceQuota
* LimitRange
* pod count limits
* CPU/memory guardrails

Avoid constraints that make normal development impossible.

Production and non-production defaults may differ.

---

# 34. Kubernetes RBAC

Implement least-privilege Kubernetes RBAC for:

* workloads
* platform components
* deployment/service accounts
* operators/controllers where required

Do not give application workloads cluster-admin privileges.

Do not use broad ClusterRoleBindings unnecessarily.

Avoid embedding human identity management into application manifests.

---

# 35. Cluster Access Boundary

Document and configure the administrative access boundary for EKS.

Support where appropriate:

* AWS IAM to Kubernetes access
* EKS access entries
* role-based administrative access
* read-only operational access
* deployment identity

Do not create permanent shared admin credentials.

Do not commit kubeconfigs containing credentials.

---

# 36. Operational Annotations and Metadata

Add only useful annotations for:

* load balancer behavior
* TLS
* rollout behavior
* external secrets
* workload identity
* service integration
* operational metadata

Do not add unexplained annotations copied from unrelated examples.

Document non-obvious annotations.

---

# 37. Deployment Validation

Implement repository-side validation for:

* Terraform
* Helm
* Kubernetes manifests
* policy configuration
* YAML
* templates

Use:

* `terraform fmt`
* `terraform validate`
* Helm lint
* Helm template rendering
* Kubernetes schema validation
* static analysis
* security scanning

Use repository-supported tooling where already available.

---

# 38. Local Kubernetes Development

Where useful and compatible with the repository, provide a local Kubernetes path using a tool such as:

* kind
* minikube
* k3d
* another repository-compatible local cluster

The local environment should validate:

* Helm rendering
* service discovery
* configuration wiring
* readiness
* deployment lifecycle
* networking

Do not require local Kubernetes for ordinary development if Docker Compose remains the simpler supported workflow.

---

# 39. Testing

Implement meaningful infrastructure tests.

Cover:

### Terraform

* EKS module inputs
* outputs
* IAM roles/policies
* networking references
* environment configuration

### Helm

* chart lint
* rendered manifests
* values overrides
* environment differences
* required fields

### Kubernetes

* schema validity
* selectors
* probes
* resources
* security contexts
* RBAC
* network policies
* PDBs
* HPA configuration

### Local Cluster

Where feasible:

* pod scheduling
* readiness
* service discovery
* rolling update
* termination behavior

Use static or mocked validation when external cluster access is unavailable.

Do not claim cluster-level validation that was not actually executed.

---

# 40. Documentation

Create or update Kubernetes/EKS documentation covering:

* cluster architecture
* Terraform structure
* cluster access
* namespaces
* workload identity
* Helm charts
* application deployments
* ingress
* TLS
* websocket handling
* probes
* graceful shutdown
* PDBs
* HPA
* network policies
* security contexts
* RBAC
* secrets/configuration
* local Kubernetes development
* validation
* external infrastructure limitations
* troubleshooting basics

Documentation must distinguish:

* repository-defined configuration
* locally validated behavior
* actually deployed AWS behavior

---

# OUT OF SCOPE

Do not implement the later infrastructure scopes in this volume.

Explicitly out of scope:

* detailed production PostgreSQL/RDS architecture
* PostgreSQL backup/PITR implementation
* production Redis cluster/replication architecture
* production Kafka/Redpanda cluster architecture
* production OpenSearch cluster architecture
* detailed S3 lifecycle/DR hardening beyond the foundational layer already established
* observability platform
* Prometheus
* Grafana
* Loki
* Tempo
* complete OpenTelemetry collector deployment
* centralized security monitoring
* CI/CD pipeline implementation
* GitHub Actions deployment workflow
* ECR build/release automation
* Route 53 global DNS architecture
* CloudFront/global edge architecture
* WAF architecture
* multi-region traffic failover
* disaster-recovery execution
* load/capacity testing program
* resilience drills
* day-2 operational runbooks
* backend code changes unrelated to Kubernetes compatibility
* frontend implementation
* mobile implementation
* separate QA phase
* separate final-integration phase

Do not create additional infrastructure volumes.

The next volume is **Infrastructure Volume 3 — Stateful Production Data**.

---

# IMPLEMENTATION RULES

## Repository First

Inspect before modifying.

Determine the actual:

* deployable services
* runtime commands
* ports
* probes
* environment variables
* secrets
* dependencies
* Docker images
* health endpoints
* worker types
* shutdown behavior

Do not invent workloads.

## Preserve Volume 1

Reuse and extend:

* VPC
* subnets
* security groups
* IAM
* KMS
* environment model
* naming
* tagging
* secret/configuration boundaries

Do not create conflicting parallel foundations.

## Infrastructure as Code

Kubernetes/EKS infrastructure must be represented in Terraform/Helm/manifests/scripts as appropriate.

Do not rely on undocumented manual cluster configuration.

Where bootstrapping requires an external step:

* document it
* provide repository-side configuration
* do not claim it was executed unless it was

## Security

Use:

* least privilege
* workload identity
* non-root containers
* secure network policies
* controlled RBAC
* encrypted secrets/configuration

Do not distribute AWS credentials to pods.

## Production Runtime

Configure:

* readiness
* liveness/startup probes
* resources
* graceful shutdown
* rolling updates
* PDBs
* autoscaling
* topology distribution

Do not claim these settings guarantee zero downtime under all conditions.

## No Fake Infrastructure

Do not create fake:

* services
* images
* clusters
* certificates
* secrets
* AWS resources
* deployment results

Do not report a workload as deployed when only manifests were generated.

## Environment-Aware Execution

The implementation agent may not have:

* AWS credentials
* EKS access
* kubectl access
* external registry access
* cluster-admin permissions

When external execution is unavailable:

* implement the repository artifacts
* validate Terraform/Helm/manifests statically
* use local Kubernetes where possible
* report unavailable external validation honestly

## No Pseudo-Code

Create actual:

* Terraform
* Helm charts
* Kubernetes manifests
* RBAC
* policies
* configuration
* validation scripts
* documentation

Do not use placeholder YAML presented as production-ready implementation.

---

# VALIDATION REQUIREMENTS

Before considering this volume complete:

1. Inspect all current infrastructure and application deployment requirements.
2. Run Terraform formatting.
3. Run Terraform validation.
4. Run Terraform static analysis available in the repository.
5. Run infrastructure security scanning available in the repository.
6. Validate EKS Terraform dependencies.
7. Validate IAM/workload-identity configuration.
8. Lint all Helm charts.
9. Render all relevant Helm templates for each configured environment.
10. Validate rendered Kubernetes manifests against schemas.
11. Validate Kubernetes RBAC.
12. Validate NetworkPolicies.
13. Validate security contexts.
14. Validate resource requests/limits.
15. Validate startup/readiness/liveness probes.
16. Validate PDBs.
17. Validate HPA configuration.
18. Validate topology/spread constraints.
19. Validate service selectors/ports.
20. Validate ingress/load-balancer configuration.
21. Validate TLS references/configuration.
22. Validate websocket routing configuration where applicable.
23. Validate secrets/configuration references.
24. Validate workload IAM bindings.
25. Validate namespace/resource-governance configuration.
26. Build relevant container images where possible.
27. Start a local Kubernetes cluster where practical.
28. Deploy rendered manifests/charts to the local cluster where practical.
29. Verify pods schedule.
30. Verify readiness.
31. Verify service discovery.
32. Verify rolling-update behavior.
33. Verify graceful termination behavior.
34. Verify no public exposure exists for internal stateful services.
35. Verify no production secrets are committed.
36. Verify no kubeconfigs or credentials are committed.
37. Verify documentation commands remain accurate.
38. Verify no later infrastructure scope was unnecessarily implemented.

If AWS/EKS access is unavailable:

* perform all repository-side validation possible
* render and schema-validate manifests
* use local Kubernetes where feasible
* explicitly state which cloud validations were not executed

Never claim:

* EKS cluster creation
* pod deployment to AWS
* AWS load-balancer provisioning
* ACM certificate validation
* production autoscaling
* production websocket capacity

unless those actions were actually performed and verified.

---

# INTEGRATION CHECK

Before finalizing, verify that the Kubernetes/EKS layer integrates cleanly with Infrastructure Volume 1 and the application repository.

Confirm that:

* EKS uses the foundational VPC and subnet architecture
* node security groups are compatible with the network foundation
* workload IAM uses the established IAM/KMS model
* secrets/configuration use the established boundaries
* container images match actual application services
* service ports match actual containers
* probes match actual health/readiness endpoints
* graceful shutdown matches application behavior
* Kubernetes service discovery matches application dependencies
* internal stateful-service endpoints remain private
* application workloads can reach required dependencies through intended network paths
* websocket workloads have appropriate service/load-balancer behavior
* HPA/PDB/topology settings do not conflict
* Kubernetes RBAC does not grant unnecessary privilege
* network policies allow required application traffic
* Helm configuration can be extended by later infrastructure volumes
* the stateful-data architecture in Volume 3 can be consumed without redesigning the application deployment model
* later observability can instrument these workloads without changing their core deployment structure
* later CI/CD can deploy these charts/manifests without restructuring the platform

Do not introduce temporary Kubernetes architecture that the next infrastructure volumes must replace.

---

# DEFINITION OF DONE

This volume is complete only when:

* EKS Terraform is implemented
* EKS networking integration is implemented
* node infrastructure is implemented
* workload identity is implemented
* namespaces are implemented
* service accounts are implemented
* Helm chart architecture is implemented
* environment values are implemented
* application deployments are implemented for actual repository services
* worker/job workloads are implemented where required
* Kubernetes Services are implemented
* ingress/load-balancer boundary is implemented
* TLS integration boundary is implemented
* websocket support is configured where required
* health probes are implemented
* graceful shutdown is configured
* PDBs are implemented where justified
* resource requests/limits are defined
* HPA is implemented where justified
* topology/availability controls are implemented
* NetworkPolicies are implemented
* security contexts are implemented
* pod security controls are implemented
* secrets/configuration integration is implemented
* ConfigMaps are implemented where appropriate
* service discovery is implemented
* rolling deployment configuration is implemented
* registry integration boundary is implemented
* required cluster add-ons are defined
* application/stateful-service boundaries are correct
* labels/ownership metadata are consistent
* namespace resource governance is implemented where justified
* Kubernetes RBAC is implemented
* cluster access boundaries are documented/configured
* local Kubernetes validation path exists where useful
* infrastructure tests are implemented
* documentation is updated
* validation has been performed
* unavailable external validation is honestly reported
* no production secrets are committed
* no fake AWS/EKS deployment is reported
* no placeholder infrastructure remains
* no later infrastructure scope was unnecessarily implemented

---

# IMPLEMENTATION REPORT

At the end of execution, provide a concise report containing:

## Files Changed

List created, modified, and removed infrastructure files.

## EKS/Kubernetes Implemented

Summarize:

* EKS
* networking
* nodes
* workload identity
* namespaces
* Helm
* deployments
* services
* ingress
* TLS
* probes
* shutdown
* PDBs
* HPA
* topology
* NetworkPolicies
* security contexts
* secrets/configuration
* RBAC

## Workloads Deployed

List the actual application workloads represented in the Kubernetes configuration.

Do not list hypothetical workloads.

## Validation

Report the exact commands executed and their results.

## External Infrastructure Status

Clearly state which EKS/AWS operations were actually performed and which could not be performed due to environment limitations.

Do not claim deployment from static validation alone.

## Follow-Up Dependencies

Identify what Infrastructure Volume 3 must integrate with, especially the production stateful data services.

Do not invent additional infrastructure phases.

---

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement the complete Kubernetes/EKS infrastructure scope defined by this prompt.

Preserve all working application and infrastructure behavior outside the necessary scope of these changes.

Extend the foundational infrastructure from Infrastructure Volume 1 rather than replacing it with a parallel design.

Create the real Terraform, Helm, Kubernetes manifests, IAM/workload-identity configuration, network policies, security configuration, validation tooling, tests, and documentation required for this scope.

Do not merely describe the infrastructure.

Do not wait for another prompt.

Do not use pseudo-code, placeholder manifests, fake workloads, fabricated images, fake secrets, fake certificates, fake cluster outputs, or simulated deployment success.

When AWS/EKS access is unavailable, fully implement the repository-side infrastructure and validate it statically and locally as far as possible.

Respect least privilege, private networking, workload identity, secure pod execution, graceful shutdown, availability-zone distribution, and controlled autoscaling.

Finish only when this Kubernetes/EKS volume is genuinely implemented, validated, documented, and ready for Infrastructure Volume 3 to extend the platform with production stateful data infrastructure.
