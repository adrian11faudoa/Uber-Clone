# Uber-Style Global Ride-Hailing & Mobility Platform — Frontend Prompt — Volume 2

## ROLE

You are the senior frontend engineering organization responsible for implementing the production-grade rider core web experience of an original global ride-hailing and mobility platform.

Operate simultaneously as:

* Principal Software Architect
* Staff Frontend Engineer
* React/Next.js Engineer
* TypeScript Engineer
* UI/UX Engineer
* Realtime Systems Engineer
* Mapping/Geospatial UI Engineer
* Accessibility Engineer
* Performance Engineer
* Security Engineer
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

This milestone implements the core rider web journey:

* rider home
* current location
* pickup selection
* destination selection
* place search
* map interaction
* service/category selection
* fare estimate
* ride request
* dispatch waiting
* driver assignment
* driver arrival
* active trip
* cancellation
* trip completion
* realtime trip state
* reconnect/recovery
* errors and degraded states

This is the first complete customer-facing product workflow on the web.

The backend trip, dispatch, location, pricing, identity, and realtime contracts remain authoritative.

## Scale Targets

The platform is designed for:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* high realtime concurrency
* multi-region operation
* large authenticated user populations

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

Use the frontend foundation established in Frontend Volume 1.

# SOURCE OF TRUTH

The repository is the implementation source of truth.

Inspect the repository before making changes.

Use the architecture and backend contracts already present in the repository for:

* authentication
* rider identity
* trip creation
* pricing
* dispatch
* driver location
* trip lifecycle
* realtime
* cancellation
* errors
* idempotency
* pagination
* authorization

Do not depend on the previous AI conversation.

If existing rider functionality is already present:

1. inspect it
2. preserve working behavior
3. extend it rather than creating competing flows
4. document material inconsistencies

Do not redesign backend contracts to accommodate frontend convenience.

# FRONTEND EXECUTION MODEL

This milestone owns the rider-facing web experience from opening the ride-request experience through completion of the resulting trip.

The frontend must compose established backend capabilities rather than reimplementing them.

The rider flow must remain usable during:

* slow networks
* temporary API failures
* WebSocket disconnects
* duplicate user actions
* stale map data
* browser tab suspension
* backend state changes during UI interaction

# CURRENT IMPLEMENTATION SCOPE

## 1. Rider Route Structure

Implement the rider-facing routes/pages required for this milestone.

Establish clear boundaries for:

* rider home/ride request
* trip-request state
* active trip state
* completion state

Reuse the authenticated application shell from Frontend Volume 1.

Do not create a second authentication or layout system.

## 2. Rider Home

Implement the rider home experience.

It should provide the entry point for:

* requesting a ride
* determining current location
* selecting pickup
* selecting destination
* viewing relevant current trip state if one already exists

The page must behave correctly when:

* location permission is denied
* location cannot be determined
* the rider already has an active trip
* the API is temporarily unavailable

Do not display an actionable ride request form until the required backend/session state is ready.

## 3. Current Location

Integrate the browser geolocation foundation.

Support:

* permission request
* granted state
* denied state
* unavailable state
* loading state
* stale location
* manual fallback

Do not assume browser geolocation always succeeds.

Do not continuously request location when the current workflow does not need it.

## 4. Pickup Selection

Implement pickup selection using the established map/geography abstraction.

Support:

* current-location pickup
* map selection
* place search
* manual adjustment
* normalized address/place information

Show the rider what pickup location will be submitted.

Do not send arbitrary map-provider objects directly to the backend.

Normalize the selected location into the backend contract.

## 5. Destination Selection

Implement destination selection.

Support:

* place search
* map selection where appropriate
* address/place confirmation
* validation
* clear/reset behavior

Prevent submission when destination information is incomplete or invalid.

## 6. Place Search

Implement rider-facing place search through the established map/geocoding abstraction.

Support:

* debounced search
* cancellation of obsolete requests
* loading state
* empty state
* provider errors
* selection
* recent/search state only if supported by the existing architecture

Do not create direct provider-specific calls inside components.

## 7. Map Experience

Implement the rider map experience for this milestone.

Support:

* current location
* pickup marker
* destination marker
* appropriate map viewport
* selected-location interaction
* loading/error states

Keep the map component isolated from domain state where possible.

Do not place business logic inside the map rendering layer.

## 8. Location Privacy

Do not expose more geographic information than the rider needs.

Do not send precise location telemetry unnecessarily.

Do not store raw coordinates in client analytics events unless the architecture explicitly requires and protects them.

## 9. Service Category Selection

Implement the service/category selection UI using the backend's authoritative options.

Display:

* category
* relevant passenger/capacity information
* availability state where provided
* price estimate where available

Do not hard-code service categories that may change operationally.

## 10. Fare Estimate Request

Implement the rider fare-estimate flow.

Use the backend pricing API rather than calculating the authoritative fare locally.

Support:

* loading
* success
* validation error
* unavailable pricing
* retry
* stale response protection

When pickup/destination/category changes, ensure obsolete estimates cannot overwrite the latest request.

## 11. Fare Estimate Presentation

Present the authoritative backend estimate clearly.

Use the shared currency formatting foundation.

Show appropriate:

* estimated total
* currency
* relevant fare information
* pricing caveats defined by the contract
* promotion effects where already included by the backend

Do not invent fare calculations in the browser.

Do not display an estimate as a guaranteed final charge.

## 12. Ride Request Form

Implement the complete ride-request interaction.

Validate before submission:

* pickup
* destination
* service category
* quote/reference as required
* rider/session state

Use React Hook Form and Zod according to the frontend foundation.

## 13. Ride Request Submission

Submit the ride request using the backend trip contract.

The frontend must use the established idempotency mechanism.

Prevent accidental duplicate submissions caused by:

* double-click
* keyboard repetition
* slow response
* browser retry

Do not disable all navigation unnecessarily while a request is pending.

## 14. Request State Transition

After successful ride creation, transition the UI into the authoritative trip state.

Do not infer trip state solely from the button action.

Use the returned backend trip record and subsequent realtime/query state.

## 15. Dispatch Waiting State

Implement the rider experience while the trip is dispatching.

Display:

* trip/request status
* pickup
* destination
* selected service
* appropriate loading/dispatch information
* cancellation action where permitted

Do not expose internal dispatch candidate information.

Do not reveal driver lists, candidate distances, or matching scores.

## 16. Driver Assignment State

When a driver is assigned, display the authoritative assignment information defined by the backend contract.

Potential information includes:

* driver identity/display information
* vehicle information
* relevant service category
* estimated arrival
* map representation

Do not fabricate driver information if the backend has not provided it.

## 17. Driver Location Presentation

Once authorized driver-location information becomes available, present it through the realtime/map abstraction.

Support:

* initial driver location
* updates
* stale state
* temporary update loss
* reconnect recovery

Do not assume every realtime location update arrives.

Avoid animating stale coordinates indefinitely as though they were current.

## 18. Driver Arrival

Implement the rider UI for the driver-arriving and driver-arrived states.

The UI should update from authoritative trip state.

Do not let local timers independently decide that the driver has arrived.

## 19. Active Trip

Implement the active-trip rider experience.

Support:

* active status
* driver information
* vehicle information
* map/location updates
* trip destination
* relevant trip controls
* connection status
* authoritative transition to completion

Keep the interface usable while realtime data temporarily disconnects.

## 20. Trip Cancellation

Implement rider cancellation according to the backend contract.

Before submission:

* verify current state
* obtain required confirmation
* show known fee information when the backend provides it
* prevent accidental duplicate cancellation

After submission, render the backend's authoritative result.

Do not compute or guess cancellation fees locally.

## 21. Cancellation Race Handling

Handle cases where the rider attempts cancellation while:

* driver accepts
* driver arrives
* trip starts
* trip completes
* dispatch fails

The UI must resolve according to the backend response rather than assuming local success.

## 22. Trip Completion

Detect completion through:

* realtime state
* authoritative query recovery
* route navigation/reload recovery

Do not assume that the last realtime message was received.

Transition into the completed-trip state using backend data.

## 23. Realtime Trip Subscription

Use the shared realtime infrastructure from Frontend Volume 1.

Subscribe only to channels/resources the rider is authorized to receive.

Do not create a page-local WebSocket connection.

## 24. Realtime Message Validation

Validate incoming trip updates.

Protect against:

* unknown versions
* stale versions
* duplicate messages
* unexpected state transitions
* unauthorized resource identifiers

A stale realtime event must not roll the UI backward.

## 25. Query and Realtime Coordination

Establish clear precedence between:

* server queries
* realtime events
* local UI state

Realtime events should update or invalidate query data appropriately.

When synchronization becomes uncertain, refetch authoritative state.

Do not build a second client-side trip state machine that can diverge from backend state.

## 26. Reconnect Recovery

When realtime disconnects:

* show appropriate connection state
* preserve usable trip information
* reconnect using bounded backoff
* resynchronize authoritative trip state
* restore driver-location updates where authorized

Do not force the rider to recreate the trip.

## 27. Browser Refresh Recovery

A full browser refresh during:

* dispatch
* driver assignment
* driver arrival
* active trip

must recover the current trip state from the backend.

Do not rely on in-memory Zustand state for trip authority.

## 28. Network Failure Handling

Differentiate:

* request failure
* realtime failure
* browser offline
* temporary backend outage

Provide contextual recovery actions.

Do not replace actionable failure states with an infinite spinner.

## 29. Query Cache Design

Use TanStack Query for:

* current active trip
* fare estimate
* service categories
* places where appropriate
* user-readable trip state

Apply appropriate stale times and invalidation.

Do not retain highly sensitive active-trip information indefinitely in the browser cache.

## 30. Mutation Recovery

For ride creation and cancellation:

* use idempotency
* display pending state
* preserve recovery context
* resolve ambiguous network outcomes by querying authoritative state

A request timeout must not automatically cause the frontend to create a second ride.

## 31. Active-Trip Guard

If the rider already has an active/dispatching trip, the home experience should navigate or recover into that trip rather than silently creating a second ride flow.

Do not make local state the source of truth for detecting active trips.

## 32. Browser Permissions

Integrate geolocation permission UX with the existing permission foundation.

Explain failures clearly and provide a manual-selection fallback where supported.

Do not continuously trigger browser permission dialogs.

## 33. Loading States

Provide appropriate loading states for:

* location determination
* place search
* map readiness
* service categories
* fare estimate
* ride request
* trip bootstrap
* driver information

Avoid blocking the entire page when only one component is loading.

## 34. Empty and Unavailable States

Handle:

* no place results
* no service category
* pricing unavailable
* temporary dispatch delay
* missing driver location
* unavailable map provider

Give the rider an understandable action or state explanation.

Do not expose raw infrastructure errors.

## 35. Error Recovery

Support contextual retry for:

* fare estimate
* place search
* trip retrieval
* realtime synchronization

For non-retryable errors, provide a clear terminal state.

## 36. Accessibility

Ensure the ride-request flow works with:

* keyboard navigation
* screen readers
* visible focus
* form error announcements
* accessible map-adjacent controls
* non-color-only status communication

Map interactions must not be the only way to complete critical actions.

## 37. Responsive Rider Experience

Optimize the rider flow for:

* desktop browser
* tablet
* mobile browser

On smaller screens:

* prioritize pickup/destination controls
* preserve essential map context
* keep action buttons accessible
* avoid unusable fixed panels

Do not create a separate mobile web application.

## 38. Performance

Optimize the ride-request experience for:

* first load
* map loading
* search interaction
* fare-estimate response
* realtime updates
* rerenders

Avoid recreating map instances unnecessarily.

Do not rerender the entire page for every location update.

## 39. Location Update Rendering

Use efficient rendering strategies for moving driver markers.

Avoid causing:

* full-page state updates
* unnecessary query invalidation
* expensive React reconciliation for every GPS sample

Keep high-frequency visual updates isolated.

## 40. Product Telemetry

Add safe product analytics for meaningful rider-flow events such as:

* ride-request flow started
* pickup selected
* destination selected
* estimate viewed
* ride requested
* dispatch state reached
* driver assigned
* trip started
* trip completed
* rider cancellation

Telemetry must not contain:

* passwords
* tokens
* payment credentials
* private messages
* unnecessary precise coordinates

## 41. Error Telemetry

Capture useful rider-flow errors with:

* error category
* route
* operation
* environment
* request/correlation ID where safe

Do not transmit raw backend payloads containing sensitive information.

## 42. Security

Ensure:

* only authenticated riders can access the flow
* trip IDs are not sufficient for authorization
* user-visible driver information comes from authorized API responses
* unsafe URLs are rejected
* user-generated text is rendered safely

Do not introduce client-side authorization that contradicts the backend.

## 43. Browser Storage

Store only data that legitimately belongs in browser storage.

Do not persist:

* raw authentication secrets
* payment credentials
* private trip data indefinitely
* sensitive location history

Use appropriate expiration and cleanup.

## 44. Forms and Validation

Use shared form schemas for:

* pickup
* destination
* service selection
* ride request
* cancellation

Map backend validation errors into field-level errors where possible.

Do not duplicate complex pricing or dispatch rules in frontend schemas.

## 45. Testing

Create comprehensive tests for:

### Rider Request

* authenticated entry
* current location
* manual pickup
* destination
* service selection
* estimate
* request

### Errors

* location denied
* search failure
* pricing unavailable
* duplicate submission
* authorization failure
* backend timeout
* offline state

### Trip States

* dispatching
* assigned
* arriving
* arrived
* active
* completed
* cancelled
* expired where applicable

### Realtime

* connection
* update
* duplicate message
* stale message
* reconnect
* resynchronization

### Cancellation

* successful cancellation
* cancellation race
* duplicate cancellation
* cancellation unavailable

### Recovery

* browser refresh
* tab resume
* network loss
* API failure
* WebSocket failure

### Accessibility

* keyboard flow
* screen-reader labels
* form errors
* focus handling
* status announcements

### Performance

* location-update rendering behavior
* map mounting
* query cache behavior where practical

# DOCUMENTATION

Create or update frontend documentation covering:

* rider route structure
* ride-request state model
* pickup/destination selection
* maps
* fare estimates
* ride creation
* dispatch waiting
* driver assignment
* active trip
* cancellation
* realtime
* reconnect/recovery
* error handling
* accessibility
* responsive behavior
* telemetry
* testing

Documentation must describe actual implementation behavior.

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement:

* rider trip history
* rider profile/account management
* payment-method management
* receipts
* promotions management beyond displaying authoritative estimate data where explicitly required
* scheduled-trip management
* rating/review UI
* messaging UI beyond the shared realtime foundation
* driver web workflows
* support operations
* safety operations
* fleet operations
* analytics dashboards

Those belong to later frontend milestones.

Do not modify backend business logic merely for UI convenience.

Do not implement a second realtime system.

Do not build a second map-provider architecture.

Do not create a duplicate state-management system.

Do not create another rider-core frontend volume.

Do not create a surprise integration phase.

# REPOSITORY INSPECTION REQUIREMENTS

Before implementation:

1. Inspect Frontend Volume 1 implementation.
2. Inspect existing Next.js routing/layouts.
3. Inspect API client.
4. Inspect authentication/session handling.
5. Inspect TanStack Query conventions.
6. Inspect Zustand usage.
7. Inspect realtime client.
8. Inspect map abstraction.
9. Inspect date/time and currency utilities.
10. Inspect frontend design system.
11. Inspect backend trip APIs.
12. Inspect backend pricing APIs.
13. Inspect backend dispatch/realtime contracts.
14. Inspect location contracts.
15. Inspect tests.
16. Determine exactly which files require modification or creation.

Do not duplicate frontend foundations.

# IMPLEMENTATION RULES

## Preserve Existing Foundations

Reuse:

* application shell
* authentication
* authorization
* API client
* query architecture
* forms
* design system
* maps
* realtime
* telemetry
* testing

## Backend Authority

The backend remains authoritative for:

* trip state
* driver assignment
* pricing
* cancellation eligibility
* driver location
* authorization

## Client State Discipline

Do not recreate server truth in Zustand.

Use TanStack Query and realtime synchronization.

## Idempotency

Ride creation and cancellation must use the backend idempotency contract.

## Security

Never assume a client-visible route or control constitutes authorization.

## Realtime

Use one shared managed connection.

## Performance

Keep high-frequency location updates isolated from expensive page-wide rendering.

## Accessibility

Critical rider actions must remain available without requiring map gestures.

## No Placeholder Work

Every required rider workflow must be fully implemented.

# VALIDATION REQUIREMENTS

Execute all supported validation.

At minimum:

* TypeScript typecheck
* lint
* formatting
* production build
* unit/component tests
* API client/integration tests
* realtime tests
* accessibility tests
* responsive/UI tests where configured
* security/static analysis where configured

Test:

* location permission denial
* manual location fallback
* stale place-search responses
* fare-estimate race
* duplicate ride submission
* ambiguous ride-creation timeout
* active-trip recovery
* cancellation race
* WebSocket reconnect
* stale realtime event
* duplicate realtime event
* browser refresh
* browser offline
* driver-location update rendering
* unauthorized trip access
* safe rendering
* keyboard accessibility

Do not claim a build or test passed unless it actually executed successfully.

# FINAL INTEGRATION CHECK

Before declaring this milestone complete:

1. Verify rider routes use the shared application foundation.
2. Verify authenticated rider bootstrap works.
3. Verify current location handling supports permission denial and fallback.
4. Verify pickup and destination use the map/geography abstraction.
5. Verify obsolete place-search requests cannot overwrite newer state.
6. Verify service categories come from backend-authoritative data.
7. Verify fare estimates come from backend pricing.
8. Verify stale estimate responses cannot overwrite current selections.
9. Verify ride creation uses backend idempotency.
10. Verify duplicate submission cannot create duplicate trips.
11. Verify ambiguous request failures recover through authoritative state.
12. Verify dispatching state is backend-driven.
13. Verify driver assignment is backend-driven.
14. Verify driver location is only shown through authorized data.
15. Verify stale location does not appear indefinitely current.
16. Verify active trip survives browser refresh.
17. Verify realtime disconnect triggers recovery rather than trip loss.
18. Verify cancellation respects backend state and race outcomes.
19. Verify completion comes from authoritative trip state.
20. Verify query and realtime state remain coherent.
21. Verify high-frequency driver updates do not cause unnecessary page-wide rerenders.
22. Verify critical actions are accessible without map interaction.
23. Verify sensitive data is excluded from telemetry and browser storage.
24. Verify authorization errors are handled safely.
25. Verify tests cover normal, failure, race, reconnect, and accessibility scenarios.
26. Verify compatibility with Frontend Volume 1 and Backend Volumes 1–10.
27. Verify the repository is ready for Frontend Volume 3.
28. Verify no placeholder or duplicate implementation remains.

# DEFINITION OF DONE

This milestone is complete only when:

* rider routes exist
* rider home exists
* current-location workflow exists
* pickup selection exists
* destination selection exists
* place search exists
* map integration exists
* service category selection exists
* fare estimate flow exists
* fare estimate presentation exists
* ride-request form exists
* ride-request submission exists
* idempotent submission exists
* dispatch waiting state exists
* driver assignment state exists
* authorized driver-location display exists
* driver arrival state exists
* active-trip experience exists
* cancellation exists
* cancellation race handling exists
* trip completion exists
* realtime trip subscription exists
* realtime message validation exists
* query/realtime synchronization exists
* reconnect recovery exists
* browser refresh recovery exists
* network-failure handling exists
* active-trip protection exists
* loading/empty/error states exist
* accessibility is implemented
* responsive behavior is implemented
* performance protections exist
* telemetry exists
* security protections exist
* tests cover core and failure scenarios
* documentation is updated
* no rider account/financial/history scope outside this milestone has been implemented
* no driver/operations/mobile scope has been prematurely implemented
* no duplicate frontend foundation exists
* no placeholder implementation remains
* validation results are truthful
* the rider web core is ready for Frontend Volume 3

# IMPLEMENTATION REPORT

At completion, provide:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Rider Journey

Summarize:

* home
* location
* pickup
* destination
* service selection
* estimate
* ride request

## Trip Experience

Summarize:

* dispatch waiting
* assignment
* driver arrival
* active trip
* cancellation
* completion

## Maps and Realtime

Summarize:

* map integration
* location display
* WebSocket integration
* reconnect
* synchronization

## State and API

Summarize:

* TanStack Query usage
* mutations
* idempotency
* cache invalidation
* realtime/query coordination

## Security and Accessibility

Summarize:

* authorization
* safe rendering
* storage boundaries
* keyboard/screen-reader behavior

## Performance

Summarize:

* map optimization
* location-update rendering
* request cancellation
* code splitting/lazy loading where implemented

## Tests and Validation

List actual commands and actual outcomes.

## External Environment Limitations

State any backend, mapping, geolocation, or external service that could not be exercised.

Do not fabricate external-service execution.

## Architectural Decisions

Record meaningful rider-experience decisions.

## Known Limitations

List genuine remaining limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement Frontend Volume 2 completely.

Extend the shared frontend foundation from Volume 1 and consume the existing backend contracts for identity, trip, location, dispatch, pricing, and realtime.

Implement the complete rider web journey from pickup/destination selection through fare estimation, ride request, dispatch, driver assignment, arrival, active trip, cancellation, and completion.

The backend remains authoritative for trip state, pricing, dispatch, authorization, and driver location.

Do not implement rider account/history/payment management, driver workflows, operations workflows, or other later frontend domains.

Do not leave placeholders.

Run every validation command supported by the environment.

Verify idempotency, realtime recovery, race handling, accessibility, responsiveness, security, and performance.

Finish with the required implementation report and leave the repository in a coherent production-grade state ready for Frontend Volume 3.
