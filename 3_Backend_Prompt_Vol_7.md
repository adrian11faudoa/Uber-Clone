You are operating in Senior Engineering Team Mode.

Complete the remaining production-ready backend for analytics, administration, moderation, feature flags, dynamic configuration, audit, privacy workflows, reconciliation, cross-domain integration, security hardening, and operational readiness for an enterprise-scale global ride-hailing and mobility platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

The backend must follow the approved Uber-like architecture, domain boundaries, database ownership, API contracts, event architecture, queue architecture, Redis strategy, geospatial architecture, dispatch architecture, trip architecture, financial architecture, safety architecture, fraud architecture, support architecture, business-account architecture, security model, and Project Index.

Do not redesign the architecture.

Do not generate frontend code.

Do not generate mobile code.

Do not generate infrastructure implementation code.

Do not generate Terraform.

Do not generate Kubernetes manifests.

Do not generate CI/CD workflows.

────────────────────────────────────────

MISSION

Complete the enterprise backend systems required for:

• Operational analytics
• Business analytics
• Driver analytics
• Rider analytics
• Dispatch analytics
• Matching analytics
• Location analytics
• ETA analytics
• Trip analytics
• Pricing analytics
• Promotion analytics
• Payment analytics
• Earnings analytics
• Payout analytics
• Safety analytics
• Fraud analytics
• Support analytics
• Business-account analytics
• Administration
• Moderation
• Feature flags
• Dynamic configuration
• Audit
• Privacy requests
• Data export
• Data deletion workflows
• Reconciliation
• Cross-domain health validation
• Security hardening
• Production-readiness checks

The implementation must support:

• Hundreds of millions of riders
• Millions of drivers
• Millions of vehicles
• Millions of trips
• Massive event volumes
• High administrative workloads
• Large support workloads
• Large fraud workloads
• Large analytics volumes
• Multiple business organizations
• Multiple regions
• Strict privacy
• Strict security
• High availability
• Strong auditability

────────────────────────────────────────

TECHNOLOGY STACK

Backend:

• Node.js
• NestJS
• TypeScript

Database:

• PostgreSQL
• Prisma ORM
• PostGIS where appropriate

Cache:

• Redis

Event streaming:

• Kafka or Redpanda

Background processing:

• BullMQ

Search:

• Elasticsearch/OpenSearch

Object storage:

• AWS S3-compatible object storage

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

Testing:

• Jest
• Supertest
• Integration and contract testing

────────────────────────────────────────

IMPLEMENTATION RULES

Never generate pseudo-code.

Never generate placeholders.

Never generate TODO comments.

Never omit implementations.

Never say:

- "implement similarly"
- "left as an exercise"
- "for brevity"
- "remaining code omitted"

Every generated file must be complete.

Every generated file must compile.

Never regenerate unchanged files.

Only modify existing files when required.

Use strict TypeScript.

Use dependency injection.

Keep controllers thin.

Keep business logic outside controllers.

Use repositories for persistence.

Use DTOs for external contracts.

Use centralized validation.

Use centralized error handling.

Use structured logging.

Every administrative mutation must be auditable.

Every privacy workflow must be idempotent.

Analytics processing must not block transactional requests.

────────────────────────────────────────

DOMAIN OWNERSHIP

Maintain explicit boundaries between:

• Operational analytics
• Analytical aggregation
• Administration
• Moderation
• Feature flags
• System configuration
• Audit
• Privacy
• Reconciliation

Do not combine:

• Analytical records with transactional business state
• Audit logs with ordinary application logs
• Feature flags with authorization
• Privacy-deletion logic with uncontrolled physical deletion
• Administrative data with user-facing data

────────────────────────────────────────

ANALYTICS INGESTION

Implement production-ready analytics event ingestion.

Accept events representing:

• Ride requests
• Driver offers
• Matching
• Assignments
• Driver locations where approved
• Trip lifecycle
• Fare calculations
• Promotions
• Payments
• Refunds
• Earnings
• Payouts
• Ratings
• Reviews
• Messaging
• Notifications
• Safety
• Fraud
• Support
• Business trips

All analytics events must use the established event envelope.

────────────────────────────────────────

ANALYTICS EVENT VALIDATION

Validate:

• Event type
• Version
• Producer
• Timestamp
• Entity reference
• Region
• Correlation ID
• Payload schema

Reject malformed events.

Do not allow analytics payloads to become an arbitrary data-ingestion surface.

────────────────────────────────────────

ANALYTICS PIPELINE

Implement the backend architecture:

Application
→ Event
→ Kafka/Redpanda
→ Validation
→ Processing
→ Aggregation
→ Analytical storage
→ Reporting

Do not synchronously calculate large analytical metrics during transactional API requests.

────────────────────────────────────────

ANALYTICS RETENTION

Define retention for:

• Raw operational events
• Aggregated metrics
• User-level analytics
• Driver analytics
• Business analytics
• Safety analytics
• Fraud analytics
• Support analytics

Apply privacy and retention policies.

────────────────────────────────────────

OPERATIONAL METRICS

Support analytics for:

• Ride-request rate
• Matching success
• Matching latency
• Offer acceptance
• Assignment failure
• Driver supply
• Rider demand
• ETA
• Cancellation
• Completion
• Active trips
• Regional utilization

Provide time-windowed aggregation.

────────────────────────────────────────

DRIVER ANALYTICS

Support:

• Online time
• Available time
• Trips
• Acceptance rate
• Cancellation rate
• Earnings
• Incentives
• Payouts
• Rating
• Utilization

Only expose a driver’s own private analytics unless authorized.

────────────────────────────────────────

RIDER ANALYTICS

Support:

• Ride requests
• Completed trips
• Cancellation
• Spend
• Promotions
• Loyalty/retention signals where approved

Do not expose individual behavioral analytics to unauthorized users.

────────────────────────────────────────

BUSINESS ANALYTICS

Support:

• Business rides
• Spend
• Cost centers
• Policy violations
• Employee usage
• Trips by region
• Billing summaries

Business users must only see authorized organization data.

────────────────────────────────────────

SAFETY ANALYTICS

Track aggregated:

• Incident volume
• Incident type
• Severity
• Response time
• Resolution time
• Region
• Trip category

Do not expose sensitive case details through aggregate dashboards unless authorized.

────────────────────────────────────────

FRAUD ANALYTICS

Track:

• Risk evaluations
• Risk decisions
• Fraud cases
• Fraud trends
• False-positive rates
• Appeal outcomes

Sensitive risk data remains restricted.

────────────────────────────────────────

SUPPORT ANALYTICS

Track:

• Case volume
• Category
• Priority
• SLA
• Resolution time
• Reopen rate
• Escalation

Support analytics must not reveal private case contents unnecessarily.

────────────────────────────────────────

REPORTING

Implement asynchronous report generation.

Support:

• Report type
• Scope
• Filters
• Time range
• Region
• Organization
• Status
• Requested by
• Output format
• Expiration

Use BullMQ.

Store generated artifacts in secure object storage.

────────────────────────────────────────

REPORT SECURITY

Reports must:

• Be scoped to the requester
• Use short-lived download authorization
• Expire
• Be auditable
• Avoid publicly accessible object URLs

Administrators must not automatically gain unrestricted access to all reports.

────────────────────────────────────────

ADMINISTRATION

Implement the backend administration platform.

Support administrative management of:

• Riders
• Drivers
• Vehicles
• Trips
• Ride requests
• Dispatch
• Pricing
• Promotions
• Payments
• Refunds
• Wallets
• Earnings
• Payouts
• Ratings
• Reviews
• Messaging
• Notifications
• Safety
• Fraud
• Support
• Business accounts
• Analytics
• Feature flags
• System configuration
• Audit
• Privacy requests

────────────────────────────────────────

ADMINISTRATIVE ROLES

Support roles such as:

• Support Agent
• Verification Agent
• Safety Agent
• Fraud Analyst
• Finance Analyst
• Operations Manager
• Business Administrator
• Content/Moderation Agent
• System Administrator
• Security Administrator
• Super Administrator

Apply least privilege.

────────────────────────────────────────

ADMIN PERMISSION MODEL

Permissions should distinguish:

• Read
• Create
• Update
• Suspend
• Delete/retire
• Refund
• Financial adjustment
• Security action
• Configuration change
• Feature-flag change
• Audit access
• Privacy access

Do not give broad access merely because someone has an administrative role.

────────────────────────────────────────

SENSITIVE ADMIN ACTIONS

Require stronger controls for:

• Refunds
• Wallet adjustments
• Earnings adjustments
• Payout intervention
• Driver suspension
• Account suspension
• Safety actions
• Fraud restrictions
• Rights/availability overrides
• Feature kill switches
• System configuration
• Permission changes
• Privacy operations

Support:

• Reason
• Actor
• Request ID
• Confirmation
• Audit
• Additional approval where configured

────────────────────────────────────────

MODERATION

Complete backend moderation workflows for:

• Ratings
• Reviews
• Messages
• Driver profiles
• Rider profiles
• Support content
• Business content
• User reports

Support:

• Case
• Subject
• Policy
• Evidence
• Action
• Appeal
• Resolution
• Audit

────────────────────────────────────────

MODERATION STATES

Support:

• Reported
• Queued
• Assigned
• Investigating
• Action Required
• Action Taken
• Appealed
• Resolved
• Closed
• Reopened

────────────────────────────────────────

FEATURE FLAGS

Implement dynamic feature flags.

Support:

• Boolean flags
• Percentage rollout
• Region
• City
• User
• Driver
• Business organization
• Ride category
• Application version
• Platform
• Environment

Define:

• Evaluation
• Caching
• Propagation
• Versioning
• Audit
• Expiration

Feature flags must not replace authorization or safety controls.

────────────────────────────────────────

FEATURE FLAG ROLLOUT

Support:

• Dark launch
• Canary
• Percentage rollout
• Region rollout
• Emergency kill switch
• Rollback

Every flag change must be auditable.

────────────────────────────────────────

SYSTEM CONFIGURATION

Implement typed dynamic configuration.

Support configuration for:

• Pricing thresholds
• Surge limits
• Dispatch parameters
• Matching parameters
• Offer timeout
• Driver eligibility
• Notification limits
• Fraud thresholds
• Support SLA
• Safety policies
• Rate limits
• Feature defaults

Configuration values must be:

• Typed
• Validated
• Versioned
• Audited
• Rollback-capable

Never allow arbitrary executable configuration.

────────────────────────────────────────

CONFIGURATION VERSIONING

Every configuration version includes:

• Configuration key
• Version
• Value
• Environment
• Region where applicable
• Effective timestamp
• Expiration timestamp
• Created by
• Approved by
• Status

Support:

• Draft
• Approved
• Active
• Superseded
• Rolled back

────────────────────────────────────────

AUDIT

Implement immutable audit records.

Audit:

• Administrative actions
• Permission changes
• Driver actions
• Safety actions
• Fraud actions
• Financial adjustments
• Refunds
• Payout interventions
• Configuration changes
• Feature-flag changes
• Privacy requests
• Data exports
• Deletion workflows

Store:

• Actor
• Role
• Action
• Resource type
• Resource ID
• Reason
• Request ID
• Correlation ID
• Region
• Timestamp
• Result

Never store secrets.

────────────────────────────────────────

AUDIT ACCESS

Audit records must:

• Be immutable
• Be append-only
• Be searchable
• Support pagination
• Support filtering
• Have restricted access

Ordinary administrators must not delete audit records.

────────────────────────────────────────

PRIVACY REQUESTS

Implement privacy workflows for:

• Data export
• Data access
• Data deletion
• Account closure
• Data-retention enforcement

Classify data into:

• User-owned data
• Operational data
• Analytics data
• Financial/legal-retention data
• Audit data
• Security data

Do not indiscriminately delete data required for legal, financial, fraud, safety, or audit obligations.

────────────────────────────────────────

DATA EXPORT

Implement asynchronous export.

Support:

• Request
• Scope
• Status
• Progress
• Secure artifact
• Expiration
• Download authorization

Use BullMQ.

Exports must not expose another user’s data.

────────────────────────────────────────

DATA DELETION

Implement controlled deletion/anonymization workflows.

Support:

• Request
• Validation
• Dependency analysis
• De-identification
• Deletion
• Verification
• Completion

Some records may require:

• Retention
• Pseudonymization
• Restricted archival

Do not physically delete financial/audit records when retention obligations prohibit it.

────────────────────────────────────────

PRIVACY RECONCILIATION

After deletion/export jobs, verify:

• User-account data
• Profile data
• Device data
• Trip references
• Analytics references
• Support references
• Notification data

Remain consistent with approved retention policies.

────────────────────────────────────────

CROSS-DOMAIN RECONCILIATION

Implement reconciliation jobs for:

IDENTITY

• User/account/profile consistency

DRIVERS

• Driver eligibility
• Verification
• Vehicle compliance

AVAILABILITY

• Online status
• Active driver state

TRIPS

• Assignment
• Trip state
• Driver state

FINANCE

• Payment
• Fare
• Wallet
• Earnings
• Payout

PROMOTIONS

• Redemption
• Campaign state

SAFETY

• Incident references

SUPPORT

• Trip/payment case references

BUSINESS

• Organization/member/policy consistency

ANALYTICS

• Event processing lag
• Aggregate consistency

Reconciliation must detect mismatches without unsafe automatic destructive correction.

────────────────────────────────────────

CROSS-DOMAIN HEALTH

Create operational health checks covering:

• PostgreSQL
• PostGIS
• Redis
• Kafka
• BullMQ
• Search
• Object storage
• Maps provider
• Payment provider
• Notification providers

Separate:

• Liveness
• Readiness
• Dependency health
• Functional health

────────────────────────────────────────

SECURITY HARDENING

Perform a final backend security review.

Validate:

AUTHENTICATION

• Password security
• Session security
• Token handling
• MFA architecture
• Device authentication

AUTHORIZATION

• RBAC
• Resource ownership
• Rider scope
• Driver scope
• Business scope
• Admin scope

API

• Input validation
• Rate limiting
• Secure headers
• Error handling
• Request-size limits
• Timeout handling

REAL-TIME

• WebSocket authentication
• Room authorization
• Connection limits
• Message validation

FINANCE

• Webhook verification
• Idempotency
• Provider-reference validation

LOCATION

• Location access controls
• Privacy
• Retention
• Auditing

────────────────────────────────────────

ABUSE PREVENTION

Final architecture must mitigate:

• Fake accounts
• Fake drivers
• GPS spoofing
• Driver/rider collusion
• Trip manipulation
• Payment abuse
• Promotion abuse
• Referral abuse
• Refund abuse
• Account takeover
• API flooding
• WebSocket abuse
• Notification abuse
• Support abuse

Use:

• Rate limits
• Risk signals
• Behavioral controls
• Device controls
• Account controls
• Audit

────────────────────────────────────────

PERFORMANCE REVIEW

Review all critical paths:

• Authentication
• Driver availability
• Location
• Nearby-driver search
• Ride request
• Matching
• Assignment
• Trip-state update
• Fare estimation
• Payment
• Wallet
• Payout
• Notifications
• Support
• Business policy
• Analytics ingestion

Identify:

• N+1 queries
• Hot keys
• Hot partitions
• Long transactions
• Blocking operations
• Excessive synchronous calls
• Inefficient pagination

────────────────────────────────────────

DATA CONSISTENCY REVIEW

Verify strong consistency where required for:

• Driver assignment
• Trip state
• Financial ledger
• Payment state
• Wallet
• Earnings
• Payouts
• Authorization decisions

Use eventual consistency where appropriate for:

• Analytics
• Search
• Dashboards
• Recommendations
• Notifications
• Derived operational views

────────────────────────────────────────

EVENT CONSISTENCY REVIEW

Validate:

• Event versions
• Producer ownership
• Consumer ownership
• Schema compatibility
• Ordering
• Partition keys
• Retry
• Dead-letter handling
• Replay
• Idempotency

No critical state transition may succeed without producing required durable events when the architecture depends on those events.

────────────────────────────────────────

API CONTRACT REVIEW

Audit:

• Naming
• Versioning
• Error format
• Authentication
• Authorization
• Pagination
• Cursor behavior
• Idempotency
• Request validation
• Response schema

Detect:

• Breaking changes
• Inconsistent contracts
• Missing authorization
• Missing validation

────────────────────────────────────────

DATABASE REVIEW

Audit:

• Indexes
• Constraints
• Foreign keys
• Transactions
• Isolation
• Partitioning
• Migration safety
• Connection pools
• Replica strategy
• Backup

Detect:

• N+1 queries
• Sequential scans
• Lock contention
• Deadlocks
• Connection exhaustion

────────────────────────────────────────

REDIS REVIEW

Audit:

• Key names
• TTL
• Memory
• Eviction
• Hot keys
• Distributed locks
• Failure behavior

Verify Redis is never authoritative for:

• Trips
• Payments
• Wallets
• Earnings
• Payouts
• Driver identity
• Financial state

────────────────────────────────────────

KAFKA REVIEW

Audit:

• Topic ownership
• Partitioning
• Retention
• Replication
• Consumer groups
• Lag
• Dead-letter topics
• Replay

Detect hot partitions.

────────────────────────────────────────

QUEUE REVIEW

Audit BullMQ queues for:

• Retry
• Backoff
• Timeout
• Concurrency
• Dead-letter behavior
• Poison-job handling
• Scaling

No queue should retry forever.

────────────────────────────────────────

OBSERVABILITY REVIEW

Ensure all critical workflows have:

• Structured logs
• Metrics
• Distributed traces
• Request IDs
• Correlation IDs
• Error tracking
• Latency tracking

Critical workflows:

• Authentication
• Driver verification
• Location
• Dispatch
• Matching
• Trip
• Pricing
• Payment
• Wallet
• Earnings
• Payout
• Safety
• Fraud
• Support
• Business
• Administration
• Privacy

────────────────────────────────────────

SLO / SLI

Define measurable SLOs for:

• Authentication
• Driver availability
• Location freshness
• Matching
• Assignment
• Trip-state propagation
• Fare estimation
• Payment
• Wallet
• Payout
• Notifications
• Support
• Business APIs
• Analytics ingestion

For every SLO define:

• SLI
• Source
• Target
• Alert threshold
• Error budget

────────────────────────────────────────

FINAL TESTING

UNIT TESTS

Cover:

• Analytics transformations
• Permission logic
• Moderation state
• Feature-flag evaluation
• Configuration validation
• Privacy workflow state
• Reconciliation rules

INTEGRATION TESTS

Cover:

• PostgreSQL
• PostGIS
• Redis
• Kafka
• BullMQ
• Search
• S3
• External providers

E2E TESTS

Cover:

• Customer journeys
• Driver journeys
• Business journeys
• Admin workflows
• Safety workflows
• Fraud workflows
• Privacy workflows

CONCURRENCY TESTS

Cover:

• Admin conflicts
• Configuration changes
• Feature flags
• Reconciliation races
• Privacy request duplication
• Report generation duplication

SECURITY TESTS

Cover:

• Admin escalation
• Cross-business access
• Privacy-data leakage
• Audit manipulation
• Configuration injection
• Feature-flag abuse

PERFORMANCE TESTS

Cover:

• Analytics ingestion
• Report generation
• Admin searches
• Audit searches
• Reconciliation workloads

────────────────────────────────────────

FINAL PROJECT READINESS

Perform a complete backend audit covering:

• Architecture conformance
• API correctness
• Database correctness
• Event correctness
• Queue correctness
• Security
• Privacy
• Performance
• Scalability
• Observability
• Reconciliation
• Disaster recovery readiness
• Operational readiness

Identify:

• Remaining defects
• Known risks
• Technical debt
• Scalability risks
• Security risks
• Operational risks

Do not declare production readiness unless required checks actually pass.

────────────────────────────────────────

DOCUMENTATION

Generate:

• Analytics architecture
• Reporting architecture
• Administration architecture
• Moderation architecture
• Feature-flag architecture
• Dynamic-configuration architecture
• Audit architecture
• Privacy architecture
• Data-export architecture
• Data-deletion architecture
• Reconciliation architecture
• Security-hardening guide
• API contract review
• Event catalog review
• Queue catalog review
• Database review
• Redis review
• Kafka review
• Observability review
• SLO/SLI guide
• Testing strategy
• Production-readiness checklist

────────────────────────────────────────

PROJECT INDEX

Update the backend Project Index with:

• Analytics
• Reporting
• Administration
• Moderation
• Feature flags
• System configuration
• Audit
• Privacy workflows
• Data export
• Data deletion
• Reconciliation
• Security hardening
• Performance review
• API review
• Event review
• Database review
• Redis review
• Kafka review
• Queue review
• Observability
• SLO/SLI
• Tests
• Generated files
• Modified files
• Remaining work
• Known risks
• Technical debt
• Current milestone
• Production-readiness status

────────────────────────────────────────

IMPLEMENTATION MILESTONES

BACKEND MILESTONE 61

Analytics ingestion, validation, event processing, aggregation, operational analytics, and analytics retention.

BACKEND MILESTONE 62

Driver, rider, trip, safety, fraud, support, and business analytics.

BACKEND MILESTONE 63

Asynchronous reporting, secure report storage, report authorization, expiration, and report processing.

BACKEND MILESTONE 64

Administration APIs, administrative roles, permissions, sensitive-action controls, and audit integration.

BACKEND MILESTONE 65

Moderation workflows, moderation cases, appeals, reports, evidence references, and audit.

BACKEND MILESTONE 66

Feature flags, rollout rules, kill switches, dynamic system configuration, versioning, approval, and rollback.

BACKEND MILESTONE 67

Privacy workflows, data export, data deletion/anonymization, retention enforcement, and privacy reconciliation.

BACKEND MILESTONE 68

Cross-domain reconciliation, integrity checks, dependency health, and operational diagnostics.

BACKEND MILESTONE 69

Final security hardening, API review, database review, Redis/Kafka/queue review, performance optimization, and observability validation.

BACKEND MILESTONE 70

Comprehensive E2E, concurrency, security, performance, resilience, privacy, recovery, and production-readiness validation.

Each milestone should contain approximately 20–40 files where practical.

Every milestone must compile before proceeding.

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never truncate code.

Never summarize source code instead of generating it.

Never generate pseudo-code.

Never generate placeholders.

Never generate TODO implementations.

When modifying an existing file:

1. Provide the exact file path.
2. State why it must change.
3. Provide the complete updated file.

Never regenerate unchanged files.

────────────────────────────────────────

SCOPE RESTRICTION

This volume covers:

• Analytics
• Reporting
• Administration
• Moderation
• Feature flags
• Dynamic configuration
• Audit
• Privacy workflows
• Data export
• Data deletion/anonymization
• Reconciliation
• Cross-domain health
• Security hardening
• Performance review
• API review
• Event review
• Database review
• Redis review
• Kafka review
• Queue review
• Observability review
• SLO/SLI
• Final backend testing
• Production-readiness validation

Do not redesign or reimplement previously completed domains.

Use the existing approved architecture and contracts.

Do not implement:

• Frontend
• Mobile
• Infrastructure
• Terraform
• Kubernetes
• CI/CD

────────────────────────────────────────

QUALITY BAR

Treat this as the final enterprise backend completion and hardening stage.

Assume:

• Hundreds of millions of riders
• Millions of drivers
• Massive trip volume
• Massive telemetry volume
• High financial volume
• Multiple regions
• Large business customers
• Strict privacy
• Strict security
• High availability
• Disaster recovery
• Continuous deployments

Prioritize:

• Correctness
• Security
• Privacy
• Financial integrity
• Trip integrity
• Data integrity
• Reconciliation
• Observability
• Scalability
• Resilience
• Auditability
• Maintainability
• Production readiness
