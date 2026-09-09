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
- Configuration: the same `EveConsole` directory.

This is per-user, so the account that runs the app is the account whose data you see — worth remembering when you set up a service.

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

The worker handles **`SIGTERM`** itself and releases its work lease on the way out, so another client (or a restart) can pick the work up cleanly — let it stop gracefully rather than killing it. See [Background processing](background-processing.md) for how the lease and the client/worker hand-off work.

## Building from source on Linux

The same steps as anywhere — clone, restore, run — using the [.NET 9 SDK](https://dotnet.microsoft.com/download/dotnet/9.0):

```bash
git clone https://github.com/kernoeve/EveConsole.git
cd EveConsole
dotnet run
```
