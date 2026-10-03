# Logs & Map Data

EVE Console can read the log files your EVE client writes, and it collects hourly statistics for the whole cluster. Both are set up in **Settings** — click the **⚙** gear button in the top-right of the title bar — on three tabs:

- **Game Logs** — combat, mining, bounties, jumps and undocking from EVE's game logs.
- **Chat Logs** — messages from chat channels you choose, including intel channels.
- **Map Data** — jumps, kills, sovereignty, industry indices, faction warfare and incursions for the [Universe Map](tools/universe-map.md), and Thera and Turnur connections from EVE-Scout.

What the logs hold is browsed in the **Game Log** and **Chat Log** viewers — see [Game & Chat Logs](tools/logs.md).

## Game Logs

Game log import is **on by default**. It reads EVE's own game logs and stores what it finds — combat, mining, bounties, jumps, undocking — so other tools can query it. [Alarms](tools/alarms.md) read it too: the **Game log event** check, and **Stopping the ship ends it** on the wake-up call.

Logs are opened read-only. Nothing is ever written back, and nothing is sent to the game client.

!!! note "Client languages"

    The game writes its log in the client's language. Combat (damage and misses, dealt and taken), warp scrambles and disruptions, decloaking, stopping the ship, jumps and undocking are recognised in all eight client languages: English, German, Spanish, French, Japanese, Korean, Russian and Chinese. Other lines, such as mining and bounties, are recognised from an English client only; with **Keep lines that no rule recognised** on, the rest are still stored.

!!! note "It captures from now on"

    Turning the importer on picks up new activity from that point. Logs EVE had already written are only loaded if you run an import — see [Import Past Logs](#import-past-logs).

### Log Folders

This computer's own game log folder is **always read** when EVE Console can find it: `Documents\EVE\logs\Gamelogs`, including a Documents folder redirected to OneDrive. On Linux it looks in `~/Documents/EVE/logs/Gamelogs`. You don't need to add it.

The **Log Folders** list is for folders **in addition** to that one — most often the logs of EVE clients on **other computers**. Add a network path such as `\\PC2\eve-logs`. Nothing needs to be installed on the other machines.

- **Add** — type a folder into the box and click **Add**.
- **Remove** — removes the selected folder.
- **Open** — opens the selected folder in your file manager.

**Currently reading** shows every folder actually in use. This computer's own folder is marked **(this computer)**. Each one is marked ✓ when it can be reached and ✗ when it can't. If it says no game log folder was found, add yours by hand.

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
2. Check the **Log Folders** list. It works the same way as for game logs: this computer's own `Chatlogs` folder is always read, and the folders you add — such as network paths for other computers — are read as well.
3. Under **Channels to Store**, click **Discover Channels**. This reads file names only, from every folder being read, and can take a moment — the folder often holds tens of thousands of files.
4. Tick the channels to store in the **CHANNEL** column. Only ticked channels are read at all; files for other channels are never opened. **Untick All** clears the selection.
5. Tick **INTEL** for channels that carry intel reports.
6. Optionally, fill in **REGIONS** for each intel channel — see [Intel channels](#intel-channels).

### Intel channels

Messages in channels ticked as **INTEL** are parsed into *sightings*: the system, how many were reported, the pilots named, what they fly, and anything else said about the system. A "clr" message clears what was standing in that system.

Sightings feed:

- the live marks and Intel overlays on the [Universe Map](tools/universe-map.md#intel-from-chat-logs);
- each system's **Intel** tab;
- the **Intel report** alarm in [Alarms](tools/alarms.md#intel-report).

Reports of only your own pilots, or of pilots at positive standing, aren't counted as sightings.

**Parse Stored History** parses the messages already stored for your intel channels. Use it after ticking an intel channel, so the overlays aren't empty until someone posts fresh intel. It works on stored messages only — to load older messages from the log files, run an import first.

#### Regions

Intel channels often shorten null-sec system names — "QZ-X" for QZ-X77. Which system a short name means is decided by the regions the channel reports on.

- Leave **REGIONS** empty and they are learned from the systems the channel has reported over the last year. The box then shows what was learned ("Learned: …").
- Type regions, comma-separated, to set them yourself for that channel. Names can be in English or in the interface language. A name that isn't a region is pointed out under the box.

The box saves as you type, and the next intel pass reads it.

#### What the parser reads

- **Systems** — full names, and shortened null-sec names narrowed down by the channel's regions. When that still leaves several, the one the channel has named far more often wins; otherwise none is taken. A zero typed for an O is read as an O, and system names in other client languages are understood. A system right after words such as "left", "from" or "not" isn't taken as where the hostiles are.
- **Ships** — hull names in every client language, common slang ("kiki", "vaga", "inty", "dictors"), plurals and ship classes, and "navy" for a Navy Issue hull.
- **Counts** — numbers tied to ships or people: "3 lokis", "Sabre x2", "+5", "14 man", "=8", "4 total", "3 camping". A bare number is never a count, since pilot names often end in one.
- **What's going on** — a spike, gate camp, bubbles, wormhole, the ESS, a cyno, a skyhook, combat probes or a hotdrop risk, and which gate ("on the QZ-X77 gate"). A report that only says one of these still counts.
- **Pilots** — names pasted from the game. A one-word name typed differently from the character's own counts only if that character has been on a killmail in the system, so ordinary chatter isn't taken for pilots.
- **Clears** — "clr" and its common typos.

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

### Thera and Turnur

**Read Thera/Turnur connections and storms from EVE-Scout** is **on by default**. EVE Console reads the wormhole connections from Thera and Turnur from [EVE-Scout](https://www.eve-scout.com/) every five minutes, and the metaliminal storms it lists every hour. They are shown on the [Universe Map](tools/universe-map.md#other-marks) and on each system's page, and the [Route Planner](tools/route-planner.md) can route through the wormholes.

The line under the box says how many connections were read, and when. If EVE-Scout can't be reached, the last list is kept until the next read.

Unticking it stops the reading and **deletes** what is stored: holes close within hours and storms move, so an old list would mislead.

### History and coverage

- **History** — the backfill's status and a progress bar.
- **Backfill now** — runs the backfill for the number of days set above. Use it after raising **Backfill days** to fetch the extra history.
- **Cancel** — stops a running backfill.
- **Refresh current hour** — asks ESI for the current hour straight away.
- **Coverage** — one line per dataset: how many hourly buckets and days are stored, and the earliest and latest.

!!! note "Several clients on one database"

    Map statistics and EVE-Scout's connections are collected by the client doing the background work. When several clients share a [PostgreSQL](storage-postgresql.md) database, that is the one holding the lease — see [Background processing](background-processing.md). Game and chat logs are different: each client reads its own log folders.
