# Languages

EVE Console can be shown in the same eight languages as the EVE client:

| Language | In the list as |
| --- | --- |
| English | English |
| German | Deutsch |
| Spanish | Español |
| French | Français |
| Japanese | 日本語 |
| Korean | 한국어 |
| Russian | Русский |
| Simplified Chinese | 简体中文 |

Every screen, dialog, alert and message is translated, and so are the names of items, ships, systems, stations, corporations and factions — they come from the game's own data, so they match what you see in the client.

## Choosing a language

1. Open **Settings** (the **⚙** gear button, top-right) ▸ **Other**.
2. Under **Appearance**, pick a **Language**.
3. A note says **The new language is used from the next start.** Click **Restart now** to switch straight away, or carry on and it takes effect the next time you start EVE Console.

The first entry, **System default**, follows your computer's display language. It shows in brackets which language that comes to — German Windows starts EVE Console in German. A system language that isn't one of the eight falls back to English.

The list names each language in the language you're using, then as it calls itself, for example **German (Deutsch)**, so you can find your way back from a language you can't read.

!!! info "Per computer, not shared"

    Like the theme and UI scale, the language is remembered for this client only. Two clients on the same [PostgreSQL](storage-postgresql.md) database can each use their own language. A `--profile` copy has its own setting too.

### Dates and numbers

Dates and numbers follow your computer's regional format when that format is in the same language as the interface — English on a UK computer keeps UK dates. When the two differ, for example Chinese on a computer set to an English region, they follow the interface language instead, so a date doesn't appear in a different language from the text around it.

Numbers you type are read in the interface's format first: in German `1,5` is one and a half.

### Chinese, Japanese and Korean fonts

The app picks a font made for each of these languages, so characters are drawn in the right style. Windows already has them. On Linux, install your distribution's **Noto Sans CJK** fonts if Chinese, Japanese or Korean text shows as boxes (most desktops ship them).

## Names from the game

Item, ship, system, station, corporation and faction names come from the game's static data (the SDE), which carries every name in all eight languages. The [SDE](getting-started.md#first-launch) import stores them all; when it finishes, **Settings ▸ SDE** reports how many names it stored for each language. A version that needs more from the SDE imports it again by itself on its first start.

- **Search boxes find either name.** Type the name you see, or paste the English from a website — both work.
- **Item Valuation reads any client's list.** A list copied from the game client is read whatever language the client is in. See [Item Valuation](tools/item-valuation.md).
- **The alarm editor takes names in your language.** A ship, place or item typed in the interface language, or in another of the client's languages, is found and stored by its English name. The list shows it in your language, with the English in its tooltip.

## What stays in English

Some text is deliberately not translated:

- **What the AI model reads.** The [AI agent's](ai-agent-eden.md) instructions, tool descriptions and notes stay in English. The agent **answers** in the interface language, unless you write to it in another, and gives item and place names in English as the database holds them.
- **What is saved or matched.** Settings, alarms and filters store the English name, so they keep working after you switch language.
- **The [Error Log](tools/error-log.md).** Its messages are kept in English, so they can be searched and reported.
- **Mail commands.** A store's command words (**PRICES**, **ORDER**, **STATUS**, **CANCEL**, **INFO**, **HELP**) stay English, in every language.

!!! note "Background messages come in the worker's language"

    When several clients share a PostgreSQL database, one of them does the [background work](background-processing.md) and writes the status lines the others show. Those lines arrive in that client's language.

## Stores

Each store has a **Language** of its own, on the store's **General** tab: **Same as the app** (the default) or any of the eight. Buyers get the price list, order confirmations and status mail, and the web site's item names, in that language. You can play in one language and sell in another. See [Stores](stores/index.md).

## Posts

Sale postings and corp reports you post to Slack or Discord are written in the interface language, item names included, as the screen shows them.
