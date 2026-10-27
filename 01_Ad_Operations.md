# Ad Operations

How advertising is run. Development keeps the sites up. This function turns the attention on those sites into revenue, and records it so the sheets and the owner update describe the same thing.

**Publishers in Revive:** IsexyChat (id 2543) for isexychat.com, BDSMLR (id 1980) for bdsmlr.com. The shop at shop.bdsmlr.com is PayPal. It is not a Revive advertiser and it does not go on the ISC sheet.

**Sheets:** ISC Dashboard Stats, daily from 2019. BDSMLR Dashboard Stats, daily from 2021, including the shop.

## 1. Decide whether the change is yours

When something looks wrong, or a partner asks for a placement, walk this before opening Revive.

1. Pavel sees it in the ISC sheet, the BDSMLR sheet, or Revive: a partner has stopped paying, a contract rate is wrong, a zone is empty, or the new BDSMLR is not showing a placement the old site showed.
2. If the fix is a campaign, a banner, a click URL, or a link between a banner and a zone, **Ad Ops changes it in Revive.** Marko can do this with Pavel. Development is not required.
3. If the site has to render a new placement, hide ads for logged-in users, or show a subscribe state, **stop and ask Simon.** The known example is porting the ISC interstitial onto the new BDSMLR for anonymous sessions only. Logged-in pages stay without ads.
4. After the change, Rigela records the outcome in the sheet that Looker and the owner update read. She does not copy Revive’s eCPM into a revenue cell.
5. Pavel reads the next days and weeks: impressions, fill, and revenue by partner. A tag that exists but does not deliver is not a live partner.

Revive’s API accepts only an allow-listed IP. The working host on the tailnet is named `adops`.

## 2. Weekly cycle

Read ISC before BDSMLR. ReactAds, GSM (Adnium), and 4thWhale move the month. A small partner does not.

1. Open the ISC sheet. Check ReactAds, GSM, and 4thWhale against the recent daily run. If one of them drops and the others do not, treat it as that partner, not as “the site.”
2. In Revive, open the campaigns that changed or that the sheet no longer matches. Check the creative size, the click URL, and whether the tag is delivering or only exists.
3. Update both sheets the same day you know the number.
   - **Direct CPM** (React Ads, Grand Slam Media / Adnium, 4th Whale, Stripchat / Technius): revenue = impressions ÷ 1,000 × the **contract** CPM. The only contract rate written down is React Ads tabunders at **$10**. If you do not have the contract rate in front of you, leave the row as volume and ask Pavel. Do not invent a rate from Revive’s eCPM.
   - **RevShare and affiliate:** enter the revenue the partner reported. If they have not reported yet, enter impressions only and leave revenue blank until they pay. Candy AI is the pattern: Revive can show hundreds of thousands of impressions and zero revenue, because the money is not in Revive.
4. Match Revive to the sheet. A partner can be serving in one and missing from the other. When that happens, write the name down. Do not unlink it in the same motion. The August review found OnlyFans, JoyOurSelf, and LiveSexAwards serving on ISC and absent from the sheet. Unlinking a dead name does not empty the zone, because the keep-list and those leftovers share the rotation.
5. If Simon shipped a login change, a layout change, or a new BDSMLR shell since the last check, re-read fill and revenue before you attribute a drop to a partner.
6. BDSMLR second. Split the sheet into shop versus display and affiliate before you conclude the property is up or down. The shop is its own line.
7. Once a month, assemble the owner section in §7. Do not put an unlaunched subscription forecast in it.

Marko’s hour-by-hour week and Rigela’s checklist are not written down beyond “Marko works in Revive” and “Rigela enters the sheets.” Until Pavel writes those, the cycle above is the job.

## 3. How to treat a partner

Score is not a feeling. In the rating files it is 100 × (that advertiser’s last 90 days ÷ the leader’s last 90 days). India splits roll into the parent. ReactAds means GAM-TPMedia plus ReactAds India.

### You may do this without Sakura

- Turn off a tag that is not paying.
- Move inventory toward a partner already under contract.
- Ask Simon for a placement or a tracking parameter.
- Draft the user-facing explanation. Brief Ezra before it goes up (§5 of Marketing).

### Bring this to Sakura first

Use the form in the company guide: what happened, why it matters, the options, the recommendation, and the decision you need.

- A new payment processor, or a change in what the receipt says the company sells.
- A price and a public paywall.
- Switching off ReactAds, GSM, or 4thWhale.
- Any change whose downside is a large share of the month.

No dollar threshold is written down. Until Pavel sets one, those four are the line.

### ISC book, as last written

Keep serving and keep entering: ReactAds / TP Media, GSM, 4thWhale, Chaturbate, Technius / Stripchat, StripCash. StripCash is on the sheet and is not a Revive advertiser on IsexyChat, so its money comes from the partner, not from a zone.

Do not spend time chasing: AWEmpire, Crak, CamBuilder, BongaCash, CamSoda.

Stop, or confirm they are already stopped: JuicyAds (payment was requested), Streamray, GSM India (the advertiser does not want Indian traffic), Flirt4Free, Lovense, WeVibe, TwinRed. Confirm in Revive before you tell anyone the cleanup is finished. The August notes analyzed it. They did not mark it done.

### BDSMLR book, as last written

Keep the shop, Technius, and Affiliatly (Oxy-Shop). Leave Exoclick in place only if it costs no time.

Do not add a new affiliate network. The next demand step is to **offer** BDSMLR inventory to GSM, ReactAds / TP Media, 4thWhale, and Chaturbate, if they will take the traffic. Record a yes or a no. Do not assume the offer was made.

When Simon is ready, put anonymous-user ads on the new experience in the formats ISC already runs: interstitials and tabunders, plus banners. Do not A/B test the advertising to decide this. Pavel rejected that test.

Blog orientation (gay, trans, straight, lesbian, other) is prepared data for a later match of interstitial and tabunder to the page. It is not a live targeting system. Do not describe it as one.

## 4. Record the money

| You have | You enter | You do not enter |
| --- | --- | --- |
| A direct CPM deal and an impression count | impressions ÷ 1,000 × contract CPM, on that property’s sheet | Revive eCPM, a rounded “about $10,” or another property’s rate |
| A revshare or affiliate statement | The partner’s revenue, on the day or month they report | A Revive revenue figure for that tag |
| Impressions and no statement yet | Volume only | A guessed dollar amount |
| Shop.bdsmlr.com | The BDSMLR sheet, as the shop, separate from display | Anything on the ISC sheet |
| A test campaign, an MCP test, or an internal tag | Leave it out of the revenue book | A row that looks like a partner |

Fill is the share of requests that received an ad. On ISC, fill is already essentially full, so an empty-request problem is not the diagnosis. On BDSMLR, fill is also high. The diagnosis there is demand: who will pay for the traffic. Empty desktop interstitial and desktop close-tabunder requests are the room where an ISC winner could be placed, after they agree.

After a layout or login change, a fall in impressions can be the placement, not the partner. Check the GA split in §6 before you renegotiate.

## 5. Logged-in tracking

Hand the code-level version to the developer: `ad data analysis\GA4-logged-in-tracking.md`. This is the sequence.

The site is bdsmlr.com. Container `GTM-WZKGN4B`. Measurement id `G-9VSP3HR9NF`. Property `bdsmlr.com PROD - GA4` (`properties/322459837`).

**Why.** Page views, ads, premium clicks, and outages have to split by whether the user was logged in at that moment. Without the parameter, the ad rule in the read-me cannot be checked.

**What the site sends.** On every page load, route change, login, logout, and custom event, the parameter `logged_in` is the string `"true"` or `"false"`. Not a boolean. Not `"unknown"`. If the state is unknown, fix the check. Do not send email, username, cookies, or account ids.

Reuse the same login check that already decides `interstitial_displayed` versus `interstitial_suppressed_login`. A second source of truth will make the reports lie.

1. Push `logged_in` into the dataLayer before GTM fires `page_view`. If auth is async, delay the first GA hit until the value is known. A follow-up event does not repair the unsplit page view.
2. On login, push `login_state_change` with `logged_in` `"true"`. On logout, push it with `"false"` immediately, including when the user stays on the same page.
3. On an in-app route change, push the current auth state, not the value from the first load.
4. In GTM, create a Data Layer variable named `logged_in` (`DLV - logged_in`, version 2). Put `logged_in` = `{{DLV - logged_in}}` on **every** tag that sends to `G-9VSP3HR9NF`, preferably through one Event Settings variable so a new tag cannot forget it. Publishing the container is required. Preview mode only affects your browser.
5. In GA4 Admin → Custom definitions, create dimension **Logged in**, scope **Event**, parameter `logged_in`. User scope will mix both states into one person. The dimension does not backfill.
6. Verify the same day in DebugView. Logged out in a private window: `page_view` and, if it shows, `interstitial_displayed` carry `"false"`. Signed in: the next `page_view` carries `"true"`. Log out without leaving: the next event is `"false"`. Stop if the parameter is missing, stuck, sent as a boolean, or the dimension is User-scoped.
7. Wait 24–48 hours before looking for the dimension in Looker. Do not use Looker as the acceptance test.

Ad events that must carry it: `revive_ad_pageload`, `revive_ad_refresh`, `interstitial_displayed`, `interstitial_suppressed_login`, `interstitial_suppressed_login_feed_landi`. Social events (`post_liked` and the rest) should almost always be `"true"`. `normal_login_button_click` should almost always be `"false"`.

`GA4_EVENT_TRACKING_SPECIFICATION.md` in the monetization folder is a future spec. Do not implement it in place of this list.

## 6. Read behavior in Looker

Click-path source: `ad data analysis\Looker-Studio-report-instructions.md`. Data source is GA4 **bdsmlr.com PROD**, not the Google Sheet. The sheet is the money. This report is behavior.

Login-split data starts **31 August 2026**. Social events start **31 July 2026**. Ignore `(not set)` when you compare logged in with logged out.

### Build it once

1. Resource → Manage added data sources → Edit the GA4 source → Refresh fields → confirm **LoggedIn** → Done.
2. File → Report settings → custom date range from 31 August 2026 to today.
3. Insert → Date range control, top-right, set to report-level.
4. Insert → Drop-down list on **LoggedIn**, report-level. Empty means everyone. `true` is logged in. `false` is logged out. Exclude `(not set)` if the control offers a filter.

### The pattern for every event card

Insert a scorecard. Metric: **Event count**. Filter that chart only: Event name equal to the exact event string. Do not put an Event name filter on the whole report. It breaks Users and Sessions.

Event name must match, including spaces and case (`proceed to checkout button click` starts with a lowercase p). If a chart says incompatible, you mixed Event name with Sessions. Use Event count for events, Sessions or Active users for traffic.

### Pages, in this order

1. **Traffic.** Active users, new users, sessions, engagement rate, and page views (`page_view`). A time series of users and sessions. A device pie. A country table sorted by sessions. Use the dropdown on this page for the login split.
2. **Logged in versus logged out.** Fixed cards, two filters each (LoggedIn and Event name), so the comparison does not depend on the dropdown. Logged-in column: page views, likes, reblogs, follows, comments. Logged-out column: page views, `interstitial_displayed`, `normal_login_button_click`. Under them, a time series of `page_view` broken down by LoggedIn.
3. **Social.** Likes, reblogs, unlikes, follows, unfollows, comments. These are almost only logged-in people.
4. **Ads.** This is the page Ad Ops uses after a placement change. Cards for `interstitial_displayed`, `interstitial_suppressed_login`, `interstitial_suppressed_login_feed_landi`, and `interstitial_suppressed_ab` if that event exists. Then `revive_ad_pageload`, `revive_ad_refresh`, `ad_empty_inventory`, `ad_sdk_blocked`, `ad_load_failed`. Time series for the three `ad_*` failures. **Do not put LoggedIn on `revive_ad_refresh`.** That event often has no login parameter. Page views and `ad_empty_inventory` can use the dropdown.
5. **Reliability, premium, login, and the event catalog** when the first four pages work. Premium clicks are small. Use bars, not a smooth line. Looker cannot show “the same person clicked premium, then checkout.” That funnel is GA4 Explore.

Empty usually means the date range starts before 31 August 2026, or the event did not fire. New versus returning is not logged in versus logged out.

The 7 October draft also describes Looker reports built from the **revenue sheets**. Those are a second family. Do not build them from this GA4 source, and do not read GA4 event counts as invoice dollars.

## 7. Monthly owner update

Rotchilda collects it. Pavel supplies a short section. Sakura should not have to open Revive, GA, or Looker.

1. ISC this month versus last month versus the same month last year, from the ISC sheet, plus one sentence on whether ReactAds, GSM, and 4thWhale are healthy.
2. BDSMLR this month as shop versus display and affiliate, from the BDSMLR sheet.
3. One sentence on what changed the number: a partner paused, a placement shipped or removed, a logging change, a processor conversation.
4. One risk. The standing risk is that two ISC partners are most of the company.
5. One recommendation, or “none.”
6. Decisions for Sakura, or “none.”

Say which figure is the sheet and which is Melissa’s deposits if they differ. They differed in every compared month of early 2026. Which of the two belongs in the pack is still Pavel’s to close. Do not publish both as if they were one number.

Advertising income in the books should be reconcilable to the two sheets. If it is not, the update says which one is cash and which one is delivery.

## 8. After you change something

| You did this | Check this next |
| --- | --- |
| Edited a banner or a zone link | The next day’s impressions for that campaign in Revive, then the sheet row if it is a CPM deal |
| Turned a tag off | That the zone is still filling from the partners you meant to keep, not from an untracked leftover you forgot |
| Asked Simon for a placement | `interstitial_displayed` versus `interstitial_suppressed_login`, then fill, then the sheet |
| Entered a revshare statement | That the month on the statement matches the month on the row |

Stop and re-check the login rule if logged-in sessions start showing `interstitial_displayed`, or logged-out sessions start showing `interstitial_suppressed_login`.
