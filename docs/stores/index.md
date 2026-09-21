# Stores

A **store** lets you sell to other players straight from EVE Console. The app prices from one of your [Sale Postings](../tools/sale-posting.md), takes orders, books each one into the [Order Tracker](../tools/order-tracker.md), and keeps buyers posted as their orders move along. You run it from the **Stores** tool in the left sidebar (under **Market / Trade**).

## Two shop fronts

A store can take orders through either or both of two channels — independent switches on the same store, sharing one catalogue and one set of rules:

- **[EVE Mail Store](eve-mail.md)** — buyers place and manage orders by mailing simple commands (`PRICES`, `ORDER`, `STATUS`, `CANCEL`) to one of your characters, and the app replies.
- **[Web Storefront](web-site.md)** — buyers sign in to a website with EVE SSO, browse your price list, and place and follow orders there. You host the site on your own Cloudflare account; the app can deploy and update it for you.

Whichever channels are open, orders land in the same place and follow the same rules.

## Shared setup

Everything below is set once on the store's **Config** tab and applies to both channels.

- **General** — the store's name, the EVE **mailbox character** (used for notifications and, if the mail channel is on, for requests), the **[Sale Posting](../tools/sale-posting.md)** the store prices from, and options like serve/estimate and labels.
- **Restrictions** — **who may order** (*Anyone*, or only a list you supply) and an optional per-buyer **purchase limit** (how many units one buyer may take, by item type / market group / whole store, over a period). The same policy governs mail and web; on the web an item a buyer has reached their limit on is greyed out.
- **EVE Mail** and **Web site** — the two channel tabs (see their pages).

## Where orders and pricing come from

- **Pricing is taken from your Sale Posting at the moment an order is placed** — never from anything a buyer types or a stale web page. Keep your [Sale Posting](../tools/sale-posting.md) current so quotes are right.
- Every order — mail, web, or entered by hand — is booked into the [Order Tracker](../tools/order-tracker.md), and new orders also surface in the [Overview](../tools/overview.md) **Orders** section.
- An optional **Store order events** [alarm](../tools/alarms.md) can tell you when orders come in.
