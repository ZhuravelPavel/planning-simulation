# Dual-Revenue Strategy: Development & Launch Work Plan

**Status**: Technical foundation in POC, core development tasks pending  
**Approach**: Not detailed, not personalized (roles only, no names)

---

## EPIC 1: PLATFORM/TENANT ENTITLEMENT INFRASTRUCTURE

**Status**: POC exists, implementation pending

### Story 1.1: Split Platform & Tenant Authorities
- Complete codebase separation between platform (billing) and tenant (local users/IRC)
- Configure separate WordPress databases for platform vs tenants
- Implement OAuth account linking flow

### Story 1.2: Implement Entitlement Resolution System
- Create entitlement schema (platform + tenant grants)
- Build effective entitlement resolver (merges platform + tenant grants)
- Add capability derivation logic

### Story 1.3: Platform Subscription Webhooks
- Build platform webhook emitter for subscription events
- Build tenant webhook receiver for entitlement projection
- Implement link-time entitlement sync

### Story 1.4: Staging Integration & Deployment
- Update staging integration tests for platform/tenant separation
- Deploy to staging environment
- Verify end-to-end entitlement flow

---

## EPIC 2: OFFLINE MESSAGING IMPLEMENTATION

**Status**: Design confirmed, implementation pending

### Story 2.1: Message Store & Queueing
- Implement offline message storage helper
- Add message queue for offline users
- Create sender acknowledgment system

### Story 2.2: Capability-Based Gating
- Gate offline messaging by entitlements
- Implement sender/recipient capability checks
- Add denial notices for non-entitled users

### Story 2.3: Message Delivery & History
- Implement message delivery on user reconnect
- Add chat history retrieval
- Ensure message persistence across sessions

---

## EPIC 3: USER MIGRATION EXECUTION

**Status**: Ready base for import exists, testing plan needed

### Story 3.1: Migration Testing & Validation
- Load test with production-scale data
- Test edge cases (special characters, old formats)
- Validate OAuth flow end-to-end under load

### Story 3.2: Rollback & Safety Plan
- Document and test rollback procedure
- Set up old system as read-only backup
- Configure monitoring and alert thresholds

### Story 3.3: Phased Migration Rollout
- Deploy 5% user migration, monitor
- Deploy 20% if stable, monitor  
- Deploy 100% if stable
- Retire old system after verification

---

## EPIC 4: COMMUNICATION & USER ACCEPTANCE

**Status**: Strategy defined, content creation pending

### Story 4.1: Pre-Launch Communication
- Draft and publish blog post series (infrastructure investment, new messaging, launch announcement)
- Brief support team before each announcement
- Monitor community sentiment after each post

### Story 4.2: Support Preparation
- Create FAQ for migration and premium features
- Define escalation protocols
- Prepare for increased ticket volume

### Story 4.3: Fallback Mechanisms
- Define fallback pricing if negative sentiment
- Prepare kill switch for paid messaging gating
- Document fast-response procedures

---

## EPIC 5: AD-FIRST MONETIZATION SETUP

**Status**: Strategy confirmed, implementation pending

### Story 5.1: Ad Network Partnerships
- Negotiate CPM deals with multiple ad networks
- Set up multi-network portfolio
- Configure ad integrations

### Story 5.2: Ad Implementation
- Port interstitial ad code to platform
- Implement tabunder technique
- Add "log in to reduce ads" messaging
- Bounce non-logged users to ad-optimized UI

### Story 5.3: SEO Implementation
- Make public content crawlable
- Implement infinite interlinking via recommendations
- Create landing pages for high-traffic keywords

### Story 5.4: Revenue Monitoring
- Set up ad revenue dashboards
- Configure subscription tracking
- Set up traffic monitoring
- Define alert thresholds

---

## EPIC 6: SUBSCRIPTION FEATURES

**Status**: Features defined, implementation pending

### Story 6.1: Premium Feature Gating
- Implement ad-free experience for premium users
- Add privacy features (private blogs, hidden activity)
- Build discovery power tools (sorting, search, impersonation)

### Story 6.2: Metered Free Tier
- Implement 10 messages/month quota
- Track and display remaining quota
- Reset quota monthly
- Show upsell messaging when exhausted

### Story 6.3: Conversion Optimization
- Streamline sign-up flow
- Implement gradual messaging paywall introduction
- Track conversion funnel metrics

---

## EPIC 7: WORDPRESS PROVISIONING & INTEGRATION

**Status**: Design complete, implementation pending

### Story 7.1: BNC User Provisioning
- Implement WordPress-to-BNC user sync
- Add provisioning triggers
- Backfill existing WordPress users

### Story 7.2: WordPress Entitlements Plugin
- Create platform entitlements plugin
- Create tenant entitlements plugin
- Integrate with WooCommerce subscriptions

### Story 7.3: Badge Rendering
- Implement entitlement badge system
- Add IRC metadata projection
- Display badges in UI

---

## NOT IN SCOPE

Based on confirmed decisions:
- ❌ **Cross-tenant messaging** (explicitly deferred)
- ❌ **Creator monetization platform** (Phase 2 consideration)
- ❌ **Ad performance A/B testing** (approach already validated)

---

## CRITICAL PATH

**Success depends on 3 factors:**
1. **Communication execution** - Blog posts, sentiment monitoring, fallback ready
2. **Migration quality** - Dev testing, phased rollout, rollback plan
3. **Ad network partnerships** - Multi-network deals, CPM negotiations

**Timeline**: Development + rollout phases as resources allow
