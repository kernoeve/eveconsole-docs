# Order Tracker

Track your **outgoing orders** — items you've committed to deliver to a buyer — from the moment they're placed to the contract that closes them. For each order it shows the agreed price and the profit against build cost, and, while the order is still open, how far fulfilment has got: what's on the shelf, what's in build, and what's still short.

Orders arrive two ways: you **enter them by hand**, or a **[store](../stores/index.md)** books them for you when a buyer orders — by [EVE mail](../stores/eve-mail.md) or on your [web storefront](../stores/web-site.md).

Open it from the left sidebar under **Market / Trade**.

## What it shows

One row per order line, newest first. A multi-item order appears as several rows that share a single **Order #**.

**Identity**

- **Created** — the date the order was placed.
- **Type** — the item; opens in the [Item Browser](item-browser.md).
- **Units** — quantity.
- **Buyer** — who the order is for; opens in the [entity browser](entities.md).
- **Order #** — the order's reference. Rows repeating the same code are lines of one multi-item order, not duplicates.
- **Labels** — colour-coded tags for grouping (a customer, a corp programme, a shipment). Read-only here; add or remove them by right-click or in the edit window.
- **Store** — the [store](../stores/index.md) that booked the order (by EVE mail or web). **Blank means you entered it by hand.**
- **Contract To** — who the delivering contract is made out to. Blank means the buyer; a name appears only when someone asked for it to go elsewhere.

**Fulfilment** (shown while the order is open)

- **Stock** — a ✓ when the order is being filled from existing shelf stock.
- **On hand** — units on hand against units ordered, e.g. `19/50`.
- **Indy Job** — units currently in build, e.g. `120 in build`.
- **Short** — what's still unaccounted for once shelf stock and running jobs are counted (`Units − on hand − in build`, never below zero). Shown in red while there's a shortfall, blank once there isn't.
- **Contract** — the contract that fulfils the order; opens in the [Contracts](contracts.md) tool. Matched automatically (see below), blank until a match is found.

**Price & status**

- **Est. Date** — your optional estimated delivery date.
- **Pri** — a marker for orders flagged **Priority**.
- **Purchase Price** — the total agreed price.
- **Status** — *Pending*, *Completed*, or *Canceled*.
- **Completed** — the completion date (set automatically; see below).
- **Build Cost** — the item's build cost × units, from your build-cost data (`—` when unavailable). For a settled order the figure is quoted as of the day it settled — hover the cell to see which day.
- **Profit** / **Profit %** — purchase price minus build cost, when a build cost exists.

The status line shows how many orders are currently listed.

## Fulfilment tracking

For open orders, the tracker works out how each one is being met and keeps it current on its own (it reloads about once a minute; there's also a **Refresh** button):

- **On hand / in build / short** come from your stockpile and your industry jobs.
- **Contract** is matched automatically from your synced ESI contracts by their item list. When a contract can't be matched — usually because its items differ from the order — you can paste its id into the edit window, or clear it to remove the link.
- **Completed** is set automatically: to today when you mark an order completed or cancelled, or to the date the linked contract was accepted. You can override it in the edit window if the real date differs.

## Using it

Add and maintain orders from the header:

- **Add Order** — opens a dialog: search and pick an **item type**, set **units** and **total purchase price**, pick a **buyer** (a character/corporation, or free text for someone the search can't reach), and optionally an **estimated date**, **completed date**, **contract id**, **labels**, and the **Priority** flag. Finish with a **status**.
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
- The Order Tracker is forward-looking: what you've *committed to deliver*. For completed sales pulled from your wallet and contracts and the profit realised on each, use the [Sales Tracker](sales-tracker.md).
