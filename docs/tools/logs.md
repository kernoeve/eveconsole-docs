# Game & Chat Logs

Two viewers over the log files your EVE client writes — the **Game Log** and the **Chat Log** — so you can search your history.

Open them from the left sidebar under **Data / Logs**.

What gets imported is set up in **Settings**, on the **Game Logs** and **Chat Logs** tabs: which folders are read, which chat channels are stored, and how far back to import. See [Logs & Map Data](../logs-and-map-data.md).

## What it shows

- **Game Log** — the activity found in your game logs: combat, mining, bounties, jumps, undocking, stopping the ship and decloaking. Columns are **Time**, **Type**, **Character**, **Amount**, **Source**, **Target** and **Detail**. Select an entry to see its full detail.
- **Chat Log** — a list of channels with messages in the chosen dates, and the messages of the selected channel. Columns are **Time**, **Sender**, **Message** and **Listener** (the character whose log it came from).

Chat logs from intel channels are also parsed into *sightings*: who was seen, where, in what hull, and anything else said about the system. Those sightings surface on the [Universe Map](universe-map.md)'s live marks and overlays, on each system's **Intel** tab, and in the **Intel report** [alarm](alarms.md#intel-report).

## Using it

- **From** / **Thru** — a date range. Leave **Thru** empty to read up to now.
- **Type** (Game Log) — show one kind of activity.
- **Find** — search by name or text (Game Log), or by sender or text (Chat Log).
- **Hide system** (Chat Log) — hides system lines such as the MOTD and channel changes.
- **Refresh** — reloads the list.

## Notes

!!! note
    Duplicate messages are recognised across characters and machines, so importing a second computer's logs does not double-count the same sighting.

- Game log import is on by default. Chat log import is off until you turn it on and tick channels. Both only capture new activity until you run an import — see [Logs & Map Data](../logs-and-map-data.md).
- What the viewers show was imported from the log files EVE writes — on this PC (its own Gamelogs and Chatlogs folders are always read), and on other PCs through the network paths you add. Nothing is fetched from ESI.
- The game writes its log in the client's language. Combat, warp scrambles, decloaking, stopping the ship, jumps and undocking are recognised in all eight client languages; mining and bounties from an English client only. See [Logs & Map Data](../logs-and-map-data.md#game-logs).
