# Sale Posting

Build shareable sale postings from your own stock: assemble the items you want to offer into a structured posting, price them against build, market or contract references, and render the result as text you can paste into Slack, Discord or a forum.

Open it from the left sidebar under **Market / Trade**.

## What it shows

The screen has two tabs: **Definitions**, where you build the posting, and **Posting**, the rendered, shareable output.

### Definitions tab

A toolbar sits at the top with a **+ Add Posting** button, a **Refresh** button, and a **Profit based on** dropdown (**Build** or **Market**) that chooses which price reference the profit columns use.

The posting itself is a tree:

- A **Posting** (e.g. "Primary Marketplace Post") is the top level. It can carry a region and a build-price multiplier (e.g. "Build ×115%").
- Each posting contains **Sections** (e.g. "Carriers (Command)", "Dreadnoughts (Navy)", "Force Auxiliaries", "Jump Freighters"). A section can override the posting's multiplier for its own items (e.g. "Build ×112% — all items").
- Each section contains **Items**.

Every posting and section row carries **+ Section** / **+ Item**, **Edit** and **Delete** controls, so you build the tree in place.

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

Renders the posting as shareable text in a chosen format: **Plain**, **Slack**, **Discord**, **Markdown**, **HTML** or **BBCode**.

## Using it

1. On the **Definitions** tab, click **+ Add Posting** and give it a region and a build-price multiplier.
2. Add **Sections** to the posting with **+ Section**, optionally overriding the multiplier for a section's items.
3. Add **Items** to a section with **+ Item**.
4. Set a **Sale Price** per item, and add a **Name Override** or **Prefix** where you want one. Use the **Ovr** columns to correct any stock, build or reserved figure by hand.
5. Choose the reference for the profit columns with the **Profit based on** dropdown.
6. Switch to the **Posting** tab, pick a format (Plain, Slack, Discord, Markdown, HTML or BBCode) and copy the rendered text to share it.

## Notes

- Pricing needs a configured market ([Configuring Markets](../configuring-markets.md)); build costs also need an industry park ([Indy Parks](../industry-parks.md)).
- Contract pricing is used for items that have no market pricing, such as BPCs.
- In-stock, in-build and reserved figures are computed from your assets and jobs; the **Ovr** columns let you override them when the computed value isn't what you want to advertise.
- To follow up on what actually sells, see [Sales Tracker](sales-tracker.md).
