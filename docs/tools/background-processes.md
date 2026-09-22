# Background Processes

A live monitor for the work EVE Console does on a timer — ESI polling, market pricing, contracts, killmails, LP-store catalogues, alarms and order fulfilment. It's a diagnostic view: somewhere to see what has run, what's due next, and how a long sweep is progressing.

Open it from the left sidebar under **Tools**, or by clicking any of the background-process labels in the **status bar** (each opens this tool at the matching tab).

## What it shows

One tab per kind of background work:

- **ESI Activity Log** — recent ESI calls the app has made.
- **ESI Call Schedule** — what's due next, split into **Character / Corporation** polling and **Market Refresh**, so you can see when each endpoint will next run.
- **Price History** — per-region sweep progress: how many items are refreshed versus queued, and whether a sweep is currently running.
- **Contract Items**, **LP Store**, **Killmails**, **Intel**, **Alarms** — progress and recent activity for each of those areas.
- **Order Fulfilment** — how the app is matching your stock, jobs and contracts against open [store](../stores/index.md) and tracked orders.

The **status bar** along the bottom of the app carries a live progress label for each of these, updated about once a second whatever tool you're on; clicking one jumps straight to its tab here.

## Notes

- This is a read-only monitor — it reports on the background work, it doesn't change what runs. The polling intervals themselves are set under **Settings ▸ Timers**.
- In a multi-client [PostgreSQL](../storage-postgresql.md) setup the background work runs on whichever client holds the worker lease; the title bar says which one, and this view reflects that client's activity. See [Background processing](../background-processing.md) for how that lease and the headless worker work.
- For browsing the *data* the polling has stored (rather than the schedule), use the [ESI Explorer](esi-explorer.md); for the app's own error log, see [Error Log](error-log.md).
