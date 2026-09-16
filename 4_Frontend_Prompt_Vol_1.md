# UBER-STYLE RIDE-HAILING PLATFORM — FRONTEND PROMPT — VOLUME 1

## ROLE

You are the senior frontend engineering organization responsible for implementing the production web platform for a globally scalable ride-hailing and mobility marketplace comparable in product depth and operational sophistication to Uber.

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

You are not creating a tutorial, prototype, visual mockup, static HTML demonstration, or disconnected frontend shell.

Implement complete, connected, production-grade web functionality using the existing backend contracts and repository architecture.

The repository is the source of truth for what currently exists.

Do not assume that another AI prompt or previous conversation is available.

---

# PROJECT

Implement the production web platform for an Uber-style ride-hailing system supporting:

* riders
* authenticated rider accounts
* ride estimates
* ride requests
* dispatch state
* driver assignment
* active-trip tracking
* driver location
* trip lifecycle
* payments
* receipts
* ratings
* ride history
* notifications
* support
* safety
* administrative and operational interfaces where appropriate

The web application must use:

* Next.js 15
* React 19
* TypeScript
* Tailwind CSS
* shadcn/ui
* TanStack Query
* Zustand only where persistent client state is justified
* React Hook Form
* Zod
* date-fns
* Recharts where analytics visualization is required
* Framer Motion only where it materially improves usability

Use the backend APIs and realtime contracts already present in the repository.

Do not invent incompatible APIs.

Do not move authoritative business logic into the frontend.

---

# SOURCE OF TRUTH

Before changing code:

Inspect the repository thoroughly.

Determine:

* Next.js application structure
* routing architecture
* layouts
* existing design system
* shared UI components
* API client
* authentication implementation
* token/session handling
* TanStack Query configuration
* Zustand stores
* forms
* validation
* existing rider experiences
* existing driver/operations experiences if present
* WebSocket/realtime integration
* error handling
* loading-state conventions
* accessibility implementation
* testing framework
* analytics instrumentation
* environment configuration
* backend API contracts
* OpenAPI-generated types or equivalent contracts

Preserve compatible implementation.

Do not create parallel API clients, authentication systems, design systems, or state-management architectures when compatible infrastructure already exists.

Do not regenerate unchanged files.

---

# FRONTEND SCOPE

This volume owns the production foundation and primary rider web experience.

Implement:

* application shell
* routing
* authentication UI
* secure session integration
* rider account
* rider profile
* rider navigation
* location selection
* pickup/destination workflow
* map integration boundary
* ride-product selection
* fare estimation
* ride request creation
* request status
* dispatch status
* driver assignment presentation
* active-trip experience foundation
* realtime connection foundation
* trip state synchronization
* loading/error/empty states
* notifications foundation
* accessibility
* responsive behavior
* frontend error boundaries
* analytics foundation
* frontend security controls
* automated tests

Do not implement the complete operations dashboard or every future administrative surface in this volume.

Do not implement the mobile applications.

---

# APPLICATION ARCHITECTURE

Use a maintainable frontend architecture that separates:

* application shell
* routes/pages
* feature modules
* reusable UI
* API clients
* server state
* local UI state
* authentication
* realtime state
* validation
* analytics
* error handling

Do not place all application state inside a single global Zustand store.

Use TanStack Query for server-owned data.

Use Zustand only for local cross-route UI state that genuinely benefits from centralized client state.

---

# ROUTING

Define production routes for the rider experience.

At minimum provide appropriate routes for:

* landing/home
* authentication
* account/profile
* ride booking
* active ride
* ride history
* trip detail
* payment methods
* notifications
* support
* safety
* ratings where a dedicated surface is justified

Route naming must follow repository conventions.

Protected routes must enforce authentication at the appropriate application layer.

Do not rely solely on hiding navigation links.

---

# APPLICATION SHELL

Implement a consistent responsive application shell.

Support:

* primary navigation
* authenticated user controls
* notification access
* account access
* responsive navigation
* loading boundaries
* error boundaries
* accessible focus management

The shell must work across:

* desktop
* tablet
* mobile web

Do not duplicate shell logic across pages.

---

# DESIGN SYSTEM

Use the repository's existing shadcn/ui/Tailwind architecture where present.

Establish or preserve reusable primitives for:

* buttons
* inputs
* selects
* dialogs
* sheets
* cards
* badges
* alerts
* tabs
* dropdowns
* tooltips
* skeletons
* forms
* pagination
* toasts

Do not create one-off styling for repeated interface patterns.

---

# VISUAL CONSISTENCY

Maintain:

* consistent spacing
* typography hierarchy
* responsive breakpoints
* interaction states
* focus states
* disabled states
* error states
* loading states
* empty states

Do not prioritize animation over clarity.

Use motion sparingly for:

* state transitions
* route transitions
* ride-state changes
* notification arrival

Respect reduced-motion preferences.

---

# ACCESSIBILITY

Implement accessible web interactions.

At minimum consider:

* semantic HTML
* keyboard navigation
* visible focus
* ARIA where appropriate
* form labels
* error associations
* accessible dialogs
* screen-reader announcements
* sufficient touch target size
* reduced-motion support
* accessible map alternatives
* accessible live-trip status

Do not make critical ride actions dependent on visual map interpretation alone.

---

# AUTHENTICATION UI

Implement the rider-facing authentication flows supported by the backend.

Support appropriate:

* registration
* login
* logout
* credential recovery
* session expiration handling
* authentication errors
* account restriction messaging

Do not expose internal authentication errors.

Do not reveal whether an arbitrary account exists when backend behavior intentionally prevents enumeration.

---

# AUTHENTICATION STORAGE

Follow the repository's actual authentication contract.

Do not introduce insecure browser storage for highly sensitive long-lived credentials merely for convenience.

Where access/refresh tokens are used:

* follow backend token lifecycle
* handle expiration
* handle refresh safely
* clear invalid state
* prevent stale authenticated UI

Do not persist secrets into:

* localStorage
* URL parameters
* analytics payloads
* logs

unless the repository's security model explicitly requires and protects such use.

---

# API CLIENT

Create or extend one consistent API client.

It must support:

* base URL configuration
* authentication
* request IDs
* correlation IDs where appropriate
* JSON serialization
* typed responses
* typed errors
* timeouts where appropriate
* retry classification
* cancellation
* normalized error handling

Do not create separate ad hoc `fetch` wrappers for every feature.

---

# API CONTRACTS

Consume the existing backend contracts.

The frontend must not invent request/response fields simply because they are convenient.

Inspect:

* OpenAPI
* backend DTOs
* existing API client types
* generated contract types where present

When backend functionality is missing, implement the UI around the existing contract boundary and clearly identify the missing backend dependency rather than silently inventing an incompatible response.

---

# SERVER STATE

Use TanStack Query for data that originates from the backend.

Manage:

* rider profile
* payment methods
* ride estimates
* ride requests
* trip state
* ride history
* notifications
* support cases
* ratings
* safety records where exposed

Define:

* query keys
* stale times
* refetch behavior
* invalidation
* mutation behavior
* error state

Do not manually synchronize large amounts of server state inside Zustand.

---

# CLIENT STATE

Use Zustand only where a centralized client store materially improves the architecture.

Potential uses:

* active booking UI state
* map interaction state
* selected ride product
* local modal/sheet state
* transient navigation context

Do not duplicate server-authoritative trip/payment states inside long-lived client-only stores.

---

# FORM ARCHITECTURE

Use:

* React Hook Form
* Zod

for complex user input.

Validate:

* pickup
* destination
* ride product
* profile data
* payment-related form metadata where applicable
* support forms
* safety forms

Client validation improves UX but must never replace backend validation.

---

# BOOKING EXPERIENCE

Implement a production rider booking workflow.

The experience must allow:

1. Select pickup.
2. Select destination.
3. Resolve locations.
4. Display applicable ride products.
5. Request fare estimate.
6. Show pricing information.
7. Confirm ride.
8. Submit idempotent ride request.
9. Enter dispatch state.
10. Transition to matched state.
11. Transition to active trip.

The UI must correctly represent each state.

Do not assume that one API request completes the entire ride lifecycle.

---

# LOCATION INPUT

Support:

* address search
* current location where browser permissions allow
* map selection
* pickup adjustment
* destination selection
* location validation errors

External geocoding must use the backend/provider architecture established by the repository where possible.

Do not expose provider API credentials in browser code unless the provider architecture explicitly requires a safe public key.

---

# BROWSER GEOLOCATION

When using browser geolocation:

* request permission intentionally
* explain why location is needed
* handle denied permission
* handle unavailable location
* handle timeout
* avoid continuous high-frequency browser tracking when unnecessary

Never treat browser location as authoritative.

---

# MAP EXPERIENCE

Implement a reusable map abstraction compatible with the project's selected provider.

Support:

* pickup marker
* destination marker
* route visualization where provided
* driver location during active ride
* fit-to-bounds
* loading state
* provider failure state

Do not expose provider secrets.

Do not make the entire booking experience unusable merely because the map visualization failed if equivalent textual/address interaction remains possible.

---

# ACCESSIBLE MAP ALTERNATIVE

Provide non-map information for critical states.

Examples:

* pickup address
* destination address
* driver name
* vehicle
* ETA
* trip status

Users must not need visual map interpretation to understand essential ride status.

---

# RIDE PRODUCT SELECTION

Display available ride products returned by the backend.

For each product show, as provided:

* name
* description
* capacity
* estimated fare
* ETA
* applicable features

Do not calculate authoritative prices independently in the client.

Do not invent ride-product availability.

---

# FARE ESTIMATE

Implement a TanStack Query-driven estimate flow.

Handle:

* loading
* success
* stale quote
* pricing unavailable
* map unavailable
* validation errors
* retryable dependency errors

Display enough context for users to understand the estimate.

Make clear when a value is an estimate rather than a final charge.

Do not silently reuse an expired quote.

---

# QUOTE EXPIRATION

If the backend provides:

* quote ID
* quote version
* expiration timestamp
* pricing version

preserve them through booking.

The client must not modify them.

When a quote expires:

* invalidate it
* request a new estimate when appropriate
* avoid submitting stale pricing assumptions

---

# RIDE REQUEST SUBMISSION

Implement idempotent ride-request creation using the backend's supported contract.

Handle:

* successful request
* duplicate submission
* validation error
* no eligible drivers
* market unavailable
* payment readiness failure
* network timeout
* uncertain request outcome

If the network fails after the backend may have accepted the request, reconcile through authoritative ride retrieval rather than blindly creating another request.

---

# UNCERTAIN MUTATIONS

For critical mutations such as ride creation:

Do not assume:

`network error = server did not process request`

Instead:

1. preserve the client operation identifier where supported
2. inspect/reconcile authoritative server state
3. display the correct current state
4. retry only when safe

This applies to:

* ride requests
* cancellations
* ratings
* support submissions
* payment-related actions

---

# DISPATCH UI

After ride creation, display:

* request submitted
* searching
* matching
* driver assigned
* no-match/retry
* cancellation option where valid

Do not simulate driver matching locally.

The UI must derive actual state from backend responses and realtime events.

---

# DRIVER ASSIGNMENT UI

After assignment, display appropriate:

* driver name
* driver photo if available
* vehicle
* vehicle identifier
* rating
* estimated arrival
* pickup information
* communication/safety controls as supported

Only display information returned by authorized backend APIs.

Do not expose private driver information unnecessarily.

---

# REALTIME FOUNDATION

Implement a production WebSocket client for rider realtime experiences.

Support:

* authenticated connection
* connection state
* subscribe/unsubscribe
* heartbeat where required
* reconnect
* exponential backoff
* duplicate handling
* stale-message handling
* teardown
* cleanup

Do not create a WebSocket connection per component.

Use a centralized lifecycle with well-defined ownership.

---

# REALTIME AUTHENTICATION

Follow the backend's realtime authentication contract.

Never put long-lived secrets directly into arbitrary URL parameters.

Do not allow subscription based solely on a client-supplied trip ID.

The backend remains the authorization authority.

---

# REALTIME STATE

Use realtime events as incremental updates to server state.

When a realtime event is received:

* validate its structure
* determine whether it is current
* update/invalidate TanStack Query state
* ignore duplicates
* recover through API state when necessary

Do not treat a socket event as more authoritative than the backend's current state.

---

# REALTIME RECONNECTION

After reconnecting:

1. re-authenticate if required
2. restore authorized subscriptions
3. fetch authoritative active-ride state
4. reconcile missed events
5. resume live updates

Do not assume the socket connection automatically provides complete history.

---

# LIVE DRIVER LOCATION

During an active eligible ride, show the driver's latest authorized location.

Handle:

* location updates
* stale location
* delayed messages
* reconnect
* missing location
* permission changes
* trip completion

If location becomes stale, communicate uncertainty appropriately rather than displaying an old position as current.

---

# TRIP STATE UI

Build explicit UI states for:

* driver en route
* driver arrived
* trip starting
* trip active
* trip completed
* trip canceled
* payment processing
* completed/receipt available

Do not collapse all active states into one generic "trip in progress" view.

---

# TRIP START

The client must consume the backend's trip-start verification flow where required.

Support the appropriate UX for:

* verification code
* rider confirmation
* driver-arrived confirmation

Do not trust a client-side "started" state as proof.

---

# ACTIVE TRIP

The active-trip experience must show authoritative information such as:

* current state
* driver
* vehicle
* pickup
* destination
* ETA
* route where available
* safety controls
* support access
* trip-sharing access where supported

Keep critical information accessible when map rendering fails.

---

# TRIP COMPLETION

When the backend reports completion:

* stop active-location rendering
* fetch final trip/fare state
* show final receipt state
* provide rating flow
* preserve history

Do not locally infer completion merely because an expected duration has elapsed.

---

# CANCELLATION UI

Implement cancellation flows according to backend eligibility.

Display:

* cancellation action only when appropriate
* reason choices if required
* applicable fee information returned by the backend
* confirmation
* processing
* completed result
* conflict if state changed concurrently

If cancellation loses a race with trip start or another terminal state, reconcile with authoritative backend state.

---

# ERROR HANDLING

Create consistent user-facing error behavior.

Handle:

* validation
* unauthorized
* forbidden
* not found
* conflict
* rate limiting
* dependency unavailable
* timeout
* network failure
* unknown error

Do not expose:

* stack traces
* raw backend errors
* provider internals
* database errors
* sensitive identifiers

---

# RETRY STRATEGY

Retry only operations classified as safely retryable.

Good candidates may include:

* selected reads
* idempotent fetches
* transient provider-independent queries

Do not blindly retry:

* ride creation
* payment mutations
* cancellation
* ratings
* support submissions

unless the backend contract provides idempotency.

---

# LOADING STATES

Every async user workflow must define:

* initial loading
* background refresh
* mutation pending
* optimistic state where safe
* disabled controls
* timeout behavior

Avoid blank screens.

Use skeletons where content shape is known.

---

# EMPTY STATES

Design intentional empty states for:

* ride history
* notifications
* payment methods
* support cases
* ratings awaiting completion
* saved locations if implemented

Empty states should explain what the user can do next when appropriate.

---

# ERROR BOUNDARIES

Implement route/feature error boundaries appropriate to Next.js architecture.

A failure in:

* notification panel
* map visualization
* ride history

must not unnecessarily crash the entire application.

Critical authentication/session failures may require controlled global handling.

---

# SECURITY

The frontend must enforce presentation-level protections but never substitute for backend authorization.

Protect against:

* XSS
* unsafe HTML rendering
* malicious URLs
* token leakage
* sensitive data in analytics
* accidental secret exposure
* insecure client-side persistence

Never use `dangerouslySetInnerHTML` for untrusted content without an explicit, safe sanitization strategy.

---

# XSS

Treat all server-returned text as untrusted.

Use React's escaping behavior.

Sanitize any rich text intentionally rendered as HTML using a vetted strategy already compatible with the repository.

Do not render provider content as raw HTML.

---

# OPEN REDIRECTS

Validate redirect destinations.

Do not blindly navigate to URLs returned from arbitrary server/client inputs.

Authentication redirects must be limited to known application routes.

---

# ENVIRONMENT VARIABLES

Only expose variables intended for browser use through Next.js's public configuration mechanism.

Never expose:

* private API secrets
* provider secret keys
* signing keys
* database credentials
* internal service credentials

in browser bundles.

---

# ANALYTICS

Implement a frontend analytics abstraction.

Track meaningful user interactions such as:

* booking started
* estimate requested
* ride requested
* ride assigned
* trip started
* trip completed
* cancellation
* support opened

Do not send:

* access tokens
* payment credentials
* exact unnecessary location history
* private support content
* security secrets

Respect applicable consent/privacy controls.

---

# PERFORMANCE

Optimize:

* initial application load
* route transitions
* map rendering
* realtime updates
* list rendering
* image loading
* JavaScript bundle size
* server/client boundaries

Avoid:

* unnecessary client components
* repeated API requests
* unbounded realtime state
* re-rendering the entire application on every location update

Use appropriate Next.js server/client separation.

---

# MAP PERFORMANCE

Do not re-render the entire map for every location event.

Update only the relevant entities.

Throttle visual updates where the incoming location frequency is higher than the UI needs.

Preserve latest authoritative state independently from animation frequency.

---

# REALTIME PERFORMANCE

A driver may send frequent location updates.

The web client must:

* avoid excessive React renders
* avoid rebuilding large objects unnecessarily
* clean up subscriptions
* throttle visual state changes where safe
* stop processing location updates after trip completion

---

# RESPONSIVE DESIGN

The rider web application must support:

* desktop
* tablet
* mobile web

Critical booking actions must remain usable at small widths.

Do not rely on hover-only interaction.

---

# MOBILE WEB LOCATION AND PERMISSIONS

Provide clear states for:

* permission not requested
* permission granted
* permission denied
* location unavailable
* location stale

Never repeatedly prompt without user action.

---

# NOTIFICATIONS

Implement the frontend notification foundation.

Support:

* unread state
* notification list
* notification detail where appropriate
* navigation from notification to related resource
* read/unread mutation
* graceful failure

Do not trust a notification as authoritative trip state.

---

# RIDE HISTORY

Implement rider trip history.

Support:

* pagination
* filtering if provided by backend
* loading
* empty
* error
* trip detail
* final fare
* receipt state
* rating status

Do not load the entire historical ride set at once.

---

# TRIP DETAIL

Implement a secure trip-detail view.

Display only fields authorized for the rider.

Potential information:

* date/time
* pickup
* destination
* driver
* vehicle
* fare
* payment state
* rating
* support options
* receipt

Do not expose internal dispatch information.

---

# PAYMENT METHODS UI

Consume the backend payment-method abstraction.

Support:

* list
* default method
* add method through provider-supported flow
* remove method where allowed

Do not handle raw card credentials in custom application state if the payment architecture provides secure provider-hosted/tokenized flows.

---

# RECEIPTS

Display or retrieve receipts through secure backend APIs.

Where receipt artifacts exist:

* verify authorization
* avoid exposing predictable storage paths
* use expiring/signed access where appropriate

Do not expose private object-storage URLs permanently.

---

# RATING UI

Provide rider rating workflow after eligible completed trips.

Support:

* rating selection
* optional review
* submission
* validation
* duplicate prevention
* already-rated state

The backend remains authoritative for eligibility.

---

# SUPPORT UI

Provide rider support entry points for:

* trip issue
* payment issue
* driver issue
* safety issue
* general support

Support forms must use backend case APIs.

Do not embed email-only fallback as the authoritative support system when backend support cases exist.

---

# SAFETY UI

Provide accessible safety controls appropriate to backend capabilities.

Potential functionality:

* report incident
* access trusted contact/share trip
* emergency action
* trip safety information

Safety controls must remain easy to reach during active trips.

---

# PRIVACY

The frontend must minimize exposure of:

* precise driver location
* historical route
* financial metadata
* identity information
* support content
* safety data

Do not cache sensitive information longer than needed.

Clear local sensitive state on logout where appropriate.

---

# QUERY CACHE SECURITY

Do not place highly sensitive information in:

* public URLs
* persistent browser caches
* analytics
* client logs

Configure TanStack Query persistence only where the data class permits it.

Do not persist active-trip private data across accounts without explicit cache isolation.

---

# ACCOUNT SWITCHING

If the product permits account/session switching, ensure:

* query cache isolation
* WebSocket teardown
* local state reset
* notification state reset
* route protection

A previous user's active-trip state must never appear after another user authenticates.

---

# LOGOUT

Logout must:

* clear authenticated client state
* clear sensitive cached data
* disconnect realtime
* cancel relevant requests
* redirect appropriately

Do not leave active-trip data in memory where another user could later observe it.

---

# TESTING REQUIREMENTS

Write comprehensive frontend tests.

## AUTHENTICATION

Test:

* login
* registration
* logout
* session expiration
* refresh behavior
* unauthorized route handling
* account restriction

## BOOKING

Test:

* location selection
* estimate request
* quote expiration
* ride product selection
* ride creation
* duplicate-click behavior
* network uncertainty

## DISPATCH

Test:

* searching
* matched
* offer/assignment presentation
* no-driver state
* stale realtime event handling

## TRIP

Test:

* driver en route
* arrived
* start
* active trip
* location updates
* cancellation
* completion
* receipt
* rating

## REALTIME

Test:

* connect
* authenticate
* subscribe
* event delivery
* duplicate event
* stale event
* disconnect
* reconnect
* state reconciliation

## ACCESS CONTROL

Test:

* protected routes
* user ownership
* expired session
* restricted account
* incorrect resource access

## FORMS

Test:

* validation
* server errors
* loading
* submission
* retry
* accessibility

---

# END-TO-END TESTING

Create E2E coverage for the primary rider journey:

1. authenticate
2. select pickup
3. select destination
4. request estimate
5. select ride
6. create request
7. observe dispatch
8. receive driver assignment
9. observe active trip
10. observe completion
11. view final fare
12. rate driver

Use the actual backend contracts in the repository or a dedicated test environment.

Do not fake the entire backend in the primary E2E journey.

---

# ACCESSIBILITY TESTING

Validate:

* keyboard navigation
* focus management
* dialogs
* forms
* error messages
* live status announcements
* responsive interaction
* reduced motion

Critical booking and active-trip workflows must be accessible.

---

# PERFORMANCE TESTING

Measure:

* initial page load
* route navigation
* booking interaction latency
* map rendering
* realtime rendering
* trip history pagination
* bundle size

Do not optimize based solely on assumptions.

---

# BROWSER ERROR RECOVERY

Handle:

* offline
* temporary network loss
* API timeout
* WebSocket disconnect
* stale query state
* page refresh during active trip

During an active trip, page refresh must recover the current authoritative trip state rather than resetting to a blank booking state.

---

# OFFLINE BEHAVIOR

The web client is not authoritative.

When offline:

* clearly communicate connectivity state
* stop unsafe mutations
* preserve safe local UI state
* reconnect automatically
* reconcile authoritative state

Do not queue arbitrary financial/ride mutations locally unless the backend contract explicitly supports offline idempotency.

---

# DOCUMENTATION

Update frontend documentation for:

* local setup
* environment variables
* API client
* authentication
* route architecture
* state management
* WebSockets
* map provider integration
* analytics
* testing
* accessibility
* security

Documentation must describe actual implementation.

---

# IMPLEMENTATION DISCIPLINE

Before modifying files:

1. Inspect the repository.
2. Identify existing frontend infrastructure.
3. Identify current backend contracts.
4. Preserve compatible components.
5. Establish or extend the application shell.
6. Implement routing.
7. Integrate authentication.
8. Implement API client.
9. Configure TanStack Query.
10. Configure appropriate local state.
11. Implement rider booking.
12. Implement estimate display.
13. Implement ride request.
14. Implement dispatch/match state.
15. Implement realtime.
16. Implement active-trip experience.
17. Implement history and trip detail foundations.
18. Implement payment/notification/support/safety entry points supported by backend contracts.
19. Add accessibility.
20. Add analytics.
21. Add tests.
22. Validate production builds.
23. Review security and privacy.
24. Update documentation.
25. Produce the required completion report.

Do not rewrite unrelated frontend code.

---

# PRODUCTION COMPLETENESS

Never leave:

* static fake trip states
* mocked drivers presented as real users
* hardcoded prices
* fake ETA
* simulated WebSocket events
* fake payment status
* placeholder APIs
* TODO/FIXME implementation gaps
* inaccessible critical controls
* disconnected screens
* hardcoded production credentials

A UI is not complete merely because the screen renders.

Every implemented workflow must connect to the appropriate backend contract.

---

# PROHIBITED PRACTICES

Never:

* calculate authoritative fare solely in the browser
* trust client role data
* expose provider secrets
* store long-lived sensitive credentials insecurely
* trust a WebSocket event as permanent state
* render unauthorized driver/user information
* persist private active-trip state across account boundaries
* send sensitive information to analytics
* silently retry non-idempotent mutations
* create arbitrary backend endpoints from frontend assumptions
* disable accessibility to simplify UI
* build a second API client when a repository client already exists

---

# IMPLEMENTATION BOUNDARIES

This volume establishes the production web foundation and primary rider journey.

Do not implement:

* React Native mobile applications
* complete driver mobile application
* complete operations/admin dashboard
* backend services
* cloud infrastructure

unless minimal integration changes are required within the existing web application.

The web application must consume backend contracts rather than redesigning them.

---

# REQUIRED IMPLEMENTATION DELIVERABLES

Implement or update:

## APPLICATION FOUNDATION

* Next.js structure
* routing
* layouts
* error boundaries
* responsive shell
* design-system integration

## AUTHENTICATION

* registration
* login
* logout
* recovery
* session handling
* protected routes

## DATA LAYER

* API client
* TanStack Query
* validation
* error normalization
* request/correlation metadata

## RIDER EXPERIENCE

* profile
* booking
* location selection
* ride products
* fare estimates
* ride request
* dispatch state
* driver assignment

## REALTIME

* WebSocket client
* authentication
* subscriptions
* reconnect
* reconciliation

## ACTIVE TRIP

* driver tracking
* trip states
* cancellation
* completion
* receipt
* rating

## ACCOUNT

* trip history
* trip detail
* payment methods
* notifications
* support
* safety

## SECURITY

* XSS protection
* route protection
* cache isolation
* secret protection
* privacy controls

## QUALITY

* accessibility
* responsive design
* tests
* performance
* analytics
* documentation

---

# REQUIRED FRONTEND CONTRACTS

Create or preserve typed client contracts for:

* authentication
* rider profile
* ride estimate
* ride creation
* ride state
* driver assignment
* trip state
* driver location
* cancellation
* payment methods
* notifications
* ratings
* support
* safety

Use backend-defined semantics.

Do not define fake response models merely to complete the UI.

---

# RUNTIME VALIDATION

Verify:

* production build
* type checking
* linting
* authentication
* protected routes
* booking
* estimate
* ride creation
* realtime
* active trip
* cancellation
* completion
* history
* payment method flows where supported
* notifications
* support
* safety

Verify page refresh during an active trip correctly reconstructs state.

---

# COMPLETION REPORT REQUIREMENTS

When implementation is complete, report:

## FILES CREATED

List every new file.

## FILES MODIFIED

List every modified file.

## APPLICATION FOUNDATION

Report:

* routing
* layouts
* design system
* error boundaries
* responsive architecture

## AUTHENTICATION

Report:

* login
* registration
* logout
* recovery
* session handling

## RIDER EXPERIENCE

Report:

* booking
* locations
* estimates
* ride request
* dispatch
* driver assignment
* active trip

## REALTIME

Report:

* WebSocket integration
* subscriptions
* reconnect
* recovery
* duplicate handling

## ACCOUNT

Report:

* profile
* history
* trip detail
* payment methods
* notifications
* support
* safety

## SECURITY

Report:

* XSS controls
* auth protection
* cache isolation
* sensitive-data handling
* environment configuration

## ACCESSIBILITY

Report:

* keyboard
* focus
* screen-reader considerations
* live status
* reduced motion

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
* performance validation where performed

## COMPATIBILITY

Identify:

* backend API compatibility
* WebSocket compatibility
* mobile/web implications
* existing route compatibility

## UNRESOLVED ISSUES

List only genuine remaining issues.

Do not claim completion if the primary rider workflows remain disconnected, untested, insecure, or dependent on fake data.

---

# FINAL ENGINEERING PRINCIPLE

The web application must be a real production client of the ride-hailing backend.

The frontend owns presentation, client experience, local interaction state, and server-state orchestration.

The backend remains authoritative for:

* identity
* authorization
* ride state
* dispatch
* trip state
* pricing
* payments
* driver eligibility
* location authorization

Build the rider experience so that it remains coherent through:

* slow networks
* dropped connections
* WebSocket interruptions
* duplicate events
* stale estimates
* concurrent cancellations
* page refresh
* backend failures
* mobile-web viewport constraints

Prioritize:

* correctness
* accessibility
* security
* responsive UX
* realtime recovery
* performance
* maintainability
* contract compatibility

The repository remains the implementation source of truth.

Every subsequent client and infrastructure prompt must be able to integrate with this web application without introducing alternate API contracts, authentication mechanisms, or competing sources of authoritative state.
