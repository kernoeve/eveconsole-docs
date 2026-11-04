# Standing Buy Orders

Declare the buy orders you intend to keep standing at a given station or structure, and let EVE Console check whether they're actually up — surfacing missing, outbid, run-down and near-expiry orders as the distinct problems they are.

Open it from the left sidebar under **Market / Trade**.

## What it shows

A list of the buy orders you've declared. Each order is reported by state:

- **present / active** — the order is up as intended.
- **missing** — the order isn't found.
- **outbid** — someone is bidding above you.
- **run down** — the remaining quantity is low.
- **close to expiry** — the order is near its expiry date.

Columns per declared order:

- **Status** — the order's state (e.g. Active).
- **Item** — the item being bought.
- **Location** — the station or structure it should stand at.
- **Held by** — the character or corporation holding the live order.
- **Our bid** — your bid price.
- **Station best bid** — the highest bid at the station.
- **Build Cost** — what a unit costs to build, the figure [Industry Opportunities](industry-opportunities.md) and the [Production Calculator](production-calculator.md) use. `—` for an item that isn't built.
- **Market value** — what a unit is worth, as the app values assets: the asset-value market and price type in **Settings ▸ Market**, the same figure as [Net Worth](net-worth.md).
- **Best Bid / Value** — the best bid at the station, yours or anyone's, as a share of the market value. Over 100% it turns amber: the station is paying more than the item is worth.
- **Remaining**, **%** — how much of the order is left.
- **Expires** — the expiry date and the days left.
- **Note**.

## Using it

1. Declare the buy orders you intend to keep standing at a station or structure: **Add** opens the dialog, and **Edit** and **Delete** act on the selected order.
2. Read down the list and check each order's **Status**.
3. Act on the ones flagged **missing**, **outbid**, **run down** or **close to expiry** — each is the distinct problem it says it is.

### Adding from other tools

**Add to Standing Buy Orders…** is on the right-click menu in [Industry Opportunities](industry-opportunities.md), [Inventory Levels](inventory-levels.md), [Market Levels](market-levels.md), [Sale Posting](sale-posting.md), [Corp Activity](corp-activity.md) and the [Item Browser](item-browser.md). The items go to the station of the last order you added, with no dialog, and you stay where you are. A message says how many were added, and how many were already standing orders there. The dialog only appears when you have no orders yet, to ask for a station. Each order can be moved here afterwards.

## Notes

- It compares your declared standing orders against your live market orders synced from ESI.
- It is one of the sources feeding the [Worklist](worklist.md); a summary also appears on the [Overview](overview.md) and in [Corp Activity](corp-activity.md).
