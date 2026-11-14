# Client Layouts

Client Layouts shares each monitor between your game clients and EVE Console panels. You build a layout from panels docked to the monitor's edges, and put clients, controls and grids inside them. Then you say which characters run in each client position, save that as a profile, and press **Apply**. From then on, clients are kept in place as they start and log in, and the panels around them carry clocks, server status, Mumble, a Worklist that follows the client in use, a menu of the tools, and Tool Containers that hold tools like a window that stays put.

Open it from the left sidebar under **General**, after **Characters**.

!!! info "Windows only"
    Client Layouts needs the game's windows, which only Windows gives the app. On Linux and macOS the sidebar item isn't there, and no panels show. The [tray icon](#keeping-the-app-running-in-the-tray) and [Overview layouts](overview.md#saved-layouts) work everywhere.

!!! warning "Only size and position"
    EVE Console only ever sets a game client's size and position, and raises it when you click a panel or another client on its monitor. It never sends a client input or keystrokes, never gives it focus, never changes its window style, and never reads its memory or its screen. It reads the client's window title, to know who is logged in, and where the window is. Everything you do in the game, you do yourself.

## What a layout is

A layout is the shape you give one monitor. It holds no monitors or characters, so one layout can be used on several monitors, or on another desktop that shares your database.

- **The monitor holds only panels.** Each is docked to an edge (**Top**, **Bottom**, **Left**, **Right**), or fills what's left (**Full**). The first docked takes its whole edge; the next ones fit in what is left.
- **Everything else goes inside a panel**: more panels, controls, clients and grids, each docked to an edge of the panel or filling it.
- **A client** is a game client's place. The panel has a hole where the client sits, so the client shows through and takes its own clicks. A panel that is nothing but a client puts up no window at all, so a layout of one client is just that client, sized to the monitor.
- **A grid** divides a panel into cells, and every cell is a panel of its own. Grids can sit inside grids, up to five deep.
- **A control** is one of the [panel controls](#panel-controls) below.

Sizes are in pixels at 100%, and follow the UI scale: at 125%, a 40 px panel is drawn 50 px wide. Panels take the theme's colours unless you give one a colour of its own.

## Building a layout

Layouts are made on the **Layouts** tab. Everything saves as you change it, but nothing moves on screen until you [Apply](#apply-and-its-notices).

**The list on the left** holds your layouts, with **New**, **Duplicate**, **Delete**, **Export** and **Import** under it. A layout a monitor is using can't be deleted; the tool says so. Under the list, the **Outline** shows the whole layout as a tree. Click a line to select it on the drawing, or fold a branch away.

**The drawing** shows the layout on one of your monitors, picked in **Show on**. Name it in **Layout name**.

1. Click **New ▸ Blank** for one empty panel, or start from a [template](#export-import-and-templates).
2. **Right-click the monitor** to dock a panel on it: **Dock a panel on the monitor ▸ Top**, **Bottom**, **Left**, **Right** or **Full**.
3. **Right-click a panel** to put something in it:
    - **Dock a panel inside** — another panel, to an edge or full.
    - **Dock a control** — any [control](#panel-controls), **Client** among them, then where it goes.
    - **Dock a grid** — a grid that starts as 2 × 2 empty panels.
    - **Remove panel**, and for something docked, **Send to Back** and **Bring to Front** in its dock order.
    - **Parent: …** — the menu of whatever holds it, with **Select**. That's how to reach a panel that's completely covered by what it holds.
4. **Drag the lines** between things to resize them.
5. **Drag something into another panel** to move it there, on the drawing or in the outline. A grid is dragged by any of its cells.
6. **Delete** removes what's selected. **Undo** and **Redo** (or **Ctrl+Z** and **Ctrl+Y**) step back and forward through up to 200 changes to the layout. A name typed in one go, or a colour dragged across the picker, is one step.

**Full** is offered only while nothing fills the area, so it never replaces what's there.

### Beside the drawing

What you can set depends on what's selected:

- **Panel name** — shown in the outline and, for an empty panel, on screen.
- **Docked to** — **Top**, **Bottom**, **Left**, **Right** or **Full**.
- **Dock order** — everything docked beside the selection. Drag a row up or down to change the order; click one to select it. Higher docks first and takes its whole edge; lower ones fit in what is left.
- **Size in pixels**, or **Width in pixels** / **Height in pixels** — how wide or high it is along its edge, at 100%.
- **Grid** — **Columns** and **Rows**, 1 to 12. Each cell is a panel and keeps its row and column, with what's in it. Making the grid smaller removes the cells past its new edge, with what's in them; Undo brings them back. Click a line between cells to select the grid.
- **Color** — a colour picker, and **Use the theme's color** to go back to following the theme.
- **Style** — **Flat**, **Raised**, **Inset**, **Ridge**, or **Card** (the Overview's rounded look). Raised, Inset and Ridge keep what the panel holds 4 px in from the edge, Card 5 px, so nothing sits on the edge or its corners.
- **Content padding** — **Left**, **Top**, **Right** and **Bottom**, in pixels at 100%, kept free inside the panel. On a grid, it's kept round the cells and between them: padding 3 leaves 3 px between panels.
- **Control** — the settings of a selected control, where it has any (see [Panel controls](#panel-controls)).

### Layout warnings

For each of your monitors using the layout, the tool warns when:

- a client is smaller than 800 × 600, *small for playing*;
- the panels don't fit, so something has no room;
- part of the layout can't be used as saved, which can happen with a layout made by a newer version.

## Panel controls

Every control behaves as its twin does on the main window, with the same values and the same clicks. Pick one from **Dock a control** on a panel's right-click menu.

**Clocks and status**

- **EVE time** — the game clock. Click it to open the EVE time link in your browser.
- **Local time** — your own clock.
- **EVE server status** — Tranquility's state and how many are playing. Click it for the server status page.
- **Users online** — how many of your characters are online. Hover for each one, where it is and what it's flying.
- **App version** — this build, and a link to the newer release when there is one.
- **SDE version** — the static data loaded. **Update available** opens the Settings tab that imports it.
- **Database** — whether this copy uses SQLite or [PostgreSQL](../storage-postgresql.md).
- **Background worker** — which copy of the app does the [background work](../background-processing.md).
- **ESI status** — the background processes, as at the bottom left of the main window. Each opens [Background Processes](background-processes.md) at its own tab; a warning opens where it's put right.

**Shortcuts**

- **Settings** — the gear. Settings opens on the panel's monitor.
- **Theme** and **UI scale** — the one in use, and the others on click. See [Themes](../themes.md).
- **Alarm light** — opens [Alarms](alarms.md). Right-click it to mute this machine.
- **Scheduler** — opens the [Scheduler](scheduler.md).
- **Eve Mail** — the envelope, opening [Eve Mail](eve-mail.md) on your unread mail when there is some.
- **Menu** — ☰, a menu of every tool, by sidebar section. **Opens tools in** sets where: **A new window**, **The window used last**, or one of your [Tool Containers](#tool-containers) of tabs. A tool already open moves there. If the container isn't on screen, the tool goes to the window used last.

**Things to work in**

- **Worklist** — the ready tasks of the character in the client you were last in on this monitor. See [The Worklist control](#the-worklist-control).
- **Mumble** — one [Mumble](../mumble.md) server, set in **Server**. **Shows as**: **One line, listing who talks beside it**, or **A list of the channel, talkers at the top**. Both show the server and channel; the name is green while connected. The power button connects or disconnects. Right-click a person for the same menu as the channel tree.
- **Intel** — live intel near the character in this monitor's client: systems with hostiles, nearest first, with how far, how many, in what and how long ago. **Shows as** the live list, or one line with the nearest threat that drops the list down when clicked. **Looks out to** 3, 5, 10, 15 or 20 jumps (10 to start), through stargates and open Thera or Turnur holes; jump bridges aren't counted. See [Intel](intel.md).
- **Tool Container** — tools as tabs, or one tool, that stay where the layout puts them. See [Tool Containers](#tool-containers).
- **AI companion** — the conversation with the [AI agent](../ai-agent-eden.md), the same one as on the main window. While the companion is off, it says so.
- **Alerts** — the Overview's alerts. Clicking one goes where it's about and brings that window forward.
- **Direct messages** and **Group chat** — icons that drop down what's new: the conversations or rooms with something unread, each opening where it is, and a link to [Messages](messages.md) or Group Chat.
- **Direct message conversations** — everyone you have a conversation with down the side, and the one you pick beside it. Enter sends.
- **Group chat room** — one room, set in **Room**, and changeable from its own drop-down while the panel shows. Enter sends.
- **Orders**, **Sale Listing (Build)**, **Sale Listing (Market)**, **Notifications**, **Eve Online News** and **Personal Killmails** — the [Overview](overview.md)'s sections, one each. Put one in a **Card** panel for the Overview's look.

Small controls, such as the gear, the alarm light and the clocks, shrink to fit a thin bar rather than being cut off.

### The Worklist control

The [Worklist](worklist.md) for one character, on a panel beside that character's client.

- **Who it shows.** The character in whichever client you were last in on this monitor. Bring another client forward, or log that client in as someone else, and the list follows. The drop-down lists everyone set for that client's position, logged in or not, so you can look at an alt's tasks before switching to it, then anyone else logged in on the monitor. A name you pick holds until the client in use changes or logs in again.
- **Shows as** **The list of ready tasks**, or **One line of counts, the list dropping down when clicked**.
- **The list.** Each kind of task is a heading with its count, in the Worklist's own order, and tasks are sorted by name under it. Click a heading to close it; it stays closed across refreshes and character switches. A task opens to its detail, as in the Worklist, and lines that name an item show its picture.
- **Hauling.** Loop stops and trips carry **✓ Hauled**, or **✓ Contracted** for a hauling service, first on the line so a long station name never pushes it out of reach. They tick hauls off just as the Worklist does, including the Contracted cargo dialog. See [Ticking hauls off](worklist.md#ticking-hauls-off).
- **Only that character's tasks.** A task with no one character, such as delivering finished jobs, isn't shown, and a long haul shows only for its lead pilot.
- The button at the top opens the full Worklist.

If no one is logged in on the monitor, it says so. A character not in EVE Console is named as such.

## Tool Containers

A Tool Container is the app's own tabs, with no window border, so the tools in it stay where the layout puts them. Select one in the editor to set it up:

- **Name** — shown on the drawing and in the Menu control's choices.
- **Holds** — **One tool**, or **Tabs**. Tabs take more tools dragged in from any window, and give theirs up the same way. **Can split in two** lets a container of tabs split, as a tab window does.
- **Opens with** — the tools it starts with, in order. Pick a tool and click **Add**; **×** removes one. In a container of tabs, **Can close** decides whether each tab can be closed. A tab that can't be closed stays in this container.
- **… opens with** — pick a tool in the list to set how it opens. The Overview has its **Layout**, one of the Overview's [saved layouts](overview.md#saved-layouts). Other tools have nothing to set.

When a container shows, a tool open somewhere else moves into it. An Overview in a container is one of its own, showing the layout you chose; the main window's Overview stays where it is.

A container of tabs has its own ☰ menu at the top right of its tabs. It opens a tool in those tabs, or shows it if it's already there. A tool open elsewhere comes in as another copy.

Click into a container and it becomes *the window used last*, so tools set to open there land in it, and you can type in its tool.

While a panel is hidden (see **Panels start** under [Setting up your monitors](#setting-up-your-monitors)), the tools in its container don't count as open. Open one from the sidebar and it comes out into a window you can see.

### Tool copies

**Shift-click** a tool in the left sidebar, in a panel's Menu or in a container's ☰ menu to open another copy of it, in the place the menu would open it. Each copy is independent and lets go of everything it uses when closed.

Most tools can have copies, the Universe Map and the Overview among them. Client Layouts, Indy Parks, Background Processes, Messages and Group Chat can't; Shift-click moves the one you have to where you asked instead.

## Setting up your monitors

The **Monitors** tab is for this desktop: its monitors, which layout each uses and who runs where.

- **This desktop** — the desktop's name, which starts as the machine name.
- **Place clients and show panels on this desktop** — off to start. While it's off, your game clients are left alone, no panels show, and **Apply** can't be pressed.
- **Profile** — see [Profiles](#profiles).

Click a monitor on the map to set it up:

- **Layout** — one of your layouts, or **None: leave this monitor alone**.
- **Panels start** — **With EVE Console**, or **When EVE starts on this monitor**. The second hides the monitor's panels while no client is on it.
- **Use the full monitor, including where the taskbar is** — off, the layout stays clear of the taskbar. On, it covers the whole monitor, and the taskbar moves behind it (see [The taskbar](#the-taskbar-on-a-full-monitor)).

### Who runs where

Under the monitor, each client position in its layout is listed with its size. Add the characters that should run there:

1. Type a name in **Character name**. It offers your characters in EVE Console and names seen in client windows; an alt doesn't have to be in the app.
2. Click **Add**, or press Enter. **×** takes a character out.

A position can hold several characters: they're the group that plays there, one at a time. A character has one position per profile, so adding it to another takes it out of the first. Names match whatever their case.

Switching a monitor to a layout that has no one assigned on it yet carries the last layout's characters over, client 1 to client 1 and so on. Each layout keeps its own groups after that, so switching back finds them as they were.

### Other desktops

If several desktops share your database, the others are listed under **Other desktops**, and you can rename them. After reinstalling Windows, this computer looks like a new desktop. Click **This is that desktop** on its old entry, then again to confirm, to take over its monitors and groups. This replaces what is set for this desktop.

## Profiles

A profile is a named set of everything on the Monitors tab for this desktop: each monitor's layout and settings, and who runs where. One is in use at a time, shown as **In use:**.

- **Profile** chooses which one the tab shows and edits. Choosing one moves nothing.
- **Name** renames it. **New** starts an empty one, **Duplicate** copies this one with the same people in the same places, and **Delete** removes it. A desktop always keeps one, so the last can't be deleted.
- To switch, pick the profile and press **Apply**.

Profiles belong to one desktop. Layouts are shared by every desktop on the database.

## Apply and its notices

**Apply** moves clients and panels to match the profile on screen, on this desktop only. It also puts back clients that were moved by hand, and clears the notices.

The line beside it says what's waiting, such as *Changes to apply on monitors: 1, 3. Nothing moves until you press Apply*, or *Everything is applied*.

When placement leaves a client alone, a notice with a warning icon appears next to **Apply**:

| Notice | What to do |
| --- | --- |
| *… isn't in Fixed Window mode, so it was left alone.* | Change the client's window mode to Fixed Window in the game's settings, then Apply. |
| *…: its position is in use by another logged-in character, so it stayed where it is.* | Log the other character out, or move one of them to another position. |
| *… is logged in but isn't in any group, and no client position on its monitor is free.* | Add the character to a client position. |
| *… was moved by hand, so it is left alone until you press Apply.* | Press Apply to put it back. |
| *… didn't stay where it was placed, so it is left alone until you press Apply.* | Something else moved it straight back. Press Apply to try again. |

## As clients start and log in

While placement is on, the app looks at the clients' windows a few times a second.

- **Clients already running** when EVE Console starts may be in a fight, so they aren't moved. One sitting exactly in a client position holds it.
- **A new client** at its login screen goes to an empty client position on the monitor it opened on.
- **When it logs in**, it moves to the position that character is in, on whichever monitor that is. If a client still at its login screen is sitting there, it gives way and takes the place the logged-in one came from.
- **A character in no group** keeps the position it has, or takes a free one, positions no one is set for first.
- **A client you move or resize yourself** is left alone until you press Apply. So is a minimised one, until it's restored.

Apart from Apply, a client is only ever moved at its login screen and the moment it logs in, never while someone could be flying it. Changing the UI scale places the panels, and the clients beside them, again for the new size, as Apply would.

### Clicking panels and clients

A monitor's panels come forward together when you click one of them, or when you bring a client on that monitor to the front, and that monitor's other clients come up beneath them. Raising one monitor's panels doesn't touch the other monitors.

Clicking a panel doesn't take the keyboard from the game: whichever window had it keeps it until you click into a client. A Tool Container, a menu or a box you type in takes the keyboard when you click it, until you click something else. Panels stay out of Alt-Tab.

Opening a tool that shows in a panel, from the Overview's Worklist link for example, brings that panel, the rest of its monitor's panels and its clients forward with it.

## The taskbar on a full monitor

On a monitor set to **Use the full monitor, including where the taskbar is**, the taskbar moves behind the layout while its clients and panels are on top.

- Bring one of EVE Console's own windows in front there, such as the main window, a window of tabs, a dialog or an alarm, and the taskbar comes back. It hides again once the layout is back on top.
- Another program's window in front of the layout brings the taskbar back as Windows always does.
- Floating windows that sit over the game, such as the Mumble overlay, menus and drop-downs, leave it hidden.
- Each monitor goes by what is on top on that monitor only.

The app only tells the taskbar which windows to stay behind; nothing is sent to a client.

## Export, import and templates

**Export** saves the selected layout to a `.json` file, to keep or to share. **Import** adds a layout from a file as a new layout, with *(2)* after its name if the name is taken. Monitors are not changed. Both open in your Downloads folder.

- A Mumble control's server is written by its address, and matched on import to the server at the same address in this database. With no match, it's left unset for you to pick. After an import, check its Mumble controls if it came from another database.
- A file that isn't a layout is refused: *That file isn't an EVE Console layout.* So is one from a newer version, until you update.

**New** is a menu:

- **Blank** — one empty panel, no client.
- **The templates**, by name. A new layout from one is a copy, under the template's name.
- **Open templates folder** — the `Layout Templates` folder in the app's data folder (`%LOCALAPPDATA%\EVE Console Data\Layout Templates`, or in the profile's folder when you run a profile).

Nine templates come with the app: **Plain Vanilla**, **One Client - Standard**, **One Client - Minimal**, **Two Clients - Horizontal**, **Two Clients - Horizontal - Minimal**, **Two Clients - Vertical**, **Two Clients - Vertical - Minimal**, **Four Clients** and **Four Clients - Minimal**. They carry no Mumble server or chat room.

Any layout file saved in the templates folder shows up under **New**, so export a layout there to make it a template. Templates are copied in once: one you delete or change stays that way, a file of yours is never overwritten, and templates added in later versions still arrive.

## Keeping the app running in the tray

With panels and Tool Containers on screen, you may not need the main window. Under **Settings ▸ Polling ▸ Notification Area Icon**, tick **Keep EVE Console running in the notification area when the main window is closed** (on a Mac, *in the menu bar*). It's off to start.

Closing the main window then only hides it: panels, alarms and the background work carry on. Click or double-click the icon, or choose **Open EVE Console** on its menu, to bring the window back, and **Exit** to end EVE Console. The menu also opens **Background Processes**, and the icon's tooltip says which copy does the background work.

The icon is part of the app itself and shows whenever it runs, on Windows, Linux and macOS. The separate `--tray` icon process of earlier versions is gone: if you had it starting at logon, that entry is removed, and this setting is turned on for you instead.

## Notes

- **Placement is per desktop.** Every desktop that shares your database has its own monitors, profiles and switch, and only places its own clients. Layouts are shared.
- **Fixed Window mode only.** A client in any other window mode is left alone.
- **Clients are found by their window title**, which names the logged-in character. That's how a client is matched to its position.
- **Nothing is ever fought over.** A client that ends up somewhere other than where it was sent is left where it is until you Apply.
- **Panels are hidden, not closed**, when their monitor's clients go, so they come back at once. They close when placement is turned off, when the layout no longer has them, or when the app exits. Clients stay where they are when the app exits, and the taskbar goes back to normal.
- **A control the app doesn't know**, from a newer version sharing your database, is kept as it is rather than spoiling the layout.
