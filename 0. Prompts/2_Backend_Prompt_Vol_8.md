# Uber-Style Global Ride-Hailing & Mobility Platform — Backend Prompt — Volume 8

## ROLE

You are the senior backend engineering organization responsible for implementing the trust, safety, ratings, support, fraud/risk, and operational administration foundation of an original, production-grade global ride-hailing and mobility platform.

Operate simultaneously as:

* Principal Software Architect
* Staff Backend Engineer
* Trust and Safety Systems Architect
* Risk and Fraud Systems Engineer
* Support Platform Engineer
* Database Architect
* Distributed Systems Engineer
* Security Engineer
* Reliability Engineer
* Performance Engineer
* QA Engineer
* Observability Engineer
* Technical Writer

You are implementing production software, not demonstrating concepts.

Do not act as a teacher.

Do not provide pseudo-code.

Do not provide incomplete examples instead of implementation.

Do not leave TODO or FIXME placeholders for required work.

Do not omit implementations with statements such as:

* "implement similarly"
* "remaining code omitted"
* "for brevity"
* "left as an exercise"

Every required file must contain a real implementation.

# PROJECT

## Project Identity

Build an original global ride-hailing and mobility platform supporting:

* riders
* drivers
* operations personnel
* support personnel
* trust and safety personnel
* fleet personnel
* administrators

This milestone implements the platform's trust, safety, ratings, support, fraud/risk, and administrative-operations backend foundation.

The platform is architected for targets such as:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* 100,000+ concurrent realtime sessions and higher during peak
* globally distributed operations
* high-volume support and safety workflows
* sensitive personal and operational data
* strong security and audit requirements

These are architectural targets, not measured capacity claims.

## Technology Direction

Use the locked project stack:

### Runtime

* Node.js
* TypeScript

### Framework

* NestJS

### Database

* PostgreSQL
* PostGIS where applicable
* Prisma where compatible with the architecture

### Cache and Ephemeral State

* Redis

### Events

* Kafka or Redpanda

### Background Jobs

* BullMQ or equivalent

### Search

* OpenSearch or Elasticsearch-compatible architecture

### Object Storage

* Amazon S3

### Realtime

* authenticated WebSockets

### Observability

* OpenTelemetry
* Prometheus-compatible metrics
* structured logs
* Loki-compatible logging
* Tempo-compatible tracing

# SOURCE OF TRUTH

The repository is the implementation source of truth.

Inspect the repository before making changes.

Use the architecture artifacts already present in the repository as the authoritative architecture and contract reference.

Backend Volumes 1–7 establish:

* backend platform foundations
* identity and authorization
* driver onboarding and vehicles
* availability and location
* trip lifecycle
* dispatch
* pricing and payments
* earnings and payouts
* notifications
* messaging
* canonical API/error/idempotency/concurrency contracts
* events and outbox
* realtime
* jobs
* audit

This milestone must build trust, safety, support, risk, ratings, and administration around those established boundaries.

Do not depend on the previous AI conversation.

If existing implementation differs from the architecture:

1. inspect the actual implementation
2. preserve compatible working behavior
3. make the minimum coherent changes required
4. document material discrepancies

Do not create competing sources of truth for trip, identity, payment, or communication state.

# BACKEND EXECUTION MODEL

This milestone owns:

### Trust and Safety

* ratings
* reviews
* blocking
* safety contacts
* incident reporting
* safety cases
* evidence references
* safety status
* operational restrictions
* safety auditability

### Support

* support cases
* case categories
* case state
* assignment
* notes
* internal/external visibility
* attachments/references
* case history
* escalation
* resolution

### Risk and Fraud

* risk signals
* rules
* risk assessments
* review queues
* account restrictions
* holds
* fraud-case references
* decision history

### Administrative Operations

* administrative actions
* approvals
* service-area operations
* operational search boundaries
* bulk operations
* feature/configuration references where required
* audit-sensitive administrative workflows

These domains must remain modular.

Do not merge safety, support, fraud, and general administration into one uncontrolled data model merely for convenience.

# TRUST, SAFETY, AND SUPPORT PRINCIPLES

These systems handle highly sensitive information.

The implementation must enforce:

* least privilege
* explicit authorization
* separation of duties where required
* auditability
* privacy-aware data access
* controlled evidence access
* immutable history where appropriate
* safe operational actions
* idempotent workflows
* bounded retention
* secure attachment references

Do not expose safety reports, evidence, internal notes, fraud signals, or privileged support information through ordinary rider or driver APIs.

# CURRENT IMPLEMENTATION SCOPE

# RATINGS AND REVIEWS

## 1. Rating Domain Ownership

Establish authoritative ownership for ratings and reviews.

The ratings domain owns:

* rating records
* review text where supported
* rating participants
* trip reference
* rating lifecycle
* eligibility
* visibility rules
* moderation state

It does not own:

* trip lifecycle
* payment state
* driver account status
* support cases

## 2. Rating Eligibility

Implement eligibility checks based on authoritative trip facts.

The system must determine:

* whether the rider may rate the driver
* whether the driver may rate the rider
* whether the relevant trip qualifies
* whether the rating window remains open
* whether the rating has already been submitted

Do not allow arbitrary rating submission based only on possession of a trip ID.

## 3. Rating Model

Implement the canonical rating record.

Support the architecture-defined information such as:

* rating ID
* trip ID
* reviewer
* reviewed party
* score
* optional review/reference
* creation timestamp
* visibility/moderation state
* update/revision metadata where supported

Do not expose private moderation metadata to normal clients.

## 4. Rating Constraints

Enforce:

* one rating per reviewer/target/trip where defined
* valid rating range
* authorized participant
* valid rating window
* terminal or eligible trip state

Use database constraints where appropriate.

## 5. Review Moderation Boundary

Provide a moderation state for review content where the architecture requires it.

Potential states include:

* pending
* visible
* hidden
* removed
* under-review

Use exact repository contracts.

Do not implement an arbitrary machine-learning moderation system.

Provide integration points for later trust/risk mechanisms.

## 6. Rating Aggregation Boundary

Implement the backend structures required for aggregate rating calculations.

Support:

* current rating
* rating count
* recalculation/rebuild

Prefer derived aggregates rather than repeatedly scanning all historical ratings on every request.

Do not make aggregate values more authoritative than the underlying ratings.

# BLOCKING AND SAFETY CONTACTS

## 7. Blocking

Implement participant blocking where defined by the architecture.

Support:

* blocker
* blocked party
* creation time
* status
* scope

Blocking must affect only the domains that explicitly consume it.

Do not make blocking silently modify account status.

## 8. Blocking Authorization

Users may create/remove their own blocks.

Privileged personnel require explicit administrative permission.

Do not allow a rider to alter another user's block records.

## 9. Safety Contacts

Implement user safety-contact configuration where defined.

Support:

* owner
* contact reference
* relationship/label
* notification eligibility
* status

Protect contact information.

Do not expose safety-contact data to ordinary users beyond their own authorized scope.

# SAFETY INCIDENTS

## 10. Incident Domain

Implement the safety incident domain.

Support:

* incident ID
* reporter
* affected trip/account where applicable
* incident category
* status
* severity classification where defined
* created/updated timestamps
* assignment
* resolution
* restricted metadata

Do not place full sensitive evidence directly inside general incident rows when object-storage references are appropriate.

## 11. Incident Lifecycle

Implement explicit incident states such as those defined by the architecture.

Potential concepts include:

* reported
* triaged
* investigating
* action-required
* resolved
* closed

Define legal transitions.

Do not allow arbitrary state changes from ordinary user APIs.

## 12. Incident Reporting

Implement authorized incident creation.

Support reporting from:

* rider
* driver
* authorized operations/safety personnel
* system-generated signals where the architecture supports them

Validate participant/trip relationships.

Do not permit a random user to create a report against an unrelated trip without an explicit privileged workflow.

## 13. Incident Categorization

Support stable categories for incidents such as:

* accident
* unsafe driving
* harassment
* assault
* discrimination
* property issue
* emergency
* other supported categories

Use configuration/reference data rather than scattering category strings throughout the codebase.

## 14. Safety Severity and Escalation

Implement deterministic severity metadata and escalation hooks.

Do not invent a proprietary risk-scoring formula.

Severity must be:

* auditable
* versioned/configurable where appropriate
* protected from arbitrary client manipulation

## 15. Safety Evidence References

Integrate incident cases with the S3/object-storage architecture established elsewhere.

Support references to:

* uploaded evidence
* attachments
* documents
* approved media

Enforce object authorization.

Do not create a parallel file-storage mechanism.

## 16. Safety Access Control

Use strong role/resource authorization.

Distinguish:

* reporter
* incident participant
* support personnel
* safety investigator
* operations personnel
* administrator

Not every support or operations role should automatically receive full safety-evidence access.

## 17. Safety Contacts and Emergency Communication

Where architecture requires emergency contacts to be notified, expose the appropriate communication-domain integration boundary.

Do not implement a separate notification engine.

## 18. Safety Audit

Audit:

* incident creation
* severity changes
* investigator assignment
* evidence access where required
* privileged state changes
* resolution
* administrative intervention

Do not log raw evidence content.

# SUPPORT CASES

## 19. Support Case Domain

Implement the support-case model.

Support cases should include:

* case ID
* requester/subject
* category
* source
* status
* priority
* assigned team/agent
* related domain references
* creation/update timestamps
* resolution metadata

Do not duplicate the full trip/payment/dispatch record inside the case.

Use references.

## 20. Support Case Lifecycle

Implement explicit case states defined by the architecture.

Potential concepts:

* open
* assigned
* in-progress
* waiting
* resolved
* closed

Define legal transitions.

## 21. Case Assignment

Implement support assignment.

Support:

* team assignment
* individual assignment
* reassignment
* unassigned state
* priority

Assignment must be concurrency-safe.

Do not allow two agents to believe simultaneously that they own exclusive assignment when the contract requires one owner.

## 22. Support Notes

Implement case notes with explicit visibility.

Distinguish:

* internal notes
* customer-visible responses
* system-generated notes

Internal notes must never accidentally appear in rider/driver APIs.

## 23. Support Case History

Record case-state and assignment history.

Support:

* previous state
* new state
* actor
* timestamp
* reason/reference

Do not rely solely on application logs for case history.

## 24. Support Attachments

Integrate with existing object-storage attachment infrastructure.

Enforce:

* case ownership
* support authorization
* private access
* lifecycle
* auditability

Do not expose attachments through public object URLs.

## 25. Case Linking

Allow cases to reference relevant entities such as:

* account
* trip
* payment
* payout
* notification
* message
* safety incident

Use references rather than copying source data.

## 26. Support Search Boundary

Expose a search integration boundary for support operations.

Search remains derived and must respect authorization.

Do not implement a new search engine.

# FRAUD AND RISK

## 27. Risk Domain Boundary

Implement the foundational risk domain.

It owns:

* risk signals
* rule definitions
* risk assessments
* decisions
* review queues
* restrictions/holds
* decision history

It does not own account, payment, trip, or dispatch data.

## 28. Risk Signals

Create a normalized representation for relevant risk signals.

Signals may reference:

* account behavior
* authentication activity
* payment anomalies
* trip behavior
* device metadata
* operational patterns

Do not copy excessive raw personal data into risk records.

## 29. Rule Model

Implement configurable risk rules or rule metadata.

Each rule should have:

* stable identifier
* version
* status
* scope
* effective period
* configuration metadata
* owner

Do not implement an arbitrary machine-learning platform.

## 30. Risk Assessment

Implement a risk-assessment record.

Support:

* target
* assessment type
* rule/version reference
* outcome
* reason category
* confidence/score only where defined
* timestamp
* decision source

Do not expose internal risk signals to ordinary users.

## 31. Risk Decisions

Implement explicit outcomes such as:

* allow
* review
* restrict
* block
* hold

The exact states must match architecture.

Decision changes must be auditable.

## 32. Review Queue

Implement a review-queue foundation.

Support:

* case/reference
* priority
* status
* assigned reviewer
* created timestamp
* resolution

Do not create an unrelated workflow system.

## 33. Restrictions and Holds

Provide a controlled mechanism for placing restrictions/holds on:

* accounts
* payments
* payouts
* operations

Restrictions must have:

* type
* reason
* scope
* actor/source
* creation/expiration
* active state

Do not allow arbitrary service code to insert opaque permanent restrictions.

## 34. Fraud Audit

Audit:

* risk-rule changes
* risk decisions
* restrictions
* holds
* review outcomes
* privileged overrides

Do not store raw credentials or secrets in risk data.

# ADMINISTRATIVE OPERATIONS

## 35. Administrative Action Model

Implement a controlled administrative-action foundation.

Actions may include:

* account restriction
* trip intervention
* support assignment
* safety escalation
* configuration reference changes
* service-area changes
* operational corrections

Administrative actions must be:

* authenticated
* authorized
* scoped
* audited
* attributable

Do not create an unrestricted "superadmin can do anything" API.

## 36. Approval Workflow

Where architecture requires approvals for sensitive operations, implement a basic approval model.

Support:

* requested action
* requester
* approver
* approval state
* timestamp
* expiration
* final outcome

Avoid self-approval when segregation of duties is required.

## 37. Geographic Administration

Implement backend ownership for operational geographic configuration references such as:

* service area
* region
* operational status
* availability configuration reference

Do not implement low-level map/geospatial infrastructure already owned by the location/routing architecture.

## 38. Operational Flags

Integrate administrative operations with the established configuration/feature-control architecture.

Support references to:

* feature flags
* operational switches
* region controls

Do not create a second configuration system.

## 39. Bulk Operations

Where the architecture requires bulk operational changes, implement safe, bounded workflows.

Support:

* explicit selection
* permission checks
* dry-run where appropriate
* batching
* progress
* audit
* failure handling

Never implement an unrestricted "modify all users" endpoint.

## 40. Administrative Search

Integrate operations with the existing search abstraction.

Provide authorization-aware access to searchable records.

Do not return sensitive fields merely because a record is searchable.

# EVENTS AND JOBS

## 41. Trust and Safety Events

Publish canonical events for major state changes such as:

* rating.created
* rating.updated where supported
* incident.reported
* incident.status.changed
* safety.restriction.changed
* support.case.created
* support.case.assigned
* support.case.resolved
* risk.assessment.created
* risk.decision.changed
* account.restriction.changed

Use the project's existing event-envelope conventions.

## 42. Transactional Outbox

Use the established outbox for durable domain events.

Critical state changes and their required events must commit atomically.

## 43. Background Jobs

Implement appropriate jobs for:

* incident escalation
* support-case reminders
* expired restrictions
* risk-review deadlines
* stale review queues
* rating aggregation
* reconciliation where needed

Jobs must be:

* idempotent
* bounded
* retry-safe
* observable

# DATABASE AND DATA PROTECTION

## 44. Database Constraints

Use database constraints for:

* one rating per eligible relationship
* valid participant relationships
* unique support assignments where required
* valid restriction relationships
* risk-reference integrity
* case linkage integrity

## 45. Sensitive Data Separation

Separate highly sensitive data from ordinary operational records where appropriate.

Do not place:

* raw safety evidence
* private contact information
* sensitive risk signals
* internal support notes

into ordinary user-facing tables without proper access boundaries.

## 46. Retention Integration

Use the existing data-lifecycle architecture.

Do not invent independent retention systems.

Support retention/deletion boundaries for:

* ratings
* reviews
* incidents
* evidence
* support cases
* notes
* risk records
* administrative audit

Respect domain-specific preservation requirements without inventing legal retention periods.

# SECURITY, PRIVACY, AND OBSERVABILITY

## 47. Authorization

Every sensitive operation must validate:

* authenticated actor
* role/permission
* resource scope
* case/trip/account relationship

## 48. Privacy

Never expose:

* internal safety notes
* fraud signals
* risk scores
* private support notes
* sensitive evidence
* privileged administrative metadata

to ordinary users.

## 49. Audit

Audit sensitive actions including:

* safety access
* risk decisions
* support administrative actions
* restrictions
* approvals
* bulk operations
* privileged search
* evidence access

## 50. Logging and Telemetry

Do not place sensitive safety/support/fraud content into logs or traces.

Metrics must use bounded labels and avoid:

* account IDs
* trip IDs
* case IDs
* message content
* incident contents

where not required.

## 51. Failure Handling

Handle:

* database failure
* Redis failure
* event-broker failure
* worker failure
* search failure
* object-storage failure
* concurrent operational actions

Administrative and safety actions must fail safely rather than silently appearing successful.

# API SURFACE

## 52. APIs

Implement only the APIs defined by the architecture.

Potential capabilities include:

### Ratings

* submit rating
* retrieve own ratings
* eligible rating lookup

### Safety

* report incident
* retrieve authorized incident
* safety-contact management
* restricted safety operations

### Support

* create case
* list own cases
* retrieve authorized case
* authorized case notes/actions

### Risk/Operations

* authorized review operations
* restrictions/holds
* administrative case management
* approved operational actions

Do not expose privileged internals through public APIs.

# TESTING

## 53. Ratings

Test:

* eligibility
* duplicate rating
* invalid score
* unauthorized access
* moderation state

## 54. Safety

Test:

* authorized incident creation
* invalid trip relationship
* unauthorized case access
* privileged evidence access
* state-transition races
* audit

## 55. Support

Test:

* case creation
* assignment
* concurrent assignment
* notes visibility
* attachment authorization
* state transitions
* unauthorized access

## 56. Risk

Test:

* signal creation
* rule versioning
* deterministic assessment
* restriction placement
* restriction expiration
* review assignment
* privileged override

## 57. Administration

Test:

* role/permission enforcement
* approval requirements
* bulk-operation bounds
* dry-run behavior
* audit
* concurrent administrative actions

## 58. Events and Jobs

Test:

* outbox creation
* duplicate delivery
* retry
* worker restart
* expired restrictions
* escalation jobs
* aggregate rebuilds

# DOCUMENTATION

Create or update documentation covering:

* ratings/reviews
* blocking
* safety contacts
* incidents
* evidence
* safety authorization
* support cases
* notes
* attachments
* risk signals
* rules
* risk decisions
* review queues
* restrictions/holds
* administrative actions
* approvals
* geographic operations
* bulk operations
* audit
* privacy
* operational procedures

Documentation must describe actual implementation behavior.

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement:

* trip lifecycle
* dispatch
* pricing
* payment processing
* payout processing
* rider-driver messaging
* notification delivery
* fleet maintenance
* scheduled-trip orchestration
* full analytics/reporting

Do not create a second search engine.

Do not create a second object-storage system.

Do not create a second audit platform.

Do not create a second configuration platform.

Do not build a proprietary fraud machine-learning system.

Do not create an unrestricted administrative superuser API.

Do not create another trust/safety backend volume.

Do not create a surprise integration phase.

# REPOSITORY INSPECTION REQUIREMENTS

Before implementation:

1. Inspect the backend repository.
2. Inspect Backend Volumes 1–7 implementation.
3. Inspect identity and authorization.
4. Inspect trip and dispatch.
5. Inspect pricing/payment/earnings.
6. Inspect notification and messaging.
7. Inspect S3/object-storage abstraction.
8. Inspect search abstraction.
9. Inspect event/outbox infrastructure.
10. Inspect jobs.
11. Inspect audit.
12. Read trust, safety, support, risk, and administrative contracts.
13. Determine exactly which files require creation or modification.

Do not duplicate existing platform foundations.

# IMPLEMENTATION RULES

## Preserve Existing Foundations

Reuse:

* authentication
* authorization
* database
* Redis
* events
* outbox
* jobs
* search
* object storage
* audit
* observability
* configuration

## Sensitive Operations

All safety, risk, support, and administrative operations must be explicitly authorization-protected.

## Separation of Duties

Where approval is required, do not allow requesters to silently approve their own sensitive action.

## Immutable History

Where history must be preserved, use append-oriented records and explicit corrections rather than mutation.

## Privacy

Sensitive information must remain unavailable to unauthorized users even if they know an entity ID.

## Idempotency

Incident reporting, administrative actions, restrictions, and other retryable mutations must be safe under duplicate requests.

## Bounded Bulk Operations

Never allow an unbounded production bulk operation.

## No Placeholder Work

Every required capability must be fully implemented.

# VALIDATION REQUIREMENTS

Execute all supported validation.

At minimum:

* TypeScript compilation
* linting
* formatting
* unit tests
* API integration tests
* Prisma validation
* migration validation
* Redis tests
* event/outbox tests
* job tests
* search-integration tests where available
* object-storage authorization tests where available
* OpenAPI validation
* security tests
* dependency/security scanning where configured

Test:

* rating authorization
* duplicate rating
* incident authorization
* evidence authorization
* support-case access
* internal-note privacy
* concurrent assignment
* risk restriction behavior
* restriction expiry
* administrative permission enforcement
* approval enforcement
* bulk-operation bounds
* duplicate events
* worker retry
* database failure
* event-broker failure
* object-storage failure
* search failure

Do not claim successful execution against unavailable external infrastructure.

# FINAL INTEGRATION CHECK

Before declaring this milestone complete:

1. Verify ratings are limited to eligible participants.
2. Verify rating uniqueness and integrity.
3. Verify blocking does not become account-state mutation.
4. Verify safety incidents have explicit lifecycle ownership.
5. Verify incident access is strongly authorized.
6. Verify safety evidence uses private object-storage references.
7. Verify safety actions are auditable.
8. Verify support cases use references rather than duplicated source records.
9. Verify internal support notes cannot reach public APIs.
10. Verify support assignment is concurrency-safe.
11. Verify risk signals and decisions have explicit ownership.
12. Verify risk restrictions/holds are scoped and expirable.
13. Verify privileged overrides are audited.
14. Verify administrative actions are permission-protected.
15. Verify sensitive operations requiring approval enforce separation of duties.
16. Verify geographic administration does not duplicate location infrastructure.
17. Verify bulk operations are bounded and auditable.
18. Verify search is authorization-aware and remains derived.
19. Verify retention follows the established data-lifecycle architecture.
20. Verify trust/safety/support events use the transactional outbox.
21. Verify background jobs are retry-safe.
22. Verify sensitive data is absent from ordinary logs and telemetry.
23. Verify tests cover authorization, concurrency, privacy, and failure modes.
24. Verify compatibility with Backend Volumes 1–7.
25. Verify the repository is ready for Backend Volume 9.
26. Verify no placeholder or fake implementation remains.

# DEFINITION OF DONE

This milestone is complete only when:

* ratings exist
* rating eligibility exists
* rating uniqueness exists
* review moderation boundaries exist
* rating aggregation support exists
* blocking exists where required
* safety contacts exist
* incident domain exists
* incident lifecycle exists
* incident authorization exists
* severity/escalation boundaries exist
* evidence references exist
* safety access controls exist
* safety audit exists
* support cases exist
* case lifecycle exists
* case assignment exists
* support notes exist with visibility controls
* case history exists
* case attachments use the established object-storage architecture
* case linking exists
* search integration boundary exists
* risk domain exists
* risk signals exist
* rule metadata exists
* risk assessments exist
* risk decisions exist
* review queues exist
* restrictions/holds exist
* fraud/risk audit exists
* administrative actions exist
* approval workflow exists where required
* geographic administration references exist
* operational flags use the established configuration architecture
* bounded bulk operations exist
* administrative search integrates with existing search
* events and transactional outbox integration exist
* required background jobs exist
* authorization and privacy controls exist
* metrics/tracing are safe
* APIs conform to the architecture
* tests cover adversarial and failure cases
* documentation is updated
* no duplicate platform foundation has been created
* no unrelated domain has been implemented
* no placeholder implementation remains
* validation results are truthful
* the backend is ready for Backend Volume 9

# IMPLEMENTATION REPORT

At completion, provide:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Ratings and Trust

Summarize:

* rating eligibility
* reviews
* moderation
* blocking
* aggregation

## Safety

Summarize:

* incidents
* lifecycle
* evidence
* severity
* access control
* audit

## Support

Summarize:

* cases
* assignment
* notes
* attachments
* history
* linking

## Risk and Fraud

Summarize:

* signals
* rules
* assessments
* decisions
* review queues
* restrictions/holds

## Administrative Operations

Summarize:

* administrative actions
* approvals
* geographic operations
* feature/configuration integration
* bulk operations
* search

## Security and Privacy

Summarize:

* authorization
* privileged access
* separation of duties
* sensitive-data protection
* audit

## Events and Jobs

Summarize:

* domain events
* outbox
* background jobs
* retries

## Database and Storage

Summarize:

* schema
* constraints
* indexes
* object-storage integration
* retention boundaries

## API

Summarize implemented trust/safety/support/operations endpoints.

## Tests and Validation

List actual commands and actual outcomes.

## External Environment Limitations

State any external systems that could not be exercised.

Do not fabricate production or provider results.

## Architectural Decisions

Record meaningful implementation decisions.

## Known Limitations

List genuine remaining limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement Backend Volume 8 completely.

Extend the existing backend, identity, trip, dispatch, financial, communication, event, job, search, object-storage, authorization, and audit foundations.

Implement ratings, trust, safety incidents, evidence references, blocking, safety contacts, support cases, case assignment and notes, risk signals and decisions, restrictions/holds, administrative actions, approvals, geographic operations, bounded bulk workflows, authorization, audit, events, and required jobs.

Keep all source-domain business state authoritative in its existing domain.

Do not implement scheduled trips, fleet operations, routing/geocoding, or analytics yet.

Do not create duplicate platform foundations.

Do not leave placeholders.

Do not fabricate external infrastructure execution.

Run every validation command supported by the environment.

Verify privacy, authorization, concurrency, auditability, sensitive-data handling, and failure recovery.

Finish with the required implementation report and leave the repository in a coherent production-grade state ready for Backend Volume 9.
