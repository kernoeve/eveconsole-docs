# FAQ & Troubleshooting

## Where is my data stored?

Locally, in a SQLite database in the app's data folder:

- **Windows:** `%LOCALAPPDATA%\EVE Console Data\EveConsole.db`
- **Linux:** `~/.local/share/EveConsole/EveConsole.db`

The same folder holds `config.json`, backups, profiles and downloaded models. Nothing
is uploaded; the app only talks to CCP's ESI API to refresh your data. If you moved
the database or switched to [PostgreSQL](storage-postgresql.md), **Settings ▸
Database** shows where it is.

## My data isn't in `%LOCALAPPDATA%\EveConsole` any more

That folder now holds only the program, which installing and updating replace as a
whole. On its first start, the new version moved your settings and data to
`%LOCALAPPDATA%\EVE Console Data` and left a note, **Your EVE Console data has
moved.txt**, in the old folder. Nothing was lost, and reinstalling or uninstalling no
longer touches your data. See [Where your data lives on
Windows](getting-started.md#where-your-data-lives-on-windows).

If the old folder still holds your data, the move couldn't finish — usually because
another copy of EVE Console was running. The [Error Log](tools/error-log.md) says why,
and the next start tries again. Close every copy, then start EVE Console once.

## "Upgrade the database?" at start

You've started a newer version on a database an older one last used. The upgrade
can't be undone — earlier versions can't open the database afterwards — so EVE
Console asks before it changes anything. **Yes** upgrades it and starts; **No**
closes the app and leaves the database as it was, so you can take a backup first or
go back to your earlier version. See [Upgrading the
database](getting-started.md#upgrading-the-database).

## "This build is older than the database"

Another copy of EVE Console, on a newer version, has already upgraded this database,
and this older copy can't safely open it. The dialog checks for an update: click
**Update and restart** to install it and carry on. If it can't offer one — the tarball
and source builds can't update themselves, or the version isn't released yet — use
**Releases page** to download a newer build. See [When this copy is older than the
database](getting-started.md#when-this-copy-is-older-than-the-database).

## The SDE import says "Waiting for the database"

On SQLite only one thing can write to the database at a time. If background polling
holds the write lock for longer than SQLite will wait (30 seconds), an SDE or
Hoboleaks import pauses and shows **Waiting for the database: something else is
writing to it. Trying this write again (attempt N)…**. It waits a few seconds and makes
that one write again, as often as it takes, until it goes through or you cancel the
import, then carries on where it was. Nothing is
lost or written twice, and the import doesn't start over. When it finishes, its
warnings say how many times it had to wait, and the [Error Log](tools/error-log.md)
names what held the lock.

You don't need to do anything. If the waits go on for a long time, check the Error
Log for what is holding the database. On [PostgreSQL](storage-postgresql.md) imports
never wait like this.

## Can I run a second, separate copy?

Yes. Start the app with `--profile <name>` and it runs a completely separate copy —
its own config, database and caches — under
`%LOCALAPPDATA%\EVE Console Data\Profiles\<name>` (`~/.local/share/EveConsole/Profiles/<name>`
on Linux). You can give a folder path instead of a name. A new profile starts empty,
like a fresh install, and runs alongside your normal copy. The window title shows
the profile name, and **Settings ▸ Database** says which folder is in use. It's
handy for trying a development build without touching your real data.

## My settings were lost or look reset

EVE Console saves `config.json` in one step, so it's never left half-written, and
keeps the previous version beside it as `config.json.bak`. If `config.json` is
corrupt or locked by another program when the app starts, it reads the `.bak`
instead of starting from defaults. If your settings still look wrong, close the app
and check whether `config.json.bak` in the data folder holds them.

## Where is the Save button in Settings?

There isn't one: Settings saves as you go. A tick or a pick saves at once, and text
saves when you pause typing, leave the box or close the window. The one exception is
switching database engine, which takes **Save and Restart**. See [Settings save as you
go](getting-started.md#settings-save-as-you-go).

## Can I use EVE Console in another language?

Yes — German, Spanish, French, Japanese, Korean, Russian and Simplified Chinese as
well as English. Choose under **Settings ▸ Other ▸ Language** and restart. See
[Languages](languages.md).

## Do I have to use the AI agent?

No. It's optional and stays inactive until you configure it. See
[AI Agent (Eden)](ai-agent-eden.md).

## Prices / build costs look wrong or empty

Make sure you've [configured a market](configuring-markets.md) and, for build costs,
an [industry park](industry-parks.md). Prices and build costs are (re)calculated as
market data refreshes while the app is running, so give it a refresh cycle after
first setup.

## Is this affiliated with CCP?

No. EVE Console is a third-party tool and is not affiliated with or endorsed by
CCP Games. EVE Online and the EVE logo are trademarks of CCP hf.

<!-- Add more entries here as common questions come up. -->
