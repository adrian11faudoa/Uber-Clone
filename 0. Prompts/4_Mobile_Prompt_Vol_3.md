# Uber-Style Global Ride-Hailing & Mobility Platform — Mobile Prompt — Volume 3

## ROLE

You are acting as the complete senior mobile engineering organization responsible for implementing the driver-facing mobile application experience for this project to production-grade standards.

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

Your responsibility is to inspect the repository and implement the complete driver mobile experience covered by this prompt without breaking existing functionality.

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
2. Inspect Expo/native configuration, navigation, authentication/session handling, secure storage, API client, TanStack Query configuration, local state, realtime transport, notifications, deep links, permissions, location, maps, shared UI primitives, tests, and documentation.
3. Inspect backend and architecture contracts available in the repository.
4. Determine the actual driver-facing APIs, DTOs, enums, authorization boundaries, dispatch-offer contracts, work-session/availability contracts, location contracts, trip state machine, scheduled-trip contracts, notifications, messaging, safety, and earnings contracts.
5. Determine which driver functionality already exists.
6. Preserve compatible working behavior.
7. Reuse the shared mobile foundation established in the repository rather than creating parallel infrastructure.
8. Do not invent endpoint paths, event names, DTO fields, permissions, state transitions, or mutation semantics where repository contracts already define them.
9. Where a required capability genuinely depends on a missing backend contract, implement the correct typed integration boundary based on the established architecture and document the dependency rather than fabricating backend behavior.
10. Treat this prompt as independently executable. Do not depend on another AI conversation or another prompt being pasted into the repository.

---

# TECHNOLOGY BASELINE

Use the repository's established implementation where it is already present and compatible.

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
* push notifications
* deep links
* permissions
* location
* maps
* telemetry
* accessibility
* connectivity
* lifecycle handling

The mobile application integrates with the backend architecture based on:

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

Implement the complete **driver core mobile journey**.

The driver must be able to:

* open the authenticated driver workspace
* understand readiness and operational eligibility
* start and stop availability/work sessions
* safely provide driver location while operational
* receive realtime dispatch offers
* inspect offers
* accept or reject offers
* recover from offer races/expiration
* receive trip assignments
* navigate to pickup
* mark arrival
* communicate with the rider where supported
* wait for pickup
* start and conduct the active trip
* navigate to destination
* complete the trip
* cancel or report allowed exceptions
* recover from network/realtime interruptions
* handle app background/foreground transitions according to actual platform capabilities
* receive scheduled assignments where supported
* access safety/support entry points during the working journey

This volume implements the driver operational journey.

It does not implement the broader driver account, earnings, payout, ratings, notification-management, or advanced profile functionality that belongs to the final mobile volume.

---

# PRIMARY SCOPE

## 1. Driver Application Entry and Workspace

Implement the driver mobile home/workspace.

Include:

* authenticated driver entry
* current driver operational state
* readiness summary
* availability/work-session control
* current trip state
* incoming offer state
* current location status
* realtime connection status
* relevant operational warnings
* support/safety access
* notifications entry point through the shared notification architecture
* scheduled-assignment entry point where appropriate

When the driver has an active assignment or trip:

* recover the authoritative state
* route to the correct workflow
* do not present a fresh availability screen as though no work exists

Do not rely exclusively on local navigation state for recovery.

---

# 2. Driver Readiness

Implement driver readiness presentation.

Display server-authoritative information relevant to whether the driver may receive trips.

Possible states include:

* ready
* onboarding incomplete
* verification pending
* verification failed where user-visible
* vehicle unavailable
* document expired
* service area unavailable
* account restricted
* temporary hold
* dispatch unavailable
* maintenance restriction

Clearly distinguish:

* identity/account readiness
* vehicle readiness
* location capability
* work-session state
* dispatch eligibility

Do not expose internal risk or fraud decisions.

---

# 3. Availability and Work Session

Implement driver availability/work-session controls.

Support backend-defined behavior for:

* go online
* go offline
* start work session
* end work session
* temporary unavailable state
* blocked/restricted state
* pending transition

Requirements:

* clear current state
* action confirmation where required
* mutation progress
* success
* failure
* retry
* duplicate-submission protection
* reconciliation after reconnect
* browser/mobile lifecycle recovery

Never assume an availability transition succeeded because the button was tapped.

Wait for the appropriate backend confirmation.

---

# 4. Location Permission and Operational Location

Integrate the shared mobile location foundation.

Support:

* foreground location
* background location where the native app and backend contract permit it
* permission request
* denied permission
* blocked permission
* unavailable location
* poor accuracy
* stale location
* location acquisition failure
* location-sharing status
* recovery/retry
* lifecycle cleanup

The driver must understand when location is preventing them from being operational.

Do not claim background location capability that the actual app configuration and platform permissions do not provide.

---

# 5. Driver Location Transmission

Implement the driver-facing location transmission required by the established backend contract.

Support, as defined by the platform:

* location sampling
* appropriate update interval
* accuracy handling
* stale-location detection
* authenticated transmission
* retry
* batching where contractually supported
* connection recovery
* foreground/background transitions
* duplicate/out-of-order protection at the client boundary where necessary

Avoid unnecessarily transmitting more location data than the backend contract requires.

Do not log precise location unnecessarily.

Do not make client-side filtering authoritative for backend operational eligibility.

---

# 6. Driver Realtime Connection

Use the shared authenticated websocket infrastructure.

Support:

* connect
* authenticate
* subscribe
* heartbeat/liveness where defined
* reconnect
* exponential/backoff behavior where established
* resubscribe
* disconnect on logout
* foreground/background lifecycle transitions
* stale-connection detection
* missed-event recovery
* event routing

Provide clear driver-facing connection state:

* connected
* connecting
* reconnecting
* degraded
* disconnected

Do not allow a disconnected websocket to make the driver appear fully operational.

---

# 7. Dispatch Offer Reception

Implement realtime ride-offer reception.

When a driver receives an offer, present the backend-authoritative information permitted by the product.

Possible information:

* pickup
* destination where permitted
* estimated travel time
* estimated pickup distance
* service category
* relevant rider information
* earnings/price estimate where permitted
* offer expiration
* trip characteristics
* operational warnings

Do not expose information forbidden by rider privacy or dispatch contracts.

Do not independently calculate an authoritative earning value.

---

# 8. Offer Presentation

Build a focused, interruption-safe offer UI.

Support:

* new-offer state
* visible expiration/countdown
* accept
* reject
* expired state
* resolved state
* unavailable state
* duplicate event handling
* connection degradation
* accessibility announcement

The offer must not remain actionable after the backend says it is no longer available.

Do not use a local countdown as the authoritative offer expiration source.

The countdown is a UX representation of backend-established expiration semantics.

---

# 9. Offer Acceptance

Implement offer acceptance using the established dispatch contract.

Requirements:

* explicit confirmation/action state
* duplicate-submit protection
* idempotency where required
* success handling
* offer already taken
* offer expired
* eligibility changed
* trip canceled
* dispatch conflict
* timeout
* uncertain network result
* authoritative reconciliation

For an uncertain acceptance result:

1. do not blindly submit another acceptance
2. reconcile offer/trip state
3. reuse required idempotency semantics
4. route to the correct resulting state

Do not claim assignment until confirmed by the backend.

---

# 10. Offer Rejection

Implement offer rejection.

Support:

* rejection reason where required
* confirmation where necessary
* submission progress
* success
* rejected-state cleanup
* failure
* retry
* already-resolved offer
* expired offer

Do not keep resolved offers in actionable UI state.

Do not invent rejection reasons when the backend contract defines a fixed set.

---

# 11. Offer Expiration and Concurrency

Handle dispatch races correctly.

Examples include:

* another driver accepts first
* backend expires offer before local countdown reaches zero
* driver loses connectivity during acceptance
* duplicate offer event
* old offer arrives after a newer offer
* assignment event arrives before acceptance response

Use backend identifiers and ordering/version semantics where available.

The UI must converge to the authoritative state.

---

# 12. Assignment Recovery

When the driver has been assigned a trip:

* retrieve authoritative assignment/trip state
* reconnect relevant realtime subscriptions
* restore the trip workflow
* initialize location/navigation state as required
* dismiss obsolete offers
* prevent conflicting actions

If the application restarts during an active assignment, recover the assignment rather than returning the driver to the offline screen.

---

# 13. Assigned Trip Workspace

Implement the driver assigned-trip screen.

Display relevant information such as:

* trip state
* pickup
* destination
* rider summary
* service category
* map
* navigation action
* trip progress
* relevant ETA
* contact action
* safety action
* support action
* allowed trip transition actions

Actions must be derived from the canonical trip state machine.

Do not display actions that are invalid in the current state.

---

# 14. Navigation to Pickup

Integrate the maps/routing abstraction.

Support:

* pickup map
* route visualization where available
* navigation handoff
* current location
* pickup marker
* ETA
* route updates where supported
* stale-route indication
* provider failure/retry

Do not hard-code provider-specific routing logic into trip screens.

Do not implement a second routing engine.

---

# 15. Arrival at Pickup

Implement driver arrival workflow.

Support:

* arriving
* arrival action
* pending arrival confirmation
* confirmed arrival
* waiting for rider
* passenger-ready state where supported
* wait-time information where supported
* contact rider where permitted
* cancellation path where allowed
* safety/support access

Do not mark arrival complete before authoritative confirmation.

If the arrival mutation conflicts with backend state:

* refresh/reconcile
* show the actual trip state
* avoid duplicating the mutation

---

# 16. Rider Communication

Integrate the shared messaging capability where supported.

Support:

* trip-linked conversation
* message history
* sending
* delivery state
* read state where supported
* realtime messages
* reconnect
* failed-send retry
* attachment support only where established

Do not expose unrelated conversations.

Do not expose private rider data beyond the trip's authorized messaging context.

---

# 17. Passenger Pickup

Implement the transition from waiting to trip start.

Support the backend-defined progression from:

* waiting
* rider ready
* passenger onboard
* trip started

where applicable.

Handle:

* duplicate start actions
* backend rejection
* cancellation
* stale state
* reconnect
* app resume

Do not allow local state to bypass the trip state machine.

---

# 18. Active Trip

Implement the driver's active-trip mobile workflow.

Support:

* active trip state
* destination
* route/navigation
* trip progress
* current location
* ETA
* rider communication
* safety controls
* support
* cancellation/exception action where permitted
* trip completion

Use performant map and location rendering.

Do not rerender the full screen for every raw location update unnecessarily.

---

# 19. Active-Trip Realtime

During active trips, reconcile:

* trip transitions
* rider-visible state changes relevant to the driver
* route/ETA updates where supplied
* cancellation
* support/safety events
* messaging
* payment/earnings state where immediately relevant

Handle:

* duplicate events
* out-of-order events
* missed events
* reconnect
* API reconciliation
* app restart

Use the backend's version/sequence/timestamp semantics when available.

---

# 20. Trip Cancellation and Exception Handling

Implement driver cancellation/exception flows supported by the backend.

Include:

* current cancellation eligibility
* reason selection
* confirmation
* mutation progress
* result
* server rejection
* stale-state conflict
* network uncertainty
* recovery
* resulting trip state

When the backend provides cancellation consequences/fees/penalties:

* display the authoritative value
* do not calculate it locally
* do not expose internal enforcement formulas

Do not allow a client-only cancellation state.

---

# 21. Trip Completion

Implement driver trip completion.

Support:

* completion action
* confirmation where required
* completion progress
* success
* failure
* duplicate-completion protection
* state reconciliation
* transition to completed-trip state
* subsequent earnings state where returned
* rating eligibility where supported
* support/safety access

Do not claim finalized earnings merely because the completion request succeeded.

The authoritative earnings state may be asynchronous.

---

# 22. Active Trip Recovery

Implement recovery across:

* app restart
* app termination
* foreground/background transition
* network loss
* websocket loss
* authentication refresh
* location permission changes
* navigation away and back

On resume/start:

1. restore authenticated session
2. determine whether a driver has an active/pending assignment
3. obtain authoritative trip/work-session state
4. restore correct screen
5. reconnect realtime
6. restore location transmission where permitted
7. reconcile missed events

Do not rely only on persisted navigation state.

---

# 23. Driver Safety and Emergency Access

Integrate driver-facing safety functionality supported by the backend/product contracts.

Provide appropriate entry points during:

* offer state where relevant
* pickup
* waiting
* active trip
* post-trip

Depending on actual contracts, this may include:

* emergency/help action
* incident report
* safety case creation
* trip-specific support
* suspicious/risk reporting
* evidence submission

Do not invent emergency-service integrations that are not actually implemented.

Do not make false claims about contacting emergency services.

---

# 24. Trip-Specific Support

Implement contextual support access.

Support:

* trip-linked support case creation where supported
* issue category
* description
* attachment handoff where supported
* submission state
* existing case status
* retry/error

Use authorized trip context.

Do not build the support-agent interface.

---

# 25. Scheduled Assignments

Implement the driver operational portion of scheduled trips where the backend supports it.

Support:

* scheduled assignment visibility
* scheduled pickup
* destination
* service category
* scheduled time
* preparation status
* pre-dispatch status
* assignment state
* accept/reject where contractually supported
* cancellation/exception behavior where permitted
* transition into the ordinary pickup/trip workflow

Clearly distinguish scheduled work from immediate dispatch offers.

Do not claim assignment before backend confirmation.

---

# 26. Driver Operational Notifications

Use the shared push notification/deep-link system for driver events such as:

* assignment
* scheduled assignment
* offer-related event where push is applicable
* trip changes
* account/readiness state
* operational alerts
* support/safety updates

Notification handling must:

* validate destination
* respect authentication
* respect driver role
* handle stale resources
* work from cold start
* avoid duplicate navigation

Do not implement a second notification delivery system.

---

# 27. Permissions and Platform State

Handle platform changes during operational use.

Examples:

* location permission revoked
* notifications disabled
* app backgrounded
* location services disabled
* network switched
* Bluetooth/system capability changes only where actually required
* low-connectivity state

The UI must clearly communicate the operational consequence.

Do not silently continue as though permissions remain valid.

---

# 28. Offline and Network Degradation

Driver workflows require strong treatment of uncertain connectivity.

Handle:

* offline
* reconnecting
* websocket disconnected
* backend unavailable
* location upload failure
* delayed mutation response
* stale trip state

For important mutations:

* use idempotency where required
* do not blindly retry
* reconcile authoritative state after uncertain results

During an active trip, retain only bounded last-known state.

Clearly communicate when information is stale.

Do not claim live operational status without recent authoritative state.

---

# 29. Driver UI and Interaction Quality

Optimize the driver app for use while operational.

Design for:

* large primary actions
* clear state hierarchy
* quick access to navigation
* minimal interaction steps
* readable information under time pressure
* safe confirmation for destructive actions
* one-handed use where practical

Do not overload the active-trip screen with low-priority information.

Follow the established mobile design system.

---

# 30. Accessibility

Support:

* screen readers
* dynamic text
* accessible buttons
* accessible countdowns
* accessible status announcements
* accessible map alternatives
* sufficient touch targets
* non-color-only state indicators
* accessible dialogs
* focus/interaction consistency

Important operational events such as:

* offer received
* offer expired
* assignment received
* driver arrival confirmed
* trip started
* trip canceled
* trip completed

must have an appropriate accessibility announcement strategy.

Avoid duplicate announcements caused by both query updates and realtime events.

---

# 31. Security and Privacy

Protect:

* driver credentials
* driver location
* rider information
* trip information
* conversations
* safety data
* earnings information

Requirements:

* secure credential storage
* backend-authoritative authorization
* no raw tokens in logs
* no unnecessary precise-location telemetry
* no unnecessary rider data persistence
* safe deep links
* safe notification payload handling
* no provider secrets in the app
* safe rendering of user-controlled content

Do not expose internal dispatch/risk information.

---

# 32. Performance

The driver application may receive frequent location and realtime updates.

Optimize:

* location transmission workload
* map updates
* driver marker movement
* websocket processing
* query updates
* countdowns
* timers
* navigation
* message rendering
* notification processing
* image loading
* memory usage

Avoid:

* full application rerender per location event
* duplicate websocket subscriptions
* uncontrolled timers
* unlimited event history
* excessive location frequency
* stale listeners after navigation

Use lifecycle-aware cleanup.

---

# 33. Testing

Implement meaningful automated tests.

## Unit Tests

Cover:

* driver readiness-state mapping
* work-session state mapping
* availability action eligibility
* offer-state mapping
* offer expiration logic
* accept/reject state handling
* trip-action eligibility
* cancellation eligibility
* location-state mapping
* realtime reconciliation
* deep-link routing
* scheduled-assignment state mapping

## Component Tests

Cover:

* driver home/workspace
* readiness
* availability controls
* location permission state
* offer card
* offer expiration
* accept/reject
* assigned trip
* navigation/pickup
* arrival
* waiting
* active trip
* cancellation
* completion
* scheduled assignment
* messaging
* safety/support entry points
* offline/reconnect states

## Integration Tests

Cover:

* authenticated driver entry
* session restoration
* readiness retrieval
* availability transition
* location initialization
* realtime connection
* incoming dispatch offer
* acceptance race
* rejection
* assignment
* pickup
* arrival
* rider messaging
* trip start
* active trip
* cancellation
* completion
* scheduled assignment
* app restart recovery
* websocket reconnect
* location permission loss
* push/deep-link routing

Use mocks/test doubles for unavailable device or external services.

Do not claim real physical-device or production dispatch validation when it was not performed.

---

# 34. Documentation

Update mobile documentation to describe the implemented driver journey.

Document:

* driver navigation
* readiness/eligibility
* availability/work sessions
* location permissions
* location transmission behavior
* realtime events
* dispatch offers
* offer concurrency/recovery
* trip-state UI
* navigation/maps
* messaging
* safety/support
* scheduled assignments
* lifecycle recovery
* offline behavior
* testing
* platform limitations

Documentation must describe actual implementation rather than planned functionality.

---

# OUT OF SCOPE

Do not implement the broader driver product surface in this volume.

Explicitly out of scope:

* full driver profile/settings management
* detailed driver onboarding management
* driver earnings dashboards
* earnings history
* payout management
* driver ratings/reputation screens
* full notification-management UI
* advanced account/security settings
* rider mobile implementation
* operations/admin mobile application
* backend implementation
* database/schema redesign
* dispatch-engine implementation
* payment-provider backend implementation
* routing-provider backend implementation
* infrastructure/Terraform
* Kubernetes/EKS
* cloud provisioning
* CI/CD redesign
* separate QA phase
* separate final-integration phase

Where this journey needs a navigation entry point to one of those later features, create the correct navigation boundary without implementing the unrelated feature.

---

# IMPLEMENTATION RULES

## Repository First

Inspect before modifying.

Determine the actual:

* mobile architecture
* navigation
* shared foundation
* authentication
* API client
* query architecture
* realtime
* notification/deep-link handling
* location
* maps
* UI system
* tests

Reuse the shared foundation.

## No Parallel Infrastructure

Do not create another:

* API client
* websocket client
* location service
* notification manager
* authentication system
* map abstraction
* state architecture

when the repository already has a suitable shared implementation.

## State-Machine Discipline

Only expose driver actions valid for the authoritative backend state.

Do not create client-only trip transitions.

## Dispatch Discipline

Treat offer availability, expiration, acceptance, assignment, and conflicts as backend-authoritative.

Do not infer assignment from local UI actions.

## Location Discipline

Use actual platform capabilities.

Do not promise continuous background location if the app's configuration/platform permissions do not support it.

Do not transmit location more frequently than required by the established contract.

## Financial Discipline

Use backend-provided earnings/payment values.

Do not calculate authoritative earnings or penalties on-device.

## Mutation Discipline

Use idempotency and concurrency controls required by the backend.

Never blindly retry uncertain mutations.

## No Pseudo-Code

Implement real production code.

Do not use:

* placeholders
* TODO-only implementations
* fake offers
* fake drivers
* fake locations
* fake trip transitions
* fabricated endpoints
* simulated successful assignments
* fabricated earnings
* omitted implementations
* “implement similarly”

---

# VALIDATION REQUIREMENTS

Before considering this volume complete:

1. Run formatting checks.
2. Run linting.
3. Run TypeScript/type checks.
4. Run driver unit tests.
5. Run driver component tests.
6. Run driver integration tests available in the repository.
7. Validate authenticated driver bootstrap.
8. Validate readiness/eligibility presentation.
9. Validate availability/work-session transitions.
10. Validate location permission handling.
11. Validate location lifecycle/transmission behavior where testable.
12. Validate realtime connection/reconnect.
13. Validate dispatch-offer reception.
14. Validate offer expiration.
15. Validate acceptance/rejection.
16. Validate acceptance-race reconciliation.
17. Validate assignment recovery.
18. Validate pickup navigation.
19. Validate arrival flow.
20. Validate rider messaging where supported.
21. Validate active-trip lifecycle.
22. Validate cancellation behavior.
23. Validate completion.
24. Validate scheduled assignments where supported.
25. Validate push/deep-link routing.
26. Validate app restart recovery.
27. Validate offline/degraded-network behavior.
28. Validate location-permission loss.
29. Validate accessibility checks available in the repository.
30. Validate performance-sensitive realtime/location cleanup.
31. Validate sensitive-data storage/logging boundaries.
32. Validate production mobile build or strongest available equivalent.
33. Verify no TODO/placeholder implementation remains.
34. Verify no duplicate shared infrastructure was introduced.
35. Verify documentation matches the actual implementation.

Where device, simulator, native permission, cloud, map, notification, or external-provider validation cannot be performed, execute every repository-side validation that is possible and explicitly report what could not be validated.

Never claim a physical-device or production-provider test that did not occur.

---

# INTEGRATION CHECK

Before finalizing, verify that this driver implementation integrates cleanly with the shared mobile foundation and existing rider implementation.

Confirm that:

* driver authentication uses the shared session system
* driver API calls use the shared API client
* driver server state uses the shared query architecture
* driver realtime uses the shared websocket foundation
* driver location uses the shared location abstraction
* driver maps use the shared map abstraction
* driver notifications use the shared notification system
* driver deep links use the shared navigation architecture
* driver availability uses canonical backend contracts
* dispatch offers use the canonical dispatch contract
* assignment and trip actions use the canonical trip state machine
* active-trip events reconcile safely
* location updates do not create application-wide performance regressions
* uncertain offer/trip mutations use correct idempotency behavior
* app restart can recover active driver work
* logout clears driver-specific sensitive/query state
* rider and driver experiences can coexist without duplicating core infrastructure
* the final mobile volume can extend the driver journey with account, earnings, payouts, ratings, notifications, and other extended capabilities without rewriting this volume

The completed mobile application must remain one coherent production-grade architecture.

Do not introduce temporary architecture that requires a later rewrite.

---

# DEFINITION OF DONE

This volume is complete only when:

* driver home/workspace is implemented
* readiness/eligibility state is implemented
* availability/work-session controls are implemented
* location permission handling is implemented
* operational location behavior is implemented
* realtime driver connection is implemented
* dispatch offers are implemented
* offer presentation/expiration is implemented
* offer acceptance is implemented
* offer rejection is implemented
* offer concurrency/reconciliation is implemented
* assignment recovery is implemented
* assigned-trip workspace is implemented
* navigation to pickup is implemented
* arrival workflow is implemented
* rider communication is integrated where supported
* passenger pickup/start workflow is implemented
* active-trip workflow is implemented
* active-trip realtime is integrated
* cancellation/exception flow is implemented
* trip completion is implemented
* active-trip recovery is implemented
* safety entry points are integrated where supported
* trip-specific support entry points are integrated where supported
* scheduled assignments are implemented where supported
* operational push/deep-link handling is integrated
* offline/degraded-network handling is implemented
* accessibility requirements are addressed
* security/privacy requirements are addressed
* performance requirements are addressed
* meaningful tests are implemented
* documentation is updated
* validation has been executed
* actual limitations are honestly reported
* no fake dispatch, location, trip, or financial behavior is presented as real
* no placeholders remain
* no unrelated driver/account/earnings scope was introduced

---

# IMPLEMENTATION REPORT

At the end of execution, provide a concise report containing:

## Files Changed

List created, modified, and removed files.

## Implemented Scope

Summarize the driver workspace, readiness, availability, location, dispatch offers, assignment, pickup, active trip, messaging, cancellation, completion, recovery, scheduled assignment, and safety/support functionality actually implemented.

## Contracts Used

Identify the API, dispatch, trip-state, location, realtime, notification, deep-link, map, messaging, support, and safety contracts used.

## Validation

Report the exact validation commands executed and their results.

## Limitations

Report only actual environment, device, provider, or contract limitations.

## Follow-Up Dependencies

Identify genuine dependencies required by the final mobile volume.

Do not invent additional project phases.

---

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement the complete driver mobile core journey defined by this prompt.

Preserve all working behavior that is outside the scope of necessary changes.

Use the repository's actual architecture and contracts as the source of truth.

Do not wait for another prompt.

Do not merely describe the implementation.

Create and modify the real production-grade mobile code, tests, configuration, and documentation required for this scope.

Do not use pseudo-code, placeholders, fabricated APIs, fake offers, fake locations, fake assignments, fake trip transitions, fake earnings, or simulated success presented as real functionality.

Respect actual iOS, Android, Expo, permission, background-execution, lifecycle, connectivity, and location constraints.

Validate the implementation as thoroughly as the environment permits.

Finish only when this volume is genuinely implemented and integrated into the repository.
