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
5. Save the choice and **restart** EVE Console. The engine choice takes effect on restart — the title bar then shows which database is open.

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

## Notes for the SQL-minded

Moving from SQLite to PostgreSQL meant reconciling roughly sixty places where the two dialects disagree — `LIKE` is case-sensitive on PostgreSQL, booleans aren't integers, `COUNT` returns `bigint`, dates aren't strings, and `REAL` is 32-bit (which had been quietly truncating large ISK figures on the way in). This is all handled inside the app; it's noted here only so that, if you inspect the database directly, you know the schema is written to satisfy PostgreSQL's stricter type checking.

---

*Postgres, PostgreSQL and the Slonik Logo are trademarks or registered trademarks of the PostgreSQL Community Association of Canada, and used with their permission.*
