You are operating in Senior Engineering Team Mode.

Build the production-ready web frontend foundation for an enterprise-scale global ride-hailing, mobility, transportation, and delivery platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

The frontend must consume the approved backend APIs, authentication contracts, authorization model, real-time contracts, trip-state model, pricing contracts, payment contracts, maps integration, notification system, safety system, business-account system, and Project Index.

Do not redesign the backend.

Do not implement backend code.

Do not implement mobile code.

Do not implement infrastructure code.

Do not generate Terraform.

Do not generate Kubernetes manifests.

Do not generate CI/CD workflows.

────────────────────────────────────────

MISSION

Build the production-ready web applications for:

• Riders
• Drivers
• Business users
• Support users
• Operations users
• Administrators

The web platform must support:

RIDER

• Registration
• Login
• Profile
• Saved places
• Ride booking
• Fare estimation
• Ride category selection
• Driver matching
• Driver tracking
• Trip tracking
• Multi-stop rides
• Scheduled rides
• Promotions
• Payment methods
• Wallet
• Receipts
• Trip history
• Ratings
• Reviews
• Support
• Trip sharing
• Safety
• Notifications
• Account settings

DRIVER

• Registration
• Onboarding
• Verification status
• Documents
• Vehicles
• Availability
• Ride offers
• Trip execution
• Navigation
• Earnings
• Incentives
• Payouts
• Ratings
• Support
• Safety
• Notifications

BUSINESS

• Business account
• Members
• Roles
• Policies
• Cost centers
• Business rides
• Receipts
• Billing
• Usage analytics

ADMIN / OPERATIONS

• Riders
• Drivers
• Vehicles
• Trips
• Dispatch
• Matching
• Pricing
• Promotions
• Payments
• Refunds
• Earnings
• Payouts
• Fraud
• Safety
• Support
• Business accounts
• Analytics
• Moderation
• Feature flags
• Configuration
• Audit

────────────────────────────────────────

TECHNOLOGY STACK

Framework:

• Next.js
• React
• TypeScript

Styling:

• Tailwind CSS
• shadcn/ui
• CSS variables

Server State:

• TanStack Query

Client State:

• Zustand

Forms:

• React Hook Form
• Zod

Maps:

• Google Maps JavaScript API or approved abstraction

Charts:

• Recharts

Animation:

• Framer Motion where appropriate

Icons:

• Lucide React

Testing:

• Jest
• React Testing Library
• Playwright
• Accessibility testing tooling

────────────────────────────────────────

FRONTEND ARCHITECTURE

Use:

• Next.js App Router
• Feature-first architecture
• Strict TypeScript
• Server Components where appropriate
• Client Components only when interaction requires them
• Typed API clients
• Explicit domain boundaries
• Reusable design system
• Separation of server state and client state
• Secure authentication handling
• URL-driven state where appropriate

Do not make the entire application a Client Component.

Do not place backend business logic inside components.

Do not use Zustand as the authoritative source for server state.

────────────────────────────────────────

APPLICATION STRUCTURE

Create a scalable structure containing:

app/

features/

components/

layouts/

hooks/

providers/

services/

stores/

lib/

config/

types/

utils/

styles/

public/

assets/

tests/

Separate applications/route groups for:

• Rider
• Driver
• Business
• Administration

Use shared components only where the semantics are genuinely shared.

────────────────────────────────────────

NEXT.JS FOUNDATION

Implement:

• App Router
• Route groups
• Layouts
• Loading states
• Error boundaries
• Not-found pages
• Suspense
• Metadata
• Open Graph foundations
• Middleware
• Authentication-aware routing

Support:

• Public routes
• Authenticated routes
• Rider routes
• Driver routes
• Business routes
• Administrative routes

Navigation is not a security boundary.

────────────────────────────────────────

DESIGN SYSTEM

Build reusable components with shadcn/ui and Tailwind.

Include:

• Button
• Input
• Textarea
• Select
• Checkbox
• Radio
• Switch
• Dialog
• Drawer
• Popover
• Dropdown
• Tooltip
• Tabs
• Card
• Badge
• Avatar
• Breadcrumb
• Table
• Pagination
• Skeleton
• Alert
• Toast
• Progress
• Slider
• Calendar
• Date picker
• Command
• Separator
• Scroll area
• Empty state
• Error state
• Loading state
• Map panel
• Status badge
• Trip timeline
• Fare breakdown
• Data table
• Confirmation dialog

All components must support:

• Keyboard navigation
• Focus management
• Responsive behavior
• Dark mode
• Accessibility

────────────────────────────────────────

THEMING

Support:

• Light
• Dark
• System

Persist the user's theme preference.

Respect:

• Reduced motion
• High contrast
• Browser accessibility preferences

Use centralized design tokens.

────────────────────────────────────────

API CLIENT

Implement a typed API client.

Support:

• Base URL
• Authentication
• Request IDs
• Correlation IDs
• Error normalization
• Timeout
• Cancellation
• Retry where safe
• Pagination
• Cursor pagination
• File-upload authorization
• WebSocket connection support

Do not implement business logic inside the API client.

────────────────────────────────────────

SERVER STATE

Use TanStack Query for:

• Accounts
• Profiles
• Drivers
• Vehicles
• Ride requests
• Trips
• Pricing
• Promotions
• Payments
• Wallet
• Earnings
• Payouts
• Ratings
• Support
• Safety
• Business accounts
• Notifications
• Analytics
• Administration

Implement:

• Query keys
• Mutations
• Infinite queries
• Caching
• Background refetching
• Optimistic updates where safe
• Invalidation
• Retry
• Error handling

────────────────────────────────────────

CLIENT STATE

Use Zustand for client-owned state such as:

• Current booking flow
• Map UI state
• Trip UI state
• Driver availability UI
• Navigation panel
• Selected ride category
• Active support panel
• Notification UI
• Modal state
• Theme
• Local presentation preferences

Do not duplicate authoritative trip state unnecessarily.

────────────────────────────────────────

AUTHENTICATION

Implement:

• Registration
• Login
• Logout
• Email verification
• Password reset
• Password change
• Session restoration
• Session expiration
• Token refresh
• Protected routing

Prepare for:

• OAuth
• MFA
• Passkeys

Never expose secrets unnecessarily to browser JavaScript.

────────────────────────────────────────

RIDER APPLICATION

Create the complete rider-facing web architecture.

Core routes:

• Home
• Book a ride
• Search destination
• Ride estimate
• Ride confirmation
• Matching
• Driver assigned
• Active trip
• Trip complete
• Trip history
• Trip detail
• Payments
• Wallet
• Promotions
• Ratings
• Support
• Safety
• Notifications
• Account
• Settings

────────────────────────────────────────

RIDER HOME

Display:

• Current location
• Destination search
• Saved places
• Recent destinations
• Ride categories
• Promotions
• Scheduled rides
• Active trip if any

Provide clear loading and error states.

────────────────────────────────────────

DESTINATION SEARCH

Implement:

• Search
• Autocomplete
• Places
• Recent destinations
• Saved places
• Map selection
• Current-location selection

Debounce requests.

Cancel stale requests.

Avoid unnecessary map-provider requests.

────────────────────────────────────────

MAP EXPERIENCE

Integrate the approved maps provider abstraction.

Support:

• Current location
• Destination
• Pickup marker
• Driver marker
• Route
• Route alternatives where supported
• Service areas
• Pickup zones
• Airport zones

Never expose provider API secrets that belong on the server.

────────────────────────────────────────

RIDE ESTIMATE

Display:

• Ride categories
• Estimated fare
• Estimated duration
• Estimated distance
• ETA
• Surge indicator where applicable
• Promotion
• Accessibility options

Clearly distinguish:

• Estimate
• Final fare

Do not calculate the authoritative fare independently.

────────────────────────────────────────

RIDE BOOKING

Implement booking flow:

Destination
→ Ride category
→ Fare estimate
→ Payment method
→ Promotion
→ Confirmation

Support:

• Immediate rides
• Scheduled rides
• Multi-stop rides where supported

Prevent accidental duplicate submissions.

────────────────────────────────────────

RIDE REQUEST STATES

Display backend states such as:

• Created
• Searching
• Driver Assigned
• Driver En Route
• Driver Arrived
• Trip Started
• Trip In Progress
• Trip Completed
• Canceled
• Failed

Do not invent client-only authoritative states.

────────────────────────────────────────

MATCHING EXPERIENCE

During matching display:

• Searching animation
• Ride category
• Estimated price
• Cancellation option
• Approximate wait time

Handle:

• No driver available
• Matching timeout
• Retry
• System cancellation

────────────────────────────────────────

DRIVER ASSIGNED

Display:

• Driver name
• Driver rating
• Vehicle
• Vehicle color
• License plate
• Driver photo where permitted
• Pickup ETA
• Driver location
• Contact/messaging controls where supported
• Safety controls

────────────────────────────────────────

ACTIVE TRIP

Display:

• Driver location
• Route
• Current ETA
• Destination
• Stops
• Trip status
• Driver/vehicle information
• Share trip
• Safety tools
• Messaging
• Cancellation where allowed

Use real-time updates.

Do not poll aggressively when WebSockets provide the needed state.

────────────────────────────────────────

REAL-TIME CLIENT ARCHITECTURE

Implement WebSocket/Socket.IO integration for:

• Ride matching
• Driver assignment
• Driver location
• ETA
• Trip status
• Messages
• Notifications

Support:

• Authentication
• Reconnection
• Connection status
• Event validation
• Duplicate event handling
• Ordering where required

The client must tolerate:

• Disconnect
• Reconnect
• Delayed events
• Duplicate events
• Stale events

────────────────────────────────────────

DRIVER LOCATION UI

Display authorized driver location.

Support:

• Smooth marker transitions
• Stale location indicators
• Reconnection handling
• Map recenter
• Manual map movement

Do not create misleading movement when location updates are stale.

────────────────────────────────────────

TRIP COMPLETION

Display:

• Final fare
• Fare breakdown
• Payment status
• Promotion
• Tip
• Receipt
• Rating
• Review
• Support

────────────────────────────────────────

TRIP HISTORY

Implement:

• Trip list
• Trip detail
• Date filters
• Search
• Fare
• Payment status
• Receipt
• Driver
• Vehicle
• Pickup
• Destination

Use cursor pagination.

────────────────────────────────────────

PAYMENTS

Support:

• Payment methods
• Add payment method
• Remove payment method
• Default payment method
• Payment status
• Failed payment recovery
• Receipts
• Refund status

Use approved payment-provider UI/components where card entry is required.

Never handle raw payment credentials unnecessarily.

────────────────────────────────────────

WALLET

Display:

• Balance
• Promotional credits
• Refund credits
• Expiration
• Transaction history

Do not calculate wallet balance independently from backend data.

────────────────────────────────────────

PROMOTIONS

Support:

• Promo code entry
• Eligibility state
• Discount preview
• Redemption
• Expiration
• Usage status

Display server-authoritative eligibility.

────────────────────────────────────────

SCHEDULED RIDES

Support:

• Create
• View
• Edit where supported
• Cancel
• Driver assignment
• Reminder
• Status

Clearly distinguish scheduled rides from active trips.

────────────────────────────────────────

MULTI-STOP RIDES

Support:

• Add stop
• Remove stop
• Reorder stops
• View route
• Updated ETA
• Updated fare estimate

Handle server conflicts.

────────────────────────────────────────

SAFETY

Create rider safety UI for:

• Trip sharing
• Trusted contacts
• Emergency-assistance action
• Safety incident reporting
• Driver/vehicle information
• Safety check-ins where supported

Do not present software as guaranteeing physical safety.

────────────────────────────────────────

TRIP SHARING

Support:

• Share trip
• Select contact/channel
• Display share status
• Revoke share

Use backend-generated authorization.

Do not generate permanent public access links on the client.

────────────────────────────────────────

RATINGS AND REVIEWS

Implement:

• Driver rating
• Optional review
• Structured feedback
• Submit
• Rating history where allowed

Prevent duplicate UI submissions.

────────────────────────────────────────

SUPPORT

Implement:

• Help center
• Trip-specific support
• Payment support
• Lost item
• Safety support
• Account support
• Case status
• Case messaging

Display backend-authoritative case states.

────────────────────────────────────────

DRIVER APPLICATION

Create the driver-facing web application.

Routes:

• Dashboard
• Onboarding
• Verification
• Documents
• Vehicle
• Availability
• Ride offers
• Active trip
• Earnings
• Incentives
• Payouts
• Ratings
• Support
• Safety
• Account

────────────────────────────────────────

DRIVER ONBOARDING

Implement:

• Personal information
• Documents
• Verification status
• Vehicle
• Insurance
• Compliance
• Application progress

Show:

• Draft
• Submitted
• Pending
• Approved
• Rejected
• Resubmission required

Do not expose raw provider verification data unnecessarily.

────────────────────────────────────────

DOCUMENT UPLOADS

Support:

• Upload authorization
• Upload progress
• File validation
• Preview where appropriate
• Replace
• Expiration
• Verification status

Use signed upload flows.

Never expose raw storage credentials.

────────────────────────────────────────

DRIVER DASHBOARD

Display:

• Online/offline state
• Today's trips
• Earnings
• Incentives
• Rating
• Vehicle
• Notifications
• Support
• Verification alerts

────────────────────────────────────────

DRIVER AVAILABILITY

Implement:

• Go online
• Go offline
• Current status
• Connection status
• Location status
• Region/service area

Provide clear feedback if the driver is not eligible to go online.

────────────────────────────────────────

RIDE OFFERS

Display:

• Pickup
• Estimated distance
• Estimated ETA
• Ride category
• Passenger count where authorized
• Accessibility requirements where permitted
• Offer expiration countdown

Support:

• Accept
• Reject

Prevent duplicate actions.

────────────────────────────────────────

ACTIVE DRIVER TRIP

Display:

• Pickup
• Destination
• Stops
• Rider information permitted by policy
• Navigation
• Trip status
• Arrival
• Start
• Stop completion
• Complete

Use real-time trip state.

────────────────────────────────────────

DRIVER EARNINGS

Display:

• Daily earnings
• Weekly earnings
• Trip breakdown
• Incentives
• Tips
• Adjustments
• Pending earnings
• Available balance

Use server data.

────────────────────────────────────────

DRIVER PAYOUTS

Support:

• Payout method
• Available balance
• Payout request
• Payout status
• Payout history
• Failed payout handling

Never assume a payout succeeded from the UI submission alone.

────────────────────────────────────────

DRIVER RATINGS

Display:

• Overall rating
• Rating trends
• Eligible feedback
• Rating count

Do not expose unauthorized rider information.

────────────────────────────────────────

BUSINESS APPLICATION

Implement business-user web interfaces.

Support:

• Business dashboard
• Members
• Roles
• Policies
• Cost centers
• Ride history
• Spending
• Receipts
• Billing
• Reports
• Settings

────────────────────────────────────────

BUSINESS POLICY UI

Display and manage, when authorized:

• Allowed ride categories
• Spending limits
• Geographic restrictions
• Service hours
• Approval requirements
• Payment policy

Use backend validation.

────────────────────────────────────────

ADMINISTRATION

Implement an administrative web application.

Sections:

• Dashboard
• Riders
• Drivers
• Vehicles
• Trips
• Dispatch
• Pricing
• Promotions
• Payments
• Refunds
• Wallets
• Earnings
• Payouts
• Ratings
• Reviews
• Messaging
• Safety
• Fraud
• Support
• Business
• Analytics
• Moderation
• Feature flags
• Configuration
• Audit

────────────────────────────────────────

ADMIN DASHBOARD

Display operational metrics:

• Ride requests
• Active trips
• Drivers online
• Matching rate
• Match latency
• Cancellation
• Completion
• Payment failures
• Safety incidents
• Fraud alerts
• Support backlog

Use charts and tables.

────────────────────────────────────────

DISPATCH OPERATIONS

Provide operational visualization of:

• Active ride requests
• Matching
• Driver supply
• Regional demand
• Active trips
• Assignment failures

Do not allow ordinary administrators to arbitrarily manipulate dispatch state.

────────────────────────────────────────

TRIP ADMINISTRATION

Support authorized users:

• Search trip
• View trip
• View timeline
• View assignment
• View fare
• View payment reference
• View support cases
• View safety state where authorized

High-sensitivity data must be permission-restricted.

────────────────────────────────────────

DRIVER ADMINISTRATION

Support:

• Search drivers
• View onboarding
• Verify documents
• View vehicles
• View eligibility
• Suspend
• Reinstate

Sensitive verification information must be restricted.

────────────────────────────────────────

FRAUD UI

Support:

• Risk cases
• Risk score reference where authorized
• Signals
• Decision
• Case state
• Evidence
• Appeals

Do not expose sensitive fraud models to unauthorized users.

────────────────────────────────────────

SAFETY ADMINISTRATION

Support:

• Safety incidents
• Severity
• Assignment
• Evidence
• Escalation
• Resolution
• Audit

Restrict precise location and sensitive evidence.

────────────────────────────────────────

MODERATION

Support:

• Reports
• Reviews
• Messages
• Cases
• Evidence
• Actions
• Appeals

Only expose content needed for moderation.

────────────────────────────────────────

FEATURE FLAGS

Create administrative UI for:

• Feature list
• Rollout percentage
• Region
• Driver/rider targeting
• Environment
• Kill switch
• History

Feature flag evaluation remains backend-authoritative.

────────────────────────────────────────

SYSTEM CONFIGURATION

Support authorized administrators with:

• Configuration list
• Search
• Editing
• Version history
• Approval
• Activation
• Rollback

Never expose secrets.

────────────────────────────────────────

AUDIT

Implement:

• Audit search
• Filters
• Actor
• Action
• Resource
• Time
• Region
• Result

Use server-side pagination.

Do not allow ordinary administrators to modify audit records.

────────────────────────────────────────

ACCESSIBILITY

Target WCAG 2.2 AA.

Implement:

• Semantic HTML
• Keyboard navigation
• Focus management
• Screen readers
• Accessible maps alternatives
• Accessible forms
• Accessible dialogs
• Accessible tables
• Accessible charts
• Accessible status indicators

Critical trip information must not be communicated visually only.

────────────────────────────────────────

RESPONSIVE DESIGN

Support:

• Desktop
• Tablet
• Mobile web

Prioritize responsive layouts for:

• Booking
• Active trip
• Maps
• Driver trip screens
• Tables
• Admin dashboards

────────────────────────────────────────

INTERNATIONALIZATION

Support:

• Multiple languages
• Locale persistence
• Currency formatting
• Date/time formatting
• Number formatting
• Relative time
• RTL

Do not hard-code customer-facing strings throughout feature modules.

────────────────────────────────────────

SEO

Optimize public pages where appropriate:

• Service-area landing pages
• Public help pages
• Public business information
• Public support content

Never index:

• Private trips
• Rider accounts
• Driver accounts
• Business private data
• Administrative pages
• Sensitive support content

────────────────────────────────────────

PERFORMANCE

Optimize:

• Booking flow
• Map rendering
• Search
• Active-trip updates
• Trip history
• Driver dashboard
• Admin tables
• Analytics

Use:

• Server Components
• Suspense
• Code splitting
• Dynamic imports
• Virtualized tables/lists
• Query caching
• Request cancellation
• Image optimization

────────────────────────────────────────

SECURITY

Implement:

• Protected routes
• Permission-aware navigation
• Safe URL handling
• Safe rendering
• Sensitive-data masking
• Secure payment integrations
• Secure report downloads
• WebSocket authentication
• Safe handling of temporary trip-share access

Frontend authorization is never the final security boundary.

────────────────────────────────────────

ERROR HANDLING

Handle:

• Authentication failure
• Session expiration
• Ride request failure
• Matching failure
• Driver assignment failure
• Map-provider failure
• Payment failure
• Promotion failure
• Trip-state conflict
• WebSocket disconnect
• Support failure
• Business-policy rejection

Provide clear recovery actions.

────────────────────────────────────────

TESTING

UNIT TESTS

Test:

• Booking state
• Trip-state presentation
• Fare display
• Validation
• Permission-aware UI
• Formatting
• Utilities

COMPONENT TESTS

Test:

• Booking
• Map panels
• Fare breakdown
• Driver offers
• Active trip
• Trip history
• Payments
• Ratings
• Support
• Business
• Admin

INTEGRATION TESTS

Test:

• API client
• Authentication
• TanStack Query
• WebSockets
• Booking flow
• Trip state
• Payments
• Support

END-TO-END TESTS

RIDER:

• Register
• Search destination
• Request ride
• Matching
• Driver assignment
• Active trip
• Completion
• Rating
• Receipt
• Support

DRIVER:

• Register
• Onboarding
• Verification
• Go online
• Receive offer
• Accept
• Start trip
• Complete trip
• Earnings
• Payout

BUSINESS:

• Create organization
• Invite member
• Configure policy
• Book business ride
• View receipt

ADMIN:

• Login
• Search trip
• Manage driver
• Review safety
• Review fraud
• Manage promotion
• Audit

ACCESSIBILITY TESTS

Test:

• Keyboard navigation
• Screen readers
• Forms
• Maps alternatives
• Dialogs
• Tables
• Charts

PERFORMANCE TESTS

Test:

• Booking
• Map rendering
• Active trip
• Trip history
• Driver dashboard
• Admin dashboards

────────────────────────────────────────

DOCUMENTATION

Generate:

• Web architecture
• Rider application
• Driver application
• Business application
• Administration application
• Booking UX
• Map UX
• Real-time UX
• Trip-state UX
• Driver-offer UX
• Pricing UX
• Payment UX
• Safety UX
• Support UX
• Business UX
• Admin UX
• Accessibility
• Localization
• Security
• Performance
• Testing

────────────────────────────────────────

PROJECT INDEX

Update the frontend Project Index with:

• Applications
• Routes
• Features
• Components
• Layouts
• Hooks
• Stores
• Queries
• API integrations
• WebSocket integrations
• Maps
• Rider flows
• Driver flows
• Business flows
• Admin flows
• Payments
• Safety
• Support
• Analytics
• Tests
• Dependencies
• Generated files
• Modified files
• Remaining work
• Current milestone

────────────────────────────────────────

IMPLEMENTATION MILESTONES

FRONTEND MILESTONE 1

Next.js foundation, route architecture, design system, API client, providers, authentication, theme, error handling, and configuration.

FRONTEND MILESTONE 2

Rider account, profile, destination search, maps foundation, saved places, ride-category selection, fare estimates, and booking flow.

FRONTEND MILESTONE 3

Real-time matching, driver assignment, active-trip map, trip state, ETA, driver details, messaging, safety, and trip sharing.

FRONTEND MILESTONE 4

Trip history, receipts, payments, wallet, promotions, ratings, reviews, support, and notifications.

FRONTEND MILESTONE 5

Driver onboarding, document workflows, vehicle management, verification status, availability, and driver dashboard.

FRONTEND MILESTONE 6

Driver offers, active trips, navigation integration, trip completion, earnings, incentives, ratings, payouts, and support.

FRONTEND MILESTONE 7

Business accounts, members, roles, policies, cost centers, business rides, receipts, billing, and analytics.

FRONTEND MILESTONE 8

Administration, dispatch operations, trip management, driver management, payments, fraud, safety, support, moderation, and audit.

FRONTEND MILESTONE 9

Feature flags, dynamic configuration, advanced analytics, accessibility, localization, SEO, responsive optimization, and security hardening.

FRONTEND MILESTONE 10

Complete integration testing, E2E testing, real-time testing, accessibility testing, performance testing, security testing, and production readiness.

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

This volume covers the production web frontend.

Do not implement:

• Backend code
• Mobile code
• Infrastructure
• Terraform
• Kubernetes
• CI/CD

Consume the established backend contracts exactly.

Do not redesign APIs or database structures.

────────────────────────────────────────

QUALITY BAR

Treat the web platform as a production mobility application supporting:

• Hundreds of millions of riders
• Millions of drivers
• Massive ride-request traffic
• Real-time maps
• Real-time driver tracking
• Large trip histories
• Business customers
• Financial workflows
• Safety workflows
• Fraud workflows
• Multiple regions
• Multiple languages
• Strict accessibility
• Strict privacy
• Strict security

Prioritize:

• Booking reliability
• Real-time responsiveness
• Map performance
• Secure data handling
• Correct trip-state presentation
• Payment correctness
• Safety UX
• Accessibility
• Responsive design
• Maintainability
• Scalability
• Production readiness
