# Worklist

The Worklist is a single, always-current list of **what to do next** across all of your authorized characters and personal corporations. It is rebuilt from scratch on every refresh by pulling from up to nine independent sources — industry jobs, logistics, invention and copying, material purchases, standing buy orders, inventory levels, corp projects, skill queues and asset safety — and turning each into a concrete task.

Open it from the left sidebar under **General**.

## What it shows

The tool has several tabs: **Worklist** (the task list), **Station Needs** (the same work rolled up by location), **Bottlenecks** (what's holding work up), **Final Products** (a record of what the work has produced), and **Config** (which sources are on and how they behave — see [Setting it up](#setting-it-up)).

### Worklist tab

- A **Refresh** button and a "Refreshed *hh:mm*" timestamp — the list is regenerated each time.
- A **summary strip** of counts: a large **ready now** total, and a breakdown by task type (for example **buy**, **haul**, **manufacturing** and **reactions**).
- Two toggles: **Show blocked / waiting** (tasks that can't be done yet — e.g. waiting on an upstream job — with their own count) and **Show snoozed** (tasks you've set aside).
- A row of **filters**: **State**, **Type**, a **Search task** box, **Character**, **Source**, **Destination**, and a **Search note** box.
- The **task list**, grouped by task type (Buy, Haul, Manufacturing, Reactions, …). Each row shows the task itself — the item and quantity, the station/structure it applies to, and the responsible character — plus a **Value** and a **Volume** column, and a per-row info control for more detail.

### Station Needs tab

The same outstanding work aggregated **by station/structure**, so you can see everything that needs buying or moving at a given location in one place — useful when planning a shopping or hauling run.

### Bottlenecks tab

What's holding the rest of the work up. Each sub-tab answers a single question — **Slots**, **Item Contention**, **BPO / Formula**, and **Hauling** — and a **Summary** ranks the *actions* themselves by how much work each one is blocking (for example "raise level 200 to 570", or "buy 1 of 4 owned (+25% output)"). Every "how much does this hold up" figure is measured by walking the actually-blocked tasks, not the recipe tree, so it reflects work you're really doing rather than everything a recipe could theoretically need.

### Final Products tab

A record of **what the work has produced**: every job — finished or still running — whose output is something your operation sells. A job's value is taken as of the day it completed, and can be read either as **market value** or as a **fixed percentage over build cost** (a shop selling at a set margin never sees the market price). Profit is shown as *potential* profit throughout, because nothing on this tab has actually been sold yet.

## The nine sources

Each source can be switched on or off independently (see [Setting it up](#setting-it-up)):

- **Industry jobs** — jobs to start or collect.
- **Logistics** — items that need hauling between locations.
- **Invention and copying** — invention and blueprint-copy jobs.
- **Material purchases** — inputs to buy for planned builds.
- **Standing buy orders** — see [Standing Buy Orders](standing-buy-orders.md).
- **Inventory levels** — restock shortfalls, from [Inventory Levels](inventory-levels.md).
- **Corp projects** — deliveries toward corp standing projects.
- **Skill queues** — characters whose skill queue needs attention.
- **Asset safety** — assets in asset safety that need handling.

!!! note
    Five of the Worklist's sections are also available as panels on the [Overview](overview.md) dashboard, so the most important work shows up there without opening the tool.

## Setting it up

Because the Worklist is assembled from other tools' data, a little configuration makes it far more useful.

1. **Open the Config tab** and turn on the sources you want to see. Each of the nine sources above is independently switchable, so you can start with just industry jobs and material purchases and add more as you go.
2. **Feed the sources that need data:**
    - Configure your stockpile targets in [Inventory Levels](inventory-levels.md) so *inventory levels* shortfalls appear.
    - Declare your recurring buy orders in [Standing Buy Orders](standing-buy-orders.md) so *standing buy orders* tasks appear.
    - Keep your [Indy Parks](../industry-parks.md) and [Production Calculator](production-calculator.md) plans current so *material purchases*, *industry jobs* and *invention and copying* reflect what you're actually building.
    - Corp *projects* and *asset safety* are driven by ESI data the app already syncs.
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
