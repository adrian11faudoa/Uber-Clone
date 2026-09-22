# Uber-Style Global Ride-Hailing & Mobility Platform — Frontend Prompt — Volume 4

## ROLE

You are acting as the complete senior frontend engineering organization responsible for implementing this project's driver-facing web application to production-grade standards.

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

Your responsibility is to inspect the repository and implement the complete driver web experience covered by this prompt without breaking existing functionality.

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

1. Inspect the existing repository structure.
2. Inspect the web application's package configuration and scripts.
3. Inspect existing routes, layouts, navigation, components, hooks, API clients, query definitions, state stores, realtime infrastructure, authentication, styling, tests, and documentation.
4. Inspect the backend contracts and architecture artifacts available in the repository.
5. Determine the actual driver-related APIs, DTOs, authorization boundaries, enums, identifiers, pagination conventions, location contracts, dispatch contracts, trip state transitions, earnings/payment contracts, notifications, messaging, ratings, and scheduled-trip contracts already established.
6. Determine which driver functionality already exists.
7. Preserve compatible working behavior.
8. Do not invent backend contracts where documented contracts already exist.
9. Do not assume that a backend feature is available merely because this prompt describes the intended product.
10. Where a required capability depends on a backend contract that is genuinely absent, create the frontend integration against the established architectural boundary and document the dependency rather than fabricating a production backend.

This prompt is independently executable.

Do not depend on another AI conversation, another prompt being pasted into the conversation, or undocumented assumptions about earlier work.

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

The frontend must integrate with the existing backend architecture based on:

* Node.js
* NestJS
* PostgreSQL
* PostGIS
* Redis
* Kafka or Redpanda
* BullMQ or equivalent
* OpenSearch/Elasticsearch-compatible search
* S3-compatible object storage
* Stripe-compatible payment abstraction
* maps/routing provider abstraction
* authenticated WebSockets

Do not redesign backend architecture in this task.

---

# MISSION

Implement the complete **driver web experience** for operating as an active driver on the platform.

The driver must be able to use the web application to:

* access the driver workspace
* understand onboarding/readiness state
* manage availability/work sessions
* present current operational eligibility
* share current location when required by the backend flow
* receive realtime ride offers
* inspect offer details
* accept or reject offers
* manage an assigned trip
* navigate through pickup, arrival, passenger-onboard, active-trip, and completion states
* communicate with the rider where supported
* handle cancellations and exceptions according to backend contracts
* view completed trips and driver earnings
* inspect payout state
* manage driver-facing notifications
* access ratings/reputation information exposed by the product
* access driver profile/vehicle information supported by the web product
* interact correctly with scheduled-trip assignments where the backend exposes them

The web experience must remain authoritative to backend state.

The frontend must never claim that the driver is available, assigned, paid, or completed merely because a local UI state changed.

---

# PRIMARY SCOPE

## 1. Driver Workspace

Create or complete the primary authenticated driver workspace.

Include:

* driver home/dashboard
* current operational state
* availability state
* work-session state
* readiness indicators
* active trip state when one exists
* pending offer state when one exists
* current location/session state where relevant
* relevant earnings summary
* relevant notifications
* relevant warnings and operational blockers
* clear entry points to active work, earnings, profile, support, and other driver functionality already established by the product

The workspace must respond correctly to:

* offline state
* stale state
* authentication expiration
* connection loss
* backend degradation
* driver account restrictions
* missing eligibility requirements

Avoid creating a dashboard overloaded with data that belongs in dedicated surfaces.

---

# 2. Driver Profile

Implement the user-facing driver profile experience supported by the backend.

Include, where applicable:

* driver display information
* profile photo
* contact information
* driver-facing preferences
* language/localization
* notification preferences
* status/readiness information
* verification status summary
* account restrictions or required actions
* profile edit flows supported by the backend

Do not expose:

* internal risk scores
* private verification data
* internal administrative notes
* security secrets
* backend-only identifiers
* internal fraud/risk rules

All profile changes must use validated forms and established authorization boundaries.

---

# 3. Driver Onboarding and Operational Readiness

Implement the driver-facing status and readiness experience available through the backend.

The UI may include:

* onboarding completion state
* identity verification state
* vehicle verification state
* document/status requirements
* service-area eligibility
* operational restrictions
* action-required states
* approved/eligible state
* suspended/restricted state where user-facing information is contractually provided

For every readiness blocker:

* explain what the driver can do next
* distinguish pending from failed
* show server-authoritative status
* avoid exposing internal approval/risk criteria

Where document uploads or media are already supported by the backend:

* use the established secure upload flow
* never upload directly with permanent credentials
* show upload progress/state
* handle expiration and replacement correctly
* validate file types/sizes on the client as a convenience only
* treat backend validation as authoritative

Do not redesign the identity/verification backend in this volume.

---

# 4. Availability and Work Sessions

Implement the complete driver-facing availability/work-session experience.

Support backend-defined concepts such as:

* offline
* online/available
* unavailable
* working session started
* working session ended
* temporarily unavailable
* restricted from receiving trips
* pending transition

Where supported, include:

* start work session
* stop work session
* availability toggle
* transition confirmation where necessary
* current session duration
* current status
* reason/blocker presentation
* retry behavior when state changes fail

The UI must protect against contradictory local state.

For example:

* do not visually switch to available until the server confirms the transition when the backend contract is asynchronous or authoritative
* prevent duplicate start/stop requests
* reconcile the state after reconnect or browser refresh

---

# 5. Eligibility and Driver State

Implement rider-independent driver operational state presentation.

Include relevant states such as:

* eligible
* not eligible
* verification pending
* vehicle unavailable
* service area unavailable
* account restricted
* document expired
* maintenance restriction
* temporary hold
* dispatch unavailable
* platform degraded

The UI should distinguish:

* account state
* vehicle state
* work-session state
* dispatch eligibility

Do not collapse these into one misleading generic status.

---

# 6. Driver Location

Integrate the web application with the established location model when browser-based driver location is part of the product contract.

Support:

* location permission request
* current location acquisition
* location permission denied
* location unavailable
* stale location
* browser geolocation lifecycle
* background/visibility limitations of browser environments
* reconnect behavior
* location-sharing state
* operational warnings where browser constraints prevent required behavior

Use the existing location abstraction rather than creating a second competing implementation.

Do not expose raw internal location ingestion details.

Do not imply that the browser can provide native-background location guarantees if it cannot.

Where the web product is inherently unsuitable for a backend capability that requires native background execution, preserve the documented product boundary rather than faking that behavior.

---

# 7. Realtime Driver Connection

Implement the authenticated realtime driver connection used by the product.

Support:

* authentication
* connection initialization
* reconnect
* resubscription
* heartbeat/liveness behavior where defined
* stale-connection detection
* connection state
* missed-event recovery
* subscription cleanup
* browser/tab lifecycle handling
* duplicate-event protection

The driver should have a clear indication of whether realtime communication is:

* connected
* connecting
* reconnecting
* degraded
* disconnected

Do not let a stale websocket make the driver appear operationally current.

---

# 8. Realtime Trip Offers

Implement the driver-facing dispatch-offer experience.

Support:

* incoming offer
* pickup information
* destination information when policy/contracts permit
* estimated distance/time information where available
* service category
* pricing/earnings estimate where contractually provided
* offer expiration
* countdown behavior
* accept
* reject
* expired offer
* already-resolved offer
* duplicate offer event handling
* connection recovery

Offer UI must be driven by the dispatch contract.

Do not expose rider information that the platform's privacy policy or backend authorization does not permit.

Do not calculate an authoritative payout estimate independently from backend values.

---

# 9. Offer Acceptance and Rejection

Implement driver offer actions with correct concurrency handling.

For acceptance:

* show explicit action state
* prevent double submission
* use required idempotency semantics
* handle success
* handle already-accepted-by-another-driver outcomes
* handle expiration
* handle trip no longer available
* handle eligibility changes
* handle network timeout
* reconcile after uncertain outcomes

For rejection:

* implement required reason selection if backend requires it
* validate reason
* submit safely
* handle failure
* update local offer state only after the appropriate server confirmation

Never turn an uncertain mutation into a successful UI state.

---

# 10. Assigned Trip Workspace

Implement the driver's active assigned-trip workspace.

Support, according to the established trip state machine:

* assignment confirmed
* en route to pickup
* arrived at pickup
* passenger onboard
* active trip
* trip completion
* cancellation
* failed/exception state where applicable

Display:

* trip status
* pickup
* destination
* passenger summary permitted by authorization
* relevant contact/communication actions
* map/navigation entry points
* trip timers where defined
* trip progress
* earnings/fare information permitted by contract
* action buttons valid for the current state

Actions must be state-dependent.

Do not display invalid actions for the current backend lifecycle state.

---

# 11. Pickup Workflow

Implement the driver pickup workflow.

Support:

* navigation to pickup
* arrival action
* arrival confirmation
* waiting state
* passenger-ready state when exposed
* pickup timeout/waiting information where supported
* cancellation options exposed to drivers
* rider contact where permitted
* location/map context
* network and realtime failure recovery

The interface must clearly distinguish:

* approaching pickup
* arrived
* waiting
* pickup completed

Never mark a pickup as complete merely because the driver clicked the button unless the backend confirms the transition.

---

# 12. Active Trip Workflow

Implement the active-trip driver experience.

Support:

* trip started
* destination display
* route/navigation handoff
* elapsed time/distance where available
* trip status
* passenger contact where supported
* safety entry points
* cancellation/exception flows allowed by backend policy
* trip completion action
* realtime synchronization

Handle:

* duplicate events
* missed events
* browser refresh
* reconnect
* backend state changes
* driver attempting a stale action

The backend state machine remains authoritative.

---

# 13. Trip Completion

Implement driver trip completion.

Support:

* completion action
* completion confirmation when required
* pending completion state
* successful completion
* completion failure
* duplicate-completion protection
* subsequent payment/earnings state presentation
* rating eligibility where supported

After completion:

* invalidate/reconcile affected trip state
* refresh earnings state where appropriate
* update history
* update relevant notifications
* expose support/reporting entry points where appropriate

Do not claim that driver earnings are final merely because trip completion was submitted.

---

# 14. Driver Cancellation and Exceptions

Implement driver cancellation flows allowed by the backend contract.

Include:

* cancellation eligibility
* cancellation reason
* confirmation
* fees/penalties when backend-authoritative and user-visible
* state transition handling
* server rejection
* retry/reconciliation
* support escalation where appropriate

Do not expose internal enforcement/risk formulas.

Never calculate a cancellation penalty independently when the backend supplies the authoritative value.

---

# 15. Scheduled Trip Assignments

Implement driver-facing scheduled-trip functionality only where the backend exposes it for drivers.

Support:

* scheduled assignment visibility
* scheduled pickup details
* scheduled date/time
* preparation/pre-dispatch state
* assignment confirmation
* driver eligibility/state
* accept/reject if contractually supported
* cancellation/exception path where permitted
* status updates
* transitions into active trip workflow

Clearly distinguish scheduled work from immediate dispatch offers.

Do not imply assignment before the backend confirms it.

---

# 16. Navigation and Maps Integration

Use the existing map/routing abstraction.

Provide:

* pickup map
* destination map
* route visualization where supported
* navigation handoff
* current-location marker
* trip context

Do not hard-code a specific provider if the architecture uses a provider abstraction.

Do not duplicate geocoding/routing logic already implemented in shared frontend infrastructure.

Respect map-provider API keys and browser security requirements.

---

# 17. Driver Earnings

Implement the driver-facing earnings experience supported by the backend.

Include:

* current earnings summary
* trip-level earnings
* earnings by period
* gross earnings where applicable
* platform fees where user-visible
* adjustments
* tips
* bonuses/incentives where supported
* refunds/corrections where they affect driver-facing balances
* currency
* payout state

Use backend-authoritative financial values.

Support appropriate time filters and pagination.

Do not reconstruct authoritative earnings from individual frontend events.

---

# 18. Earnings History

Implement paginated earnings/history views.

Support:

* daily/weekly/monthly summaries where backend supports them
* trip-level history
* cursor pagination
* filters
* empty state
* no-result state
* loading
* errors
* stale data
* responsive presentation

Do not fetch unlimited historical earnings into browser memory.

Ensure financial cache keys are scoped to the authenticated driver and all relevant filter parameters.

---

# 19. Payouts

Implement driver-facing payout information according to backend contracts.

Where supported:

* payout methods summary
* payout destination summary using safe masked information
* payout status
* pending payout
* completed payout
* failed payout
* payout schedule
* payout history
* payout detail
* account/action-required states

Never expose payment credentials or provider secrets.

Do not claim a payout is complete before the backend confirms completion.

When a payout provider requires external secure setup:

* use the approved provider handoff
* do not collect sensitive credentials directly in the application
* handle return/callback state correctly

---

# 20. Driver Ratings and Reputation

Implement driver-facing ratings/reputation information exposed by the backend.

Support, where available:

* current rating summary
* rating breakdown
* historical rating summaries
* trip-related rating information permitted by privacy rules
* rating/review visibility rules
* unavailable/insufficient-data state

Do not reveal private reviewer information unless explicitly authorized by the backend.

Do not infer hidden trust/risk decisions from rating information.

---

# 21. Driver Notifications

Integrate the driver workspace with the established notification system.

Support:

* unread count
* notification list
* read/unread state
* notification detail
* navigation to related resources
* relevant operational alerts
* payout/earnings notifications
* trip notifications
* account/verification notifications
* system availability/degradation notices where applicable

Use the existing notification architecture.

Do not duplicate notification delivery logic in the frontend.

---

# 22. Driver Messaging

Integrate rider-driver messaging where supported.

Support:

* conversation access from active trip
* message history
* message composition
* read state
* realtime delivery
* reconnect
* missed-event recovery
* sending state
* failure/retry
* attachment handling if already supported

Do not expose conversations unrelated to the authenticated trip/participants.

Respect backend message authorization and lifecycle.

Do not introduce a second chat implementation separate from the established messaging contract.

---

# 23. Driver Safety and Support Entry Points

Provide driver-facing entry points into:

* trip safety
* incident reporting
* support
* trip-specific support
* account support
* vehicle/eligibility support
* payment/earnings support

Where backend contracts support structured case creation, integrate with them.

Do not implement operator/admin tooling in this volume.

Support should remain contextual to the current driver's authorized resources.

---

# 24. State Synchronization

Coordinate TanStack Query server state, local UI state, and realtime events correctly.

Use clear boundaries:

### Server state

Use TanStack Query for:

* driver profile
* eligibility
* work-session state
* trip state
* offers
* scheduled trips
* earnings
* payouts
* ratings
* notifications
* messaging data where appropriate

### Local UI state

Use Zustand or component state only where appropriate for:

* transient UI
* map presentation state
* modal state
* navigation/UI preferences
* ephemeral interaction state

Do not copy authoritative backend entities into global local stores without a clear reason.

---

# 25. Realtime and Query Reconciliation

For important driver events:

* accept/reject offer
* offer expiration
* trip assignment
* trip transition
* scheduled assignment
* earnings update
* payout update
* notification arrival
* message arrival

implement a robust reconciliation strategy.

The system must survive:

* websocket disconnect
* browser refresh
* duplicate events
* out-of-order events
* delayed API response
* event received before query resolution
* query resolved after event reception

Do not simply overwrite newer state with an older event.

Where the backend provides version/sequence/timestamp semantics, use them.

---

# 26. Browser Lifecycle

Driver workflows are sensitive to browser lifecycle.

Handle:

* tab visibility
* page refresh
* route transitions
* browser navigation
* temporary tab suspension
* reconnect
* logout
* session expiration
* unexpected component unmount

Ensure active subscriptions, timers, geolocation watchers, and listeners are cleaned up correctly.

Do not assume that a hidden browser tab behaves like a native mobile driver application.

---

# 27. Loading, Empty, Error, and Degraded States

Every driver-facing feature must intentionally handle:

* first load
* refreshing
* empty state
* no eligible trips
* no offers
* expired offer
* failed mutation
* unauthorized state
* forbidden state
* backend unavailable
* websocket disconnected
* stale location
* location permission denied
* payment/earnings provider degradation
* scheduled-trip unavailable state
* retry

A blank page is not an acceptable error state.

---

# 28. Responsive Driver Experience

Support:

* desktop
* tablet
* mobile web

Prioritize usable layouts for:

* active trip
* offer screen
* availability controls
* map views
* earnings
* payout status
* notifications
* profile/settings

Interactive trip controls must remain usable at smaller sizes.

Do not rely on hover-only controls.

---

# 29. Accessibility

Implement production-grade accessibility.

Include:

* semantic HTML
* accessible navigation
* keyboard support
* focus management
* accessible dialogs
* accessible countdown/status messaging
* accessible forms
* clear labels
* error associations
* screen-reader-friendly trip state changes
* accessible notifications
* sufficient interaction targets

Important operational state changes such as:

* new offer
* offer expiration
* assignment
* arrival
* trip completion
* payment/payout status

must be communicated accessibly without overwhelming users with duplicate announcements.

---

# 30. Security and Privacy

Treat driver information, location, trip information, earnings, payout data, and conversations as sensitive.

Requirements:

* never trust frontend authorization
* enforce backend authorization
* prevent cross-driver query-cache leakage
* do not store sensitive payment credentials
* do not expose provider secrets
* safely render rider-generated content
* avoid leaking private rider data
* avoid logging raw location unnecessarily
* avoid logging financial credentials
* avoid exposing internal risk or enforcement data
* ensure protected driver routes cannot be accessed by unauthorized roles

Do not weaken security to simplify the implementation.

---

# 31. Performance

The driver interface must remain performant during realtime activity.

Pay special attention to:

* websocket message frequency
* location update frequency
* map rerenders
* trip-state updates
* timer updates
* offer countdowns
* notification bursts
* earnings lists
* query invalidation storms
* unnecessary React rerenders
* cleanup of listeners/watchers
* resource lifecycle

Do not trigger expensive global rerenders for every location update.

Throttle/debounce UI work where appropriate without altering backend event semantics.

Do not retain unlimited realtime history in browser state.

---

# 32. Testing

Implement meaningful automated tests.

## Unit tests

Cover:

* driver-state mapping
* offer-state mapping
* trip-state action eligibility
* countdown/expiration logic
* earnings/currency formatting
* payout-state presentation
* form validation
* cancellation validation
* scheduling validation
* realtime reconciliation helpers
* permission/visibility helpers

## Component tests

Cover:

* driver workspace
* availability controls
* readiness state
* incoming offer
* accept/reject actions
* active trip
* pickup workflow
* trip completion
* cancellation
* earnings
* payout state
* notifications
* messaging
* profile/readiness surfaces

## Integration tests

Cover important flows:

* authenticated driver access
* availability transition
* incoming offer
* offer acceptance
* offer rejection
* trip assignment
* pickup progression
* active trip progression
* completion
* cancellation
* earnings refresh
* payout state
* scheduled assignment where supported
* realtime reconnect/reconciliation
* authorization failure

Use mocks/test providers when actual external infrastructure is unavailable.

Do not claim real external-provider validation when only mocked behavior was tested.

---

# 33. Documentation

Update the frontend documentation to reflect the actual driver implementation.

Document, where applicable:

* driver routes
* driver workspace structure
* availability/work-session behavior
* realtime event consumption
* dispatch-offer state model
* trip lifecycle UI
* location/browser limitations
* earnings/payout integration
* notification/messaging integration
* authorization boundaries
* driver-specific security/privacy considerations
* tests
* local-development requirements

Documentation must describe implemented behavior.

Do not create speculative documentation for features that were not implemented.

---

# OUT OF SCOPE

Do not implement unrelated domains.

Explicitly out of scope:

* rider account implementation
* rider trip-history implementation
* rider payment-method management
* rider receipts/promotions/refunds UI
* operations/admin dashboards
* support-agent tooling
* fleet-manager dashboards
* backend services
* database migrations/schema redesign
* dispatch-engine implementation
* payment-provider backend implementation
* routing-provider backend implementation
* infrastructure/Terraform
* Kubernetes/EKS
* CI/CD redesign
* cloud provisioning
* platform analytics dashboards
* a separate final-integration phase
* redesign of the overall frontend architecture

Do not create additional project phases to absorb work outside this scope.

---

# IMPLEMENTATION RULES

## Repository First

Inspect before modifying.

Determine the actual:

* frontend architecture
* route conventions
* component patterns
* auth/session implementation
* API client
* TanStack Query setup
* local state conventions
* websocket architecture
* maps abstraction
* testing setup
* styling system
* existing driver functionality

Preserve working behavior.

## No Pseudo-Code

Implement real working code.

Do not use:

* TODO implementations
* placeholders
* fake endpoints
* fake dispatch events
* fabricated trip transitions
* hard-coded driver identities
* hard-coded earnings
* fake payout completion
* mock success paths presented as production logic
* omitted implementations
* “implement similarly” instructions

## Backend Contract Discipline

Use documented contracts.

Do not invent:

* endpoint paths
* event names
* DTO fields
* enum values
* authorization behavior
* financial states
* trip transitions
* cancellation rules

when those are already defined by the repository.

## Financial Accuracy

All driver earnings and payout values must be backend-authoritative.

Do not calculate authoritative totals using frontend floating-point arithmetic.

Do not display final financial success before confirmation.

Do not blindly retry financial mutations.

## State-Machine Discipline

Only expose actions valid for the current backend trip state.

Do not bypass backend lifecycle rules.

## Realtime Discipline

Treat websocket events and API responses as coordinated state sources.

Implement deterministic reconciliation.

Avoid event-driven memory leaks and stale subscriptions.

## Security Discipline

Never weaken authorization, session protection, or privacy controls.

## Existing Code

Reuse existing abstractions where appropriate.

Do not build parallel:

* API clients
* websocket clients
* map systems
* notification systems
* trip state machines
* design systems

when equivalent infrastructure already exists.

---

# VALIDATION REQUIREMENTS

Before considering this volume complete:

1. Run formatting checks.
2. Run linting.
3. Run TypeScript/type checks.
4. Run relevant unit tests.
5. Run component tests.
6. Run relevant integration tests.
7. Run the production build or strongest available equivalent.
8. Verify protected driver routes.
9. Verify role/authorization boundaries.
10. Verify driver availability transitions.
11. Verify offer acceptance/rejection behavior.
12. Verify active-trip state transitions.
13. Verify cancellation behavior.
14. Verify realtime reconnect/reconciliation.
15. Verify location-permission and location-failure states.
16. Verify earnings/payout presentation.
17. Verify scheduled-trip behavior where implemented.
18. Verify responsive behavior.
19. Verify accessibility checks available in the repository.
20. Verify sensitive data is not exposed in browser storage or telemetry.
21. Verify no broken imports remain.
22. Verify no debug-only functionality remains.
23. Verify no TODO/placeholder production implementation was introduced.
24. Verify documentation matches the implementation.

Where the environment prevents a validation step, execute every available validation and explicitly report what could not be executed.

Never claim a deployment, cloud integration, or external-provider test that was not actually performed.

---

# INTEGRATION CHECK

Before finalizing, verify that the driver implementation integrates cleanly with the rest of the project.

Confirm that:

* driver routes coexist correctly with rider routes
* role-based navigation remains correct
* authenticated session handling remains shared and consistent
* driver availability uses the established backend contract
* dispatch offers integrate with the established dispatch/realtime model
* active-trip UI uses the canonical trip state machine
* location uses the established location abstraction
* maps use the established provider abstraction
* earnings use the established financial contracts
* payouts use the established payment/earnings contracts
* scheduled assignments use the established scheduling model
* notifications and messaging use existing platform infrastructure
* safety/support entry points connect to established contracts
* query keys remain properly scoped
* realtime events do not corrupt server state
* existing rider functionality remains intact
* the frontend remains compatible with later infrastructure and mobile integration

Every independent frontend milestone must combine cleanly into one coherent production-grade application.

---

# DEFINITION OF DONE

This volume is complete only when:

* driver workspace is implemented
* driver profile functionality in scope is implemented
* onboarding/readiness state is implemented
* availability/work-session functionality is implemented
* eligibility state is implemented
* location/browser integration is implemented where supported
* realtime connection is implemented
* dispatch offers are implemented
* accept/reject behavior is implemented
* assigned-trip workflow is implemented
* pickup workflow is implemented
* active-trip workflow is implemented
* trip completion is implemented
* driver cancellation/exception handling is implemented
* scheduled assignments are implemented where supported
* maps/navigation integration is implemented
* earnings are implemented
* earnings history is implemented
* payouts are implemented
* ratings/reputation are implemented
* notifications are implemented
* messaging is integrated where supported
* safety/support entry points are implemented
* loading/empty/error/degraded states are handled
* responsive layouts are complete
* accessibility requirements are addressed
* security/privacy requirements are addressed
* performance requirements are addressed
* meaningful tests are present
* documentation is updated
* validation has been performed
* actual limitations are documented
* no fake behavior is presented as production-ready
* no placeholders remain
* no unrelated scope was introduced

---

# IMPLEMENTATION REPORT

At the end of execution, provide a concise report containing:

## Files Changed

List created, modified, and removed files.

## Implemented Scope

Summarize the driver workspace, availability, offers, trip workflow, realtime, location, earnings, payouts, notifications, messaging, and other functionality actually implemented.

## Contracts Used

Identify the backend API, realtime, trip, dispatch, location, financial, scheduling, notification, and messaging contracts used.

## Validation

Report the exact validation commands executed and their results.

## Limitations

Report only actual environment or contract limitations.

Do not convert unavailable infrastructure into fake success.

## Follow-Up Dependencies

Report genuine dependencies on backend/repository capabilities where applicable.

Do not invent additional project phases.

---

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement the complete driver frontend scope defined by this prompt.

Preserve all working behavior that is outside the scope of necessary changes.

Use the repository's actual contracts and architecture as the source of truth.

Do not wait for another prompt.

Do not merely describe the implementation.

Create and modify the real production-grade code, tests, and documentation required for this scope.

Do not use pseudo-code, placeholders, fabricated APIs, fake dispatch behavior, fake trip completion, fake earnings, fake payouts, or simulated success presented as real functionality.

Respect the browser's real capabilities and limitations, especially for high-frequency location/background execution.

Validate the implementation as thoroughly as the environment permits.

Finish only when this volume is genuinely implemented and integrated into the repository.
