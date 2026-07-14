# GA4 Event Tracking Specification for BDSMLR

**Document Version:** 1.0  
**Date:** July 14, 2026  
**Purpose:** Define all GA4 events to track for the new BDSMLR subscription model

---

## **Overview**

This document specifies all Google Analytics 4 (GA4) events to implement for BDSMLR's dual-revenue model (subscriptions + ads). These events will track:
- Subscription conversion funnel
- Premium feature usage
- Free tier friction points
- Ad performance
- User engagement
- Platform cross-usage

---

## **1. CORE CONVERSION FUNNEL EVENTS**

### Subscription Journey

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `subscription_prompt_shown` | User sees upgrade prompt | `context` (messaging_quota, private_blog_post, discovery_tool_locked) | `quota_usage_percent`, `feature_attempted` |
| `subscription_cta_click` | User clicks "Subscribe" or "Upgrade" | `source` (prompt, menu, banner) | `context` |
| `platform_redirect_start` | Redirected to platform.getrelayos.com | `from_url` | - |
| `oauth_link_complete` | Successfully linked BDSMLR → relayOS account | `user_id`, `platform_user_id` | - |
| `checkout_started` | Began WooCommerce checkout | `product_sku` (relaybnc), `price` (5.00), `currency` (USD) | - |
| `payment_info_entered` | Entered card details | `payment_method` (card) | - |
| `subscription_completed` | Payment successful | `transaction_id`, `price`, `currency`, `subscription_id` | - |
| `subscription_cancelled` | User cancelled subscription | `reason` (user_initiated, payment_failed) | `days_subscribed` |
| `subscription_reactivated` | User resubscribed after cancellation | `days_since_cancellation` | - |

### Free Tier Friction Points

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `messaging_quota_warning` | Hit 75% of free quota | `quota_used`, `quota_limit` | `days_into_month` |
| `messaging_quota_exceeded` | Hit 100% of quota | `quota_limit`, `messages_attempted_over` | - |
| `private_blog_post_blocked` | Tried to post to private blog without sub | `blog_id` | `post_type` |
| `discovery_feature_blocked` | Tried to use subscriber-only discovery tool | `feature` (archive_sort, masonry, search_sort, unpixelated_search, following_feed) | `attempted_action` |

---

## **2. PREMIUM FEATURE USAGE EVENTS**

### Discovery Tools (Subscriber-Only)

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `archive_sort_used` | User changed archive sort order | `sort_type` (popular, liked, newest) | `blog_id` |
| `masonry_layout_toggled` | User toggled masonry layout | `enabled` (true, false) | `blog_id` |
| `archive_variant_filter_applied` | User filtered originals/reblogs | `filter` (originals, reblogs, all) | `blog_id` |
| `search_sort_changed` | User changed search sort order | `sort_type` (newest, popular, liked) | `query` |
| `unpixelated_search_used` | User performed deep search | `depth` (deep, medium), `query` | `result_count` |
| `following_feed_viewed` | User viewed another's following feed | `target_blog` | - |

### Messaging Features

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `offline_message_sent` | User sent offline message | `user_tier` (free, premium) | `recipient_id` |
| `offline_message_received` | User received offline message | `user_tier` (free, premium) | `sender_id` |
| `message_history_accessed` | User viewed message history | `user_tier` (free, premium) | `days_back` |

### Private Blog Features

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `private_blog_post_created` | Premium user posted to private blog | `blog_id`, `post_type` (text, photo, video) | `has_tags` |
| `private_blog_toggled` | User changed blog privacy setting | `is_private` (true, false) | `blog_id` |

---

## **3. AD PERFORMANCE EVENTS**

### Ad Tracking (Anonymous Users Only)

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `ad_impression` | Ad displayed to user | `ad_network`, `ad_unit_id`, `placement`, `user_logged_in` (true, false) | `ad_size` |
| `ad_click` | User clicked ad | `ad_network`, `ad_unit_id`, `placement` | `destination_url` |
| `ad_blocked_detected` | User has ad blocker enabled | `page_url` | `blocker_type` |
| `ad_load_failed` | Ad failed to load | `error_type`, `ad_unit_id` | `ad_network` |

**Important:** Only track ads for anonymous (not logged in) users. Logged-in free users do NOT see ads.

---

## **4. ENGAGEMENT & CONTENT EVENTS**

### Content Interaction

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `post_created` | User created a post | `content_type` (text, photo, video), `blog_privacy` (public, private) | `has_tags`, `has_media` |
| `post_viewed` | User viewed a post | `view_source` (feed, archive, search, direct) | `post_id`, `blog_id` |
| `post_reblogged` | User reblogged a post | `post_id` | `with_tags` (true, false) |
| `post_liked` | User liked a post | `post_id` | `blog_id` |
| `comment_posted` | User posted a comment | `post_id` | `comment_length` |
| `blog_followed` | User followed a blog | `blog_id` | - |
| `blog_unfollowed` | User unfollowed a blog | `blog_id` | `days_followed` |

### Search & Discovery

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `search_performed` | User performed search | `query`, `result_count`, `user_tier` (free, premium, anonymous) | `filters_applied` |
| `recommendation_clicked` | User clicked recommendation | `rec_type` (more_like_this, for_you, blogs_you_may_like) | `post_id`, `blog_id` |
| `archive_browsed` | User browsed blog archive | `blog_id` | `sort`, `layout`, `variants` |

---

## **5. MODERATION & SAFETY EVENTS**

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `content_reported` | User reported content | `report_type` (spam, abuse, illegal), `content_type` (post, comment, blog) | `content_id` |
| `user_blocked` | User blocked another user | `blocked_user_id` | - |
| `user_unblocked` | User unblocked another user | `unblocked_user_id` | `days_blocked` |
| `blog_hidden` | User hid their blog/activity | `privacy_setting` (followers_hidden, following_hidden, likes_hidden) | - |

---

## **6. USER LIFECYCLE EVENTS**

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `account_created` | New user registered | `invite_used` (true, false) | `registration_source` |
| `first_post_created` | User's first post (activation milestone) | `content_type` | `days_since_registration` |
| `verification_completed` | ID verification for uploaders | `verification_type` (photo_id, facial) | - |
| `account_linked` | Linked BDSMLR to relayOS platform | `platform_user_id` | - |
| `return_visit_day_7` | User returned after 7 days | - | `posts_created`, `interactions` |
| `return_visit_day_30` | User returned after 30 days | - | `posts_created`, `interactions` |

---

## **7. API & EXTERNAL TOOLS EVENTS**

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `api_key_generated` | Developer created API key | `user_id` | `scopes` |
| `api_request_failed` | API request error | `endpoint`, `error_code` | `user_agent` |
| `mcp_discovery_accessed` | AI agent accessed MCP discovery | `user_agent` | `tool_count` |

---

## **8. OAUTH & AUTHENTICATION EVENTS**

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `login_started` | User began login flow | `method` (oauth, legacy) | - |
| `login_completed` | User successfully logged in | `method` (oauth, legacy) | `user_tier` |
| `login_failed` | Login attempt failed | `error_type` (invalid_credentials, account_locked) | `method` |
| `oauth_consent_granted` | User approved platform account linking | - | - |
| `oauth_consent_denied` | User denied platform account linking | - | - |

---

## **9. ERROR & PERFORMANCE TRACKING**

### Errors

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `checkout_error` | Error during checkout | `error_type`, `step` (payment_info, confirmation) | `error_message` |
| `payment_failed` | Payment declined | `decline_reason` | `payment_method` |
| `feature_load_error` | Feature failed to load | `feature_name` | `error_message` |

### Performance

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `slow_page_load` | Page load exceeded threshold | `page_type`, `load_time_ms` | `page_url` |
| `media_load_failed` | Image/video failed to load | `media_type` (image, video), `media_url` | `error_code` |

---

## **10. SUPPORT & HELP**

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `support_ticket_created` | User submitted support ticket | `category` (billing, technical, abuse) | `user_tier` |
| `faq_viewed` | User viewed FAQ article | `question_id` | `search_query` |

---

## **11. PLATFORM CROSS-USAGE**

| Event Name | Description | Required Parameters | Optional Parameters |
|------------|-------------|-------------------|-------------------|
| `bb_chat_accessed` | Premium user accessed bb.chat | `user_id` | `from_bdsmlr` (true, false) |
| `multi_tenant_activity` | User active on multiple tenants | `tenants` (bdsmlr, bbchat, relayos) | `subscription_status` |

---

## **IMPLEMENTATION PRIORITY**

### **Phase 1: Launch Critical** (Implement First)
Must be live before subscription launch:

- All **Conversion Funnel Events** (Section 1)
- **Free Tier Friction Events** (Section 1)
- **Premium Feature Usage** (Section 2)
- **Ad Performance Events** (Section 3)
- Basic **Login/Auth Events** (Section 8)

### **Phase 2: Optimization** (Implement within 2 weeks of launch)
For optimization and debugging:

- **Engagement & Content Events** (Section 4)
- **Error & Performance Tracking** (Section 9)
- **Moderation Events** (Section 5)

### **Phase 3: Growth** (Implement within 1 month)
For long-term insights:

- **User Lifecycle Events** (Section 6)
- **Support Events** (Section 10)
- **API & External Tools** (Section 7)
- **Platform Cross-Usage** (Section 11)

---

## **KEY METRICS TO CALCULATE**

From these events, you can derive:

1. **Subscription Conversion Rate:**  
   `subscription_completed` / `subscription_prompt_shown` × 100

2. **Funnel Drop-off Analysis:**  
   Track each step: prompt → click → redirect → oauth → checkout → payment

3. **Free Tier Friction:**  
   % of free users hitting `messaging_quota_exceeded`  
   % attempting blocked features

4. **Premium Feature Adoption:**  
   % of premium users using each discovery tool per month

5. **Ad Revenue per User:**  
   `ad_impression` count × CPM (for anonymous users)

6. **Feature Value Validation:**  
   Correlation between premium feature usage and retention

7. **Churn Risk Indicators:**  
   Premium users who stopped using premium features

8. **Quota Calibration:**  
   Distribution of `messaging_quota_exceeded` events across user base

---

## **TECHNICAL IMPLEMENTATION NOTES**

### Standard GA4 Parameters to Always Include:
- `user_id` (when logged in)
- `session_id`
- `timestamp`
- `user_tier` (anonymous, free, premium)
- `platform` (web, mobile_web)

### User Tier Classification:
- **anonymous:** Not logged in
- **free:** Logged in, no subscription
- **premium:** Active relayOS subscription

### Privacy Considerations:
- Do NOT track PII (email, names, etc.) directly in GA4
- Use hashed `user_id` for logged-in users
- Respect cookie consent for anonymous users
- Do NOT track content of messages or posts

### Event Naming Convention:
- Use lowercase with underscores: `event_name_format`
- Be descriptive but concise
- Group related events with common prefixes where possible

---

## **TESTING CHECKLIST**

Before launch, verify:

- [ ] All Phase 1 events fire correctly in staging
- [ ] User tier parameter is accurate (anonymous/free/premium)
- [ ] Subscription funnel events fire in correct order
- [ ] Ad events only fire for anonymous users
- [ ] Premium feature events only fire for subscribers
- [ ] No PII is being tracked
- [ ] Events match this specification exactly
- [ ] GA4 debug mode shows all parameters correctly

---

## **QUESTIONS FOR DEVELOPER**

1. What GA4 measurement ID should be used?
2. Are you using gtag.js or Google Tag Manager?
3. Do we need server-side tracking for any events?
4. How will you handle user consent for anonymous visitors?
5. Timeline for Phase 1 implementation?

---

**Document Owner:** Product/Analytics Team  
**Implementation Owner:** Development Team  
**Review Date:** Upon completion of each phase
