You are operating in Senior Engineering Team Mode.

Build the production-ready backend for ratings, reviews, rider-driver messaging, notifications, safety, trip sharing, fraud and risk, blocking, reporting, support, business accounts, business trips, receipts integration, operational analytics, and related administrative workflows for an enterprise-scale global ride-hailing and mobility platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

The backend must follow the approved Uber-like architecture, domain boundaries, database ownership, trip architecture, dispatch architecture, location architecture, pricing architecture, financial architecture, security model, event architecture, queue architecture, and Project Index.

Do not redesign the architecture.

Do not generate frontend code.

Do not generate mobile code.

Do not generate infrastructure implementation code.

Do not generate Terraform.

Do not generate Kubernetes manifests.

Do not generate CI/CD workflows.

────────────────────────────────────────

MISSION

Implement the production-ready backend required for:

• Rider ratings
• Driver ratings
• Reviews
• Structured trip feedback
• Rider-driver messaging
• Trip-scoped conversations
• Message moderation
• Push notifications
• In-app notifications
• Notification preferences
• Safety incidents
• Emergency assistance boundaries
• Trip sharing
• Trusted contacts
• Safety check-ins
• Rider/driver blocking
• Reporting
• Fraud detection
• Risk scoring
• Fraud case management
• Support cases
• Trip disputes
• Payment support escalation
• Lost item support
• Rider support
• Driver support
• Business accounts
• Business members
• Business trips
• Business policies
• Business billing references
• Cost centers
• Business receipts
• Operational analytics
• Safety analytics
• Fraud analytics
• Support analytics
• Administrative workflows
• Audit integration

The implementation must support:

• Hundreds of millions of riders
• Millions of drivers
• Millions of trips
• High notification volume
• Large messaging volume
• Large support volume
• High fraud-signal volume
• Strict safety requirements
• Strict privacy requirements
• Multiple business organizations
• Multiple regions
• High availability
• Horizontal scalability

────────────────────────────────────────

TECHNOLOGY STACK

Backend:

• Node.js
• NestJS
• TypeScript

Database:

• PostgreSQL
• Prisma ORM

Cache / transient state:

• Redis

Event streaming:

• Kafka or Redpanda

Background processing:

• BullMQ

Real-time:

• WebSockets
• Socket.IO

Notifications:

• Firebase Cloud Messaging
• Apple Push Notification Service
• Email provider abstraction
• SMS provider abstraction where approved

Object storage:

• AWS S3-compatible storage where evidence or reports require it

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

Testing:

• Jest
• Supertest
• Integration and security testing tools

────────────────────────────────────────

IMPLEMENTATION RULES

Never generate pseudo-code.

Never generate placeholders.

Never generate TODO comments.

Never omit implementations.

Never say:

- "implement similarly"
- "left as an exercise"
- "for brevity"
- "remaining code omitted"

Every generated file must be complete.

Every generated file must compile.

Never regenerate unchanged files.

Only modify existing files when required.

Use strict TypeScript.

Use dependency injection.

Keep controllers thin.

Keep business logic outside controllers.

Use repositories for persistence.

Use DTOs for API contracts.

Use centralized validation.

Use centralized error handling.

Use structured logging.

Use idempotency for all mutation operations that can be retried.

Do not allow sensitive safety, fraud, or support data to leak through ordinary rider/driver APIs.

────────────────────────────────────────

DOMAIN OWNERSHIP

Maintain explicit boundaries between:

• Ratings
• Reviews
• Messaging
• Notifications
• Safety
• Trip sharing
• Blocking
• Reporting
• Fraud
• Risk
• Support
• Business accounts
• Business trips
• Business policy
• Analytics
• Administration
• Audit

Do not combine:

• Safety incident data with public review data
• Fraud risk data with ordinary user profile data
• Support case data with trip state
• Notification delivery state with business state
• Business billing policy with personal rider billing
• Messaging state with trip authorization

────────────────────────────────────────

RATINGS DOMAIN

Implement:

• Rider rates driver
• Driver rates rider
• Rating submission
• Rating eligibility
• Rating window
• Rating update policy where approved
• Rating visibility
• Rating aggregation
• Rating moderation

Prevent:

• Duplicate ratings
• Ratings outside eligible trip window
• Ratings by unauthorized users
• Rating manipulation

────────────────────────────────────────

RATING ELIGIBILITY

A rating should be permitted only when:

• Trip is completed or otherwise eligible
• User participated in trip
• Rating window remains open
• Rating has not already been submitted
• Account/profile is authorized

Do not permit arbitrary rating creation.

────────────────────────────────────────

RATING PRIVACY

Define what each party can see:

• Individual rating
• Aggregate rating
• Structured feedback
• Review text
• Anonymous summaries where appropriate

Do not reveal sensitive or unnecessary reviewer identity.

────────────────────────────────────────

RATING AGGREGATION

Support:

• Overall rating
• Recent rating
• Rating count
• Distribution
• Category scores where supported

Define:

• Recalculation
• Caching
• Event-driven aggregation

Do not calculate large rating aggregates synchronously for every API request.

────────────────────────────────────────

REVIEWS

Support:

• Structured feedback
• Optional text review
• Moderation state
• Report
• Visibility
• Resolution

Review states may include:

• Submitted
• Under Review
• Published
• Hidden
• Removed
• Appealed

────────────────────────────────────────

REVIEW MODERATION

Detect:

• Spam
• Harassment
• Threats
• Personally identifying data
• Abusive content
• Fraudulent reviews

Support:

• Automated classification
• Human review
• Appeal
• Audit

Do not expose moderation internals unnecessarily.

────────────────────────────────────────

MESSAGING DOMAIN

Implement trip-scoped rider-driver messaging.

Support:

• Conversation creation
• Message creation
• Message retrieval
• Read state
• Delivery state
• Attachments where explicitly supported
• Message expiration
• Safety moderation
• Trip association

A conversation should be bound to an authorized trip context.

────────────────────────────────────────

MESSAGE LIFECYCLE

Support:

• Created
• Queued
• Delivered
• Read
• Failed
• Expired
• Removed by moderation

Use server timestamps.

Do not trust client timestamps for ordering.

────────────────────────────────────────

MESSAGE DELIVERY

Use WebSockets/Socket.IO for real-time delivery.

Fallback:

• Persisted messages
• Push notification

Support:

• Reconnection
• Duplicate message suppression
• Delivery acknowledgment
• Read receipts
• Offline retrieval

────────────────────────────────────────

MESSAGE AUTHORIZATION

A user may access a conversation only if:

• They are an authorized trip participant
• The trip state allows messaging
• The conversation has not expired
• They are not blocked/restricted by safety rules

Do not expose private contact details.

────────────────────────────────────────

MESSAGE SECURITY

Protect against:

• Spam
• Flooding
• Malicious attachments
• Phishing
• Harassment
• Contact-information leakage
• Message scraping

Apply:

• Rate limits
• Content validation
• Attachment validation
• Abuse detection
• Moderation boundaries

────────────────────────────────────────

NOTIFICATION DOMAIN

Implement:

• Notification creation
• Notification routing
• Notification template
• Notification preference
• Delivery state
• Read state
• Deduplication
• Scheduling
• Expiration

Channels:

• Push
• In-app
• Email
• SMS where approved

────────────────────────────────────────

NOTIFICATION TYPES

Support:

• Ride requested
• Driver assigned
• Driver arriving
• Driver arrived
• Trip started
• Trip completed
• Cancellation
• Payment
• Receipt
• Promotion
• Safety
• Support
• Rating reminder
• Business trip
• Account security

────────────────────────────────────────

NOTIFICATION PREFERENCES

Support:

• Account security
• Trip activity
• Driver activity
• Promotions
• Marketing
• Safety
• Support
• Business notifications

Security-critical notifications cannot be disabled when policy requires mandatory delivery.

────────────────────────────────────────

PUSH NOTIFICATIONS

Implement:

• Device token registration
• FCM
• APNS
• Token rotation
• Invalid token cleanup
• Retry
• Backoff
• Deduplication

Support multiple devices.

────────────────────────────────────────

NOTIFICATION QUEUES

Use BullMQ.

Queues:

• Push notifications
• Email notifications
• SMS notifications
• Notification retries
• Scheduled notifications
• Cleanup

Each job must be:

• Idempotent
• Retryable
• Observable
• Time-bounded

────────────────────────────────────────

SAFETY DOMAIN

Implement safety incident architecture.

Support:

• Safety incident
• Severity
• Trip
• Rider/driver
• Category
• Description
• Evidence references
• Current state
• Escalation
• Resolution
• Audit

Categories may include:

• Harassment
• Threat
• Accident
• Unsafe driving
• Assault
• Suspicious activity
• Other configured safety categories

────────────────────────────────────────

SAFETY STATES

Support:

• Reported
• Acknowledged
• Investigating
• Escalated
• Action Taken
• Resolved
• Closed
• Reopened

High-severity incidents must support urgent escalation workflows.

────────────────────────────────────────

EMERGENCY ASSISTANCE BOUNDARY

Create backend integration boundaries for emergency assistance.

Support:

• Emergency action
• Incident reference
• Trip context
• Current location where authorized
• Emergency metadata
• Escalation state

Do not represent the software as replacing emergency services.

────────────────────────────────────────

TRIP SHARING

Implement:

• Create share
• Recipient
• Trip scope
• Expiration
• Revocation
• Shared view

The shared view may expose:

• Trip status
• Driver
• Vehicle
• Pickup
• Destination
• ETA
• Current location during authorized trip state

Do not expose payment details.

────────────────────────────────────────

TRIP-SHARE SECURITY

Use:

• Short-lived tokens
• Explicit trip binding
• Expiration
• Revocation
• Rate limiting

Do not use permanent public URLs as indefinite trip-access mechanisms.

────────────────────────────────────────

TRUSTED CONTACTS

Support:

• Trusted contact
• Contact verification
• Notification preference
• Trip-share preference
• Emergency preference

Validate contact ownership or authorization where appropriate.

────────────────────────────────────────

BLOCKING

Implement:

• Rider blocks driver
• Driver blocks rider
• Account-level block where supported
• Block expiration where policy allows

Blocking should influence future matching.

Do not expose the full blocking history.

────────────────────────────────────────

REPORTING

Support reports for:

• Safety
• Fraud
• Harassment
• Payment
• Driver behavior
• Rider behavior
• Technical issue

A report may create or attach to:

• Support case
• Moderation case
• Fraud case
• Safety incident

────────────────────────────────────────

FRAUD DOMAIN

Implement fraud/risk architecture.

Signals may include:

ACCOUNT

• Account age
• Device behavior
• Authentication patterns

PAYMENT

• Payment behavior
• Chargebacks
• Failed payments

TRIP

• Cancellation pattern
• Trip frequency
• Route anomalies
• Rider/driver relationships

LOCATION

• GPS anomalies
• Impossible movement
• Repeated suspicious routes

PROMOTION

• Referral behavior
• Promo redemption patterns

DEVICE

• Device fingerprint references where legally and technically appropriate
• Emulator/root/jailbreak signals where available

────────────────────────────────────────

RISK ENGINE

Implement:

• Risk evaluation
• Signal collection
• Rule evaluation
• Risk score
• Decision
• Reason references

Possible decisions:

• Allow
• Allow with monitoring
• Challenge
• Review
• Restrict
• Block

Do not store opaque unexplained risk values without associated decision metadata.

────────────────────────────────────────

FRAUD CASES

Support:

• Case creation
• Assignment
• Investigation
• Evidence
• Decision
• Appeal
• Resolution

Cases must be auditable.

────────────────────────────────────────

FRAUD EVENTS

Publish:

• RiskEvaluationCreated
• RiskDecisionCreated
• FraudCaseOpened
• FraudCaseUpdated
• FraudCaseResolved
• AccountRiskChanged

Consumers must be idempotent.

────────────────────────────────────────

SUPPORT DOMAIN

Implement:

• Support case
• User
• Trip
• Category
• Priority
• SLA
• Assignment
• Messages
• Evidence
• Resolution
• Reopen

Categories:

• Trip
• Payment
• Refund
• Lost item
• Driver
• Rider
• Safety
• Account
• Technical

────────────────────────────────────────

SUPPORT CASE STATE

Support:

• Created
• Assigned
• Investigating
• Waiting on User
• Waiting on Internal Team
• Resolved
• Closed
• Reopened

────────────────────────────────────────

SUPPORT ACCESS

Support agents should see only information necessary for resolution.

Sensitive data must be masked.

Location and safety details require additional authorization.

────────────────────────────────────────

LOST ITEM WORKFLOW

Support:

• Lost item report
• Trip association
• Driver notification
• Rider communication
• Item status
• Resolution

Do not disclose personal contact details unnecessarily.

────────────────────────────────────────

BUSINESS ACCOUNTS

Implement:

• Business organization
• Business members
• Business roles
• Business profile
• Business payment reference
• Cost centers
• Spending limits
• Ride policies
• Employee eligibility
• Business receipts

Roles may include:

• Owner
• Admin
• Billing Admin
• Travel Manager
• Employee

────────────────────────────────────────

BUSINESS MEMBER MANAGEMENT

Support:

• Invite
• Accept
• Remove
• Suspend
• Role assignment
• Department
• Cost center

Ensure one business organization cannot access another organization's data.

────────────────────────────────────────

BUSINESS TRIPS

Support:

• Business ride profile
• Cost center
• Department
• Business purpose
• Expense metadata
• Policy validation
• Receipt classification

Do not mix business and personal trip accounting.

────────────────────────────────────────

BUSINESS POLICIES

Support:

• Allowed categories
• Spending limit
• Service hours
• Geographic restriction
• Approval requirement
• Payment method restriction

Policies are versioned configuration.

────────────────────────────────────────

BUSINESS BILLING

Integrate with the financial architecture.

Support:

• Business payment reference
• Billing account reference
• Invoice reference
• Payment status
• Business receipt

Do not duplicate the payment ledger.

────────────────────────────────────────

ANALYTICS

Implement operational analytics interfaces.

Track:

OPERATIONS

• Ride requests
• Match rate
• Offer acceptance
• Driver availability
• ETA
• Trip completion
• Cancellation

SAFETY

• Incidents
• Incident categories
• Resolution time
• Escalation

FRAUD

• Risk evaluations
• Risk decisions
• Fraud cases
• False-positive review

SUPPORT

• Case volume
• Resolution time
• Reopen rate
• Category distribution

BUSINESS

• Business trips
• Spend
• Usage
• Policy violations

Do not store unlimited raw telemetry in PostgreSQL.

────────────────────────────────────────

ANALYTICS PIPELINE

Use:

Event
→ Kafka
→ Validation
→ Processing
→ Aggregation
→ Analytics storage

Analytics must not block transactional APIs.

────────────────────────────────────────

ADMINISTRATIVE WORKFLOWS

Support controlled administrative actions for:

• Rating moderation
• Review moderation
• Messaging investigation
• Safety
• Fraud
• Support
• Business accounts
• Notification configuration
• Block management
• Risk-policy review

High-risk operations require:

• Permission
• Reason
• Audit
• Confirmation

────────────────────────────────────────

DATABASE

Implement Prisma models and migrations for:

• Rating
• RatingAggregate
• Review
• ReviewModeration
• Conversation
• ConversationParticipant
• Message
• MessageDelivery
• Notification
• NotificationPreference
• NotificationDelivery
• PushToken
• SafetyIncident
• SafetyAction
• TripShare
• TrustedContact
• BlockedEntity
• UserReport
• FraudRiskEvaluation
• FraudCase
• FraudCaseAction
• SupportCase
• SupportCaseMessage
• SupportCaseEvidenceReference
• BusinessAccount
• BusinessMember
• BusinessRole
• BusinessPolicy
• BusinessTripMetadata
• BusinessCostCenter
• BusinessReceiptReference
• AnalyticsReference where required

Use:

• Primary keys
• Foreign keys
• Unique constraints
• Composite indexes
• Status fields
• Version fields
• Expiration timestamps

Partition high-volume tables where appropriate.

────────────────────────────────────────

DATABASE CONSISTENCY

Use transactions for:

• Rating submission
• Block creation
• Support-case creation
• Business-member changes
• Policy changes
• Trip-share creation/revocation
• Notification state changes
• Fraud-case transitions

Use idempotency for retried mutations.

────────────────────────────────────────

REDIS

Use Redis for:

• Notification deduplication
• Rate limiting
• WebSocket coordination
• Message delivery state
• Trip-share short-lived state
• Risk-evaluation caching where appropriate
• Support-rate limiting
• Business-policy caching

Redis must not be authoritative for:

• Safety incidents
• Fraud cases
• Support cases
• Ratings
• Business ownership
• Financial records

────────────────────────────────────────

KAFKA EVENTS

Publish:

RATINGS

• RatingSubmitted
• RatingAggregated
• ReviewSubmitted
• ReviewModerationChanged

MESSAGING

• ConversationCreated
• MessageCreated
• MessageDelivered
• MessageRead
• MessageExpired

NOTIFICATIONS

• NotificationCreated
• NotificationDelivered
• NotificationFailed

SAFETY

• SafetyIncidentCreated
• SafetyIncidentEscalated
• SafetyActionTaken
• TripShareCreated
• TripShareRevoked

FRAUD

• RiskEvaluationCreated
• RiskDecisionCreated
• FraudCaseCreated
• FraudCaseResolved

SUPPORT

• SupportCaseCreated
• SupportCaseAssigned
• SupportCaseResolved
• SupportCaseReopened

BUSINESS

• BusinessAccountCreated
• BusinessMemberAdded
• BusinessMemberRemoved
• BusinessPolicyChanged
• BusinessTripCreated

All events must be:

• Versioned
• Idempotently consumable
• Minimal
• Auditable where required

────────────────────────────────────────

BACKGROUND JOBS

Implement BullMQ jobs for:

• Rating aggregation
• Review moderation
• Notification delivery
• Message cleanup
• Expired trip-share cleanup
• Trusted-contact verification
• Fraud-risk processing
• Fraud-case reminders
• Support SLA monitoring
• Support escalation
• Business-policy synchronization
• Analytics aggregation
• Notification cleanup
• Report generation

Every job must support:

• Retry
• Backoff
• Timeout
• Idempotency
• Dead-letter handling
• Metrics
• Structured logging

────────────────────────────────────────

API

Implement production-ready REST APIs.

RATINGS

• Submit rating
• Get rating eligibility
• Get rating summary
• Submit review
• Report review

MESSAGING

• Get conversation
• List messages
• Send message
• Mark read
• Report message

NOTIFICATIONS

• List notifications
• Mark read
• Mark all read
• Get preferences
• Update preferences
• Register device token

SAFETY

• Create safety incident
• Get incident
• Add evidence reference
• Request assistance boundary
• Get safety status

TRIP SHARING

• Create share
• Get shared-trip status
• Revoke share

TRUSTED CONTACTS

• Add contact
• Verify contact
• Remove contact
• List contacts

BLOCKING

• Block user
• Unblock user
• List blocked entities

REPORTING

• Create report
• Get report status

SUPPORT

• Create case
• Get case
• Add message
• Add evidence reference
• Reopen case

BUSINESS

• Create business account
• Get business account
• Update business account
• Invite member
• Remove member
• Assign role
• Manage cost centers
• Manage policies
• Get business trips
• Get business receipts

ADMIN

• Manage ratings
• Moderate reviews
• Review safety
• Review fraud
• Manage support
• Manage business accounts
• Manage policies

Every endpoint must implement:

• Authentication
• Authorization
• Resource ownership
• Profile/business scoping
• Validation
• Rate limiting
• Idempotency
• OpenAPI
• Consistent errors
• Audit where required

────────────────────────────────────────

REAL-TIME APIs

Implement WebSocket/Socket.IO events for:

MESSAGING

• message.created
• message.delivered
• message.read

NOTIFICATIONS

• notification.created

SAFETY

• trip.safety.updated

TRIP SHARING

• trip-share.updated

SUPPORT

• support-case.updated where appropriate

All subscriptions require authorization.

────────────────────────────────────────

SECURITY

Protect against:

• Message abuse
• Notification spam
• Safety-data leakage
• Fraud-signal leakage
• Support-data leakage
• Business-data leakage
• Cross-organization access
• Trip-share token theft
• Rating manipulation
• Review manipulation
• Administrative privilege escalation

Implement:

• RBAC
• Resource ownership
• Business isolation
• Rate limiting
• Secure tokens
• Audit logging
• Least privilege

────────────────────────────────────────

PRIVACY

Protect:

• Safety incidents
• Emergency information
• Precise trip information
• Private messages
• Fraud signals
• Support conversations
• Business travel data
• Trusted contacts

Minimize retention where appropriate.

Apply strict access controls.

────────────────────────────────────────

OBSERVABILITY

Instrument:

• Rating submission
• Message creation
• Message delivery
• Notification delivery
• Safety incident creation
• Trip sharing
• Risk evaluation
• Fraud cases
• Support cases
• Business operations

Track:

• Message delivery latency
• Notification delivery rate
• Safety escalation latency
• Fraud-processing latency
• Support SLA breaches
• Business-policy evaluation latency
• Rating submission failures

Never log:

• Private messages unnecessarily
• Safety evidence unnecessarily
• Fraud-risk details unnecessarily
• Secrets
• Authentication credentials

────────────────────────────────────────

TESTING

UNIT TESTS

Test:

• Rating eligibility
• Rating uniqueness
• Review moderation
• Message authorization
• Notification routing
• Notification preferences
• Trip-share expiration
• Trusted contacts
• Blocking
• Fraud decisions
• Support state machine
• Business-policy evaluation

INTEGRATION TESTS

Test:

• PostgreSQL
• Redis
• Kafka
• BullMQ
• WebSockets
• Notification providers
• Object storage

MESSAGING TESTS

Test:

• Delivery
• Retry
• Duplicate suppression
• Reconnect
• Read receipts
• Authorization
• Rate limiting

SAFETY TESTS

Test:

• Incident creation
• Escalation
• Access control
• Trip-share expiration
• Revocation

FRAUD TESTS

Test:

• Risk evaluation
• Rule execution
• Decision thresholds
• Duplicate signals
• Case creation
• Appeals

SUPPORT TESTS

Test:

• Case creation
• Assignment
• SLA
• Escalation
• Reopen

BUSINESS TESTS

Test:

• Organization isolation
• Member roles
• Policy enforcement
• Cost-center assignment
• Business-trip classification

SECURITY TESTS

Test:

• Cross-user access
• Cross-business access
• Safety-data access
• Support-data access
• Fraud-data access
• Admin privilege escalation

PERFORMANCE TESTS

Test:

• Messaging throughput
• Notification throughput
• Safety incident creation
• Risk evaluation
• Support-case throughput

────────────────────────────────────────

DOCUMENTATION

Generate:

• Ratings architecture
• Review architecture
• Messaging architecture
• WebSocket messaging
• Notification architecture
• Safety architecture
• Emergency assistance boundary
• Trip-sharing architecture
• Trusted contacts
• Blocking
• Reporting
• Fraud/risk architecture
• Support architecture
• Business-account architecture
• Business-policy architecture
• Business-trip architecture
• Analytics architecture
• API contracts
• Event contracts
• Queue catalog
• Database schema
• Redis key catalog
• Security model
• Privacy model
• Testing strategy

────────────────────────────────────────

PROJECT INDEX

Update the backend Project Index with:

• Ratings
• Rating aggregates
• Reviews
• Review moderation
• Messaging
• Conversations
• Messages
• Notifications
• Notification preferences
• Push tokens
• Safety
• Trip sharing
• Trusted contacts
• Blocking
• Reporting
• Fraud
• Risk
• Fraud cases
• Support
• Business accounts
• Business members
• Business policies
• Business trips
• Cost centers
• Business receipts
• Analytics
• Database objects
• Migrations
• APIs
• WebSocket events
• Kafka topics
• BullMQ queues
• Workers
• Redis keys
• Audit
• Security
• Privacy
• Tests
• Generated files
• Remaining work
• Current milestone
• Dependencies

────────────────────────────────────────

IMPLEMENTATION MILESTONES

BACKEND MILESTONE 51

Ratings, rating eligibility, rating aggregation, reviews, review moderation, and rating APIs.

BACKEND MILESTONE 52

Messaging, conversations, messages, WebSocket delivery, read state, message expiration, and abuse protection.

BACKEND MILESTONE 53

Notifications, notification preferences, push-token registration, FCM/APNS integration, email/SMS abstraction, delivery queues, retry, and deduplication.

BACKEND MILESTONE 54

Safety incidents, escalation, emergency-assistance boundary, safety actions, evidence references, and safety APIs.

BACKEND MILESTONE 55

Trip sharing, trusted contacts, secure share tokens, expiration, revocation, blocking, and reporting.

BACKEND MILESTONE 56

Fraud signals, risk evaluation, risk decisions, fraud cases, review workflows, appeals, and fraud events.

BACKEND MILESTONE 57

Support cases, case messaging, evidence references, SLA tracking, escalation, lost-item workflow, and support APIs.

BACKEND MILESTONE 58

Business accounts, business members, roles, cost centers, business policies, employee eligibility, and organization isolation.

BACKEND MILESTONE 59

Business trips, business receipt integration, analytics events, administrative workflows, audit integration, and operational reporting.

BACKEND MILESTONE 60

Security hardening, privacy validation, cross-tenant isolation, concurrency testing, performance testing, resilience testing, and production readiness.

Each milestone should contain approximately 20–40 files where practical.

Every milestone must compile before proceeding.

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never truncate code.

Never summarize source code instead of generating it.

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

This volume covers:

• Ratings
• Reviews
• Messaging
• Notifications
• Safety
• Trip sharing
• Trusted contacts
• Blocking
• Reporting
• Fraud
• Risk
• Fraud cases
• Support
• Business accounts
• Business members
• Business policies
• Business trips
• Cost centers
• Business receipt integration
• Operational analytics interfaces
• Administrative workflows
• Related events
• Related queues and workers

Do not redesign or reimplement:

• Identity
• Driver onboarding
• Location
• Dispatch
• Matching
• Trip lifecycle
• Pricing
• Payments
• Wallets
• Earnings
• Payouts

Use the previously established systems and contracts.

Do not implement:

• Frontend
• Mobile
• Infrastructure
• Terraform
• Kubernetes
• CI/CD

────────────────────────────────────────

QUALITY BAR

Treat safety, fraud, messaging, business accounts, and support as sensitive enterprise systems.

Assume:

• Hundreds of millions of riders
• Millions of drivers
• Large messaging volumes
• Large notification volumes
• Millions of support cases
• High fraud-signal volumes
• Multiple business organizations
• Multiple regions
• Sensitive safety information
• Strict privacy requirements
• Strict authorization requirements

Prioritize:

• Safety
• Privacy
• Security
• Tenant isolation
• Reliable messaging
• Notification reliability
• Fraud resilience
• Auditability
• Idempotency
• Scalability
• Observability
• Production readiness
