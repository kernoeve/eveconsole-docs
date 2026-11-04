# Players & NPCs

A searchable browser for the entities of New Eden — the players who inhabit it and the NPCs defined in the game's static data. Look any of them up by name, then open a detail panel with everything the app knows about them.

Open **Player Entities** or **NPC Entities** from the left sidebar under **Corp / Interactions**.

## What it shows

Each side is a set of tabs you search and page through:

**Player Entities**

- **Pilots**, **Corporations**, **Alliances**.

**NPC Entities** (from the bundled SDE — the game's static data)

- **Agents**, **Stations**, **Corporations**, **Factions**.

### The detail panel

Selecting any entity opens a detail card with:

- Its **portrait or logo**, and a small copy button beside the name that copies it to the clipboard.
- A **Facts** list — the key figures for that kind of entity. For an NPC corporation, for example, that includes its **headquarters, ticker, tax rate and description**; for a pilot, its corp, alliance and security status.
- For pilots, corporations and alliances, a **zKillboard stats** panel — see below.
- A set of **sub-tabs**, each shown only when there's something in it:
    - **Description**
    - **Kills / Losses** — pilots, corporations and alliances; see below.
    - **Members** — the corp's members, or an alliance's member corps.
    - **Corp History** (pilots) / **Alliance History** (corps). For a pilot, pick a row to see [what they did there](#corp-history-summary).
    - **Contracts** and **Market** — pilots and player corporations; see [Contracts, Market and Corp Taxes](#contracts-market-and-corp-taxes).
    - **Corp Taxes** — a pilot or corporation that has paid tax into one of your corporations.
    - **Stations** — the NPC corporation's stations, with system, region, security and agent count.
    - **Orders** — the NPC corporation's sell and buy orders, with low/high prices.
    - **LP Offers** — the corporation's loyalty-point store, with LP and ISK cost per item.
    - **Faction Warfare**
    - **Intel Reports**

### zKillboard stats

For a pilot, corporation or alliance, the header shows zKillboard's own figures, laid out the way zKillboard shows them:

- **Ships**, **Points** and **ISK** — **Destroyed** and **Lost**, each with its **Rank**, and the efficiency (**Eff.**) between them.
- **All time**, **90 days** or **7 days** — switches the period. The overall rank for the period is shown beside it.
- **Dangerous** against **Snuggly**, **Gang** against **Solo**, the average gang size, and solo kills and losses. These follow the period too. zKillboard publishes them for all time only, so for 90 and 7 days they are worked out the way zKillboard's own page works them out.
- **zKillboard** — opens the entity's page on zKillboard.

The figures are fetched when you pick the entity, and kept for ten minutes.

### Kills / Losses

The **Kills / Losses** tab lists kills and losses newest first, in the same layout as the [Killmails](killmails.md) browser. Double-click a row to open that killmail.

The kills already stored in EVE Console show at once. The first time you open the tab for an entity, EVE Console also asks zKillboard for its latest 200 kills and losses, and stores the ones it doesn't have yet.

- **Load 200 more from zKillboard** — fetches the next page, further back.
- The status line says how far back the list reaches, and how many kills were fetched that weren't stored before.
- A page zKillboard hasn't served lately can take a minute to arrive.
- If zKillboard can't be reached, the status says why and the button changes to **Try zKillboard again**.
- zKillboard serves at most 100 pages — an entity's most recent 20,000 kills and losses. The status says when you've reached that limit.

### Contracts, Market and Corp Taxes

These tabs show what your own data says a pilot or player corporation did. They hold only what something has brought in, so they are not the whole picture for someone else.

**Contracts** lists the contracts they're on: **Issued**, **Type**, **Role** (*Issued*, *Accepted*, *Offered to them* or *Issued by a member*), **Contents**, **Price**, **Reward**, **Other party**, **Status**, **Location** and **Region**. Public contracts come from the [Contracts](contracts.md) tool's sweep of every region; the rest are your own characters' and corporations'. Click a contract to open it in the Contracts tool.

**Market** lists their trades: **Date**, **Item**, **Side** (*Bought* or *Sold*, from their side), **Qty**, **Unit Price**, **Total**, **Other party** and **Location**. Only trades in your wallets show: all of them if this is one of your characters or corporations, otherwise only the ones made with you.

Both tabs have **From** and **Thru** boxes. The range starts as the past twelve months, and stays as you set it when you move to the next entity.

**Corp Taxes** gives, month by month, the **Ratting tax** and **Industry tax** paid into each of your corporations, with a total above. It reads the same journal entries as [Corp Activity](corp-activity.md)'s tax payer lists, and shows only when there is something to list.

### Corp History summary

On a pilot's **Corp History**, pick a row to see a summary below the grid of what the app holds of their time in that corporation: **Kills**, **Losses**, **Ratting tax**, **Industry tax**, **Contracts** and **Market trades**. Taxes read *No journal held* for a corporation whose wallet journal you don't have, which isn't the same as nothing paid.

## Using it

- **Search by name** to look up any entity, on either side.
- **Select an entity** to open its detail panel, then use the sub-tabs.
- Entity names are clickable across the app's tools, so you can jump to a record from wherever a name appears.
- **Copy the name** with the copy button beside it. The main window says it was copied.

## Notes

- Kills fetched on the **Kills / Losses** tab are stored like any other kill from [zKillboard](../zkillboard.md). Kills that don't involve your own characters or corporations are trimmed by the **Others** rule under **Settings ▸ Data Retention**, if you turn it on — see [Data retention](../storage-postgresql.md#kill-mails).
- The zKillboard stats and the extra kills need zKillboard to be reachable. Without it, the tab shows only the kills stored here. They're fetched whether or not **Enable zKillboard kill import** is ticked under **Settings ▸ Kill Mails**.
- The NPC side comes from the bundled SDE and needs no ESI authorization. The NPC corporation facts (headquarters, ticker, tax rate, description) and their station lists are read from SDE fields added in 0.9.13 — if they're blank, run **Update SDE** once (see [Getting Started](../getting-started.md)).
- Player detail such as market **Orders**, **LP Offers** and **Faction Warfare** is populated from synced data and appears once it's available.
