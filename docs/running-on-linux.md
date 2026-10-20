# Running on Linux

From 0.9.13, EVE Console runs natively on 64-bit Linux, and Linux builds ship alongside the Windows builds with every release. Everything the app needs is bundled, including the .NET runtime.

## Downloads

Both come from the [Releases page](https://github.com/kernoeve/EveConsole/releases/latest):

- **[AppImage — `EveConsole.AppImage`](https://github.com/kernoeve/EveConsole/releases/latest/download/EveConsole.AppImage)** — a single self-contained file. Make it executable and run it:

    ```bash
    chmod +x EveConsole.AppImage
    ./EveConsole.AppImage
    ```

    Like the Windows builds, the AppImage **keeps itself up to date automatically**.

- **[Tarball — `EveConsole-linux-x64.tar.gz`](https://github.com/kernoeve/EveConsole/releases/latest/download/EveConsole-linux-x64.tar.gz)** — extract anywhere and run the binary:

    ```bash
    tar -xzf EveConsole-linux-x64.tar.gz -C ~/eveconsole
    ~/eveconsole/EveConsole
    ```

    The tarball does **not** self-update; download a newer tarball to upgrade. It's the layout to use for a service (see below).

## The one dependency: `vlc`

The only thing the build can't carry is your distribution's **`vlc`** package, which the app uses for **alarm sounds** and the **AI agent's speech** (text-to-speech). Everything else works without it. Install it from your package manager if you want audio:

```bash
# Debian / Ubuntu
sudo apt install vlc
# Fedora
sudo dnf install vlc
# Arch
sudo pacman -S vlc
```

## Where data lives

Your data and configuration live under your home directory:

- Database (SQLite): `~/.local/share/EveConsole/EveConsole.db`
- Configuration (`config.json`), backups and profiles: the same `EveConsole` directory.

This is per-user, so the account that runs the app is the account whose data you see — worth remembering when you set up a service. The data never shares a folder with the AppImage or the tarball, so replacing either leaves it alone.

## Chinese, Japanese and Korean

EVE Console can be shown in [eight languages](languages.md). For Chinese, Japanese and Korean it uses your system's **Noto Sans CJK** fonts, which most desktops already have. If that text shows as empty boxes, install them:

```bash
# Debian / Ubuntu
sudo apt install fonts-noto-cjk
# Fedora
sudo dnf install google-noto-sans-cjk-fonts
# Arch
sudo pacman -S noto-fonts-cjk
```

Package names can differ between releases; search your package manager for "noto cjk" if one of these isn't found.

## Running headless as a service

On Linux the [background worker](background-processing.md) can run with no window as a **systemd user unit**, so ESI polling, imports, alarms, the scheduler and backups keep going after you close the desktop client — or on a machine that never opens one at all.

!!! warning "Headless on Linux means PostgreSQL"

    A SQLite file can only be held by one process, so a worker running as a service would lock the desktop client out entirely. Run the worker headless only when the app is on [PostgreSQL](storage-postgresql.md); the app tells you as much on stdout if you try it on SQLite.

A unit file ships in the source tree at `packaging/eveconsole-worker.service`. The essentials:

- **Run it as a real login user**, not `root` or a system account — the data directory is under that user's home, and it's that user's keyring a UI-saved password would land in.
- **Supply the connection string in the environment**, not from saved settings — a daemon has no login session and can't open the keyring:

    ```bash
    sudo install -m 600 /dev/null /etc/eveconsole.env
    echo 'EVECONSOLE_DB_CONNECTION=Host=db.example;Database=eveconsole;Username=eveconsole;Password=…' \
      | sudo tee /etc/eveconsole.env >/dev/null
    ```

- **Point `ExecStart` at the tarball binary** with `--headless`:

    ```ini
    ExecStart=/opt/eveconsole/EveConsole --headless
    ```

    To run the **AppImage** as a service instead, use its extract-and-run flag — a system service often can't mount FUSE, and without this the AppImage exits before it reaches any of the app's own code:

    ```ini
    ExecStart=/opt/eveconsole/EveConsole.AppImage --appimage-extract-and-run --headless
    ```

    Keep the filename stable across upgrades, or the unit will keep starting the old build.

Install and manage it like any user/system unit:

```bash
sudo cp packaging/eveconsole-worker.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable --now eveconsole-worker
journalctl -u eveconsole-worker -f
```

A worker on an older version than the database stops at start and logs whether a release that can open it is out; see [Version safety](background-processing.md#version-safety).

The worker handles **`SIGTERM`** itself and releases its work lease on the way out, so another client (or a restart) can pick the work up cleanly — let it stop gracefully rather than killing it. See [Background processing](background-processing.md) for how the lease and the client/worker hand-off work.

## Running in Docker

If you'd rather self-host the worker in a container, the source tree ships a Docker setup in [`packaging/docker`](https://github.com/kernoeve/EveConsole/tree/main/packaging/docker): a `Dockerfile` that builds an image from the release tarball, and a `docker-compose.yml` that runs that image beside the **PostgreSQL** server it needs (`postgres:17`). The worker runs on a headless platform, so it needs no display, no keyring and no `vlc` in the container. The image runs as an unprivileged user, keeps its files in `/data`, and carries `pg_dump` 17 for the built-in backups.

```bash
git clone https://github.com/kernoeve/EveConsole.git
cd EveConsole/packaging/docker
cp .env.example .env        # set POSTGRES_PASSWORD, and EVECONSOLE_VERSION to your clients' version
docker compose up -d --build
docker compose logs -f worker
```

On its first start the worker creates the tables in the empty database. The log opens with the same four lines as any headless start: the version, the database, whether this worker holds the lease, and which logs it reads.

`.env` holds four settings:

| Setting | What it is |
| --- | --- |
| `POSTGRES_PASSWORD` | The database password, for the server and the worker. Desktop clients sign in as user `eveconsole` with it. Required. |
| `POSTGRES_PORT` | The port desktop clients connect to on this machine. `5432` by default. |
| `EVECONSOLE_VERSION` | The release to run, without the leading `v` — for example `0.9.17`. `latest` (the default) takes the newest release each time the image is rebuilt. |
| `TZ` | The time zone of the worker's log timestamps. `UTC` by default. |

`.env` holds the database password: keep it out of version control and readable by you alone.

What to know:

- **Build the image at the version your desktop clients run.** Set `EVECONSOLE_VERSION` in `.env`. A worker newer than your clients upgrades the database, and the clients then refuse to open it until they're updated too. See [Version safety](background-processing.md#version-safety). To upgrade, change the version and run `docker compose up -d --build` again. The version must be 0.9.17 or later: before that, `--headless` on Linux needed a display, and couldn't start in a container.
- **Point your desktop clients at the same server.** In each one, open **Settings ▸ Database**, choose **PostgreSQL**, and enter this machine's address, the port from `.env`, database `eveconsole`, user `eveconsole` and your password. See [Storage & PostgreSQL](storage-postgresql.md#switching-to-postgresql).
- **Bringing an existing SQLite database across?** Copy it before the worker's first start, while the server is still empty. Start only the database with `docker compose up -d db`, copy your data across from the desktop client (**Bring your existing data across** in **Settings ▸ Database**), and then start everything with `docker compose up -d --build`. Once the worker has started, the server already holds tables, and a copy would have to erase them first.
- **Add characters and corporations from a desktop client.** Signing in to EVE needs a browser, and the container has none. Once a character is added, the worker polls it.
- **The database port is published** so clients on other machines can reach it. The database holds your characters' refresh tokens, so keep that port on your own network. If the only client is on the same machine, change the mapping to `127.0.0.1:5432:5432`.
- **Data lives in two volumes:** `db` for PostgreSQL, and `data` for the worker's own files (config, the SDE cache, pictures and its `pg_dump` backups).
- **Game and chat logs** are imported only if you mount them. Uncomment the log volumes and the matching `EVECONSOLE_GAMELOG_DIRS` / `EVECONSOLE_CHATLOG_DIRS` lines. Leave them out on a host with no EVE client; desktop clients keep importing their own logs.
- **`docker compose stop` is a clean stop.** The worker handles `SIGTERM`, releases its lease and exits, so a desktop client takes over the work on its next tick.

## Building from source on Linux

The same steps as anywhere — clone, restore, run — using the [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0):

```bash
git clone https://github.com/kernoeve/EveConsole.git
cd EveConsole
dotnet run
```
