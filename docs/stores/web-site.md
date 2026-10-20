# Web Storefront

A **shop front on the web**, on a site you host. Buyers sign in with EVE SSO, see your price lists with what's in stock, in build and reserved, place orders and follow them. If the store has [Buy listings](buy-listings.md), sellers can offer you items there too. The app sends the site what it may show and collects what buyers did every few minutes; **nothing on the site ever reaches your database**.

It's one of a store's two shop fronts — see [Stores](index.md) for the shared setup (catalogue, who may order, purchase limits), and the [EVE Mail Store](eve-mail.md) for the other. All of the web settings live on the store's **Config ▸ Web site** tab.

!!! info "How it fits together"

    The **app stays the source of truth**; the site is a shop window plus an inbox. The app *pushes* your catalogue (every one of the store's [listings](index.md#listings), with prices, stock states and lead times) and the allowed-buyer list, and *pulls* new orders and cancellations — a signed sync every few minutes, run by whichever client holds the [background-worker](../background-processing.md) lease. The database is never exposed.

## What you need

- A **Cloudflare account** (the free tier is plenty).
- A store already set up in EVE Console (a name, a mailbox character, and at least one [listing](index.md#listings) to price from — see [Stores](index.md)).
- A few minutes to register an **EVE application** for sign-in.

There are two ways to get the site running: let the app **deploy it for you** (recommended), or **set it up by hand**. Either way you finish by registering the EVE application.

## Option A — deploy from the app (recommended)

The app can put the site on your own Cloudflare account and keep it current: it creates the database, uploads the newest release of the site, sets the secrets, and puts it on the free `workers.dev` address or a domain of your own. **Deploying again updates the site without touching its orders.**

On **Config ▸ Web site**, under **Automatic deployment and updates on Cloudflare**:

1. **Create a Cloudflare API token.** Open [the API-tokens page](https://dash.cloudflare.com/profile/api-tokens) → **Create Token** → the **"Edit Cloudflare Workers"** template, then **add the permission `D1 → Edit`** → **Continue** and **Create**. Copy the token.
2. **Save the token** in the app: paste it into **API token** and press **Save token**. It's checked, then kept on this machine only, encrypted for your account.
3. **Pick the account** (the dropdown fills once the token is saved) and a **Worker name** — lower-case letters, digits and hyphens. This is also the database's name.
4. **Choose the address:**
    - **The free `workers.dev` address** — your site is `<worker-name>.<account>.workers.dev`.
    - **A domain of your own** — must already be on this Cloudflare account with its DNS there. The deploy attaches the site to it, Cloudflare makes the record and certificate, and `workers.dev` is switched off so buyers and the sign-in callback see one name.
5. Press **Deploy or update site**. Use **Check** any time to confirm the live site's version and health. When a newer release of the site is out, **Check** says so — press **Deploy or update site** again to update.

### Which site release is deployed

The app deploys the newest release of the site that speaks its own protocol. If the site's newest release needs a newer EVE Console, the app says so; update EVE Console first, then deploy.

A new version of the site sometimes comes first as a **release candidate**, tagged with a hyphen (`v0.2.0-rc.1`) and published on GitHub as a pre-release:

- **A released EVE Console never deploys a release candidate or offers it.** It keeps to full releases.
- **A development build deploys a release candidate like any other release.** This lets a candidate be tried on a real store before anyone else gets it.
- **A candidate counts as older than its release.** A store left on `0.2.0-rc.1` is offered `0.2.0` once it is out.

!!! info "What counts as a development build"

    A **development build** is a copy built from source, or a build from a pull request or the `develop` branch: anything not published by EVE Console's release workflow. The Windows installer, the Portable zip, the Linux tarball and AppImage, and the Docker image are all releases, and never see a site release candidate.

!!! note "Changing the address later changes the callback"

    Switching between `workers.dev` and your own domain changes the site's address, and therefore the **sign-in callback URL** — so you'll need to update the EVE application (below) to match. You can also rename the account's whole `workers.dev` subdomain from here (every Worker on the account moves with it).

## Option B — set it up by hand

If you'd rather host the site yourself, deploy it from its source and releases at **[github.com/kernoeve/eveconsole-store](https://github.com/kernoeve/eveconsole-store)** (follow the instructions there). Then, on **Config ▸ Web site**:

- Enter the **Site address** (e.g. `https://your-shop.your-account.workers.dev`).
- Set the **Secret** to the same value as the site's `STORE_SYNC_SECRET`. This is what the app signs every sync call with. Use **New secret** to roll it (update both sides).

None of the Cloudflare token / account / worker fields are needed for a hand-built site.

## Register the EVE application (needed before buyers can sign in)

**Deploy first**, so the site has an address — then:

1. Open **[developers.eveonline.com](https://developers.eveonline.com/applications/create)** and create an application: any name and description, **Authentication only (no scopes)**, and the **callback address shown in the app** (copy it from the Web site tab).
2. Copy the application's **Client ID** and **Secret Key** into the two boxes on the Web site tab.

They save as you enter them, and a site **deployed from the app receives them straight away**. The line under the boxes tells you whether the live site is holding *these* keys (green) or not (red). A hand-built site needs the same values as its `EVE_CLIENT_ID` and `EVE_CLIENT_SECRET` secrets.

!!! warning
    Keep your EVE **Secret Key** private — treat it like a password. It's write-only in the app and lives only on the site.

## Appearance

- **Theme** — tick which of the app's themes buyers may choose from; they pick one on the site with a header selector. **The store's theme is its own and has nothing to do with the theme your desktop is showing.** On the site the themes are named in the store's language.
- **About this store** — a blurb shown above the price list. Plain text is kept as written; a small set of **HTML** is welcome (`<b> <i> <u> <a href> <br> <p> <h2> <ul> <ol> <li> <hr> <img src> <table> <blockquote> <code>` and the mail markup's `<font color>`). Anything else — scripts, event handlers, unknown tags — is dropped, and open tags are closed.
- **Banner** — an optional image across the top of the price list, full page width and up to 300 px tall; about **1100 × 250** fits best. A large file is scaled down and sent as WebP.

## Language

The site speaks the store's **Language** (**Config ▸ General**; see [Stores](index.md#the-stores-language)): its pages and messages, the item and group names, and numbers and ISK written that language's way. A change reaches the site at the next sync.

This needs site version **0.1.13** or later. An older site shows English with item names in the store's language — press **Deploy or update site** to bring it up to date. A hand-built site updates from its releases.

## Going live

1. Switch on **Open on the web — publish to the site and take its orders**.
2. Set **who may order** on the **Restrictions** tab (the same policy as mail). *List* stores show nothing until a permitted buyer signs in.
3. Optionally tick **Also mail web buyers as their orders move** (needs the store's mailbox character).
4. Press **Sync now** to publish immediately; after that the app keeps the site current on its own. The status line reports the result.

## Listings on the site

Each of the store's [listings](index.md#listings) is a **tab** above the price list, in the store's order, headed with the listing's tab title or its posting's name. A Sell listing without either is headed *We sell*, a Buy listing *We buy*, and a Buy listing's tab is marked *buying*. Adding, removing or reordering listings reaches the site at the next sync.

Tabs and [Buy listings](buy-listings.md) need site version **0.2.0** or later. An older site shows only the store's first Sell listing — press **Deploy or update site** to bring it up to date.

## What buyers see

- They **sign in with EVE SSO** and see your price lists with per-item **in stock / in build / reserved** figures.
- **Placing an order** opens a dialog for one item type at a time (item, units, price each, total). If your store has a mailbox, a **"Keep me posted by EVE mail"** box lets them opt into mail updates.
- The **price shown at purchase is honoured** — the site prices from its stored catalogue copy, never from the browser.
- A buyer sees their **whole order history** — web, mail and manual orders in their name — and can **cancel any of their active orders**. Corporation orders are visible to, and cancellable by, that corporation's members.
- **Purchase limits** are enforced live: an item a buyer can no longer order is greyed out, and the units box holds what remains.
- On a **Buy listing**, sellers see what you pay and offer items to you instead of ordering. Their offers show on **My orders** as *You sell*, with the contract to make. See [Buy Listings](buy-listings.md#on-the-web-site).

## Orders, events and reviews

New orders, offers and cancellations come back to the app and are booked into the [Order Tracker](../tools/order-tracker.md) like any other. On the store **Overview** tab, a **Web site events** list shows what buyers did, with the **Item** each event concerns: an order's lines (*Rhea × 1, Ark × 2*), or the item of the order a cancellation is for.

- Orders that need a look (for example, an order that came in **over a purchase limit**, or priced well off the posting) are held for you with **Book it** / **Decline** buttons rather than booked on their own.
- Tick **Show visits** to include sign-ins and return visits in the list.
- A **[Store order events](../tools/alarms.md)** alarm can notify you when orders and offers arrive.
- The **Visits** and **Unique visitors** counts on the same tab come from these events. See [The Overview tab](index.md#the-overview-tab).

## Notes

- **Self-hosted, free tier.** The site is one Cloudflare Worker plus a D1 database; Cloudflare's free tier is plenty for a store. There is no hosting through eveconsole.com.
- **Deploying never touches orders.** Updates upload the newest site release and re-apply settings; the site migrates its own database additively on first request.
- **Nothing on the site reaches your database.** The app decides what the site may show and reads back only what buyers did.
- The two channels are independent: you can run the web store with or without the [EVE Mail Store](eve-mail.md).
