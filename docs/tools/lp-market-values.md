# LP Market Values

See what your loyalty points are actually worth, corporation by corporation: each LP store's offers are priced against the market and net of everything each offer also consumes, then summarized as a mean ISK per loyalty point.

Open it from the left sidebar under **Market / Trade**.

## What it shows

The screen has two tabs: **Current Values** and **History**.

A header reads "N corporation(s) valued — updated <time>" with a **Recalculate** button, and an explanatory line: the figure is the mean ISK per loyalty point across the offers in each store that price out above zero. Offers worth nothing or less are shown per item in the [Item Browser](item-browser.md) but are not counted here. Corporations you personally hold LP with are listed first.

Columns:

- **Corporation** — the LP store's corporation.
- **ISK / LP** — the mean value per loyalty point (the sort key).
- **Median** — the median ISK/LP across counted offers.
- **Best Offer** and **Best Item** — the highest-valuing offer and the item it yields.
- **Counted** — how many offers in the store priced out into the total.
- **Your LP** — the loyalty points you hold with the corporation.
- **Holding Worth** — the value of your LP at this corporation's ISK/LP.
- **Updated** — when the row was last calculated.

The list is sorted by ISK/LP. Double-click a row to open its history.

## Using it

1. Open the tool; corporations you hold LP with appear first.
2. Read across a row to see its **ISK / LP**, **Median** and the **Best Offer** / **Best Item** driving it.
3. Check **Your LP** and **Holding Worth** to see what your balance at that corporation is worth.
4. Double-click a row to open its **History**, or switch to the **History** tab.
5. Click **Recalculate** to re-price the stores against the current market.

## Notes

- Values depend on a configured market for prices ([Configuring Markets](../configuring-markets.md)).
- Offers that price out at zero or below are excluded from a corporation's ISK/LP, but their per-item LP value still appears in the [Item Browser](item-browser.md).
