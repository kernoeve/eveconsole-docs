# Background Processes

A live monitor for the work EVE Console does on a timer — ESI polling, market pricing, contracts, killmails, LP-store catalogues, alarms and order fulfilment. It's a diagnostic view: somewhere to see what has run, what's due next, and how a long sweep is progressing.

Open it from the left sidebar under **Data / Logs**, or by clicking any of the background-process labels in the **status bar** (each opens this tool at the matching tab).

## What it shows

One tab per kind of background work:

- **ESI Activity Log** — recent ESI calls the app has made.
- **ESI limits** — how close the app is to ESI's limits, and what it is doing to stay under them (see [ESI limits](#esi-limits)).
- **ESI Call Schedule** — what's due next, split into **Character / Corporation** polling and **Market Refresh**, so you can see when each endpoint will next run.
- **Price History** — per-region sweep progress: how many items are refreshed versus queued, and whether a sweep is currently running.
- **Contract Items**, **LP Store**, **Killmails**, **Intel**, **Alarms** — progress and recent activity for each of those areas. The **Killmails** tab shows [zKillboard](../zkillboard.md) import: its scope, how far the daily dumps have been imported, and a row for each stage — from fetching kill mail details to posting.
- **Order Fulfilment** — how the app is matching your stock, jobs and contracts against open [store](../stores/index.md) and tracked orders.

The **status bar** along the bottom of the app carries a live progress label for each of these, updated about once a second whatever tool you're on; clicking one jumps straight to its tab here.

## ESI limits

ESI allows about 100 failed calls a minute for everything on your internet connection — other programs and computers included — and refuses every call (error 420) once they are spent. Some routes, such as market orders and sovereignty, also have an allowance of their own, a **rate-limit group**. EVE Console slows its own background work to stay under both. Anything you do yourself goes straight through.

The **ESI limits** tab shows:

- **Error budget** — errors left of the allowance and when the window resets, and what was spent this window: how much by this app, and how much by something else on the same connection.
- The **counts** — calls and errors in the last minute, errors in the last hour, and refusals since the app started, for the error limit (420) and for rate limits (429).
- **Governor** — what the app is doing about it (below).
- **Rate-limit groups** — each group ESI has answered for, with its **Limit** (for example *150 per 15 min*), how much is **Left**, how many calls were **Refused**, its **State** (**Paced**, or **Refused until** a time) and its **Routes**.
- **Errors by route** — failed calls by ESI route and status, in the **Last minute**, the **Last hour** and **Since start**, with the time of the **Last** one.

### How background work is slowed

| Errors left | Background work |
| --- | --- |
| 70 or more | Full speed. |
| Under 70 | Calls spaced out. |
| Under 50 | One call at a time. |
| Under 20 | Waits for the window to reset. |

A rate-limit group running low — under a fifth of its allowance — is paced at the rate it refills. The governor goes by what ESI says is left, not by the app's own count, so errors spent by another program on the same connection slow EVE Console down too. Each change of level is written to the [Error Log](error-log.md), with what is left, who spent it and the routes that spent the most.

While the governor holds work back, **▲ ESI slowed** shows in the title bar beside the Tranquility status. Hover it for the governor's state and the error budget; click it to open this tab.

## Notes

- This is a read-only monitor — it reports on the background work, it doesn't change what runs. The polling intervals themselves are set under **Settings ▸ Timers**.
- In a multi-client [PostgreSQL](../storage-postgresql.md) setup the background work runs on whichever client holds the worker lease; the title bar says which one, and this view reflects that client's activity. See [Background processing](../background-processing.md) for how that lease and the headless worker work.
- For browsing the *data* the polling has stored (rather than the schedule), use the [ESI Explorer](esi-explorer.md); for the app's own error log, see [Error Log](error-log.md).
