# Notifications

Browse the in-game EVE notifications (structure alerts, war updates, insurance, corp and faction messages, and more) that EVE Console has synced for your characters.

Open it from the left sidebar under **Communication**.

## What it shows

A filter bar sits above a paged grid, with a details pane below.

- **Grid columns** — **Date** (local time), **Type** (the game's own name for the notification type, e.g. *Corporation bill*), **Character** (every character the notification arrived under), **Sender**, **Sender Type** (Character / Corporation), and **Read** (Read / Unread).
- **Details pane** (below the grid) — for the selected notification: a compact header with the sender's icon (portrait, corp/alliance logo, or a structure's own icon), the type, **Sender**, **Date**, **Read** and **Character**, followed by the notification body.
- **Body** — laid out for each type, with every field named for what it means in that type. IDs are shown as names, with icons and links (characters, corporations, alliances, factions, agents, items, systems, stations and structures). Lists appear as tables — ore volumes with a total, fuel, implants, standings and so on — and standings changes are shown signed and coloured, with the resulting standing. Tick **Show the original text** to see the raw notification text; a notification with nothing more to show says *No further details.*
- **Unread count** — the filter bar shows an "*N* unread" tally for the current filters (this ignores the *Unread only* toggle).

The same notification is often delivered to several of your characters; the grid collapses those into one row per notification and lists all recipient characters in the **Character** column. A row counts as unread if any recipient still has it unread.

## Using it

Filtering, sorting, and paging all run against the whole notifications table, not just the current page.

- **Character** — limit to one character, or *All characters*.
- **Type** — filter to a single notification type, or *All types*. Types are listed by the game's own names.
- **Sender** — *All senders*, *Corporation*, or *Character*.
- **From** / **Thru** — date range (calendar pickers). **From** defaults to 30 days ago; **Thru** is open-ended unless set. Dates are treated as UTC.
- **Sort** — *Date: newest first* (default), *Date: oldest first*, or *Type (A → Z)*, which sorts by the type names shown.
- **Unread only** — show only notifications with an unread recipient.
- **Clear** — reset every filter to its default (character = all, type = all, sender = all, From = 30 days ago, Thru = none, unread-only off).
- **Pager** (bottom) — **First / Prev / Next / Last** buttons with a page indicator.

Select any row to load its details in the pane below. Clicking a notification card on the [Overview](overview.md) opens this tool on that notification.

## Notes

- Requires characters authorized with the `esi-characters.read_notifications.v1` ESI scope. Add characters and grant scopes from the [getting-started guide](../getting-started.md).
- The grid shows what EVE Console has already synced, so freshness depends on the app's last notification sync rather than a live fetch.
- For player-written mail rather than system notifications, see [Eve Mail](eve-mail.md).
