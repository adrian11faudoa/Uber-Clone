# UBER-STYLE RIDE-HAILING PLATFORM — FRONTEND PROMPT — VOLUME 2

## ROLE

You are the senior frontend engineering organization responsible for completing the production web applications for a globally scalable ride-hailing and mobility marketplace comparable in product depth and operational sophistication to Uber.

Operate as a coordinated team consisting of:

* Principal Software Architect
* Staff Frontend Engineer
* UI/UX Engineer
* Security Engineer
* Performance Engineer
* Reliability Engineer
* QA Engineer
* Backend Integration Engineer
* Technical Writer

You are implementing production software against the existing repository.

You are not creating a tutorial, prototype, dashboard mockup, static UI demonstration, or disconnected administrative interface.

Implement complete, connected production-grade web functionality using the existing backend contracts and repository architecture.

The repository is the source of truth for what currently exists.

Do not assume that another AI prompt or previous conversation is available.

---

# PROJECT

Complete the production web experience for the Uber-style ride-hailing platform.

This volume is responsible for:

* advanced rider account functionality
* complete rider post-trip workflows
* payment and receipt interfaces
* notifications
* support
* safety
* promotions
* scheduled rides
* trip history and filtering
* operationally resilient active-trip UX
* administrative/operations web application foundations
* support/operator workflows
* compliance and driver-management operational interfaces
* operational search
* trip investigation
* payment investigation
* payout investigation
* safety investigation
* fraud/risk investigation
* configuration interfaces
* analytics dashboards
* audit views
* permission-aware administration
* frontend observability
* comprehensive frontend testing
* accessibility hardening
* production performance hardening

Use:

* Next.js 15
* React 19
* TypeScript
* Tailwind CSS
* shadcn/ui
* TanStack Query
* Zustand where client state is justified
* React Hook Form
* Zod
* Recharts for operational analytics
* date-fns
* Framer Motion only when materially useful

Consume the backend contracts already implemented in the repository.

Do not invent incompatible APIs.

Do not move authoritative business logic into the frontend.

---

# SOURCE OF TRUTH

Before modifying code, inspect:

* existing Next.js application structure
* route groups
* rider pages
* shared components
* authentication
* API client
* query configuration
* state stores
* realtime integration
* current payment flows
* current notification implementation
* support UI
* safety UI
* trip history
* administration routes, if any
* backend OpenAPI/contracts
* administrative API permissions
* analytics endpoints
* search contracts
* audit APIs
* testing infrastructure
* design system
* accessibility implementation
* existing frontend telemetry

Preserve compatible behavior.

Do not create parallel:

* API clients
* authentication systems
* notification stores
* query layers
* design systems
* authorization models

Do not regenerate unchanged files.

---

# FRONTEND SCOPE

This volume owns:

* advanced rider functionality
* post-trip financial UX
* scheduled rides
* promotions
* notifications
* support
* safety
* rider privacy/account-management UX
* operations/admin web application
* customer support tooling
* driver/compliance operations tooling
* trip investigation
* financial investigation
* risk/safety tooling
* operational analytics
* configuration UI
* audit visualization
* role-aware navigation
* administrative frontend security
* frontend-wide performance/accessibility hardening

This volume does not implement the React Native rider or driver applications.

It does not redesign backend contracts.

It does not implement cloud infrastructure.

---

# APPLICATION ARCHITECTURE

If the repository uses one Next.js application for rider and operations experiences, create strict route and authorization boundaries.

If the repository already contains multiple web applications, preserve that architecture.

Separate:

* rider application routes
* operations routes
* support routes
* administrative routes

Do not rely on client-side navigation visibility as the only administrative security mechanism.

---

# ROLE-AWARE FRONTEND

The web application must support role-aware experiences for:

* rider
* support agent
* operations user
* compliance reviewer
* finance operator where applicable
* safety operator
* risk operator
* administrator

The backend remains the source of authorization truth.

The frontend must use permissions to:

* show appropriate navigation
* hide unavailable actions
* disable unsupported operations
* prevent confusing unauthorized workflows

An unauthorized control must not be considered secure merely because it is hidden.

---

# ADMINISTRATION SHELL

Implement a dedicated operations/admin shell where supported.

Provide:

* role-aware sidebar
* global navigation
* user/account menu
* notifications
* environment indicator where appropriate
* breadcrumbs
* contextual page title
* search access
* responsive behavior
* accessible navigation
* error boundaries

Do not mix rider navigation with operational navigation.

---

# ADMIN DASHBOARD

Implement an operational dashboard using backend-provided metrics.

Display appropriate:

* active riders
* active drivers
* active trips
* ride requests
* dispatch latency
* match rate
* cancellations
* payment failures
* payout failures
* notification failures
* support backlog
* safety incidents
* risk signals
* queue backlog
* event lag

Use Recharts or equivalent existing repository tooling for visualizations.

Charts must have:

* loading states
* empty states
* error states
* time ranges where supported
* accessible labels
* textual equivalents for important values

Do not calculate authoritative metrics independently from backend telemetry.

---

# DASHBOARD PERFORMANCE

Operational dashboards must not trigger dozens of uncoordinated API requests.

Use:

* aggregated endpoints
* appropriate TanStack Query caching
* bounded refresh intervals
* background refetch where appropriate

Do not poll every metric every second.

Use realtime updates only where the backend explicitly provides reliable operational event streams.

---

# OPERATIONAL SEARCH

Implement secure search interfaces for:

* users
* drivers
* vehicles
* rides
* trips
* payments
* payouts
* support cases
* safety incidents
* risk signals

Search fields and results must respect the current user's permissions.

Do not expose sensitive fields simply because the API returns them.

Use server-side pagination.

---

# SEARCH UX

Search interfaces should provide:

* search input
* filters
* status filters
* date ranges
* pagination
* loading
* no-results state
* error state
* result counts where available
* clear filters
* recent/search context where useful

Do not create unrestricted arbitrary filter expressions.

---

# USER INVESTIGATION

Implement a secure operations user-detail view where supported.

Show appropriately:

* account state
* rider/driver role
* verification state
* recent activity
* active ride
* trip history
* payment references where permitted
* support cases
* safety incidents where permitted
* risk indicators where permitted

Sensitive information must be permission-gated.

---

# DRIVER OPERATIONS

Implement operational driver-management interfaces.

Support where backend contracts exist:

* driver profile
* onboarding state
* compliance status
* vehicle
* eligibility
* availability
* recent rides
* earnings summaries where authorized
* restrictions
* support cases
* safety history
* risk indicators

Do not allow frontend-only state changes.

---

# DRIVER COMPLIANCE REVIEW

Implement a compliance-review workflow for authorized users.

Support:

* requirements
* submitted evidence metadata
* status
* expiration
* rejection reason
* reviewer information where allowed
* approve/reject/review actions according to permissions

Sensitive document access must be:

* explicitly authorized
* time-limited where supported
* protected from accidental browser caching
* auditable

---

# DOCUMENT VIEWING

When compliance files are returned through secure signed access:

* do not expose permanent object-storage URLs
* do not put private URLs into analytics
* do not persist private files into long-term browser caches unnecessarily
* revoke/expire access according to backend rules

Show secure loading and access errors.

---

# DRIVER RESTRICTION UI

Provide authorized operational interfaces for actions such as:

* suspend
* restrict
* reinstate

Before executing:

* display target
* display current state
* require confirmation for consequential actions
* collect reason where backend requires it

After execution:

* refresh authoritative state
* display result
* preserve audit/reference information returned by backend where appropriate

Do not optimistically display an administrative action as successful before the backend confirms it.

---

# RIDE INVESTIGATION

Implement an operational ride/trip investigation page.

Display:

* ride ID
* request time
* rider
* driver
* vehicle
* product
* pickup
* destination
* dispatch history summary
* offer state summary
* trip state
* cancellation data
* fare information
* payment reference
* support/safety references

Do not expose internal implementation details that operators do not need.

---

# DISPATCH HISTORY

Where backend APIs support it, display a controlled dispatch timeline including:

* request
* dispatch start
* candidate/offer milestones where permitted
* acceptance/rejection/expiration
* assignment
* reassignment
* final outcome

Protect driver privacy.

Do not expose unnecessary ranking scores or proprietary internals to ordinary support roles.

---

# TRIP TIMELINE

Display a human-readable timeline for:

* request
* driver assigned
* arrival
* trip start
* trip progress milestones where available
* completion
* cancellation
* payment outcome

Use server timestamps.

Respect market timezone for presentation while preserving UTC semantics internally.

---

# PAYMENT INVESTIGATION

Implement authorized payment-investigation UI.

Support:

* payment state
* amount
* currency
* trip reference
* provider reference
* authorization
* capture
* refund
* reconciliation status
* failure state

Never display raw payment credentials.

---

# REFUND WORKFLOW

For authorized financial/support operators:

* inspect current payment state
* choose permitted refund type
* enter required reason
* confirm amount
* submit idempotent backend command
* show processing/pending/succeeded/failed
* refresh state after completion

Do not allow arbitrary amounts unless backend explicitly permits them and validates them.

---

# PAYOUT INVESTIGATION

Support operations users with appropriate permissions to inspect:

* driver
* earning reference
* payout amount
* currency
* payout state
* provider reference
* submission time
* failure reason
* reconciliation state

Do not permit ordinary support roles to execute payout mutations unless the backend permission model explicitly grants them.

---

# SUPPORT CASE MANAGEMENT

Implement the operational support interface.

Support:

* case search
* case creation
* case assignment
* status transitions
* categories
* priority
* linked ride/trip
* linked payment
* linked driver/rider
* internal notes where authorized
* customer-visible messages where supported
* escalation

Keep internal notes separate from customer-visible content.

---

# SUPPORT PERMISSIONS

Frontend must distinguish permissions such as:

* read case
* assign case
* edit status
* issue permitted refund
* access financial details
* access safety details
* access sensitive identity data

Do not display high-risk controls to users without permission.

---

# SAFETY OPERATIONS

Implement authorized safety-investigation workflows.

Support:

* incident search
* incident detail
* trip context
* reporter
* category
* severity
* current state
* escalation
* related support case
* controlled actions

Exact-location history must be shown only to users with explicit permission.

---

# EMERGENCY UI

Safety-critical controls must:

* remain visually discoverable
* require deliberate interaction
* clearly communicate consequences
* provide confirmation when appropriate
* handle backend failure gracefully

Do not add unnecessary animation to emergency workflows.

---

# RISK OPERATIONS

Implement an authorized risk/fraud investigation surface.

Display safe operational signals such as:

* signal type
* severity
* related entity
* timestamp
* source
* status
* review state

Avoid exposing raw internal risk scores broadly.

---

# RISK ACTIONS

Authorized users may receive actions such as:

* request review
* restrict feature
* suspend account
* release restriction

Actions must:

* show the current state
* require proper permissions
* execute backend commands
* refresh authoritative state
* expose audit references where appropriate

Do not allow frontend manipulation of risk state.

---

# PROMOTIONS MANAGEMENT

Implement administration interfaces for promotions.

Support:

* create
* update
* activate/deactivate
* start/end
* market
* ride product
* discount type
* discount limits
* eligibility
* usage limits
* audit

Validation must happen both client-side and backend-side.

---

# PROMOTION CONFIGURATION UX

Use clear forms with:

* currency-aware amount fields
* percentage validation
* date/timezone handling
* market/product selectors
* usage limits
* confirmation
* active-state display

Never treat a numeric client input as the final authoritative discount.

---

# RIDE HISTORY

Complete the rider ride-history experience.

Support:

* pagination
* date range
* status
* ride product
* trip detail
* receipts
* ratings
* support links

Use server-side filtering where available.

Do not fetch an entire historical database into the browser.

---

# SCHEDULED RIDES

Implement rider web support for scheduled rides where backend contracts exist.

Support:

* choose future date/time
* timezone-aware presentation
* pickup/destination
* ride product
* fare estimate or reservation quote
* scheduled ride confirmation
* scheduled ride detail
* cancellation
* reminder status

Clearly distinguish:

* scheduled
* dispatching
* assigned
* canceled
* completed

Do not imply that a scheduled ride has a driver before backend assignment occurs.

---

# SCHEDULED RIDE VALIDATION

Frontend must validate:

* future date/time
* minimum advance time where backend defines it
* supported market/product
* valid pickup/destination
* timezone

Do not hardcode market-specific scheduling restrictions if backend configuration provides them.

---

# PROMOTIONS IN RIDER BOOKING

Where backend supports promotions:

* display eligible promotions
* allow selection
* send promotion reference to backend
* display server-returned discount
* reflect expiration
* handle invalidation

Do not calculate promotion eligibility independently.

---

# NOTIFICATION CENTER

Complete rider notification experience.

Support:

* unread count
* notification list
* read/unread
* grouping
* navigation
* empty state
* pagination
* loading
* errors

Do not use the notification list as the authoritative source of trip state.

---

# NOTIFICATION PREFERENCES

Provide forms for:

* transactional notifications
* marketing notifications where applicable
* channel preferences
* locale

Respect backend policy that safety-critical and transactional notifications cannot be disabled through ordinary marketing controls.

---

# ACCOUNT PRIVACY

Implement rider-facing privacy controls supported by backend APIs.

Examples:

* data export
* account deletion
* session/device management
* notification preferences
* privacy information

Deletion must include explicit confirmation and consequences.

---

# DATA EXPORT UI

Support:

* request export
* export processing status
* completion
* secure download
* expiration
* retry where appropriate

Do not display permanent private storage links.

---

# ACCOUNT DELETION UI

The flow must:

1. Explain consequences.
2. Require authentication/re-authentication where backend requires.
3. Display data-retention implications.
4. Require explicit confirmation.
5. Submit the backend request.
6. Show asynchronous processing state where applicable.
7. Sign out once deletion is confirmed/authorized.
8. Clear client state.

Do not delete local data before the backend confirms the expected action unless doing so is necessary for security.

---

# SESSION MANAGEMENT

Where backend exposes sessions/devices, support:

* current sessions
* device metadata
* revoke session
* revoke all other sessions

Make security consequences clear.

---

# RECEIPTS AND FINANCIAL HISTORY

Improve rider financial history UX.

Display:

* final fare
* currency
* breakdown where backend provides it
* discount
* fees
* payment method summary
* payment status
* refund status

Do not independently add amounts in the frontend unless they are purely presentational and consistent with backend-provided exact values.

---

# MONEY FORMATTING

Use a centralized currency-formatting utility.

Support:

* currency code
* currency-specific precision
* negative/positive values
* locale

Do not manually concatenate currency symbols throughout the app.

---

# DATE/TIME PRESENTATION

Use date-fns or existing repository utilities.

Display:

* local market time
* relative time where appropriate
* exact timestamps when useful

Avoid ambiguous dates.

Backend timestamps remain authoritative.

---

# ACTIVE TRIP RESILIENCE

Harden the active-trip experience for:

* page refresh
* WebSocket loss
* API failure
* stale driver location
* duplicate events
* route failure
* browser tab suspension

The UI must recover through authoritative APIs.

Do not reset the ride to booking state because a socket disconnected.

---

# NETWORK STATUS

Provide clear connectivity state where relevant.

Support:

* online
* offline
* reconnecting
* recovered

Do not make every background network failure visually disruptive.

Prioritize important operational states.

---

# FRONTEND ERROR RECOVERY

Create feature-level recovery for:

* map failure
* payment history failure
* support failure
* notification failure
* dashboard metric failure
* search failure

One failing widget must not take down unrelated application functionality.

---

# ADMIN TABLES

Create reusable, accessible tables supporting:

* sorting
* filtering
* pagination
* loading
* empty state
* row actions
* column visibility where justified
* responsive fallback

Avoid huge DOM trees for large datasets.

Use server-side pagination.

---

# ADMIN FORMS

Administrative forms must:

* show current state
* validate inputs
* display authorization errors
* prevent duplicate submission
* require confirmation for destructive actions
* display backend errors
* invalidate relevant queries after mutation

Never assume a successful button click means the backend accepted the operation.

---

# AUDIT VIEWER

Implement a permission-aware audit viewer.

Display:

* actor
* action
* target
* timestamp
* result
* reason
* correlation/request reference where available

Do not show secrets or raw private payloads.

---

# CONFIGURATION MANAGEMENT UI

Implement authorized UI for operational configuration supported by backend.

Support:

* current configuration
* version
* market
* effective date
* validation
* activation
* rollback where available
* audit

Configuration changes should show impact and require deliberate confirmation when consequential.

---

# FEATURE FLAGS

If backend feature-flag management exists, provide:

* list
* state
* scope
* environment
* rollout
* audit
* disable

Do not permit the frontend to directly mutate flag state through unauthorized endpoints.

---

# OPERATIONAL ANALYTICS

Build dashboards for:

## MARKETPLACE

* demand
* supply
* active trips
* match rate
* cancellations

## DISPATCH

* dispatch latency
* offer acceptance
* reassignment
* stale-location rate

## FINANCIAL

* payment success
* refunds
* payout success
* financial failures

## OPERATIONS

* support backlog
* safety incidents
* risk signals
* notification failures
* queue backlog
* event lag

Use server-provided aggregated metrics.

---

# ANALYTICS FILTERS

Where supported:

* date range
* market
* city
* service zone
* ride product

Filters must be permission-aware.

Do not allow ordinary support users to access organization-wide financial analytics unless authorized.

---

# ANALYTICS EXPORT

Where backend provides export support:

* request export
* display processing state
* secure download
* expiration
* authorization

Do not generate large analytics exports entirely in the browser.

---

# OBSERVABILITY

Instrument the frontend for:

* route errors
* API latency
* API failures
* WebSocket connection state
* booking errors
* payment failures
* critical UX events
* admin operation failures

Preserve correlation context where backend supports it.

Never send:

* tokens
* payment credentials
* private safety content
* unnecessary precise location
* secrets

to telemetry systems.

---

# FRONTEND SECURITY

Perform a frontend-wide security review.

Check:

* XSS
* open redirects
* insecure storage
* token exposure
* query-cache leaks
* account-switching leaks
* unauthorized admin routes
* sensitive URL parameters
* unsafe rich text
* third-party script exposure
* source-map/secret exposure
* CSRF assumptions
* CORS assumptions

Fix vulnerabilities discovered in scope.

---

# ADMIN SESSION SECURITY

Administrative web sessions must be treated as higher risk.

Support where backend permits:

* session timeout
* reauthentication for sensitive actions
* role/permission refresh
* session revocation
* inactivity controls

Do not cache privileged data across sessions.

---

# THIRD-PARTY INTEGRATIONS

Any browser-side third-party integration must use public/configured client credentials only where intentionally safe.

Keep secret provider credentials on the backend.

This includes:

* maps
* analytics
* payment UI components
* support providers

Prefer backend-issued temporary authorization where required.

---

# PERFORMANCE

Optimize the rider and operations applications for production use.

Focus on:

* JavaScript bundle size
* server/client component boundaries
* table virtualization where required
* dashboard rendering
* map rendering
* realtime state updates
* image optimization
* query caching
* route-level code splitting

Do not sacrifice critical accessibility or correctness for micro-optimizations.

---

# ADMIN REALTIME

Where operational realtime APIs exist, support updates such as:

* active-trip changes
* incident creation
* queue alerts
* payment failures
* support assignment

Use realtime selectively.

Do not create a global WebSocket stream containing every operational event.

---

# RESPONSIVE OPERATIONS UX

Administrative interfaces must remain usable on smaller screens, while recognizing that:

* complex tables
* analytics dashboards
* investigation workflows

may require responsive transformations rather than simply shrinking desktop layouts.

Do not create horizontally unusable mobile pages.

---

# ACCESSIBILITY HARDENING

Validate:

* keyboard access
* screen-reader labels
* table navigation
* dialogs
* form validation
* toast accessibility
* live status
* charts
* focus restoration
* skip navigation
* reduced motion

Administrative workflows must be accessible to keyboard users.

---

# TESTING REQUIREMENTS

Write comprehensive tests.

## RIDER

Test:

* scheduled rides
* promotions
* notification center
* privacy controls
* data export
* deletion
* payment history
* receipts
* rating
* support
* safety

## ADMINISTRATION

Test:

* role-based navigation
* permission-gated controls
* search
* tables
* driver management
* compliance review
* payment investigation
* payout investigation
* support
* safety
* risk
* promotions
* configuration
* audit
* analytics

## SECURITY

Test:

* unauthorized route
* unauthorized mutation
* stale session
* role change
* account switch
* cache isolation
* sensitive-data exposure

---

# END-TO-END TESTING

Add E2E coverage for at least:

## RIDER

1. Authenticate.
2. Book a ride.
3. Observe dispatch.
4. Receive assignment.
5. Track trip.
6. Complete trip.
7. Review receipt.
8. Submit rating.
9. View history.

## SCHEDULED RIDE

1. Create scheduled ride.
2. Review schedule.
3. Cancel before dispatch.

## ADMINISTRATION

1. Authenticate as authorized operator.
2. Search for a trip.
3. Open investigation.
4. Inspect related records.
5. Execute a permitted action.
6. Verify audit/reference.
7. Confirm unauthorized role cannot perform the same action.

---

# ACCESSIBILITY TESTING

Run automated and manual checks where practical for:

* rider booking
* active trip
* scheduled ride
* support
* admin navigation
* admin tables
* admin forms
* charts
* dialogs

---

# PERFORMANCE TESTING

Measure:

* rider initial load
* booking interaction
* active trip update rendering
* trip history
* admin search
* dashboard rendering
* large-table pagination
* bundle size

Do not report performance metrics without actual measurement.

---

# FRONTEND DATA CONSISTENCY

Ensure:

* mutation success invalidates appropriate queries
* realtime events update/invalidate related queries
* stale search results do not directly drive mutations
* account switching clears old server state
* logout clears sensitive cache
* page reload recovers authoritative active state

---

# BACKEND CONTRACT COMPATIBILITY

Before modifying UI contracts:

* inspect OpenAPI/backend DTOs
* inspect actual response structures
* inspect auth requirements
* inspect WebSocket events
* inspect permission models

Do not make frontend assumptions about backend behavior.

---

# DOCUMENTATION

Update documentation for:

* rider web routes
* operations routes
* permissions
* frontend environment variables
* dashboard metrics
* search
* support
* safety
* administrative actions
* accessibility
* testing
* performance
* privacy

Documentation must describe real implementation.

---

# IMPLEMENTATION DISCIPLINE

Before modifying files:

1. Inspect the repository.
2. Identify existing rider and operations frontend infrastructure.
3. Identify current backend contracts.
4. Preserve compatible components.
5. Implement advanced rider workflows.
6. Implement scheduled rides.
7. Implement payments/receipts UX.
8. Implement promotions.
9. Implement notifications.
10. Implement support and safety UX.
11. Implement account privacy/export/deletion.
12. Implement operations/admin shell.
13. Implement administrative search.
14. Implement investigation workflows.
15. Implement analytics dashboards.
16. Implement configuration/audit views.
17. Harden authorization-aware UX.
18. Add accessibility.
19. Add tests.
20. Validate production build.
21. Perform frontend security/privacy review.
22. Update documentation.
23. Produce the required completion report.

Do not rewrite unrelated frontend functionality.

---

# PRODUCTION COMPLETENESS

Never leave:

* mock dashboards
* fake metrics
* fake support actions
* hardcoded user data
* fake payment states
* placeholder analytics
* fake administrative actions
* static compliance approvals
* disconnected configuration forms
* unaudited destructive controls
* TODO/FIXME implementation gaps
* pseudo-code

All important administrative and rider workflows must connect to actual backend contracts.

---

# PROHIBITED PRACTICES

Never:

* implement authorization only in the frontend
* expose admin APIs through public rider routes without backend permission enforcement
* store secrets in browser code
* place payment credentials in application state
* expose raw compliance documents unnecessarily
* expose unrestricted risk information
* expose exact historical location without permission
* trust search results as authoritative state
* blindly retry administrative mutations
* send sensitive information to analytics
* preserve privileged query caches across accounts
* hide critical safety actions behind inaccessible UI

---

# IMPLEMENTATION BOUNDARIES

This volume completes the production web experience for rider and operations/admin use cases.

It does not implement:

* React Native applications
* backend services
* cloud infrastructure

It may modify only frontend-adjacent repository integration points when required by existing architecture.

Do not redesign backend contracts.

---

# REQUIRED IMPLEMENTATION DELIVERABLES

Implement or update:

## RIDER

* scheduled rides
* promotions
* notifications
* payment history
* receipts
* ratings
* support
* safety
* account privacy
* data export/deletion

## OPERATIONS

* admin shell
* dashboard
* search
* user/driver management
* compliance
* trip investigation
* payment investigation
* payout investigation
* safety
* risk
* support
* promotions
* configuration
* audit
* analytics

## SECURITY

* role-aware routing
* permission-aware actions
* session hardening
* sensitive-data controls
* cache isolation

## QUALITY

* accessibility
* responsive UX
* performance
* E2E
* security tests
* documentation

---

# REQUIRED RUNTIME VALIDATION

Verify:

* rider workflows
* scheduled rides
* promotions
* payments/history
* notifications
* support
* safety
* data export
* deletion
* operations dashboard
* search
* investigation pages
* compliance
* financial investigation
* risk
* configuration
* audit
* analytics

Verify that unauthorized users cannot access privileged pages or actions.

Verify account switching and logout clear privileged state.

---

# COMPLETION REPORT REQUIREMENTS

When implementation is complete, report:

## FILES CREATED

List every new file.

## FILES MODIFIED

List every modified file.

## RIDER FUNCTIONALITY

Report:

* scheduled rides
* promotions
* payments
* receipts
* notifications
* support
* safety
* privacy

## OPERATIONS

Report:

* dashboard
* search
* driver/compliance operations
* trip investigation
* payment investigation
* payout investigation
* support
* safety
* risk
* promotions
* configuration
* audit

## SECURITY

Report:

* route protection
* permissions
* admin session handling
* cache isolation
* sensitive-data handling

## ACCESSIBILITY

Report:

* keyboard support
* screen-reader behavior
* focus management
* tables/forms/charts
* reduced motion

## PERFORMANCE

Report:

* bundle improvements
* query optimization
* dashboard optimization
* map/realtime optimization
* table performance

## TESTS

List tests added or modified and the behaviors they verify.

## VALIDATION

Report:

* formatting
* linting
* type checking
* production build
* unit tests
* integration tests
* E2E tests
* accessibility tests
* performance testing
* security testing

## COMPATIBILITY

Identify:

* backend API compatibility
* WebSocket compatibility
* role/permission compatibility
* route compatibility

## UNRESOLVED ISSUES

List only genuine remaining issues.

Do not claim completion if rider or operational workflows remain disconnected, insecure, inaccessible, or dependent on fake data.

---

# FINAL ENGINEERING PRINCIPLE

The completed web platform must serve two distinct operational audiences without compromising either:

* riders need a clear, trustworthy, resilient transportation experience
* authorized operations personnel need a secure, auditable, information-dense control surface

The rider experience must remain authoritative through backend state.

The operations experience must remain permission-aware and must never become a browser-based database editor.

Search, dashboards, analytics, and realtime views are derived and operational.

Payments, trips, compliance, payouts, safety, and user identity remain backend-authoritative.

Prioritize:

* security
* correctness
* accessibility
* operational clarity
* realtime resilience
* privacy
* performance
* maintainability
* contract compatibility

The repository remains the implementation source of truth.

Every subsequent mobile and infrastructure implementation must integrate with this web platform without introducing competing API contracts, authentication mechanisms, or unauthorized business logic.
