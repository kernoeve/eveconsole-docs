# Corp Structures

A corporation's Upwell structures, starbases and skyhooks in one list: state, services, fuel left and when it runs out, what the fuel costs a day, and whether each structure carries the fit you set for its type.

Open it from the left sidebar under **Corp / Interactions**.

## What it shows

The tool has two tabs, **Structures** and **Config**. Above them:

- **Corporation:** — whose structures to show. Your choice is remembered on this machine.
- **Search** — by name, type, system or region.
- **Upwell structures**, **Starbases**, **Skyhooks** — tick boxes for what to list.
- A summary line, such as *12 structures · 3 starbases · 2 low on fuel · 0 out · fuel 48.2M ISK a day*. It also counts skyhooks, and structures not matching their fit, when there are any.
- **Refresh**. The tool also reloads every five minutes, so the fuel left keeps counting down.

### The list

| Column | What it shows |
| --- | --- |
| **Name**, **Type**, **System**, **Region** | Where and what it is. A starbase is named after its moon, a skyhook after its planet. |
| **State** | Online, reinforced, anchoring and so on, in the game's own terms. |
| **Services** | Services online out of the total, such as *3 / 4*. |
| Info icon | A red **i** when the structure is off the fit set for its type. Hover for what is wrong. |
| **Fuel left** | Time until it runs out. Shows as running low under 7 days and as critical under 3 days. It reads **Out of fuel**, or for a structure with no fuel at all **Low power**, or **No services** where nothing is fitted to burn any. |
| **Runs out** | The date and time it does. |
| **Blocks / day** | Fuel blocks burned a day. |
| **ISK / day** | What the fuel costs a day. See [Fuel](#fuel). |
| **Pickup value**, **Pickup vol (m³)** | What a Metenox has drilled and holds, ready to collect. |

Structures with fuel come first, those running out soonest at the top.

### The detail panel

Select a row to see it in full. Each part shows only when there is something in it.

- **Status** — state, fuel run-out, blocks a day and an hour, fuel cost, state timers, reinforce hour and any change coming to it, when it unanchors, and the access profile.
- **Fuel** — each fuel in the bay, with **On hand**, **Per day**, **Lasts**, the run-out date and where the burn came from.
- **Services** — each service and whether it is online.
- **Fit check** — the structure against the fit set for its type, line by line. See [Config](#config-the-fit-each-type-should-carry).
- **Fit** — what is fitted, by slot: high, medium and low slots, rigs, service slots and quantum core, then fighter tubes, fighter bay and the ammo hold. Modules marked *entered by hand* were typed into the [Structure Browser](structure-browser.md) where the assets don't reach.
- **Moon drilling** — a refinery's extraction: when it started, when the chunk arrives and when it fractures on its own. For a Metenox, the moon material bay by **Material**, **Units**, **m³** and **Value (ISK)**, with how full the bay is.
- **Skyhook** — see [Skyhooks](#skyhooks).
- **Starbase settings** — who may use the starbase, what it fires on, and which role may anchor, unanchor, online, offline, view the fuel bay and take from it.
- **Location** — system and security, region, and the nearest celestial, the moon or the planet.

## Fuel

### Upwell structures

**The time left is the game's own.** It is the fuel expiry ESI reports for the structure, not an estimate.

**Blocks a day are worked out from the fit:**

1. Take each running service module's rate from the game data.
2. Take off the structure's fuel bonus for that module's group.
3. Add them up, then round the **total** down to whole blocks an hour.

The rounding is on the total, not on each module, because that is what the game's expiry shows. A Tatara with three reactors and a reprocessing plant burns 11.25 × 3 + 7.5 = 41.25 an hour, so 41.

- A module counts as running unless all of its services read offline.
- **With no fit known, no burn is shown.** If the corporation's assets haven't been read, the app doesn't guess at consumption from the services. The time left still shows, since it comes from the game.
- If the burn and the expiry disagree by more than rounding, the fuel row says so: *the fuel expiry implies N a day*.

**Other fuels, such as a Metenox's gas,** burn at what the bay has actually lost since it was last topped up. That figure needs at least six hours of readings; until then the row reads *burn not measured yet*. A refill starts the measuring again. If a structure's gas runs out before its blocks, **Runs out** gives the gas's date.

### Starbases

- **Fuel blocks** burn at the tower's size: 10, 20 or 40 an hour for small, medium and large. Faction towers burn 10% less, or 20% less for the top faction tier (Dark Blood, Domination, Dread Guristas, Shadow, True Sansha).
- **Strontium** burns 100, 200 or 400 an hour by size, only while reinforced. The panel gives it as hours of reinforcement held.
- **Charters** and the actual burn are measured since the bay was last topped up, as above. Where the measured burn is known, it shows beside the expected one.
- **Runs out** is the first of the blocks and charters to go, from the last reading of the bay.

### ISK a day

Priced at the same prices your assets are valued at. Blocks are priced as the kinds in the bay, by how many of each; with none in the bay, as the average of the four kinds. Any other fuel with a burn is added: a Metenox's gas, a starbase's charters, and strontium while reinforced. Where the blocks a day aren't known, the column is blank.

## Skyhooks

A skyhook's detail shows:

- **Producing** — whether it is producing workforce, power or reagents.
- **Workforce** — its workforce now. A mercenary den attached to it lowers this.
- **Theft window** — when reagents can be stolen. It is flagged while open.
- **Reagents** — **Secured** and **Unsecured**, as of the last cycle.
- **Your characters' dens on it** — any [Mercenary Dens](mercenary-dens.md) your own characters run there.

!!! note "Anarchy is visible only to a den's owner"
    The game tells a den's anarchy only to the character who owns the den. A den of anyone else's on your corporation's skyhook isn't listed; it shows only as lower workforce.

## Config: the fit each type should carry

The **Config** tab has one row for each type of Upwell structure the corporation has anchored, with a **Fit to carry** dropdown and a status such as *4 anchored · 1 not matching*. The list holds EVE Console's own [fits](fitting.md) for that type, and your characters' fittings in the game. Choosing one saves it at once, for this corporation. **No fit — not checked** turns the check off for the type.

Each structure of the type is then checked:

- **Modules** — every module of the fit must be there, in any slot of the right kind. Extra modules and rigs are fine.
    - A module short of the fit is **Missing** while that kind of slot has one free.
    - Once those slots are full it is **Not fitted**, and the check lists what is **Fitted instead**.
- **Ammo** — each charge in the fit, against how many the structure holds, loaded or in its ammo hold. Ammo in the corporation's hangars doesn't count.
- **Fighters** — each fighter in the fit, against the tubes and the fighter bay together.

Ammo and fighters count as low below a share of the fit's amount, set on **Settings ▸ Alerts** (50% to start).

If a game fitting is saved again it is found again by its owner, name and hull. If the chosen fit can no longer be found, the check goes on against a copy kept when it was last read, and the list says *no longer saved; its copy is checked*.

Starbases and skyhooks aren't checked against a fit.

## Alerts

These appear on the [Overview](overview.md#structure-alerts), for corporations with **Structure alerts** ticked on **Settings ▸ Corporations** (all of them to start). Each kind has its own switch under **Structures** on **Settings ▸ Alerts**. Clicking one opens this tool on that corporation and structure.

## What it needs

Everything is read by background polling from a corporation login, so the character behind it needs the role in game as well as the scope on its token. A Director can read all of it.

| What | Scope | Role in game |
| --- | --- | --- |
| Structures, services, fuel expiry, timers | `esi-corporations.read_structures.v1` | Station Manager |
| Fit, fuel amounts, ammo, fighters, moon bay | `esi-assets.read_corporation_assets.v1` | Director |
| Starbase list | `esi-corporations.read_starbases.v1` | Starbase equipment config |
| A starbase's fuel and settings | `esi-corporations.read_starbases.v1` | Director |
| Skyhooks | | Station Manager |
| Moon extractions | `esi-industry.read_corporation_mining.v1` | Station Manager |

Your characters' own tokens add two more things: attacks come from their notifications (`esi-characters.read_notifications.v1`), and game fittings from `esi-fittings.read_fittings.v1`.

How often each is read is on **Settings ▸ Timers**. To start, structures and skyhooks are read hourly, and corporation assets and starbases every two hours. So the fuel on hand and the fit lag behind the game by up to that long.

## Notes

- **No assets, no fit.** Without a Director's access the list and fuel expiry still work, but blocks a day, the fuel table, the fit and the moon bay stay empty, and the fit check reads *Not checked*. Modules entered by hand in the [Structure Browser](structure-browser.md) still show.
- **A starbase's modules** show only where the corporation has one starbase in that system. The assets give no position, so two starbases' modules can't be told apart.
- **Attack alerts rely on your characters' notifications.** A character has to have received the notification, and one that can't be put to a structure of the corporation raises nothing.
- The list reads the local database, not the game. **Refresh** shows what the polls have brought in so far.
