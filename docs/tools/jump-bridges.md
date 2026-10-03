# Jump Bridges

Every jump bridge EVE Console knows, where each one leads, who may jump each way and what the jump costs. Bridges are drawn on the [Universe Map](universe-map.md) and used by the [Route Planner](route-planner.md).

Open it from the [Universe Map](universe-map.md): click **Jump bridges** above the tabs.

## Where bridges come from

**From ESI.** A corporation's structures include its Ansiblex jump gates, but nothing in ESI says where a gate leads. Its name does: by convention a gate is named `Source » Destination - label`, and EVE Console reads the destination from that. A bridge is two gates, one in each system.

- When both gates belong to corporations you have added a token for, both are shown.
- When the far gate belongs to someone else, the bridge is still known from the near gate's name, and is drawn fainter on the map.
- A gate whose name doesn't say where it goes is listed under **Gates whose name does not say where they go**, not guessed at.
- Only gates in the corporation's current structure list count, so a gate that has been taken down drops off.

**By hand.** Add the rest yourself — other corporations' and allies' bridges:

- **Add a bridge** — pick a system for each end, add an optional note, and click **Add**.
- **Paste a list** — paste one bridge per line and click **Import**. The game's own `QZ-X77 » XQ1-Z2 - Home run`, `XQ1-Z2 <-> 9-97XQ`, `A -> B`, and other tools' exports with ids or notes around the names are all read: any line that names two systems. Bridges already known are counted, not added twice. Lines that don't name two systems stay in the box for you to fix.

Only bridges added by hand can be removed here — click **✕** on the row.

## What it shows

A summary line counts the bridges, how many are from ESI and how many were added by hand. Then one row per bridge:

- **System** and **System** — the two ends. Click a name to open that system in a tab.
- **Source** — *ESI, both gates*, *ESI, one gate*, *Added by hand*, or *ESI and by hand*.
- **Fuel** — the days of fuel left in whichever gate runs dry first, and the date. Under a week is shown in amber.
- **Gates** — the gates' names and owners.
- A line for each direction: who may jump that way, and the zone and capacitor cost of the jump.

The list is read when the app starts, again every minute with the map's overlays, and at once after you add or remove a bridge.

## Who may jump

Since 22 September 2026 an Ansiblex can be used only by pilots of the **alliance holding sovereignty in the system the jump starts from**. An access list can narrow that, but no longer widen it. Capital ships cannot use bridges at all, except Rorquals, freighters and jump freighters.

So each way across a bridge is judged on its own. A system nobody holds means nobody can jump from it. If sovereignty can't be read at the moment, the tab says so.

Sovereignty and capital systems come from ESI's public sovereignty data, read at most every half hour.

## Zones

Zones don't bar anyone. They set how much of the bridge's capacitor a jump uses: the ship's base cost times a multiplier, by the straight-line distance from the sovereign alliance's **capital system** to where the jump **lands**.

| Zone | Distance from the capital | Capacitor cost | Colour |
| --- | --- | --- | --- |
| 1 | within 5 ly | free | blue |
| 2 | 5–10 ly | 2× | green |
| 3 | 10–15 ly | 6× | yellow |
| 4 | 15–20 ly | 9× | orange |
| 5 | beyond 20 ly | 15× | red |

The same bridge is cheaper jumping towards the capital than away from it. An alliance with no capital system has no zones; its bridges show "zone unknown" and are drawn in plain violet.

Distances are true 3D light years from the game's static data, not the map's flat layout.

On the map, each half of a bridge's arc is coloured by the zone of its end — the zone a jump landing there is charged at. The **Sovereignty zones** overlay colours every claimed system the same way, captioned with its zone and holder, and a system's page shows its **Ansiblex zone** in the header.

## Using it

1. Open the **Jump bridges** tab from the Universe Map.
2. Check the bridges read from ESI, and any gates whose names couldn't be read.
3. Add your allies' bridges, one at a time or by pasting a list.
4. Read each direction's line to see who may jump that way and what it costs.

## Notes

- Bridges from ESI need a token for a corporation that owns Ansiblexes, with access to its structures. See [Getting Started](../getting-started.md).
- A gate renamed in game is picked up on the next structure poll.
- Bridges added by hand are stored in the database, so every client sharing it sees them.
