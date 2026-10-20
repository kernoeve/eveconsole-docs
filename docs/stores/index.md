# Stores

A **store** lets you trade with other players straight from EVE Console. It sells from your [Sale Postings](../tools/sale-posting.md) and, if you like, buys into them too. It takes orders and offers, books each one into the [Order Tracker](../tools/order-tracker.md), and keeps the other party posted as things move along. You run it from the **Stores** tool in the left sidebar (under **Market / Trade**).

## Two shop fronts

A store can take orders through either or both of two channels. They are independent switches on the same store, sharing one set of listings and one set of rules:

- **[EVE Mail Store](eve-mail.md)** — players place and manage orders by mailing simple commands (`PRICES`, `ORDER`, `SELL`, `STATUS`, `CANCEL`) to one of your characters, and the app replies.
- **[Web Storefront](web-site.md)** — players sign in to a website with EVE SSO, browse your price lists, and place and follow orders there. You host the site on your own Cloudflare account; the app can deploy and update it for you.

Whichever channels are open, orders land in the same place and follow the same rules.

## Shared setup

Everything below is set once on the store's **Config** tab and applies to both channels.

- **General** — the store's name, the **EVE Mailbox** character (used for notifications and, if the mail channel is on, for requests), the store's **Listings** (see below), the store's **Language** (see below), and options like serve/estimate and labels.
- **Restrictions** — **who may order** (*Anyone*, or only a list you supply) and an optional per-buyer **purchase limit** (how many units one buyer may take, by item type / market group / whole store, over a period). The same policy governs mail and web; on the web an item a buyer has reached their limit on is greyed out. Purchase limits apply to Sell listings only.
- **EVE Mail** and **Web site** — the two channel tabs (see their pages).

Changes on the Config tabs save as you make them.

## Listings

A store's **Listings** are the price lists it shows. Each one is a [Sale Posting](../tools/sale-posting.md), and each is either:

- **Sell** — buyers order from your stock and builds.
- **Buy** — the prices you pay, with no stock counts. A player offers to sell to you, then makes an Item Exchange contract to you asking that ISK, and the offer completes when you accept the contract. See [Buy Listings](buy-listings.md).

Each listing is a price list mail of its own and a tab of its own on the web site, in the order you set. To manage them, on **Config ▸ General**:

1. Press **Add listing**. It adds a Sell listing of the first posting the store doesn't list yet.
2. Pick the **posting**, and **Sell** or **Buy** beside it.
3. Optionally type a **Tab title**. Without one, the tab and the mail are headed with the posting's name.
4. Use **▲** and **▼** to change the order, and **Remove** to take a listing off.

A store with a single Sell listing and no title mails its price list under the same subject as a store always has. List each posting once: the web site shows one tab per posting.

!!! note "Buy listings need someone to receive their contracts"

    When a store has a Buy listing, **Buy contracts to** appears under the listings. Until you choose a character, corporation or alliance there, Buy listings take no offers. See [Buy Listings](buy-listings.md#setting-one-up).

## The store's language

**Language** on **Config ▸ General** sets the language the store speaks to its buyers: its mails, and the item and group names on its web site. It can differ from the language your own app shows — you might play in one language and sell in another, or run the same price list as two stores in two languages.

- **Same as the app** (the default) follows the interface language of the computer that serves the store — the one doing the [background work](../background-processing.md).
- What *you* read about the store — the Stores screen, its logs and status lines — stays in your own interface language.
- The mail **command words** (`PRICES`, `ORDER`, `SELL`, `STATUS`, `CANCEL`, `INFO`, `HELP`) stay English in every language. See [EVE Mail Store](eve-mail.md).
- An NPC station named in **Buy contracts at** is written in the store's language too.

## The Overview tab

The store's **Overview** tab shows how it is doing:

- **Counts** — **Inquiries**, **Active items**, **Completed**, **Cancelled**, **Visits** and **Unique visitors**. Each shows the all-time figure, with the last 48 hours beneath it (*Last 48 h: 3*). A visit is a buyer signing in to the web site, or coming back after a while away. Unique visitors counts each buyer once, however often they came. Completed and cancelled orders keep only the day they settled, so their 48-hour figure can reach back up to a day further.
- **Active orders** — the store's open orders: **Created on** (EVE time, to the minute), the order reference, item, units, buyer, estimated date, **Source** and status. Source says where the units are coming from. An offer to a Buy listing reads *Offer · waiting for their contract* or *Offer · their contract to accept*.
- **Messages** — the store's mail log.
- **Web site events** — what buyers did on the site, with the **Item** each event concerns. See [Web Storefront](web-site.md#orders-events-and-reviews).

## Where orders and pricing come from

- **Pricing is taken from the listing's Sale Posting at the moment an order is placed** — never from anything a buyer types or a stale web page. Keep your [Sale Postings](../tools/sale-posting.md) current so quotes are right.
- Every order — mail, web, or entered by hand — is booked into the [Order Tracker](../tools/order-tracker.md), and new orders also surface in the [Overview](../tools/overview.md) **Orders** section.
- An optional **Store order events** [alarm](../tools/alarms.md) can tell you when orders and offers come in, and as they move along.

## Stock follows the store's rules

A store says what's **in stock** by the rules of the [Sale Posting](../tools/sale-posting.md) the order was placed from: the posting's (or section's) **inventory scope**, **only include packaged items**, and an item's stock override. Orders follow the same rules.

- **An order placed through the store is in stock only from that listing's shelf.** The [Order Tracker](../tools/order-tracker.md) — and the mail it sends the buyer — calls a store order "in stock" only from what that posting counts. A store that sells packaged hulls from one station won't call an order in stock off assembled hulls in use somewhere else.
- **A posting's places are its shelf too.** An order for an item a posting lists from its [places](../tools/sale-posting.md#listing-what-places-hold) is in stock only from what those places hold, not from the same item in another hangar.
- **A stock override is a ceiling, not a source.** If you override an item's stock to show five, an order is still in stock only for units that are really on the shelf.
- **Everything else takes from all you own.** Orders entered without a store, and orders for an item the store's posting doesn't list, count every unit you own, as before.
- **No double promises.** Two stores' shelves can hold the same units. After each order is placed against stock, no store may promise more than you have left overall.
- **Offers never touch the shelf.** An offer to a Buy listing is goods coming in. It reserves nothing, counts toward no purchase limit, and asks the [Worklist](../tools/worklist.md) to build nothing.

Stock also keeps up with **contracts** between asset updates. Assets are refreshed about once an hour, contracts every five minutes. A contract you create takes its goods off the shelf straight away, and a contract deleted since the last asset update puts them back — so the next order for the same item isn't called in stock off goods already on their way to someone else. ESI never lists what is in a courier contract, so a courier's goods are followed only when you [enter its cargo by hand](../tools/contracts.md#courier-cargo), and they reach the shelf only once the courier is delivered.
