# Uber-Style Global Ride-Hailing & Mobility Platform — Mobile Prompt — Volume 1

## ROLE

You are acting as the complete senior mobile engineering organization responsible for implementing the foundation of this project's mobile applications to production-grade standards.

Operate as a coordinated:

* Principal Software Architect
* Staff Mobile Engineer
* Staff React Native Engineer
* Staff TypeScript Engineer
* Mobile Security Engineer
* Mobile Performance Engineer
* Reliability Engineer
* QA Engineer
* Accessibility Engineer
* UX Engineer
* Technical Writer

You are an implementation agent, not a teacher.

Your responsibility is to inspect the repository and implement the complete mobile foundation covered by this prompt without breaking existing functionality.

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
2. Identify the mobile application(s), package configuration, workspace/monorepo structure, Expo configuration, native configuration, build configuration, scripts, and existing mobile code.
3. Inspect existing React Native components, navigation, authentication/session handling, API clients, query/state infrastructure, realtime code, maps, notifications, deep links, permissions, storage, analytics, crash/error handling, tests, and documentation.
4. Inspect the backend and architecture contracts available in the repository.
5. Determine the actual mobile-facing authentication, API, realtime, notification, location, maps, trip, dispatch, account, payment, support, and safety contracts.
6. Determine which mobile functionality already exists.
7. Preserve compatible working behavior.
8. Reuse existing shared frontend/mobile packages and abstractions where appropriate.
9. Do not invent backend endpoints, event names, DTOs, authorization semantics, or state transitions where repository contracts already define them.
10. Where a capability depends on a contract genuinely absent from the repository, establish the correct typed integration boundary and document the dependency rather than fabricating backend behavior.

This prompt is independently executable.

Do not depend on another AI conversation or on another prompt being pasted into the repository.

---

# TECHNOLOGY BASELINE

Use the repository's established implementation where it is already present and compatible.

The intended mobile stack is:

* React Native
* Expo
* TypeScript

Use the project's established Expo-compatible libraries and native modules where appropriate.

The mobile applications integrate with the platform backend based on:

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

Implement the complete **shared mobile foundation** required by the rider and driver applications.

This volume establishes the mobile platform upon which the rider and driver product experiences will be built.

Implement the core foundation for:

* Expo application structure
* shared mobile architecture
* environment/configuration
* navigation
* authentication/session management
* secure storage
* API client
* server-state management
* local UI state boundaries
* authenticated realtime connectivity
* push notifications
* deep links
* permissions
* device/app lifecycle
* connectivity/offline handling
* maps/location foundations
* analytics/telemetry
* error/crash handling
* accessibility foundations
* localization/time/currency
* performance
* testing
* build-quality controls
* documentation

This volume must create a stable mobile platform that later rider and driver volumes can extend without creating parallel infrastructure.

Do not implement the full rider or driver product journeys here.

---

# PRIMARY SCOPE

## 1. Mobile Application Architecture

Establish or complete a maintainable React Native + Expo architecture.

Where the repository contains separate rider and driver applications, establish appropriate shared foundations without forcing unrelated product logic into one application.

Where a single application supports both roles, establish clean role-aware boundaries.

Create clear boundaries for:

* app shell
* navigation
* authentication
* API/data layer
* realtime
* storage
* notifications
* device capabilities
* maps/location
* telemetry
* UI primitives
* feature modules
* testing

Avoid circular dependencies.

Do not create a giant global module containing all mobile behavior.

---

# 2. Expo and Runtime Configuration

Implement the mobile runtime configuration system.

Support appropriate configuration for:

* development
* test
* staging
* production

Configuration may include:

* API base URL
* realtime endpoint
* environment name
* maps configuration
* notification configuration
* analytics configuration
* feature configuration references
* app metadata
* platform-specific configuration

Requirements:

* typed configuration
* environment validation
* safe defaults only where appropriate
* fail-fast behavior for missing required configuration
* no secrets embedded unnecessarily in client bundles
* no production configuration committed as sensitive plaintext

Distinguish public mobile configuration from true secrets.

A mobile application cannot reliably keep client-shipped values secret.

---

# 3. Application Bootstrap

Implement a deterministic application bootstrap sequence.

The app should initialize, in the correct dependency order:

* runtime configuration
* error/crash handling
* telemetry where appropriate
* persisted session state
* secure storage
* query client
* local state
* authentication
* navigation
* notification/deep-link handling
* realtime initialization when authenticated
* other required platform services

Avoid race conditions where screens render before required authentication/configuration state is known.

Handle startup failure gracefully.

Do not block the entire app unnecessarily on non-critical services.

---

# 4. Navigation Architecture

Implement the mobile navigation foundation.

Support clear boundaries for:

* authenticated area
* unauthenticated area
* role-specific area
* modal/presentational flows
* deep-linked destinations
* protected screens
* fallback/not-found states where applicable

Use the repository's established React Navigation/Expo Router architecture when already present.

Navigation must react correctly to:

* authenticated state
* logout
* session expiration
* role changes
* account restrictions
* deep links
* app cold start
* app resume

Do not rely solely on client-side navigation guards for authorization.

---

# 5. Authentication

Implement the shared mobile authentication foundation according to backend contracts.

Support, where established:

* sign-in
* sign-out
* authenticated session restoration
* access-token use
* refresh-token/session refresh
* session expiration
* unauthorized response handling
* reauthentication
* account-state handling
* secure logout

Authentication state must be centralized enough to avoid multiple competing session implementations.

Do not duplicate authentication logic across feature modules.

---

# 6. Secure Token and Credential Storage

Use platform-appropriate secure storage for sensitive session material.

Where the authentication architecture requires:

* access-token persistence
* refresh-token persistence
* session credentials
* secure device state

use an appropriate Expo/native secure-storage mechanism.

Do not store sensitive credentials in:

* AsyncStorage
* ordinary Redux/Zustand persistence
* plain files
* URL parameters
* analytics payloads
* general-purpose logs

Except for values explicitly classified as non-sensitive by the architecture.

Handle:

* secure-storage read failure
* secure-storage write failure
* invalid credential state
* logout cleanup

---

# 7. API Client

Implement the shared mobile API client.

Requirements:

* typed requests/responses
* base URL configuration
* authentication injection
* request cancellation where appropriate
* normalized errors
* timeout behavior
* retry behavior
* refresh-token/session-refresh coordination
* unauthorized handling
* request correlation/trace metadata where appropriate
* safe logging

The client must prevent multiple concurrent requests from independently attempting the same token/session refresh.

Do not retry non-idempotent mutations blindly.

Honor backend idempotency contracts.

---

# 8. Query and Server-State Management

Establish the shared server-state layer using TanStack Query where appropriate.

Support:

* typed query keys
* authenticated query scoping
* stale-time configuration
* retry configuration
* mutation handling
* invalidation
* optimistic updates only where safe
* offline-aware behavior
* cache persistence only where appropriate
* cache cleanup on logout/account change

Do not duplicate server state in global local stores without a clear reason.

User/account boundaries must be explicit in cache design.

---

# 9. Local State Architecture

Establish rules for mobile local/client state.

Use Zustand or another already-established repository solution only where justified.

Appropriate examples:

* transient UI state
* modal state
* navigation/UI preferences
* ephemeral interaction state
* device capability state

Do not move authoritative backend entities into global client state merely for convenience.

Define clear ownership of:

* server state
* local UI state
* persisted preferences
* secure credentials

---

# 10. Realtime Foundation

Implement the authenticated WebSocket foundation used by mobile features.

Support:

* authentication
* connection initialization
* connection states
* reconnect
* backoff
* resubscription
* heartbeat/liveness where defined
* disconnect on logout
* app foreground/background transitions
* duplicate-event handling
* stale connection detection
* missed-event recovery
* event routing to feature-level handlers

Do not create separate rider and driver websocket infrastructure.

Provide a shared foundation that later feature modules can consume.

---

# 11. Realtime and Query Reconciliation

Establish reusable patterns for integrating realtime events with TanStack Query.

Support:

* event normalization
* entity identification
* version/sequence/timestamp semantics where provided
* safe cache updates
* invalidation where direct updates are unsafe
* duplicate-event protection
* reconnect reconciliation
* stale-state recovery

The mobile application must recover correctly after missed websocket events.

Do not treat an event as authoritative beyond the semantics defined by backend contracts.

---

# 12. Connectivity and Offline Foundation

Implement mobile connectivity awareness.

Support:

* online
* offline
* reconnecting
* degraded network
* request failure due to connectivity
* app resume after network loss
* retry affordances

Provide shared utilities/hooks for feature modules.

Distinguish:

* offline
* backend unavailable
* websocket disconnected
* authentication expired

Do not represent all failures as "offline."

---

# 13. Offline Data Policy

Establish safe persistence rules.

Determine which data may be:

* persisted
* cached
* memory-only
* secure-storage-only
* discarded on logout
* expired after a defined time

Do not persist highly sensitive data merely to improve convenience.

Financial, security, safety, and private communication data must follow the project's privacy requirements.

Do not promise full offline functionality unless the backend and product contracts explicitly support it.

---

# 14. Push Notifications

Implement the shared push-notification foundation.

Support appropriate Expo/native notification capabilities for:

* permission state
* token registration
* token refresh
* notification handling
* foreground notifications
* background/open behavior where supported
* notification navigation/deep links
* logout cleanup/unregistration where contractually required

The mobile client must distinguish:

* notification received
* notification displayed
* notification tapped
* destination resolved

Do not duplicate notification delivery infrastructure.

Do not expose notification-provider credentials in the app.

---

# 15. Deep Links

Implement a centralized deep-linking system.

Support routing from:

* push notifications
* universal/app links where configured
* internal links
* authentication callbacks where applicable

Deep links must:

* validate destination
* respect authentication
* respect role
* handle expired resources
* handle unauthorized access
* work from cold start
* work when the app is already running
* queue navigation until required bootstrap state is ready

Do not allow arbitrary URLs to bypass navigation or authorization boundaries.

---

# 16. App Lifecycle

Handle key lifecycle states:

* cold start
* foreground
* background
* inactive
* resumed
* terminated

Ensure appropriate behavior for:

* websocket connection
* query refetch
* notification handling
* location sessions
* authentication
* timers
* resource cleanup

Do not assume a backgrounded mobile application has unlimited execution time.

Respect platform lifecycle constraints.

---

# 17. Device and Permission Foundation

Implement reusable permission handling.

Support appropriate capabilities such as:

* location
* notifications
* camera
* photo library
* microphone where messaging requires it
* other permissions explicitly required by implemented features

Provide a common permission abstraction that can represent:

* unknown/not requested
* granted
* denied
* blocked/restricted
* unavailable

Include appropriate UX for:

* first request
* denial
* "don't ask again"/blocked state
* opening system settings where supported
* feature degradation when permission is unavailable

Never assume that a permission request succeeded merely because it was initiated.

---

# 18. Location Foundation

Implement the shared mobile location abstraction needed by later rider and driver features.

Support:

* permission state
* current position
* accuracy
* timestamp
* acquisition errors
* stale position
* foreground location
* background location capability where the native application and product requirements support it
* subscription lifecycle
* cleanup

Use platform-appropriate Expo/native APIs.

Do not prematurely implement the complete driver location-ingestion product in this volume.

The goal is a reliable reusable location layer.

---

# 19. Maps Foundation

Implement the shared map abstraction.

Support:

* map initialization
* map configuration
* provider configuration
* markers
* user-location display
* camera state
* interaction callbacks
* route/polyline primitives
* loading/error states
* cleanup

Keep provider-specific implementation behind a stable application-facing abstraction where practical.

Do not duplicate routing/geocoding business logic.

Do not hard-code one provider throughout unrelated feature modules when the architecture defines a provider boundary.

---

# 20. Time, Date, Currency, and Localization

Establish shared mobile formatting behavior.

Support:

* timezone-aware dates
* locale-aware dates
* relative timestamps where appropriate
* currency formatting
* decimal precision
* pluralization
* language selection where supported

Never treat device timezone as necessarily equal to trip/service-region timezone.

Financial presentation must use authoritative currency data.

Do not perform authoritative financial calculations in the mobile client.

---

# 21. Mobile Design System Foundation

Establish or extend a consistent mobile UI foundation.

Provide reusable primitives for:

* typography
* spacing
* buttons
* inputs
* cards
* lists
* sheets
* dialogs
* alerts
* toasts
* banners
* loading indicators
* empty states
* error states
* status indicators

Use the repository's existing design language where available.

Do not create an unrelated visual system.

---

# 22. Accessibility Foundation

Establish mobile accessibility standards.

Support:

* screen-reader semantics
* accessibility labels
* roles
* state announcements
* dynamic text sizing
* keyboard/focus behavior where relevant
* accessible touch targets
* color-independent state communication
* reduced-motion considerations
* accessible forms
* accessible dialogs

Do not merely label every control generically.

Accessibility labels must describe the actual action or content.

Important trip/notification/status changes should have an appropriate accessible announcement strategy in later feature modules.

---

# 23. Mobile Security Foundation

Implement mobile security protections appropriate to the platform.

Cover:

* secure credential storage
* secure logout
* authentication boundaries
* certificate/network configuration according to project requirements
* safe URL/deep-link handling
* sensitive-data minimization
* secure clipboard behavior where relevant
* safe screenshot behavior only where product/security requirements justify it
* log filtering
* analytics filtering
* environment separation
* no client-embedded backend secrets

Do not add security mechanisms that contradict platform capabilities without documenting the tradeoff.

---

# 24. Analytics, Telemetry, and Crash Handling

Establish shared application telemetry.

Support:

* structured application events
* error reporting
* crash reporting integration boundary
* correlation identifiers where supported
* performance measurements
* screen/navigation telemetry where appropriate

Privacy requirements:

* do not log raw payment credentials
* do not log access/refresh tokens
* do not log sensitive safety evidence
* do not log unnecessary precise location
* do not send message contents unless explicitly authorized by product requirements
* minimize personally identifiable data

Telemetry must not become a shadow data store.

Where third-party providers are not available locally, implement and validate the repository-side abstraction honestly.

---

# 25. Performance Foundation

Establish mobile performance practices.

Address:

* startup time
* navigation performance
* unnecessary rerenders
* list rendering
* memory usage
* image loading
* map lifecycle
* websocket message handling
* query cache size
* background work
* event listeners
* timers
* resource cleanup

Use appropriate list virtualization.

Avoid rendering large server datasets directly.

Do not optimize prematurely at the expense of maintainability, but do address obvious hot paths.

---

# 26. Resource and Subscription Lifecycle

Every shared mobile service must clean up correctly.

Verify lifecycle handling for:

* event listeners
* websocket subscriptions
* location watchers
* notification listeners
* timers
* AppState listeners
* network listeners
* navigation listeners
* map resources

No screen should leave persistent listeners behind after unmount unless the listener intentionally belongs to a longer-lived application service.

---

# 27. Error Model

Establish a consistent mobile error model.

Distinguish:

* validation errors
* authentication errors
* authorization errors
* network errors
* timeout errors
* backend errors
* rate limiting
* stale-state/concurrency errors
* provider errors
* unexpected client errors

Provide shared translation utilities for user-facing messages.

Do not leak raw backend stack traces or internal implementation details to users.

Preserve diagnostic metadata for logs/telemetry where safe.

---

# 28. Loading and Empty-State Foundation

Provide reusable patterns for:

* initial loading
* refreshing
* paginated loading
* skeletons
* empty state
* no results
* retry
* offline
* degraded backend
* unauthorized state

Later rider/driver features must be able to use these patterns consistently.

---

# 29. Testing Foundation

Establish or complete mobile test infrastructure.

Use the repository's existing test stack when available.

Cover foundation behavior including:

### Unit tests

* configuration validation
* authentication state
* token/session handling
* API error normalization
* query-key construction
* permission state mapping
* connectivity state mapping
* date/currency/localization utilities
* deep-link parsing
* realtime event routing
* lifecycle state handling

### Component tests

Cover:

* navigation guards
* auth loading states
* error states
* permission prompts
* offline indicators
* reusable UI primitives
* notification/deep-link handling

### Integration tests

Cover important foundation flows:

* app bootstrap
* session restoration
* logout
* expired-session handling
* token refresh coordination
* realtime connect/reconnect
* push notification routing
* deep link from cold start
* connectivity recovery
* permission-denied flows

Use mocks/test doubles when device or external services are unavailable.

Do not claim real device/provider validation when it was not performed.

---

# 30. Build and Development Quality

Verify the mobile project can be developed and built through repository-supported tooling.

Check:

* TypeScript
* lint
* formatting
* tests
* Expo configuration
* dependency consistency
* environment validation
* development startup
* production build configuration where available

Do not perform cloud or app-store deployment unless the environment explicitly supports it.

Repository-side build configuration must still be correct and production-oriented.

---

# 31. Documentation

Update mobile documentation to describe the actual foundation.

Document:

* application structure
* navigation architecture
* authentication/session lifecycle
* secure storage
* API client
* query/state boundaries
* realtime architecture
* notification system
* deep links
* permissions
* location/maps
* lifecycle behavior
* localization/time/currency
* telemetry
* testing
* environment configuration
* local development
* build requirements
* known platform limitations

Documentation must describe real implementation.

Do not create speculative instructions for unavailable infrastructure.

---

# OUT OF SCOPE

Do not implement the complete user-facing rider or driver journeys in this volume.

Explicitly out of scope:

* rider ride-request journey
* rider trip-history/account/payment feature screens
* rider scheduled-trip feature screens
* driver availability/work-session product screens
* driver dispatch-offer screens
* driver active-trip screens
* driver earnings/payout product screens
* operations/admin mobile application
* backend implementation
* database schema redesign
* dispatch-engine implementation
* payment-provider backend implementation
* infrastructure/Terraform
* Kubernetes/EKS
* CI/CD redesign
* cloud provisioning
* full native-background business workflows beyond the reusable location/lifecycle foundation
* separate QA phase
* separate final-integration phase

Do not create another mobile foundation volume to replace work that belongs here.

---

# IMPLEMENTATION RULES

## Repository First

Inspect the repository before modifying it.

Determine:

* actual mobile architecture
* Expo setup
* navigation solution
* shared packages
* API client
* authentication
* storage
* query architecture
* state-management conventions
* realtime
* notifications
* maps/location
* testing
* build tooling

Reuse existing infrastructure where appropriate.

## No Parallel Foundations

Do not create multiple:

* API clients
* authentication managers
* websocket clients
* notification managers
* permission managers
* location managers
* configuration systems
* design systems

unless the application architecture genuinely requires distinct implementations.

## No Pseudo-Code

Implement real production code.

Do not use:

* TODO-only implementations
* placeholders
* fake API endpoints
* fake authentication
* fabricated notification delivery
* fabricated device capabilities
* simulated provider success presented as real integration
* omitted implementations
* "implement similarly"

## Platform Reality

Respect actual iOS, Android, and Expo lifecycle/permission behavior.

Do not promise background execution guarantees that the selected platform APIs cannot provide.

## Security

Never place secrets in client code or ordinary storage.

Never log sensitive credentials.

Never weaken authentication to simplify development.

## Contract Discipline

Use established API and realtime contracts.

Do not invent endpoint paths, payloads, events, or state transitions when they already exist.

## Compatibility

Preserve compatibility with:

* backend contracts
* web architecture where shared packages exist
* mobile role separation
* later rider implementation
* later driver implementation
* infrastructure/environment conventions

Every independently executable milestone must still combine into one coherent final project.

---

# VALIDATION REQUIREMENTS

Before considering this volume complete:

1. Run formatting checks.
2. Run linting.
3. Run TypeScript/type checks.
4. Run unit tests.
5. Run component tests.
6. Run integration tests available for the mobile project.
7. Validate Expo configuration.
8. Validate environment/configuration handling.
9. Validate app bootstrap.
10. Validate authentication/session restoration.
11. Validate secure credential storage.
12. Validate token/session refresh coordination.
13. Validate logout cleanup.
14. Validate API error normalization.
15. Validate TanStack Query cache boundaries.
16. Validate websocket reconnect/reconciliation foundation.
17. Validate push-notification handling.
18. Validate deep linking.
19. Validate connectivity handling.
20. Validate permission state handling.
21. Validate location lifecycle.
22. Validate map initialization/cleanup where testable.
23. Validate accessibility foundations.
24. Validate telemetry does not contain sensitive data.
25. Validate no secrets are committed or bundled unnecessarily.
26. Validate production build configuration or strongest available equivalent.
27. Verify no broken imports or duplicate infrastructure were introduced.
28. Verify no TODO/placeholder production implementations remain.
29. Verify documentation matches actual implementation.

Where a device, simulator, external provider, cloud service, or other environment dependency prevents validation, run all possible repository-side validation and explicitly report the unavailable validation.

Never claim a real iOS/Android/device/provider test that was not performed.

---

# INTEGRATION CHECK

Before finalizing, verify that the mobile foundation integrates cleanly with the project's existing architecture.

Confirm that:

* rider and driver feature modules can consume the shared API client
* rider and driver feature modules can consume shared authentication
* role-aware navigation can be extended without rewrites
* realtime event handling can support both rider and driver domains
* location services can support rider and driver workflows
* maps can support trip and dispatch features
* notifications can route to rider/driver screens
* deep links respect role and authorization
* account logout clears appropriate cached/sensitive state
* query state cannot leak between users or roles
* lifecycle handling does not leave stale subscriptions
* shared UI primitives remain reusable
* telemetry boundaries are compatible with privacy requirements
* the foundation does not require a second parallel infrastructure in later mobile volumes

The resulting mobile foundation must support the remaining mobile implementation volumes as one coherent application architecture.

Do not introduce temporary architecture that will require a rewrite later.

---

# DEFINITION OF DONE

This volume is complete only when:

* mobile application architecture is established
* Expo/runtime configuration is implemented
* application bootstrap is implemented
* navigation foundation is implemented
* authentication/session handling is implemented
* secure credential storage is implemented
* API client is implemented
* TanStack Query/server-state foundation is implemented
* local-state boundaries are established
* realtime foundation is implemented
* realtime/query reconciliation foundation is implemented
* connectivity/offline foundation is implemented
* push notifications are implemented
* deep links are implemented
* app lifecycle handling is implemented
* permissions foundation is implemented
* location foundation is implemented
* maps foundation is implemented
* time/date/currency/localization utilities are implemented
* mobile design-system foundation is implemented
* accessibility foundation is implemented
* mobile security foundation is implemented
* telemetry/error/crash boundaries are implemented
* performance/resource lifecycle practices are implemented
* consistent error/loading/empty foundations are implemented
* testing infrastructure and tests are implemented
* development/build quality is validated
* documentation is updated
* actual limitations are documented
* no fake functionality is presented as real
* no secrets are improperly stored or exposed
* no placeholders remain
* no unrelated product scope was introduced

---

# IMPLEMENTATION REPORT

At the end of execution, provide a concise report containing:

## Files Changed

List created, modified, and removed files.

## Implemented Scope

Summarize the mobile architecture, authentication, storage, API, query/state, realtime, notification, deep-link, permission, location, maps, lifecycle, telemetry, accessibility, and testing foundations actually implemented.

## Shared Architecture

Identify the shared mobile services and abstractions established for later rider and driver features.

## Validation

Report the exact validation commands executed and their results.

## Limitations

Report only actual environment or platform limitations.

## Follow-Up Dependencies

Identify genuine dependencies required by the later rider and driver mobile volumes.

Do not invent additional project phases.

---

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement the complete shared mobile foundation defined by this prompt.

Preserve all working behavior that is outside the scope of necessary changes.

Use the repository's actual architecture and contracts as the source of truth.

Do not wait for another prompt.

Do not merely describe the implementation.

Create and modify the real production-grade mobile code, tests, configuration, and documentation required for this scope.

Do not use pseudo-code, placeholders, fabricated APIs, fake authentication, fake notifications, fake device capabilities, or simulated external-provider success presented as real functionality.

Respect actual Expo, iOS, Android, network, permission, background-execution, and device-lifecycle constraints.

Validate the implementation as thoroughly as the environment permits.

Finish only when this volume is genuinely implemented and integrated into the repository.
