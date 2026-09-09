# Themes

From 0.9.13 EVE Console's interface is themeable. The whole app is drawn from a palette rather than fixed colours, so a theme change repaints everything at once — including charts, the [Universe Map](tools/universe-map.md), the [Jump Planner](tools/jump-planner.md) and the ship fitting canvas — live, with no restart.

## The themes on offer

- **Dark** *(default)* and **Light** — the two base looks.
- **Blue**, **Pink** and **Beige** — tinted themes, each available in a **light** and a **dark** variant.

## Switching theme

Two places, and each follows the other:

- **Title bar** — click the theme name shown on the title bar to cycle/pick.
- **Settings ▸ Other** — pick from the list.

Your choice is saved on this machine (it's a local UI preference, not stored in the shared database), so each client can look however you like even when several share one PostgreSQL server.

!!! note "Tints change the room, not the signals"

    The tinted themes inherit Dark or Light and restate only the **neutrals and the accent**. Everything that *carries meaning* is deliberately left alone — a chart line, a status word, a coloured row, EVE's own security-status ramp read exactly the same on Blue or Beige as they do on plain Dark. A theme changes the mood of the interface; it never changes what a colour is telling you.
