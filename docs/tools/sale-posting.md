# Sale Posting

Build shareable sale postings from your own stock: assemble the items you want to offer into a structured posting, price them against build, market or contract references, and render the result as text you can paste into Slack, Discord or a forum — or post it to Slack or Discord straight from the app.

Open it from the left sidebar under **Market / Trade**.

## What it shows

The screen has two tabs: **Definitions**, where you build the posting, and **Posting**, the rendered, shareable output.

### Definitions tab

A toolbar sits at the top with a **+ Add Posting** button, a **Refresh** button, and a **Profit based on** dropdown (**Build** or **Market**) that chooses which price reference the profit columns use.

The posting itself is a tree:

- A **Posting** (e.g. "Primary Marketplace Post") is the top level. It carries the settings below, such as a sale price basis (e.g. "Build ×115%").
- Each posting contains **Sections** (e.g. "Carriers (Command)", "Dreadnoughts (Navy)", "Force Auxiliaries", "Jump Freighters"). A section can override the posting's inventory scope, sale price basis and packaged-only setting for its own items (e.g. "Build ×112% — all items").
- Each section contains **Items**.

Every posting and section row carries **+ Section** / **+ Item**, **Edit** and **Delete** controls, so you build the tree in place.

### Posting settings

**+ Add Posting** and **Edit** on a posting open its settings:

- **Posting name**.
- **Inventory scope (In Stock / In Build)** — where stock is counted: **Everywhere**, or one **Station**, **System** or **Region**.
- **Sale price basis** — **Build Cost**, **Contract Cost** or a **Specific Market** (with its price type), and **Sale price = basis × %**. Build defaults to 110 %, contract and market to 100 %.
- **Show quantities in posting** — whether **In Stock**, **In Build** and **Reserved** appear in the rendered text, and whether to include the earliest job completion date for an item that's out of stock but building.
- **Only include packaged items** — skip assembled or fitted hulls when counting stock.
- **Colour** — line colours for EVE mail; other formats ignore them.
- **Post blocks** — the messages the posting is rendered as, in order: **Summary**, **Detail** or **Static** (text you type), each with an optional header and footer. On a Slack channel the first block is the message and the rest go in its thread.

A section's **Edit** offers the same scope, price basis and packaged-only settings, each with an **Override … for this section** box.

Columns per row:

- **Posting / Section / Item** — the tree label.
- **Name Override** — a display name to use instead of the item's own.
- **Prefix** — a text or emoji prefix (such as a Slack or Discord emoji code) placed before the name in the rendered output.
- **In Stock**, **In Build**, **Reserved** — computed from your assets and jobs.
- **Stock Ovr**, **Build Ovr**, **Rsrv Ovr** — hand overrides for the three quantities above.
- **Build Cost**, **Mkt Value**, **Contract** — three price references.
- **Sale Price** — your configurable asking price.
- **Profit** and **Profit %** — relative to the reference chosen in **Profit based on**.
- **Ready (est.)** — an estimate of when the item will be available.

### Posting tab

Pick a posting from the list on the left. Its post blocks are rendered as shareable text in the chosen **Format**: **Plain**, **Slack**, **Discord**, **Markdown**, **HTML** or **BBCode**. Each block has a **Copy** button, and **Refresh** renders it again.

- **Post to Slack** — shown once a Slack channel or webhook is set for Sale Posting under **Settings ▸ Slack**. On a channel, the first block is the message and the rest go in its thread.
- **Post to Discord** — shown once a Discord webhook is set for Sale Posting under **Settings ▸ Discord** (see [Posting to Discord](../discord.md)). Each block goes as its own message, in order, since a webhook can't start a thread.

Both buttons post in their own service's format, whatever the **Format** box shows. Each has its own status line, and asks before posting the same posting again within 24 hours.

## Using it

1. On the **Definitions** tab, click **+ Add Posting** and give it a name, an inventory scope and a sale price basis.
2. Add **Sections** to the posting with **+ Section**, optionally overriding the scope, price basis or packaged-only setting for a section's items.
3. Add **Items** to a section with **+ Item**.
4. Set a **Sale Price** per item, and add a **Name Override** or **Prefix** where you want one. Use the **Ovr** columns to correct any stock, build or reserved figure by hand.
5. Choose the reference for the profit columns with the **Profit based on** dropdown.
6. Switch to the **Posting** tab, pick a format (Plain, Slack, Discord, Markdown, HTML or BBCode) and copy the rendered text to share it — or press **Post to Slack** or **Post to Discord**.

## Notes

- Pricing needs a configured market ([Configuring Markets](../configuring-markets.md)); build costs also need an industry park ([Indy Parks](../industry-parks.md)).
- Contract pricing is used for items that have no market pricing, such as BPCs.
- In-stock, in-build and reserved figures are computed from your assets and jobs; the **Ovr** columns let you override them when the computed value isn't what you want to advertise.
- A [store](../stores/index.md) that prices from a posting also takes its stock rules from it. An order placed through the store counts as in stock only from what that posting's scope and packaged-only setting count — see [Stock follows the store's rules](../stores/index.md#stock-follows-the-stores-rules).
- To post a posting on a timetable, add a **Sale Posting** section to a [Scheduler](scheduler.md) task.
- To follow up on what actually sells, see [Sales Tracker](sales-tracker.md).
