You are operating in Senior Engineering Team Mode.

Build the production-ready backend for identity, rider accounts, driver accounts, authentication, authorization, sessions, devices, driver onboarding, driver verification, vehicle management, vehicle verification, and driver eligibility for an enterprise-scale global ride-hailing and mobility platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

The backend must follow the approved Uber-like architecture, domain boundaries, database ownership, API conventions, event architecture, Redis architecture, PostGIS architecture, security model, and Project Index.

Do not redesign the architecture.

Do not generate frontend code.

Do not generate mobile code.

Do not generate infrastructure implementation code.

Do not generate Terraform.

Do not generate Kubernetes manifests.

Do not generate CI/CD workflows.

────────────────────────────────────────

MISSION

Implement the production-ready backend domains for:

• Users
• Accounts
• Profiles
• Riders
• Drivers
• Authentication
• Authorization
• Sessions
• Devices
• Driver onboarding
• Driver verification
• Driver documents
• Driver eligibility
• Vehicles
• Vehicle categories
• Vehicle verification
• Insurance records
• Driver status
• Driver compliance
• Driver organization boundaries

The implementation must support:

• Hundreds of millions of rider accounts
• Millions of drivers
• Multiple devices per user
• Multiple driver vehicles where permitted
• Regional driver requirements
• Driver verification workflows
• Document expiration
• Vehicle verification
• Driver suspension
• Account recovery
• Secure sessions
• Role-based access control
• Organization-scoped permissions

────────────────────────────────────────

TECHNOLOGY STACK

Backend:

• Node.js
• NestJS
• TypeScript

Database:

• PostgreSQL
• Prisma ORM
• PostGIS where geospatial entities require it

Cache:

• Redis

Event Streaming:

• Kafka or Redpanda

Background Processing:

• BullMQ

External Providers:

• Identity verification provider abstraction
• Background-check provider abstraction
• Document-verification abstraction
• Payment provider abstraction
• Notification provider abstraction

Testing:

• Jest
• Supertest
• Integration testing tools

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

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

Use DTOs for external contracts.

Use centralized validation.

Use centralized error handling.

Use structured logging.

Use idempotency for security-sensitive and verification workflows.

Never trust client-supplied ownership or organization identifiers.

────────────────────────────────────────

DOMAIN OWNERSHIP

Maintain explicit boundaries between:

• Identity
• Accounts
• Profiles
• Riders
• Drivers
• Authentication
• Authorization
• Sessions
• Devices
• Driver onboarding
• Driver verification
• Documents
• Vehicles
• Vehicle verification
• Eligibility
• Compliance

Do not combine:

• User identity with driver eligibility
• Driver availability with driver account state
• Vehicle ownership with trip state
• Verification results with raw provider responses

────────────────────────────────────────

IDENTITY

Implement:

• User creation
• User lookup
• User status
• Identity lifecycle
• Account association
• Account activation
• Account suspension
• Account deactivation
• Account deletion workflow

Support states:

• Pending
• Active
• Suspended
• Disabled
• Deactivated
• Deleted

Use stable public identifiers.

Do not expose internal database IDs unnecessarily.

────────────────────────────────────────

RIDER DOMAIN

Implement:

• Rider profile
• Rider preferences
• Saved locations
• Accessibility preferences
• Safety preferences
• Payment-method references
• Account status

Keep rider-specific data separate from generic identity.

────────────────────────────────────────

DRIVER DOMAIN

Implement:

• Driver profile
• Driver status
• Driver eligibility
• Driver region
• Driver category eligibility
• Driver onboarding state
• Driver suspension
• Driver activation
• Driver deactivation

Driver states may include:

• Registered
• Onboarding
• Verification Pending
• Verified
• Active
• Suspended
• Deactivated

Separate:

• Account status
• Verification state
• Eligibility state
• Availability state
• Current trip state

────────────────────────────────────────

DRIVER ONBOARDING

Implement:

• Driver application
• Personal information
• Driver-license reference
• Document submission
• Vehicle submission
• Insurance submission
• Verification requests
• Application review
• Approval
• Rejection
• Re-submission

Support state transitions:

Draft
→ Submitted
→ Review
→ Verification Pending
→ Approved
→ Rejected
→ Resubmission
→ Suspended

All transitions must be:

• Authorized
• Idempotent
• Auditable

────────────────────────────────────────

DRIVER DOCUMENTS

Support:

• Document type
• Document reference
• Issuing region
• Expiration date
• Verification status
• Rejection reason
• Review state

Examples:

• Driver license
• Registration
• Insurance
• Background-check reference
• Other region-specific requirements

Do not store raw sensitive documents unnecessarily.

Where documents must be uploaded, use secure object-storage references and signed upload workflows.

────────────────────────────────────────

DOCUMENT EXPIRATION

Implement:

• Expiration detection
• Reminder scheduling
• Eligibility suspension
• Re-verification
• Renewal

Use BullMQ for scheduled expiration processing.

Do not rely on clients to determine whether a document has expired.

────────────────────────────────────────

VERIFICATION PROVIDER ABSTRACTION

Create provider-neutral interfaces for:

• Identity verification
• Driver license verification
• Background checks
• Vehicle verification
• Insurance verification

Provider responses must be normalized before entering the domain.

Do not allow provider-specific data models to leak into core domain entities.

────────────────────────────────────────

VERIFICATION WORKFLOW

Implement:

Request
→ Provider Submission
→ Provider Processing
→ Result
→ Internal Validation
→ Approval/Review/Reject

Handle:

• Provider timeout
• Provider outage
• Duplicate request
• Delayed result
• Inconsistent provider result
• Provider callback/webhook

Never trust an unverified provider callback.

────────────────────────────────────────

DRIVER ELIGIBILITY

Eligibility should depend on:

• Driver verification
• Required documents
• Vehicle verification
• Insurance
• Regional rules
• Driver status
• Compliance state

Eligibility may determine whether a driver can:

• Go online
• Accept trips
• Operate a category
• Enter specific service areas

Availability remains a separate state.

────────────────────────────────────────

VEHICLE DOMAIN

Implement:

• Vehicle registration
• Vehicle profile
• Make
• Model
• Year
• Color
• License plate
• VIN/reference where legally appropriate
• Capacity
• Accessibility capabilities
• Fuel/power type
• Vehicle category
• Verification status
• Insurance status

Use appropriate regional validation.

────────────────────────────────────────

VEHICLE CATEGORIES

Support configurable categories such as:

• Economy
• Standard
• Premium
• XL
• Accessible
• Electric
• Other market-specific categories

Do not hard-code category rules into every service.

Define category configuration for:

• Capacity
• Fare eligibility
• Driver eligibility
• Region
• Service hours
• Accessibility requirements

────────────────────────────────────────

VEHICLE VERIFICATION

Implement:

• Verification submission
• Inspection reference
• Required documents
• Verification state
• Expiration
• Suspension
• Renewal

Vehicle states may include:

• Draft
• Submitted
• Pending Review
• Verified
• Rejected
• Suspended
• Expired

────────────────────────────────────────

INSURANCE

Support:

• Policy reference
• Provider
• Coverage metadata
• Effective date
• Expiration date
• Verification state

Do not store unnecessary raw insurance documents indefinitely.

────────────────────────────────────────

DRIVER COMPLIANCE

Support:

• Compliance requirements
• Regional rules
• Required documents
• Expiration
• Verification
• Suspension
• Reinstatement

Model regional requirements as configuration/policy data where possible.

────────────────────────────────────────

REGIONAL DRIVER RULES

Support region-specific:

• Minimum age
• Required license
• Insurance
• Vehicle age
• Vehicle inspection
• Required documents
• Driver training
• Service-category restrictions

Do not hard-code a single city's requirements into the driver domain.

────────────────────────────────────────

ACCOUNT AUTHENTICATION

Implement:

• Registration
• Login
• Logout
• Token refresh
• Email verification
• Password reset
• Password change
• Session restoration

Prepare for:

• OAuth
• MFA
• Passkeys

Never store plaintext passwords.

────────────────────────────────────────

PASSWORD SECURITY

Use industry-standard password hashing.

Support:

• Password verification
• Password reset
• Reset-token expiration
• Single-use reset tokens
• Password-change invalidation
• Login-attempt protection
• Rate limiting

Never log passwords.

Never expose password hashes.

────────────────────────────────────────

SESSION MANAGEMENT

Implement:

• Session creation
• Session listing
• Session expiration
• Session refresh
• Session revocation
• Logout-all-sessions

Track:

• Device
• Platform
• Application version
• Creation time
• Last activity
• Expiration
• Revocation state

Do not store unnecessary secrets.

────────────────────────────────────────

DEVICE MANAGEMENT

Implement:

• Device registration
• Device identification
• Platform
• Application version
• Push-token reference
• Session association
• Device revocation

Support:

• Rider devices
• Driver devices

Device authorization must remain distinct from account authentication.

────────────────────────────────────────

AUTHORIZATION

Implement:

• RBAC
• Permissions
• Resource ownership
• Rider scope
• Driver scope
• Administrative scope
• Organization scope

Roles may include:

• Rider
• Driver
• Driver Manager where applicable
• Verification Agent
• Support Agent
• Moderator
• Administrator
• Super Administrator
• System Service

────────────────────────────────────────

RESOURCE AUTHORIZATION

Verify ownership for:

• Driver profiles
• Driver documents
• Vehicles
• Onboarding applications
• Verification records
• Sessions
• Devices

Never trust a client-provided user/driver ID as proof of authorization.

────────────────────────────────────────

ADMINISTRATIVE DRIVER ACTIONS

Support authorized administrators to:

• View driver
• Review onboarding
• Review verification
• Suspend driver
• Reinstate driver
• Review vehicle
• Suspend vehicle
• Approve documents
• Reject documents

High-risk operations require:

• Explicit permissions
• Reason
• Audit event

────────────────────────────────────────

DATABASE

Implement Prisma models and migrations for:

• User
• Account
• Profile
• Rider
• Driver
• Session
• Device
• Role
• Permission
• RolePermission
• UserRole
• DriverApplication
• DriverDocument
• DriverVerification
• VerificationRequest
• VerificationResultReference
• DriverEligibility
• DriverCompliance
• Vehicle
• VehicleCategory
• VehicleDocument
• VehicleVerification
• InsurancePolicyReference
• RegionalRequirement
• DriverRegionEligibility

Use:

• Primary keys
• Foreign keys
• Unique constraints
• Composite indexes
• Check constraints
• Status fields
• Effective dates
• Expiration dates

────────────────────────────────────────

DATABASE CONSISTENCY

Use transactions for:

• User/account creation
• Driver creation
• Vehicle creation
• Role assignment
• Driver status transitions
• Verification state transitions
• Vehicle eligibility transitions
• Document state transitions

Do not use distributed transactions with external verification providers.

Use:

• Idempotency
• Provider references
• Webhooks
• Reconciliation

────────────────────────────────────────

REDIS

Use Redis for:

• Session cache
• Rate limiting
• Verification rate limits
• Temporary verification state
• Short-lived authorization state
• Idempotency
• Notification deduplication

Do not use Redis as authoritative storage for:

• Driver state
• Vehicle state
• Verification history
• Compliance state

────────────────────────────────────────

EVENTS

Publish:

IDENTITY

• UserCreated
• AccountCreated
• AccountActivated
• AccountSuspended

AUTHENTICATION

• UserLoggedIn
• SessionCreated
• SessionRevoked
• DeviceRegistered
• DeviceRevoked

DRIVERS

• DriverRegistered
• DriverApplicationSubmitted
• DriverVerificationStarted
• DriverVerified
• DriverRejected
• DriverSuspended
• DriverReinstated
• DriverEligibilityChanged

DOCUMENTS

• DriverDocumentSubmitted
• DriverDocumentVerified
• DriverDocumentRejected
• DriverDocumentExpired

VEHICLES

• VehicleRegistered
• VehicleSubmitted
• VehicleVerified
• VehicleRejected
• VehicleSuspended
• VehicleExpired

INSURANCE

• InsuranceSubmitted
• InsuranceVerified
• InsuranceExpired

Events must contain only information required by consumers.

Do not publish raw sensitive documents or credentials.

────────────────────────────────────────

BACKGROUND JOBS

Implement BullMQ jobs for:

• Email verification expiry
• Password-reset expiry
• Session cleanup
• Document expiration
• Insurance expiration
• Driver eligibility recalculation
• Verification retry
• Provider reconciliation
• Vehicle verification reminders
• Compliance reminders

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

AUTHENTICATION

• Register
• Login
• Logout
• Refresh
• Verify email
• Password reset
• Password change

ACCOUNTS

• Get account
• Update account
• Security settings

PROFILES

• Get profile
• Update profile

DEVICES

• Register device
• List devices
• Revoke device

SESSIONS

• List sessions
• Revoke session
• Revoke all sessions

RIDERS

• Get rider
• Update rider
• Saved locations foundation
• Preferences

DRIVERS

• Register driver
• Get driver
• Update driver
• Driver status
• Eligibility

ONBOARDING

• Create application
• Get application
• Submit application
• Upload document authorization
• List documents
• Replace document

VEHICLES

• Create vehicle
• Get vehicle
• Update vehicle
• List vehicles
• Submit for verification
• Remove vehicle

VERIFICATION

• Get verification status
• Retry verification where permitted

ADMIN

• Search drivers
• Review application
• Review documents
• Approve/reject
• Suspend/reinstate

Every endpoint must implement:

• Authentication
• Authorization
• Validation
• Rate limiting
• Idempotency where appropriate
• OpenAPI
• Consistent error handling
• Audit requirements

────────────────────────────────────────

SECURITY

Protect against:

• Account takeover
• Credential stuffing
• Session hijacking
• Token replay
• IDOR
• Driver impersonation
• Cross-user access
• Document enumeration
• Organization escalation
• Verification manipulation
• Admin privilege escalation

Use:

• Rate limiting
• Secure sessions
• RBAC
• Resource ownership
• Short-lived verification operations
• Audit logging

────────────────────────────────────────

PRIVACY

Protect:

• Personal identity data
• Driver documents
• License information
• Insurance information
• Device metadata
• Verification results
• Background-check information

Minimize stored sensitive data.

Use secure references for external documents.

Do not expose provider-sensitive verification details to ordinary clients.

────────────────────────────────────────

OBSERVABILITY

Instrument:

• Registration
• Login
• Session creation
• Session revocation
• Driver onboarding
• Verification requests
• Verification results
• Document processing
• Vehicle verification
• Eligibility recalculation
• Administrative actions

Track:

• Login failure rate
• Verification latency
• Verification failure rate
• Application completion
• Document rejection rate
• Driver approval latency
• Eligibility failures
• Provider errors

Never log:

• Passwords
• Authentication tokens
• Private documents
• Verification secrets
• Provider credentials

────────────────────────────────────────

TESTING

UNIT TESTS

Test:

• Authentication
• Password policy
• Session lifecycle
• Authorization
• Driver eligibility
• Verification state machine
• Vehicle state machine
• Document expiry
• Regional requirement rules

INTEGRATION TESTS

Test:

• PostgreSQL
• Prisma
• PostGIS where applicable
• Redis
• Kafka
• BullMQ
• Provider abstractions

SECURITY TESTS

Test:

• IDOR
• Horizontal privilege escalation
• Vertical privilege escalation
• Driver impersonation
• Document access
• Admin access
• Session replay

CONCURRENCY TESTS

Test:

• Concurrent verification requests
• Duplicate document submission
• Duplicate driver registration
• Concurrent role changes
• Concurrent vehicle updates
• Duplicate provider callbacks

PROVIDER TESTS

Test:

• Timeout
• Delayed response
• Failure
• Duplicate callback
• Malformed result
• Unknown result

PERFORMANCE TESTS

Test:

• Login
• Session validation
• Driver lookup
• Eligibility lookup
• Verification status

────────────────────────────────────────

DOCUMENTATION

Generate:

• Identity architecture
• Rider architecture
• Driver architecture
• Authentication
• Authorization
• Sessions
• Devices
• Driver onboarding
• Verification
• Documents
• Vehicle management
• Vehicle verification
• Insurance
• Driver eligibility
• Regional requirements
• API contracts
• Database schema
• Events
• Queues
• Security
• Privacy
• Testing

────────────────────────────────────────

PROJECT INDEX

Update the backend Project Index with:

• Identity modules
• Account modules
• Profile modules
• Rider modules
• Driver modules
• Authentication
• Authorization
• Session modules
• Device modules
• Driver onboarding
• Driver verification
• Document modules
• Eligibility modules
• Compliance modules
• Vehicle modules
• Vehicle verification
• Insurance modules
• Regional requirements
• Database objects
• Migrations
• API endpoints
• Events
• Queues
• Workers
• Redis usage
• Provider integrations
• Tests
• Generated files
• Remaining work
• Current milestone
• Dependencies

────────────────────────────────────────

IMPLEMENTATION MILESTONES

BACKEND MILESTONE 11

Identity, accounts, profiles, riders, drivers, sessions, and devices.

BACKEND MILESTONE 12

Authentication, password management, email verification, refresh tokens, session security, and account recovery.

BACKEND MILESTONE 13

Authorization, RBAC, resource policies, administrative permissions, and security hardening.

BACKEND MILESTONE 14

Driver onboarding, applications, document submission, document lifecycle, and verification orchestration.

BACKEND MILESTONE 15

Verification-provider integrations, provider callbacks, reconciliation, and compliance workflows.

BACKEND MILESTONE 16

Vehicles, vehicle categories, vehicle documents, vehicle verification, and insurance.

BACKEND MILESTONE 17

Driver eligibility, regional requirements, compliance rules, expiration processing, and reinstatement.

BACKEND MILESTONE 18

Administrative driver/vehicle workflows, audit integration, events, queues, and notification integration.

BACKEND MILESTONE 19

Integration, security, concurrency, provider-failure, and performance testing.

BACKEND MILESTONE 20

Production hardening, observability validation, reconciliation, documentation, and Project Index completion.

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

• Identity
• Accounts
• Profiles
• Riders
• Drivers
• Authentication
• Authorization
• Sessions
• Devices
• Driver onboarding
• Driver verification
• Driver documents
• Driver eligibility
• Driver compliance
• Vehicles
• Vehicle categories
• Vehicle verification
• Insurance
• Regional requirements
• Related events
• Related background jobs

Do not implement complete:

• Driver availability
• Driver location
• Geospatial matching
• Dispatch
• Ride requests
• Trips
• Scheduled rides
• Shared rides
• Pricing
• Surge
• Promotions
• Payments business logic
• Wallets
• Earnings
• Payouts
• Ratings
• Messaging
• Notifications business logic
• Safety
• Fraud
• Support
• Business accounts
• Analytics
• Administration UI
• Infrastructure
• Frontend
• Mobile

Those belong to later implementation volumes.

────────────────────────────────────────

QUALITY BAR

Treat rider identity, driver onboarding, verification, vehicle eligibility, and authentication as mission-critical systems.

Assume:

• Hundreds of millions of riders
• Millions of drivers
• Multiple devices
• Multiple regions
• Regional compliance requirements
• Sensitive identity data
• High login traffic
• High verification traffic
• Strict privacy requirements
• High availability
• Global operation

Prioritize:

• Security
• Privacy
• Correct authorization
• Verification correctness
• Eligibility correctness
• Auditability
• Idempotency
• Provider resilience
• Scalability
• Observability
• Maintainability
• Production readiness
