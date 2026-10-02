# Storage & PostgreSQL

EVE Console keeps everything it knows in a database. By default that's a single **SQLite** file on your machine, and nothing you do is required to keep it that way. From 0.9.13 you can instead point the app at a **PostgreSQL** server — which is what lets several clients, on several machines, share one set of data, and what makes the [background worker](background-processing.md) able to run on its own.

!!! info "Opt-in — nothing moves on its own"

    Existing installations keep opening the same SQLite file they always have. You switch engines deliberately, in Settings, and the app offers to copy your existing data across before anything changes.

## SQLite vs. PostgreSQL

| | **SQLite** (default) | **PostgreSQL** |
|---|---|---|
| Setup | none — a local file | you run (or rent) a server |
| Data location | `EveConsole.db` on this machine | on the server |
| Multiple clients | one at a time (the file is held exclusively) | many at once, sharing one dataset |
| Headless [background worker](background-processing.md) | not alongside a desktop client on the same machine | yes — that's the point |
| Backups | file copy / built-in backup | `pg_dump` (built in) |

If you only ever run one client on one machine, SQLite is the simpler choice and there's no reason to change. Reach for PostgreSQL when you want more than one client on the same data, or a background process that keeps polling after the app is closed.

## What you need

A PostgreSQL server EVE Console can reach, and a database it can create its tables in. The simplest arrangement is a database owned by the connecting user, which grants everything needed without any further permissions:

```sql
CREATE DATABASE eveconsole OWNER myuser;
```

The server can be on the same machine, on your LAN, or anywhere you can reach it over the network.

## Switching to PostgreSQL

Open **Settings** (the **⚙** gear, top-right) ▸ **Database**.

1. Under **Database Type**, choose **PostgreSQL**.
2. In the **PostgreSQL Server** panel, fill in **Host**, **Port**, **Database**, **Username** and **Password**.
3. Click **Test Connection**. The app connects and reports what it found.
4. If the server answers and you still have a SQLite database to bring over, a copy offer appears:
    - **Bring your existing data across** — the destination is empty; your current data is copied in.
    - **Replace what is on the server** — the destination already holds tables; the panel turns red, because the copy **erases first**. Read the message before you confirm.
5. Click **Save and Restart**. Unlike the rest of Settings, which saves as you go, the engine choice waits for this button, because it takes effect only on a restart. The title bar then shows which database is open.

!!! warning "The copy is one-off, and the confirmation matters"

    Copying is a snapshot taken when you click, not ongoing replication. And copying into a database that already holds data **overwrites it** — the app says so and turns the panel red first, but there is no undo once you confirm.

### Where the password is stored

The connection password is **not** written into `config.json`. It's kept in your operating system's secure store (the Windows credential store / a Linux login keyring), which is per-user and per-login-session. Settings shows a short line noting this next to the password field.

!!! note "Headless workers can't read the keyring"

    Because the saved password lives behind a login session, a [background worker](background-processing.md) running as a service has no way to read it. For those, supply the connection string through an environment variable instead — see [Background processing](background-processing.md) and [Running on Linux](running-on-linux.md).

## Backups

Backups and restores work on both engines, from **Settings ▸ Database**:

- On **SQLite**, a backup is a copy of the database file.
- On **PostgreSQL**, backups and restores run through **`pg_dump`** / `pg_restore`, which ship with the app.

You can enable scheduled backups, choose an interval, set how many to keep, and take a manual backup on demand. The storage breakdown (what's taking up space) works the same way on both engines.

## Data retention

**Settings ▸ Data Retention** sets how long EVE Console keeps data it can afford to forget. Each kind of data has its own rule: tick **Purge … older than**, set the number of days, and the rule runs once a day. **Purge Now** runs it straight away, and each rule shows when it last ran.

Only **Agent Activity** is on by default. Every other rule is off until you turn it on.

| Rule | Removes | Default | Shortest |
| --- | --- | --- | --- |
| **Error Log** | entries in the [Error Log](tools/error-log.md) | 30 days | 7 days |
| **Kill Mails ▸ Characters / Corps** | kills and losses of your own characters and corporations | 365 days | 30 days |
| **Kill Mails ▸ Others** | everyone else's kills | 7 days | 7 days |
| **Price History** | daily market history, and the price snapshots built from it | 90 days | 30 days |
| **Game Log** | parsed game-log events | 365 days | 30 days |
| **Chat Messages** | stored chat messages (intel sightings already parsed are kept) | 90 days | 30 days |
| **Agent Activity** | the record of past [AI Agent](ai-agent-eden.md) exchanges, which the usage and cost figures are built from | 90 days | 7 days |

### Kill mails

Kill mails are usually the largest thing in the database, so these two rules are the ones that free the most space. A purge removes the kill and everything attached to it: attackers, items, references and zKillboard flags.

- **Characters / Corps** — a kill counts as yours when one of your characters, or any corporation you have added, is the victim or among the attackers. That includes every corporation you have added, not only the ones marked personal, and it doesn't matter whether its token still works.
- **Others** — everything else: the [zKillboard](zkillboard.md) feed and fights you only watched. On a database that captures all kills, this is nearly all of them.

The two windows let you keep your own history for a year while keeping only a week of everyone else's.

!!! warning "Purged kills are gone"

    To get deleted kills back you have to fetch them again from ESI or zKillboard, and ESI only serves recent ones.

If you had the older single kill-mail rule turned on, both rules start from its setting and window.

### Game and chat logs

Purging game-log events or chat messages leaves the `.log` files on disk alone. As long as those files exist, you can load the data again with **Import Past Logs** or **Import Past Chat** — see [Logs & Map Data](logs-and-map-data.md).

!!! note "The file doesn't shrink by itself"

    Purging removes rows, but SQLite reuses the freed space rather than giving it back, so the file only gets smaller after **Settings ▸ Database ▸ Shrink Database**. The **Storage Breakdown** on the same tab shows where the space went.

## Notes for the SQL-minded

Moving from SQLite to PostgreSQL meant reconciling roughly sixty places where the two dialects disagree — `LIKE` is case-sensitive on PostgreSQL, booleans aren't integers, `COUNT` returns `bigint`, dates aren't strings, and `REAL` is 32-bit (which had been quietly truncating large ISK figures on the way in). This is all handled inside the app; it's noted here only so that, if you inspect the database directly, you know the schema is written to satisfy PostgreSQL's stricter type checking.

---

*Postgres, PostgreSQL and the Slonik Logo are trademarks or registered trademarks of the PostgreSQL Community Association of Canada, and used with their permission.*
