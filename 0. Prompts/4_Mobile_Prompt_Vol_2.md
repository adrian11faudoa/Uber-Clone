# Uber-Style Global Ride-Hailing & Mobility Platform — Mobile Prompt — Volume 2

## ROLE

You are acting as the complete senior mobile engineering organization responsible for implementing the rider-facing mobile application experience for this project to production-grade standards.

Operate as a coordinated:

* Principal Software Architect
* Staff Mobile Engineer
* Staff React Native Engineer
* Staff TypeScript Engineer
* Staff UX Engineer
* Mobile Security Engineer
* Mobile Performance Engineer
* Reliability Engineer
* Accessibility Engineer
* QA Engineer
* Technical Writer

You are an implementation agent, not a teacher.

Your responsibility is to inspect the repository and implement the complete rider mobile experience covered by this prompt without breaking existing functionality.

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

1. Inspect the existing mobile application structure.
2. Inspect the Expo configuration, navigation, authentication/session layer, secure storage, API client, TanStack Query setup, local state, realtime infrastructure, push notifications, deep links, permissions, location/maps abstractions, UI components, tests, and documentation.
3. Inspect the backend and architecture contracts available in the repository.
4. Determine the actual rider-facing APIs, DTOs, enums, trip states, dispatch contracts, pricing contracts, location contracts, realtime events, authorization boundaries, idempotency behavior, and cancellation semantics.
5. Determine which rider functionality already exists.
6. Preserve compatible working behavior.
7. Reuse the shared mobile foundation established in the repository rather than creating parallel implementations.
8. Do not invent backend endpoints, events, state transitions, or payload structures where repository contracts already define them.
9. Where a required capability depends on a backend contract genuinely absent from the repository, implement the correct typed integration boundary and document the dependency rather than fabricating backend behavior.
10. Treat this prompt as independently executable. Do not rely on another AI conversation or on another prompt being pasted into the repository.

---

# TECHNOLOGY BASELINE

Use the repository's established mobile implementation where it is already present and compatible.

The intended mobile stack is:

* React Native
* Expo
* TypeScript

Use the shared mobile foundation for:

* authentication
* secure storage
* API communication
* TanStack Query
* local state
* realtime
* notifications
* deep linking
* permissions
* location
* maps
* telemetry
* accessibility
* connectivity

The mobile application integrates with the existing backend architecture based on:

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

Implement the complete **rider core mobile journey** from opening the rider home screen through requesting, tracking, completing, and recovering a ride.

The rider must be able to:

* open the rider experience
* determine current location where permitted
* select pickup
* search for a destination
* view map context
* select a service category
* obtain a fare estimate where supported
* request a ride
* wait for dispatch
* receive driver assignment
* track the assigned driver
* receive arrival updates
* begin and track the active trip
* cancel when permitted
* complete the trip
* handle post-trip state
* recover from network interruptions
* recover from websocket interruptions
* recover after app restart/backgrounding
* receive relevant push notifications/deep links into the active journey

This volume is the mobile counterpart of the rider's core operational experience.

Do not implement the complete rider account/payment/history/scheduled-trip experience here; that belongs to a later mobile volume.

---

# PRIMARY SCOPE

## 1. Rider Application Entry and Home

Implement the rider home experience.

Include:

* authenticated rider home
* map-first interface where appropriate
* current-location context
* pickup context
* destination entry
* service-category entry point
* active-trip recovery
* pending-request recovery
* scheduled-trip entry point where the existing navigation architecture requires it, without implementing the full scheduled-trip feature here
* notifications entry point where already available
* connection/offline state

When an active or pending trip exists, the application must recover into the correct trip state instead of presenting a fresh ride-request screen.

Do not assume an empty local store means there is no active trip.

The backend must be consulted when needed to recover authoritative state.

---

# 2. Current Location

Use the shared location foundation.

Support:

* permission request
* current location acquisition
* location accuracy state
* unavailable location
* denied permission
* blocked permission
* stale location
* refresh/retry
* map centering
* manual pickup override

The rider must still be able to select a pickup manually when current location is unavailable or inaccurate.

Do not continuously transmit rider location merely because the app is open.

Only use location transmission required by the established product/backend contract.

---

# 3. Pickup Selection

Implement rider pickup selection.

Support:

* current location as pickup
* map selection
* place search
* autocomplete where available
* selected-place confirmation
* address display
* coordinate representation
* map marker
* pickup correction
* loading/error state

Use the existing maps/geocoding/provider abstraction.

Do not hard-code provider-specific business logic into rider screens.

Do not assume an address string alone uniquely identifies a location.

Where backend contracts define canonical place/coordinate representations, preserve them.

---

# 4. Destination Search

Implement rider destination selection.

Support:

* typed destination search
* autocomplete
* result selection
* map confirmation
* address display
* coordinate data
* recent destinations only where already contractually supported
* retry/error
* empty results

Search interactions must be performant.

Do not issue uncontrolled requests on every keystroke.

Use the repository's established debouncing/cancellation strategy.

Do not persist sensitive destination history unless explicitly supported by the product/privacy model.

---

# 5. Map Interaction

Implement the core rider ride-request map experience.

Support:

* pickup marker
* destination marker
* user location
* camera movement
* route visualization where available
* loading state
* provider failure state
* map interaction
* recenter
* accessible alternatives for important information shown only on the map

Avoid unnecessary map rerenders.

Clean up listeners and subscriptions correctly.

---

# 6. Service Category Selection

Implement rider service/category selection.

Display only categories returned or permitted by the backend.

Support, where defined:

* service name
* category description
* passenger/capacity information
* availability
* estimated arrival
* fare estimate
* currency
* relevant product options
* unavailable category explanation

Do not hard-code service availability.

Do not show a service category that the backend says is unavailable.

---

# 7. Fare Estimate

Implement the rider fare-estimate experience.

Support:

* estimated total
* currency
* fare components where provided
* estimated travel time
* estimated distance
* service category
* dynamic pricing indicators where contractually exposed
* promotion indicator where already supported by the backend contract
* estimate expiration/staleness where applicable

Clearly distinguish:

**Estimate**

from:

**Final trip fare**

The frontend must never represent the estimate as the final charge.

Use backend-authoritative monetary values.

Do not perform authoritative price calculation in the mobile application.

---

# 8. Ride Request Form and Confirmation

Implement the ride-request confirmation flow.

Display:

* pickup
* destination
* service category
* fare estimate
* estimated pickup time where available
* important pricing disclosures where provided
* request action
* cancellation policy information where contractually appropriate

Before submission:

* validate required fields
* validate selected category
* verify required location data
* verify current trip/request state
* prevent duplicate submissions

Use the backend's required idempotency mechanism.

---

# 9. Ride Request Submission

Implement ride-request submission.

Requirements:

* use established API contract
* use required idempotency key
* prevent duplicate requests
* show pending state
* handle success
* handle validation failure
* handle category unavailable
* handle dispatch unavailable
* handle server rejection
* handle timeout/uncertain network outcome
* reconcile the authoritative request/trip state after uncertain outcomes

Do not create a new idempotency key simply because a network retry occurred.

Do not optimistically show a successfully created trip when the request outcome is unknown.

---

# 10. Dispatch Waiting State

Implement the rider waiting-for-dispatch experience.

Support:

* request accepted
* dispatch searching
* searching indicator
* candidate/assignment status only where the backend explicitly exposes it
* estimated wait where available
* cancellation
* backend errors
* retry where appropriate
* realtime updates
* app background/resume recovery

The rider must understand that:

* the request exists
* a driver may not yet be assigned
* the system is still attempting assignment

Do not expose internal dispatch candidate lists or confidential driver-selection logic.

---

# 11. Driver Assignment

Implement the rider experience after a driver is assigned.

Display information contractually available to the rider, such as:

* driver name
* driver photo
* driver rating
* vehicle details
* vehicle identifier
* pickup ETA
* trip/request state
* map position
* relevant contact options

Respect backend privacy and authorization.

Do not expose:

* internal driver identifiers
* private contact data
* raw driver location history
* internal risk/dispatch information

---

# 12. Driver Location Tracking

Integrate authenticated realtime driver-location updates.

Support:

* current driver position
* position updates
* stale-location handling
* reconnect
* missed-event recovery
* API reconciliation
* map marker updates
* ETA changes where supported

Do not let every raw location message trigger an expensive full-screen rerender.

Bound browser/device state to current relevant data.

If realtime is disconnected:

* show an appropriate degraded state
* reconcile through the authoritative API when supported
* recover automatically when the connection returns

---

# 13. Driver Arrival

Implement rider-facing driver-arrival behavior.

Support:

* approaching pickup
* near pickup
* arrived
* waiting
* relevant ETA updates
* arrival notification
* contact options where allowed
* cancellation options where still permitted
* safety/support entry points

Do not mark arrival based solely on a local timer.

Use backend/realtime state.

---

# 14. Active Trip

Implement the rider active-trip experience.

Support the established state machine for:

* trip started
* passenger onboard
* active journey
* route/progress
* destination
* trip completion
* cancellation/exception where permitted

Display:

* current trip state
* route/map
* destination
* driver summary
* relevant ETA/time/distance
* appropriate safety controls
* support access
* trip cancellation where still valid
* relevant notifications

Do not create client-only trip state transitions.

---

# 15. Trip Cancellation

Implement rider cancellation according to backend rules.

Support:

* determine whether cancellation is currently allowed
* cancellation reason where required
* confirmation
* cancellation fee when backend provides it
* mutation state
* success
* rejection
* stale-state handling
* network timeout/reconciliation
* post-cancellation state

Do not calculate cancellation fees locally.

Do not show a completed cancellation until the backend confirms it or the canonical resource state establishes it.

---

# 16. Trip Completion

Implement the rider post-completion transition.

After backend-confirmed completion:

* show completion state
* show final fare when available
* display payment state where available without implementing full payment management
* provide receipt entry point where supported
* provide rating entry point where supported
* provide support entry point
* preserve access to trip details

Do not claim final payment settlement merely because the trip was completed.

---

# 17. Trip-State Recovery

Implement robust recovery for:

* app termination
* app restart
* foreground/background transitions
* lost websocket connection
* missed events
* delayed API response
* stale local state
* network interruption
* authentication refresh during a trip

On app startup/resume:

1. determine whether the authenticated rider has an active/pending trip
2. obtain authoritative state
3. restore the correct screen
4. reconnect realtime
5. reconcile missed updates

Do not rely exclusively on local navigation state to determine the current trip.

---

# 18. Realtime Event Handling

Consume the rider-relevant realtime events established by backend contracts.

Potential events include:

* request accepted
* dispatch progress
* driver assigned
* driver location update
* driver arrival
* trip started
* trip state transition
* trip canceled
* trip completed
* fare/payment state update
* notification
* other rider-visible events

Implement:

* authenticated subscriptions
* event validation
* event deduplication
* ordering/version handling where defined
* cache reconciliation
* reconnect/resubscription
* missed-event recovery

Do not invent event names.

---

# 19. Push Notifications and Deep Links

Integrate the shared push/deep-link foundation for rider trip events.

Support routing from notifications into:

* pending ride request
* assigned driver
* driver arrival
* active trip
* completed trip
* cancellation
* relevant support/safety destination

Handle:

* cold start
* warm start
* authenticated state not yet restored
* expired/invalid destination
* unauthorized resource
* already-completed trip
* duplicate notification

Do not navigate to sensitive resources before authentication and authorization state are established.

---

# 20. Network and Offline Behavior

Ride requests and active trips require careful handling of unreliable connectivity.

Support:

* online
* offline
* reconnecting
* backend unavailable
* websocket disconnected
* request timeout
* uncertain mutation result

For a request with uncertain outcome:

* do not submit blindly again
* reconcile through the authoritative resource/API
* reuse idempotency semantics where required

During an active trip:

* maintain the last known valid state
* clearly identify stale information
* recover automatically when connectivity returns

Do not claim live trip status while disconnected and without recent authoritative data.

---

# 21. Loading, Empty, Error, and Degraded States

Implement intentional rider UX for:

* initial map loading
* location loading
* search loading
* no search results
* unavailable service category
* fare-estimate loading
* request submission
* dispatch waiting
* driver assignment
* realtime disconnection
* stale driver location
* backend errors
* cancellation errors
* expired request
* trip unavailable
* authentication expiry
* permission denial

Do not use generic blank screens.

---

# 22. Rider Safety and Support Entry Points

Integrate safety/support entry points that are already defined by backend/product contracts.

Support contextual access during:

* waiting for pickup
* driver arrival
* active trip
* completed trip

Where the backend supports structured incident/support creation:

* pass only authorized trip/context identifiers
* validate state
* prevent duplicate submissions
* show resulting status

Do not implement the full operations/safety investigation system in this volume.

---

# 23. Accessibility

The rider journey must be accessible.

Support:

* screen-reader-friendly map alternatives
* accessible pickup/destination controls
* accessible search results
* accessible fare information
* accessible ride-request confirmation
* accessible trip status announcements
* accessible cancellation dialogs
* accessible driver-arrival status
* accessible action buttons
* dynamic text sizing
* sufficient touch targets
* color-independent status communication

Important trip-state changes should be announced appropriately without creating duplicate announcements from both realtime and query updates.

---

# 24. Mobile UX and Responsive Layout

Because this is native mobile rather than responsive web, optimize for:

* one-handed interaction where practical
* safe-area handling
* different screen sizes
* portrait/landscape behavior where relevant
* readable map overlays
* thumb-friendly primary actions
* modal/sheet ergonomics
* system navigation areas

Do not allow critical actions to be hidden behind inaccessible gesture-only interactions.

---

# 25. Rider Security and Privacy

Protect:

* trip information
* driver information
* location information
* contact information
* authentication state

Requirements:

* backend-authoritative authorization
* secure storage for credentials
* no sensitive credentials in general local state
* no raw tokens in logs
* no unnecessary precise-location telemetry
* no unnecessary destination-history persistence
* safe deep-link handling
* no exposure of private driver data
* safe analytics instrumentation

Do not use trip identifiers or other sensitive data unnecessarily in logs or analytics.

---

# 26. Performance

The core ride journey must remain responsive despite realtime updates.

Optimize:

* map rendering
* location rendering
* driver-marker updates
* realtime event processing
* query updates
* route/polyline rendering
* search requests
* fare-estimate requests
* list rendering
* image loading
* state transitions

Avoid:

* full-screen rerender for every driver-location event
* duplicate websocket subscriptions
* duplicate API requests
* unlimited event retention
* unnecessary global state updates

Clean up every location watcher, event listener, timer, and realtime subscription correctly.

---

# 27. Testing

Implement meaningful mobile tests for the rider journey.

## Unit Tests

Cover:

* rider trip-state mapping
* action eligibility by state
* location-state mapping
* service-category presentation
* fare/currency formatting
* cancellation eligibility
* deep-link parsing
* realtime event reconciliation
* request/idempotency helpers
* stale-data detection

## Component Tests

Cover:

* rider home
* pickup selector
* destination search
* service-category selection
* fare estimate
* ride confirmation
* dispatch waiting
* driver assignment
* driver arrival
* active trip
* cancellation
* completion
* connection/offline states
* permission-denied states

## Integration Tests

Cover:

* authenticated rider entry
* location permission flow
* pickup selection
* destination selection
* fare estimate
* ride request
* uncertain request outcome/reconciliation
* dispatch waiting
* driver assignment
* realtime driver location
* driver arrival
* active trip
* cancellation
* completion
* app restart/recovery
* websocket reconnect
* push/deep-link routing

Use mocks/test doubles for unavailable external services.

Do not claim production map, routing, push, or provider integration was validated when only mocked behavior was tested.

---

# 28. Documentation

Update mobile documentation for the rider journey.

Document:

* rider route/navigation structure
* trip state UI mapping
* ride-request flow
* location usage
* maps integration
* dispatch waiting
* driver assignment
* realtime events consumed
* recovery behavior
* cancellation semantics
* push/deep-link behavior
* support/safety entry points
* testing
* known platform limitations

Documentation must describe actual implementation.

Do not document unsupported capabilities as completed.

---

# OUT OF SCOPE

Do not implement the broader rider account/product surface in this volume.

Explicitly out of scope:

* rider profile/settings implementation
* trip-history screens
* detailed receipt management
* payment-method management
* refund management
* promotions management
* full scheduled-trip management
* driver mobile product experience
* driver earnings/payout screens
* operations/admin mobile experience
* backend implementation
* database changes
* dispatch-engine implementation
* payment-provider backend implementation
* routing-provider backend implementation
* infrastructure/Terraform
* Kubernetes/EKS
* cloud provisioning
* CI/CD redesign
* separate QA phase
* separate final-integration phase

Where later rider functionality needs an entry point from this journey, create the correct navigation boundary without implementing the unrelated feature itself.

---

# IMPLEMENTATION RULES

## Repository First

Inspect before modifying.

Determine the actual:

* mobile application architecture
* navigation
* API client
* query architecture
* realtime architecture
* maps abstraction
* location abstraction
* notification/deep-link system
* UI primitives
* testing setup

Reuse the shared mobile foundation.

## No Parallel Infrastructure

Do not create:

* another API client
* another websocket client
* another map abstraction
* another location service
* another notification manager
* another authentication system
* another state-management architecture

when the repository already provides an appropriate shared implementation.

## Backend Contract Discipline

Do not invent:

* endpoints
* DTOs
* event names
* trip-state enums
* cancellation rules
* dispatch semantics
* fare rules

when contracts already exist.

## State-Machine Discipline

Only expose actions valid for the authoritative trip/request state.

Do not allow client-side state to bypass backend lifecycle rules.

## Financial Discipline

Use backend-provided estimates and final values.

Do not calculate authoritative fares on-device.

Do not claim final settlement from request or trip completion alone.

## Realtime Discipline

Reconcile events with API state when necessary.

Handle:

* duplicates
* ordering
* reconnect
* missed events
* stale state

## Mutation Discipline

Use idempotency as required.

Do not blindly retry ride creation or cancellation.

## Platform Reality

Respect actual iOS/Android/Expo behavior for:

* permissions
* app backgrounding
* notifications
* location
* lifecycle
* connectivity

Do not claim native background guarantees from APIs that do not provide them.

## No Pseudo-Code

Implement real production code.

Do not use:

* placeholders
* TODO implementations
* fake endpoints
* fake trips
* fake drivers
* fake locations
* fake fare calculations
* simulated successful ride requests presented as real
* omitted implementations
* “implement similarly”

---

# VALIDATION REQUIREMENTS

Before considering this volume complete:

1. Run formatting checks.
2. Run linting.
3. Run TypeScript/type checks.
4. Run rider unit tests.
5. Run rider component tests.
6. Run rider integration tests available in the repository.
7. Validate rider navigation.
8. Validate authenticated rider bootstrap.
9. Validate location permission/error handling.
10. Validate pickup selection.
11. Validate destination search.
12. Validate service-category selection.
13. Validate fare-estimate state handling.
14. Validate idempotent ride request behavior.
15. Validate dispatch waiting.
16. Validate driver assignment.
17. Validate driver-location updates.
18. Validate driver-arrival state.
19. Validate active-trip state machine.
20. Validate cancellation behavior.
21. Validate trip completion.
22. Validate app restart/recovery.
23. Validate websocket reconnect.
24. Validate push/deep-link routing.
25. Validate offline and degraded-network handling.
26. Validate accessibility checks available in the repository.
27. Validate sensitive-data logging/storage boundaries.
28. Validate map/location resource cleanup.
29. Validate production build or strongest available mobile build equivalent.
30. Verify no TODO/placeholder production code remains.
31. Verify documentation matches actual behavior.

Where the environment prevents device/provider validation, perform all repository-side validation that is possible and explicitly report what could not be validated.

Never claim real physical-device, map-provider, notification-provider, or production backend validation unless it actually occurred.

---

# INTEGRATION CHECK

Before finalizing, verify that this rider mobile implementation integrates cleanly with the shared mobile foundation and the rest of the project.

Confirm that:

* rider authentication uses the shared session implementation
* rider API calls use the shared API client
* rider server state uses the shared query architecture
* rider realtime uses the shared websocket foundation
* rider location uses the shared location abstraction
* rider maps use the shared map abstraction
* rider push notifications use the shared notification system
* deep links route through the shared navigation/deep-link architecture
* rider trip state uses the canonical backend lifecycle
* dispatch updates reconcile with authoritative trip state
* driver-location updates do not create performance regressions
* ride request and cancellation honor idempotency/concurrency contracts
* application restart correctly restores active/pending trip state
* logout clears rider-specific sensitive/query state
* later rider account/history/payment/scheduled-trip functionality can integrate without rewriting this journey
* later driver functionality can coexist without duplicating the shared mobile foundation

The mobile application must remain one coherent architecture as the remaining mobile volumes are implemented.

---

# DEFINITION OF DONE

This volume is complete only when:

* rider mobile home is implemented
* current-location handling is implemented
* pickup selection is implemented
* destination search is implemented
* rider map interaction is implemented
* service-category selection is implemented
* fare-estimate experience is implemented
* ride confirmation is implemented
* idempotent ride-request submission is implemented
* dispatch waiting is implemented
* driver assignment is implemented
* realtime driver-location tracking is implemented
* driver-arrival experience is implemented
* active-trip experience is implemented
* rider cancellation is implemented
* trip completion flow is implemented
* trip-state recovery is implemented
* realtime event handling is integrated
* push/deep-link handling is integrated
* network/offline/degraded states are handled
* safety/support entry points are integrated where supported
* accessibility requirements are addressed
* performance requirements are addressed
* security/privacy requirements are addressed
* meaningful tests are implemented
* documentation is updated
* validation has been executed
* limitations are honestly reported
* no fake functionality is presented as real
* no placeholders remain
* no unrelated rider/driver/mobile scope was introduced

---

# IMPLEMENTATION REPORT

At the end of execution, provide a concise report containing:

## Files Changed

List created, modified, and removed files.

## Implemented Scope

Summarize the rider home, pickup, destination, maps, fare estimate, request, dispatch, assignment, driver tracking, active-trip, cancellation, completion, recovery, and notification/deep-link functionality actually implemented.

## Contracts Used

Identify the API, trip-state, dispatch, location, realtime, map, notification, and support/safety contracts used.

## Validation

Report the exact validation commands executed and their results.

## Limitations

Report only actual environment, device, provider, or contract limitations.

## Follow-Up Dependencies

Identify genuine dependencies for the later rider and driver mobile volumes.

Do not invent additional project phases.

---

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement the complete rider mobile core journey defined by this prompt.

Preserve all working behavior that is outside the scope of necessary changes.

Use the repository's actual architecture and contracts as the source of truth.

Do not wait for another prompt.

Do not merely describe the implementation.

Create and modify the real production-grade mobile code, tests, configuration, and documentation required for this scope.

Do not use pseudo-code, placeholders, fabricated APIs, fake trips, fake driver locations, fake fares, fake dispatch behavior, or simulated success presented as real functionality.

Respect actual iOS, Android, Expo, location, notification, lifecycle, and connectivity constraints.

Validate the implementation as thoroughly as the environment permits.

Finish only when this volume is genuinely implemented and integrated into the repository.
