# Production Calculator

Plan a production run end to end: queue the items you want to build, and get the full material shopping list, a multi-level job breakdown, and the build-cost-versus-market profit for each product. The left-nav label is **Production Calc**.

Open it from the left sidebar under **Industry**.

## What it shows

The screen is split into an input panel on the left and a tabbed results area on the right.

### Input panel

- **Indy Park** — the industry park whose blueprint ME/TE, skills and structure bonuses are used for the calculation. Your default park is selected automatically. The list updates as soon as you add, rename or delete a park in [Indy Parks](../industry-parks.md); the park you chose stays chosen, and if it's deleted the default park takes its place.
- **Add Item** — a search box that only offers items you can actually build (types that are the output of a manufacturing or reaction blueprint); raw materials and blueprints are excluded.
- **Quantity** and **ME Level** — for the item being added. ME starts at the usual level for the item's kind of blueprint; change it before adding if yours differs.
- **Production Queue** — the list of items to build, each with its icon and name. Change an item's quantity or **ME** right in the queue; **✕** takes it off, and **Clear** empties the queue and the results with it. Adding an item that's already queued adds to its quantity.
- **Include BPC cost** — see [Notes](#notes).
- **Calculate** — runs the plan.

When you change the queue, the park or **Include BPC cost** after calculating, a bar above the results says *The queue has changed since these results were calculated*, with a **Recalculate** button.

### Results tabs

- **Summary** — headline figures first: **Net cost**, **Market value**, **Profit**, **Margin**, **Raw material volume** and **Job time**. **Job time** is the longest chain of jobs that must run one after another — how soon the plan could be done with a slot for every job — with every job's time added up beneath it. Job times assume all-V skills and TE twice the ME (up to 20), in the structures the plan placed each job in. Below the headline: the cost summary (Raw Materials, Job Costs, Leftover Value, Net Cost, Raw Material Volume) and a card per final product with requested/produced quantities, material and job cost, unit cost, market unit price, profit and margin.
- **Raw Materials** — every base material to buy, with **Quantity**, **Volume** (packed volume of the whole quantity), **Missing**, **Unit Price** and **Total Cost**. **Missing vs** compares against stock at each job's facility (**Station**) or everything you own (**All assets**). **Shopping List** copies every material; **Shopping List (Missing)** copies only what's short; **Export** copies or saves all columns (clipboard, CSV, or tab-delimited).
- **Final Products** — a grid of the queued products with Req, Produced, ME, Mat Cost, Job Cost, Unit Cost, Total Cost, Market/Unit, Profit and Margin.
- **Intermediates** — the sub-components built along the way, with quantities needed/produced, leftover, **Produced value** (everything the job makes, at build value) and leftover value.
- **Leftovers** — items produced in excess (batch/run rounding), with their source, quantity and build-cost value.
- **Jobs** — every job in the plan, in one of two views (the one you pick is remembered):
    - **Hierarchy** — each job under the job that needs what it makes. Each job shows its blueprint, runs, time, input and output volume, and material and job cost. Expand a job's **Materials** to see each input's base and effective quantity per run, total, what's missing at the job's facility, cost, source and the SDE-base-to-result formula. Shared sub-jobs needed by more than one parent (fuel blocks, reactions, etc.) appear once at the tree root rather than being duplicated.
    - **By station** — each job under the facility it runs at. Stations start closed. Each station lists its jobs, their time, how many materials they need and what they cost, and how many are short — or **Everything on hand**. Its **Materials** list what the station's jobs need between them: **Needed**, **On hand** (how much of the need is there, never more than the need), **Missing**, **Cost** and **Source** (**Buy**, **Built here** or **Built elsewhere**). A material another job at the same station makes is never short. Each station has its own **Shopping List** and **Shopping List (Missing)**.

Every copy button shows **Copied to clipboard** in the middle of the window for a moment, or **Nothing to copy** when there's nothing to copy.

## Using it

1. Pick your **Indy Park**.
2. Type in **Add Item**, choose a result, set **Quantity** and **ME Level**, and click **Add to Queue**. Repeat for as many items as you want to plan together.
3. Check **Include BPC cost** (see [Notes](#notes)).
4. Click **Calculate**.
5. Review the tabs — start with **Summary** for the bottom line, use **Raw Materials** to generate a shopping list, and drill into **Jobs** to see how each number is derived. Switch **Jobs** to **By station** to shop and haul for one facility at a time.
6. Adjust quantities or ME in the queue and click **Recalculate** to compare.

Click an item name (or double-click a grid row) anywhere in the results to open that item in the Item Browser. The status line under Calculate reports the job and raw-material counts when done.

## Notes

- **Include BPC cost** counts blueprint copies (at their contract price) as an input: the final product's, and those of any item in the plan that can only be built from a copy (faction and other BPC-only items). Queuing a BPC-only item ticks it for you. Untick it to see the build without any copies; the **Summary** then lists **Blueprint copy costs left out**, and the totals don't include them.
- **Build or buy components** — by default the calculator builds every component it can and buys only items that can't be costed. To buy a component instead when its market value is at or below a share of its build cost, turn on **Purchase a component instead of building when its market value is ≤ N % of build value** in **Settings ▸ Industry** (see [Build costs](../configuring-markets.md#build-costs)).
- Accurate costs require a configured market for prices ([Configuring Markets](../configuring-markets.md)) and an industry park for the build parameters ([Indy Parks](../industry-parks.md)).
- A category the park leaves unassigned is costed at the park's [default facility](../industry-parks.md#the-default-facility), with that system's cost index, the facility's tax and its role bonus (but no rig bonus). Versions before 0.9.15 costed such jobs with no facility at all, so **Job Costs** for them may now be higher.
- Item icons are fetched from the EVE image server, so they may take a moment to appear.
- To scan across many items for the best things to build, use [Industry Opportunities](industry-opportunities.md); to track jobs you've started, use [Industry Jobs](industry-jobs.md).
