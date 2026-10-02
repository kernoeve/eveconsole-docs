# Jump Planner & Jump Range

Two tabs of the [Universe Map](universe-map.md) for ships with a jump drive. The **Jump planner** plans a capital jump route: pick a hull and jump skills, add your waypoints, and get the full route with per-leg distances and fuel. The **Jump range** lists every system a jump drive reaches from a character or a system.

Open them from the [Universe Map](universe-map.md): click **Jump planner** or **Jump range** above the tabs.

## Jump planner

The tab is split into an input panel on the left and its own galaxy map on the right.

### Input panel

- **Ship** — a **Hull** dropdown (for example a jump freighter).
- **Jump Drive Calibration** and **Jump Fuel Conservation** — the skill levels (0–5) used in the calculation.
- A computed **jump range** line ("X ly per jump").
- **Jump Through** — limits where the route may *stop*: **Anywhere**, **Stations & structures**, **Fortizar / Keepstar systems** or **Keepstar systems**. It does not restrict where the route may start or end.
- **Waypoints** — the list of systems to route through; add systems by name, and drag them to reorder. Each waypoint shows its region and security.
- **Plan Route** and **Clear**, plus a status line ("Route planned.").
- **Show on map** — also draws the route on the Universe Map's tabs, dashed. Remembered; a route still planned comes back when you reopen the tab.

### Map area

- The galaxy map with the planned route drawn through the waypoints and any intermediate midpoints.
- A summary header showing the total jumps, total light years, the fuel required (with the isotope type) and the jump range.
- A per-leg table below: #, From, Jump to, Region, Sec, Distance and Fuel.

### Using it

1. Choose a **Hull** and set your **Jump Drive Calibration** and **Jump Fuel Conservation** skill levels.
2. Optionally set **Jump Through** to control where the route may stop.
3. Add your **Waypoints** by name.
4. Click **Plan Route**.
5. Read the summary header for the totals and the per-leg table for each jump; use **Clear** to start over.

Interact with the route directly: drag a midpoint to move it, click a midpoint for alternative systems, and scroll to zoom.

## Jump range

Every system a jump drive reaches from a system, nearest first.

- **Character** — picking a character takes their system, their hull if it has a jump drive, and their trained Jump Drive Calibration. The range then follows them as they move, re-read every 30 seconds.
- **From** — the system to measure from. **Here** takes the character's system. Typing a system stops following the character.
- **Hull** and **Jump Drive Calibration** — what sets the range.
- **Land in** — **Anywhere**, **Stations & structures**, **Fortizar / Keepstar systems** or **Keepstar systems**.
- **Show on map** — rings the systems in range green on every map tab, with the origin ringed heavier. Zoomed out, each region holding one is ringed. Remembered.

The list shows each **System**, its **Region**, **Sec** and the distance in **LY**. Click a system to open its page.

## Notes

- A jump drive cannot be used in high sec, wormhole space, Pochven or Zarzakh, so none of those are ever in range or used as a landing place. Starting in one, the tab says why nothing is in range.
- Distances are straight-line light years.
- The planner understands jump-through structures, restricts midpoints to systems you can actually use, and offers alternatives when a midpoint won't work. Player structures count only once the app has resolved them, so the station options under-report rather than guess.
- For a route through gates, jump bridges and wormholes, use the [Route Planner](route-planner.md).
