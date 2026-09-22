# Uber-Style Global Ride-Hailing & Mobility Platform — Backend Prompt — Volume 7

## ROLE

You are the senior backend engineering organization responsible for implementing the notification, delivery, rider-driver messaging, conversation, and communication-state platform of an original, production-grade global ride-hailing and mobility system.

Operate simultaneously as:

* Principal Software Architect
* Staff Backend Engineer
* Distributed Systems Engineer
* Realtime Systems Engineer
* Messaging Systems Engineer
* Notification Systems Engineer
* Database Architect
* Security Engineer
* Reliability Engineer
* Performance Engineer
* QA Engineer
* Observability Engineer
* Technical Writer

You are implementing production software, not demonstrating concepts.

Do not act as a teacher.

Do not provide pseudo-code.

Do not provide incomplete examples instead of implementation.

Do not leave TODO or FIXME placeholders for required work.

Do not omit implementations with statements such as:

* "implement similarly"
* "remaining code omitted"
* "for brevity"
* "left as an exercise"

Every required file must contain a real implementation.

# PROJECT

## Project Identity

Build an original global ride-hailing and mobility platform supporting:

* riders
* drivers
* operations personnel
* support personnel
* safety personnel
* fleet personnel
* administrators

This milestone implements the communication platform used for:

* transactional notifications
* push notifications
* email
* SMS where supported
* in-app/realtime notifications
* rider-driver messaging
* conversation management
* message delivery state
* read state
* reconnect/recovery
* communication preferences
* provider abstraction
* communication auditability

The platform is architected for targets such as:

* 100+ million riders
* 10+ million drivers
* millions of trips per day
* 100,000+ concurrent realtime sessions and higher during peak
* globally distributed users
* large asynchronous notification volumes
* high availability for critical trip communications

These are architectural targets, not measured capacity claims.

## Technology Direction

Use the locked project stack:

### Runtime

* Node.js
* TypeScript

### Framework

* NestJS

### Database

* PostgreSQL
* PostGIS where required
* Prisma where compatible with the architecture

### Cache and Ephemeral State

* Redis

### Events

* Kafka or Redpanda

### Background Jobs

* BullMQ or equivalent

### Realtime

* authenticated WebSockets

### Object Storage

* Amazon S3 where messaging attachments or communication artifacts require it

### External Communication Providers

Use provider abstractions for:

* push notifications
* email
* SMS

Do not couple communication-domain logic directly to a provider SDK.

### Observability

* OpenTelemetry
* Prometheus-compatible metrics
* structured logs
* Loki-compatible logging
* Tempo-compatible tracing

# SOURCE OF TRUTH

The repository is the implementation source of truth.

Inspect the repository before making changes.

Use the architecture artifacts already present in the repository as the authoritative architecture and communication-contract reference.

Backend Volumes 1–6 establish:

* backend platform foundations
* identity and authorization
* driver availability and location
* trip lifecycle
* dispatch
* pricing and payments
* earnings and payouts
* canonical API/error/idempotency/concurrency contracts
* event/outbox infrastructure
* realtime infrastructure

This milestone must integrate communication behavior with those established domains rather than replacing them.

Do not depend on the previous AI conversation.

If existing implementation differs from the architecture:

1. inspect the actual implementation
2. preserve compatible working behavior
3. make the minimum coherent changes required
4. document material discrepancies

Do not create competing notification, messaging, or realtime foundations.

# BACKEND EXECUTION MODEL

This milestone owns two closely related communication domains:

### Notification Platform

Own:

* notification creation
* notification preferences
* notification templates
* localization metadata
* channel selection
* delivery attempts
* provider abstraction
* retries
* deduplication
* notification state
* in-app notification records
* realtime notification delivery

### Rider-Driver Messaging

Own:

* conversations
* participants
* messages
* message ordering
* delivery state
* read state
* reconnect/recovery
* authorization
* retention boundaries
* attachment references where defined

Notifications and messaging must remain distinct concepts.

A notification informs a recipient about an event.

A message is user-generated communication between authorized participants.

# COMMUNICATION PRINCIPLES

The communication platform must satisfy:

* authenticated access
* explicit recipient authorization
* at-least-once delivery tolerance
* idempotent processing
* provider abstraction
* retry safety
* bounded retries
* privacy-aware logging
* deterministic message ordering
* reconnect recovery
* delivery-state correctness
* graceful degradation

Do not assume that:

* external providers are always available
* push delivery is immediate
* SMS/email delivery is guaranteed
* WebSocket connections remain connected
* consumers receive every event exactly once

# CURRENT IMPLEMENTATION SCOPE

## 1. Notification Domain Boundary

Establish authoritative ownership for:

* notification
* notification preference
* template/reference
* delivery attempt
* channel selection
* notification state

Notification logic may consume events from:

* trip
* dispatch
* payment
* earnings/payout
* safety
* support
* scheduled trips

but those domains remain authoritative for their own business state.

Do not duplicate their state models inside notifications.

## 2. Notification Event Intake

Implement notification consumers for the communication-triggering events required by the architecture.

Support:

* event validation
* recipient resolution
* notification categorization
* idempotency
* correlation metadata
* template/version resolution
* delivery scheduling

Do not create notification records for events that are not contractually intended to notify users.

## 3. Notification Model

Implement the canonical notification record.

Support, according to the contract:

* notification ID
* recipient
* category/type
* source domain
* source/reference ID
* template/version
* locale
* channel
* state
* creation time
* delivery metadata
* expiration where required

Do not store complete source-domain payloads unnecessarily.

## 4. Notification Preferences

Implement user notification preferences.

Support the preference dimensions actually defined by the architecture, potentially including:

* notification category
* channel
* enabled/disabled
* locale
* quiet-hours metadata where applicable

Separate mandatory transactional/safety notifications from user-configurable marketing or informational notifications when the architecture distinguishes them.

Do not allow preference settings to suppress required security or safety notifications.

## 5. Preference Authorization

Users must only modify their own preferences unless the architecture explicitly grants an authorized operational override.

Administrative changes must be permission-protected and auditable.

Do not expose provider credentials or internal notification configuration through preference APIs.

## 6. Notification Templates

Implement a versioned notification-template abstraction.

Templates must support:

* stable identifier
* version
* locale
* channel
* content structure
* active state

Do not scatter provider-specific text or formatting logic throughout domain services.

Template selection must be deterministic.

## 7. Localization

Support locale-aware notification rendering.

Use the recipient's configured locale according to the identity/client architecture.

Provide safe fallback behavior when a requested translation is unavailable.

Do not let arbitrary client input select privileged internal templates.

## 8. Channel Selection

Implement the architecture's channel-selection logic.

Potential channels include:

* push
* email
* SMS
* in-app
* realtime

Channel selection may depend on:

* user preference
* notification category
* available recipient endpoint
* operational criticality
* provider availability

Do not treat every channel as equivalent.

## 9. Notification Priority

Support notification priority where required.

Differentiate, as appropriate:

* critical
* high
* normal
* low

Priority may affect:

* queue selection
* retry behavior
* expiration
* provider strategy

Do not create unlimited priority levels.

## 10. Notification Deduplication

Prevent duplicate notifications caused by:

* duplicate events
* consumer retries
* worker retries
* reconnect logic
* provider ambiguity

Use stable source references and notification idempotency keys.

Do not rely on client-side deduplication alone.

## 11. Delivery Attempt Model

Implement delivery-attempt records where required.

Track:

* notification ID
* channel
* provider
* attempt number
* status
* provider reference
* attempt timestamp
* error category
* retryability

Do not persist provider secrets or sensitive response bodies.

## 12. Notification State Machine

Implement the canonical notification state model.

Support states appropriate to the architecture, such as:

* queued
* processing
* sent
* delivered
* failed
* expired
* suppressed
* cancelled

Use the exact repository contract.

A provider acknowledgement must not automatically be treated as user-visible delivery unless the provider semantics actually support that distinction.

## 13. Push Notification Provider Abstraction

Create a provider-neutral push interface.

The abstraction must support:

* send
* delivery/response handling where available
* provider reference
* invalid-token response
* transient failure
* permanent failure

Keep provider-specific SDKs inside adapters.

## 14. Push Token Management

Integrate push-token management with the device/account model.

Support:

* token registration
* device association
* token refresh
* token invalidation
* revoked/expired tokens
* multiple devices
* platform metadata

Do not allow arbitrary users to send notifications to tokens they do not own.

## 15. Push Token Cleanup

Automatically invalidate tokens when providers report permanent invalidity.

Cleanup must be:

* idempotent
* safe across multiple workers
* auditable where required

Do not delete a device account association merely because one push token became invalid.

## 16. Email Provider Abstraction

Implement an email-provider boundary.

Support:

* send
* provider reference
* retryable error
* permanent error
* delivery status where supported

Do not expose provider-specific SDK types outside the adapter.

## 17. SMS Provider Abstraction

Where SMS is part of the architecture, implement the same provider boundary.

Support:

* send
* provider reference
* retryable failure
* permanent failure
* delivery state where available

Do not turn SMS into a generic unrestricted messaging mechanism.

## 18. Provider Failure Classification

Classify communication-provider failures into:

* retryable
* permanent
* rate-limited
* invalid recipient
* authentication/configuration failure
* ambiguous

Do not infinitely retry permanent failures.

## 19. Notification Retry Strategy

Use the shared job infrastructure.

Implement:

* bounded retries
* exponential/backoff behavior where appropriate
* channel-specific limits
* dead-letter/terminal failure handling
* retry observability

Do not let provider outages create unbounded queue growth.

## 20. Communication Backpressure

Protect providers and workers from retry amplification.

Use:

* queue isolation where necessary
* concurrency controls
* provider rate limits
* bounded worker scaling
* expiration

A provider outage must not cause every queued notification to retry simultaneously without limits.

## 21. In-App Notifications

Implement persistent in-app notifications where defined.

Support:

* unread/read state
* creation time
* category
* target/reference
* expiration where required
* pagination

Use cursor pagination for high-volume histories.

## 22. Notification Read State

Implement read/unread state according to the contract.

Support:

* single notification read
* bulk read where permitted
* unread count
* idempotent read operations

Do not allow one user's notification state to affect another user's state.

## 23. Notification Retrieval Authorization

Recipients may access only their own notifications unless a privileged operational scope is explicitly defined.

Do not expose source-domain internal payloads through notification retrieval.

## 24. Communication Auditability

Audit security-sensitive notification operations such as:

* administrative notification
* preference override
* privileged template changes
* manual resend where supported

Do not create human-action audit records for every ordinary provider delivery attempt.

# RIDER-DRIVER MESSAGING

## 25. Conversation Model

Implement the canonical conversation aggregate.

Support:

* conversation ID
* participant references
* trip association where applicable
* creation timestamp
* status
* last-message reference
* authorization scope

A conversation associated with a trip must only be accessible to authorized participants.

## 26. Participant Authorization

Enforce participant access using authoritative identity/trip relationships.

A rider must only access conversations they participate in.

A driver must only access authorized rider conversations.

Operational personnel require explicit privileged access.

Do not authorize conversation access merely because a caller knows its ID.

## 27. Conversation Lifecycle

Implement states required by the architecture, such as:

* active
* closed
* archived

Define whether new messages are allowed in each state.

Do not let a closed conversation silently accept new messages.

## 28. Message Model

Implement the canonical message model.

Support:

* message ID
* conversation ID
* sender
* message type
* content/reference
* sequence/order metadata
* creation time
* delivery state
* edit/delete metadata where contractually supported

Do not store unnecessary duplicated participant data.

## 29. Message Ordering

Implement deterministic per-conversation ordering.

Support:

* monotonically ordered sequence where required
* server timestamp
* message ID
* conflict handling

Do not rely solely on client timestamps.

Messages must retain stable ordering after reconnect or retry.

## 30. Message Creation Idempotency

Message creation must tolerate client retries.

Use:

* client message/idempotency key
* conversation scope
* uniqueness constraints
* deterministic retry behavior

The same logical send request must not create duplicate messages.

## 31. Message Delivery State

Implement delivery-state semantics defined by the contract.

Distinguish, where applicable:

* accepted
* sent
* delivered
* read

Do not claim "delivered" merely because the server persisted the message.

## 32. Read State

Implement per-recipient read tracking.

Support:

* read timestamp
* read sequence
* unread count
* idempotent read update

Do not require writing one record per client poll if a compact sequence/watermark representation is sufficient.

## 33. Realtime Message Delivery

Integrate messaging with the authenticated WebSocket system.

Support:

* authorized conversation subscription
* new-message delivery
* read-state updates
* delivery-state updates
* reconnect
* duplicate message tolerance

Realtime delivery must be derived from authoritative message state.

## 34. Reconnect Recovery

When a client reconnects, it must be able to determine:

* messages it missed
* current read state
* current conversation state
* pending delivery state

Do not assume the client received every prior WebSocket event.

Provide bounded synchronization mechanisms.

## 35. Offline Messaging

Support message submission after temporary connectivity loss according to the client contract.

The backend must tolerate:

* retries
* delayed submission
* duplicate client attempts
* reordered network delivery

Do not rely on realtime delivery for message durability.

## 36. Message Editing and Deletion

Where Architecture Volume 2 permits message edits/deletes, implement explicit state transitions.

Support:

* authorization
* allowed time/window where applicable
* immutable original identity
* audit/reference metadata
* realtime propagation

Do not silently overwrite historical message content if the architecture requires edit history or tombstoning.

## 37. Attachment References

Where messaging supports attachments, store references to the object-storage architecture rather than arbitrary public URLs.

Validate:

* ownership
* authorization
* object state
* purpose
* attachment size/type according to the established media contract

Do not implement a second object-storage system.

## 38. Messaging Abuse Controls

Protect messaging with appropriate:

* rate limits
* message-size limits
* attachment limits
* participant validation
* spam/abuse hooks
* blocked-user checks where the trust architecture already provides them

Do not duplicate the fraud/trust system.

Expose clear integration points for the later trust/safety milestone.

## 39. Conversation Closure

Conversation closure must integrate with trip/domain state where the architecture requires it.

Do not make messaging responsible for trip state.

When an associated trip terminates, follow the documented communication lifecycle rather than arbitrarily deleting conversations.

## 40. Message Privacy

Protect message content.

Never place full message bodies into:

* Prometheus labels
* tracing attributes
* ordinary infrastructure logs
* notification delivery logs

Use redaction and metadata-only telemetry.

## 41. Message Retention

Follow the architecture's retention contract.

Differentiate:

* active messages
* closed conversations
* deleted/tombstoned messages
* attachments
* backups

Do not invent legal retention periods.

## 42. Events

Publish communication events required by the architecture.

Examples may include:

* notification.created
* notification.sent
* notification.failed
* notification.delivered
* message.created
* message.delivered
* message.read
* conversation.created
* conversation.closed

Use the project's canonical event naming and envelope.

Do not create excessive internal events that become external contracts without need.

## 43. Transactional Outbox

Use the established outbox for durable communication events.

Message creation and its required durable event must commit atomically.

Notification state transitions requiring domain events must follow the same pattern.

## 44. Consumer Idempotency

Notification and messaging consumers must tolerate duplicate event delivery.

Use stable event IDs, source references, and domain constraints.

Do not assume exactly-once consumption.

## 45. Background Jobs

Implement jobs for:

* notification delivery
* retries
* stale delivery cleanup
* unread-count reconciliation where required
* expired notification cleanup
* communication reconciliation

Messaging delivery must not depend entirely on a continuously connected worker.

## 46. Queue Isolation

Separate workloads where characteristics differ materially, such as:

* push
* email
* SMS
* critical notifications
* ordinary notifications
* messaging processing

Avoid allowing one provider outage to block unrelated communication channels.

## 47. Communication Provider Rate Limits

Implement provider-specific rate-limit handling at the adapter/queue boundary.

Support:

* throttling
* retry-after behavior where provided
* bounded backlog
* circuit/degraded behavior

Do not repeatedly hammer a throttled provider.

## 48. Notification Preferences and Critical Communications

Clearly distinguish:

* user-controlled preferences
* operational notifications
* security notifications
* safety notifications
* required trip notifications

Critical communication categories must not be accidentally suppressed by generic preference settings.

# SECURITY AND OBSERVABILITY

## 49. Security Controls

Apply:

* authentication
* participant authorization
* role-based access
* resource ownership
* rate limiting
* request validation
* attachment authorization
* provider credential isolation

Do not expose arbitrary conversation or notification records.

## 50. Audit

Audit:

* privileged conversation access
* privileged message intervention
* preference overrides
* administrative notification
* template-management actions
* communication-policy overrides

Do not audit every realtime message delivery as a human security action.

## 51. Metrics

Expose bounded metrics such as:

* notification creation rate
* notification delivery success/failure
* provider latency
* queue depth
* retry count
* invalid-token rate
* unread notification count by aggregate category where needed
* messages created
* message delivery latency
* message read latency
* realtime communication failures
* conversation synchronization failures

Do not use:

* message IDs
* user IDs
* phone numbers
* email addresses
* message content

as Prometheus labels.

## 52. Tracing

Trace representative flows through:

* event consumption
* notification creation
* provider delivery
* message creation
* persistence
* realtime delivery
* reconnect synchronization

Never place message bodies or sensitive notification contents into spans.

## 53. Failure Handling

Handle:

* Redis failure
* PostgreSQL failure
* Kafka/Redpanda failure
* worker failure
* push-provider outage
* email-provider outage
* SMS-provider outage
* WebSocket gateway failure
* duplicate events
* reconnect storms

Communication failures must not corrupt the authoritative source data.

## 54. APIs

Implement only communication APIs defined by the architecture.

Potential operations include:

* notification list
* unread count
* mark notification read
* preference management
* conversation list
* conversation retrieval
* message retrieval
* send message
* mark messages read
* close conversation where authorized

Apply:

* authentication
* authorization
* validation
* pagination
* idempotency
* canonical errors

## 55. Testing

Create comprehensive tests for:

### Notifications

* event-to-notification mapping
* preference filtering
* template selection
* locale handling
* deduplication
* provider success
* provider failure
* retries
* provider rate limits
* invalid push token
* read state

### Messaging

* conversation creation
* participant authorization
* message creation
* duplicate send
* message ordering
* delivery state
* read state
* reconnect recovery
* authorization after participant status changes
* attachment references
* closed conversation

### Realtime

* authorized subscription
* unauthorized subscription
* delivery
* duplicate messages
* reconnect
* missed-message synchronization

### Security

* cross-user notification access
* cross-conversation access
* privileged operations
* rate-limit enforcement
* sensitive-data leakage prevention

### Jobs

* retry
* backoff
* dead-letter/terminal failure
* worker restart
* queue isolation

# EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement:

* trip lifecycle
* dispatch
* pricing
* payments
* earnings
* payouts
* safety case workflows
* fraud/risk decisioning
* support-case workflows
* fleet maintenance
* scheduled-trip business logic
* analytics/reporting

Do not create a second WebSocket platform.

Do not create a second event-broker integration.

Do not create a second object-storage system.

Do not implement provider-specific business logic outside adapters.

Do not expose messaging as unrestricted general-purpose social messaging.

Do not allow notifications to become a hidden source of business state.

Do not create another communication backend volume.

Do not create a surprise integration phase.

# REPOSITORY INSPECTION REQUIREMENTS

Before implementation:

1. Inspect the backend repository.
2. Inspect Backend Volumes 1–6 implementation.
3. Inspect identity/device/session models.
4. Inspect realtime infrastructure.
5. Inspect event/outbox infrastructure.
6. Inspect job/queue infrastructure.
7. Inspect Redis usage.
8. Inspect object-storage abstractions.
9. Inspect trip/dispatch/payment event contracts.
10. Inspect authentication and authorization.
11. Inspect audit infrastructure.
12. Read notification and messaging contracts from the architecture.
13. Determine exactly which files require creation or modification.

Do not duplicate foundational infrastructure.

# IMPLEMENTATION RULES

## Preserve Existing Foundations

Reuse:

* authentication
* authorization
* request context
* database
* Redis
* events
* outbox
* jobs
* realtime
* object storage
* audit
* observability

## Provider Isolation

Provider-specific SDKs and status models must remain inside adapters.

## Idempotency

Notification creation, provider operations, message creation, and read-state mutations must behave safely under retries.

## Ordering

Messaging order must remain deterministic within the contractual scope.

## Delivery Semantics

Do not equate:

* persisted
* sent
* delivered
* read

unless the contract explicitly defines those states as equivalent.

## Privacy

Treat message content, contact information, notification content, and communication metadata as sensitive where applicable.

## Backpressure

Provider outages must not create unbounded worker growth.

## No Placeholder Work

Every required capability must be fully implemented.

# VALIDATION REQUIREMENTS

Execute all supported validation.

At minimum:

* TypeScript compilation
* linting
* formatting
* unit tests
* API integration tests
* Prisma validation
* migration validation
* Redis tests
* event/outbox tests
* job tests
* realtime tests
* OpenAPI validation
* security tests
* dependency/security scanning where configured

Test:

* notification preferences
* critical-notification bypass rules
* duplicate notification events
* duplicate provider operation
* provider timeout
* provider rate limiting
* invalid push token
* message authorization
* message idempotency
* concurrent message creation
* message ordering
* read-state races
* reconnect recovery
* closed-conversation behavior
* attachment authorization
* queue backlog
* worker restart
* Kafka/Redpanda outage
* Redis outage
* database outage
* WebSocket failure

Where an external communication provider is unavailable, use deterministic test doubles or the existing provider abstraction and clearly report that live provider execution was not performed.

# FINAL INTEGRATION CHECK

Before declaring this milestone complete:

1. Verify notification ownership is clearly separated from source-domain ownership.
2. Verify notification preferences cannot suppress protected critical communication.
3. Verify notification templates are versioned.
4. Verify channel selection is deterministic.
5. Verify duplicate notification creation is prevented.
6. Verify provider adapters are isolated.
7. Verify retries are bounded.
8. Verify provider outages cannot cause unlimited retry amplification.
9. Verify in-app notifications are correctly authorized.
10. Verify push-token ownership is enforced.
11. Verify notification read state is idempotent.
12. Verify conversations have explicit participant authorization.
13. Verify messages have deterministic ordering.
14. Verify duplicate message creation is prevented.
15. Verify delivery and read states are distinct.
16. Verify reconnect synchronization works from authoritative state.
17. Verify message content is excluded from ordinary observability.
18. Verify attachments use the established object-storage architecture.
19. Verify communication events use the transactional outbox.
20. Verify consumers tolerate duplicate delivery.
21. Verify queue isolation protects unrelated communication channels.
22. Verify provider rate limits are respected.
23. Verify privileged communication operations are audited.
24. Verify cross-user notification and conversation access is impossible.
25. Verify tests cover authorization, concurrency, retries, and reconnect behavior.
26. Verify compatibility with Backend Volumes 1–6.
27. Verify the repository is ready for Backend Volume 8.
28. Verify no placeholder or fake provider implementation remains.

# DEFINITION OF DONE

This milestone is complete only when:

* notification domain exists
* notification records exist
* notification preferences exist
* template/version handling exists
* localization exists
* channel selection exists
* notification deduplication exists
* delivery-attempt tracking exists
* notification state machine exists
* push-provider abstraction exists
* push-token management exists
* email-provider abstraction exists
* SMS-provider abstraction exists where required
* provider failure classification exists
* bounded notification retry exists
* communication backpressure exists
* in-app notifications exist
* notification read state exists
* recipient authorization exists
* notification audit controls exist
* conversation domain exists
* participant authorization exists
* conversation lifecycle exists
* message domain exists
* message ordering exists
* message idempotency exists
* delivery state exists
* read state exists
* realtime message delivery exists
* reconnect recovery exists
* offline/retry-safe messaging exists
* edit/delete behavior exists where contractually required
* attachment references exist where supported
* messaging abuse controls exist
* conversation closure behavior exists
* message privacy controls exist
* communication retention behavior follows the architecture
* communication events exist
* transactional outbox integration exists
* consumer idempotency exists
* notification/message jobs exist
* queue isolation exists
* provider rate-limit handling exists
* security controls exist
* audit controls exist
* metrics and traces exist
* APIs conform to the architecture
* tests cover normal, adversarial, and failure flows
* documentation is updated
* no unrelated domain has been implemented
* no second realtime/event/object-storage foundation has been introduced
* no placeholder implementation remains
* validation results are truthful
* the backend is ready for Backend Volume 8

# IMPLEMENTATION REPORT

At completion, provide:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Notification System

Summarize:

* notification model
* preferences
* templates
* localization
* channel selection
* provider adapters
* delivery states
* retries

## Messaging System

Summarize:

* conversations
* participants
* messages
* ordering
* delivery
* read state
* reconnect
* attachments
* closure

## Events and Jobs

Summarize:

* communication events
* outbox usage
* notification workers
* retry behavior
* queue isolation

## Security and Privacy

Summarize:

* recipient authorization
* conversation authorization
* provider credentials
* message privacy
* audit

## Realtime

Summarize:

* subscription authorization
* message delivery
* notification delivery
* reconnect synchronization

## Database and Redis

Summarize:

* schema
* constraints
* indexes
* Redis usage
* failure behavior

## API

Summarize implemented communication endpoints.

## Tests and Validation

List actual commands and outcomes.

## External Environment Limitations

State any push, email, SMS, or other provider services that could not be exercised.

Do not fabricate provider delivery or production results.

## Architectural Decisions

Record meaningful communication-system decisions.

## Known Limitations

List genuine remaining limitations.

# FINAL EXECUTION DIRECTIVE

Inspect the repository first.

Then implement Backend Volume 7 completely.

Extend the existing backend, identity, realtime, event, job, object-storage, and security foundations.

Implement notifications, preferences, templates, provider abstractions, delivery state, retries, in-app notifications, rider-driver conversations, messages, ordering, delivery/read state, reconnect recovery, attachment references, communication events, and the required operational controls.

Keep source-domain business state authoritative in its existing domains.

Do not implement safety, support, fraud, pricing, payments, or unrelated business logic.

Do not create a second realtime or event infrastructure.

Do not leave placeholders.

Do not fabricate external provider execution.

Run every validation command supported by the environment.

Verify authorization, privacy, idempotency, ordering, retry behavior, provider isolation, queue backpressure, realtime recovery, and failure handling.

Finish with the required implementation report and leave the repository in a coherent production-grade state ready for Backend Volume 8.
