# Scheduler

The Scheduler runs tasks on a timetable — posting reports to Slack or raising an in-app alert — so recurring updates like a corp Top 10 or a monthly summary go out on their own, without you being at the screen.

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

### Post to Slack

- **Post to** — choose a destination from your Slack settings; workspace **channels** and **webhooks** appear in one list. (Connect Slack first under **Settings ▸ Slack**.)
- **Do not post if the dynamic sections are empty** — when ticked, the message is held back unless at least one data-reading section (anything but a plain Text section) actually has something to say, so a quiet week doesn't send an empty report.
- **Message** — the body is built from **sections**, in order, as one message (see below). **Add Section** to add one; **Preview** renders the whole thing exactly as it would post, without posting.

### Raise an alert

- Set an **alert title** and **text**. When the task fires, it shows on the [Overview](overview.md) and in the [Alarms](alarms.md) tool until dismissed — the same alert an alarm raises. Useful for a recurring reminder that doesn't need Slack.

## Post sections

A Slack post is assembled from sections. Each carries **its own parameters**, because a task firing at 00:01 has no open screen to read settings from, and each takes an optional **section title**:

- **Text** — a fixed block of text (Slack markup works).
- **Corp Top 10** and **Corp Monthly Summary** — from [Corp Activity](corp-activity.md); the monthly summary takes which month to cover (a *months-back* offset, so "last month" keeps working every month).
- **Sale Posting** — a rendered [sale posting](sale-posting.md), priced and counted exactly as the Sale Posting tool shows it.
- **Standing Projects** — with options for what to include (for example **Missing** projects nothing is covering, and **Low** ones under ~10 % remaining).
- **Corp ISK Trends Chart** and **Corp Activity Trends Chart** — twelve months of trends, drawn to a PNG and uploaded as an image under the message.

## Using it

1. Create a task and set its **schedule** (interval, days of week, monthly, or yearly — in EVE time).
2. Choose the **action**: post to Slack, or raise an alert.
3. For a Slack post, pick the destination, then **Add Section** for each part you want and set its parameters; use **Preview** to check the result.
4. Make sure the task is **Enabled**, and save. It then fires on its schedule on its own.

## Notes

- **Chart sections need a Slack channel.** An incoming webhook can't carry a file, so a task aimed at a webhook skips the two chart sections, and the run reports how many were skipped rather than claiming success.
- The reports the Scheduler posts use the **same definitions** the on-screen tabs use, so a scheduled post can't drift from what the corresponding screen shows. Headings — Top 10 and monthly summary alike — can be overridden in the **Corp Top 10 / Summary** settings, and Top 10 headings carry the month they cover.
- To post a report manually instead of on a schedule, use the relevant tool's own "Post to Slack" action (e.g. on [Corp Activity](corp-activity.md)).
