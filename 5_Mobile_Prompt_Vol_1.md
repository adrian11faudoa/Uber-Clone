# UBER-STYLE RIDE-HAILING PLATFORM — MOBILE PROMPT — VOLUME 1

## ROLE

You are the senior mobile engineering organization responsible for implementing the production mobile applications for a globally scalable ride-hailing and mobility marketplace comparable in product depth and operational sophistication to Uber.

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

You are not creating a tutorial, prototype, simulated ride application, static mobile mockup, or simplified demonstration.

Implement complete, connected, production-grade mobile functionality using the existing backend contracts, authentication architecture, realtime architecture, and repository conventions.

The repository is the source of truth for what currently exists.

Do not assume that another AI prompt or previous conversation is available.

---

# PROJECT

Implement the production mobile platform for an Uber-style ride-hailing marketplace using:

* React Native
* Expo
* TypeScript

The platform must provide two distinct first-class mobile applications:

* rider application
* driver application

Both applications must consume the same production backend while maintaining clearly separated product experiences, permissions, navigation, state, and device capabilities.

The mobile platform must support:

* authentication
* secure credential/session handling
* rider booking
* driver onboarding
* vehicle management
* driver availability
* high-frequency driver location
* ride dispatch
* realtime offers
* active trips
* navigation-supporting flows
* push notifications
* deep links
* offline/reconnect handling
* trip lifecycle
* payments and receipts where applicable
* earnings
* safety
* support
* ratings
* performance
* accessibility
* app lifecycle management
* iOS requirements
* Android requirements
* production release configuration
* automated testing

Do not invent incompatible APIs.

Do not put authoritative business logic in the mobile applications.

---

# SOURCE OF TRUTH

Before changing code:

Inspect the repository thoroughly.

Determine:

* mobile workspace/application structure
* Expo configuration
* existing React Native screens
* navigation architecture
* shared mobile components
* authentication implementation
* secure storage
* API client
* TanStack Query setup
* Zustand or equivalent client state
* WebSocket client
* push notification implementation
* deep-link configuration
* location services
* map integration
* permission handling
* background tasks
* app lifecycle handling
* rider/driver separation
* existing mobile tests
* TypeScript configuration
* build configuration
* environment configuration
* backend API contracts
* backend realtime contracts
* notification contracts
* existing web/mobile shared packages

Preserve compatible implementation.

Do not create parallel:

* authentication systems
* API clients
* WebSocket clients
* design systems
* state-management layers
* notification abstractions

unless the repository does not already provide an appropriate production foundation.

Do not regenerate unchanged files.

---

# MOBILE SCOPE

This volume is responsible for the shared production mobile foundation and the core rider and driver application foundations.

Implement:

* mobile workspace architecture
* rider/driver application separation
* navigation
* authentication
* secure session handling
* API integration
* server-state management
* local-state management
* push notifications foundation
* deep-link foundation
* device permissions
* app lifecycle
* connectivity detection
* WebSocket foundation
* shared error handling
* shared design primitives
* rider booking foundation
* rider active-trip foundation
* driver onboarding foundation
* driver availability foundation
* driver location foundation
* driver realtime offer foundation
* mobile observability
* security controls
* accessibility foundation
* automated testing
* iOS/Android configuration foundations

Do not attempt to implement every advanced rider/driver workflow in one volume.

This volume must establish stable mobile architecture for later mobile functionality.

---

# MOBILE ARCHITECTURE

Use a maintainable architecture that separates:

* application bootstrap
* navigation
* screens
* feature modules
* shared UI
* API clients
* server state
* local state
* secure storage
* realtime
* device services
* permissions
* background services
* analytics
* error handling

Keep rider and driver application experiences separate at the product layer while reusing safe shared infrastructure.

Do not place all state in one global store.

Use TanStack Query for backend-owned server state.

Use Zustand only for local cross-screen state where justified.

---

# APPLICATION STRUCTURE

If the repository uses:

* one Expo workspace with separate rider/driver entry points
* two Expo applications
* a monorepo with shared packages

preserve the established architecture.

Shared libraries may contain:

* API client primitives
* authentication primitives
* UI primitives
* validation
* telemetry
* networking
* shared domain types

Do not place rider-specific business behavior into a generic shared package merely to reduce file count.

---

# NAVIGATION

Implement secure, lifecycle-aware navigation.

Rider navigation should support appropriate areas for:

* home
* booking
* active ride
* ride history
* account
* payments
* notifications
* support
* safety

Driver navigation should support appropriate areas for:

* home/availability
* active offer
* active trip
* earnings
* vehicle
* onboarding/compliance
* notifications
* support
* safety
* account

Protected navigation must reflect authentication state and server-authoritative account state.

Do not allow a disabled or suspended account to remain operational merely because a screen was already mounted.

---

# NAVIGATION STATE RECOVERY

Support app restart at any point.

Examples:

* rider restarts while matching
* rider restarts during active trip
* driver restarts while online
* driver restarts after receiving an offer
* driver restarts during active trip

After startup:

1. restore secure session if valid
2. obtain authoritative server state
3. reconstruct only necessary client UI state
4. restore appropriate navigation
5. reconnect realtime
6. reconcile missed events

Do not blindly restore stale local navigation state.

---

# AUTHENTICATION

Implement mobile authentication using the repository's backend contract.

Support:

* registration
* login
* logout
* session restoration
* token refresh where applicable
* session expiration
* account recovery where supported
* account restriction/suspension handling

Do not duplicate authentication business rules in the mobile clients.

---

# SECURE STORAGE

Store sensitive credentials only through an appropriate secure platform mechanism.

Use Expo-compatible secure storage or the repository's established secure storage implementation for:

* refresh tokens
* protected session credentials
* device-bound secrets where appropriate

Do not store long-lived sensitive credentials in:

* AsyncStorage
* plain files
* navigation params
* logs
* analytics
* Redux/Zustand persistence without encryption

If non-sensitive UI state is persisted, keep it clearly separated from secrets.

---

# SESSION SECURITY

Support:

* access-token expiration
* refresh
* refresh failure
* revocation
* logout
* remote session invalidation

When refresh fails irrecoverably:

* clear secure session state
* disconnect realtime
* clear protected query cache
* navigate to authentication

Do not leave protected screens operational after authorization has expired.

---

# API CLIENT

Create or extend the repository's mobile API client.

Support:

* authenticated requests
* request IDs
* correlation IDs where appropriate
* typed responses
* typed errors
* timeout handling
* request cancellation
* retry classification
* auth refresh
* concurrent-refresh protection

Prevent multiple simultaneous requests from independently attempting refresh-token rotation.

---

# SERVER STATE

Use TanStack Query for server-owned data.

Manage, where applicable:

* current user
* rider profile
* driver profile
* onboarding
* compliance
* vehicles
* ride estimates
* ride request
* trip
* earnings
* payments
* notifications
* support
* safety

Define stable query keys.

Do not duplicate entire server entities inside persistent local state.

---

# CLIENT STATE

Use Zustand or equivalent only for:

* local navigation context
* ephemeral booking UI
* map interaction
* local driver availability UI
* temporary form state where justified
* transient device status

Do not make the client store authoritative for:

* ride state
* trip state
* payment state
* driver eligibility
* payout state

---

# CONNECTIVITY

Implement network-state awareness.

Support states such as:

* online
* offline
* reconnecting
* recovered

When offline:

* stop unsafe mutations
* communicate connection state
* preserve safe local UI
* reconnect automatically
* reconcile authoritative backend state

Do not blindly queue ride/payment mutations locally.

---

# MOBILE ERROR MODEL

Normalize backend errors into safe user-facing categories.

Handle:

* validation
* authentication
* authorization
* not found
* conflict
* rate limiting
* dependency unavailable
* timeout
* offline
* unknown error

Do not expose:

* stack traces
* SQL errors
* provider internals
* internal service topology

---

# RETRY MODEL

Retry only safely retryable operations.

Potentially retry:

* selected reads
* refresh operations
* explicitly idempotent requests
* realtime reconnection

Do not blindly retry:

* ride creation
* payment mutations
* payout mutations
* cancellation
* trip transitions

unless the backend contract explicitly supports idempotency.

---

# PUSH NOTIFICATIONS

Implement the push-notification foundation using Expo-compatible production mechanisms.

Support:

* permission request
* token registration
* token refresh
* device registration
* logout/unregistration
* notification categories
* foreground handling
* background handling
* deep-link handling
* notification state synchronization

Push delivery is not authoritative business state.

---

# PUSH PERMISSION UX

Do not request push permissions immediately on first launch without context unless required by product behavior.

Explain appropriate value before permission request where possible.

Handle:

* granted
* denied
* restricted
* unavailable
* provisional/platform-specific states where applicable

Allow the app to function appropriately when notifications are unavailable, except where a platform capability is genuinely required.

---

# DEEP LINKS

Implement secure deep-link handling for:

* authentication
* active ride
* trip detail
* support case
* notification destination
* account-related workflows where appropriate

Validate destination context.

Do not allow arbitrary URLs to navigate users into unauthorized screens.

---

# DEEP-LINK AUTHORIZATION

A deep link must never grant access.

For example:

A trip ID contained in a push/deep link must still be checked against authenticated backend state.

Do not open sensitive screens solely because a user tapped a valid-looking identifier.

---

# APP LIFECYCLE

Handle:

* foreground
* background
* inactive
* resumed
* terminated
* cold start

Critical workflows must reconcile state after resume.

Examples:

* rider resumes while driver is approaching
* driver resumes while an offer expired
* driver resumes while trip completed
* app resumes after several minutes offline

---

# APP STATE RECOVERY

On foreground/resume:

* determine whether authentication remains valid
* refresh authoritative active state
* reconnect realtime
* refresh time-sensitive information
* refresh permission-sensitive data
* stop stale animations/timers

Do not assume local timers accurately represent backend state.

---

# RIDER BOOKING FOUNDATION

Implement the rider booking foundation.

Support:

* pickup selection
* destination selection
* current location
* map interaction
* address search
* ride-product selection
* estimate request
* quote presentation
* ride creation
* dispatch status

Use backend-authoritative pricing.

Do not calculate final fare in the mobile application.

---

# RIDER LOCATION PERMISSION

When using device location:

* request permission intentionally
* handle denial
* handle approximate/coarse location where the platform supports it
* handle unavailable location
* handle timeout
* avoid excessive background tracking

Explain location usage clearly.

Do not store unnecessary historical rider location locally.

---

# RIDER ACTIVE TRIP FOUNDATION

Implement the mobile active-trip architecture.

Support:

* driver assignment
* driver details
* vehicle details
* ETA
* driver location
* trip status
* safety actions
* support
* reconnect
* page/app restart recovery

Do not trust local trip state.

---

# RIDER REALTIME

Implement a secure WebSocket client for rider trip events.

Support:

* authentication
* subscription
* connection state
* reconnect
* duplicate handling
* stale event handling
* teardown

After reconnect:

* obtain authoritative active-trip state
* restore authorized subscription
* resume updates

---

# DRIVER ONBOARDING FOUNDATION

Implement the driver onboarding mobile foundation.

Support:

* profile information
* onboarding status
* compliance requirement display
* evidence submission entry points
* vehicle registration
* eligibility status

Sensitive compliance data must use secure upload flows provided by backend APIs.

Do not upload documents directly to public object storage.

---

# DRIVER COMPLIANCE UX

Display:

* required items
* pending
* under review
* approved
* rejected
* expired
* suspended

Clearly distinguish:

* account authentication
* onboarding completion
* compliance approval
* operational eligibility

Do not display an "online" control as available when backend eligibility is not satisfied.

---

# SECURE DOCUMENT UPLOAD

Where mobile document upload is supported:

* use backend-authorized upload flows
* validate MIME/type and size before upload where practical
* use provider-issued temporary credentials/URLs as designed
* avoid storing sensitive files permanently in app storage
* clear temporary local files after upload where appropriate

Never embed object-storage credentials in the application bundle.

---

# DRIVER VEHICLE FOUNDATION

Implement mobile screens for:

* vehicle list
* vehicle detail
* vehicle creation
* vehicle update
* eligibility state

Enforce ownership through backend authorization.

Do not trust local driver identity fields.

---

# DRIVER AVAILABILITY

Implement driver online/offline foundation.

Display:

* current availability
* eligibility
* service state
* connection state
* location permission state

The backend remains authoritative.

When the driver taps online:

* submit a backend command
* wait for authoritative response
* reflect server state

Do not optimistically assume online status if it can cause dispatch inconsistency.

---

# DRIVER LOCATION FOUNDATION

Driver location is a high-frequency production workflow.

Implement a robust mobile location pipeline supporting:

* foreground location
* background location where product/platform rules permit
* permission handling
* sampling
* batching where beneficial
* authenticated submission
* retry only where safe
* local queueing only within bounded safe constraints
* stale-update detection
* lifecycle management

Do not implement an unbounded offline location queue.

---

# DRIVER LOCATION PERMISSIONS

Handle platform permissions for:

* foreground location
* background location

The UX must explain why each permission is required.

Handle:

* denied
* denied permanently
* approximate/coarse
* foreground-only
* background-enabled
* restricted platform state

The driver must not appear fully online when required location capability is unavailable.

---

# DRIVER LOCATION SAMPLING

Use appropriate sampling to balance:

* dispatch accuracy
* battery
* CPU
* mobile network
* backend ingestion load

Do not send location updates at maximum device frequency by default.

Allow backend/server policy to influence acceptable update behavior where appropriate.

---

# DRIVER LOCATION BUFFERING

If temporary network loss occurs:

* maintain bounded local state
* discard obsolete samples
* preserve only the data necessary for safe recovery
* avoid unbounded disk usage
* do not fabricate historical timestamps

The backend remains authoritative about accepted location updates.

---

# DRIVER REALTIME OFFERS

Implement the driver-side realtime offer foundation.

Support:

* authenticated connection
* ride-offer event
* offer display
* countdown
* accept
* reject
* expiration
* duplicate event handling
* reconnect

The backend remains authoritative for offer expiration.

---

# OFFER COUNTDOWN

A local timer is only a presentation aid.

The mobile app must never treat its local countdown as the authoritative expiration rule.

Before accepting:

* send the server command
* allow the server to reject an expired/stale offer
* reconcile current state

---

# DRIVER ACCEPTANCE

Implement idempotent driver offer acceptance.

Handle:

* success
* offer already accepted
* offer expired
* offer canceled
* network timeout
* duplicate request
* another driver won

After uncertain response:

* retrieve authoritative current offer/trip state
* do not issue unlimited retries

---

# DRIVER ACTIVE TRIP FOUNDATION

Implement the driver's active-trip mobile architecture.

Support:

* route to pickup
* driver arrived
* trip-start verification
* active trip
* completion
* cancellation where permitted
* rider/trip information
* safety
* support

Use backend-authoritative lifecycle states.

---

# DRIVER TRIP ACTIONS

Critical actions such as:

* arrive
* start trip
* complete trip
* cancel

must:

* validate current server state
* be disabled while pending
* use idempotency where supported
* reconcile conflicts
* display the authoritative result

Do not let button state alone prevent duplicates.

---

# DRIVER NAVIGATION INTEGRATION

Where an external navigation application is used:

* create secure navigation intents
* use server/backend-provided destination information
* avoid exposing unnecessary rider private data
* handle missing navigation applications
* return to the ride application gracefully

Do not treat external navigation as authoritative trip state.

---

# DRIVER TRIP PRIVACY

The driver should see only information necessary to complete the trip.

Avoid exposing:

* unnecessary rider personal data
* payment credentials
* unrelated historical ride information
* private support content

---

# RIDER/DRIVER COMMUNICATION

Where backend communication support exists, implement the mobile entry points.

Do not build an independent messaging backend in the mobile apps.

Support:

* communication initiation
* safe contact
* masked contact mechanisms where backend provides them
* trip-linked context

---

# SAFETY FOUNDATION

Implement rider and driver safety access points.

Support backend-provided capabilities such as:

* emergency workflow
* trusted contacts
* trip sharing
* safety incident reporting
* safety information

Safety actions must remain accessible during active trips.

---

# TRIP SHARING

Where supported:

* initiate sharing
* display sharing status
* revoke if supported
* handle expiration
* preserve privacy

Do not expose raw share tokens in analytics or logs.

---

# SUPPORT FOUNDATION

Implement rider and driver support access.

Support:

* trip issue
* payment issue where applicable
* driver/rider issue
* safety issue
* general support
* case status

Use backend support APIs.

Do not create direct email-only flows as the primary support mechanism when a case system exists.

---

# EARNINGS FOUNDATION

Implement driver-facing earnings screens using backend APIs.

Support:

* available earnings
* pending earnings
* historical earnings
* payout status
* adjustments where backend exposes them

Use server pagination.

Do not calculate official earnings solely from local trip history.

---

# PAYMENT FOUNDATION

Implement rider-facing payment surfaces where supported.

Support:

* payment methods
* default method
* payment status
* receipt history
* refunds/status

Use provider-supported secure payment UI where required.

Do not handle raw card data unnecessarily.

---

# NOTIFICATION CENTER

Implement mobile notification state.

Support:

* unread
* read/unread
* notification list
* deep-link navigation
* notification refresh
* offline behavior
* push/open correlation

Do not assume notification arrival means the underlying trip state has changed successfully.

---

# OFFLINE MODE

The app must distinguish between:

* safe cached reads
* unsafe mutations
* realtime state
* stale data

During offline operation:

* preserve safe local UI
* show stale state indicators
* disable unsafe actions
* reconnect
* reconcile authoritative state

Do not queue payments or trip-state transitions for arbitrary later submission.

---

# MOBILE CACHE SECURITY

Do not persist sensitive server state indefinitely.

At minimum protect or avoid persistent storage of:

* active-trip exact location
* payment-sensitive information
* compliance documents
* safety incident details
* support content

When persistence is necessary:

* encrypt where appropriate
* scope by account
* clear on logout
* expire according to data sensitivity

---

# ACCOUNT SWITCHING

If the repository supports switching accounts:

* terminate previous WebSockets
* clear query caches
* clear local state
* clear device registrations as necessary
* reset navigation
* re-authenticate
* obtain fresh permissions

Never show one user's trip or driver state to another authenticated user.

---

# LOGOUT

Logout must:

* revoke/clear session according to backend contract
* unregister push token where applicable
* stop location services
* disconnect WebSockets
* clear sensitive caches
* clear local protected state
* return to authentication

Driver logout must not silently leave location streaming active.

---

# APP PERMISSIONS

Centralize permission handling for:

* location
* notifications
* camera
* photo library
* microphone where genuinely required

Each permission must have:

* request
* current state
* denied handling
* retry path
* platform-specific behavior

Do not request permissions that the application does not actually use.

---

# APP LIFECYCLE AND LOCATION SAFETY

When the driver application transitions to background:

* maintain background location only when the driver is permitted and expected to be operational
* reduce unnecessary work
* maintain necessary networking
* stop location tracking when driver should no longer be online

When the driver goes offline or logs out:

* stop background location services
* clean up subscriptions

Do not drain battery with unnecessary continuous services.

---

# MOBILE SECURITY

Perform a security review for:

* insecure storage
* token leakage
* logs
* screenshots where sensitive information exists
* deep-link abuse
* WebSocket abuse
* unauthorized navigation
* certificate/security configuration where appropriate
* debug configuration leaking into production
* insecure API endpoints
* clipboard exposure

Follow platform security best practices appropriate to iOS and Android.

---

# SENSITIVE SCREEN PROTECTION

For appropriate sensitive screens, consider platform controls against:

* unintended screenshots
* app-switcher previews exposing private information
* clipboard leakage

Use these controls only where product requirements justify them and ensure they do not create inaccessible behavior.

---

# NETWORK SECURITY

All production API traffic must use secure transport.

Do not disable TLS validation.

If certificate pinning is introduced, it must be operationally supportable and include a rotation strategy.

Do not implement brittle security controls that could cause complete outage without recovery.

---

# PUSH TOKEN SECURITY

Push tokens must:

* be associated with the authenticated account/device
* be registered through backend authorization
* be removed/unregistered where appropriate
* not be treated as authentication credentials

---

# ANALYTICS

Implement a mobile analytics abstraction.

Track appropriate events such as:

* app launch
* authentication
* booking started
* estimate requested
* ride requested
* ride assigned
* trip started
* trip completed
* driver online
* offer received
* offer accepted
* notification opened
* safety action

Do not send:

* tokens
* payment credentials
* private messages
* unnecessary precise location
* compliance documents
* safety-sensitive content

Respect applicable consent/privacy controls.

---

# CRASH REPORTING

Integrate the repository's chosen crash/telemetry mechanism where present.

Crash reports must redact:

* tokens
* credentials
* payment information
* private support content
* unnecessary exact location

Include useful contextual metadata such as:

* app version
* build
* platform
* environment
* anonymized user/session reference
* active feature

---

# PERFORMANCE

Optimize mobile performance for:

* startup
* navigation
* map rendering
* location updates
* WebSocket traffic
* list rendering
* image loading
* memory
* battery
* network consumption

Avoid:

* excessive renders
* unnecessary polling
* unbounded location queues
* large persistent caches
* unnecessary background tasks

---

# BATTERY

Driver location is especially battery-sensitive.

Measure and optimize:

* location sampling frequency
* background wakeups
* network requests
* map rendering
* WebSocket keepalive

Do not sacrifice critical dispatch visibility, but do not continuously perform maximum-rate device work.

---

# MEMORY

Prevent:

* retaining thousands of location events
* unbounded notification arrays
* duplicate query caches
* large image caches
* retained navigation stacks containing obsolete trip state

Use pagination and bounded data structures.

---

# ACCESSIBILITY

Implement mobile accessibility for:

* forms
* buttons
* ride state
* active trip
* driver offer
* safety controls
* navigation
* error messages
* notifications

Support:

* screen readers
* dynamic text sizing
* sufficient contrast
* large touch targets
* reduced motion where applicable

Do not rely solely on color to convey trip state.

---

# INTERNATIONALIZATION

Structure mobile UI so it can support:

* multiple languages
* locale-specific formatting
* currency
* date/time
* pluralization
* right-to-left expansion where future markets may require it

Do not concatenate user-facing sentences in ways that prevent translation.

---

# TIME AND TIMEZONE

Display dates/times using appropriate market/user timezone rules.

For scheduled rides:

* show local time clearly
* preserve timezone metadata
* avoid device-clock assumptions

The backend remains authoritative for actual event timestamps.

---

# TESTING REQUIREMENTS

Write comprehensive mobile tests.

## AUTHENTICATION

Test:

* login
* registration
* logout
* session restore
* refresh
* session expiration
* account restriction

## RIDER

Test:

* location permission
* booking
* estimate
* ride creation
* dispatch
* active trip
* reconnect
* cancellation
* completion
* rating
* payment display
* notifications

## DRIVER

Test:

* onboarding
* compliance
* vehicle
* availability
* location
* offer
* acceptance
* expiration
* active trip
* start
* completion
* cancellation
* earnings

## REALTIME

Test:

* connect
* authenticate
* subscription
* duplicate events
* stale events
* disconnect
* reconnect
* authoritative state recovery

## PERMISSIONS

Test:

* granted
* denied
* restricted
* revoked while app is running
* background permission behavior where applicable

---

# DEVICE TESTING

Validate on representative:

* iOS versions
* Android versions
* screen sizes
* safe-area configurations
* background/foreground transitions
* poor network conditions

Do not claim mobile release readiness from simulator-only testing.

---

# END-TO-END TESTING

Implement E2E coverage for critical flows where the repository has an established mobile E2E framework.

Rider:

1. authenticate
2. select pickup
3. select destination
4. estimate
5. request ride
6. receive assignment
7. observe trip
8. complete
9. review receipt

Driver:

1. authenticate
2. complete onboarding prerequisites
3. become available
4. receive offer
5. accept
6. navigate/pick up
7. start
8. complete
9. view earnings

---

# BACKGROUND LOCATION TESTING

Driver location must be tested under:

* foreground
* background
* screen locked
* temporary network loss
* app resume
* permission downgrade
* logout
* offline/online transitions

Verify that tracking stops when it should.

---

# PUSH TESTING

Test:

* permission flow
* token registration
* notification receipt
* foreground notification
* background notification
* notification tap
* deep link
* logged-out notification
* stale notification
* duplicate notification

---

# DEEP-LINK TESTING

Validate:

* authenticated destination
* unauthenticated destination
* expired resource
* unauthorized resource
* malformed identifier
* notification-originated navigation

A valid link must not bypass authorization.

---

# ACCESSIBILITY TESTING

Validate:

* screen-reader navigation
* labels
* focus
* dynamic text
* buttons
* forms
* trip status
* offer countdown
* safety controls

---

# PERFORMANCE TESTING

Measure:

* cold start
* warm start
* screen navigation
* map rendering
* location ingestion client load
* realtime event processing
* memory
* battery
* network traffic

Use actual devices where possible.

---

# BUILD CONFIGURATION

Establish production-ready Expo configuration for:

* development
* test
* staging
* production

Manage:

* bundle identifiers
* package names
* environment variables
* push notification configuration
* deep links
* permissions
* icons/splash
* update channels/strategy where used
* signing configuration

Never commit:

* signing secrets
* private credentials
* provider secrets

---

# IOS REQUIREMENTS

Address where applicable:

* permission descriptions
* background location configuration
* push notification capabilities
* deep linking
* associated domains where required
* app lifecycle
* secure storage
* background execution rules
* release configuration

Do not request background capabilities without legitimate application use.

---

# ANDROID REQUIREMENTS

Address where applicable:

* foreground location
* background location
* notification permissions
* deep links
* secure storage
* foreground services where required
* app lifecycle
* notification channels
* battery optimizations
* release configuration

Follow current platform rules rather than assuming unrestricted background execution.

---

# DOCUMENTATION

Update mobile documentation for:

* development setup
* rider app
* driver app
* environment configuration
* authentication
* push notifications
* deep links
* location permissions
* background location
* maps
* testing
* build profiles
* iOS requirements
* Android requirements
* release workflow
* security

Documentation must describe actual implementation.

---

# IMPLEMENTATION DISCIPLINE

Before modifying files:

1. Inspect the repository.
2. Determine existing Expo/mobile architecture.
3. Identify shared packages and contracts.
4. Preserve compatible infrastructure.
5. Establish navigation.
6. Establish secure authentication.
7. Establish API client.
8. Establish server state.
9. Establish local state.
10. Establish push notifications.
11. Establish deep links.
12. Establish permissions.
13. Establish lifecycle management.
14. Establish realtime.
15. Implement rider booking foundation.
16. Implement rider active-trip foundation.
17. Implement driver onboarding foundation.
18. Implement driver availability.
19. Implement driver location.
20. Implement driver offer foundation.
21. Add safety/support foundations.
22. Add observability.
23. Add accessibility.
24. Add tests.
25. Validate iOS/Android builds.
26. Perform security/privacy/performance review.
27. Update documentation.
28. Produce the required completion report.

Do not rewrite unrelated mobile code.

---

# PRODUCTION COMPLETENESS

Never leave:

* fake location
* fake ride offers
* simulated trip state
* hardcoded driver data
* fake authentication
* fake push handling
* insecure token storage
* placeholder background location
* disconnected navigation
* TODO/FIXME implementation gaps
* pseudo-code

Every implemented workflow must connect to actual backend contracts.

---

# PROHIBITED PRACTICES

Never:

* store long-lived sensitive tokens in insecure storage
* expose backend secrets in mobile bundles
* trust local role state for authorization
* trust notification payloads as authoritative state
* assume the local offer countdown controls expiration
* send unlimited location samples
* retain unbounded offline location
* continue location after logout/offline state requires termination
* expose precise user data unnecessarily
* queue financial mutations without an explicit safe backend contract
* bypass backend authorization through deep links
* leave background services running unnecessarily
* disable TLS validation in production

---

# IMPLEMENTATION BOUNDARIES

This volume establishes the production mobile foundation and core rider/driver operational architecture.

It does not implement every advanced screen.

Later mobile work must extend:

* navigation
* authentication
* secure storage
* API client
* state management
* realtime
* location
* push notifications
* permissions
* lifecycle

without creating parallel foundations.

Do not implement backend services.

Do not implement web applications.

Do not implement cloud infrastructure.

---

# REQUIRED IMPLEMENTATION DELIVERABLES

Implement or update:

## SHARED MOBILE FOUNDATION

* application architecture
* navigation
* authentication
* secure storage
* API client
* TanStack Query
* local state
* connectivity
* push notifications
* deep links
* permissions
* app lifecycle
* WebSocket
* observability
* accessibility

## RIDER

* booking
* location
* estimate
* ride request
* dispatch state
* active trip
* realtime

## DRIVER

* onboarding
* compliance foundation
* vehicle
* availability
* location
* offers
* acceptance
* active trip foundation

## PLATFORM SECURITY

* secure storage
* token handling
* deep-link authorization
* permission handling
* privacy
* logging redaction

## QUALITY

* tests
* device validation
* accessibility
* performance
* build configuration
* documentation

---

# REQUIRED BACKEND CONTRACT CONSUMPTION

Use the backend's existing contracts for:

* authentication
* rider
* driver
* compliance
* vehicles
* availability
* location
* ride estimates
* ride requests
* dispatch offers
* trips
* notifications
* safety
* support
* payments
* earnings

If a required backend capability is missing, identify the dependency explicitly rather than inventing a fake mobile implementation.

---

# RUNTIME VALIDATION

Verify:

* authentication
* rider booking
* rider active trip
* driver login
* driver onboarding
* driver availability
* location permissions
* location submission
* driver offers
* acceptance
* active trip
* push notifications
* deep links
* logout
* session expiration
* reconnect
* app restart

Verify driver location stops appropriately when:

* driver logs out
* driver goes offline
* account becomes unavailable
* application no longer has required permission

---

# COMPLETION REPORT REQUIREMENTS

When implementation is complete, report:

## FILES CREATED

List every new file.

## FILES MODIFIED

List every modified file.

## MOBILE FOUNDATION

Report:

* navigation
* authentication
* secure storage
* API client
* query state
* local state
* permissions
* push
* deep links
* lifecycle
* realtime

## RIDER

Report:

* booking
* location
* estimate
* request
* active trip
* realtime

## DRIVER

Report:

* onboarding
* compliance
* vehicle
* availability
* location
* offers
* active trip

## PLATFORM SECURITY

Report:

* secure credential handling
* deep-link protection
* permission handling
* data privacy
* logging

## OBSERVABILITY

Report:

* analytics
* crash reporting
* telemetry
* correlation

## TESTS

List tests added or modified and the behaviors they verify.

## DEVICE VALIDATION

Report:

* iOS devices/versions tested
* Android devices/versions tested
* background/foreground validation
* permission validation
* poor-network validation

## BUILD VALIDATION

Report:

* TypeScript
* lint
* tests
* Expo validation
* iOS build
* Android build
* runtime smoke tests

## COMPATIBILITY

Identify:

* backend API compatibility
* WebSocket compatibility
* push/deep-link compatibility
* iOS/Android implications

## UNRESOLVED ISSUES

List only genuine remaining issues.

Do not claim mobile foundation completion if critical authentication, location, realtime, navigation, or lifecycle behavior remains insecure, disconnected, or unverified.

---

# FINAL ENGINEERING PRINCIPLE

The mobile applications must behave as secure, resilient production clients of the ride-hailing backend.

The mobile layer owns:

* presentation
* device capabilities
* local interaction state
* networking
* realtime connection management
* push notifications
* lifecycle
* platform integration

The backend remains authoritative for:

* authentication
* authorization
* driver eligibility
* ride state
* dispatch
* trip state
* pricing
* payments
* earnings
* payout
* safety state

The rider and driver applications must remain correct through:

* app restarts
* background/foreground transitions
* network loss
* WebSocket interruptions
* duplicate notifications
* stale local state
* denied permissions
* device resource constraints

Prioritize:

* security
* correctness
* battery efficiency
* realtime resilience
* privacy
* accessibility
* performance
* maintainability
* platform compatibility

The repository remains the implementation source of truth.

All subsequent mobile functionality must build on these foundations without introducing competing authentication, networking, state, location, notification, or realtime architectures.
