# Mercenary Dens

Every mercenary den your characters own, on one screen: where it is, whose skyhook it sits on, its state, its infomorphs, development and anarchy, whether it is reinforced, and the tactical operations it offers.

Open it from the left sidebar under **Corp / Interactions**.

## What it shows

A summary line sits at the top, such as *3 dens · 1 at anarchy 3 or above · 2 operations open*, with a **Refresh** button.

### The list

One row per den, the highest anarchy first:

| Column | What it shows |
| --- | --- |
| **Owner** | The character whose den it is. |
| **Planet**, **System**, **Region** | Where it is. |
| **Skyhook owner** | The corporation that owns the skyhook it sits on. |
| **State** | **Running**, **Paused** or **Disabled**; *Not read yet* until the detail has been read. |
| **Infomorphs** | How many it holds. |
| **Per hour** | How fast they build, from the last two readings. Blank until there are two, or when the count fell because they were taken out. |
| **Development**, **Anarchy** | The level (0–4), then the amount out of 100: *3 · 72*. Anarchy shows red at or above the level set for its alert. |
| **Reinforced until** | When it comes out of reinforcement, while it is reinforced. |
| **Operations** | Tactical operations open now. |

### The detail panel

Select a row for the same figures in full, plus when the den was last read. Below them, **Tactical operations** lists each operation with its **State** (*Available*, *Started*, *Completed*, *Expired* or *Removed*), when it **Expires** and when it was **First seen**. Open ones come first.

## Only your own dens

!!! warning "Anarchy is visible only to a den's owner"
    The game tells a den's anarchy only to the character who owns the den. So this tool lists your characters' own dens and no others.

    A den of anyone else's, even on your corporation's skyhook, can't be seen. The skyhook's data doesn't name it. On [Corp Structures](corp-structures.md#skyhooks), it shows only as the skyhook's lower workforce.

## Alerts

Under **Mercenary dens** on **Settings ▸ Alerts**, these raise alerts on the [Overview](overview.md#mercenary-den-alerts). Clicking one opens this tool on that den.

- **A den's anarchy at level** — at this level or above (0–4). The default is **3**.
- **A den attacked or reinforced** — from the notifications of the last day, which can be dismissed, and for as long as a den is reinforced.
- **A new mercenary tactical operation** — from the notifications of the last day, which can be dismissed.

## What it needs

Each character needs these scopes on its token. Add them with **Settings ▸ ESI Tokens** (see [Getting Started](../getting-started.md)).

| What | Scope | Read |
| --- | --- | --- |
| Dens and their details | `esi-structures.read_character.v1` | Hourly |
| Tactical operations | `esi-activities.read_character.v1` | Every 15 minutes to start |
| Attacks, reinforcement and new operations alerts | `esi-characters.read_notifications.v1` | Every 30 minutes to start |

How often each is read is on **Settings ▸ Timers**.

## Notes

- With no dens, the tool says so. It can't tell a character with no dens from one whose token doesn't allow reading them, so check the scope if a den is missing.
- The figures are as of the last reading, so anarchy can have moved on by up to an hour. The panel says when each den was read.
- Your dens also show on the skyhook's entry in [Corp Structures](corp-structures.md#skyhooks), when the skyhook belongs to a corporation you have a login for.
