# Planetary Industry

Every planetary colony of your characters in one list: when the extractors stop, when storage fills, when a factory planet runs out of input, and what each colony earns a day. A colony opens in detail, down to each extractor's program and each factory.

Open it from the left sidebar under **Industry**.

The same figures drive [Overview](overview.md) alerts, an [alarm](alarms.md) check and [Worklist](worklist.md) tasks, so the colony the list calls "stopping" is the one the Overview warns about and the Worklist asks you to restart.

## Where the data comes from

EVE Console reads each character's colony list from ESI, and then each colony's layout: its command center, extractors, factories, storage, launchpads and routes. ESI only has a new layout after the colony has been **opened in the game**, so every figure starts from that moment.

- **Extractor times are exact.** An extractor program's end is fixed when it is set.
- **Storage and input times are estimates.** The app replays the colony from the last time it was opened in the game — what the extractors deliver, what the factories take and make, and where the routes send it. The **Data age** column says how old that starting point is.

When a colony hasn't been opened in the game for too long (7 days unless you change it), its data is marked old: its estimates can't be trusted until you open it in the game again.

!!! note
    Characters need the **esi-planets.manage_planets.v1** scope. Colonies are read only for characters with the **PI** box ticked on **Settings ▸ Characters** (see [Choosing which characters do PI](#choosing-which-characters-do-pi)).

## What it shows

Above the tabs is a summary line — for example *22 colonies · 3 extractors stopped · 2 need hauling · 1 input low* — with **Open colony**, **Refresh**, and when the list was last read. The list re-reads every minute while it's open; new colony layouts are read from ESI every ten minutes.

### Colonies tab

One row per colony, the ones needing action soonest first:

| Column | Meaning |
| --- | --- |
| **Character** | Who owns the colony. |
| **Planet**, **Type** | The planet, with its type's icon, and the planet type (Barren, Gas, …). |
| **System**, **Region** | The solar system with its security, and its region. |
| **Kind** | **Extractor** (sends its own output off), **Factory** (needs input brought in) or **Empty**. |
| **Imports** | What the colony needs brought in from off the planet: anything used on it that nothing on it makes. Hover to see how many units of each a day. |
| **Exports** | What goes off the planet: anything made on it that nothing on it uses. Hover to see how many units of each a day. |
| **Waiting (m³)**, **Waiting (ISK)** | The exports in storage, launchpads and the command center now, waiting to be picked up, at market prices. Estimated. Hover for each item, and the visit the estimate starts from. |
| **CC** | Command center level against the highest your **Command Center Upgrades** skill allows. |
| **Extractors end** | When the first extractor program ends, or **Stopped**. Exact. |
| **Storage full** | When storage or a launchpad first fills, or **Full**. Estimated. |
| **Inputs run out** | For a factory planet, when its brought-in input runs out, or **Ran out**. Estimated. |
| **Status** | **OK**, **Attention** or **Action**, as a word and a mark as well as a colour. Hover to see why. |
| **Data age** | How long ago the colony was last opened in the game; **(old)** when it's past the limit. |
| **Efficiency** | The forecast as a share of what the colony could make (see [Potential and forecast](#potential-and-forecast)). |
| **Profit** | Profit per day: output, less inputs and import and export charges, at market prices. |

**Action** means something has already happened — extractors stopped, storage full, input run out. **Attention** means something comes due within the lead times (see [Settings](#settings)), output will be destroyed or raw material will overflow, or the data is old.

**Exports** are the end of each chain, not everything the colony makes: what one factory makes for the next is left out. Raw material the factories can't keep up with is listed, because it has to be hauled too. **Waiting** counts exports only — input sitting on a launchpad, and a part-made product waiting for the next factory, aren't included. The summary line adds the total waiting across all colonies, for example *4,210 m³ of exports waiting, worth 1.20B ISK*.

Double-click a colony, or select it and click **Open colony**, to see it on the **Colony** tab.

### Colony tab

One colony in detail. Under the planet's name: the character, system, planet type and kind, and how old the data is.

- **Potential and forecast** — what the colony could make over its period against what it will (see below).
- **Command center** — its level of the highest allowed, with the CPU and powergrid that gives.
- **Extractors (exact)** — each extractor's product, number of heads, program start and end, the cycle it's on, total output and what is still to come. A chart puts each cycle on a timeline in local time, with a line for now; hover a bar for its time window and units.
- **Factories (estimated)** — each factory's schematic, output, facility type, and whether it's **Running**, **Idle** or **Idle since** a time.
- **Storage and launchpads (estimated)** — fill, volume of capacity, when it fills, and contents.
- **Flows per day** — each item's tier, and how much is made, used, brought in and taken off a day, running as built.
- **Money per day** — output value, input cost, export and import charges, profit, and the tax rate used.

The **Tax rate** says where it came from: learned for this planet from your wallet journal, or the default from **Settings ▸ Industry** while it hasn't been learned yet. A rate is learned after you've exported or imported at that planet.

### Potential and forecast

Each colony has a period: until its extractors stop (at most 30 days), or the next 30 days for a factory planet.

- **Potential** — the colony running as built for the whole period: its output at market prices, less the input it's brought and the charges.
- **Forecast** — what the replayed colony actually gets into storage and launchpads over the period, less the input its factories use and the charges.
- **Short by** — the difference, explained underneath:
    - **Destroyed** — products thrown away because storage was full, or because a factory had no route for them, and from when;
    - **Raw overflow** — raw material lost because extraction outpaces the factories;
    - **Idle factories** — output not made while factories waited for input.

The shortfall is roughly what is destroyed plus what idle factories don't make; the rest is part-finished cycles and stock still in storage when the period ends. For an extractor planet whose extractors have all stopped, there's nothing to forecast until they're restarted.

### Characters tab

The characters that do PI:

- **Colonies** — colonies in use of the number allowed;
- **Free slots** — colonies the character could still set up;
- **Skills** — **Interplanetary Consolidation** (one colony plus one per level) and **Command Center Upgrades** (the highest command center level);
- **Command centers** — each colony's command center level; an ↑ marks one that can be upgraded.

**PI box in Settings…** opens **Settings ▸ Characters**.

## Using it

1. Check the **Status** column; hover the chip to see what's due.
2. Open a colony to see why — a full launchpad, a factory waiting for input, or an extractor about to stop.
3. Do the work in the game. Opening the colony there also refreshes its data; it's read again within about ten minutes.
4. Use the [Worklist](worklist.md)'s PI tasks for a to-do list across all colonies, with what to haul.

## Alerts, alarms and tasks

- **Overview alerts** — extractors stopped or stopping, storage full or filling, factory input out or running out, a PI character with a free colony slot, and colony data too old to trust. See [Overview](overview.md).
- **Alarm** — the **Planetary Industry** check in the alarm editor fires for extractors, storage or inputs, with its own lead time in hours. Each colony's event fires once; restarting the extractors or opening the colony again makes it news again. See [Alarms](alarms.md).
- **Worklist tasks** — restart extractors, take output off, bring input, set up a colony, upgrade a command center, and open a colony whose data is old. See [Worklist](worklist.md#planetary-industry-tasks).

## Settings

### Choosing which characters do PI

**Settings ▸ Characters** has a **PI** box for each character, ticked by default. Clear it for a character that doesn't do PI: its colonies aren't read, and it's left out of this tool, its alerts and its worklist tasks.

### Settings ▸ Industry

- **Planetary Industry tax** — the **Customs office tax** and **Skyhook tax** used for a planet until its own rate has been learned (10 % each to start). Customs offices are in high-sec, low-sec, wormholes and NPC null-sec; sovereignty null-sec has skyhooks instead. Bringing goods in costs half of taking them off.
- **Planetary Industry alerts and tasks** — how far ahead the alerts and tasks look, and when data is too old:

| Setting | Default |
| --- | --- |
| **Extractors stopping** | 24 hours ahead |
| **Storage or a launchpad full** | 24 hours ahead |
| **Factory input running out** | 48 hours ahead |
| **Colony data too old after** | 7 days |
| **An input haul brings** | 7 days of running |

Which alerts are raised at all is on **Settings ▸ Alerts**, under **Planetary Industry**. Settings save as you change them.

## Notes

- Everything is only as fresh as the last time each colony was opened in the game. Open your colonies in the game now and then, even when nothing needs doing.
- Prices are the market prices used to value assets (see [Configuring Markets](../configuring-markets.md)).
- Learning a planet's tax rate needs the wallet journal synced for that character.
