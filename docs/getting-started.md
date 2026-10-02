# Getting Started

## Requirements

- **Windows** 10 or 11, **or** a modern 64-bit **Linux** desktop.
- An EVE Online account (you'll authorize characters via EVE's official Single Sign-On).

Everything the app needs is bundled, including the .NET runtime. On Linux the one external dependency is your distribution's **`vlc`** package, used for alarm sounds and the AI agent's speech — see **[Running on Linux](running-on-linux.md)** for details, headless setups, and file locations.

## Download & install

Grab the latest build from the project's [Releases page](https://github.com/kernoeve/EveConsole/releases/latest). The links below always point at the **newest** release, so they don't go stale.

### Windows

- **[Installer — `EveConsole-win-Setup.exe`](https://github.com/kernoeve/EveConsole/releases/latest/download/EveConsole-win-Setup.exe)** — installs EVE Console (adds Start-menu and uninstall entries), then launch it.
- **[Portable — `EveConsole-win-Portable.zip`](https://github.com/kernoeve/EveConsole/releases/latest/download/EveConsole-win-Portable.zip)** — no install; extract it anywhere and run `EveConsole.exe`.

Both are the same app and **both keep themselves up to date automatically** (see below), so which you choose is a matter of preference — the installer if you'd like it integrated into Windows, the portable ZIP if you'd rather keep everything in a single folder you can move or delete.

### Linux

- **[AppImage — `EveConsole.AppImage`](https://github.com/kernoeve/EveConsole/releases/latest/download/EveConsole.AppImage)** — a single self-contained file. Mark it executable (`chmod +x EveConsole.AppImage`) and run it. Like the Windows builds, the AppImage **keeps itself up to date automatically**.
- **[Tarball — `EveConsole-linux-x64.tar.gz`](https://github.com/kernoeve/EveConsole/releases/latest/download/EveConsole-linux-x64.tar.gz)** — extract anywhere and run `./EveConsole`. The tarball does not self-update; grab a newer tarball to upgrade.

See **[Running on Linux](running-on-linux.md)** for the `vlc` dependency, running headless as a systemd service, and where data lives.

Your data is stored locally — on **Windows** at `%LOCALAPPDATA%\EVE Console Data\EveConsole.db`, on **Linux** at `~/.local/share/EveConsole/EveConsole.db`. By default nothing leaves your machine; the app talks only to CCP's ESI API to refresh your data. If you'd rather keep the data on a shared server, you can point it at your own **[PostgreSQL](storage-postgresql.md)** instead.

### Where your data lives on Windows

The installer puts the program in `%LOCALAPPDATA%\EveConsole` and treats that folder as its own: installing again over it, or uninstalling, replaces or deletes it. So EVE Console keeps your settings, database, backups and profiles **beside** it, in `%LOCALAPPDATA%\EVE Console Data`.

Older versions kept everything in the install folder. The first time an installed copy starts on the new version, it moves your data across before it opens anything:

- Everything that isn't part of the program goes — `config.json`, the database, backups, profiles, downloaded voice models and caches.
- Settings that pointed inside the old folder, such as a profile's own database, are updated to the new one. A database you moved somewhere else yourself stays exactly where it is.
- A note, **Your EVE Console data has moved.txt**, is left in the old folder saying where the data went.
- It's all or nothing. If a file is in use — usually because another copy of EVE Console is running — nothing moves, the app uses the old folder for that run, the reason goes in the [Error Log](tools/error-log.md), and the next start tries again.

The portable ZIP and builds from source never move anything: they use whichever folder holds your data. On **Linux** nothing changes, because the data never shared a folder with the AppImage.

!!! warning "Coming from an older version? Update from inside the app"

    Until the move has happened, your data is still in the install folder, and running the installer (`EveConsole-win-Setup.exe`) over an older install deletes that folder with everything in it. Take the update the app offers (or **Settings ▸ Updates ▸ Update Now**), let it restart once, and only then reinstall if you need to.

!!! tip "Reinstalling is safe once the data has moved"

    After the new version has started once, running the installer again or uninstalling leaves your data alone. To remove everything after uninstalling, delete `%LOCALAPPDATA%\EVE Console Data` yourself.

## Staying up to date

You normally won't need to download the app again. Whether you installed it or run the portable build, EVE Console **checks for updates on startup and once an hour**, and when a new version is available it **prompts you inside the app** — accepting downloads the update and restarts to apply it. Declining won't nag you again until the *next* version.

You can manage this under **Settings** (the **⚙** gear button, top-right) → **Updates**:

- **Automatically check for updates** — on by default; untick to only check manually.
- **Current version** / **Latest version** — what you're running vs. what's available.
- **Check Now** — check on demand.
- **Update Now** — appears when an update is available; downloads and restarts.

!!! note

    Automatic updates apply to the self-managing released builds — the Windows installer and portable ZIP, and the Linux **AppImage**. The Linux **tarball** and any build you run **from source** can't self-update — the Updates tab shows *"n/a — not an installed build,"* and you update those by downloading a newer build (or pulling and rebuilding).

An update restarts EVE Console with the same command-line options it was started with, so a `--profile` copy comes back in its profile.

### When this copy is older than the database

A new version upgrades the database the first time it opens it. That usually matters when several clients share one [PostgreSQL](storage-postgresql.md) database: the first to update upgrades it for all of them. A copy still on the older version can't safely open an upgraded database, so instead of starting it shows **This build is older than the database** and checks for an update there and then:

- If a release that can open the database is out, it says which version and offers **Update and restart**. The update downloads with a progress line, installs, and restarts EVE Console on the same database.
- Otherwise it says why not — this copy wasn't set up by the installer (the tarball or a source build), the check failed, or the version the database needs hasn't been released yet (the database was opened by a development build). **Releases page** opens the download page.

**Close** leaves the app without changing anything. A copy started with `--tray` shows the same dialog; a [headless worker](background-processing.md#version-safety) writes to its log whether an update exists, and stops.

## Building from source

If you'd rather build it yourself (or want to contribute), you'll also need the
[.NET 9 SDK](https://dotnet.microsoft.com/download/dotnet/9.0):

```powershell
git clone https://github.com/kernoeve/EveConsole.git
cd EveConsole
dotnet restore
dotnet run
```

A `dotnet run` build doesn't self-update — `git pull` and rebuild to get newer changes.

!!! tip "Keep a development build away from your real data"

    Start the app with `--profile <name>` (for example `dotnet run -- --profile dev`)
    to run a completely separate copy — its own config, database and caches — under
    `%LOCALAPPDATA%\EVE Console Data\Profiles\<name>` (`~/.local/share/EveConsole/Profiles/<name>`
    on Linux), or give a folder path instead of a name. It starts empty, like a fresh
    install, and runs alongside your normal copy. The window title shows the profile
    name, and **Settings ▸ Database** says which folder is in use.

### Building a self-updating package

If you want a **packaged, self-updating build from your own checkout** — the same
kind of installer/portable the downloads produce — run the packager the release
pipeline uses ([Velopack](https://velopack.io/)) yourself:

1. Install the Velopack CLI (pinned to the version CI uses):

    ```powershell
    dotnet tool install -g vpk --version 1.2.0
    ```

2. Publish a self-contained Windows build. Use a version number — matching the
   latest release (or the `VERSION` file) is a good default:

    ```powershell
    dotnet publish EveConsole.csproj -c Release -r win-x64 --self-contained true -p:Version=0.9.5 -o publish
    ```

3. Pack it with Velopack. Keep `--packId EveConsole` so the updater recognizes the
   project's official releases:

    ```powershell
    vpk pack --packId EveConsole --packTitle "EVE Console" --packVersion 0.9.5 --packDir publish --mainExe EveConsole.exe
    ```

The installer (`EveConsole-win-Setup.exe`) and portable ZIP appear in the `Releases`
folder. Run either and you have a Velopack-managed build that self-updates exactly
like an official download.

!!! warning "A self-updating source build tracks the *official* releases"

    Because it checks the project's GitHub releases, a locally-packed build will
    **update itself to the next official release**, replacing your custom build. That's
    fine if you just want the latest source as a self-updating app, but your local
    changes get overwritten when a new release ships. For ongoing development, stick
    with `dotnet run` and `git pull`.

## First launch

The first time you launch EVE Console, it starts downloading the EVE game data it
needs (the Static Data Export and Hoboleaks data) **in the background**. A short
**Welcome** dialog explains this — item lookups, market pricing, and industry tools
fill in over a few minutes as the download completes, and you can watch progress on
the **SDE** tab in Settings. Once it finishes, restart EVE Console: some tools load
their reference data when they first open, and a restart makes sure they all see it.

Click **Get Started** on that dialog and the **Settings** window opens automatically
on the **ESI Tokens** tab. That's where you authorize your characters and
corporations — click **Add** under **Characters** to log in your first character through EVE's
Single Sign-On, as described next.

You can reopen ESI Tokens any time from **Settings** (the **⚙** gear button,
top-right); it's the first tab.

## Managing ESI tokens (characters & corporations)

Everything the app knows comes from ESI tokens you authorize. Manage them under
**Settings ▸ ESI Tokens**, which has a **Characters** list and a **Corporations**
list, each with **Add**, **Update**, and **Remove** buttons.

### Adding a character

1. Under **Characters**, click **Add**.
2. Pick which **scopes** (permissions) to grant — they're grouped by category. Only
   the data you grant can be pulled.
3. Continue to EVE's SSO page in your browser and authorize the character.
4. The character appears in the list with its status and granted scopes. Selecting
   it shows when it was last authenticated and exactly which scopes it has.

**Update** re-runs the SSO flow for the selected character — use it to add or change
scopes, or to refresh an expired token. **Remove** deletes that character's token
and data.

### Adding a corporation

1. Under **Corporations**, click **Add**.
2. Pick the corporation scopes to grant.
3. In the browser, **log in as a character who holds the required corporation roles**
   (Director / Accountant) — corporation ESI data isn't available without them. The
   app uses that character only to resolve and authorize the corp; the corp's token
   is stored on the corporation itself.
4. The corporation appears in the list (ticker, name, status).

### Personal corporations

A corporation you own is a **personal corporation** — its activity and assets should
count as *yours*. Select a corp and tick **Personal Corporation** to mark it (a gold
dot flags personal corps in the list).

!!! info "What 'personal' changes"

    Personal corps count toward your **individual net worth**, and their activity and
    assets are treated as part of your own. Alliance or employer corporations — ones
    you've added for visibility but don't own — are treated as separate entities and
    are kept out of your personal totals.

## Characters tab

**Settings ▸ Characters**, right after **ESI Tokens**, lists every authorised
character automatically and says what each is used for:

- **Slots used for** — **Mfg** (manufacturing), **Rxn** (reactions) and **Sci**
  (science: copying, research, invention). All three start ticked; clear the ones a
  character shouldn't be given, which is how you keep an alt out of that work. Jobs
  go to the least capable character who can run them, keeping your high-skill
  characters free for the work only they can do.
- **Free / total** — the character's free and total job slots.
- **Skill queue** — ticked means the skill queue should be kept running. Clear it for
  an alt whose queue is empty on purpose, and it raises no [Overview](tools/overview.md)
  alert or [Worklist](tools/worklist.md) item.
- **PI** — ticked (the default) means the character does Planetary Industry. Clear
  it, and the character is left out of the PI tool, gets no PI alerts or Worklist
  tasks, and its colonies aren't read.

Changes save as you make them.

## Settings save as you go

There are no Save buttons to remember in **Settings**. A tick, a pick from a list, a
number or a change to a list saves at once. Text saves when you pause typing, when
you leave the box, and when you close the window. On several tabs a short status
line confirms each save. A value that can't be right — a market **Location ID** that
isn't a number, say — is shown as an error and not saved.

The buttons that remain do something beyond saving: **Test Connection**, **Test
This Model**, **Refresh This**, **Recalculate Build Costs** and the like. The one
exception is **Settings ▸ Database**, where switching between SQLite and PostgreSQL
still takes **Save and Restart**, because it only takes effect on a restart (see
[Storage & PostgreSQL](storage-postgresql.md)).

## Language

EVE Console is available in English, German, Spanish, French, Japanese, Korean,
Russian and Simplified Chinese. Pick one under **Settings ▸ Other ▸ Language**; it
takes effect from the next start, and **Restart now** switches straight away.
**System default** follows your computer's language. See **[Languages](languages.md)**
for what is translated and what stays in English.

## Sizing the interface

If the app is too small or too large on your display, set a **UI scale** between
**50 % and 200 %** (in 25 % steps). It's at the right-hand end of the **status bar**,
and also under **Settings ▸ Other**. The scale applies to every window, dialog and
popup at once, and is remembered per machine.

## Tabs, split view and separate windows

Each tool you open from the navigation on the left opens as a tab. You can arrange
the tabs to see several tools at once.

### Two tools side by side

1. Drag a tab by its title.
2. Drop it on the right half of the window, where **Drop here to see two tools side
   by side** appears.

The window splits into two halves, each with its own row of tabs. Drag tabs along a
row to reorder them, or across to the other half. The half you last clicked is the
one new tools open in; the other half's selected tab is shown dimmed. When the last
tab leaves either half, the window goes back to one.

### A tool in its own window

Drag a tab out of the main window and let go, or drag it down into the tool's own
area until **Release to open in its own window** appears — the way to do it when the
window is maximised. The tool opens in a window of its own, with its own row of
tabs. You can drag more tabs into it, and split it in two the same way.

To put a tool back, drag its tab onto the main window. A window left with no
tabs closes; closing a window closes the tools in it. Every tool except the
**Overview** can leave the main window.

### Closing tabs

Right-click a tab for **Close**, **Close other tabs** and **Close all tabs**. In a
split window there are also **Close other tabs on this side** and **Close all tabs
on this side**. The Overview always stays open.

### More room for tools

- Click the **☰** button at the left of the title bar to hide or show the navigation.
- Click a navigation heading to fold its section away. A folded section still marks
  when one of its tools is open.

Both are remembered on this computer. The tabs and windows themselves aren't: each
start opens on the Overview.

## How data stays fresh

While EVE Console is running it performs background ESI pulls on a schedule. Most
screens update automatically as new data arrives, so you can leave it open in the
background. Some data (like market price history) is cached and refreshed on longer
intervals to respect ESI limits.

## Recommended next steps

Most tools depend on a little configuration first:

1. **[Configure a market](configuring-markets.md)** so the app knows where prices come from.
2. **[Set up an industry park](industry-parks.md)** so build costs and the Production Calculator are accurate.
3. Optionally, **[set up the AI agent](ai-agent-eden.md)**.

<!--
  SCREENSHOT SLOTS (add files to docs/images/, then uncomment):

  Welcome dialog:
  ![Welcome dialog](images/welcome.png)

  ESI Tokens settings tab:
  ![ESI Tokens](images/esi-tokens.png)
-->
