Using the approved Architecture Blueprint and the Master Prompt above.

Begin backend implementation ONLY.

Do NOT generate frontend code.

Do NOT generate mobile code.

Do NOT generate infrastructure code unless required for backend execution.

Assume the Architecture Blueprint has been approved.

Follow it exactly.

Never redesign APIs.

Never redesign the database.

Never modify architectural decisions unless explicitly requested.

Generate code incrementally according to the Master Prompt milestone strategy.

────────────────────────────────────────

MISSION

Build the complete production-ready backend for the enterprise ride-hailing platform.

The backend must support:

• Uber-scale ride dispatch
• Millions of concurrent users
• Millions of concurrent drivers
• Real-time GPS tracking
• Dynamic pricing
• High availability
• Event-driven processing
• Zero downtime deployment

Every milestone must compile successfully before continuing.

────────────────────────────────────────

TECH STACK

Language

• TypeScript

Framework

• NestJS

Runtime

• Node.js

Database

• PostgreSQL
• Prisma ORM

Cache

• Redis

Realtime

• Socket.IO

Maps

• Google Maps Platform

Payments

• Stripe

Background Jobs

• BullMQ

Documentation

• OpenAPI / Swagger

────────────────────────────────────────

ARCHITECTURE

Strictly follow:

• Clean Architecture
• Domain-Driven Design (DDD)
• SOLID
• Repository Pattern
• Service Layer
• Dependency Injection
• CQRS where beneficial
• Event-Driven Architecture
• Feature-first organization

Never violate architectural boundaries.

────────────────────────────────────────

IMPLEMENT THE FOLLOWING DOMAINS

Identity

Authentication

Authorization

Users

Profiles

Drivers

Driver Verification

Vehicles

Fleet Management

Documents

GPS Tracking

Ride Requests

Ride Matching

Dispatch

Trips

Navigation

Routing

Pricing

Dynamic Surge Pricing

Coupons

Promotions

Wallets

Payments

Driver Earnings

Payouts

Refunds

Ratings

Reviews

Messaging

Notifications

Support

Emergency SOS

Incident Reports

Fraud Detection

Analytics

Administration

Audit

Feature Flags

System Configuration

────────────────────────────────────────

AUTHENTICATION

Implement:

• Registration
• Login
• Logout
• Email Verification
• Password Reset
• JWT
• Refresh Tokens
• MFA-ready Architecture
• Google OAuth
• Apple OAuth
• Session Management
• Device Management
• Token Revocation

────────────────────────────────────────

AUTHORIZATION

Implement complete RBAC.

Support:

Guest

Rider

Driver

Fleet Manager

Customer Support

Operations

Moderator

Administrator

Super Administrator

System Services

Generate:

Permission Guards

Policies

Decorators

Permission Matrix

────────────────────────────────────────

DATABASE

Generate:

• Prisma Schema
• Repositories
• Migrations
• Indexes
• Constraints
• Transactions
• Optimized Queries
• Read Models
• Seeders
• Geospatial Index Strategy
• Partitioning Strategy

────────────────────────────────────────

REAL-TIME LOCATION

Implement:

Driver Location Updates

Rider Location Updates

Location Streaming

Driver Availability

Heartbeat Monitoring

Connection Recovery

Presence Detection

Location History

Geofencing

Nearby Driver Lookup

High-frequency updates optimized for millions of concurrent drivers.

────────────────────────────────────────

DISPATCH ENGINE

Implement production-ready dispatch logic supporting:

Ride Requests

Nearby Driver Discovery

Matching Algorithm

ETA Calculation

Acceptance Timeout

Automatic Reassignment

Driver Prioritization

Trip Reservation

Scheduled Trips

Multi-stop Trips

Ride Recovery

────────────────────────────────────────

PRICING ENGINE

Implement:

Base Fare

Distance Pricing

Duration Pricing

Dynamic Surge Pricing

Airport Fees

Toll Calculation

Regional Pricing Rules

Promotions

Coupons

Taxes

Booking Fees

Cancellation Fees

────────────────────────────────────────

TRIP MANAGEMENT

Implement:

Trip Creation

Driver Assignment

Pickup Workflow

Trip Start

Waypoint Management

Navigation Updates

Trip Completion

Trip Cancellation

Trip Recovery

Trip Replay

Trip Timeline

────────────────────────────────────────

GOOGLE MAPS INTEGRATION

Implement services for:

Geocoding

Reverse Geocoding

Directions

Distance Matrix

ETA Calculation

Traffic-aware Routing

Route Optimization

Place Search

────────────────────────────────────────

PAYMENTS

Implement Stripe.

Support:

Payment Intents

Payment Authorization

Payment Capture

Refunds

Partial Refunds

Driver Earnings

Fleet Earnings

Platform Commission

Payout Scheduling

Webhook Processing

Idempotency

Payment Recovery

────────────────────────────────────────

WALLETS

Implement:

Rider Wallet

Driver Wallet

Credits

Promotions

Bonuses

Transaction History

Ledger

────────────────────────────────────────

DRIVER MANAGEMENT

Implement:

Driver Onboarding

Identity Verification

Vehicle Verification

Document Validation

Background Check Hooks

Approval Workflow

Suspension

Reactivation

────────────────────────────────────────

EMERGENCY SYSTEM

Implement:

SOS Trigger

Emergency Contacts

Live Trip Sharing

Incident Reports

Safety Timeline

Support Escalation

────────────────────────────────────────

NOTIFICATIONS

Generate queue-based services for:

Push

Email

SMS-ready Architecture

In-App Notifications

Include:

Retry Policies

Priority Queues

Scheduling

────────────────────────────────────────

MESSAGING

Implement:

Driver ↔ Rider Chat

Media Attachments

Typing Indicators

Read Receipts

Conversation History

Unread Counts

────────────────────────────────────────

ANALYTICS

Generate services for:

Ride Analytics

Driver Analytics

Demand Heatmaps

Revenue Analytics

Dispatch Performance

Cancellation Rates

ETA Accuracy

Fleet Analytics

Operational Metrics

────────────────────────────────────────

FRAUD DETECTION

Implement architecture for:

Fake GPS Detection

Duplicate Accounts

Payment Fraud

Ride Abuse

Promotion Abuse

Suspicious Activity Events

Future ML-based fraud scoring

────────────────────────────────────────

BACKGROUND WORKERS

Implement BullMQ workers for:

Dispatch Optimization

Pricing Updates

Payment Processing

Driver Verification

Notification Delivery

Analytics Aggregation

Receipt Generation

Payout Processing

Fraud Analysis

Cache Invalidation

Scheduled Maintenance

────────────────────────────────────────

EVENT BUS

Implement complete event-driven architecture.

Generate events including:

UserRegistered

DriverRegistered

DriverApproved

VehicleApproved

RideRequested

DriverMatched

RideAccepted

DriverArrived

RideStarted

RideCompleted

RideCancelled

PaymentAuthorized

PaymentCaptured

RefundIssued

DriverLocationUpdated

SOSActivated

ReviewSubmitted

NotificationQueued

AnalyticsUpdated

FraudDetected

Define publishers and subscribers.

────────────────────────────────────────

CACHE

Implement Redis for:

Sessions

Driver Locations

Nearby Drivers

Dispatch Cache

ETA Cache

Pricing Cache

Trip Cache

Rate Limiting

Distributed Locks

────────────────────────────────────────

SECURITY

Implement:

JWT

Refresh Tokens

RBAC

Secure Headers

Rate Limiting

Input Validation

SQL Injection Protection

XSS Protection

Secrets Management

Audit Logging

Encryption at Rest

Encryption in Transit

OWASP Top 10 Compliance

Abuse Detection Hooks

────────────────────────────────────────

OBSERVABILITY

Generate:

Structured Logging

Metrics

Distributed Tracing

Health Checks

Readiness Checks

Liveness Checks

Dispatch Monitoring

Trip Monitoring

Error Monitoring

Performance Monitoring

────────────────────────────────────────

RESILIENCY

Implement:

Retry Policies

Circuit Breakers

Timeouts

Graceful Shutdown

Dead Letter Queues

Failure Recovery

Idempotency

────────────────────────────────────────

TESTING

Generate:

Unit Tests

Integration Tests

Repository Tests

Service Tests

Controller Tests

API Contract Tests

Load Tests

GPS Simulation Tests

Dispatch Simulation Tests

Security Tests

────────────────────────────────────────

PROJECT ORGANIZATION

Maintain throughout development:

Current Milestone

Generated Files

Completed Modules

Remaining Modules

Database Objects

API Endpoints

Workers

Events

Dependencies

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never generate pseudo-code.

Never generate placeholders.

Never omit implementations.

Never regenerate unchanged files.

Only modify files when required.

────────────────────────────────────────

STOP CONDITIONS

Generate the backend incrementally according to the Master Prompt.

Each milestone should contain approximately 20–40 files.

At the end of every milestone:

• Verify the backend compiles successfully.
• Update the project index.
• List completed modules.
• Identify the next file to generate.

STOP and wait for approval before generating the next milestone.
