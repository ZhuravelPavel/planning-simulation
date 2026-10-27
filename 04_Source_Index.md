# Source index

Facts in the handbook were taken from these files. Code trees (`bdsmlr_relayos`, `relayos`, `monetization` PHP beyond its header) were not line-audited. Binary Revive exports in `ROI\` were not opened. W-8 forms in `payment data` were not read into the handbook.

Status words match the handbook: a file can be the record of a decision, a measurement, a draft, or a plan that a later file replaced.

## Company

| Path | What it is |
| --- | --- |
| `101\Forward Handle (FWD) 101.md` | October 2026 company guide for Sakura and Adam. Advertising section is still a stub asking Pavel to correct it. |
| `101\FWD 101 - Pavel input - Advertising and Monetization.md` | 7 October 2026 draft of that correction. Newest narrative of the ad business, the team, and the open checklist. Data through early September. |

## Ad operations

| Path | What it is |
| --- | --- |
| `ad data analysis\isc-advertiser-rating.html` | ISC keep / test / kill, 90-day, 365-day, and lifetime dollars, Revive ids, 99.4% fill. Sheet through 18 August 2026. |
| `ad data analysis\bdsmlr-advertiser-rating.html` | The same for BDSMLR, including the shop. 95.5% fill. Through 20 August 2026. |
| `ad data analysis\ISC_active_ad_links.csv` | 4,120 serving rows with banner ids and 7-day impressions. No export date. |
| `ad data analysis\ISC_active_ad_links_unique.csv` | Those links collapsed to 1,775 URLs. |
| `ad data analysis\BDSMLR_active_ad_links.csv` | 194 BDSMLR serving rows. Undated. |
| `ad data analysis\BDSMLR_active_ad_links_unique.csv` | 71 unique BDSMLR links. |
| `ad data analysis\batch_data.json` | Sheet formula: CPM, RevShare, Affiliate. |
| `ad data analysis\GA4-logged-in-tracking.md` | Live GTM and GA4 spec for the logged-in parameter and ad events. |
| `ad data analysis\Looker-Studio-report-instructions.md` | Click-path for the BDSMLR GA4 Looker report. |
| `ad data analysis\process_revive_data.ps1` | Helper that built the link extracts. Not a policy. |
| `04_Data_Analytics\ISC Dashboard Stats - GDS_All.csv` | Daily ISC sheet extract from 2019. Totals used here come from the later rating and the July P&L, not from a fresh sum of this file. |
| `04_Data_Analytics\isc_network_analysis.json` | 90-day ISC network totals as of 7 October 2025. Older than the August 2026 rating. |
| `04_Data_Analytics\ISC_Ad_Network_Dashboard.html` | Browser view of that October 2025 analysis. |
| `04_Data_Analytics\bdsmlr_revive_stats.csv` | Publisher 1980 daily requests and impressions, September 2025–February 2026. Revenue blank. |
| `04_Data_Analytics\bdsmlr_shop_stats.csv` | Monthly shop gross and order counts, September 2025–February 2026. |
| `bdsmlr\BDSMLR Dashboard Stats.csv` | Daily BDSMLR sheet. Totals used here come from the August 2026 rating. |
| `bdsmlr\bdsmlr_analysis.json` | 90-day BDSMLR totals as of 23 October 2025. |
| `Revive_mcp\revive_adserver_mcp\README.md` | Local MCP action catalog. Wider than the exported JavaScript. |
| `ROI\Marketing_ROI_Analysis_Methodology_Documentation.md` | September 2025 costing model (FWDAD-414). Example payments do not match the dashboard. |
| `ROI\FWDAD_413_Validation_Report.md` | Marks that ROI validation complete. |
| `ROI\Exported Statistics - Campaigns from 01-09-2024 to 12-09-2025*.xls` | Ten binary campaign exports. Not read. |

## Marketing, product, and money

| Path | What it is |
| --- | --- |
| `BDSMLR_Monetization_Plan\PRODUCT_DECISIONS_SUMMARY_20042026.md` | Record of the 20 April call: full migration, $12, no cross-tenant chat, anonymous ads. |
| `BDSMLR_Monetization_Plan\BDSMLR_TIER_MATRIX_V1.md` | 11 June draft. $5. Logged-in users see no ads. |
| `BDSMLR_Monetization_Plan\BB_CHAT_TIER_MATRIX_V2.md` | 11 June draft. Supersedes v1. |
| `BDSMLR_Monetization_Plan\BB_CHAT_TIER_MATRIX_V1.md` | 10 June draft. Superseded. |
| `BDSMLR_Monetization_Plan\bdsmlr_pricing_page.html` | Draft $0 / $5 page. |
| `BDSMLR_Monetization_Plan\bbchat_pricing_page.html` | Draft $0 / $5 page. |
| `BDSMLR_Monetization_Plan\relayos_pricing_page.html` | Draft neutral $5 page. Does not name BDSMLR perks. |
| `BDSMLR_Monetization_Plan\PRODUCT_FRAMING_STRATEGY.md` | 8 May framing: sell IRC, not adult uploads. |
| `BDSMLR_Monetization_Plan\COMPLIANCE_ROADMAP.md` | 1 May. CCBill rejected. 12–18 month path. |
| `BDSMLR_Monetization_Plan\PAYMENT_PROCESSOR_12_REQUIREMENTS_V2.md` | Which of the 12 adult-merchant rules are covered. |
| `BDSMLR_Monetization_Plan\MANAGER_APPROVAL_RESULTS.md` | 10 April. TheMunch stops planning until processors answer. |
| `BDSMLR_Monetization_Plan\THEMUNCH_FEEDBACK_RESPONSE.md` | 10 April feature sketch. Replaced by the June matrices. |
| `BDSMLR_Monetization_Plan\BLOGPOST_HISTORY_BDSMLR.md` | Direction post. Early-supporter cutoff 1 January 2027 UTC. |
| `BDSMLR_Monetization_Plan\BLOG_POST_1` through `BLOG_POST_5` | Draft launch sequence. Post 5 says the switch is not flipped. |
| `BDSMLR_Monetization_Plan\ACTION_PLAN_V2.md` | Superseded two-product $12 / $10 / $18 model. |
| `BDSMLR_Monetization_Plan\KEY_DECISIONS_STATUS.md` | 14 May. Partly superseded. Password choice still open there. |
| `BDSMLR_Monetization_Plan\KEY_DECISIONS_STATUS_V2.md` | Pre-decision note favoring lazy migration and $12. |
| `BDSMLR_Monetization_Plan\DUAL_REVENUE_STRATEGY_FINAL_VERDICT.md` | 21 May simulation. Not a target. |
| `BDSMLR_Monetization_Plan\ALLEN_PROPOSAL_FINAL_VERDICT.md` | 18 May. Recommends lazy migration. Not adopted. |
| `BDSMLR_Monetization_Plan\DUAL_REVENUE_JIRA_WORK_PLAN_22052026.md` | 22 May. Build still pending past POC. Includes the BDSMLR SEO story. |
| `BDSMLR_Monetization_Plan\GA4_EVENT_TRACKING_SPECIFICATION.md` | Future event spec. Not the live tag list. |
| `BDSMLR_Data_Collection\1_FINAL_DELIVERABLES\EXECUTIVE_SUMMARY_OPTION_B.md` | 18 March. The $20 product’s churn. The $50k figure is a simulation. |
| `PnL\Forward_Handle_PnL_Executive_Summary.md` | 27 July 2026 Ad Ops P&L. Margin is not safe to repeat. |
| `PnL\ISC_Ad_Network_Performance_2025-2026.csv` | Network sums for that window. ReactAds and TP Media are split. |
| `PnL\Revenue_Projections_Summary_Accountant.md` | Dashboard versus accountant, and the $45k baseline. |
| `PnL\Accountant_Email_Revenue_Projections.txt` | The August–December 2026 email. |
| `PnL\Revenue_Categorization_Structure_Proposal.txt` | July 2025 QuickBooks classes. FWDAD-324. |
| `PnL\Expense_Categorization_Summary.md` | Revive vendor tagged to ISC only. Understates BDSMLR, which is also a publisher. |
| `ISC_Chat_Monetization_Plan\ANALYSIS_SUMMARY.md` | 18 March exploration. 1.5% day-1 return. Not launched. |
| `User_Documentation\` | 7 November 2025 user pack. DEVB-1870. Describes the old premium. |
| `08_WordPress_Projects\WordPress Migration Communication Plan.md` | DEVB-1674 preview comms. Dates blank. |
| `01_BDSMLR_Migration\BDSMLR_Migration_Epic_Structure.txt` | 14-week epic, including the older “hide ads for premium” rule. |
| `02_BDSMLR_Monetization\` | 18 February creator-platform plan. Superseded. |
| `06_Implementation_Plans\` | Tracker and B2B prices for that same plan. Boxes unchecked. |
| `05_Creative_Strategies\creative-monetization-strategies.md` | Unadopted idea list. |
| `08_WordPress_Projects\wordpress-adult-chat-monetization-plan.md` | Generic Silver / Gold / Platinum draft. Not the live model. |
| `monetization\init.php` | PHP v1.0.0 for the superseded creator paywall. |

## SEO

| Path | What it is |
| --- | --- |
| `ISC SEO\isexychat.com-Performance-on-Search-2026-10-26\isexychat-seo-status.md` | 26 October performance brief and the repair plan. |
| `ISC SEO\isexychat.com-Performance-on-Search-2026-10-26\*.csv` | Search Console, GA4 channels, and Ahrefs exports behind that brief. |
| `ISC SEO\START_HERE.md` | 10 August gap note. Still says there is no AI page. |
| `ISC SEO\GLOBAL_ENGLISH_Keywords_Report.md` | Full English gap and a technical checklist. |
| `ISC SEO\missing_keywords_GLOBAL_ENGLISH.csv` | The 1,198-keyword list. |
| `ISC SEO\FINAL_REPORT.md` | Same-day crawl-aware gap. Admits `/ai-chat/` exists. Six priority URLs. |
| `ISC SEO\FINAL_missing_pages_report.csv` | Those six URLs. |
| `ISC SEO\internal_all.csv` | Internal crawl, 10 August 2026. |
| `ISC SEO\PAGES_TO_CREATE.md`, `MISSING_PAGE_CATEGORIES.md`, `REFINED_Analysis_With_Existing_Rooms.md` | Earlier August drafts. Superseded where they deny the AI page. |
| `ISC SEO\AI_CHAT_PAGE_ANALYSIS.md` | On-page gaps for `/ai-chat/`. |
| `ISC SEO\IMPLEMENTATION_GUIDE.md` | How to ship the rewrite. |
| `ISC SEO\AI_SEX_CHAT_OPTIMIZED_CONTENT.md` | Proposed replacement copy. |
| `ISC SEO\isexychat.com-Performance-on-Search-2026-08-10\` | Search Console for `/ai-chat/` only, last 16 months. |
| `IRC_chat_SEO\SEO_STRATEGY_PHASE1_FOUNDATION.md` | RelayOS pre-launch SEO, 20 April 2026. |
| `IRC_chat_SEO\SEO_STRATEGY_PHASE2_GROWTH.md` | Months 1–24. Internal targets disagree. |
| `IRC_chat_SEO\SEO_GANTT_CHART.md` | 24-month Gantt. Launch marked 20 July 2026. |
| `IRC_chat_SEO\google_us_irc-chat_matching-terms_2026-04-20_13-09-54.csv` | US Ahrefs IRC terms. |
| `IRC_chat_SEO\KC.csv` | Keyword and volume extract. |
| `Reviews\` | Affiliate and product drafts, October 2025–January 2026. |
| `ISC AI chats\` | INIT-9, the Jira breakdown, the review template. |
| `AI chats\` | Duplicate initiative docs, the 120-site guide, FWDAD-622 table notes. Saved webpage folders were not used. |

## Reviewed and not used as FWD operating material

| Path | Why it is not in the chapters |
| --- | --- |
| `07_Case_Studies` | University coursework. |
| `Anna_psy` | Personal project. |
| `Jane` | Personal projects. |
| `03_Business_Analysis` | February 2026 image-marketplace exercise. |
| `payment data` | Tax forms. Not extracted. |
| `Pavel\main_result.pdf` | Not needed once the October narrative and the ratings were in hand. |
| `04_Data_Analytics\extract_sites_data.py` | Competitor scrape for the AI-chat catalog, not an ad or rank report. |
