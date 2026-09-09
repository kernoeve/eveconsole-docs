# Sales Tracker

Reviews everything you've sold — market (wallet) sell transactions and finished item-exchange contracts — with each sale's build cost, market value, and profit. A shared filter bar drives two tabs: a **Summary** of rollups and charts, and a **Detail** grid of individual sales.

Open it from the left sidebar under **Market / Trade**.

## Filters

The filter bar sits above both tabs and governs both:

- **From** / **Thru** — date range (`yyyy-MM-dd`). Defaults to the last year; leave **Thru** blank for "up to now."
- **Owner** — *All*, *All Characters and Personal Corps* (the default), or a specific tracked character or corporation.
- **Sale Type** — *All types*, *Market*, or *Contract*.
- **Profit based on** — the cost basis the profit figures measure against, everywhere on the screen:
    - **Build** — profit versus the item's build cost (the default).
    - **Market** — profit versus the item's market value.
- **Show not for profit** — include sales you've marked *not for profit* (see [Detail](#detail)). When ticked, they count everywhere — summaries, charts and grid alike.

## Summary

**Three rollup panels**, each summarising the currently filtered sales:

- **Top Buyers** — buyers ranked by total ISK bought from you (opens each in the [entity browser](entities.md)).
- **Profit by Market Group** — sales grouped by the item's market group (two levels up, e.g. a Revelation rolls up to *Standard Dreadnoughts*), with summed profit and average profit %.
- **Profit by Item** — the same profit summary per item (opens each in the [Item Browser](item-browser.md)).

**Two charts** below them, over the same filtered sales:

- **Costs, sales and profit** — totals over time in ISK.
- **Margin** — profit margin as a percentage (kept on its own chart so ISK figures in the billions don't flatten it).

A **Chart by** selector buckets the charts by **Daily**, **Weekly** or **Monthly**. A note flags any sales that couldn't be costed (no price snapshot), since those are left out of the chart maths.

## Detail

One row per sale, newest first:

- A marker in the first column flags a sale you've set **not for profit**.
- **Date / Time** — when the sale happened (UTC).
- **Type** — `Market` for a wallet sell transaction, `Contract` for a finished item-exchange contract sold for ISK.
- **Owner** — the character or corporation that made the sale.
- **Location** — the station or structure the items sold at (for contracts, the items' start location).
- **Buyer** — the client (market) or acceptor (contract).
- **Item(s)** — the item sold; a multi-item contract shows the first item plus a `+N more items` note.
- **Units** — quantity sold (`Multiple` for a multi-item contract).
- **Total Sale** — what the sale brought in.
- **Build Price** / **Market Price** — the item's build cost and market value at the time of the sale, from the nearest daily price snapshot (`—` when none was available).
- **Profit** / **Profit %** — the sale total minus the chosen cost basis. Green when positive, red when negative, `—` when the basis is unknown.
- **Labels** — colour-coded tags (the same tags, and the same colours, as the [Order Tracker](order-tracker.md)). Add or remove them by right-click.
- **Contract** — the contract behind a contract sale (blank on market rows); opens in the [Contracts](contracts.md) tool.

**Owner**, **Location**, **Buyer** and **Item(s)** open the thing they name. Right-click a row (or several) to **Mark as not for profit** / **Restore to profit**, or to **Add label** / **Remove label**.

## Notes

- Sales data comes from your synced wallet transactions and contracts, so it appears only once the relevant characters/corporations are authorized via EVE SSO and their data has been pulled. The tracker refreshes itself every few minutes.
- Build cost and market value depend on daily price snapshots, which rely on your configured market price sources — see [Configuring Markets](../configuring-markets.md). Sales of items with no snapshot show `—` for cost and profit, and are excluded from the charts.
- A corp trade a character executes is recorded once, under the corporation, to avoid double-counting.
- Marking sales **not for profit** (gifts, corp transfers, break-even moves) keeps them out of your profit figures without deleting them; the filter checkbox brings them back when you want to see them.
- The Sales Tracker is backward-looking: sales already made. For orders you've *committed to deliver* and their fulfilment, see the [Order Tracker](order-tracker.md).
