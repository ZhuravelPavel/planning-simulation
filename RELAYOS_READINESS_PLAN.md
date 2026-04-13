# RelayOS Chat App - Production Readiness Plan
## Issues Found & Steps to Address

**Date:** April 6, 2026  
**Purpose:** Prepare RelayOS for monetized production launch  
**Timeline:** 8-9 weeks (parallel with monetization development)

---

## Overview

Based on repository analysis, RelayOS requires stabilization work before production launch. This plan outlines what needs to be done.

---

## Priority 1: CRITICAL (Must be done before launch)

### 1. Complete Configuration
**Issue:** `.env` file doesn't exist (only `.env.example`)

**What to do:**
- Copy `.env.example` to `.env`
- Fill in all production values (domains, passwords, API keys)
- Set up secrets management (TLS certs, database passwords, etc.)
- Test all services start correctly with production config

**Timeline:** Week 1-2

---

### 2. Stabilize Core Components
**Issue:** Recent commits show bugs being fixed in critical components

**Components needing stabilization:**
- **KiwiBNC** (always-on IRC bouncer) - Just marked "working" 10 days ago
- **KiwiIRC + Nginx** (web client) - Recent compatibility fixes
- **Jitsi** (video conferencing) - Just got "working config"
- **WordPress Auth** (password verification) - Just implemented correctly

**What to do:**
- Run integration tests on all components
- Fix any remaining bugs found during testing
- Verify KiwiBNC stays connected (no disconnects)
- Verify Jitsi calls work end-to-end
- Verify WordPress password auth works reliably

**Timeline:** Week 1-4

---

### 3. Production Deployment Setup
**Issue:** Only staging deployment exists (`relayos-staging`), no production

**What to do:**
- Create production Kubernetes cluster (if not using staging)
- Set up production domains (chat.isexychat.com, chat.bdsmlr.com)
- Configure production TLS certificates (Let's Encrypt via cert-manager)
- Set up production database (MariaDB with backups)
- Configure monitoring/alerting

**Timeline:** Week 2-4

---

### 4. Load Testing
**Issue:** Unknown if system handles real user load

**What to do:**
- Test with 100 concurrent IRC connections
- Test with 500 concurrent IRC connections
- Test with 50 simultaneous Jitsi video calls
- Identify bottlenecks
- Optimize or scale components as needed

**Timeline:** Week 5-6

---

## Priority 2: HIGH (Should be done before launch)

### 5. Fix BuddyBoss Theme CSS
**Issue:** "broken CSS generation" (currently patched/disabled)

**What to do:**
- Investigate root cause of broken CSS generation
- Fix properly OR replace BuddyBoss theme
- Verify WordPress admin interface works correctly

**Timeline:** Week 3-4

---

### 6. Complete OAuth Implementation
**Issue:** OAuth "not ready for prod" (only password auth works)

**What to do:**
- Finish OAuth implementation for WordPress ↔ IRC
- Test OAuth flow end-to-end
- OR: Defer to Phase 2 if password auth is sufficient

**Timeline:** Week 5-7 (optional, can defer)

---

### 7. Complete TODOs in Configuration
**Issue:** Multiple "TODO" items in configs

**TODOs found:**
- Services MOTD (currently just says "TODO")
- Some config items marked "TODO factor out"
- Chanstats config has "TODO: verify mysql instance"

**What to do:**
- Review all TODO items in codebase
- Complete or remove each one
- Write proper MOTD for IRC services
- Verify all database connections

**Timeline:** Week 3-5

---

## Priority 3: MEDIUM (Nice to have before launch)

### 8. Documentation
**Issue:** Limited user-facing documentation

**What to do:**
- Write user guide: "How to use RelayOS IRC"
- Write admin guide: "How to manage RelayOS"
- Document troubleshooting steps
- Create FAQ

**Timeline:** Week 6-8

---

### 9. Security Audit
**Issue:** No evidence of security review

**What to do:**
- Review security of all exposed ports
- Audit IRC server config (rate limits, flood protection)
- Review WordPress security settings
- Enable/configure spam protection (tarpit module exists)
- Set up fail2ban or similar

**Timeline:** Week 5-7

---

### 10. Backup & Recovery
**Issue:** No backup strategy mentioned

**What to do:**
- Set up automated database backups (MariaDB)
- Set up automated IRC data backups (InspIRCd, Anope)
- Set up WordPress backups
- Document recovery procedures
- Test restore from backup

**Timeline:** Week 6-8

---

## Priority 4: LOW (Can defer to Phase 2)

### 11. FCZ Integration
**Issue:** Several "TODO possibly integrate with FCZ" items

**What to do:**
- Clarify if FCZ (freechat.zone?) integration is needed
- If yes: implement integrations
- If no: remove TODOs

**Timeline:** Phase 2 (post-launch)

---

### 12. Mobile Apps
**Issue:** KiwiIRC is web-only (responsive but not native apps)

**What to do:**
- Build iOS app (optional)
- Build Android app (optional)
- OR: Rely on responsive web interface

**Timeline:** Phase 2 (post-launch)

---

## Testing Checklist (Before Launch)

### Functional Tests:
- [ ] User can register on WordPress
- [ ] User can log into IRC using WordPress password
- [ ] User can connect to chat.isexychat.com
- [ ] User can connect to chat.bdsmlr.com
- [ ] KiwiBNC keeps user connected (always-on works)
- [ ] Jitsi video calls work
- [ ] File uploads work
- [ ] IRC services work (NickServ, ChanServ)
- [ ] WordPress admin interface works

### Load Tests:
- [ ] 100 concurrent IRC connections (stable)
- [ ] 500 concurrent IRC connections (stable)
- [ ] 50 simultaneous Jitsi calls (stable)
- [ ] Database handles query load
- [ ] No memory leaks after 24 hours

### Security Tests:
- [ ] IRC flood protection works
- [ ] Spam detection works (tarpit)
- [ ] Rate limiting works
- [ ] TLS certificates valid
- [ ] No exposed admin ports

---

## Parallel Timeline with Monetization

**Week 1-2:** Core setup (config, domains, deployment)  
**Week 3-4:** Stabilization (fix bugs, test components)  
**Week 5-6:** Load testing and optimization  
**Week 7-8:** Final polish (docs, security, backups)  
**Week 9:** Integration with monetization layer (feature gates)  
**Week 10:** Launch (if all tests pass)

---

## Decision Points

### Week 4: Go/No-Go Decision #1
**Question:** Is RelayOS stable enough for beta testing?
- If YES → Proceed to Week 5-6 (load testing)
- If NO → Extend stabilization (delay 1-2 weeks)

### Week 8: Go/No-Go Decision #2
**Question:** Is RelayOS ready for production launch?
- If YES → Proceed to Week 9 (integration + launch)
- If NO → Identify blockers, delay launch

---

## Summary

**What RelayOS needs before monetized launch:**

**MUST HAVE (Blocking):**
1. Production config complete
2. Core components stable (no crashes/disconnects)
3. Production deployment working
4. Load tested (handles expected users)

**SHOULD HAVE (Important):**
5. BuddyBoss CSS fixed
6. All TODOs completed
7. Basic security audit done

**NICE TO HAVE (Optional):**
8. OAuth working
9. Documentation complete
10. Backup/recovery tested

---

**Estimated Timeline:** 8-9 weeks (can run parallel with monetization development)

**Risk:** If RelayOS isn't ready by Week 9, launch delays (but monetization code is ready)

---

**Next Steps:**
1. Developer reviews this plan
2. Developer confirms timeline
3. Developer identifies any additional issues
4. Agree on final launch criteria
