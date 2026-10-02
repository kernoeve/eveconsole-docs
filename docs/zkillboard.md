# zKillboard

EVE Console merges kills from **zKillboard** into its own killmail data. It's on by default, and there's nothing to sign up for — no key and no contact details.

The settings are in **Settings** — click the **⚙** gear button in the top-right of the title bar, then open the **Kill Mails** tab.

## Why zKillboard

ESI only returns a killmail when you were the **victim** or got the **final blow**. If you took part in a kill without the final blow — routine in fleet fights — ESI never shows it to you.

zKillboard tracks every participant, so merging it in fills that gap. Kills from zKillboard go into the same killmail data as the ones from ESI. They never duplicate or overwrite what ESI already provided.

## Turning it on or off

**Enable zKillboard kill import** is **on by default**. Untick it to stop all zKillboard import. A status line under the box shows what live capture is doing.

## Scope

Choose which kills are captured:

- **My characters & corp only** (the default) — kills and losses of your authorised characters and their corporations. EVE Console asks zKillboard about each of them at the interval set under **Live Poll Interval**.
- **Capture all kills** — every kill in New Eden, streamed live from zKillboard's real-time feed (R2Z2). There's no interval to set; the feed paces itself.

!!! warning "Capture all kills grows the database quickly"

    With **Capture all kills**, every kill in New Eden is stored, not just your own. The database grows much faster than with **My characters & corp only**.

    To keep it in check, turn on the **Others** kill-mail rule under **Settings ▸ Data Retention**. It trims everyone else's kills after a window you choose — 7 days by default — while your own are kept on a separate, longer window. See [Data retention](storage-postgresql.md#kill-mails).

!!! note "zKillboard's rate limit"

    zKillboard's real-time feed (R2Z2) allows 15 requests a second from one internet address, and refuses that address for up to an hour when it's exceeded. Every R2Z2 request EVE Console makes — the live feed and the daily dumps — keeps to at most four a second, so up to three copies of EVE Console behind one internet connection stay under the limit together.

    If zKillboard does refuse, EVE Console stops asking for as long as it was told to (or five minutes, doubling up to an hour while refusals continue). The live capture and backfill status lines say they are paused, and until when.

### Live Poll Interval

**Check zKillboard for new kills every (s)** sets how often **My characters & corp only** asks zKillboard for new kills. The default is **300** seconds; the range is 60–3600. It isn't used with **Capture all kills**.

## Backfill History

Live capture only catches kills from the time the app is running. The backfill loads zKillboard's **daily kill dumps** and merges in every kill that matches your scope.

It also runs by itself once an hour, to fill any days missed while the app was closed. The button is mainly for pulling in history from before you started using EVE Console.

1. Set **Backfill the last (days)**. The default is **30**; the range is 1–3650.
2. Click **Start Backfill**. A progress bar shows how far it has got; **Cancel** stops it.

**last full day** shows the latest day whose dump has been fully imported.

!!! note "The latest day lags"

    zKillboard publishes each day's dump some hours after that day ends. So **last full day** is usually yesterday or the day before, never today. Live capture covers the time in between.

## Post Kills to zKillboard

**Post killmails to zKillboard** is **off by default**. When it's on, EVE Console submits kills it has that zKillboard is missing — usually ESI kills that nobody else uploaded.

- Each kill is checked against zKillboard first, so only kills it really lacks are submitted.
- A kill is only considered once it's a few hours old, so a kill still working its way through zKillboard is left alone.
- Nothing is ever submitted twice.

**Covered from** shows the oldest kill confirmed to be on zKillboard. Anything older can't be judged missing, so it's left alone. To widen the range, backfill further back.

## Checking on it

The **Killmails** tab of [Background Processes](tools/background-processes.md) shows the zKillboard state: whether it's on, the scope, and **Coverage** — how far the daily dumps have been imported. Below that, one row per stage says what each is doing: **ESI kill mail details**, **Live capture**, **Daily dump backfill** and **Posting to zKillboard**.

zKillboard import is background work. When several clients share a [PostgreSQL](storage-postgresql.md) database, it runs on the client doing the background work — see [Background processing](background-processing.md).

## Where the kills show up

Everything that reads killmails reads the merged data:

- the [Killmails](tools/killmails.md) browser;
- [Corp Activity](tools/corp-activity.md) — the recent kills and losses, and the **Killmails** tab;
- the **Personal Killmails** section of the [Overview](tools/overview.md);
- the **Ship kills** and **Pod kills** overlays on the [Universe Map](tools/universe-map.md), and each system's **Kills** tab;
- kills and losses in [Players & NPCs](tools/entities.md).

With **My characters & corp only**, those only show kills involving you and your corporations. The Universe Map's kill overlays in particular are only cluster-wide with **Capture all kills**.
