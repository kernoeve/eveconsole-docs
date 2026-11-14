# Assets

A searchable, filterable browser over all of your synced assets across every authorized character and corporation, with valuation and location roll-ups.

Open it from the left sidebar under **Assets**.

## What it shows

The window has a **Scope** picker and a filter bar at the top, a set of tabs in the middle, and a status bar at the bottom.

**Scope** sets whose assets are searched: **Characters and personal corps** (the default — your own characters and the corporations marked personal) or **Everything** (every asset the app holds, other corporations included). The filters search within the scope, and your choice is remembered.

### Detailed View

One row per asset stack. Columns include:

- **Owner Type**, **Owner Name** — the character or corporation that holds the item.
- **Type Name**, **Group**, **Category** — the item and its SDE classification.
- **Quantity**.
- **Value Per Unit**, **Value** — ISK valuation of the stack (see valuation notes below).
- **Build Cost** — computed build cost of the type, when available.
- **Volume**, **Total Volume**, **ISK/m³**.
- **Location Name**, **Container**, **Flag** — where the item sits, including the nested container path (up to three levels deep; [grouping](#grouping) by **Location** goes further) and the inventory flag.
- **Solar System**, **Region Name**, **Security**, **Location Type**.
- **Is Singleton**, **Is Blueprint Copy**.
- **Since poll** — blank for a row as ESI last gave it. A row written since the last asset poll reads **Added** or **Changed**, with what did it: *Added (job 123456)*, *Changed (contract 789012)*, *Added (haul)*, *Changed (market order 345678)* or *Added (bought on the market)*. See [What's written between polls](#whats-written-between-polls).
- **Type Id**, **Item Id**, **Location Id** (identifier columns).

Blueprints and products tied to active, paused, or ready industry jobs are folded into the list as extra rows, flagged with `Industry Job` in the Flag column and located at the job facility.

The status bar says when the asset lists were current, by ESI's own time for the copies the polls fetched: *Current as of 14:05*, or *Current as of 13:12 to 14:05* when your characters and corporations were read at different times. When anything has been written since, it adds how many rows: *12 rows written since*.

#### Grouping

**Group by**, above the grid, folds the rows under headers:

| Group by | Rows fold under |
| --- | --- |
| **None** | Nothing: the plain grid, the default. |
| **Owner** | Each character or corporation. |
| **System** | Each solar system, with its region. |
| **Station** | Each station or structure. |
| **Location** | A full tree of where things sit: the station or structure (or the system, for things in space), then the owner, then every container down to the item. Corporation hangar divisions are shown by their names, along with deliveries, POS structures, ships, asset safety wraps and containers. It goes as deep as the items do. |

A group's row shows its item count and the totals of everything in it: quantity, value and volume. **Expand all** and **Collapse all** open and close every group, and open groups stay open as you sort and filter. A grouped view reads every matching row, so there are no pages to load.

### By Location / By System / By Region

Three aggregation tabs that group the (filtered) assets and sum them up:

- **By Location** — totals per station/structure/system, with Item Count, Total Volume, Total Value, and ISK/m³.
- **By System** — the same totals grouped by solar system.
- **By Region** — the same totals grouped by region.

## What's written between polls

Assets are read from ESI about once an hour, and ESI's copy can itself be up to an hour old. Things you do in the game in between are written into your assets as soon as the app hears of them, so this tool, the [Worklist](worklist.md#how-stock-is-counted), [Inventory Levels](inventory-levels.md#how-on-hand-stock-is-counted), the [Order Tracker](order-tracker.md) and the [stores](../stores/index.md) all see them before the next asset poll:

| What happened | What you see |
| --- | --- |
| **A manufacturing or reaction job started** | Its materials leave the hangar, worked out from the blueprint's ME, and the blueprint goes into the job. |
| **A research, copying or invention job started** | The blueprint goes into the job. Invention's datacores and decryptors are left to the poll. |
| **A job delivered** | What it made appears in the hangar: items, or blueprint copies. The blueprint comes back, unless it was a copy whose runs are used up. |
| **A sell order placed** | The units it lists leave the hangar. |
| **A sell order cancelled or expired** | What was left on it comes back. |
| **Something bought on the market** | It appears where it was bought. A character buying for the corporation counts once, under the corporation. |
| **A contract made** | The goods on it leave the hangar; for a courier, only cargo you [entered by hand](contracts.md#courier-cargo). Deleted again, they come back. |
| **An item exchange accepted** | Goods move both ways: what was offered to the acceptor, what was asked for to the issuer. |
| **A courier delivered** | Its cargo, if you entered it by hand, appears at the destination. |
| **A haul ticked off as delivered** on the Worklist | The goods move to where you put them down. |

Industry jobs and contracts are read about every five minutes, market orders every twenty and wallet transactions about once an hour, so that is how soon each shows here. The next asset poll replaces it all with what ESI then reports, and only what happened after ESI made that copy is written on top again.

How a written row looks:

- **What arrives is its own row**, marked **Added**, in the corporation's first hangar division or the character's hangar. A job's output goes where the job puts it. It has a made-up negative **Item Id** until the poll gives the real one.
- **What leaves comes off the stacks already there**, which then read **Changed**. A stack used up is gone. Nothing is ever taken out of a ship.

What still waits for the asset poll:

- moving items between hangars, containers and ships, trading them, or anything else in the game that isn't one of the above;
- cargo still on a courier, which is on no shelf until the courier is delivered;
- items sold straight into someone's buy order, since nothing says which hangar they came from;
- a Worklist [Transfer](worklist.md#transfers-and-character-levels) once you've done it.

## Using it

- **Filtering** — the filter bar starts with one filter row. Pick a column, choose an operator, and type a value. Operators are: Contains, Does Not Contain, Equal, Not Equal, Greater Than, Greater Than or Equal, Less Than, Less Than or Equal. Press **+ Filter** to add more rows (up to 10); multiple rows are combined with AND. Click **Apply** (or press Enter in a value box) to run the filters, and **Clear** to reset. The same filters drive both the Detailed View and the three aggregation tabs.
- **Sorting** — click a column header. In the Detailed View sorting is applied across the whole result set in the database; in the aggregation tabs it sorts the loaded rows.
- **Paging** — results load in pages of 5,000 rows. The status bar shows how many of the total are loaded; scroll to the bottom or press **Load More** to fetch the next page.
- **Selecting and copying** — click and drag to select a rectangular block of cells (Shift-click extends the selection). Use the row-selector column at the far left to grab whole rows. Copy with Ctrl+C or the right-click **Copy** / **Copy w/Headers** menu.
- **Open in Item Browser** — double-click a row in the Detailed View, or right-click and choose **Open in Item Browser**, to jump to that type in the [Item Browser](item-browser.md).

## Notes

- Assets come from synced ESI data, so you must have authorized characters and/or corporations with the relevant asset scopes. Items only appear after an asset sync has run.
- This tool shows the assets as ESI last reported them, with what has happened since written on top (see [What's written between polls](#whats-written-between-polls)). The tools that count stock read the same rows, so their figures match what you see here, apart from courier cargo still in transit, which they count as on its way.
- If several PCs share one [PostgreSQL database](../storage-postgresql.md), run the same version of EVE Console on all of them, so they all write the activity above the same way.
- **Valuation** depends on the asset-value price source configured in your market settings (see [Configuring Markets](../configuring-markets.md)). Blueprint copies are valued at 0; blueprint originals use the NPC base price; other items use the configured market price, falling back to build cost plus a markup when no market price is available. If no asset-value source is set, market-derived values will be missing.
- Location, system, and region names resolve from the SDE and from synced structure names. Unresolved locations show a placeholder such as `<Unresolved - Please Refresh>` until the next sync.
