# Item Browser

A full reference browser over the EVE item database, combining SDE data (descriptions, attributes, blueprints, skills) with your synced market and price data for any type.

Open it from the left sidebar under **Assets**.

## What it shows

The window is split into a left navigation pane and a right detail pane.

### Left pane — Browse and Quickbar

The left pane has two tabs. **Browse** holds the tree and search:

- A **market-group tree** of every published type, expandable by category.
- A **search box**: type at least two characters to switch from the tree to a live results list. Results show the item name and its group path, and are ranked so that names starting with your text come first. In a language other than English, the search finds both the name shown and the English one, so a name pasted from an English site still works.
- **Back / Forward** buttons that walk your navigation history (up to 100 items). Clicking any linked item elsewhere in the window pushes onto this history.

**Quickbar** holds the items you keep to hand — see [Quickbar](#quickbar) below.

### Right pane — item header and detail tabs

The header shows the item icon, name, group path, and a stat strip with **Volume**, **Market Value** (labelled with the configured price type), **Build Cost**, and **Reproc Value** where available. Beside the name, a small copy button copies the name to the clipboard (right-click the name for **Copy Name**), and **☆ Add to Quickbar** puts the item on the quickbar (**★ On Quickbar** takes it off).

Below the header are detail tabs:

- **Description** — the type's in-game description (HTML stripped), in the interface language where the game has one.
- **Attributes** — fixed type stats (Volume, Mass, Capacity, Portion Size, Base Price where applicable) followed by the item's published dogma attributes, grouped by attribute category. Values are shown the way the game client shows them:
    - with the unit's own name — `41 MW`, `130 tf`, `365 m/sec`;
    - milliseconds as seconds;
    - resonances and multipliers as the percentage they mean — a resonance of 0.6 is a **40 %** resistance, a rate-of-fire multiplier of 0.895 a **10.5 %** bonus;
    - an attribute that points at a group, type or attribute as its name, such as *Missile Launcher Light* or *Perception*;
    - codes as words: yes / no, small to extra large, and expiry dates as dates;
    - slot and level counts as the plain number, since the attribute's name already says what it is.
- **Requirements** — the skills required to use or build this item, with the required level (in Roman numerals). Skill names are clickable and navigate to that skill.
- **Required For** — only shown when the loaded item is itself a skill. A I–V level selector lets you pick a skill level; the tab lists the ships, modules, and other items that require this skill at that level, grouped by category. Levels that actually have items are highlighted on the selector.
- **Industry** — for a regular item, up to four sections:
    - **Produced By** — the blueprints and reaction formulas that make it, with their input materials.
    - **Produced By Reprocessing** — what yields this item when reprocessed, per batch, at the best rate each source can reach (90.6% for ore, ice and moon ore, 55% for everything else). A **Show** dropdown picks **All**, **Ore** (the whole Asteroid category: ore, ice and moon ore) or **Non Ore** (modules, ships, salvage and the like); your choice stays as you move between items.
    - **Reprocesses To** — what one batch of this item returns when reprocessed, at the best rate it can be refined at.
    - **Used In Manufacturing** — the blueprints and reaction formulas that consume it.

    For a blueprint or reaction formula: an activity selector (Manufacturing, Reaction, Invention, Copying, ME Research, TE Research) showing the outcome/products, required skills, and input materials for the selected activity. All names are clickable to navigate.
- **Assets** — every stack of the item the app knows of. See [Assets tab](#assets-tab) below.
- **Contracts** — every item exchange with the item on either side. See [Contracts tab](#contracts-tab) below.
- **LP Store** — only shown when a loyalty-point store offers the item. One row per offer: Corporation, Qty, LP Cost, ISK Cost, Your LP, LP Est. Value, Required Items and AK. For whole-store comparisons, use [LP Market Values](lp-market-values.md).
- **Market Orders** — live buy and sell orders for the item from a selected market source. Sell orders show Qty, Price, Location, and Expires; buy orders additionally show Range and Min Qty. Sell orders are sorted cheapest-first, buy orders highest-first.
- **Price History** — only shown when at least one price-history region is configured. Pick a region and a period (All Time, 30, 90, or 365 days). A **Chart** sub-tab plots average / high / low price and trade volume; a **Grid** sub-tab lists Date, Volume, Avg Price, High, Low, and Orders per day.
- **Derived History** — a chart of the item's recorded daily **Market**, **Build**, and **Contract** value snapshots, filterable by period. These snapshots are captured automatically as prices refresh.

### Assets tab

The **Assets** tab lists every stack of the item that your synced assets hold — the same data as the [Assets](assets.md) tool, filtered to this one item.

- **Group by** — **Location** (the default), **Owner** or **None**. Grouped rows fold under a collapsible header naming the location or owner, with the stacks, units and value it adds up to. Clicking a column header sorts within each group.
- **Scope** — **Characters and personal corps** (the default) or **All owners**.

Columns: **Location**, **Owner**, **Qty**, **Container**, **Flag**, **Value**, **System**, **Sec** and **Region**. **Location**, **Owner** and **System** are links to their pages. The product of a running industry job is included, with the flag **Industry Job**.

A summary line above the grid gives the total units, stacks and locations, what they're worth, and how many are still in industry jobs.

### Contracts tab

The **Contracts** tab lists item exchanges with this item on them, offered by the issuer or asked for in return. A contract with the item on both sides is two rows.

- **Status** dropdown: **Active**, **Historical** or **All**. Past contracts are limited to the newest 1,000 for an item, and the caption says when it has cut any off.
- **Owner** dropdown: **All**, **Public**, or **Corporation & Personal** (your own, as the [Contracts](contracts.md) tool's first tab holds them).

Columns: **Contract** (a link that opens it in the Contracts tool), **Side** (**Offered** or **Wanted**), **Qty**, **Blueprint** (a copy's or original's ME, TE and runs), **Price**, **Reward**, **Per unit / run**, **Rest of contract**, **Location**, **Sec**, **Region**, **Expires** and **Status**.

**Per unit / run** is shown only where the item is all there is on its side and only ISK comes the other way, since a bundle's price isn't this item's. A copy is priced per run.

Public contracts come from the Contracts tool's sweep of every region.

### Quickbar

The **Quickbar** tab keeps the items you go back to, in nested folders. It's stored in the database, so every copy of the app on that database sees the same one.

- **To add an item**, right-click it under **Browse** or in the search results and choose **Add to Quickbar** (with folders, pick one from its submenu), or use the button beside an item's name. **Remove from Quickbar** takes it off.
- **On an item** in the quickbar, right-click for **Move to Folder** and **Remove from Quickbar**.
- **On a folder**, right-click for **New Folder…** (inside it), **Rename Folder…**, **Move to Folder** and **Delete Folder (Its Items Move Up)**.
- **On the empty space**, right-click for **New Folder…**.

## Using it

- **Find an item** — browse the tree, or type in the search box and click a result.
- **Follow links** — clickable (underlined) item, skill, blueprint, and material names navigate to that type. Use the Back / Forward buttons to retrace your path.
- **Read stats and requirements** — use the Description, Attributes, and Requirements tabs. For a skill, the Required For tab reverses the lookup to show what needs it.
- **Trace production** — the Industry tab shows both directions of the blueprint graph, including reactions and reprocessing, and, for blueprints, the per-activity materials and skills.
- **Find your stock** — the Assets tab shows where every stack of the item is and who holds it.
- **Check the market** — on the Market Orders tab, choose a source from the **Source** dropdown to load orders. On Price History, choose region and period. The Contracts tab shows what it's being sold for on contract.
- **Send it on** — right-click an item under **Browse**, in the search results or on the quickbar for **Add to Standing Buy Orders…** and **Add to Production Calc Queue**. Both leave you here, with a message saying what was added. An item nothing builds is left out of the queue, and the message says so.

## Notes

- Tree, search, descriptions, attributes, blueprints, and skill data come from the bundled SDE and need no ESI authorization.
- **Market Value** and **Build Cost** in the header, and the values on the Derived History tab, depend on your market configuration (see [Configuring Markets](../configuring-markets.md)). If no asset-value price source is set, the Market Value figure is blank. A T2 item's **Build Cost** includes what inventing its copy costs.
- The **Market Orders** tab requires at least one enabled ESI Region or player-structure market source; without one the tab shows a prompt to add a source in Settings → Market. Orders are read from synced data.
- The **Price History** tab only appears when a price-history region is configured (Settings → Price History). History for a region/type is refreshed on demand when you open it.
- Item icons load from the EVE image server, so they require an internet connection; they are optional and the rest of the page works without them.
- The [Assets](assets.md) and [Inventory Levels](inventory-levels.md) tools can open a selected item directly in this browser.
