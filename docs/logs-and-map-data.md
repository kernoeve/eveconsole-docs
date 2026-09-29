# Logs & Map Data

EVE Console can read the log files your EVE client writes, and it collects hourly statistics for the whole cluster. Both are set up in **Settings** — click the **⚙** gear button in the top-right of the title bar — on three tabs:

- **Game Logs** — combat, mining, bounties, jumps and undocking from EVE's game logs.
- **Chat Logs** — messages from chat channels you choose, including intel channels.
- **Map Data** — jumps, kills, sovereignty, industry indices, faction warfare and incursions for the [Universe Map](tools/universe-map.md).

What the logs hold is browsed in the **Game Log** and **Chat Log** viewers — see [Game & Chat Logs](tools/logs.md).

## Game Logs

Game log import is **on by default**. It reads EVE's own game logs and stores what it finds — combat, mining, bounties, jumps, undocking — so other tools can query it.

Logs are opened read-only. Nothing is ever written back, and nothing is sent to the game client.

!!! note "It captures from now on"

    Turning the importer on picks up new activity from that point. Logs EVE had already written are only loaded if you run an import — see [Import Past Logs](#import-past-logs).

### Log Folders

Leave the **Log Folders** list empty and EVE Console finds the local folder by itself: `Documents\EVE\logs\Gamelogs`, including a Documents folder redirected to OneDrive. On Linux it looks in `~/Documents/EVE/logs/Gamelogs`.

**Currently reading** shows the folder(s) actually in use. Each one is marked ✓ when it can be reached and ✗ when it can't. If it says no game log folder was found, add yours by hand.

- **Add** — type a folder into the box and click **Add**.
- **Remove** — removes the selected folder.
- **Detect** — adds the local folder EVE Console found on its own.
- **Open** — opens the selected folder in your file manager.

To read the logs of EVE clients on **other computers**, add a network path such as `\\PC2\eve-logs`. Nothing needs to be installed on the other machines.

!!! tip "Steam and Proton on Linux"

    If you run EVE through Steam and Proton, its logs live inside the game's Proton prefix, not in your own Documents folder. Find the `Gamelogs` folder there and add it with **Add**.

### Import Past Logs

This loads what EVE has already logged. It runs once — after that, new activity is picked up automatically.

1. Set **Import logs from the last (days)**. The default is **30**; **0** means all history.
2. Check the file count below it. Click **Recount** to count again.
3. Click **Start Import**. A progress bar shows how far it has got; **Cancel** stops it.

EVE Console remembers where it stopped reading each file. When it starts again it reads on from there, but only in log files that changed in the last three hours. If the app was closed for longer while you played, run an import to pick up that gap.

### Options

- **Check for new lines every (s)** — how often the importer looks for new lines. The default is **5** seconds; the range is 2–300.
- **Keep lines that no rule recognised** — on by default, and recommended. EVE's log format is undocumented and changes between client versions. Keeping lines the app doesn't understand means missing coverage shows up in your own data instead of going unnoticed.

## Chat Logs

Chat log import is **off by default**. Unlike game logs, chat logs hold what other people wrote, so nothing is stored until you both turn it on **and** tick specific channels.

!!! warning "Private conversations"

    Private conversations appear as channels named **Private Chat (2)**, **Private Chat (3)** and so on. EVE reuses those names for different people over time, so ticking one can capture direct messages with many different players.

To set it up:

1. Tick **Import chat logs**.
2. Check the **Log Folders** list. It works the same way as for game logs: leave it empty to use the local `Chatlogs` folder, or add network paths for other computers.
3. Under **Channels to Store**, click **Discover Channels**. This reads file names only, and can take a moment — the folder often holds tens of thousands of files.
4. Tick the channels to store in the **CHANNEL** column. Only ticked channels are read at all; files for other channels are never opened. **Untick All** clears the selection.
5. Tick **INTEL** for channels that carry intel reports.

### Intel channels

Messages in channels ticked as **INTEL** are parsed into *sightings*: the system, how many were reported, and any pilots named. A "clr" message clears what was standing in that system.

Sightings feed:

- the Intel overlays on the [Universe Map](tools/universe-map.md#intel-from-chat-logs);
- each system's **Intel** tab;
- the **Intel report** alarm in [Alarms](tools/alarms.md#intel-report).

**Parse Stored History** parses the messages already stored for your intel channels. Use it after ticking an intel channel, so the overlays aren't empty until someone posts fresh intel. It works on stored messages only — to load older messages from the log files, run an import first.

### Import Past Chat

As with game logs, turning chat import on only captures new messages.

1. Set **Import chat from the last (days)**. The default is **7**; **0** means all history.
2. Click **Start Import**. Only the channels you ticked are imported. **Cancel** stops it.

## Map Data

Map statistics feed the [Universe Map](tools/universe-map.md) overlays and each system's activity graphs. **Collect map statistics** is **on by default**.

Seven datasets are collected: jumps, kills, sovereignty, sovereignty structures, industry indices, faction warfare and incursions.

ESI only serves the current hour. EVE Console asks it for that about every 10 minutes, and takes all earlier hours from the **EVE Ref** archive. Because the history comes from the archive, closing the app doesn't leave permanent gaps — missing hours can always be fetched later.

- **Backfill days** — how much history the backfill fetches. The default is **7**.
- **Keep hourly detail (days)** — how long hourly rows are kept. The default is **1**, which covers the 24-hour overlays. After that, jumps and kills are totalled per day, and sovereignty, industry and structure data keep one snapshot a day. Industry indices are still refreshed every hour, so the current value stays current.

The first backfill runs by itself the first time the app starts. Map Data overlays stay empty until it has finished.

After that, each start fills in any hours missing from the last three days. If the app was closed for longer, click **Backfill now** to fill the rest.

### History and coverage

- **History** — the backfill's status and a progress bar.
- **Backfill now** — runs the backfill for the number of days set above. Use it after raising **Backfill days** to fetch the extra history.
- **Cancel** — stops a running backfill.
- **Refresh current hour** — asks ESI for the current hour straight away.
- **Coverage** — one line per dataset: how many hourly buckets and days are stored, and the earliest and latest.

!!! note "Several clients on one database"

    Map statistics are collected by the client doing the background work. When several clients share a [PostgreSQL](storage-postgresql.md) database, that is the one holding the lease — see [Background processing](background-processing.md). Game and chat logs are different: each client reads its own log folders.
