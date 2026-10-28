# Advertising and revenue — draft for the 10 November owner update

Prepared 28 October 2026 for Sakura. Rotchilda gathers the full note. This is the advertising section.

**This is not the final.** The sheets do not yet contain a closed October. The figures below are 1–26 October against the same 26 days of September, and against 1–26 October 2025. 27 October is in the sheet and is not reconciled. 28 October is a partial day. 29–31 October are not closed. Refresh this section after 31 October, and before the note goes out on 10 November.

The number in this section is the property sheet: delivery valued at the deal, or at the partner figure already entered. It is not cash. Melissa’s deposits are not in this draft.

## Revenue

Company sheet total, 1–26 October: **$40,819**. Same 26 days in September: **$44,776**, down **$3,958 (−8.8%)**. Same 26 days in October 2025: **$30,695**, up **$10,123 (+33%)**.

| | 1–26 Oct 2026 | 1–26 Sep 2026 | 1–26 Oct 2025 |
| --- | ---: | ---: | ---: |
| iSexyChat | $39,957 | $43,562 | $26,697 |
| BDSMLR, of which shop | $862, shop $643 | $1,214, shop $948 | $3,999, shop split not read |
| BDSMLR advertising and affiliate | $219 | $265 | not split in this pull |
| Company | $40,819 | $44,776 | $30,695 |

iSexyChat is 98% of the company month. About $3,368 of the iSexyChat total is the India slice. The rest is the main property.

iSexyChat, 1–26 October, by the lines that carry it:

| Line | Amount | Share |
| --- | ---: | ---: |
| GSM | $19,547 | 49% |
| React Ads | $9,946 | 25% |
| 4th Whale | $4,787 | 12% |
| Technius | $1,386 | 3% |
| Smaller partners and affiliate already in the sheet | $4,291 | 11% |

There is no separate subscription line. On BDSMLR the paid product in the sheet is the shop. A visit-to-purchase rate is not in this draft.

Sources: [iSexyChat Dashboard Stats](https://docs.google.com/spreadsheets/d/1G5znkOZx1a0OT_AQOeXQjGtq4xLDiR4FRmxt30Nj2po), tab GDS_All. [BDSMLR Dashboard Stats](https://docs.google.com/spreadsheets/d/1htvMiz5C9kWfEmmndn4wRoKDzFss2298YebjEr0LkTg), tab GDS_All, shop column. Cash: not read. Ask Melissa.

## What moved the number

**Confirmed.** iSexyChat organic sessions in GA4 were 619,667 for 1–27 October, against 681,076 for 1–27 September (−9%). Direct was slightly higher. Page views moved with sessions. The sheet moved by about the same amount as search traffic.

**Confirmed, and separate from that traffic change.** The React Ads chat tabunder in Revive was delivering about 35,000–45,000 impressions a day through 19 October, and about 14,000–22,000 from 21 October. Requests fell with impressions. The slots that were requested were still filled (842,210 impressions on 848,398 requests for 1–27 October). This is a smaller audience for that format, not empty inventory.

**Confirmed.** On the days that reconcile, the sheet prices that tabunder near $10 per thousand. Example: 42,213 Revive impressions appear in the sheet as $422.13. Revive’s own revenue field on the same advertiser is a calculated yield near $4 and is not the figure in this note.

**Hypothesis.** The early-October company dip versus September is mostly fewer iSexyChat search visits, plus the React Ads volume drop from 21 October. Those are two different movements. The search decline does not explain a halving of one format.

**Confirmed.** BDSMLR sessions did not fall. GA4 shows about 976,000 sessions for 1–27 October against about 952,000 for 1–27 September, mostly direct. The sheet still fell, and the shop is most of that fall ($643 against $948). Advertising on the BDSMLR sheet is about $8 a day.

**Hypothesis.** BDSMLR’s year-over-year drop (the sheet was $3,999 for the same 26 days of October 2025) is the smaller ad inventory on the new experience and a smaller shop, not fewer arrivals this month. How much of October 2025 was shop rather than display was not split in this pull, so the year-over-year mix is unverified.

**Unverified.** Whether every October revenue-share statement is already in the “smaller partners” line. Whether GA4 in October 2025 counted sessions the same way as now. BDSMLR page views per session are much higher than October 2025; that may be the new site’s counting, not deeper use.

Sources: GA4, iSexyChat and bdsmlr.com, 1–27 October against 1–27 September and 1–27 October 2025. Revive, publisher IsexyChat, advertiser “IsexyChat ReactAds Chat Tabunder (Contract updated 10.02.2026)”, daily impressions 1–28 October.

## What changed

- The React Ads tabunder record in Revive carries the label “Contract updated 10.02.2026”. The date order in that label is not confirmed. The volume change that is confirmed is 21 October, not 2 October. [Revive, that advertiser.](https://fwd.atlassian.net/browse/DEVB-2604) is related work, not proof of the cause: “Confirm and populate tab under ad inventory on ISC homepage”, Marko, Done 27 October.
- Interstitial test on the product side was closed earlier: [DEVB-2673](https://fwd.atlassian.net/browse/DEVB-2673), Done 15 September. Logged-out advertising-versus-engagement test is still in testing: [DEVB-2669](https://fwd.atlassian.net/browse/DEVB-2669).
- Premium bugs on BDSMLR that were blocking paid features were closed in September: [DEVB-2643](https://fwd.atlassian.net/browse/DEVB-2643), [DEVB-2703](https://fwd.atlassian.net/browse/DEVB-2703).
- No FWD AdOps ticket was updated in October. The commercial changes above are in Revive and in Development, not in the AdOps project.

## BDSMLR monetization

Ads for people who are not logged in, and the shop, are both still in the sheet. The shop is the paid product. Display is a thin remainder: Technius and a few other tags, a few dollars a day.

Revive, 1 September–27 October, shows the impression volume on BDSMLR as Technius, Oxy-Shop, and the Kinky Dollars tabunder. Revive revenue on those advertisers is blank. That blank is expected for tags whose money is entered from a statement or not at all. It is not the shop. The shop is the PayPal line in the BDSMLR sheet.

What the new experience still does not have, relative to a full advertising page, is the interstitial and the denser zone set the old pages carried. The work that would add measurement, not the zones themselves:

- [DEVB-2592](https://fwd.atlassian.net/browse/DEVB-2592) GA4 events for the new site, Done.
- [DEVB-2683](https://fwd.atlassian.net/browse/DEVB-2683) a post-viewed event, still In Progress.
- [DEVB-2594](https://fwd.atlassian.net/browse/DEVB-2594) Looker for those events, still In Progress, Pavel.
- [DEVB-2518](https://fwd.atlassian.net/browse/DEVB-2518) gradual paywall, still To Do.

Until the post-viewed event and the shop are in the same report, “a visit became a use, or a payment” cannot be read. Do not treat a session count as that.

## Risks

- **Concentration.** GSM, React Ads, and 4th Whale are 86% of iSexyChat for 1–26 October, and iSexyChat is 98% of the company sheet. A loss of GSM or React Ads is a company event.
- **React Ads volume.** From 21 October the tabunder is about half the impressions it had in the first three weeks. If that holds, November iSexyChat is lighter even if search traffic is flat.
- **Rate unverified.** The tabunder is labeled as a contract update. The sheet still books reconciled days near $10 per thousand. If the contract rate is no longer $10, October iSexyChat in this note is overstated. Pavel can check this with Marko before the note is sent. It becomes a decision for Sakura only if the rate actually changed.
- **27 October is incomplete.** The sheet shows React Ads at $12.62 that day. Revive still recorded about 18,500 tabunder impressions. Do not read $1,112 as that day’s result.
- **BDSMLR display** is about $8 a day. Losing it would not move the company month. The shop, at about $25 a day in this window, is the BDSMLR number that matters, and it is already down from September.
- **Cash and receivables** are Melissa’s. This draft does not say what has been paid.

## What to do

**Continue.** The iSexyChat mix. GSM, React Ads, and 4th Whale are the book. Search is still how that audience arrives, and it is still far above October 2025.

**Check before 7 November.** The React Ads contract rate against the $10 the sheet is using, and re-enter 27–31 October, including that tabunder. Success is a sheet day that matches Revive impressions times the confirmed rate. No benefit is claimed until that match exists.

**Watch, don’t cut.** The halved tabunder through the first week of November. Success is impressions back toward the early-October level, or a written reason they will stay near 15,000–20,000 a day. The tradeoff of waiting one week is small. The tradeoff of switching the format off is the 25% of iSexyChat that React Ads still is.

**Do not expect BDSMLR advertising to recover from traffic.** Sessions are already there. More display requires zones on the logged-out new experience, which is development work, not a partner change. Success would be the BDSMLR advertising line moving off about $8 a day, read on the sheet, without the shop falling further. The shop’s September-to-October drop should be looked at on its own. This draft does not have a conversion rate for it.

## Before 10 November, and what Sakura is asked to decide

1. **Close October.** Rigela and Pavel reconcile the sheets through 31 October, and the React Ads line for 27–31 October, before 7 November. This draft’s $40,819 is 26 days, not the month.
2. **Confirm the React Ads rate.** If it is still $10, no decision is needed. If it is not, bring Sakura the old rate, the new rate, and the effect on the October sheet. Proposed date: before the note is sent.
3. **No other approval.** Nothing in this draft asks Sakura to add a price, change a processor, or drop a partner.

**Decision needed from Sakura on this draft: none,** unless the rate check in item 2 comes back changed.
