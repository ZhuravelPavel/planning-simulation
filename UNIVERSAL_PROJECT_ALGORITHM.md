# Universal Project Planning Algorithm
## Battle-Tested on BDSMLR Monetization → 70:1 ROI

---

## Core Principle

> **Think before you build. Optimize before you code. Ship what works.**

The single biggest waste in software projects is implementing a plan that was never stress-tested. This algorithm forces you to find and fix problems *before* they cost you real time and money.

---

## The Algorithm at a Glance

```
PHASE 1 → Capture        (30 min)   What are we building?
PHASE 2 → Design         (60 min)   How do we build it?
PHASE 3 → Stress-Test    (45 min)   What's wrong with this plan?
PHASE 4 → Optimize       (60 min)   Rewrite with improvements
PHASE 5 → Operationalize (30 min)   Make it executable
PHASE 6 → Execute        (ongoing)  Build with AI assistance
PHASE 7 → Ship           (1 week)   Test, deploy, monitor
```

**Total planning time**: ~4 hours
**Typical savings**: 30-50% less implementation time

---

# PHASE 1: Capture
## "What exactly are we building?"
**Time**: 30 minutes

### Steps:

**1.1 Write the one-sentence problem statement**
```
[WHO] needs [WHAT] so they can [WHY]
```
Example: "Adult content creators need a monetization system so they can earn revenue from their audience."

**1.2 List all features (brain dump)**
- Write everything, don't filter yet
- Group into: Must Have / Should Have / Nice to Have

**1.3 Identify hard constraints**
Ask these questions:
- Who is building this? (solo, small team, large team)
- What's the budget ceiling?
- What's the deadline?
- What tech stack must be used (or avoided)?
- Are there compliance/legal requirements?

**1.4 Define "done"**
What does success look like in 3 months? In 1 year?
Write 3-5 measurable success criteria.

**1.5 List what you don't know**
Assumptions that need to be validated. These become your highest-risk items.

### Output:
- ✅ Problem statement (1 sentence)
- ✅ Feature list (Must/Should/Nice)
- ✅ Constraints document
- ✅ Success criteria
- ✅ Assumptions & unknowns list

---

# PHASE 2: Design
## "How do we build it?"
**Time**: 60 minutes | **Use AI heavily here**

### Steps:

**2.1 Sketch the architecture**
- What are the main components?
- How do they connect?
- What external services are needed?

**2.2 Design the data model**
- What entities exist?
- What are the relationships?
- What data needs to be stored?

**2.3 Define the API surface**
- What are the main endpoints/operations?
- Who calls what?
- What are the inputs/outputs?

**2.4 Map out user flows**
- Walk through each key user journey
- Identify every step and decision point

**2.5 Create rough estimates**
- How long will each feature take?
- What are the dependencies?
- What can be built in parallel?

**2.6 Identify risks**
- Technical risks (new technology, integrations)
- Business risks (market, compliance, competition)
- Resource risks (skills gap, capacity)

### AI Prompt Template:
```
Create a detailed technical implementation plan for [PROJECT]:

Requirements:
- [Feature 1]
- [Feature 2]
- [Constraint 1]

Include:
1. Database schema (tables, relationships, indexes)
2. API design (endpoints, request/response)
3. Architecture (components, services, integrations)
4. Implementation phases with time estimates
5. Risks and mitigations

Tech stack: [Your stack]
Team size: [Your team]
```

### Output:
- ✅ Architecture diagram (even rough text diagram)
- ✅ Data model
- ✅ API list
- ✅ User flow maps
- ✅ Timeline estimate
- ✅ Risk register

---

# PHASE 3: Stress-Test
## "What's wrong with this plan?"
**Time**: 45 minutes | **Most valuable phase**

This is the phase most teams skip. Don't skip it.

### The Stress-Test Framework

Walk through your plan and rate each section on:

```
For each component, ask:
1. COMPLEXITY   - Is this overbuilt for the problem?
2. REDUNDANCY   - Does something similar exist already?
3. TECH CHOICE  - Is this the right tool?
4. RISK         - What's the worst case if this fails?
5. ROI          - Does the effort match the value delivered?
```

### Grade Your Plan (A-F Scale):

| Grade | Score | Meaning |
|-------|-------|---------|
| A | 85-100 | Minor tweaks only, proceed |
| B | 70-84 | Some optimization possible |
| C | 55-69 | Significant issues, rewrite |
| D | 40-54 | Major problems, rethink |
| F | < 40 | Start over |

**If B or below → proceed to Phase 4**
**If A → skip Phase 4, go to Phase 5**

### Common Issues to Look For:

**Database:**
- [ ] Duplicate tables for the same concept?
- [ ] Wrong database type (SQL vs NoSQL)?
- [ ] Missing indexes on queried columns?
- [ ] No soft delete / audit trail?

**Code Architecture:**
- [ ] Same logic duplicated in multiple places?
- [ ] God objects (one class doing everything)?
- [ ] Tight coupling between unrelated modules?
- [ ] Missing abstraction layers?

**Integrations:**
- [ ] Building something a paid service already does?
- [ ] Relying on unreliable third-party APIs?
- [ ] No fallback if external service is down?

**UX/Product:**
- [ ] Friction where users need to be fast?
- [ ] Hard blocks where soft nudges would work better?
- [ ] Missing onboarding / empty state handling?

**Costs:**
- [ ] Expensive infrastructure for low traffic?
- [ ] Metered APIs without usage caps?
- [ ] No caching layer for repeated expensive operations?

### AI Prompt Template:
```
Review this implementation plan as an experienced senior engineer.
Find every problem, inefficiency, and risk.

[Paste your plan]

For each issue found, provide:
- Severity: Critical / High / Medium / Low
- The problem (specific, not vague)
- The solution (concrete, actionable)
- Impact: time saved / cost reduced / risk eliminated

Then grade the overall plan A-F and explain why.
```

### Output:
- ✅ Issues list (categorized by severity)
- ✅ Baseline grade (A-F)
- ✅ Proposed solutions
- ✅ Decision: optimize or proceed?

---

# PHASE 4: Optimize
## "Rewrite it better"
**Time**: 60 minutes | **Only if Phase 3 grade < A**

### Decision Gate:

```
Potential improvement > 20%?
    YES → Rewrite (Phase 4)
    NO  → Proceed (Phase 5)
```

Measure improvement across:
- Timeline (weeks saved)
- Cost ($ saved)
- Complexity (story points reduced)
- Risk (critical risks eliminated)

### Steps:

**4.1 Prioritize optimizations**
Sort by: Impact × Ease of implementation
Attack Critical issues first, then High, then Medium.

**4.2 Rewrite the plan**
Don't patch the old plan. Start fresh with optimizations baked in.
Keep all features. Just implement them better.

**4.3 Recalculate estimates**
New timeline, new cost, new complexity.
Document the before/after delta.

**4.4 Verify nothing was lost**
Check every feature from Phase 1 is still covered.
A simpler plan should not mean fewer features.

**4.5 Re-grade**
Apply the Phase 3 framework again.
Target: A grade (85+).

### AI Prompt Template:
```
Rewrite [PLAN NAME] incorporating these optimizations:
[List from Phase 3]

Rules:
- Keep ALL original features
- Apply every optimization
- Simplify wherever possible
- Use the best tool for each job

Show the before/after improvement for:
- Timeline
- Estimated cost
- Complexity (story points)
- Number of critical risks
```

### Output:
- ✅ Optimized plan (full rewrite)
- ✅ Revised estimates
- ✅ Before/after improvement table
- ✅ New grade (target: A)

---

# PHASE 5: Operationalize
## "Make it executable"
**Time**: 30 minutes

Turn plans into actionable work items.

### Steps:

**5.1 Break into Epics**
Group features into logical milestones (3-7 epics).
Each epic should be independently deliverable.

**5.2 Break Epics into Tasks**
3-8 tasks per epic.
Each task = one focused area of work (e.g., "Database setup", "Auth API").

**5.3 Break Tasks into Subtasks**
3-8 subtasks per task.
Each subtask = one specific, completable action.
Rule: If you can't complete a subtask in one session, break it down further.

**5.4 Assign story points**
Use Fibonacci scale: 1, 2, 3, 5, 8, 13
- 1-2 SP: Simple, well-understood (< 4 hours)
- 3-5 SP: Moderate, some unknowns (4-16 hours)
- 8-13 SP: Complex, many unknowns (> 16 hours)
If a task is 13+ SP, break it down.

**5.5 Define dependencies**
Which tasks must complete before others can start?
Draw a simple dependency chain.

**5.6 Set priorities**
- P0: System doesn't work without this
- P1: Major feature, high user value
- P2: Nice to have, can defer
- P3: Future consideration

**5.7 Create the implementation guide**
Write the first 3 AI prompts someone needs to start coding.
This is the bridge from planning to execution.

### Output:
- ✅ Epics list
- ✅ Tasks with story points and priorities
- ✅ Subtasks
- ✅ Dependency map
- ✅ Implementation guide (first prompts)

---

# PHASE 6: Execute
## "Build it with AI"
**Time**: Ongoing (implementation phase)

### The 3-Step AI Development Cycle:

```
┌─────────────────────────────────────┐
│                                     │
│   PROMPT → REVIEW → TEST → REPEAT  │
│                                     │
└─────────────────────────────────────┘
```

**Step 1: PROMPT**
Give AI one task at a time. Be specific.
```
Implement [SPECIFIC TASK] for [PROJECT].

Context:
- Tech stack: [stack]
- Database schema: [relevant tables]
- Related code: [existing code]

Requirements:
- [Specific requirement 1]
- [Specific requirement 2]

Do NOT implement anything outside this scope.
```

**Step 2: REVIEW**
Before accepting AI output, check:
- [ ] Does it solve exactly what was asked?
- [ ] Are there edge cases not handled?
- [ ] Is error handling present?
- [ ] Does it introduce unnecessary complexity?
- [ ] Does it follow existing patterns in the codebase?

**Step 3: TEST**
- Run the code
- Test happy path
- Test error path
- Test edge cases
- Commit only when tests pass

### Common AI Development Pitfalls:

| Pitfall | Fix |
|---------|-----|
| AI generates too much code | Scope prompts tighter |
| AI ignores existing patterns | Include more context |
| AI uses wrong tech | State tech stack explicitly |
| AI skips error handling | Ask for it explicitly |
| AI makes untested assumptions | Ask AI to list assumptions |

### Velocity Expectations (AI-assisted):
- Simple CRUD endpoint: 30-60 min
- Complex service with tests: 2-4 hours
- Database migration + service: 3-6 hours
- Full feature (DB + API + frontend): 1-2 days

### Output:
- ✅ Working code, committed to git
- ✅ Tests passing
- ✅ Each task moves to "Done" in Jira

---

# PHASE 7: Ship
## "Test, deploy, monitor"
**Time**: 1 week per major release

### Pre-Launch Checklist:

**Security**
- [ ] All inputs validated
- [ ] Authentication on all protected endpoints
- [ ] No secrets in code (use env vars)
- [ ] SQL injection prevention
- [ ] Rate limiting on public APIs

**Testing**
- [ ] Unit tests for critical business logic
- [ ] Integration tests for API endpoints
- [ ] Manual end-to-end test of all user flows
- [ ] Load test if expecting high traffic

**Infrastructure**
- [ ] Production environment configured
- [ ] Database backups scheduled
- [ ] Error monitoring set up (Sentry/etc.)
- [ ] Uptime monitoring configured
- [ ] Logs aggregated and searchable

**Rollout Strategy**
```
Step 1: Deploy to staging → test
Step 2: Release to 5-10% of users → monitor 24h
Step 3: Release to 50% → monitor 24h
Step 4: Release to 100%
Step 5: Monitor KPIs for 1 week
```

**Rollback Plan**
Always have an answer to: "If this breaks, how do we revert in under 10 minutes?"

### Post-Launch Monitoring (First 48 hours):
- Error rate (target: < 0.1%)
- Response times (target: < 500ms p95)
- Payment success rate (target: > 98%)
- Any alerts firing?

### Output:
- ✅ Deployed to production
- ✅ Monitoring in place
- ✅ No critical errors in first 48 hours
- ✅ KPIs trending correctly

---

# Quality Gates

These are checkpoints you must pass before moving to the next phase.
**Do not skip them.** They exist to catch problems early when they're cheap to fix.

```
After Phase 1: Can I describe what we're building in 2 sentences?
               YES → continue | NO → back to Phase 1

After Phase 2: Does the plan cover every requirement from Phase 1?
               YES → continue | NO → back to Phase 2

After Phase 3: Is the plan grade A? Or are we OK with the tradeoffs?
               YES → continue | NO → back to Phase 4

After Phase 4: Is the improvement > 20%? Did we keep all features?
               YES → continue | NO → redo Phase 4

After Phase 5: Is every Epic/Task/Subtask clear enough to act on?
               YES → continue | NO → back to Phase 5

After Phase 6: Do all tests pass? Is the code reviewed?
               YES → continue | NO → back to Phase 6

After Phase 7: Are KPIs healthy? No critical errors?
               YES → done | NO → hotfix or rollback
```

---

# Universal Templates

## Template 1: Problem Statement
```
PROJECT: [Name]
PROBLEM: [Who] needs [what] so they can [why]
SUCCESS: [Measurable outcome in 6 months]
CONSTRAINTS:
  - Team: [size/type]
  - Budget: [range]
  - Deadline: [date]
  - Tech: [required/forbidden]
  - Legal: [any compliance requirements]
ASSUMPTIONS:
  - [Assumption 1 — needs validation]
  - [Assumption 2 — needs validation]
```

## Template 2: Feature Prioritization
```
MUST HAVE (P0 - system doesn't work without these):
  - [Feature]

SHOULD HAVE (P1 - major value, high priority):
  - [Feature]

NICE TO HAVE (P2 - defer if behind):
  - [Feature]

FUTURE (P3 - not this release):
  - [Feature]
```

## Template 3: Risk Register
```
| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| [Risk 1] | High | Medium | [How to prevent/handle] |
```

## Template 4: Before/After Optimization Table
```
| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| Timeline | X weeks | Y weeks | Z% faster |
| Upfront cost | $X | $Y | Z% cheaper |
| Story points | X SP | Y SP | Z% simpler |
| Critical risks | X | Y | Z eliminated |
| Projected ROI | X% | Y% | +Z% |
```

## Template 5: Sprint Planning
```
SPRINT [N] — [Date range]
Goal: [One sentence goal]
Committed:
  - [Task] (X SP)
  - [Task] (X SP)
Total: X SP
Carried over: [From previous sprint]
Blockers: [Known blockers]
```

---

# The Algorithm in One Page

```
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  1. CAPTURE (30 min)                                     │
│     → Problem statement, features, constraints           │
│                                                          │
│  2. DESIGN (60 min)                                      │
│     → Architecture, data model, API, estimates           │
│                                                          │
│  3. STRESS-TEST (45 min) ← NEVER SKIP THIS              │
│     → Grade plan A-F, find all problems                  │
│     → Grade A? Skip step 4.                             │
│                                                          │
│  4. OPTIMIZE (60 min)                                    │
│     → Rewrite with fixes, recalculate estimates          │
│     → Improvement > 20%? Worth it.                      │
│                                                          │
│  5. OPERATIONALIZE (30 min)                              │
│     → Epics → Tasks → Subtasks → Story Points            │
│     → Push to Jira                                       │
│                                                          │
│  6. EXECUTE (ongoing)                                    │
│     → Prompt → Review → Test → Repeat                    │
│                                                          │
│  7. SHIP (1 week)                                        │
│     → Security, deploy, monitor, iterate                 │
│                                                          │
│  Total planning: ~4 hours                                │
│  Typical ROI: 10:1 to 70:1                               │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

---

# When to Use This Algorithm

## ✅ Use it for:
- New product or feature (> 3 weeks of work)
- Major refactors or migrations
- Multi-system integrations
- High-stakes, high-cost projects
- Anything where a mistake is expensive

## ⚡ Shortened version for smaller projects:
For features taking 1-5 days, compress to:
1. **Capture** (15 min): Write requirements in 5 bullets
2. **Design** (30 min): Sketch the solution
3. **Stress-Test** (15 min): List 3 ways it could go wrong
4. **Execute**: Build it
5. **Ship**: Deploy with basic monitoring

## ❌ Skip for:
- Bug fixes
- Copy changes
- Config updates
- Anything you can fully spec in your head in 30 seconds

---

# The ROI Case for Planning

Spending 4 hours planning a 3-month project:

| Scenario | Without Algorithm | With Algorithm |
|----------|-----------------|----------------|
| Rework rate | 40-60% | 10-20% |
| Scope creep | Common | Rare |
| Architecture changes mid-project | Common | Rare |
| Deadline hit | 30% of projects | 70% of projects |
| Budget overrun | Common | Rare |

**Proven result from BDSMLR project:**
- 4 hours of planning → 280 hours of implementation saved
- **70:1 ROI**

---

# Applying to Any Domain

This algorithm works for:

| Domain | Phase 2 Focus | Phase 3 Focus |
|--------|--------------|---------------|
| Web App | DB schema, API design | Security, scalability |
| Mobile App | UX flows, offline sync | Performance, battery |
| Data Pipeline | Schema, transforms | Reliability, cost |
| Marketing Campaign | Funnel, channels | CAC, conversion |
| Business Process | Workflow, roles | Bottlenecks, handoffs |
| SaaS Product | Pricing, onboarding | Churn, LTV |

The phases are universal. Only the questions inside each phase change.

---

*Algorithm derived from real-world application: BDSMLR Monetization System planning session.*
*Result: B- plan (75/100) optimized to A (88/100). Timeline reduced 35%. ROI increased 26%.*
