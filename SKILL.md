---
name: semantic-sim-method
description: Use when you need to simulate futures in a reduced semantic space with rotations, falsification checks, and adversary analysis
---

# Semantic Simulation Method

## Why This Exists

You're facing a decision with real stakes, incomplete information, and no historical dataset to model from. You need to think about what might happen — but you want something more rigorous than brainstorming and less demanding than quantitative forecasting.

Most scenario planning falls into one of two traps:
- **Too loose:** "Let's brainstorm three scenarios" produces narratives that confirm what you already believe
- **Too heavy:** Quantitative models require data you don't have and produce false precision

The Semantic Simulation Method sits in between. It gives you a **structured process** for exploring futures that's rigorous enough to reveal blind spots, but doesn't require probability distributions or historical data.

### The Core Idea

In any complex situation, a small number of forces explain most of what will happen. If you can:
1. Identify those forces
2. Systematically ask "what happens when each force wins?"
3. Check whether your plan survives all of those worlds
4. Figure out what *you* can do to reshape the forces in your favor
5. Then consider what happens when others are doing the same

...you'll understand the possibility space better than most people who spend 10x longer thinking about it.

This borrows intuition from **dimensionality reduction** in statistics (like PCA — Principal Component Analysis). Instead of reducing numeric variables to principal components, you reduce a complex situation to a small set of **driving forces** and simulate by letting each one dominate.

---

## Concepts

Before walking through the method, here are the key ideas you'll need.

### Forces (Semantic Attractors)

A force is a **pressure that shapes outcomes**. Not something you control, but something that pulls the situation toward a particular configuration. Good forces are:

- **Independent enough** from each other to generate meaningfully different scenarios
- **Observable** — you can point to real-world signals that show a force strengthening or weakening
- **Not outcomes** — "success" isn't a force; "foot traffic" is

Choose **4–6 forces**. Fewer than 4 won't capture enough of the picture. More than 6 becomes incoherent.

### Dominant-Force Transitions

The key rule: **when one force dominates, it reconfigures the others.** This is what makes the simulations non-trivial.

You're not just asking "what if foot traffic is high?" You're asking "what does the whole situation look like when foot traffic is *the* dominant force — and how does that reshape rent costs, competition, and customer loyalty?"

### Rotations

After running your initial simulations, you may notice that one force doesn't generate much difference across scenarios — every sim looks about the same along that axis. That's a signal to **rotate**: replace it with a related but more discriminating concept.

Think of it like adjusting the angle of a camera. The subject is the same, but a better angle reveals details you couldn't see before.

### Idempotency

Your plan should be **idempotent across simulations** — it should work regardless of which force dominates. If your plan only works in one scenario, it's fragile.

Idempotency checking forces you to separate:
- **Core** — What's true in every scenario (your real plan)
- **Boundary** — What's true in some scenarios (your assumptions)
- **Fragile** — What's only true in one scenario (your risks)

### Three Layers of Simulation

The method builds up in layers, each adding realism:

1. **Passive landscape** — You observe. Forces play out. You check if your plan survives. ("What world am I walking into?")
2. **Active agency** — You act. Your moves reshape the forces. Boundary conditions become things you can influence. ("What can I do about it?")
3. **Live competition** — Others act too. Multiple agents with agency reshape forces simultaneously. ("What happens when someone is actively working against me?")

Each layer depends on the one before it. You can't act intelligently without first mapping the landscape. You can't model competition without first understanding your own moves.

---

## The Method

### Step 1: Define Your Space

Before simulating, get explicit about three things:

1. **Your objective** — What are you trying to achieve? State it concretely. Not "succeed" but "sustain a profitable business for 5+ years."
2. **Your forces (4–6)** — The pressures that will shape whether you achieve that objective
3. **Your survival test** — What must remain true across all scenarios for your plan to work? This is your idempotency criterion.

### Step 2: Run Base Simulations

*Layer 1 — Passive landscape. You're an observer.*

Run **3 simulations**, each with a different force as the dominant pressure:

| Sim | Structure |
|-----|-----------|
| A | First force dominates — how does it reshape everything else? Where does your plan land? |
| B | Second force dominates — different configuration, different trajectory |
| C | Third force dominates, or no single force dominates (fragmented/multipolar) |

For each simulation, write:
- **Configuration** — How the dominant force reshapes the other forces
- **Trajectory** — What happens over time (early → mid → late dynamics)
- **Your position** — Does your plan achieve the objective in this world?

### Step 3: Check Idempotency

Review all 3 simulations against your survival test. Categorize everything:

- **Core** — True across all sims (this is your real plan)
- **Boundary** — True in some sims, contingent in others (these are assumptions you're making)
- **Fragile** — Only true in one sim (these are risks you need to manage or accept)

### Step 4: Rotate for Variance

Look at your simulations. Is there a force that doesn't generate much difference?

- Replace it with a related concept that's more discriminating
- Re-run the simulation that changes most under the new axis
- Document **why** you rotated — this is insight, not just bookkeeping

Usually 1–2 rotations is enough. Stop when each force generates a meaningfully different scenario.

### Step 5: Falsify (Mandatory)

*Still Layer 1 — neutral world, no agency yet.*

Write the **devil's-advocate simulation** — the scenario where your plan fails. This is not optional.

Answer three questions:
1. **What events would cause your plan to fail?** Be specific.
2. **What would you do instead?** (Your pivot — what you become when Plan A dies)
3. **What early signals would tell you this scenario is materializing?** (So you can pivot before it's too late)

If you can't write a convincing falsification, either you don't understand the situation well enough, or your plan is trivially safe (and probably not very ambitious).

### Step 6: Act (Your Agency)

*Layer 2 — You're no longer an observer. You're a player.*

Up to now, you've been mapping a landscape that happens *to* you. But you have agency. Your actions reshape the forces too.

Go back to your idempotency check from Step 3 and ask:

1. **Which boundary conditions can you move to core?** — Are there assumptions that you could *make true* through deliberate action? A boundary condition isn't necessarily a fact of life — it might be something you can influence.

2. **Which fragile findings can you move to boundary?** — Can you reduce your exposure to single-scenario risks by taking specific actions?

3. **What moves reshape the forces in your favor?** — Not just "what's my strategy" but "how do my actions change the landscape itself?"

For each action you identify, ask:
- **What does it cost?** (money, time, attention, optionality)
- **When does it need to happen?** (some moves only work early; others are evergreen)
- **Is it reversible?** (irreversible moves need higher confidence)

The output of this step is an **action plan layered onto your landscape map** — not just "what world am I in" but "what am I doing about it."

### Step 7: Compete (Multiple Live Players)

*Layer 3 — Other agents have agency too.*

If someone could actively work against your plan — a competitor, a regulator, a market force with its own agenda — model them as a live player:

1. **What are their objectives?** — They have goals too. What are they optimizing for?
2. **What can they capture?** — Which leverage points (locations, suppliers, regulations, platforms, relationships) could they control?
3. **What friction can they create?** — How could they make it harder for you to operate or for customers/partners to choose you?
4. **What's their optimal sequence?** — If they were running this method from their perspective, what would their action plan look like?

Then overlay their moves onto yours:
- **Where do your actions conflict?** — Are you competing for the same leverage points?
- **Where do their moves invalidate your Step 6 actions?** — Does their agency undo the boundary→core moves you planned?
- **What are your course-correction triggers?** — At what point do you change strategy in response to their moves?
- **What are your abort criteria?** — When do you stop competing head-on and adapt?

---

## Worked Example: Opening a Coffee Shop

*This walks through every step so you can see how the pieces connect.*

### Context

You're deciding whether to open a coffee shop on a specific street in a mid-sized city. There are two candidate locations: a busy main street spot (high rent, high foot traffic) and a quieter side street spot (lower rent, less visibility, near a university).

### Step 1: Define the Space

**Objective:** Operate a profitable coffee shop that sustains itself for 5+ years without requiring ongoing outside investment.

**Forces:**
1. **Foot traffic** — How many potential customers walk past daily?
2. **Rent pressure** — How fast are commercial rents rising in the area?
3. **Competition density** — How many other coffee options are nearby?
4. **Customer loyalty** — Do people come back, or do they grab whatever's closest?

**Survival test (idempotency criterion):** Revenue must exceed operating costs (rent + staff + supplies) within 12 months regardless of which force dominates.

### Step 2: Base Simulations

**Sim A — Foot Traffic dominates:**

The neighborhood is booming. A new transit stop opens, office buildings fill up, the street becomes a major pedestrian corridor. Foot traffic doubles in 18 months.

*What it reshapes:* Rent pressure rises sharply — landlords see the traffic and raise rates. Competition density increases — chains notice the foot traffic and open nearby. Customer loyalty matters less because volume compensates.

*Your position:* Main street location thrives early but faces a squeeze: rising rent + chain competition erodes margins by year 3. Side street location misses the boom — traffic increase doesn't reach one block over.

*Does the plan survive?* Yes for main street in years 1–2, precarious by year 3–5. No for side street.

**Sim B — Rent Pressure dominates:**

The city rezones the area. Developers buy up commercial property. Rents increase 40% over 3 years. Several small businesses close. The neighborhood becomes more upscale but less dense with shops.

*What it reshapes:* Foot traffic decreases as small shops close (fewer reasons to walk the street). Competition density drops — only well-capitalized businesses survive. Customer loyalty becomes critical — your remaining customers are your lifeline.

*Your position:* Main street location is in direct danger — you're paying top dollar and foot traffic is declining. Side street location is cheaper and more survivable, especially if university students are loyal.

*Does the plan survive?* Barely for main street (margin pressure is severe). Yes for side street if you've built loyalty with the university crowd.

**Sim C — Fragmented / No dominant force:**

The neighborhood stays roughly as-is. Modest foot traffic, stable rents, a few competitors, some regulars. No dramatic changes in any direction. Growth is slow and organic.

*What it reshapes:* Nothing reshapes dramatically. Differentiation and execution matter more than positioning.

*Your position:* Both locations are viable. The decision comes down to execution: quality, atmosphere, community building. Main street has a slight edge on discovery; side street has a slight edge on cost.

*Does the plan survive?* Yes for both, with tighter margins on main street.

### Step 3: Idempotency Check

| Category | Finding |
|----------|---------|
| **Core** | The shop must build a repeat-customer base within 12 months. This is true in every sim — volume alone (Sim A) is temporary, and in every other scenario loyalty is what sustains you. |
| **Boundary** | Main street works *if* rent stays manageable. Side street works *if* you can attract customers despite lower visibility. These are assumptions, not certainties. |
| **Fragile** | Main street's high-volume, low-loyalty model only works in Sim A — and even there, only for 2 years before competition and rent catch up. |

**Key insight:** The survival test (profitable in 12 months) is easier to hit on main street in Sim A, but easier to *sustain for 5 years* on side street in Sims B and C. The objective was 5+ years — so the side street is more robust against the full objective, even though main street looks better in the short term.

### Step 4: Rotation

"Competition density" didn't generate much variance — in every sim, some competitors exist and you deal with them. It's not driving different outcomes.

**Rotate to: "Neighborhood identity"** — Is this area becoming known *for* something? A food destination, a student quarter, a tech hub? Neighborhood identity affects who shows up and why, which is more discriminating than just counting competitors.

**Re-running Sim A with "Neighborhood identity":** The area becomes known as a trendy food/coffee destination. This *amplifies* foot traffic but also attracts specialty competitors (not just chains). Your differentiation matters more. Side street benefits if the "neighborhood" expands to include it — a university-adjacent café becomes part of the destination identity rather than being off the beaten path.

*This rotation revealed that the side street isn't necessarily disadvantaged — if the neighborhood identity expands, being "the quiet one near campus" is a positioning advantage, not a visibility problem.*

### Step 5: Falsification

**The scenario where the plan fails:** The university announces it's relocating its campus to a different part of the city (consolidating two campuses). Over 18 months, the student population in the neighborhood drops 60%. Simultaneously, a major chain opens on main street with a loss-leader pricing strategy.

**Trigger events:**
- University announces campus consolidation study
- Student housing occupancy in the area drops below 80%
- A chain signs a lease within 2 blocks

**Pivot boundary:** If student traffic drops >40%, convert the side street space to a co-working café model (targeting remote workers rather than students). The lower rent gives you runway to experiment.

**Early signals to watch:**
- University real estate transactions
- Student enrollment trends at the nearby campus
- Commercial lease signings in the area (public records)

### Step 6: Act

*Now we stop observing and start playing.*

Revisiting the idempotency check — what can you actually do about your boundary conditions and fragile findings?

**Boundary → Core moves:**

| Boundary condition | Action to make it core | Cost | Timing |
|---|---|---|---|
| Side street needs to attract customers despite low visibility | Partner with the university: student discount program, event hosting, bulletin board presence. Make the shop a *destination* rather than relying on walk-by discovery. | Low cost (time + small discounts). Low risk. | Must start pre-launch. |
| Rent must stay manageable | Negotiate a 5-year lease with a fixed escalation cap (e.g., max 3%/year) before signing. Trade a longer commitment for rate certainty. | Reduces flexibility (locked in). High confidence needed in location. | Must happen at signing — irreversible. |

**Fragile → Boundary moves:**

| Fragile finding | Action to reduce exposure | Cost | Timing |
|---|---|---|---|
| High-volume model only works in Sim A | Don't pursue a high-volume model at all. Design for loyalty from day one: learn names, build community, host events. This makes you resilient to traffic fluctuations. | Slower initial revenue. Requires more personal investment. | Ongoing from day one. |

**Force-reshaping moves:**

- **Create foot traffic yourself:** Host weekly events (open mic, study nights, local art). You're not just responding to foot traffic — you're generating it. This partially decouples you from the "foot traffic" force.
- **Shape neighborhood identity:** If you're among the first quality shops on the side street, you help *define* what the area is known for. Early movers shape identity; latecomers respond to it.

**Key realization from this step:** Several "boundary" items from Step 3 aren't actually things that happen to you — they're things you can influence through deliberate action. The side street's visibility problem looked like a landscape fact. It's actually an action item.

### Step 7: Compete

**Competitor:** A well-funded chain considering the main street location.

**Their objectives:** Maximize locations in growing neighborhoods. Unit economics driven by volume. Brand consistency over local character.

**What they can capture:** Prime main street lease (exclusive), supplier volume discounts, brand recognition, app-based loyalty infrastructure.

**What friction they can create:** Loss-leader pricing for 6–12 months to drain your customer base; loyalty app with rewards that create switching costs; hiring away your trained baristas with higher wages.

**Their optimal sequence:** Secure the high-traffic lease → launch with aggressive pricing → build app-based loyalty → raise prices once independents have closed.

**Overlay with your Step 6 actions:**

Your university partnership and community-building strategy *specifically targets customers the chain is bad at serving*. Students and regulars who want a "third place" aren't well-served by a chain's volume model. Your Step 6 moves and their Step 7 moves don't directly conflict — you're competing for different segments.

However: if they launch loss-leader pricing, some of your price-sensitive customers (students) will drift. Your fixed-cost lease protects you from rent pressure, but you need a **loyalty moat** deep enough to survive 6–12 months of a chain undercutting on price.

**Course-correction triggers:**
- If a chain signs the main street lease → validate that your university partnerships are generating enough traffic. If yes, stay the course. If no, accelerate community programming.
- If you lose >20% of revenue for 2 consecutive months → launch a "locals card" (punch card / membership) to formalize loyalty before it erodes further.
- **Abort criteria:** If you lose >30% of revenue for 3 consecutive months despite loyalty efforts, sublease and relocate rather than bleed cash.

### Synthesis

| Layer | Finding |
|-------|---------|
| **Robust** | Building a repeat-customer base is essential in every scenario. The side street location is more resilient across the full 5-year objective. |
| **Contingent** | Side street viability depends on university presence and the ability to attract customers despite lower foot traffic — but Step 6 showed these are *actionable*, not just assumptions. |
| **Fragile** | A high-volume, low-loyalty strategy on main street — only works in one scenario, and only temporarily. |
| **Your moves** | Lock in a fixed-escalation lease. Partner with the university pre-launch. Build community from day one. Shape neighborhood identity as an early mover. |
| **Competitive exposure** | A chain on main street threatens price-sensitive customers but not your core loyalty base. Your biggest risk is the 6–12 month loss-leader window — survive that and the chain actually *validates the neighborhood* for you. |
| **Watch for** | University campus changes, neighborhood rezoning, chain lease signings, rent escalation clauses, your own repeat-customer rate (the canary in the coal mine). |

**Decision:** The side street location better serves the stated objective (5+ years of profitability) — and the gap widens once you factor in your agency. The main street location bets on a landscape you can't control. The side street location lets you *build the landscape you need*.

---

## Advanced Example: Coffee Chain vs. Franchise

*Now that you've seen the method on a single-location decision, here's a setup with a harder objective and more moving parts. This one isn't fully worked — it's a prompt for you to try the method yourself.*

### Context

You've run a successful independent coffee shop for 3 years. You want to expand to 10 locations within 5 years. Two models are on the table:

- **Build a chain** — You own and operate every location. Full control, full cost, full risk.
- **Franchise** — You license your brand, recipes, and systems. Franchisees put up capital and run locations. You collect fees but cede control.

### Setup (Try This Yourself)

**Objective (note: multi-dimensional):**
Reach 10 profitable locations within 5 years *while* maintaining brand quality *and* positioning for continued growth beyond year 5.

This is harder than the single-shop example because the objective has **three components** that can conflict. Fast expansion (locations) can undermine quality. Maintaining quality can slow growth. Positioning for the future might require sacrificing short-term profit.

**Suggested forces:**
1. **Capital availability** — How much funding can you access, and at what cost?
2. **Labor market** — Can you hire (chain) or attract franchisees (franchise) fast enough?
3. **Brand coherence** — Does the customer experience stay consistent as you scale?
4. **Market timing** — Is the window for expansion open now, or is the market saturating?
5. **Regulatory environment** — Franchise law, commercial lease regulations, food safety requirements at scale

**Survival test:** At least 7 of 10 locations must be individually profitable by year 3, AND brand perception (measured by repeat-customer rate) must not drop below the original shop's baseline.

### What Makes This Harder

- **The objective has tension built in.** Fastest path to 10 locations (franchise) may be the worst for brand coherence. The method's idempotency check will force you to confront this: can *any* model satisfy all three parts of the objective?

- **Forces interact more.** Capital availability reshapes differently depending on the model — abundant capital favors chains (you can self-fund), scarce capital favors franchising (other people's money). The same force pushes toward opposite decisions depending on context.

- **Step 6 (Act) becomes critical.** Your agency isn't just "which location" — it's "which *model*." And the model you choose reshapes every force. Chain ownership gives you direct control over brand coherence but requires massive capital. Franchising solves capital but creates a principal-agent problem with quality.

- **Step 7 (Compete) gets interesting.** Your competitor isn't just another coffee shop — it might be a well-funded chain *and* a franchise network simultaneously. How do you model an adversary that can play both strategies while you're committed to one?

- **Falsification has two targets.** You need to falsify both the chain model and the franchise model. One of them should fail more convincingly — that's signal.

### Hints for Running It

- Your base sims should each produce a different answer about *which model to choose*, not just different outcomes for the same model. If all three sims favor franchising, your forces aren't discriminating enough.

- The rotation opportunity: "Market timing" might not differentiate much. Consider rotating to **"Customer sophistication"** — are your target customers the type who care about brand authenticity (favors chain) or just want reliable coffee (favors franchise)?

- For Step 6: The most interesting moves are ones that blur the chain/franchise boundary. Can you create a hybrid — company-owned flagships in key markets with franchised locations elsewhere? How does that reshape your forces?

- For falsification: The scariest scenario is probably one where you expand successfully but brand quality degrades invisibly — customers leave slowly, and by the time you notice, your repeat-customer rate has cratered across all locations. What early signals would catch this?

- The synthesis should give you either a clear model choice *or* a hybrid strategy with specific criteria for when to use each model. If the method doesn't help you decide, your objective might need sharpening.

---

## Extensions

These are optional layers you can add once you're comfortable with the base method. Each one sharpens a different aspect of the output — communication, precision, or grounding in reality.

### Extension A: Variable Interaction Report

After completing the full simulation, compress your findings into a structured report that maps how forces interact with each other. This is about **communication** — the method produces rich insight, but stakeholders need different levels of detail.

**Analyst version — Interaction matrix:**

Build a matrix of force pairs and classify each interaction:

| | Foot Traffic | Rent Pressure | Neighborhood Identity | Customer Loyalty |
|---|---|---|---|---|
| **Foot Traffic** | — | Amplifies (↑ traffic → ↑ rent) | Amplifies (↑ traffic → area becomes "known for" something) | Dampens (high volume reduces dependency on loyalty) |
| **Rent Pressure** | Dampens (↑ rent → shops close → ↓ traffic) | — | Reshapes (rising rents push toward upscale identity) | Amplifies (fewer options → remaining customers more loyal) |
| **Neighborhood Identity** | Amplifies (strong identity → destination traffic) | Amplifies (desirable identity → ↑ rent) | — | Amplifies (identity creates belonging → loyalty) |
| **Customer Loyalty** | Decouples (loyal base reduces traffic dependency) | Buffers (loyal revenue survives rent increases longer) | Amplifies (loyal customers become ambassadors for identity) | — |

Interaction types:
- **Amplifies** — Force A strengthening makes Force B stronger
- **Dampens** — Force A strengthening makes Force B weaker
- **Reshapes** — Force A doesn't change Force B's intensity but changes its *character*
- **Decouples** — Force A reduces your sensitivity to Force B
- **Buffers** — Force A gives you more time before Force B becomes critical
- **Conflicts** — Forces push toward mutually exclusive configurations

The matrix reveals **feedback loops** (amplify cycles that accelerate), **natural hedges** (forces that buffer each other), and **critical dependencies** (where a single interaction drives most of the variance).

**Executive version — 3–5 bullets:**

Distill the matrix into what matters for the decision:

> 1. **Foot traffic and rent are in a reinforcing loop** — any scenario where traffic booms will also squeeze margins within 2–3 years. Don't optimize for traffic alone.
> 2. **Customer loyalty decouples us from traffic risk** — the single most protective force. Every investment in loyalty reduces exposure to our biggest vulnerability.
> 3. **Neighborhood identity is a multiplier, not a force we control directly** — but we can influence it as an early mover (Step 6). It amplifies both traffic and loyalty, making it the highest-leverage indirect investment.
> 4. **Rent pressure has no natural counterforce in our model** — loyalty buffers it but doesn't reverse it. The fixed-escalation lease (Step 6) is the only structural protection. Non-negotiable.
> 5. **The dangerous scenario is the one that looks good** — Sim A (traffic boom) triggers the amplify loop between traffic and rent that eventually kills margins. Our falsification scenario is less likely but less survivable; Sim A is more likely and more insidious.

### Extension B: Quantized Model

The base method is qualitative — forces "dominate" or "don't," and findings are "core" or "fragile." You can add a lightweight quantization layer to catch distinctions that narratives blur, without going full quant.

**This is not a statistical model.** It's structured intuition with numbers — a way to make implicit judgments explicit and comparable.

**Step 1: Score forces per simulation**

For each sim, rate each force on a simple ordinal scale:

| | Sim A (Traffic) | Sim B (Rent) | Sim C (Fragmented) |
|---|---|---|---|
| Foot Traffic | 5 (dominant) | 2 (declining) | 3 (stable) |
| Rent Pressure | 4 (rising fast) | 5 (dominant) | 3 (stable) |
| Neighborhood Identity | 4 (emerging) | 3 (reshaping) | 2 (undefined) |
| Customer Loyalty | 2 (not needed yet) | 4 (critical) | 3 (helpful) |

Scale: 1 (negligible) → 5 (dominant). Score reflects the force's *intensity in that scenario*, not whether it's good or bad for you.

**Step 2: Sensitivity analysis**

For each force in each sim, ask: **if this force shifted one level (±1), would the outcome flip?**

| Force | Sim | Current | Flip if shifted? | Direction |
|---|---|---|---|---|
| Rent Pressure | A | 4 | Yes — if rent hits 5, main street fails by year 2 instead of year 3 | Fragile upward |
| Customer Loyalty | B | 4 | Yes — if loyalty drops to 3, side street becomes unviable | Fragile downward |
| Neighborhood Identity | C | 2 | No — identity at 1 or 3 doesn't change the "both viable" conclusion | Robust |

Sensitivity flags tell you **where your analysis is thin**. A finding that flips on a ±1 shift needs either more investigation or explicit risk management.

**Step 3: Confidence markers**

Tag your idempotency categories with confidence:

| Category | Finding | Confidence | Why |
|---|---|---|---|
| Core | Must build repeat-customer base | High | True in all sims, not sensitive to ±1 shifts |
| Boundary | Side street needs university presence | Medium | Sensitive to loyalty dropping (Step 2), but Step 6 actions mitigate |
| Fragile | High-volume model on main street | High (that it's fragile) | Fails in 2 of 3 sims, sensitive to rent ±1 in the one where it works |

"High confidence that something is fragile" is useful — it means you should definitely not bet on it, not that you're uncertain.

**When quantization helps most:**
- Comparing two options that feel similar in narrative form (the scores may reveal a gap)
- Communicating to stakeholders who want "how sure are you?" answers
- Identifying which forces to monitor most closely (the sensitive ones)

**When to skip it:**
- First pass through the method (get the narratives right first)
- When the qualitative analysis already produces a clear decision
- When scoring would be false precision (you genuinely can't distinguish a 3 from a 4)

### Extension C: Data Augmentation

The base method works with zero external data — that's a feature, not a bug. But real data, applied at specific points, **reduces uncertainty where it matters most.** The key is knowing *where* data helps vs. where it's noise.

**Principle: Data sharpens steps, it doesn't replace them.** You still need the method's structure to know what questions to ask. Data helps you answer those questions with less guesswork.

**Where data helps, mapped to method steps:**

| Step | What data sharpens | Example data sources | What to watch for |
|---|---|---|---|
| **Step 1: Force selection** | Are these actually the dominant forces, or are you projecting? | Market reports, industry analyses, analogous case studies | If data suggests a force you didn't include is more important than one you did — rotate |
| **Step 2: Base sims** | Are your "dominant force" scenarios realistic? | Historical examples of similar transitions (neighborhood gentrification data, transit impact studies) | Use data to calibrate magnitude, not to pick winners |
| **Step 4: Rotations** | Is the replacement axis actually more discriminating? | Survey data, customer segmentation, demographic trends | A rotation that's supported by data is stronger than one based on intuition alone |
| **Step 5: Falsification** | Is your devil's advocate realistic or a strawman? | Base rates for your trigger events (how often do universities relocate? What % of chain launches succeed?) | If your falsification scenario has a <1% base rate, it's not a real stress test — find a more likely one |
| **Step 6: Act** | Will your actions actually work? | Case studies of similar moves, cost data, market response data | Validate your most expensive/irreversible moves with the hardest data you can find |
| **Step 7: Compete** | What is the competitor actually capable of? | Public filings, pricing data, expansion history, job postings (signal of plans) | Competitor data is often available but not obvious — job postings reveal strategic direction, lease filings reveal location plans |
| **Extension B: Quantization** | Sharpen ordinal scores from vibes to grounded estimates | Any quantitative data relevant to force intensity | Don't false-precision — if data gets you from "somewhere 2–4" to "probably 3," that's useful. If it gets you from "3" to "3.2," that's noise |

**Data quality tiers:**

Not all data is equally useful. Prioritize:

1. **Direct observation** — You visited competing shops, counted foot traffic, talked to the landlord. Highest signal.
2. **Structured data** — Census data, commercial lease databases, university enrollment records. Reliable but may not map perfectly to your context.
3. **Analogous cases** — "A similar neighborhood in another city experienced X." Useful for calibration, dangerous for prediction.
4. **Expert opinion** — Real estate agents, industry analysts, local business owners. Valuable for force selection and reality-checking, but subject to their own biases.
5. **Vibes / anecdotal** — "I heard the neighborhood is changing." Starting point only — upgrade to a higher tier before relying on it.

**Signal monitoring (turning "watch for" into action):**

Your synthesis produces a "watch for" list. Data augmentation turns that list into an **early-warning system:**

| Watch for | Data source | Check frequency | Threshold |
|---|---|---|---|
| University campus changes | University board meeting minutes, real estate filings | Quarterly | Any mention of campus consolidation study |
| Rent escalation | Commercial lease databases, nearby listing prices | Monthly | >10% YoY increase in comparable spaces |
| Chain expansion | Commercial lease filings, franchise disclosure documents, job postings in area | Monthly | Any national chain signing within 3 blocks |
| Repeat-customer rate decay | Your own POS data | Weekly | <5% decline from baseline triggers investigation |

The watch list is only useful if you actually watch it. Define the source, frequency, and threshold *before* you need them — when things are calm, not when they're moving.

---

## Deliverables

A complete semantic simulation produces:

1. **Objective** — stated concretely
2. **3 base simulations** with dominant-force configurations (Layer 1: passive landscape)
3. **Idempotency assessment** — core / boundary / fragile
4. **1–2 axis rotations** with rationale
5. **1 falsification simulation** with trigger events, pivot boundary, and early signals
6. **Action plan** — boundary→core moves, force-reshaping moves, with costs and timing (Layer 2: your agency)
7. **1 competitive simulation** (optional) with objectives, leverage, friction, and course-correction triggers (Layer 3: multi-player)
8. **Synthesis** — What's robust, what's contingent, what's fragile, what you're doing about it, and what to watch for
9. *(Optional)* **Variable interaction report** — analyst matrix + executive bullets (Extension A)
10. *(Optional)* **Quantized scores** — ordinal force ratings, sensitivity flags, confidence markers (Extension B)
11. *(Optional)* **Data augmentation plan** — sources mapped to steps, signal monitoring with thresholds (Extension C)

---

## Common Mistakes

| Mistake | Why It Hurts | Fix |
|---------|-------------|-----|
| No explicit objective | You can't check idempotency if you haven't defined success | State your objective concretely before choosing forces |
| Too many forces (>6) | Simulations become incoherent — too many moving parts | Merge correlated forces or drop the least discriminating one |
| Forces that are outcomes | "Success" or "growth" as a force just begs the question | Forces are pressures, not results. Ask "what *causes* growth?" |
| No rotations | Your initial framing has blind spots you'll never find | Always try at least one rotation. If nothing improves, document that |
| Skipping falsification | Confirmation bias — you only explored worlds where you win | Mandatory. No exceptions. If you can't falsify, you don't understand the space |
| Treating simulations as predictions | Anchoring on a specific scenario instead of mapping the space | Simulations are for coverage and stress-testing, not forecasting |
| Optimizing for one scenario | Choosing the plan that wins biggest in Sim A without checking B and C | Idempotency check exists precisely to prevent this |
| Skipping Step 6 (Act) | Treating boundary conditions as facts of life when they're actually actionable | Always ask "can I change this?" before accepting a boundary condition |
| Jumping to Step 7 (Compete) without Step 6 | You can't model competition intelligently if you haven't mapped your own moves first | Layer 2 before Layer 3. Know your own game before modeling theirs. |

---

## Quick Reference

For practitioners who've internalized the method:

1. **Objective + 4–6 forces + survival test**
2. **3 base sims** (each with different dominant force) — *Layer 1: passive landscape*
3. **Idempotency check** → core / boundary / fragile
4. **1–2 rotations** on low-variance axes
5. **1 falsification sim** with triggers + pivot + early signals
6. **Action plan** — boundary→core moves, force-reshaping, costs, timing — *Layer 2: your agency*
7. **1 competitive sim** (optional) with objectives + leverage + friction + course-correction — *Layer 3: multi-player*
8. **Synthesis:** robust / contingent / fragile / your moves / competitive exposure / watch-for
