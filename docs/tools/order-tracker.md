# Order Tracker

Track your **outgoing orders** — items you've committed to deliver to a buyer — from the moment they're placed to the contract that closes them. For each order it shows the agreed price and the profit against build cost, and, while the order is still open, how far fulfilment has got: what's on the shelf, what's in build, and what's still short.

Orders arrive two ways: you **enter them by hand**, or a **[store](../stores/index.md)** books them for you when a buyer orders — by [EVE mail](../stores/eve-mail.md) or on your [web storefront](../stores/web-site.md).

It also tracks **offers** to a store's [Buy listings](../stores/buy-listings.md): items a player is selling to you. These are **Buy** rows, matched to the seller's contract rather than filled from your stock.

Open it from the left sidebar under **Market / Trade**.

## What it shows

One row per order line, newest first. A multi-item order appears as several rows that share a single **Order #**.

**Identity**

- **Created** — when the order was placed, in EVE time to the minute.
- **Type** — the item; opens in the [Item Browser](item-browser.md).
- **Units** — quantity.
- **Side** — **Sell** for an order you deliver, **Buy** for an offer to one of your [Buy listings](../stores/buy-listings.md).
- **Purchase Price** — the total agreed price. On a Buy row it is what you pay, and it turns red with a ⚠ when the seller's contracts ask more than was quoted; hover it to see both amounts.
- **Buyer** — who the order is for; opens in the [entity browser](entities.md). On a Buy row, the seller.
- **Order #** — the order's reference. Rows repeating the same code are lines of one multi-item order, not duplicates.
- **Labels** — colour-coded tags for grouping (a customer, a corp programme, a shipment). Read-only here; add or remove them by right-click or in the edit window.
- **Store** — the [store](../stores/index.md) that booked the order (by EVE mail or web). **Blank means you entered it by hand.**
- **Contract To** — who the delivering contract is made out to. Blank means the buyer; a name appears only when someone asked for it to go elsewhere. On a Buy row it is blank unless the seller named someone else the contract will come from, such as an alt or their corporation.

**Fulfilment** (shown while the order is open)

- **Stock** — a ✓ when the order is being filled from existing shelf stock.
- **On hand** — units on hand against the units still to come, e.g. `19/50`.
- **Indy Job** — units currently in build, e.g. `120 in build`.
- **Short** — what's still unaccounted for once shelf stock and running jobs are counted (`units still to come − on hand − in build`, never below zero). Shown in red while there's a shortfall, blank once there isn't.
- **On contract** — units on contracts made out and waiting for the other party to accept. On a Buy row, units on the seller's contracts waiting for you to accept.
- **Delivered** — units accepted, against units ordered, e.g. `1/2`.
- **Contract** — the contract carrying the order; opens in the [Contracts](contracts.md) tool. Matched automatically (see below), blank until a match is found. Hover it to see every contract on the order, with the units each carries and where it stands.

**On hand**, **Indy Job** and **Short** count only the units still to come — not units already on a contract — and are blank once the order is settled. They are always blank on a Buy row: its goods are coming in, not going out.

**Price & status**

- **Est. Date** — your optional estimated delivery date.
- **Pri** — a marker for orders flagged **Priority**.
- **Status** — *Pending*, *Completed*, or *Canceled*.
- **Completed** — the completion date (set automatically; see below).
- **Build Cost** — the item's build cost × units, from your build-cost data (`—` when unavailable). For a settled order the figure is quoted as of the day it settled — hover the cell to see which day.
- **Profit** / **Profit %** — purchase price minus build cost, when a build cost exists. On a Buy row it is the other way round: build cost minus what you pay, and the percentage is of what you pay.

The status line shows how many orders are currently listed.

## Fulfilment tracking

For open orders, the tracker works out how each one is being met and keeps it current on its own (it reloads about once a minute; there's also a **Refresh** button):

- **On hand / in build / short** come from your stockpile and your industry jobs.
- **Contract** is matched automatically from your synced ESI contracts. A contract matches when the ordered item, summed over all of the contract's lines, covers what's still to come; extra items (fitted rigs and the like) and packaged versus assembled don't matter.
- **An order can go out over several contracts**, and **one contract can carry several orders** (say, two hulls for two orders of one). Exact fits are matched first, so a contract cut for one order isn't taken by another.
- **Completed** is set automatically: to today when you mark an order completed or cancelled, or, once accepted contracts carry every unit, to the date of the last acceptance. You can override it in the edit window if the real date differs.
- **A declined contract** for the whole order cancels it; a declined contract for part of it leaves the order open, with those units wanted again.
- A linked contract is let go only when it lapses — cancelled, deleted, failed, reversed, or expired without being accepted.

**Buy rows** are matched the other way round. The app looks for an Item Exchange contract **to** the store's **Buy contracts to**, issued by the seller (or by their corporation, or by whoever they named) after the offer was made, and carrying the item. The quoted price stays: a contract asking more is linked all the same and flagged on **Purchase Price**, so you can check it before accepting. Accepting the contract completes the offer; declining it cancels the offer. See [Buy Listings](../stores/buy-listings.md#matching-the-contract).

When a contract can't be matched — usually because it was made out before the order was entered — add its id in the edit window. The box takes several contract ids, separated by commas. Attaching a contract by hand takes it off any other pending order that held all of it; removing an id lets that contract go.

## Using it

Add and maintain orders from the header:

- **Add Order** — opens a dialog: search and pick an **item type**, set **units** and **total purchase price**, pick a **buyer** (a character/corporation, or free text for someone the search can't reach), and optionally an **estimated date**, **completed date**, **contract ids**, **labels**, and the **Priority** flag. Finish with a **status**.
- **Edit** — change the selected order (also opens on double-click).
- **Delete** — remove the selected order.
- **Refresh** — reload now, to pick up fulfilment changes.

Select several rows and **right-click** to **Add label** / **Remove label** in a batch. Labels typed in the edit window are created on the spot if they don't exist yet.

Filters in the header narrow the list, live:

- **Status** — *Active* (pending; the default), *Completed*, *Canceled*, or *All*.
- **Created** — a from/thru date range (`yyyy-MM-dd`).
- **Type** — substring match on the item name.
- **Buyer** — substring match on the buyer.
- **Label** — *(any)*, *(labelled)* (anything tagged, whatever the tag), or a specific label.

Columns are sortable.

## Notes

- **Build Cost** and **Profit** appear only for items with build-cost data; others show `—`. Build costs derive from your configured market price sources — see [Configuring Markets](../configuring-markets.md).
- Marking an order **Priority** pushes it — and the jobs, purchases and hauls that serve it — to the top of the [Worklist](worklist.md), regardless of estimated date.
- Buy rows never reserve stock or ask the [Worklist](worklist.md) to build anything. They come only from a store's Buy listings; **Add Order** enters Sell orders.
- The Order Tracker is forward-looking: what you've *committed to deliver*, and what you've agreed to buy. For completed sales pulled from your wallet and contracts and the profit realised on each, use the [Sales Tracker](sales-tracker.md).
