# How marketing works

Marketing, in this company, is the commercial shape of the properties: what a visitor can do without paying, what a payment unlocks, which property the payment sits on, and how that is explained. Advertising operations is the part of marketing that sells attention. This chapter is the rest of the shape, and the way the two fit.

There is no separate brand or email team. Community communication, when it happens, goes out on the site itself.

Pavel is the Ads, Marketing, and SEO lead. This chapter is the marketing part of that role. Rotchilda is the project manager. She does not own the offer. She carries a decision that needs Sakura, in the monthly note and sooner when it cannot wait.

## Who is responsible for which part

| Part | Responsible |
| --- | --- |
| What is free, what is paid, and what the receipt is allowed to say | Pavel |
| The public price, once a figure is chosen | Pavel recommends it. Sakura decides it. |
| The gate, the quota, the link between a tenant account and a billing account | Simon. Akira takes the development work Simon assigns. |
| The words on the blog, the home banner, and the update box | Pavel |
| Customer support | Ezra. He handles every ticket that comes from a user. Bug reports are the part of that work he does with Simon. Before a membership or pricing change is public, Pavel gives him the text, so those tickets are not the first time he sees it. |
| The PayPal shop as a checkout | The shop is the live checkout. Melissa records the cash. Pavel decides how that line is described next to advertising. |
| Which processor is approached, and whether the product is described as an IRC client or as an adult membership | Pavel prepares it. Sakura decides. Adam is responsible for the legal and corporate side of what the company is said to sell. |
| The rule that anonymous visitors are the ad audience and logged-in visitors are not | Pavel. Simon makes the page obey it. |
| Search that exists to bring those visitors | Pavel, as Ads, Marketing, and SEO lead. The search guide is that part of the role. |

## What the function includes

**A publisher business and a membership, side by side.** Most of the company’s money is advertisers paying to reach people on iSexyChat. BDSMLR carries a smaller version of that, plus a shop. The membership is the other product. It is not a second advertising network, and it is not a charge to remove ads.

**One membership across properties.** The paid product is a single RelayOS subscription. Paying it makes the person premium on the properties linked to that billing account. BDSMLR and bb.chat are tenants of that membership. They are not sold as separate products, and they are not customers of it. A future outside network could be a tenant in the same sense. That is the shape of the model. It is not a sales motion aimed at BDSMLR or bb.chat themselves.

**Two accounts for one person.** Each property has its own user account. Billing is a different account, in a shop database that holds the payment and not the social profile. The two are linked after the person already exists. Offline delivery of messages is why the user has to exist in the property’s database. The link is not a second registration the user is asked to understand.

**A neutral receipt.** The charge is described as the company’s, Forward Handle LLC, on a neutral property. The adult site is not what the receipt says was purchased. BDSMLR-only tools are therefore not listed on the RelayOS pricing page. They stay on BDSMLR. The public pricing page describes the IRC client: a connection that stays up, offline messages, more than one network, and uploads.

**The shop that exists today.** shop.bdsmlr.com is a PayPal checkout. The product on it is the older membership, sold as ad-free BDSMLR. The card statement already says Forward Handle LLC. That shop line is real ecommerce. It is not an ad tag, and it is not the membership described above. The newer membership is specified so that ad removal is only a side effect of being logged in, not the thing for sale.

**The channels a user can be spoken to on.** The site blog, a banner on the home page, and an update box. There is no mailing list. Support mail is the address already published on the site. Those are the whole of user-facing marketing.

## How attention and membership divide the audience

Almost everyone on BDSMLR is not logged in. Those visitors are the advertising audience. Once someone is logged in, the page does not show them ads, free or paid. The membership is then a set of tools for the people who use the product heavily, not a fee to make the ads go away.

That split is why the two functions can run on the same site without one eating the other. Advertising is priced against anonymous traffic. The membership is priced against logged-in use. Hiding ads only for paying users would make the membership an ad product. The pages are not built that way.

Messages follow the same boundary. Offline delivery is inside one network: BDSMLR with BDSMLR, bb.chat with bb.chat. A subscription does not open a path from one tenant’s users to another’s.

## What free and paid include

The price on the June specification is $5 a month, bought at getrelayos.com. An earlier specification used $12. The shop product is $20, and it buys ad removal only. Pavel is responsible for which figure is put in front of Sakura. Sakura is responsible for the figure the company actually charges. The contents below are the specification of the offer, and they are Pavel’s. The number printed on them is not.

Nothing in a public post states a price, or states how many free offline messages a person gets, until that number has been chosen. The working allowance in the specification is about ten offline messages a month for a free logged-in user, set high enough that only the heaviest users run out. Subscribers get unlimited offline messages.

**On BDSMLR, once logged in.**

| | Included without paying | Included with the membership |
| --- | --- | --- |
| Ads | None | None |
| Offline messages | A quota, number unpublished | Unlimited |
| Private blogs | Reading a blog you already follow | Posting to a private blog |
| Archive | Newest, in a grid | Popular, liked, and newest; masonry; originals distinguished from reblogs |
| Search | Newest only, and pixelated once you go deep | Clear at any depth; popular, liked, and newest |
| Other people’s following feeds | No | Yes |
| Privacy controls | Yes | Yes |

Privacy settings stay free on purpose. So does reading a private blog the person already follows. The paid act is posting to one.

**On bb.chat.** History is unlimited whether or not the person pays, because the text is cheap to keep. Free includes the same unpublished message quota, a disconnection after idle time, and the bb.chat network only. The idle timeout is not given a duration in the specification. Paid adds a connection that stays up, access to other IRC networks, and uploads of files, photos, and video stored in Wasabi. Uploads are for registered paying users. Anonymous uploads are not part of the product. A third-party client can still join the bb.chat network. Using the client across many networks is the paid capability. Caps on file size, and whether uploads are only in direct messages, are not in the specification.

**On the RelayOS page.** Free is the web client and ordinary IRC, unlimited history, the message quota, an idle disconnect, and one identity, with a way through to the participating sites. Paid is the bouncer, unlimited offline messages, the always-on connection, uploads, and premium standing on the sites that have been linked. The page does not enumerate BDSMLR tools.

A Contributor mark exists on BDSMLR for people doing that work. An Early Supporter mark is for people who pay, or who start paying, before 1 January 2027. Those are recognition, not a separate tier.

## How a user is told

A change that people will notice is written as a continuation of what the site has already said, in ordinary paragraphs, about the product rather than about the stack. The post does not name the databases, the protocol, or the billing machinery. It does not announce a date that has not been set. It does not say a feature is available when it is still being built. Something in progress is described as coming. Something deployed is described as present.

The series of explanations, when a membership change is being introduced, has a fixed shape. The first post is the messaging rebuild and the tools, without numbers. The next is what the person will actually see. The next is that the move is about to happen, and where to ask for help. The one that accompanies the change states the concrete difference between free and paid behavior, including quiet fallbacks, such as a paid sort simply showing newest when the person is not entitled to it. A later post says what has since appeared and what is still absent.

Pavel writes that series. Before any of it is public, Ezra has the text, a statement of what is really switched on, and the questions people are likely to ask: where the old premium went, why a blog will not accept a post, what the name on the card charge refers to. Those questions arrive as tickets, and Ezra handles them along with every other user ticket. When a ticket is a bug, he and Simon work it together.

If the response to a real launch is hostile, the specification already contains the response. Pavel revises the explanation if a large minority objects. A lower price is the relief valve written for that case, and it is Sakura’s to approve because it is a price. If the objection is general, the gated behavior returns to free. Simon is who removes the gate. That is part of how the offer is built, not a separate campaign.

The older help pages tell users that premium continues, that the price will not change, and that premium means ad-free browsing, early access, and higher upload limits. Those pages describe the shop product. They are not a description of the membership in this chapter.

## How the payment sits in the product

The shop’s processor is PayPal. Melissa is responsible for that cash once it has arrived. The membership is designed to be sold as a plain IRC client so that a mainstream processor can describe the charge without describing an adult site. Selling “BDSMLR Premium” as the product name would put the charge on an adult-merchant path instead, which is a heavier compliance burden and a clearer description. Pavel is responsible for which of those two shapes is recommended. They are not both used at once. The receipt follows whichever shape Sakura and Adam have accepted. Adam is responsible for that acceptance matching what the company can legally say it sells.

An adult-merchant relationship, if that shape were used, expects a fixed set of conditions: the uploader has agreed to terms, the site does not present child exploitation or non-consensual material as the product, complaints are handled within five business days, a person depicted can appeal to have material removed, there is an anti-trafficking position, and a card-scheme reviewer can be shown paywalled content. Identity checks on uploaders, an age check on visitors, and review of an upload before it is public are the conditions that were not met in the written score of that list. Live streaming and rules about AI-generated content were marked as outside the product. The score is a description of the requirements, not a claim that a processor has accepted the site.

## How marketing uses search and advertising

Search brings people to iSexyChat. Advertising operations sells that visit. The membership does not depend on search, and the RelayOS site is not supposed to mention the adult properties. That separation is the same idea as the neutral receipt: the paid IRC product can be described on its own.

iSexyChat’s rooms are not packaged as a subscription. Gender-matched entry and similar ideas have been explored and are not part of the product. The creative catalog of levels, season passes, and room ownership is not part of the product either. Neither is a creator marketplace that pays people per post. The commercial model in force is advertising on anonymous traffic, plus one membership for the tools above.

## How marketing meets the other functions

Pavel holds both sides of the commercial rule. As advertising operations, he owns the zones, the partners, and the meaning of the sheets. As marketing, he owns the rule those zones obey: anonymous traffic is the ad audience, logged-in use is the membership audience. When a page has to grow a new zone, or has to enforce a quota, that work is Simon’s. When the words go out, Ezra already has them, because he is the person who will receive the tickets. Sakura is asked when the decision changes the processor, the public price, or a partner that carries the advertising business. Adam is in that conversation when the decision describes the company to a bank, a processor, or a contract. The explanation that reaches Sakura is the same shape every time: what is going on, why it matters, the real options, and what Pavel, and Simon where the page is involved, recommend. Rotchilda, the project manager, is who assembles it.
