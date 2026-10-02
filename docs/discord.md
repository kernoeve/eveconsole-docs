# Posting to Discord

EVE Console can post into **Discord channels**: the corp Top 10, the monthly summary, sale postings and [scheduled tasks](tools/scheduler.md). It posts through **webhooks** — no bot to invite and no sign-in. A webhook is a link a channel hands out; anything sent to the link appears in that channel.

The settings are in **Settings** — click the **⚙** gear button in the top-right of the title bar, then open the **Discord** tab. Slack has its own tab beside it, and the two work side by side.

Nothing is posted until you press a **Post to Discord** button or set up a scheduled task.

## Make a webhook in Discord

You need the **Manage Webhooks** permission on the channel — usually a server's managers have it. If you don't, ask one of them for a webhook link.

1. In Discord, open the channel's settings: **Edit Channel** (the cog beside the channel name).
2. Go to **Integrations ▸ Webhooks** and click **New Webhook**.
3. Give it a name and, if you like, an avatar. Posts from EVE Console appear under this name and picture.
4. Click **Copy Webhook URL**.

The link starts with `https://discord.com/api/webhooks/`.

!!! warning "A webhook URL is a secret"

    A webhook URL works like a password: anyone who has it can post to that channel. Don't paste it in chat, in a screenshot or in a bug report.

    EVE Console never shows the link in full and never writes it to a log; the list shows only the webhook's number. If a link leaks, delete the webhook in Discord and add a new one here.

## Add it to EVE Console

On **Settings ▸ Discord**, under **Webhooks**:

1. Type a **Name** — what you'll pick it by, such as "Corp announcements".
2. Paste the link into the URL box.
3. Click **Add**.
4. Click **Test** on the new row. EVE Console posts one short line to the channel, and the status line says whether Discord accepted it. Check the channel to be sure.

Add as many webhooks as you like — one per channel you want to post to.

- A Slack webhook link is refused here; add it on the **Slack** tab instead.
- To post into a **thread**, add `?thread_id=` and the thread's id to the end of the link. EVE Console keeps it.
- **Remove** takes a webhook out of the list. It's refused while a part of the app still posts to it (see below) — pick a different webhook there first.

## Choose where each part posts

Under **Where each part posts**, pick the webhook for each part of the app:

- **Corp Activity — Top 10** — the [Top 10 Lists](tools/corp-activity.md) tab.
- **Corp Activity — Monthly Summary** — the [Monthly Summary](tools/corp-activity.md) tab.
- **Sale Posting** — the **Posting** tab of [Sale Posting](tools/sale-posting.md).

A part's **Post to Discord** button appears once a webhook is set for it and you close Settings. Pick **(none)** to hide the button again. Changes save as you make them.

[Scheduled tasks](tools/scheduler.md) don't use these picks: each task chooses its own destination, and every webhook on this tab is in its list.

## What a post looks like

- **Discord's own formatting.** The text is what the **Discord** export format gives for the same content, so tables line up in code blocks and headings are bold.
- **Nobody is pinged.** Every post tells Discord to ignore mentions, so `@everyone`, `@here`, a role or a pilot's name in corp data never notifies anyone.
- **Long posts go out in parts.** Discord takes up to 2,000 characters per message, so EVE Console sends anything over 1,900 as several messages, in order. A heading stays with its table, and a code block is never cut open: a table longer than one message is split between rows, with its header repeated at the top of the next message.
- **Charts are attached.** A scheduled task aimed at a Discord webhook uploads its chart sections as images, one message each, under the chart's title.

## Posting twice

Each **Post to Discord** button remembers when it last posted. Press it again within 24 hours and EVE Console asks before posting a second time. This is kept apart from Slack: posting to Slack doesn't count as having posted to Discord, or the other way round.

## When a post fails

The status line beside the button (or the task's last-run result in the Scheduler) says what went wrong:

- **Discord no longer accepts this webhook** — the webhook was probably deleted in Discord. Make a new one, add it, and pick it where the old one was used.
- **Discord kept asking to slow down** — Discord's rate limit. EVE Console waits and retries a few times on its own; if it still can't post, try again in a minute.
- **Posted 2 of 3 messages…** — the first parts arrived and a later one was refused. The message says which. The parts that arrived stay in the channel.

## Notes

- Webhooks only post. EVE Console doesn't read anything from Discord.
- The webhook list is stored in the database, so on a [PostgreSQL setup](storage-postgresql.md) every client shares it.
- For the EVE Console community server, see the Discord link at the bottom of every page.
