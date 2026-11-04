# Themes

From 0.9.13 EVE Console's interface is themeable. The whole app is drawn from a palette rather than fixed colours, so a theme change repaints everything at once — including charts, the [Universe Map](tools/universe-map.md), the [Jump Planner](tools/jump-planner.md) and the ship fitting canvas — live, with no restart.

!!! tip "Video walkthrough"

    The UI Setup video shows switching theme, UI scale and language — [watch it on YouTube](https://www.youtube.com/watch?v=5JAsNgvPvnc).

## The themes on offer

- **Dark** *(default)* and **Light** — the two base looks.
- **Blue**, **Pink** and **Beige** — tinted themes, each available in a **light** and a **dark** variant.
- **Your own** — as many as you like, made in the [theme editor](#making-your-own-theme).

## Switching theme

Two places, and each follows the other:

- **Title bar** — click the theme name shown on the title bar and pick from the menu that opens.
- **Settings ▸ Other** — pick a **Theme** under **Appearance**, beside the **UI scale** and the [language](languages.md).

Tooltips follow the theme too, and the light themes are kept a step dimmer than pure white, so they don't glare.

Your choice is saved on this machine (it's a local UI preference, not stored in the shared database), so each client can look however you like even when several share one PostgreSQL server.

!!! note "Tints change the room, not the signals"

    The tinted themes inherit Dark or Light and restate only the **neutrals and the accent**. Everything that *carries meaning* is deliberately left alone — a chart line, a status word, a coloured row, EVE's own security-status ramp read exactly the same on Blue or Beige as they do on plain Dark. A built-in theme changes the mood of the interface; it never changes what a colour is telling you.

## Making your own theme

The theme editor opens from **Edit themes…**, beside **Theme** under **Settings ▸ Other ▸ Appearance**, or from the bottom of the title bar's theme menu. Its list shows the eight built-in themes, marked **Built-in**, then your own.

**Built-in themes stay as they are.** You can look at their colours but not change them.

### Starting a theme

- **New theme** — **Blank, dark** or **Blank, light**.
- **Copy** — a theme of your own made from whichever theme is selected, built-in or yours.

Give it a **Name** and a **Ground**, **Dark** or **Light**. The ground decides what the editor doesn't cover: the standard controls, chart lines and security colours.

### Setting the colours

There are 31 colours, each with a colour picker and a box for its hex value, in five groups: **BACKGROUNDS**, **LINES**, **TEXT**, **ACCENT** and **STATUS COLOURS**.

You don't have to set them one at a time. Under **Quick start**, pick a **Background**, a **Text** colour and an **Accent**, then click **Work out the rest**. Every background, line, text and accent shade is mixed from those three, replacing what was there. Status colours are left as they are.

!!! tip "Keep the status colours apart"

    Status colours carry meaning in grids and charts. Keep them easy to tell apart from each other and from the backgrounds.

### The preview

The **PREVIEW** beside the colours wears the theme you're editing while the rest of the app keeps the one in use. It shows tabs, a filter bar with real buttons, a text box, a drop-down and a tick box, a panel with plain, banded, hovered and selected rows, the status pills, a notice, the text steps and a popup.

### Saving and using it

- Changes **save as you go**, like the rest of Settings.
- **Undo changes** puts back the colours and name the theme had when you opened it.
- **Use this theme** puts it on. Editing the theme in use repaints the whole app a moment after your last change.
- **Delete** removes one of your own, and asks first. Deleting the theme in use falls back to its ground, Dark or Light.

Your themes are kept on this machine, like the choice of theme, and aren't shared through a PostgreSQL database.

!!! note "Tick boxes and radio buttons"

    The ticks and radio buttons of the standard controls don't follow a theme's accent, on built-in tints or your own: amber on a dark ground, blue on a light one. The preview shows them the same way.
