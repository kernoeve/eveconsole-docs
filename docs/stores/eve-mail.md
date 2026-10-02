# EVE Mail Store

The EVE Mail Store lets buyers place and manage orders by **sending EVE mail** to one of your characters. The app polls that character's inbox, understands a small set of commands, replies, books each order into the [Order Tracker](../tools/order-tracker.md), and keeps the buyer updated by mail as the order progresses.

It's one of a store's two shop fronts — see [Stores](index.md) for the shared setup (catalogue, who may order, purchase limits), and the [Web Storefront](web-site.md) for the other channel. Open it from the **Stores** tool under **Market / Trade**.

## The screen

- **Overview** — the store's current state and its outstanding orders (mail and web).
- **Config** — sub-tabs for **General** (store character, the [sale posting](../tools/sale-posting.md) it prices from, the store's language), **Restrictions** (who may order, purchase limits), **EVE Mail**, and **Web site**.
- **Info** — the reference the store hands buyers (also available to them via the `INFO` command).
- **Usage** — how the commands work, for your own reference.

## Turning it on

On **Config ▸ EVE Mail**, switch the mail channel on (*Open by EVE mail*). Buyers then write to the store's mailbox character. You can set a message header/footer and review the exact commands there.

## How buyers order

A buyer puts a **command in the mail subject** and the app answers:

- **`PRICES`** — the current price list for the store.
- **`ORDER`** — place an order.
- **`STATUS`** — the state of an existing order.
- **`CANCEL`** — cancel an order.
- **`INFO`** — general store information.
- **`HELP`** — the list of commands.

Items in an order are read from **dragged `showinfo:` links first** and typed names second, so a buyer can drag an item straight into the mail. When a reply is longer than EVE's mail size limit, it is **split across several mails**, up to five. An answer that needs more says how much didn't fit; a status answer also says how to ask about one order.

## Language

The store writes its mails — price lists, confirmations, status and cancel answers, order updates — in the store's **Language** (**Config ▸ General**; see [Stores](index.md#the-stores-language)). Numbers and ISK amounts follow that language's format.

The **command words stay English** in every language: buyers type `PRICES`, `ORDER`, `STATUS`, `CANCEL`, `INFO` or `HELP` whatever language the store writes in. The rest of a buyer's mail can be in their own language:

- Item names are read in any of the game's languages — English, the store's, or the buyer's own client's.
- Quantities written with group separators, as other clients write them (`1.000`, `1 000`), are read as one number.
- **Full-width** letters, digits and spaces, as Chinese, Japanese and Korean keyboards type them, read as their ordinary forms — `ＳＴＡＴＵＳ` is `STATUS`, `５` is `5`.
- A **counter word** after a number counts as part of it — `5個`, `5个`, `5개`, `5 шт.`, `5 pcs`.
- An order reference written straight against other text, as Chinese and Japanese do, is still found.

## Notes

- **Pricing is taken from the sale posting at the moment an order is placed** — never from anything written in the mail. Keep your [Sale Posting](../tools/sale-posting.md) current so quotes are right.
- Contracts default to the **sender** when no other recipient is named, so every order has someone to deliver to.
- This is the app's **only untrusted input**, so the mail path is deliberately careful: ownership on `CANCEL` and `STATUS` is checked against the ESI mail header rather than anything the sender writes, quantities are bounded, and a mail with no identifiable sender is refused rather than served.
- Only **Inbox** mail is read, and `RE:` / `FW:` subjects are ignored, so a reply thread doesn't re-trigger a command. That's why the store's mails tell buyers to *send* a new mail with `STATUS`, not to reply.
- New orders and their progress also surface in the [Overview](../tools/overview.md) **Orders** section and in the [Order Tracker](../tools/order-tracker.md).
