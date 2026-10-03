<p align="center">
  <img src="images/banner.png" alt="EVE Console">
</p>

# EVE Console

**EVE Console** is a local-first, free, open-source desktop companion for [EVE Online](https://www.eveonline.com/). All of your data stays on your machine in a local SQLite database, refreshed from CCP's ESI API while the app runs.

!!! note

    These docs are a work in progress alongside the app (currently Beta, `0.9.x`). Pages will fill out over time.

## New here?

Start with **[Getting Started](getting-started.md)** — download, install, first launch, and authorizing your characters.

## Setup guides

Before most tools are useful, configure a few things:

- **[Configuring Markets](configuring-markets.md)** — define which market(s) prices come from, and how per-item prices are calculated (including lowball/highball handling and build-cost-based pricing).
- **[Industry Parks](industry-parks.md)** — define the structures used for industry/build-cost calculations, including per-category structures and per-item exceptions.
- **[AI Agent (Eden)](ai-agent-eden.md)** — optional conversational assistant with access to your local data, plus optional text-to-speech and voice input.
- **[Storage & PostgreSQL](storage-postgresql.md)** — stay on the default local SQLite file, or move to a PostgreSQL server so several clients can share one set of data.
- **[Background Processing](background-processing.md)** — run the ESI polling, imports and alarms without a desktop window — headless, on another machine, or in a container.
- **[Logs & Map Data](logs-and-map-data.md)** — read EVE's game and chat logs (including intel channels) and collect the public map statistics the Universe Map's overlays use.
- **[zKillboard](zkillboard.md)** — merge in kills from zKillboard, so kills you helped on without the final blow are counted too.
- **[Posting to Slack](slack.md)** and **[Posting to Discord](discord.md)** — send corp summaries, Top 10s, sale postings and scheduled reports to your channels.
- **[Themes](themes.md)** — pick from the light, dark and tinted themes; the whole interface repaints live.
- **[Languages](languages.md)** — use EVE Console in any of the game's eight languages, with item and system names as the game client shows them.

On Linux? See **[Running on Linux](running-on-linux.md)** for downloads, the one dependency, and headless service setups.

## Functionality

EVE Console is organized into tools you open from the left sidebar, grouped as below; two more — Alarms and the Scheduler — open from the title bar. Each opens as a tab; you can show two side by side or drag one out into a window of its own (see [Tabs, split view and separate windows](getting-started.md#tabs-split-view-and-separate-windows)). Each tool below links to its own page with details on what it does and how to use it.

### General

- **[Overview](tools/overview.md)** — the landing dashboard: at-a-glance alerts, recent notifications and killmails, and a customizable grid of summary panels.
- **[Worklist](tools/worklist.md)** — one always-current list of what to do next across all your characters, rebuilt on each refresh from up to eleven sources (industry jobs, purchases, logistics, corp projects, skills, Planetary Industry and more).
- **[Characters](tools/characters.md)** — an in-app character sheet (skills, attributes, and info) for your authorized characters, handy when you'd rather not log the character into the game.

### Assets

- **[Assets](tools/assets.md)** — search and browse all of your personal and corp assets across stations, structures, and containers.
- **[Item Browser](tools/item-browser.md)** — look up any item with its description, attributes, and blueprint/industry info, plus live market orders and price history for your configured markets.
- **[Inventory Levels](tools/inventory-levels.md)** — track a defined list of items (on hand, in build, on order) against target levels, similar to jEveAssets stockpiles.

### Ships

- **[Fitting](tools/fitting.md)** — open your saved fits and your characters' in-game fittings, and build or edit fits with their numbers worked out for a chosen pilot.

### Structures / Navigation

- **[Structure Browser](tools/structure-browser.md)** — browse player-owned structures from ESI's public list, and link them to your Indy Parks.
- **[Universe Map](tools/universe-map.md)** — one continuous map from the whole cluster down to a single system, with overlays for security, sovereignty, kills, industry and intel — plus a detailed page for every system.
- **[Route Planner](tools/route-planner.md)** — plan a route on the map with an avoid list and Thera/Turnur shortcuts, and set it as your in-game destination.
- **[Jump Planner & Jump Range](tools/jump-planner.md)** — map tabs for planning capital jump routes, with distance and fuel for every leg, and for showing what is in jump range.
- **[Jump Bridges](tools/jump-bridges.md)** — the jump bridges the map routes through, read from ESI or added by hand, with their zones.

### Industry

- **[Industry Jobs](tools/industry-jobs.md)** — monitor your active and finished industry jobs (manufacturing, research, reactions) across characters and corp.
- **[Indy Parks](industry-parks.md)** — define the structures you build in (type, rigs, system, tax) so build-cost and production calculations use your real bonuses.
- **[Production Calculator](tools/production-calculator.md)** — plan production runs: full build cost, materials needed, and a multi-level breakdown, with ME levels and an optional final blueprint-copy cost.
- **[Planetary Industry](tools/planetary-industry.md)** — your colonies at a glance: extractor timers, storage and production forecasts, with alerts and Worklist tasks for the chores.
- **[Industry Opportunities](tools/industry-opportunities.md)** — scan items for build-and-sell profit, ranked by margin and profit per slot-day using your build costs and market prices.

### Market / Trade

- **[Market Overview](tools/market-overview.md)** — a regional market dashboard: order and sales summaries, breakdowns by group and type, and a daily-sales chart.
- **[Item Valuation](tools/item-valuation.md)** — paste a list of items and value it against your own market data — market, build and reprocessed side by side, with buyback percentages and multi-station comparison.
- **[LP Market Values](tools/lp-market-values.md)** — what your loyalty points are worth, corp by corp, priced against the market.
- **[Market Levels](tools/market-levels.md)** — monitor sell-order inventory for a chosen list of items in a specific market, so you can spot stock and restock gaps.
- **[Contracts](tools/contracts.md)** — browse your personal and corp contracts and their items, with valuations.
- **[Trade Opportunities](tools/trade-opportunities.md)** — compare two markets to surface profitable hauls between them, with cargo/ISK limits, group exclusions, and profit per unit and per m³.
- **[Standing Buy Orders](tools/standing-buy-orders.md)** — declare the buy orders you keep standing and see whether they're actually up (missing, outbid, run down, or near expiry).
- **[Order Tracker](tools/order-tracker.md)** — track your active and historical market orders and how they're filling.
- **[Sales Tracker](tools/sales-tracker.md)** — review your completed sales and the profit on each, with a toggle for how profit is calculated.
- **[Sale Posting](tools/sale-posting.md)** — build shareable sale postings from your stock and render them to Plain, Slack, Discord, Markdown, HTML or BBCode.
- **[Stores](stores/index.md)** — sell to other players from EVE Console through two shop fronts: an [EVE Mail Store](stores/eve-mail.md) (buyers mail commands) and a [Web Storefront](stores/web-site.md) (buyers order on a site you host).

### Finance

- **[Net Worth](tools/net-worth.md)** — a running chart of your total value over time across wallets, assets, and jobs.
- **[Income & Expense](tools/income-expense.md)** — a categorized breakdown of where your ISK comes from and goes over a chosen period.
- **[Wallet](tools/wallet.md)** — wallet balances plus journal and transaction history for your characters and corp.

### Corp / Interactions

- **[Corp Activity](tools/corp-activity.md)** — corp-wide activity: ratting/industry/mining tax, donations, kills, projects, and Top 10 leaderboards, over 24h or monthly.
- **[Killmails](tools/killmails.md)** — your and your corp's recent kills and losses, with values and details.
- **[Players & NPCs](tools/entities.md)** — a searchable browser for pilots, corps and alliances, with their zKillboard kills and losses, plus NPC agents, corps and factions.

### Communication

- **[Eve Mail](tools/eve-mail.md)** — read and compose EVE mail from inside the app.
- **[Notifications](tools/notifications.md)** — view your in-game EVE notifications.

### Data / Logs

- **[Background Processes](tools/background-processes.md)** — a live monitor of the app's polling and syncing: recent ESI calls, what's due next, and how each sweep is progressing.
- **[ESI Explorer](tools/esi-explorer.md)** — a power-user browser for the raw ESI data the app has synced into its local database: filter, sort, and page through the underlying tables.
- **[Error Log](tools/error-log.md)** — a viewer for the app's own internal error log, filterable by date range — handy for troubleshooting and bug reports.
- **AI Usage** — what each AI agent turn cost and did: tokens, cache use and the estimated price; see [AI Usage & Cost](ai-agent-eden.md#ai-usage-cost).
- **[Game & Chat Logs](tools/logs.md)** — search your local EVE game and chat logs; intel-channel messages become sightings on the Universe Map.

### Title bar

- **[Alarms](tools/alarms.md)** — opened from the alarm light beside the ⚙ gear: conditions you define that the app checks on a timer and tells you about once, when they first become true.
- **[Scheduler](tools/scheduler.md)** — opened from the title bar: run reports on a timetable — post a corp Top 10, monthly summary, sale posting or charts to [Slack](slack.md) or [Discord](discord.md), or raise an alert — on an interval or a calendar, in EVE time.

## Help

- **[FAQ & Troubleshooting](faq-and-troubleshooting.md)**
- **[Discord](https://discord.gg/H6NaAjJMar)** — join the community for help, questions, and release news.

---

*EVE Console is a third-party tool and is not affiliated with or endorsed by CCP Games. EVE Online and the EVE logo are trademarks of CCP hf.*
