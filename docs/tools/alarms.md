# Alarms

Conditions you define that the app checks on a timer and tells you about once they become true, so you can be told when something has happened instead of watching for it yourself.

Open it from the **alarm light** in the title bar, beside the **⚙** settings gear. The light is lit while any alarm is armed, with the number of armed alarms beside it. Right-click it to mute alarms on this client.

## How an alarm works

Each alarm is a **condition** the app evaluates repeatedly in the background, plus one or more **actions** that run when it fires. While the condition stays false, nothing happens; when it becomes true, the alarm fires.

- **It fires once per thing.** An alarm only announces something it hasn't announced before, so a condition that simply stays true doesn't repeat. (A price alarm that has already told you an item is cheap won't nag every check — it fires again only when a *new* matching listing appears.)
- **Continuous or one shot.** A *Continuous* alarm stays armed until you disable it; a *One shot* alarm disables itself after firing once.
- **Check every (sec).** How often the condition is evaluated. Some checks suggest their own interval when you pick them.
- **Cooldown (sec).** An optional minimum gap between firings, on top of the "not announced before" rule.
- **Active hours.** Optional **Active From** / **Thru** wall-clock times restrict when the alarm is even evaluated (for example `18:00`–`02:00`, which wraps past midnight). Leave them blank for "always". Outside its hours the condition isn't checked at all.
- **Enabled.** Each alarm has its own on/off switch.

### What happens when it fires

Add one or more **actions** to an alarm. You can combine them:

- **A recorded alert** — always logged, and shown on the [Overview](overview.md) dashboard. This happens regardless of the machine-local actions below, and other clients are unaffected.
- **A sound** — pick one (or **Add Sound…** your own). It can **repeat until acknowledged**, or until the situation ends on its own.
- **Words to say** — spoken directly by **text-to-speech**, with no agent or model involved (it just needs a voice configured under [Settings ▸ AI Agent](../ai-agent-eden.md), and works with the agent switched off). Leave it blank to speak what the check itself composed. Placeholders: `{alarm}` `{summary}` `{count}` `{time}` `{date}`.
- **An instruction for the agent** — the [AI agent](../ai-agent-eden.md) is told what fired and phrases it in its own words (speaking aloud if you have TTS set up). If the agent isn't configured, this is recorded as an alert instead.

A few conditions fire in **stages** — an escalating sequence where each stage has its own actions (see *[Undocked too long](#undocked-too-long-wake-up-call)*).

!!! note
    Sounds, dialogs and agent notifications play **on this machine only**. The recorded alert is kept either way, so a background/headless client still logs the event even with nothing to play it.

## Condition types

When you press **New Alarm**, you pick the kind of check. Each kind has its own settings, and settings that don't apply to your choices are hidden.

### Date / time

Fires at a specific date and time, and optionally repeats on a fixed interval thereafter. Use it for reminders and anything scheduled. An occurrence that came due **while the app was closed fires at the next start** rather than being skipped.

### Intel report

Fires when a hostile pilot is reported near what you're watching. It reads the intel channels already being parsed under **Settings ▸ Chat Logs** (see [Logs & Map Data](../logs-and-map-data.md#chat-logs)), and kills in the watched systems too.

**Watch around** — what the range is drawn around:

- **Undocked characters** (the default) — wherever your online characters are in space. Docked characters aren't watched.
- **Characters** — your characters wherever they are while online, docked or not.
- **Systems** — a list of systems you name.

With **Undocked characters** or **Characters**, the **Characters** list narrows it to the characters you name; leave it empty for all of them. With **Systems**, add each system to the **Systems** list.

**Range:**

- **Jumps** — how many gate jumps out from each character or system to watch. The default is **5**; **0** watches only the system itself. The most is 15.
- **Light years** — optional. Also watch every system within this many light years, however many gates away — what a jump drive or a cyno puts in reach. The most is 20; empty or 0 is off.

A report caught by either range fires.

**Filters:**

- **Min players** — only fire when the report is of at least this many pilots. The default is 1.
- **Ignore no visual** — skip reports flagged NV, where someone is relaying a contact they can't actually see.

**Kills count as sightings.** A kill in a watched system places its attackers there at that moment, with their exact hulls. So a kill with hostile pilots among the attackers fires the alarm too, even if nobody called it in. NPC attackers don't count, the victim isn't a sighting, and **Min players** counts the hostile attackers. A gang that is both reported and seen on a kill within the same few minutes is one alert, and the spoken line adds "Seen on a kill".

*Hostile* means the same as on the [Universe Map](universe-map.md#live-marks): not your characters, corporations or alliances, and not anyone your characters, corporations or alliances have set to positive standing. Alliance contacts count, so a pilot blue only through your alliance won't set it off. Reports of only such pilots don't fire.

What the alarm says names the place and, around characters, the character: "2 jumps from *character*", "where *character* is", or the light years when only that range caught it. Anything else the report said — a gate camp, bubbles, which gate — is said before the hulls.

!!! note "How far back it looks"
    Around characters, an alarm looks at the last **10 minutes** of reports, because the watched systems move with the pilot. It's checked again as soon as a character undocks or changes system. Around systems, it looks back **2 hours**.

    The same sighting called by several people is one alert. A pilot reported again later is news again.

### Market / contract price

Fires when an item is listed at or below a price you name — **on the market, in public contracts, or both**. It reads the markets configured under **Settings ▸ Market** and the public contracts the app already sweeps, so it sees what those cover and nothing more.

### Database query

Runs a `SELECT` against the local EVE Console database on an interval and fires on the rows it returns — or on there being none. Use it when no purpose-built check fits. **Only `SELECT` is permitted.**

!!! warning "Write the query so the same situation gives the same rows"
    Because an alarm only re-announces results it hasn't seen before, a query whose output changes every run — for example one that selects the current time — will fire on *every* interval. Return a stable key for a given situation so it fires once, when the situation is new.

### Ship undocks

Fires when one of your characters undocks. Narrow it with filters: only from named **stations, structures, systems or regions**; only in named **hulls or ship classes**; and only in a given **state** — fit or not fit, jump fuel below a number, ammunition below a number. Every filter narrows, so two alarms can be set to cover different undocks rather than the same one twice. The undock is seen by the location poll within about ten seconds; **what was aboard is judged from the last asset snapshot, which ESI refreshes hourly**, and each match says how old that reading was.

### Undocked too long (wake-up call)

A **staged** wake-up. Fires in up to three stages when one of your characters, in a named hull or ship class, undocks and is **still sitting in the same system after a number of seconds** — a freighter or jump freighter idling on a tether while its pilot dozes off. Optionally it also covers **jump arrivals**: a jump-capable hull that has landed by jump drive or bridge and is still in space (the thirty seconds after a jump). Docking, leaving the system, or logging off ends it. Acknowledging the dialog — or replying anything at all to the agent — quiets it for a while; when that lapses and the ship is still there, the stages start over. Each stage has its own actions (a spoken line, a dialog, a sound that repeats until acknowledged); repeat and cooldown don't apply.

**Stopping the ship ends it** — ticked by default. Pressing stop after the undock ends that undock's alarm, and a repeating sound stops with it: a stopped ship isn't drifting off the undock, and somebody pressed stop. This is read from the game log, so that client's game log folder must be read (see [Game Logs](../logs-and-map-data.md#game-logs)); without it, the stages run as before. It applies to undocks only, and is hidden when **Jump arrivals** is ticked.

### Game log event

Fires on what a character's game log says happened to it. Tick any mix:

- **Decloaked** — your cloak dropped near a gate, a structure or anything else that drops one.
- **Warp scrambled** — a warp scramble or warp disruption landed on you. One aimed at a fleet member doesn't count.
- **Under attack** — you are taking damage.

Narrow it with:

- **Players only** — ticked by default. A scramble or an attack counts only from a player, not an NPC, so ratting doesn't set it off all evening.
- **Characters** — your own characters to watch; leave it empty for all of them.

A scramble or an attack fires **once per fight**: lines with no more than two minutes between them are one fight. A new alarm of this kind checks every **5** seconds, so an event is seen within seconds.

It needs that client's game log folder to be read — see [Game Logs](../logs-and-map-data.md#game-logs). Game logs are read in every client language.

### Planetary Industry

Fires for the colonies of characters that do planetary industry:

- **Extractors stopping** — an extractor program has ended or is about to (exact).
- **Storage filling** — storage or a launchpad is full or filling.
- **Inputs running out** — a factory planet's input is running out.

Storage and inputs are estimated from the last time the colony was opened in the game. Under **Watch for**, choose **All three** or one of them. **Lead time** fires that many hours before it happens; **0** fires when it happens.

Each colony's event fires once. Restarting the extractors, or opening the colony again in the game, makes it news again.

### Store order events

Fires on what happens to a [store's](../stores/index.md) orders: a **new order placed** — with the store, buyer, item, price, and whether it's in stock or must be built — an order **newly fillable from stock** or **newly in build**, a **contract issued** for it, the **contract accepted** (the order complete), or the order **canceled**. Tick the kinds you want. Orders you add by hand in the [Order Tracker](order-tracker.md) aren't reported. It runs the moment the store books or updates an order.

## Using it

1. **New Alarm** — choose a condition type and fill in its settings.
2. **Add Action** — a sound, words to say, and/or an agent instruction.
3. Set **Continuous** or **One shot**, an optional **cooldown**, and tick **Enabled**.
4. Click **Save**.
5. **Test Sounds** plays the alarm's sounds once, so you can check they can be heard.

The list shows each alarm's state — **Armed**, **Disabled** or **Error** — and how many times it has fired. **Recent firings** lists when the selected alarm fired, in EVE time.

## Notes

- Alarms are checked by the background poller, so they keep running on a [background/headless worker](../background-processing.md) even with no window open — the machine that plays sounds or talks is whichever client is in front of you.
- Alarms complement the actionable **alerts** on the [Overview](overview.md) dashboard: use alarms for conditions you want checked on a timer and surfaced when they first occur.
- The [AI agent](../ai-agent-eden.md) can create and change alarms for you too.
