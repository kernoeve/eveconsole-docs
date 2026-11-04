# Worklist

The Worklist is a single, always-current list of **what to do next** across all of your authorized characters and personal corporations. It is rebuilt from scratch on every refresh by pulling from up to twelve independent sources — industry jobs, completed jobs, logistics, invention and copying, material purchases, refining, standing buy orders, inventory levels, corp projects, skill queues, asset safety and planetary industry — and turning each into a concrete task. For work that can't start, it says what really stops it.

Open it from the left sidebar under **General**.

## What it shows

The tool has several tabs: **Worklist** (the task list), **Station Needs** (the same work rolled up by location), **Item Needs** (rolled up by item — what still has to be made), **Bottlenecks** (what's holding work up), **Final Products** (a record of what the work has produced), and **Config** (which sources are on and how they behave — see [Config tab](#config-tab)).

### Worklist tab

- A **Refresh** button, an **Auto refresh** box, and a "Refreshed *hh:mm*" timestamp — the list is regenerated each time. With **Auto refresh** ticked (the default), the list rebuilds itself every few minutes. Untick it while you fly a hauling loop, so the plan doesn't change under you; **Refresh** still rebuilds it.
- A **summary** of how the work stands — see [The summary](#the-summary) below.
- Two toggles: **Show blocked / waiting** (tasks that can't be done yet — e.g. waiting on an upstream job — with their own count) and **Show snoozed** (tasks you've set aside). These only change what's on screen, so they don't plan the list again or reshuffle it.
- A row of **filters**: **State**, **Type**, a **Search task** box, **Character**, **Source**, **Destination**, and a **Search note** box.
- The **task list**, grouped by task type (Buy, Haul — in system, Haul — nearby, Haul — long distance, Manufacturing, Reactions, PI, …). Each row shows the task itself — the item and quantity, the station/structure it applies to, and the responsible character — plus a **Value** and a **Volume** column. Hover the **ⓘ** marker for the full reasoning: a line to a sentence, with a picture beside each item it names.
- An **icon** on each row: the item's own, or for a task with no item, a picture of what it's about — the ore for a refining task, the character's portrait for a skill queue or **Set up a colony** task, the planet for a task on one colony, and the station for an asset safety task. A blueprint is named and drawn as what it is, **(Copy)** or **(Original)**, wherever it appears.

A row with more to say has a **+** in front of it. Click it and the row opens in place, in the grid, with its detail as rows beneath it:

- the task's reason, in one or two lines;
- for a haul, the **MANIFEST** (what to load) or the loop's stops — see [Hauling](#hauling);
- **WAITING ON THIS** — the jobs held up by this task, each with its verdict in colour: green where this task starts the job (see [What a trip does for the jobs waiting on it](#what-a-trip-does-for-the-jobs-waiting-on-it)).

Click **−** to close it again.

#### The summary

The top of the tab says how the work stands. Each figure adds up to its headline. Click a figure to show only what it counts, and click it again to clear it. A figure that counts blocked tasks turns **Show blocked / waiting** on while it's picked, so it never narrows the list to nothing. Nothing is planned again, so the figures respond at once.

- **Slots** lead, because they decide whether the rest can start at all: for example *Reaction slots 181/181 full* or *Manufacturing slots 240/300, 60 free*, with full ones first. Click a full one to see what's waiting on it, or one with room to see what can start in it.
- **Do now** — the tasks you can do this minute, divided into **deliver**, **buy**, **haul**, **manufacturing**, **reactions**, **science** and any other kinds on the list.
- **Blocked** — tasks that can't start, by their true cause: **short of materials**, **blueprints all in use**, **no blueprint here** and **other**.
- **No free slot** — jobs that could start but for a slot, by **reactions**, **manufacturing** and **science**. These rows read **No free slot** in the **State** column.
- **Not due yet** — shown only when there are any: tasks waiting on a timer, which ask nothing of you.
- **Best next moves** — the first few tasks to do, whatever their kind, since the list below is grouped by kind. Finished jobs to deliver come first, then what restarts the most stopped work, then the plan's order. Each names its errand (**Buy**, **Haul**, **Build**, **React**, **Copy**, **Invent** or **Deliver**) and how many jobs it frees. Click one to go to that task in the list.
- A small line says what changed: *Since last refresh: 12 newly ready, 3 no longer ready*.

### Station Needs tab

The same outstanding work aggregated **by station/structure**, so you can see everything that needs buying or moving at a given location in one place — useful when planning a shopping or hauling run.

### Item Needs tab

The outstanding work aggregated **by item** — what still has to be *made*, with the tasks waiting on each item beneath it. Where Station Needs answers "what does this place want," Item Needs answers "what do I still have to produce," so it counts production rather than just what a station holds.

### Bottlenecks tab

What's holding the rest of the work up. Each sub-tab answers a single question — **Slots**, **Item Contention**, **BPO / Formula**, and **Hauling** — and a **Summary** ranks the *actions* themselves by how much work each one is blocking (for example "raise level 200 to 570", or "buy 1 of 4 owned (+25% output)"). Every "how much does this hold up" figure is measured by walking the actually-blocked tasks, not the recipe tree, so it reflects work you're really doing rather than everything a recipe could theoretically need. Open a row to see the tasks behind it. Numeric columns sort as numbers.

- **Summary** — its status line judges free slots pool by pool: free science slots say nothing about reactions. It points at prints only where that pool has slots to spare and jobs are stopped on them now.
- **Hauling** — the hauls holding up the most work, by the jobs they restart, using the [haul plan](#hauling)'s own figures, so it never asks you to draw a station below its own need. Hauls already raised and ready to fly are listed too, and the card says which: *8 haul(s) holding up 222 job(s). Every one of them is on the worklist: flying them restarts the work.* A haul of a single item is titled with that item.
- **Item Contention** — shortages of items you own that no trip can solve. A shortage is on **Hauling** when a haul brings it or the plan finds it spare elsewhere, and on **Item Contention** otherwise, so each is on exactly one.
- **BPO / Formula** — one line per *use*, because originals at the copy lab and those elsewhere can't stand in for each other. **Use** says **Build**, **Copy**, or **Build + copy** for the only original of a type, which does both. Each line has its own contention, rank and verdict.
    - **All busy** and **Used** count only jobs on those originals, all activities included, measured from the line's first job rather than the whole 90 days, and never over less than 30.
    - **Rank** goes by the worse of the last 90 and 30 days, and 90% or more counts as tight.
    - The **No free slot** verdict marks jobs that another print wouldn't start, because what they're waiting on is a slot.

### Final Products tab

A record of **what the work has produced**: every job — finished or still running — whose output is something your operation sells. A job's value is taken as of the day it completed, and can be read either as **market value** or as a **fixed percentage over build cost** (a shop selling at a set margin never sees the market price). Profit is shown as *potential* profit throughout, because nothing on this tab has actually been sold yet.

### Config tab

How the list is built, in sub-tabs:

- **Sources** — which sources are on (see [The sources](#the-sources)).
- **Market** — where shortfalls are bought, and which character keeps orders at each station.
- **Inventory Rules** — when a group from [Inventory Levels](inventory-levels.md) falls below **Trigger below (%)**, what to do about it at which station, and how far to **Fill up to (%)**.
- **Station Levels** — where each group's stock should live; this raises hauling only (see [Station levels](#station-levels)).
- **Hauling** — how each kind of trip is made and who flies it (see [Setting up hauling](#setting-up-hauling)).
- **Other** — the park to plan against, the asset scope, job lengths, how long materials are held for a busy blueprint (see [What stops a job](#what-stops-a-job)) and corp project owners.

A fill target above 100 % is rounded down, so it never adds more than its percentage: a level of 1 at 110 % stays 1, and 10 at 110 % is 11. Below 100 % it's rounded up, so filling to 80 % of 1 still means 1.

## The sources

Each source can be switched on or off independently on **Config ▸ Sources** (see [Setting it up](#setting-it-up)). A source that is off is skipped entirely.

- **Industry Jobs** — jobs to start.
- **Completed Jobs** — one **Deliver** task for all your finished jobs, at the top of the jobs, listing each output with its pilot and station. Delivering frees the slot and puts the output in the hangar, so it comes before starting anything new. A job installed by someone who isn't one of your characters is left out.
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

Storage and input times are estimates. The lead times and the days of input are set in **Settings ▸ Industry** and shared with the Overview's PI alerts. Turning those alerts off on **Settings ▸ Alerts** doesn't hide the tasks — use the **Planetary Industry** source switch for that.

### Asset safety tasks

When an Upwell structure is destroyed or abandoned, what you had inside goes into **asset safety** as a wrap. For the first five days nothing can be done; then you may choose a station to deliver it to, until a deadline. After that the game delivers it itself, at a higher fee.

The Worklist lists the wraps still waiting for that choice — one task per owner and deadline, with the deadline in the title:

*Station* — **choose a destination for 1 asset safety wrap by 12 Oct 23:28**

- Wraps with different deadlines are separate tasks.
- Before the five days are up, the task waits, with the date it can be delivered from.
- A wrap past its deadline raises no task: there is nothing left to choose.
- A wrap already delivered to a station isn't listed.

Each wrap is matched to its owner's own asset safety notification for its deadline. A corporation's wraps are matched to the notifications its characters received for it. Choosing a destination in the game takes the wrap out of asset safety, so its task drops off at the next asset update.

## What stops a job

Jobs are judged in plan order, and each names the thing that really stops it rather than a knock-on effect of something else. The questions come in this order:

1. **Is there a slot?** A job blames a blueprint only if a slot would be free for it after the jobs ahead of it. Otherwise it reads **No free slot**, and buying another print wouldn't start it.
2. **Is there a blueprint?** A blueprint is busy only when every print at the site is running or going to a job that can start now: *Every blueprint here is in use: 3 running, 1 about to start*. Other reasons say what's wrong: *No usable blueprint at Example Fortress (best owned: …)*, *No blueprint owned — one has to be acquired*, or *Its blueprint is held for an earlier job that is short of materials*.
3. **Are the materials there?** A job is short only against jobs that can really start. Jobs still queued don't spend stock on paper, and a job with no slot or print reads as short only when not one run could go. What a job lacks is always listed.

In the [summary](#the-summary), a blueprint reason counts as **blueprints all in use** or **no blueprint here**, and the third question as **short of materials**.

**Stock already at a site is held for that site's work.** Only what's left over counts as haulable elsewhere. A shortage that nobody can spare reads **None to spare**, with anything that can be hauled listed after it: *None to spare in Example Fortress: Morphite; elsewhere: Tritanium*.

**Materials can be held for a busy blueprint.** Suppose a job ranked ahead can start only once its blueprint comes out of a running job. If that job ends soon, the materials at the site are held for it, so jobs ranked below don't use them up in the meantime. It holds one job's worth for each print that frees in time, and the job's reason says so. Set how soon on **Config ▸ Other**: **Hold materials for a busy blueprint freeing within** *24* **hours**. **0** turns it off.

A blueprint on a courier, or bought on a contract and not yet polled, counts as owned, so it isn't asked for again. Ore and compressed gas on a courier still count toward what they turn into, so their minerals and gas aren't bought again. Containers don't count as raw material, and a copy spent by a delivered job isn't handed out again.

## How the work is ranked

Slots and scarce materials go to whatever unblocks the most finished goods, not to whatever looks lowest:

- **Parts are ranked by the final jobs they stop.** A blocked final or ordered job credits what it must have built, and their inputs while those are at least as short. A part no planned final is short of holds nothing up today, however low its stock.
- **A waiting hull counts for the input holding it up**, not for every input it uses. So an empty material that four hulls are stopped for beats a part-stocked one that feeds fifteen.
- **An order's urgency is passed down only for what the parent's stock doesn't cover.**
- **A final's high rank applies only while a sold job is actually stopped** for the part.

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

With the **Hauling service** method, a trip bigger than one courier contract may hold is one task that opens into its contracts, with the cargo needed most in the first: *12 item(s) in 3 contracts*. Each **CONTRACT 1 OF 3** in the opened row has its own manifest and its own tick.

### Capital hulls

A capital can't go in anyone's cargo, so a hull is never part of a load. Each is its own **Fly** task for a pilot to fly, jumping if the systems are apart: *Fly Chimera × 1*.

A hull only goes where it can dock:

| Hull | Docks at |
| --- | --- |
| Carriers, dreadnoughts, force auxiliaries and other standard capitals | NPC stations, Fortizars, Sotiyos and Keepstars |
| Supercarriers and titans | Keepstars only |

A structure of unknown type counts as one it can't dock at. Freighters, Orcas and Bowheads dock anywhere, and subcapitals go as cargo.

A hull wanted at a site it can't dock at is met only from that site, and is built there. So the T1 hull for a T2 capital built in an Azbel is built in that Azbel and not undocked. The job says so: *Chimera cannot dock at Example Azbel: it has to be built there and not undocked*.

### Blueprints

Originals aren't moved because the ones already at a site are busy: a busy print comes back to the same hangar when its job ends. The copy lab (the structure your park assigns to copying) keeps its own originals where they are, unless one is the only original of its type you own. Then a factory with none can take it, rather than nothing being built at all.

### Station levels

**Config ▸ Station Levels** says where stock should live. A level works in two directions:

- **As a source**, a station never goes below its level. With a level of 1,000 and 2,000 in the hangar, other stations can draw 1,000. One large need can't empty every buffer.
- **As a destination**, a level pulls stock in only when no job anywhere still wants that item, whether or not that job could start today. Jobs always fill first.

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

### What a trip does for the jobs waiting on it

**WAITING ON THIS** works through the jobs in plan order against one pile per item, so the same units are never promised twice. Each line gives the units, and a build the cargo only partly covers is split into what starts and what doesn't:

| Reads | Meaning |
| --- | --- |
| **starts on arrival** / **starts when the loop is done** | The cargo covers what those units lack, and a slot and a print are free for them. |
| **starts once the other loop is done too** | It needs another loop in this system as well. |
| **then waits for a slot** / **then waits for a blueprint** | The cargo covers those units, but they would stop again for a slot or a print. |
| **needs 3 more items** | Still short of something else after this. Hover it to see each item, how many and their m³. |
| **nothing else missing** | A build the trip was raised for, with nothing else lacking. |

A build is measured on its own needs, not the whole station's. Cargo is judged where it's bound, not where the trip stops, and a job is listed only for something it's actually short of.

### Ticking hauls off

Assets are read from ESI once an hour, so without help the Worklist would keep sending you for cargo already in your hold. Tick work off as you do it:

- **✓ Hauled** on a loop's stop — what was picked up there counts as in your hold, and what was dropped off counts as delivered. The loop moves on, and jobs waiting on it can start.
- **✓ Hauled** on a trip's **MANIFEST** — the whole cargo counts as at the destination at once. From a staging or drop-off station, the next leg on is planned.
- **✓ Contracted** on a hauling service's trip, or on each of its contracts — opens the **Contracted** dialog, which starts as the plan. Change quantities, take off what you left out, or paste the contract's items copied in game and click **Replace all** (or **Add** to add them). **Record** keeps it with the courier contract: the cargo counts as on its way, so nothing is bought or hauled for it again. Once the contracts update sees the courier, the cargo is kept with it, where you can correct it in the [Contracts](contracts.md) tool. A tick that no courier from the same start to the same end turns up for within a day lapses, and the trip comes back.

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
2. Read the [summary](#the-summary): how full the slots are, what can be done, and what's blocked and why. Click a figure to see those tasks, or a best next move to go straight to it.
3. Narrow it down with the **State / Type / Character / Source / Destination** filters or the search boxes — for example, show only *buy* tasks for one character.
4. Work the tasks, using **Station Needs** to batch everything at a location. Tick hauls off with **✓ Hauled** or **✓ Contracted** as you go.
5. Use **Show blocked / waiting** to see what's queued behind upstream work, and **Show snoozed** to review anything you've set aside.

## Notes

- The Worklist reads only your **local database**, so it rebuilds quickly — but it is only as complete as your last ESI sync and your configuration of the feeder tools above.
- Data covers your **authorized characters** and **personal corporations**.
- Known gap (Beta): the Worklist's five science-related settings run on sensible defaults but do not yet have their own controls in the UI.
- Known gaps in the reasons a job gives:
    - **starts on arrival** overstates it when cargo stops at a staging station and needs another leg first. It checks that a slot was free when the job was planned, not that there are enough for all of them.
    - A job can say *elsewhere* when the only stock elsewhere is protected by a station level, so it won't be hauled.
    - A station's own queued jobs always keep its stock, even from a higher-priority job elsewhere.
    - A blueprint on a courier counts as one run, and an original as a one-run copy, until it arrives.
    - The hold for a busy print can still make a later job look short of materials.
