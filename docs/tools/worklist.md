# Worklist

The Worklist is a single, always-current list of **what to do next** across all of your authorized characters and personal corporations. It is rebuilt from scratch on every refresh by pulling from up to eleven independent sources — industry jobs, logistics, invention and copying, material purchases, refining, standing buy orders, inventory levels, corp projects, skill queues, asset safety and planetary industry — and turning each into a concrete task.

Open it from the left sidebar under **General**.

## What it shows

The tool has several tabs: **Worklist** (the task list), **Station Needs** (the same work rolled up by location), **Item Needs** (rolled up by item — what still has to be made), **Bottlenecks** (what's holding work up), **Final Products** (a record of what the work has produced), and **Config** (which sources are on and how they behave — see [Config tab](#config-tab)).

### Worklist tab

- A **Refresh** button, an **Auto refresh** box, and a "Refreshed *hh:mm*" timestamp — the list is regenerated each time. With **Auto refresh** ticked (the default), the list rebuilds itself every few minutes. Untick it while you fly a hauling loop, so the plan doesn't change under you; **Refresh** still rebuilds it.
- A **summary strip** of counts: a large **ready now** total, and a breakdown by task type (for example **buy**, **haul**, **manufacturing**, **reactions** and **PI**).
- Two toggles: **Show blocked / waiting** (tasks that can't be done yet — e.g. waiting on an upstream job — with their own count) and **Show snoozed** (tasks you've set aside).
- A row of **filters**: **State**, **Type**, a **Search task** box, **Character**, **Source**, **Destination**, and a **Search note** box.
- The **task list**, grouped by task type (Buy, Haul — in system, Haul — nearby, Haul — long distance, Manufacturing, Reactions, PI, …). Each row shows the task itself — the item and quantity, the station/structure it applies to, and the responsible character — plus a **Value** and a **Volume** column. Hover the **ⓘ** marker for the full reasoning.
- An **icon** on each row: the item's own, or for a task with no item, a picture of what it's about — the ore for a refining task, the character's portrait for a skill queue or **Set up a colony** task, the planet for a task on one colony, and the station for an asset safety task. A copy job, a manifest line or a print to buy shows the blueprint's own picture.

A row with more to say has a **+** in front of it. Click it and the row opens in place, in the grid, with its detail as rows beneath it:

- the task's reason, in one or two lines;
- for a haul, the **MANIFEST** (what to load) or the loop's stops — see [Hauling](#hauling);
- **WAITING ON THIS** — the jobs held up by this task, each with its verdict in colour: green where this task starts the job.

Click **−** to close it again.

### Station Needs tab

The same outstanding work aggregated **by station/structure**, so you can see everything that needs buying or moving at a given location in one place — useful when planning a shopping or hauling run.

### Item Needs tab

The outstanding work aggregated **by item** — what still has to be *made*, with the tasks waiting on each item beneath it. Where Station Needs answers "what does this place want," Item Needs answers "what do I still have to produce," so it counts production rather than just what a station holds.

### Bottlenecks tab

What's holding the rest of the work up. Each sub-tab answers a single question — **Slots**, **Item Contention**, **BPO / Formula**, and **Hauling** — and a **Summary** ranks the *actions* themselves by how much work each one is blocking (for example "raise level 200 to 570", or "buy 1 of 4 owned (+25% output)"). Every "how much does this hold up" figure is measured by walking the actually-blocked tasks, not the recipe tree, so it reflects work you're really doing rather than everything a recipe could theoretically need.

### Final Products tab

A record of **what the work has produced**: every job — finished or still running — whose output is something your operation sells. A job's value is taken as of the day it completed, and can be read either as **market value** or as a **fixed percentage over build cost** (a shop selling at a set margin never sees the market price). Profit is shown as *potential* profit throughout, because nothing on this tab has actually been sold yet.

### Config tab

How the list is built, in sub-tabs:

- **Sources** — which sources are on (see [The sources](#the-sources)).
- **Market** — where shortfalls are bought, and which character keeps orders at each station.
- **Inventory Rules** — when a group from [Inventory Levels](inventory-levels.md) falls below **Trigger below (%)**, what to do about it at which station, and how far to **Fill up to (%)**.
- **Station Levels** — where each group's stock should live; this raises hauling only.
- **Hauling** — how each kind of trip is made and who flies it (see [Setting up hauling](#setting-up-hauling)).
- **Other** — the park to plan against, the asset scope, job lengths and corp project owners.

A fill target above 100 % is rounded down, so it never adds more than its percentage: a level of 1 at 110 % stays 1, and 10 at 110 % is 11. Below 100 % it's rounded up, so filling to 80 % of 1 still means 1.

## The sources

Each source can be switched on or off independently on **Config ▸ Sources** (see [Setting it up](#setting-it-up)). A source that is off is skipped entirely.

- **Industry Jobs** — jobs to start or collect.
- **Logistics** — items that need hauling between locations (see [Hauling](#hauling)).
- **Invention & Copying** — invention and blueprint-copy jobs. Each invention job goes to the character with the best odds for it who has a slot free; copy jobs go to the scientists invention needs least, so the best inventors keep their slots for the attempts.
- **Material Purchases** — inputs to buy for planned builds, plus the datacores and decryptors the planned invention jobs need. Like any material, these are netted against stock anywhere in the industry scope (that's a haul, not a buy), open buy orders, output on its way, and what started jobs have already taken. The row says what they're for — for example *For Hawk Blueprint (3 run(s)) and Harpy Blueprint (3 run(s)) and 2 more: need 120; 16 on hand in Jita — short 104.*
- **Refining** — ore, ice and gas to reprocess or decompress.
- **Standing Buy Orders** — see [Standing Buy Orders](standing-buy-orders.md).
- **Inventory Levels** — restock shortfalls, from [Inventory Levels](inventory-levels.md).
- **Standing Projects** — deliveries toward corp standing projects.
- **Skill Queues** — characters whose skill queue needs attention. A character whose **Skill queue** box is cleared in **Settings ▸ Characters** is left out.
- **Asset Safety** — asset safety wraps waiting for you to choose where they go (see [Asset safety tasks](#asset-safety-tasks)).
- **Planetary Industry** — work on your planetary colonies (see [Planetary Industry tasks](#planetary-industry-tasks)).

The same tab also has **Customer orders**: plan the pending orders from the [Order Tracker](order-tracker.md), netted against what is already built or in production. It isn't a source of its own — it adds demand that the industry and material-purchase sources plan for.

### Planetary Industry tasks

Built from the same figures as the [Planetary Industry](planetary-industry.md) tool, for characters whose **PI** box is ticked in **Settings ▸ Characters**:

- **Restart extractors on *planet*** — ready once the extractors have stopped; while they're still running inside the lead time, it waits, with the time left.
- **Take output off *planet*** — when storage is full, fills within the lead time, or is half full of output or more. Several colonies of one character in one system become one stop (**Take output off 3 planets in *system***), with a list of what to pick up.
- **Bring input to *planet*** — a factory planet whose input has run out or runs out within the lead time. The list is enough input for a set number of days of running.
- **Set up a colony** — a character with a free colony slot.
- **Upgrade the command center on *planet*** — when **Command Center Upgrades** allows a higher level.
- **Open *planet* in the game** — a colony whose data is too old to trust, when no other task will take you there anyway.

Storage and input times are estimates; a task built from old colony data says so. The lead times, the age limit and the days of input are set in **Settings ▸ Industry** and shared with the Overview's PI alerts. Turning those alerts off on **Settings ▸ Alerts** doesn't hide the tasks — use the **Planetary Industry** source switch for that.

### Asset safety tasks

When an Upwell structure is destroyed or abandoned, what you had inside goes into **asset safety** as a wrap. For the first five days nothing can be done; then you may choose a station to deliver it to, until a deadline. After that the game delivers it itself, at a higher fee.

The Worklist lists the wraps still waiting for that choice — one task per owner and deadline, with the deadline in the title:

*Station* — **choose a destination for 1 asset safety wrap by 12 Oct 23:28**

- Wraps with different deadlines are separate tasks.
- Before the five days are up, the task waits, with the date it can be delivered from.
- A wrap past its deadline raises no task: there is nothing left to choose.
- A wrap already delivered to a station isn't listed.

Each wrap is matched to its owner's own asset safety notification for its deadline. A corporation's wraps are matched to the notifications its characters received for it. Choosing a destination in the game takes the wrap out of asset safety, so its task drops off at the next asset update.

## Hauling

The **Logistics** source turns "this job's inputs are somewhere else" into trips. Each trip is one of three kinds, and each kind is set up on its own on **Config ▸ Hauling** (see [Setting up hauling](#setting-up-hauling)):

| Kind | What it covers |
| --- | --- |
| **Haul — in system** | Moving things between structures in one system, as jobs finish. Planned as a loop, from where the pilot is now, in the ship they're in. |
| **Haul — nearby** | Trips to systems up to the jump limit (15 gate jumps unless you change it). |
| **Haul — long distance** | Anything further, or with no gate route — usually the market hubs. |

Distances are counted in stargate jumps only; jump bridges aren't included. A wormhole, or a structure whose system isn't known, is long distance.

### Trips between systems

A nearby or long-distance haul is one task per pair of stations, carrying everything that station wants from that source. The row shows the route (*Jita IV - Moon 4 - Caldari Navy Assembly Plant → Staging Fortress*), how many items, and how the trip is made — for example:

*Ana Example · Through the gates · 9 jump(s) · Bustard (62,500 m³) · 3 load(s)*

That is the pilot, the method, the gate jumps, the ship with the hold the trip was sized by, and the loads — the volume over the hold, rounded up. With several pilots on the lane the loads are shared: *4 loads, 2 each for 2 pilots*. A hauling service has no ship of yours to size by, so it shows no loads.

Open the row to see its **MANIFEST** first — each item with its quantity, volume and value — and then **WAITING ON THIS**.

With the **Hauling service** method, a trip bigger than one courier contract may hold is split into one task per contract, with the cargo needed most in the first: *12 item(s), contract 1 of 3*.

### In-system loops

Inside one system there's no single far end: every structure can be both a pick-up and a drop-off. So in-system moves are planned as a **loop** — *Loop from Example Fortress* — with the stops in the order to fly them. The row shows the pilot, the ship and its hold, how many stops, and how many turns.

Open the loop to see each stop, numbered, with what comes off and goes on there:

- each stop's totals — *drop off 12,400 m³ · 85.2M* and *pick up 3,100 m³ · 40.1M*;
- a line per item: **Drop off** *item* *quantity* **from** *where it came from*, or **Pick up** *item* *quantity* **for** *where it's going*;
- **turn round** beside a stop that sits behind the one before it, so the ship turns after undocking — the slow part of a freighter's leg.

How the loop is planned:

- **Facing.** A structure faces its closest stargate unless you've recorded its facing in the [Structure Browser](structure-browser.md). The order is chosen to keep turns down, so a freighter and a small industrial can get the same stops in a different order.
- **Where it starts.** From the structure the pilot is docked in, if that's in the system, or from the undock of the one they just left.
- **One loop per pilot on hand.** When two or more of the lane's pilots are online, in the system and sitting in a hauler, the work is shared between them, each planned from their own dock in their own ship. With one or none on hand, it's one loop for whoever is there, or for the lane's first pilot.
- **Each leg stays with its pilot.** Everything from one structure to another rides with the same pilot until it's moved, so a refresh halfway round doesn't hand the rest of your loop to someone else. A leg only moves when its pilot goes offline, leaves the system or leaves their hauler.
- **The same facts give the same plan.** A loop half flown and planned again from where you are now gives the rest of the loop you started.
- A long loop lists its first 60 stops: *The first 60 stops are planned; 1,200,000 m³ more needs further loops.* An item a single unit of which is bigger than the hold can't be planned at all, and the loop says so.

Cargo already in a pilot's hold shows as its own place — *Ana Example's hold* — and is dropped off by that pilot.

### Which trips come first

A trip that carries **everything** a stopped job is short of goes to the top: the job starts when it lands. The loop says so — *Restarts 2 stopped job(s) once the loop is done: Hawk, Harpy.* — and the job under **WAITING ON THIS** reads *starts when the loop is done*. A trip that carries only part of what a job needs says *1 stopped job(s) want part of this cargo but will not start on this load.* Trips of material for planned work rank with that work, never below a restock.

### Ticking hauls off

Assets are read from ESI once an hour, so without help the Worklist would keep sending you for cargo already in your hold. Tick work off as you do it:

- **✓ Hauled** on a loop's stop — what was picked up there counts as in your hold, and what was dropped off counts as delivered. The loop moves on, and jobs waiting on it can start.
- **✓ Hauled** on a trip's **MANIFEST** — the whole cargo counts as at the destination at once. From a staging or drop-off station, the next leg on is planned.
- **✓ Contracted** on a hauling service's trip — opens the **Contracted** dialog, which starts as the plan. Change quantities, take off what you left out, or paste the contract's items copied in game and click **Replace all** (or **Add** to add them). **Record** keeps it with the courier contract: the cargo counts as on its way, so nothing is bought or hauled for it again. Once the contracts update sees the courier, the cargo is kept with it, where you can correct it in the [Contracts](contracts.md) tool. A tick that no courier from the same start to the same end turns up for within a day lapses, and the trip comes back.

A tick holds until the next asset update shows the goods where they are. Nothing is added to your assets.

### Staging and drop-off stations

- **Deliver to** (long distance) — one station every long-distance haul goes to, as one task per source. The nearby and in-system hauls take the cargo on from there once it has landed. Leave it on **Each item's own station** to haul straight to where each item is needed.
- **Drop-off station per system** (nearby) — when one source has cargo for more than one station in a system, it's hauled to that system's drop-off station as one task, and the in-system loop hands it out from there. Cargo for a single station still goes straight to it, and a system without a drop-off is always hauled to directly.

A trip that stops short says where its cargo goes next: *Then on from there to Example Fortress.*

### Setting up hauling

**Config ▸ Hauling** says how each kind of trip is made and who flies it. It saves as you change it, and the list rebuilds a moment later.

1. **Nearby means up to** *15* **gate jumps** — anything further is long distance.
2. For each kind of trip:
    - **Method** — **Through the gates**, **Bridged freighter**, **Jump freighter** or **Hauling service**. In system there's nothing to choose: you fly it. Nearby starts on **Through the gates**, long distance on **Hauling service**.
    - **Ship** — the hull to size trips by, or **Pilot's current ship** (the default), read from the game for the first pilot listed. Not shown for a hauling service, which flies its own ships.
    - **Hold (m³)** — leave it empty to use the ship's own hold. The pilot's current ship is sized as fitted and flown, expanders and skills included; enter a figure to plan with a different one.
    - **Per contract (m³)** — hauling service only: the most one courier contract may hold. Leave it empty for 350,000 m³.
    - **Pilots** — who flies this kind of trip, in order. The first is the **Primary**, used when only one is needed. Pick from **Add a pilot…**; use the arrow to move a pilot up the list and **✕** to remove one. Only pilots listed here are planned for — a character who happens to be online in a freighter isn't.
    - **Deliver to** (long distance) and **Drop-off station per system** (nearby) — see [Staging and drop-off stations](#staging-and-drop-off-stations). The stations offered are the ones your operation already uses: structures the Structure Browser knows, your corporations' own, and NPC stations where you have something.

!!! tip
    For an in-system loop, untick **Auto refresh** before you undock. A rebuild replans from where every pilot is now, and with the stops ticked off as you go you can press **Refresh** whenever you want the rest of the loop.

## How stock is counted

With the default timers, assets are read from ESI once an hour, but industry jobs and contracts every five minutes. So that a task never relies on an out-of-date hangar, the Worklist corrects the last asset snapshot for what has happened since:

- **Jobs delivered** since the snapshot — their output is counted where it was delivered.
- **Contracts made** since the snapshot — the goods they offer are no longer on hand.
- **Contracts deleted** since the snapshot — the goods are back.
- **Item exchange contracts accepted** since the snapshot — the acceptor gains what was offered and loses what was asked for; the issuer gains what was asked for.
- **Courier contracts delivered** since the snapshot — the goods are counted at the destination, as the issuer's.
- **Hauls ticked off** on the Worklist since the snapshot — delivered goods are counted where they were put down; goods picked up and not yet put down stay counted where they were, so nothing is bought again while you carry them (see [Ticking hauls off](#ticking-hauls-off)).
- **Courier cargo entered by hand** — while the courier is out, its cargo counts as on its way to the destination, so nothing is bought or hauled for it again; once it's delivered, it counts as there. It isn't on a shelf yet, so a job waiting on it doesn't start until it lands.

Each correction is measured against the asset snapshot of the character or corporation whose hangar the goods left or reached, and a count never goes below zero. The same corrections apply in [Inventory Levels](inventory-levels.md), the [Order Tracker](order-tracker.md) and sale postings. The [Assets](assets.md) tool shows the snapshot itself.

!!! note
    Five of the Worklist's sections are also available as panels on the [Overview](overview.md) dashboard, so the most important work shows up there without opening the tool.

## Setting it up

Because the Worklist is assembled from other tools' data, a little configuration makes it far more useful.

1. **Open Config ▸ Sources** and turn on the sources you want to see. Each source is independently switchable, so you can start with just industry jobs and material purchases and add more as you go.
2. **Feed the sources that need data:**
    - Configure your stockpile targets in [Inventory Levels](inventory-levels.md) so *inventory levels* shortfalls appear.
    - Declare your recurring buy orders in [Standing Buy Orders](standing-buy-orders.md) so *standing buy orders* tasks appear.
    - Keep your [Indy Parks](../industry-parks.md) and [Production Calculator](production-calculator.md) plans current so *material purchases*, *industry jobs* and *invention and copying* reflect what you're actually building. **Plan against park** on the Config tab picks the park; **&lt;Default&gt;** follows your default park. The list picks up park changes at once, and a chosen park that's deleted goes back to **&lt;Default&gt;**.
    - Corp *projects*, *asset safety* and *planetary industry* are driven by ESI data the app already syncs.
    - On **Config ▸ Hauling**, list the pilots who haul and how each kind of trip is made (see [Setting up hauling](#setting-up-hauling)).
3. **Set your markets** ([Configuring Markets](../configuring-markets.md)) so the Value column and any price-based decisions are meaningful.
4. **Refresh** to rebuild the list, then use the **Station Needs** tab to plan runs.

## Using it

1. Click **Refresh** to rebuild the list against your latest synced data.
2. Narrow it down with the **State / Type / Character / Source / Destination** filters or the search boxes — for example, show only *buy* tasks for one character.
3. Work the tasks, using **Station Needs** to batch everything at a location. Tick hauls off with **✓ Hauled** or **✓ Contracted** as you go.
4. Use **Show blocked / waiting** to see what's queued behind upstream work, and **Show snoozed** to review anything you've set aside.

## Notes

- The Worklist reads only your **local database**, so it rebuilds quickly — but it is only as complete as your last ESI sync and your configuration of the feeder tools above.
- Data covers your **authorized characters** and **personal corporations**.
- Known gap (Beta): the Worklist's five science-related settings run on sensible defaults but do not yet have their own controls in the UI.
