You are operating in Senior Engineering Team Mode.

Build the production-ready mobile customer applications for an enterprise-scale global ride-hailing, mobility, transportation, and delivery platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

The mobile applications must consume the approved backend APIs, authentication contracts, authorization model, real-time contracts, trip-state model, pricing contracts, payment contracts, maps integration, notification system, safety system, business-account system, and Project Index.

Do not redesign the backend.

Do not implement backend code.

Do not implement web frontend code.

Do not implement infrastructure code.

Do not generate Terraform.

Do not generate Kubernetes manifests.

Do not generate CI/CD workflows.

────────────────────────────────────────

MISSION

Build the production-ready native-feeling mobile applications for:

• Riders
• Drivers

Platforms:

• iOS
• Android

RIDER FEATURES

• Registration
• Login
• Account
• Profiles
• Saved places
• Current location
• Destination search
• Places
• Geocoding
• Ride categories
• Fare estimates
• Ride booking
• Driver matching
• Driver assignment
• Live driver tracking
• Trip tracking
• ETA
• Multi-stop rides
• Scheduled rides
• Promotions
• Payment methods
• Wallet
• Receipts
• Trip history
• Ratings
• Reviews
• Messaging
• Notifications
• Trip sharing
• Safety
• Support
• Business rides
• Account settings

DRIVER FEATURES

• Registration
• Onboarding
• Verification
• Documents
• Vehicle management
• Availability
• Location
• Ride offers
• Accept/reject
• Navigation
• Pickup
• Arrival
• Trip start
• Trip stops
• Trip completion
• Earnings
• Incentives
• Payouts
• Ratings
• Messaging
• Notifications
• Safety
• Support
• Account settings

The mobile applications must be:

• Fast
• Reliable
• Secure
• Battery-conscious
• Data-efficient
• Accessible
• Offline-aware
• Resilient to network interruption
• Production-ready

────────────────────────────────────────

TECHNOLOGY STACK

Framework:

• React Native
• Expo
• TypeScript

Navigation:

• React Navigation

Server State:

• TanStack Query

Client State:

• Zustand

Forms:

• React Hook Form
• Zod

Secure storage:

• Expo Secure Store or approved platform-secure storage

Local database:

• SQLite or approved mobile persistence layer

Maps:

• Google Maps SDK or approved provider abstraction

Location:

• Expo Location
• Approved background-location integration

Notifications:

• Firebase Cloud Messaging
• Apple Push Notification Service

Real-time:

• WebSockets
• Socket.IO client where appropriate

Testing:

• Jest
• React Native Testing Library
• Detox or approved mobile E2E framework

────────────────────────────────────────

MOBILE ARCHITECTURE

Use:

• Feature-first architecture
• Strict TypeScript
• Reusable components
• Platform abstraction
• Separation of UI and domain presentation
• Server state separation
• Local persistence boundaries
• Secure-storage boundaries
• Explicit navigation boundaries
• Dependency injection where appropriate

Do not put backend business logic inside screens.

Do not duplicate authoritative backend state unnecessarily.

Do not use Zustand as the server-state source of truth.

────────────────────────────────────────

APPLICATION STRUCTURE

Create a scalable structure:

src/

features/

components/

navigation/

screens/

layouts/

providers/

hooks/

services/

stores/

database/

storage/

location/

maps/

realtime/

notifications/

audio/

network/

config/

types/

utils/

assets/

tests/

Separate feature modules for:

• Authentication
• Rider
• Driver
• Booking
• Trips
• Maps
• Location
• Payments
• Promotions
• Wallet
• Ratings
• Messaging
• Notifications
• Safety
• Support
• Business
• Earnings
• Payouts
• Settings

────────────────────────────────────────

EXPO FOUNDATION

Implement:

• Expo configuration
• App metadata
• Bundle identifiers
• Android application configuration
• iOS application configuration
• Environment configuration
• Deep-link configuration
• Notification configuration
• Location configuration
• Secure-storage configuration

Separate development and production configuration.

────────────────────────────────────────

NAVIGATION

Implement React Navigation.

RIDER NAVIGATION:

• Home
• Booking
• Activity
• Wallet
• Account
• Search
• Trip
• Notifications
• Support

DRIVER NAVIGATION:

• Home
• Offers
• Active Trip
• Earnings
• Incentives
• Account
• Vehicle
• Notifications
• Support

Support:

• Stack navigation
• Tab navigation
• Modal flows
• Protected navigation
• Deep links

Navigation is never an authorization boundary.

────────────────────────────────────────

AUTHENTICATION

Implement:

• Registration
• Login
• Logout
• Session restoration
• Token refresh
• Email verification
• Password reset
• Password change
• Device registration
• Secure session storage

Sensitive authentication state must use secure storage.

Never store passwords.

────────────────────────────────────────

ACCOUNT AND PROFILE

RIDER:

• Profile
• Account settings
• Saved places
• Preferences
• Language
• Notifications
• Privacy
• Security
• Payment settings

DRIVER:

• Profile
• Vehicle
• Account
• Compliance
• Notifications
• Security
• Preferences

Profile-specific information must remain isolated.

────────────────────────────────────────

SECURE STORAGE

Use secure platform storage for:

• Access credentials
• Refresh credentials
• Device identity
• Other secrets

Use ordinary/local persistence only for:

• Non-sensitive cache
• Preferences
• Offline metadata
• Safe UI state

Do not place authentication secrets in SQLite or AsyncStorage-like ordinary storage.

────────────────────────────────────────

NETWORKING

Implement a typed API client supporting:

• HTTPS
• Authentication
• Request IDs
• Correlation IDs
• Timeouts
• Cancellation
• Retries where safe
• Error normalization
• Connectivity detection

Never retry non-idempotent financial mutations blindly.

────────────────────────────────────────

CONNECTIVITY

Handle:

• Online
• Offline
• Weak connectivity
• Wi-Fi
• Cellular
• Network transition
• Reconnection

When reconnecting:

• Refresh important queries
• Reconcile trip state
• Reconcile driver availability
• Reconcile queue
• Reconcile pending mutations

Do not use aggressive polling when real-time events are available.

────────────────────────────────────────

LOCATION PERMISSIONS

Implement platform-safe location permissions.

Support:

• Foreground permission
• Background permission where required
• Permission denied
• Permission revoked
• Limited permission
• Approximate location where applicable

Explain why permissions are requested.

Never request unnecessary permissions.

────────────────────────────────────────

RIDER LOCATION

Support:

• Current location
• Location permission state
• Location accuracy
• Map marker
• Pickup selection
• Map movement

Do not continuously collect location when it is not needed.

────────────────────────────────────────

DRIVER LOCATION

Support:

• High-accuracy location while online/active
• Background location where required by trip/availability state
• Location heartbeat
• Network-aware throttling
• Battery-aware update strategy
• Permission handling

Driver location reporting must follow backend requirements.

────────────────────────────────────────

DRIVER AVAILABILITY

Support:

• Go online
• Go offline
• Availability status
• Location status
• Connection status
• Eligibility error

Prevent accidental transition into online state when required verification is incomplete.

────────────────────────────────────────

MAP EXPERIENCE

RIDER:

• Current location
• Pickup
• Destination
• Driver
• Route
• ETA
• Service area
• Pickup zone
• Airport zone

DRIVER:

• Current location
• Pickup
• Destination
• Stops
• Route
• Navigation context
• Traffic information where available

Handle map loading and provider errors gracefully.

────────────────────────────────────────

DESTINATION SEARCH

Implement:

• Search
• Autocomplete
• Recent destinations
• Saved places
• Current location
• Place details
• Map selection

Debounce requests.

Cancel stale requests.

Cache safe place information where appropriate.

────────────────────────────────────────

BOOKING FLOW

RIDER:

Current Location
→ Destination
→ Ride Category
→ Fare Estimate
→ Payment
→ Promotion
→ Confirmation
→ Ride Request

Support:

• Immediate rides
• Scheduled rides
• Multi-stop rides

Prevent duplicate ride requests through client-side guards plus backend idempotency.

────────────────────────────────────────

RIDE CATEGORY UI

Display:

• Category
• Capacity
• ETA
• Estimated fare
• Accessibility
• Vehicle attributes where provided

Do not display unavailable categories.

────────────────────────────────────────

FARE ESTIMATE

Display:

• Estimated fare
• Currency
• Fare components
• Surge
• Promotion
• Estimated duration
• Estimated distance

Clearly distinguish:

• Estimate
• Final fare

The backend remains authoritative.

────────────────────────────────────────

MATCHING EXPERIENCE

Display:

• Searching
• Estimated wait
• Selected category
• Cancellation
• Matching failure
• Retry

Use real-time state when available.

Do not poll continuously.

────────────────────────────────────────

DRIVER ASSIGNMENT

Display:

• Driver name
• Driver rating
• Driver photo where authorized
• Vehicle
• Color
• License plate
• ETA
• Driver location
• Contact/messaging controls
• Safety controls

────────────────────────────────────────

ACTIVE RIDER TRIP

Display:

• Driver location
• Route
• ETA
• Pickup
• Destination
• Stops
• Trip status
• Vehicle
• Driver
• Messaging
• Trip sharing
• Safety

Support real-time updates.

────────────────────────────────────────

ACTIVE DRIVER TRIP

Display:

• Pickup
• Rider information permitted by policy
• Destination
• Stops
• ETA
• Navigation
• Trip status
• Safety
• Messaging

Support:

• Arrived
• Start
• Stop reached
• Complete

All state transitions must call backend APIs.

────────────────────────────────────────

REAL-TIME MOBILE ARCHITECTURE

Use WebSockets/Socket.IO for:

• Matching state
• Assignment
• Driver location
• Rider trip location
• ETA
• Trip state
• Messaging
• Notifications

Support:

• Authentication
• Authorization
• Reconnect
• Duplicate event handling
• Stale event handling
• Connection state
• Regional routing

When disconnected:

• Show connection state
• Reconcile after reconnect
• Do not fabricate current trip state

────────────────────────────────────────

TRIP STATE RECONCILIATION

On app resume or reconnect:

1. Determine connection state.
2. Fetch authoritative trip state.
3. Compare local state.
4. Apply server state.
5. Resume real-time subscriptions.

Never assume locally cached trip state is authoritative.

────────────────────────────────────────

SCHEDULED RIDES

Support:

• Create
• View
• Edit where supported
• Cancel
• Reminder
• Driver assignment
• Status

Use server-provided status.

────────────────────────────────────────

MULTI-STOP RIDES

Support:

• Add stop
• Remove stop
• Reorder
• View updated route
• Updated ETA
• Updated estimate

Handle backend version conflicts.

────────────────────────────────────────

TRIP HISTORY

Implement:

• Trip list
• Trip detail
• Date grouping
• Fare
• Driver
• Vehicle
• Pickup
• Dropoff
• Receipt
• Payment status
• Support

Use paginated queries.

────────────────────────────────────────

PAYMENTS

Support:

• Payment methods
• Add
• Remove
• Default
• Payment status
• Failed-payment recovery
• Receipts
• Refund status

Use provider-approved mobile payment UI when needed.

Never store raw card data.

────────────────────────────────────────

WALLET

Display:

• Balance
• Promotional credits
• Refund credits
• Expiration
• Ledger history where permitted

Do not calculate authoritative wallet balance locally.

────────────────────────────────────────

PROMOTIONS

Support:

• Promo entry
• Validation
• Eligibility
• Applied promotion
• Expiration
• Usage state

Backend remains authoritative.

────────────────────────────────────────

RATINGS

Implement:

• Driver rating
• Rider rating for driver-side flow
• Structured feedback
• Review
• Submit

Prevent duplicate submissions with local UI state and backend idempotency.

────────────────────────────────────────

MESSAGING

Support trip-scoped messaging:

• Conversation
• Messages
• Delivery
• Read state
• Push fallback
• Reconnection

Never expose phone numbers unless the approved product requires it.

────────────────────────────────────────

NOTIFICATIONS

Support:

• FCM
• APNS
• Permission handling
• Token registration
• Token refresh
• Foreground notifications
• Background notifications
• Terminated-app notifications
• Badge count
• Deep-link actions

Categories:

• Ride
• Driver
• Payment
• Promotion
• Safety
• Support
• Account

────────────────────────────────────────

DEEP LINKS

Support:

• Ride
• Trip
• Driver
• Support
• Payment
• Promotion
• Notification
• Business
• Account

Validate authentication and authorization after opening a deep link.

Never trust deep-link data as security authority.

────────────────────────────────────────

TRIP SHARING

Implement:

• Share trip
• Select channel/contact
• View active share
• Revoke share

Use backend-issued temporary access.

────────────────────────────────────────

SAFETY

Implement:

• Emergency assistance action
• Trip sharing
• Trusted contacts
• Safety information
• Incident reporting
• Safety check-in where supported

Do not represent the application as guaranteeing physical safety.

────────────────────────────────────────

SUPPORT

Implement:

• Help
• Trip support
• Payment support
• Lost item
• Safety support
• Account support
• Case list
• Case detail
• Case messaging

────────────────────────────────────────

DRIVER ONBOARDING

Implement:

• Driver registration
• Application
• Personal details
• Documents
• Vehicle
• Insurance
• Verification
• Compliance
• Application state

Display:

• Draft
• Submitted
• Pending
• Approved
• Rejected
• Resubmission required

────────────────────────────────────────

DOCUMENT UPLOADS

Support:

• Camera
• Gallery/file selection
• Upload
• Upload progress
• Replace
• Preview where appropriate
• Verification status
• Expiration

Use signed backend upload authorization.

Never expose storage credentials.

────────────────────────────────────────

VEHICLE MANAGEMENT

Support:

• Add vehicle
• Update
• Category
• Documents
• Verification state
• Insurance
• Expiration

Display eligibility clearly.

────────────────────────────────────────

DRIVER OFFERS

Display:

• Pickup
• Estimated distance
• Pickup ETA
• Category
• Passenger count where permitted
• Accessibility
• Offer expiration

Support:

• Accept
• Reject

Disable buttons appropriately while request is being processed.

────────────────────────────────────────

DRIVER NAVIGATION

Support integration with approved navigation/map systems.

Provide:

• Pickup navigation
• Destination navigation
• Stop navigation
• Route updates

Do not build an entire navigation engine inside the app.

────────────────────────────────────────

DRIVER EARNINGS

Display:

• Daily
• Weekly
• Trip-level
• Incentives
• Tips
• Adjustments
• Pending
• Available

────────────────────────────────────────

DRIVER PAYOUTS

Support:

• Payout methods
• Available balance
• Payout request
• Payout state
• Payout history
• Failure state

Never present payout as completed before backend confirmation.

────────────────────────────────────────

DRIVER RATINGS

Display:

• Overall rating
• Rating count
• Trend
• Available feedback

Respect privacy.

────────────────────────────────────────

BUSINESS RIDES

For supported business users:

• Business profile
• Business trip selection
• Cost center
• Policy state
• Receipt type

Use backend policy decisions.

────────────────────────────────────────

OFFLINE-AWARE BEHAVIOR

Implement safe caching for:

• User profile
• Saved places
• Recent destinations
• Recent trips
• Basic catalog-like UI state
• Business policy metadata where appropriate

When offline:

• Clearly indicate unavailable operations
• Preserve safe unsent state
• Retry only safe operations

Do not create offline ride requests that could unexpectedly execute later.

────────────────────────────────────────

LOCAL PERSISTENCE

Use SQLite or approved local persistence for:

• Safe cache
• Pending sync metadata
• Offline UI state
• Download metadata in later phases

Sensitive credentials remain outside ordinary database storage.

────────────────────────────────────────

ACCESSIBILITY

Support:

• VoiceOver
• TalkBack
• Dynamic Type
• Large text
• Screen reader labels
• Accessible map alternatives
• Large touch targets
• Contrast
• Reduced motion

Important trip information must have non-visual alternatives.

────────────────────────────────────────

LOCALIZATION

Support:

• Multiple languages
• Locale selection
• Date/time
• Currency
• Number formatting
• Relative time
• RTL
• Localized notifications
• Localized validation

Do not hard-code user-facing strings.

────────────────────────────────────────

THEMING

Support:

• Light
• Dark
• System
• Persistent choice

Respect platform accessibility settings.

────────────────────────────────────────

PERFORMANCE

Optimize:

• Startup
• Navigation
• Map loading
• Location updates
• Real-time connections
• Booking flow
• Trip rendering
• Large trip history
• Image loading
• Memory usage

Avoid unnecessary re-renders.

────────────────────────────────────────

BATTERY OPTIMIZATION

Minimize:

• Background location when unnecessary
• Polling
• Network retries
• Analytics requests
• Image downloads

Use state-dependent location frequencies.

Driver online/trip mode may use higher frequency than normal browsing.

────────────────────────────────────────

DATA USAGE

Support:

• Image optimization
• Network-aware loading
• Reduced background requests
• Efficient location updates
• Batched telemetry

Warn appropriately about data-intensive operations.

────────────────────────────────────────

SECURITY

Implement:

• Secure storage
• Session protection
• Device registration
• Safe deep links
• Protected navigation
• Safe URL handling
• Sensitive data minimization
• Secure document uploads

Never store:

• Passwords
• API secrets
• Payment credentials
• Long-lived sensitive tokens

────────────────────────────────────────

ERROR HANDLING

Handle:

• Network failure
• Location permission failure
• Map failure
• Matching failure
• Trip-state conflict
• Payment failure
• Driver-offer expiration
• WebSocket disconnect
• Notification failure
• Document-upload failure
• Verification failure

Provide understandable recovery actions.

────────────────────────────────────────

TESTING

UNIT TESTS

Test:

• Booking state
• Trip state
• Driver availability state
• Offer state
• Fare display
• Validation
• Synchronization logic

COMPONENT TESTS

Test:

• Booking
• Maps
• Fare estimate
• Matching
• Active trip
• Driver offer
• Driver trip
• Payments
• Ratings
• Messaging
• Safety
• Support

INTEGRATION TESTS

Test:

• API client
• Authentication
• WebSockets
• Location
• Maps
• Notifications
• Booking
• Trip reconciliation

END-TO-END TESTS

RIDER:

• Registration
• Login
• Search
• Booking
• Matching
• Driver assignment
• Active trip
• Completion
• Rating
• Receipt
• Support

DRIVER:

• Registration
• Onboarding
• Documents
• Vehicle
• Verification
• Go online
• Offer
• Accept
• Pickup
• Trip
• Completion
• Earnings
• Payout

BUSINESS:

• Select business profile
• Book business ride
• Apply policy
• View receipt

────────────────────────────────────────

PLATFORM TESTING

Test on:

• Supported iOS versions
• Supported Android versions
• Phones
• Tablets where supported
• Different screen sizes
• Different network conditions
• Location permission states
• Background/foreground transitions

────────────────────────────────────────

ACCESSIBILITY TESTING

Test:

• VoiceOver
• TalkBack
• Dynamic Type
• Large text
• Player/map alternatives
• Booking
• Forms
• Dialogs
• Notifications

────────────────────────────────────────

PERFORMANCE TESTING

Measure:

• Cold startup
• Warm startup
• Booking latency
• Map rendering
• Real-time connection
• Location processing
• Large trip-history rendering
• Memory
• Battery impact

────────────────────────────────────────

DOCUMENTATION

Generate:

• Mobile architecture
• Rider application
• Driver application
• Navigation
• Maps
• Location
• Booking
• Real-time
• Trip lifecycle
• Driver offers
• Driver onboarding
• Payments
• Wallet
• Promotions
• Ratings
• Messaging
• Notifications
• Safety
• Support
• Business rides
• Offline-aware architecture
• Secure storage
• Accessibility
• Localization
• Performance
• Testing

────────────────────────────────────────

PROJECT INDEX

Update the mobile Project Index with:

• Rider screens
• Driver screens
• Navigation
• Features
• Components
• Hooks
• Stores
• Queries
• API integrations
• Maps
• Location
• Real-time
• Booking
• Trips
• Payments
• Wallet
• Promotions
• Ratings
• Messaging
• Notifications
• Safety
• Support
• Business
• Onboarding
• Documents
• Vehicle
• Earnings
• Payouts
• Tests
• Dependencies
• Generated files
• Modified files
• Remaining work
• Current milestone

────────────────────────────────────────

IMPLEMENTATION MILESTONES

MOBILE MILESTONE 1

Expo foundation, navigation, configuration, design system, API client, providers, secure storage, authentication, and connectivity handling.

MOBILE MILESTONE 2

Rider onboarding, profile, destination search, current location, maps, saved places, ride categories, fare estimates, and booking.

MOBILE MILESTONE 3

Real-time matching, driver assignment, live tracking, ETA, active-trip experience, trip state reconciliation, messaging, and safety.

MOBILE MILESTONE 4

Trip history, receipts, payments, wallet, promotions, ratings, support, notifications, and trip sharing.

MOBILE MILESTONE 5

Driver onboarding, documents, verification, vehicles, compliance, availability, and driver home.

MOBILE MILESTONE 6

Driver offers, active driver trips, navigation, trip completion, earnings, incentives, payouts, ratings, and support.

MOBILE MILESTONE 7

Business rides, advanced synchronization, accessibility, localization, theming, performance, battery, and data optimization.

MOBILE MILESTONE 8

Security hardening, offline-aware recovery, integration testing, E2E testing, platform testing, accessibility testing, performance testing, and production readiness.

Each milestone should contain approximately 20–40 files where practical.

Every milestone must compile before proceeding.

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never truncate code.

Never summarize code instead of generating it.

Never generate pseudo-code.

Never generate placeholders.

Never generate TODO implementations.

When modifying an existing file:

1. Provide the exact file path.
2. State why it must change.
3. Provide the complete updated file.

Never regenerate unchanged files.

────────────────────────────────────────

SCOPE RESTRICTION

This volume covers the mobile rider and driver applications and their shared mobile foundations.

Do not implement:

• Backend code
• Web frontend code
• Infrastructure
• Terraform
• Kubernetes
• CI/CD

Do not redesign backend APIs or database structures.

Consume the approved backend contracts exactly.

────────────────────────────────────────

QUALITY BAR

Treat the mobile applications as mission-critical transportation clients supporting:

• Hundreds of millions of riders
• Millions of drivers
• Large real-time traffic
• Continuous driver location
• Real-time trip state
• Multiple network conditions
• Multiple device classes
• Multiple regions
• Financial workflows
• Safety workflows
• Business accounts

Prioritize:

• Booking reliability
• Real-time responsiveness
• Location accuracy
• Battery efficiency
• Data efficiency
• Secure storage
• Privacy
• Accessibility
• Resilience
• Correct state reconciliation
• Maintainability
• Production readiness
