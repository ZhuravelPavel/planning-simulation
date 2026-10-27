# How advertising operations works

Advertising operations is the function that sells attention on Forward Handle’s sites. The company is the publisher. An advertiser pays to be shown to people who are already on isexychat.com or bdsmlr.com. The function does not build the sites. It decides which advertisers are present, in which formats, and how the resulting delivery is turned into a number the company can reconcile.

Pavel is the Ads, Marketing, and SEO lead. This chapter is the advertising part of that role. Rotchilda is the project manager for the work that has to cross from this function to development or to the owner.

## Who is responsible for which part

| Part | Responsible |
| --- | --- |
| Which advertisers stay, and on which terms | Pavel. He negotiates with the networks. Those relationships are his. |
| Campaigns, banners, click URLs, and zone links inside Revive | Pavel, with Marko. Marko is the named contact on the Candy AI account. |
| The contract rate used on a CPM row | Pavel. Rigela does not choose the rate. |
| The iSexyChat sheet and the BDSMLR sheet | Rigela enters them. Pavel reads them and decides what they mean. |
| A zone that does not yet exist on the page, and the rule that hides ads from logged-in people | Simon. Akira takes the development work Simon assigns. |
| The `logged_in` parameter, GTM, and the GA4 dimension | Simon, as the development lead for the site. Pavel says what the split has to show. |
| Looker reports on that behavior | Pavel. They are his reading layer, not a report anyone else is expected to maintain. |
| The shop line on the BDSMLR sheet | Rigela enters it. It is not Marko’s, because it is not in Revive. |
| What cash arrived | Melissa, in the books. Pavel’s sheets are not her ledger. |
| The advertising section of the monthly owner note | Pavel, as Ads, Marketing, and SEO lead, writes the substance. Rotchilda, as project manager, gathers the note. Sakura receives it. |
| Switching off React Ads, GSM, or 4th Whale, or changing what a processor is told the company sells | Sakura, on a recommendation from Pavel. Adam is on the legal side of a processor or a description of what the company sells. |

Ordinary trafficking does not wait for Sakura. A banner, a link, or a tag that is not paying is Pavel and Marko.

## What the function includes

**Two publishers inside one ad server.** The server is Revive Adserver, hosted. A publisher is the site the ad is for. IsexyChat is isexychat.com. BDSMLR is bdsmlr.com. A third publisher exists for staging and is not part of delivery. The shop is not a publisher. Its money never enters the chat site’s book.

**The objects inside Revive.** An advertiser has campaigns. A campaign has banners, which are the creatives. A zone is a place on the site that asks the server for an ad. Linking a banner or a campaign to a zone is what makes that creative eligible to appear there. The server’s record is requests, impressions, and which creative served. It is not the record of what a revenue-share partner later pays.

**The formats.** A banner is a display unit in a fixed size. Sizes in use include 300×250, 728×90, and 320×50. A tabunder, also called a popunder in older setups, opens in a new tab, usually when the current tab closes. An interstitial is a full page between actions. The iSexyChat book also has nav and button placements. A button redirect is filed with banners in the link exports, even though it behaves like a button.

**The way an advertiser pays.** There are three arrangements, and they are entered differently.

| Arrangement | What the advertiser bought | Where the dollars come from |
| --- | --- | --- |
| CPM | A price per thousand impressions | The contract rate times the impressions, divided by 1,000 |
| Revenue share | A share of what the advertiser earns from the visitor | The partner’s own statement, later |
| Affiliate | The same shape as revenue share | The partner’s own statement, later |

A contract rate is the deal CPM. Revive also calculates an eCPM from whatever it knows. That calculated field is not the invoice and is not what goes in the sheet. Revenue-share tags are the clearest case: Revive can count a large number of impressions and still show no revenue, because the money never passes through the ad server. Candy AI on iSexyChat is that kind of tag.

The direct CPM relationships used for day-to-day reading are React Ads, Grand Slam Media (also called Adnium or GSM), 4th Whale, and Stripchat through Technius. React Ads tabunders are contracted at $10. Other partners in the book, including Chaturbate and StripCash, are part of the same publisher but are not all on that direct-CPM list. StripCash is paid from the partner side and is not itself a Revive advertiser on IsexyChat.

**Two sheets, which are the commercial book.** The iSexyChat sheet is a daily record of partner revenue from 2019. The BDSMLR sheet is the same idea from 2021, and it includes the shop. Rigela keeps both. Pavel is responsible for the rate on a CPM row and for reading the result. Looker reports and the monthly owner note are read from these sheets, not from Revive’s calculated yield.

**Behavior measurement, separate from the book.** GA4 records what people did. On bdsmlr.com the container is `GTM-WZKGN4B`, the measurement id is `G-9VSP3HR9NF`, and the property is bdsmlr.com PROD. Simon is responsible for the tag and for the login parameter it sends. Looker Studio is Pavel’s reading layer on top of that property. It is not a second set of invoices, and it is not Melissa’s books.

**Access.** Revive’s API answers only from an allow-listed address. The machine on the tailnet that Ad Ops uses for that access is named `adops`.

## How a page view becomes an impression

Someone opens a page that contains a zone. The zone asks Revive for an ad. Revive chooses among the banners linked to that zone, subject to the targeting on those banners, and returns a creative. That return is an impression. If nothing is linked, or nothing matches, the request is unfilled.

Fill is the share of requests that received a creative. On both publishers the zones are built to be full. An empty request is a gap in what was linked, not the normal state of the business. On iSexyChat the formats that carry the direct deals are banners, tabunders, and interstitials. On BDSMLR the same formats exist. The new BDSMLR experience simply contains fewer of those zones than the old pages did. Linking a creative to a zone that already exists is Pavel and Marko, inside Revive. Adding a zone to the page is Simon.

Targeting that already exists on creatives is expressed in the campaign itself: device (desktop, tablet, mobile), a named placement (sidebar above the fold, sidebar below, sticky, profile scroll, the left-hand “kiwi” placement, main pages), and, for 4th Whale on iSexyChat, a pair code such as `m4m` or `w4w` plus a separate India set. GSM India is not part of the main iSexyChat mix, because that advertiser does not want Indian traffic. BDSMLR blogs also carry an orientation label, across gay, trans, straight, lesbian, and a large remainder. That label is available as data. It is not wired up as a live targeting system.

Who sees the zone is a property of the page, not of the contract. Pavel sets the rule. Simon builds it. On BDSMLR the page is built so that a visitor who is not logged in can be shown an ad, and a visitor who is logged in is not shown one, whether or not they pay. The events that describe this are `interstitial_displayed` for a person who was shown it, and `interstitial_suppressed_login` for a person who was skipped because they were logged in. Ad events that belong to the same picture are `revive_ad_pageload`, `revive_ad_refresh`, an empty zone, a blocked SDK, and a load that failed. The refresh event often arrives without a login flag, so it cannot be split the way a page view can.

The login flag itself is a string, `logged_in`, either `"true"` or `"false"`, sent with the event and registered in GA4 as an event-scoped dimension named Logged in. It uses the same check the page already uses to decide whether to suppress the interstitial. It does not identify the person.

## How delivery becomes a number in the book

At the end of a day, Revive knows how many times each creative was requested and shown. The sheet is then brought in line with the arrangement.

For a CPM deal, the impressions are divided by 1,000 and multiplied by the contract rate. The rate lives in the deal, not in Revive. For a revenue-share or affiliate deal, the row waits for the partner’s statement. Until that statement exists, the row can hold volume and no dollars. Guessing a dollar figure from eCPM would mix a calculated yield into the book.

The shop is entered on the BDSMLR sheet as its own line. It is PayPal ecommerce. It is never copied onto the iSexyChat sheet, and it is never created as a Revive advertiser.

A tag can be alive in Revive and absent from the sheet, or present on the sheet and absent from Revive. Those are different lists of “who is in the book.” OnlyFans, JoyOurSelf, and LiveSexAwards are examples of tags that have served on iSexyChat without a sheet row. Internal and test campaigns also exist inside Revive and are not partners. Matching the two lists is part of how the book stays honest. Removing a tag from a zone does not leave the zone empty, because other advertisers are linked to the same zone and absorb the requests.

## How the two publishers differ

They use the same server and the same objects. They are not the same business.

iSexyChat is a full advertising operation: several formats, a mix of contract CPM and revenue share, and a short list of partners that account for most of the money. The sheet is the thing you read to know whether the month is healthy. The partners that reading starts with are React Ads, GSM, and 4th Whale.

BDSMLR uses the same machinery for display and affiliate tags, and then has the shop beside it. The shop is the membership people can buy today. Display on BDSMLR is whatever is linked in that publisher. Because the new pages have fewer zones than the old ones, the same advertiser demand produces fewer impressions until those zones exist. Empty interstitial and close-tabunder requests on desktop are the slots that exist without a creative in them.

iSexyChat’s chat is not an advertising product and not a paid product. People come to talk. The ads are around that activity. Ideas about charging for the chat itself are not part of how the function works.

## How the function is read

There are four readings, and they answer different questions.

| Reading | Question it answers |
| --- | --- |
| Revive | What was requested, what was shown, and which creative did it |
| The property sheet | What that delivery is worth, under the contract or the partner’s statement |
| GA4 and Looker | Whether the person was logged in, and whether the ad was shown, skipped, empty, or blocked |
| The company’s books | What cash actually arrived |

The sheet and the books describe the same activity at different moments. The sheet, which Rigela keeps and Pavel interprets, is delivery valued at the deal. The books, which Melissa keeps, are deposits. Deposits can lag, and they can be net of fees. The two are not interchangeable. A monthly note to the owner is a short reading of the two sheets: iSexyChat against the recent months, BDSMLR split into shop and display, what changed in the setup, and whether the large partners are still the ones carrying the publisher. Pavel, the Ads, Marketing, and SEO lead, supplies that reading. Rotchilda, the project manager, puts it into the note. Sakura is who it is for. It is not a reading of Revive’s eCPM, and it is not a forecast from a planning model.

Looker, for behavior, is built on the GA4 property rather than the sheet. A report-level date control and a LoggedIn control sit on every page. Event charts count events and filter to one event name. Traffic charts use users and sessions and are not filtered to an event, or the user count breaks. The pages that describe the function are traffic, the login split, and ads. Social, reliability, and premium clicks are on the same report because they share the property. They are not advertising revenue.

## What sits next to the function

A change that only relinks a banner, edits a click URL, or turns off a tag that is not paying stays with Pavel and Marko, inside Revive. A change that adds a zone to a page, or that shows or hides ads based on login, is Simon’s. The iSexyChat interstitial is the format that would be brought onto the new BDSMLR pages for visitors who are not logged in. Akira’s recommendation engine sits on the logged-out side of that same page. It can change how many of those visitors stay long enough to be shown an ad. It is not part of the ad server, and Pavel does not run it.

Turning off a partner that still carries a large share of iSexyChat is Sakura’s decision, made on Pavel’s recommendation. Changing what the company tells a processor it sells is Sakura’s, with Adam on the legal description. Ordinary trafficking is not.

Ezra is responsible for customer support. Every ticket that comes from a user goes to him, including a complaint about an ad, a charge, or a page that broke. When the ticket is a bug, he works it with Simon. He does not traffic campaigns or enter the sheets. Pavel tells him before a user-visible advertising change goes out, so the tickets that follow are ones he already understands. The words of that change are described in the marketing guide.
