# Scheduler

The Scheduler runs tasks on a timetable — posting reports to Slack or raising an in-app alert — so recurring updates like a corp Top 10 or a monthly summary go out on their own, without you being at the screen.

Open it from the **clock icon in the title bar** (it isn't in the left sidebar).

!!! warning
    The Scheduler is still taking shape (Beta). Its stored settings may change between releases.

## What it shows

Your scheduled **tasks**, each with a **schedule**, an **action**, and — for a post — the **sections** it is built from.

### Schedule

A task can fire on an **interval**, on chosen **days of the week**, **monthly**, or **yearly** — all in **EVE time**.

### Action

Each task either:

- **posts to Slack**, or
- **raises the same alert** an [alarm](alarms.md) raises.

### Post sections

A Slack post is assembled from sections, each carrying its own parameters (a task firing at 00:01 has no open screen to read settings from):

- **Text** — a fixed block of text.
- **Corp Top 10** and **Corp Monthly Summary** — from [Corp Activity](corp-activity.md).
- **Sale Posting** — a rendered [sale posting](sale-posting.md).
- **Standing Projects**.
- **Corp ISK Trends Chart** and **Corp Activity Trends Chart** — drawn to PNG and uploaded as images.

## Using it

1. Create a task and set its **schedule** (interval, days of week, monthly, or yearly — in EVE time).
2. Choose the **action**: post to Slack, or raise an alert.
3. For a Slack post, add the **sections** you want and set each one's parameters.
4. Save; the task then fires on its schedule on its own.

## Notes

- **Chart sections need a Slack channel.** An incoming webhook can't carry a file, so if a task targets a webhook the two chart sections are skipped, and the run reports how many were skipped rather than claiming success.
- The reports the Scheduler posts are the **same definitions** the on-screen tabs use, so a scheduled post can't drift from what the corresponding screen shows. Headings — Top 10 and monthly summary alike — can be overridden in the **Corp Top 10 / Summary** settings, and Top 10 headings carry the month they cover.
- To post a report manually instead of on a schedule, use the relevant tool's own "Post to Slack" action (e.g. on [Corp Activity](corp-activity.md)).
