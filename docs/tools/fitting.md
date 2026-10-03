# Fitting

A ship fitting tool built on the game's own rules: open a fit from the game or one of your own ships, or start a new one, change modules, charges, drones and implants, and see CPU, powergrid, damage, tank, capacitor, speed and value worked out as you go.

Open it from the left sidebar under **Ships**.

The numbers come from the game data (the SDE). Each module's effects are applied the way the game applies them, stacking penalties included, so the figures follow the SDE rather than a hand-kept list. Ships, Upwell structures, Tech III subsystems and tactical destroyer modes are all covered.

!!! note
    The tool needs the game data imported (**Settings ▸ SDE**). If it isn't there yet, the status line says so; import it, then reopen the tool. After an app update that needs new game data, the import runs by itself and the status line asks you to reopen the tool when it finishes.

## What it shows

The tool has three parts:

- **Items** on the left — everything that can go on a fit, as the market groups it. The **☰ Items** button hides or shows it.
- **The new-fit bar** along the top — the ways to start a fit.
- **The fits**, one per tab. Each fit shows its hull with a ring of slots, a list of modules, drones, cargo, implants and fleet boosts under it, and its figures on the right.

### Starting a fit

Each of these opens the fit in a new tab:

- **Hull** — type a ship's name or its class (for example *Rifter* or *frigate*) and pick one.
- **Paste EFT…** — paste a fit in EFT format, the text the game's fitting window copies and fitting sites share. The first line names the hull, like `[Rifter, My fit]`. Item names in any of the game client's languages are understood. Lines that aren't recognised are named in the status line.
- **Open fit…** — pick a fit saved in EVE Console, or one of your characters' saved fittings in the game (see [Opening a saved fit](#opening-a-saved-fit)).
- **Existing ships…** — pick one of your own assembled ships, with what is fitted to it (see [Opening one of your ships](#opening-one-of-your-ships)).

### The fit

Above each fit:

- **PILOT** — whose skills the numbers are worked out with: **All V**, **All 0**, or one of your characters (their trained skills, as last synced). A fit opened from a character's in-game fittings is worked out with that character's skills, unless you've already picked a character.
- **MODE** — for a tactical destroyer, the mode it's in. Its bonuses are in the numbers.
- The fit's name, and where **Save** writes it: **Saved in EVE Console**, **Saved in *character*'s fittings in the game**, or **Not saved yet**.
- **Copy EFT**, **Save** and **Save As…**.

Below the hull and its ring of slots:

- **The module list**, by rack — **High slots**, **Mid slots**, **Low slots**, **Rig slots**, and **Subsystem slots** or **Service slots** where the hull has them. Each heading shows slots used of slots available. Each module has a state button, a **HEAT** switch where it can be overheated, a charge pick list where it takes charges, its CPU and powergrid, its own figures (DPS, repair, mining yield, electronic warfare strength) and its market value.
- **DRONES AND FIGHTERS** — drone stacks with how many are **in bay** and how many are **launched**; fighter squadrons with their size, an **in tube** box and an on/off switch for each ability.
- **CARGO HOLD** — anything at all, with a quantity.
- **IMPLANTS AND BOOSTERS** — the pilot's implants and boosters.
- **FLEET BOOSTS** — other fits that boost this one (see [Fleet boosts](#fleet-boosts)).

### The figures

On the right of each fit:

| Section | What it shows |
| --- | --- |
| **RESOURCES** | **CPU**, **Powergrid** and **Calibration** used of what the hull has; turret and launcher hardpoints; drone bay and bandwidth, or fighter bay and launch tubes; cargo used. Anything over the limit is shown in the warning colour. |
| **VALUE** | What the fit is worth, split into hull, modules, drones and cargo. Implants and boosters are shown apart and left out of the total — they belong to the pilot. The line under it says which prices are used and how many items have none. |
| **OFFENSE** | Total DPS, split into weapons, drones and fighters; the damage mix; volley; DPS with reloads; full spool-up for weapons that build up; energy neutralizer and nosferatu drain. Doomsdays, lances, bombs and breacher pods are listed apart, as strikes, rather than added to DPS. |
| **MINING** | Ore, ice and gas per hour, with every miner running. Shown only for a fit that mines. |
| **DEFENSE** | Effective HP against a damage profile you choose, a resistance table for shield, armor and hull, shield regeneration, and what the fit's own repairers and any remote repairs give back. If the capacitor runs out, it says when those repairs stop. |
| **CAPACITOR** | **Stable at** a percentage, or how long it **Lasts**; capacitor use against peak recharge; capacitor boosters and incoming transfers. |
| **NAVIGATION** | Align time, signature radius, warp speed, mass and inertia. A structure shows only its signature. |
| **TARGETING** | Targeting range, scan resolution, number of targets, sensor strength, and lock times against a typical frigate, cruiser, battleship and capital. |

**Against** in the DEFENSE section picks the damage the tank is judged against: **Even (25% each)**, one damage type, or **Custom** (four boxes for relative amounts). A Reactive Armor Hardener adapts to the damage chosen, and the module list shows what it settles at. Your choice is remembered.

## Using it

### Adding modules and other items

1. Find the item in **Items**. Pick a category (**All**, **Modules**, **Rigs**, **Subsystems**, **Charges**, **Drones**, **Implants**, **Boosters** or **Other items**), or type in the search box. Tick **Only what fits this hull** to hide modules the hull can't take.
2. Put it on the fit in one of these ways:
    - double-click it;
    - select it and click **Add to fit**;
    - drag it onto a slot on the ring, or onto a row in the module list. Dropping on a filled slot replaces what is there.

Click an empty slot on the ring to list only modules for that kind of slot; the ✕ beside the note above the list shows everything again.

A module that can't go on the fit isn't added, and the status line says why — no free slot or hardpoint, the wrong rig size, a module the hull can't use, or a limit on how many of that module can be fitted.

**Add to cargo** puts the selected item in the cargo hold instead. Anything can be carried.

### Charges

Pick a charge from a module's charge list, or add one from **Items**: it goes into the selected module if that module can take it, otherwise into every fitted module that can. Drag a charge onto a module to load just that one.

### Module states

Click a module's state button to step it through **OFF**, **ON** and **ACT**; the **HEAT** switch overheats it. A module added to a fit starts active if it can be activated, otherwise online (cloaks and cynosural field generators start online). On the ring, right-click a module for **Put online**, **Activate**, **Overheat**, **Unload** and the rest.

Only active modules count toward damage, capacitor use and active tank.

### Drones and fighters

Set how many drones are **in bay** and how many are **launched**; only launched drones count toward damage. If more are launched than the pilot can control and the hull can launch, the number is cut back.

For fighters, tick **in tube** for each squadron that is launched, and switch its abilities on or off. Damage abilities count toward DPS while they're on. The OFFENSE section also gives a **sustained** fighter figure, which counts time spent rearming in the tube.

### Fleet boosts

**FLEET BOOSTS** adds the help other fits give this one:

1. Click **Add a boosting fit…** and pick a fit, from the same list as **Open fit…**.
2. Pick that fit's pilot, whose skills its bursts and remote modules are worked out with.

Add as many as you like. Their command bursts apply (of the same bonus from several fits, the strongest), and their remote shield boosters, armor and hull repairers, capacitor transmitters and logistics drones add up. Switch a booster off to keep it in the list without its help. If the fit runs command bursts of its own, **Its own command bursts boost it** decides whether they count for it too.

### Working with several fits

Each fit has its own tab; a dot on the tab means it has changed since it was opened or saved. Drag a tab to reorder it, or drop it on the right half of the tool to see two fits side by side. New fits open on the side you last clicked, and **Items** adds to the fit showing there.

### Opening a saved fit

**Open fit…** lists, in one tree by hull:

- fits saved in EVE Console, and
- the saved fittings of every character that has granted the fittings read scope.

Use the owner pick list to show one character's fittings, or EVE Console's, and the search box to find a fit by its name or its hull's. Select a fit to see its contents, then click **Load Fit**. **Delete** removes the selected fit — only fits saved in EVE Console can be deleted here.

### Opening one of your ships

**Existing ships…** lists every assembled ship your characters and [personal corporations](../getting-started.md#personal-corporations) own, wherever it is. Packaged hulls and capsules aren't listed — a packaged ship has nothing fitted.

Each row shows the ship's name (**Ship**), **Hull**, **Owner** and **System**, with its **Hull value**, **Fit value** and **Total value**. The most valuable ships come first; click a column header to sort another way.

1. Type in the filter box to narrow the list. It matches part of a ship's name, hull, system or owner, and every word you type must match.
2. Select a ship and click **Open as a new fit**, or double-click it.

The ship opens in a new tab as a new fit, saved nowhere yet: use **Save As…** to keep it in EVE Console or in a character's fittings. When a character owns the ship and no character is picked as **PILOT** yet, the fit is worked out with that character's skills.

The fit holds the modules, rigs and subsystems in their slots, the charge loaded in each, and the drone and fighter bays. The cargo hold and other holds are left out.

!!! note "As the last asset update saw it"
    The list is read from your stored assets, which ESI refreshes about once an hour. A module swapped in the game since then isn't shown until the next asset update. Ship names aren't in the asset list: they are asked of the game when the list opens and kept until the app closes. A ship whose name can't be read is listed by its hull, and the note under the list says so.

### Saving

- **Save** writes over the fit this one was opened from or last saved as, without asking: back to EVE Console, or back to the character's fittings in the game.
- **Save As…** asks for a name and where to save:
    - **EVE Console (this app)**;
    - **In game: replace "*fit*" in *character*'s fittings**, for a fit opened from the game;
    - **In game: new fitting on *character***, for any of your characters.

Save As asks before it overwrites a fit of the same name for the same hull in EVE Console, or replaces a fitting in the game. Characters that can't be saved to are listed with the reason.

Fits saved in EVE Console keep everything: module states, launched drones and squadrons in tubes.

### Sharing a fit

**Copy EFT** puts the fit on the clipboard as EFT text, ready to paste into the game or a fitting site. Item names are always written in English, which is what the game and other tools read.

## Notes

- **Saving to the game** needs the character's **Write Fittings** scope. A character without it, or whose token has expired, is named in the save dialog; update the character under **Settings ▸ ESI Tokens** (see [Getting Started](../getting-started.md#managing-esi-tokens-characters-corporations)).
- **The game can't change a fitting.** Replacing one saves the new fitting first, then deletes the old one. If the old one can't be deleted, the status line says so and you can delete it in the game.
- **In-game fittings hold less than a fit here.** The game keeps no loaded charges, so one load per module is saved in the cargo, and is loaded again when the fit is opened. Implants and boosters aren't saved to the game (the status line names what was left out). The game keeps no tactical destroyer mode, so a fit from the game starts in the first mode; EFT text carries it.
- **Corporation fittings aren't listed.** ESI has no way to read or write them.
- **Value** uses the asset-value market and price type from **Settings ▸ Market** (see [Configuring Markets](../configuring-markets.md)). With none set, the VALUE section says so. The **Existing ships…** values are on the same basis, and an item with no market price there counts as nothing.
- A character pilot uses the skills last synced from ESI. The tool doesn't warn about modules the pilot can't use; pick **All 0** or a character to see the numbers with their skills.
- **Add Items From Fit** in [Inventory Levels](inventory-levels.md) reads your characters' in-game fittings, not fits saved in EVE Console.
