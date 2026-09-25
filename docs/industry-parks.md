# Industry Parks

An **industry park** describes the structures you actually build in, so that
build-cost and production calculations reflect your real bonuses (material
efficiency, rig bonuses, structure type, security modifiers, and facility tax)
instead of generic values.

Open **Indy Parks** from the left sidebar under the **Industry** group.

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
  (Athanor/Tatara) offer reaction and reprocessing rigs; NPC Stations take no rigs
  or service modules.
- **Actual facility** — the real in-game station or structure a park structure
  describes. Linking one lets EVE Console check the industry jobs running there
  against your rigs, and keeps the park's fitting in step with the real structure.
- **Default facility** — each park has exactly one structure ticked **Default**:
  its catch-all. Any item that no production assignment covers is planned there,
  with **no rig bonus**, so a calculation still completes instead of failing. This
  is separate from the park-level **★ Set Default**.
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

1. In **Indy Parks**, click **+ New Park**. It appears in the list on the left;
   select it to edit. Rename it in the **Park Name** box at the top.
2. Add your structures. There are two ways, and you can mix them:
    - **A whole system at once** — see [Adding every structure in a
      system](#adding-every-structure-in-a-system) below. This is the quickest way
      when your structures are ones EVE Console already knows about.
    - **One at a time** — click **+ Add Structure** and fill in the card, as
      described in [Adding a structure by hand](#adding-a-structure-by-hand).
3. Under **Production Assignments**, set each category's dropdown to the structure
   that produces it. Leave a category on *— not assigned —* if you don't build it.
   Click **Auto-assign from rigs** to fill the empty categories for you (see
   [Auto-assigning from rigs](#auto-assigning-from-rigs)).
4. (Optional) Under **Item Exceptions**, type an item name into the search box,
   pick it from the results to add it, then choose the structure that should build
   that specific item. Remove an exception with its **✕** button.
5. Check which structure is ticked **Default**. It's the catch-all for anything
   left unassigned.
6. To make this the park used everywhere, click **★ Set Default**.

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

Click **+ Add Structure**. The new card starts as *New Structure*, a **Raitaru** in
**Null Sec**. Fill in:

- **Name** — a label such as *Main Raitaru*.
- **Type** — the structure hull; this determines which rigs are available.
- **Solar system** and **Security** — these drive the security/system-cost
  modifiers.
- **Tax Percentage** — the facility's job tax.
- **Rigs** — pick up to three from the per-type dropdowns (leave a slot on
  *— empty —* if unused).
- **Service modules** — see [Service modules](#service-modules).

Remove a structure with the **✕** button on its card.

!!! warning "Set the security class yourself"

    A structure added by hand is **not** given a security class from its solar system.
    It starts as **Null Sec** whatever system you type. Rig bonuses scale with security,
    so a high-sec or low-sec structure left on Null Sec gets the wrong bonus. Pick the
    right **Security** on every card you add by hand. **+ Add Missing In System** sets
    it for you.

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
Upwell hull offers the same list; NPC Stations take none.

- To add one, pick it from *— add a service module —* and click **Add**. Adding a
  module that's already listed does nothing.
- To remove one, click its **✕**.
- Click a module's name to open it in the Item Browser.

When the fitting comes **from assets**, the list follows the game and can't be edited.

## The default facility

Tick **Default** on a structure's card to make it the park's catch-all. Items that no
production assignment or item exception covers are planned at this structure with no
rig bonus, so the calculation still completes.

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
check **Tax Percentage** and **Default** after an import.

## Related

- [Configuring Markets](configuring-markets.md)
- [Structure Browser](tools/structure-browser.md)
- [Browse all tools](index.md)
