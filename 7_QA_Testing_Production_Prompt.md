You are operating in Senior Engineering Team Mode.

Build the complete production-grade QA, testing, security validation, performance validation, resilience validation, privacy validation, accessibility validation, infrastructure validation, and production-readiness system for an enterprise-scale global ride-hailing, mobility, transportation, and delivery platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

The testing system must validate the established backend, web frontend, mobile applications, infrastructure, real-time location system, dispatch, matching, trip lifecycle, pricing, payments, wallets, driver earnings, payouts, ratings, messaging, notifications, safety, fraud, support, business accounts, analytics, administration, moderation, and disaster-recovery architecture.

Do not redesign the approved architecture.

Do not implement unrelated product features.

────────────────────────────────────────

MISSION

Build a complete quality-engineering system covering:

• Unit testing
• Integration testing
• API testing
• Contract testing
• WebSocket testing
• Event testing
• Queue testing
• Database testing
• PostGIS testing
• Redis testing
• Location testing
• Geospatial testing
• ETA testing
• Dispatch testing
• Matching testing
• Driver-offer testing
• Trip-state testing
• Scheduled-ride testing
• Multi-stop testing
• Shared-ride testing
• Pricing testing
• Surge testing
• Promotion testing
• Payment testing
• Webhook testing
• Refund testing
• Wallet testing
• Earnings testing
• Payout testing
• Ratings testing
• Messaging testing
• Notification testing
• Safety testing
• Trip-sharing testing
• Fraud testing
• Support testing
• Business-account testing
• Analytics testing
• Administration testing
• Moderation testing
• Web frontend testing
• Mobile testing
• Accessibility testing
• Security testing
• Privacy testing
• Abuse testing
• Performance testing
• Load testing
• Stress testing
• Soak testing
• Resilience testing
• Chaos testing
• Disaster-recovery testing
• Backup restoration testing
• Infrastructure testing
• CI/CD validation
• Production smoke testing
• Regression testing
• Release validation
• Production-readiness certification

The final QA system must validate:

• Functional correctness
• Trip-state correctness
• Financial correctness
• Geospatial correctness
• Security
• Privacy
• Availability
• Reliability
• Scalability
• Performance
• Recoverability
• Accessibility
• Maintainability
• Operational readiness

────────────────────────────────────────

TECHNOLOGY STACK

Backend:

• Node.js
• NestJS
• TypeScript
• PostgreSQL
• Prisma
• PostGIS
• Redis
• Kafka or Redpanda
• BullMQ
• OpenSearch/Elasticsearch
• AWS S3
• Payment-provider abstraction
• Maps-provider abstraction
• Notification-provider abstractions

Frontend:

• Next.js
• React
• TypeScript
• Tailwind CSS
• TanStack Query
• Zustand

Mobile:

• React Native
• Expo
• TypeScript
• React Navigation
• TanStack Query
• Zustand

Infrastructure:

• Docker
• Kubernetes
• Helm
• Terraform
• AWS
• GitHub Actions

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

Testing:

• Jest
• Supertest
• React Testing Library
• Playwright
• React Native Testing Library
• Detox or approved mobile E2E framework
• Load-testing tools
• Accessibility testing tools
• Security-scanning tools

────────────────────────────────────────

TESTING PRINCIPLES

Use a layered test strategy.

Do not rely entirely on end-to-end tests.

Use:

• Unit tests for domain logic
• Integration tests for real dependencies
• Contract tests for service boundaries
• API tests for public/internal APIs
• Real-time tests for WebSockets
• End-to-end tests for critical user journeys
• Performance tests for expected scale
• Security tests for attack resistance
• Resilience tests for failure behavior
• Recovery tests for operational readiness

Tests must be deterministic whenever practical.

Avoid:

• Arbitrary sleeps
• Test-order dependencies
• Shared mutable state
• Production data
• Production credentials
• Real payment credentials
• Real sensitive identity documents
• Real customer location histories

────────────────────────────────────────

TEST PYRAMID

UNIT

Broad domain coverage.

INTEGRATION

Real:

• PostgreSQL
• PostGIS
• Redis
• Kafka/Redpanda
• BullMQ
• OpenSearch
• S3 abstractions
• Maps abstractions
• Payment abstractions
• Notification abstractions

CONTRACT

Validate compatibility between:

• Services
• REST APIs
• WebSockets
• Events
• Webhooks

E2E

Validate critical rider, driver, business, support, and admin journeys.

────────────────────────────────────────

IDENTITY TESTING

Validate:

• Registration
• Login
• Logout
• Email verification
• Password reset
• Password change
• Session refresh
• Session expiration
• Session revocation
• Device registration
• Device revocation

Security cases:

• Invalid credentials
• Credential stuffing
• Brute force
• Reset-token replay
• Session replay
• Revoked-session access
• Account takeover

────────────────────────────────────────

AUTHORIZATION TESTING

Validate:

• RBAC
• Resource ownership
• Rider isolation
• Driver isolation
• Business isolation
• Administrative permissions
• Support permissions
• Safety permissions
• Fraud permissions

Test:

• Horizontal privilege escalation
• Vertical privilege escalation
• IDOR
• Cross-user access
• Cross-driver access
• Cross-business access
• Unauthorized location access

────────────────────────────────────────

DRIVER ONBOARDING TESTING

Test:

• Application creation
• Document submission
• Identity verification
• Driver-license verification
• Background-check integration
• Insurance verification
• Vehicle verification
• Approval
• Rejection
• Resubmission
• Expiration
• Suspension
• Reinstatement

Provider cases:

• Timeout
• Duplicate request
• Delayed response
• Invalid result
• Duplicate callback
• Out-of-order callback

────────────────────────────────────────

VEHICLE TESTING

Test:

• Creation
• Update
• Category assignment
• Verification
• Insurance
• Expiration
• Suspension
• Eligibility

Validate category restrictions.

────────────────────────────────────────

LOCATION TESTING

Test:

• Valid GPS
• Invalid GPS
• Out-of-order location
• Duplicate location
• Stale location
• GPS jump
• Impossible velocity
• Clock skew
• Sequence numbers
• Driver reconnect
• Driver disconnect

Validate:

• Freshness
• Accuracy
• Region assignment
• Candidate eligibility

────────────────────────────────────────

AVAILABILITY TESTING

Test:

• Go online
• Go offline
• Heartbeat
• Expiration
• Recovery
• Suspension interaction
• Active-trip interaction

Verify a driver cannot appear available when in an incompatible state.

────────────────────────────────────────

GEOSPATIAL TESTING

Test:

• Nearby-driver search
• Radius queries
• Neighbor-cell expansion
• Geohash/H3
• PostGIS
• Spatial indexes
• Service areas
• Geofences
• Airport zones
• Pickup zones
• Dropoff zones
• Region boundaries

Test edge cases around polygon boundaries.

────────────────────────────────────────

MAPS TESTING

Test:

• Geocoding
• Reverse geocoding
• Places
• Directions
• Routes
• Distance
• Traffic
• ETA

Provider failures:

• Timeout
• Rate limit
• Invalid response
• Outage
• Partial response

Verify provider abstraction behavior.

────────────────────────────────────────

ETA TESTING

Validate:

• Driver-to-pickup ETA
• Pickup ETA
• Trip ETA
• Multi-stop ETA
• Traffic changes
• Route changes
• Stale route
• Provider failure

Do not require exact real-world ETA values in deterministic tests.

Instead validate:

• Correct provider interaction
• Correct update behavior
• Staleness handling
• Bounds
• Cache behavior

────────────────────────────────────────

RIDE REQUEST TESTING

Test:

• Valid request
• Invalid pickup
• Invalid destination
• Unsupported service area
• Unsupported category
• Capacity violation
• Accessibility constraints
• Scheduled time
• Payment-method requirement
• Duplicate request

Verify backend idempotency.

────────────────────────────────────────

DISPATCH TESTING

Test:

• Candidate generation
• Eligibility filtering
• Regional partition
• Neighbor-cell expansion
• ETA integration
• Scoring
• Offer generation
• Offer timeout
• Reassignment
• Dispatch failure

Measure:

• Match latency
• Candidate lookup latency
• Assignment latency

────────────────────────────────────────

MATCHING TESTING

Test:

• Correct candidates
• Hard constraints
• Soft scoring
• Fairness rules
• Accessibility
• Vehicle category
• Service-area rules
• Driver state
• Trip conflicts

Validate that invalid drivers never enter final assignment.

────────────────────────────────────────

MATCHING CONCURRENCY

Simulate:

• Two rides competing for one driver
• Two drivers accepting same assignment
• Driver going offline during offer
• Driver becoming ineligible during matching
• Offer expiration during acceptance
• Duplicate acceptance
• Late acceptance
• Cancellation during assignment

The system must resolve every race deterministically.

────────────────────────────────────────

DRIVER-OFFER TESTING

Test:

• Creation
• Delivery
• Viewed
• Accept
• Reject
• Expiration
• Cancellation
• Retry
• Duplicate response
• Late response

Verify server-authoritative expiration.

────────────────────────────────────────

TRIP STATE TESTING

Test every valid and invalid transition.

Validate:

Requested
→ Searching
→ Assigned
→ Driver En Route
→ Driver Arrived
→ Trip Started
→ Trip In Progress
→ Stop Reached
→ Trip Completed

and:

• Rider canceled
• Driver canceled
• System canceled
• Disputed

Invalid transitions must fail safely.

────────────────────────────────────────

TRIP CONCURRENCY

Test:

• Simultaneous start requests
• Simultaneous cancellation
• Duplicate arrival
• Duplicate completion
• Stop-order conflicts
• Assignment changes
• Stale version updates
• App reconnect with stale local state

────────────────────────────────────────

SCHEDULED-RIDE TESTING

Test:

• Create
• Update
• Cancel
• Reminder
• Pre-dispatch
• Driver assignment
• Driver replacement
• Expiration
• Failure recovery

Test scheduling around:

• Time zones
• Daylight-saving transitions where relevant
• Regional boundaries
• Large request bursts

────────────────────────────────────────

MULTI-STOP TESTING

Test:

• Add stop
• Remove stop
• Reorder
• Arrive
• Complete
• Route recalculation
• ETA recalculation
• Fare recalculation
• Concurrent stop edits

────────────────────────────────────────

SHARED-RIDE TESTING

Test:

• Multiple riders
• Capacity
• Pickup ordering
• Dropoff ordering
• Route detour
• Participant cancellation
• Driver cancellation
• Fare allocation

Validate maximum-detour and capacity constraints.

────────────────────────────────────────

PRICING TESTING

Test:

• Base fare
• Distance
• Time
• Minimum fare
• Fees
• Taxes
• Tolls
• Category
• Accessibility
• Surge
• Promotions

Test exact arithmetic and rounding.

Never use floating-point comparison for money.

────────────────────────────────────────

SURGE TESTING

Test:

• Demand increase
• Supply decrease
• Zone changes
• Category differences
• Caps
• Floors
• Smoothing
• Hysteresis
• Expiration

Validate that surge does not oscillate unexpectedly under noisy data.

────────────────────────────────────────

PROMOTION TESTING

Test:

• Eligibility
• Usage limit
• Customer limit
• Expiration
• Region
• Category
• Minimum fare
• Maximum discount
• Stacking
• Concurrent redemption

Prevent:

• Double redemption
• Negative fare
• Unauthorized use

────────────────────────────────────────

PAYMENT TESTING

Test:

• Payment-method validation
• Authorization
• Capture
• Failure
• Retry
• Timeout
• Cancellation
• Refund
• Partial refund
• Dispute

Never use production financial credentials.

────────────────────────────────────────

WEBHOOK TESTING

Test:

• Signature verification
• Duplicate event
• Replay
• Delayed event
• Out-of-order event
• Unknown event
• Malformed event
• Provider retry

Verify idempotency.

────────────────────────────────────────

REFUND TESTING

Test:

• Full refund
• Partial refund
• Duplicate refund
• Refund after failure
• Provider timeout
• Refund reconciliation

A refund cannot exceed captured funds.

────────────────────────────────────────

WALLET TESTING

Test:

• Credit
• Debit
• Expiration
• Concurrent debit
• Double spend
• Duplicate mutation
• Compensating entry
• Balance projection

The authoritative ledger must remain internally consistent.

────────────────────────────────────────

EARNINGS TESTING

Test:

• Trip earnings
• Tips
• Incentives
• Bonuses
• Adjustments
• Refund impact
• Compensation-version consistency

────────────────────────────────────────

PAYOUT TESTING

Test:

• Payout eligibility
• Available balance
• Payout creation
• Duplicate payout
• Provider timeout
• Provider failure
• Reversal
• Reconciliation

A driver cannot withdraw more than available funds.

────────────────────────────────────────

RATINGS TESTING

Test:

• Eligibility
• Rating window
• Duplicate rating
• Driver-to-rider
• Rider-to-driver
• Aggregation
• Review moderation

Prevent ratings by unauthorized participants.

────────────────────────────────────────

MESSAGING TESTING

Test:

• Conversation creation
• Message creation
• Delivery
• Read state
• Reconnect
• Duplicate message
• Message expiration
• Authorization
• Rate limiting

Verify users cannot access unrelated trip conversations.

────────────────────────────────────────

NOTIFICATION TESTING

Test:

• FCM
• APNS
• Device-token registration
• Token rotation
• Invalid tokens
• Retry
• Deduplication
• In-app notifications
• Email/SMS abstractions
• Deep links

────────────────────────────────────────

SAFETY TESTING

Test:

• Safety incident creation
• Severity
• Escalation
• Evidence references
• Safety action
• Trip sharing
• Share expiration
• Share revocation
• Trusted contacts
• Emergency-assistance boundary

Verify safety data isolation.

────────────────────────────────────────

TRIP-SHARING TESTING

Test:

• Share creation
• Recipient
• Token expiration
• Revocation
• Unauthorized access
• Expired access
• Access after trip completion

────────────────────────────────────────

FRAUD TESTING

Test:

• Fake account signals
• GPS anomalies
• Promo abuse
• Payment anomalies
• Referral abuse
• Fake trips
• Collusion patterns
• Account takeover
• Device anomalies

Test outcomes:

• Allow
• Monitor
• Challenge
• Review
• Restrict
• Block

Avoid making every anomaly an automatic irreversible block.

────────────────────────────────────────

SUPPORT TESTING

Test:

• Case creation
• Assignment
• Priority
• SLA
• Escalation
• Messaging
• Evidence
• Resolution
• Reopen

Verify support agents only see authorized data.

────────────────────────────────────────

BUSINESS ACCOUNT TESTING

Test:

• Organization creation
• Member invite
• Role assignment
• Member removal
• Cost centers
• Spending limits
• Ride policies
• Business trips
• Business receipts
• Organization isolation

Security:

• Cross-business access
• Unauthorized billing access
• Unauthorized policy changes

────────────────────────────────────────

ANALYTICS TESTING

Test:

• Event validation
• Event publishing
• Kafka processing
• Aggregation
• Deduplication
• Retention
• Reporting

Verify analytics failures do not block transactional systems.

────────────────────────────────────────

ADMINISTRATION TESTING

Test:

• User search
• Driver search
• Trip search
• Payment investigation
• Refund actions
• Safety actions
• Fraud actions
• Support operations
• Business administration
• Feature flags
• Configuration
• Audit

Sensitive actions require appropriate permissions.

────────────────────────────────────────

MODERATION TESTING

Test:

• Reports
• Reviews
• Messages
• Safety cases
• Moderation actions
• Appeals
• Resolution
• Reopening

Verify evidence isolation.

────────────────────────────────────────

WEB FRONTEND TESTING

RIDER:

• Registration
• Login
• Destination search
• Map
• Fare estimate
• Booking
• Matching
• Driver tracking
• Active trip
• Completion
• Rating
• Receipt
• Support
• Safety

DRIVER:

• Registration
• Onboarding
• Documents
• Vehicle
• Verification
• Online/offline
• Offers
• Active trip
• Earnings
• Payout

BUSINESS:

• Organization
• Members
• Policy
• Business ride
• Receipts
• Reports

ADMIN:

• Authentication
• Search
• Dispatch operations
• Drivers
• Trips
• Payments
• Safety
• Fraud
• Support
• Configuration
• Audit

────────────────────────────────────────

WEB REAL-TIME TESTING

Validate:

• WebSocket authentication
• Subscription authorization
• Driver tracking
• Trip-state updates
• Offer updates
• Messaging
• Reconnect
• Duplicate events
• Stale events
• Connection draining

────────────────────────────────────────

MOBILE TESTING

RIDER:

• Authentication
• Location permissions
• Destination search
• Maps
• Booking
• Driver assignment
• Tracking
• Messaging
• Safety
• Trip completion
• Payments
• Notifications
• Deep links

DRIVER:

• Onboarding
• Location permissions
• Background location
• Availability
• Offers
• Navigation
• Trip lifecycle
• Earnings
• Payouts
• Notifications
• Safety

────────────────────────────────────────

MOBILE NETWORK TESTING

Simulate:

• No network
• Weak network
• High latency
• Packet loss
• Intermittent connection
• Wi-Fi/cellular transition
• Reconnection

Verify:

• No duplicate ride
• Correct state reconciliation
• Safe retries
• No fabricated state

────────────────────────────────────────

ACCESSIBILITY TESTING

WEB

Target WCAG 2.2 AA.

Test:

• Keyboard navigation
• Screen readers
• Focus management
• Contrast
• Forms
• Dialogs
• Tables
• Charts
• Status updates
• Map alternatives

MOBILE

Test:

• VoiceOver
• TalkBack
• Dynamic Type
• Large text
• Accessible labels
• Touch targets
• Player-free transportation controls
• Map alternatives

────────────────────────────────────────

PRIVACY TESTING

Verify:

• Rider profile isolation
• Driver profile isolation
• Precise location restrictions
• Trip-history privacy
• Payment privacy
• Business-trip isolation
• Safety-data privacy
• Fraud-data privacy
• Support-data privacy

Test:

• Data export
• Data deletion/anonymization
• Retention enforcement

────────────────────────────────────────

SECURITY TESTING

Test against:

• Authentication bypass
• Session hijacking
• Token replay
• IDOR
• Privilege escalation
• SQL injection
• XSS
• CSRF where applicable
• SSRF where applicable
• Path traversal
• Malicious uploads
• Webhook spoofing
• API abuse
• WebSocket abuse
• Credential stuffing
• Rate-limit bypass
• Location scraping
• Financial manipulation
• Payout manipulation

────────────────────────────────────────

LOAD TESTING

Simulate:

• Normal traffic
• Peak traffic
• Burst traffic
• City-level surge in demand
• Major events
• Large driver-online spikes
• Large concurrent trips
• Notification bursts

Measure:

• API throughput
• Matching throughput
• Location throughput
• WebSocket connections
• Payment throughput
• Notification throughput

────────────────────────────────────────

DISPATCH LOAD TESTING

Generate:

• Large ride-request bursts
• Large nearby-driver pools
• High candidate churn
• High acceptance rates
• High rejection rates

Measure:

• Request-to-match latency
• Candidate lookup
• Offer latency
• Assignment latency
• Redis load
• Kafka load

────────────────────────────────────────

LOCATION LOAD TESTING

Simulate:

• Millions of online drivers
• High-frequency GPS updates
• Rapid driver movement
• Region migration
• Reconnect storms

Measure:

• Ingestion throughput
• Redis operations
• WebSocket fan-out
• CPU
• Network
• Memory
• Location freshness

────────────────────────────────────────

WEBSOCKET LOAD TESTING

Test:

• Concurrent rider connections
• Concurrent driver connections
• Subscription churn
• Reconnect storms
• Location fan-out
• Trip-state broadcasts
• Message traffic

Verify backpressure behavior.

────────────────────────────────────────

FINANCIAL LOAD TESTING

Test high-volume:

• Fare calculations
• Payment requests
• Webhooks
• Refunds
• Wallet transactions
• Earnings
• Payouts

Verify transactional integrity under load.

────────────────────────────────────────

STRESS TESTING

Push systems beyond expected limits.

Identify:

• API saturation
• Redis saturation
• PostgreSQL saturation
• Kafka saturation
• WebSocket limits
• Dispatch limits
• Location limits
• Payment limits
• Worker limits

Document:

• Failure point
• Failure mode
• Recovery
• Scaling action

────────────────────────────────────────

SOAK TESTING

Run long-duration tests.

Monitor for:

• Memory leaks
• Connection leaks
• Redis growth
• Kafka consumer lag
• Queue growth
• Database degradation
• WebSocket instability
• Worker degradation
• Log growth
• Storage exhaustion

────────────────────────────────────────

RESILIENCE TESTING

Inject controlled failures into:

• PostgreSQL
• Redis
• Kafka
• BullMQ workers
• OpenSearch
• Maps provider
• Payment provider
• Notification providers
• WebSocket gateways
• Dispatch workers
• Location workers
• Kubernetes nodes
• Availability zones
• Regions

Verify:

• Detection
• Timeout
• Retry
• Fallback
• Degraded operation
• Recovery
• Reconciliation

────────────────────────────────────────

CHAOS TESTING

Test:

• Pod termination
• Node termination
• Network latency
• Packet loss
• Redis restart
• PostgreSQL failover
• Kafka broker failure
• Search failure
• Dispatch-worker failure
• Location-worker failure
• Region failure

Begin in non-production environments.

Only promote validated scenarios under controlled operational procedures.

────────────────────────────────────────

DISASTER-RECOVERY TESTING

Test:

• PostgreSQL restore
• PITR
• Redis recovery
• Kafka recovery
• OpenSearch restore
• S3 recovery
• EKS reconstruction
• Terraform reconstruction
• Regional failover
• Regional failback

Measure actual:

• RTO
• RPO

Compare with approved targets.

────────────────────────────────────────

BACKUP TESTING

Validate restoration of:

• PostgreSQL
• S3
• OpenSearch
• Terraform state
• Critical configuration

A backup is not considered valid without restoration evidence.

────────────────────────────────────────

INFRASTRUCTURE TESTING

Validate:

• Terraform
• Helm
• Kubernetes
• Docker
• IAM
• Security Groups
• NetworkPolicies
• WAF
• Load balancers
• Autoscaling
• TLS
• Backup configuration
• Disaster-recovery configuration

────────────────────────────────────────

CI/CD QUALITY GATES

PULL REQUEST:

• Formatting
• Linting
• Type checking
• Unit tests
• Integration tests
• Contract tests
• Security scans
• Secret scans
• Dependency scans
• Docker validation
• Terraform validation
• Helm validation
• Kubernetes validation

RELEASE:

• Build
• Unit
• Integration
• Contract
• E2E smoke
• Security scan
• Image scan
• Deployment verification
• Production smoke

────────────────────────────────────────

PRODUCTION SMOKE TESTING

After production deployment, validate safely:

• Authentication
• Rider APIs
• Driver APIs
• Location
• Ride request
• Dispatch
• Matching
• Trip-state propagation
• Pricing
• Payment connectivity
• Notifications
• Business APIs
• Support
• Admin APIs

Do not create real financial charges or real customer trips unless the test environment explicitly supports safe synthetic transactions.

────────────────────────────────────────

REGRESSION STRATEGY

Maintain regression suites for all critical domains.

Every defect that reaches production must result in:

• Root-cause analysis
• Regression test
• Documentation
• Appropriate monitoring improvement

────────────────────────────────────────

TEST DATA STRATEGY

Create deterministic factories for:

• Users
• Riders
• Drivers
• Vehicles
• Documents
• Service areas
• Geofences
• Ride requests
• Driver offers
• Trips
• Stops
• Scheduled rides
• Shared rides
• Fares
• Promotions
• Payments
• Refunds
• Wallets
• Earnings
• Payouts
• Ratings
• Messages
• Notifications
• Safety cases
• Fraud cases
• Support cases
• Business accounts

Generate:

• Small fixtures
• Medium datasets
• Large synthetic datasets

────────────────────────────────────────

QUALITY DASHBOARDS

Create dashboards for:

• Test pass rate
• Test duration
• Flaky-test rate
• Coverage
• Regression failures
• Security findings
• Performance regressions
• E2E failures
• Production smoke results

────────────────────────────────────────

QUALITY METRICS

Track:

• Unit coverage
• Integration coverage
• API coverage
• Critical-path E2E coverage
• Security finding count
• Critical defect count
• Flaky-test rate
• Mean test execution time
• Mean time to detect regression
• Mean time to resolve test failures

Do not treat coverage percentage as the only quality metric.

────────────────────────────────────────

RELEASE CERTIFICATION

Define objective release criteria.

A release is production-ready only when:

• Required tests pass
• Blocking security issues are resolved
• Critical-path E2E tests pass
• Performance budgets pass
• Contract compatibility passes
• Infrastructure validation passes
• Smoke tests pass
• Monitoring is operational
• Backup validation is current
• Rollback is available
• Known risks are documented
• Required approvals are complete

────────────────────────────────────────

DOCUMENTATION

Generate:

• QA architecture
• Test strategy
• Test matrix
• Unit-test standards
• Integration-test standards
• Contract-test standards
• API-testing standards
• WebSocket-testing standards
• Event-testing standards
• Queue-testing standards
• Location-testing strategy
• Geospatial-testing strategy
• Dispatch-testing strategy
• Matching-testing strategy
• Trip-state testing
• Pricing-testing strategy
• Payment-testing strategy
• Wallet-testing strategy
• Payout-testing strategy
• Messaging-testing strategy
• Safety-testing strategy
• Fraud-testing strategy
• Support-testing strategy
• Business-testing strategy
• Frontend-testing strategy
• Mobile-testing strategy
• Accessibility-testing guide
• Security-testing guide
• Privacy-testing guide
• Performance-testing guide
• Load-testing guide
• Stress-testing guide
• Soak-testing guide
• Resilience-testing guide
• Chaos-testing guide
• Disaster-recovery testing guide
• Backup-testing guide
• Infrastructure-testing guide
• CI/CD quality gates
• Production-smoke-testing guide
• Regression-testing guide
• Release-certification guide

────────────────────────────────────────

PROJECT INDEX

Maintain the QA Project Index.

Track:

• Test suites
• Unit tests
• Integration tests
• API tests
• Contract tests
• WebSocket tests
• Event tests
• Queue tests
• Database tests
• PostGIS tests
• Redis tests
• Location tests
• Geospatial tests
• ETA tests
• Dispatch tests
• Matching tests
• Offer tests
• Trip tests
• Scheduled-ride tests
• Multi-stop tests
• Shared-ride tests
• Pricing tests
• Surge tests
• Promotion tests
• Payment tests
• Refund tests
• Wallet tests
• Earnings tests
• Payout tests
• Ratings tests
• Messaging tests
• Notification tests
• Safety tests
• Trip-sharing tests
• Fraud tests
• Support tests
• Business tests
• Analytics tests
• Administration tests
• Moderation tests
• Web frontend tests
• Mobile tests
• Accessibility tests
• Security tests
• Privacy tests
• Abuse tests
• Performance tests
• Load tests
• Stress tests
• Soak tests
• Resilience tests
• Chaos tests
• Disaster-recovery tests
• Backup tests
• Infrastructure tests
• CI/CD gates
• Smoke tests
• Regression suite
• Release certification
• Coverage
• Known defects
• Known risks
• Generated files
• Remaining work
• Current milestone
• Production-readiness status

────────────────────────────────────────

IMPLEMENTATION MILESTONES

QA MILESTONE 1

Testing infrastructure, test configuration, factories, fixtures, mocks, helpers, coverage, and reporting.

QA MILESTONE 2

Identity, authentication, authorization, rider/driver onboarding, verification, vehicles, sessions, and devices.

QA MILESTONE 3

Location, availability, PostGIS, Redis geospatial state, service areas, geofences, maps, routing, and ETA.

QA MILESTONE 4

Ride requests, dispatch, matching, driver offers, assignment, trip state, scheduled rides, multi-stop trips, shared rides, and real-time state.

QA MILESTONE 5

Pricing, surge, promotions, payments, webhooks, refunds, wallets, earnings, incentives, payouts, and financial reconciliation.

QA MILESTONE 6

Ratings, reviews, messaging, notifications, safety, trip sharing, blocking, reporting, fraud, and support.

QA MILESTONE 7

Business accounts, business trips, business policies, analytics, administration, moderation, feature flags, configuration, audit, and privacy.

QA MILESTONE 8

Web frontend unit, component, integration, accessibility, real-time, performance, and E2E testing.

QA MILESTONE 9

Mobile unit, component, integration, real-time, location, notification, deep-link, accessibility, offline/network, performance, and E2E testing.

QA MILESTONE 10

Security testing, privacy testing, abuse testing, load/stress/soak testing, resilience, chaos, disaster recovery, backup restoration, infrastructure validation, production smoke testing, release certification, and final Project Index completion.

Each milestone should contain approximately 20–40 files where practical.

Every milestone must produce measurable and verifiable results.

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never truncate code.

Never summarize implementation instead of generating it.

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

This prompt is dedicated to:

• QA
• Testing
• Security validation
• Privacy validation
• Abuse validation
• Performance validation
• Scalability validation
• Resilience validation
• Accessibility validation
• Infrastructure validation
• Disaster-recovery validation
• Backup validation
• CI/CD quality gates
• Regression testing
• Production smoke testing
• Release certification
• Production-readiness validation

Do not redesign the approved architecture.

Do not implement unrelated product features.

────────────────────────────────────────

FINAL QUALITY BAR

The completed mobility platform must provide objective evidence that it can operate as a production-grade global transportation service supporting:

• Hundreds of millions of riders
• Millions of drivers
• Millions of vehicles
• Massive location traffic
• Massive WebSocket traffic
• Large dispatch workloads
• Large financial workloads
• Business accounts
• Safety workflows
• Fraud workflows
• Support workflows
• Multiple regions
• High availability
• Disaster recovery
• Strict privacy
• Strict security

The final system must demonstrate:

• Correctness
• Trip-state integrity
• Financial integrity
• Geospatial correctness
• Security
• Privacy
• Performance
• Scalability
• Reliability
• Resilience
• Observability
• Recoverability
• Accessibility
• Maintainability
• Production readiness
