# FAQ & Troubleshooting

## Where is my data stored?

Locally, in a SQLite database at `%LOCALAPPDATA%\EveConsole\EveConsole.db`. Nothing
is uploaded; the app only talks to CCP's ESI API to refresh your data.

## Can I run a second, separate copy?

Yes. Start the app with `--profile <name>` and it runs a completely separate copy —
its own config, database and caches — under
`%LOCALAPPDATA%\EveConsole\Profiles\<name>` (`~/.local/share/EveConsole/Profiles/<name>`
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
