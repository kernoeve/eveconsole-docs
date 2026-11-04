# Industry Parks

An **industry park** describes the structures you actually build in, so that
build-cost and production calculations reflect your real bonuses (material
efficiency, rig bonuses, structure type, security modifiers, and facility tax)
instead of generic values.

Open **Indy Parks** from the left sidebar under the **Industry** group. It has two
tabs: **Parks**, where you set your parks up, and **Compare**, which does the same
jobs in several parks and sets the costs and times side by side (see
[Comparing parks](#comparing-parks)).

<details class="tip" open>
<summary>Video walkthrough — Indy Park Setup (7 min)</summary>
<div class="video-embed">
<iframe src="https://www.youtube-nocookie.com/embed/q-i8qI3RvDU" title="EVE Console: Indy Park Setup" loading="lazy" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
</details>

## Key concepts

- **Park** — a named collection of structures plus the rules mapping production
  work to them. One park can be marked the **default** (shown with a ★); that's
  the park used by build-cost calculations and the Production Calculator.
- **Structure** — a single facility in the park. Each has a name, a **type**
  (Raitaru, Azbel, Sotiyo, Athanor, Tatara, or NPC Station), a **solar system**,
  a **security class** (High Sec, Low Sec, Null Sec, or Wormhole), a **facility
  tax %**, up to **three rig slots**, and any number of **service modules**. The
  available rigs adapt to the structure type — engineering complexes
  (Raitaru/Azbel/Sotiyo) offer manufacturing rigs sized to the hull; refineries
  (Athanor/Tatara) offer reaction and reprocessing rigs; NPC Stations take no rigs,
  and their service modules are the station's own (see [NPC stations](#npc-stations)).
- **Actual facility** — the real in-game station or structure a park structure
  describes. Linking one lets EVE Console check the industry jobs running there
  against your rigs, and keeps the park's fitting in step with the real structure.
- **Default facility** — each park has exactly one structure ticked **Default**:
  its catch-all. Any category left unassigned, and any item that no production
  assignment covers, is planned there — with that system's cost index, the
  structure's tax and its hull's role bonus, but **no rig bonus**. This is separate
  from the park-level **★ Set Default**.
- **Production assignments** — map each production **category** (Large Ships,
  Capital Components, Ammo and Charges, the various reaction and reprocessing
  categories, etc.) to the structure that handles it.
- **Item exceptions** — override the category assignment for one specific item
  that doesn't belong with its category's default structure.

Parks feed the system-wide **build cost** EVE Console calculates and stores for
every craftable item, which in turn feeds the [Production Calculator](tools/production-calculator.md)
and the build-cost floor in [market pricing](configuring-markets.md).

> Changes save automatically as you type or pick from a dropdown — there's no
> separate Save button. Stored build costs are recalculated automatically after
> every market refresh. To apply a park change straight away, click **Recalculate
> Build Costs** in **Settings ▸ Industry** (see [Build costs](configuring-markets.md#build-costs)).

## Building a park

1. On the **Parks** tab, click **+ New Park**. It appears in the list on the left;
   select it to edit. Rename it in the **Park Name** box at the top. The first park
   you add (or import) becomes the default park automatically.
2. Add your structures. There are two ways, and you can mix them:
    - **A whole system at once** — see [Adding every structure in a
      system](#adding-every-structure-in-a-system) below. This is the quickest way
      when your structures are ones EVE Console already knows about.
    - **One at a time** — click **+ Add Structure** and fill in its card, as
      described in [Adding a structure by hand](#adding-a-structure-by-hand).
3. Under **Production Assignments**, set each category's dropdown to the structure
   that produces it. A category left on *— not assigned —* is planned at the park's
   [default facility](#the-default-facility).
   Click **Auto-assign from rigs** to fill the empty categories for you (see
   [Auto-assigning from rigs](#auto-assigning-from-rigs)).
4. (Optional) Under **Item Exceptions**, type an item name into the search box,
   pick it from the results to add it, then choose the structure that should build
   that specific item. Remove an exception with its **✕** button.
5. Check which structure is ticked **Default**. It's the catch-all for anything
   left unassigned.
6. To make this the park used everywhere, click **★ Set Default**.

Structure cards are laid out in as many equal columns as the window has room for,
filling left to right and then down. Long rig names are trimmed, with the whole name in
a tooltip.

The park lists in the [Production Calculator](tools/production-calculator.md) and the
[Worklist](tools/worklist.md) update as soon as you add, rename, delete or import a park.

### Deleting a park

Deleting a park asks for confirmation first (**Removal Confirmation**) and says what
goes with it: its structures with their rigs and service modules, its category
assignments and its item exceptions. It can't be undone.

- If the park was the default, the default passes to the first remaining park by
  name, and the confirmation says which.
- If the Worklist had the deleted park chosen, it goes back to **&lt;Default&gt;**;
  the Production Calculator switches to the default park.

<!--
  SCREENSHOT SLOTS (add files to docs/images/, then uncomment):

  ![Industry park setup](images/industry-park.png)
-->

## Adding every structure in a system

The **Structures** toolbar can add every industrial structure in a system in one go.
Each one arrives already linked to the real structure, with its real fitting.

1. Type in the **System…** box and pick the system from the list.
2. Leave **Skip moon refineries** ticked (the default) to leave out Athanors and
   Tataras anchored to a moon, which are usually moon mining rather than industry.
   Untick it to include them.
3. Click **+ Add Missing In System**.

For each structure it adds, EVE Console:

- names the card after the structure and sets its type (Raitaru, Azbel, Sotiyo,
  Athanor, or Tatara; citadels have no industry slots and are never added);
- sets **Solar system** and **Security** from the system;
- links it as the card's [actual facility](#linking-the-actual-facility);
- pulls in its real fitting — rigs and service modules — where the app knows it.

Only structures EVE Console has already resolved a name for can be added. These are
the ones listed in the [Structure Browser](tools/structure-browser.md). A line under
the toolbar reports how many were added, how many were already in the park, and how
many moon refineries were skipped. Structures already linked in this park are left
alone, so pressing the button again, for example after adding one by hand, doesn't
create duplicates.

After a bulk add, set each structure's **Tax Percentage**; it isn't read from the game.

## Adding a structure by hand

Click **+ Add Structure**. The new card starts as *New Structure*, a **Raitaru**.
Fill in:

- **Name** — a label such as *Main Raitaru*.
- **Type** — the structure hull; this determines which rigs are available.
- **Solar system** — type at least two letters and pick the system from the list
  (wormhole systems are included). This sets the system cost index.
- **Security** — set for you from the system's own security (High Sec, Low Sec,
  Null Sec or Wormhole) and locked; its tooltip says so. Rig bonuses scale with
  security. Only a card with no known system lets you choose it by hand.
- **Tax Percentage** — the facility's job tax.
- **Rigs** — pick up to three from the per-type dropdowns (leave a slot on
  *— empty —* if unused).
- **Service modules** — see [Service modules](#service-modules).

Remove a structure with the **✕** button on its card. It asks for confirmation
first (**Removal Confirmation**) and says what goes: the card's rigs and service
modules are deleted, and any category or item exception that sent work to it is left
unassigned. The structure in game isn't affected.

!!! note "Stored system and security are kept right"
    When a park loads, a stored system name or security class that disagrees with the
    system (or with the linked facility) is corrected, since rig strength is planned
    from the stored class.

## Linking the actual facility

The **ACTUAL FACILITY** section of each card says which real station or structure the
card describes. Until you link one, it reads *Not linked — jobs here won't be
rig-checked*.

1. Type part of the station or structure name into **Search station or structure to
   link…** and click **Search**.
2. Click the right result to link it.

Once it's linked, the facility's name replaces the hint. Click the name to open it: an
NPC station opens in [Players & NPCs](tools/entities.md), a player structure in the
[Structure Browser](tools/structure-browser.md). Click **Unlink** to remove the link.

A linked facility decides the card's **Name**, **Type** (its hull, when the app knows
it), **Solar system** and **Security**, and all four lock while the link stands; their
tooltips say why. Unlink it to change them. If linking changes the hull, rigs that no
longer fit it are removed.

Linking also brings the card's fitting into line with the real structure, and the
line at the bottom of the card says which side is in charge:

- **From assets** — your characters can see the structure's fitted modules in their
  assets, so the game is the authority. The card's rigs and service modules follow
  the game and can't be edited here.
- **Entered by hand** — the game doesn't report the fitting, so the card is the
  record. Rigs and service modules you pick here are also written to the linked
  structure.

## Service modules

The **SERVICE MODULES** section lists the service modules fitted to a structure. Every
Upwell hull offers the same list. NPC stations work differently; see
[NPC stations](#npc-stations).

- To add one, pick it from *— add a service module —* and click **Add**. Adding a
  module that's already listed does nothing.
- To remove one, click its **✕**.
- Click a module's name to open it in the Item Browser.

When the fitting comes **from assets**, the list follows the game and can't be edited.

## NPC stations

A card whose **Type** is **NPC Station** takes no rigs, and its service modules and
tax are locked:

- **Service modules** stand for the station's own services. Link the station and
  they're filled in from what it offers, as the Upwell modules that do the same job:

    | Station service | Service module |
    |---|---|
    | Factory | Manufacturing Plant |
    | Laboratory | Research Lab and Invention Lab |
    | Reprocessing | Reprocessing Facility |
    | Market | Market Hub |
    | Cloning | Cloning Center |

- **Tax Percentage** is the game's fixed **0.25%** facility tax.

Industry jobs at NPC stations are never flagged as running without rigs.

## The default facility

Tick **Default** on a structure's card to make it the park's catch-all. Categories
left *— not assigned —*, and items that no production assignment or item exception
covers, are planned at this structure: with its system's cost index, its facility tax
and its hull's role bonus, but no rig bonus. An assignment or exception that points
at a structure no longer in the park falls through to it too.

- A park has exactly one default facility. Ticking **Default** on one structure clears
  it from the others, and you can't untick the current one without ticking another.
- The first structure you add to a park becomes the default automatically.
- If you delete the default structure, the role passes to another structure in the
  park.

## Auto-assigning from rigs

**Auto-assign from rigs**, at the top of **Production Assignments**, fills categories
from the rigs fitted to your structures:

- Only **empty** categories are filled. A category you've already set is left alone.
- A rig made for that exact category beats a broad rig that covers it along with
  others. For example, an Athanor rigged for one reaction type wins that category over
  a Tatara whose rig covers every reaction.
- If more than one structure qualifies, or none does, the category stays empty for
  you to choose.

A line under the button reports how many categories were assigned, how many were
already set, and which were left because more than one structure matched or none did.

## Sharing parks

Use **Export Park** to write the selected park (structures, rigs, service modules,
facility links, assignments, and exceptions) to a JSON file, and **Import** to load
one back — handy for backing up a setup or sharing a corp-standard park with alliance
mates. Imported parks arrive as new entries and never overwrite an existing one.

The file doesn't carry each structure's tax or which one is ticked **Default**, so
check **Tax Percentage** and **Default** after an import. A park imported into an
empty list becomes the default park.

## Comparing parks

The **Compare** tab answers *where is this cheapest and quickest?* It does the same list
of jobs in every park you tick and shows each job's cost and time side by side, along
with what the cost would have been on each past day as system cost indices moved.

1. Under **Parks**, tick the parks to compare. All are ticked to start, and a park you
   add later starts ticked.
2. Under **Jobs to compare**, type at least two letters of an item or blueprint and pick
   it from the list. It becomes a card, with the name on its header strip, **▲** and **▼**
   to move it up and down the list, and **✕** to remove it.
3. On each card, pick the operation and fill in its numbers (see below).
4. Click **Calculate**.

The list of jobs and the parks you left unticked are remembered on this machine.

### Operations

An item offers **Build** and starts on it. A blueprint offers the rest as well, and starts
on **Copy**. Changing the operation fills the boxes with its starting numbers.

| Operation | Offered for | Boxes | Starts at |
| --- | --- | --- | --- |
| **Build** | Any item or blueprint; a blueprint builds what it makes | **Units**, and **ME**: the item's own blueprint ME, 0 to 10 | 1 unit, ME 10 |
| **Copy** | A blueprint | **Runs** on each copy, and how many **Copies** | 10 runs, 1 copy |
| **Invention** | A blueprint that can be invented from | **Runs wanted** of the invented blueprint, and a decryptor | 10 runs, no decryptor |
| **ME research** | A blueprint | **To ME**, 1 to 10 | ME 10 |
| **TE research** | A blueprint | **To TE %**, 2 to 20 | TE 20% |

- **Build** plans the whole chain with the Production Calculator's own costing, in the
  structures each park assigns. Components use the calculator's usual ME.
- **Invention** plans enough attempts to expect the runs wanted, with skills at V, as the
  [Worklist](tools/worklist.md) plans them, plus the copying of the source runs those
  attempts use.
- **Research** starts at ME 0 or TE 0 and goes to the level entered.
- The same blueprint can be listed more than once, each line with its own operation.

### Results

The grid has one row for each job in each park:

| Column | Meaning |
| --- | --- |
| **Item**, **Operation**, **Park** | The job, and where it's done. |
| **Units** | What comes out: units built, copy runs, runs invented, or one researched blueprint. |
| **Materials**, **Job Cost** | What goes in. |
| **Leftovers** | Components made beyond need. They are kept rather than used up, so they come off the total, as in the Production Calculator's **Net Cost**. |
| **Total**, **Per Unit** | Materials plus job cost, less the leftovers. A park that can't do the job reads **Not built here**. |
| **vs Best** | How much dearer than the cheapest park for that job, or **Best**. |
| **Time** | Every job's duration added up, as if run one after another, with skills at V. |
| **vs Best** | How much slower than the quickest park for that job, or **Best**. |
| **Detail** | What the job came to: attempts and chance, copies, or levels. |

Costs use today's prices and indices.

**Summary** is the same results pivoted, so you can read them at a glance. **Rows** chooses
**Jobs** (a row per job, a group of columns per park) or **Parks** (the other way round),
and your choice is remembered. Each group has **Cost**, **vs Best**, **Time** and **vs Best**
under a heading naming the park or job. The best figure for a job is green, and one a
quarter or more behind is red.

### Charts

**Charts for** picks **All items together** or one job. Both charts follow it, and a park
keeps its colour in both.

- **Cost with each day's indices** — a line per park. It takes today's plan, materials and
  taxes and works out the cost again with each day's system cost indices, so only the index
  moves. The note above the charts gives the dates covered. A day with no index for a system
  uses its last known one. The figures come from the same record as the
  [System Index](tools/system-index.md) tool; with none yet, the note says so.
- **Job time per park** — a group of bars per job, a bar per park.

Each chart draws the first eight parks; the grid lists them all.

### Copy image

**Copy image** on each chart and on the summary puts a picture on the clipboard, ready to
paste into Discord, Slack or a document. The summary is drawn whole, every column, however
far it's scrolled.

To post these on a schedule, use the **Indy Park Compare** section in the
[Scheduler](tools/scheduler.md). It keeps its own parks and job list.

### How science jobs are worked out

Copying, invention and research times and costs follow the game's rules, checked against
real finished jobs:

- **Lab rigs** give their time bonus only to their own kind of job: a copying rig to
  copying, an invention rig to invention. An ME research rig helps only ME research and a TE
  research rig only TE research, so a lab fitted with both isn't counted twice. A Laboratory
  Optimization rig serves all of them.
- **The SCC surcharge** is 2% on ME and TE research, and 4% on copying and invention.

The rig bonuses apply wherever the app plans science jobs, so copy and invention durations
on the [Worklist](tools/worklist.md) follow the same rules.

## Related

- [Configuring Markets](configuring-markets.md)
- [Structure Browser](tools/structure-browser.md)
- [System Index](tools/system-index.md)
- [Browse all tools](index.md)
