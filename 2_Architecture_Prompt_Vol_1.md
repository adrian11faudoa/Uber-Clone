You are operating in Senior Engineering Team Mode.

Design the complete foundational architecture for an enterprise-scale global ride-hailing, mobility, transportation, and delivery platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

This is an ARCHITECTURE PHASE.

Do not implement backend code.

Do not implement frontend code.

Do not implement mobile code.

Do not generate infrastructure implementation files.

Do not generate Dockerfiles.

Do not generate Kubernetes manifests.

Do not generate Terraform files.

Do not generate application source code.

Produce architecture, specifications, contracts, diagrams, schemas, ownership rules, engineering decisions, and implementation guidance only.

────────────────────────────────────────

PROJECT

Build a production-ready global mobility platform supporting:

• Riders
• Drivers
• Driver onboarding
• Driver verification
• Vehicle management
• Vehicle categories
• Driver availability
• Real-time driver location
• Ride requests
• Driver matching
• Dispatch
• Fare estimation
• Dynamic pricing
• Surge pricing
• One-to-one rides
• Multi-stop rides
• Scheduled rides
• Airport trips
• Shared rides where supported
• Trip tracking
• Navigation integration
• Payments
• Cash payments where supported
• Wallets
• Promotions
• Coupons
• Refunds
• Driver earnings
• Driver incentives
• Driver payouts
• Ratings
• Reviews
• Rider-driver messaging
• Push notifications
• Safety systems
• Trip sharing
• Emergency assistance boundaries
• Fraud prevention
• Abuse prevention
• Blocking
• Reporting
• Support
• Business accounts
• Business rides
• Receipts
• Tax-related metadata
• Analytics
• Administration
• Moderation
• High availability
• Multi-region deployment
• Disaster recovery
• Horizontal scalability

The platform must be designed for:

• Very low dispatch latency
• Massive location-update throughput
• Large concurrent trip volumes
• Strong financial correctness
• Strong trip-state correctness
• Global operation
• Regional routing
• Fault tolerance

────────────────────────────────────────

PRIMARY TECHNOLOGY STACK

WEB

• Next.js
• React
• TypeScript
• Tailwind CSS
• shadcn/ui
• TanStack Query
• Zustand

MOBILE

• React Native
• Expo
• TypeScript

BACKEND

• Node.js
• NestJS
• TypeScript

DATABASE

• PostgreSQL
• Prisma ORM
• PostGIS

CACHE / EPHEMERAL STATE

• Redis

EVENT STREAMING

• Kafka or Redpanda

BACKGROUND PROCESSING

• BullMQ

REAL-TIME

• WebSockets
• Socket.IO where appropriate

MAPS / GEOSPATIAL

• Google Maps Platform or approved mapping abstraction
• Geocoding
• Reverse geocoding
• Routes
• ETA
• Places
• Geofencing where appropriate

PAYMENTS

• Stripe or approved payment abstraction

PUSH NOTIFICATIONS

• Firebase Cloud Messaging
• Apple Push Notification Service

OBJECT STORAGE

• AWS S3-compatible object storage

CDN

• CloudFront or equivalent CDN

INFRASTRUCTURE

• Docker
• Kubernetes
• Helm
• Terraform
• GitHub Actions

OBSERVABILITY

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

SECRETS

• AWS Secrets Manager
• HashiCorp Vault or approved cloud-native secret management

────────────────────────────────────────

ARCHITECTURAL APPROACH

Determine the appropriate architecture between:

• Modular Monolith
• Service-Oriented Architecture
• Microservices

Do not blindly create a microservice for every domain.

Evaluate:

• Dispatch latency
• Location-update scale
• Geospatial workloads
• Trip consistency
• Financial consistency
• Driver availability
• Real-time communication
• Failure isolation
• Operational complexity
• Deployment independence
• Cost
• Team ownership
• Global deployment

Clearly identify:

• Independently deployable services
• Shared transactional boundaries
• Authoritative data ownership
• Synchronous communication
• Asynchronous communication
• Event-driven communication
• Real-time communication
• Read models
• CQRS requirements
• Strong consistency boundaries
• Eventual consistency boundaries

Provide a future service-extraction strategy.

────────────────────────────────────────

DOMAIN DECOMPOSITION

Define bounded contexts for:

Identity

Accounts

Profiles

Authentication

Authorization

Sessions

Devices

Riders

Drivers

Driver Onboarding

Driver Verification

Driver Documents

Vehicles

Vehicle Verification

Vehicle Categories

Driver Availability

Location

Geospatial

Geofencing

Maps

Routing

ETA

Ride Requests

Dispatch

Matching

Driver Offers

Trip Lifecycle

Trip Stops

Scheduled Rides

Shared Rides

Fare Estimation

Pricing

Surge

Promotions

Coupons

Payments

Wallet

Refunds

Driver Earnings

Driver Incentives

Driver Payouts

Ratings

Reviews

Messaging

Notifications

Safety

Trip Sharing

Emergency Assistance

Fraud

Risk

Blocking

Reporting

Support

Business Accounts

Business Trips

Business Billing

Receipts

Taxes

Analytics

Administration

Moderation

Audit

Feature Flags

System Configuration

For every bounded context define:

• Responsibility
• Aggregate roots
• Entities
• Value objects
• Domain services
• Repositories
• Domain events
• Data ownership
• Consistency model
• Scaling requirements
• Security boundaries

────────────────────────────────────────

SERVICE DECOMPOSITION

Evaluate appropriate services for:

API Gateway

Authentication Service

Identity Service

Account Service

Profile Service

Session Service

Device Service

Rider Service

Driver Service

Driver Onboarding Service

Driver Verification Service

Vehicle Service

Vehicle Verification Service

Availability Service

Location Service

Geospatial Service

Map Integration Service

Routing Service

ETA Service

Ride Request Service

Dispatch Service

Matching Service

Driver Offer Service

Trip Service

Scheduled Ride Service

Shared Ride Service

Fare Service

Pricing Service

Surge Service

Promotion Service

Coupon Service

Payment Service

Wallet Service

Refund Service

Earnings Service

Incentive Service

Payout Service

Rating Service

Review Service

Messaging Service

Notification Service

Safety Service

Trip Sharing Service

Fraud Service

Risk Service

Blocking Service

Reporting Service

Support Service

Business Account Service

Business Trip Service

Receipt Service

Analytics Service

Administration Service

Moderation Service

Audit Service

Feature Flag Service

Configuration Service

Do not create unnecessary services.

Combine tightly coupled responsibilities where justified by:

• Transactional consistency
• Latency
• Operational complexity
• Ownership

For every final service define:

• Responsibility
• Owned data
• APIs
• Events produced
• Events consumed
• Synchronous dependencies
• Asynchronous dependencies
• Scaling
• Availability
• Security

────────────────────────────────────────

SERVICE OWNERSHIP MATRIX

Create a complete ownership matrix identifying:

• Authoritative service
• Database owner
• Cache owner
• Event owner
• Read-model owner
• Search owner
• Administrative owner

Explicitly prohibit direct writes to another domain's authoritative database.

────────────────────────────────────────

COMMUNICATION MATRIX

For major service interactions define:

• Producer
• Consumer
• Protocol
• Purpose
• Direction
• Sync/async
• Timeout
• Retry
• Idempotency
• Consistency
• Failure behavior

Evaluate:

• REST
• Kafka/Redpanda
• BullMQ
• Redis
• WebSockets
• Server-Sent Events where useful

Avoid unnecessary synchronous dependency chains.

────────────────────────────────────────

SYSTEM ARCHITECTURE

Generate text-based diagrams for:

CLIENT LAYER

• Rider web
• Rider mobile
• Driver web
• Driver mobile
• Administration

EDGE LAYER

• DNS
• CDN
• WAF
• Load balancer
• API gateway
• WebSocket gateway

APPLICATION LAYER

• Rider APIs
• Driver APIs
• Dispatch
• Matching
• Trip management
• Pricing
• Payment
• Notification
• Support
• Administration

REAL-TIME LAYER

• Driver location
• Ride status
• Dispatch offers
• Rider tracking
• Messaging

DATA LAYER

• PostgreSQL
• PostGIS
• Redis
• Kafka
• Object storage
• Search where appropriate

INTEGRATION LAYER

• Maps provider
• Payment provider
• Push providers
• Verification providers

OBSERVABILITY LAYER

• Metrics
• Logs
• Traces
• Alerts

SECURITY LAYER

• Authentication
• Authorization
• IAM
• Secrets
• Encryption
• Audit

Do not use images.

────────────────────────────────────────

MONOREPO ARCHITECTURE

Design a production-ready monorepo containing:

APPLICATIONS

• Rider Web
• Rider Mobile
• Driver Web
• Driver Mobile
• Admin Dashboard

BACKEND

• API Gateway
• Domain services
• Real-time services
• Dispatch services
• Matching services
• Workers
• Event consumers

SHARED PACKAGES

• API contracts
• Event contracts
• Shared types
• Validation
• Configuration
• Authentication
• Authorization
• Geospatial interfaces
• Maps interfaces
• Payment interfaces
• Observability
• Testing utilities

INFRASTRUCTURE

• Docker
• Kubernetes
• Helm
• Terraform
• CI/CD

DOCUMENTATION

• Architecture
• APIs
• Events
• Database
• Dispatch
• Maps
• Security
• Operations
• ADRs
• Runbooks

Do not create uncontrolled shared packages.

────────────────────────────────────────

FOLDER HIERARCHY

Generate a detailed production-ready hierarchy for:

• Monorepo root
• Rider web
• Driver web
• Rider mobile
• Driver mobile
• Admin
• API gateway
• Backend services
• Dispatch
• Matching
• Real-time systems
• Workers
• Shared packages
• Database
• Infrastructure
• Tests
• Documentation
• Migrations
• Configuration

The hierarchy must be consistent with future implementation prompts.

────────────────────────────────────────

CORE DOMAIN MODEL

Evaluate and define:

User

Account

Profile

Session

Device

Rider

Driver

DriverDocument

DriverVerification

Vehicle

VehicleCategory

VehicleVerification

DriverAvailability

DriverLocationReference

ServiceArea

Geofence

RideRequest

RideRequestStop

DriverOffer

Trip

TripStop

TripParticipant

TripStateTransition

ScheduledRide

SharedRide

FareEstimate

Fare

FareComponent

PricingRule

SurgeZone

Promotion

Coupon

Payment

PaymentAttempt

Refund

Wallet

WalletTransaction

DriverEarning

DriverIncentive

DriverPayout

Rating

Review

Conversation

Message

Notification

SafetyIncident

TripShare

BlockedEntity

Report

SupportCase

BusinessAccount

BusinessMember

BusinessTrip

Receipt

TaxRecord

AuditLog

FeatureFlag

SystemConfiguration

Do not force every conceptual entity into a separate table.

Use aggregates and normalized relational structures appropriately.

────────────────────────────────────────

TRIP AGGREGATE

Define the Trip aggregate and exact ownership of:

• Rider
• Driver
• Vehicle
• Pickup
• Dropoff
• Stops
• Fare
• Pricing snapshot
• Status
• Payment reference
• Cancellation
• Completion
• Safety metadata

Trip state must be strongly controlled.

Define valid state transitions.

────────────────────────────────────────

TRIP STATE MACHINE

Define states such as:

• Requested
• Searching
• Offered
• Assigned
• Driver En Route
• Driver Arrived
• Trip Started
• Trip In Progress
• Stop Reached
• Trip Completed
• Rider Canceled
• Driver Canceled
• System Canceled
• Disputed

Define all valid and invalid transitions.

Every transition must be:

• Authorized
• Idempotent
• Auditable
• Version-aware

────────────────────────────────────────

DRIVER STATE MACHINE

Define:

• Registered
• Onboarding
• Verification Pending
• Verified
• Offline
• Available
• Offered
• En Route
• Arrived
• On Trip
• Suspended
• Deactivated

Separate:

• Account state
• Driver eligibility state
• Availability state
• Current trip state

────────────────────────────────────────

VEHICLE DOMAIN

Support:

• Vehicle registration
• Category
• Make
• Model
• Year
• Color
• Plate
• Capacity
• Accessibility
• Verification
• Insurance
• Registration status

Define vehicle eligibility for trip categories.

────────────────────────────────────────

DRIVER ONBOARDING

Define workflows for:

• Identity
• Driver license
• Background verification
• Vehicle registration
• Insurance
• Profile
• Required documents

Support states:

• Draft
• Submitted
• Pending Review
• Approved
• Rejected
• Suspended

Use external provider abstractions.

────────────────────────────────────────

LOCATION ARCHITECTURE

Design a high-scale location platform supporting:

• Driver location
• Rider location
• Pickup location
• Dropoff location
• Route progress
• Geofences

Define:

• Update frequency
• Accuracy
• Compression
• Validation
• Privacy
• Retention

Do not persist every GPS update indefinitely in PostgreSQL.

────────────────────────────────────────

REAL-TIME LOCATION ARCHITECTURE

Support:

• Driver location streams
• Rider trip tracking
• Location heartbeats
• WebSocket connections
• Reconnection
• Ordering
• Stale updates
• Regional routing

Evaluate:

• Redis
• WebSockets
• Kafka
• PostGIS

Define which component owns which responsibility.

────────────────────────────────────────

GEOLOCATION PRIVACY

Define:

• Who can see driver location
• Who can see rider location
• During which trip states
• For how long
• Approximation/anonymization where required
• Retention

Administrative location access must be tightly restricted and audited.

────────────────────────────────────────

GEOSPATIAL ARCHITECTURE

Use PostGIS where authoritative spatial queries are needed.

Evaluate Redis geospatial functionality for:

• Nearby driver discovery
• Temporary availability

Use PostGIS for:

• Service-area boundaries
• Geofences
• Airport zones
• Historical spatial analysis where justified

────────────────────────────────────────

DISPATCH ARCHITECTURE

Design low-latency dispatch.

Flow:

Ride Request
→ Candidate Search
→ Eligibility
→ Scoring
→ Driver Offer
→ Driver Response
→ Assignment
→ Trip

Define:

• Regional dispatch
• Candidate pool
• Timeouts
• Retries
• Reassignment
• Fallback

Do not make all global drivers compete in one global matching operation.

────────────────────────────────────────

MATCHING ARCHITECTURE

Define:

1. Candidate generation
2. Eligibility
3. ETA
4. Scoring
5. Offer
6. Acceptance
7. Reservation
8. Assignment

Candidate scoring may consider:

• ETA
• Distance
• Vehicle category
• Accessibility
• Driver availability
• Trip direction
• Regional policy
• Rider preferences

Do not hard-code the design around a single matching algorithm.

────────────────────────────────────────

MATCHING RACE CONDITIONS

Prevent:

• Driver accepting two rides
• Duplicate assignments
• Duplicate offers
• Stale availability
• Offer replay
• Late acceptance

Use:

• Idempotency
• Short-lived leases
• Atomic state transitions
• Optimistic concurrency
• Redis coordination where appropriate

Avoid long-lived distributed locks.

────────────────────────────────────────

DRIVER OFFER ARCHITECTURE

Support:

• Offer creation
• Delivery
• Acceptance
• Rejection
• Expiration
• Cancellation

Define:

• Offer timeout
• Idempotency
• Retry
• Reassignment
• Driver response ordering

────────────────────────────────────────

SCHEDULED RIDES

Support:

• Future pickup
• Reservation
• Reminder
• Driver assignment
• Driver replacement
• Cancellation
• Reconciliation

Use background scheduling.

────────────────────────────────────────

MULTI-STOP RIDES

Support:

• Stop creation
• Stop ordering
• Stop completion
• Stop removal
• Stop insertion
• Route recalculation
• ETA recalculation
• Fare recalculation

Define pricing behavior when stops change.

────────────────────────────────────────

SHARED RIDES

Create an extensible shared-ride architecture.

Support:

• Multiple riders
• Shared route
• Pickup sequence
• Dropoff sequence
• Capacity
• Fare allocation
• Shared-trip state

Keep shared-trip logic isolated from ordinary one-rider trips.

────────────────────────────────────────

MAPS ARCHITECTURE

Create an abstraction around:

• Geocoding
• Reverse geocoding
• Places
• Directions
• ETA
• Distance
• Traffic
• Map rendering
• Route matching

Do not tightly couple core business domains to one provider.

────────────────────────────────────────

ETA ARCHITECTURE

Support:

• Driver-to-pickup ETA
• Trip ETA
• Dynamic traffic
• Route changes
• Driver movement

Define:

• Caching
• Refresh frequency
• Accuracy
• Stale-data handling
• Provider fallback

────────────────────────────────────────

FARE ARCHITECTURE

Fare components may include:

• Base
• Distance
• Time
• Minimum fare
• Booking fee
• Tolls
• Taxes
• Promotions
• Surge
• Other regulated fees

Use exact monetary arithmetic.

────────────────────────────────────────

PRICING SNAPSHOT

At request/confirmation time preserve:

• Pricing version
• Fare components
• Surge multiplier
• Currency
• Tax assumptions
• Promotion
• Calculation metadata

Completed trips must remain reconstructable.

────────────────────────────────────────

SURGE ARCHITECTURE

Support:

• Geographic zones
• Demand
• Supply
• Time windows
• Ride categories
• Multipliers
• Caps
• Regional regulations

Separate:

• Demand measurement
• Supply measurement
• Surge calculation
• Pricing application

────────────────────────────────────────

PROMOTION ARCHITECTURE

Support:

• Promo codes
• Campaigns
• Eligibility
• Usage limits
• Customer limits
• Expiration
• Region
• Trip category

Prevent:

• Double redemption
• Negative fares
• Reuse beyond limits

────────────────────────────────────────

PAYMENT ARCHITECTURE

Support:

• Payment methods
• Authorization
• Capture
• Failure
• Refund
• Partial refund
• Chargebacks
• Reconciliation

Separate:

• Trip state
• Payment state
• Wallet state
• Driver earning state

────────────────────────────────────────

WALLET ARCHITECTURE

Support:

• Promotional credits
• Refund credits
• Stored credits
• Business credits

Use an immutable ledger:

• Transaction
• Entry
• Amount
• Currency
• Source
• Expiration
• Balance projection

The wallet ledger is authoritative.

Redis is not.

────────────────────────────────────────

DRIVER EARNINGS

Support:

• Trip earnings
• Tips
• Incentives
• Bonuses
• Fees
• Adjustments
• Refund effects

Use immutable financial ledger entries.

────────────────────────────────────────

PAYOUTS

Support:

• Pending earnings
• Available earnings
• Payout
• Provider reference
• Payout status
• Failed payout
• Reconciliation

Prevent:

• Duplicate payout
• Double withdrawal
• Payout beyond available balance

────────────────────────────────────────

RATINGS AND REVIEWS

Support:

• Rider-to-driver rating
• Driver-to-rider rating
• Structured feedback
• Optional review
• Rating eligibility
• Rating window
• Moderation

Prevent duplicate ratings.

────────────────────────────────────────

MESSAGING

Design trip-scoped messaging between:

• Rider
• Driver

Support:

• Message
• Conversation
• Read state
• Attachments where required
• Expiration
• Safety controls

Avoid exposing personal phone numbers.

────────────────────────────────────────

SAFETY ARCHITECTURE

Support:

• Trip sharing
• Trusted contacts
• Emergency assistance boundary
• Safety check-ins
• Driver/rider information
• Incident reporting
• Safety alerts

Define strict permissions.

Software must not be represented as guaranteeing physical safety.

────────────────────────────────────────

TRIP SHARING

Support temporary trip-sharing access.

Define:

• Share token
• Recipient
• Expiration
• Revocation
• Visible trip data

Do not expose unnecessary personal information.

────────────────────────────────────────

FRAUD AND RISK

Protect against:

• Fake accounts
• GPS spoofing
• Driver/rider collusion
• Payment fraud
• Coupon abuse
• Referral abuse
• Chargeback abuse
• Fake trips
• Cash abuse
• Account takeover
• Location anomalies

Define:

• Signals
• Rules
• Scoring
• Actions
• Appeals
• Manual review

────────────────────────────────────────

BLOCKING AND REPORTING

Support:

• Rider blocks
• Driver blocks
• Safety reports
• Fraud reports
• Harassment reports

A block should influence future matching appropriately.

────────────────────────────────────────

SUPPORT

Design support-case architecture for:

• Trip disputes
• Payment disputes
• Refunds
• Lost items
• Safety
• Driver support
• Rider support

Case lifecycle:

• Created
• Assigned
• Investigating
• Waiting
• Resolved
• Closed
• Reopened

────────────────────────────────────────

BUSINESS ACCOUNTS

Support:

• Business organization
• Members
• Roles
• Employee eligibility
• Business payment
• Cost centers
• Ride policies
• Spending limits
• Business receipts
• Business trips

Separate business and personal ride data.

────────────────────────────────────────

RECEIPTS

Define receipt architecture containing:

• Trip
• Timestamp
• Pickup
• Dropoff
• Driver
• Vehicle
• Fare
• Taxes
• Promotions
• Tips
• Payment
• Currency

Receipts must remain reconstructable.

────────────────────────────────────────

ANALYTICS

Design analytics for:

OPERATIONS

• Ride requests
• Match rate
• Acceptance
• Cancellation
• Completion
• ETA
• Supply
• Demand

DRIVER

• Online time
• Trips
• Earnings
• Acceptance
• Cancellation
• Ratings

RIDER

• Requests
• Completion
• Spend
• Retention

FINANCIAL

• GMV
• Revenue
• Take rate
• Incentives
• Refunds
• Payouts

Do not overload PostgreSQL with raw telemetry.

────────────────────────────────────────

EVENT-DRIVEN ARCHITECTURE

Define Kafka/Redpanda events including:

• AccountCreated
• DriverRegistered
• DriverVerified
• DriverSuspended
• VehicleRegistered
• VehicleVerified
• DriverWentOnline
• DriverWentOffline
• DriverLocationUpdated
• RideRequested
• RideMatchingStarted
• DriverOfferCreated
• DriverOfferAccepted
• DriverOfferRejected
• DriverOfferExpired
• RideMatched
• RideAssignmentChanged
• RideCanceled
• DriverArrived
• TripStarted
• TripStopReached
• TripCompleted
• FareCalculated
• PaymentAuthorized
• PaymentCaptured
• PaymentFailed
• RefundCreated
• PromotionRedeemed
• RatingSubmitted
• ReviewSubmitted
• WalletCreditAdded
• WalletCreditUsed
• DriverEarningCreated
• DriverPayoutCreated
• NotificationCreated
• SafetyIncidentReported
• TripShared
• SupportCaseCreated
• BusinessTripCreated
• AuditLogCreated
• FeatureFlagChanged

Events must:

• Be versioned
• Be idempotently consumed
• Contain only required information
• Preserve ownership boundaries

────────────────────────────────────────

QUEUE ARCHITECTURE

Define BullMQ queues for:

• Scheduled rides
• Driver verification
• Notifications
• Receipt generation
• Payment reconciliation
• Payout processing
• Fraud processing
• Support workflows
• Data cleanup
• Promotion expiration
• Analytics aggregation

For every queue define:

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

API ARCHITECTURE

Define public/internal/real-time APIs.

RIDER

• Register
• Login
• Profile
• Saved places
• Payment methods
• Fare estimate
• Ride request
• Ride status
• Cancel
• Trip tracking
• History
• Receipt
• Rating
• Promotion
• Wallet
• Support

DRIVER

• Register
• Onboarding
• Documents
• Vehicle
• Verification
• Availability
• Location
• Ride offers
• Accept
• Reject
• Arrive
• Start
• Complete
• Earnings
• Incentives
• Payouts
• Ratings
• Support

REAL-TIME

• Location
• Dispatch offers
• Ride status
• Trip tracking
• Messaging

ADMIN

• Riders
• Drivers
• Vehicles
• Trips
• Payments
• Fraud
• Safety
• Support
• Promotions
• Business
• Analytics
• Audit

Define:

• Authentication
• Authorization
• API versioning
• Validation
• Pagination
• Cursor pagination
• Error format
• Rate limiting
• Idempotency

────────────────────────────────────────

DATABASE ARCHITECTURE

Design PostgreSQL/PostGIS for:

• Hundreds of millions of riders
• Millions of drivers
• Millions of vehicles
• Large trip history
• Large financial ledgers
• High-volume operational records

Define:

• Database ownership
• Schemas
• Primary keys
• Foreign keys
• Unique constraints
• Check constraints
• Spatial indexes
• Partitioning
• Archival
• Retention
• Read replicas
• Connection pooling
• Backup
• Recovery

Partitioning candidates include:

• Trips
• Trip events
• Payments
• Refunds
• Driver earnings
• Payouts
• Support cases
• Audit logs
• Analytics references

Do not treat raw GPS streams as ordinary transactional records.

────────────────────────────────────────

PRISMA STRATEGY

Define:

• Schema ownership
• Service-specific Prisma clients where appropriate
• Migration ownership
• Transaction boundaries
• Read replicas
• Connection pooling
• Query optimization
• Large-table migration strategy

────────────────────────────────────────

REDIS ARCHITECTURE

Use Redis for:

• Driver availability
• Driver location
• Nearby-driver candidates
• Active trip state
• Matching coordination
• Short-lived leases
• ETA cache
• Rate limiting
• Idempotency
• WebSocket coordination
• Notification deduplication

For each define:

• Key pattern
• TTL
• Invalidation
• Consistency
• Failure behavior

Redis must never be authoritative for:

• Trips
• Payments
• Wallets
• Earnings
• Payouts
• Driver identity
• Historical data

────────────────────────────────────────

MULTI-REGION ARCHITECTURE

Design:

• Regional application clusters
• Regional dispatch
• Regional geospatial processing
• Regional data ownership
• Global routing
• Cross-region events where required
• Regional failover

Dispatch must prefer regional drivers and regional state.

Avoid unnecessary cross-region synchronous calls in the dispatch critical path.

────────────────────────────────────────

SCALABILITY

Design for:

• Hundreds of millions of riders
• Millions of drivers
• Tens of millions of concurrent mobile sessions
• Millions of active drivers
• Massive location updates
• Very high ride-request throughput
• Large financial throughput

Analyze scaling for:

• API gateway
• WebSocket gateways
• Location service
• Redis
• PostGIS
• Dispatch
• Matching
• Kafka
• Payments
• Notifications
• Maps
• Support
• Analytics

Identify bottlenecks and mitigation strategies.

────────────────────────────────────────

FAILURE SCENARIOS

Define graceful behavior when:

• PostgreSQL unavailable
• Redis unavailable
• Kafka unavailable
• Maps provider unavailable
• Payment provider unavailable
• Push provider unavailable
• WebSocket gateway fails
• Dispatch service fails
• Matching service fails
• Region unavailable

For each define:

• Detection
• Timeout
• Retry
• Fallback
• Degraded behavior
• Recovery
• Reconciliation

────────────────────────────────────────

DATA CONSISTENCY

Explicitly define consistency for:

• Accounts
• Driver verification
• Driver availability
• Ride request
• Driver assignment
• Trip state
• Fare
• Payment
• Wallet
• Earnings
• Payouts
• Promotions
• Ratings
• Safety
• Support
• Business accounts

Identify where to use:

• Strong consistency
• Eventual consistency
• Idempotency
• Optimistic concurrency
• Short-lived leases
• Transactional outbox

────────────────────────────────────────

SECURITY ARCHITECTURE

Design:

AUTHENTICATION

• Passwords
• OAuth
• MFA
• Passkeys where approved
• Sessions
• Device authentication

AUTHORIZATION

• RBAC
• Resource ownership
• Rider scope
• Driver scope
• Business scope
• Administrative scope

LOCATION SECURITY

• Location access rules
• Location privacy
• Retention
• Audit

PAYMENT SECURITY

• Provider tokens
• Webhook validation
• Idempotency
• Secret management

APPLICATION SECURITY

• Validation
• Rate limiting
• Secure headers
• CORS
• CSRF where applicable
• XSS prevention
• SQL injection protection
• SSRF mitigation where relevant

────────────────────────────────────────

ABUSE PREVENTION

Design against:

• Fake-driver accounts
• Fake rider accounts
• GPS spoofing
• Trip manipulation
• Driver collusion
• Rider collusion
• Coupon abuse
• Referral abuse
• Payment abuse
• Cash fraud
• API abuse
• Credential stuffing
• Account takeover

Define prevention and detection.

────────────────────────────────────────

OBSERVABILITY

Design:

• Structured logs
• Metrics
• Distributed tracing
• Correlation IDs
• Dispatch metrics
• Matching metrics
• Location metrics
• ETA metrics
• Trip metrics
• Payment metrics
• Payout metrics
• Safety metrics
• Fraud metrics
• Queue metrics

Use:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

Define dashboards and alerts.

Critical metrics include:

• Ride-request rate
• Matching latency
• Match success rate
• Driver-offer latency
• Offer acceptance
• Assignment failures
• Location freshness
• ETA latency
• Trip completion
• Payment success
• Cancellation
• Queue backlog

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

Include recovery procedures for:

• Database failure
• Dispatch failure
• Matching failure
• Region failure
• Payment failure
• Location-system failure

────────────────────────────────────────

TESTING ARCHITECTURE

UNIT:

• Fare calculation
• Pricing
• Surge
• Dispatch rules
• Matching
• Trip state
• Authorization
• Promotion
• Wallet
• Earnings

INTEGRATION:

• PostgreSQL
• PostGIS
• Redis
• Kafka
• BullMQ
• Maps
• Payments
• Notifications

CONTRACT:

• REST
• WebSocket
• Events
• Webhooks

E2E:

• Rider registration
• Driver onboarding
• Ride request
• Matching
• Driver acceptance
• Pickup
• Trip
• Payment
• Receipt
• Rating
• Payout

PERFORMANCE:

• Location throughput
• Dispatch
• Matching
• Fare estimates
• API
• Notifications

RESILIENCE:

• Database failure
• Redis failure
• Kafka failure
• Maps failure
• Payment failure
• WebSocket failure
• Region failure

SECURITY:

• Authentication
• Authorization
• Location privacy
• Financial security
• Fraud
• Abuse

────────────────────────────────────────

ARCHITECTURAL DECISION RECORDS

Create ADRs for:

• Architecture style
• Service decomposition
• Dispatch
• Matching
• Location
• Redis geospatial state
• PostGIS
• Maps abstraction
• Pricing
• Surge
• Payments
• Wallet
• Driver earnings
• Payouts
• Real-time architecture
• Scheduled rides
• Multi-stop rides
• Shared rides
• Business accounts
• Safety
• Fraud
• Multi-region
• Kubernetes
• Terraform
• Observability
• Secrets management

Each ADR must contain:

• Context
• Decision
• Alternatives considered
• Consequences

────────────────────────────────────────

ARCHITECTURE VOLUME 1 OUTPUT

Produce:

1. Executive Architecture Overview
2. System Context
3. Architectural Approach
4. System Architecture
5. Client Architecture
6. Domain Decomposition
7. Service Decomposition
8. Service Ownership Matrix
9. Communication Matrix
10. Monorepo Architecture
11. Detailed Folder Hierarchy
12. Core Domain Model
13. Aggregate Boundaries
14. Trip Aggregate
15. Trip State Machine
16. Driver State Machine
17. Complete Text-Based ERD
18. PostgreSQL/PostGIS Architecture
19. Prisma Strategy
20. Redis Architecture
21. Location Architecture
22. Real-Time Location Architecture
23. Geospatial Architecture
24. Driver Availability Architecture
25. Dispatch Architecture
26. Matching Architecture
27. Driver Offer Architecture
28. Scheduled Ride Architecture
29. Multi-Stop Ride Architecture
30. Shared Ride Architecture
31. Maps Architecture
32. ETA Architecture
33. Fare Architecture
34. Pricing Snapshot
35. Surge Architecture
36. Promotion Architecture
37. Payment Architecture
38. Wallet Architecture
39. Driver Earnings Architecture
40. Payout Architecture
41. Ratings and Reviews
42. Messaging Architecture
43. Safety Architecture
44. Trip Sharing
45. Fraud and Risk Architecture
46. Blocking and Reporting
47. Support Architecture
48. Business Account Architecture
49. Receipt Architecture
50. Analytics Architecture
51. Event-Driven Architecture
52. Queue Architecture
53. API Architecture
54. Multi-Region Architecture
55. Scalability Strategy
56. Failure Scenarios
57. Data Consistency Strategy
58. Security Architecture
59. Abuse Prevention
60. Observability Architecture
61. Disaster Recovery
62. Testing Architecture
63. Architectural Decision Records

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
• Explicit domain ownership
• PostGIS for authoritative spatial data
• Redis for ephemeral geospatial state
• Stateless APIs
• Event-driven communication
• Idempotent consumers
• Transactional outbox
• Strong trip-state correctness
• Strong financial correctness
• Short-lived resource leases
• Horizontal scaling
• Graceful degradation

Avoid:

• Unnecessary microservices
• Shared database ownership
• Global synchronous matching
• Permanent storage of every GPS update
• Long-lived distributed locks
• Redis as a system of record
• Tight coupling to one maps provider
• Application servers handling unnecessary map/media payloads
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
• Ownership rules
• Database schemas
• ERD
• API contracts
• Event contracts
• Queue definitions
• Geospatial architecture
• Dispatch architecture
• Matching architecture
• Pricing architecture
• Financial architecture
• Safety architecture
• Security architecture
• Scalability strategy
• Multi-region architecture
• Failure handling
• Disaster recovery
• Testing architecture
• ADRs

The resulting architecture must be sufficiently detailed that separate backend, frontend, mobile, infrastructure, DevOps, and QA teams can implement the mobility platform without making major architectural decisions themselves.
