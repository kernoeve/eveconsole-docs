# Jump Planner

Plan a capital jump route across New Eden: pick a hull and jump skills, add your waypoints, and get the full route with per-leg distances and fuel.

Open it from the left sidebar under **Universe**.

## What it shows

The screen is split into an input panel on the left and the galaxy map on the right.

### Input panel

- **Ship** — a **Hull** dropdown (e.g. a jump freighter).
- **Jump Drive Calibration** and **Jump Fuel Conservation** — the skill levels (0–5) used in the calculation.
- A computed **jump range** line ("X ly per jump").
- **Jump Through** — a dropdown that limits where the route may *stop* (e.g. stations & structures); it does not restrict where the route may start or end.
- **Waypoints** — the list of systems to route through; add systems by name, and each waypoint shows its security.
- **Plan Route** and **Clear**, plus a status line ("Route planned.").

### Map area

- The galaxy map with the planned route drawn through the waypoints and any intermediate midpoints.
- A summary header showing the total jumps, total light-years, the fuel required (with the isotope type) and the jump range.
- A per-leg table below: #, From, Jump to, Region, Sec, Distance and Fuel.

## Using it

1. Choose a **Hull** and set your **Jump Drive Calibration** and **Jump Fuel Conservation** skill levels.
2. Optionally set **Jump Through** to control where the route may stop.
3. Add your **Waypoints** by name.
4. Click **Plan Route**.
5. Read the summary header for the totals and the per-leg table for each jump; use **Clear** to start over.

## Notes

- Interact with the route directly: drag a midpoint to move it, click a midpoint for alternative systems, and scroll to zoom.
- The planner understands jump-through structures, restricts midpoints to systems you can actually use, and offers alternatives when a midpoint won't work.
- To browse systems, overlays and intel, use the [Universe Map](universe-map.md).
