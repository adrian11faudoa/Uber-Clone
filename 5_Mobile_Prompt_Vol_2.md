# UBER-STYLE RIDE-HAILING PLATFORM — MOBILE PROMPT — VOLUME 2

## ROLE

You are the senior mobile engineering organization responsible for completing the production rider and driver applications for a globally scalable ride-hailing and mobility marketplace comparable in product depth and operational sophistication to Uber.

Operate as a coordinated team consisting of:

* Principal Software Architect
* Staff Mobile Engineer
* Mobile Platform Engineer
* UI/UX Engineer
* Security Engineer
* Performance Engineer
* Reliability Engineer
* QA Engineer
* Backend Integration Engineer
* Technical Writer

You are implementing production software against the existing repository.

You are not creating a tutorial, prototype, static screen collection, simulated ride application, or disconnected mobile experience.

Implement complete, connected, production-grade mobile functionality using the repository's established backend contracts, mobile foundation, security model, realtime architecture, and platform configuration.

The repository is the source of truth for what currently exists.

Do not assume that another AI prompt or previous conversation is available.

---

# PROJECT

Complete the production rider and driver mobile experiences for the Uber-style ride-hailing marketplace.

This volume is responsible for advanced rider and driver workflows beyond the mobile foundation, including:

* complete rider booking and trip experience
* scheduled rides
* promotions
* payment-method experiences
* receipts
* ratings
* rider trip history
* rider notifications
* rider support
* rider safety
* rider account/privacy controls
* complete driver onboarding
* compliance evidence workflows
* vehicle management
* driver availability
* dispatch offers
* driver navigation workflow
* pickup workflow
* rider verification
* active trip execution
* trip completion
* driver earnings
* payout visibility
* driver trip history
* driver notifications
* driver support
* driver safety
* operational status recovery
* background location hardening
* offline/reconnect behavior
* push notification flows
* deep-link flows
* accessibility
* performance
* mobile security
* comprehensive rider and driver testing

Use:

* React Native
* Expo
* TypeScript

and the existing repository libraries for networking, server state, local state, secure storage, realtime, analytics, and UI.

Do not invent incompatible backend contracts.

---

# SOURCE OF TRUTH

Before modifying code, inspect:

* rider mobile application
* driver mobile application
* shared mobile packages
* navigation
* authentication
* API client
* TanStack Query configuration
* local state
* secure storage
* push notifications
* deep links
* WebSockets
* location/background tasks
* maps/navigation
* booking
* trip state
* driver availability
* offers
* onboarding
* compliance
* vehicle management
* earnings
* payment methods
* ratings
* support
* safety
* mobile analytics
* crash reporting
* tests
* Expo/EAS configuration
* iOS configuration
* Android configuration
* backend API contracts
* backend realtime contracts
* backend event semantics

Preserve compatible implementation.

Do not create parallel mobile foundations.

Do not regenerate unchanged files.

---

# MOBILE SCOPE

This volume owns the advanced functional mobile experience for both clients.

## RIDER

Implement:

* full booking flow
* saved/current locations where supported
* ride-product selection
* fare quote
* promotion application
* payment-method selection
* ride creation
* dispatch waiting
* driver assignment
* driver tracking
* trip verification
* active trip
* cancellation
* trip completion
* receipt
* rating
* trip history
* scheduled rides
* notifications
* support
* safety
* trusted contacts/trip sharing where supported
* privacy/account controls

## DRIVER

Implement:

* onboarding
* profile
* compliance
* document/evidence workflow
* vehicle management
* availability
* ride offers
* dispatch response
* navigation workflow
* arrival
* rider verification
* trip start
* active trip
* completion
* cancellation
* earnings
* payout visibility
* trip history
* notifications
* support
* safety
* operational recovery

---

# SHARED MOBILE CONTRACT PRINCIPLES

The mobile applications must remain thin clients of authoritative backend state.

Never make mobile state authoritative for:

* ride assignment
* trip lifecycle
* pricing
* payment
* compliance approval
* driver eligibility
* earnings
* payouts

Use local state only to improve interaction and rendering.

After:

* app restart
* reconnect
* background resume
* network restoration
* push notification
* deep-link navigation

reconcile with the backend.

---

# RIDER BOOKING EXPERIENCE

Complete the rider booking experience.

The workflow must support:

1. Open booking.
2. Resolve pickup.
3. Resolve destination.
4. Select ride product.
5. Request estimate.
6. Select promotion if eligible.
7. Select payment method if required.
8. Confirm booking.
9. Create idempotent ride request.
10. Observe dispatch.
11. Receive driver assignment.
12. Transition to active trip.

Each state requires:

* loading
* success
* validation failure
* conflict
* network failure
* retry/recovery

---

# LOCATION SELECTION

Support:

* current location
* address search
* map selection
* pickup editing
* destination editing
* recent/saved locations where backend supports them

Do not store private location history indefinitely on-device.

If recent locations are persisted locally, classify their sensitivity and provide appropriate clearing behavior.

---

# SAVED LOCATIONS

Where backend support exists, allow riders to manage saved locations such as:

* home
* work
* custom saved place

Each saved location must remain tied to the authenticated account.

Do not trust locally stored saved-location IDs without backend validation.

---

# RIDE PRODUCT PRESENTATION

Display server-provided:

* product name
* description
* capacity
* ETA
* estimated price
* applicable features
* availability

Do not determine eligibility locally.

When product availability changes while booking is open:

* refresh
* invalidate stale state
* require the rider to select a currently valid option

---

# FARE ESTIMATE

Display:

* estimated fare
* currency
* estimate expiration where provided
* applicable fees
* discount
* estimated travel time
* route distance where appropriate

Clearly distinguish estimate from final fare.

Do not silently reuse expired quotes.

---

# PROMOTION APPLICATION

Support:

* eligible promotions
* code entry where applicable
* promotion selection
* removal
* server recalculation
* expired promotion handling
* ineligible promotion errors

Do not calculate the final promotion discount locally.

Use the backend's authoritative quote.

---

# PAYMENT METHOD SELECTION

Allow riders to select an authorized payment method.

Display only safe provider metadata such as:

* brand
* last four digits where provided
* expiration status where appropriate
* default status

Never display raw payment credentials.

If provider-hosted/tokenized UI exists, use it rather than collecting sensitive credentials unnecessarily.

---

# RIDE REQUEST CONFIRMATION

The confirmation screen must clearly show:

* pickup
* destination
* ride product
* estimate
* selected promotion
* payment method
* relevant scheduling information

Before submission, validate the latest known quote state.

Do not let the client modify:

* fare
* currency
* pricing version
* dynamic pricing multiplier

---

# RIDE CREATION

Implement an idempotent ride-creation mutation.

The client must generate/use the backend-supported operation identifier.

Disable duplicate manual submissions while a request is pending, but do not rely on UI disabling for correctness.

If the network fails after submission:

* preserve the operation identifier
* query authoritative ride state
* determine whether the request exists
* retry only when safe

---

# DISPATCH EXPERIENCE

After ride creation, show states such as:

* requested
* searching
* matching
* driver assigned
* no driver
* canceled
* error requiring user action

Do not animate a fake search process independently of backend state.

The user must be able to recover after app restart.

---

# DRIVER ASSIGNMENT

Once a driver is assigned, display:

* driver name
* rating where permitted
* photo where permitted
* vehicle
* vehicle identifier
* ETA
* pickup
* contact/safety actions where supported

Do not expose unrelated private driver data.

---

# DRIVER LOCATION

Display live driver location only while the rider is authorized to receive it.

Handle:

* fresh
* stale
* missing
* delayed
* reconnecting

Do not present a stale location as though it were current.

Use visual indicators where appropriate without making exact positioning the only way to understand the trip.

---

# DRIVER LOCATION ANIMATION

Decouple:

* incoming location frequency
* rendered animation frequency

Interpolate or smooth only for presentation.

Never alter the authoritative latest location merely to make animation smoother.

When a newer server location arrives, reconcile the visual marker safely.

---

# ACTIVE TRIP UX

Implement the complete rider active-trip interface.

Support:

* driver en route
* driver arrived
* trip verification
* trip started
* trip in progress
* route
* ETA
* destination
* safety
* support
* cancellation where permitted
* completion

The interface must adapt to orientation and screen-size differences.

---

# TRIP VERIFICATION

Where the backend uses a PIN, code, or equivalent:

* display the verification requirement
* provide accessible input
* validate locally for format
* submit to backend
* show server result
* handle expiration/invalidity
* avoid exposing verification secrets in logs or analytics

Do not locally mark the trip started after input acceptance.

---

# CANCELLATION

Implement rider cancellation based on backend eligibility.

Show:

* current cancellation eligibility
* reason options
* fee information where provided
* confirmation
* processing
* success
* conflict

When a cancellation loses a race against another trip transition:

* refresh authoritative state
* explain the resulting state
* do not leave the UI in an impossible hybrid state

---

# TRIP COMPLETION

On authoritative completion:

* stop driver-location rendering
* retrieve final fare
* retrieve payment outcome
* show receipt
* offer rating
* preserve trip-history availability

Do not infer completion from elapsed time.

---

# RECEIPT UX

Display:

* trip date/time
* pickup
* destination
* ride product
* fare
* discounts
* fees
* payment method summary
* payment status
* refund state where applicable

Amounts must be formatted using backend-provided currency and exact values.

---

# RIDER TRIP HISTORY

Implement paginated history.

Support:

* date filters
* status
* trip product
* trip detail
* receipt
* rating state
* support access

Never request an unbounded historical dataset.

---

# RATING

Implement rider rating flow after eligible completed trips.

Support:

* rating
* optional review
* submission
* loading
* success
* duplicate
* already-rated state
* server validation errors

Do not allow rating an arbitrary driver from a generic profile page unless the backend explicitly provides an authorized relationship.

---

# SCHEDULED RIDES

Implement complete rider scheduled-ride functionality where supported.

Support:

* date/time selection
* timezone presentation
* pickup
* destination
* ride product
* estimate/quote
* promotion
* payment method
* confirmation
* detail
* modification where backend permits
* cancellation

Clearly show that scheduled rides are not necessarily driver-assigned yet.

---

# SCHEDULED-RIDE RECOVERY

After app restart or notification tap:

* fetch authoritative scheduled-ride state
* determine next lifecycle
* display appropriate navigation

Do not trust local scheduled timers.

---

# PAYMENT HISTORY

Provide rider-facing payment history where backend supports it.

Support:

* payment state
* amount
* currency
* trip reference
* refunds
* receipt access

Do not expose provider internal data unless intentionally returned.

---

# REFUND EXPERIENCE

Where users are permitted to request or view refunds:

* explain status
* display amount
* display reason/category where appropriate
* show pending/success/failure
* link to support where required

Refund execution remains backend-authoritative.

---

# NOTIFICATIONS

Complete push and in-app notifications.

Support:

* ride status
* driver assignment
* driver arrival
* trip completion
* payment status
* support updates
* safety messages
* scheduled-ride reminders

Notification payloads must not be treated as authoritative.

On notification open:

1. validate authentication
2. validate destination
3. fetch authoritative data
4. navigate

---

# RIDER SUPPORT

Implement production support flows.

Support:

* trip-specific support
* payment issue
* driver issue
* safety issue
* general support
* case history
* case status
* secure messaging where backend supports it

Do not expose internal support notes to riders.

---

# RIDER SAFETY

Implement accessible safety tools.

Depending on backend capabilities:

* emergency action
* trusted contacts
* trip sharing
* safety incident
* safety information

Safety actions must remain available during active trip states.

---

# TRUSTED CONTACTS

Support:

* add contact
* edit
* remove
* verify
* enable/disable

Validate ownership through backend APIs.

Protect contact data in local persistence and analytics.

---

# TRIP SHARING

Support secure trip sharing.

Display:

* active share
* expiration
* revoke where available

When opening a shared trip:

* validate the share state through backend
* do not treat the URL/token alone as proof of identity

---

# DRIVER HOME

Implement the driver home experience.

Display:

* online/offline state
* eligibility
* current market/service area
* connection
* location permission
* relevant operational alerts
* current earnings summary where appropriate

The online control must reflect authoritative backend state.

---

# DRIVER AVAILABILITY

When driver goes online:

1. verify local required permissions
2. verify network
3. submit backend availability command
4. receive authoritative result
5. begin appropriate realtime/location services
6. display current state

When going offline:

1. submit backend command
2. receive confirmation
3. stop unnecessary location transmission
4. stop offer subscriptions where appropriate
5. update local state

Do not leave the driver appearing online after a failed offline/online command.

---

# DRIVER ONBOARDING

Complete the driver onboarding workflow.

Support:

* personal information
* profile completion
* required compliance items
* document capture/upload
* review state
* rejection/retry
* approval
* expiration
* suspension

The interface must clearly communicate what is blocking eligibility.

---

# DOCUMENT CAPTURE

Where camera/document capture is supported:

* request permission only when required
* guide framing/orientation
* validate file type and size
* preview before submission
* allow retake
* securely upload through backend-authorized flow
* clear temporary files appropriately

Do not retain compliance documents indefinitely in application storage.

---

# VEHICLE MANAGEMENT

Support:

* vehicle list
* add vehicle
* edit vehicle
* activate/deactivate
* compliance status
* eligibility
* supported ride products

The backend remains authoritative for eligibility.

---

# DRIVER ELIGIBILITY

Show distinct states:

* account active
* onboarding incomplete
* compliance pending
* compliance approved
* vehicle ineligible
* temporarily restricted
* eligible to drive

Do not display a generic green "online" state when the backend says the driver is ineligible.

---

# DRIVER OFFERS

Implement offer handling.

Display:

* pickup
* estimated distance/time
* ride product
* applicable information
* offer expiration
* safe relevant rider context

Do not reveal unnecessary rider information.

---

# OFFER COUNTDOWN

A countdown is presentation only.

Use backend expiration as authority.

At the moment of acceptance:

* send server command
* handle expired response
* refresh current offer state

Do not extend offers locally.

---

# DRIVER OFFER NOTIFICATION

Offer presentation must remain reliable when:

* app is foregrounded
* app resumes
* push wakes the app
* WebSocket reconnects

A notification must still require authoritative offer retrieval before acceptance.

---

# DRIVER ACCEPTANCE

Implement:

* accept
* reject
* expiration
* conflict
* network timeout
* duplicate submit

After success:

* transition to active assigned-trip state
* stop presenting the offer
* begin appropriate navigation/location behavior

---

# DRIVER NAVIGATION

Integrate external or embedded navigation according to repository architecture.

Support:

* pickup navigation
* destination navigation
* return to app
* destination updates where supported

Use authoritative backend destination data.

Do not embed private rider details into external navigation URLs unnecessarily.

---

# PICKUP WORKFLOW

Implement:

* driver en route
* proximity/status
* arrived
* rider verification
* start trip

Where backend supports geofenced arrival, the mobile UI should use backend state rather than claiming arrival purely from GPS calculations.

---

# RIDER VERIFICATION

If a trip PIN/code is used:

* present verification UI
* capture safely
* validate format
* submit backend command
* handle invalid/expired
* do not expose it in screenshots/analytics/logs

---

# ACTIVE DRIVER TRIP

Implement complete driver active-trip experience.

Support:

* rider-safe identity information
* pickup/destination
* route
* current trip state
* navigation
* rider verification
* trip start
* active trip
* completion
* cancellation where permitted
* safety
* support

---

# DRIVER TRIP COMPLETION

On completion:

* send authoritative command
* wait for server state
* retrieve final trip/fare state
* display earnings impact where available
* return to eligible/available state only after backend confirmation

Do not locally toggle online state without the backend.

---

# DRIVER CANCELLATION

Support driver cancellation only in backend-permitted states.

Show:

* reason
* confirmation
* processing
* result
* impact information returned by backend where applicable

Do not hardcode cancellation rules that differ across markets.

---

# DRIVER EARNINGS

Implement:

* earnings summary
* daily/weekly views where backend supports them
* earnings by trip
* adjustments
* payout status

Use paginated backend data.

Do not calculate official earnings from local trip information.

---

# PAYOUTS

Display:

* payout status
* payout amount
* destination/account summary where safe
* submitted/paid/failed
* reconciliation issues where appropriate

Do not expose provider secrets or full payout-account credentials.

---

# DRIVER TRIP HISTORY

Support:

* date range
* trip detail
* earnings
* cancellation state
* ratings where permitted

Use server pagination.

---

# DRIVER NOTIFICATIONS

Handle:

* new offers
* driver eligibility changes
* compliance updates
* payout updates
* support updates
* safety notifications
* operational alerts

Offer notifications must route through authoritative offer retrieval.

---

# DRIVER SUPPORT

Provide:

* active-trip support
* ride issue
* payout issue
* compliance issue
* vehicle issue
* account issue
* safety issue

Support cases remain backend-authoritative.

---

# DRIVER SAFETY

Provide driver access to:

* emergency tools
* safety incident reporting
* trip safety information
* trusted mechanisms where supported

Keep safety controls accessible while driving without encouraging unsafe interaction patterns.

---

# DRIVING SAFETY UX

Avoid interfaces that demand prolonged typing or attention while a vehicle may be moving.

Use:

* large touch targets
* concise controls
* voice/system capabilities where intentionally supported
* confirmation for critical actions
* minimal text entry during active driving

Do not make unsafe driver interaction a requirement for ordinary trip operation.

---

# BACKGROUND LOCATION

Harden production background location.

The driver app must:

* start background location only when operationally necessary
* stop it when driver is offline
* stop it on logout
* handle permission changes
* handle OS task termination
* recover after process restart
* avoid duplicate background tasks
* respect platform battery policies

---

# LOCATION DELIVERY

Implement resilient driver location submission.

Handle:

* online
* temporary offline
* reconnect
* duplicate samples
* stale samples
* server rejection
* permission changes

Bound the local pending location set.

Prefer newer samples when older ones become obsolete.

Never fabricate location points.

---

# LOCATION PRIVACY

Do not show rider/driver location history outside authorized workflows.

Do not store exact locations in analytics unless required and approved.

Protect location-derived telemetry.

---

# OFFLINE RECOVERY

Driver workflows must be safe during temporary offline periods.

When offline:

* display clear state
* preserve safe trip context
* stop unsafe commands
* maintain bounded location recovery
* reconnect automatically
* reconcile trip/availability state

Do not continue presenting the driver as authoritative online if the backend state cannot be confirmed for an extended period.

---

# APP RESUME

On foreground/resume, refresh:

* authentication
* active ride/trip
* driver availability
* active offer
* location permission
* push registration
* time-sensitive data

Do not trust elapsed client time for offer/trip state.

---

# PUSH NOTIFICATION DE-DUPLICATION

The same backend event may arrive through:

* WebSocket
* push
* API refresh

The app must avoid presenting multiple contradictory UI transitions.

Use server identifiers/versioning to reconcile.

---

# MOBILE STATE SYNCHRONIZATION

For important server entities maintain:

* query data
* latest event/version where useful
* invalidation rules

When a mutation completes:

* update or invalidate server state
* do not leave stale cached data visible indefinitely

---

# CACHE INVALIDATION

Invalidate relevant queries after:

* ride creation
* cancellation
* trip transition
* payment change
* rating
* support creation
* vehicle update
* compliance submission
* availability change
* payout action

Use targeted invalidation rather than clearing the entire cache on every mutation.

---

# ACCOUNT SWITCHING AND LOGOUT

Rider and driver applications must completely isolate account state.

On logout:

* unregister/disable push where appropriate
* stop driver location
* disconnect WebSocket
* clear sensitive query data
* clear local state
* clear navigation
* clear account-specific deep-link context

Do not leave one account's active trip visible after another user signs in.

---

# MOBILE ACCESSIBILITY

Complete accessibility for:

* rider booking
* scheduled ride
* active trip
* rating
* support
* safety
* driver availability
* offer
* compliance
* vehicle management
* earnings
* payout
* navigation

Support:

* screen readers
* dynamic type
* large text
* touch targets
* semantic state
* reduced motion
* non-color status indicators

---

# INTERNATIONALIZATION

Use translation-ready structures.

Support:

* string catalogs
* pluralization
* date formatting
* currency
* locale
* timezone

Avoid embedding English strings directly inside logic.

---

# PERFORMANCE

Optimize production mobile performance.

Focus on:

* startup
* map rendering
* location updates
* WebSocket events
* navigation transitions
* list virtualization
* image loading
* memory
* battery
* network usage

Do not perform full application renders for every location update.

---

# MAP PERFORMANCE

Use map references and marker updates efficiently.

Avoid:

* rebuilding full map state for every GPS sample
* rendering unnecessary polylines
* loading unbounded route history
* retaining completed trip map state indefinitely

---

# LIST PERFORMANCE

Use appropriate list primitives and pagination for:

* ride history
* notifications
* earnings
* support cases
* payout history
* saved locations

Do not render unbounded arrays.

---

# IMAGE PERFORMANCE

Use:

* correct image sizing
* caching where appropriate
* placeholders
* memory-conscious loading

Do not retain high-resolution document images after compliance submission unless required.

---

# SECURITY REVIEW

Review:

* secure storage
* deep links
* push payloads
* screen previews
* screenshots
* logs
* analytics
* clipboard
* external URLs
* document files
* location permissions
* session handling
* account switching

Fix issues discovered within scope.

---

# TESTING REQUIREMENTS

Write comprehensive tests.

## RIDER

Test:

* booking
* promotions
* payment selection
* scheduling
* dispatch
* driver tracking
* verification
* active trip
* cancellation
* completion
* receipt
* rating
* history
* notifications
* support
* safety
* privacy

## DRIVER

Test:

* onboarding
* compliance
* document upload
* vehicle
* eligibility
* availability
* offer
* acceptance
* rejection
* expiration
* navigation state
* arrival
* verification
* trip start
* active trip
* completion
* cancellation
* earnings
* payouts
* support
* safety

---

# CONCURRENCY AND RECOVERY TESTING

Test mobile behavior for:

* double tap on ride creation
* double tap on accept
* repeated trip transition
* app kill after command submission
* network loss during mutation
* push + WebSocket duplicate
* stale notification
* app restart during active trip
* account logout during location tracking

The tests must validate reconciliation with authoritative backend state.

---

# BACKGROUND TESTING

Driver application must be tested under:

* foreground
* background
* locked screen
* app suspension
* app termination
* network loss
* network recovery
* permission downgrade
* permission revocation
* device battery constraints

---

# PUSH TESTING

Test:

* token registration
* token refresh
* logout/unregistration
* foreground notifications
* background notifications
* tap handling
* deep links
* duplicate delivery
* invalid/stale destinations

---

# END-TO-END TESTING

Provide E2E coverage for:

## RIDER

1. Authenticate.
2. Book ride.
3. Receive assignment.
4. Track driver.
5. Verify/start.
6. Complete.
7. View receipt.
8. Rate.
9. View history.

## DRIVER

1. Authenticate.
2. Complete onboarding.
3. Go online.
4. Receive offer.
5. Accept.
6. Navigate to pickup.
7. Arrive.
8. Verify rider.
9. Start.
10. Complete.
11. View earnings.

---

# DEVICE MATRIX

Validate representative:

* current supported iOS versions
* current supported Android versions
* small-screen phones
* large-screen phones
* poor network
* background location
* notification permissions
* high-text-size accessibility settings

Use actual physical devices for critical location/background workflows where practical.

---

# BUILD AND RELEASE

Validate:

* development build
* test/staging build
* production build

Verify:

* app identifiers
* signing
* push configuration
* deep links
* permissions
* environment variables
* OTA/update strategy where used
* release metadata

Never commit:

* signing credentials
* private provisioning credentials
* secret provider keys

---

# CRASH AND TELEMETRY REVIEW

Crash/telemetry systems must redact:

* authentication tokens
* payment credentials
* compliance documents
* safety content
* private support data
* exact unnecessary location

Include useful metadata:

* platform
* app version
* build
* feature
* sanitized session reference
* lifecycle state

---

# DOCUMENTATION

Update mobile documentation for:

* rider workflows
* driver workflows
* scheduling
* promotions
* payment UI
* compliance
* background location
* navigation
* earnings
* payouts
* safety
* support
* testing
* device requirements
* release configuration
* troubleshooting

Documentation must reflect actual implementation.

---

# IMPLEMENTATION DISCIPLINE

Before modifying files:

1. Inspect the repository.
2. Map existing mobile foundation to advanced workflows.
3. Preserve compatible infrastructure.
4. Complete rider functionality.
5. Complete driver functionality.
6. Integrate payments/earnings/payouts.
7. Integrate support/safety.
8. Integrate scheduling/promotions.
9. Harden background location.
10. Harden realtime and push synchronization.
11. Implement recovery behavior.
12. Complete accessibility.
13. Add tests.
14. Validate physical-device scenarios.
15. Validate builds.
16. Review security/privacy/performance.
17. Update documentation.
18. Produce the required completion report.

Do not rewrite unrelated mobile architecture.

---

# PRODUCTION COMPLETENESS

Never leave:

* fake offers
* fake driver locations
* fake earnings
* hardcoded fares
* simulated compliance
* mock payout status
* disconnected support
* placeholder scheduling
* fake push workflows
* fake trip states
* TODO/FIXME implementation gaps
* pseudo-code

Every advanced workflow must connect to the actual backend contract.

---

# PROHIBITED PRACTICES

Never:

* trust local trip state
* trust local driver eligibility
* trust push payloads as truth
* extend offer expiration locally
* submit duplicate financial/trip commands without idempotency
* expose sensitive rider/driver data unnecessarily
* store raw payment credentials
* store compliance documents indefinitely
* leave background location active after logout/offline state
* maintain unbounded offline location
* bypass backend authorization through deep links
* log tokens or sensitive document contents
* send precise unnecessary location to analytics
* silently suppress backend conflicts

---

# IMPLEMENTATION BOUNDARIES

This volume completes the advanced rider and driver mobile application experiences.

It must extend the mobile foundation without introducing:

* another navigation system
* another authentication system
* another API client
* another realtime implementation
* another state-management system
* another location pipeline
* another push notification architecture

Do not implement web applications.

Do not implement backend services.

Do not implement cloud infrastructure.

---

# REQUIRED IMPLEMENTATION DELIVERABLES

Implement or update:

## RIDER

* booking
* promotions
* payments
* scheduled rides
* active trips
* receipts
* ratings
* history
* notifications
* support
* safety
* privacy

## DRIVER

* onboarding
* compliance
* documents
* vehicle
* eligibility
* availability
* offers
* navigation
* pickup
* verification
* active trip
* earnings
* payouts
* history
* notifications
* support
* safety

## SHARED

* synchronization
* push
* deep links
* lifecycle
* offline/reconnect
* security
* accessibility
* performance
* testing

---

# REQUIRED RUNTIME VALIDATION

Verify:

* rider end-to-end journey
* rider scheduled ride
* rider payment/receipt
* rider notification
* rider support
* rider safety
* driver onboarding
* driver document flow
* driver eligibility
* driver availability
* driver offer
* driver acceptance
* pickup
* verification
* active trip
* completion
* earnings
* payout state
* push
* deep links
* offline recovery
* app restart
* background location
* logout

Verify all critical workflows recover through authoritative backend state after interruption.

---

# COMPLETION REPORT REQUIREMENTS

When implementation is complete, report:

## FILES CREATED

List every new file.

## FILES MODIFIED

List every modified file.

## RIDER

Report:

* booking
* promotions
* payments
* scheduled rides
* trips
* receipts
* ratings
* history
* notifications
* support
* safety
* privacy

## DRIVER

Report:

* onboarding
* compliance
* documents
* vehicle
* availability
* offers
* navigation
* pickup
* active trip
* earnings
* payouts
* history
* support
* safety

## SHARED PLATFORM

Report:

* push
* deep links
* lifecycle
* offline/reconnect
* synchronization
* secure storage
* analytics
* crash reporting

## SECURITY

Report:

* credentials
* deep links
* permissions
* location
* sensitive files
* telemetry
* account isolation

## ACCESSIBILITY

Report:

* screen readers
* dynamic text
* touch targets
* reduced motion
* status semantics

## PERFORMANCE

Report:

* startup
* rendering
* maps
* location
* WebSockets
* memory
* battery
* network optimization

## TESTS

List tests added or modified and the behaviors they verify.

## DEVICE VALIDATION

Report:

* iOS testing
* Android testing
* background/foreground
* location
* push
* poor network
* account switching

## BUILD VALIDATION

Report:

* TypeScript
* lint
* unit tests
* integration tests
* E2E tests
* Expo/EAS validation
* iOS build
* Android build
* runtime smoke tests

## COMPATIBILITY

Identify:

* backend API compatibility
* WebSocket compatibility
* notification compatibility
* mobile platform implications

## UNRESOLVED ISSUES

List only genuine remaining issues.

Do not claim mobile completion if critical rider or driver workflows remain disconnected, insecure, untested, or dependent on fake behavior.

---

# FINAL ENGINEERING PRINCIPLE

The rider and driver mobile applications must operate as resilient production clients of one authoritative ride-hailing platform.

Rider and driver experiences must remain distinct while sharing only infrastructure that is genuinely common.

Critical functionality must remain correct through:

* app restarts
* background execution
* foreground transitions
* poor connectivity
* duplicate notifications
* WebSocket interruptions
* stale local state
* permission changes
* worker-side state changes
* server-side conflicts

The driver application must prioritize:

* location reliability
* battery efficiency
* safe interaction
* offer correctness
* trip-state correctness

The rider application must prioritize:

* booking correctness
* transparent state
* realtime resilience
* payment clarity
* safety
* accessibility

The backend remains authoritative for all business-critical state.

The repository remains the implementation source of truth.

All subsequent infrastructure work must support these mobile requirements without introducing alternate authentication, API, realtime, notification, or location architectures.
