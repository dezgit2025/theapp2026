# Product Requirements Document
## Hinge Clone — Dating App MVP

**Version:** 1.0 | **Date:** February 2026 | **Status:** DRAFT | **Classification:** Confidential

**Prepared by:** [Your Name]

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Product Vision & Goals](#2-product-vision--goals)
3. [Target Audience](#3-target-audience)
4. [Core Feature Set](#4-core-feature-set-hinge-feature-parity)
5. [Monetization Strategy](#5-monetization-strategy)
6. [Technical Architecture](#6-technical-architecture)
7. [Data Model (MongoDB)](#7-data-model-mongodb)
8. [API Design](#8-api-design)
9. [User Flows](#9-user-flows)
10. [Safety & Moderation](#10-safety--moderation)
11. [Non-Functional Requirements](#11-non-functional-requirements)
12. [MVP Phasing & Roadmap](#12-mvp-phasing--roadmap)
13. [Risks & Mitigations](#13-risks--mitigations)
14. [Appendices](#14-appendices)

---

## 1. Executive Summary

This document defines the product requirements for a Hinge-style dating application built as a web-first MVP using React Native (Expo). The product targets real user validation ahead of a seed funding round. The core thesis is that prompt-based, intention-driven dating produces higher-quality connections than swipe-based alternatives.

The MVP will replicate Hinge's proven interaction model — curated daily suggestions, profile prompts, specific-content likes, and text-based messaging — while being architected for rapid iteration and eventual mobile deployment on iOS and Android using the same Expo codebase.

---

## 2. Product Vision & Goals

### 2.1 Vision Statement

Build a dating app designed to be deleted — where every design decision optimizes for meaningful connections over engagement metrics. Prove this model with a lean, web-first MVP before scaling to native mobile apps.

### 2.2 Strategic Goals

1. Validate product-market fit with 1,000+ active users in a target metro area within 90 days of launch.
2. Achieve a match-to-conversation rate of 60%+ (industry average for Hinge is ~50%).
3. Demonstrate monetization viability through freemium tier conversion rate of 5%+ within 6 months.
4. Establish a technical foundation (Expo + MongoDB) that supports iOS/Android deployment with less than 2 weeks of additional engineering post-funding.
5. Generate sufficient traction data to support a seed funding round of $1–2M.

### 2.3 Success Metrics (KPIs)

| Metric | Target (MVP) | Measurement |
|--------|-------------|-------------|
| Weekly Active Users (WAU) | 1,000+ | Analytics dashboard |
| Match-to-Conversation Rate | >60% | Backend event tracking |
| Day 7 Retention | >40% | Cohort analysis |
| Day 30 Retention | >20% | Cohort analysis |
| Avg. Session Duration | >8 min | Analytics |
| Free-to-Paid Conversion | >5% | Stripe dashboard |
| Profiles Reported (safety) | <2% of MAU | Moderation queue |
| App Store Rating (post-mobile) | >4.2 | App Store / Play Store |

---

## 3. Target Audience

### 3.1 Primary Persona

| Attribute | Detail |
|-----------|--------|
| Age Range | 18–35 |
| Intent | Social connection |
| Behavior | Has used Hinge/Bumble/Tinder; frustrated by low-quality matches |
| Tech Comfort | Comfortable with web apps; uses mobile-first but web is acceptable for MVP |
| Geography | Single target metro (e.g., Austin, Denver, or NYC) for launch density |

### 3.2 Secondary Persona

Users aged 22–40 who are new to dating apps and prefer a less superficial, more curated experience. These users value authenticity and are willing to invest time in crafting a detailed profile.

---

## 4. Core Feature Set (Hinge Feature Parity)

### 4.1 Feature Priority Matrix

| Feature | Priority | MVP | Description |
|---------|----------|-----|-------------|
| Onboarding & Profile Creation | P0 | Yes | Phone/email auth, photo upload (6 max), 3 voice/text prompts, demographics, preferences |
| Discovery Feed | P0 | Yes | Curated stack of profiles; scroll-through card UI showing photos + prompts |
| Like / Comment on Specific Content | P0 | Yes | Like a specific photo or prompt answer (not just the whole profile) |
| Skip / Remove | P0 | Yes | Pass on a profile without negative signal stored |
| Likes You (Incoming Queue) | P0 | Yes | View who liked you; accept or decline to form a match |
| Match & Chat | P0 | Yes | Mutual like = match; opens text conversation thread |
| Dealbreakers & Preferences | P0 | Yes | Age range, distance, height, religion, ethnicity, children, smoking, drinking |
| Push Notifications (Web) | P1 | Yes | Browser push for new likes, matches, and messages |
| Profile Verification (Selfie) | P1 | Yes | Photo verification badge via selfie comparison |
| Most Compatible (Daily Pick) | P1 | Yes | One algorithmically-selected top match per day |
| Roses (Super Like) | P2 | Yes | Limited premium currency; sends profile to top of recipient's queue |
| Standouts Feed | P2 | Yes | Curated feed of high-engagement profiles; roses required to like |
| Boost (Visibility) | P2 | Post-MVP | Temporarily increase profile visibility; premium feature |
| Video Prompts | P3 | Post-MVP | Short video answers to prompts in addition to text |
| Voice Notes in Chat | P3 | Post-MVP | Audio messages within conversations |
| Video Calling | P3 | Post-MVP | In-app video dates |
| Date Scheduling | P3 | Post-MVP | In-app date planning with venue suggestions |

### 4.2 Onboarding & Profile Creation

#### 4.2.1 Authentication

Users authenticate via phone number (SMS OTP) as the primary method, with email/password as a secondary option. Social login (Apple, Google) should be supported for frictionless onboarding. Phone number is required for account recovery and anti-spam.

- Phone number verification via SMS OTP (Twilio or equivalent)
- Email/password with email verification link
- Apple Sign-In and Google Sign-In as supplementary options
- Rate limiting: max 5 OTP requests per phone number per hour

#### 4.2.2 Profile Setup Flow

The profile setup is a guided, multi-step wizard. Each step must be completed before progressing. The flow should feel conversational rather than form-like.

1. **Basic Info:** First name, date of birth (must be 18+), gender identity, who you're looking for (men, women, everyone).
2. **Photos:** Upload 6 photos (minimum 3 required). Support crop, reorder, and delete. First photo is the primary/cover photo.
3. **Prompts:** Select 3 prompts from a curated library (60+ options, organized by category). Write text answers (150 character max each). Categories include: conversation starters, dating intentions, personality, lifestyle, pop culture.
4. **Vitals:** Height, hometown, job title, company, education, religious beliefs, political leanings, drinking/smoking/drug habits, children status.
5. **Preferences (Dealbreakers):** Set age range, max distance (miles), and optionally mark any vital as a dealbreaker (hard filter vs. soft preference).
6. **Location:** Request geolocation permission; fallback to city/ZIP entry.

### 4.3 Discovery Feed

The discovery feed is the primary interaction surface. It presents one profile at a time in a vertically-scrollable card format, revealing photos and prompt answers as the user scrolls. This is the core Hinge UX pattern.

#### 4.3.1 Card Layout

- Full-bleed photos interspersed with prompt answer cards
- Each photo has a like button (heart icon) and a comment button
- Each prompt answer has a like button and a comment button
- Bottom action bar: X (skip) on left, heart (like) on right, rose (super like) in center
- Profile info overlay: name, age, location, job, education, verification badge
- Scroll progress indicator (dots or subtle progress bar)

#### 4.3.2 Feed Algorithm (MVP)

For MVP, the matching algorithm uses a pragmatic scoring system based on preference compatibility and engagement signals. A full ML recommendation engine is deferred to post-funding.

- Hard filters applied first: dealbreaker preferences (age, distance, gender)
- Soft scoring: weighted match on shared preferences (religion, lifestyle, etc.)
- Recency boost: newer profiles ranked slightly higher
- Engagement penalty: profiles that have been shown but not acted on are deprioritized
- Daily limit: free users see up to 8–10 profiles per day (Hinge model)
- Most Compatible: one algorithmically top-scored profile highlighted daily at the top of the feed

### 4.4 Likes & Matching

#### 4.4.1 Sending Likes

Unlike swipe-based apps, likes are targeted at specific content. The user taps the heart icon on a specific photo or prompt answer. Optionally, they can attach a comment (up to 200 characters) explaining why they liked that specific piece of content. This is Hinge's key differentiator — it gives the recipient context and a conversation starter.

- Free users: 8 likes per day (resets at midnight local time)
- Preferred subscribers: unlimited likes
- Rose (super like): 1 free rose per week; additional roses purchasable via in-app purchase

#### 4.4.2 Likes You Queue

When someone likes you, you see their profile in the "Likes You" tab. This is where asymmetric interest becomes a match. Free users can see that they have pending likes but see blurred previews. Paid users see full profiles.

- Free tier: blurred thumbnails of incoming likes with count badge; can reveal one at a time
- Preferred tier: full access to all incoming likes with ability to filter and sort
- Each incoming like shows: the specific photo/prompt they liked, their optional comment, and their full profile to review
- Actions: Accept (creates a match) or Decline (removes silently; no notification to sender)

#### 4.4.3 Match Creation

A match is created when User A likes User B AND User B accepts the like (or independently likes User A back). Upon match creation, both users receive a push notification and a new conversation thread is opened in the Messages tab.

### 4.5 Messaging

Messaging is unlocked only between matched users. The chat interface is a standard real-time text conversation.

- Real-time messaging via WebSocket (Socket.io or equivalent)
- Message types for MVP: text only (images, GIFs, voice notes deferred to post-MVP)
- Read receipts: sender sees when message is delivered and read
- Typing indicators: real-time typing bubble shown to recipient
- Conversation starters: if the liker attached a comment, it appears as the first message automatically
- Unmatch: either user can unmatch at any time, which deletes the conversation for both parties
- Report: ability to report a user directly from the conversation (harassment, spam, fake profile)

### 4.6 Profile Management

- Edit all profile fields at any time (photos, prompts, vitals, preferences)
- Pause profile: temporarily hide from discovery without deleting account
- Delete account: permanent deletion with 30-day grace period for recovery
- Profile preview: see how your profile appears to others
- Activity status: "Recently Active" badge shown to others (can be toggled off by paid users)

---

## 5. Monetization Strategy

### 5.1 Tier Comparison

| Feature | Free | Preferred ($29.99/mo) | HingeX ($49.99/mo) |
|---------|------|-----------------------|---------------------|
| Daily Likes | 8 | Unlimited | Unlimited |
| See Who Likes You | Blurred preview | Full access | Full access |
| Roses per Week | 1 | 5 | 5 |
| Dealbreaker Preferences | Basic (age, distance) | Advanced filters | Advanced filters |
| Most Compatible | 1/day | 1/day | Priority ranking |
| Profile Boost | No | No | 1 free boost/month |
| Hide Activity Status | No | Yes | Yes |
| Enhanced Recommendations | No | No | Yes (priority algo) |
| Skip the Line (Roses) | No | No | Profile seen first |

### 5.2 In-App Purchases

- Individual Roses: $3.99 each, or packs of 3 ($9.99), 12 ($29.99)
- Profile Boosts: $5.99 each (1 hour of increased visibility)
- Payment processing via Stripe (web) with Apple/Google IAP planned for mobile launch

### 5.3 Revenue Projections (MVP Phase)

Assuming 1,000 MAU at month 3 with a 5% conversion rate and $29.99 ARPU on paid tier, projected MRR is approximately $1,500. The primary goal of the MVP phase is user validation, not revenue.

---

## 6. Technical Architecture

### 6.1 System Overview

The architecture is designed for a lean startup context: minimize infrastructure cost, maximize developer velocity, and ensure the codebase can scale from web MVP to native mobile with minimal rework.

### 6.2 Technology Stack

| Layer | Technology | Rationale |
|-------|-----------|-----------|
| Frontend | React Native (Expo) with expo-router | Single codebase for web MVP + future iOS/Android. Expo's web support enables browser deployment now. |
| UI Library | React Native Paper or Tamagui | Cross-platform component library with web support and Material Design patterns. |
| State Management | Zustand or React Context + useReducer | Lightweight, minimal boilerplate for MVP. Migrate to Redux Toolkit if complexity grows. |
| Backend API | Node.js (Express or Fastify) | JavaScript ecosystem consistency. Fastify preferred for performance. |
| Real-Time | Socket.io on Node.js | WebSocket abstraction for chat, typing indicators, and push events. |
| Database (Production) | MongoDB Atlas (Free Tier — M0) | Flexible document model for user profiles, messages, matches. 512MB storage on free tier. |
| Database (UAT) | MongoDB Community on Azure VM | Self-managed instance for staging/testing with full control over data. |
| Authentication | Firebase Auth or custom JWT with Twilio SMS | Phone OTP + social logins. Firebase Auth free tier covers MVP scale. |
| File Storage | Azure Blob Storage or AWS S3 | Photo uploads with CDN for low-latency delivery. Azure Blob has generous free tier. |
| Image Processing | Sharp (Node.js) | Resize, crop, and optimize uploaded photos server-side. |
| Payments | Stripe | Subscription management, one-time purchases, webhook events. |
| Push Notifications | Firebase Cloud Messaging (FCM) | Web push for MVP; extends to mobile push natively. |
| Hosting (API) | Azure App Service (Free/B1) or Railway | Low-cost Node.js hosting. Azure synergizes with existing VM for UAT. |
| Hosting (Web) | Vercel or Azure Static Web Apps | Expo web builds deploy as static sites with SSR support if needed. |
| CI/CD | GitHub Actions | Automated testing, linting, and deployment pipelines. |
| Monitoring | Azure Application Insights or Sentry | Error tracking, performance monitoring, user analytics. |

### 6.3 High-Level Architecture Diagram (Textual)

The system follows a standard three-tier architecture: **Client (Expo Web)** communicates over HTTPS with the **API Server (Node.js/Express)**, which reads/writes to **MongoDB Atlas**. Real-time features (chat, typing indicators, online status) use a persistent WebSocket connection via Socket.io. Photo uploads flow from the client to Azure Blob Storage via presigned URLs, with the API server generating the upload tokens. Stripe webhooks notify the API server of payment events for subscription management.

**Client → API Flow:**
- Expo Web App → HTTPS → API Gateway/Load Balancer → Node.js API Server
- Expo Web App → WebSocket (Socket.io) → Node.js Real-Time Server

**API → Data Flow:**
- Node.js API → MongoDB Atlas (user profiles, matches, messages, preferences)
- Node.js API → Azure Blob Storage (photo CDN)
- Node.js API → Firebase Auth (token verification)
- Node.js API → Stripe API (payment processing)
- Node.js API → Twilio (SMS OTP)
- Node.js API → FCM (push notifications)

---

## 7. Data Model (MongoDB)

MongoDB's document model is ideal for dating profiles, which are highly variable and nested. Below are the core collections and their schemas.

### 7.1 Users Collection

| Field | Type | Description |
|-------|------|-------------|
| `_id` | ObjectId | Primary key |
| `phone` | String (encrypted) | Phone number for auth (unique, indexed) |
| `email` | String | Optional email (unique, sparse index) |
| `firstName` | String | Display name |
| `dateOfBirth` | Date | Must be 18+ at registration |
| `gender` | String | man \| woman \| nonbinary |
| `genderPreference` | String[] | Who they want to see: [man, woman, nonbinary] |
| `photos` | Object[] | Array of {url, order, isVerified}. Max 6. |
| `prompts` | Object[] | Array of {promptId, category, question, answer}. Exactly 3. |
| `vitals` | Object | Nested: {height, hometown, jobTitle, company, education, religion, politics, drinking, smoking, drugs, children} |
| `preferences` | Object | Nested: {ageRange: {min, max}, maxDistance, dealbreakers: {...}} |
| `location` | GeoJSON Point | {type: 'Point', coordinates: [lng, lat]}. 2dsphere indexed. |
| `tier` | String | free \| preferred \| hingex |
| `subscription` | Object | {stripeCustomerId, stripeSubId, currentPeriodEnd, status} |
| `dailyLikesRemaining` | Number | Reset at midnight local time |
| `rosesRemaining` | Number | Weekly reset for free allotment + purchased |
| `isVerified` | Boolean | Selfie verification status |
| `isPaused` | Boolean | Profile hidden from discovery |
| `lastActive` | Date | Last app interaction timestamp |
| `createdAt` | Date | Account creation |
| `updatedAt` | Date | Last profile update |

### 7.2 Likes Collection

| Field | Type | Description |
|-------|------|-------------|
| `_id` | ObjectId | Primary key |
| `senderId` | ObjectId | User who sent the like (indexed) |
| `receiverId` | ObjectId | User who received the like (indexed) |
| `contentType` | String | photo \| prompt |
| `contentRef` | String | Reference to specific photo URL or promptId |
| `comment` | String | Optional comment (max 200 chars) |
| `isRose` | Boolean | Whether a Rose was used |
| `status` | String | pending \| accepted \| declined \| expired |
| `createdAt` | Date | Timestamp |

Compound index on `{senderId, receiverId}` for duplicate prevention and `{receiverId, status}` for the Likes You queue.

### 7.3 Matches Collection

| Field | Type | Description |
|-------|------|-------------|
| `_id` | ObjectId | Primary key |
| `users` | ObjectId[] | Pair of matched user IDs [userA, userB] (indexed) |
| `likeId` | ObjectId | Reference to the Like that triggered the match |
| `status` | String | active \| unmatched |
| `unmatchedBy` | ObjectId | User who unmatched (null if active) |
| `lastMessageAt` | Date | Timestamp of most recent message (for sorting) |
| `createdAt` | Date | Match creation timestamp |

### 7.4 Messages Collection

| Field | Type | Description |
|-------|------|-------------|
| `_id` | ObjectId | Primary key |
| `matchId` | ObjectId | Reference to parent Match (indexed) |
| `senderId` | ObjectId | Message author |
| `content` | String | Message text (encrypted at rest) |
| `type` | String | text (expandable to image, gif, voice later) |
| `readAt` | Date | Timestamp when recipient read message (null if unread) |
| `createdAt` | Date | Sent timestamp |

Index on `{matchId, createdAt}` for paginated conversation retrieval. Consider TTL index for message retention policies.

### 7.5 Reports Collection

| Field | Type | Description |
|-------|------|-------------|
| `_id` | ObjectId | Primary key |
| `reporterId` | ObjectId | User filing the report |
| `reportedUserId` | ObjectId | User being reported |
| `reason` | String | harassment \| spam \| fake_profile \| inappropriate_content \| other |
| `details` | String | Optional free-text description |
| `status` | String | pending \| reviewed \| action_taken \| dismissed |
| `createdAt` | Date | Report timestamp |

### 7.6 Indexing Strategy

- **Users:** 2dsphere index on `location` for geospatial proximity queries
- **Users:** compound index on `{gender, isPaused, tier}` for discovery feed filtering
- **Likes:** compound unique index on `{senderId, receiverId}` to prevent duplicate likes
- **Likes:** index on `{receiverId, status, createdAt}` for Likes You queue
- **Matches:** index on `{users, status}` for finding a user's active matches
- **Messages:** index on `{matchId, createdAt}` for conversation pagination

---

## 8. API Design

RESTful API with JWT authentication. All endpoints require a valid Bearer token except auth routes. API versioned under `/api/v1/`.

### 8.1 Authentication Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/auth/otp/send` | Send SMS OTP to phone number |
| POST | `/api/v1/auth/otp/verify` | Verify OTP and return JWT |
| POST | `/api/v1/auth/register` | Create new user account |
| POST | `/api/v1/auth/login` | Login with email/password |
| POST | `/api/v1/auth/social` | Social login (Apple/Google) |
| POST | `/api/v1/auth/refresh` | Refresh expired JWT |

### 8.2 Profile Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/profile/me` | Get current user's profile |
| PUT | `/api/v1/profile/me` | Update profile fields |
| POST | `/api/v1/profile/photos/upload` | Get presigned URL for photo upload |
| DELETE | `/api/v1/profile/photos/:photoId` | Remove a photo |
| PUT | `/api/v1/profile/photos/reorder` | Reorder photos |
| POST | `/api/v1/profile/verify` | Submit selfie for verification |
| PUT | `/api/v1/profile/preferences` | Update dating preferences and dealbreakers |
| PUT | `/api/v1/profile/pause` | Toggle profile visibility |
| DELETE | `/api/v1/profile/me` | Delete account (soft delete, 30-day grace) |

### 8.3 Discovery Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/discover/feed` | Get next batch of profiles (paginated, 10 per request) |
| GET | `/api/v1/discover/most-compatible` | Get daily Most Compatible profile |
| GET | `/api/v1/discover/standouts` | Get Standouts feed (premium) |

### 8.4 Interaction Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/likes` | Send a like (with optional comment, rose flag) |
| GET | `/api/v1/likes/received` | Get incoming likes (Likes You queue) |
| PUT | `/api/v1/likes/:likeId/accept` | Accept a like (creates match) |
| PUT | `/api/v1/likes/:likeId/decline` | Decline a like |
| POST | `/api/v1/skip/:userId` | Skip a profile in discovery |

### 8.5 Match & Messaging Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/matches` | Get all active matches (sorted by lastMessageAt) |
| DELETE | `/api/v1/matches/:matchId` | Unmatch |
| GET | `/api/v1/matches/:matchId/messages` | Get messages (paginated, newest first) |
| POST | `/api/v1/matches/:matchId/messages` | Send a message |
| PUT | `/api/v1/matches/:matchId/messages/:msgId/read` | Mark message as read |

### 8.6 Payments Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/payments/subscribe` | Create Stripe checkout session for subscription |
| POST | `/api/v1/payments/purchase` | One-time purchase (roses, boosts) |
| GET | `/api/v1/payments/subscription` | Get current subscription status |
| POST | `/api/v1/payments/cancel` | Cancel subscription (end of billing period) |
| POST | `/api/v1/payments/webhook` | Stripe webhook handler (no auth) |

### 8.7 Reporting & Safety Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/reports` | Report a user |
| POST | `/api/v1/block/:userId` | Block a user |
| GET | `/api/v1/block` | Get blocked users list |
| DELETE | `/api/v1/block/:userId` | Unblock a user |

---

## 9. User Flows

### 9.1 New User Onboarding

1. User lands on marketing page / app store listing and taps "Get Started."
2. Phone number entry → SMS OTP verification.
3. Multi-step profile wizard: name, DOB, gender, gender preference.
4. Photo upload screen: drag-and-drop or camera capture. Minimum 3, maximum 6.
5. Prompt selection: choose 3 prompts from categorized library, write answers.
6. Vitals entry: height, hometown, job, education, lifestyle preferences.
7. Preference setup: age range slider, distance slider, dealbreaker toggles.
8. Location permission request (geolocation API) with city/ZIP fallback.
9. Profile preview screen: see how profile appears to others.
10. Onboarding complete → redirect to discovery feed.

### 9.2 Core Discovery → Like → Match → Chat Loop

1. User opens app → lands on Discovery tab.
2. Scrolls through a profile card (photos interspersed with prompt answers).
3. Taps heart on a specific photo or prompt → like sent (with optional comment).
4. OR taps X to skip to the next profile.
5. Recipient sees like in their "Likes You" tab.
6. Recipient reviews the liker's profile and taps Accept or Decline.
7. If accepted: both users see match animation, new conversation thread created.
8. If the liker attached a comment, it auto-populates as the first message.
9. Users exchange text messages in real-time.
10. Either user can unmatch at any time (conversation deleted).

### 9.3 Upgrade → Premium Flow

1. User encounters a gated feature (e.g., blurred Likes You, ran out of daily likes).
2. Paywall modal appears showing tier comparison and pricing.
3. User selects tier and payment plan (monthly, 3-month, 6-month).
4. Stripe checkout completes payment.
5. Webhook confirms → user's tier updated in real-time.
6. Gated features immediately unlock.

---

## 10. Safety & Moderation

### 10.1 Content Moderation

- All uploaded photos scanned for explicit/inappropriate content using a moderation API (Azure Content Safety or AWS Rekognition).
- Text prompts and messages scanned for harassment, hate speech, and spam patterns.
- Flagged content queued for human review before publication (photos) or after send (messages).

### 10.2 User Safety Features

- Report user: accessible from profile view and chat view. Predefined categories + free text.
- Block user: immediately removes all visibility between both users. Blocked user cannot re-discover the blocker.
- Unmatch: removes conversation and prevents re-matching.
- Profile verification: selfie-based photo comparison to reduce catfishing.

### 10.3 Anti-Abuse Measures

- Rate limiting on all API endpoints (per-user and per-IP).
- CAPTCHA on registration after failed OTP attempts.
- Automated ban triggers: 3+ reports from unique users triggers review; 5+ triggers temporary suspension.
- IP and device fingerprinting to prevent banned users from creating new accounts.
- Shadow banning: flagged accounts remain functional to the user but are hidden from all other users' feeds.

---

## 11. Non-Functional Requirements

### 11.1 Performance

- Discovery feed load time: < 2 seconds (P95).
- Message delivery latency: < 500ms (P95) for real-time chat.
- Photo upload + processing: < 5 seconds end-to-end.
- API response time: < 300ms (P95) for standard CRUD operations.

### 11.2 Scalability

- MVP architecture supports up to 10,000 concurrent users on current infrastructure.
- MongoDB Atlas free tier limits: 512MB storage, 100 max connections. Plan migration to M10+ at ~5,000 users.
- Horizontal scaling via load balancer + multiple API server instances when needed.
- WebSocket connections managed via Socket.io with Redis adapter for multi-instance.

### 11.3 Security

- All data in transit encrypted via TLS 1.3.
- Sensitive fields (phone, email) encrypted at rest in MongoDB using field-level encryption.
- JWT tokens with short expiry (15 min access, 7 day refresh) and rotation.
- OWASP Top 10 mitigations: input validation, parameterized queries, CSRF protection, rate limiting.
- GDPR and CCPA compliance: data export, right to deletion, consent management.
- Photo URLs use signed, time-limited CDN tokens to prevent hotlinking.

### 11.4 Accessibility

- WCAG 2.1 AA compliance target for the web application.
- Keyboard navigation support for all core flows.
- Screen reader compatible (ARIA labels on all interactive elements).
- Minimum contrast ratio of 4.5:1 for text.

### 11.5 Reliability

- Target uptime: 99.5% (allows ~3.6 hours downtime/month for MVP).
- Automated health checks and alerting via Application Insights.
- Database backups: MongoDB Atlas handles automated daily backups on free tier.
- Disaster recovery plan documented before public launch.

---

## 12. MVP Phasing & Roadmap

### 12.1 Phase 1: Foundation (Weeks 1–4)

- Project scaffolding: Expo (web), Express API, MongoDB Atlas setup
- Authentication: phone OTP + JWT
- Profile creation wizard (full flow)
- Photo upload pipeline (Blob Storage + Sharp processing)
- Basic discovery feed with preference-based filtering

### 12.2 Phase 2: Core Loop (Weeks 5–8)

- Like/comment on specific content
- Likes You queue (free: blurred; paid: full access)
- Match creation logic
- Real-time messaging (Socket.io + Messages collection)
- Push notifications (FCM web push)

### 12.3 Phase 3: Monetization & Polish (Weeks 9–12)

- Stripe integration: subscriptions + one-time purchases
- Freemium gating (daily likes, blurred likes, roses)
- Profile verification (selfie comparison)
- Content moderation pipeline
- Reporting, blocking, and unmatch flows
- Analytics instrumentation (events, funnels, cohorts)

### 12.4 Phase 4: Beta Launch (Weeks 13–16)

- Private beta with 100–200 invited users in target metro
- Bug fixes and UX refinement based on feedback
- Performance optimization and load testing
- Terms of service, privacy policy, and legal review
- Public launch in single metro area

### 12.5 Post-MVP (Post-Funding)

- Native iOS and Android deployment via Expo EAS Build
- ML-based recommendation engine (collaborative filtering + NLP on prompts)
- Voice notes and video prompts
- In-app video calling
- Date scheduling with venue integration
- Expand to additional metro areas
- Boost feature and enhanced premium tiers

---

## 13. Risks & Mitigations

| Risk | Severity | Likelihood | Mitigation |
|------|----------|-----------|------------|
| Cold start problem (not enough users for matches) | High | High | Launch in single dense metro area. Seed with beta invites. Offer referral incentives. Consider partnerships with local influencers. |
| Gender imbalance (common in dating apps) | High | High | Waitlist-based launch by gender to maintain ratio. Prioritize marketing to underrepresented gender. |
| MongoDB Atlas free tier storage limit (512MB) | Medium | Medium | Monitor storage via Atlas alerts. Photo storage is external (Blob). Migrate to M10 ($57/mo) when approaching limit. |
| Safety incidents (harassment, catfishing) | High | Medium | Proactive moderation, photo verification, robust reporting. Clear community guidelines and swift enforcement. |
| Stripe payment failures / fraud | Medium | Low | Stripe Radar for fraud detection. Webhook retry logic. Dunning management for failed renewals. |
| Expo web limitations (performance, native APIs) | Medium | Medium | Profile web target early. Use expo-web-compatible libraries. Plan native-only features for post-funding. |
| Regulatory (GDPR, age verification) | Medium | Medium | Legal review before launch. Age gating at registration. Data processing agreement. Consent flows. |
| Competitive pressure (Hinge, Bumble, Tinder) | High | High | Differentiate through community focus, niche targeting, or AI features post-MVP. Speed to market for validation. |

---

## 14. Appendices

### 14.1 Prompt Library (Sample — MVP Starter Set)

A curated set of profile prompts, organized by category. Users select 3 from this library.

**Conversation Starters:**
- Two truths and a lie...
- A shower thought I recently had...
- Believe it or not, I...
- My most controversial opinion is...
- The way to win me over is...

**Dating Intentions:**
- I'm looking for...
- After the first date, I love when...
- Dating me is like...
- Together, we could...
- I want someone who...

**Personality:**
- I'm convinced that...
- My simple pleasures are...
- I geek out on...
- A life goal of mine is...
- The hallmark of a good relationship is...

**Lifestyle:**
- My go-to karaoke song is...
- Typical Sunday for me...
- My most irrational fear is...
- I'll know it's time to delete this app when...
- Don't hate me if I...

### 14.2 Environment Configuration

| Environment | Database | API Host | Purpose |
|-------------|----------|----------|---------|
| Development | MongoDB Atlas M0 (Free) | localhost:3000 | Local development |
| UAT / Staging | MongoDB Community on Azure VM | staging.yourapp.com | QA testing, stakeholder demos |
| Production | MongoDB Atlas M0 → M10+ | api.yourapp.com | Live user-facing application |

### 14.3 Glossary

| Term | Definition |
|------|-----------|
| Like | An expression of interest directed at a specific piece of content (photo or prompt) on another user's profile. |
| Rose | A premium "super like" that places the sender's profile at the top of the recipient's Likes You queue. |
| Match | A mutual connection formed when both users express interest in each other. |
| Dealbreaker | A preference that acts as a hard filter, excluding profiles that don't meet the criteria. |
| Discovery Feed | The primary interface where users browse potential matches, one profile card at a time. |
| Likes You | The queue showing profiles of users who have liked the current user. |
| Most Compatible | A daily algorithmically-selected profile presented as a top recommendation. |
| Standouts | A curated feed of high-engagement profiles requiring Roses to interact with. |
| Boost | A paid feature that temporarily increases the user's visibility in others' discovery feeds. |

---

*— End of Document —*
