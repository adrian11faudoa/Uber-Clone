# Uber-Style Global Ride-Hailing & Mobility Platform — Frontend Prompt — Volume 1

## ROLE

You are the senior frontend engineering organization responsible for implementing the production-grade web application foundation of an original global ride-hailing and mobility platform.

Operate simultaneously as:

* Principal Software Architect
* Staff Frontend Engineer
* Frontend Platform Engineer
* React Architect
* Next.js Engineer
* TypeScript Engineer
* UI/UX Engineer
* Accessibility Engineer
* Performance Engineer
* Security Engineer
* Realtime Systems Engineer
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

The web application must eventually provide production-grade experiences for:

* rider ride requests and active trips
* rider account and financial management
* driver operations
* driver earnings and communication
* operations/support/safety workflows
* fleet and geographic administration

This milestone establishes the shared web platform foundation used by all later frontend volumes.

The platform is architected for targets such as:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* 100,000+ concurrent realtime sessions
* global multi-region operation
* large authenticated user populations
* high availability for critical user workflows

These are architectural targets, not measured frontend capacity claims.

# TECHNOLOGY DIRECTION

Use the locked web stack:

* Next.js
* React
* TypeScript
* Tailwind CSS
* shadcn/ui
* TanStack Query
* React Hook Form
* Zod
* Zustand where justified

Use the backend contracts already implemented by the repository.

Do not introduce a second frontend framework or state-management architecture.

# SOURCE OF TRUTH

The repository is the implementation source of truth.

Inspect the repository before making changes.

The architecture and backend contracts already present in the repository define:

* API behavior
* authentication
* authorization
* pagination
* errors
* idempotency
* concurrency
* realtime
* trip lifecycle
* dispatch
* pricing
* payments
* notifications
* messaging
* safety
* support
* fleet
* scheduled trips
* analytics

Do not depend on the previous AI conversation.

If frontend code already exists:

1. inspect it
2. preserve working behavior
3. extend existing patterns where compatible
4. avoid unnecessary rewrites
5. document material conflicts

The frontend must consume backend contracts rather than recreating backend business logic.

# FRONTEND EXECUTION MODEL

This milestone owns the shared web application platform.

Implement:

* Next.js application structure
* routing architecture
* application shell
* layouts
* design system foundation
* responsive behavior
* accessibility foundation
* theme support
* API client
* authentication/session handling
* authorization-aware routing
* TanStack Query foundation
* client state foundation
* forms and validation foundation
* global error handling
* loading/empty states
* realtime foundation
* offline/connectivity handling
* date/time/currency formatting
* localization foundation
* security protections
* analytics/telemetry hooks
* performance foundations
* map integration boundary
* reusable UI primitives
* frontend testing foundation
* frontend documentation

Do not implement the complete rider, driver, or operations product experiences in this milestone.

# CURRENT IMPLEMENTATION SCOPE

## 1. Repository Inspection

Before changing anything:

* inspect the repository
* identify the existing web application
* inspect package.json
* inspect Next.js configuration
* inspect TypeScript configuration
* inspect Tailwind configuration
* inspect shadcn/ui configuration
* inspect routing structure
* inspect API client code
* inspect authentication code
* inspect existing components
* inspect tests
* inspect environment configuration
* inspect frontend documentation
* inspect backend API contracts
* inspect realtime contracts

Determine which files can be extended and which foundational pieces are missing.

Do not regenerate an existing working application unnecessarily.

## 2. Next.js Application Foundation

Implement or complete the Next.js application architecture.

Establish a clean structure for:

* application routes
* layouts
* shared components
* feature modules
* API/client infrastructure
* state
* hooks
* utilities
* forms
* validation
* realtime
* tests

Use the repository's existing Next.js routing approach where already established.

Do not create an unnecessary second routing system.

## 3. TypeScript Configuration

Ensure strict and maintainable TypeScript configuration.

Use:

* strict type checking
* consistent module resolution
* safe path aliases where justified
* type-safe environment configuration
* predictable build configuration

Do not weaken strictness merely to make existing errors disappear.

## 4. Environment Configuration

Implement typed frontend environment configuration.

Separate:

* public client-safe configuration
* server-only configuration where applicable
* environment identifiers
* API base configuration
* realtime endpoint configuration
* map configuration
* analytics configuration

Never expose secrets through client bundles.

Do not put private backend credentials into `NEXT_PUBLIC_*` values.

## 5. Application Shell

Create the shared application shell used by later experiences.

Support:

* responsive layout
* desktop/mobile browser behavior
* navigation boundaries
* authentication-aware shell
* page content regions
* global notifications/toasts
* loading boundaries
* error boundaries

Do not implement complete domain-specific navigation yet.

## 6. Layout Architecture

Establish reusable layouts for future roles such as:

* public
* authenticated user
* rider
* driver
* operations
* support
* safety
* administrative

Only create structural layout boundaries at this stage.

Do not fill them with complete product workflows.

## 7. Routing Architecture

Implement routing conventions for:

* public routes
* authenticated routes
* role-aware routes
* protected resources
* error/not-found handling

Define route ownership clearly.

Do not rely solely on client-side route hiding for authorization.

The backend remains authoritative for access control.

## 8. Authentication Client

Implement the web authentication/session foundation.

Support the backend contract for:

* sign-in
* registration where applicable
* access-token handling
* refresh
* logout
* session expiration
* session revocation
* authenticated bootstrap

Do not invent authentication APIs.

Consume the implemented backend contract exactly.

## 9. Secure Session Handling

Use the safest repository-compatible browser/session strategy.

Do not place long-lived credentials into insecure storage without an architectural reason.

Protect against:

* token leakage
* accidental logging
* duplicate refresh requests
* refresh races
* stale sessions

Where server-side cookie/session handling is used by the backend architecture, preserve it rather than creating a client-managed token system.

## 10. Authentication Bootstrap

Implement application startup behavior that determines:

* whether the user is authenticated
* current session state
* current principal
* relevant permissions/roles

Avoid flashing protected pages to unauthenticated users unnecessarily.

Do not block the entire application on noncritical requests.

## 11. Token Refresh Coordination

If the API contract requires client-side refresh handling, implement coordinated refresh behavior.

Prevent:

* simultaneous refresh storms
* multiple refresh requests for one expiration event
* stale credential overwrites
* infinite refresh loops

A failed refresh must transition the application into a deterministic signed-out or reauthentication state.

## 12. Authorization Client Foundation

Implement frontend authorization utilities for:

* roles
* permissions
* route access
* feature visibility
* capability checks

These utilities are for user experience and navigation.

They must not be treated as the final security boundary.

Never assume hiding a button is sufficient authorization.

## 13. API Client

Implement one canonical typed API client.

Support:

* base URL
* authentication
* request IDs where appropriate
* correlation IDs
* JSON handling
* request cancellation
* timeout handling where supported
* canonical error parsing
* response typing

Do not allow every feature to create its own HTTP client.

## 14. API Error Handling

Consume the backend canonical error model.

Create typed frontend error representations for:

* authentication failure
* authorization failure
* validation failure
* not found
* conflict
* rate limiting
* transient server failure
* network failure

Do not display raw server stack traces.

Do not silently discard important error context needed for recovery.

## 15. Request Cancellation

Use `AbortController` or the repository's equivalent for cancellable operations.

Important use cases include:

* search
* route/geocoding requests
* queries replaced by newer requests
* page navigation
* component unmount
* map interactions

Prevent obsolete requests from overwriting newer state.

## 16. TanStack Query Foundation

Establish a consistent TanStack Query architecture.

Define:

* QueryClient
* default retry behavior
* stale times
* cache policies
* mutation behavior
* error handling
* query-key conventions
* invalidation conventions

Do not allow arbitrary query-key formats across features.

## 17. Query Key Architecture

Create typed or strongly standardized query keys.

Keys should encode:

* domain
* resource
* scope
* relevant identifiers
* filters

Avoid putting unbounded arbitrary objects into query keys.

Do not create cache collisions between users or roles.

## 18. Mutation and Invalidation Strategy

Establish reusable patterns for:

* mutation submission
* optimistic updates where safe
* invalidation
* refetch
* rollback
* duplicate submission prevention

Do not use optimistic updates for financial or state transitions where incorrect UI state could create misleading behavior unless the contract explicitly supports them.

## 19. Client State Architecture

Use Zustand only for genuine client/application state not better owned by:

* server data
* URL state
* local component state
* form state

Avoid creating a global store for every server response.

Define clear ownership between:

* TanStack Query
* Zustand
* React state
* URL/search parameters
* browser storage

## 20. Form Foundation

Establish React Hook Form + Zod patterns.

Support:

* typed schemas
* client-side validation
* server-error mapping
* field errors
* submission state
* reset behavior
* accessibility
* duplicate-submit protection

Do not duplicate backend business rules blindly.

Client validation improves UX; backend validation remains authoritative.

## 21. Shared UI System

Create or complete the shared design system using:

* Tailwind CSS
* shadcn/ui
* accessible primitives

Provide reusable components for:

* buttons
* inputs
* selects
* dialogs
* dropdowns
* cards
* tables
* badges
* tabs
* alerts
* toasts
* loading states
* empty states
* confirmation flows

Do not build separate visually inconsistent versions of the same component.

## 22. Design Tokens

Establish consistent design tokens for:

* spacing
* typography
* radii
* shadows
* breakpoints
* focus states
* semantic status states

Avoid hard-coding arbitrary visual values throughout feature code.

## 23. Responsive Architecture

Design for:

* desktop
* tablet
* mobile browser

Responsive behavior must be intentional.

Do not simply shrink desktop layouts.

Ensure touch targets and navigation remain usable on smaller screens.

## 24. Accessibility Foundation

Implement accessible defaults for:

* keyboard navigation
* focus management
* semantic HTML
* labels
* descriptions
* error messaging
* dialogs
* menus
* tables
* loading states
* reduced-motion behavior

Use appropriate ARIA only where native semantics are insufficient.

Do not use color alone to communicate state.

## 25. Theme Foundation

Implement theme architecture if required by the product.

Support:

* light/dark mode where established
* system preference where appropriate
* persistence
* hydration-safe behavior
* accessible contrast

Do not create theme logic that causes layout or hydration instability.

## 26. Global Loading and Error Boundaries

Implement consistent loading/error behavior for route and data boundaries.

Support:

* skeletons
* spinners where appropriate
* retry actions
* empty states
* not-found states
* authentication recovery

Avoid displaying infinite loading states when a dependency has actually failed.

## 27. Toast and Notification UI Foundation

Provide a shared mechanism for transient user feedback.

Use it for:

* successful mutations
* recoverable failures
* warnings
* connection state
* background updates where appropriate

Do not use toasts as the only mechanism for critical errors or accessibility-critical information.

## 28. Realtime Client Foundation

Implement the shared WebSocket client layer according to the backend contract.

Support:

* connection
* authentication
* authorization-aware subscriptions
* heartbeat
* reconnect
* exponential/backoff behavior
* connection state
* message parsing
* duplicate handling
* sequence/version handling

Do not let individual screens establish their own unmanaged sockets.

## 29. Realtime State Recovery

The realtime client must support recovery after:

* browser reconnect
* network loss
* server restart
* token refresh
* tab suspension
* temporary gateway failure

Use authoritative API/query state to resynchronize.

Do not assume WebSocket delivery is perfectly reliable.

## 30. Realtime Message Safety

Validate incoming realtime messages.

Reject or safely ignore:

* malformed messages
* unsupported versions
* unauthorized channels
* unknown message types

Do not render arbitrary server-provided HTML.

## 31. Connectivity and Offline Foundation

Implement browser connectivity awareness.

Distinguish:

* browser offline
* API unavailable
* WebSocket disconnected
* server degraded

Do not treat a WebSocket disconnect as proof that the entire API is offline.

Provide appropriate recovery behavior.

## 32. Retry Architecture

Establish retry behavior appropriate to:

* read queries
* mutations
* authentication
* realtime connection
* external map requests

Do not automatically retry non-idempotent mutations without an idempotency contract.

Avoid retry storms.

## 33. Date and Time Utilities

Implement centralized date/time formatting.

Support:

* server UTC timestamps
* user-local display
* explicit timezone where required
* relative time
* scheduled-trip time display

Do not scatter ad hoc date parsing across feature code.

## 34. Currency and Money Display

Implement shared currency formatting.

Support:

* currency code
* locale
* minor-unit-safe display
* consistent rounding presentation

Never use frontend floating-point calculations as the source of financial truth.

The frontend displays backend-authoritative monetary values.

## 35. Localization Foundation

Establish localization architecture for:

* UI strings
* validation messages
* dates
* numbers
* currency
* notifications

Do not hard-code large quantities of user-visible strings directly into components.

Do not allow localization to change business logic semantics.

## 36. Maps Integration Boundary

Create the shared map abstraction used by later ride and operations experiences.

Support an architecture-neutral boundary for:

* map rendering
* markers
* user location
* route visualization
* geocoding/search integration
* map lifecycle

Do not couple the entire frontend directly to one provider.

Do not implement full rider/driver map workflows yet.

## 37. Browser Permissions Foundation

Provide shared handling for browser capabilities needed later, such as:

* geolocation
* notifications

Support:

* permission state
* denied state
* unavailable state
* request flow
* fallback behavior

Do not repeatedly trigger permission prompts.

## 38. Security Foundations

Implement frontend protections for:

* XSS prevention
* safe rendering
* trusted URL handling
* safe external navigation
* secure storage boundaries
* CSRF strategy consistent with the backend
* dependency-safe handling of user-generated content

Never use `dangerouslySetInnerHTML` for untrusted content without an explicit sanitization strategy.

## 39. User-Generated Content Safety

Treat as untrusted:

* message content
* support content
* review text
* external provider text
* uploaded filenames
* search results

Render text safely.

Do not interpolate raw HTML into the DOM.

## 40. Analytics and Telemetry Foundation

Provide a frontend abstraction for product telemetry.

It should support:

* page/view events
* feature events
* error events
* performance events

Events must avoid exposing:

* passwords
* tokens
* payment credentials
* private messages
* precise location unnecessarily
* internal risk information

Do not couple every component directly to a telemetry vendor.

## 41. Frontend Error Reporting

Create an error-reporting boundary for:

* React render errors
* route errors
* API failures
* realtime failures
* unexpected client errors

Use the repository's configured telemetry architecture.

Redact sensitive information before transmission.

## 42. Performance Foundation

Implement shared performance practices for:

* route-level code splitting
* lazy loading
* image optimization
* query caching
* bundle boundaries
* rendering discipline
* map-component isolation

Do not optimize prematurely at the expense of maintainability.

Measure before making aggressive changes.

## 43. Browser Resource Management

Ensure shared resources are cleaned up:

* WebSocket connections
* event listeners
* timers
* geolocation watchers
* map instances
* subscriptions

Prevent memory leaks during route navigation and component remounts.

## 44. Browser Tab and Visibility Handling

Provide shared hooks/utilities for:

* tab visibility
* focus/reconnect
* background browser behavior

Realtime synchronization should recover when a tab becomes active again.

## 45. Access to Backend Capabilities

Create typed client modules organized by domain boundaries, without implementing full domain workflows.

Potential client boundaries include:

* auth
* accounts
* trips
* dispatch
* pricing
* payments
* notifications
* messaging
* support
* safety
* fleet
* scheduled trips
* analytics

Only implement API clients for backend contracts actually needed by this milestone.

Do not create speculative endpoints.

## 46. URL and Search-State Management

Establish patterns for storing shareable UI state in URLs where appropriate.

Examples:

* filters
* pagination
* tabs
* search terms

Do not put sensitive tokens or confidential state in URLs.

## 47. Frontend Authorization UX

Provide reusable behavior for:

* protected routes
* unavailable capabilities
* unauthorized actions
* account restrictions

Do not render privileged controls merely because a user navigated directly to a route.

However, always rely on backend authorization as the final security boundary.

## 48. Testing Foundation

Create frontend testing infrastructure covering:

* component tests
* hook tests
* utility tests
* API client tests
* authentication tests
* authorization tests
* query behavior
* realtime behavior
* forms
* accessibility checks

Use the repository's established testing framework if one already exists.

## 49. Accessibility Testing

Automate accessibility checks where tooling supports it.

Test:

* keyboard navigation
* labels
* focus behavior
* dialog behavior
* form errors
* color-independent status
* responsive interaction

## 50. API Mocking and Local Development

Provide deterministic frontend test/local-development mechanisms for backend-dependent flows.

Where supported, create typed mocks or test handlers without replacing production API contracts.

Do not create a permanently separate fake API architecture.

## 51. Build and Quality Tooling

Ensure the frontend has consistent commands for:

* development
* build
* lint
* typecheck
* test
* formatting
* accessibility validation where configured

Do not hide build warnings or type failures.

## 52. Documentation

Create or update frontend documentation covering:

* application structure
* routing
* layouts
* design system
* API client
* authentication
* authorization
* TanStack Query
* Zustand boundaries
* forms
* realtime
* connectivity
* maps
* localization
* accessibility
* security
* telemetry
* performance
* testing
* local development

Documentation must describe actual implementation behavior.

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement the complete rider experience.

Do not implement:

* ride request screens
* active trip screens
* full trip history
* complete payment management
* driver dispatch interface
* driver earnings interface
* operations dashboard
* safety management UI
* support workflow UI
* fleet UI
* scheduled-trip UI
* analytics dashboard UI

Those belong to later frontend volumes.

Do not implement mobile applications.

Do not implement backend changes merely to accommodate frontend convenience.

Do not create a second API client architecture.

Do not create a second realtime connection manager.

Do not create a second state-management system.

Do not add a second design system.

Do not create another frontend foundation volume.

Do not create a surprise integration phase.

# REPOSITORY INSPECTION REQUIREMENTS

Before implementation:

1. Inspect the web application.
2. Inspect package.json.
3. Inspect Next.js configuration.
4. Inspect TypeScript configuration.
5. Inspect Tailwind/shadcn configuration.
6. Inspect routing/layouts.
7. Inspect existing API clients.
8. Inspect authentication/session code.
9. Inspect state/query code.
10. Inspect WebSocket/realtime code.
11. Inspect existing forms and validation.
12. Inspect testing configuration.
13. Inspect accessibility tooling.
14. Inspect backend API/error contracts.
15. Inspect architecture artifacts.
16. Determine exactly which files require creation or modification.

Do not overwrite working frontend infrastructure unnecessarily.

# IMPLEMENTATION RULES

## Preserve Existing Foundations

Reuse existing:

* routing
* components
* styles
* API utilities
* authentication
* state management
* tests
* telemetry

when compatible.

## Server State vs Client State

Use TanStack Query for server state.

Use Zustand only where persistent client/application state is genuinely required.

Use local React state for local ephemeral state.

Do not duplicate one piece of state across all three without a clear reason.

## Type Safety

Avoid `any`.

Use generated or manually maintained API types consistently.

Do not duplicate incompatible models across features.

## Security

Never expose:

* secrets
* backend credentials
* private tokens
* payment credentials

in browser code.

## Accessibility

Every shared component must provide usable keyboard and screen-reader behavior.

## Responsive Behavior

All shared layouts and components must work across supported viewport ranges.

## Realtime

Use one managed connection architecture.

Do not open per-component sockets.

## Error Handling

Errors must be recoverable where possible and clearly presented.

Do not swallow errors.

## Performance

Avoid:

* unnecessary rerenders
* unbounded query caches
* duplicated API calls
* memory leaks
* oversized bundles

## No Placeholder Work

Every required foundation capability must be fully implemented.

# VALIDATION REQUIREMENTS

Execute all supported validation.

At minimum:

* dependency verification
* TypeScript typecheck
* ESLint/lint
* formatting checks
* production build
* unit/component tests
* API client tests
* authentication/session tests
* authorization tests
* realtime tests
* form-validation tests
* accessibility tests where configured
* security/static-analysis checks where configured

Test:

* unauthenticated navigation
* authenticated bootstrap
* session expiration
* refresh race
* logout
* authorization failures
* API validation errors
* network failure
* retry behavior
* WebSocket disconnect/reconnect
* duplicate realtime messages
* stale realtime messages
* browser offline behavior
* form submission duplication
* responsive layouts
* keyboard accessibility
* theme hydration
* safe rendering of user-generated content

Do not claim a production build passed unless it actually executed successfully.

# FINAL INTEGRATION CHECK

Before declaring this milestone complete:

1. Verify the Next.js application structure is coherent.
2. Verify routing and layout boundaries are established.
3. Verify environment configuration does not expose secrets.
4. Verify authentication bootstrap is reliable.
5. Verify session refresh cannot create refresh storms.
6. Verify logout/revocation behavior is handled.
7. Verify authorization utilities are reusable.
8. Verify one canonical typed API client exists.
9. Verify API errors map consistently.
10. Verify TanStack Query conventions are consistent.
11. Verify query-key conventions avoid collisions.
12. Verify Zustand is limited to appropriate client state.
13. Verify forms use shared validation conventions.
14. Verify the design system is reusable and accessible.
15. Verify responsive behavior works across supported sizes.
16. Verify realtime uses one shared connection architecture.
17. Verify realtime reconnect/resynchronization exists.
18. Verify browser connectivity states are differentiated correctly.
19. Verify date/time/currency/localization utilities are centralized.
20. Verify maps have a provider-neutral frontend boundary.
21. Verify user-generated content is rendered safely.
22. Verify telemetry redacts sensitive information.
23. Verify frontend error reporting is safe.
24. Verify performance foundations avoid unnecessary resource usage.
25. Verify event listeners/timers/sockets are cleaned up.
26. Verify tests cover authentication, errors, realtime, accessibility, and responsive behavior.
27. Verify no complete product domain was prematurely implemented.
28. Verify compatibility with all completed backend contracts.
29. Verify the repository is ready for Frontend Volume 2.
30. Verify no placeholder or duplicate frontend foundation remains.

# DEFINITION OF DONE

This milestone is complete only when:

* Next.js foundation exists
* routing architecture exists
* shared layouts exist
* environment configuration exists
* application shell exists
* authentication client exists
* secure session handling exists
* token refresh coordination exists where required
* authorization utilities exist
* canonical API client exists
* canonical error handling exists
* TanStack Query foundation exists
* query-key conventions exist
* mutation/invalidation patterns exist
* client-state boundaries exist
* form/validation foundation exists
* shared UI/design-system foundation exists
* responsive architecture exists
* accessibility foundation exists
* theme foundation exists
* loading/error boundaries exist
* toast/feedback system exists
* realtime client exists
* realtime recovery exists
* connectivity handling exists
* retry behavior exists
* date/time formatting exists
* currency formatting exists
* localization foundation exists
* maps abstraction exists
* browser-permission utilities exist
* frontend security protections exist
* safe user-generated-content rendering exists
* telemetry abstraction exists
* error reporting exists
* performance foundations exist
* resource cleanup is implemented
* browser visibility/focus behavior is handled
* typed domain API boundaries exist where required
* URL state conventions exist
* authorization-aware UX exists
* testing infrastructure exists
* accessibility testing exists where configured
* local development/mocking support exists
* build/quality tooling works
* documentation is updated
* no full rider/driver/operations product has been prematurely implemented
* no duplicate API/realtime/state/design foundation exists
* no placeholder implementation remains
* validation results are truthful
* the frontend is ready for Frontend Volume 2

# IMPLEMENTATION REPORT

At completion, provide:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Application Architecture

Summarize:

* Next.js structure
* routing
* layouts
* application shell
* environment configuration

## Authentication and Authorization

Summarize:

* session handling
* refresh
* logout
* authorization utilities
* protected routes

## Data and API

Summarize:

* API client
* errors
* TanStack Query
* caching
* mutations
* client-state boundaries

## UI System

Summarize:

* design system
* components
* responsive behavior
* accessibility
* theme

## Realtime and Connectivity

Summarize:

* WebSocket client
* reconnect
* synchronization
* offline/connectivity handling

## Maps and Localization

Summarize:

* map abstraction
* permissions
* date/time
* currency
* localization

## Security and Telemetry

Summarize:

* safe rendering
* storage boundaries
* telemetry
* error reporting

## Testing and Quality

Summarize:

* unit/component tests
* API tests
* realtime tests
* accessibility checks
* typecheck/lint/build

## Validation Executed

List actual commands and outcomes.

## External Environment Limitations

State any backend, map provider, or external service that could not be exercised.

Do not fabricate external-service execution.

## Architectural Decisions

Record meaningful frontend implementation decisions.

## Known Limitations

List genuine remaining limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement Frontend Volume 1 completely.

Build the shared web application foundation that every later web experience will use.

Implement the Next.js structure, routing, layouts, design system, responsive/accessibility foundation, API client, authentication/session handling, authorization-aware navigation, TanStack Query, client-state boundaries, forms, error/loading behavior, realtime client, connectivity handling, maps boundary, localization, security, telemetry, performance foundations, and testing.

Do not implement full rider, driver, support, safety, fleet, scheduled-trip, or analytics product experiences yet.

Do not duplicate backend business logic.

Do not create a second API client, realtime manager, state system, or design system.

Do not leave placeholders.

Run every validation command supported by the environment.

Verify authentication, authorization, API error handling, realtime recovery, accessibility, responsive behavior, security, performance foundations, and resource cleanup.

Finish with the required implementation report and leave the repository in a coherent production-grade state ready for Frontend Volume 2.
