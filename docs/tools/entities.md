# Players & NPCs

A searchable browser for the entities of New Eden — the players who inhabit it and the NPCs defined in the game's static data. Look any of them up by name, then open a detail panel with everything the app knows about them.

Open it from the left sidebar under **Corp / Interactions**.

## What it shows

The browser has two sides, each a set of tabs you search and page through:

**Players**

- **Pilots**, **Corporations**, **Alliances** — with kills, losses and member counts in the lists.

**NPCs** (from the bundled SDE — the game's static data)

- **Agents**, **Stations**, **Corporations**, **Factions**.

### The detail panel

Selecting any entity opens a detail card with:

- Its **portrait or logo**.
- A **Facts** list — the key figures for that kind of entity. For an NPC corporation, for example, that includes its **headquarters, ticker, tax rate and description**; for a pilot, its corp and alliance; for most, member and kill counts.
- A set of **sub-tabs**, each shown only when there's something in it:
    - **Description**
    - **Kills / Losses** — the same activity as [Killmails](killmails.md).
    - **Members** — the corp's members, or an alliance's member corps.
    - **Corp History** (pilots) / **Alliance History** (corps).
    - **Stations** — the NPC corporation's stations, with system, region, security and agent count.
    - **Orders** — the NPC corporation's sell and buy orders, with low/high prices.
    - **LP Offers** — the corporation's loyalty-point store, with LP and ISK cost per item.
    - **Faction Warfare**
    - **Intel Reports**

## Using it

- **Search by name** to look up any entity, on either side.
- **Select an entity** to open its detail panel, then use the sub-tabs.
- Entity names are clickable across the app's tools, so you can jump to a record from wherever a name appears.

## Notes

- The kills and losses shown here are the same activity recorded in [Killmails](killmails.md); open that tool for the individual killmail detail.
- The NPC side comes from the bundled SDE and needs no ESI authorization. The NPC corporation facts (headquarters, ticker, tax rate, description) and their station lists are read from SDE fields added in 0.9.13 — if they're blank, run **Update SDE** once (see [Getting Started](../getting-started.md)).
- Player detail such as market **Orders**, **LP Offers** and **Faction Warfare** is populated from synced data and appears once it's available.
