# PRD — HingeX Social Connector (MVP1)

**Version:** v1.3 (Simplified Authentic Profiles + Anti-Curation Brand Voice)
**Date:** 2026-02-16
**Launch markets (Wave 1):** New York City metro + Southern California metro  
**Audience:** 18+ (friends + dating)  
**Product mode:** Friends / Dating / Both (explicit)

---

## 1) Summary

**HingeX Social Connector** is a relationship-first, **low-curation social connection app** broadened for **friends + dating** and optimized for people who like to meet others around **food, nightlife, and social "vibes."** Profiles are intentionally minimal — the real connection happens through conversation and showing up, not curated highlight reels.

**Core loop:**
Create a simple profile (2-3 photos, a quote, one activity) → **go out and move** → discover people within 1 mile who are also out → like their profile → mutual match (24h window) → chat → meet at a public location.

**Key differentiator — Three pillars:**

**Primary Feature I: Geo-Movement Matching (MVP1)** — Users can **only** discover and match with others by physically going out and moving within proximity (default: 1 mile). No couch swiping. The app rewards real-world movement with connection opportunities that **expire in 24 hours**, creating urgency and authenticity. Combined with a lightweight **Status / Catchline** ("Tonight I'm…") to signal intent.

**Primary Feature II: Professional Verification (MVP1)** — Optional Blind-style work email verification and LinkedIn validation that surfaces real professional identity (title, company) as trust signals. Three tiers (Silver / Gold / Platinum) at accessible annual pricing — no major dating app offers verified professional credentials outside The League ($300+/mo). Verified profiles see higher match and response rates, and verified users can filter to only see other verified users, cutting spam.

**Primary Feature III: Vibe Map (Simulated in MVP1 · Live in Phase II+)** — Real-time crowd density heat map powered entirely by HingeX users' own GPS data — no third-party APIs. Solves "where's the party at?" — Google reviews are stale, but HingeX users are already out with location active. Waze-style dots on a map (1 dot = 3+ users) show which bars and restaurants are actually busy tonight. MVP1 ships a simulated version for investor demo; real user-powered data goes live in Phase II when user density supports it. Premium feature for paying users. Evolves into a nightlife marketplace (bar/restaurant deals, promoted listings) and eventually AR overlays with happy hour specials.

> *"You don't find connections — you earn them by showing up. You know who you're meeting. And you always know where the party's at."*

---

## 1.1) Brand Voice — Anti-Curation Positioning

HingeX is the **anti-highlight-reel** dating app. While competitors encourage curated perfection (6 photos, detailed prompts, personality quizzes, Spotify integration), HingeX strips profiles down to the essentials and lets real-world interaction do the rest.

**Core brand pillars:**
- **Real over curated** — selfies welcome, no pressure for professional photos
- **Show up over swipe up** — you earn connections by going out, not optimizing your profile
- **Discover through conversation** — the person behind the profile is found in chat and meetups, not a bio

**Marketing taglines (candidate):**
- *"No filters. No fake perfect lives. Just real people, really out there."*
- *"Your profile is simple. Your conversations are everything."*
- *"Stop swiping from your couch. Start meeting in the real world."*
- *"2 photos. 1 quote. Go outside. That's it."*
- *"The dating app that rewards you for leaving the house."*
- *"Less profile. More presence."*

---

## 2) Goals & Non-goals

### Goals (MVP1)
1. Enable users to quickly create **simple, authentic profiles** (2-3 photos + quote + activity) — no over-curation.
2. Drive **meaningful conversations**, not infinite swiping.
3. Support explicit connection intent: **Friends**, **Dating**, or **Both**.
4. Provide baseline **Trust & Safety** suitable for an 18+ consumer app.
5. Prove value with **low-cost MVP**: validate activation, match-to-chat, and retention signals.
6. **Validate geo-movement matching** as the primary discovery mechanism — users must physically go out and be within proximity to discover and connect.
7. **Prove the "go out to connect" thesis** — measure whether movement-gated matching drives higher-quality conversations and meetup rates vs. traditional swiping.
8. **Demo the Vibe Map concept** — ship a simulated crowd density heat map (Waze-style dots on a map) to validate the "where's the party at?" value prop with investors. Real user-powered data in Phase II.

### Non-goals (Out of scope for MVP1)
- ~~Neighborhood selection or hyperlocal "areas"~~ → Replaced by geo-movement proximity
- Traditional card-based "browse all profiles" feed (no couch swiping)
- Real-time WebSocket location tracking (use polling for MVP1; WebSockets in Phase III)
- H3 hexagonal zone mapping / gamification badges (Phase II)
- ML-heavy "Most compatible" ranking (use heuristics)
- Video-first dating, live events, or group chats
- Unmatched DMs / open messaging (consent-first only)
- Extensive venue integrations (Yelp/Resy/OpenTable) — later phase
- Exact location sharing between users (privacy-first: fuzzy proximity only)

---

## 3) Target Users

### Persona A — New to the city
Wants friends and plans; hates awkward intros; values low friction.

### Persona B — Social regular
Goes out often; wants new people for dinner, drinks, shows, or “a crew.”

### Persona C — Dating-open
Wants dating + friend vibes; cares about authenticity and communication.

### Persona D — Cautious user
Needs controls (block/report), privacy, and safer identity options.

---

## 4) Key User Journeys

### J1: Signup → Profile → First Like
1. Phone verify  
2. Age gate 18+  
3. Choose City/Metro (NYC or SoCal) + Mode (Friends/Dating/Both)  
4. Build profile (2-3 photos + quote + emoji activity)
5. Grant location permission (required for geo-movement matching)
6. Go out — app detects movement and shows Nearby Now feed
7. Send first like to a nearby user

**Success:** first like within first outing session.

### J2: Go Out → Discover Nearby → Match → Chat → Meet Up
1. User goes out; app detects movement (GPS displacement > 100m in 30 min)
2. App shows **"Nearby Now"** feed — other active users within 1 mile
3. User likes a nearby profile (simple like — no prompt-specific interactions)
4. If the other user also likes back within **24 hours**, mutual match is created
5. Chat unlocks (text) with optional starter suggestions
6. Users coordinate to meet at a **public location**
7. User optionally sets a Status ("Tonight I'm…") for momentum

**Success:** mutual geo-match within 24h window; meaningful convo (4+ messages each within 48 hours); meetup intent expressed.

**Key constraints:**
- Connection opportunity **expires in 24 hours** if not mutual — profile disappears from Nearby Now
- User must be **actively moving** (not stationary) to appear in others' Nearby Now feeds
- Exact location is **never shared** — only approximate distance ("0.3 mi away")

### J3: Safety Incident
1. User reports/block from chat or profile  
2. Immediate separation (hard block)  
3. Review + enforcement actions

**Success:** fast resolution; repeat offenders reduced.

---

## 5) MVP1 Scope (P0 Features)

### 5.1 Onboarding & Identity
- Phone verification (required)
- Age gate 18+ (required)
- City/Metro selection (NYC or SoCal)
- Mode selection: Friends / Dating / Both
- Location permission grant (required — core to geo-movement matching)
- Basic preferences:
  - **Proximity radius** (default: 1 mile, configurable: 0.5 / 1 / 2 / 5 miles)
  - Age range
  - Gender/orientation (for dating logic)

**Acceptance:** user cannot enter discovery without verification + minimum profile completeness.

---

### 5.2 Profile (Simple & Authentic)

> **Design philosophy:** Profiles are intentionally minimal. No curated highlight reels, no algorithm-optimized prompt answers. The real person is discovered through conversation and meeting up — not a profile page. This is the anti-Hinge/Bumble approach.

**Required**
- **2–3 photos** (uploaded from gallery; selfies welcome and encouraged)
- **1 quote / catchline** — free text, max 150 chars (e.g., *"Life's too short for bad tacos"*)
- **1 emoji activity** — pick an emoji + short text, max 80 chars (e.g., 🍜 *"hunting for the best ramen"*, 🎸 *"live music on weeknights"*, 🏃 *"morning runs in Griffith Park"*)
- Age (auto from DOB)
- Mode (Friends / Dating / Both)

**Optional**
- Display name: handle/nickname OR first name
- Verified badge (if Professional Verification completed)

**Not included (by design)**
- No prompt library (Hinge-style "My most controversial opinion is…")
- No vibe tags or interest lists
- No bio / "About me" paragraph
- No Spotify, Instagram, or social media links
- No height, education, religion, or politics filters

**Acceptance**
- Minimum: 2 photos + quote + emoji activity → profile is live.
- No "completeness score" — all required fields are simple enough to fill in < 2 minutes.

**Phased additions**
- **Phase II**: Optional 2nd emoji activity. Optional "Ask me about…" single prompt.
- **Phase III**: Interaction-earned badges (e.g., "Great Conversationalist" voted by matches, "Always Shows Up" from meetup confirmations). Profile grows from behavior, not self-curation.

---

### 5.3 Geo-Movement Discovery — "Nearby Now" (Primary Feature I)

> **This replaces the traditional card-based discovery feed.** Users cannot browse profiles from home. They must go out and move to discover nearby users.

#### How It Works (Phase I — MVP1)

1. **Location polling**: App sends GPS coordinates to server every **10 minutes** via HTTPS POST
2. **Movement detection**: Server compares current position to last position. User is marked **"active"** if GPS displacement > **100 meters** within the last 30 minutes
3. **Proximity query**: Server finds all other active users within the configured radius (default: **1 mile / 1609 meters**) using PostGIS `ST_DWithin`
4. **Nearby Now feed**: Returns card-based list of nearby active users, sorted by proximity + heuristics
5. **Actions**: Like (whole profile) or Pass — simple binary action, no prompt-specific likes
6. **24-hour window**: Each nearby discovery expires **24 hours** after first appearance. If no mutual like by then, the connection opportunity disappears

#### Feed Content
- Profile cards showing: photos, quote, emoji activity, approximate distance ("~0.3 mi away")
- Verified badge overlay (if applicable)
- **Never** shows exact coordinates, street address, or real-time pin location
- Status / Catchline overlay if the user has one active

#### Ranking (heuristic, MVP1)
- Proximity (closest first)
- Mode compatibility (Friends/Dating/Both)
- Movement recency (more recently active = higher)
- Trust score (small boost if verified)

#### Daily Limits
- Daily like limit (tunable, same as before)
- Location updates: every 10 minutes when app is open or backgrounded

#### Movement Requirement
- Users who are **stationary** (< 100m displacement in 30 min) do NOT appear in others' Nearby Now feeds
- Stationary users CAN still browse their own Nearby Now feed (they see active users near them) but will see a prompt: *"Start moving to appear in others' feeds!"*
- This is the core gamification: **you must go out to be discovered**

---

### 5.4 Matching — Geo-Gated with 24h Expiry

#### Match Flow
1. User A likes User B's profile from Nearby Now feed
2. User B receives notification: *"Someone nearby liked your profile!"*
3. User B has **24 hours** from the original discovery to like back
4. If mutual like within 24h → **Match created** → Chat unlocks
5. If 24h expires without mutual like → connection opportunity removed silently

#### Expiry & Extend
- **24-hour countdown** visible on pending connections (visual timer, similar to Bumble)
- **1 free Extend per day** (adds 24 more hours) — available to free users
- Premium users: unlimited Extends

#### Unmatch & Block
- Unmatch: removes match, hides from each other
- Block: hard block — removes all mutual visibility permanently

#### Anti-abuse
- Rate limiting (likes/day, repeated rapid likes)
- GPS spoofing detection (see Section 5.9)
- Cannot re-discover the same user within 7 days after a Pass or expired connection

#### Mode Rules
- Friends-only users do not appear in Dating-only Nearby Now feeds
- "Both" users can be shown to Friends + Dating audiences

---

### 5.5 Messaging
- Text chat (MVP1) — **unlocked only after mutual geo-match**
- No messaging without matching (consent-first)
- In-chat controls: block, report
- Basic spam/scam detection (heuristics + rate limits)
- **"Meet Up" prompt**: After 4+ messages each, suggest meeting at a public location

**Photo sharing**
- Allowed **only for Verified** users (hard rule)

---

### 5.6 Status / Catchline (“Tonight I’m…”) — MVP1
- Short status (e.g., ≤ 60 characters)
- **Expires automatically** (default: 12 hours)
- Visibility controls (MVP1 minimal):
  - Matches only (default ON)
  - Everyone in discovery (default OFF / opt-in)
  - Hidden

**Safety guardrails**
- Discourage exact venue/address text (UX warning + simple detection)
- Provide preset suggestions (e.g., “Trying a new spot”, “Coffee walk”, “Live music”)

---

### 5.7 Professional Verification — Tiered Trust System

> **Key differentiator**: No major dating app verifies professional credentials (except The League at $300+/mo). HingeX brings Blind-style work email verification + LinkedIn validation to social connections at accessible pricing. Verified profiles see **67% more matches** and **200% more dates** (industry benchmarks).

#### Overview

Professional verification is **optional but incentivized**. Three tiers, each adding trust signals. Same price for all genders (legally required — see Risks). Annual subscription model.

#### Tier Structure

| Tier | Method | Annual Cost | Badge | What's Displayed | Perks |
|------|--------|-------------|-------|-----------------|-------|
| **Silver** | Work email verification | $35/yr | Silver shield | Company name (derived from email domain) | Photo sharing in chat, small ranking boost, "Verified" filter access |
| **Gold** | Work email + LinkedIn | $59/yr | Gold shield | Company name + title + "Verified on LinkedIn" badge | Everything in Silver + priority in Nearby Now feed, profile highlighted |
| **Platinum** | Work email + LinkedIn + ID verification | $99/yr | Platinum shield | Company + title + "Identity Verified" badge | Everything in Gold + top placement in Nearby Now, exclusive Platinum-only filter |

#### Work Email Verification Flow (Blind-style — Phase I)

```
1. User taps "Verify Professional" in profile settings
2. User enters work email (e.g., joe@microsoft.com)
3. System checks domain against free email blocklist (Gmail, Yahoo, etc.)
   ├── If free/personal email → Rejected: "Please use your work email"
   └── If corporate domain → Continue
4. System sends 6-digit OTP to work email (10-min TTL)
5. User enters OTP in app
6. System maps email domain to company name (via enrichment API)
7. Email is hashed + salted + encrypted, stored separately from profile data
8. Company name badge appears on profile: "Microsoft" with Silver shield
9. Plaintext email deleted from all systems
```

**Domain-to-company mapping**: Use enrichment APIs (Hunter.io free tier: 50 searches/mo, or Abstract API) to resolve `@microsoft.com` → "Microsoft". Maintain internal lookup table for top 1,000 company domains as fallback.

**Privacy architecture** (inspired by Blind):
- Auth server stores hashed email + company domain — NO profile/activity data
- Activity server stores company label + badge tier — NO email data
- No API endpoint joins auth data with activity data
- Verification email is the **only** email ever sent to the work address

#### LinkedIn Verification Flow (Phase II)

```
1. User taps "Upgrade to Gold" after Silver verification
2. OAuth flow: "Sign in with LinkedIn" → user authorizes app
3. Phase II (Lite tier - free): Pull verification status only
   → Display "Verified on LinkedIn" badge if user has workplace verification
   → Title/company still self-reported (confirmed by work email)
4. Phase III (Plus tier - requires LinkedIn BD approval): Pull title + company directly
   → Display "AI Director at Microsoft" with LinkedIn badge
   → Auto-populate from LinkedIn, user confirms
5. LinkedIn data refreshed only when user actively re-verifies (annually)
```

#### ID Verification Flow (Phase II+)

- Selfie/liveness check via vendor (e.g., Jumio, Onfido, Veriff)
- Government ID scan matched against selfie
- Vendor cost: ~$1-3 per verification (covered by $99/yr Platinum fee)
- Badge: "Identity Verified" — confirms the person is who they claim to be

#### Annual Re-verification

- All tiers require **annual re-verification** to maintain badge (addresses Blind's stale-verification problem — people keep badges after leaving jobs)
- 30-day grace period after expiry
- Push notification at 30 days, 7 days, and 1 day before expiry
- Expired badges show as "Verification expired" (greyed out) until renewed
- Re-verification cost = renewal at same tier price

#### "Verified Only" Filter

- Available **only to verified users** (any tier) — creates network effect and incentive to verify
- Verified users can toggle "Show me only verified users" in Nearby Now preferences
- Non-verified users see all profiles (verified and unverified)
- Verified profiles show badge in Nearby Now cards and in chat

#### Spam Reduction

- Work email verification eliminates most bots (bots don't have corporate email)
- Paid verification ($35+/yr) creates economic barrier against spam accounts
- Verified-only filter lets users opt into a higher-trust environment
- Expected impact: **40-67% reduction** in fake/spam profiles among verified users

#### Phased Rollout

| Component | Phase I (S) | Phase II (M) | Phase III (L) |
|-----------|-------------|--------------|---------------|
| **Work email** | OTP + domain mapping | Same | Same |
| **LinkedIn** | Not available | Lite tier (badge only) | Plus tier (title + company pull) |
| **ID verification** | Not available | Selfie/liveness vendor | + ML fraud detection |
| **Tiers available** | Silver only | Silver + Gold | Silver + Gold + Platinum |
| **Pricing** | $35/yr (Silver) | + $59/yr (Gold) | + $99/yr (Platinum) |
| **Enrichment API** | Hunter.io free tier + manual table | Abstract API paid | Clearbit/custom |
| **Build effort** | ~0.5 sprint | ~1 sprint | ~1 sprint |

#### Example Profile Display

```
┌──────────────────────────────────┐
│  [Photo]                          │
│                                   │
│  Joe, 32                          │
│  🥇 AI Director at Microsoft     │
│  ✓ Verified on LinkedIn           │
│  ~0.4 mi away                     │
│                                   │
│  "Life's too short for bad tacos" │
│  🍜 hunting for the best ramen   │
│                                   │
│  Status: "Tonight I'm exploring   │
│   new coffee spots in SoHo"       │
└──────────────────────────────────┘
```

---

### 5.8 Trust & Safety (Baseline)
- Report categories: harassment, hate, sexual content, scam, underage, impersonation
- Hard block: removes mutual visibility (feed + chat)
- Rate limiting and spam controls
- Underage fast-path: suspend pending review

---

### 5.9 Primary Feature I: Geo-Movement Matching — Full Spec & Phased Roadmap

> This section defines the complete vision for geo-movement matching across three phases, sized by implementation complexity and funding level.

---

#### Phase I (S) — "Proximity Polling" | Pre-seed / Bootstrapped | ~1 Sprint

**Target**: Validate the core thesis — does movement-gated matching drive better connections?

| Component | Implementation |
|-----------|---------------|
| **Location capture** | Client sends GPS coords via HTTPS POST every **10 minutes** |
| **Storage** | Supabase Postgres + PostGIS extension. `user_locations` table with `geography(Point, 4326)` column + spatial index |
| **Proximity query** | `ST_DWithin(a.location, b.location, 1609)` — 1609 meters = 1 mile |
| **Movement detection** | Server-side: compare current coords vs previous coords. Active = displacement > 100m in last 30 min |
| **Nearby Now feed** | Server returns profiles within radius who are active. Client polls every 10 min. |
| **24h expiry** | `discovered_at` timestamp on each connection opportunity. Supabase cron (pg_cron) expires rows older than 24h. |
| **Anti-spoof (basic)** | Android: check `isFromMockProvider()`. Both platforms: flag if speed between pings > 100 mph. |
| **Privacy** | Only approximate distance shown ("~0.3 mi"). Exact coordinates never sent to other users. Location data auto-deleted after 48h. |

**Architecture (Phase I):**
```
Mobile App (foreground/background)
  └─→ HTTPS POST /api/location  (every 10 min)
        └─→ Supabase Edge Function
              ├─→ UPDATE user_locations SET location = ST_SetSRID(ST_MakePoint(lng, lat), 4326)
              ├─→ Check displacement from last location (movement detection)
              └─→ SELECT nearby active users via ST_DWithin
                    └─→ Return "Nearby Now" feed to client
```

**Infra cost estimate:**
| Users (MAU) | Supabase Tier | Est. Monthly Cost |
|-------------|---------------|-------------------|
| 0–500 | Free | $0 |
| 500–5,000 | Pro | ~$25 |
| 5,000–20,000 | Pro + compute add-on | ~$50–100 |

---

#### Phase II (M) — "Smart Polling + Geofence Zones + Gamification" | Pre-seed Funded ($100K–$500K) | ~2 Sprints

Everything in Phase I, plus:

| Component | Implementation |
|-----------|---------------|
| **Adaptive polling** | 10 min when stationary → **2–3 min when moving** (using OS significant-change location API) |
| **H3 hexagonal zones** | Divide metro areas into Uber H3 hexagons (resolution 8, ~0.7 km² each). Each zone has an ID. |
| **Zone discovery** | When user enters a new H3 zone, log it. Track which zones each user has visited. |
| **Explorer Score** | Points for visiting new zones. Shown on profile. |
| **Badges** | "Night Owl" (3+ zones after 8pm), "Weekend Warrior" (5+ zones Sat–Sun), "Neighborhood Explorer" (10+ unique zones), "First Mover" (first person in a zone that day) |
| **Leaderboard** | Opt-in weekly leaderboard (friends or metro-wide). Rewards: priority placement in Nearby Now. |
| **Zone-aware discovery** | "2 active users in your zone" push notification. Nearby Now shows zone context. |
| **Connection Extend** | 1 free Extend/day (24h → 48h). Premium: unlimited. |
| **Anti-spoof (enhanced)** | + Velocity anomaly detection (impossible travel). + Cross-validate GPS vs IP geolocation region. + Flag jailbroken/rooted devices. |
| **Supabase Realtime** | WebSocket subscription for **matched pairs only** (chat + "nearby now" indicator on match). Discovery still uses polling. |

**New gamification analytics:**
- `zone_entered`, `zone_discovered_new`, `explorer_score_updated`, `badge_earned`
- `nearby_user_detected`, `connection_extended`, `connection_expired`
- `leaderboard_viewed`, `leaderboard_rank_changed`

**Infra cost estimate:**
| Users (MAU) | Est. Monthly Cost |
|-------------|-------------------|
| 5,000 | ~$50–150 |
| 20,000 | ~$150–300 |

---

#### Phase III (L) — "Real-Time Roaming" | Seed Funded ($500K+) | ~4–6 Sprints

Everything in Phase II, plus:

| Component | Implementation |
|-----------|---------------|
| **Real-time location** | **WebSocket persistent connection** when app is foregrounded. Background: OS significant-change events. Sub-second proximity awareness. |
| **Live "pulse" UI** | Map-like interface with **fuzzy zones** (not exact pins). Nearby users appear/disappear as you walk. Animated proximity rings. |
| **Encounter Streaks** | Match in 3 different zones in a week → streak bonus. Seasonal challenges ("Explore 20 zones this month"). |
| **Team challenges** | Friend groups explore together. Group explorer score. |
| **Unlockable profile flair** | Earn badges, borders, and effects through movement milestones. |
| **Smart suggestions** | "3 active users at Zone X (0.4 mi away) — head that direction?" AI-powered nudges based on popular zones and user preferences. |
| **Meeting flow** | After match + chat: in-app **"Meet Up" card** suggesting nearby public venues (parks, cafes). Both users confirm. **Safety check-in timer** after meetup begins (opt-in). |
| **Anti-spoof v2** | ML-based anomaly detection. Device attestation (Android SafetyNet / iOS App Attest). Behavioral movement pattern analysis. |
| **Privacy (enhanced)** | Differential privacy on aggregated location data. Fuzzy zone display only (never exact coords). All location data auto-purges after 48h. GDPR/CCPA compliant location data handling. |

**Infra cost estimate:**
| Users (MAU) | Est. Monthly Cost |
|-------------|-------------------|
| 5,000 | ~$300–800 |
| 50,000 | ~$1,000–3,000 |

---

#### Phase Comparison Summary

| Dimension | Phase I (S) | Phase II (M) | Phase III (L) |
|-----------|-------------|--------------|---------------|
| **Funding level** | Bootstrapped | Pre-seed ($100K–$500K) | Seed ($500K+) |
| **Location updates** | 10-min HTTP polling | Adaptive 2–10 min polling | Real-time WebSocket |
| **Movement detection** | GPS displacement | GPS + significant-change API | GPS + pedometer + ML |
| **Discovery** | Nearby Now list | Zone-aware Nearby Now + push | Live map with fuzzy zones |
| **Gamification** | None | Explorer Score + badges | Streaks + teams + flair |
| **Anti-spoof** | Basic flag checks | Velocity + IP cross-validation | ML + device attestation |
| **24h expiry** | Yes | Yes + Extend mechanic | Yes + Extend + smart suggestions |
| **Meeting support** | None | None | In-app Meet Up cards + safety check-in |
| **Build effort** | ~1 sprint | ~2 sprints | ~4–6 sprints |
| **Infra @ 5K MAU** | ~$25/mo | ~$50–150/mo | ~$300–800/mo |

---

## 6) Monetization (Pay-to-save-time)

### Philosophy
Avoid “pay-to-win” mechanics (e.g., pay-to-message or unlimited likes). Monetize by **reducing friction** and improving efficiency.

### MVP1 Offering
**Free**
- Limited likes/day
- Basic filters (age/proximity radius)
- Nearby Now feed (standard refresh rate)
- 1 free Extend per day (24h → 48h on a pending connection)

**Premium**
- 2–3x likes/day (not unlimited)
- Activity-match filter (e.g., "show me users with similar emoji activities")
- Rewind last pass
- **Unlimited Extends** (extend any expiring connection)
- **Expanded radius option** (up to 5 miles, default 1 mile)
- **Priority placement** in Nearby Now feed (small boost)

**Professional Verification (annual)**
- Silver: $35/yr — work email verification, company badge, verified filter access
- Gold: $59/yr — work email + LinkedIn, title + company displayed (Phase II+)
- Platinum: $99/yr — work email + LinkedIn + ID verification, top placement (Phase II+)

**A la carte**
- Priority like (rose-equivalent)
- Light "spotlight" boost (capped)
- **Re-discover** (bring back one expired connection from the last 7 days)

---

## 7) Success Metrics (MVP1)

### North Star
- **Meaningful Conversations per Active User (MCAU)**  
  *Definition (MVP1):* ≥ 4 messages each way within 48 hours, not blocked/reported.

### Supporting metrics
- Activation: profile completion rate (target: < 2 min), location permission grant rate, **time to first outing**, time to first like, time to first match
- Engagement: D1/D7 retention, likes/day, matches/week, **outings/week** (sessions with movement detected), **unique zones visited** (Phase II)
- Geo-movement: **avg Nearby Now users per session**, **24h conversion rate** (% of discoveries that become mutual matches), **Extend usage rate**
- Quality: reply rate, unmatch rate, report rate per 1,000 chats, **meetup intent rate** (% of chats where meeting suggested)
- Safety: time-to-action on reports, repeat offender rate, **spoof flag rate**
- Revenue: free→paid conversion, ARPPU, churn (later)

---

## 8) Analytics Events (Minimal Taxonomy)

**Onboarding**
- `signup_started`, `phone_verified`, `age_verified`, `mode_selected`, `profile_completed` (with `completion_time_seconds`)
- `location_permission_granted`, `location_permission_denied`

**Geo-Movement (Primary Feature I)**
- `location_update_sent` — each 10-min ping
- `movement_detected` — user crossed 100m displacement threshold
- `movement_stopped` — user became stationary
- `nearby_now_loaded` — feed rendered with count of nearby users
- `nearby_now_empty` — feed loaded but zero nearby active users

**Discovery & Matching**
- `like_sent`, `like_received`, `match_created`
- `connection_expired` — 24h window elapsed without mutual like
- `connection_extended` — user used Extend on a pending connection
- `connection_rediscovered` — user purchased Re-discover (a la carte)

**Chat & Meeting**
- `chat_opened`, `message_sent`
- `meetup_suggested` — Phase III: Meet Up card shown
- `meetup_confirmed` — Phase III: both users confirmed

**Status**
- `status_set`, `status_expired`, `status_visibility_changed`

**Safety & Moderation**
- `report_submitted`, `block_created`
- `spoof_flag_triggered` — GPS spoofing detection fired

**Revenue**
- `paywall_viewed`, `subscription_started`, `purchase_completed`

**Professional Verification**
- `verification_started` — user tapped "Verify Professional"
- `work_email_submitted` — corporate email entered
- `work_email_rejected` — free/personal email blocked
- `work_email_verified` — OTP confirmed, Silver badge granted
- `linkedin_connected` — LinkedIn OAuth completed (Phase II+)
- `linkedin_verified` — LinkedIn verification confirmed, Gold badge granted
- `id_verified` — ID + selfie match confirmed, Platinum badge granted (Phase II+)
- `verification_expired` — annual verification lapsed
- `verification_renewed` — user re-verified and renewed
- `verified_filter_enabled` — user toggled "Show only verified"
- `verified_filter_disabled` — user toggled filter off

**Gamification (Phase II+)**
- `zone_entered`, `zone_discovered_new`, `explorer_score_updated`, `badge_earned`
- `leaderboard_viewed`

---

## 9) Architecture (High-level, Low-cost MVP)

### Suggested Lean Stack (example)
- **Auth**: Firebase Auth or Supabase Auth (phone)
- **DB**: **Supabase Postgres + PostGIS extension** (required for geo-movement matching)
- **Geo indexing**: PostGIS spatial index on `user_locations` table. `ST_DWithin` for proximity queries. (Phase II: add Uber H3 via `h3-pg` extension)
- **Location service**: Supabase Edge Functions — receives location pings, runs proximity queries, returns Nearby Now feed
- **Expiry service**: `pg_cron` job runs every 5 min to expire 24h-old connection opportunities
- **Media**: Object storage (S3/GCS) with signed URLs
- **Chat**: Stream/Sendbird/Firebase realtime (choose based on cost). Phase III: Supabase Realtime for live proximity indicators.
- **Moderation**: basic text filters + enforcement service
- **Anti-spoof**: Edge function validates location pings (mock location flag, velocity checks)
- **Verification service**: Work email OTP + domain-to-company mapping. Separate auth DB for hashed emails (Blind-style privacy). Phase II+: LinkedIn OAuth (Verified on LinkedIn API), ID verification vendor (Jumio/Onfido/Veriff)
- **Email enrichment**: Hunter.io (free tier: 50 lookups/mo) or Abstract API for domain→company mapping. Internal lookup table for top 1,000 company domains.

### Location Data Schema (Phase I)
```sql
-- User locations (updated every 10 min)
CREATE TABLE user_locations (
  user_id UUID PRIMARY KEY REFERENCES profiles(id),
  location GEOGRAPHY(Point, 4326) NOT NULL,
  previous_location GEOGRAPHY(Point, 4326),
  is_active BOOLEAN DEFAULT false,  -- true if displacement > 100m in 30 min
  updated_at TIMESTAMPTZ DEFAULT now()
);

CREATE INDEX idx_user_locations_geo ON user_locations USING GIST(location);

-- Connection opportunities (24h expiry)
CREATE TABLE nearby_connections (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  discoverer_id UUID REFERENCES profiles(id),
  discovered_id UUID REFERENCES profiles(id),
  discovered_at TIMESTAMPTZ DEFAULT now(),
  expires_at TIMESTAMPTZ DEFAULT now() + INTERVAL '24 hours',
  status TEXT DEFAULT 'pending',  -- pending, liked, mutual, expired
  extended BOOLEAN DEFAULT false
);
```

### Verification Schema (Phase I)
```sql
-- Professional verification (separate auth DB in production)
CREATE TABLE user_verifications (
  user_id UUID PRIMARY KEY REFERENCES profiles(id),
  tier TEXT DEFAULT 'none',          -- none, silver, gold, platinum
  company_name TEXT,                  -- derived from email domain
  company_domain TEXT,                -- e.g., 'microsoft.com'
  email_hash TEXT,                    -- salted + hashed work email
  title TEXT,                         -- self-reported (Phase I), LinkedIn-pulled (Phase III)
  linkedin_verified BOOLEAN DEFAULT false,
  id_verified BOOLEAN DEFAULT false,
  verified_at TIMESTAMPTZ,
  expires_at TIMESTAMPTZ,            -- verified_at + 1 year
  updated_at TIMESTAMPTZ DEFAULT now()
);

-- Domain-to-company lookup (internal enrichment cache)
CREATE TABLE company_domains (
  domain TEXT PRIMARY KEY,            -- e.g., 'microsoft.com'
  company_name TEXT NOT NULL,         -- e.g., 'Microsoft'
  logo_url TEXT,
  employee_count_range TEXT,          -- 'small', 'medium', 'large', 'enterprise'
  source TEXT DEFAULT 'manual'        -- 'manual', 'hunter', 'abstract', 'linkedin'
);
```

### Logical services (can start as a monolith)
- Auth/Profile
- **Verification** (new — work email OTP, domain mapping, LinkedIn OAuth, ID verification. Separate DB for hashed emails.)
- **Location/Geo** (new — handles pings, movement detection, proximity queries)
- Discovery/Ranking (now powered by Nearby Now geo-feed)
- Match/Chat
- Trust & Safety (includes anti-spoof)
- Payments/Entitlements
- Analytics

---

## 10) Risks & Mitigations

1. **Two-region liquidity risk (NYC + SoCal) — amplified by geo-movement requirement**
   Mitigation: concentrate marketing on micro-areas per metro first; referral loops. **Phase I risk**: low user density means few nearby active users. Mitigation: show "X users were active in your area today" to encourage return visits. Consider temporarily wider radius (2–3 mi) during early launch.

2. **Cold-start problem: "I went out and saw nobody"**
   Mitigation: seed initial markets with waitlist + coordinated launch events. Show historical activity ("12 users were active here yesterday") even if nobody is nearby right now. "Invite a friend" bonus: both get wider radius for a day.

3. **GPS spoofing / fake location**
   Mitigation: Phase I — basic mock location detection + velocity anomaly flags. Phase II — IP cross-validation + jailbreak detection. Phase III — device attestation + ML. Ban accounts confirmed spoofing.

4. **Location privacy and stalking risk**
   Mitigation: **never** expose exact coordinates. Show only approximate distance ("~0.3 mi"). 48h auto-purge of all location data. Location shared only while app is active. Hard block immediately removes all mutual location awareness.

5. **Battery drain from location tracking**
   Mitigation: 10-min polling interval (Phase I) is very low drain. Use OS significant-change APIs where possible. Phase II adaptive polling only increases frequency when user is already moving.

6. **18+ safety exposure**
   Mitigation: strong report/block UX, anti-spam limits, verified gating for photo sharing, underage fast-path.

7. **Status feature increasing stalking/venue risk**
   Mitigation: default matches-only; explicit warnings; presets; detect and discourage exact addresses.

8. **Monetization harming match quality**
   Mitigation: cap paid advantages; avoid pay-to-message; run controlled experiments. Extend mechanic is pay-for-time, not pay-for-access.

9. **Gender-based pricing legal risk (CRITICAL)**
   California Unruh Civil Rights Act prohibits sex-based pricing. Tinder paid **$60.5M** (age-based pricing, 2018). Bumble paid **$3.26M** (gender-based feature, 2022). **Decision: same price for all genders at every tier.** No exceptions. If user base is gender-imbalanced, use time-limited launch promotions (not permanent gender pricing).

10. **Work email verification — stale credentials**
    Users may leave their company but retain the verification badge. Mitigation: **annual re-verification required**. 30-day grace period. Badge greys out if expired. This addresses a known Blind weakness.

11. **Work email verification — employer email blocking**
    Some companies block verification emails (reported on Blind). Mitigation: allow retry from personal device. Provide fallback: LinkedIn-only verification path (Phase II). Document known blocked domains.

12. **Verification creating class divide**
    Non-verified users may feel excluded if verified-only filters are popular. Mitigation: verified-only filter is opt-in, not default. Non-verified users always see all profiles. Unverified experience remains fully functional. Verification is positioned as "trust signal" not "premium access."

13. **LinkedIn API access risk**
    Plus tier (needed for title/company pull) requires LinkedIn BD approval and may be denied or expensive. Mitigation: MVP1 uses work email only (no LinkedIn dependency). Self-reported title validated by work email domain. LinkedIn is Phase II enhancement, not Phase I requirement.

---

## 11) Delivery Plan (Phased)

### Phase I — MVP1 (2 sprints) | Bootstrapped / Pre-seed

#### Sprint 1 — Core loop + Geo-Movement
- Auth + age gate + mode selection + **location permission**
- Profile builder (2-3 photos + quote + emoji activity) + minimum completeness gate
- **Location service**: POST endpoint, `user_locations` table with PostGIS, spatial index
- **Movement detection**: server-side displacement calculation
- **Nearby Now feed**: proximity query + card rendering
- **24h expiry**: `nearby_connections` table + pg_cron cleanup
- **Basic anti-spoof**: mock location flag + velocity check
- Text chat (unlocked on mutual match)
- Block/report

**Demo:** Create simple profile (< 2 min) → go out → see nearby active users → like → mutual match → chat

#### Sprint 2 — Status + Professional Verification + safety hardening + monetization
- Status feature (expiry + visibility)
- **Professional Verification (Silver tier)**: work email OTP flow, domain-to-company mapping, company badge on profile, hashed email storage
- **Verified-only filter** (available to Silver+ users)
- **Free email domain blocklist** + internal company domain lookup table (top 1,000)
- Verified gating for chat photos
- Rate limits + spam heuristics
- **Extend mechanic** (1 free/day)
- Premium entitlements + purchases (incl. unlimited Extends, expanded radius, Silver verification)
- Analytics + dashboards (including geo events + verification events)
- **"Meet at a public place" suggestion** in chat after 4+ messages

**Demo:** Full geo-movement loop + status + Silver verification badge + premium + safer messaging

---

### Phase II — Gamification + Smart Polling + Gold Verification (~2 sprints) | Pre-seed Funded ($100K–$500K)

- Adaptive polling (2–10 min based on movement)
- H3 hexagonal zone mapping for launch metros
- Explorer Score + badge system
- Zone-aware discovery + push notifications
- Opt-in leaderboard
- Enhanced anti-spoof (velocity + IP + jailbreak detection)
- Supabase Realtime for matched pairs (live "nearby" indicator)
- **Gold verification**: LinkedIn OAuth (Verified on LinkedIn Lite tier) — "Verified on LinkedIn" badge
- **Annual re-verification** enforcement + expiry notifications
- **ID verification vendor integration** (Jumio/Onfido/Veriff) for Platinum tier

**Demo:** Go out → explore zones → earn badges → verify with LinkedIn (Gold badge) → "Verified: Joe, AI Director at Microsoft" → match → chat

---

### Phase III — Real-Time Roaming + Platinum Verification (~4–6 sprints) | Seed Funded ($500K+)

- WebSocket real-time location (foreground)
- Live fuzzy-zone map UI
- Encounter Streaks + seasonal challenges + team challenges
- Unlockable profile flair
- Smart suggestions ("3 users near Zone X — head that way?")
- In-app Meet Up cards with venue suggestions
- Safety check-in timer after meetup
- ML anti-spoof + device attestation
- Differential privacy on location data
- **LinkedIn Plus tier** integration (pull title + company + education directly from LinkedIn)
- **Platinum verification** fully operational (work email + LinkedIn + ID)
- **Verification analytics dashboard** (conversion rates, tier distribution, renewal rates)

**Demo:** Walk around → live pulse of nearby users → see "Platinum Verified: Sarah, VP at Google" → match → chat → tap "Meet Up" → confirm public venue → safety check-in

---

## 12) Open Questions

### MVP1 (Phase I)
- What is the minimum viable user density per square mile to make Nearby Now useful? Need to model for NYC vs. SoCal suburban areas.
- Should the 100m displacement threshold be tunable per market (denser city = lower threshold)?
- How to handle users who commute through areas (passive movement) vs. users who are intentionally out socializing? Is all movement equal?
- Should there be a "quiet hours" mode where location tracking pauses (e.g., late night)?
- If a user denies location permission, what fallback experience exists? (Currently: none — location is required.)
- How many company domains should be pre-seeded in the lookup table for launch? (Suggest: Fortune 500 + top 500 tech companies = ~1,000 domains)
- Should Silver verification be offered free during launch to seed the verified user base?
- How to handle contractors with company email domains? (They'd verify as the company — is this acceptable?)

### Phase II
- Add selfie/liveness verification vendor? timeline/cost? (Jumio ~$1-3/check, Onfido ~$2-4/check, Veriff ~$1-2/check)
- H3 zone resolution: resolution 8 (~460m edge) vs resolution 9 (~174m edge) — which feels right for "neighborhood" zones?
- Should Explorer Score decay over time (use-it-or-lose-it) or be cumulative?
- Leaderboard scope: friends-only vs. metro-wide vs. zone-local?
- LinkedIn Plus tier: when to apply to LinkedIn BD team? Need user traction metrics to demonstrate value.
- Should .edu and .gov emails be accepted for Silver verification? What company name to display?

### Phase III
- Add voice notes or date planning cards?
- In-app Meet Up: integrate with venue APIs (Yelp/Google Places) for public location suggestions?
- Safety check-in: partner with safety apps (Noonlight, bSafe) or build in-house?
- Expand beyond NYC/SoCal: next market selection criteria? (Density-dependent feature requires careful market selection.)
- WebSocket infrastructure: Supabase Realtime vs. dedicated solution (Ably, Pusher) at scale?
- Should Platinum verification include background check integration? (Legal and cost implications.)
- LinkedIn data retention: how long can we cache title/company before requiring refresh?

---

## 13) Enhancements to Review

> Proposed enhancements for future consideration. Not committed to any phase — pending review, prioritization, and user research validation.

---

### 13.1 Gamification — "The dating app that rewards you for leaving the house"

#### Option S — "Go Out Streaks" (Low effort, ~2-3 days)
*Candidate for: Phase I / MVP1*

| Mechanic | How It Works |
|----------|-------------|
| **Outing Points** | Earn **10 pts** each time detected as active (moved 100m+). Max 1 claim per 4-hour window to prevent gaming. |
| **Daily Streak** | Consecutive days going out → streak counter on profile. 3-day streak = **2x points**. 7-day = **3x points**. Miss a day = reset. |
| **Weekly Reward** | 3+ outings in a week → earn **1 free Extend** (normally paid). Tangible reward tied to core matching loop. |
| **Match Bonus** | +25 pts for mutual match. +50 pts for 4+ message exchange. Rewards real connection, not just showing up. |
| **Profile badge** | Flame icon + streak count on Nearby Now card: 🔥7 = "7-day streak" |

**Why it works:** Streak psychology is proven (Snapchat, Duolingo). Costs nothing extra — just a counter + a few DB columns. Free Extend ties gamification directly to the matching loop.

---

#### Option M — "Explorer Levels + Nightlife Multipliers" (Moderate effort, ~1 sprint)
*Candidate for: Phase II (depends on H3 zone infrastructure)*

| Mechanic | How It Works |
|----------|-------------|
| **Zone Discovery** | First time entering a new H3 zone = **25 pts** + "New Zone!" animation. 10 unique zones = **Bronze Explorer**. 25 = **Silver**. 50 = **Gold**. |
| **Time Multipliers** | Happy Hour (5-8pm): **1.5x** points. Night Out (8pm-2am Fri/Sat): **2x** points. Weekend Brunch (10am-2pm Sat/Sun): **1.5x** points. Rewards the times people actually want to meet. |
| **Explorer Level** | Total points → level (1-50). Shown on profile. Higher levels = small boost in Nearby Now ranking. |
| **Weekly Challenges** | Auto-generated: *"Visit 3 new zones this week"* (+100 pts), *"Go out on a weeknight"* (+50 pts), *"Match with someone in a new zone"* (+75 pts). |
| **Points Store** | Spend points on: free Extends (200 pts), Re-discover expired connection (500 pts), priority Nearby Now placement for 1 hour (300 pts). |

**Why it works:** Zone discovery creates an exploration game on top of dating. Time multipliers push users out when venues are active. Points store gives a reason to accumulate without spending real money.

---

#### Option L — "Social Quests + Crew Mode" (High effort, ~3-4 sprints)
*Candidate for: Phase III*

| Mechanic | How It Works |
|----------|-------------|
| **Weekly Quests** | Multi-step challenges: *"The Explorer: Visit 5 zones → Match → Exchange 10 messages → Suggest a meetup"* = **500 pts** + exclusive badge. Rotate weekly. |
| **Crew Mode** | Form a crew (2-5 friends). Collective crew points. Crew challenges: *"Your crew explored 15 zones this week — top 10% in NYC!"*. Crew leaderboard. Crews can "claim" zones they visit most. |
| **Seasonal Events** | Monthly themes: *"Summer Night Challenge"* (3x for outings after 9pm), *"Brunch Marathon"* (points for 4 weekend brunches in a row). Limited-edition profile badges. |
| **Interaction Rewards** | *"Great Conversationalist"* — voted by 3+ matches. *"Always Shows Up"* — confirmed 3+ meetups. *"Connector"* — introduced 2 friends who matched. Permanent badges earned through behavior, not self-curation. |
| **Zone Leaderboard** | *"Top Explorer in Williamsburg this week"* — opt-in per-zone leaderboard. Top 3 get highlighted placement in that zone's Nearby Now the following week. |
| **Points Tiers** | Lifetime accumulation: **Newcomer** (0-500) → **Regular** (500-2K) → **Explorer** (2K-10K) → **Legend** (10K+). Legend = permanent profile flair + priority in all zones. |

**Why it works:** Crew Mode turns dating-app-awkwardness into a group activity ("let's go out and earn points together"). Interaction rewards mean your profile improves the more genuinely you engage — the ultimate anti-fake mechanic. Seasonal events drive retention spikes.

**Recommendation:** Ship Option S with MVP1 (streaks + outing points create immediate habit loops). Plan Option M for Phase II when H3 zones land. Option L is the long-term retention moat.

---

### 13.2 Primary Feature III — "Vibe Map": Real-Time Crowd Density + Nightlife Discovery

> **Problem:** "Where's the party at?" Google reviews are stale. Users want to know which bars and restaurants are actually busy *right now* — not which ones had a good review 6 months ago. Users currently have to hop bar to bar just to find the one that's actually crowded.

> **Opportunity:** HingeX already collects user geo-location data for Nearby Now. That same data can power a real-time heat map showing where people are congregating — a Waze-style crowd density map for nightlife. This becomes a **third pillar differentiator** and a **future revenue engine** (bar/restaurant advertising).

> **Data source: Internal only.** No third-party APIs. The Vibe Map is powered entirely by HingeX users' own rough GPS data (already being collected for Nearby Now). This is a Waze-like internal feature — the value scales with the user base.

> **MVP1 approach:** Ship a **simulated** Vibe Map for investor demos. Seed heat dots in known nightlife districts (East Village, WeHo, etc.) using realistic patterns. The simulation validates the UX and the value prop. Real user-powered data goes live in Phase II when user density supports it (target: 3+ users per H3 cell in active nightlife areas).

> **Cold start reality:** At <5K users in a city, real density data will be sparse. Strategy: concentrate launch in 1 neighborhood first to hit critical density faster. The simulated MVP1 buys time.

#### MVP1 — Simulated Vibe Map (~2-3 days)
*Ships with MVP1 for investor demo.*

| Aspect | Detail |
|--------|--------|
| **What users see** | Map view with colored heat dots in known nightlife districts. Warmer colors = more activity. Looks and feels like the real Vibe Map. |
| **Data source** | **Seeded/simulated** — realistic dot patterns in popular bar zones (East Village, LES, WeHo, Santa Monica). Patterns vary by time of day and day of week to feel authentic. |
| **Map SDK** | Google Maps SDK for iOS/Android — **completely free**, no usage caps. Heatmap via utility library (`HeatmapTileProvider` on Android / `GMUHeatmapTileLayer` on iOS). |
| **Access** | Visible to all users (demo feature). Premium-gated in Phase II when real data goes live. |
| **Build effort** | ~2-3 days (map view + heatmap overlay + seeded data JSON + time-of-day logic) |
| **Infra cost** | Google Maps mobile SDK: **$0**. Seeded data: static JSON, no API cost. |
| **Purpose** | Validate UX, gather user feedback on the concept, show investors the vision is tangible. |

---

#### Option S — "Vibe Map" — Real User-Powered Heat Dots (~1 sprint)
*Candidate for: Phase II*

| Aspect | Detail |
|--------|--------|
| **What users see** | Map view with colored dots showing where HingeX users are actually concentrated. 1 dot = 3+ users in a cluster. Warmer colors = more people. |
| **Data source** | **Internal only** — your own geo-location data (already collected for Nearby Now). No third-party APIs. |
| **Map SDK** | Google Maps SDK for iOS/Android — **completely free**, no usage caps. Heatmap via utility library (`HeatmapTileProvider` on Android / `GMUHeatmapTileLayer` on iOS). |
| **Privacy** | k-anonymity: **minimum 3 users** in a cell before showing a dot. Never show a dot for 1-2 people. H3 resolution 9 (~174m cells). Dots are approximate, not exact positions. |
| **Access** | Premium feature (paid users only). Free users see Nearby Now list only. |
| **Cold start strategy** | Concentrate launch in 1 neighborhood. Transition from simulated (MVP1) to real data when a zone consistently has 3+ active users during peak hours. Blend: show real dots where data exists, fade out gracefully where it doesn't. |
| **Update frequency** | Refreshes every 10 min (matches existing location polling interval). |
| **Infra cost** | Google Maps mobile SDK: **$0**. PostGIS aggregation: negligible (already running). |
| **Build effort** | ~1 sprint (aggregation query + H3 cell grouping + privacy threshold + transition from simulated data) |

**Technical architecture:**
```
Existing location polling (every 10 min)
  → user_locations table (PostGIS)
  → Aggregate into H3 hex-9 cells
  → Filter: only show cells with >= 3 users (k-anonymity)
  → Weight by user count
  → Send weighted lat/lng array to client
  → Client renders via Google Maps heatmap utility library
```

**Why it works:** Zero additional data collection needed — piggybacks on existing Nearby Now location data. Google Maps mobile SDK is free. No third-party dependency. Premium-only access creates monetization lever. The value scales directly with user growth — a built-in network effect.

---

#### Option M — "Vibe Map + Venue Cards" — See what's nearby & what's happening (~2 sprints)
*Candidate for: Phase III*

Everything in Option S, plus:

| Aspect | Detail |
|--------|--------|
| **Venue overlay** | Tap a hot zone → see venue cards (bar name, rating, hours, "seems busy" / "packed" / "quiet"). Powered by **Google Places API** + **Foursquare Places API** (free 10K calls/mo). |
| **Deal cards** | Merchants can post deals (happy hour, specials) via a self-service portal. Shown as pins on the Vibe Map. |
| **Social signal** | "5 HingeX users here now" badge on venue card. Only shows if 3+ users present at that venue (privacy). |
| **Push nudges** | Geofenced notifications for active users: *"A bar 0.3 mi from you has 12 people — head that way?"* |
| **Venue busyness labels** | Instead of precise numbers, use fuzzy labels: "Quiet" / "Getting busy" / "Packed" / "At capacity" — more forgiving of small sample sizes. |
| **Merchant self-service** | Simple web portal: create account → claim venue → post deals → view impressions. |

**Revenue model:**

| Model | Price | Effort |
|-------|-------|--------|
| **Promoted listings** | $50-200/mo per merchant — highlighted pin + priority placement | Low — sort/display change |
| **Geofenced push** | $0.05-0.25 per notification delivered to nearby users | Medium — notification infrastructure |
| **Featured deal cards** | $100-500/mo for premium placement in deal feed/map | Low — display logic |

**Infra cost:** Google Places API: ~$17/1K calls (queries on tap only, not passive). Foursquare: free tier covers early scale. Merchant portal: standard CRUD app.

**Why it works:** Venue cards give context to the dots. Deal cards create a reason for bars to engage (and pay). Push nudges drive foot traffic — which is exactly what bars want to buy. The "5 HingeX users here" social signal is something Google Maps can never offer.

---

#### Option L — "Vibe Map + AR Overlay + Nightlife Marketplace" (~4-6 sprints)
*Candidate for: Phase IV+*

Everything in Option M, plus:

| Aspect | Detail |
|--------|--------|
| **AR camera view** | Point phone at a street → see floating deal cards anchored to real bar locations. *"🍺 $5 margaritas until 8pm"* hovering over the bar entrance. Uses **ARKit geo-anchors** (iOS) / **ARCore Geospatial API** (Android). |
| **Live venue vibe** | Short video clips (10-sec, Atmosfy-style) uploaded by users showing the energy inside. *"See the vibe before you walk in."* |
| **Merchant dashboard** | Full self-service: create deals, view impressions/clicks/visits, analytics on foot traffic driven by HingeX. |
| **Visit verification** | Detect when a user enters a venue after seeing a deal → charge merchant per verified visit (CPV model). |
| **Crew coordination** | "Your crew is heading to [Bar X] — join them?" Ties into Crew Mode (see 13.1 Option L). |

**Revenue models (layered):**

| Model | Price | Effort |
|-------|-------|--------|
| **CPC deal clicks** | $1-3 per click on deal detail | Medium — click tracking + billing |
| **CPV verified visits** | $5-15 per verified foot traffic visit | High — visit verification |
| **Commission on redemptions** | 10-20% of deal value when redeemed | High — redemption tracking |
| **Sponsored AR experiences** | $500-2K per campaign (custom branded AR overlays) | Very high — custom AR content |

**Data moat — why this is defensible:**
Your app uniquely knows:
- Where users are **right now** (real-time location)
- Where users **tend to go** (historical patterns)
- **When** users go out (activity patterns)
- **Who** users go out with (social graph from matches/crews)

No other platform — not Google, not Yelp, not Atabarra — has this combination for the nightlife vertical. A bar owner pays a premium to reach *"people who are out right now, within walking distance, looking for somewhere to go"* vs. generic mobile ad impressions.

**AR technical notes:**
- ARKit geo-anchors require iOS 14+, A12 chip+, and Apple's location anchor coverage (major US cities covered)
- ARCore Geospatial API uses Google's Visual Positioning System (Street View imagery) — free, covers most urban areas
- Both SDKs are free. The cost is in building content creation tools and the AR UX.
- **Recommendation:** Build map-based deals first (Option M). Add AR as a "wow factor" layer once the merchant pipeline is established. AR without deals to show is an empty gimmick.

**Infra cost:** ARKit/ARCore SDKs: free. Venue data APIs: ~$100-300/mo. Merchant portal + dashboard dev: significant. Video hosting (if vibe clips): ~$50-100/mo at scale.

---

**Lessons from failed apps in this space:**
- **SceneTap** (cameras in bars to count patrons) — shut down after ACLU backlash and patron boycotts. Lesson: don't use invasive tracking.
- **BarPeak → Atmosfy** — pivoted from busyness data to video reviews. Lesson: busyness data alone isn't compelling enough; layer social/visual content on top.
- **Foursquare check-ins** — check-in fatigue killed the consumer product (shut down Dec 2024). Lesson: passive data beats manual check-ins.
- **Google Maps Popular Times** — works because of 3B+ Android devices. Lesson: you can't out-Google Google on raw data; compete on social context and deals instead.

**Recommendation:** Ship Option S in Phase II (heat dots are ~1 sprint on top of existing geo infra). Option M in Phase III adds the revenue engine (merchant deals). Option L is the long-term vision — AR + marketplace — but only after proving merchant demand with Option M.
