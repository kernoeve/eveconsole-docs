# Configuring Markets

Markets are the foundation for almost everything price-related in EVE Console —
Trade Opportunities, Net Worth, build costs, the Production Calculator, and the
Item Browser all read from the prices produced here.

A **price source** answers two questions:

1. **Where do orders come from?** — an entire ESI region, or a single
   player-owned structure.
2. **How is the raw order book cleaned up?** — an optional high/low percentile
   filter that trims outlier orders before a price is computed.

You then choose, once, **which source values your assets** and **which source
prices your manufacturing inputs**, and how gaps are filled when the market has no
orders for an item.

All of this lives in **Settings** — click the **⚙** gear button in the top-right
of the title bar, then open the **Market** tab.

!!! tip "Recommended setup"

    A fresh install of EVE Console already has two Region sources: **The Forge**
    (Jita's region) and **Domain** (Amarr's). Both have the high/low filter on at 1 %.
    **Asset Value** and **Manufacturing Cost** both default to **The Forge / Sell**,
    which is the recommended choice, so you normally don't need to change them. Keep
    The Forge even if you trade elsewhere, because asset valuation uses it.

    If there's a market you regularly use **outside Jita** — another region, or your
    home player structure — add it as its own source as well. Several tools compare two
    markets (for example **Trade Opportunities**), so they only become useful once you
    have a second source to compare against.

## Key concepts

- **Price source (method)** — each source pulls order data one of two ways:
    - **Region** — all public orders for an entire region, from ESI. Use this for
      NPC trade hubs (e.g. **The Forge** for Jita). Orders placed *inside*
      player-owned structures aren't included; only regional buy orders posted from
      structures appear.
    - **Player Structure** — every order inside one player-owned structure (citadel,
      engineering complex, etc.). Requires an auth character with docking access.
      Use this for null-sec staging keeps and other private markets.
- **High/low percentile filter** — thinly-traded items (capitals, supers, titans)
  often carry a few garbage orders far from real value. Enabled per source, it
  discards the extreme *N* % of the book: sell price becomes the *N*-th-percentile
  cheapest order, buy price the *(100−N)*-th-percentile highest. Sources you add
  yourself start at 5 %; the two seeded sources use 1 %.
- **Default pricing** — separately from the sources, you pick which source (and
  whether **Buy**, **Sell**, or **Split** — the midpoint of buy and sell) drives
  **asset valuation** and which drives **manufacturing cost**.
- **Missing-price markup** — a build-cost floor for items the market can't price:
  `price = build cost × (1 + markup%)`.

> NPC-seeded sell orders (which never expire) are excluded from pricing so that
> anonymous NPC orders don't drag prices toward seed value.

!!! note "Fuzzwork sources from older versions"

    Earlier versions also offered a **Fuzzwork** method, which read pre-computed
    percentile prices from fuzzwork.co.uk. You can no longer pick it for a new source,
    but an existing Fuzzwork source still refreshes. It stores one price per item and no
    individual orders, so the Item Browser's **Market Orders** tab needs a Region or
    Player Structure source instead.

## Adding a price source

1. Open **Settings ▸ Market**. Existing sources are listed on the left under
   **Price Sources**; click **Add** to create a new source, then fill in its
   details on the right.
2. In the edit panel on the right, pick a **Method**: **Region** or **Player
   Structure**. A short note explains each one, and the fields below adapt to your
   choice.
3. Set a **Location Name** — a friendly label such as *Jita 4-4* that appears in
   the source list and the Default Pricing dropdowns.
4. Point the source at a location, depending on the method:
    - **Region** — choose from the **Region** dropdown (e.g. *The Forge*).
      Optionally set a **Station Filter** to restrict prices to one station; the
      list is populated *after* the source's first refresh.
    - **Player Structure** — enter the structure's **Location ID**; the resolved
      name appears automatically a moment after you stop typing. Don't know the ID?
      Expand **Find Location by Name…**, search, pick a result, and click **Use
      Selected**. This method also needs an **Auth Character** with docking access —
      select one from the dropdown (structure lookups fail without it).
5. Leave **Filter High/Low Orders** on (default) unless you have a reason not to,
   and adjust **Filter %** if needed (0.1–25, default 5).
6. Make sure **Enabled** is ticked, then click **Save**.
7. Click **Refresh This** to pull prices now (or **Refresh All** at the bottom to
   refresh every source). The **Last refresh** and **Status** lines report the
   result.

<!--
  SCREENSHOT SLOTS (add files to docs/images/, then uncomment):

  ![Market configuration](images/market-config.png)
  ![Price type and outlier filtering](images/market-price-type.png)
-->

## Setting default pricing

The **Default Pricing** panel (below the source list) decides how the rest of the
app turns sources into the single price it needs:

- **Asset Value** — the source and price type (**Split** / **Buy** / **Sell**)
  used for Net Worth and asset valuation. Defaults to **The Forge / Sell**.
- **Manufacturing Cost** — the source and price type used when pricing build
  inputs. Defaults to **The Forge / Sell**, which is what you'd pay to buy the
  materials.
- **Missing Price Markup** (default 15 %) — applied when the market has no sell
  orders for an item: `price = build cost × (1 + markup%)`. If there are no buy
  orders, buy falls back to sell.
- **Filter lowball buy orders below N % of build cost** (on by default, 10 % on a
  fresh install) — drops absurd buy orders from the *buy* price calculation. It
  applies to Region and Player Structure sources only. Those orders still show in
  the market UI; they're just ignored when computing a price.

Click **Save Defaults** after changing anything here.

## Build costs

EVE Console stores a build cost for every manufacturable item, worked out from your
[industry park](industry-parks.md) and the **Manufacturing Cost** source above. Build
costs are recalculated **automatically after every market refresh**.

To force an update, for example after changing pricing or your industry park, open
**Settings ▸ Industry** and click **Recalculate Build Costs** under **Build Costs**. The
line beside the button reports progress.

The same tab has a **Production Calculator** option: **Purchase a component instead of
building when its market value is ≤ N % of build value** (off by default, 100 %). When
it's off, the calculators build every component they can, and buy only the items that
genuinely can't be costed. When it's on, a component whose market value is at or below
that share of its build cost is bought instead of built. It's off by default because
component markets move a lot, and a few cheap units don't guarantee the quantity you
need at that price. Click **Save** at the bottom of the tab after changing it.

## Price history

The **Settings ▸ Price History** tab lists the **Price History Regions**. A background
job refreshes the last 30 days of market history for every traded item in these
regions, once every 24 hours per item, so the opportunity tools and the Item Browser's
**Price History** tab can read it from the database. **The Forge** and **Domain** are
set up on a fresh install.

- To add a region, pick it from the dropdown and click **Add Region**. To stop
  collecting a region, click **Remove** on its row.
- The job paces itself against ESI's error limit, so a large region such as The
  Forge fills in gradually over several sessions.
- Watch progress on the **Price History** tab of
  [Background Processes](tools/background-processes.md).

## Related

- [Industry Parks](industry-parks.md) — build costs feed the missing-price markup and
  lowball filter above.
- [Production Calculator](tools/production-calculator.md)
- [Browse all tools](index.md)
