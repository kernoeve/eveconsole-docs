# Industry Opportunities

Find what is worth building: every item that shows a profit at your chosen market, with what it has actually sold for over the last 30 days. The left-nav label is **Industry Opportunities**; the tab reads **Industry Opps**.

Open it from the left sidebar under **Industry**.

The tool has two tabs, both filled by one calculation:

- **Summary** — what sold at a profit in the last 30 days, in ten lists by kind of item.
- **Detail** — every item the calculation found, with all the columns and its own filters.

The calculation runs by itself the first time you open the tool in a session. After that, set the controls along the top and click **Refresh**.

## The controls along the top

These apply to both tabs, and take effect at the next **Refresh**:

- **Mode** — *Build & Sell Order* prices against the lowest sell order; *Build & Sell to Buy Order* prices against the highest buy order (items with no buy orders are skipped in that mode).
- **Price at** — the market pricing config to value output against (these are your configured market sources).
- **Min 30d ISK Vol** / **Min 30d Unit Vol** — optional thresholds to hide thin, illiquid items. Leave blank for no filter.
- **Min Margin %** — only items whose **Margin** is at least this. `15` and `15%` both mean fifteen percent.
- **Min Margin % 30d** — only items whose **Margin 30d** is at least this. An item that didn't sell in the last 30 days has no such margin, so it's left out while this is set.
- **Skip Non BPO traceable Items** — keeps only items whose blueprint is a buyable BPO, or is invented from one (e.g. T2 from a T1 BPO). Excludes faction/limited-run BPC items with no obtainable BPO, storyline, officer and deadspace items, and "Limited Time" event items whose blueprint can no longer be bought. On by default.
- **Only blueprints I own** — only items whose own manufacturing or reaction blueprint, an original or a copy, is held by one of your characters or a corporation marked personal: what you can start without buying a print first. An original you would have to invent from doesn't count. Off by default.

The footer summarises the result count and the pricing market, and notes how many rows were priced from 30-day history.

## Summary tab

Ten lists, two to a row. Each holds **every** item of its kind that sold at a profit over the last 30 days, most profit first, and scrolls if it's long:

| | |
| --- | --- |
| **T1 Ships — Large & Capital** | **T1 Ships — Small & Medium** |
| **T2 Ships — Large & Capital** | **T2 Ships — Small & Medium** |
| **Ammo & Drones** | **Modules** |
| **Rigs & Subsystems** | **Deployables** |
| **Components** | **Structure Modules & Rigs** |

Ships are sorted by hull size as the engineering rigs class them: frigates to battlecruisers are small and medium; battleships, freighters, industrial command ships and capitals are large. A faction ship is in neither tech list.

Columns: **Item**, **Build Cost**, and under *Sales Over the Past 30 Days*: **Units**, **Avg Price**, **Margin**, **Sales** and **Profit**.

The controls along the top apply here. The Detail tab's filters don't: the Summary covers every meta group and market group.

## Detail tab

Each row is one item where building it and selling it turns a profit at your chosen market. Only items that show a profit at that price are listed. Its 30-day figures can still be red, if it actually sold for less than it costs to build.

| Column | Meaning |
| --- | --- |
| Item | The item to build. Click the name to open it in the [Item Browser](item-browser.md). |
| Build Cost | Cached total build cost for one unit. |
| Sell Price | The market number you'd sell into. A `*` means the item has no live sell orders and was priced from its 30-day trade history instead. |
| Profit / Unit | Sell Price − Build Cost. |
| Margin | Profit as a percentage of build cost. |
| Build Time | Time to build one unit. |
| Slot Days | Build Time expressed in days (the time one manufacturing slot is tied up). |
| Profit / Slot Day | Profit per unit ÷ Slot Days. |
| Units Sold 30d | Units traded in the pricing region over the last 30 days. |
| Avg Price 30d | What those units sold for on average: Sales 30d ÷ Units Sold 30d. |
| Margin 30d | The margin at that average price, against build cost. Red when it's a loss. `–` when nothing sold. |
| Sales 30d | ISK traded in the pricing region over the last 30 days. |
| Profit 30d | Sales 30d less the build cost of every unit sold. Red when it's a loss. The default sort, highest first. |

Click any column header to re-sort. Double-click a row to open that item in the Item Browser.

### The Detail tab's filters

These narrow the list above as you change them, with no need to click **Refresh**:

- **Meta Groups** — a dropdown of tick boxes: Tech I, Tech II, Tech III, Faction, Storyline, Abyssal, Structure Tech I, Structure Tech II, Structure Faction and None (materials, components…). Every group but Faction is ticked to start, since faction items are mostly ME0 copies that are often not worth building. An item in a group not on the list, such as officer or limited-time items, never appears.
- **Exclude Groups** — add market groups (and everything nested under them) to leave out; remove a chip with its ✕.
- **Include Groups** — when any are chosen, only items in these market groups or the groups under them. **Exclude Groups** still apply inside them, so you can include a group and exclude part of it.
- **Item name** — type all or part of a name. The list narrows as you type; case and accents don't matter. Beside the box, **Showing *12* of *840*** says how many rows the filter leaves.

## Sending items to other tools

On any grid, on either tab, highlight one or more rows (Ctrl-click, Shift-click) and right-click:

- **New Production Calc Queue** — empties the [Production Calculator](production-calculator.md)'s queue, puts these items in and takes you there.
- **Add to Production Calc Queue** — adds them after what's queued and leaves you here, saying how many were added.
- **Add to Standing Buy Orders…** — adds them at the station of your last [standing buy order](standing-buy-orders.md).

A right-click on a row that isn't highlighted acts on that row alone. **Ctrl+C** copies the highlighted rows.

## What is remembered

**Price at**, **Mode**, the volume and margin boxes, the tick boxes, **Meta Groups**, the group lists and the sort are all kept, so they're as you left them when you come back to the tab or restart the app. The **Item name** filter isn't: it starts empty each time, so no rows seem to be missing.

## Posting it

The [Scheduler](scheduler.md) has an **Industry Opportunities** section that posts a table of these results to Discord or Slack. The section keeps its own filters and never reads the ones set here.

## Notes

- Build cost and build time are read from your cached build costs, computed for the default industry park — set one up under [Indy Parks](../industry-parks.md) and configure a market under [Configuring Markets](../configuring-markets.md) for accurate numbers. A T2 item's build cost includes what inventing its copy costs.
- The 30-day columns and filters, and the fallback pricing for items with no sell orders, rely on market history that the app caches in the background; if it hasn't run yet, those figures may be missing, and the Summary lists stay empty.
- The 30-day filters need the pricing config's region to resolve — if it can't, the scan reports that instead of applying them.
- Once you've picked a target, model it in detail with the [Production Calculator](production-calculator.md), and track the resulting builds in [Industry Jobs](industry-jobs.md).
