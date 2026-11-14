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
- **♦ rats** — shows or hides [♦ rat activity](#rat-activity-and-npc-capitals). On by default.
- **NPC capitals** — shows or hides [NPC capitals](#rat-activity-and-npc-capitals). Its arrow opens **Titans**, **Supercarriers** and **Dreadnoughts** boxes to choose which. All on by default.
- **Intel** — a drop-down of what the map draws from intel besides the marks. See [Intel layers](#intel-layers).
- **Details** — shows or hides the details and legend panel on the right, giving the map the whole tab. Each tab remembers its own choice; a new tab starts with the last one you made.

The toggles are remembered on this computer.

**Right-hand panel**

- The details of what you clicked.
- **Legend** — the colour key for the active overlay, and keys for the marks below.
- **Docking** — read from the bar above each system box: *Supers & titans* (Keepstar only), *Capitals* (Fortizar, Sotiyo or NPC station) and *Subcapitals* (any other structure).
- **Services** — read from the indicators under each box: Manufacturing, Research / Invention, Reprocessing, Reactions, Clone bay and Market.

### Live marks

While the Universe Map is on screen, it reads who is where every 5 seconds, and at once when new intel is written on any PC, and marks every map tab. It shows the same intel as the [Intel](intel.md) tool:

- **Round mark** — hostiles placed in that system by an intel report, a pasted Local or a killmail, in their standing's colour: red, orange or neutral grey, by the worst among them. It fades as the news ages, and goes once its time is up (see [How long intel lasts](intel.md#how-long-intel-lasts)). Hover for when the newest news came, the standing, what was said about the system, and each pilot's portrait, corporation and alliance, what they fly, how long ago, and whether intel or a killmail put them there.
- **Hollow mark with a dashed ring** — *no visual*: reported in Local, never seen on grid.
- **Red "!"** — intel said something about the system (a spike, bubbles, a gate camp) but counted nobody. Hover to read what was said.
- **Green check** — the system was called clear, and nothing has been said since. It fades over the clear's lifetime.
- **Blue square mark** — your characters online there. Hover for their ship and whether they are docked or in space.
- **Fuchsia ★** — officer NPCs seen in that system since the last downtime (11:00 EVE time), with a count when there is more than one. An officer's own death leaves no killmail, but every pilot it kills does, with the officer among the attackers; officers despawn at downtime, so the star points to where one may still be. Whether somebody has killed it since can't be seen. Hover for each officer's portrait, its latest kill in EVE time and how long ago, the ship it killed, and how many killmails it has been on there since downtime. It reads the killmails the app has stored, so with [zKillboard](../zkillboard.md) on it sees far more than your own kills.

Zoomed out, each region carries the total of its systems, in the worst standing in it and as fresh as its freshest news.

A pilot is placed where their newest sighting puts them: an intel report naming them, a pasted Local, or a killmail they were an attacker on, with the hull from the mail. The victim of a killmail is no threat and isn't counted. A pilot leaves a system when seen somewhere else, when the system is called clear, or when a pasted Local of it leaves them out.

*Hostile* means neutral or worse. Your own characters are left out, and so is anyone in a corporation or alliance one of your characters is in. The map has no single character looking, so a pilot counts as friendly when any of your characters, their corporations or their alliances has them at positive standing, or, when **Settings ▸ Intel** forces one character's standings, when that character does (see [Standings](intel.md#standings)). Blues are usually set once, on the alliance, so each character's alliance contacts are read along with the character's and corporation's own — at most once per alliance every five minutes.

### ♦ rat activity and NPC capitals

Two more marks, read from the killmails the app has stored. They sit in the lower-left tag row of a system, left of the officer ★. Zoomed out, each region lists its marked systems.

- **Sky-blue ◆ tag** — ♦ pirate NPCs have killed players in this system in the last 5 days. The number is the players killed in the current run: a run is one faction's ♦ kills in the system with no quiet spell over 5 days, and the mark stays until 5 days after its last kill. Runs are traced back up to 60 days, and one still going at that limit says "since before". Hover for each faction, the players killed and over how long, the first and last kill in EVE time and how long ago, and the hulls seen. The mark says what was seen, not what is behind it.
- **Orange T, S or D tag** — NPC titans (T), supercarriers (S) or dreadnoughts (D) on a killmail here since downtime (11:00 EVE time); the letter is the biggest class seen. Hover for each hull's faction, its kills here since downtime, and its last kill in EVE time and how long ago.

Only the pirate factions count — Guristas, Angel Cartel, Blood Raiders, Sansha's Nation and Serpentis. EDENCOM and CONCORD police and the empire mining guards kill players too, but aren't rats. Pods aren't counted: a pod after its ship is the same player, not a second kill. Faction warfare, mission and Homefront capitals are left out.

The **♦ rats** and **NPC capitals** buttons turn them on and off, and the capitals' arrow chooses the classes. Turning a class off takes it out of the counts and the hovers too. The choices are kept on this computer. The killmails are read at most every 2 minutes, and the capitals start afresh at downtime. With [zKillboard](../zkillboard.md) on **Capture all kills** they see far more than your own kills.

### Intel layers

The **Intel** drop-down on the toolbar switches what the map draws from intel besides the marks. They are drawn only where systems are shown, not on the regions, and each is in the standing's colour of the pilots behind it, fading as the news ages.

- **Gate camps** — a gate camp found from kills, drawn as a thick stub on the gate's line, from the camped system towards where the gate leads, with the kills counted on it. Hover for the kills, how long ago the last was, the attackers and what they brought. On by default. See [Camps](intel.md#camps).
- **Movement arrows** — a solid arrow from where reported pilots came from into the system they were seen in. On by default.
- **Heading arrows** — a dashed arrow from the system a pilot was seen in to where they were said to be heading. On by default.
- **Alert zones** — a thin dashed outline round every system an enabled [Intel report](alarms.md#intel-report) alarm watches now: what would make one go off. Off by default.

At most the newest 30 arrows in view are drawn.

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
    - **Now** — hostiles placed here by intel or killmails that are still current, and your characters here.
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

If you monitor intel channels (see [Logs & Map Data](../logs-and-map-data.md#chat-logs)), or have Jabber rooms or IRC channels whose **Type** is **Intel**, their messages are parsed into *sightings* — who was seen, where, in what hull, where they came from or were heading, and anything else said about the system, such as a gate camp or bubbles. Sightings appear on the live marks, the intel overlays and each system's **Intel** tab, with pilot / corp / alliance portraits and the original chat line kept alongside. The [Intel](intel.md) tool lists them all, measured from your characters.

On the **Intel** tab, the note column leads with what was said about the system ("gate camp, bubbles · on the QZ-X77 gate"), then any hulls nobody was named in, then the rest of the line.

Reports of only your own pilots, or of pilots at positive standing, are left out of the marks.

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
- Hostiles placed by killmails, the ◆ and NPC capital marks, and gate camps read the killmails the app has stored, so with the default [zKillboard](../zkillboard.md) scope, **My characters & corp only**, they see only kills involving you and your corporations.
- Map statistics are collected hourly and thinned to daily as they age, with history backfilled from EVE Ref's archives for spans ESI does not serve. How much is fetched and kept is set under **Settings ▸ Map Data** — see [Logs & Map Data](../logs-and-map-data.md#map-data).
