# Ad Operations

**Lead:** Pavel  
**With him:** Marko (part-time, Revive; named contact on at least one live ISC account, Candy AI) and Rigela (data entry into the sheets)  
**Systems of record:** the ISC and BDSMLR Google Sheets for money; Revive for what was requested and what was shown  
**Newest narrative:** `101\FWD 101 - Pavel input - Advertising and Monetization.md` (draft, 7 October 2026, data through early September)  
**Newest ratings:** `ad data analysis\isc-advertiser-rating.html` (sheet through 18 August 2026) and `bdsmlr-advertiser-rating.html` (through 20 August 2026)

Revive eCPM is a calculated field. Invoices, the sheets, and the owner report use the **contract CPM** or the **partner’s statement**.

## How the ad business works

Forward Handle is the publisher. Advertisers pay to reach people on the sites. The ad server is **hosted Revive Adserver**.

| Payment type | How revenue is entered | Source |
| --- | --- | --- |
| CPM | impressions / 1000 × the contract rate | Sheet formula in `ad data analysis\batch_data.json` |
| RevShare | the partner’s reported revenue | Same formula. Candy AI on ISC is the example: hundreds of thousands of Revive impressions and $0 inside Revive. |
| Affiliate | same as RevShare | Same formula |

Direct CPM deals named for daily tracking: **React Ads, Grand Slam Media (Adnium / GSM), 4th Whale, Stripchat / Technius.** The only contract rate written in prose is **React Ads tabunders at $10 CPM** (July 2026 check, cited in the 7 October draft).

Ad Ops can change a campaign, a banner, a click URL, or a zone link in Revive without development. A new placement, hiding ads by login state, or porting the ISC interstitial onto the new BDSMLR needs Simon.

Revive’s API only accepts an allow-listed IP. An earlier MCP host on an old Tailscale machine was offline for weeks (found mid-May 2026). A tailnet host named `adops` was up and used in August 2026.

### Publishers

| Publisher | Revive id | Role |
| --- | --- | --- |
| IsexyChat | 2543 | ISC. Main income. |
| BDSMLR | 1980 | Display and affiliate on bdsmlr.com. |
| Staging | 4581 | No delivery in the 25 July–23 August 2026 window. |

Formats on ISC: **banners, tabs / tabunders, nav, buttons, interstitials.** A tabunder is an ad that opens in a new tab, usually when the current tab closes. FWD also calls the older version a popunder. An interstitial is a full-page ad between actions. ISC runs them. The new BDSMLR experience mostly does not, yet.

Sizes named on campaigns include 300×250, 728×90, and 320×50. Campaign names also split desktop, tablet, and mobile, and name placements (sidebar ATF, sidebar BTF, sticky, profile scroll, “kiwi” left side, main pages, button redirects). Those names are trafficking labels, not a written placement policy. 4thWhale ISC campaigns are further split by pair codes (`m4m`, `t4t`, `w4w`, `x4x`, and the cross pairs) plus an India set.

BDSMLR blog orientation labels (about 84,500 blogs: gay, trans, straight, lesbian, and a large “other”) exist and can later match interstitial and tabunder campaigns to the page. That targeting is prepared data, not a live system.

### Product rule for ads

**Anonymous visitors see ads. Logged-in users, free or paid, do not.** Pavel set this. Ad removal is therefore not a reason to subscribe. He rejected A/B testing the advertising as a way to choose the strategy. On 7 October 2026 he still asked himself to confirm that the rule stands on both the old and the new BDSMLR.

GA events already exist for `interstitial_displayed` and `interstitial_suppressed_login`. See Tracking below.

## ISC — the book that matters

**Measured.** Sheet from 1 January 2019 through 18 August 2026, rating HTML.

| Cut | Amount |
| --- | ---: |
| Lifetime | $2.76 million |
| Last 365 days | $455k |
| Last 90 days | $144k |
| 90-day daily average | $1,599 |

Revive zone fill in the 25 July–23 August 2026 window: **99.4%.** The 7 October draft adds about **46 million ad requests** in a recent 30-day window, with only a few hundred thousand unfilled. That request count is not repeated in the HTML KPIs. Empty requests are not the ISC problem.

### Last 90 days to about 18 August 2026

| Rank | Partner | 90 days | About $/day | Score | Notes |
| --- | --- | ---: | ---: | ---: | --- |
| 1 | ReactAds / TP Media | $54,536 | $606 | 100 | Lifetime $533,112. 365 days $139,132. |
| 2 | GSM (Adnium) | $52,273 | $581 | | 365 days $168,075. Lifetime $941,836. |
| 3 | 4thWhale | $18,404 | $204 | | Lifetime $628,869. |
| 4 | Chaturbate | $8,547 | $95 | | |
| 5 | Technius / Stripchat | $5,797 | $64 | | |
| 6 | StripCash | $3,045 | $34 | | On the sheet. **Not a Revive advertiser on IsexyChat.** |

ReactAds + GSM = **74%** of those 90 days. Score = 100 × (advertiser’s 90-day revenue / the leader’s). India splits roll into the parent. **ReactAds = GAM-TPMedia + ReactAds India.**

Rounded monthly bars in the same HTML (thousands, not exact dollars): Aug 2025 33, Sep 31, Oct 32, Nov 29, Dec 34, Jan 32, Feb 29, Mar 34, Apr 44, May 51, Jun 45, **Jul 52**, Aug 2026 **28** (18 days). July in this chart is not the same number as the 27 July P&L, which stops on 23 July at $30,951.72. See the financial chapter.

### Keep, test, stop

**Keep:** ReactAds / TP Media, GSM, 4thWhale, Chaturbate, Technius / Stripchat, StripCash.

**Test, do not chase:** AWEmpire ($1,071 in the 90 days), Crak ($74), CamBuilder ($113), BongaCash ($22), CamSoda (on the order of $1k per year).

**Stop or already stopped, from Pavel’s August notes.** Cleanup was analyzed. It had **not** been confirmed finished.

| Partner | Note |
| --- | --- |
| JuicyAds | Stopped. Payment has been requested. Last live 2025-08-09. Revive id 8989 still showed about 440k impressions in the rating window. |
| Streamray (all three) | Stopped. Advertiser is dead. Streamate ids 8824/8976 still showed about 1.23 million impressions in that window. |
| GSM India | Off the main mix. The advertiser does not want Indian traffic. Last live 2024-05-04. |
| Flirt4Free | Dead. |
| CamSoda | Almost dead. |
| Lovense, WeVibe, TwinRed | Can be removed or stopped. |
| Empty historic tabs | AshleyMadison, ToyDemon, Liberator, Wicked Temptations, AcmeJoy, TrafficStars, Crypto Chaturbate. |

### Tags that were serving and were not in the Google Sheet

In the 25 July–23 August 2026 Revive window, live but untracked names included JoyOurSelf (ids 8770/9221, 1.67 million impressions), OnlyFans (10792, 1.36 million), LiveSexAwards (8805, 1.34 million), CameraBoys (8863), Candy AI (16558, 338k), Allure AI (16559), plus smaller tags. Internal junk in the same pull: Test Campaigns 8767, MCP test 15425, Pavel&Hlib 15426.

Unlinking only the named kill list does **not** empty the zones. Shared rotations absorb the share. The rating says about **21%** of ISC opens only if both the kill list and the untracked list are unlinked. The 7 October draft calls the untracked leftover “about 15%.” Those are different cuts. A real shift toward ReactAds, GSM, and 4thWhale means deciding, partner by partner, what happens to OnlyFans, JoyOurSelf, LiveSexAwards, and the rest.

### What was actually linked (undated export)

`ISC_active_ad_links.csv` has **4,120** rows (4,089 banner, 18 interstitial, 13 tabunder). Unique by link: **1,775**. Last-7-day impressions in that file: banners 8,696,038, tabunder 832,800, interstitial 254,234. The file has no export date in the header. Do not treat those seven days as the same week as the 25 July–23 August rating. Top names in that file are 4thWhale CPM banners (including India), Technius Stripchat banners, a GSM CPM tabunder, Chaturbate, and a ReactAds chat tabunder whose campaign name says “Contract updated 10.02.2026” (330,595 impressions). That name does not state the $10 rate. Button redirects such as Candy AI are filed under `banner`.

## BDSMLR — remnant plus the shop

**Measured.** Sheet from 1 February 2021 through 20 August 2026.

| Cut | Amount |
| --- | ---: |
| Lifetime | $469k |
| 2021 | $99,311 |
| 2022 | $97,903 |
| 2023 | $98,793 |
| 2024 | $98,629 |
| 2025 | $56,540 |
| 2026 to 20 August | $17,605 (pace called about $27k for a full year) |
| Last 365 days | $38k |
| Last 90 days | $7.2k, about **$80/day** |

It used to be about **$98k a year**. TwinRed stopped in May 2025 (about $140,982 lifetime, ~30% of lifetime revenue). GrandSlam last went live on 2025-04-14 ($48,748). 2025 fell to about $57k.

Revive fill in late July–August 2026: **95.5%.** About 92k requests were already unfilled in 30 days, mostly desktop interstitial and desktop close-tabunder. The problem is **who will pay for the traffic**, not a shortage of slots.

### Last 90 days to 20 August 2026

| Line | 90 days | About $/day | Share of the story |
| --- | ---: | ---: | --- |
| BDSMLR Shop | $3,929 | $44 | Largest line. Lifetime $108,447. Not a Revive advertiser. |
| Technius | $2,051 | $23 | |
| Affiliatly (Oxy-Shop) | $963 | $11 | |
| Exoclick | $146 | $1.62 | Remnant. About $0.80/day in the last 30, and **0 Revive impressions** in that window. |
| Kinky Dollars | $94 | | Two paid days in the 90. Large impression share in Revive (about 312k / 21% of ~1.50 million advertiser impressions). |
| TrafficStars | $0.20 | | |

Shop + Technius + Affiliatly were **about 97%** of those 90 days.

**Keep the shop.** Treat it as its own line, not as ISC and not as a Revive advertiser. Offer BDSMLR inventory to the ISC winners (GSM, ReactAds / TP Media, 4thWhale, Chaturbate) if they will take the traffic. That offer is a recommendation. The files do not record that the partners said yes. ReactAds on BDSMLR died on 2022-11-29 ($12,993 lifetime). 4thWhale died on 2021-11-02. GSM is not in the live BDSMLR revenue mix. A small ReactAds test was quiet by late August: 216k impressions in the rating window (14%), but only **488 in the last 7 days of that window**. Candy AI on BDSMLR (Revive id 17919) was created and never given banners.

**Kill or already dead on BDSMLR:** TwinRed, GrandSlam (ids 4845/9412/13423 still had ~34k impressions), Streamray ALT/AFF, JuicyAds, ClickAdu, ADXAD, Awempire, Evadav, Ad-Maven, Sub-Shop, ClickAdilla, TrafficStars. Kill-list impressions were about 41k (~3%). Untracked was about 11k.

### Serving links (undated)

`BDSMLR_active_ad_links.csv`: **194** rows (153 banner, 1 interstitial, 40 tabunder). Unique: **71**. Last-7-day impressions: tabunder 151,610, interstitial 28,360, banner 9,197. Largest names: Oxy-Shop 62,054; Kinky Dollars tabunder 47,212; Technius 46,302; Reactads 28,821; GSM 893.

The rating’s “488 ReactAds impressions in the last 7 days” and this file’s “28,821” are **not the same week**. Do not merge them. Mid-August, the homepage interstitial that was actually filling was one ReactAds creative.

An older 90-day cut (`bdsmlr\bdsmlr_analysis.json`, 23 October 2025, range 18 July–15 October 2025) had the shop at $9,238.57 ($106.19/day). The shop was much hotter then than the August 2026 $44/day.

### What the new site is missing

The new BDSMLR experience has far fewer ads than the old one. When Simon is ready, anonymous sessions should get the formats ISC already runs: interstitials and tabunders, plus banners. Simon had said the ISC interstitial could be ported. Logged-in pages stay ad-free. Zone ids called out as Simon test zones: **13518** and **13524**.

Revive delivery for publisher 1980 from 1 September 2025 to 28 February 2026 (`04_Data_Analytics\bdsmlr_revive_stats.csv`) shows roughly 300k–430k requests a day, impressions almost equal to requests, CTR about 0.02–0.06%, conversions 0. Revenue and eCPM are blank. Do not sum that file into cash.

## The weekly loop

From the 7 October draft. Pavel still needs to confirm the week in his own words.

1. Read ISC first. ReactAds, GSM, and 4thWhale move the month. A small partner does not.
2. In Revive, check sizes, click URLs, and whether a tag is delivering or only exists.
3. Keep the two dashboards current. Direct-deal rows use the contract CPM. Revshare and affiliate rows use the partner’s reported revenue, or they stay volume-only until the partner pays.
4. Match what Revive is serving with what the sheet is paying. Partners can be live in one and invisible in the other. That mismatch was still true in August 2026.
5. When development changes login, layout, or the new BDSMLR shell, re-check fill and revenue. Those changes change impressions.
6. Prepare the figures Melissa and, monthly, Sakura need. Sakura should not have to open Revive, GA, or Looker.

### What goes in the monthly owner update

Rotchilda collects it. Suggested standing items:

1. ISC this month versus last month versus the same month last year, plus one sentence on ReactAds, GSM, and 4thWhale.
2. BDSMLR: shop versus display and affiliate. One sentence unless something broke.
3. What changed the number: a partner paused, a placement shipped or removed, a logging change, a processor conversation.
4. One risk. The structural one is concentration: two ISC partners are most of the company.
5. One recommendation, or none.
6. Decisions for Sakura, or none.

Do not put simulation ranges or unlaunched chat-subscription math in that update.

**Unconfirmed:** which day of the month the sheets are trustworthy, and whether Melissa’s deposit total or the dashboard total is the number in the pack. They were not the same number in July 2026. Advertising income in the books should be reconcilable to the two sheets. If it is not, the update should say which figure is cash and which is delivery.

### Decisions Pavel can make, and decisions that go to Sakura

Pavel can turn a non-paying tag off, move inventory toward a partner already under contract, ask Simon for a placement or a tracking parameter, and draft the user-facing post.

These go to Sakura in the form the company guide already asks for (what happened, why it matters, options, recommendation, what is needed):

- a new payment processor, or a change in what the receipt says the company sells
- a price and a public paywall on BDSMLR or RelayOS
- killing a partner that is still a meaningful share of ISC (ReactAds, GSM, 4thWhale)
- any plan whose downside is a large share of monthly revenue

No dollar threshold is written down. **Unconfirmed.**

Backup if Pavel is out is also **unconfirmed**. Marko can operate Revive. He is part-time. The dashboards and the network relationships sit with Pavel.

Finance allocation FWDAD-375 split Pavel **90% ISC / 10% BDSMLR** and Rigela **75% ISC / 25% BDSMLR**. That is an allocation, not a job description, and it is unconfirmed as still true. Marko’s weekly checklist and Rigela’s weekly checklist are not written down.

## Tracking

| System | What it is for |
| --- | --- |
| Revive, hosted | Campaigns, creatives, zones, requests, impressions. Not revshare cash. |
| ISC Dashboard Stats (Google Sheet) | Daily partner revenue from 2019. This is the ISC revenue book. |
| BDSMLR Dashboard Stats (Google Sheet) | Daily partner revenue from 2021, including the shop. |
| GA4 | Behavior, not invoices. |
| Looker Studio | Reports Pavel builds for himself. Not a system Sakura needs to open. |
| PayPal, shop.bdsmlr.com | The existing subscription checkout. |
| Jira project FWDAD | Monetization and tracking tasks that need development. |

The Google Cloud project still used for Sheets and GA is named `reblogme-2aa32`. That is an access key, not a live product.

### GA4 on BDSMLR

From `ad data analysis\GA4-logged-in-tracking.md`:

- Site bdsmlr.com, GTM **GTM-WZKGN4B**, measurement **G-9VSP3HR9NF**, property **bdsmlr.com PROD - GA4 (`properties/322459837`)**.
- Parameter `logged_in` is the string `"true"` or `"false"`. Event-scoped dimension name **Logged in**. It does not backfill.
- Ad events that must carry it: `revive_ad_pageload`, `revive_ad_refresh`, `interstitial_displayed`, `interstitial_suppressed_login`, `interstitial_suppressed_login_feed_landi`.
- A second property, **`328421085`**, was added in the same setup. The logged-in parameter was seen again in GA on **4 September 2026**.

`BDSMLR_Monetization_Plan\GA4_EVENT_TRACKING_SPECIFICATION.md` is a **future** spec (`ad_impression` times CPM, `user_tier`). It is not the live GTM list.

### Looker

`ad data analysis\Looker-Studio-report-instructions.md` is the click-path for a **GA4 behavior report**, source **bdsmlr.com PROD**, explicitly not the Google Sheet. Dimension **LoggedIn**. Login-split data starts **31 August 2026**. Social events from **31 July 2026**. The ads page covers interstitial shown and skipped, plus `revive_ad_pageload`, `revive_ad_refresh`, `ad_empty_inventory`, `ad_sdk_blocked`, and `ad_load_failed`. Do not put LoggedIn on `revive_ad_refresh` (it is often missing).

The 7 October draft also describes Looker reports built from the **revenue sheets**. That is a second family of reports. The September instructions are only the GA behavior report.

## Older numbers that must not be mixed in

| Source | Window | Why it is a different number |
| --- | --- | --- |
| `04_Data_Analytics\isc_network_analysis.json` | 9 July–7 October 2025 | GSM $34,829 ($383/day). A year before the August 2026 rating. |
| `PnL\ISC_Ad_Network_Performance_2025-2026.csv` | January 2025–July 2026 | ReactAds and TP Media are **separate columns**. Do not add TP Media on top of the August combined ReactAds figure. GSM $251,210 in that window. |
| `ROI\` methodology (15 September 2025, FWDAD-414) | Example month, July 2025 | GSM $9,690, ReactAds $7,475, 4th Whale $16,900, against an $8,000 infrastructure pool. A costing model. It does not match dashboard run-rates. Ten binary Revive `.xls` exports (1 September 2024–12 September 2025) were not opened. |
| Dual-revenue simulations | May 2026 | Hypothetical CPMs. Not delivery stats. |

## Open ad-ops checklist

Still open in the 7 October draft:

1. Which of the kill-list partners are actually off in Revive.
2. Untracked ISC tags (OnlyFans, JoyOurSelf, LiveSexAwards, and the rest): keep, ask for a rate, or remove.
3. Whether anyone has offered GSM, ReactAds, 4thWhale, or Chaturbate a BDSMLR placement.
4. Whether the logged-in ad rule still stands on both old and new BDSMLR.
5. Marko’s week, Rigela’s week, and the backup if Pavel is out.
6. The dollar or percent threshold that brings Sakura into an ad decision.
7. Whether anything in the August picture is wrong because October is not August.

## Revive tooling

The checked-in server in `Revive_mcp\revive_adserver_mcp` (README 0.1.0) is a local HTTP wrapper over Revive XML-RPC. The README lists campaign, banner, and zone create/read/update/delete, zone linking, zone tags, and a wide statistics catalog. The exported JavaScript is narrower: add and get for campaigns, banners, and zones; banner targeting; link and unlink; zone tags; and daily statistics for campaign, banner, and zone. Deletes and most cross-breakdowns are in the README and not in the exported JS.

The live Cursor connection `user-revive-adserver` is wider than that folder: agencies, advertisers, publishers, users, audit log, creative upload, the link and unlink calls, daily and cross statistics, and helpers such as `get_server_capabilities`, `get_account_summary`, and `link_zone_compatible_banners`. Deletes are permanent. Check server capabilities before assuming a failed delete was archived.
