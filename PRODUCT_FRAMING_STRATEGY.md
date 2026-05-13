# Product Framing Strategy
## Final Recommendation from Team Meeting Analysis

**Date:** May 8, 2026  
**Meeting Participants:** Allen Day, Pavel Zhuravel, Simon  
**Decision:** Strategic pivot to IRC/Chat subscription model

---

## Executive Summary

After encountering payment processor compliance barriers (specifically ID verification requirements for content upload platforms), the team has decided to reframe the product offering to focus on **private IRC server membership** rather than adult content subscriptions. This strategic positioning bypasses major compliance hurdles while maintaining the core business model.

---

## Core Product Positioning

### **Primary Framing:**
**"Subscription to a Private IRC Chat Server / Members-Only Community"**

### **What This IS:**
- Private IRC/chat server access
- Members-only community subscription
- BNC bouncer service
- Text-based social network
- Similar model to Discord server subscriptions

### **What This Is NOT (for payment processor purposes):**
- Adult content subscription platform
- Photo/video upload service
- Content hosting platform
- Media sharing service

---

## Strategic Rationale

### Why This Approach Works

1. **Compliance Simplification**
   - Text chat doesn't require ID verification
   - No photo/video upload liability
   - Users not responsible for shared links in chat
   - Lower regulatory scrutiny from payment processors

2. **Proven Business Model**
   - Discord successfully sells private server subscriptions
   - IRC bouncer services are established products
   - Community membership is a recognized value proposition

3. **Payment Processor Acceptance**
   - Removes "adult content platform" red flags
   - Standard subscription model
   - No special verification requirements
   - Lower risk classification

4. **Flexibility for Future**
   - Can add features incrementally
   - Compliance can be layered in over time
   - Existing users can be grandfathered

---

## Payment Processor Communication

### Application Description Template

**For CC Bill / Epoch / Other Processors:**

> "We operate a subscription-based private IRC chat server, providing members-only access to our community chat platform. Similar to Discord or other chat community services, users pay a monthly subscription for access to our private server infrastructure. The service is text-based communication between community members."

### What to Emphasize:
- Community/social network aspect
- Text-based chat infrastructure
- Members club model
- Similar to Discord/Slack private communities

### What to Avoid Mentioning:
- Adult content
- Photo/video uploads
- Media hosting
- Content subscriptions
- Any adult-related keywords

---

## Product Features & Boundaries

### Included in Subscription (What You're Selling):
- ✅ Access to private IRC server
- ✅ Text chat functionality
- ✅ BNC bouncer service
- ✅ Forum membership (text-based, no uploads)
- ✅ Community membership status

### NOT Included in Subscription (What You're NOT Selling):
- ❌ Photo/video upload capabilities
- ❌ Adult content access (not advertised)
- ❌ Media hosting services
- ❌ Content downloads

### Technical Implementation Note:
> *"The puzzle to solve"* - How to link access so that paid subscribers can access additional services without explicitly tying those services to the payment transaction. This is a formulation/description challenge, not a technical one.

---

## Compliance Framework (For Future Implementation)

When compliance becomes necessary, implement in layers:

### Tier 1: Basic (Immediate Implementation Possible)
- **Age Assurance:** Simple checkbox confirmation (18+)
- **Email Verification:** Required for all new registrations
- **Terms of Service:** Updated to reflect chat service

### Tier 2: Enhanced (For Payment Processor Requirements)
- **AI Age Assurance:** Face scan technology (not full ID verification)
- **Account Verification:** Additional verification steps for paid accounts

### Tier 3: Content Upload (Only for Users Who Upload)
- **ID Verification:** Required only for users who want to upload photos/videos
- **Content Moderation:** Pre-review before content goes live
- **Identity Matching:** Uploaded content must match uploader's ID

### Grandfathering Strategy:
- New compliance applies to new registrations only
- Existing 3M+ users are grandfathered
- Old content is not retroactively reviewed
- Payment processors typically don't ask about pre-existing users/content

---

## Implementation Timeline

Based on meeting discussion:

| Milestone | Timeline | Status |
|-----------|----------|--------|
| Relay stack integration complete | 2 weeks | In Progress |
| Testing phase with Rabbit | 2-4 weeks | Pending |
| Production ready | 4 weeks | Target |
| Chat subscription launch | 4+ weeks | Planning |

**Current State:** Team is integrating Simon's relay work. The technical infrastructure for launching a chat subscription product is nearly ready.

---

## Marketing & User Communication

### To Potential Subscribers:
**Messaging:**
> "Join our exclusive members-only chat community. Connect with like-minded individuals in our private server. Get access to moderated, private IRC channels and engage with our community."

**Value Propositions:**
- Private, moderated community
- Exclusive member access
- Quality discussions
- Stable, reliable chat infrastructure
- Community ownership model

### What NOT to Say in Marketing:
- Avoid adult content mentions in payment-related marketing
- Don't advertise photo/video access as primary benefit
- Keep focus on community/social aspects
- Don't position as content platform

---

## Risk Mitigation

### Potential Challenges:

1. **"If they notice someone is underage"**
   - **Risk:** Payment processor requests ID for specific user
   - **Response:** Only occurs if underage content is uploaded
   - **Mitigation:** No upload feature in paid subscription product
   
2. **Account Termination Risk**
   - **Risk:** Payment processor terminates account if compliance fails
   - **Response:** Implement content moderation for any uploads
   - **Mitigation:** Separate upload feature from paid product

3. **User Confusion**
   - **Risk:** Users don't understand what they're paying for
   - **Response:** Clear messaging about chat/community access
   - **Mitigation:** Transparent value proposition

---

## Key Decision Quotes from Meeting

### Allen Day on Framing:
> "I think it's more important to frame it as like a social network as opposed to selling clips or selling. It's more like a members club."

### On Compliance Simplification:
> "I think this is actually a much more defensible position is to sell a chat client subscription where it's just text chat... This is what they're very sensitive about is photos and videos."

### On Technical vs. Description Challenge:
> "It's not like technical. I mean if it's basically selling a chat client or selling access to a private IRC server... it's pay a subscription and join my IRC server."

### Pavel on Business Model:
> "It's a matter of formulation, the description of the business model."

---

## Alternative Approaches Discussed (But Deprioritized)

### Crypto Payments
- **Status:** Possible fallback option
- **Tools:** BTC Pay Server, stablecoin payments
- **Issue:** Does NOT eliminate compliance requirements
- **Conclusion:** May implement eventually, but doesn't solve core problem

### Split Service Model
- **Concept:** Sell chat subscription, "secretly" grant access to content site
- **Status:** This is the approach being adopted
- **Implementation:** Technical linking without explicit marketing connection

---

## Action Items

### Pavel's Next Steps:
1. ✅ Review previous planning documents
2. ⏳ Adapt monetization plan to chat-first model
3. ⏳ Update CC Bill application with new framing
4. ⏳ Continue Epoch application process

### Technical Team:
1. ⏳ Complete relay stack integration (Allen, 2 weeks)
2. ⏳ Begin testing phase (4 weeks)
3. ⏳ Implement basic age assurance (checkbox)
4. ⏳ Set up email verification system

### Future Planning:
1. ⏳ Design subscription tiers for chat service
2. ⏳ Create marketing materials for chat community
3. ⏳ Plan user migration/messaging strategy
4. ⏳ Design access linking system (technical puzzle)

---

## Success Metrics

### Short-term (Next 30 days):
- Complete payment processor application with new framing
- Get relay stack into production
- Design subscription offering

### Medium-term (60-90 days):
- Launch chat subscription product
- First paying subscribers
- Validate payment processor acceptance

### Long-term:
- Scale subscriber base
- Add compliance layers as needed
- Optimize conversion funnel

---

## Additional Context: Revenue Update

**Positive News from Meeting:**
- React Ads revenue has doubled thanks to Simon's additional tab-unders on IRC chat
- Invoice sent: ~$15K
- First full 30-day measurement coming within this week or later this month
- This provides breathing room while subscription model is being implemented

---

## Conclusion

The strategic reframing from "adult content subscription" to "private IRC server membership" represents a **formulation change, not a technical change**. By positioning the product as chat infrastructure rather than content infrastructure, the team can:

1. Bypass major compliance barriers
2. Get payment processor approval
3. Launch subscription service within ~4 weeks
4. Layer in additional features and compliance over time
5. Maintain the core business model while managing regulatory risk

**The key insight:** Payment processors care about what you say you're selling, not necessarily what technical features your platform has. Frame it as chat/community, and the path becomes much clearer.

---

*Document prepared from meeting transcript analysis*  
*Last updated: May 8, 2026*
