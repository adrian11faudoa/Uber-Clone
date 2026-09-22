# Uber-Style Global Ride-Hailing & Mobility Platform — Frontend Prompt — Volume 5

## ROLE

You are acting as the complete senior frontend engineering organization responsible for implementing this project's operations, administration, support, safety, fleet, geographic-operations, configuration, search, and audit web application to production-grade standards.

Operate as a coordinated:

* Principal Software Architect
* Staff Frontend Engineer
* Staff UX Engineer
* Staff TypeScript Engineer
* Staff Security Engineer
* Accessibility Engineer
* Performance Engineer
* Reliability Engineer
* QA Engineer
* Technical Writer

You are an implementation agent, not a teacher.

Your responsibility is to inspect the repository and implement the complete operations-facing web experience covered by this prompt without breaking existing functionality.

Do not merely describe what should be built. Build it.

---

# PROJECT

## Project

**Uber-Style Global Ride-Hailing & Mobility Platform**

## Product

A production-grade global ride-hailing and mobility platform supporting riders, drivers, dispatch, realtime communication, payments, earnings, scheduled trips, safety, support, fleet operations, analytics, and global geographic operations.

## Scale Target

The architecture targets:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* 100,000+ concurrent realtime sessions and higher
* high-frequency driver-location ingestion
* global and multi-region operation

These are architecture targets, not claims that this repository has already demonstrated those capacities.

---

# SOURCE OF TRUTH

The repository is the source of truth for the current implementation state.

Before changing anything:

1. Inspect the repository structure.
2. Inspect the existing Next.js application, route system, package configuration, scripts, authentication, authorization, layouts, navigation, components, API client, TanStack Query configuration, state management, realtime infrastructure, maps, tables, forms, tests, and documentation.
3. Inspect architecture and backend contracts available in the repository.
4. Determine the actual operations/admin/support/safety/fleet/geographic/configuration/search/audit APIs and authorization boundaries already established.
5. Determine which administrative roles, scopes, permissions, approval requirements, and geographic restrictions are actually defined.
6. Determine which functionality already exists and preserve compatible working behavior.
7. Do not invent backend endpoints, permissions, domain states, approval semantics, or audit requirements where repository contracts already define them.
8. Where a required interface depends on a backend capability not yet implemented, create the correct frontend integration boundary based on the established architecture and document the dependency.
9. Never bypass backend authorization merely because the frontend is an administrative application.
10. Treat this prompt as independently executable. Do not rely on another AI conversation or another prompt being pasted into the repository.

---

# TECHNOLOGY BASELINE

Use the repository's established implementation where it is already present and compatible.

The intended web stack is:

* Next.js
* React
* TypeScript
* Tailwind CSS
* shadcn/ui
* TanStack Query
* React Hook Form
* Zod
* Zustand where justified
* authenticated API communication
* authenticated realtime WebSocket communication

The frontend integrates with the existing backend architecture based on:

* Node.js
* NestJS
* PostgreSQL + PostGIS
* Redis
* Kafka or Redpanda
* BullMQ or equivalent
* OpenSearch/Elasticsearch-compatible search
* S3-compatible object storage
* Stripe-compatible payment-provider abstraction
* maps/routing-provider abstraction
* authenticated WebSockets

Do not redesign backend architecture in this task.

---

# MISSION

Implement the complete **operations and administrative web experience** required to operate the platform safely at global scale.

This includes authorized interfaces for:

* operational dashboards
* global/geographic operations
* trip and driver/rider search
* support cases
* safety incidents
* fleet operations
* vehicle status
* operational restrictions
* configuration
* feature controls where backend support exists
* approval workflows
* bulk administrative actions
* audit history
* operational detail views
* cross-domain investigation workflows
* controlled administrative mutations

This application is for privileged operators and support/safety personnel.

Every sensitive action must respect:

* authentication
* authorization
* role/permission boundaries
* geography/region scope
* approval requirements
* audit requirements
* concurrency rules
* backend state

The frontend must not become a shortcut around the platform's security model.

---

# PRIMARY SCOPE

## 1. Operations Application Shell

Implement or complete the privileged operations application shell.

Include:

* dedicated operations navigation
* role-aware route visibility
* operational dashboard/home
* search
* alerts/attention indicators
* region/geography context
* support entry points
* safety entry points
* fleet entry points
* configuration entry points
* audit entry points
* user/session controls
* responsive behavior appropriate for operational users

Navigation must reflect actual permissions.

Do not merely hide an unauthorized link and assume authorization is enforced.

---

# 2. Role and Permission-Aware UI

Implement a consistent frontend permission model for operations surfaces.

Support the repository's established concepts for:

* roles
* permissions
* resource scopes
* region/geography scopes
* support scopes
* safety privileges
* fleet privileges
* configuration privileges
* approval privileges
* audit access

The frontend may use permissions to:

* hide unavailable navigation
* disable unavailable actions
* explain why an action is unavailable
* prevent accidental requests

But all security-sensitive authorization must remain server-authoritative.

Do not infer privileged access from client-side state alone.

Do not expose privileged data before authorization has been established.

---

# 3. Global Operations Dashboard

Implement the operations home/dashboard based on available backend reporting/operational contracts.

Possible operational summaries include:

* active trips
* pending dispatch
* driver availability
* supply/demand indicators
* service degradation
* scheduled-trip volume
* support backlog
* safety incident backlog
* fleet restrictions
* region health
* payment/provider operational issues
* alerts requiring operator attention

Use actual backend metrics/contracts.

Do not invent operational metrics merely to populate dashboard cards.

The dashboard must distinguish:

* current measurements
* stale measurements
* unavailable measurements
* delayed analytical data

Where data freshness is available, display it appropriately.

---

# 4. Global and Geographic Operations

Implement the geographic-operations experience using the established PostGIS/geography domain contracts.

Support, where backend contracts allow:

* region list
* region detail
* service-area views
* operational status by region
* region-specific driver/rider/trip counts
* supply/demand views
* geographic restrictions
* region configuration
* service-category availability
* region-specific feature state
* geographic operational alerts

Use the existing map abstraction.

Do not hard-code geographic assumptions into the frontend.

---

# 5. Operational Map

Implement an operations map where contractually supported.

Possible map layers:

* active trip locations
* available drivers
* assigned drivers
* service areas
* restricted zones
* operational regions
* incident locations
* fleet locations
* other explicitly authorized operational overlays

The map must:

* respect operator permission
* avoid exposing unauthorized personal information
* avoid rendering unbounded high-cardinality datasets directly into the browser
* use clustering/viewport filtering where necessary
* handle stale location state
* support loading/degraded states
* clean up map listeners/resources correctly

Do not treat map visualization as a source of truth for operational state.

---

# 6. Trip Search

Implement privileged trip search and investigation.

Support repository-defined search by fields such as:

* trip ID
* rider
* driver
* region
* status
* service category
* date/time
* scheduled/immediate type
* payment state
* support/safety linkage where permitted

Use server-side search and filtering.

Do not load all trips into browser memory.

Use the established OpenSearch/Elasticsearch-compatible search boundary when applicable.

Implement:

* search form
* filters
* result list/table
* cursor pagination
* sorting
* empty state
* no-results state
* retry
* loading
* authorization failures

---

# 7. Trip Detail for Operations

Implement an authorized operational trip-detail surface.

Where permitted, include:

* trip lifecycle
* timestamps
* rider summary
* driver summary
* vehicle summary
* pickup/destination
* assignment information
* relevant location/route state
* cancellation state
* payment state
* refund state
* promotion state
* support cases
* safety incidents
* rating/review status
* event/timeline history
* region/service context

Sensitive fields must be filtered according to role and privacy policy.

Do not expose more rider/driver information merely because the operator is authenticated.

---

# 8. Rider and Driver Search

Implement privileged search for riders and drivers where backend contracts support it.

Support:

* identifier lookup
* name/display-name lookup where permitted
* contact lookup where permitted
* region
* account status
* eligibility state
* vehicle association
* trip association
* support/safety history where authorized

Use server-backed search.

Protect against:

* broad unbounded queries
* enumeration where inappropriate
* accidental exposure of private data
* cross-region access violations

---

# 9. Rider Detail for Operations

Implement an authorized rider operational profile.

Possible sections:

* account status
* profile summary
* recent trips
* scheduled trips
* payment-related status where authorized
* support cases
* safety incidents
* restrictions/holds where authorized
* ratings/reviews where policy permits
* relevant audit/activity history

Do not display raw payment credentials.

Do not expose internal risk models or hidden trust scores unless the backend explicitly provides an operator-facing representation for that role.

---

# 10. Driver Detail for Operations

Implement an authorized driver operational profile.

Possible sections:

* driver profile
* onboarding/verification status
* eligibility
* current work-session state
* service-area associations
* current vehicle
* trip history
* earnings/payout operational state where authorized
* ratings
* support cases
* safety incidents
* operational restrictions
* maintenance/document status
* audit/activity history

Do not expose internal secrets or raw verification data.

Do not expose internal risk algorithms merely because an operator has some administrative permission.

---

# 11. Support Cases

Implement the operator/support support-case experience.

Support:

* support-case queue
* assignment
* filtering
* status
* priority
* category
* related rider/driver/trip
* search
* pagination
* case detail
* internal notes
* customer-facing response boundaries where supported
* attachment metadata
* activity history
* escalation
* resolution
* reopening
* audit trail

Respect the established support-case lifecycle.

Do not allow arbitrary state transitions.

Do not allow unauthorized agents to access cases outside their scope.

---

# 12. Support Case Assignment

Implement case assignment workflows where supported.

Support:

* assign to operator
* reassign
* team/queue routing
* priority changes
* ownership changes
* escalation
* confirmation for sensitive changes
* concurrency handling

When a case changes underneath the operator:

* detect stale state
* reconcile
* avoid silently overwriting someone else's changes

Use backend version/concurrency controls where defined.

---

# 13. Safety Incidents

Implement authorized safety-incident operations.

Support:

* incident queue
* severity
* status
* category
* related trip
* rider/driver
* region
* timestamps
* evidence metadata
* notes
* investigation state
* resolution state
* escalation
* incident timeline
* authorized safety actions
* audit history

Protect highly sensitive incident information.

Apply least-privilege rendering.

Do not expose incident information outside the authorized operational boundary.

---

# 14. Safety Incident Investigation

Implement the operational investigation workspace where backend contracts permit.

Provide:

* incident details
* related trip
* involved participants
* relevant event timeline
* evidence references
* communication/support context when authorized
* operator notes
* status transitions
* escalation workflow
* resolution
* action history

Do not allow operators to alter immutable historical evidence.

Do not expose raw storage credentials.

Where evidence is stored in private object storage:

* use authorized backend access
* respect expiration
* handle unavailable/expired access gracefully
* never embed permanent storage credentials

---

# 15. Safety and Operational Actions

Implement only backend-authorized safety/operations actions such as:

* placing a temporary restriction
* removing a restriction
* suspending an account where permitted
* restoring an account where permitted
* disabling a vehicle
* changing an operational status
* escalating an incident
* assigning an incident

Every sensitive mutation must provide:

* clear action description
* affected entity
* reason field where required
* confirmation
* mutation progress
* success state
* failure state
* authorization failure
* concurrency conflict handling

High-impact actions should require the approval/confirmation semantics established by the backend.

Do not implement irreversible actions without explicit backend support.

---

# 16. Fleet Operations

Implement the fleet-operations interface.

Support where available:

* fleet list
* fleet detail
* vehicle list
* vehicle detail
* vehicle status
* driver association
* service category
* service-area association
* operational eligibility
* inspection status
* maintenance status
* restriction state
* availability
* document status
* search/filter/pagination

Do not build a separate vehicle domain model in the frontend.

Use the canonical backend contract.

---

# 17. Vehicle Operations

Implement vehicle operational workflows.

Support contractually defined actions such as:

* activate/deactivate vehicle
* mark operational/unavailable
* update operational status
* associate/disassociate driver
* service-area assignment
* restriction
* inspection status update
* maintenance-related status
* required-document status

Sensitive actions must be authorized and auditable.

Do not allow client-only changes to become authoritative.

---

# 18. Fleet Inspections and Maintenance

Implement operator-facing inspection/maintenance state where supported.

Display:

* inspection status
* inspection date
* next required inspection
* maintenance status
* restriction status
* action required
* historical records where permitted

Support update flows only where the backend defines them.

Do not fabricate regulatory or inspection requirements.

---

# 19. Geographic Configuration

Implement authorized geographic configuration interfaces.

Depending on backend support, include:

* region management
* service-area boundaries
* service-category availability
* operational limits
* region status
* localized configuration
* geographic restrictions
* regional feature configuration

For map-based geometry:

* use established geometry formats
* validate before submission
* preserve precision appropriate to backend requirements
* display server-authoritative geometry
* avoid silently altering polygons

Do not create a proprietary geometry format.

Do not bypass backend validation.

---

# 20. Platform Configuration

Implement configuration UI for settings exposed by backend contracts.

Possible configuration categories:

* service categories
* cancellation policies
* operational thresholds
* pricing configuration summaries
* region-specific configuration
* notification configuration
* feature configuration
* provider configuration references
* operational limits

Configuration UI must respect:

* environment/region scope
* effective dates
* versioning
* approval requirements
* auditability
* concurrency control

Do not expose secrets.

Do not expose provider credentials or infrastructure secrets in configuration screens.

---

# 21. Feature Controls

Where the backend supports operator-facing feature controls, implement:

* current value
* scope
* effective state
* rollout state
* activation/deactivation
* region scope
* environment scope where relevant
* approval state
* audit history

Do not invent a separate frontend feature-flag system.

Do not allow client-only feature toggles to be mistaken for production configuration.

---

# 22. Approval Workflows

Implement approval interfaces where the backend contract defines controlled administrative changes.

Support:

* pending approvals
* request detail
* requested change
* scope
* requester
* created time
* approval/rejection
* required justification
* current status
* audit history

Prevent an operator from approving an action that they are not authorized to approve.

Respect separation-of-duties rules if present.

Do not encode approval policy solely in frontend code.

---

# 23. Bulk Operations

Implement safe operator bulk actions where explicitly supported.

Examples may include:

* bulk status update
* bulk assignment
* bulk restriction
* bulk queue changes
* bulk geographic operations
* bulk configuration updates

Bulk flows must include:

* selection
* result count
* confirmation
* reason where required
* validation
* progress
* partial-success presentation
* failed-item reporting
* authorization handling
* retry behavior appropriate to the backend contract
* audit reference

Do not assume all selected records will succeed.

Do not silently repeat a bulk mutation.

Prefer backend batch operations rather than issuing thousands of browser requests.

---

# 24. Global Search

Implement a privileged global search experience where supported.

Search may span:

* riders
* drivers
* trips
* vehicles
* support cases
* safety incidents
* scheduled trips
* configuration records

Search results must:

* identify resource type
* show only authorized fields
* provide clear navigation
* paginate appropriately
* handle ambiguous results
* prevent unauthorized resource access after navigation

Do not use client-side aggregation over unrelated private datasets.

---

# 25. Audit History

Implement an operator-facing audit interface where authorized.

Support:

* audit-event list
* timestamp
* actor
* action
* resource type
* resource reference
* region/scope
* outcome
* correlation/trace reference where appropriate
* reason/metadata where contractually exposed
* filtering
* pagination
* search
* detail view

Audit logs are historical records.

Do not allow ordinary operators to edit or delete audit events.

Do not render secrets embedded in audit metadata.

---

# 26. Operational Activity Timeline

Where supported, provide a unified authorized timeline for important resources.

Possible timeline events:

* trip transitions
* assignment changes
* support actions
* safety actions
* account-status changes
* vehicle-status changes
* configuration changes

Clearly differentiate:

* system event
* operator action
* user action
* asynchronous background event

Do not imply causality when the backend only provides event ordering.

---

# 27. Realtime Operations Updates

Integrate operations surfaces with established realtime infrastructure where appropriate.

Support relevant events such as:

* new support case
* case assignment change
* safety incident creation/update
* trip-state change
* dispatch issue
* driver availability change
* fleet status change
* configuration change
* operational alert

Implement:

* authenticated subscription
* role-aware topic subscription
* reconnect
* resubscription
* deduplication
* missed-event recovery
* query reconciliation
* cleanup on navigation/logout

Do not subscribe every operator to every high-volume stream when scoped subscriptions are available.

---

# 28. Search and Pagination Performance

Operational datasets can become extremely large.

Requirements:

* server-side filtering
* cursor pagination where defined
* sensible default page size
* explicit maximum page size
* column selection appropriate to the view
* debounced text search where useful
* request cancellation
* stale request protection
* virtualization for very large tables when justified
* stable sorting semantics

Do not fetch millions of records into the browser.

---

# 29. Data Privacy

Operations interfaces handle highly sensitive data.

Implement:

* least-privilege rendering
* field-level redaction where contractually appropriate
* masked personal/contact information where appropriate
* no raw payment credentials
* no raw authentication secrets
* no internal provider secrets
* controlled evidence access
* safe clipboard behavior where sensitive values can be copied
* safe logging
* privacy-aware analytics
* restricted browser persistence

Do not cache sensitive administrative data indefinitely.

Respect backend retention and authorization semantics.

---

# 30. Administrative Security

Implement strong frontend defenses around privileged operations.

Include:

* authenticated protected routes
* role/permission checks
* session-expiration handling
* reauthentication flows where supported
* destructive-action confirmation
* prevention of accidental duplicate submission
* idempotency where required
* concurrency conflict handling
* safe rendering of operator/user-provided text
* CSRF protections according to the established authentication architecture
* no secret exposure in client bundles
* no privileged information in URLs unless explicitly designed and safe

Never treat the frontend as the security boundary.

---

# 31. Forms and Mutation Safety

Use React Hook Form and Zod for structured administrative forms where appropriate.

Mutations must provide:

* validation
* dirty-state handling
* confirmation when required
* loading state
* duplicate-submit protection
* server-error mapping
* authorization-error handling
* concurrency conflict handling
* success confirmation
* cache invalidation/reconciliation

For dangerous actions:

* state exactly what will change
* identify the affected resource
* display the scope
* require the appropriate confirmation
* require a reason where backend contracts require it

Do not add fake approval or confirmation semantics that the backend does not enforce.

---

# 32. Configuration Versioning and Concurrency

When editing configuration:

* load current version
* display current state clearly
* preserve version/revision information where required
* submit against the expected version
* handle conflicts
* refresh stale configuration
* never silently overwrite a newer operator's changes

Where configuration is effective-dated:

* show current value
* show pending value
* show effective time
* distinguish future versus active configuration

Do not implement version semantics only in the UI.

---

# 33. Accessibility

Operations interfaces must remain accessible despite high information density.

Implement:

* semantic tables
* keyboard navigation
* focus management
* accessible dialogs
* accessible filters
* accessible status indicators
* accessible map alternatives
* screen-reader-readable operational state
* form error association
* accessible pagination
* accessible notifications
* sufficient interaction target sizes

Important operational changes should be announced appropriately without producing excessive duplicate announcements.

Provide non-map alternatives for information conveyed only through geographic visualization.

---

# 34. Responsive Behavior

Support:

* desktop-first operational workflows
* tablet layouts
* constrained laptop viewports
* mobile access for essential operational tasks where appropriate

Do not force large tables into unusable narrow layouts.

Use:

* responsive tables
* horizontal scrolling where appropriate
* stacked detail panels
* contextual drawers
* dedicated mobile views where justified

Preserve access to critical operational actions.

---

# 35. Performance

Operations screens can combine large datasets, maps, realtime events, and complex tables.

Optimize for:

* virtualized lists/tables where justified
* server-side filtering
* pagination
* map clustering
* bounded realtime state
* query deduplication
* selective invalidation
* resource cleanup
* code splitting
* route-level loading
* efficient memoization
* minimized rerenders
* browser memory limits

Do not let high-frequency trip/location events trigger full application rerenders.

Do not retain unlimited audit or event history in client memory.

---

# 36. Testing

Implement meaningful automated tests.

## Unit Tests

Cover:

* permission mapping
* role-to-navigation mapping
* redaction helpers
* status mapping
* configuration form validation
* approval-state mapping
* bulk-operation result mapping
* pagination/filter state
* geographic configuration helpers
* audit presentation helpers

## Component Tests

Cover:

* operations shell
* role-aware navigation
* search
* trip detail
* support queue
* support case detail
* safety incident queue/detail
* fleet views
* geographic views
* configuration forms
* approval workflows
* bulk-operation flows
* audit history
* error/empty/loading states

## Integration Tests

Cover important privileged workflows:

* authorized operations access
* unauthorized route access
* trip search/detail
* support assignment
* safety incident update
* vehicle-status mutation
* geographic configuration
* feature/configuration update where supported
* approval flow
* bulk operation
* audit-history retrieval
* realtime operational update
* session expiration/recovery

Use test doubles/mocks for unavailable external services.

Do not claim production provider behavior was validated when only mocks were used.

---

# 37. Documentation

Update frontend documentation to describe actual operations functionality.

Document where applicable:

* operations routes
* role/permission boundaries
* major screens
* data sources
* search model
* pagination
* realtime subscriptions
* support workflows
* safety workflows
* fleet workflows
* geographic workflows
* configuration workflows
* approval semantics
* bulk-operation behavior
* audit access
* privacy/security considerations
* testing
* local-development requirements

Documentation must match actual implementation.

---

# OUT OF SCOPE

Do not implement unrelated domains in this prompt.

Explicitly out of scope:

* new rider-facing product functionality
* new driver-facing product functionality
* mobile application implementation
* backend services
* backend authorization implementation
* database schema redesign
* dispatch-engine implementation
* payment-provider backend implementation
* routing-provider backend implementation
* analytics-pipeline backend implementation
* infrastructure/Terraform
* Kubernetes/EKS
* cloud provisioning
* CI/CD redesign
* native mobile background location
* a separate QA phase
* a separate final-integration phase
* a new architecture volume

Do not create additional project phases to absorb work outside this scope.

---

# IMPLEMENTATION RULES

## Repository First

Inspect before modifying.

Determine the actual:

* route structure
* operations/admin architecture
* authentication
* authorization
* API clients
* query patterns
* state management
* realtime implementation
* map abstraction
* table components
* forms
* design system
* testing infrastructure
* documentation

Preserve working behavior.

## Security Is Server-Authoritative

Frontend permission checks exist for UX and workflow control.

They are not a substitute for backend authorization.

Never remove a security boundary merely to make an operation work.

## No Pseudo-Code

Implement real code.

Do not use:

* TODO implementations
* placeholders
* fake API endpoints
* fabricated permissions
* fake audit events
* fake support cases
* fake incidents
* fake operational metrics presented as real
* omitted implementations
* simulated privileged success

## No Contract Fabrication

Do not invent:

* endpoint names
* DTO fields
* permission IDs
* event names
* approval policies
* administrative roles
* geographic capabilities
* bulk mutation semantics

when repository/backend contracts already define them.

## Sensitive Information

Minimize data displayed and persisted.

Do not expose:

* payment credentials
* authentication secrets
* infrastructure secrets
* provider credentials
* internal risk-model details
* hidden enforcement rules
* private evidence beyond authorization

## Mutation Safety

Sensitive mutations must be deterministic and safe.

Use:

* idempotency where defined
* concurrency controls
* confirmation
* validation
* error handling
* cache reconciliation

Do not optimistically represent irreversible administrative actions as successful before confirmation.

## Existing Code

Reuse established:

* search
* tables
* forms
* API client
* query architecture
* realtime architecture
* map components
* dialogs
* status components

Do not build parallel infrastructures without a compelling architectural reason.

---

# VALIDATION REQUIREMENTS

Before considering this volume complete:

1. Run formatting checks.
2. Run linting.
3. Run TypeScript/type checks.
4. Run relevant unit tests.
5. Run component tests.
6. Run integration tests.
7. Run the production build or strongest available equivalent.
8. Verify privileged routes.
9. Verify unauthorized access handling.
10. Verify role/permission-aware navigation.
11. Verify sensitive-data redaction.
12. Verify trip/rider/driver search.
13. Verify support flows.
14. Verify safety flows.
15. Verify fleet workflows.
16. Verify geographic workflows.
17. Verify configuration workflows.
18. Verify approval flows.
19. Verify bulk-operation behavior.
20. Verify audit-history access.
21. Verify realtime reconnection/reconciliation.
22. Verify pagination and server-side filtering.
23. Verify responsive behavior.
24. Verify accessibility checks available in the repository.
25. Verify no secrets appear in client bundles, browser storage, logs, or test fixtures.
26. Verify no fake operational data is presented as authoritative.
27. Verify no TODO/placeholder production implementation was introduced.
28. Verify documentation matches the implementation.

Where the environment prevents a validation step, perform everything that is available and explicitly report what could not be validated.

Never claim real cloud, production, or third-party validation that did not occur.

---

# INTEGRATION CHECK

Before finalizing, verify that this operations frontend integrates cleanly with the rest of the project.

Confirm that:

* rider and driver routes remain intact
* operations routes are isolated behind the correct authentication/authorization boundaries
* shared API infrastructure remains consistent
* shared realtime infrastructure remains consistent
* global search links to authorized resource details
* operational trip views use the canonical trip contract
* support references use canonical support contracts
* safety references use canonical safety contracts
* fleet views use canonical vehicle/driver contracts
* geographic configuration uses canonical geography contracts
* financial details are displayed only where authorized
* audit views use canonical audit contracts
* configuration mutations respect version/concurrency semantics
* realtime events reconcile safely with query state
* navigation remains coherent across user roles
* existing rider and driver experiences were not unintentionally broken

The completed web application must remain one coherent production-grade system.

Do not introduce temporary architecture that will conflict with the mobile or infrastructure implementation.

---

# DEFINITION OF DONE

This volume is complete only when:

* operations shell is implemented
* role/permission-aware UI is implemented
* operations dashboard is implemented
* global/geographic operations views are implemented
* operational map is implemented where supported
* trip search/detail is implemented
* rider/driver operational search/detail is implemented
* support cases are implemented
* safety incidents are implemented
* safety investigation flows are implemented
* authorized safety/operational actions are implemented
* fleet management is implemented
* vehicle operations are implemented
* inspection/maintenance status is implemented where supported
* geographic configuration is implemented where supported
* platform configuration is implemented where supported
* feature controls are implemented where supported
* approval workflows are implemented where supported
* bulk operations are implemented where supported
* global search is implemented where supported
* audit history is implemented
* operational timelines are implemented where supported
* realtime operational updates are integrated
* privacy/redaction controls are implemented
* privileged mutation safety is implemented
* loading/empty/error/degraded states are handled
* responsive behavior is complete
* accessibility requirements are addressed
* performance requirements are addressed
* tests are implemented
* documentation is updated
* validation has been performed
* limitations are honestly reported
* no sensitive secrets are exposed
* no fake operational/admin behavior is presented as production-ready
* no placeholders remain
* no unrelated scope was introduced

---

# IMPLEMENTATION REPORT

At the end of execution, provide a concise report containing:

## Files Changed

List created, modified, and removed files.

## Implemented Scope

Summarize the operations, support, safety, fleet, geographic, configuration, search, approval, bulk-operation, and audit functionality actually implemented.

## Authorization and Privacy

Summarize the permission boundaries, redaction behavior, and privileged-action protections implemented.

## Contracts Used

Identify the API, realtime, geography, support, safety, fleet, configuration, approval, search, and audit contracts used.

## Validation

Report the exact validation commands executed and their results.

## Limitations

Report only actual implementation or environment limitations.

## Follow-Up Dependencies

Report genuine backend or repository dependencies where they exist.

Do not invent additional project phases.

---

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement the complete operations/admin frontend scope defined by this prompt.

Preserve all working behavior that is outside the scope of necessary changes.

Use the repository's actual architecture and contracts as the source of truth.

Do not wait for another prompt.

Do not merely describe the implementation.

Create and modify the real production-grade code, tests, and documentation required for this scope.

Do not use pseudo-code, placeholders, fabricated permissions, fabricated APIs, fake audit data, fake operational state, or simulated privileged success presented as real functionality.

Treat security, privacy, authorization, concurrency, auditability, and operational safety as first-class requirements.

Validate the implementation as thoroughly as the environment permits.

Finish only when this volume is genuinely implemented and integrated into the repository.
