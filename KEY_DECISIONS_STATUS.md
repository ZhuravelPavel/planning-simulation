# Key Decisions Status

**Date:** May 14, 2026  
**Status:** Decisions made, some need discussion

---

## **Decision 1: User Import Strategy**

**Question:** 100K active users OR full 3M?

**Decision:** ✅ **Import active users only**

**Status:** ⚠️ **Needs Discussion**
- Need to define criteria for "activity"
- Options to discuss:
  - Last login in 90 days?
  - Last login in 180 days?
  - Last post/interaction in 90 days?
  - Combination of metrics?

---

## **Decision 2: Demo Network Timeline**

**Question:** Build now OR later?

**Decision:** ✅ **RelayOS as a product will be launched earlier than the features on BDSMLR**

**Implication:**
- RelayOS IRC product launches first (pure IRC SaaS)
- BDSMLR premium features come later
- This provides:
  - Clean launch with non-BDSMLR users
  - Demo network IS the actual product launch
  - Organic traffic before BDSMLR integration
  - Lower PayPal risk (diverse traffic from day 1)

**Timeline:**
- Weeks 1-4: Launch RelayOS IRC (standalone)
- Weeks 5-8: Add BDSMLR premium features integration

---

## **Decision 3: Password Strategy**

**Question:** Bridge OR force reset?

**Decision:** ⚠️ **For discussion**

**Options:**

### **Option A: Password Bridge (Recommended)**
- User enters BDSMLR password on RelayOS
- WordPress checks BDSMLR API to verify
- WordPress stores the password for future logins
- **Pros:** Best UX, seamless for users
- **Cons:** Requires BDSMLR API endpoint

### **Option B: Force Password Reset**
- All imported users get password reset email
- User must set new WordPress password
- **Pros:** Simpler implementation, no API needed
- **Cons:** Poor UX, friction, lower conversion

### **Option C: Magic Link (Alternative)**
- User enters email
- WordPress sends login link
- No password needed
- **Pros:** Modern UX, no password issues
- **Cons:** Requires email access, slight friction

**Discussion Needed:**
- Which option aligns best with technical constraints?
- Does BDSMLR API have /auth/verify endpoint ready?
- What's the priority: UX vs. implementation speed?


---

## **Questions for Next Discussion**

1. **Activity Criteria:**
   - What metrics define an "active" user?
   - Should we include users who browse but don't post?
   - What's the estimated count for each criteria option?

2. **RelayOS Standalone Launch:**
   - What's the target audience for initial launch?
   - How do we market it without mentioning BDSMLR?
   - What's the pricing for pure IRC (same $12 or different)?

3. **Password Strategy:**
   - Is BDSMLR auth API ready?
   - If building it, how long?
   - Should we start with simple option (force reset) and upgrade later?

---

**Next Steps:** Schedule discussion to resolve pending decisions
