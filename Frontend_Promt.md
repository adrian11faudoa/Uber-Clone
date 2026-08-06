Using the approved Architecture Blueprint and the Master Prompt above.

Begin frontend and mobile implementation ONLY.

Do NOT generate backend code.

Do NOT generate infrastructure code.

Do NOT redesign APIs.

Do NOT redesign the database.

Assume the backend implementation already exists and consume its published API contracts exactly as defined in the Architecture Blueprint.

The applications must achieve App Store / Google Play flagship quality comparable to:

- Uber
- Lyft
- DiDi
- Bolt

Every implementation must be production-ready, accessible, responsive, highly performant, and maintainable.

Generate code incrementally according to the Master Prompt milestone strategy.

────────────────────────────────────────

MISSION

Build the complete production-ready client applications for the enterprise ride-hailing platform.

Generate:

- Rider Mobile App
- Driver Mobile App
- Admin Dashboard (Web)
- Operations Dashboard (Web)
- Customer Support Dashboard (Web)
- Shared UI Libraries
- Shared API SDK

The applications must provide real-time interactions, smooth animations, offline resilience, excellent battery efficiency, and enterprise-grade UX.

Optimize for:

- 60–120 FPS animations
- Fast startup
- Low memory usage
- Low battery consumption
- Reliable background location
- Offline recovery
- High responsiveness

────────────────────────────────────────

TECH STACK

Mobile

- React Native
- Expo
- TypeScript

Web

- Next.js 15
- React 19
- TypeScript

Navigation

- React Navigation

State Management

- Zustand

Server State

- TanStack Query

Forms

- React Hook Form
- Zod

Maps

- Google Maps SDK
- react-native-maps

Realtime

- Socket.IO Client

Animations

- React Native Reanimated
- React Native Gesture Handler
- Moti
- Framer Motion (Web)

Lists

- FlashList

Storage

- MMKV
- SecureStore

Notifications

- Expo Notifications

Charts

- Recharts

────────────────────────────────────────

ARCHITECTURE

Follow:

- Feature-first organization
- Clean Architecture
- SOLID
- Strict TypeScript
- Modular design
- Shared component library
- Shared design system
- Shared API layer
- Separation of presentation and business logic

────────────────────────────────────────

APPLICATIONS

Generate:

Rider Mobile App

Driver Mobile App

Admin Dashboard

Operations Dashboard

Customer Support Dashboard

Shared UI Components

Shared Design System

Shared API SDK

Shared Hooks

Shared Utilities

────────────────────────────────────────

FOLDER STRUCTURE

Generate scalable organization including:

app/

features/

components/

screens/

navigation/

layouts/

hooks/

providers/

services/

stores/

theme/

styles/

assets/

animations/

config/

types/

utils/

────────────────────────────────────────

NAVIGATION

Implement:

Authentication Flow

Role-based Navigation

Deep Linking

Protected Routes

Modal Navigation

Drawer Navigation

Bottom Tabs

Universal Links

────────────────────────────────────────

AUTHENTICATION

Generate interfaces for:

Registration

Login

Logout

Forgot Password

Reset Password

Email Verification

Session Management

Token Refresh

Biometric Authentication

Role Switching

────────────────────────────────────────

RIDER APPLICATION

Generate complete interfaces for:

Home

Ride Request

Pickup Selection

Destination Search

Saved Places

Nearby Drivers

Ride Options

Fare Estimate

Surge Pricing

Driver Matching

Driver Tracking

Trip Status

Live Map

ETA

Trip Sharing

Ride History

Payments

Wallet

Promotions

Coupons

Ratings

Reviews

Notifications

Support

Emergency SOS

Settings

Profile

────────────────────────────────────────

DRIVER APPLICATION

Generate:

Driver Dashboard

Online / Offline Toggle

Ride Requests

Ride Acceptance

Navigation

Pickup

Passenger Verification

Trip Progress

Drop-off

Trip Completion

Earnings

Wallet

Payouts

Ratings

Documents

Vehicle Management

Shift Statistics

Performance Metrics

Support

Emergency SOS

────────────────────────────────────────

ADMIN DASHBOARD

Generate:

Overview

Live Map

Users

Drivers

Vehicles

Trips

Payments

Refunds

Promotions

Fraud Detection

Reports

Analytics

Audit Logs

Feature Flags

System Settings

Moderation

────────────────────────────────────────

OPERATIONS DASHBOARD

Generate:

Active Trips

Driver Monitoring

Dispatch Monitoring

Incident Queue

SOS Queue

Heat Maps

Demand Monitoring

Regional Performance

Fleet Monitoring

────────────────────────────────────────

CUSTOMER SUPPORT DASHBOARD

Generate:

User Search

Ride Search

Refund Management

Support Tickets

Trip Replay

Incident Reports

Messaging

Audit Timeline

────────────────────────────────────────

MAP EXPERIENCE

Implement:

Real-time Driver Locations

Pickup Pin

Destination Pin

Route Preview

Navigation

Traffic Visualization

ETA Updates

Driver Arrival Animation

Trip Replay

Geofencing Indicators

────────────────────────────────────────

REAL-TIME FEATURES

Implement:

Live Driver Tracking

Driver Availability

Ride Status Updates

ETA Updates

Socket Reconnection

Offline Recovery

Connection Indicators

────────────────────────────────────────

STATE MANAGEMENT

Implement Zustand stores for:

Authentication

Ride

Trip

Driver

Maps

Notifications

Wallet

Theme

Settings

User Preferences

────────────────────────────────────────

SERVER STATE

Implement TanStack Query.

Support:

Caching

Optimistic Updates

Background Refresh

Retries

Offline Cache

Cache Invalidation

Pagination

────────────────────────────────────────

API CLIENT

Generate:

Typed API SDK

Authentication Interceptors

Retry Logic

Socket Management

Pagination Helpers

Upload Helpers

Cancellation Helpers

────────────────────────────────────────

FORMS

Generate production-ready forms using:

React Hook Form

Zod Validation

Inline Validation

Async Validation

Loading States

Error Handling

────────────────────────────────────────

BACKGROUND SERVICES

Implement:

Background Location Updates

Background Ride Tracking

Push Notification Handling

Offline Synchronization

Pending Requests Queue

Automatic Recovery

────────────────────────────────────────

OFFLINE MODE

Support:

Offline Maps Cache

Ride Recovery

Queued Requests

Synchronization

Automatic Retry

Conflict Resolution

────────────────────────────────────────

PERFORMANCE

Optimize:

FlashList

Memoization

Map Rendering

Socket Performance

Location Updates

Lazy Loading

Image Optimization

Startup Optimization

Memory Usage

Battery Consumption

────────────────────────────────────────

ACCESSIBILITY

Implement:

WCAG 2.2 AA Compliance

Screen Reader Support

VoiceOver

TalkBack

Dynamic Text

Keyboard Navigation (Web)

Reduced Motion

Focus Management

────────────────────────────────────────

RESPONSIVE DESIGN

Support:

Phones

Tablets

Foldables

Desktop

Large Displays

Landscape

Portrait

────────────────────────────────────────

THEMING

Support:

Light Theme

Dark Theme

System Theme

Dynamic Themes

────────────────────────────────────────

ANIMATIONS

Use Reanimated, Moti and Framer Motion for:

Map Transitions

Ride Matching

Driver Arrival

Bottom Sheets

Cards

Dialogs

Navigation

Micro-interactions

Loading States

Success States

────────────────────────────────────────

ERROR HANDLING

Generate:

Error Boundaries

Offline Screens

Connection Recovery

Retry Components

Maintenance Screens

────────────────────────────────────────

TESTING

Generate:

Unit Tests

Component Tests

Integration Tests

Accessibility Tests

GPS Simulation UI Tests

Performance Tests

Visual Regression Test Architecture

────────────────────────────────────────

DOCUMENTATION

Generate:

Component Documentation

Navigation Documentation

Design System Documentation

Frontend Standards

State Management Standards

API Usage Guide

────────────────────────────────────────

PROJECT ORGANIZATION

Maintain throughout development:

Current Milestone

Generated Screens

Generated Components

Generated Features

API Integrations

Remaining Work

Dependencies

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never generate placeholders.

Never generate pseudo-code.

Never omit implementations.

Never regenerate unchanged files.

Only modify files when required.

────────────────────────────────────────

STOP CONDITIONS

Generate the frontend incrementally according to the Master Prompt.

Each milestone should contain approximately 20–40 files.

At the end of every milestone:

- Verify all applications compile successfully.
- Update the project index.
- List completed screens and features.
- Identify the next file to generate.

STOP and wait for approval before generating the next milestone.
