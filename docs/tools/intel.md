# Intel

Live intel in one place: who is reported where, how far they are from your characters, how they stand with you, where they were last seen, and which gates are camped. It gathers your intel channels, the kills the app collects and the Local and d-scan you paste, and every intel view reads the same picture: this tool, the [Intel panel control](#the-intel-panel-control) beside a game client, the [Universe Map](universe-map.md#live-marks) and the [Intel report alarm](alarms.md#intel-report).

Open it from the left sidebar under **Structures / Navigation**, after **Universe Map**.

## Where intel comes from

- **Intel channels in the chat logs** — the channels you tick as **INTEL** under **Settings ▸ Chat Logs**. See [Logs & Map Data](../logs-and-map-data.md#intel-channels).
- **Jabber rooms and IRC channels** whose **Type** is set to **Intel**. They are read the same way as an intel channel. See [Jabber](../jabber.md) and [IRC](../irc.md).
- **Kills** — every kill the app has stored, from ESI and from [zKillboard](../zkillboard.md). A kill places its attackers in the system with the hulls they flew, and its victim is no threat, so is never counted.
- **Your pastes** — a Local member list or a d-scan, on the [Paste](#paste) tab.

Your characters' own whereabouts come from ESI and from the chat logs. The game logs don't feed intel.

A report relayed from one channel into another (an EVE channel into a Jabber room, say) is recognised and counted once; it shows as **×2** with the places it was heard in its tooltip.

!!! warning "Kills need the full zKillboard feed"
    With the [zKillboard](../zkillboard.md) scope on **My characters & corp only**, only kills involving you and your corporations arrive, so kills between other pilots near you, and the gate camps worked out from them, are missing. The tool says so in a bar across every tab until you choose **Capture all kills**. **Open Kill Mails settings** takes you there; the **✕** hides the bar on every PC until the full feed is switched on and off again.

Without any intel channel set, the tool still shows kills and pastes, and says how to add a channel.

## What it shows

The tool has six tabs: **Board**, **Feed**, **Pilots**, **Camps**, **Paste** and **Watch list**. The bar above the first four filters what they show, and is kept on this computer.

- **Distance from** — where jumps are counted from: **Nearest online character** (each system measured from whichever of your characters is nearest), one of your characters, or a system typed in **or a system…**. A character who isn't online gets no jumps until they log in.
- **Within** — 5, 10, 15, 20 or 30 jumps, or **Any distance**. 15 to start.
- **My jump bridges** — counts your own jump bridges in how far *you* have to go. How near a threat can come never uses them.
- **Standings** — chips for **Red**, **Orange**, **Neutral**, **Light blue** and **Blue**. Red, Orange and Neutral are on to start.
- **Sources** — tick which channels, **Kills (zKillboard and ESI)** and **Pasted Local and d-scan** to show.
- A **search** box for a system or pilot (on **Pilots**: a pilot, corporation or alliance).

Jumps are counted through stargates and through every open Thera and Turnur connection, both ways. Thera and Turnur connections are read from EVE-Scout, so they count only while EVE-Scout reading is on under **Settings ▸ Map Data** (see [Map Data](../logs-and-map-data.md#map-data)). A distance through one is marked so.

Pilots are coloured by their standing. A portrait sits beside a single pilot's name and a ship icon beside a hull name. Click a system to open its page on the Universe Map, a pilot, corporation or alliance to open them in [Players & NPCs](entities.md), and a hull to open it in the Item Browser. Right-click a line for **Show on map**, **Copy system name**, **Open pilot**, and **Always alert** or **Ignore** for a pilot (see [Watch list](#watch-list)).

### Standings

A pilot's standing is how the character looking sees them, in the game's five steps: **Red** (below −5), **Orange** (−5 up to 0), **Neutral** (0 or none), **Light blue** (above 0 up to +5) and **Blue** (above +5).

- Your own characters are never hostile.
- Anyone in a corporation or alliance one of your characters is in is blue to all of them.
- Otherwise the looking character's personal contacts decide first, then its corporation's, then its alliance's. In each list a contact on the pilot counts first, then one on the pilot's corporation, then on their alliance. Faction standings aren't used.

*The character looking* is the one a panel follows, or the nearest online character, or the one chosen in **Distance from**. When jumps are counted from a system, nobody in particular is looking, so a pilot counts as friendly if any of your characters has them blue. **Settings ▸ Intel** can make one character's standings apply everywhere instead (see [Settings](#settings)).

Without the contacts scope for a character, its personal contacts aren't known, and the panel says that colours come from the corporation and alliance contacts only.

### How long intel lasts

Each kind of news counts as current for a while after it was reported, fading as it ages, and then drops off the Board, the panels and the map:

| News | Lasts (default) |
| --- | --- |
| A named pilot | 15 minutes |
| An unnamed count ("+5") | 15 minutes |
| A system called clear | 10 minutes |
| A gate camp or bubbles | 30 minutes |
| A cyno | 10 minutes |
| A pilot on a kill | 15 minutes |
| A pilot who lost a ship | 5 minutes |

Change them under **Settings ▸ Intel**. Sooner than that, a pilot leaves a system when they are reported or seen on a kill somewhere else, when the system is called clear, or when a pasted Local of it leaves them out.

### Board

One row per system with live intel, within the distance chosen. The strip above it counts the systems, hostiles and gate camps, says when it was last updated, and which PC is parsing intel. **Sort** by **Nearest**, **Newest** or **Most hostiles**.

| Column | What it shows |
| --- | --- |
| **Jumps** | How far, from the character or system in **Distance from**. |
| **System** | The system, with its region under it. |
| **State** | **Hostile**, **No visual** (reported in Local, not seen on grid), **Camp**, **Flags** (something said, nobody counted) or **Clear**. |
| **Hostiles** | How many: the pilots named, plus the most anyone counted without naming. |
| **Who** | The alliances (or corporations) there with how many each, or the one pilot. |
| **Ships** | What they fly, the most flown first. |
| **Flags** | A kill, a gate camp, bubbles, a cyno and the like, as icons; hover for the words. |
| **Moving** | Where they came from, or where they were said to be heading. |
| **Age** | How long ago the newest news came. |
| **Nearest** | Which of your characters it was measured from. |
| **Sources** | Which channels, kills or pastes said it. |

Click a row to open it: the pilots there first, then the system's reports, follow-up lines and kills. Double-click to open the system's page. The Board lists up to 200 systems.

### Feed

Every line, newest first: reports, follow-up lines, clears, pastes, kills and gate camps, each labelled by what it is, with who reported it and where. Lines that have expired or been replaced by newer news stay, faded and marked **expired** or **superseded**.

- **Last** — 15, 30 or 60 minutes. 60 to start.
- **Show kills** — on to start.
- **Unlinked chatter** — also show lines from the intel channels that gave no intel (talk, questions, a follow-up with nothing to attach to), muted. Off to start. Chatter is never stored as intel.

The Feed shows up to 500 lines.

### Pilots

Where each pilot was last seen, by any source: a report, a pasted Local, or a kill they were on or lost a ship in. Choose **Seen in the last** 1 hour, 6 hours, 24 hours (the start), 7 days or 60 days, and search by pilot, corporation or alliance. Columns: **Pilot**, **Last seen in**, **Seen**, **Hull**, **How**, **Corporation** and **Alliance**; each sorts when clicked, and the other way round when clicked again. The newest 500 are listed; search to narrow.

The standings chips apply here too: pilots of a standing switched off aren't listed, and the line says how many were hidden.

A pilot's page in [Players & NPCs](entities.md) shows the same **Last seen** line.

### Camps

Gate camps near you, active and lately ended. A camp is worked out from kills on a gate: kills within 150 km of a stargate, each no more than 30 minutes after the one before and sharing an attacker, once at least 2 different pilots have been lost there. A single kill isn't a camp. An intel report calling a camp on that gate counts too.

Columns: **Jumps**, **Camp** (the system and the gate, named for where it leads), **Status** (**Active** or **Ended**), **Kills**, **Last**, **Attackers**, **Flags** (smartbombs, an interdictor or heavy interdictor, bubbles) and **Sources** (**Kills**, **Reported**, or **Kills and reports**). An ended camp stays, faded, for an hour after its last kill.

Double-click a camp, or right-click it for **Open kills**, to open its kills in [Battle Report](battle-report.md).

### Paste

Turns a Local member list or a d-scan into intel for a system.

1. Choose the **System** it is from. It starts on your first online character's system; the list offers your characters' systems, or **or another system…**.
2. Check **Pasted by**. It follows the system's character until you pick one yourself.
3. In the game, select everything in the Local member list or the d-scan window, copy, and paste into the box with **Ctrl+V**. The app never reads the clipboard by itself; only what you paste into the box is used.
4. The preview under the box shows what would be stored, before anything is saved: **Detected: Local list** or **Detected: d-scan**, and who is on it, by standing, alliance and corporation.
5. Press **Save** (or **Ctrl+Enter**). The line shows on the Feed and the Board at once. **Clear** empties the box and the preview.

**A Local is the whole roster.** Saving it takes out everyone reported in that system and places everyone on the list, so a Local with nobody of the chosen standings on it saves the system as clear. The **Save:** chips choose which standings a Local saves (Red, Orange and Neutral to start, kept on this computer); your own characters are never saved. Save stays off, with the reason shown, while every chip is off, while the chips would leave out someone who may be hostile, or while names haven't been looked up yet because ESI isn't answering (it tries again every 15 seconds).

**A d-scan only adds.** It adds an unnamed count of the ships on it, and never clears the system, since d-scan doesn't see everyone. A Mobile Warp Disruptor on scan adds bubbles, and a Cynosural Field a cyno.

**Recent pastes** lists what was pasted lately, on any PC.

### Watch list

Pilots, corporations, alliances, hulls and ship groups you always want to hear about, or never. The list is shared by every PC on the database.

- **Always alert** — shown in bold, and an intel alarm using the watch list fires for them from farther away, said first.
- **Ignore** — shown dimmed, and never alerted for.

A pilot's own entry decides first, then their corporation's, their alliance's, their hull's and its group's.

To add one, choose the kind, type a name in **Name to add…**, choose the mode, add an optional note and press **Add**. Or right-click a pilot anywhere in intel and choose **Always alert** or **Ignore**; choosing the ticked one takes them off. The list shows **Kind**, **Name**, **Mode**, **Note** and **Added**; change a mode in its row, or take an entry off with its button.

## The Intel panel control

On Windows, [Client Layouts](client-layouts.md#panel-controls) can put an **Intel** control in a panel beside a game client. It follows the character in that monitor's client and shows live intel around them, one line per system with hostiles, nearest first: how far, the system and region, how many, what they fly, who, the flags, and how long ago. Click a line to open it to the pilots there and the system's reports, kills and camp lines.

- **Shows as** — the live list, or one line with the nearest threat and how many more, the list dropping down when clicked.
- **Looks out to** — 3, 5, 10, 15 or 20 jumps (10 to start), through stargates and open Thera or Turnur holes. Jump bridges aren't counted.

Both are set in the layout editor. The control shows threats only: blue and light blue are left out, and at most 50 lines show. Fresh news within five jumps lights its line up; that is a look only, and the sound is the alarms' job. Its buttons paste Local or d-scan (the **Paste** tab, with this character and system chosen) and open the Intel tool. Nothing is ever sent to the game client.

The control is part of Client Layouts, which needs Windows. On Linux and macOS, use the tool itself.

## Alarms

The [Intel report](alarms.md#intel-report) alarm reads the same intel: sightings near your characters or chosen systems, kills, gate camps, the route ahead, the watch list and pilots coming closer. Each pilot is said once while they stay in a system. The Universe Map's **Alert zones** layer outlines what the intel alarms watch now (see [Universe Map](universe-map.md#intel-layers)).

## Settings

**Settings ▸ Intel** holds what every PC on the database shares:

- **How long intel lasts** — the lifetimes in the table above, from 1 to 120 minutes each.
- **Follow-up lines** — **Follow-up window**, 180 seconds to start (30 to 600). A line with no system of its own ("+2", "nv", "clr") adds to the same reporter's last report in the same channel when it comes within this time.
- **Gate camps from kills** — **Within this distance of a gate** (150 km; 20 to 1,000), **Longest gap between kills** (30 minutes; 5 to 120) and **Pilots lost before it is a camp** (2; 2 to 20).
- **Standings** — **Standings from**: **(each client's own character)**, or one character whose standings colour everything.
- **Distance** — **Use our jump bridges in travel distances**. Off to start. Threat distances never use them.
- **Intel alarms** — **Wake only for news newer than** (120 seconds; 15 to 1,800) and **Wait between wakes** (15 seconds; 0 for no wait, up to 600). See [Alarms](alarms.md#intel-report).
- **Kill feed warning** — **Show the warning again** after it was hidden.

How long intel history is kept is set under **Settings ▸ Data Retention**: **Purge intel history older than**, 90 days when ticked (at least 7). It removes intel reports, the pilots named in them and where each pilot was last seen. Chat messages and kills are kept by their own rules.

## Using it

1. Tick your intel channels under **Settings ▸ Chat Logs**, or set a Jabber or IRC room's **Type** to **Intel**.
2. For kills from everyone, set [zKillboard](../zkillboard.md) to **Capture all kills**.
3. Open **Intel** and pick **Distance from** and **Within**.
4. Read the **Board**; click a row for who is there and what was said.
5. Paste Local or d-scan on the **Paste** tab when you look at a system yourself.
6. Put pilots or groups on the **Watch list**, and set up an [Intel report](alarms.md#intel-report) alarm to be told.

## Notes

- Every PC on a shared [PostgreSQL](../storage-postgresql.md) database shows the same intel. Only the PC doing the background work parses intel and runs the intel alarms; the status line says which (**Intel parsing: this PC**, **worker on …** or **no worker**). See [Background processing](../background-processing.md).
- The tool's view refreshes every 5 seconds while it is on screen, and at once when new intel is written on any PC.
- Which camps have ended, and what an intel alarm has already announced, are remembered by the running app only. After a restart, or when the background work moves to another PC, an alarm can announce something old once more.
- Lines stored for a channel before it was ticked as intel aren't parsed by themselves: use **Parse Stored History** under **Settings ▸ Chat Logs**.
