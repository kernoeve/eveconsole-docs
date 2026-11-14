# Online Services

EVE Console's online services run on eveconsole.com. Right now they do one thing: they host the pictures a [scheduled post](tools/scheduler.md) sends to a **Slack webhook**, so the webhook can show them.

Online Services are **optional**. Everything else in EVE Console works without them, and nothing is sent to eveconsole.com until you sign in.

The settings are in **Settings**: click the **⚙** gear button in the top-right of the title bar, then open the **Online Services** tab.

## Why a webhook needs it

A [Slack webhook](slack.md#add-a-webhook) can't carry a file. It can only show a picture that is already on the web, by its address: Slack fetches the picture from that address and shows it in the channel. So a chart drawn on your computer has to be put somewhere Slack can reach before a webhook post can show it. Online Services is that place.

You don't need it for:

- **Slack channels you post to after [Connect to Slack](slack.md#connect-to-slack).** EVE Console uploads the pictures to Slack directly.
- **Discord webhooks.** They carry pictures as attachments.
- **Slack posts with images and columns** (the boxes and tables described in [Slack formats](tools/scheduler.md#slack-formats)). Their portraits, logos and item pictures come from EVE's own image server, which Slack can already reach.

## Sign in

1. On **Settings ▸ Online Services**, click **Read the Terms** if you want to read them first. Signing in means you agree to them.
2. Click **Sign In with EVE**. EVE's own sign-in page opens in your browser.
3. Sign in to EVE if it asks, and pick **one character**. The page asks for no permissions: this sign-in can't read your wallet, assets, mail or anything else.
4. The browser shows **Sign-In Successful** and names the character. Close the tab and go back to the app.

The status line now reads **Signed in as** and the character's name. Under it, a usage line says how much you have stored and how many uploads you have used today, each against its limit.

- The app waits five minutes for you to finish in the browser. If you closed the tab or changed your mind, click **Cancel**.
- If something goes wrong, the browser shows **Sign-In Failed** with the reason, and the same reason appears in the status line.
- Any character will do. It doesn't have to be one registered in EVE Console. Its name is what Settings shows.

### One sign-in per database

The sign-in belongs to EVE Console's database, not to one computer. On a [PostgreSQL setup](storage-postgresql.md), every EVE Console on that database uses it, with no restart. A scheduled task can then post pictures to a webhook from whichever client runs it, including a [background worker](background-processing.md).

## What leaves your computer

Only these, and only to `api.eveconsole.com`:

- **At sign-in:** the one-time token EVE's sign-in page gives back for the character you picked. It carries no permissions. The service checks it with EVE, answers with a key of its own, and the token is thrown away. EVE Console keeps no EVE token for this. The tokens of your registered characters, which can read your game data, are never sent.
- **The key**, with each request below. It is kept in the database.
- **The pictures** a scheduled post sends to a Slack webhook: charts and tables drawn from your data, for example a corp's ISK trends, a park cost comparison or a system index chart. Only pictures from sections you chose, and only when that task runs.
- **A usage check** each time Settings opens while you're signed in, to show the usage line.
- **Sign-out**, when you click **Sign Out**.

As with any web request, the service also sees your computer's internet address. The webhook link itself is never sent to eveconsole.com. EVE Console posts to Slack directly, with the picture's address in the message.

What the service keeps is listed in the [terms](https://eveconsole.com/services/terms): for example the character's name and number, and each picture you upload until it expires.

!!! warning "Uploaded pictures are public to anyone with the link"

    A picture's address is long and random, but anyone who has it can open the picture without signing in, including everyone in the channel it was posted to. Pictures are kept for 12 months, then removed. Slack may keep its own copy for longer.

    Don't schedule a picture to a webhook if its content shouldn't be seen outside the channel.

## Sign out

Click **Sign Out**. EVE Console tells the service to end the key, and forgets it from the database. If the service can't be reached, the key is forgotten anyway and never used again.

- Signing out affects every EVE Console on the database.
- Pictures already uploaded stay online until they expire, and posts that show them keep showing them. EVE Console has no screen yet to list or delete uploaded pictures.
- According to the terms, the service keeps a record of the character after you sign out.

If the service stops accepting the key, uploads fail with **Not signed in.**, and the next time Settings opens, EVE Console forgets the key and shows **Not signed in.** again. Sign in again to carry on.

## Without Online Services

Signed out, a scheduled task aimed at a Slack webhook:

- **Skips its chart sections.** The task's last-run result says how many it skipped and where to sign in.
- **Leaves out the pictures** of its **Indy Park Compare** and **System Index** sections, and posts their tables and boxes.
- Posts everything else as normal, including the boxes and tables with images.

The Scheduler's editor warns you when a section has pictures that a webhook won't show until you sign in.

## When an upload fails

The reason goes into the task's last-run result in the [Scheduler](tools/scheduler.md), beside whatever did get through. The run still counts as done, so a missed picture isn't sent again until the task's next scheduled run:

- **Not signed in. Sign in again under Settings, Online Services.** — the key is no longer accepted.
- **The storage limit has been reached. Images free up as they expire.**
- **Today's upload limit has been reached.** The count starts again each day.
- **The image is too large to upload.**
- **This character may not use the online services.**
- **eveconsole.com could not be reached.** — the service or your connection is down.

If Slack refuses a picture after it was uploaded, EVE Console deletes it from the service again so it doesn't hold storage. It still counts towards the day's uploads.

## Notes

- Limits are set by the service and may change; the usage line always shows the current ones.
- The sign-in uses a local address on your computer to receive the answer from EVE's page, as registering a character does. It works the same on Windows, Linux and macOS.
