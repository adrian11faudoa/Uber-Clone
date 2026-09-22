# Uber-Style Global Ride-Hailing & Mobility Platform — Mobile Prompt — Volume 4

## ROLE

You are acting as the complete senior mobile engineering organization responsible for implementing the remaining rider and driver extended mobile product capabilities for this project to production-grade standards.

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

Your responsibility is to inspect the repository and implement the complete extended mobile experience covered by this prompt without breaking existing functionality.

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

1. Inspect the existing mobile applications and shared mobile architecture.
2. Inspect navigation, authentication/session management, secure storage, API client, TanStack Query setup, local state, realtime infrastructure, notifications, deep links, permissions, location/maps, UI primitives, forms, tests, and documentation.
3. Inspect the backend and architecture contracts available in the repository.
4. Determine the actual rider and driver APIs, DTOs, enums, authorization boundaries, pagination conventions, financial contracts, payment-provider contracts, scheduled-trip contracts, ratings/review contracts, notification contracts, messaging contracts, support/safety contracts, and account/security contracts already established.
5. Determine which extended mobile functionality already exists.
6. Preserve compatible working behavior.
7. Reuse the shared mobile foundation and the already implemented rider/driver core journeys.
8. Do not create parallel API clients, authentication systems, realtime systems, map systems, notification systems, or state architectures.
9. Do not invent endpoint paths, payloads, event names, permissions, lifecycle rules, financial states, or mutation semantics where repository contracts already define them.
10. Where a required capability genuinely depends on an absent backend capability, implement the correct typed integration boundary based on the established architecture and document the dependency rather than fabricating backend behavior.

This prompt is independently executable.

Do not depend on another AI conversation or another prompt being pasted into the repository.

---

# TECHNOLOGY BASELINE

Use the repository's established mobile implementation where it is already present and compatible.

The intended mobile stack is:

* React Native
* Expo
* TypeScript

Use the shared mobile foundation and previously implemented mobile architecture for:

* authentication
* secure storage
* API communication
* TanStack Query
* local state
* realtime
* notifications
* deep links
* permissions
* location
* maps
* telemetry
* accessibility
* connectivity
* lifecycle management

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

Implement the remaining **extended rider and driver mobile product experience**, completing the mobile application's major end-user capabilities around:

* rider account/profile/settings
* rider trip history and trip details
* rider payment methods
* rider receipts
* rider promotions
* rider refunds
* rider scheduled trips
* rider ratings/reviews
* rider notifications
* rider messaging
* rider support and safety
* driver profile/settings
* driver onboarding/readiness detail
* driver vehicle information
* driver scheduled-trip management
* driver earnings
* driver earnings history
* driver payouts
* driver ratings/reputation
* driver notifications
* driver messaging
* driver support and safety
* shared account/security/device/session management
* shared offline/realtime/query integration for these extended surfaces

This volume completes the mobile feature set before infrastructure work.

Do not create another mobile volume for these capabilities.

---

# PRIMARY SCOPE

# RIDER EXTENDED EXPERIENCE

## 1. Rider Account and Profile

Implement the rider account/profile experience.

Support, according to backend contracts:

* profile overview
* editable profile fields
* profile photo
* contact information
* localization/language preferences
* timezone-aware settings
* notification preferences
* privacy-facing settings
* account status
* profile validation
* save/cancel
* stale-data handling
* update success/failure
* unauthorized handling

Use the established forms and validation architecture.

Do not expose backend-only metadata.

---

# 2. Rider Security and Device/Session Management

Implement rider-facing account security capabilities supported by the backend.

Where available:

* active sessions/devices
* session/device summary
* session revocation
* security events suitable for user display
* logout-other-devices functionality
* sensitive-operation confirmation
* reauthentication
* expired-session recovery

Never expose:

* access tokens
* refresh tokens
* private credentials
* secret hashes
* provider credentials

Securely clear sensitive state on logout.

---

# 3. Rider Trip History

Implement complete rider trip history.

Support:

* trip list
* cursor pagination
* filtering
* sorting
* date ranges where supported
* status
* service category
* scheduled/immediate distinction
* fare summary
* origin/destination
* search where backend supports it
* pull-to-refresh
* incremental loading
* loading/error/empty states

Do not fetch unbounded historical data.

Use backend pagination.

---

# 4. Rider Trip Detail

Implement detailed historical trip views.

Display, where authorized:

* trip status
* requested time
* pickup
* destination
* driver summary
* vehicle summary
* service category
* trip distance/time
* final fare
* fare breakdown
* payment state
* promotion
* refund state
* receipt
* rating/review status
* support
* safety-related entry points

Support all relevant terminal states.

Do not expose private driver information.

---

# 5. Rider Receipts

Implement receipt access.

Support where backend contracts provide:

* receipt detail
* receipt generation status
* official receipt artifact/access
* fare breakdown
* tax
* discounts
* payment summary
* refund information
* secure download/view
* expiration handling

Use backend-authorized receipt access.

Do not reconstruct official financial documents solely on-device when an authoritative backend artifact exists.

Never expose storage credentials.

---

# 6. Rider Payment Methods

Implement rider payment-method management.

Support, according to provider/backend contracts:

* list payment methods
* masked payment-method details
* add payment method
* set default
* remove
* expiration state
* provider handoff
* verification/action-required state
* empty state
* error/degraded provider state

Never collect or persist raw payment credentials unless an approved provider SDK explicitly requires an ephemeral secure handoff.

Never store:

* raw card numbers
* CVV
* bank credentials
* payment-provider secrets

in ordinary mobile state or general-purpose storage.

---

# 7. Rider Payment State

Implement rider-facing payment state associated with trips and transactions.

Support:

* pending
* authorized
* processing
* captured
* failed
* requires action
* refunded
* partially refunded
* canceled
* other repository-defined states

The UI must remain synchronized with backend state.

Do not claim payment success merely because a client mutation was submitted.

---

# 8. Rider Promotions

Implement rider promotion capabilities.

Support where available:

* available promotions
* code entry
* validation
* eligibility
* applied promotion
* discount
* expiration
* usage status
* invalid state
* expired state
* already-used state
* removal

Promotion validity remains server-authoritative.

Do not reveal internal promotion/risk rules.

---

# 9. Rider Refunds

Implement rider-facing refund capability.

Where supported:

* refund status/history
* refund amount
* currency
* associated trip/payment
* pending
* completed
* partial
* failed
* support escalation

Where refund requests can be initiated:

* validation
* reason/category
* confirmation
* idempotency
* pending state
* duplicate-submission protection
* result reconciliation

Where self-service refund requests are not supported, provide the correct support workflow rather than inventing one.

---

# 10. Rider Scheduled Trips

Implement complete rider scheduled-trip management.

Support:

* upcoming scheduled trips
* scheduled-trip history
* create
* detail
* edit where permitted
* cancel where permitted
* scheduled date/time
* timezone
* pickup
* destination
* service category
* pricing/payment status
* pre-dispatch state
* assignment state where exposed
* expiration/cancellation states

Respect:

* scheduling windows
* modification windows
* cancellation windows
* service-area restrictions
* category restrictions
* payment requirements

Never imply a driver is assigned before backend confirmation.

---

# 11. Rider Ratings and Reviews

Implement rider rating/review workflows.

Support:

* rating eligibility
* rating submission
* optional review
* validation
* duplicate-submission protection
* already-rated state
* expired eligibility
* unavailable state
* retry
* trip-history/detail integration

Do not reveal private reviewer/moderation information.

Do not invent rating-edit semantics if backend does not support them.

---

# 12. Rider Notifications

Implement the rider notification center.

Support:

* notification list
* unread count
* read/unread
* detail
* deep linking
* trip updates
* payment updates
* scheduled-trip updates
* promotion notifications
* support/safety updates
* account notifications

Use the shared push and in-app notification infrastructure.

Do not create another notification subsystem.

---

# 13. Rider Messaging

Implement the rider side of trip-linked messaging.

Support:

* conversation list or active-trip entry
* message history
* text messages
* delivery state
* read state
* realtime delivery
* reconnect
* failed-send retry
* attachment support where already established

Restrict conversations to authorized participants/resources.

Do not persist message contents outside approved application storage policies.

---

# 14. Rider Support

Implement rider support access.

Support:

* support entry
* trip-linked support
* account support
* issue categories
* description
* attachments where supported
* existing case status
* case history
* submission state
* retry
* escalation

Do not build the support-agent interface.

---

# 15. Rider Safety

Implement rider-facing safety entry points supported by the backend/product contracts.

Support where defined:

* safety center
* trip safety actions
* incident report
* emergency/help entry
* safety contacts
* incident status
* evidence submission
* safety follow-up

Do not invent emergency-service integrations.

Do not falsely claim that an action contacts emergency services unless it actually does.

---

# DRIVER EXTENDED EXPERIENCE

## 16. Driver Profile

Implement driver profile/settings.

Support:

* profile details
* profile photo
* contact information
* language/localization
* notification preferences
* user-visible account status
* editable fields supported by backend

Preserve the shared authentication/session model.

---

# 17. Driver Onboarding and Readiness Detail

Implement the extended driver readiness experience.

Support:

* identity verification status
* onboarding checklist/state
* vehicle verification status
* document state
* service-area eligibility
* action-required items
* pending items
* restrictions
* expiry warnings
* approved/eligible state

Where document uploads are supported:

* secure provider/backend upload flow
* progress
* retry
* replacement
* expiration handling
* failure

Never store permanent object-storage credentials on-device.

---

# 18. Driver Vehicle Management

Implement driver-facing vehicle information and management supported by backend contracts.

Support:

* current vehicle
* vehicle details
* service category
* status
* operational eligibility
* inspection status
* document status
* maintenance state where user-visible
* driver-vehicle association
* change vehicle where permitted

Never expose internal fleet/admin metadata.

---

# 19. Driver Scheduled Trips

Implement driver-side scheduled-trip management.

Support:

* upcoming scheduled assignments
* scheduled detail
* pickup
* destination
* scheduled time
* service category
* assignment status
* preparation state
* pre-dispatch
* accept/reject where allowed
* cancellation/exception where allowed
* transition into ordinary pickup/trip workflow

Do not duplicate the dispatch offer implementation.

Reuse shared trip/assignment infrastructure.

---

# 20. Driver Earnings Overview

Implement driver earnings.

Support, according to backend contracts:

* current earnings
* daily/weekly/monthly summary
* trip earnings
* tips
* bonuses/incentives
* platform fees where user-visible
* adjustments
* corrections
* currency
* earnings status

Use backend-authoritative values.

Do not calculate authoritative totals on-device.

---

# 21. Driver Earnings History

Implement paginated earnings history.

Support:

* date filtering
* trip-level detail
* period summaries
* cursor pagination
* loading
* empty
* error
* refresh

Do not fetch unlimited earnings records.

Ensure cache keys are scoped to the authenticated driver.

---

# 22. Driver Payouts

Implement payout information and supported management.

Support where backend/provider contracts permit:

* payout methods
* masked destination information
* payout history
* pending
* processing
* completed
* failed
* payout schedule
* action-required state
* provider setup handoff

Never expose bank credentials or provider secrets.

Do not claim payout completion without authoritative confirmation.

---

# 23. Driver Ratings and Reputation

Implement driver-facing rating information.

Support:

* current rating
* rating summaries
* historical summaries
* eligible review information
* insufficient-data state
* privacy-aware presentation

Do not expose individual rider identities unless explicitly authorized.

Do not reveal hidden risk or enforcement information.

---

# 24. Driver Notifications

Implement driver notification center functionality.

Support:

* unread count
* list
* detail
* read state
* trip updates
* assignments
* scheduled-trip updates
* earnings/payout updates
* account/readiness updates
* support/safety updates
* operational alerts

Use the shared notification system.

---

# 25. Driver Messaging

Complete the driver-facing messaging experience.

Support:

* active-trip conversations
* conversation history
* message delivery/read states
* realtime
* reconnect
* retry
* attachments where supported
* authorized participants

Do not duplicate the rider messaging infrastructure.

---

# 26. Driver Support

Implement driver support.

Support:

* account issues
* trip issues
* earnings issues
* payout issues
* vehicle/eligibility issues
* support-case history
* issue creation
* attachments where supported
* status
* escalation

Use the canonical support contract.

---

# 27. Driver Safety

Implement driver-facing safety functionality.

Support where defined:

* safety center
* trip safety
* emergency/help actions actually implemented by the product
* incident reporting
* incident history/status
* evidence submission
* safety follow-up

Do not fabricate external emergency integrations.

---

# SHARED EXTENDED MOBILE BEHAVIOR

## 28. Shared Account Switching and Role Boundaries

Where the product permits an account to operate as both rider and driver, implement safe role-aware navigation.

Support:

* current role
* permitted role switching
* role-specific navigation
* role-specific cached data
* role-specific permissions
* revalidation after switching

Do not assume the presence of a role in the client means the user is currently authorized to perform role-specific actions.

---

# 29. Session and Cache Isolation

Ensure:

* logout clears user-specific caches
* role switching does not expose stale data
* account changes invalidate sensitive queries
* cached payment/earnings/trip data cannot bleed between accounts
* secure state is removed appropriately

Test transitions such as:

* rider logout → new rider
* rider → driver
* driver → rider
* expired session → reauthentication
* account restriction → restored access

---

# 30. Realtime Extended-State Integration

Integrate extended mobile screens with realtime events where applicable.

Examples:

### Rider

* payment update
* refund update
* scheduled-trip change
* receipt availability
* rating eligibility
* notification
* message

### Driver

* scheduled assignment
* earnings update
* payout update
* rating update
* notification
* message
* readiness/eligibility change

For each event:

* validate
* deduplicate
* reconcile
* update/invalidate the correct query
* recover missed events after reconnect

Do not create duplicated domain caches for each event type.

---

# 31. Pagination and Large-Data Handling

Use backend pagination for:

* trip history
* scheduled-trip history
* earnings
* payouts
* notifications
* messages
* support cases
* other large mobile collections

Support:

* cursor state
* refresh
* incremental loading
* duplicate-page protection
* retry
* end-of-list handling

Do not load unbounded historical datasets.

---

# 32. Offline and Stale-State Policy

Define safe offline behavior for extended screens.

Where appropriate:

* display last known read-only data
* identify stale state
* queue only mutations that the product/backend explicitly supports
* reconcile after reconnect

Do not queue sensitive financial or destructive mutations unless backend semantics explicitly support safe offline submission.

Never present stale financial state as current.

---

# 33. Deep-Linking Across Extended Features

Support deep links from notifications and internal navigation into:

* trip detail
* receipt
* scheduled trip
* payment method
* refund/support case
* rider promotion
* rating
* driver earnings
* payout
* support
* safety
* message conversation

Validate:

* authentication
* role
* resource authorization
* resource existence
* resource lifecycle

Handle expired or inaccessible destinations gracefully.

---

# 34. Forms and Mutation Safety

Use the shared mobile form and validation patterns.

All important mutations should provide:

* validation
* confirmation where necessary
* progress
* success
* failure
* retry
* duplicate-submission protection
* idempotency where required
* concurrency handling
* authoritative refresh

Financial and administrative mutations must not be blindly retried.

---

# 35. Privacy and Sensitive Data Handling

Protect:

* payment data
* financial data
* trip history
* location
* driver/rider information
* message content
* safety data
* identity/verification data

Do not:

* log raw credentials
* log card data
* persist raw tokens outside secure storage
* persist unnecessary precise location
* expose sensitive values in notifications unnecessarily
* include sensitive data in analytics
* retain private evidence outside approved storage boundaries

Use masked presentation for financial/payment information.

---

# 36. Accessibility

Complete accessibility across the extended mobile application.

Cover:

* account forms
* payment methods
* receipts
* trip history
* scheduled trips
* earnings
* payouts
* notifications
* messaging
* support
* safety
* dialogs
* confirmations
* errors
* loading states
* dynamic text

Ensure important state changes have appropriate accessible announcements.

Avoid inaccessible gesture-only workflows.

---

# 37. Performance

Optimize extended mobile experiences for:

* large lists
* infinite scrolling
* notifications
* conversations
* receipt/document loading
* payment-method screens
* scheduled-trip screens
* earnings/payout data
* realtime event bursts
* map/resource lifecycle
* image loading
* memory usage

Use list virtualization.

Bound cached historical data.

Avoid rendering unnecessary financial/history records.

Clean up all subscriptions and listeners.

---

# 38. Testing

Implement meaningful automated tests.

## Unit Tests

Cover:

* profile validation
* payment-state mapping
* refund-state mapping
* promotion-state mapping
* scheduled-trip-state mapping
* rating eligibility
* earnings formatting
* payout-state mapping
* notification routing
* message/realtime reconciliation
* deep-link parsing
* role switching
* permission/state helpers
* cache-isolation helpers

## Component Tests

Cover:

### Rider

* profile
* account/security
* trip history
* trip detail
* receipts
* payment methods
* promotions
* refunds
* scheduled trips
* ratings
* notifications
* messaging
* support
* safety

### Driver

* profile
* readiness
* vehicle
* scheduled trips
* earnings
* payouts
* ratings
* notifications
* messaging
* support
* safety

## Integration Tests

Cover critical flows:

* rider profile update
* rider session/device management
* rider trip-history pagination
* rider receipt retrieval
* payment-method management
* promotion validation
* refund request/state
* scheduled-trip create/edit/cancel
* rider rating
* rider notification navigation
* rider messaging

And:

* driver profile/update
* readiness state
* vehicle information
* scheduled assignment
* earnings retrieval
* payout state
* ratings
* notification navigation
* messaging
* support
* safety

Also test:

* role switching
* logout/cache isolation
* session expiry
* websocket reconnect
* deep links
* offline/recovery
* stale-state reconciliation

Use mocks/test doubles where external providers are unavailable.

Do not claim real payment, push, maps, device, provider, or backend production validation when only mocks were used.

---

# 39. Documentation

Update mobile documentation to describe the completed extended feature set.

Document:

* rider account
* rider history
* payments
* receipts
* promotions
* refunds
* scheduled trips
* ratings
* notifications
* messaging
* support
* safety
* driver profile
* readiness
* vehicle
* scheduled assignments
* earnings
* payouts
* ratings
* notifications
* messaging
* support
* safety
* role boundaries
* cache isolation
* deep linking
* offline behavior
* privacy rules
* testing
* platform limitations

Documentation must reflect actual implementation.

---

# OUT OF SCOPE

This is the final mobile volume.

Do not create another mobile implementation volume for the features in this prompt.

Explicitly out of scope:

* operations/admin mobile application
* fleet-management mobile application
* backend implementation
* database/schema redesign
* dispatch-engine redesign
* payment-provider backend implementation
* routing-provider backend implementation
* analytics-pipeline backend implementation
* infrastructure/Terraform
* Kubernetes/EKS
* AWS provisioning
* CI/CD redesign
* separate mobile QA phase
* separate final-integration phase

Infrastructure work begins in the project's next phase.

---

# IMPLEMENTATION RULES

## Repository First

Inspect the repository before modifying it.

Determine the actual:

* rider mobile implementation
* driver mobile implementation
* shared mobile foundation
* navigation
* API/query architecture
* realtime
* notification system
* forms
* storage
* maps/location
* testing infrastructure

Reuse existing implementations.

## No Parallel Infrastructure

Do not create additional:

* API clients
* query architectures
* authentication services
* websocket clients
* notification managers
* payment clients
* map abstractions
* storage systems
* design systems

when suitable shared infrastructure already exists.

## Backend Contract Discipline

Use established contracts.

Do not invent:

* endpoint paths
* DTOs
* event names
* financial states
* payment semantics
* refund rules
* scheduling rules
* rating rules
* notification payloads
* support workflows

when the repository defines them.

## Financial Security

Never expose or store raw payment credentials.

Use provider/backend-authorized references.

Treat financial state as backend-authoritative.

## State-Machine Discipline

Trip, scheduled-trip, payment, refund, payout, and account state must follow backend contracts.

Do not create client-only authoritative transitions.

## Mutation Discipline

Use idempotency where required.

Never blindly retry sensitive or financial mutations.

## Privacy

Minimize persisted sensitive data.

Clear protected data on logout/account changes as required.

## No Pseudo-Code

Implement real production code.

Do not use:

* placeholders
* TODO implementations
* fake payment success
* fake refund completion
* fake payout completion
* fake scheduled assignments
* fabricated endpoints
* simulated notifications presented as real
* omitted implementations
* “implement similarly”

---

# VALIDATION REQUIREMENTS

Before considering this volume complete:

1. Run formatting checks.
2. Run linting.
3. Run TypeScript/type checks.
4. Run unit tests.
5. Run component tests.
6. Run integration tests.
7. Validate rider account/profile.
8. Validate rider security/session management.
9. Validate rider trip history.
10. Validate rider trip details.
11. Validate receipts.
12. Validate payment-method behavior.
13. Validate payment-state behavior.
14. Validate promotions.
15. Validate refunds.
16. Validate scheduled trips.
17. Validate ratings/reviews.
18. Validate rider notifications.
19. Validate rider messaging.
20. Validate rider support/safety entry points.
21. Validate driver profile.
22. Validate driver readiness/onboarding state.
23. Validate driver vehicle features.
24. Validate driver scheduled trips.
25. Validate driver earnings.
26. Validate driver earnings history.
27. Validate driver payouts.
28. Validate driver ratings.
29. Validate driver notifications.
30. Validate driver messaging.
31. Validate driver support/safety.
32. Validate role switching where supported.
33. Validate cache isolation.
34. Validate logout/session-expiry behavior.
35. Validate realtime extended-state reconciliation.
36. Validate deep links.
37. Validate offline/stale-state behavior.
38. Validate sensitive-data storage/logging boundaries.
39. Validate accessibility checks available in the repository.
40. Validate list performance/virtualization where applicable.
41. Validate production mobile build or strongest available equivalent.
42. Verify no duplicate infrastructure was introduced.
43. Verify no TODO/placeholder production implementation remains.
44. Verify documentation matches implementation.

Where a device, simulator, external provider, cloud service, or other environment dependency prevents validation, perform all repository-side validation that is possible and explicitly report what could not be tested.

Never claim real production/provider/device validation that did not occur.

---

# INTEGRATION CHECK

Before finalizing, verify that the entire mobile application remains one coherent architecture.

Confirm that:

* rider core and extended features use the same authentication/session system
* driver core and extended features use the same authentication/session system
* rider and driver features use the same API client
* server state uses the same query architecture
* realtime uses the shared websocket foundation
* notifications use the shared notification system
* deep links use the shared routing architecture
* payments use the established provider abstraction
* receipts use authorized backend storage/access mechanisms
* scheduled trips reuse the canonical scheduling/trip contracts
* ratings reuse canonical rating contracts
* messaging is shared rather than duplicated
* support and safety entry points use canonical contracts
* role switching cannot leak data across roles
* logout cannot leave sensitive cached state behind
* pagination remains bounded
* realtime events reconcile safely
* mobile lifecycle behavior remains correct
* later infrastructure work can deploy/configure the resulting application without requiring a mobile rewrite

This is the final mobile implementation volume.

Do not leave core mobile product functionality intentionally deferred to another mobile volume.

---

# DEFINITION OF DONE

This volume is complete only when:

### Rider

* account/profile is implemented
* security/session/device controls are implemented where supported
* trip history is implemented
* trip detail is implemented
* receipts are implemented
* payment methods are implemented
* payment states are implemented
* promotions are implemented
* refunds are implemented where supported
* scheduled trips are implemented
* ratings/reviews are implemented
* notifications are implemented
* messaging is implemented
* support is implemented where supported
* safety is implemented where supported

### Driver

* profile is implemented
* readiness/onboarding detail is implemented
* vehicle information/management is implemented where supported
* scheduled trips are implemented
* earnings are implemented
* earnings history is implemented
* payouts are implemented
* ratings are implemented
* notifications are implemented
* messaging is implemented
* support is implemented where supported
* safety is implemented where supported

### Shared

* role boundaries are correct
* cache isolation is correct
* session lifecycle is correct
* deep linking is correct
* realtime synchronization is correct
* pagination is bounded
* offline/stale-state behavior is handled
* privacy/security requirements are addressed
* accessibility requirements are addressed
* performance requirements are addressed
* meaningful tests are implemented
* documentation is updated
* validation has been performed
* actual limitations are documented
* no fake functionality is presented as real
* no placeholders remain
* no unrelated scope was introduced

---

# IMPLEMENTATION REPORT

At the end of execution, provide a concise report containing:

## Files Changed

List created, modified, and removed files.

## Implemented Scope

Summarize all rider and driver extended functionality actually implemented.

## Shared Architecture

Summarize the shared mobile services and abstractions reused across the complete rider and driver experience.

## Security and Privacy

Summarize sensitive-data handling, secure storage, payment protections, role boundaries, and cache/session isolation.

## Validation

Report the exact validation commands executed and their results.

## Limitations

Report only actual device, environment, provider, or contract limitations.

## Follow-Up Dependencies

Report only genuine dependencies that remain for backend/infrastructure work.

Do not invent another mobile phase.

---

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement the complete remaining rider and driver mobile experience defined by this prompt.

Preserve all working behavior that is outside the scope of necessary changes.

Use the repository's actual architecture and contracts as the source of truth.

Reuse the shared mobile foundation and the already implemented rider/driver core journeys.

Do not wait for another prompt.

Do not merely describe the implementation.

Create and modify the real production-grade mobile code, tests, configuration, and documentation required for this scope.

Do not use pseudo-code, placeholders, fabricated APIs, fake payments, fake refunds, fake payouts, fake scheduled assignments, fake ratings, fake notifications, or simulated success presented as real functionality.

Respect actual iOS, Android, Expo, storage, payment-provider, notification, lifecycle, connectivity, and background-execution constraints.

Validate the implementation as thoroughly as the environment permits.

Finish only when this final mobile volume is genuinely implemented and integrated into the repository.
