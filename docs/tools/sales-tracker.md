# Sales Tracker

Reviews everything you've sold — market (wallet) sell transactions and finished item-exchange contracts — with each sale's build cost, market value, and profit. A shared filter bar drives three tabs: a **Summary** of rollups and charts, **By period** totals with for-profit and not-for-profit sales side by side, and a **Detail** grid of individual sales.

Open it from the left sidebar under **Market / Trade**.

## Filters

The filter bar sits above the tabs and governs all of them:

- **From** / **Thru** — date range (`yyyy-MM-dd`). Defaults to the last year; leave **Thru** blank for "up to now."
- **Owner** — *All*, *All Characters and Personal Corps* (the default), or a specific tracked character or corporation. Characters and corporations you add or remove appear or go at once; the owner you picked stays picked unless it is the one removed.
- **Sale Type** — *All types*, *Market*, or *Contract*.
- **Profit based on** — the cost basis the profit figures measure against, everywhere on the screen:
    - **Build** — profit versus the item's build cost (the default).
    - **Market** — profit versus the item's market value.
- **Show not for profit** — include sales you've marked *not for profit* (see [Detail](#detail)). When ticked, they count everywhere — summaries, charts and grid alike. [By period](#by-period) always counts them, on their own side.
- **Item groups** — narrow every tab to sales of items under chosen market groups. Click **+ Group**, pick a market group and click **Add group**; each group shows as a chip, and its **×** removes it. A sale counts when its item sits anywhere under one of the groups, so *Capital Ships* takes every capital hull. A contract counts under its most valuable item (see [how a contract is filed](#how-a-multi-item-contract-is-filed)). With no group chosen, every sale counts.

## Summary

**Three rollup panels**, each summarising the currently filtered sales:

- **Top Buyers** — buyers ranked by total ISK bought from you (opens each in the [entity browser](entities.md)).
- **Profit by Market Group** — sales grouped by the item's market group (two levels up, e.g. a Revelation rolls up to *Standard Dreadnoughts*), with summed profit and average profit %.
- **Profit by Item** — the same profit summary per item (opens each in the [Item Browser](item-browser.md)).

**Two charts** below them, over the same filtered sales:

- **Costs, sales and profit** — totals over time in ISK.
- **Margin** — profit margin as a percentage (kept on its own chart so ISK figures in the billions don't flatten it).

A **Chart by** selector buckets the charts by **Daily**, **Weekly** or **Monthly**. A note flags any sales that couldn't be costed (no price snapshot), since those are left out of the chart maths.

## By period

Your sales period by period, with the for-profit and not-for-profit sides next to each other, for a monthly report or a summary to post in a chat. Not-for-profit sales always count here, whatever **Show not for profit** says: the mark only decides which side a sale is on.

Above the table:

- **Rows** — **Daily**, **Weekly** (from Monday) or **Monthly** (the default). This is separate from the charts' **Chart by**.
- **Split by** — what each period is broken into, under its own line: **None**, **Tag** (the default), **Market group**, **Item**, **Buyer** or **Owner**.
- **For-profit share by** — what the share is a share of: **Cost** (the default), **Sale ISK** or **Units**.
- **Copy as text** copies both tables as plain text in a code block, ready to paste into a chat. **Export CSV** saves them as a CSV file, numbers unrounded.

Four cards sum up the whole range: **Units** (with the ISK they sold for), **For profit** (units, with the profit and profit %), **Not for profit** (units, with the ISK they sold for) and **For-profit share**.

**The period table** has a line for each period from the first sale to the last, a quiet one included, then its splits indented beneath it, and a **Total** line at the end. The current week or month reads *to date*. Its columns come in three groups:

| Group | Columns |
| --- | --- |
| **All sales** | **Units**, **Sale ISK**, **For-profit share** (with a bar) |
| **For profit** | **Units**, **Sale ISK**, **Cost**, **Profit**, **Profit %** |
| **Not for profit** | **Units**, **Sale ISK** |

**Cost** is the **Profit based on** basis from the filter bar, as of each sale's day, and **Profit %** is profit over that cost. Sales with no cost are left out of cost and profit.

**Units sold** below it counts units period by period, one column a period plus a **Total**, by what you choose in **Count by**: **Market group** (the default), **Item**, **Tag**, **Buyer** or **Owner**. Each cell gives the units, then the for-profit and not-for-profit split in brackets: *12 (9·3)*. Only items in the chosen item groups count, so a carrier sold with its fittings is one carrier, not one carrier and forty modules.

!!! note "Tags are just text"
    A split or count by **Tag** uses a sale's **Labels**. A sale with no label is under **No tag**. A sale with two labels shows under both, but counts once in its period and in the total, so a period's splits can add up to more than the period.

## Detail

One row per sale, newest first:

- A marker in the first column flags a sale you've set **not for profit**.
- **Date / Time** — when the sale happened (UTC).
- **Type** — `Market` for a wallet sell transaction, `Contract` for a finished item-exchange contract sold for ISK.
- **Owner** — the character or corporation that made the sale.
- **Location** — the station or structure the items sold at (for contracts, the items' start location).
- **Buyer** — the client (market) or acceptor (contract).
- **Item(s)** — the item sold; a multi-item contract shows its most valuable item plus a `+N more items` note. See [how a contract is filed](#how-a-multi-item-contract-is-filed).
- **Units** — quantity sold (`Multiple` for a multi-item contract).
- **Total Sale** — what the sale brought in.
- **Build Price** / **Market Price** — the item's build cost and market value at the time of the sale, from the nearest daily price snapshot (`—` when none was available).
- **Profit** / **Profit %** — the sale total minus the chosen cost basis. Green when positive, red when negative, `—` when the basis is unknown.
- **Labels** — colour-coded tags (the same tags, and the same colours, as the [Order Tracker](order-tracker.md)). Add or remove them by right-click.
- **Contract** — the contract behind a contract sale (blank on market rows); opens in the [Contracts](contracts.md) tool.

**Owner**, **Location**, **Buyer** and **Item(s)** open the thing they name. Right-click a row (or several) to **Mark as not for profit** / **Restore to profit**, or to **Add label** / **Remove label**.

### How a multi-item contract is filed

A contract sold as one sale is filed under its most valuable item: that item names the row, and its type and market group are where the whole sale counts in **Profit by Market Group** and **Profit by Item**. Items are ranked by worth, using market value, else build cost, else CCP's adjusted price. So a hull sold with its rigs counts as a hull sale, not a rig sale. The Sale Listing panels on the [Overview](overview.md) name a contract the same way.

## Notes

- Sales data comes from your synced wallet transactions and contracts, so it appears only once the relevant characters/corporations are authorized via EVE SSO and their data has been pulled. The tracker refreshes itself every few minutes.
- Build cost and market value depend on daily price snapshots, which rely on your configured market price sources — see [Configuring Markets](../configuring-markets.md). Sales of items with no snapshot show `—` for cost and profit, and are excluded from the charts.
- A corp trade a character executes is recorded once, under the corporation, to avoid double-counting.
- Marking sales **not for profit** (gifts, corp transfers, break-even moves) keeps them out of your profit figures without deleting them; the filter checkbox brings them back when you want to see them.
- The Sales Tracker is backward-looking: sales already made. For orders you've *committed to deliver* and their fulfilment, see the [Order Tracker](order-tracker.md).
