# Universe Map

A single continuous map of New Eden, from the whole cluster down to an individual system, with overlays for sovereignty, security, kills, jumps, industry and intel. Double-clicking a system opens its own detailed page.

Open it from the left sidebar under **Universe**.

## What it shows

The map is one continuous view — there are no separate drill-down levels. Scroll to zoom and drag to pan; double-click a system (or region) to zoom straight in. At the region scale the map shows region boxes; zooming in opens the regions into their systems.

**Toolbar**

- **Overlay** dropdown — the data colouring the map: Sovereignty, Security, kills, jumps, industry indices, stations, planetary output, and intel sightings.
- **Go To** — a search box; type a region or system name to jump to it.
- **Refresh** — reloads the map data.
- A **status line** reporting the current scale, e.g. "70 regions · 5,485 systems".

**Right-hand panel**

- **Legend** — the colour key for the active overlay.
- **Docking** key — read from the bar above each system box: *Supers & titans* (Keepstar only), *Capitals* (Fortizar or NPC station) and *Subcapitals* (any other structure).
- **Services** key — read from the indicators under each box: Manufacturing, Research/Invention, Reprocessing, Reactions, Clone bay and Market.

**Nodes**

- System nodes render as small boxes coloured by the active overlay, with the docking bar above and service indicators below.
- At the region scale, region boxes and docking-class badges are shown instead.

!!! note
    Kill counts on the map come from killmails this app has stored (see [Killmails](killmails.md)), not from all of New Eden.

## System view

Double-clicking a system — or clicking a system name anywhere in the app, or from a killmail — opens that system's own page.

- A **breadcrumb** (Universe ▸ Region ▸ System).
- A **header** with security / true-sec, region, constellation, sovereignty, local pirate faction and the system's industry indices (Manufacturing, TE, ME, Copy, Invention, Reaction).
- A **stats box**: Planets, Moons, Belts, Jumps 1h/24h, Ship kills, NPC kills and Pod kills.

Tabs:

- **Overview** — hourly Jumps / NPC kills / Ship kills / Pod kills graphs, sovereignty structures and recorded sovereignty changes, a Gates list (each gate's security and destination region) and an NPC Stations table of Name / Type / Corporation / Location.
- **Celestials** — the system's celestials as a tree.
- **Graphs**, **Agents**, **Kills**, **Events** and **Intel**.

## Intel from chat logs

If you monitor intel channels (see [Game & Chat Logs](logs.md)), their messages are parsed into *sightings* — who was seen, where, and in what hull. Sightings appear on the map's intel overlays and on each system's **Intel** tab, with pilot / corp / alliance portraits and the original chat line kept alongside.

!!! note
    Duplicate messages are recognised across characters and machines, so importing a second computer's logs doesn't double-count sightings.

## Using it

1. Choose an **Overlay** to colour the map by the data you care about.
2. Scroll to zoom and drag to pan, or type a name into **Go To** to jump straight there.
3. Double-click a region to open it into systems, then a system to open its page.
4. On a system's page, use the tabs to read its activity graphs, gates, stations, celestials and intel.

## Notes

- The map and overlays reflect only data the app has synced — killmails, sovereignty, industry indices, and so on.
- Map statistics are collected hourly and thinned to daily as they age, with history backfilled from EVE Ref's archives for spans ESI does not serve.
- To plan a capital route across the map, use the [Jump Planner](jump-planner.md).
