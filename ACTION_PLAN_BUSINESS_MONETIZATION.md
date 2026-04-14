# Action Plan: Business & Monetization Track
## Timeline: Week 0-11 (12 weeks total, parallel with developer)

**Epic:** RelayOS Premium Subscription Launch  
**Goal:** Launch $12/month RelayOS Premium IRC subscription for ISC + BDSMLR  
**Success Criteria:** $12-20K/month revenue by Month 6, 0.8-1.5% conversion, <20% churn, 96K+ MAU retained

---

## PHASE 1: Foundation (Week 0)

### Epic: Payment & Infrastructure Setup

#### Task 1.1: Payment Processor Application (BLOCKING)
- **Choose primary payment processor:**
  - **Stripe:** 2.9% + $0.30, excellent UX, 95%+ acceptance for software SaaS, robust WooCommerce integration
  - **PayPal:** 2.9% + $0.30, familiar to users, potentially easier approval for adult-adjacent platforms, strong WooCommerce support
  - **Decision criteria:** Acceptance probability, fees, checkout UX, user trust
- Register account as business entity
- Complete business verification (tax ID, bank account)
- Apply as "RelayOS - IRC Client SaaS"
- Business type: Software/SaaS subscription
- Product: Communication platform with always-on, video, file sharing
- Website: subscriptions.relayos.com (clean, professional)
- Submit application
- **Acceptance:** Application submitted, confirmation email received
- **Risk:** 5% rejection risk → If rejected, activate backup processor immediately

#### Task 1.2: Backup Payment Processor Research (CONTINGENCY)
- **If Stripe chosen:** Research PayPal as backup
- **If PayPal chosen:** Research Stripe as backup
- Research CCBill (adult-friendly, 7.5% fees, 85% checkout - last resort)
- Document application process
- Document fees and integration requirements
- Prepare application (DO NOT submit unless primary rejects)
- **Acceptance:** Backup plan documented, ready to activate if needed

#### Task 1.3: WordPress Instance Setup
- Choose domain name (e.g., subscriptions.relayos.com)
- Register domain + configure DNS
- Provision hosting (VPS or managed WordPress)
- Install WordPress 6.8+
- Configure SSL certificate
- Set up WordPress admin account
- **Acceptance:** WordPress live, accessible via HTTPS, admin can login

#### Task 1.4: Strategic Decision - Account Sync Strategy
- Review Simulation F (separate accounts) vs. Simulation G (synced accounts)
- Decision: Synced accounts recommended (2x conversion, worth +1 week)
- Document decision and rationale
- **Acceptance:** Decision documented, team aligned

**Week 0 Decision Tree:**
- 🟢 Team chooses synced → Week 10 launch, 1.2% conversion target
- 🟡 Team chooses separate → Week 9 launch, 0.6% conversion (half revenue)

---

## PHASE 2: Communication & Community (Week 1-3)

### Epic: Early Communication & Champion Activation

#### Task 2.1: Week 1 Public Announcement (CRITICAL - NON-NEGOTIABLE)
- Write blog post: "Premium IRC Coming - Support Platform + New Features"
  - Messaging: Support + Features + Premium tier (unified framing)
  - Explain WHY: Platform sustainability, better features
  - Explain WHAT: Always-on IRC, video calls, file uploads, history
  - Explain WHEN: Launching in ~9-10 weeks
  - Explain HOW: $12/month, one subscription for ISC + BDSMLR
- Publish on BDSMLR.com blog
- Publish on ISC website
- Add site banner (2 weeks): "Big news! Click to read more"
- Send IRC system message to all connected users
- Pin announcement in major IRC channels
- **Acceptance:** Announcement published, visible on both sites, IRC message sent
- **Impact:** 2x conversion multiplier (1.2% vs. 0.6% without communication)

#### Task 2.2: Identify Early Preview Champions (Week 1)
- Compile list of 150 candidates:
  - Power users (high activity, respected)
  - Channel operators (community leaders)
  - Long-time members (loyal)
  - Vocal users (will spread the word)
- Categorize by platform: ISC vs. BDSMLR
- Document contact method (IRC nick, email, PM)
- **Acceptance:** List of 150 champions ready, categorized

#### Task 2.3: Week 2-3 Early Preview Program
- Send invitations to 150 champions
- Message: "You're invited to test premium IRC features early"
- Offer: Free 2-week preview access (when ready Week 6-7)
- Survey: "Would you pay $12?" "What features most important?"
- Create feedback channel in IRC (e.g., #premium-preview)
- **Acceptance:** Invitations sent, 100+ confirmed participants, feedback channel active

#### Task 2.4: Week 2 Gate - Payment Processor Approval Check
- Check application status daily
- **If APPROVED (95% probability):**
  - ✅ Proceed with integration
  - Document approval confirmation
- **If REJECTED (5% probability):**
  - ❌ Immediately submit backup processor application (Day 1)
  - Communicate timeline impact to team (~1-2 weeks delay)
- **Acceptance:** Payment processor confirmed (primary or backup), ready for integration

---

## PHASE 3: Monetization Build (Week 4-7)

### Epic: WordPress Subscription Platform (AI Agent Track)

#### Task 3.1: WooCommerce Setup (Week 4-5)
- Install WooCommerce plugin
- Install WooCommerce Subscriptions plugin
- Configure WooCommerce settings (currency, tax, shipping disabled)
- Create product: "RelayOS Premium IRC" - $12/month subscription
- Configure subscription settings (billing cycle, renewal, cancellation)
- Set up email templates (purchase, renewal, cancellation)
- **Acceptance:** WooCommerce operational, test product created, emails configured

#### Task 3.2: Payment Processor Integration (Week 4-5)
- **If Stripe chosen:**
  - Install WooCommerce Stripe Payment Gateway plugin
  - Connect Stripe account (API keys - test mode first)
  - Configure Stripe settings (checkout flow, webhooks)
- **If PayPal chosen:**
  - Install WooCommerce PayPal Payments plugin
  - Connect PayPal business account (API credentials - sandbox first)
  - Configure PayPal settings (checkout flow, IPN/webhooks)
- Test purchase flow end-to-end (test/sandbox mode)
- Verify webhooks working (subscription.created, subscription.cancelled, payment.failed)
- **Acceptance:** Payment processor connected, test purchases successful, webhooks firing

#### Task 3.3: Subscription Status API (Week 5-6)
- Build custom REST API endpoint: `/wp-json/relayos/v1/check-subscription/{user_id}`
- API returns JSON: `{"subscribed": true/false, "plan": "premium", "expires": "2026-05-06"}`
- Add authentication (API key or WordPress session)
- Add caching (Redis, 5-10 min TTL to reduce load)
- Test API responses for various scenarios (active, expired, cancelled)
- **Acceptance:** API working, returns correct status, cached, documented

#### Task 3.4: User Account Sync (SSO) - If Synced Accounts (Week 6-7)
- Configure WordPress SSO with ISC
- Configure WordPress SSO with BDSMLR
- Test login flow: User logs into ISC → redirected to WordPress → already logged in
- Test login flow: User logs into BDSMLR → redirected to WordPress → already logged in
- Verify user ID mapping between systems
- **Acceptance:** SSO working, users seamlessly logged in, no account creation friction
- **Note:** Skip if "separate accounts" chosen (faster, but 50% lower conversion)

#### Task 3.5: Feature Gates (Anope Module or Custom Service) (Week 6-7)
- Determine where to implement feature gates:
  - Option A: Anope IRC services module (queries WordPress API)
  - Option B: Custom middleware service (sits between user and RelayOS)
- Implement subscription check before enabling premium features:
  - KiwiBNC (always-on connections)
  - Jitsi (video conferencing)
  - File/image uploads
  - Message history
- Configure free tier limitations:
  - Text only (no files/images)
  - No message history (not saved)
  - Disconnects on browser close
- Test feature gates: Free user can't upload images, premium user can
- **Acceptance:** Feature gates working, free vs. premium access enforced correctly

#### Task 3.6: Week 7 Checkpoint - Monetization Ready
- WordPress + WooCommerce + Payment Processor fully configured
- Subscription API working and tested
- SSO working (if synced accounts chosen)
- Feature gates ready for integration
- All code in version control (Git)
- Documentation complete (API docs, setup guide)
- **Acceptance:** Monetization layer ready, waiting for RelayOS (Week 8)

---

## PHASE 4: Integration & Testing (Week 9-10)

### Epic: RelayOS + Monetization Integration

#### Task 4.1: Integrate Feature Gates with RelayOS (Week 9)
- Connect Anope (or custom service) to WordPress Subscription API
- Configure API endpoint URL and authentication
- Test premium feature activation:
  - User subscribes → API returns "subscribed": true → Premium features enabled
  - User cancels → API returns "subscribed": false → Premium features disabled
- Test caching (API not called on every request, cached 5-10 min)
- **Acceptance:** Integration working, premium features activate/deactivate based on subscription

#### Task 4.2: Add "Get Premium" Buttons (Week 9)
- Design "Get Premium" button (CTA)
- Add button to chat.bdsmlr.com (visible in IRC interface or landing page)
- Add button to chat.isexychat.com (visible in IRC interface or landing page)
- Button redirects to subscriptions.relayos.com checkout
- If synced accounts: User already logged in → straight to checkout
- If separate accounts: User must create account first
- **Acceptance:** Buttons visible, clickable, redirect working

#### Task 4.3: Beta Test with 150 Champions (Week 10)
- Send beta invitations to 150 Early Preview champions
- Provide test accounts or discount codes (optional)
- Test full flow:
  - Click "Get Premium" → Redirect to WordPress → Checkout → Pay → Return to IRC → Premium features enabled
- Monitor for issues:
  - Payment failures
  - API errors
  - Feature gates not working
  - SSO issues
- Collect feedback via survey + feedback channel
- **Acceptance:** 100+ champions completed beta test, no critical bugs, feedback collected

#### Task 4.4: Bug Fixes & Polish (Week 10)
- Fix any bugs found during beta test
- Optimize checkout flow (reduce steps, improve UX)
- Fix API performance issues (if any)
- Polish UI/UX (buttons, messaging, design)
- Test edge cases (expired subscription, failed payment, cancellation)
- **Acceptance:** All critical bugs fixed, checkout flow smooth, ready for public launch

---

## PHASE 5: Launch (Week 11)

### Epic: Public Launch

#### Task 5.1: Switch Payment Processor to Live Mode
- Change API keys/credentials from test/sandbox to live mode
- Verify webhooks configured for live mode
- Test one live transaction (product owner makes purchase)
- **Acceptance:** Payment processor live, real money processing, webhooks working

#### Task 5.2: Public Launch Announcement
- Write launch blog post: "RelayOS Premium IRC is LIVE!"
  - Messaging: Thank champions, explain value, clear CTA
  - Link to checkout: subscriptions.relayos.com
  - Explain features: Always-on, video, uploads, history
  - Price: $12/month, one subscription for ISC + BDSMLR
- Publish on BDSMLR.com blog
- Publish on ISC website
- Update site banner: "Premium IRC is LIVE - Get always-on chat, video calls, and more!"
- Send IRC system message to all connected users
- Pin announcement in major IRC channels
- Email 150 champions: "Thanks for beta testing - premium is now live!"
- **Acceptance:** Launch announcement published, visible everywhere, community aware

#### Task 5.3: Daily Monitoring (Week 11+)
- Monitor payment success rate (target >95%)
- Monitor conversion rate (signups / MAU)
- Monitor API uptime (target >99%)
- Monitor support tickets (volume, type, resolution time)
- Monitor IRC for user feedback/complaints
- **Daily dashboard:** Key metrics visible, alerts configured
- **Acceptance:** Monitoring in place, team reviewing metrics daily

#### Task 5.4: Post-Launch Onboarding Flow
- After successful payment: Redirect to welcome page
- Welcome page content:
  - "You're premium! Here's how to use your new features"
  - Link to feature guide (always-on IRC setup, video calls, uploads)
  - Premium badge appears in IRC (visual status indicator)
- Send welcome email with feature guide link
- **Acceptance:** Welcome flow working, users know how to use premium features

---

## PHASE 6: Operations (Month 1-6)

### Epic: Post-Launch Operations & Optimization

#### Task 6.1: Weekly Metrics Tracking (Month 1-6)
- Track KPIs weekly:
  - Conversion rate (target: 0.8-1.5%)
  - Churn rate (target: <20%)
  - Revenue (target: $12-20K/month by Month 6)
  - MAU (target: 96-102K retained)
  - Feature usage (% using KiwiBNC, Jitsi, uploads)
  - Payment success rate (target: >95%)
- Create metrics dashboard (Google Sheets or analytics tool)
- Review metrics every Monday
- **Acceptance:** Metrics tracked weekly, trends visible, team informed

#### Task 6.2: Month 2-3 Optimization (If Needed)
- **If conversion <0.5%:**
  - Investigate: Price too high? Messaging unclear? Features not valuable?
  - Test: Adjust messaging, add feature demos, survey non-converters
- **If churn >25%:**
  - Investigate: Not using features? Poor UX? Expectations not met?
  - Test: Improve onboarding, send usage tips, survey churned users
- **If payment success <90%:**
  - Investigate: Checkout friction? Payment processor issues? Card declines?
  - Test: Simplify checkout, add alternative payment methods
- **Acceptance:** Issues identified and addressed, metrics improving

#### Task 6.3: Ongoing Management (18-22 hrs/week)
- Support tickets (respond to user questions/issues)
- Monitor payment processor for disputes/chargebacks
- Update documentation as needed
- Communicate with community (respond to feedback)
- Plan Phase 2 features (BDSMLR website perks - collections, downloads, bookmarks, ad-free)
- **Acceptance:** Business running smoothly, issues handled promptly

#### Task 6.4: Payment Processor Monitoring (Watch for Termination Signals)
- Monitor for review requests or account warnings
- **If payment processor sends termination notice (2-6% probability):**
  - Immediately apply to CCBill (adult-friendly, 98% approval)
  - Build CCBill integration (2 weeks)
  - Migrate subscribers (accept 10% churn)
  - Communicate to users transparently
- **Acceptance:** Account healthy, or CCBill migration completed successfully

---

## Success Metrics

### Week 0-2 (Foundation)
- ✅ Payment processor approved (primary or backup)
- ✅ WordPress instance live
- ✅ Account sync strategy decided

### Week 1-3 (Communication)
- ✅ Public announcement published
- ✅ 150 champions identified
- ✅ 100+ Early Preview participants confirmed

### Week 4-7 (Build)
- ✅ WooCommerce + Payment Processor operational
- ✅ Subscription API working
- ✅ SSO configured (if synced accounts)
- ✅ Feature gates ready

### Week 8 (Gate)
- ✅ RelayOS production-ready (or delay communicated)

### Week 9-10 (Integration)
- ✅ Feature gates integrated
- ✅ "Get Premium" buttons live
- ✅ Beta test completed (100+ users)
- ✅ No critical bugs

### Week 11 (Launch)
- ✅ Payment processor live mode
- ✅ Public launch announcement
- ✅ Monitoring active

### Month 1
- Target: 850 subscribers (0.8% conversion)
- Target: $10,200/month revenue
- Target: 98K+ MAU retained

### Month 6
- Target: 1,270-1,590 subscribers (1.2-1.5% conversion)
- Target: $12,000-$19,080/month revenue
- Target: 96-102K MAU retained (90-96% retention)
- Target: <20% churn
- Target: 18-22 hrs/week management

---

## Dependencies Between Tracks

| Week | Developer Track | Business Track | Dependency |
|------|----------------|----------------|------------|
| 0 | - | Payment processor application, WordPress setup | None (parallel) |
| 1-3 | RelayOS config + bug fixes | Public announcement, champions | None (parallel) |
| 4-5 | Load testing | WooCommerce + Payment Processor setup | None (parallel) |
| 6-7 | Optimization | Feature gates + SSO | None (parallel) |
| 8 | **GO/NO-GO GATE** | Monetization ready | **SYNC POINT** |
| 9 | Integration support | Feature gate integration | **BLOCKER: RelayOS must be ready** |
| 10 | Beta support | Beta test with champions | **BLOCKER: Both tracks ready** |
| 11 | Launch support | Public launch | **BLOCKER: Both tracks ready** |

---

**Status:** Ready to start Week 0  
**Next Action:** Payment processor application + WordPress setup  
**Expected Launch:** Week 11 (80% probability) or Week 15 (20% probability if RelayOS delays)
