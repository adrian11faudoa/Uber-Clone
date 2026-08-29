You are operating in Senior Engineering Team Mode.

Build the production-ready backend for high-scale real-time location, driver availability, geospatial indexing, maps integration, routing, ETA calculation, trip discovery, and regional mobility state for an enterprise-scale global ride-hailing and mobility platform comparable in architectural scope to Uber.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, or private implementation details from Uber or any other company.

This prompt is completely independent and may be executed in a separate conversation.

The backend must follow the approved Uber-like architecture, domain boundaries, database ownership, PostGIS strategy, Redis strategy, WebSocket architecture, maps abstraction, security model, event architecture, queue architecture, and Project Index.

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

• Driver availability
• Driver online/offline state
• Driver location ingestion
• Driver location validation
• Driver location freshness
• Rider trip location
• Real-time location streaming
• Geospatial indexing
• Nearby-driver discovery
• Service areas
• Geofences
• Airport zones
• Pickup zones
• Dropoff zones
• Maps integration
• Geocoding
• Reverse geocoding
• Places
• Directions
• Routes
• Distance
• ETA
• Traffic-aware routing
• Route recalculation
• Regional dispatch state
• Location subscriptions
• WebSocket location streams
• Driver location privacy
• Location cleanup
• Location analytics events

The implementation must support:

• Millions of drivers
• Millions of online drivers
• Millions of active location streams
• Very high GPS update volume
• Tens of millions of concurrent mobile connections
• Global operation
• Regional processing
• Low-latency nearby-driver discovery
• Low-latency ETA calculation
• High availability

────────────────────────────────────────

TECHNOLOGY STACK

Backend:

• Node.js
• NestJS
• TypeScript

Database:

• PostgreSQL
• Prisma ORM
• PostGIS

Ephemeral state:

• Redis

Event streaming:

• Kafka or Redpanda

Background processing:

• BullMQ

Real-time:

• WebSockets
• Socket.IO

Maps:

• Google Maps Platform or approved provider abstraction

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

Testing:

• Jest
• Supertest
• Integration and performance testing tools

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

Keep domain logic outside controllers.

Use repositories for persistence.

Use DTOs for external contracts.

Use centralized validation.

Use centralized error handling.

Use structured logging.

Use bounded timeouts for provider requests.

Use idempotency for location mutations where required.

Do not use PostgreSQL as the primary high-frequency transient location store.

────────────────────────────────────────

DOMAIN OWNERSHIP

Maintain explicit boundaries between:

• Driver availability
• Driver location
• Rider trip location
• Geospatial search
• Service areas
• Geofences
• Maps
• Routing
• ETA
• Real-time subscriptions
• Trip state

Do not combine:

• Driver account state with driver availability
• Driver availability with current trip state
• Transient location with historical trip data
• Maps-provider objects with core domain models

────────────────────────────────────────

DRIVER AVAILABILITY

Implement:

• Go online
• Go offline
• Pause availability
• Resume availability
• Availability heartbeat
• Availability timeout
• Availability reconciliation

States may include:

• Offline
• Available
• Temporarily Unavailable
• Offered
• En Route
• Arrived
• On Trip
• Suspended

Availability must not be inferred solely from the driver's last GPS point.

────────────────────────────────────────

AVAILABILITY HEARTBEAT

Support:

• Heartbeat
• Last-seen timestamp
• Device status
• Network status where available
• Region
• Current service area

Use Redis TTL for transient availability.

Define:

• Key pattern
• TTL
• Refresh interval
• Expiration
• Failure behavior

When heartbeat stops:

• Mark transient availability stale
• Remove from candidate pools
• Preserve authoritative driver status
• Reconcile state when the driver reconnects

────────────────────────────────────────

DRIVER LOCATION

Implement:

• Location ingestion
• Latitude
• Longitude
• Accuracy
• Timestamp
• Heading
• Speed
• Altitude where available
• Device timestamp
• Server timestamp
• Sequence number where available

Validate:

• Geographic bounds
• Timestamp
• Accuracy
• Velocity
• Update frequency
• Device association

Reject clearly invalid coordinates.

────────────────────────────────────────

LOCATION SEQUENCING

Support ordered location updates.

Handle:

• Duplicate update
• Older update
• Out-of-order update
• Missing update
• Device reconnect
• Server retry

Use:

• Device sequence number where available
• Server receive time
• Monotonic comparison

Do not replace a newer location with an older one.

────────────────────────────────────────

LOCATION QUALITY

Classify location quality such as:

• Excellent
• Good
• Poor
• Stale
• Invalid

Use accuracy and freshness to determine whether a location is appropriate for:

• Dispatch
• ETA
• Rider display
• Analytics

────────────────────────────────────────

LOCATION STORAGE

Use Redis for high-frequency transient location.

Possible state:

• Current location
• Last update
• Accuracy
• Heading
• Speed
• Region
• Geospatial index membership

Do not permanently persist every raw GPS point in PostgreSQL.

Persist selected information only when required for:

• Trip reconstruction
• Compliance
• Safety
• Analytics
• Fraud

────────────────────────────────────────

REDIS GEO / SPATIAL INDEX

Evaluate and implement an appropriate spatial strategy using:

• Redis GEO
• Geohash
• H3
• Other approved spatial indexing method

Support:

• Nearby-driver lookup
• Radius searches
• Candidate cells
• Region partitioning

Define:

• Key structure
• Member IDs
• TTL
• Region ownership
• Cleanup

Avoid global unbounded spatial indexes.

────────────────────────────────────────

GEOHASH / H3 PARTITIONING

Define a spatial partition strategy.

Support:

• Driver cell assignment
• Neighbor-cell lookup
• Zone boundaries
• Region boundaries

Candidate search should expand progressively:

Initial nearby cells
→ Adjacent cells
→ Wider cells

Do not scan all drivers in a city.

────────────────────────────────────────

POSTGIS

Use PostGIS for durable geospatial data.

Support:

• Service areas
• Geofences
• Airport zones
• Pickup zones
• Dropoff zones
• Operational boundaries

Use:

• Spatial indexes
• Geography/geometry appropriately
• SRID conventions
• Distance functions

Do not use PostGIS for every real-time driver-location lookup.

────────────────────────────────────────

SERVICE AREAS

Implement:

• Service area
• Region
• City
• Country
• Polygon
• Status
• Effective dates

Support:

• Ride availability
• Driver eligibility
• Pricing applicability
• Surge applicability

Service-area changes must be auditable.

────────────────────────────────────────

GEOFENCES

Support:

• Geofence
• Polygon/circle
• Type
• Region
• Effective dates
• Priority
• Policy

Use cases:

• Airports
• Pickup zones
• Restricted areas
• Toll zones
• Event zones
• Operational zones

────────────────────────────────────────

GEOFENCE EVALUATION

Support point-in-polygon and distance-based evaluation.

Define:

• Accuracy tolerance
• Boundary behavior
• Cache
• Update frequency

Do not assume GPS coordinates at a zone boundary are perfectly precise.

────────────────────────────────────────

AIRPORT ZONES

Support configurable airport areas:

• Airport
• Terminal
• Pickup area
• Dropoff area
• Driver staging
• Queue area
• Restricted area

Do not hard-code a single airport into the system.

────────────────────────────────────────

PICKUP ZONES

Support:

• Designated pickup locations
• Pickup polygons
• Pickup restrictions
• Landmark references
• Terminal restrictions

Expose appropriate pickup guidance to clients through APIs.

────────────────────────────────────────

LOCATION PRIVACY

Define visibility rules.

DRIVER:

Pre-trip:
• Limited/approximate visibility where appropriate

During assignment:
• Authorized rider visibility

During trip:
• Authorized real-time visibility

After trip:
• Access expires/restricts

RIDER:

Before assignment:
• Rider pickup data exposed only to authorized services

During trip:
• Driver receives authorized pickup/dropoff information

After trip:
• Historical access according to privacy policy

Administrative access must be restricted and audited.

────────────────────────────────────────

REAL-TIME LOCATION STREAMING

Implement WebSocket/Socket.IO infrastructure for:

• Driver location
• Rider trip location
• Trip state updates

Support:

• Authentication
• Authorization
• Room membership
• Subscription lifecycle
• Connection heartbeat
• Reconnect
• Backpressure
• Rate limiting

Clients must subscribe only to resources they are authorized to view.

────────────────────────────────────────

LOCATION FAN-OUT

Avoid broadcasting every location update to unnecessary subscribers.

Define:

• Authorized recipients
• Update frequency
• Adaptive frequency
• Distance thresholds
• Significant-change thresholds

For example, rider-facing updates can use a lower frequency than dispatch-internal updates when product requirements allow it.

────────────────────────────────────────

LOCATION BACKPRESSURE

Support:

• Sampling
• Coalescing
• Batching
• Latest-value-wins for transient location

When a subscriber is slow:

• Do not queue unlimited location messages
• Prefer latest state
• Drop stale intermediate updates

────────────────────────────────────────

LOCATION FAILURE BEHAVIOR

If Redis is unavailable:

• Do not claim current location is accurate
• Stop using unavailable transient state for new dispatch decisions where unsafe
• Fall back to safe stale-state rules
• Recover when Redis returns

Do not write millions of location updates directly to PostgreSQL as a naive fallback.

────────────────────────────────────────

LOCATION EVENTS

Publish appropriate events:

• DriverLocationUpdated
• DriverLocationStale
• DriverLocationInvalid
• DriverWentOnline
• DriverWentOffline
• DriverAvailabilityChanged
• RiderLocationUpdated where required

High-frequency events must have an explicit retention and partitioning strategy.

────────────────────────────────────────

MAP PROVIDER ABSTRACTION

Implement interfaces for:

• Geocoding
• Reverse geocoding
• Places
• Routes
• Route alternatives
• Distance
• ETA

Normalize provider responses into platform-owned models.

Do not allow Google-specific objects to become domain entities.

────────────────────────────────────────

GEOCODING

Implement:

• Address search
• Coordinate-to-address
• Place ID/reference
• Structured address
• Confidence

Cache safe, reusable results where appropriate.

Do not cache user-private locations under globally shared keys.

────────────────────────────────────────

PLACES

Support:

• Place search
• Place details
• Nearby places
• Address normalization

Protect against excessive provider calls with:

• Cache
• Deduplication
• Rate limits
• Request collapsing

────────────────────────────────────────

ROUTING

Implement:

• Route calculation
• Route alternatives
• Distance
• Duration
• Traffic-aware routing
• Waypoints
• Multi-stop routes

Define provider timeout.

Support future provider replacement.

────────────────────────────────────────

ETA

Implement:

• Driver-to-pickup ETA
• Pickup ETA
• Trip ETA
• Multi-stop ETA

Inputs:

• Driver location
• Destination
• Route
• Traffic
• Route state

Output:

• ETA
• Distance
• Timestamp
• Confidence/staleness metadata where appropriate

────────────────────────────────────────

ETA CACHING

Use Redis for short-lived ETA caching where safe.

Define:

• Cache key
• TTL
• Refresh
• Staleness threshold
• Invalidation

Do not return stale ETA indefinitely.

────────────────────────────────────────

ETA FAILURE

If map provider is unavailable:

• Use recent ETA if within safety bounds
• Mark ETA stale
• Reduce confidence
• Retry with bounded backoff
• Use approved fallback provider where configured

Never fabricate an accurate ETA.

────────────────────────────────────────

MAP PROVIDER RATE LIMITING

Implement provider-aware:

• Rate limits
• Quotas
• Request collapse
• Cache
• Retry
• Exponential backoff
• Circuit breaking

Avoid retry storms during provider outages.

────────────────────────────────────────

LOCATION REGION OWNERSHIP

Assign location processing to a region.

Define:

• Region
• City
• Service area
• Driver cell

Prefer keeping:

• Driver
• Location
• Dispatch candidate state

within the same regional processing boundary.

────────────────────────────────────────

REGIONAL LOCATION FAILOVER

Define behavior when a region fails.

Support:

• Region detection
• Traffic redirection
• Location reconnection
• Candidate rebuilding
• Driver state reconciliation

Avoid split-brain location ownership.

────────────────────────────────────────

API

Implement production-ready APIs.

AVAILABILITY

• Go online
• Go offline
• Get availability
• Heartbeat

LOCATION

• Submit location
• Get current location where authorized
• Location stream authorization

GEOSPATIAL

• Nearby drivers where authorized
• Service-area lookup
• Geofence lookup
• Pickup-zone lookup

MAPS

• Geocode
• Reverse geocode
• Place search
• Place details
• Route
• ETA

TRIP LOCATION

• Subscribe to trip location
• Get authorized current trip location

Every endpoint must implement:

• Authentication
• Authorization
• Validation
• Rate limiting
• Region awareness
• OpenAPI
• Consistent errors

────────────────────────────────────────

DATABASE

Implement Prisma models and migrations for durable geospatial configuration and references.

Include appropriate structures such as:

• ServiceArea
• ServiceAreaRegion
• Geofence
• GeofenceRule
• Airport
• AirportTerminal
• PickupZone
• DropoffZone
• OperationalZone
• DriverAvailabilitySnapshot where required
• LocationAuditReference where required
• MapProviderReference where necessary

Do not create a PostgreSQL row for every transient GPS update.

────────────────────────────────────────

REDIS KEY ARCHITECTURE

Define exact key conventions such as:

• availability:{region}:{driverId}
• location:{region}:{driverId}
• geo:{region}:{cell}
• trip-location:{region}:{tripId}
• eta:{region}:{routeKey}
• websocket:{region}:{connectionId}

Define:

• TTL
• serialization
• ownership
• cleanup
• failure behavior

────────────────────────────────────────

BACKGROUND JOBS

Implement jobs for:

• Stale-driver cleanup
• Location-index cleanup
• Service-area cache refresh
• Geofence cache refresh
• ETA cache cleanup
• Provider quota reconciliation
• Location audit aggregation
• Historical-location compaction where required

Every job must support:

• Retry
• Backoff
• Timeout
• Idempotency
• Dead-letter handling
• Monitoring

────────────────────────────────────────

SECURITY

Protect against:

• GPS spoofing
• Location flooding
• Unauthorized location access
• Cross-driver access
• Cross-rider access
• WebSocket room abuse
• Geospatial enumeration
• Provider-key exposure
• API abuse

Implement:

• Authentication
• Authorization
• Rate limiting
• Resource scoping
• Location privacy
• Audit

────────────────────────────────────────

OBSERVABILITY

Instrument:

• Location ingestion
• Availability changes
• Geospatial lookup
• Nearby-driver search
• ETA calculation
• Map-provider calls
• WebSocket subscriptions
• Location fan-out

Track:

• Location freshness
• Update rate
• Invalid location rate
• Stale-driver rate
• Nearby-search latency
• Candidate lookup latency
• ETA latency
• Map-provider errors
• Provider quota usage
• WebSocket connection count
• WebSocket message rate

Never log unnecessary precise location data.

────────────────────────────────────────

TESTING

UNIT TESTS

Test:

• Coordinate validation
• Location freshness
• Sequence handling
• Availability state machine
• Geospatial filtering
• Geofence logic
• Service-area rules
• ETA caching
• Provider fallback
• Rate limiting

INTEGRATION TESTS

Test:

• PostgreSQL
• PostGIS
• Redis
• Kafka
• BullMQ
• WebSockets
• Maps abstraction

LOCATION TESTS

Test:

• Valid location
• Invalid location
• Out-of-order location
• Duplicate location
• Stale location
• GPS jump
• High-frequency updates
• Disconnect
• Reconnect

GEO TESTS

Test:

• Nearby search
• Neighbor-cell expansion
• Geofence boundary
• Airport zone
• Service area
• Region boundary

WEBSOCKET TESTS

Test:

• Authentication
• Authorization
• Subscribe
• Unsubscribe
• Reconnect
• Backpressure
• Unauthorized subscription

MAP TESTS

Test:

• Provider success
• Timeout
• Rate limit
• Provider failure
• Cached response
• Fallback provider

PERFORMANCE TESTS

Test:

• Location ingestion throughput
• Concurrent WebSocket connections
• Nearby-driver search
• ETA requests
• Geofence evaluation

────────────────────────────────────────

DOCUMENTATION

Generate:

• Driver availability architecture
• Location ingestion architecture
• Location validation
• Redis spatial indexing
• PostGIS architecture
• Geohash/H3 strategy
• Service areas
• Geofences
• Airport zones
• Pickup zones
• Location privacy
• WebSocket location streaming
• Fan-out
• Backpressure
• Maps provider abstraction
• Geocoding
• Places
• Routing
• ETA
• Provider failure handling
• Regional location architecture
• API contracts
• Database schema
• Redis key catalog
• Event contracts
• Queue architecture
• Testing strategy
• Security model

────────────────────────────────────────

PROJECT INDEX

Update the backend Project Index with:

• Availability modules
• Location modules
• Geospatial modules
• Service-area modules
• Geofence modules
• Airport modules
• Pickup-zone modules
• Maps abstraction
• Routing
• ETA
• WebSocket location streaming
• Redis spatial state
• PostGIS objects
• APIs
• Events
• Queues
• Workers
• Database migrations
• Redis keys
• Security controls
• Privacy controls
• Tests
• Generated files
• Remaining work
• Current milestone
• Dependencies

────────────────────────────────────────

IMPLEMENTATION MILESTONES

BACKEND MILESTONE 21

Driver availability, online/offline state, heartbeats, TTL state, reconciliation, and APIs.

BACKEND MILESTONE 22

Location ingestion, validation, sequencing, freshness, anomaly handling, Redis transient state, and location APIs.

BACKEND MILESTONE 23

Redis geospatial indexing, Geohash/H3 strategy, nearby-driver discovery, candidate-cell expansion, and regional partitioning.

BACKEND MILESTONE 24

PostGIS, service areas, geofences, airport zones, pickup zones, dropoff zones, and spatial configuration APIs.

BACKEND MILESTONE 25

WebSocket/Socket.IO location streams, authorization, rooms, reconnect handling, fan-out, coalescing, and backpressure.

BACKEND MILESTONE 26

Maps provider abstraction, geocoding, reverse geocoding, places, caching, and provider rate limiting.

BACKEND MILESTONE 27

Routing, multi-stop route calculation, ETA engine, ETA caching, provider failures, and fallback strategy.

BACKEND MILESTONE 28

Regional location ownership, region failover, location privacy, auditing, and operational tooling.

BACKEND MILESTONE 29

Kafka events, background jobs, cleanup, observability, and provider reconciliation.

BACKEND MILESTONE 30

Integration, geospatial, WebSocket, performance, security, privacy, and resilience testing.

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

• Driver availability
• Driver location
• Rider trip location
• Location validation
• Location freshness
• Redis spatial state
• Geospatial indexing
• Nearby-driver discovery
• PostGIS
• Service areas
• Geofences
• Airport zones
• Pickup/dropoff zones
• Maps abstraction
• Geocoding
• Places
• Routing
• ETA
• WebSocket location streaming
• Location privacy
• Regional location ownership
• Related events
• Related background jobs

Do not implement complete:

• Ride requests
• Dispatch
• Matching assignment
• Trip lifecycle
• Scheduled rides
• Shared rides
• Pricing
• Surge
• Promotions
• Payments
• Wallets
• Earnings
• Payouts
• Ratings
• Messaging business logic
• Notifications business logic
• Safety
• Fraud
• Support
• Business accounts
• Analytics platform
• Administration UI
• Infrastructure
• Frontend
• Mobile

Those belong to later implementation volumes.

────────────────────────────────────────

QUALITY BAR

Treat location, availability, geospatial discovery, routing, and ETA as mission-critical real-time infrastructure.

Assume:

• Millions of drivers
• Millions of online drivers
• Massive GPS traffic
• Tens of millions of concurrent connections
• High nearby-driver lookup volume
• High routing volume
• Global regions
• Low-latency dispatch requirements
• Strict location privacy
• High availability

Prioritize:

• Low latency
• Location freshness
• Geospatial correctness
• Privacy
• Horizontal scalability
• Backpressure
• Provider resilience
• Regional isolation
• Observability
• Security
• Maintainability
• Production readiness
