# Inventory Levels

A stockpile monitor: define target quantities for the items you want to keep on hand, and see at a glance how much you actually have versus your targets.

Open it from the left sidebar under **Assets**.

## What it shows

A single tree-style grid organised as **Collections → Groups → Items**.

- **Collections** are optional folders that hold groups. Groups with no collection appear under a synthetic **Default** collection.
- **Groups** define *where* and *from which sources* availability is counted, plus a **multiplier** applied to every item's target in the group.
- **Items** are the tracked types, one row each, with their target and current availability.

Item rows show these columns:

- **GROUP / ITEM** — the item name (groups and collections render their name and controls here).
- **TARGET** — the per-item target quantity you set.
- **TGT TOTAL** — the effective target, i.e. TARGET × the group's multiplier.
- **AVAIL** — total available across all counted sources.
- **DIFF** — AVAIL minus TGT TOTAL, coloured green when at/over target and red when short.
- **%** — the difference as a percentage of the target, over a bar filled to how much of the target is on hand. The bar's colour says how short it is.
- **ASSETS**, **IND JOBS**, **BUY ORDERS**, **CONTRACTS BUYING**, **SELL ORDERS**, **CONTRACTS SELLING** — the availability broken down by source: assets on hand, products of active industry jobs, quantities on your market buy orders, quantities on contracts you're buying through, units still listed on your own sell orders, and items on your own outstanding contracts that hand them over. A source the group doesn't count adds nothing to **AVAIL**. **ASSETS** is kept current between asset polls — see [How on-hand stock is counted](#how-on-hand-stock-is-counted).
- **MKT PRICE (TARGET)**, **MKT PRICE (AVAIL)**, **MKT PRICE (DIFF)** — what the target, what's available and the difference are worth at market prices.
- **BUILD PRICE (DIFF)** — what the difference comes to at build cost.
- **VOLUME - TARGET**, **VOLUME - AVAIL**, **VOLUME - DIFF** — the same three in m³.

Prices and volumes are abbreviated, and a zero in a source or total column is left blank.

**Group and collection lines** add up the items under them, whether open or closed:

- the totals, in each of those columns. A line's **DIFF** figures add up only what's short, so a surplus of one item doesn't hide a shortage of another;
- the **%** cell shows the items' average cover, each item counting once, and how many are short: *6 short*. Hover it for the short items, worst first, each with its target, what's available and a bar;
- hover a group's name for its full scope and sources, which a narrow column cuts off.

The toolbar carries **+ Add Group**, **+ Collection**, **Import Collection** (reads a collection from a file — always as a new collection, never merged into an existing one), and **Refresh** buttons, plus a status line.

## Using it

### Set up groups and collections

1. Click **+ Add Group** and configure it in the dialog:
   - **Scope** — where availability is counted: Station, System, Region, or Everywhere. For the first three you also pick a location; Everywhere counts across all of your holdings.
   - **Sources to include** — Assets, Industry Jobs (products), Market Buy Orders, Contracts Buying, Market Sell Orders, and Contracts Selling. Assets is on by default. See [Counting stock you're selling](#counting-stock-youre-selling) for the last two.
   - **Only count packaged items (skip assembled / fitted hulls)** — leave out assembled ships and other assembled items, so a hull you're flying doesn't count as stock. Blueprints are never filtered by this.
   - **Multiplier** — multiplies every item's target in the group (useful for "I want N sets of this").
   - Optionally assign the group to a collection.
2. Use **+ Collection** to create a named folder, then assign groups to it. A collection's **⋯** menu, shown when you hover or select its line, has **Expand all groups**, **Collapse all groups**, **Rename**, **Export** and **Delete**. **Export** saves its groups, scopes and item targets to a file, which **Import Collection** reads back.

### Add items to a group

A group's **⋯** menu, shown when you hover or select its line, has **Add item…** to add a single type, along with **Edit** and **Delete**. For bulk adds, right-click in the grid and use:

- **Add Items From Fit** — add a ship fit's hull and modules, from your characters' saved fittings in the game (characters need the fittings read scope).
- **Add Items From Market Group** — add every published item under a chosen market group (you are asked to confirm for very large groups).
- **Add Items From Blueprint** — add a blueprint's materials, either the direct inputs or the whole production chain, honouring runs and material efficiency.

Items already present in the group are skipped.

### Monitor and adjust

- Edit a row's **TARGET** inline; changes are saved automatically. Edit a group's multiplier inline the same way.
- Click **Refresh** to recompute availability from current data. Availability also refreshes automatically about once a minute.
- Click a column header to sort items within their groups.
- Right-click an item and choose **Open in Item Browser** to inspect it, or **Delete Item** to remove it.
- To send items elsewhere, highlight them and right-click: **Add to Production Calc Queue** adds them to the [Production Calculator](production-calculator.md)'s queue, and **Add to Standing Buy Orders…** to your [standing buy orders](standing-buy-orders.md). Both act on every highlighted item and leave you here, with a message saying what was added.

## Counting stock you're selling

Goods you list for sale leave your hangar, so by default they stop counting and the level asks for more. For a group you sell from, that's usually not what you want. Two sources in the group dialog count them as still yours:

- **Market Sell Orders** — units still listed on your open sell orders count as on hand until they sell. Shown in **SELL ORDERS**.
- **Contracts Selling** — items on your own outstanding item exchange and auction contracts count as on hand until a buyer accepts. They're counted where the contract starts. Shown in **CONTRACTS SELLING**.

Both are off by default. Tick them for a group whose stock you sell from, so listing it doesn't raise a restock.

## How on-hand stock is counted

**ASSETS** reads your assets, and they keep up with the game between asset polls: jobs started and delivered, contracts made, deleted or accepted, sell orders placed or cancelled, market purchases and hauls ticked off on the [Worklist](worklist.md#ticking-hauls-off) are written into them within minutes. So a job's output, or goods put on a sell order, show here before the next asset poll. See [What's written between polls](assets.md#whats-written-between-polls) for the full list and what still waits for the poll.

Two things are added on top, because they are in no hangar yet:

- **courier cargo entered by hand** (in the [Contracts](contracts.md) tool, or ticked off as contracted on the Worklist) counts at the destination while the courier is out;
- **blueprint copies** from delivered copy and invention jobs count, in runs, before the blueprint poll sees them.

Both follow the group's scope and owners, and the **Only count packaged items** setting; a count never drops below zero. The [Worklist](worklist.md#how-stock-is-counted), [Order Tracker](order-tracker.md) and [Sale Posting](sale-posting.md) read the same assets.

## Notes

- Availability is only as current as your synced data. Counting assets, industry-job products, market orders, and contracts requires the relevant characters/corporations to be authorized and synced via ESI.
- The **MKT PRICE** and **BUILD PRICE** columns come from your market configuration (see [Configuring Markets](../configuring-markets.md)); they are blank when no price is available.
- Related tools: the [Item Browser](item-browser.md) (opened from the item context menu) and [Assets](assets.md).
