# Route Planner

Plan a route from one system to another through stargates, the jump bridges your alliance may use, and the wormholes of Thera and Turnur — keeping out of the systems you avoid. The route is listed jump by jump, drawn on the map, and can be sent to the game's autopilot.

Open it from the [Universe Map](universe-map.md): click **Route planner** above the tabs.

## What it shows

### Planning

- **Character** — whose route this is. Their alliance decides which jump bridges are open: only the alliance holding sovereignty where a jump starts may use the bridge. Online characters are listed first, with the system they're in.
- **From** — the start. **Here** starts from where the character is. The route starts there by itself when the chosen character is online.
- **To** — the destination. **⇅** swaps From and To.
- **Prefer** — **Shortest**, **Safer (high security)** or **Less secure (low and null)**. Like the game's own settings, a safer or less secure route keeps to that space whenever it can. When two routes are as good, the one with fewer bridge and wormhole jumps wins.
- **Use jump bridges** — on by default. See [Jump Bridges](jump-bridges.md).
- **Use Thera and Turnur** — on by default. Uses the wormholes EVE-Scout lists (see [Map Data](../logs-and-map-data.md#map-data)), if the ship fits through them.
- **Ship** — the size of ship, for the wormholes: **Frigate or destroyer**, **Cruiser or battlecruiser**, **Battleship** (the default) or **Freighter**.
- **Avoid list** — shows or hides the systems routes keep out of. See [Avoid list](#avoid-list).
- **Plan Route** and **Clear** — **Clear** takes the route off this tab and off the map.
- **Show on map** — draws the route on the Universe Map's tabs. Remembered.
- **Set destination** — sends the route to the game's autopilot.

### The route

A summary line gives the number of jumps, how many are by jump bridge and by wormhole, and the lowest security on the way. Then one row per system:

- **System**, **Region** and **Sec**. Click a system to open its page.
- **Via** — how the system was reached: *Gate*, *Jump bridge* (with its zone and capacitor cost) or *Wormhole* (with the signatures to warp to on each side).
- **Hostiles** — hostiles placed there now, from intel and killmails, as on the map's [live marks](universe-map.md#live-marks).
- **Kills (1 h)** — kills there in the last hour.

If some bridges on the route have no known sovereignty holder, a line says so: who may use them isn't known, and they're allowed rather than left out.

## Set destination

The game's autopilot knows nothing of jump bridges or wormholes. So **Set destination** gives it a waypoint on each Ansiblex on the route, in order, then the destination. The game picks the gates in between by its own route settings; each bridge or wormhole is yours to jump. A bridge added by hand names no structure, and a wormhole is a signature, so the system it's in stands in for it.

Who it's sent for is read when you click:

- With one character online (or none), it goes at once.
- With more than one online, a list drops down: **All online**, then each character.

The game only takes a destination for a character who is logged in. The character's token needs the waypoint scope (`esi-ui.write_waypoint.v1`); if it was added before you granted it, re-authorise the character.

## Avoid list

Systems on the avoid list are never routed through, and are ringed red on every map tab.

- In the route planner, click **Avoid list**, then type a system to add it, or click **×** to take one off.
- Right-click a system on the map, or in a route, to add it to the avoid list or remove it.

The avoid list is kept on this computer.

## Using it

1. Click **Route planner** above the Universe Map's tabs.
2. Pick a **Character** — the one who will fly the route.
3. Set **From** (or click **Here**) and **To**.
4. Choose what to **Prefer**, whether to use bridges and wormholes, and the **Ship** size.
5. Click **Plan Route**, and read the route jump by jump.
6. Click **Set destination** to send it to the game.

## Notes

- Capital ships cannot use jump bridges, except Rorquals, freighters and jump freighters. For a capital's jump drive route, use the [Jump Planner](jump-planner.md).
- If no route is found, the systems aren't connected in the ways allowed, or the avoid list closes every way.
- Thera and Turnur connections go stale within hours. EVE-Scout is read every five minutes; switching it off under **Settings ▸ Map Data** deletes the stored list.
