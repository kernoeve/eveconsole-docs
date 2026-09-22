# Item Valuation

Paste a list of items and see what it's worth — the way an appraisal site does, but priced from **your own market data** rather than a third-party service. Each item is valued three ways side by side — at the **market**, as a **build**, and **reprocessed** — at a station you choose, and you can compare the same list across several stations.

Open it from the left sidebar under **Market / Trade**.

## Valuing a list

Paste into the box on the left. It understands most things you can copy in EVE:

- a **hangar or cargo hold** copied from the client,
- a **contract** item list, a **fit**, or a **multibuy** list,
- or plain lines like `Tritanium 22222`, `Pyerite x 3000`, `Warrior II 5`, or just an item name.

**Pasting values the list on its own** — so does pressing **Enter**, or the **Appraise** button. Once valued, the list folds away to give the results room; **Edit list** brings it back to change it. Anything that couldn't be matched to an item is listed in a warning beneath the results.

## Options

These sit above the results, because changing any of them re-prices the same list:

- **Station** — any station or structure the app holds orders for (from whichever [market source](../configuring-markets.md) fetched them). **Sell** orders are read at the station itself; **buy** orders count when placed at the station, anywhere in its system within range, or region-wide. (NPC floor buy orders and out-of-range buys are ignored.)
- **Prices** — the basis: **Sell** (the lowest sell order), **Buy** (the highest buy order), or **Split** (halfway between).
- **Value** — the items **as pasted**, or their **reprocessed output** (the materials, batch by batch at the app's standard refining yields, plus anything that couldn't be reprocessed).
- **Price %** — the share of the price to value at: `100` is the price itself, `90` a buyback paying nine-tenths.

## Reading the result — Values tab

At the top: the total **volume** and **item/unit** count, and a filter to show only items whose name contains some text.

Each item is priced three ways, in three colour-washed column groups — **Market**, **Build**, and **Reprocessed** — each showing:

- **Unit** — the per-unit value.
- **Total** — value × quantity.
- **vs best** — how this value stands against the best of the three for that item (the best in green, a value far behind in red).

Each group's **heading** carries that value's **total** across the whole list, its **standing** against the other two, and its **coverage** (how much of the list it could price), along with how old the station's prices are — flagged **stale** after a couple of hours, or *"no orders held"* when the app has none.

An item with **no orders at the chosen station** is priced from **contracts** where the app has a price, and marked so you can see it wasn't a live order.

## Comparing stations — Market compare tab

The station you chose above leads; **Add** more to price the same list at each. Every station gets its own unit / total / per-cent columns, with its total, standing, coverage and price age beneath its name and a **×** to remove it (the primary station stays). Useful for deciding where a haul is worth the most, or cheapest to buy.

## Output

- **Copy** — both tables and the totals as tab-separated text, ready to paste into a spreadsheet or a chat.
- Item names link to the [Item Browser](item-browser.md).

## Notes

- Prices come entirely from the app's **own order books** — the [market sources](../configuring-markets.md) you've configured — so a value is only as complete and as fresh as what the app has fetched for that station (watch the coverage and age in each heading). Nothing is sent to or fetched from an external appraisal site.
- **Build** values use your build-cost data (see [Configuring Markets](../configuring-markets.md) and [Industry Parks](../industry-parks.md)); **Reprocessed** values use the app's standard refining yields (the same ones the [Item Browser](item-browser.md) shows).
- Use **Price %** for a buyback program — paste a customer's list, set the percentage you pay, and read the total.
