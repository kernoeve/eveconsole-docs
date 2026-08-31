# EVE Mail Store

The EVE Mail Store lets buyers place and manage orders by **sending EVE mail** to one of your characters. The app polls that character's inbox, understands a small set of commands, replies, books each order into the [Order Tracker](order-tracker.md), and keeps the buyer updated by mail as the order progresses. The left-nav label is **Stores**.

Open it from the left sidebar under **Market / Trade**.

## What it shows

The screen has four tabs:

- **Overview** — the store's current state and its outstanding orders.
- **Config** — the store character, the [sale posting](sale-posting.md) it prices from, and how it behaves.
- **Info** — the reference the store hands buyers (also available to them via the `INFO` command).
- **Usage** — how the commands work, for your own reference.

### How buyers order

A buyer puts a **command in the mail subject** and the app answers:

- **`PRICES`** — the current price list for the store.
- **`ORDER`** — place an order.
- **`STATUS`** — the state of an existing order.
- **`CANCEL`** — cancel an order.
- **`INFO`** — general store information.
- **`HELP`** — the list of commands.

Items in an order are read from **dragged `showinfo:` links first** and typed names second, so a buyer can drag an item straight into the mail. When a reply is longer than EVE's mail size limit, it is **split across several mails**.

## Using it

1. On the **Config** tab, choose the **store character** whose inbox will be polled and the **[sale posting](sale-posting.md)** the store prices from.
2. Share the **Info** text (or point buyers at the `INFO` / `HELP` commands) so they know how to order.
3. As mail arrives, the app replies, **books orders into [Order Tracker](order-tracker.md)**, and mails the buyer as the order moves along.
4. Watch outstanding orders from the store **Overview** tab or in the [Order Tracker](order-tracker.md).

## Notes

- **Pricing is taken from the sale posting at the moment an order is placed** — never from anything written in the mail. Keep your [Sale Posting](sale-posting.md) current so quotes are right.
- Contracts default to the **sender** when no other recipient is named, so every order has someone to deliver to.
- This is the app's **only untrusted input**, so the mail path is deliberately careful: ownership on `CANCEL` and `STATUS` is checked against the ESI mail header rather than anything the sender writes, quantities are bounded, and a mail with no identifiable sender is refused rather than served.
- New orders and their progress also surface in the [Overview](overview.md) **Orders** section.
