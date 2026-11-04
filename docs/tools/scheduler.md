# Scheduler

The Scheduler runs tasks on a timetable — posting reports to Slack or Discord, or raising an in-app alert — so recurring updates like a corp Top 10 or a monthly summary go out on their own, without you being at the screen.

Open it from the **clock icon in the title bar** (it isn't in the left sidebar).

!!! warning
    The Scheduler is still taking shape (Beta). Its stored settings may change between releases.

## How a task works

Each task has three parts: **when** it fires, **what** it does, and whether it's **enabled**. A task runs in the background on whichever client is doing the [background work](../background-processing.md), so it fires whether or not you have the Scheduler open — or, on a PostgreSQL setup, whether or not *your* client is running.

All times are **EVE time** (UTC).

## When — the schedule

Pick one schedule kind and set its fields:

- **Interval** — **every** N **minutes** or N **hours**. Good for frequent, clock-agnostic tasks.
- **Days of week** — tick the days (Mon–Sun) and set a **time of day** (e.g. `00:01`). Fires on each ticked day at that time.
- **Monthly** — a **day of month** plus a time of day. Fires once a month.
- **Yearly** — a **month** and **day** plus a time of day. Fires once a year.

For the day-based kinds there's a **Skip if the app was closed on the day** option: leave it off and a fire missed while everything was closed is caught up at the next start; tick it and a missed day is simply skipped.

## What — the action

A task does one of two things.

### Post to Slack or Discord

- **Post to** — choose a destination. One list holds your Slack workspace **channels** and **webhooks**, then your Discord webhooks, each marked **Discord:**. Set them up first under **Settings ▸ Slack** and **Settings ▸ Discord** (see [Posting to Discord](../discord.md)).
- **Do not post if the dynamic sections are empty** — when ticked, the message is held back unless at least one data-reading section (anything but a plain Text section) actually has something to say, so a quiet week doesn't send an empty report.
- **Message** — the body is built from **sections**, in order, as one message (see below). **Add Section** to add one; **Preview** renders the whole thing exactly as it would post, without posting.

### Raise an alert

- Set an **alert title** and **text**. When the task fires, it shows on the [Overview](overview.md) and in the [Alarms](alarms.md) tool until dismissed — the same alert an alarm raises. Useful for a recurring reminder that doesn't need posting anywhere.

## Post sections

A post is assembled from sections. Each carries **its own parameters**, because a task firing at 00:01 has no open screen to read settings from, and each takes an optional **section title**:

- **Text** — a fixed block of text, sent as typed — Slack or Discord markup works, whichever the task posts to.
- **Corp Top 10** and **Corp Monthly Summary** — from [Corp Activity](corp-activity.md); the monthly summary takes which month to cover (a *months-back* offset, so "last month" keeps working every month).
- **Sale Posting** — a rendered [sale posting](sale-posting.md), priced and counted exactly as the Sale Posting tool shows it.
- **Standing Projects** — with options for what to include (for example **Missing** projects nothing is covering, and **Low** ones under ~10 % remaining).
- **[Industry Opportunities](#industry-opportunities-section)** — a table of what's worth building, with filters and columns set in the section.
- **[Indy Park Compare](#indy-park-compare-section)** — your parks compared on a list of jobs, as tables and pictures.
- **[System Index](#system-index-section)** — today's system cost indices and their charts, for systems you list.
- **Corp ISK Trends Chart**, **Corp Activity Trends Chart**, **Corp Kills / Losses Chart** and **Corp Mining Chart** — twelve months of trends, drawn to a PNG and uploaded as an image under the message. On Discord each chart is its own message, under the chart's title.

!!! note "Kept in the section"
    The Industry Opportunities, Indy Park Compare and System Index sections keep everything they need in the section itself. None of them reads the tools' remembered choices, so changing a filter in the tool doesn't change a post. Each is worked out when the post goes out, from the prices and indices held then.

### Industry Opportunities section

The same list as the [Industry Opportunities](industry-opportunities.md) tool, as a table in the message.

**Filters**, every one the tool has:

- **Mode** — **Build & Sell Order** or **Build & Sell to Buy Order**.
- **Price at** — the market.
- **Min 30d ISK Vol**, **Min 30d Unit Vol**, **Min Margin %** and **Min Margin % 30d**. Leave one blank for no filter.
- **Meta Groups** — Tech I, Tech II, Tech III, Faction, Storyline, Abyssal, Structure Tech I, Structure Tech II, Structure Faction and None. A new section ticks all but Faction.
- **Skip Non BPO traceable Items** and **Only blueprints I own**.
- **Exclude Groups** and **Include Groups** — market groups, with **+ Add Group**. An exclusion inside an included group still applies.

**The table:**

- **Section title** — a new section starts with *Industry Opportunities*. Blank prints no title. **Column headers** turns the header row on or off.
- **Columns** — a list you add to with **Add column**, reorder and remove from: Build Cost, Sell Price, Profit / Unit, Margin, Build Time, Slot Days, Profit / Slot Day, Units Sold 30d, Avg Price 30d, Margin 30d, Sales 30d and Profit 30d. The item is always the first column. A new section prints Profit / Unit, Margin, Units Sold 30d and Sales 30d.
- **Headers** — each column has a header you can rename. One left as it is follows the interface language.
- **Sort by** — any column, **Highest first** or **Lowest first**. A new section sorts by Profit 30d, highest first. An item with no figure for the column, such as no sales in 30 days, sorts last either way.
- **Rows** — the top N. A new section posts 10; blank posts them all.

ISK in the post is shortened one step further than in the tool, to K under a million. If no item passes the filters, the section prints nothing.

### Indy Park Compare section

The Compare tab of [Indy Parks](../industry-parks.md), as a post.

- **Section title** — blank uses *Indy Park Compare*.
- **Parks** — which parks to compare. A new section ticks them all; a park added later stays out until you tick it.
- **Post** — any of these:
    - Pictures: **Summary by job (image)**, **Summary by park (image)**, **Cost chart (image)** and **Time chart (image)**.
    - Tables: **Summary by job (table)**, **Summary by park (table)** and **Every job in every park (table)**.
- **Jobs** — the job list, edited just as on the Compare tab, and saved with the section.

A new section posts the summary by job, the cost chart and the time chart. One table goes straight under the section title; several each get a sub-heading. Costs and times are worked out with skills at V.

### System Index section

The [System Index](system-index.md) tool's table and charts, as a post.

- **Section title** — blank uses *System Index*.
- **Post** — **Today's indices (table)**, and a chart (image) for any of the six activities. A new section posts the table and the Manufacturing chart.
- **Systems** — type a name to add a system to the section's own list. The order sets each line's colour.

Each chart is posted with its own legend. Indices show two decimals so the columns line up.

## Using it

1. Create a task and set its **schedule** (interval, days of week, monthly, or yearly — in EVE time).
2. Choose the **action**: post to Slack or Discord, or raise an alert.
3. For a post, pick the destination, then **Add Section** for each part you want and set its parameters. Use **Preview** to check the result — it renders in the destination's own markup, so a Discord task previews as Discord, and names each picture the post will carry.
4. Make sure the task is **Enabled**, and click **Save**. It then fires on its schedule on its own. **Discard Changes** puts the editor back to the saved task.

**Run Now** runs the task as it stands on screen, for real, and counts as its scheduled run.

## Export and import

**Export** and **Import** sit in the toolbar, and move tasks between machines or profiles as a JSON file.

- **Export** saves every task, with its settings written out as readable objects. No run history goes in, and no webhook URLs.
- **Import** only ever adds. Nothing already here is replaced. A task identical to one here is skipped, so importing a file twice adds nothing.
- **Imported tasks come in switched off**, until you look them over. Tick **Enabled** on each one you want to run.
- **The destination** is kept where it still fits. Where it doesn't, it's matched by name to a channel or webhook here; with no match, it's left empty for you to pick.

## Notes

- **Pictures need a Slack channel or a Discord webhook.** A Slack webhook can't carry a file, so a task aimed at one skips its chart sections, and the run reports how many were skipped rather than claiming success. An Indy Park Compare or System Index section posts only its tables there, and warns you in the editor when it has pictures chosen. A Discord webhook carries them all.
- **Pictures need no window.** They're drawn the same in a scheduled run, on a [background worker](../background-processing.md) and on screen.
- **Long posts go out in parts.** A message over about 3,500 characters on Slack, or 1,900 on Discord, is sent as several messages, in order. Each section is kept whole in one message; only a table longer than a whole message is split, between rows, with its header repeated at the top of the next message. If a part is refused, the run says which parts arrived.
- The reports the Scheduler posts use the **same definitions** the on-screen tabs use, so a scheduled post can't drift from what the corresponding screen shows. Headings — Top 10 and monthly summary alike — can be overridden in the **Corp Top 10 / Summary** settings, and Top 10 headings carry the month they cover.
- **Discord posts never ping anyone.** `@everyone`, `@here` or a role in a section's text is posted as plain text.
- **A deleted destination fails the run.** If a task's Discord webhook was removed from Settings, the run reports *That webhook has been deleted.* Pick another destination.
- To post a report manually instead of on a schedule, use the relevant tool's own **Post to Slack** or **Post to Discord** button (e.g. on [Corp Activity](corp-activity.md)).
