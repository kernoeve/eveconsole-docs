# Battle Report

Follow a fight live, or look back at one: who was on which side, what each side lost, who did the damage and how the fight went, across one system or several. Battles can be saved and opened again, and **Find fights** looks through a period for the big ones.

Open it from the left sidebar under **Corp / Interactions**, after **Killmails**.

!!! info "Your own database, on your screen only"
    Battle Report reads only the killmails EVE Console has stored. It asks nothing more of zKillboard or ESI, so your [zKillboard](../zkillboard.md) scope and the kill-mail rules under **Settings ▸ Data Retention** decide what it can show. ISK is the app's own market valuation of each kill. Nothing is published anywhere: a battle report is for you alone.

## What it shows

On the left, **New battle**, **Find fights** and **Saved battles**. Each saved battle shows how many systems it covers and when it starts; one marked live can still gain kills. Its delete button forgets a saved battle, after asking; its kills stay in the database.

On the right, the battles open now, each in a tab of its own. Several can be open at once, and each has its own **Watch live** switch. Closing a tab stops watching it; a saved battle stays in the list.

### Systems and times

A battle is one or more systems, each with its own start and end, in EVE time:

- **Add:** — type a system or constellation. Picking a constellation adds all its systems.
- **From (EVE time):** and **To (EVE time):** — the times new systems get, written like `2026-01-31 18:00`. Leave **To** blank for a fight still going. **Apply to all** gives every system in the list these times.
- Each system in the list keeps its own times, which you can change there. A system whose end is blank or still to come is marked **live**: it can still gain kills.
- **Kill link or id** with **Use kill** — paste a kill link or a kill's number to start from that kill: its system, from 30 minutes before to 30 minutes after.

A new battle starts at one hour ago, with no end. Then:

- **Open report** — reads the kills and shows the report. The systems and times fold away to give it room.
- **Name this battle** and **Save** — keeps it in **Saved battles**. Once saved, its changes keep themselves.
- **Watch live** — updates the report as kills arrive. Only systems with a blank or future end can gain kills. While it is on, a **LIVE** badge shows and the status says how many of the systems are being watched.

You can also start a battle from a kill: the **Battle report** link on a kill in the [Killmails](killmails.md) browser, or a gate camp's kills in the [Intel](intel.md#camps) tool.

### The report

A summary line gives the kills, pilots and ISK lost, the times, and how long ago the last kill was. A note says when your zKillboard settings limit what the report can hold.

**Team cards** side by side, one per team, each in the colour it has on the chart. Your own side is tagged **Your side**. Each card shows:

- **ISK lost** and **Efficiency** — the share of all ISK lost in the battle that the other teams lost.
- **Pilots** and **Damage dealt** (damage a team did to itself left out).
- **Ships lost**, **Pods lost**, **Structures lost** and **Deployables lost**, counted apart, and **Damage to structures**. A citadel's damage isn't counted as damage to ships, and a field of mobile tractor units isn't counted as structures.

Then four tabs:

- **Sides** — each team's alliances, corporations without one, and lone pilots in NPC corporations, with **Pilots**, **Kills**, **Lost**, **ISK lost** and **Damage**. Sides are worked out from who shot whom, with your side first. Move a side with its arrows to the team on the left or right; once you have, the sides present stay where they are. **Add a team** adds one, and an empty team can be removed. Click an alliance to list its corporations.
- **Pilots** — one line per pilot with their totals: **Ship**, **Damage**, **Kills**, **Lost**, **ISK lost**, **Corporation** and **Alliance**. Click a pilot who flew several hulls to see each hull as a line of its own. A lost hull is tinted. Sort by a column for the top damage or the biggest losses.
- **Ships** — each hull a team flew, with **Group**, **Pilots**, **Lost**, **ISK lost** and **Damage**. Click a hull to open it into alliances (or corporations with none), and an alliance into its corporations.
- **Timeline** — a chart of ISK lost over the fight, then each loss, newest first: **Time**, **Team**, **Ship**, **Victim** with corporation and alliance, **Final blow** with corporation and alliance, **System**, **Attackers** and **Value**. A kill that has just come in while watching is marked for a few seconds.

**Double-click** a line on **Pilots** or **Timeline** to open its killmail in the [Killmails](killmails.md) browser. A line without a loss does nothing, and a line with several losses gives a menu to pick one. Names are links: a pilot, corporation or alliance opens in [Players & NPCs](entities.md), and a ship name on **Ships** opens in the Item Browser.

### Find fights

**Find fights** looks through a period for large fights and lists them, the largest by ISK lost first, up to 100.

- **Last 24 hours**, **Last 3 days**, **Last 7 days**, or your own **From (EVE time):** and **To (EVE time):** (blank is up to now). A period can be at most 31 days.
- **At least pilots:** — the smallest fight to list. 50 to start.
- **Only fights my pilots were in**.
- **Find**.

Each fight shows **Started**, **Duration**, **Systems**, **Kills**, **Pilots**, **ISK lost** and **Largest sides**, with a mark on fights your pilots were in. **Open** starts a battle with its systems and times filled in, ready to adjust.

A fight is found where kills cluster in a system: a quiet of 30 minutes ends a stretch, and a stretch of fewer than 5 kills isn't looked at. Stretches in different systems are joined into one fight when they run within 15 minutes of each other and share enough pilots, up to 12 hours in all. A longer fight shows as two, for you to put together. Fights are sized by pilots, not kills, and each window is padded by 5 minutes either side. A fight whose last kill was within the last 30 minutes is left open-ended, ready to watch live.

## Using it

1. Press **New battle**, or **Find fights** and **Open** one.
2. Add the systems with **Add:**, and set their times. Leave the end blank for a fight still going.
3. Press **Open report**.
4. Tick **Watch live** to follow it as kills arrive.
5. Name it and **Save** it to come back to it later.
6. Move sides between teams on **Sides** if the guess is wrong.

## Notes

- **Live watching** asks the database every 4 seconds for kills the battle doesn't hold yet, by kill id. So a killmail that arrives late is still picked up, and it works when another client on the same [PostgreSQL](../storage-postgresql.md) database is the one importing kills. A system stays watched for 10 minutes past its end, for mails that land late.
- **Coverage.** With the [zKillboard](../zkillboard.md) scope on **My characters & corp only**, a report only has kills your characters and corporations were on, and **Find fights** only finds those fights. With zKillboard import off, it only has your own characters' and corporations' kills from ESI. For other people's fights, choose **Capture all kills**.
- Kills trimmed by the **Others** kill-mail rule under **Settings ▸ Data Retention** (7 days by default when on) are gone from battle reports too.
- A report holds at most 20,000 kills; past that it says so, and you narrow the time.
- Saved battles are kept in the database, so with PostgreSQL every PC sees them.
