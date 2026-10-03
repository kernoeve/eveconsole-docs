# Worklist

The Worklist is a single, always-current list of **what to do next** across all of your authorized characters and personal corporations. It is rebuilt from scratch on every refresh by pulling from up to eleven independent sources — industry jobs, logistics, invention and copying, material purchases, refining, standing buy orders, inventory levels, corp projects, skill queues, asset safety and planetary industry — and turning each into a concrete task.

Open it from the left sidebar under **General**.

## What it shows

The tool has several tabs: **Worklist** (the task list), **Station Needs** (the same work rolled up by location), **Item Needs** (rolled up by item — what still has to be made), **Bottlenecks** (what's holding work up), **Final Products** (a record of what the work has produced), and **Config** (which sources are on and how they behave — see [Setting it up](#setting-it-up)).

### Worklist tab

- A **Refresh** button and a "Refreshed *hh:mm*" timestamp — the list is regenerated each time.
- A **summary strip** of counts: a large **ready now** total, and a breakdown by task type (for example **buy**, **haul**, **manufacturing**, **reactions** and **PI**).
- Two toggles: **Show blocked / waiting** (tasks that can't be done yet — e.g. waiting on an upstream job — with their own count) and **Show snoozed** (tasks you've set aside).
- A row of **filters**: **State**, **Type**, a **Search task** box, **Character**, **Source**, **Destination**, and a **Search note** box.
- The **task list**, grouped by task type (Buy, Haul, Manufacturing, Reactions, PI, …). Each row shows the task itself — the item and quantity, the station/structure it applies to, and the responsible character — plus a **Value** and a **Volume** column, and a per-row info control for more detail.
- An **icon** on each row: the item's own, or for a task with no item, a picture of what it's about — the ore for a refining task, the character's portrait for a skill queue or **Set up a colony** task, the planet for a task on one colony, and the station for an asset safety task.

### Station Needs tab

The same outstanding work aggregated **by station/structure**, so you can see everything that needs buying or moving at a given location in one place — useful when planning a shopping or hauling run.

### Item Needs tab

The outstanding work aggregated **by item** — what still has to be *made*, with the tasks waiting on each item beneath it. Where Station Needs answers "what does this place want," Item Needs answers "what do I still have to produce," so it counts production rather than just what a station holds.

### Bottlenecks tab

What's holding the rest of the work up. Each sub-tab answers a single question — **Slots**, **Item Contention**, **BPO / Formula**, and **Hauling** — and a **Summary** ranks the *actions* themselves by how much work each one is blocking (for example "raise level 200 to 570", or "buy 1 of 4 owned (+25% output)"). Every "how much does this hold up" figure is measured by walking the actually-blocked tasks, not the recipe tree, so it reflects work you're really doing rather than everything a recipe could theoretically need.

### Final Products tab

A record of **what the work has produced**: every job — finished or still running — whose output is something your operation sells. A job's value is taken as of the day it completed, and can be read either as **market value** or as a **fixed percentage over build cost** (a shop selling at a set margin never sees the market price). Profit is shown as *potential* profit throughout, because nothing on this tab has actually been sold yet.

## The sources

Each source can be switched on or off independently on **Config ▸ Sources** (see [Setting it up](#setting-it-up)). A source that is off is skipped entirely.

- **Industry Jobs** — jobs to start or collect.
- **Logistics** — items that need hauling between locations.
- **Invention & Copying** — invention and blueprint-copy jobs.
- **Material Purchases** — inputs to buy for planned builds.
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

## How stock is counted

With the default timers, assets are read from ESI once an hour, but industry jobs and contracts every five minutes. So that a task never relies on an out-of-date hangar, the Worklist corrects the last asset snapshot for what has happened since:

- **Jobs delivered** since the snapshot — their output is counted where it was delivered.
- **Contracts made** since the snapshot — the goods they offer are no longer on hand.
- **Contracts deleted** since the snapshot — the goods are back.
- **Item exchange contracts accepted** since the snapshot — the acceptor gains what was offered and loses what was asked for; the issuer gains what was asked for.
- **Courier contracts delivered** since the snapshot — the goods are counted at the destination, as the issuer's.

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
3. **Set your markets** ([Configuring Markets](../configuring-markets.md)) so the Value column and any price-based decisions are meaningful.
4. **Refresh** to rebuild the list, then use the **Station Needs** tab to plan runs.

## Using it

1. Click **Refresh** to rebuild the list against your latest synced data.
2. Narrow it down with the **State / Type / Character / Source / Destination** filters or the search boxes — for example, show only *buy* tasks for one character.
3. Work the tasks, using **Station Needs** to batch everything at a location.
4. Use **Show blocked / waiting** to see what's queued behind upstream work, and **Show snoozed** to review anything you've set aside.

## Notes

- The Worklist reads only your **local database**, so it rebuilds quickly — but it is only as complete as your last ESI sync and your configuration of the feeder tools above.
- Data covers your **authorized characters** and **personal corporations**.
- Known gap (Beta): the Worklist's five science-related settings run on sensible defaults but do not yet have their own controls in the UI.
