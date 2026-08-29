You are operating in Senior Engineering Team Mode.

Complete the remaining enterprise architecture for a production-ready global ride-hailing, mobility, transportation, and delivery platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

Use the approved architecture as the source of truth.

Do not restart the architecture.

Do not implement backend code.

Do not implement frontend code.

Do not implement mobile code.

Do not generate infrastructure implementation files.

Do not generate Dockerfiles.

Do not generate Kubernetes manifests.

Do not generate Terraform files.

Do not generate application source code.

Produce architecture, specifications, contracts, diagrams, schemas, engineering decisions, security models, operational strategies, and implementation guidance only.

────────────────────────────────────────

VOLUME 2 OBJECTIVE

Complete the remaining enterprise architecture for:

1. Advanced dispatch
2. Matching optimization
3. Real-time location
4. Geospatial indexing
5. ETA and routing
6. Dynamic pricing
7. Surge
8. Fare calculation
9. Scheduled rides
10. Multi-stop trips
11. Shared rides
12. Airport operations
13. Business accounts
14. Wallets
15. Driver earnings
16. Driver incentives
17. Driver payouts
18. Payments
19. Refunds
20. Ratings and reviews
21. Messaging
22. Notifications
23. Safety
24. Trip sharing
25. Fraud and risk
26. Identity verification
27. Driver verification
28. Vehicle verification
29. Support
30. Analytics
31. Event-driven architecture
32. Multi-region architecture
33. Disaster recovery
34. Security architecture
35. Privacy
36. Observability
37. Capacity planning
38. Failure scenarios
39. Testing strategy
40. Administrative architecture
41. Backend implementation roadmap
42. Complete Project Index

────────────────────────────────────────

ADVANCED DISPATCH ARCHITECTURE

Complete the dispatch architecture for extremely high request volumes.

Define the dispatch pipeline:

Ride Request
→ Request Validation
→ Service Area Validation
→ Candidate Generation
→ Eligibility Filtering
→ ETA Calculation
→ Ranking
→ Driver Offer
→ Driver Response
→ Temporary Reservation
→ Assignment
→ Trip

Define:

• Regional dispatch cells
• Dispatch ownership
• Request partitioning
• Driver candidate pools
• Candidate refresh
• Offer batching
• Offer timeout
• Retry
• Reassignment
• Cancellation
• Backpressure
• Load shedding

Avoid a single global dispatch queue.

────────────────────────────────────────

DISPATCH PARTITIONING

Partition dispatch by appropriate dimensions such as:

• Region
• City
• Service area
• Geohash
• Operational zone

Define how partitions handle:

• Boundary crossings
• Driver movement
• Rider movement
• Region changes
• Zone saturation
• Failover

Avoid globally serialized matching.

────────────────────────────────────────

MATCHING OPTIMIZATION

Design an extensible matching architecture.

Separate:

• Candidate generation
• Hard constraints
• Soft scoring
• Ranking
• Offer strategy
• Acceptance modeling
• Assignment

Hard constraints may include:

• Driver availability
• Vehicle category
• Driver eligibility
• Passenger capacity
• Accessibility
• Service area
• Regulatory requirements

Soft signals may include:

• Pickup ETA
• Distance
• Predicted acceptance
• Trip direction
• Driver preferences
• Rider preferences
• Supply balancing
• Service quality

Do not encode all matching logic into one monolithic function.

────────────────────────────────────────

MATCHING FAIRNESS

Design configurable fairness controls for dispatch.

Consider:

• Driver opportunity
• Supply balancing
• Acceptance behavior
• Service quality
• Regulatory constraints

Do not create discriminatory or hidden rules.

Matching decisions must remain explainable at an operational level.

────────────────────────────────────────

DRIVER OFFER OPTIMIZATION

Support:

• Sequential offers
• Batched offers
• Parallel offers where justified

Define trade-offs between:

• Match latency
• Driver acceptance
• Duplicate offers
• Driver experience
• Assignment reliability

Prevent multiple drivers from believing they simultaneously own the same trip.

────────────────────────────────────────

REAL-TIME LOCATION ARCHITECTURE

Complete high-throughput location handling.

Support:

• Driver GPS updates
• Rider trip location
• Heartbeats
• Accuracy
• Timestamp
• Heading
• Speed
• Altitude where appropriate
• Battery-awareness signals where appropriate

Define:

• Update frequency
• Compression
• Validation
• Filtering
• Sampling
• Regional processing
• Retention

Do not persist every GPS point permanently.

────────────────────────────────────────

LOCATION STREAM PROCESSING

Design:

Location Update
→ Validation
→ Region Routing
→ Ephemeral State
→ Relevant Subscribers
→ Analytics Stream

Define handling for:

• Out-of-order points
• Duplicates
• Stale points
• Impossible movement
• GPS jumps
• Reconnects
• Device clock skew

────────────────────────────────────────

GEOHASH / SPATIAL INDEXING

Evaluate spatial indexing options:

• Redis GEO
• Geohash
• H3
• PostGIS
• Provider geospatial APIs

Choose appropriate technology for:

• Nearby-driver discovery
• Service zones
• Historical analysis
• Geofencing
• Heatmaps

Do not force one spatial index technology onto every workload.

────────────────────────────────────────

LOCATION PRIVACY

Define visibility by trip state:

Before assignment
→ Limited/obfuscated visibility

During driver arrival
→ Authorized location visibility

During trip
→ Full authorized tracking

After trip
→ Restricted/expired access

Define:

• Data retention
• Access control
• Audit
• Approximation
• Deletion

Administrative location access must be tightly controlled.

────────────────────────────────────────

ROUTING ARCHITECTURE

Design provider abstraction for:

• Route calculation
• Route alternatives
• Distance
• Travel time
• Traffic
• Waypoints
• Route matching

Support:

• Google Maps
• Future alternative providers

Do not couple core business logic to provider-specific response formats.

────────────────────────────────────────

ETA ENGINE

Create an ETA architecture supporting:

• Driver-to-pickup ETA
• Pickup ETA
• Destination ETA
• Multi-stop ETA

Combine:

• Map-provider routing
• Real-time driver location
• Traffic
• Historical estimates where available
• Route changes

Define:

• Refresh interval
• Cache
• Staleness threshold
• Fallback
• Provider timeout

────────────────────────────────────────

AIRPORT ARCHITECTURE

Support airport-specific operations.

Define:

• Airport zones
• Pickup zones
• Dropoff zones
• Queue zones
• Driver staging
• Geofence rules
• Terminal mapping
• Regulatory restrictions

Define airport-specific dispatch constraints.

Do not hard-code one airport's rules into the core domain.

────────────────────────────────────────

SCHEDULED RIDE ARCHITECTURE

Complete:

• Scheduling
• Reservation
• Reminder
• Driver assignment
• Pre-dispatch
• Reassignment
• Cancellation
• Expiration

Define:

• Reservation window
• Driver commitment
• Capacity management
• Failure recovery

Avoid reserving drivers indefinitely.

────────────────────────────────────────

MULTI-STOP ARCHITECTURE

Support:

• Add stop
• Remove stop
• Reorder stop
• Stop arrival
• Stop departure
• Route recalculation
• ETA recalculation
• Fare recalculation

Define which changes require rider confirmation.

────────────────────────────────────────

SHARED-RIDE ARCHITECTURE

Complete shared rides.

Support:

• Ride matching
• Shared vehicle
• Multiple riders
• Pickup ordering
• Dropoff ordering
• Capacity
• Fare allocation
• Dynamic changes

Define:

• Maximum detour
• Maximum passenger count
• Shared-route constraints
• Cancellation behavior

Keep standard trips independent of shared-trip complexity.

────────────────────────────────────────

PRICING ENGINE

Complete the pricing architecture.

Separate:

• Pricing rules
• Fare estimation
• Fare calculation
• Surge
• Promotions
• Taxes
• Fees
• Tolls

Support versioned pricing policies.

A trip should retain the pricing rules applicable to that trip.

────────────────────────────────────────

FARE CALCULATION

Define deterministic calculation:

Base

+ Distance
+ Time
+ Booking/Service Fees
+ Tolls
+ Taxes
+ Surge
  − Promotions
+ Optional Tip

Use exact monetary arithmetic.

Support:

• Currency
• Localization
• Rounding rules
• Minimum fare
• Maximum fare where required

────────────────────────────────────────

PRICING VERSIONING

Every fare should preserve:

• Pricing version
• Fare components
• Surge multiplier
• Currency
• Tax assumptions
• Promotion references
• Calculation timestamp

Historical fares must remain reconstructable.

────────────────────────────────────────

SURGE ENGINE

Complete surge architecture.

Inputs:

• Demand
• Supply
• Active trips
• Driver availability
• Request rate
• Geographic zone
• Time
• Service category

Outputs:

• Surge multiplier
• Confidence
• Effective period
• Zone
• Pricing version

Define:

• Caps
• Floors
• Smoothing
• Hysteresis
• Update frequency
• Regulatory rules

Avoid unstable oscillations.

────────────────────────────────────────

PROMOTIONS ENGINE

Complete promotion architecture.

Support:

• Promo codes
• Campaigns
• Eligibility
• First-ride promotion
• Referral promotion
• Geographic promotions
• Category promotions
• Time-window promotions
• Usage limits
• Customer limits

Prevent:

• Double redemption
• Promo stacking where prohibited
• Negative fare
• Race-condition redemption

────────────────────────────────────────

PAYMENT ARCHITECTURE

Complete payment flow:

Ride Request
→ Payment Method Validation
→ Authorization
→ Trip
→ Fare Finalization
→ Capture
→ Receipt

Support:

• Card
• Wallet
• Cash where supported
• Business payment
• Promotional credits

Separate payment state from trip state.

────────────────────────────────────────

PAYMENT STATE MACHINE

Support:

• Created
• Requires Action
• Authorized
• Capturing
• Captured
• Failed
• Canceled
• Partially Refunded
• Refunded
• Disputed

Define valid transitions.

Payments must be idempotent.

────────────────────────────────────────

PAYMENT WEBHOOKS

Support:

• Signature verification
• Event persistence
• Duplicate detection
• Replay protection
• Idempotent processing
• Retry
• Reconciliation

Never trust client-side payment state as final.

────────────────────────────────────────

REFUNDS

Support:

• Full refund
• Partial refund
• Cancellation refund
• Support refund
• Promotional refund
• Disputed refund

Track:

• Amount
• Currency
• Reason
• Actor
• Provider reference
• Timestamp

────────────────────────────────────────

WALLET ARCHITECTURE

Create a wallet ledger supporting:

• Promotional credits
• Refund credits
• Business credits
• Stored-value credits where legally supported

Use immutable entries.

Define:

• Credit
• Debit
• Expiration
• Restrictions
• Available balance
• Pending balance

Redis must never be the authoritative ledger.

────────────────────────────────────────

DRIVER EARNINGS

Support:

• Trip earnings
• Base earnings
• Incentives
• Bonuses
• Tips
• Fees
• Adjustments
• Refund effects

Use immutable financial ledger entries.

────────────────────────────────────────

DRIVER INCENTIVES

Support:

• Quest-based incentives
• Time-based incentives
• Location-based incentives
• Trip-count incentives
• Guaranteed earnings where supported

Define:

• Eligibility
• Progress
• Completion
• Payout
• Expiration

Do not hard-code incentive rules into driver logic.

────────────────────────────────────────

DRIVER PAYOUTS

Support:

• Available balance
• Pending balance
• Scheduled payout
• Instant payout where supported
• Provider payout
• Failed payout
• Reversal
• Reconciliation

Prevent:

• Duplicate payout
• Over-withdrawal
• Negative available balance

────────────────────────────────────────

RATINGS

Support:

• Rider rates driver
• Driver rates rider
• Numeric rating
• Structured feedback
• Rating window
• Eligibility

Prevent duplicate ratings.

Define aggregation and fraud controls.

────────────────────────────────────────

MESSAGING

Complete trip-scoped rider-driver messaging.

Support:

• Text
• Read state
• Attachments where required
• Safety filtering
• Trip context
• Expiration

Protect personal contact details.

────────────────────────────────────────

NOTIFICATION ARCHITECTURE

Support:

• Push
• In-app
• SMS/email where appropriate

Events:

• Ride requested
• Driver assigned
• Driver arriving
• Driver arrived
• Trip started
• Trip completed
• Payment
• Receipt
• Cancellation
• Promotion
• Safety
• Support

Define:

• Templates
• Localization
• Preferences
• Deduplication
• Retry
• Scheduling

────────────────────────────────────────

SAFETY ARCHITECTURE

Complete safety capabilities.

Support:

• Emergency assistance boundary
• Trip sharing
• Trusted contacts
• Safety check-in
• Incident reporting
• Driver/rider identification
• Trip recording references where legally supported
• Safety alerts

Define:

• Data minimization
• Access control
• Retention
• Audit

Do not imply that the platform can guarantee physical safety.

────────────────────────────────────────

TRIP SHARING

Support temporary sharing.

Define:

• Share token
• Recipient
• Trip scope
• Expiration
• Revocation
• Visible fields

Never expose unnecessary payment or personal data.

────────────────────────────────────────

IDENTITY AND DRIVER VERIFICATION

Complete architecture for:

• Identity verification
• Driver-license verification
• Background-check provider
• Vehicle verification
• Insurance verification
• Document expiration

Support external verification providers through abstractions.

Do not store unnecessary raw sensitive documents.

────────────────────────────────────────

FRAUD ARCHITECTURE

Design a risk platform.

Signals may include:

• Account behavior
• Device behavior
• Location anomalies
• Payment behavior
• Promotion behavior
• Trip patterns
• Driver/rider relationships
• Cancellation patterns

Actions:

• Allow
• Challenge
• Delay
• Review
• Restrict
• Block

Avoid fully automated irreversible punishment based on one signal.

────────────────────────────────────────

GPS FRAUD

Detect:

• Teleportation
• Impossible velocity
• Repeated route anomalies
• Mock-location indicators where available
• Sensor inconsistencies

Use multiple signals.

Provide appeal/review pathways.

────────────────────────────────────────

SUPPORT ARCHITECTURE

Create support architecture.

Cases:

• Trip dispute
• Payment dispute
• Refund
• Lost item
• Safety incident
• Driver support
• Rider support
• Account issue

Define:

• Case state
• Priority
• Assignment
• SLA
• Evidence
• Resolution
• Audit

────────────────────────────────────────

BUSINESS ACCOUNTS

Complete business mobility architecture.

Support:

• Organization
• Members
• Roles
• Cost centers
• Spending policies
• Payment methods
• Business trips
• Receipts
• Expense metadata
• Approval workflows

Keep employee personal travel separate from business travel.

────────────────────────────────────────

ANALYTICS

Define operational analytics for:

• Supply
• Demand
• Matching
• ETA
• Trip completion
• Cancellation
• Driver utilization
• Rider retention
• Revenue
• Incentives
• Payouts
• Promotions
• Fraud
• Safety

Separate:

• Operational state
• Event stream
• Aggregated analytics
• Long-term storage

────────────────────────────────────────

EVENT CATALOG

Define versioned event contracts for:

IDENTITY

• UserCreated
• DriverRegistered
• DriverVerified
• VehicleVerified

AVAILABILITY

• DriverWentOnline
• DriverWentOffline
• DriverAvailabilityChanged

LOCATION

• DriverLocationUpdated
• RiderLocationUpdated

DISPATCH

• RideRequested
• MatchingStarted
• DriverOfferCreated
• DriverOfferAccepted
• DriverOfferRejected
• DriverOfferExpired
• RideMatched
• AssignmentChanged

TRIP

• DriverArrived
• TripStarted
• TripStopReached
• TripCompleted
• TripCanceled

PRICING

• FareEstimated
• FareCalculated
• SurgeUpdated
• PromotionRedeemed

PAYMENTS

• PaymentAuthorized
• PaymentCaptured
• PaymentFailed
• RefundCreated

DRIVER FINANCE

• DriverEarningCreated
• IncentiveCompleted
• PayoutCreated
• PayoutFailed

SAFETY

• SafetyIncidentCreated
• TripShared

SUPPORT

• SupportCaseCreated
• SupportCaseResolved

NOTIFICATIONS

• NotificationCreated
• NotificationDelivered

ANALYTICS

• AnalyticsEventAccepted

ADMIN

• AdministrativeActionTaken
• FeatureFlagChanged

────────────────────────────────────────

QUEUE CATALOG

Define BullMQ queues for:

• Scheduled rides
• Driver verification
• Document expiration
• Notification delivery
• Receipt generation
• Payment reconciliation
• Refund reconciliation
• Driver payout
• Fraud review
• Promotion expiration
• Support processing
• Analytics aggregation
• Location cleanup
• Audit retention
• Report generation

Define for each:

• Producer
• Consumer
• Retry
• Backoff
• Timeout
• Concurrency
• Idempotency
• Dead-letter handling
• Monitoring

────────────────────────────────────────

MULTI-REGION ARCHITECTURE

Complete regional architecture.

Support:

• Regional API
• Regional WebSocket
• Regional dispatch
• Regional geospatial state
• Regional maps integration
• Regional background workers
• Regional observability

Define region ownership for active trips.

A trip should not casually move between regions while active.

────────────────────────────────────────

ACTIVE-TRIP REGIONAL OWNERSHIP

Define:

• Home region
• Active-trip region
• Driver region
• Rider region
• Failover ownership

During an active trip:

• One region must own authoritative trip state.
• Other regions may hold read replicas or ephemeral views.
• Cross-region synchronous operations must be minimized.

────────────────────────────────────────

REGIONAL FAILOVER

Define behavior when:

• Dispatch region fails
• WebSocket region fails
• Maps provider fails
• Database region fails
• Payment region fails

Define:

• Detection
• Traffic shift
• Ownership transfer
• State reconciliation
• Recovery

Do not create split-brain trip ownership.

────────────────────────────────────────

SECURITY ARCHITECTURE

Complete:

• Authentication
• Authorization
• RBAC
• Device trust
• Session security
• Location privacy
• Payment protection
• Secret management
• Audit
• Rate limiting
• Abuse prevention

Administrative operations must require explicit authorization.

────────────────────────────────────────

THREAT MODEL

Evaluate:

• Account takeover
• Driver impersonation
• GPS spoofing
• Trip hijacking
• Payment fraud
• Promo abuse
• Driver/rider collusion
• Credential theft
• Session theft
• Webhook spoofing
• API abuse
• Location leakage
• Admin abuse
• Insider threats
• Supply-chain attacks
• DDoS

For each define:

• Prevention
• Detection
• Response
• Recovery
• Audit

────────────────────────────────────────

PRIVACY ARCHITECTURE

Define privacy for:

• Rider profile
• Driver profile
• Location
• Trip history
• Payment information
• Business travel
• Support cases
• Safety incidents
• Fraud signals

Support:

• Data minimization
• Retention
• Deletion
• Access controls
• Audit
• Data export where required

────────────────────────────────────────

OBSERVABILITY

Complete:

• Metrics
• Logs
• Traces
• Correlation IDs
• Dispatch dashboards
• Location dashboards
• Trip dashboards
• Payment dashboards
• Safety dashboards
• Fraud dashboards

Track:

• Match latency
• Match rate
• Offer acceptance
• Assignment failures
• Location freshness
• ETA accuracy
• Trip completion
• Cancellation
• Payment success
• Payout success
• Support backlog

Use:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

────────────────────────────────────────

SLO / SLI

Define SLOs for:

• API availability
• Ride-request acceptance
• Matching latency
• Driver-offer latency
• Trip-state propagation
• Location freshness
• ETA freshness
• Payment success
• Receipt availability
• Payout processing
• Support response where applicable

Define measurable SLIs and error budgets.

────────────────────────────────────────

CAPACITY PLANNING

Model:

• Riders
• Drivers
• Online drivers
• Concurrent trips
• Location updates
• Ride requests
• Matching operations
• WebSocket connections
• API traffic
• Payment traffic
• Notifications
• Support cases
• Analytics events

Define:

• Baseline
• Peak
• Burst
• Headroom
• Autoscaling triggers
• Expansion procedures

────────────────────────────────────────

FAILURE SCENARIOS

Analyze:

• PostgreSQL failure
• Redis failure
• Kafka failure
• WebSocket failure
• Dispatch failure
• Matching failure
• Maps failure
• Payment failure
• Notification failure
• Verification-provider failure
• Region failure

For each define:

• Detection
• Timeout
• Retry
• Fallback
• Degraded behavior
• Recovery
• Reconciliation

────────────────────────────────────────

DISASTER RECOVERY

Define:

• RTO
• RPO
• PostgreSQL backup
• PITR
• Redis recovery
• Kafka recovery
• S3 recovery
• Regional recovery
• Infrastructure reconstruction

Create recovery procedures for:

• Regional dispatch failure
• Active-trip ownership failure
• Database loss
• Payment subsystem failure
• Location subsystem failure

────────────────────────────────────────

TESTING ARCHITECTURE

Define:

UNIT

• Matching
• Dispatch
• Pricing
• Surge
• Fare
• Promotions
• Trip states
• Wallet
• Earnings
• Payout
• Fraud
• Safety

INTEGRATION

• PostgreSQL
• PostGIS
• Redis
• Kafka
• BullMQ
• Maps
• Payments
• Notifications

CONTRACT

• REST
• WebSocket
• Events
• Webhooks

E2E

• Rider registration
• Driver onboarding
• Ride request
• Matching
• Driver acceptance
• Arrival
• Trip
• Payment
• Receipt
• Rating
• Payout
• Support

PERFORMANCE

• Location updates
• Dispatch
• Matching
• ETA
• WebSocket
• Fare calculation
• Notifications

RESILIENCE

• Dependency failure
• Region failure
• Dispatch failure
• Location failure
• Payment failure

SECURITY

• Authentication
• Authorization
• Location privacy
• Payment security
• Fraud
• Abuse

────────────────────────────────────────

ADMINISTRATION ARCHITECTURE

Complete administrative domains:

• Riders
• Drivers
• Vehicles
• Trips
• Dispatch
• Pricing
• Payments
• Refunds
• Payouts
• Fraud
• Safety
• Support
• Promotions
• Business accounts
• Analytics
• Feature flags
• Configuration
• Audit

High-risk actions must require:

• Explicit permission
• Reason
• Audit trail
• Confirmation
• Additional approval where appropriate

────────────────────────────────────────

BACKEND IMPLEMENTATION ROADMAP

Define the exact implementation order.

BACKEND MILESTONE 1

Foundation and infrastructure.

BACKEND MILESTONE 2

Identity, rider accounts, driver accounts, authentication, authorization, sessions, devices.

BACKEND MILESTONE 3

Driver onboarding, verification, documents, vehicles, categories.

BACKEND MILESTONE 4

Geospatial, location, availability, WebSockets, maps, routing, ETA.

BACKEND MILESTONE 5

Ride requests, dispatch, matching, driver offers, trip state.

BACKEND MILESTONE 6

Pricing, fare estimation, surge, promotions, scheduled rides, multi-stop rides.

BACKEND MILESTONE 7

Payments, wallets, refunds, receipts, earnings, incentives, payouts.

BACKEND MILESTONE 8

Ratings, reviews, messaging, notifications, safety, trip sharing.

BACKEND MILESTONE 9

Fraud, risk, support, business accounts, analytics, administration.

BACKEND MILESTONE 10

Reconciliation, security hardening, performance, resilience, disaster recovery, and production readiness.

Adjust only when dependency ordering requires it.

────────────────────────────────────────

PROJECT INDEX

Update the final Project Index with:

• Domains
• Services
• Aggregates
• Data ownership
• API contracts
• WebSocket contracts
• Event contracts
• Queue contracts
• Database objects
• Spatial indexes
• Redis keys
• External integrations
• Security controls
• Privacy controls
• Dispatch architecture
• Matching architecture
• Pricing architecture
• Financial architecture
• Safety architecture
• Fraud architecture
• Support architecture
• Multi-region design
• Disaster recovery
• Testing strategy
• Backend roadmap
• Remaining work

────────────────────────────────────────

ARCHITECTURE VOLUME 2 OUTPUT

Produce:

1. Advanced Dispatch Architecture
2. Dispatch Partitioning
3. Matching Optimization
4. Matching Fairness
5. Driver Offer Optimization
6. Real-Time Location Architecture
7. Location Stream Processing
8. Geospatial Indexing
9. Location Privacy
10. Routing Architecture
11. ETA Engine
12. Airport Architecture
13. Scheduled Ride Architecture
14. Multi-Stop Architecture
15. Shared-Ride Architecture
16. Pricing Engine
17. Fare Calculation
18. Pricing Versioning
19. Surge Engine
20. Promotions Engine
21. Payment Architecture
22. Payment State Machine
23. Payment Webhooks
24. Refund Architecture
25. Wallet Architecture
26. Driver Earnings
27. Driver Incentives
28. Driver Payouts
29. Ratings
30. Messaging
31. Notification Architecture
32. Safety Architecture
33. Trip Sharing
34. Identity and Driver Verification
35. Fraud Architecture
36. GPS Fraud
37. Support Architecture
38. Business Accounts
39. Analytics
40. Event Catalog
41. Queue Catalog
42. Multi-Region Architecture
43. Active-Trip Regional Ownership
44. Regional Failover
45. Security Architecture
46. Threat Model
47. Privacy Architecture
48. Observability
49. SLO/SLI
50. Capacity Planning
51. Failure Scenarios
52. Disaster Recovery
53. Testing Architecture
54. Administration Architecture
55. Backend Implementation Roadmap
56. Complete Project Index

────────────────────────────────────────

QUALITY REQUIREMENTS

Every architectural decision must evaluate:

• Scalability
• Availability
• Security
• Privacy
• Latency
• Data consistency
• Operational complexity
• Cost
• Developer productivity
• Maintainability
• Future extensibility

Prefer:

• Regional dispatch
• Explicit active-trip ownership
• High-throughput ephemeral location state
• PostGIS for authoritative spatial data
• Redis for low-latency ephemeral geospatial data
• Strong trip-state correctness
• Strong financial correctness
• Idempotent operations
• Transactional outbox
• Event-driven processing
• Horizontal scaling
• Graceful degradation
• Provider abstraction
• Auditability

Avoid:

• Global synchronous matching
• Permanent storage of every raw GPS update
• Long-lived distributed locks
• Shared database ownership
• Redis as a system of record
• Hard coupling to one maps provider
• Hard-coded pricing rules
• Uncontrolled synchronous dependency chains
• Frontend-only security
• Single points of failure
• Premature complexity

────────────────────────────────────────

OUTPUT RULES

This is an architecture document only.

Do not generate source code.

Do not generate placeholder implementations.

Do not generate Dockerfiles.

Do not generate Kubernetes manifests.

Do not generate Terraform files.

Do not generate frontend components.

Do not generate mobile components.

Do not implement backend services.

Provide detailed:

• Architecture specifications
• Domain boundaries
• Service responsibilities
• State machines
• Data ownership
• Geospatial architecture
• Dispatch architecture
• Matching architecture
• Pricing architecture
• Financial architecture
• Safety architecture
• Fraud architecture
• API contracts
• Event contracts
• Queue contracts
• Security architecture
• Privacy architecture
• Multi-region architecture
• Disaster recovery
• Testing architecture
• ADRs
• Backend implementation roadmap
• Project Index

The resulting architecture must be sufficiently detailed that separate backend, frontend, mobile, infrastructure, DevOps, and QA teams can implement the complete mobility platform without making major architectural decisions themselves.
