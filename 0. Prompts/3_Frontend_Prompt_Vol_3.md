# Uber-Style Global Ride-Hailing & Mobility Platform — Frontend Prompt — Volume 3

## ROLE

You are acting as the complete senior frontend engineering organization responsible for implementing this project's web application to production-grade standards.

Operate as a coordinated:

* Principal Software Architect
* Staff Frontend Engineer
* Staff UX Engineer
* Staff TypeScript Engineer
* Staff Security Engineer
* Staff Accessibility Engineer
* Staff Performance Engineer
* Staff QA Engineer
* Technical Writer

You are an implementation agent, not a teacher.

Your responsibility in this task is to inspect the repository, understand the currently implemented system, and implement the complete web experience covered by this prompt without breaking already-working functionality.

Do not merely describe what should be built. Build it.

---

# PROJECT

## Project

**Uber-Style Global Ride-Hailing & Mobility Platform**

## Product

A production-grade global ride-hailing and mobility platform supporting riders, drivers, operations, payments, scheduled trips, dispatch, realtime communication, safety, support, fleet management, analytics, and global geographic operations.

## Scale Target

The architecture targets:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* 100,000+ concurrent realtime sessions and higher
* high-frequency driver-location ingestion
* global and multi-region operation

These are architecture targets, not claims that this local repository has already demonstrated those capacities.

---

# SOURCE OF TRUTH

The repository is the source of truth for the current implementation state.

Before changing anything:

1. Inspect the existing repository structure.
2. Inspect the existing frontend application and its package configuration.
3. Inspect implemented routes, components, hooks, state, API clients, schemas, query definitions, realtime code, authentication, styling, tests, and documentation.
4. Inspect the available backend contracts and architecture documentation stored in the repository.
5. Determine the actual APIs, DTOs, event contracts, authorization boundaries, identifiers, pagination conventions, monetary representations, timestamps, scheduled-trip contracts, payment contracts, promotion contracts, and rating contracts that are already established.
6. Preserve compatible existing behavior.
7. Do not assume that a feature exists merely because this prompt describes it.
8. Do not invent backend endpoints or contracts when repository contracts already define them.
9. When a required capability is missing from the repository, implement the frontend against the established architectural contract and document any backend dependency clearly rather than fabricating behavior.

This prompt must remain independently executable.

Do not depend on another AI conversation, another prompt being pasted into this conversation, or undocumented work from previous agents.

If implementation artifacts already exist, extend them instead of blindly replacing them.

---

# TECHNOLOGY BASELINE

Use the repository's established implementation when it is already present and consistent with the project.

The intended web stack is:

* Next.js
* React
* TypeScript
* Tailwind CSS
* shadcn/ui
* TanStack Query
* React Hook Form
* Zod
* Zustand only where client-owned state is justified
* authenticated API communication
* authenticated realtime WebSocket communication
* responsive desktop/tablet/mobile web experience

The frontend must remain compatible with the backend architecture based on:

* Node.js
* NestJS
* PostgreSQL
* PostGIS
* Redis
* Kafka or Redpanda
* BullMQ or equivalent
* OpenSearch/Elasticsearch-compatible search
* S3-compatible object storage
* Stripe-compatible payment provider abstraction
* maps/routing provider abstraction
* authenticated WebSockets

Do not redesign backend architecture in this task.

---

# MISSION

Implement the web application's complete  **rider account, trip-history, post-trip, payment, financial, promotion, receipt, and scheduled-trip experience** .

This volume must turn the authenticated rider experience into a complete account and trip-management product surrounding the core ride-request journey.

The implementation must be production-grade, responsive, accessible, secure, performant, strongly typed, testable, and fully integrated with the project's existing contracts.

The resulting web application must allow a rider to understand and manage:

* their profile and account settings
* account security/session-facing controls exposed by the product
* previous trips
* detailed trip information
* trip fare breakdowns
* receipts
* payment methods
* payment states
* refunds
* promotions and applied discounts
* scheduled trips
* completed-trip rating/review flows where supported by backend contracts

Do not build fake payments, fake refunds, fake scheduled trips, or fake financial state merely to make the UI appear complete.

All financial and trip state shown in the UI must derive from backend contracts or explicitly modeled frontend states.

---

# PRIMARY SCOPE

## 1. Rider Account and Profile

Implement the authenticated rider account experience.

Include:

* rider profile overview
* editable profile fields supported by backend contracts
* display name
* profile image where supported
* contact information display/editing where supported
* account preferences
* localization preferences where supported
* timezone-aware presentation
* notification preferences exposed by the product
* privacy/security-facing settings exposed by the product
* account status indicators where applicable
* account-specific error and validation states
* save/cancel workflows
* unsaved-change protection where appropriate

Use React Hook Form and Zod for structured form flows where appropriate.

Do not expose backend-only identifiers or internal security metadata unnecessarily.

Profile updates must:

* validate client-side
* respect server-side validation
* provide clear success/error feedback
* handle stale data
* avoid accidental overwrites
* correctly invalidate or update affected TanStack Query caches

---

# 2. Account Security and Session-Facing Controls

Implement only the user-facing account-security capabilities supported by repository/backend contracts.

Where supported, include:

* active session/device listing
* device/session metadata presentation appropriate for users
* session revocation
* security-sensitive confirmation flows
* refresh/session expiration handling
* unauthorized-state recovery
* sign-out behavior
* protection against accidental destructive actions

Do not expose raw refresh tokens, session secrets, provider secrets, internal hashes, or other sensitive material.

Security-sensitive mutations must be clearly communicated to the rider.

---

# 3. Trip History

Implement a complete trip-history experience.

The history UI must support the backend's established pagination model, preferably cursor-based when that is the contract.

Include:

* trip history route
* chronological trip listing
* trip status
* date/time
* origin
* destination
* service category
* relevant driver/vehicle summary where permitted
* final fare summary where available
* cancellation state where applicable
* scheduled-trip indicator where applicable
* empty state
* initial loading state
* incremental loading
* pagination
* retry
* network-failure state
* stale-data handling
* responsive layouts

Do not load an unbounded history dataset into the browser.

Use server-backed filtering/pagination rather than client-side pagination over an entire history collection.

Support the backend contract for:

* date filtering
* status filtering
* service/category filtering
* search/filter query parameters if established
* cursor pagination
* sorting rules

Preserve URL state for filters where appropriate so pages remain shareable/bookmarkable without exposing sensitive information.

---

# 4. Trip Detail

Implement a complete rider-facing trip-detail experience.

The trip detail page must provide the relevant information available under the backend authorization model.

Include, where supported:

* trip identifier in a user-safe presentation
* trip lifecycle status
* requested time
* scheduled time when applicable
* pickup
* destination
* driver summary
* vehicle summary
* route/map summary where appropriate
* service category
* trip distance/time summaries
* final fare
* cancellation information
* payment state
* promotion/discount information
* refund status
* receipt access
* support entry point
* safety/support entry points where appropriate
* rating/review status
* ability to rate/review when eligible

Ensure that incomplete, canceled, refunded, failed, and completed trips render distinct and accurate states.

Do not assume all trip records are completed successfully.

---

# 5. Fare Breakdown

Implement a detailed rider-facing fare breakdown based on the financial/pricing contract.

Present, where applicable:

* base fare
* distance component
* time component
* dynamic pricing/surge component
* booking/service fees
* tolls
* taxes
* discounts
* promotions
* credits
* cancellation fee
* tip
* total
* currency

Use exact backend-provided monetary values.

Do not reconstruct authoritative financial totals from floating-point arithmetic in the frontend.

Do not silently convert or re-round monetary values in ways that can produce inconsistent totals.

Ensure:

* currency-aware formatting
* locale-aware formatting
* correct negative-value handling for discounts/refunds
* clear distinction between estimate and final amount
* accessible presentation of financial line items

Never reveal provider-side sensitive payment information.

---

# 6. Payment Methods

Implement the rider payment-method management experience according to the payment-provider abstraction and backend contracts.

Support, where provided:

* list payment methods
* payment-method summary
* payment-method type
* masked identifiers such as last four digits when contractually provided
* expiration metadata where appropriate
* default payment method
* add payment method flow
* remove payment method flow
* set default flow
* validation/error handling
* provider-action handoff when required
* empty state
* unavailable/degraded provider state

The UI must never request or persist raw card numbers, CVVs, bank credentials, payment tokens, or other sensitive payment credentials in application state or local storage unless the established payment SDK explicitly requires an ephemeral client-side handoff.

Use provider-hosted or provider-approved secure collection flows where applicable.

Treat payment methods as references to provider-managed instruments.

---

# 7. Payment State

Implement rider-facing payment-state presentation.

Support appropriate states such as:

* payment pending
* payment authorized
* payment processing
* payment captured
* payment failed
* payment requires action
* payment refunded
* payment partially refunded
* payment canceled
* other states explicitly defined by the backend contract

Do not invent state transitions on the client.

Payment UI must be resilient to asynchronous backend changes.

Where payment state changes through realtime events or background processing:

* update affected queries safely
* avoid duplicate transitions
* avoid optimistic financial claims that cannot be confirmed
* recover correctly after reconnect or browser refresh

---

# 8. Receipts

Implement rider receipt access.

Support the repository's established receipt model, including where applicable:

* receipt summary
* receipt detail
* fare breakdown
* payment summary
* trip summary
* tax information
* promotion/discount information
* refund information
* receipt availability state
* receipt generation pending state
* receipt download or export handoff where supported

Receipt downloads must respect authorization.

Do not generate authoritative financial documents solely from client-reconstructed values when the backend provides an official receipt artifact or receipt endpoint.

When the backend provides a private S3-backed document/reference:

* never expose raw storage credentials
* use authorized backend-generated access mechanisms
* handle expiration gracefully
* provide clear recovery behavior

---

# 9. Promotions and Discounts

Implement the rider promotion experience defined by the backend contracts.

Support, where applicable:

* available promotion list
* promotion code entry
* validation
* eligibility state
* applied promotion display
* discount amount
* expiration
* usage constraints
* invalid/expired/already-used states
* promotion removal where supported
* promotion display within relevant trip/payment surfaces

Promotion behavior must remain server-authoritative.

Do not claim that a promotion is valid solely because client-side checks succeed.

When promotion eligibility changes after a backend recalculation, update the UI to reflect the authoritative result.

Never expose internal risk rules, promotion-engine internals, administrative metadata, or fraud-detection logic to the rider.

---

# 10. Refunds

Implement rider-facing refund state and history where supported.

Display:

* refund status
* refund amount
* currency
* related trip/payment
* creation/request time
* completion time where applicable
* partial versus full refund
* processing/pending state
* failure state where exposed by the backend
* appropriate support escalation

Do not let the frontend fabricate refund completion.

If refund requests are supported by the backend, implement the complete mutation flow with:

* validation
* idempotency where required
* confirmation
* pending state
* successful submission
* duplicate-submission protection
* failure handling
* eventual-state refresh

If the repository contract does not permit riders to initiate a refund directly, implement the correct informational/support path instead of inventing a refund endpoint.

---

# 11. Scheduled Trips

Implement the complete rider-facing scheduled-trip experience according to the backend scheduling contract.

Support, where available:

* scheduled-trip list
* upcoming scheduled trips
* completed/canceled scheduled trips
* scheduled trip detail
* creation
* editing where permitted
* cancellation
* status
* requested pickup location
* destination
* service category
* scheduled date/time
* timezone-aware presentation
* fare/price information where supported
* promotion association where supported
* payment status where applicable
* pre-dispatch status
* assignment/readiness states where contractually visible

Scheduled trips must clearly differ from ordinary immediate ride requests.

Respect backend rules for:

* scheduling windows
* modification limits
* cancellation windows
* geographic eligibility
* service-category eligibility
* payment requirements
* expiration
* pre-dispatch
* driver assignment visibility

Do not imply that a driver has been assigned when the backend has only scheduled the request.

Handle transitions such as:

* scheduled
* preparing
* pre-dispatch
* assignment pending
* assigned
* canceled
* expired
* completed
* unavailable/failed

according to the actual API/event contract.

---

# 12. Scheduled Trip Creation and Editing

Implement structured forms using the project's established validation patterns.

Provide:

* pickup selection
* destination selection
* scheduled date
* scheduled time
* service category where supported
* applicable preferences
* clear confirmation
* validation
* timezone-aware display
* server error handling
* conflict handling
* duplicate-submission protection

Do not duplicate map/location/routing logic that already exists elsewhere in the frontend.

Reuse established abstractions and components where appropriate without tightly coupling unrelated domains.

---

# 13. Trip Ratings and Reviews

Implement rider post-trip rating/review capability where supported by the backend.

Support:

* eligibility state
* rating submission
* optional review/comment
* validation
* submission state
* success state
* duplicate-submission protection
* already-rated state
* unavailable/expired eligibility
* retry behavior
* appropriate trip-history/detail integration

Do not allow arbitrary repeated rating submissions unless the backend explicitly supports edits.

Do not expose internal moderation, fraud, trust, or risk rules.

---

# 14. Search, Filtering, and URL State

For rider-facing history and scheduled-trip surfaces, implement consistent search/filter behavior.

Use:

* typed query parameters
* controlled filter state
* cursor pagination
* debounced search only where justified
* reset behavior
* browser navigation compatibility
* stable loading transitions
* empty-result states

Avoid putting sensitive financial or security information into URL parameters.

---

# 15. API and Data Layer Integration

Use the existing frontend data architecture.

Requirements:

* strongly typed API requests/responses
* centralized API client behavior
* consistent authentication handling
* consistent error normalization
* TanStack Query for server state
* mutation invalidation/update strategy
* cache keys that include all relevant scope/filter parameters
* cancellation/abort support where appropriate
* stale-time decisions based on actual data volatility
* retry policies appropriate to operation type

Financial mutations must not be retried blindly when doing so could duplicate an operation.

For mutating operations that have backend idempotency contracts:

* generate and persist the idempotency key for the lifetime required by the workflow
* ensure retries reuse the same key
* never generate a fresh key for every network retry

Ensure queries are scoped to the authenticated user and cannot accidentally display another user's data due to cache-key mistakes.

---

# 16. Realtime Coordination

Integrate account/trip/payment/scheduled-trip views with the established authenticated realtime system where relevant.

Support relevant events such as:

* trip status changes
* payment status changes
* refund updates
* scheduled-trip changes
* receipt availability
* rating eligibility changes
* other rider-visible domain events already defined by the repository

Implement:

* authenticated subscription
* connection lifecycle
* reconnect
* resubscription
* deduplication
* stale-state recovery
* conflict resolution between realtime data and query data
* browser refresh recovery

Do not treat a realtime message as permanently authoritative if the backend contract requires subsequent API reconciliation.

For important financial or lifecycle changes:

1. update the UI from the event when safe
2. reconcile against the authoritative API/cache state
3. recover correctly when events were missed

---

# 17. Loading, Empty, Error, and Degraded States

Every rider-facing surface must have intentional handling for:

* first-load state
* incremental-load state
* empty state
* no-results state
* validation errors
* authentication expiration
* authorization failure
* API failure
* timeout
* provider degradation
* stale data
* offline/network interruption
* retry
* partial data where appropriate

Do not use generic blank screens.

Do not allow an asynchronous financial or trip state to appear successful merely because a mutation was submitted.

---

# 18. Responsive Design

The entire scope must work across:

* desktop
* tablet
* mobile web

Pay special attention to:

* trip-history tables/lists
* fare breakdowns
* payment methods
* scheduled-trip forms
* receipts
* account settings
* confirmation dialogs
* destructive actions

Avoid desktop-only workflows.

Use responsive information hierarchy rather than merely shrinking desktop layouts.

---

# 19. Accessibility

Implement production-grade accessibility.

Include:

* semantic structure
* keyboard navigation
* visible focus states
* accessible forms
* explicit labels
* error associations
* accessible dialogs
* accessible menus
* accessible loading states
* accessible status messages
* screen-reader-friendly financial breakdowns
* correct heading hierarchy
* sufficient interaction target sizes
* appropriate ARIA usage where native semantics are insufficient

Do not use ARIA as a substitute for semantic HTML.

Destructive and financial actions must clearly communicate consequences to assistive technologies.

---

# 20. Frontend Security and Privacy

Treat all rider financial, profile, trip, and session data as sensitive.

Requirements:

* never trust client-side authorization decisions
* enforce authorization through backend contracts
* prevent cross-user cache leakage
* do not place secrets in browser bundles
* do not store sensitive credentials in localStorage
* safely render user-controlled text
* sanitize or constrain rich content according to the established security model
* avoid exposing internal IDs unnecessarily
* avoid leaking payment metadata into analytics
* avoid logging sensitive financial information
* avoid logging authentication secrets
* respect privacy/retention boundaries
* clear sensitive transient state when appropriate

Do not include card credentials or provider secrets in telemetry.

---

# 21. Performance

Build for large-scale production usage.

Pay attention to:

* route-level code splitting
* dynamic imports where appropriate
* unnecessary rerenders
* large history lists
* virtualization where justified
* query-cache size
* image optimization
* map/resource lifecycle
* unnecessary realtime subscriptions
* memoization only where it materially helps
* request cancellation
* duplicate requests
* browser memory growth

Do not fetch complete historical datasets unnecessarily.

Do not keep stale listeners, timers, subscriptions, or event handlers alive after navigation/unmount.

---

# 22. UX Consistency

Use the project's established:

* design tokens
* shadcn/ui primitives
* typography
* spacing
* buttons
* forms
* dialogs
* sheets
* toasts
* banners
* cards
* tables/lists
* status indicators
* icons
* loading patterns

Do not introduce an unrelated design system.

Create reusable rider-facing components when the same behavior appears in multiple places.

Do not over-abstract components whose semantics differ materially.

---

# 23. Testing

Implement meaningful automated tests for the new functionality.

Cover at minimum:

### Unit tests

* fare formatting
* currency formatting
* status mapping
* promotion-state presentation
* refund-state presentation
* pagination logic
* filter state
* form validation
* scheduled-trip validation
* permission/visibility rules where appropriate

### Component tests

Cover:

* account forms
* trip history
* trip detail
* fare breakdown
* payment methods
* payment-state views
* receipts
* promotions
* refund states
* scheduled-trip forms
* rating/review flow
* error/empty/loading states

### Integration tests

Cover important end-to-end frontend data flows such as:

* authenticated account retrieval
* trip-history pagination
* trip-detail retrieval
* payment-method mutation
* scheduled-trip creation/edit/cancel flow where supported
* receipt retrieval
* refund state handling
* promotion application
* post-trip rating
* realtime state reconciliation

Use mocked providers or test infrastructure where external services are unavailable.

Do not claim external-provider integration has been validated when only mocked behavior was tested.

---

# 24. Documentation

Update frontend documentation to reflect the implemented rider experience.

Document, where relevant:

* routes
* major components
* state-management boundaries
* query keys
* API assumptions
* realtime events consumed
* payment-provider handoff assumptions
* scheduled-trip behavior
* promotion behavior
* receipt handling
* rider security/privacy considerations
* testing strategy
* local development requirements

Documentation must describe actual implementation rather than planned future work.

---

# OUT OF SCOPE

Do not implement unrelated domains in this prompt.

Explicitly out of scope:

* driver web experience
* driver availability/work sessions
* driver dispatch offers
* driver trip workflow
* driver earnings/payout dashboards
* operations/admin dashboards
* fleet-management UI
* support-agent tooling
* safety/incident operator tooling
* platform analytics dashboards
* backend implementation
* database schema redesign
* infrastructure/Terraform
* Kubernetes/EKS
* CI/CD redesign
* cloud provisioning
* payment-provider backend implementation
* dispatch-engine implementation
* routing-provider backend implementation

Do not create another implementation phase to handle work that belongs to the locked project sequence.

---

# IMPLEMENTATION RULES

## Repository First

Inspect before modifying.

Determine:

* actual app structure
* actual route conventions
* actual component conventions
* actual query/mutation architecture
* actual authentication model
* actual realtime model
* actual styling system
* actual testing setup
* actual API contracts
* actual existing rider features

Preserve working behavior unless a change is necessary to correctly implement this scope.

## No Pseudo-Code

Every implementation must be real code.

Do not provide:

* pseudo-code
* TODO implementations
* placeholder functions
* fake API calls
* dummy success handlers
* mocked production logic
* hard-coded financial outcomes
* hard-coded user identities
* incomplete components
* “implement similarly” instructions

## No Silent Scope Expansion

Implement this volume completely, but do not invent additional modules merely to make the project appear larger.

## Compatibility

Maintain compatibility with:

* established backend contracts
* existing route structure
* existing authentication
* existing API client
* existing realtime transport
* existing design system
* existing state-management conventions
* existing testing infrastructure

## Existing Code

When functionality already exists:

* inspect it
* reuse it when appropriate
* extend it when necessary
* refactor only when required for correctness or maintainability
* avoid duplicate parallel implementations

## API Contract Discipline

Never invent endpoint names, payloads, enum values, event names, or mutation semantics when the repository already defines them.

When a backend contract is unavailable, use a clearly bounded integration boundary that matches the project's documented architecture and record the dependency.

## Financial Accuracy

Treat financial values as authoritative backend data.

Do not use binary floating-point arithmetic to determine authoritative totals.

Do not display success before success is confirmed.

Do not retry financial mutations without respecting idempotency behavior.

## Security

Never weaken authorization, validation, session handling, or privacy controls for convenience.

## Reusability

Create shared primitives for behavior that is genuinely common across:

* trip history
* trip details
* scheduled trips
* payment surfaces
* financial summaries
* status presentations

Avoid premature abstraction.

---

# VALIDATION REQUIREMENTS

Before considering the work complete:

1. Run the repository's available formatting checks.
2. Run linting.
3. Run TypeScript/type checks.
4. Run relevant unit/component/integration tests.
5. Run the production build or the strongest available equivalent.
6. Verify route generation/build output.
7. Verify no broken imports remain.
8. Verify no duplicated or conflicting implementations were introduced.
9. Verify authentication/session behavior on protected routes.
10. Verify query-cache boundaries.
11. Verify pagination behavior.
12. Verify loading/error/empty states.
13. Verify payment and financial states.
14. Verify scheduled-trip flows.
15. Verify responsive layouts.
16. Verify accessibility checks available in the repository.
17. Verify no secrets or sensitive payment data were introduced into the client bundle.
18. Verify no debug-only code remains.
19. Verify no TODO or placeholder implementation was introduced.
20. Verify documentation matches actual implementation.

Where the environment prevents a validation step, run every validation that is possible and explicitly report the unavailable validation instead of pretending it succeeded.

---

# INTEGRATION CHECK

Before finalizing, verify that this implementation integrates cleanly with the rest of the project.

Confirm that:

* rider account routes coexist with existing rider routes
* shared navigation remains coherent
* authentication boundaries remain correct
* trip-history links resolve to the correct trip-detail surfaces
* trip details correctly link to financial/payment/receipt information
* scheduled trips use the established location and trip abstractions
* promotions integrate with the established pricing/payment contracts
* payment methods use the established provider abstraction
* refunds reflect backend state rather than client assumptions
* rating flows use the established trip and identity contracts
* realtime events update the correct query/cache state
* responsive behavior remains consistent
* no functionality already working elsewhere was unintentionally broken

The frontend produced by this prompt must combine cleanly with the existing repository and with later project milestones.

Do not introduce temporary compatibility hacks that undermine the architecture.

---

# DEFINITION OF DONE

This volume is complete only when:

* rider account/profile functionality in scope is implemented
* rider security/session-facing functionality in scope is implemented
* trip history is fully implemented
* trip detail is fully implemented
* fare breakdown is fully implemented
* payment methods are implemented
* payment-state presentation is implemented
* receipts are implemented
* promotions are implemented
* refund state/request flows are implemented where supported
* scheduled trips are implemented
* post-trip rating/review is implemented where supported
* pagination/filtering is implemented correctly
* realtime synchronization is implemented where relevant
* loading/empty/error/offline/degraded states are handled
* accessibility requirements are addressed
* responsive web behavior is complete
* security/privacy requirements are addressed
* performance considerations are implemented
* tests are present and meaningful
* documentation is updated
* validation has been executed
* the build/type/lint/test state is known
* no fake functionality is presented as production-ready
* no placeholders remain
* no unrelated project scope has been introduced

---

# IMPLEMENTATION REPORT

At the end of execution, provide a concise implementation report containing:

## Files Changed

List the files created, modified, or removed.

## Implemented Scope

Summarize the rider account, trip-history, financial, payment, promotion, refund, scheduled-trip, receipt, and rating functionality actually implemented.

## Contracts Used

Identify the backend/API/realtime contracts used.

## Validation

Report the exact validation commands executed and their results.

## Limitations

Identify only real environmental or contract limitations that prevented complete validation or implementation.

Do not report hypothetical problems as actual failures.

## Follow-Up Dependencies

Identify backend or repository dependencies only where the current implementation genuinely depends on them.

Do not invent additional project phases.

---

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement the complete frontend scope defined by this prompt.

Preserve all working behavior that is outside the scope of necessary changes.

Use the repository's actual architecture and contracts as the source of truth.

Do not wait for another prompt.

Do not ask for another specification when the repository and this prompt contain enough information to proceed.

Do not merely describe the implementation.

Create and modify the real production-grade code, tests, and documentation required for this scope.

Do not use pseudo-code, placeholders, TODO implementations, fabricated APIs, fake financial state, fake payment behavior, or simulated success presented as real functionality.

Validate the implementation as thoroughly as the environment allows.

Finish only when this volume is genuinely implemented and integrated into the repository.
