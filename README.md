# How the commercial side of Forward Handle works

This is a guide to three functions: advertising operations, marketing, and search. Each chapter explains what that function is, what it is made of, and how the parts work together.

It is not a record of past results, and it is not a plan of upcoming work.

| Guide | What it explains |
| --- | --- |
| [How advertising operations works](01_Ad_Operations.md) | How a page view becomes an ad, how advertisers pay, and how that money is recorded |
| [How marketing and monetization works](02_Marketing_and_Monetization.md) | How every property is presented, and how a visit or a payment becomes money |
| [How search works](03_SEO.md) | How search is used on every property, and how a query is assigned to one page |

[The parts, named](04_Source_Index.md) is a short glossary of the objects these chapters keep using.

## Where the functions sit

Forward Handle is the publisher. The sites attract people. Advertising operations sells that attention to advertisers. Marketing decides how each property is presented and which way it makes money: advertising, a direct payment, or both. Search is how a large share of the audience on iSexyChat arrives, which is what gives advertising something to sell. Other properties do not depend on search in the same way.

Development builds the pages, the login state, and the placements, and helps set up event tracking and other metrics in GA4. Support handles every ticket from a user, and works a bug report with development. Neither of those is documented here except where the commercial function depends on them.

## Who is responsible

Each guide has a fuller table for its own parts. Across the three functions, responsibility sits like this.

| Person | Responsible for |
| --- | --- |
| Pavel | Ads, Marketing, and SEO lead. Which advertisers are on the sites, the contract rates, the membership offer, the words users see, search, and the event tracking and other metrics in GA4 |
| Marko | Ad operations tech specialist. He works in Revive under Pavel’s control |
| Rigela | Entering delivery into the two property sheets |
| Simon | Development lead. The page itself, on any property: placements, who is shown an ad, the paywall, and templates. He helps Pavel set up event tracking and other metrics in GA4 |
| Akira | Development work Simon assigns, including the logged-out recommendation engine |
| Ezra | Customer support. Every ticket that comes from a user. Bug reports, which he works on with Simon |
| Melissa | The company’s books: cash received, not the advertising sheets |
| Rotchilda | Project manager. She runs the projects that cross advertising, marketing, search, development, and support. She gathers the monthly owner note. She does not produce the advertising figures |
| Sakura | A decision that changes a major advertiser, the public price, or what a processor is told the company sells |
| Adam | The legal side of that same decision: the contract, the receipt, and what the company is described as selling |

## The properties these functions cover

| Property | What it is in this guide |
| --- | --- |
| isexychat.com | The advertising property. Live chat rooms. Search is its audience. |
| bdsmlr.com | A social site. Same ad server, a different audience, plus a separate shop. |
| shop.bdsmlr.com | The checkout for a direct payment. Not an advertiser, and not part of the chat site’s ad book. |
| A membership that covers more than one property | One payment can unlock use on more than one property. Where the product can be described without naming an adult site, the receipt follows that description. |

ReblogMe is shut down. It is not part of these functions. The name still appears on an old Google Cloud project that the sheets and analytics use as an access key.
