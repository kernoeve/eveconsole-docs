# Background processing

Everything EVE Console does on a timer — ESI polling, market pricing, contracts, zKillboard, alarms, the [Scheduler](tools/scheduler.md), data retention and backups — is the *background work*. From 0.9.13 that work can run **without a desktop window**, so it keeps going after you close the app, or on a machine that never opens one.

!!! info "This needs PostgreSQL"

    Detached background work is only possible when the app is on [PostgreSQL](storage-postgresql.md). A SQLite file can be held by only one process, so a worker and a desktop client can't share it — the whole point of this mode is several clients on one server, one of which does the work.

## One worker, many readers

When several clients share a PostgreSQL database, exactly **one** of them takes a *lease* and does the background work; the others read, and show what it's doing. The lease is what stops two machines duplicating the same polling.

- A **desktop client** takes the lease if no one else holds it, and does the work in the background as usual.
- A **headless worker** waits if a desktop client already holds the lease, and takes over the moment that client exits.
- The title bar shows **which client is doing the background work**, so you can always tell.
- The worker pushes its **call logs, polling status and alarms** out to the other clients, and each client can **mute** those independently.

When a worker stops, it releases its lease on the way out, so the next client picks the work up on its next tick rather than waiting for the server to notice a dropped connection.

## Watching the background work

You don't have to run headless to see what the background work is doing. The **Background Processes** view (a tool tab, opened from the left sidebar or by clicking a status-bar label) shows each kind of work live, on its own tab:

- **ESI Activity Log** and **ESI Call Schedule** — recent calls and what's due next, by character/corporation and by market refresh.
- **Price History**, **Contract Items**, **LP Store**, **Killmails**, **Intel**, **Alarms**, and **Order Fulfilment** — per-area progress: what's been refreshed, what's queued, and whether a sweep is running.

Along the bottom, the **status bar** carries a live progress label for each background process rather than one generic "polling" line; click a label to jump straight to its tab.

## Running headless

The worker runs with no UI when started with `--headless`. It's the same worker in every case, so the mode never means two different things.

### Linux — systemd

Run it as a **systemd user unit** from the tarball or AppImage. The full walkthrough — the unit file, the environment file for the connection string, the `vlc` dependency and the AppImage's extract-and-run caveat — is in **[Running on Linux](running-on-linux.md)**.

### Windows — a service

On Windows the worker installs as a **Windows service**, managed from **Settings ▸ Polling**:

- **Install service** / **Remove service** — installs or removes the background service. This needs elevation; Windows prompts for it.
- **Repoint** — updates the service to the current build's location after an upgrade.

A service runs as **LocalSystem** and has no user session, so it reads its database from a machine-scoped configuration rather than your per-user profile — the app handles this when you install it from Settings.

### A tray icon for the service

A Windows service can't draw anything on screen. If you want a visible sign that the worker is running in your own session, start the app with `--tray` for a **notification-area icon and nothing else**. There's a checkbox for it under **Settings ▸ Polling**.

## Supplying the connection string to a service

A background service has no login session, so it can't read the connection password saved through the desktop app (that lives in a per-user secure store). For headless/service use, supply the connection string through the environment instead:

```
EVECONSOLE_DB_CONNECTION=Host=…;Database=…;Username=…;Password=…
```

On Linux this goes in the unit's environment file; on Windows it's a machine or service environment variable. See [Running on Linux](running-on-linux.md) for the Linux specifics.

## Version safety

A worker checks its build against the database schema and **exits deliberately** if they don't match — the schema belongs to a different build, and running the wrong one against it could corrupt data. On Linux the shipped unit restarts `on-failure` but not on this exit, so a clear one-line failure doesn't turn into a restart loop. Keep the worker and your desktop clients on the **same version**.
