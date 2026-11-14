# Posting to Slack

EVE Console can post into **Slack**: the corp Top 10, the monthly summary, sale postings and [scheduled tasks](tools/scheduler.md). There are two ways in, and you can use both:

- **Connect to Slack** — sign in once through your browser. EVE Console then posts **as you**, under your own name, into any channel you're a member of. This is the usual way.
- **A webhook** — a link a workspace hands out that posts into one fixed channel. Use it for a workspace you can't connect to as yourself, such as an alliance Slack that hands out webhooks but not app access.

The settings are in **Settings** — click the **⚙** gear button in the top-right of the title bar, then open the **Slack** tab. Discord has its own tab beside it (see [Posting to Discord](discord.md)), and the two work side by side.

Nothing is posted until you press a **Post to Slack** button or set up a scheduled task.

## Connect to Slack

1. On **Settings ▸ Slack**, click **Connect to Slack**. Slack opens in your browser.
2. Sign in to Slack if it asks, and pick the **workspace** to connect (top-right of Slack's page).
3. Slack lists what EVE Console asks for: to post messages and upload files as you, and to see the names of your channels. Click **Allow**.
4. The browser shows **Slack connected**. Close the tab and go back to the app.

The status line under the buttons now reads **Connected — posting as** your name **in** the workspace, and the channel lists below are filled in.

- EVE Console never sees your Slack password. Slack sends the browser to a page on eveconsole.com, which hands the approval straight back to the app on your computer; on its own that hand-off is useless to anyone else.
- The app waits five minutes for you to finish in the browser. If you closed the tab or changed your mind, click **Cancel**.
- One workspace at a time. To switch, click **Connect to Slack** again and pick the other workspace.
- Some workspaces only allow apps an admin has approved. If Slack says so on its page, ask a workspace admin — or ask for a webhook instead (below).

!!! tip "Try it on yourself first"

    The channel lists include **Note to Self** — your own direct message with yourself in Slack. Point a part of the app at it to see exactly what a post looks like before sending one to a channel.

## Add a webhook

A webhook comes from whoever runs the workspace: in Slack they add an **Incoming Webhook** for a channel and give you its link. The link starts with `https://hooks.slack.com/services/`. A webhook is tied to the one channel it was made for — nothing in EVE Console chooses where it lands.

On **Settings ▸ Slack**, under **Webhooks**:

1. Type a **Name** — what you'll pick it by, such as "Alliance market".
2. Paste the link into the URL box.
3. Click **Add**.

The webhook now appears in every channel list on this tab, and in the [Scheduler](tools/scheduler.md), as **Webhook:** and its name.

A webhook is not the same as being connected:

- **Posts show the webhook's name**, not yours — whatever name the workspace gave it.
- **It can't thread.** A sale posting's later blocks arrive as separate messages instead of replies under the first.
- **It can't carry a file.** It can only show a picture that is already on the web. So a scheduled task's charts reach a webhook only once you've signed in to [Online Services](online-services.md) (see [Pictures in scheduled posts](#pictures-in-scheduled-posts)).

There's no **Test** button for a webhook: the first post shows whether it works. **Remove** takes one out of the list. It's refused while a part of the app still posts through it (see below) — pick something else there first.

## Choose where each part posts

Under **Channels**, pick where each part of the app posts:

- **Corp Activity — Top 10** — the [Top 10 Lists](tools/corp-activity.md) tab.
- **Corp Activity — Monthly Summary** — the [Monthly Summary](tools/corp-activity.md) tab.
- **Sale Posting** — the **Posting** tab of [Sale Posting](tools/sale-posting.md).

Each list holds your channels, **Note to Self** among them, then your webhooks. Changes save as you make them. A part's **Post to Slack** button appears once it has somewhere to post and you close Settings; hovering the button shows where it posts.

- Private channels are listed only if you're a member. If a channel is missing — new, or just joined — click **Reload Channels**.
- Other people's direct messages and group messages aren't listed.

[Scheduled tasks](tools/scheduler.md) don't use these picks: each task chooses its own destination from the same channels and webhooks, followed by your Discord webhooks.

## What a post looks like

- **Corp Activity uses the format beside the button.** The Top 10 and the monthly summary post in the format picked in the format list next to **Post to Slack** — the same one **Export to Clipboard** uses. Pick **Slack**: headings are bold and tables sit in code blocks, so their columns line up. **Plain Text** is posted as one code block. The Top 10 is posted without ISK amounts, like **Export (No ISK)**.
- **Sale postings are threaded.** Each post block is rendered in Slack's own formatting, whichever format the Posting tab shows. On a channel the first block is the message and the rest go in its thread. Through a webhook each block is its own message.
- **Long posts go out in parts.** Slack cuts a long message wherever the length runs out, straight through a table. So the Top 10, the monthly summary and scheduled posts are sent as messages of up to 3,500 characters each, about a second apart, in order. A heading stays with its table, and a section that fits in one message is never split: a table longer than one message is split between rows, with its header repeated at the top of the next message.
- **Scheduled posts can use boxes, tables and pictures.** See below.

## Scheduled posts: boxes, tables and pictures

A [scheduled task](tools/scheduler.md) can post more than text to Slack. There are two separate things here, and they work differently.

### Boxes and tables

Several sections can post in Slack's own layout instead of a text table in a code block:

- **Text** in a box, narrow, standard or wide, with an optional picture beside its title.
- **Corp Top 10** lists as boxes two to a row, each name with its portrait or logo, and number 1 shown larger as the **Leader**.
- **Standing Projects** as one box with a picture, a few lines of your own and the rows lined up in columns.
- **Industry Opportunities** as a box with the **Top Item** featured and an icon on every row.
- **System Index** as a Slack table, with each index's 7-day change.
- **Indy Park Compare** as a Slack table, or as a box for each job.

Each section has its own option for this. The [Scheduler](tools/scheduler.md#slack-formats) says what each one looks like and how to turn it on.

These work on **both channels and webhooks, with no sign-in**. Their portraits, logos and item pictures come straight from EVE's image server, which Slack can reach by itself. Discord, and any post Slack refuses in this format, get the text tables instead.

### Pictures in scheduled posts

The corp trend charts, and the pictures an **Indy Park Compare** or **System Index** section can post, are drawn on your computer. How they reach Slack depends on where the task posts:

- **A channel** (after **Connect to Slack**): EVE Console uploads each picture to Slack, under the message text.
- **A webhook:** a webhook can't take a file. Slack has to fetch a picture from a web address. So EVE Console uploads it to [Online Services](online-services.md) on eveconsole.com, and posts the picture's address under its title. This needs a sign-in under **Settings ▸ Online Services**.

Signed out, a task aimed at a webhook skips its chart sections and leaves out the other sections' pictures, posts everything else, and says in its result how many sections it skipped. The Scheduler warns you about this in the editor.

!!! warning "Pictures for a webhook are public"

    A picture uploaded for a webhook can be opened by anyone who has its link, and is kept for 12 months. The Scheduler shows a note under any section this applies to. See [What leaves your computer](online-services.md#what-leaves-your-computer).

Pictures go out straight after the section they belong to, before the next section starts.

## Posting twice

Each **Post to Slack** button remembers when it last posted. Press it again within 24 hours and EVE Console asks before posting a second time. On Sale Posting this is kept per posting, so posting one listing doesn't hold up another. Slack and Discord keep track separately: posting to one doesn't count as having posted to the other.

## Keep it safe

!!! warning "Your connection and your webhook links are secrets"

    While connected, EVE Console can post as you in any channel you can reach. A webhook link works like a password: anyone who has it can post to its channel.

    The **Webhooks** list in Settings shows each link in full, so don't share a screenshot of the **Slack** tab, and don't paste a link in chat or in a bug report. If a link leaks, ask the workspace's admins to remove that webhook in Slack, then add the new one here.

- **Disconnect** clears the connection from EVE Console. The parts posting to channels lose their **Post to Slack** buttons; parts set to a webhook keep posting through it.
- **Disconnect** doesn't tell Slack. To cut off access completely, remove EVE Console from the workspace's installed apps in Slack as well.
- The connection, the channel picks and the webhook list are kept in EVE Console's database. On a [PostgreSQL setup](storage-postgresql.md) every client shares them — and so posts as the person who connected.

## When a post fails

The status line beside the button (or the task's last-run result in the Scheduler) says what went wrong. Hover a cut-off status line to read all of it. Slack's own reasons are shown as Slack gives them:

- **token_revoked**, **invalid_auth**, **account_inactive** — the connection is no longer good, usually because it was removed in Slack. Click **Connect to Slack** again.
- **not_in_channel** — you aren't a member of that channel any more. Join it in Slack, or pick another.
- **channel_not_found** — the channel was deleted or archived, or you lost access. Click **Reload Channels** and pick it again.
- **no_service**, **channel_is_archived**, **action_prohibited** — a webhook was removed, its channel archived, or the workspace blocked it. Ask for a new webhook.
- **Slack has not granted this connection permission to upload files** — a chart upload from a connection made before EVE Console asked for that. Click **Connect to Slack** again.
- **Posted 2 of 3 messages…** — the first parts arrived and a later one was refused, even after a second try. The message says why. The parts that arrived stay in the channel; a scheduled run counts as done, so the start isn't posted again.
- **Slack refused it: …** — a scheduled post where nothing arrived. The task tries the whole post again on its next pass.
- **Slack would not take the format with images (…), so this went as text.** — Slack refused a section's boxes or table, so the same numbers were posted as the text table. The reason is Slack's.
- **… chart section(s) skipped: to show images, a Slack webhook needs a sign-in under Settings, Online Services.** — a task aimed at a webhook while signed out of [Online Services](online-services.md). Everything else was posted.
- **… chart(s) failed: …** — a picture didn't arrive. Each is named with the reason, which for a webhook can be one of the [Online Services errors](online-services.md#when-an-upload-fails).
- **That webhook has been deleted.** — a scheduled task's webhook was removed from Settings. Removing a webhook isn't stopped by tasks that use it, so pick another destination in the task.

## Notes

- EVE Console only reads the list of your channels, to fill the pickers. It doesn't read messages.
- Sale postings and corp reports are written in the interface language (see [Languages](languages.md)).
