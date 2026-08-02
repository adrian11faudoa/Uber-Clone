Using the Master Prompt above:

Build a complete production-ready enterprise ride-hailing platform suitable for a venture-funded startup capable of scaling to tens of millions of users.

The platform must be modular, cloud-native, secure, event-driven, highly available, horizontally scalable, and maintainable for long-term growth.

# Primary Tech Stack

Mobile

- React Native
- Expo
- TypeScript

Backend

- Node.js
- NestJS
- TypeScript

Database

- PostgreSQL
- Prisma ORM
- Redis
- PostGIS

Maps & Navigation

- Google Maps Platform
- Directions API
- Distance Matrix API
- Places API
- Geocoding API

Real-Time Communication

- Socket.io
- WebSockets

Payments

- Stripe

Infrastructure

- Docker
- Kubernetes
- GitHub Actions

# Applications

Generate complete applications for:

- Rider App
- Driver App
- Admin Dashboard
- Operations Dashboard

# Platform Roles

Implement complete role separation for:

- Guest
- Rider
- Driver
- Fleet Manager
- Customer Support
- Operations Agent
- Administrator
- Super Administrator
- System Services

Implement full RBAC.

# Authentication

Support:

- Email/Password
- Phone Number Login
- OTP Verification
- Google Login
- Apple Login
- MFA
- Password Reset
- Email Verification
- Phone Verification
- Refresh Tokens
- Device Sessions
- Remember Me
- Suspicious Login Detection
- Account Lockout

# Rider Features

Implement:

- User Profiles
- Saved Addresses
- Favorite Locations
- Home & Work Addresses
- Ride Scheduling
- Ride Requests
- Fare Estimates
- Live Driver Tracking
- Route Preview
- Multiple Payment Methods
- Promo Codes
- Ride History
- Receipts
- Favorite Drivers
- Emergency Contact
- SOS Button
- Lost & Found
- Ride Sharing
- Split Fare
- Multi-Stop Trips

# Driver Features

Implement:

- Driver Registration
- Identity Verification
- License Verification
- Vehicle Verification
- Insurance Verification
- Background Check Workflow
- Online/Offline Status
- Ride Requests
- Navigation
- Earnings Dashboard
- Incentives
- Bonuses
- Daily Goals
- Ride History
- Ratings
- Reviews
- Wallet
- Payout Requests
- Document Expiration Alerts

# Fleet Management

Implement:

- Fleet Owners
- Multiple Drivers
- Vehicle Assignment
- Fleet Analytics
- Driver Performance
- Fleet Earnings
- Vehicle Maintenance Tracking

# Ride Matching

Implement intelligent dispatch supporting:

- Nearest Driver Matching
- ETA Optimization
- Driver Availability
- Vehicle Type Matching
- Priority Dispatch
- Driver Acceptance Timeout
- Ride Reassignment
- Queue Management

# Real-Time Location

Support:

- Live GPS Updates
- Driver Tracking
- Rider Tracking
- Route Updates
- ETA Updates
- Geofencing
- Location History
- Trip Replay

# Navigation

Implement:

- Turn-by-Turn Navigation
- Route Optimization
- Traffic Awareness
- Alternative Routes
- Road Closures
- Toll Detection

# Pricing

Support:

- Base Fare
- Distance Pricing
- Time Pricing
- Surge Pricing
- Dynamic Pricing
- Airport Pricing
- Toll Charges
- Waiting Charges
- Cancellation Fees
- Promo Discounts

# Ride Types

Support:

- Economy
- Premium
- SUV
- XL
- Luxury
- Electric Vehicles
- Motorcycle
- Shared Rides

Architecture should allow easy addition of future ride categories.

# Payments

Support Stripe including:

- Cards
- Apple Pay
- Google Pay
- Saved Payment Methods
- Ride Authorization
- Payment Capture
- Refunds
- Partial Refunds
- Tips
- Driver Payouts
- Platform Commission
- Transaction History

# Ratings & Reviews

Implement:

- Rider Rates Driver
- Driver Rates Rider
- Written Reviews
- Anonymous Feedback
- Reputation Scores
- Quality Metrics

# Notifications

Support:

- Push Notifications
- SMS
- Email
- In-App Notifications

Trigger notifications for:

- Ride Requests
- Driver Arrival
- Ride Started
- Ride Completed
- Payments
- Promotions
- Safety Alerts

# Messaging

Implement:

- Rider ↔ Driver Chat
- Voice Call Proxy
- Masked Phone Numbers
- Ride Conversation History

# Safety Features

Implement:

- SOS Button
- Emergency Contacts
- Ride Sharing
- Live Trip Sharing
- Driver Verification
- Rider Verification
- Incident Reporting
- Safety Check-In
- Trusted Contacts

# Search & Places

Support:

- Address Search
- Places Search
- Recent Locations
- Saved Places
- Popular Destinations
- Nearby Places

# Admin Dashboard

Implement:

- Live Ride Monitoring
- User Management
- Driver Management
- Fleet Management
- Vehicle Management
- Pricing Rules
- Surge Management
- Promotions
- Support Tickets
- Incident Management
- Fraud Detection
- Audit Logs
- Queue Monitoring
- Health Monitoring
- Feature Flags
- System Settings

# Operations Dashboard

Implement:

- Live Driver Map
- Active Ride Map
- Demand Heatmaps
- Surge Zones
- Driver Availability
- Dispatch Monitoring
- Traffic Monitoring

# Analytics

Track:

- Daily Active Riders
- Daily Active Drivers
- Completed Trips
- Cancellations
- Driver Acceptance Rate
- Driver Utilization
- Average ETA
- Average Trip Time
- Revenue
- Driver Earnings
- Customer Lifetime Value
- Geographic Demand
- Peak Hours

# AI Features

Implement AI-ready architecture supporting:

- Demand Forecasting
- Surge Prediction
- Driver Positioning
- Ride Demand Heatmaps
- ETA Prediction
- Fraud Detection
- Fake GPS Detection
- Driver Performance Insights
- Smart Dispatch Optimization

# Fraud Prevention

Implement:

- Fake GPS Detection
- Payment Fraud Detection
- Duplicate Accounts
- Device Fingerprinting
- Abuse Detection
- Suspicious Ride Detection

# Infrastructure Services

Generate:

- User Service
- Driver Service
- Fleet Service
- Ride Service
- Dispatch Service
- Pricing Service
- Location Service
- Payment Service
- Notification Service
- Analytics Service
- Fraud Detection Service
- Search Service
- API Gateway
- Background Workers
- Event Bus

# Security

Implement:

- JWT
- Refresh Tokens
- RBAC
- MFA
- CSRF Protection
- XSS Protection
- SQL Injection Protection
- Rate Limiting
- Secure Headers
- Secrets Management
- Audit Logging
- Encryption at Rest
- Encryption in Transit
- OWASP Top 10 Compliance

# Performance

Optimize for:

- Real-Time WebSockets
- Redis Caching
- Read Replicas
- Database Partitioning
- Geospatial Indexes
- Queue Processing
- Horizontal Scaling
- Multi-Region Deployment
- Zero-Downtime Deployments

# DevOps

Generate:

- Docker
- Docker Compose
- Kubernetes
- Helm Charts
- GitHub Actions
- Terraform
- Prometheus
- Grafana
- Loki
- OpenTelemetry
- Distributed Tracing
- Centralized Logging
- Health Checks
- Automatic Backups

# Testing

Generate:

- Unit Tests
- Integration Tests
- End-to-End Tests
- API Contract Tests
- Load Tests
- Performance Tests
- Security Tests

# Documentation

Generate:

- Architecture Documentation
- Architecture Decision Records (ADRs)
- Entity Relationship Diagram (ERD)
- OpenAPI Documentation
- Deployment Guide
- Developer Setup Guide
- CI/CD Documentation
- Security Documentation
- Operational Runbooks
- Disaster Recovery Guide

# Scalability Requirements

Design for:

- 20M+ registered users
- 2M+ daily active users
- Millions of rides per day
- Nationwide deployment
- Multi-Region Deployment
- High Availability
- Horizontal Scaling
- Zero-Downtime Deployments

# Quality Requirements

The entire project must be:

- Production Ready
- Enterprise Grade
- Cloud Native
- Event Driven
- Domain Driven Design (DDD)
- CQRS where beneficial
- Clean Architecture
- Fully Typed
- SOLID Compliant
- Modular
- Testable
- Observable
- Maintainable
- Zero-Downtime Deployable

Generate the application incrementally according to the Master Prompt phases, ensuring every milestone compiles successfully before continuing.
