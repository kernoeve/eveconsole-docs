# Trade Opportunities

Finds profitable station-to-station hauls by comparing cached sell orders at a source station against buy or sell orders at a destination, then turns the best items into a shopping list — limited, if you like, by your hold, your budget and how much the destination actually sells.

Open it from the left sidebar under **Market / Trade**.

## What it shows

A results grid, one row per item type worth hauling, sorted by total profit by default:

| Column | Meaning |
|--------|---------|
| **Item** | Type name. Double-click a row to open it in the Item Browser. |
| **Sell Price** | Cheapest sell-order price at the source station (your buy cost per unit). |
| **Dest Price** | The destination price you sell into — the best buy-order price, or the cheapest destination sell price, depending on mode. |
| **Profit / Unit** | Dest price minus source sell price. |
| **Profit / m³** | Profit per unit divided by packaged volume — the ranking metric for the underlying scan. Abbreviated like the other ISK figures (for example *12.35B*). |
| **Qty** | Units to buy, capped by available orders, cargo space, your ISK budget and the destination's sales (see **Max Buy** below). |
| **Volume (m³)** | Total packaged volume for that quantity. |
| **Total Cost** | Quantity × source sell price. |
| **Total Profit** | Quantity × profit per unit. |
| **Dest Units Sold 30d** | Units traded in the destination's region over the last 30 days. |
| **Dest ISK Sold 30d** | ISK traded in the destination's region over the last 30 days — the room a sell order there has, which matters most for **Undercut Sell Order**. |

A footer summary (shown after a run) gives loaded **Volume** (used / cargo, or just the volume when no cargo is set), total **Cost**, and total **Profit**. A status line reports the item-type count and m³ loaded, or messages such as no opportunities found.

## Using it

1. **Mode** — choose how the destination price is evaluated:
    - **Buy Sell → Sell to Buy Order** — buy from source sell orders, sell into destination buy orders. Only destination buy orders priced above the source cost are counted (junk 1-ISK orders are ignored).
    - **Buy Sell → Undercut Sell Order** — buy from source sell orders and resell against the destination's own sell orders (only where the destination sell price beats your cost).
2. **From** / **To** — pick the source and destination stations (type to filter). Only stations with cached orders appear; they must be different.
3. **Cargo (m³)** — your hauler's capacity (60000 to start). The list is packed to fit. Leave it empty for no volume limit: every profitable item is then listed at what is on offer.
4. **ISK Cap** — optional budget ceiling; leave blank for no limit.
5. **Min 30d ISK Vol** / **Min 30d Unit Vol** — optional liquidity filters that drop items whose 30-day traded volume (ISK or units) in the destination region falls below the threshold.
6. **Max Buy (Days of Dest Sales)** — buys no more of an item than the destination's region sold in this many days. It starts at **30**, a month's sales, and takes any whole number of days; leave it empty for no cap. Buying a thousand of something the destination sells three of a month is stock for years.
7. **Exclude Groups** — click **+ Add Group** to exclude a market group and everything nested under it (e.g. skip Blueprints or Ships). Excluded groups appear as chips; click **✕** to remove one. Exclusions are saved between sessions.
8. Click **Calculate**. A progress overlay shows while the scan runs.

The algorithm walks candidate items from best profit-per-m³ downward, buying as many units of each as available orders, remaining cargo, remaining ISK and the **Max Buy** cap allow, until the hold or budget is full. Click any column header to re-sort the results.

With **Max Buy** set, an item the destination sold none of in that many days drops out. An item whose sales history hasn't been read yet isn't capped at all, so check its **Dest Sold 30d** columns before buying a lot of it. The two **Dest Sold 30d** columns stay 30-day figures whatever the **Max Buy** window.

To find one item in the results, type all or part of its name in the **Item name** box under the excluded groups. The list narrows as you type, with no need to calculate again; case and accents don't matter. Beside the box, **Showing *12* of *840*** says how many rows the filter leaves. The filter only narrows what the grid shows: the footer's volume, cost and profit are still the whole list's. It isn't remembered between sessions, so no rows seem to be missing next time.

## Notes

- This tool **compares two markets**, so you need cached orders for **both** the source and destination stations. Make sure you have at least two market price sources configured and refreshed — see [Configuring Markets](../configuring-markets.md).
- The **Dest Sold 30d** columns, the **Min 30d** volume filters and the **Max Buy** cap read market history for the **destination region**, cached in the background — no ESI calls are made while you calculate. If the destination's region can't be worked out, the columns read 0 and nothing is capped; with a **Min 30d** filter set, the calculation stops with a message instead — refresh market data for the destination, or clear the filters.
- Prices reflect the last cached order sweep; they are a snapshot, not a live quote, so verify in-game before committing to a large haul.
- Related tools: [Market Overview](market-overview.md) for regional demand context, and [Market Levels](market-levels.md) for watching restock levels at a single station.
