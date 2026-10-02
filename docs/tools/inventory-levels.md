# Inventory Levels

A stockpile monitor, in the style of jEveAssets' stockpiles: define target quantities for the items you want to keep on hand, and see at a glance how much you actually have versus your targets.

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
- **%** — the difference as a percentage of the target.
- **ASSETS**, **IND JOBS**, **BUY ORDERS**, **CONTRACTS** — the availability broken down by source (assets on hand, products of active industry jobs, quantities on market buy orders, and quantities on contracts you're buying). **ASSETS** is kept current between asset polls — see [How on-hand stock is counted](#how-on-hand-stock-is-counted).
- **MKT PRICE**, **BUILD PRICE** — per-unit market and build prices for the type.
- **VOLUME (m³)** — per-unit volume.

The toolbar carries **+ Add Group**, **+ Collection**, **Import Collection** (reads a collection from a file — always as a new collection, never merged into an existing one), and **Refresh** buttons, plus a status line.

## Using it

### Set up groups and collections

1. Click **+ Add Group** and configure it in the dialog:
   - **Scope** — where availability is counted: Station, System, Region, or Everywhere. For the first three you also pick a location; Everywhere counts across all of your holdings.
   - **Sources to include** — Assets, Industry Jobs (products), Market Buy Orders, and Contracts Buying. Assets is on by default.
   - **Only count packaged items (skip assembled / fitted hulls)** — leave out assembled ships and other assembled items, so a hull you're flying doesn't count as stock. Blueprints are never filtered by this.
   - **Multiplier** — multiplies every item's target in the group (useful for "I want N sets of this").
   - Optionally assign the group to a collection.
2. Use **+ Collection** to create a named folder, then assign groups to it. Collections can be renamed, deleted, and expanded/collapsed as a whole. A collection's **Export** saves its groups, scopes and item targets to a file, which **Import Collection** reads back.

### Add items to a group

Each group row has a **+ Item** button to add a single type. For bulk adds, right-click in the grid and use:

- **Add Items From Fit** — add a ship fit's hull and modules, from your characters' saved fittings in the game (characters need the fittings read scope).
- **Add Items From Market Group** — add every published item under a chosen market group (you are asked to confirm for very large groups).
- **Add Items From Blueprint** — add a blueprint's materials, either the direct inputs or the whole production chain, honouring runs and material efficiency.

Items already present in the group are skipped.

### Monitor and adjust

- Edit a row's **TARGET** inline; changes are saved automatically. Edit a group's multiplier inline the same way.
- Click **Refresh** to recompute availability from current data. Availability also refreshes automatically about once a minute.
- Click a column header to sort items within their groups.
- Right-click an item and choose **Open in Item Browser** to inspect it, or **Delete Item** to remove it. Groups and collections have their own Edit / Rename / Delete controls on their rows.

## How on-hand stock is counted

Assets are read from ESI once an hour with the default timers, while industry jobs and contracts are read every five minutes. Between asset polls, **ASSETS** is corrected for what has already happened in the game:

- output of **jobs delivered** since the poll is added at the facility the job ran in;
- goods on a **contract made** since the poll are taken off, and put back if the contract is **deleted**;
- an **item exchange accepted** since the poll moves goods both ways — what was offered to the acceptor, what was asked for to the issuer;
- goods on a **courier contract delivered** since the poll are counted at the destination.

Each correction follows the group's scope and owners, and the **Only count packaged items** setting; a count never drops below zero. Blueprints are counted in runs: copies from delivered copy and invention jobs are added, but blueprints moved by contracts are left to the asset poll. The [Worklist](worklist.md#how-stock-is-counted), [Order Tracker](order-tracker.md) and [Sale Posting](sale-posting.md) count stock the same way.

## Notes

- Availability is only as current as your synced data. Counting assets, industry-job products, market buy orders, and contracts requires the relevant characters/corporations to be authorized and synced via ESI.
- **MKT PRICE** and **BUILD PRICE** come from your market configuration (see [Configuring Markets](../configuring-markets.md)); they are blank when no price is available.
- Related tools: the [Item Browser](item-browser.md) (opened from the item context menu) and [Assets](assets.md).
