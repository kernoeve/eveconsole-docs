# Income & Expense

A categorized breakdown of where your ISK comes from and where it goes, with a daily income/expense/cashflow chart and the journal entries behind every figure — for all your characters and personal corporations together, or for any one of them.

Open it from the left sidebar under **Finance**.

## What it shows

Across the top, an owner picker and a **From** / **Thru** date range. Everything below follows them. Under them are three tabs.

### Summary tab

Three panels driven by your wallet journal over the range:

- **Income** — income categories, largest first, with the total at the top (green).
- **Expenses** — expense categories, largest first, with the total at the top (red).
- **Daily · Income · Expense · Cashflow** — a line chart with three series: daily **Income**, daily **Expense**, and a running **Cashflow** (net) line. The panel header shows the net total (income minus expense) for the range.

Categories are derived from wallet-journal reference types. Every entry counts on its own side: money in is income and money out is expense. A type with money both ways — market transactions or contracts, say — shows on both sides, rather than as one net figure. The category lists are height-aware: the panels show as many rows as physically fit, and any remaining smaller categories are rolled up into a single **Other** line so the totals still add up.

### Income and Expense tabs

The journal entries themselves: money in on **Income**, money out on **Expense**. Each has a grid of **Date**, **Owner**, **Div** (wallet division), **Type**, **Amount** and **Description**, with paging at the bottom.

Above the grid, the total for the whole range — for example *1,234 entries · 5.67B ISK* — which matches the figure on the **Summary** tab. **Sort** orders the entries by **Date: newest first**, **Date: oldest first**, **Amount: high → low** or **Amount: low → high**; on **Expense**, the amount is sorted by its size. Click an owner's name to open it in [Players & NPCs](entities.md).

## Using it

1. Pick the owner: **All Characters & Personal Corps** (the default), or one character or personal corporation (shown as `Name [TICKER]`).
2. Set **From** and **Thru**. The range starts as the past 30 days. Dates are EVE time, and both days are included. Clear a date to leave that end open.
3. Read the **Summary** to see which reference types dominate, and watch the **Cashflow** line to see whether you're net positive or negative.
4. Open **Income** or **Expense** to see the entries behind a figure.

The panels and chart refresh automatically (roughly every five minutes). The owner list updates as soon as you add or remove a character or corporation, and keeps your choice.

## Notes

- This tool reads the wallet journal only, so it reflects realized ISK flows (bounties, market transactions, fees, taxes, contract payments, etc.), not asset or order valuation. For total worth including assets and orders see [Net Worth](net-worth.md); for the full journal and per-owner transactions see [Wallet](wallet.md).
- **ISK moved between your own wallets is left out.** Transfers between your tracked characters and personal corporations aren't income or expense — they're money changing pockets — so they're excluded from these totals and entries, the [Wallet](wallet.md) charts, and the [Overview](overview.md) income/expense pies.
- The [Overview](overview.md) has its own Income & Expense section. It always covers all your wallets and follows the Overview's period selector; choosing an owner or dates here doesn't change it.
- Only characters with a stored refresh token and corporations marked as personal are included. See [Getting Started](../getting-started.md) for the personal-corp designation.
