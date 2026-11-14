# Scheduler

The Scheduler runs tasks on a timetable — posting reports to Slack or Discord, or raising an in-app alert — so recurring updates like a corp Top 10 or a monthly summary go out on their own, without you being at the screen.

Open it from the **clock icon in the title bar** (it isn't in the left sidebar).

!!! warning
    The Scheduler is still taking shape (Beta). Its stored settings may change between releases.

It has two tabs:

- **Tasks** — the list of tasks and the editor. **New Task** always opens here.
- **Calendar** — what will run, by month, week or day (see [The calendar](#the-calendar)).

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

- **Post to** — choose a destination. One list holds your Slack workspace **channels** and **webhooks**, then your Discord webhooks, each marked **Discord:**. Set them up first under **Settings ▸ Slack** and **Settings ▸ Discord** (see [Posting to Slack](../slack.md) and [Posting to Discord](../discord.md)).
- **Do not post if the dynamic sections are empty** — when ticked, the message is held back unless at least one data-reading section (anything but a plain Text section) actually has something to say, so a quiet week doesn't send an empty report.
- **Message** — the body is built from **sections**, in order (see below). **Add Section** to add one; **Preview** renders the whole thing in the destination's markup, without posting.

### Raise an alert

- Set an **alert title** and **text**. When the task fires, it shows on the [Overview](overview.md) and in the [Alarms](alarms.md) tool until dismissed — the same alert an alarm raises. Useful for a recurring reminder that doesn't need posting anywhere.

## Post sections

A post is assembled from sections. Each carries **its own parameters**, because a task firing at 00:01 has no open screen to read settings from, and each takes an optional **section title**:

- **Text** — a fixed block of text, sent as typed — Slack or Discord markup works, whichever the task posts to. On Slack it can go in a box (see [Text in a box](#text-in-a-box)).
- **Corp Top 10** and **Corp Monthly Summary** — from [Corp Activity](corp-activity.md); the monthly summary takes which month to cover (a *months-back* offset, so "last month" keeps working every month). The Top 10 lists are **Ratting Tax**, **Mining — Reprocessed Value**, **Kills**, **Solo Kills**, **Project Contributors** and **Industry Tax**; tick the ones to post.
- **Sale Posting** — a rendered [sale posting](sale-posting.md), priced and counted exactly as the Sale Posting tool shows it.
- **Standing Projects** — with options for what to include (for example **Missing** projects nothing is covering, and **Low** ones under ~10 % remaining), a **Text above the table** box, and the columns to show.
- **[Industry Opportunities](#industry-opportunities-section)** — a table of what's worth building, with filters and columns set in the section.
- **[Indy Park Compare](#indy-park-compare-section)** — your parks compared on a list of jobs, as tables, boxes and pictures.
- **[System Index](#system-index-section)** — today's system cost indices and their charts, for systems you list.
- **Corp ISK Trends Chart**, **Corp Activity Trends Chart**, **Corp Kills / Losses Chart** and **Corp Mining Chart** — twelve months of trends, drawn as a picture. See [Pictures](#pictures) for where they can go.

!!! note "Kept in the section"
    The Industry Opportunities, Indy Park Compare and System Index sections keep everything they need in the section itself. None of them reads the tools' remembered choices, so changing a filter in the tool doesn't change a post. Each is worked out when the post goes out, from the prices and indices held then.

**Solo Kills** counts kills where no other pilot is on the killmail. NPCs and structures on the mail don't count as another pilot. Like **Kills**, it keeps its number when the section shows only the share.

### Standing Projects section

- **Project type** and **Report** — which kind of project, and **Missing projects**, **Missing and low projects** or **All projects**.
- **Section title** and **Column headers**.
- **Text above the table** — a few lines of your own, printed under the title, on Slack and in the text table alike. Emoji, links and mentions work, and a mention really pings on Slack.
- **ISK Left column** and **Last Completed column** — the optional columns.
- **On Slack, post with images and lined-up columns** — posts the list in a box (see [Standing projects in a box](#standing-projects-in-a-box)). With it ticked, a **Picture** can be chosen for the box.
- **Projects to include** — exactly the projects to report on. A project defined later doesn't join on its own.

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

- **Section title** — a new section starts with *Industry Opportunities*. Blank prints no title in the text table; Slack's box always has one, so it uses *Industry Opportunities* there. **Column headers** turns the header row on or off.
- **Columns** — a list you add to with **Add column**, reorder and remove from: Build Cost, Sell Price, Profit / Unit, Margin, Build Time, Slot Days, Profit / Slot Day, Units Sold 30d, Avg Price 30d, Margin 30d, Sales 30d and Profit 30d. The item is always the first column. A new section prints Profit / Unit, Margin, Units Sold 30d and Sales 30d.
- **Headers** — each column has a header you can rename. One left as it is follows the interface language.
- **Sort by** — any column, **Highest first** or **Lowest first**. A new section sorts by Profit 30d, highest first. An item with no figure for the column, such as no sales in 30 days, sorts last either way.
- **Rows** — the top N. A new section posts 10; blank posts them all.
- **On Slack, post with images and lined-up columns** — posts the list in a box (see [Industry Opportunities in a box](#industry-opportunities-in-a-box)). A new section starts with it ticked.

ISK in the post is shortened one step further than in the tool, to K under a million. If no item passes the filters, the section prints nothing.

### Indy Park Compare section

The Compare tab of [Indy Parks](../industry-parks.md), as a post.

- **Section title** — blank uses *Indy Park Compare*.
- **Parks** — which parks to compare. A new section ticks them all; a park added later stays out until you tick it.
- **Post** — any of these:
    - For Slack: **Summary by job (Slack table)** and **A box for each job (Slack)** (see [Indy Park Compare on Slack](#indy-park-compare-on-slack)).
    - Pictures: **Summary by job (image)**, **Summary by park (image)**, **Cost chart (image)** and **Time chart (image)**.
    - Tables: **Summary by job (table)**, **Summary by park (table)** and **Every job in every park (table)**.
- **Market value from** and **Price** — where a job box reads its market value. Left at **Default market** and **Default price**, they follow your Market defaults, with any price overrides.
- **Jobs** — the job list, edited just as on the Compare tab, and saved with the section.

A new section posts the Slack table and the job boxes, which use no picture uploads. One table goes straight under the section title; several each get a sub-heading. Costs and times are worked out with skills at V.

A build job is labelled with the item and **— Build**, for example *Vexor — Build*, in the tables, boxes and pictures alike.

The **Summary by job (image)** picture puts each park in a column, with its cost over its time.

### System Index section

The [System Index](system-index.md) tool's table and charts, as a post.

- **Section title** — blank uses *System Index*.
- **Post** — any of these:
    - **Today's indices, with the 7-day change (Slack table)** (see [System Index on Slack](#system-index-on-slack)).
    - **Today's indices, with the 7-day change (image)** — the same table as a picture.
    - **Today's indices (table)** — the text table.
    - **All six charts in one picture (image)**, and a chart (image) for any of the six activities on its own.
- **Systems** — type a name to add a system to the section's own list. The order sets each line's colour.
- **Lowest emoji**, **Rising emoji** and **Falling emoji** — the marks the Slack table uses. Blank uses the standard one shown in the box (`:large_green_circle:`, `:small_red_triangle:` and `:small_red_triangle_down:`). A custom emoji only shows in a workspace that has it.

A new section posts the Slack table and the six charts in one picture. Each chart is posted with its own legend. Indices show two decimals so the columns line up.

## Slack formats

Several sections can post on Slack in Slack's own layout — boxes, lined-up columns, tables and small pictures — instead of a text table in a code block. **Discord always gets text**, and so does the preview.

| Section | How you turn it on | What Slack gets | What Discord gets |
|---|---|---|---|
| Text | **Box on Slack**: Narrow, Standard or Wide | The text in a box, its first line as the title | The text as written |
| Corp Top 10 | **On Slack, post with images and lined-up columns** | A box per list, two to a row | The text tables |
| Standing Projects | **On Slack, post with images and lined-up columns** | One box with a picture, your text and the rows | The text table |
| Industry Opportunities | **On Slack, post with images and lined-up columns** | A box with the top item featured | The text table |
| System Index | **Today's indices, with the 7-day change (Slack table)** under **Post** | A Slack table | The text table of today's indices |
| Indy Park Compare | **Summary by job (Slack table)** or **A box for each job (Slack)** under **Post** | A Slack table, or a box per job | The summary by job text table |

- **New sections start with it on**, for Top 10, Standing Projects and Industry Opportunities, and System Index and Indy Park Compare start with their Slack outputs chosen. **Saved sections keep what they had** until you change them, so an existing schedule keeps posting text tables.
- **No sign-in is needed.** The portraits, logos and item pictures in these boxes come from EVE's own image server, so they show on a Slack channel and a Slack webhook alike, without [Online Services](../online-services.md).
- **If Slack refuses the format**, the same numbers go out as the text table, and the task's last-run result says *Slack would not take the format with images (…), so this went as text.*
- **Emoji in titles** are drawn in a box's title, as in a message.

### Text in a box

Under the text, **Box on Slack** picks **No box**, **Narrow**, **Standard** or **Wide**. In a box, the text's first line becomes the box's title, and a **Picture** can be chosen to sit beside it. Discord and plain posts keep the text as written.

### Top 10 boxes

Each list is a box, two to a row, stacking on a phone. Number 1 comes first with a larger picture, a **Leader** line, then its name, value and share. Every row after it shows that entity's own portrait or logo, its value and its share. **Show only the share of the total, not the ISK** still hides the ISK.

The share is each one's share of the whole month, the same figure the Top 10 tab shows, in the boxes and the text table alike.

### Standing projects in a box

The whole list is one box: the picture beside the title, the **Text above the table**, a line, then the rows in columns, with the same columns and order as the text table.

- **Picture** — **None**, **Character**, **Corporation**, **Alliance**, **Faction**, **NPC corporation**, **Agent** or **Item type**, then type at least two letters to find the one you want. An item uses its render where the image server has one, otherwise its icon or its blueprint.
- Slack's box always has a title, so a blank **Section title** uses the default there. The text table still prints none.
- A name too wide for its column is cut short and ends in "...". The rows leave out the word ISK, since the header says **ISK Left**.
- A list too long for one box carries on in another, with its header row.

### Industry Opportunities in a box

Number 1 is featured at the top, labelled **Top Item**, with its picture and its figures in the order of your columns. Its 30-day figures sit together under **Activity over the last 30 days**, two across, with the sort column in bold. The other items follow, one row each with an icon, under the header row.

The box has room for only so many columns:

- With the Slack format ticked, **Add column** offers only the columns that still fit, and says *Slack's box has no room for more columns* when it's full.
- A saved section with too many keeps them, and the editor names the ones the Slack post leaves out. The text table, and Discord, still get them all.
- When the post goes out, the real figures decide: columns that don't fit are dropped from the right, including from number 1's figures. That can include the sort column.

### System Index on Slack

A Slack table with the systems down the side and the six activities across, each value with its change over the last 7 days, in points. The lowest index for each activity gets the **Lowest emoji** (a green circle by default), and rises and falls get the **Rising emoji** and **Falling emoji** (red arrows by default). A note under the table explains the marks.

### Indy Park Compare on Slack

- **Summary by job (Slack table)** — a column for the job, then a cost and a time for each park. The best park for each job is marked, and the others show how far behind the best they are.
- **A box for each job (Slack)** — the job's picture and details at the top, then one row per park with its cost, its time and how far behind the best each is. Beside the picture: units and market value for a build, copies and runs for a copy, the target blueprint and its runs, ME and TE for invention, and the ME or TE range for research. Two boxes sit side by side in the desktop app.

## Pictures

The corp trend charts, and the pictures of an **Indy Park Compare** or **System Index** section, are drawn on your computer and sent as images:

| Destination | Pictures |
|---|---|
| Slack channel | Uploaded to Slack, under the section's text |
| Slack webhook | Only when signed in to [Online Services](../online-services.md): uploaded to eveconsole.com, and the webhook posts each one by its address, under its title |
| Discord webhook | Attached, one message each, under the picture's title |

A Slack webhook can't take a file: Slack has to fetch a picture from a web address. That's why it needs Online Services. Signed out, a task aimed at a webhook skips its chart sections and leaves out the other sections' pictures, and its result says how many sections it skipped. The editor says so under each section this affects.

!!! warning "Pictures for a webhook are public"
    When signed in, a section with pictures for a Slack webhook shows the note *This Slack webhook shows pictures by their address, so they are uploaded to eveconsole.com and kept for 12 months. Anyone with the link can see them.* See [What leaves your computer](../online-services.md#what-leaves-your-computer).

**Each section's pictures go straight after its text**, before the next section starts, on Slack and Discord alike. Sections with no pictures between them still share a message. A section's heading prints once at the top whenever anything in it is posted, even a section with only pictures, and the pictures' own titles don't repeat it.

## The calendar

The **Calendar** tab shows what will run, in EVE time, from now on.

- **‹**, **Today** and **›** move back, to today, and forward. **Month**, **Week** and **Day** pick the view.
- **Month** shows each task in its day. A day with more than fits ends in a line such as **+3 more**, which opens that day.
- **Week** and **Day** have one row per hour, with today and the current hour marked.
- Clicking a day's number or heading opens that day.
- A run is an entry with its time and the task's name. Several runs of one task in the same cell are one entry with a count, such as `00:06 Market check ×96`. Hover an entry to see the task's schedule and type.
- Posts and alerts have different colours, with a legend.
- Click an entry to open the task in the editor on the **Tasks** tab. If the task on screen has unsaved changes, you're asked first.
- Weeks start on the day your computer's regional settings use.

What the calendar leaves out:

- **Past days are blank.** Only each task's last run is kept, not a history.
- **Tasks switched off** are not shown.
- **Interval tasks are estimates after their next run**, because each run counts from when the one before it really happened.

It follows the same rules as the runner, so a slot already used by **Run Now** isn't shown, and a run owed since the app was closed shows as now.

## Using it

1. Create a task with **New Task** and set its **schedule** (interval, days of week, monthly, or yearly — in EVE time).
2. Choose the **action**: post to Slack or Discord, or raise an alert.
3. For a post, pick the destination, then **Add Section** for each part you want and set its parameters. Use **Preview** to check the result — it renders in the destination's own markup, so a Discord task previews as Discord. It names each picture the post will carry, or says it will be skipped. A section that Slack gets in boxes or a Slack table shows its text table in the preview, with a line saying so.
4. Make sure the task is **Enabled**, and click **Save**. It then fires on its schedule on its own. **Discard Changes** puts the editor back to the saved task.

**Run Now** runs the task as it stands on screen, for real, and counts as its scheduled run.

**Delete** asks first, for any saved task: *Delete "…"? This cannot be undone.*

## Export and import

**Export** and **Import** sit in the toolbar, and move tasks between machines or profiles as a JSON file.

- **Export** saves every task, with its settings written out as readable objects. No run history goes in, and no webhook URLs.
- **Import** only ever adds. Nothing already here is replaced. A task identical to one here is skipped, so importing a file twice adds nothing.
- **Imported tasks come in switched off**, until you look them over. Tick **Enabled** on each one you want to run.
- **The destination** is kept where it still fits. Where it doesn't, it's matched by name to a channel or webhook here; with no match, it's left empty for you to pick.

## Notes

- **Pictures need no window.** They're drawn the same in a scheduled run, on a [background worker](../background-processing.md) and on screen.
- **Long posts go out in parts.** A message over about 3,500 characters on Slack, or 1,900 on Discord, is sent as several messages, in order. Each section is kept whole in one message; only a table longer than a whole message is split, between rows, with its header repeated at the top of the next message. If a part is refused, the run stops there and says which parts arrived, so nothing is posted after a gap.
- The reports the Scheduler posts use the **same definitions** the on-screen tabs use, so a scheduled post can't drift from what the corresponding screen shows. Headings — Top 10 and monthly summary alike — can be overridden in the **Corp Top 10 / Summary** settings, and Top 10 headings carry the month they cover.
- **Discord posts never ping anyone.** `@everyone`, `@here` or a role in a section's text is posted as plain text.
- **A deleted destination fails the run.** If a task's Discord webhook was removed from Settings, the run reports *That webhook has been deleted.* Pick another destination.
- To post a report manually instead of on a schedule, use the relevant tool's own **Post to Slack** or **Post to Discord** button (e.g. on [Corp Activity](corp-activity.md)).
