# Stores

A **store** lets you sell to other players straight from EVE Console. The app prices from one of your [Sale Postings](../tools/sale-posting.md), takes orders, books each one into the [Order Tracker](../tools/order-tracker.md), and keeps buyers posted as their orders move along. You run it from the **Stores** tool in the left sidebar (under **Market / Trade**).

## Two shop fronts

A store can take orders through either or both of two channels — independent switches on the same store, sharing one catalogue and one set of rules:

- **[EVE Mail Store](eve-mail.md)** — buyers place and manage orders by mailing simple commands (`PRICES`, `ORDER`, `STATUS`, `CANCEL`) to one of your characters, and the app replies.
- **[Web Storefront](web-site.md)** — buyers sign in to a website with EVE SSO, browse your price list, and place and follow orders there. You host the site on your own Cloudflare account; the app can deploy and update it for you.

Whichever channels are open, orders land in the same place and follow the same rules.

## Shared setup

Everything below is set once on the store's **Config** tab and applies to both channels.

- **General** — the store's name, the EVE **mailbox character** (used for notifications and, if the mail channel is on, for requests), the **[Sale Posting](../tools/sale-posting.md)** the store prices from, the store's **Language** (see below), and options like serve/estimate and labels.
- **Restrictions** — **who may order** (*Anyone*, or only a list you supply) and an optional per-buyer **purchase limit** (how many units one buyer may take, by item type / market group / whole store, over a period). The same policy governs mail and web; on the web an item a buyer has reached their limit on is greyed out.
- **EVE Mail** and **Web site** — the two channel tabs (see their pages).

Changes on the Config tabs save as you make them.

## The store's language

**Language** on **Config ▸ General** sets the language the store speaks to its buyers: its mails, and the item and group names on its web site. It can differ from the language your own app shows — you might play in one language and sell in another, or run the same price list as two stores in two languages.

- **Same as the app** (the default) follows the interface language of the computer that serves the store — the one doing the [background work](../background-processing.md).
- What *you* read about the store — the Stores screen, its logs and status lines — stays in your own interface language.
- The mail **command words** (`PRICES`, `ORDER`, `STATUS`, `CANCEL`, `INFO`, `HELP`) stay English in every language. See [EVE Mail Store](eve-mail.md).

## Where orders and pricing come from

- **Pricing is taken from your Sale Posting at the moment an order is placed** — never from anything a buyer types or a stale web page. Keep your [Sale Posting](../tools/sale-posting.md) current so quotes are right.
- Every order — mail, web, or entered by hand — is booked into the [Order Tracker](../tools/order-tracker.md), and new orders also surface in the [Overview](../tools/overview.md) **Orders** section.
- An optional **Store order events** [alarm](../tools/alarms.md) can tell you when orders come in.

## Stock follows the store's rules

A store says what's **in stock** by its [Sale Posting](../tools/sale-posting.md)'s rules: the posting's (or section's) **inventory scope**, **only include packaged items**, and an item's stock override. Orders follow the same rules.

- **An order placed through the store is in stock only from that store's shelf.** The [Order Tracker](../tools/order-tracker.md) — and the mail it sends the buyer — calls a store order "in stock" only from what the store's posting counts. A store that sells packaged hulls from one station won't call an order in stock off assembled hulls in use somewhere else.
- **A stock override is a ceiling, not a source.** If you override an item's stock to show five, an order is still in stock only for units that are really on the shelf.
- **Everything else takes from all you own.** Orders entered without a store, and orders for an item the store's posting doesn't list, count every unit you own, as before.
- **No double promises.** Two stores' shelves can hold the same units. After each order is placed against stock, no store may promise more than you have left overall.

Stock also keeps up with **contracts** between asset updates. Assets are refreshed about once an hour, contracts every five minutes. A contract you create takes its goods off the shelf straight away, and a contract deleted since the last asset update puts them back — so the next order for the same item isn't called in stock off goods already on their way to someone else.
