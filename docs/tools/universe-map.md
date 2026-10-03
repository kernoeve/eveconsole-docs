# Universe Map

A map of New Eden, from the whole cluster down to a single system, with overlays for sovereignty, security, kills, jumps, industry and intel. Hostiles reported on intel or seen on killmails, and your own characters, are marked on it live. The same tool holds the route planner, the jump planner, the jump range, jump bridges and sovereignty campaigns, each in a tab of its own.

Open it from the left sidebar under **Structures / Navigation**.

## Tabs

The Universe Map is a tool of tabs. A tab is either a **map** of New Eden or a **system's page**, and you can have as many of each as you like. The other tabs — **Route planner**, **Jump planner**, **Jump range**, **Sov campaigns** and **Jump bridges** — are opened by their buttons above the tabs. There is only ever one of each; pressing its button again brings it forward.

Above the tabs:

- **+ New map** — opens another map of New Eden.
- **Route planner**, **Jump planner**, **Jump range**, **Sov campaigns**, **Jump bridges** — open those tabs. See [Route Planner](route-planner.md), [Jump Planner & Jump Range](jump-planner.md) and [Jump Bridges](jump-bridges.md).
- A **search** box for a system, constellation or region. What you pick opens in a new tab: a system's page, or a map framed on the constellation or region. A system that already has a tab is brought forward instead of opened twice.

**Side by side.** Drag a tab onto the right half of the tool to see two tabs side by side. Tabs can be dragged back and forth between the two halves, or along a strip to reorder them. The split closes when one side runs out of tabs.

Each map tab keeps its own overlay and zoom, and every tab keeps its view while it is open — a system page keeps its scroll position and sub-tab.

## The map

Scroll to zoom and drag to pan. Zoomed out, the map shows region boxes; zooming in opens the regions into their systems. Click a system or region to see its details on the right; double-click a region to open it, or a system to open its page in a tab.

**Toolbar**

- **Overlay** — the data colouring the map. See [Overlays](#overlays).
- **Refresh** — reloads the map data.
- **Clear route** — takes every planned route off the map. A tool's route comes back the next time that tool plans one.
- **Jump bridges** — shows or hides jump bridges. On by default.
- **Thera / Turnur** — shows or hides wormhole connections from Thera and Turnur. Offered only while EVE-Scout reading is on (see [Map Data](../logs-and-map-data.md#map-data)).
- **Storms** — shows or hides metaliminal storms.
- **Sov campaigns** — shows or hides sovereignty campaigns.
- **Details** — shows or hides the details and legend panel on the right, giving the map the whole tab. Each tab remembers its own choice; a new tab starts with the last one you made.

The toggles are remembered on this computer.

**Right-hand panel**

- The details of what you clicked.
- **Legend** — the colour key for the active overlay, and keys for the marks below.
- **Docking** — read from the bar above each system box: *Supers & titans* (Keepstar only), *Capitals* (Fortizar or NPC station) and *Subcapitals* (any other structure).
- **Services** — read from the indicators under each box: Manufacturing, Research / Invention, Reprocessing, Reactions, Clone bay and Market.

### Live marks

While the Universe Map is on screen, it reads who is where every 5 seconds and marks every map tab:

- **Red round mark** — hostiles placed in that system in the last 5 minutes, by an intel report or a killmail. Hover for each pilot's portrait, corporation and alliance, what they fly, how long ago, and whether intel or a killmail put them there.
- **Red "!"** — intel said something about the system (a spike, bubbles, a gate camp) but counted nobody. Hover to read what was said.
- **Blue square mark** — your characters online there. Hover for their ship and whether they are docked or in space.

Zoomed out, each region carries the total of its systems.

A pilot is placed where their newest report or killmail puts them: an intel report naming them, or a killmail they were an attacker on, with the hull from the mail. The victim of a newer killmail is down, and leaves the map.

*Hostile* means anyone who isn't yours. Your characters, corporations and alliances are left out, and so is anyone you, your corporations or your alliances have set to positive standing. Blues are usually set once, on the alliance, so each character's alliance contacts are read along with the character's and corporation's own — at most once per alliance every five minutes. A pilot blue only through the alliance counts as friendly.

### Other marks

- **Jump bridges** — a dashed arc between the two ends of each bridge. Each half is coloured by the zone of its end, because the two ways across a bridge can cost differently. The arc is fainter when ESI shows only one of the two gates. Hover for the gates, who may jump each way, fuel and where the bridge is known from. See [Jump Bridges](jump-bridges.md).
- **Θ and T** — a teal tag on each system with a wormhole to Thera (Θ) or Turnur (T). Hover for the signature in that system and on the far side, the largest ship it takes, and the time left. Dashed teal lines run from Turnur to each system it reaches; Thera is in wormhole space, off the map, so it has tags only.
- **⚡** — an amber tag on a system with a metaliminal storm, as reported to EVE-Scout. Hover for the kind of storm.
- **⚔** — a red tag on a system with a sovereignty campaign, and a solid red ring once the fight has started. Hover for the structure, the defender, the scores, and when it starts in EVE time and your local time.
- **A planned route** — drawn by the [Route planner](route-planner.md) and the [Jump planner](jump-planner.md) when their **Show on map** box is ticked. Jumps by bridge, wormhole or jump drive are dashed.
- **Green rings** — systems in range of the [Jump range](jump-planner.md#jump-range) tab, with the origin ringed heavier.
- **Red rings** — systems on your [avoid list](route-planner.md#avoid-list). Right-click a system to add it to the avoid list, or take it off.

Zoomed out, each region carries a summary of the tags of its systems.

### Overlays

Choose one from **Overlay**:

- **Security**, **Constellation**.
- **Sovereignty** and **Sovereignty ADM**.
- **Sovereignty zones** — each claimed system coloured by its distance from the holder's capital, which sets what a jump bridge jump landing there costs. See [Jump Bridges](jump-bridges.md#zones).
- **Sovereignty standings** — each claimed system in the game's standing colours, by what your side thinks of its holder. Your own space is green. The standings come from your characters', corporations' and alliances' contacts: the alliance's say wins over the corporation's, and the corporation's over a character's.
- **Industry** — manufacturing, reactions, ME research, TE research, copying and invention cost indices.
- **Ship kills** and **Pod kills** — 24 hours, 7 days or 30 days.
- **Intel (15m)** and **Intel paths** (15 minutes, 1 hour, 24 hours) — from your intel channels.
- **Ship jumps** (24 hours, 7 days) and **NPC kills** (24 hours).
- **Faction warfare** — each militia's systems in its own colour. Front-line systems (bordering another militia's) are bright, command operations (bordering their own front line) less so, and the rearguard dim. Contested or vulnerable systems have a dashed outline.
- **Incursions** — zoomed out, regions with an incursion are coloured by the most advanced one; hover to list each one's constellation, state, influence, faction and boss.
- **Planetary power**, **Planetary workforce**.
- **Stations (NPC/player)**, **Planets**, **Moons**, **Asteroid belts**.

Overlays that count intel or kills are re-read every minute while the map is on screen.

!!! note "Where the numbers come from"
    The **Ship kills** and **Pod kills** overlays are counted from the killmails this app has stored. With the default [zKillboard](../zkillboard.md) scope, **My characters & corp only**, that means only kills involving you and your corporations. Choose **Capture all kills** to see kills across all of New Eden.

    **Ship jumps**, **NPC kills**, sovereignty, industry indices, faction warfare and incursions come from the map statistics under **Settings ▸ Map Data**. Those overlays are empty until the first backfill has finished — by default it fetches 7 days. See [Logs & Map Data](../logs-and-map-data.md#map-data).

    The intel overlays count each hostile pilot named in the window once, plus the most unnamed pilots any one report gave. A "+5" reposted by three scouts counts as 5, not 15.

## System view

Double-click a system — or click a system name anywhere in the app, or pick one in the search — to open that system's page in a tab of its own.

- A **breadcrumb** (Universe ▸ Region ▸ System). The region and constellation links go back to the map tab you used last, framed on that area, and open a map tab if none is open.
- A **header** with security and true security, region, constellation, sovereignty, local pirate faction, and the system's industry indices (Manufacturing, TE, ME, Copy, Invention, Reaction). When they apply, it also shows:
    - **Incursion** — state, influence, faction, staging system and boss.
    - **Campaign** — a sovereignty campaign scheduled or running here.
    - **Weather** — a metaliminal storm.
    - **Ansiblex zone** — the zone, the distance from the holder's capital, and what a jump bridge jump landing here costs.
    - **Now** — hostiles placed here in the last 5 minutes, and your characters here.
- A **stats box**: Planets, Moons, Belts, Jumps 1h / 24h, Ship kills, NPC kills and Pod kills.

Tabs:

- **Overview** — hourly Jumps / NPC kills / Ship kills / Pod kills graphs, sovereignty structures and recorded sovereignty changes, the system's **Jump bridges** (where each leads, the gate here, who may jump each way, fuel), its **Thera and Turnur** wormholes (where each leads, the signature here and on the far side, the largest ship, the time left — Turnur's page lists all of its holes), a **Gates** list, **Player structures** and **NPC stations**.
- **Celestials** — the system's celestials as a tree, in orbital order.
- **Graphs**, **Agents**, **Kills**, **Events** and **Intel**.

While a system tab is on screen, its counts, intel, recent kills, sovereignty and incursion lines are refreshed every 30 seconds, and again when you bring the tab forward. Rows that haven't changed stay where they are.

## Sov campaigns

The **Sov campaigns** tab lists every sovereignty campaign now and coming, soonest first: **State**, **System**, **Region**, **When**, **Starts**, **Structure**, **Defender** and **Scores**. Choose a **Region** to narrow the list. Click a system to open its page.

Campaigns are read from ESI at most once a minute while the Universe Map is on screen.

## Intel from chat logs

If you monitor intel channels (see [Logs & Map Data](../logs-and-map-data.md#chat-logs)), their messages are parsed into *sightings* — who was seen, where, in what hull, and anything else said about the system, such as a gate camp or bubbles. Sightings appear on the live marks, the intel overlays and each system's **Intel** tab, with pilot / corp / alliance portraits and the original chat line kept alongside.

On the **Intel** tab, the note column leads with what was said about the system ("gate camp, bubbles · on the QZ-X77 gate"), then any hulls nobody was named in, then the rest of the line.

Reports of only your own pilots, or of pilots at positive standing, are left out.

!!! note
    Duplicate messages are recognised across characters and machines, so importing a second computer's logs doesn't double-count sightings.

## Using it

1. Choose an **Overlay** to colour the map by the data you care about.
2. Scroll to zoom and drag to pan, or search for a system, constellation or region.
3. Double-click a system to open its page in a tab.
4. Drag a tab onto the right half to keep a map and a system page side by side.
5. On a system's page, use the tabs to read its activity graphs, gates, bridges, stations, celestials and intel.

## Notes

- The map and overlays reflect only data the app has synced — killmails, sovereignty, industry indices, and so on.
- Live marks and the minute-by-minute overlay refresh run only while the Universe Map is on screen.
- Map statistics are collected hourly and thinned to daily as they age, with history backfilled from EVE Ref's archives for spans ESI does not serve. How much is fetched and kept is set under **Settings ▸ Map Data** — see [Logs & Map Data](../logs-and-map-data.md#map-data).
