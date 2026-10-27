# Marketing and monetization

**What is collecting money today:** ISC display and affiliate advertising, plus a much smaller BDSMLR remnant and the PayPal shop.  
**What was designed and is not on sale:** one RelayOS subscription that also unlocks tools on linked properties.  
**Latest price draft:** $5/month, 11 June 2026. April’s decision was $12/month. The live shop product is still $20/month to remove ads.  
**Pavel has not confirmed which price belongs in the company guide.**

## Revenue model

| Line | Status | What it actually is |
| --- | --- | --- |
| ISC advertising | Live. About 95% of the July 2026 Ad Ops P&L. | Banners, tabunders, nav, buttons, interstitials on isexychat.com. |
| BDSMLR display and affiliate | Live, and much smaller than it was. | Remnant after TwinRed (May 2025) and GrandSlam (April 2025) stopped. |
| BDSMLR Shop | Live. Healthiest BDSMLR line in August 2026, about $44/day. | The old ad-free subscription. PayPal. Forward Handle LLC on the statement. |
| RelayOS subscription | Designed. Not current revenue. | IRC bouncer, offline messages, and extra tools, billed on a neutral property. |
| ISC chat as a paid product | Explored in March 2026. Not launched. | |
| Creator marketplace and API / white-label | February–March 2026 plans. Superseded. | |

**Dual revenue, as a direction:** ads on anonymous traffic stay primary. The subscription is supplementary. A 21 May 2026 verdict treated subscriptions as about $1,200 a month (4% of a modeled baseline) and said the strategy survives if subscriptions die. Those dollars are a simulation.

**Audience the April plan was built on** (database and GA, early 2026, not ad-server stats):

- About 3.2 million registered BDSMLR accounts.
- About 66k monthly active users, about 12.7k daily. Some notes say 66k–75k MAU. An earlier 500k assumption was dropped.
- About 9,124 people sent or received a message in 30 days. About 5,555 of those did more than one.
- About 1,694 active private blogs in 30 days.
- Roughly 99% of traffic is not logged in: on the order of 1.0 million non-logged-in users versus about 23k logged-in in the April GA cut (one write-up says 1,055k versus 23k). Direct was the bulk (about 829k). Organic was about 210k.
- At 1% of about 10k power users, the call’s own math was about 50 paying users, not 2,500.

That is why anonymous ads can be the BDSMLR ad plan even if logged-in users see none.

## The subscription that is not on sale

Agreed direction after the **20 April 2026** call with Pavel, Allen, and Simon, then revised by the June tier drafts.

- One subscription at the RelayOS level. Premium on RelayOS is premium on the connected properties.
- Users have a tenant account and a separate billing account, linked afterwards by OAuth. Each tenant has its own WordPress user database. The shop database is billing-only.
- Bought on a neutral property (`getrelayos.com` in the drafts). The receipt must not describe an adult purchase. BDSMLR-only perks stay on BDSMLR and are not advertised on the RelayOS pricing page.
- Offline messaging is **same-network only**. Cross-network messaging was rejected on 20 April.
- Anonymous visitors see ads. Logged-in users, free or paid, do not. Pavel corrected the tier matrix on this point himself.
- Free logged-in users get a quota of offline messages. The matrices use **about 10 a month** as a working figure. Allen’s rule was to set it high enough that only the most active people hit it. Pavel’s rule for public posts: **do not publish a number until it is chosen.**
- Paid BDSMLR tools in the June draft: unpixelated deep search, archive sorting and layouts, posting to private blogs. Reading a private blog you already follow stays free. Privacy toggles stay free.
- Full migration of users into the WordPress side was the 20 April decision, because offline delivery needs the users in that database. Simon owns that build. Non-paying users keep the same username and password. The login page looks slightly different. Do not dump the change on users at once.
- Framing, 8 May 2026 (Allen, Pavel, Simon): sell a private IRC / members-club / text chat subscription, not an adult content or upload platform. Processors are sensitive to photos and video.

**Not adopted:** the 18 May stress test, which recommended shipping a lazy migration and said full migration could be killed. April 20 remains the decision Pavel cites. The same note warned that `getrelayos.com` is a single point of failure. That warning was not answered. A lazy-migration plugin path was described as already deployed on `account.bdsmlr.com`. That is a technical path, not a reversal of the April decision.

### June 11 tier draft — BDSMLR

One product: **relayOS Premium, $5/month**, bought at getrelayos.com. Free account $0. Clover mark on premium. Draft pages: `bdsmlr_pricing_page.html`, `bbchat_pricing_page.html`, `relayos_pricing_page.html`.

| | Free, logged in | Premium, $5/month |
| --- | --- | --- |
| Offline messages | ~10/month, unpublished until chosen | Unlimited |
| Private blogs | Read. Cannot post. | Can post |
| Archive | Newest, grid only | Popular, liked, newest; masonry; originals versus reblogs |
| Search | Pixelated at depth, newest only | Always clear; popular, liked, newest |
| Others’ following feeds | No | Yes |
| Ads while logged in | None | None |
| Other tenants | | bb.chat and relayOS premium included |

The neutral RelayOS page does not name BDSMLR perks. It sells multi-network bouncer, unlimited offline messages, a 24/7 connection, uploads, and premium on linked sites. Free on that page is web and standard IRC, unlimited history, the same unpublished message quota, idle disconnect, and one identity.

### June 11 tier draft — bb.chat (v2 supersedes v1)

| | Free | Premium, $5/month |
| --- | --- | --- |
| History | Unlimited | Unlimited. v1 had limited history for free. Closed because text is cheap. |
| Offline messages | ~10/month | Unlimited |
| Connection | Timeout after inactivity. Duration not set. | 24/7 persistent |
| Networks | bb.chat only | Any IRC network |
| Media | None | Files, photos, and videos via Wasabi. Registered plus premium only. Anonymous uploads had gone badly. |
| Support | “Fast, personal” | Priority |

Third-party clients can join the bb.chat network. The client’s multi-network access is premium. Still open: timeout length, file-size and storage caps, public channels versus DMs only.

### Price history

| Price | What it was | Where it stands |
| --- | --- | --- |
| **$20/month** | Ad removal and nothing else | **Still the product on the shop.** Failed as a product. |
| **$12/month** | RelayOS Premium / RelayBNC. April 20 decision and the 6 April simulation. | Superseded in the June drafts. Not formally killed in Pavel’s checklist. |
| **$10/month** | “BDSMLR Premium” as a separate adult product for CCBill | Superseded. Website-feature billing was blocked. |
| **$18/month** | Bundle of $12 plus $10, “save $4” | Superseded with the two-product model. |
| **$5/month** | June 11 manager feedback plus Pavel’s ad correction | **Latest draft.** Unconfirmed for the company guide. |
| **$6/month** | Fallback if public sentiment turns | Contingency only. Not a price. |
| $8–12 / $25 / $50–100 and $10 / $20 / $30 | Viewer, creator, and pro tiers in February–March | Superseded. |

Silver $9.99 / Gold $19.99 / Platinum $49.99 in `08_WordPress_Projects` is a generic greenfield draft. The prices in `05_Creative_Strategies` (levels, season passes, room ownership) were not adopted.

### Why the $20 product failed

From the March 2026 data pull. The $3,600 ad column is that study’s monthly ad figure, not the later dashboard.

| Month | Premium revenue | Orders in the 7 Oct draft | Ad revenue used in the study |
| --- | ---: | ---: | ---: |
| Sep 2025 | $3,035 | 139 | $3,600 |
| Oct 2025 | $3,123 | 142 | $3,600 |
| Nov 2025 | $1,812 | 83 | $3,600 |
| Dec 2025 | $2,023 | 72 | $3,600 |
| Jan 2026 | $1,100 | 48 | $3,600 |
| Feb 2026 | $850 | 35 | $3,600 |

`04_Data_Analytics\bdsmlr_shop_stats.csv` matches the revenue. October in the CSV is **122 orders and 143 items**, not 142 orders. Premium fell about **72%** across that window. The longer read of the product was about **84% monthly churn** and about **1.2 months** of subscriber life. Even in December 2025, when the site was up, monthly churn was about **68%** (one write-up says 67.8%). Conversion on the order of **0.009%**. The March study projected the product to $0 by May 2026 if nothing changed. It did not go to zero — the shop was still the healthiest BDSMLR line in August — but it was still the old product. Chargebacks on that specific product were low, and PayPal had not challenged it.

## Payments and compliance

This is an operating summary, not a legal conclusion.

| Path | Where it stood in these files |
| --- | --- |
| PayPal on shop.bdsmlr.com | Live for the old ad-free subscription. |
| CCBill | `COMPLIANCE_ROADMAP.md` (1 May 2026) says **CCBill rejected** BDSMLR, and that billing website features with a major processor was not possible until a **12–18 month** compliance program. Pavel’s 7 October draft is more cautious: applied, they could not tell what the site was selling, they asked for six months of financials, and they treated the new model as a proof of concept. Neither document is an approval. |
| Stripe | Not tried, as of the chats behind the October draft. Considered only if the sold product is a plain IRC client and chat domains stay out of search indexes. |
| Epoch, SegPay, Paxum, crypto | Named in the February processor survey and the May framing notes. The superseded PHP module calls a Paxum webhook. Not a chosen live processor for the new product. |

On **10 April 2026**, TheMunch’s direction was to stop more billing strategies until Pavel had actually talked to the processors. Contact CCBill for adult sites, and Stripe and PayPal for an IRC SaaS. Copyright and CSAM are the objection a processor can make immediately.

The adult-versus-mainstream split was **still unsettled on purpose** in the October draft. Selling “BDSMLR Premium” makes the adult-processor path clearer and the compliance work heavier. Selling a neutral IRC subscription makes PayPal or Stripe thinkable, and makes a user complaint that reveals the adult sites a serious risk.

`PAYMENT_PROCESSOR_12_REQUIREMENTS_V2.md` scores the 12 adult-merchant rules as 8 covered, 2 not covered, 1 partial, 2 not applicable. Gaps: **uploader identity verification** (not covered), **visitor age check** (not covered), **moderation before publish** (partial — a CSAM scan exists and runs after publish). Covered at a policy level: uploader agreement, no child-exploitation or non-consent positioning, complaint handling within 5 business days, depicted-person removal appeals, anti-trafficking policy, and a way for scheme reviewers to see paywalled content. Live streaming and AI-content rules are marked not applicable.

## What users have been told

Two different communication tracks exist. Do not treat them as one launch.

**November 2025 user pack** (`User_Documentation`, ticket DEVB-1870, marked ready for review, publication unconfirmed). It tells users nothing is lost, credentials still work, premium continues, and there is no planned price change. It describes current premium as ad-free browsing, early access, enhanced customization, priority support, and extended upload limits. That matches the **old** premium. It conflicts with the 2026 redesign.

**WordPress migration comms** (`08_WordPress_Projects`, DEVB-1674, version 1.0, dates blank). Premium users first, in a sandbox preview. Channels: site blog, homepage banner, update box. Feedback address: support@bdsmlr.com. No direct email. Preview data is temporary and will be wiped. The “preview ends” post still has blank dates.

**2026 subscription sequence** (drafts in `BDSMLR_Monetization_Plan`):

| Post | Intent |
| --- | --- |
| 1, about six weeks out | Messaging rebuild. A liberal free quota. Subscriber tools. |
| 2, about four weeks out | What the user will see. |
| 3, about two weeks out | Migration starts soon. Support at support.bdsmlr.com. |
| 4 | Concrete free versus subscriber URLs on `api-prod.bdsmlr.com`, including silent fallbacks such as `?sort=popular` falling back to newest. |
| 5, “what’s landed since June” | Messaging infrastructure is ready and **the switch has not been flipped**. Subscription UI is not done. Discovery tools are live for testing and not properly gated. Private-blog posting is ready and off. The aim was the end of July, with no committed date. |

`BLOGPOST_HISTORY_BDSMLR.md` reads as a direction post that already went out: api-prod work has landed; the direction is subscription-backed and less ad-funded; privacy fixes stay free; actively posting private blogs are the paid surface; a Contributor badge is live; an Early Supporter badge is in development for people who paid or start supporting before **2027-01-01 00:00:00 UTC**.

There is **no confirmed email list**. Ezra must be briefed before a monetization post. The tone in the plans is anti-spam and technically honest (the old messaging was flaky), not “pay to remove ads.” A sentiment rule in the May verdict — adjust above 30% negative, offer $6/month if there is backlash, return to free above 50% negative — is a plan, not a launched process.

The older Jira epic (`01_BDSMLR_Migration`, 14 weeks, 7 sprints) includes “hide ads for premium members.” That is the **old** ad rule. The June rule is that every logged-in user is ad-free.

**October 2026 actual state**, from the company guide: the new BDSMLR is only partly live. The site is still a hybrid. The new experience has substantially less advertising and does not promote premium as well as the old one. A recommendation engine Allen and Akira were building for logged-out visitors overloaded in live testing and needs review before the next step. Pavel does not own the engine. He owns the effect on ad impressions if logged-out browsing gets better, and which of those tools sit behind a paywall.

## Go-to-market that is actually in use

- Run Revive on IsexyChat and BDSMLR. Read ISC first. The August keep-list is ReactAds / TP Media, GSM, 4thWhale, Chaturbate, Technius / Stripchat, and StripCash.
- On BDSMLR, keep the shop as a real line, offer inventory to the ISC winners, and put anonymous interstitials and tabunders on the new site when Simon is ready. Do not A/B test the ad strategy.
- User-facing channels for a future subscription are the blog, a homepage banner, and an update box.
- ISC chat ideas from 18 March 2026 were not launched: bump people who match the gender choice in the funnel, gender-matched chatbots, and short interstitials on actions such as a direct message. Gender-filtered pages engaged about 3–5 times the average (10.3 and 16.3 seconds versus 3.1). Day-1 return was 1.5%. Scale behind that study: about 4.9 million users in 13 months.

B2B in the April model means **future external networks** paying RelayOS for hosted IRC plus WordPress. bb.chat and BDSMLR are internal tenants, not customers. API prices of $500–$5,000 a month and white-label prices of $2,000–$50,000 a month in `06_Implementation_Plans` belong to the superseded plan.

## Financial picture

Melissa’s books are the financial record. The build below is an Ad Ops view.

### Ad Ops P&L, generated 27 July 2026

Source: `PnL\Forward_Handle_PnL_Executive_Summary.md`. Period: January 2025–July 2026 (19 months). July 2026 stops on the 23rd.

| | Amount | Share |
| --- | ---: | ---: |
| ISC advertising | $751,669.75 | 95.3% |
| BDSMLR PayPal ecommerce | $36,847.06 | 4.7% |
| Combined revenue | $788,516.81 | |
| Expenses then recorded | $107,143.29 | |
| Net in that build | $681,373.52 | |

**Do not repeat the 86% margin.** Expense rows stop around July 2025. Later months are revenue-only, so profit is overstated. BDSMLR display advertising is not in this build. In the same file, BDSMLR revenue $36,847 against expenses $71,301 is a net of about −$34,454, and ISC’s net is about $716k, using allocations that put most development cost on BDSMLR.

**2025 revenue in that P&L:** Jan $32,243, Feb $28,043, Mar $31,021, Apr $30,941, May $31,787, Jun $30,386, Jul $31,432, Aug $33,115, Sep $30,802, Oct $31,752, Nov $29,365, Dec $34,000. Year total **$374,885.29**.

**2026 dashboard revenue in that P&L:** Jan $33,512.31, Feb $29,997.65, Mar $35,507.63, Apr $45,275.20, May $52,535.80 (highest month in the series), Jun $46,349.10, Jul 1–23 $30,951.72. Year-to-date in the file **$274,129.41**.

Allocations used there: Simon Murray 90% BDSMLR / 10% ISC; Ezra Arrogante 100% BDSMLR; Rotchilda Antigua 50/50; Akira Wu 100% BDSMLR; Rigela Miranda 25% BDSMLR / 75% ISC; Pavel Zhuravel 10% BDSMLR / 90% ISC. Infrastructure “Cloud & Services” was about $5,000 a month, allocated 60% BDSMLR / 40% ISC. A July 2025 QuickBooks proposal (FWDAD-324) adds classes Advertising, Subscriptions, and AI Services. AI Services had no activity in the July 2026 P&L.

Network totals for the same 2025–2026 window, with ReactAds and TP Media split: GSM $251,210; ReactAds $178,785; GAM-TPMedia $131,044; 4thWhale $114,346; GAM-4thWhale $78,484; Chaturbate $58,269; Technius / StripChat $20,569; StripCash $17,221; AWEmpire $5,717.

### Dashboard versus the accountant, same week

| Month 2026 | Accountant | ISC dashboard |
| --- | ---: | ---: |
| March | $16,619 | $35,508 |
| April | $34,167 | $45,275 |
| May | $25,983 | $52,536 |
| June | $44,219 | $46,349 |
| July | $31,349 | $41,718 projected for a full month |

The gap was not explained. Dashboard figures are gross advertising. The accountant’s figures may be deposits, fees, or timing. **Do not put both into an owner update as if they were the same number.** Which series Melissa should use is unconfirmed.

Pavel’s email the same week recommended about **$45,000 a month** for August–December 2026, range $44,000–$47,000, from the dashboard rather than from her deposit list. The detailed path totals **$227,947** for those five months, at about $1,490 a day. The later 90-day average in the August rating is **$1,599 a day**, above that July planning rate. A full-year 2026 sketch of $512,842 is in the same projection file. It is a sketch.

July 2026 now has three figures in the files: P&L partial through the 23rd **$30,951.72**; a full-month projection of **$41,718**; the August rating bar, rounded, **about $52k**. Use the exact P&L when citing July, and say it is partial.

### Figures that are not targets

Kept here so a later reader does not promote them into a forecast.

| Source | Figure | Why it stays out of the owner update |
| --- | --- | --- |
| March 16 strategy | Year-1 $3.39 million, including ads at $0.30 CPM | Labeled against a “current $54k/year” that is not the ISC book. |
| March 18 Option B | $50k/month versus a $2k/month trap | Simulation. Pavel excluded it. |
| April 6 v5 | $12–20k/month, 850–1,590 subscribers | Superseded planning case. |
| May 21 verdict | Likely ~$34k then ~$44k; “perfect storm” $193,800; expected value $41,400 | Conditions (6-week comms, 2 weeks of load testing, Allen’s daily standups) were not completed. |
| ISC chat scenarios | $3,640 / $13,104 / $19,656 a month | Only if retention is fixed. Not launched. |
| `08_WordPress_Projects\pnl-analysis.md` | Month-1 revenue $130 | Hypothetical chat site, not FWD actuals. |

## Decision log

| Date | Who | Decision | Status |
| --- | --- | --- | --- |
| 18 Feb 2026 | Early plan | Creator paywall, CCBill or Epoch, per-post purchases | Superseded. The PHP module and the blank 12-week tracker still match this plan. |
| 16–18 Mar 2026 | Data project | Do not sell ad removal. The $20 product’s churn and conversion are the numbers above. | The data stands. The $50k target does not. |
| 18 Mar 2026 | Pavel | ISC chat subscription ideas | Not launched. |
| 26 Mar 2026 | Simulation series | bb.chat as a payment buffer | A step on the way to the April model, not the final product. |
| 6 Apr 2026 | Simulation v5 | One RelayOS IRC subscription at $12. BDSMLR perks in a later phase. | Revised on 20 April and again in June. |
| 10 Apr 2026 | TheMunch | Stop billing plans until processors are actually contacted. | The stop was real. His free-versus-paid feature sketch (post queue, 90-day search) was replaced by the June matrices. |
| 20 Apr 2026 | Pavel, Allen, Simon | Full migration. Separate tenant databases. Shop database is billing only. No cross-tenant chat. B2C at $12. Primary opportunity is anonymous ads. | **The decision Pavel still cites.** |
| 1 May 2026 | Compliance note | CCBill rejected. 12–18 months to bill the adult site itself. | Blocks selling BDSMLR as the adult product. |
| 8 May 2026 | Allen, Pavel, Simon | Frame the sale as private IRC, not adult uploads. | Still the framing. Processor path not closed. |
| 14 May 2026 | `KEY_DECISIONS_STATUS.md` | Import active users only. Password bridge versus reset undecided. | Migration half superseded by 20 April. Password choice is not clearly re-closed. |
| 18 May 2026 | Stress test | Prefer lazy migration. | Not adopted. |
| 21 May 2026 | Dual-revenue verdict | Proceed with ads plus $12 subscriptions if comms, load tests, and Allen’s standups happen. | Conditions not completed. |
| 11 Jun 2026 | Manager feedback and Pavel | $5/month. Logged-in users see no ads. bb.chat history unlimited for everyone. | Latest tier draft. Price unconfirmed. |
| 27 Jul 2026 | Pavel | P&L and the $45k projection email | Ad Ops view, not the books. |
| 7 Oct 2026 | Pavel draft | Company-guide insert. Eleven items still marked for him to confirm. | Current operating narrative, with those blanks. |

## What is built, and what is not

**In the product:** ISC ads. BDSMLR remnant ads and the PayPal shop. A hybrid BDSMLR. Some api-prod discovery, search, recommendations, and the contributor badge. The GA logged-in parameter. A messaging stack that blog post 5 says is ready and switched off.

**Not launched:** the $5 or $12 subscription, quota enforcement, the upgrade UI, the private-blog posting lock, the full move off the old system, anonymous interstitials on the new BDSMLR at ISC strength, and a processor approval for the new product. FWD 101 in October still describes monetization on the new BDSMLR as unfinished work for Simon and Pavel.

`06_Implementation_Plans\PROGRESS_TRACKER.md` is a 12-week tracker for the superseded Gumroad-then-API plan. The start date is blank. Every box is unchecked. The 22 May 2026 Jira-style work plan says entitlement, offline messaging, and migration are POC or design, with implementation pending.

## Open commercial checklist

From the 7 October draft, still unanswered in the files:

1. Books versus dashboard: which monthly total the owner update uses, and what the gap is.
2. Price: $5, $12, or not set. Whether the guide should mention the dead $20 product.
3. One sentence on PayPal, CCBill, and Stripe as of this month, and whether Adam should see it.
4. Whether shop revenue is “advertising,” “subscriptions,” or its own line when Sakura reads the update.
5. Anything in the August revenue picture that October has already changed.
