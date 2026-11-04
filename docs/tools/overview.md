# Overview

The Overview is EVE Console's landing dashboard: a customizable grid of sections that summarizes activity, alerts, notifications, killmails, wallet income/expense and news across all of your authorized characters and personal corporations.

Open it from the left sidebar under **General**.

## What it shows

A toolbar sits at the top, with a customizable grid of sections below it.

**Toolbar**

- **Period** dropdown — the time window most sections report over: *Last 24 Hours*, *Last 7 Days*, *Last 30 Days* (default) or *Last 90 Days*. Your choice is remembered between sessions.
- A **status line** showing the current load step, the final result (owner count and period) or an error in red.
- **⚙ Customize Layout** — opens the layout editor (see [Using it](#using-it)).

**Sections** (any of these can be placed on the grid)

- **Activity Summary** — a two-column metric table.
    - *In Period* (bound to the Period dropdown): Market Sales (count + ISK), Market Purchases (count + ISK), Completed Jobs, Player Ship Kills, Ships Lost.
    - *Current State* (a live snapshot, not period-bound): Outstanding Sell Orders (count + value), Outstanding Buy Orders (count + value), Outstanding Contracts, Active Indy Jobs.
- **Alerts** — actionable warnings. Skill-queue alerts (empty, paused, or ending within your configured threshold) show the character's portrait and jump to that character's Skills tab when clicked; a character whose **Skill queue** box is cleared in **Settings ▸ Characters** raises none. Asset-safety alerts are dismissible. Inactive standing-project alerts jump to the Standing Projects view. An **industry jobs ready to deliver** alert (*"You have N industry jobs ready to deliver"*) flags finished jobs whose output is still waiting and holding a slot. A running-jobs alert flags jobs at a player structure not rigged for them; jobs at NPC stations are never counted. Contract alerts count the active contracts assigned to you, and those from or to you in the last 15% of their life. An **unread mail** alert (*"You have N unread EVE mails"*) counts each mail once and opens the **Unread** folder of [Eve Mail](eve-mail.md). [Planetary Industry](planetary-industry.md) alerts flag extractors stopped or stopping, storage full or filling, factory input run out or running out, and a PI character with an unused colony slot (see below). [Structures](#structure-alerts) and [mercenary dens](#mercenary-den-alerts) raise their own. Which alerts appear is controlled in **Settings ▸ Alerts**.
- **Notifications** — recent in-game notifications within the period, one card per notification: an icon, the title, its age and a dot while unread, then one to three lines of what matters for that type — a bill's amount and due date, a standings change, an attack's shield, armor and hull, fuel left, a corporation application, a moon extraction, a project, and so on.
- **Eve Online News** — the official EVE Online news feed. Each item can be expanded in place (More/Less) and opened in your browser.
- **Personal Killmails** — kills and losses for your authorized characters over the period, with kill/loss counts and ISK totals plus a zKillboard-style list.
- **Sale Listing (Build)** and **Sale Listing (Market)** — the Sale Listing grids embedded as sections.
- **Income (Pie)** and **Expenses (Pie)** — wallet-journal totals for the period, categorized and drawn as pie charts with a total above each.
- **Income & Expense** — the Income & Expense tool embedded as a section (it keeps its own period selector).
- **Orders** — your open outgoing orders from the [Order Tracker](order-tracker.md), and open offers to sell to a store's [Buy listing](../stores/buy-listings.md). An offer's **Source** says where it stands: **Offer · waiting for their contract** until the seller sends it, then **Offer · their contract to accept**.
- **Standing Projects** — a corp standing-projects grid.
- **Standing Buy Orders** — the [Standing Buy Orders](standing-buy-orders.md) grid embedded as a section.
- **Worklist (All)**, **Worklist (Buy)**, **Worklist (Haul)**, **Worklist (Jobs)** and **Worklist (Station Needs)** — five slices of the [Worklist](worklist.md) embedded as sections: everything, just purchases, just hauling, just industry jobs, and the per-station needs, respectively.

!!! note
    The default layout is a 2×3 grid: Sale Listing (Build), Income & Expense and Personal Killmails across the top row; Alerts, Notifications and News across the bottom.

## Using it

- **Change the period** with the dropdown to re-scope the period-based metrics, killmails and pie charts.
- **Act on alerts** by clicking them — skill-queue rows open the relevant character's Skills tab, the standing-projects row opens Standing Projects, Planetary Industry rows open the [Planetary Industry](planetary-industry.md) tool, the unread mail row opens the **Unread** folder of [Eve Mail](eve-mail.md), structure rows open [Corp Structures](corp-structures.md) and den rows open [Mercenary Dens](mercenary-dens.md). Asset-safety rows, attacks on structures and dens, and new tactical operations can be dismissed with their dismiss control.
- **Read a notification in full** by clicking its card: the [Notifications](notifications.md) tool opens with that notification selected and its details shown.
- **Customize the layout** with the **⚙ Customize Layout** button:
    1. Set the grid size with the **Rows** and **Columns** steppers (1–25 each).
    2. Drag a section from the **Sections** palette on the left onto the grid to place it.
    3. Move or resize placed sections on the grid; a section can span multiple cells, and the editor prevents overlaps and out-of-bounds placement.
    4. Click **Apply**. The layout is stored per-installation and persists between sessions.

The Overview reads only your local database, so it refreshes quickly and re-loads automatically about every 60 seconds (and immediately when you change the period or layout).

## Planetary Industry alerts

The Overview raises four kinds of Planetary Industry alert, each with its own box under **Planetary Industry** in **Settings ▸ Alerts**:

| Alert | Raised when |
| --- | --- |
| Extractors | The extractors on a colony have stopped, or stop within the lead time. Exact. |
| Storage | Storage or a launchpad is full, or fills within the lead time. Estimated. |
| Input | A factory planet's input has run out, or runs out within the lead time. Estimated. |
| Free colony slot | A PI character has a colony slot it isn't using. |

Each kind is one row. When one colony is affected, the row names the character and planet and clicking it opens that colony in the [Planetary Industry](planetary-industry.md) tool; when several are, the row gives the count and opens the tool's colony list. Free-slot rows open the tool's **Characters** tab.

The lead times are set in **Settings ▸ Industry**, and the [Worklist](worklist.md#planetary-industry-tasks)'s PI tasks use the same numbers. Only characters whose **PI** box is ticked in **Settings ▸ Characters** raise PI alerts.

## Unread mail alert

*"You have N unread EVE mails"* has its own box, **Alert when there is unread EVE mail**, under **Eve Mail** in **Settings ▸ Alerts**. It's on to start.

A corp or alliance mail reaches each of your characters in that corp, and is counted once. Clicking the alert opens the [Eve Mail](eve-mail.md) tool on *All Characters* and the **Unread** folder, where all of those mails are, however old. A mail read in the game stops counting at the next mail poll.

## Structure alerts

The structures of your corporations raise these, each with its own box under **Structures** in **Settings ▸ Alerts**:

| Alert | Raised when | To start |
| --- | --- | --- |
| **A structure runs out of fuel within** | An Upwell structure or online starbase runs out within this many days, or an Upwell structure with services is already out. | 3 days |
| **A structure is attacked (dismissible)** | A structure, starbase or skyhook is attacked, from your characters' notifications of the last day. One row per structure, its newest. | On |
| **A structure is missing a module of its fit** | A module of the fit isn't fitted, with a slot free for it. | On |
| **A structure has another module where its fit has one** | A module of the fit isn't fitted, and something else is in its slots. | On |
| **Ammo below** | A charge of the fit is below this share of the fit's amount. | 50% |
| **Fighters below** | A fighter of the fit is below this share of the fit's amount. | 50% |

- Only corporations with **Structure alerts** ticked on **Settings ▸ Corporations** raise them. All are ticked to start.
- The fit is the one set for the structure's type on the [Corp Structures](corp-structures.md#config-the-fit-each-type-should-carry) **Config** tab. A type with no fit chosen isn't checked.
- Up to three structures of a corporation are named one by one. With more, one row gives the count. Clicking a row opens Corp Structures on that corporation, and on the structure when it names one.
- Dismissing an attack dismisses every copy your characters received. A later attack raises a new row.
- Fuel and fit alerts are worked out again every five minutes. Attacks are read each time the Overview refreshes.

## Mercenary den alerts

Your characters' own dens raise these, each with its own box under **Mercenary dens** in **Settings ▸ Alerts**:

| Alert | Raised when | To start |
| --- | --- | --- |
| **A den's anarchy at level** | A den's anarchy is at this level (0–4) or above. | Level 3 |
| **A den attacked or reinforced** | A den is reinforced now, or a notification of the last day says it was attacked or reinforced. | On |
| **A new mercenary tactical operation** | A notification of the last day says a den offers a new operation. | On |

Rows from notifications can be dismissed. The anarchy row and a running reinforcement stay for as long as they hold. Clicking a row opens [Mercenary Dens](mercenary-dens.md) on that den.

The game tells a den's anarchy only to its owner, so a den of anyone else's, even on your corporation's skyhook, raises nothing.

## Notes

- Data covers only **authorized characters** (those you have signed in via EVE SSO) and **personal corporations**. If none are configured, the Overview reports that no characters were found.
- The figures are only as current as your last ESI sync — market, wallet, industry, contract, killmail and notification data are populated by the app's background polling.
- Player Ship Kills and Ships Lost require full killmail detail to have been fetched; without it these counts stay at zero.
- The Personal Killmails and Standing Projects sections only load their data when they are enabled on the grid.
