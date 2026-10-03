# Killmails

A zKillboard-style browser for every killmail EVE Console has stored — your own kills and losses, and any others brought in from [zKillboard](../zkillboard.md) — with a filterable list and a full detail view for each killmail.

Open it from the left sidebar under **Corp / Interactions**.

## What it shows

A two-pane layout:

- **Left pane** — a filter bar and a scrollable kill list. Each row shows the date/time and total ISK value, the victim ship render, the system with its security status (colour-coded) plus constellation and region, the victim (name / corp / alliance with logo), and the final-blow pilot (name / corp / alliance with logo). A status bar reports how many killmails are loaded, and whether more match.
- **Right pane** — the detail for the selected killmail:
    - **Header** — victim ship, victim name/corp/alliance, time and system/region, and an ISK summary (Destroyed, Dropped, Total).
    - **Items** — fitted and cargo items grouped by slot, each with icon, quantity destroyed, quantity dropped, and estimated value.
    - **Attackers** — every attacker with portrait, ship and weapon icons, name/corp/alliance, and damage done. The final-blow pilot is tagged **★ FB** and the top-damage dealer **▲ TD** (a pilot can be both).

Losses appear alongside kills in the same list. Ship, portrait, corp, and alliance images are loaded from EVE's image server and cached.

## Using it

- **From / Thru** — a date range, defaulting to the last 30 days.
- **Character**, **Corp**, **Ship**, **System/Region** — free-text filters. Character matches either the victim or the final-blow pilot, and Corp either one's corporation — any corporation, not only your own. System/Region matches either the system or the region name. All filters are applied together, across every stored kill, not just the rows already loaded.
- **Clear** — clears every filter, including the dates.
- **Refresh** — reloads the list.
- **Load More** — the list loads 500 killmails at a time, newest first. When more match, the status bar says so and **Load More** fetches the next 500.
- Click a row to load its full detail on the right; the detail is fetched on demand. Click a pilot, corporation or alliance to open it in [Players & NPCs](entities.md), an item to open it in the Item Browser, or the system to open it on the [Universe Map](universe-map.md).

## Notes

- Your own kills come from ESI, through character and corporation tokens with killmail scopes (see [Getting Started](../getting-started.md)). What else is listed depends on your [zKillboard](../zkillboard.md) scope, and on the kill-mail rules under **Settings ▸ Data Retention**.
- ESI only returns kills where you were the victim or got the final blow. The rest — kills you took part in without the final blow — come from [zKillboard](../zkillboard.md), which is on by default.
- Item estimated values come from stored pricing, which depends on a configured market — see [Configuring Markets](../configuring-markets.md).
- A recent 24-hour view of corp kills and losses also appears in [Corp Activity](corp-activity.md), which can hand a killmail off to this browser.
