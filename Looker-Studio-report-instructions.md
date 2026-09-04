# Looker Studio reports for bdsmlr (beginner guide)

Click-by-click instructions. One idea in Looker: **click a chart, then change it in the panel on the right.** You almost never type formulas.

Data source: GA4 **bdsmlr.com PROD**. Do not use the Google Sheet.

Login split dimension: **LoggedIn** (`true` / `false`). Data starts **31 August 2026**. Ignore `(not set)` when comparing logged in vs logged out.

---

## Words you will see

| Looker word | Meaning |
|---|---|
| **Dimension** | A label (Date, Event name, LoggedIn, Country) |
| **Metric** | A number (Event count, Active users, Sessions) |
| **Filter** | “Only show this event” or “only logged in” |
| **Scorecard** | One big number |
| **Time series** | A line or bar chart over days |
| **Control** | Date picker or dropdown at the top |

---

## Do this once (before any page)

Open your report (GA is already connected).

### 1. Refresh the data so LoggedIn appears

1. Top menu: **Resource → Manage added data sources**
2. Click **Edit** next to the GA4 source
3. Click **Refresh fields**
4. Confirm you see **LoggedIn**
5. Click **Done**, then close the list

### 2. Default dates

Login data only exists from 31 Aug 2026.

1. Top menu: **File → Report settings**
2. Data source: your GA4 property
3. Date range: **Custom** → start **31 August 2026**, end **Today**
4. Close settings

### 3. Date picker (works on every page)

1. Top menu: **Insert → Date range control**
2. Place it in the top-right
3. Click it → in the right panel, set it to **Report-level** (so it applies to all pages)

### 4. Logged in / logged out dropdown (works on every page)

1. **Insert → Control → Drop-down list**
2. Place it top-left, under the title
3. Click it
4. Dimension: **LoggedIn**
5. Make it **Report-level**
6. Optional: click the dropdown → **Setup → Filter** → Exclude LoggedIn **In** `(not set)` and (empty)

When the dropdown is empty, you see everyone. When you pick `true`, only logged in. `false` = logged out.

### 5. New page for each report

1. Bottom of the screen: **Add page** (or **Page → New page**)
2. Double-click the page name at the bottom and rename it (Traffic, Social, …)

---

## How to make a scorecard (repeat this a lot)

Example: number of likes.

1. **Insert → Scorecard**
2. Click the scorecard
3. Right panel → **Metric**: **Event count**
4. Right panel → **Filter → Add a filter**
   - Name: `Likes`
   - Include → **Event name** → **Equal to** → `post_liked`
   - Save
5. Click the title on the chart and type **Likes**

That is the whole pattern: **Event count + filter on Event name**.

**Do not** put an Event name filter on the whole report. It breaks Users and Sessions. Filter Event name **per chart**.

---

## Page 1 — Traffic

**What it shows:** is the site healthy?

Add these scorecards (**no Event name filter**, except page views):

| Title | Metric |
|---|---|
| Users | Active users |
| New users | New users |
| Sessions | Sessions |
| Engagement rate | Engagement rate |
| Page views | Event count, filter Event name = `page_view` |

**Trend line**

1. **Insert → Time series**
2. Dimension: **Date**
3. Metrics: **Active users** and **Sessions**

**Device pie**

1. **Insert → Pie chart**
2. Dimension: **Device category**
3. Metric: **Sessions**

**Countries table**

1. **Insert → Table**
2. Dimension: **Country**
3. Metrics: **Sessions**, **Active users**
4. Sort: Sessions, descending

Use the **LoggedIn** dropdown to compare logged in vs logged out on this same page.

---

## Page 2 — Logged in vs logged out

**What it shows:** the split you wanted.

Layout: two columns. You can also just use the dropdown on Page 1. This page is for **fixed** side-by-side numbers that do not depend on the dropdown.

### Left column — Logged in

For each scorecard:

- Metric: **Event count**
- **Two filters:**
  1. LoggedIn **Equal to** `true`
  2. Event name **Equal to** (see table)

| Title | Event name |
|---|---|
| Page views (in) | `page_view` |
| Likes | `post_liked` |
| Reblogs | `post_reblogged` |
| Follows | `blog_followed` |
| Comments | `comment_posted` |

### Right column — Logged out

Same, but LoggedIn = `false`:

| Title | Event name |
|---|---|
| Page views (out) | `page_view` |
| Interstitial shown | `interstitial_displayed` |
| Login button | `normal_login_button_click` |

### Line chart under both

1. Time series
2. Dimension: **Date**
3. Breakdown dimension: **LoggedIn**
4. Metric: **Event count**
5. Filter: Event name = `page_view`
6. Filter: LoggedIn **In** `true`, `false` (exclude `(not set)`)

You should see two lines: logged in vs logged out.

---

## Page 3 — Social

**What it shows:** likes, reblogs, follows (almost only logged-in people). Data from **31 Jul 2026**.

Scorecards, metric **Event count**, one filter each:

| Title | Event name |
|---|---|
| Likes | `post_liked` |
| Reblogs | `post_reblogged` |
| Unlikes | `post_unliked` |
| Follows | `blog_followed` |
| Unfollows | `blog_unfollowed` |
| Comments | `comment_posted` |

**Line chart**

1. Time series
2. Dimension: **Date**
3. Breakdown: **Event name**
4. Metric: **Event count**
5. Filter: Event name **In**  
   `post_liked`, `post_reblogged`, `post_unliked`, `blog_followed`, `blog_unfollowed`, `comment_posted`

Add a text box (**Insert → Text**):

> These actions are almost only from logged-in users. Data from 31 Jul 2026.

Skip blends (unlike rate) for now. The six numbers plus the chart are enough.

---

## Page 4 — Ads and interstitials

### Interstitial scorecards

Event count + Event name filter:

| Title | Event name |
|---|---|
| Interstitial shown | `interstitial_displayed` |
| Skipped (login) | `interstitial_suppressed_login` |
| Skipped (feed) | `interstitial_suppressed_login_feed_landi` |
| Skipped (AB) | `interstitial_suppressed_ab` |

If the last one is missing in the list, skip it.

**Time series:** Date, breakdown Event name, those names in an **In** filter.

### Ad scorecards

| Title | Event name |
|---|---|
| Ad pageload | `revive_ad_pageload` |
| Ad refresh | `revive_ad_refresh` |
| Empty inventory | `ad_empty_inventory` |
| SDK blocked | `ad_sdk_blocked` |
| Load failed | `ad_load_failed` |

**Time series** for the three `ad_*` events (empty / blocked / failed).

**Important:** do **not** add LoggedIn to the `revive_ad_refresh` chart. That event often has no login parameter. Page views and `ad_empty_inventory` can use the dropdown.

---

## Page 5 — Reliability (outages)

Scorecards:

| Title | Event name |
|---|---|
| Slow request | `outage_slow_request` |
| Config load failed | `outage_runtime_config_load_failed` |
| Retry exhausted | `outage_api_retry_exhausted` |
| Rate limited (429) | `outage_429_rate_limited` |
| Slow loading app | `slow_loading_app` |
| Media load failed | `media_load_failed` |

If a name is missing, skip that card. The event simply did not fire in your date range.

**Time series:** Date, breakdown Event name, those events in an **In** filter.

**Sessions underneath (no event filter):**  
Time series, Date, metric **Sessions** — so you can see if errors rise when traffic rises.

Better to watch errors **together with traffic**, not as raw counts alone (busy days create more errors).

---

## Page 6 — Premium and Web3

These numbers are **small** (often a few per day). Use **bars**, not a smooth line.

### Premium scorecards

| Title | Event name (type exactly) |
|---|---|
| Premium 1 month | `BDSML 1 month Premium click` |
| Community Support | `BDSMLR Premium Community Support` |
| Checkout | `proceed to checkout button click` |
| Coinbase | `Proceed to Coinbase button click` |

**Bar chart:** Dimension Event name, metric Event count, filter Event name **In** those four.

### Web3 scorecards

| Title | Event name |
|---|---|
| Web3 button | `web3_button_click` |
| MetaMask link | `metamask_link_click` |
| MetaMask Chrome | `metamask_for_chrome` |

LoggedIn dropdown works here.

Looker cannot do a true user funnel (same person clicked Premium **then** checkout). For that, use **GA4 Explore → Funnel**.

---

## Page 7 — Login, forms, search

| Title | Event name |
|---|---|
| Login button | `normal_login_button_click` |
| Form start | `form_start` |
| Form submit | `form_submit` |
| Search | `view_search_results` |

**Time series:** Date, breakdown Event name, those four in an **In** filter.

If **form submit** is close to **form start**, forms are healthy. If submit drops far below start, something is broken.

---

## Page 8 — All events (catalog)

1. **Insert → Table**
2. Dimension: **Event name**
3. Metrics: **Event count**, **Active users**
4. Filter: Event name **Does not equal** `(other)`
5. Sort: Event count, descending

This is your “did we get a new event?” page. You do not need a login split here.

Do not put `page_view` on the same stacked chart as likes. Core events are much larger and hide everything else.

---

## Page 9 — Moderation (optional)

| Title | Event name |
|---|---|
| User blocked | `user_blocked` |
| User unblocked | `user_unblocked` |
| Content reported | `content_reported` |
| Blog reported | `blog_reported` |

Table: Date + Event name, metric Event count.

For this page, set the date picker to **last 7 days** — monthly totals look empty.

---

## If a chart says “incompatible” or is empty

- You mixed **Event name** with a metric that does not like it. Use **Event count** for event charts, **Sessions** / **Active users** for traffic charts.
- Event name must match **exactly**, including spaces (`proceed to checkout button click` is lowercase `proceed`).
- Empty often means: wrong date range, or that event did not fire. Try last 7 days.
- **New vs returning** is not the same as logged in vs logged out.

---

## Suggested build order

1. Date picker + LoggedIn dropdown
2. Traffic
3. Social
4. Logged in vs logged out
5. Ads / interstitials
6. The rest when you have time

Start with **Traffic**. If Users and Sessions show numbers, the connection works and you can copy the scorecard method onto every other page.

---

## Related file

Developer tracking setup (already done): `GA4-logged-in-tracking.md`
