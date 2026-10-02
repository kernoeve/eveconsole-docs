# Corp Activity

A corporation dashboard covering 24-hour and monthly activity, wallet income and expense, ratting/industry/mining taxes, donations, killmails, corp projects, and Top 10 leaderboards.

Open it from the left sidebar under **Corp / Interactions**.

## What it shows

A toolbar with a **Corporation** picker, a live status line, and a **Refresh** button sit above a set of tabs:

- **Activity (24H)** — a summary bar (players active, income, expenses over the last 24 hours), three side-by-side leaderboards (Ratting, Industry, Mining by value), and a "Recent Kills & Losses" killmail list.
- **Monthly Activity** — a per-month table (Total Income, Total Expense, Ratting Tax, Industry Tax, Project Payouts, Units Mined, Kills, Losses, ISK Efficiency, Players Active) plus monthly ISK and count charts (the kills/losses chart plots ISK efficiency on its own 0–100% axis). See [Players Active](#players-active) for who is counted.
- **Income** and **Expense** — each has a **Summary** sub-tab (income/expense grouped by wallet reference Type, with Count and Amount) and a **Detail** sub-tab (the individual journal rows).
- **Ratting Taxes**, **Industry Taxes**, **Donations** — each has a **Summary** sub-tab (a ranked list of payers/donors by amount) and a **Detail** sub-tab (journal rows). Ratting, industry and donations also drive daily charts.
- **Mining** — a mining ledger with **Summary** (date, character, ore type, quantity, reprocessed value) and **Detail** sub-tabs.
- **Killmails** — corp kills and losses: a **Summary** sub-tab ranking characters by Kills/Losses, a daily kills/losses chart, and a **Detail** sub-tab listing individual killmails.
- **Projects** — corp projects across **Active**, **History**, and **Standing Projects** sub-tabs, with a detail panel showing project info, configuration, and a ranked contributor list (contributed / percent / payout).
- **Top 10 Lists** — leaderboards for a chosen month/year: Ratting Tax, Mining (units mined), Kills, Project Contributors, and Industry Tax. Each entry shows rank, character, amount, and share of the category total. **Export to Clipboard**, **Export (No ISK)**, **Post to Slack** and **Post to Discord** share them.
- **Monthly Summary** — a formatted corp summary for a chosen month/year, with a clipboard-format selector, **Export to Clipboard**, **Post to Slack** and **Post to Discord**. It's the same summary the [Scheduler](scheduler.md) can post on a timetable.

Most ISK figures are abbreviated (K / M / B); killmail rows use a zKillboard-style layout with ship render, system/security, victim, and final-blow columns.

### Players Active

**Players Active** counts corporation **members** only: characters seen acting while they were in the corp. That means a login seen by member tracking, a kill or loss, moon mining, a contract issued from the corp, a corp industry job, a project or medal, or the corp's tax on their ratting and mission income. Former members count for the months they were in the corp. Customers, users of the corp's structures, NPCs and other corporations never count; other wallet and contract counterparties count only if they're current members who had joined by that month.

The players-active figure in the **Activity (24H)** header is counted the same way. Both can be lower than versions before 0.9.15 showed, which also counted outsiders.

## Using it

- **Corporation** — pick the corp to inspect; the first available corp is selected automatically. Changing corp reloads every tab.
- **Refresh** — forces a full reload. The dashboard also auto-refreshes: a light refresh every 60 seconds and a full refresh (including per-tab detail rows) every 5 minutes.
- **Per-tab period selectors** — the tax, donation, mining, kills, income, and expense tabs each have their own period dropdown (7 days to 1 year; most default to 30 days). The daily chart on the main view defaults to 90 days.
- **Top 10 period** — choose Month and Year; the lists reload for that window. **Export to Clipboard** and **Export (No ISK)** copy the leaderboards out.
- **Post to Slack** and **Post to Discord** — post the Top 10 or the monthly summary to the channel set for it. Each button shows only once that service has somewhere to post this part: a Slack channel under **Settings ▸ Slack**, a webhook under **Settings ▸ Discord** (see [Posting to Discord](../discord.md)). Both show when both are set, each with its own status line. The Top 10 is posted without ISK amounts, like **Export (No ISK)**.
- **Long posts** — a post over about 3,500 characters on Slack, or 1,900 on Discord, goes out as several messages, in order. A section (a heading and its table) is kept whole in one message; only a table longer than a whole message is split, between rows, with its header repeated at the top of the next message.
- **Posting twice** — press a post button again within 24 hours and the app asks first. Slack and Discord keep track separately.
- **Standing Projects** — add, clone, edit, delete, and refresh standing project definitions; rows flag near-complete or inactive projects, and a deliver-item row can be opened in the item browser.
- Clicking a killmail row can open it in the [Killmails](killmails.md) browser.

## Notes

- This is a corporation-scoped tool: it needs valid corp tokens with the relevant wallet, industry, mining, killmail, and projects scopes. Empty tabs usually mean the required scope or data has not been fetched yet.
- Value figures (e.g. mining reprocessed value) depend on a configured market — see [Configuring Markets](../configuring-markets.md).
- Moon mining comes from your refineries' mining ledgers, which ESI serves for about the last 90 days, one row per miner, ore and day. EVE Console keeps every day it has fetched, so mining history builds up past those 90 days for as long as the app keeps polling. Versions before 0.9.15 kept only each miner's latest day per ore, so **Units Mined**, the **Mining** tab and the **Top 10** mining list read low; the first poll after upgrading restores the last ~90 days in full.
- Top 10 leaderboards honour an exclude list, so specific characters or corporations can be kept out of the rankings, on screen and in scheduled posts. Set it under **Settings ▸ Corp Top 10 / Summary ▸ Top 10 Exclude List**: the name search lists your own characters and corporations first, then anyone else the app knows of or ESI can find. The same tab sets the **Top 10 List Titles**, which save as you type.
- The corporation list is populated from your authorized corp tokens; see [Getting Started](../getting-started.md).
