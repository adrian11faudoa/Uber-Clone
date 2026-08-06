Using the approved Master Prompt above.

DO NOT begin implementation.

Your only responsibility in this phase is to design the complete enterprise architecture for the platform.

This document becomes the single source of truth for every future Backend, Mobile, Web, Infrastructure, DevOps and QA implementation.

Do NOT generate source code.

Do NOT generate placeholder implementations.

Produce only architecture, engineering specifications, contracts, infrastructure decisions, domain models, scalability strategies and implementation plans.

────────────────────────────────────────

PROJECT

Build a production-ready enterprise ride-hailing platform comparable to:

• Uber
• Lyft
• DiDi
• Bolt

The platform must support:

• Millions of riders
• Millions of drivers
• Real-time GPS
• Live dispatching
• Dynamic pricing
• Route optimization
• Enterprise administration
• Future autonomous vehicle integration

The platform must be cloud-native, modular, event-driven and horizontally scalable.

────────────────────────────────────────

PRIMARY TECHNOLOGY STACK

Mobile

• React Native
• Expo
• TypeScript

Backend

• Node.js
• NestJS
• TypeScript

Database

• PostgreSQL
• Prisma ORM
• Redis

Maps

• Google Maps Platform

Realtime

• Socket.IO

Payments

• Stripe

Infrastructure

• Docker
• Kubernetes
• GitHub Actions

Observability

• Prometheus
• Grafana
• Loki
• OpenTelemetry

────────────────────────────────────────

SYSTEM REQUIREMENTS

Design for:

• 50M+ registered users
• 10M+ daily active riders
• Millions of drivers
• Millions of daily rides
• Millions of concurrent websocket connections
• Multi-region deployment
• Horizontal scaling
• High availability
• Zero downtime deployment

────────────────────────────────────────

APPLICATIONS

Design complete architecture for:

• Rider Mobile App
• Driver Mobile App
• Admin Dashboard
• Operations Dashboard
• Customer Support Dashboard
• Public API
• Internal APIs

────────────────────────────────────────

ROLES

Design RBAC for:

• Guest
• Rider
• Driver
• Fleet Manager
• Customer Support
• Operations
• Moderator
• Administrator
• Super Administrator
• System Services

Generate a complete permissions matrix.

────────────────────────────────────────

DOMAIN MODULES

Design domain boundaries for:

Identity

Authentication

Authorization

Profiles

Driver Verification

Vehicle Management

Fleet Management

Documents

GPS Tracking

Location History

Ride Requests

Ride Matching

Dispatch

Trip Management

Pricing

Dynamic Surge Pricing

Routing

Navigation

Payments

Wallets

Promotions

Coupons

Ratings

Reviews

Notifications

Messaging

Emergency SOS

Incident Reports

Support

Analytics

Fraud Detection

Administration

Audit

Feature Flags

System Configuration

────────────────────────────────────────

REAL-TIME ARCHITECTURE

Design complete real-time communication architecture.

Include:

• Driver Location Streaming
• Rider Location Streaming
• Trip Tracking
• ETA Updates
• Dispatch Events
• Driver Acceptance
• Ride Status
• Socket Authentication
• Presence
• Connection Recovery

────────────────────────────────────────

MICROSERVICE DECISION

Determine whether the platform should initially use:

• Modular Monolith
• Service-Oriented Architecture
• Microservices

Provide justification.

Design migration strategy for future scaling.

────────────────────────────────────────

C4 ARCHITECTURE

Generate:

• Context Diagram
• Container Diagram
• Component Diagram
• Deployment Diagram

Describe every component and responsibility.

────────────────────────────────────────

DOMAIN DRIVEN DESIGN

Define:

• Bounded Contexts
• Aggregates
• Entities
• Value Objects
• Domain Events
• Application Services
• Policies
• Specifications
• Repositories

────────────────────────────────────────

DATABASE

Generate complete database architecture.

Include:

• ER Diagram
• Normalization Strategy
• Tables
• Indexes
• Foreign Keys
• Constraints
• Partitioning
• Read Replicas
• Backup Strategy
• Audit Tables
• Soft Deletes

Optimize for billions of ride records.

────────────────────────────────────────

GEOLOCATION ARCHITECTURE

Design:

• Driver Position Updates
• Rider Position Updates
• Geospatial Queries
• Nearby Driver Search
• Geofencing
• Region Partitioning
• Hotspot Detection
• Trip Replay
• Historical Locations

────────────────────────────────────────

DISPATCH SYSTEM

Design:

• Driver Discovery
• Dispatch Algorithms
• Acceptance Workflow
• Reassignment Logic
• Timeout Handling
• Driver Prioritization
• Cancellation Logic
• Multi-stop Trips
• Scheduled Trips

────────────────────────────────────────

PRICING ENGINE

Design:

• Base Fare
• Distance Pricing
• Time Pricing
• Dynamic Surge
• Airport Pricing
• Toll Calculation
• Promotions
• Coupons
• Taxes
• Fees

────────────────────────────────────────

ROUTING

Design:

• Route Planning
• ETA Calculation
• Traffic-aware Routing
• Alternative Routes
• Navigation Integration
• Trip Optimization

────────────────────────────────────────

PAYMENT ARCHITECTURE

Design:

• Stripe Integration
• Rider Payments
• Driver Earnings
• Fleet Payments
• Refunds
• Tips
• Platform Commission
• Payout Scheduling
• Webhook Processing

────────────────────────────────────────

EVENT ARCHITECTURE

Define events including:

RideRequested

DriverMatched

DriverAccepted

DriverArrived

RideStarted

RideCompleted

RideCancelled

PaymentAuthorized

PaymentCaptured

DriverLocationUpdated

SOSActivated

ReviewSubmitted

Generate producers and consumers.

────────────────────────────────────────

ASYNC PROCESSING

Identify all background jobs.

Examples:

• Notifications
• Payment Processing
• Earnings Calculation
• Analytics
• Fraud Detection
• Receipt Generation
• Driver Verification
• Cache Invalidation

────────────────────────────────────────

CACHE STRATEGY

Design Redis usage for:

• Driver Locations
• Active Trips
• Dispatch
• Sessions
• Pricing
• ETA
• Rate Limiting
• Distributed Locks

────────────────────────────────────────

SECURITY

Design:

• JWT
• Refresh Tokens
• RBAC
• Device Trust
• Encryption
• Audit Logging
• Secrets Management
• OWASP Compliance
• Fraud Prevention
• Account Protection

────────────────────────────────────────

OBSERVABILITY

Design:

• Structured Logging
• Metrics
• Distributed Tracing
• Dashboards
• Alerts
• Health Checks
• Dispatch Metrics
• Trip Metrics

────────────────────────────────────────

AI ARCHITECTURE

Design future-ready AI support for:

• Dynamic Pricing
• ETA Prediction
• Driver Matching
• Fraud Detection
• Demand Forecasting
• Route Optimization
• Driver Quality Scoring
• Customer Support Assistant
• Future Autonomous Dispatch

────────────────────────────────────────

FRONTEND & MOBILE ARCHITECTURE

Define:

• Feature-first Structure
• Navigation
• Offline Support
• Secure Storage
• Background GPS
• Push Notifications
• State Management
• API Layer
• Error Recovery

────────────────────────────────────────

DEVOPS ARCHITECTURE

Design:

• CI/CD
• Environment Strategy
• Container Strategy
• Kubernetes Organization
• Monitoring
• Rollback
• Disaster Recovery

────────────────────────────────────────

TESTING STRATEGY

Design:

• Unit Testing
• Integration Testing
• E2E Testing
• Contract Testing
• Load Testing
• GPS Simulation Testing
• Dispatch Simulation Testing
• Security Testing

────────────────────────────────────────

DOCUMENTATION

Generate:

• Architecture Overview
• ADRs
• Folder Structure
• Coding Standards
• API Standards
• Database Standards
• Security Standards
• Deployment Standards
• Operations Runbooks
• Disaster Recovery Plan

────────────────────────────────────────

DELIVERABLE

Produce a complete enterprise engineering blueprint.

This blueprint must be detailed enough that independent engineering teams can implement:

• Backend
• Mobile Apps
• Admin Dashboard
• Infrastructure
• DevOps
• QA

without making additional architectural decisions.

STOP after completing the architecture blueprint.

Wait for approval before implementation begins.
