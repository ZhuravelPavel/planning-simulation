# BDSMLR API Routes: Free vs. Paid Feature Mapping
**Version:** 1.0  
**Date:** April 27, 2026  
**Audience:** Manager / Product Team  
**Purpose:** Show how existing and new API routes map to monetization strategy

---

## Executive Summary

Based on the `api v2 routes - Sheet1.csv` file, this document maps all BDSMLR API routes to the free/paid feature split for **Product B: BDSMLR Premium ($10/month)**.

**Key Findings:**
1. ✅ **Generic recommender already exists** - `/for/you` and `/for/:blogname` routes are live
2. ✅ **Advanced search already built** - Just needs premium gating
3. ⚠️ **Premium features need NEW routes** - Collections, downloads, bookmarks require new endpoints
4. ⚠️ **Bug fixes required** - Privacy/social routes marked TODO (HIGH priority)

---

## Route Classification

### 🟢 FREE Routes (All Users)

**Core Discovery & Browsing:**
| Route | Description | Status |
|-------|-------------|--------|
| `GET /` | Home feed | ✅ Live |
| `GET /search?q=query` | Basic search (keyword only) | ✅ Live |
| `GET /search?q=query&sort=newest` | Search by newest | ✅ Live |
| `GET /search?q=query&sort=oldest` | Search by oldest | ✅ Live |
| `GET /for/you` | **Personalized recommendations (Filter 2: viewer interests)** | ✅ Live (api-dev) |
| `GET /for/:blogname` | **Blog-specific recommendations (Filter 1: blog interests)** | ✅ Live (api-dev) |
| `GET /feed/for/you` | Your following feed | ✅ Live |
| `GET /feed/for/:blogname` | Blog's feed | ✅ Live |
| `GET /follower-feed/you` | Follower activity feed | ✅ Live |
| `GET /archive/you` | Your archive | ✅ Live |
| `GET /archive/:blogname` | Blog's archive | ✅ Live |
| `GET /post/:postId` | Post details | ✅ Live |
| `GET /post/:postId/related` | Related posts (basic) | ✅ Live |

**User Management:**
| Route | Description | Status |
|-------|-------------|--------|
| `GET /settings/you` | User settings | ⚠️ TODO (privacy bugs) |
| `GET /settings/:blogname` | Blog settings | ⚠️ TODO (privacy bugs) |
| `GET /social/you/followers` | Your followers | ⚠️ TODO (privacy bugs) |
| `GET /social/you/following` | Who you follow | ⚠️ TODO (privacy bugs) |
| `GET /social/:blogname/followers` | Blog's followers | ⚠️ TODO (privacy bugs) |
| `GET /social/:blogname/following` | Blog's following | ⚠️ TODO (privacy bugs) |
| `GET /activity/you` | Your activity | ✅ Live |
| `GET /activity/:blogname` | Blog's activity | ✅ Live |

**FREE Tier Limits:**
- Search: Last 90 days, max 50 results
- Archive: Last 90 days
- No collections, downloads, or bookmarks

---

### 💰 PAID Routes (Premium Only)

#### **Advanced Search (Existing Routes - Need Gating)**
| Route | Description | Status |
|-------|-------------|--------|
| `GET /search?q=query&sort=popular` | Sort by popularity | ✅ Live (needs premium gate) |
| `GET /search?q=query&sort=liked` | Sort by most liked | ✅ Live (needs premium gate) |
| `GET /search?q=query&sort=reblogged` | Sort by most reblogged | ✅ Live (needs premium gate) |
| `GET /search?q=query&sort=commented` | Sort by most commented | ✅ Live (needs premium gate) |
| `GET /search?q=query&sort=unpopular` | Sort by unpopular | ✅ Live (needs premium gate) |
| `GET /search/for/you?q=query` | Search boosted for you | ✅ Live (needs premium gate) |
| `GET /search/for/:blogname?q=query` | Search boosted for blog | ✅ Live (needs premium gate) |

**Premium Search Features:**
- Full history (all time, not just 90 days)
- Unlimited results (vs 50 for free)
- Advanced sorting options

---

#### **Personalized Recommendations (Existing Routes - Premium Upgrade)**
| Route | Description | Status |
|-------|-------------|--------|
| `GET /post/:postId/related/for/you` | Related posts, personalized for viewer | ✅ Live (could be premium) |
| `GET /post/:postId/related/for/:blogname` | Related posts, personalized for blog | ✅ Live (could be premium) |

**Decision Needed:** Should personalized recommendations be FREE or PAID?
- **FREE:** Helps with engagement, drives conversions
- **PAID:** Premium feature for power users

**Recommendation:** Keep FREE. These are the "generic recommender" feature for the Munch post.

---

#### **Collections (New Routes - Need to Build)**
| Route | Description | Status |
|-------|-------------|--------|
| `GET /collections` | List user's collections | ❌ Not built |
| `GET /collections/:id` | Get collection details | ❌ Not built |
| `POST /collections` | Create new collection | ❌ Not built |
| `PATCH /collections/:id` | Update collection | ❌ Not built |
| `DELETE /collections/:id` | Delete collection | ❌ Not built |
| `POST /collections/:id/posts` | Add post to collection | ❌ Not built |
| `DELETE /collections/:id/posts/:postId` | Remove post from collection | ❌ Not built |

**Priority:** HIGH (Week 10-12)  
**Spec:** See `PREMIUM_API_ROUTES_SPEC.md`

---

#### **Downloads (New Routes - Need to Build)**
| Route | Description | Status |
|-------|-------------|--------|
| `GET /downloads` | List download history | ❌ Not built |
| `POST /downloads` | Download post (get download URL) | ❌ Not built |
| `DELETE /downloads/:postId` | Remove from download history | ❌ Not built |

**Priority:** HIGH (Week 10-12)  
**Spec:** See `PREMIUM_API_ROUTES_SPEC.md`

---

#### **Bookmarks (New Routes - Need to Build)**
| Route | Description | Status |
|-------|-------------|--------|
| `GET /bookmarks` | List bookmarks | ❌ Not built |
| `GET /bookmarks/:postId` | Check if post is bookmarked | ❌ Not built |
| `POST /bookmarks` | Add bookmark | ❌ Not built |
| `DELETE /bookmarks/:postId` | Remove bookmark | ❌ Not built |

**Priority:** HIGH (Week 10-12)  
**Spec:** See `PREMIUM_API_ROUTES_SPEC.md`

---

#### **Ad-Free Experience (No API Routes)**
**Implementation:** Client-side check

```javascript
if (user.subscription.capabilities.includes('ad_free')) {
  // Don't render ads
}
```

**Priority:** HIGH (Week 10-12)  
**Dependency:** `/subscription/status` endpoint (NEW - needs to be built)

---

### 🔐 Subscription Management (New Routes - Need to Build)
| Route | Description | Status |
|-------|-------------|--------|
| `GET /subscription/status` | Check if user has premium | ❌ Not built (CRITICAL) |

**This is the MOST CRITICAL route** - everything else depends on it.

**Response:**
```json
{
  "subscription": {
    "active": true,
    "plan": "bdsmlr_premium",
    "capabilities": [
      "collections",
      "downloads",
      "bookmarks",
      "ad_free",
      "search_advanced"
    ]
  }
}
```

**Priority:** HIGHEST (Week 5-6)  
**Dependency:** WordPress subscription API integration

---

## Implementation Roadmap

### **Week 1-4: Bug Fixes (HIGH Priority)**
**Fix broken FREE routes:**
- ✅ `/settings/you` - Respect privacy settings
- ✅ `/social/you/followers` - Respect hidden followers
- ✅ `/social/you/following` - Respect hidden following
- ✅ `/post/:postId` - Don't serve deleted posts
- ✅ `/search` - Fix tag search bugs

**Owner:** Developer  
**Impact:** Critical for trust/GDPR compliance

---

### **Week 5-6: Subscription Infrastructure**
**Build premium check:**
- ❌ `GET /subscription/status` - NEW endpoint
- ❌ WordPress integration - Check WooCommerce subscription status
- ❌ Capability mapping - WordPress roles → API capabilities

**Owner:** Developer + Product Owner  
**Impact:** Blocks all premium features

---

### **Week 10-12: Premium Features**
**Gate existing routes:**
- ✅ Advanced search sorts (popular, liked, reblogged, commented)
- ✅ Unlimited search results
- ✅ Full archive history

**Build new routes:**
- ❌ Collections (7 routes)
- ❌ Downloads (3 routes)
- ❌ Bookmarks (4 routes)

**Frontend:**
- ❌ React components for collections UI
- ❌ Download button UI
- ❌ Bookmark button UI
- ❌ "Upgrade to Premium" prompts
- ❌ Ad-free experience (hide ad components)

**Owner:** Developer + Product Owner  
**Impact:** Product B (BDSMLR Premium) launch ready

---

## Revenue Impact by Route Category

### **Advanced Search (Existing Routes)**
**Development Cost:** Low (just add premium gates)  
**Revenue Potential:** Medium  
**User Value:** High (power users want advanced filters)

**Conversion Driver:**
- Free users see "🔒 Premium" badges on advanced sort options
- Click to upgrade → Stripe/PayPal checkout

---

### **Collections (New Routes)**
**Development Cost:** High (7 new routes + database tables)  
**Revenue Potential:** High  
**User Value:** Very High (most requested feature)

**Conversion Driver:**
- Free users see "Save to Collection" button → "Upgrade to Premium" prompt
- Power users (creators) will pay for organization tools

---

### **Downloads (New Routes)**
**Development Cost:** Medium (3 new routes + file serving)  
**Revenue Potential:** Medium  
**User Value:** High (convenient for archiving)

**Conversion Driver:**
- Free users see "Download" button → "Upgrade to Premium" prompt
- Users who want offline access will convert

---

### **Bookmarks (New Routes)**
**Development Cost:** Low (4 simple routes)  
**Revenue Potential:** Low (less critical than collections)  
**User Value:** Medium (convenience feature)

**Conversion Driver:**
- "Quick save for later" - casual users may not need this enough to pay
- Could be bundled perk rather than main driver

---

## Free vs. Paid Feature Matrix

| Feature | FREE | PAID (Premium $10/mo) |
|---------|------|----------------------|
| **Search** | Keyword + tags, last 90 days, 50 results, basic sorts (newest/oldest) | + Advanced sorts (popular, liked, reblogged), unlimited results, full history, personalized boosting |
| **Archive** | Last 90 days | Full history (all time) |
| **Recommendations** | Basic "related posts" | + Personalized (for you & for blog) |
| **Organization** | None | Collections (unlimited), bookmarks |
| **Downloads** | None | Download posts (images/videos) |
| **Experience** | Ads | Ad-free |
| **Support Priority** | Standard | Priority support (if offered) |

---

## Generic Recommender: FREE Feature (For Munch Post)

**Routes ALREADY LIVE (api-dev):**
- `GET /for/you` - Personalized feed (viewer interests)
- `GET /for/:blogname` - Blog-specific feed (blog interests)
- `GET /post/:postId/related/for/you` - Related posts (viewer interests)
- `GET /post/:postId/related/for/:blogname` - Related posts (blog interests)

**Announcement Text (for Munch Post):**
> **Better Recommendations Coming Soon**
> 
> We're rolling out a new recommendation system that:
> 1. Matches the style of the blog you're viewing
> 2. Matches your personal interests based on what you like
> 
> No more irrelevant "More like this" suggestions! This is a **FREE** platform improvement for all users.
> 
> Routes: `/for/you`, `/for/:blogname`, `/post/:postId/related/for/you`

**Decision:** Should these be FREE or PAID?

**Recommendation:** **FREE** (all users)
- Drives engagement (more time on site)
- Improves user experience (less frustration)
- Helps free users discover content they'll want to save (drives premium conversions)
- Competitive advantage (Tumblr doesn't have this)

---

## Questions & Decisions Needed

### 1. Personalized Recommendations: FREE or PAID?
**Options:**
- **A) FREE:** `/for/you`, `/for/:blogname`, `/post/:postId/related/for/you` (all users)
- **B) PAID:** Only basic `/post/:postId/related`, personalized versions require premium

**Current Status:** Routes exist on api-dev, no premium gate implemented

**Recommendation:** FREE (see rationale above)

**Decision:** _________

---

### 2. Search History: How Far Back for FREE?
**Options:**
- **A) Last 30 days** (aggressive conversion driver)
- **B) Last 90 days** (balanced)
- **C) Last 180 days** (generous)

**Recommendation:** 90 days (balanced between user value and conversion driver)

**Decision:** _________

---

### 3. Collections Limit for FREE?
**Options:**
- **A) 0 collections** (hard paywall)
- **B) 1 collection, 25 posts max** (freemium)
- **C) 3 collections, 50 posts max** (generous freemium)

**Recommendation:** 0 collections (hard paywall) - it's a clear premium feature

**Decision:** _________

---

### 4. Bookmarks Limit for FREE?
**Options:**
- **A) 0 bookmarks** (hard paywall, bundle with collections)
- **B) 10 bookmarks** (taste test)
- **C) Unlimited bookmarks** (free feature)

**Recommendation:** 10 bookmarks (taste test) - drives collection conversions

**Decision:** _________

---

### 5. Social Routes Privacy: HIGH or MEDIUM Priority?
**Context:** Routes marked TODO in CSV, related to TheMunch feedback #7 (privacy regression)

**Options:**
- **A) HIGH (Week 1-4):** Fix before building premium features
- **B) MEDIUM (Week 5-8):** Fix alongside ISC integration

**Recommendation:** HIGH (Week 1-4) - GDPR compliance issue

**Decision:** _________

---

## Next Steps

1. **Manager Reviews & Approves:**
   - Free/paid route split
   - Decisions on questions above
   - Generic recommender positioning (FREE)

2. **Product Owner:**
   - Finalize `PREMIUM_API_ROUTES_SPEC.md`
   - Share with developer for review
   - Create Jira tickets for Week 10-12

3. **Developer:**
   - Review technical spec
   - Estimate effort for new routes (collections, downloads, bookmarks)
   - Confirm Week 10-12 timeline is realistic

4. **Manager:**
   - Write Munch post announcing generic recommender (FREE)
   - Communicate premium features coming in ~8 weeks

---

**Status:** Awaiting manager decisions on open questions  
**Timeline:** Week 10-12 for premium route implementation  
**Risk:** Medium (new routes, WordPress integration complexity)
