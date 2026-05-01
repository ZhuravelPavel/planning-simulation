# Payment Processor Compliance Requirements for Adult Content Sites
**Source:** Epoch.com Adult Content Merchant Standards  
**Date:** May 1, 2026  
**Status:** ❌ BDSMLR rejected by CCBill  
**Applies to:** Visa, Mastercard, and all adult payment processors

---

## ⚠️ CRITICAL UPDATE

**CCBill Rejection:** BDSMLR was rejected by CCBill, indicating non-compliance with these standards.

**Impact:** Without CCBill (adult-friendly backup), BDSMLR cannot monetize adult website features until compliance is achieved.

---

## Requirements Overview

The questionnaire is divided into two sections:
- **Section 1:** For sites that allow user-generated content (UGC)
- **Section 2:** For ALL adult content sites

**BDSMLR Status:** Allows UGC → Must comply with BOTH sections

---

## SECTION 1: User-Generated Content Requirements

### **Requirement 1: Written Agreement with Content Providers**

**Question:** Do you have a written agreement with your content providers, including any users who upload media for the purposes of AI generation?

**Requirements:**
- Written agreement with ALL content uploaders
- Agreement must be provided upon request

**Sub-requirements:**

#### **1a. Illegal Activity Prohibition**
**Question:** Does the agreement expressly prohibit any activity that is illegal or otherwise violates the (Visa and Mastercard) standards?

**Must include:**
- Prohibition of child sexual abuse material (CSAM)
- Prohibition of non-consensual content
- Prohibition of content depicting or promoting illegal activities
- Prohibition of human trafficking/sex trafficking
- Clear consequences for violations

**BDSMLR Status:** ❌ Likely no written agreement exists

---

#### **1b. Consent Requirements**
**Question:** Does the agreement require that the content provider obtains and keeps on record written consent from all persons depicted in the content specific to the following areas?

**Required consent types:**
1. **Consent to be depicted in the content**
   - Written consent from every person in photos/videos
   - Signed release forms
   
2. **Consent to allow for the public distribution of the content**
   - Permission to upload to merchant's website
   - Understanding that content will be publicly viewable
   
3. **Consent to have the content downloaded** (if applicable)
   - If downloads are enabled, explicit consent required
   - Separate from distribution consent

**Content provider must:**
- Obtain written consent before uploading
- Keep consent records on file
- Provide consent documentation upon request

**BDSMLR Status:** ❌ No consent verification system exists

---

#### **1c. Age and Identity Verification**
**Question:** Does the agreement require the content provider to verify the identity and age of all persons depicted in content to ensure that all persons depicted are adults and to be able to provide supporting documents upon request?

**Requirements:**
- Content provider must verify age of ALL depicted persons
- Verify identity (government ID)
- Ensure all depicted persons are adults (18+ or 21+ depending on jurisdiction)
- Keep verification records
- Provide documentation upon request

**BDSMLR Status:** ❌ No age verification system for depicted persons

---

### **Requirement 2: Content Provider Verification**

**Question:** Do you only permit content uploads from verified content providers?

**Requirements:**
- Robust process for verifying age and identity of content uploaders
- Review and validate government-issued identification
- Ensure ID is in possession of and belongs to the content provider
- Prevent uploads from unverified users

**Process must include:**
1. Upload government-issued ID (passport, driver's license, national ID)
2. Verify ID is legitimate (not fake/forged)
3. Verify ID belongs to the person submitting (liveness check)
4. Verify age meets minimum requirements (18+ or 21+)
5. Store verification records securely

**BDSMLR Status:** ❌ Anyone can create account and upload without verification

---

#### **2a. Third-Party ID Verification Vendor**
**Question:** Do you use a third-party vendor that specializes in the validation of government identifications?

**Note:** Use of third-party vendor is **highly recommended**

**Recommended vendors:**
- Jumio
- Onfido
- Veriff
- Persona
- Stripe Identity
- Trulioo

**Why third-party is recommended:**
- Professional ID verification technology
- AI-powered fraud detection
- Liveness detection (prevents photo of ID)
- Compliance expertise
- Reduces liability

**BDSMLR Status:** ❌ No third-party verification in use

---

### **Requirement 3: Content Moderation Before Publication**

**Question:** Do you review all uploaded or generated content before publication to ensure that the content is not illegal and does not otherwise violate the Standards?

**Requirements:**
- Review ALL content BEFORE it goes live
- Check for:
  - Illegal content (CSAM, non-consensual, illegal acts)
  - Violations of payment card standards
  - Prohibited content (bestiality, incest, minors, etc.)
- Content sits in moderation queue until approved

**Applies to:**
- All uploaded media (photos, videos)
- Profile pictures / avatars
- Content uploaded for AI generation
- User-submitted text (if it could violate standards)

**Process:**
1. User uploads content
2. Content goes to moderation queue
3. Moderator reviews (human or AI-assisted)
4. If approved → Content published
5. If rejected → Content deleted, user notified

**BDSMLR Status:** ❌ Content published immediately without review

---

### **Requirement 4: Real-Time Live Stream Monitoring**

**Question:** If providing real-time or live video streaming services, do you fully control and allow for real-time monitoring and the removal of the content being streamed?

**Requirements:**
- Real-time monitoring capability
- Ability to immediately terminate stream
- Record of all live streams (for review if complaint filed)
- Moderators actively watching streams or AI monitoring

**BDSMLR Status:** ✅ N/A (BDSMLR does not offer live streaming)

---

## SECTION 2: Requirements for ALL Adult Content Sites

### **Requirement 5: No Marketing of Illegal Content**

**Question:** Do you make sure that the content of the website or content search terms is not marketed to give the impression that the content contains child exploitation materials or the depiction of nonconsensual activities?

**Requirements:**
- Website content must not suggest child exploitation
- Search terms must not suggest child exploitation
- Tags/categories must not suggest non-consensual activities
- Marketing materials must not create these impressions

**Prohibited examples:**
- Tags like "teen", "young", "schoolgirl" (if ambiguous)
- Tags suggesting non-consent: "forced", "unwilling", "drugged"
- Any content/tags suggesting incest
- Any content/tags suggesting minors

**BDSMLR Status:** ⚠️ Unknown - Tags are user-generated and may include prohibited terms

---

### **Requirement 6: Complaint Process**

**Question:** Do you support a complaint process that allows for the reporting of content that may be illegal or otherwise violates the Standards?

**Requirements:**
- Clear reporting mechanism (report button, email, form)
- Review all reported complaints
- Resolve complaints within **5 business days**
- Document all complaints and resolutions

**Process:**
1. User reports content
2. Complaint logged in system
3. Content reviewed by moderator
4. Decision made within 5 business days
5. Reporter notified of outcome

**BDSMLR Status:** ⚠️ Reporting exists but 5-day SLA not guaranteed

---

#### **6a. Immediate Removal of Illegal Content**
**Question:** In the event that such review yields evidence of illegal content, do you remove that content immediately?

**Requirements:**
- If review confirms content is illegal → Remove **immediately** (not within 5 days)
- Illegal content = CSAM, non-consensual, prohibited activities
- Content removed from all servers (not just hidden)
- User account may be suspended/banned
- Report to NCMEC (National Center for Missing & Exploited Children) if CSAM

**BDSMLR Status:** ⚠️ Unknown - removal process unclear

---

### **Requirement 7: Content Removal Appeals for Depicted Persons**

**Question:** Do you offer the ability for any person depicted in a video or other content to appeal to remove such content?

**Requirements:**
- Any person depicted in content can request removal
- Clear process to submit appeal
- Reasonable process to confirm identity of depicted person
- Confirm consent was obtained (or wasn't obtained)

**Process:**
1. Depicted person submits removal request
2. Verify identity of person making request
3. Review consent records
4. If consent exists and is valid → Content stays
5. If consent doesn't exist or is invalid → Content removed

**BDSMLR Status:** ⚠️ Unknown - appeal process unclear

---

#### **7a. Immediate Removal if Consent Invalid**
**Question:** If consent cannot be established, or if the person depicted in the content can demonstrate that the consent is void under applicable law, is the content removed with immediate effect?

**Requirements:**
- If consent cannot be proven → Remove immediately
- If consent is void (coerced, underage when given, etc.) → Remove immediately
- If dispute about consent validity → Use neutral third-party arbitrator
- **You pay for arbitration**, not the depicted person

**BDSMLR Status:** ❌ Likely no consent verification system to check

---

### **Requirement 8: AI-Generated Content Compliance**

**Question:** Does your website feature functionality in any way that allows for the generation of content, such as utilizing AI?

**If yes, requirements:**
- Ensure proper consent of persons being depicted (if AI generates faces/bodies based on real people)
- Disclose to consumers that content is AI-generated
- Comply with all content standards (no AI-generated CSAM, non-consensual scenarios, etc.)
- Verify age/identity of person requesting AI generation

**BDSMLR Status:** ⚠️ AI features may be planned - would need compliance

---

### **Requirement 9: No Illegal Content Attraction Policies**

**Question:** Do you have effective policies to make sure that you are not attracting users to the website by utilizing adult content that is illegal or otherwise violates the Standards?

**Requirements:**
- Written policies prohibiting illegal content
- Enforcement of policies
- No marketing using illegal content
- No homepage featuring illegal content
- No SEO targeting illegal search terms

**BDSMLR Status:** ⚠️ Policies may exist but enforcement unclear

---

### **Requirement 10: Age Verification for Visitors**

**Question:** Do you comply with: (1) all applicable laws requiring visitors of your website to be a certain age and (2) ensuring that age verification of the visitors to your website takes place before providing access to any adult content on your website?

**Requirements:**
- Verify visitor age BEFORE showing adult content
- Comply with all applicable laws:
  - US state laws (Louisiana, Utah, Virginia, Texas, etc.)
  - UK Online Safety Act
  - EU regulations
  - Other country-specific laws
- Methods vary by location
- Age gate cannot be easily bypassed

**Common methods:**
1. **Age Gate (weak):** User enters birthdate or clicks "I am 18+"
2. **Credit Card Verification (medium):** User enters credit card (no charge)
3. **Government ID Verification (strong):** User uploads ID
4. **Third-party age verification (strong):** Services like AgeChecker, Yoti, Veriff

**BDSMLR Status:** ❌ No age verification - visitors can view adult content immediately

---

### **Requirement 11: Anti-Human Trafficking Policies**

**Question:** Do you have effective policies in place that prohibit the use of its website in any way that promotes or facilitates human trafficking, sex trafficking or physical abuse?

**Requirements:**
- Written policy prohibiting:
  - Human trafficking
  - Sex trafficking
  - Physical abuse
  - Exploitation
- Policy must be enforced
- Training for moderators to identify trafficking indicators
- Reporting mechanism for suspected trafficking
- Cooperation with law enforcement

**BDSMLR Status:** ⚠️ Policy may exist but enforcement unclear

---

#### **11a. Anti-Trafficking Organization Membership**
**Question:** Do you have an active membership, or do you participate with an anti-human trafficking and/or anti-child exploitation organization?

**Requirements:**
- Active membership OR participation
- Examples of organizations:
  - **Anti-trafficking:** Polaris, Thorn, International Justice Mission
  - **Anti-child exploitation:** NCMEC, INHOPE, Internet Watch Foundation (IWF)

**Benefits:**
- Demonstrates commitment to compliance
- Access to resources and training
- Industry best practices
- Credibility with payment processors

**BDSMLR Status:** ❌ Likely no membership

---

### **Requirement 12: Payment Scheme Access**

**Question:** Upon request, are you able to provide any of the Payment Schemes that Epoch works with with temporary account credentials that allow access to the website(s) for up to seven (7) days to view all content that is behind a paywall or otherwise restricted to members of the website(s)?

**Requirements:**
- Provide temp credentials to Visa/Mastercard upon request
- Allow access to ALL paywalled content
- Access valid for up to 7 days
- No restrictions on what they can view

**Purpose:** Payment schemes audit your site to ensure compliance

**BDSMLR Status:** ✅ Technically feasible (if monetization implemented)

---

## Summary of BDSMLR Compliance Status

| Requirement | Status | Priority |
|-------------|--------|----------|
| 1. Written agreement with content providers | ❌ Not compliant | CRITICAL |
| 1a. Agreement prohibits illegal activity | ❌ Not compliant | CRITICAL |
| 1b. Agreement requires consent from depicted persons | ❌ Not compliant | CRITICAL |
| 1c. Agreement requires age/identity verification | ❌ Not compliant | CRITICAL |
| 2. Content provider verification | ❌ Not compliant | CRITICAL |
| 2a. Third-party ID verification vendor | ❌ Not compliant | CRITICAL |
| 3. Content moderation before publication | ❌ Not compliant | CRITICAL |
| 4. Real-time live stream monitoring | ✅ N/A | N/A |
| 5. No marketing of illegal content | ⚠️ Partial | HIGH |
| 6. Complaint process (5-day SLA) | ⚠️ Partial | HIGH |
| 6a. Immediate removal of illegal content | ⚠️ Unknown | HIGH |
| 7. Content removal appeals for depicted persons | ⚠️ Unknown | HIGH |
| 7a. Immediate removal if consent invalid | ❌ Not compliant | HIGH |
| 8. AI-generated content compliance | ⚠️ Future concern | MEDIUM |
| 9. No illegal content attraction policies | ⚠️ Partial | HIGH |
| 10. Age verification for visitors | ❌ Not compliant | CRITICAL |
| 11. Anti-human trafficking policies | ⚠️ Unknown | HIGH |
| 11a. Anti-trafficking organization membership | ❌ Not compliant | MEDIUM |
| 12. Payment scheme access | ✅ Feasible | LOW |

---

## Critical Gaps (Why CCBill Rejected)

**CRITICAL (Must fix before reapplying):**
1. ❌ No content provider ID verification
2. ❌ No content moderation queue (content published immediately)
3. ❌ No age verification for visitors
4. ❌ No written agreement with content providers
5. ❌ No consent verification for depicted persons

**HIGH (Should fix before reapplying):**
6. ⚠️ Complaint resolution process unclear
7. ⚠️ Content removal appeal process unclear
8. ⚠️ User-generated tags may include prohibited terms

**MEDIUM (Good to have):**
9. ❌ No anti-trafficking organization membership

---

## Estimated Compliance Timeline

**Minimum:** 6-9 months  
**Realistic:** 12-18 months  
**Cost:** $50,000 - $150,000

**Why so long?**
- Building ID verification system: 2-3 months
- Building content moderation system: 3-4 months
- Implementing age verification: 1-2 months
- Legal review and policy creation: 1-2 months
- Testing and refinement: 2-3 months
- Staff training: 1 month
- Backlog of existing content to review: 3-6 months

---

## Impact on Monetization Plan

**Current Plan (ACTION_PLAN_V2.md):**
- Week 0: Apply to payment processors ✅
- Week 2: Payment approval ❌ BLOCKED

**Reality:**
- Months 1-12: Implement compliance requirements
- Month 13: Apply to payment processors
- Month 14: Payment approval (if approved)
- Month 15-18: Build monetization features

**Revenue Target:**
- Original: Month 6 → $14-20K/month
- New: Month 20-24 → $14-20K/month (14-18 month delay)

---

## Next Steps

See `COMPLIANCE_ROADMAP.md` for detailed implementation plan.
