# Alarms

Conditions you define that the app checks on a timer and tells you about once they become true, so you can be told when something has happened instead of watching for it yourself.

Open it from the left sidebar under **General**.

## How an alarm works

Each alarm is a **condition** the app evaluates repeatedly in the background, plus one or more **actions** that run when it fires. While the condition stays false, nothing happens; when it becomes true, the alarm fires.

- **It fires once per thing.** An alarm only announces something it hasn't announced before, so a condition that simply stays true doesn't repeat. (A price alarm that has already told you an item is cheap won't nag every check — it fires again only when a *new* matching listing appears.)
- **Continuous or one shot.** A *Continuous* alarm stays armed until you disable it; a *One shot* alarm disables itself after firing once.
- **Cooldown (sec).** An optional minimum gap between firings, on top of the "not announced before" rule.
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

When you press **New Alarm**, you pick the kind of check. Each kind has its own settings:

### Date / time

Fires at a specific date and time, and optionally repeats on a fixed interval thereafter. Use it for reminders and anything scheduled. An occurrence that came due **while the app was closed fires at the next start** rather than being skipped.

### Market / contract price

Fires when an item is listed at or below a price you name — **on the market, in public contracts, or both**. It reads the markets configured under **Settings ▸ Market** and the public contracts the app already sweeps, so it sees what those cover and nothing more.

### Intel report

Fires when someone reports a pilot in a system you're watching. Give it a **list of systems**, or **one system and a jump range** to cover everything around it. It reads the intel channels already being parsed under **Settings ▸ Chat Logs** (see [Game & Chat Logs](logs.md)).

### Database query

Runs a `SELECT` against the local EVE Console database on an interval and fires on the rows it returns — or on there being none. Use it when no purpose-built check fits. **Only `SELECT` is permitted.**

!!! warning "Write the query so the same situation gives the same rows"
    Because an alarm only re-announces results it hasn't seen before, a query whose output changes every run — for example one that selects the current time — will fire on *every* interval. Return a stable key for a given situation so it fires once, when the situation is new.

### Ship undocks

Fires when one of your characters undocks. Narrow it with filters: only from named **stations, structures, systems or regions**; only in named **hulls or ship classes**; and only in a given **state** — fit or not fit, jump fuel below a number, ammunition below a number. Every filter narrows, so two alarms can be set to cover different undocks rather than the same one twice. The undock is seen by the location poll within about ten seconds; **what was aboard is judged from the last asset snapshot, which ESI refreshes hourly**, and each match says how old that reading was.

### Undocked too long (wake-up call)

A **staged** wake-up. Fires in up to three stages when one of your characters, in a named hull or ship class, undocks and is **still sitting in the same system after a number of seconds** — a freighter or jump freighter idling on a tether while its pilot dozes off. Optionally it also covers **jump arrivals**: a jump-capable hull that has landed by jump drive or bridge and is still in space (the thirty seconds after a jump). Docking, leaving the system, or logging off ends it. Acknowledging the dialog — or replying anything at all to the agent — quiets it for a while; when that lapses and the ship is still there, the stages start over. Each stage has its own actions (a spoken line, a dialog, a sound that repeats until acknowledged); repeat and cooldown don't apply.

### Store order events

Fires on what happens to a [store's](../stores/index.md) orders: a **new order placed** — with the store, buyer, item, price, and whether it's in stock or must be built — an order **newly fillable from stock** or **newly in build**, a **contract issued** for it, the **contract accepted** (the order complete), or the order **canceled**. Tick the kinds you want. Orders you add by hand in the [Order Tracker](order-tracker.md) aren't reported. It runs the moment the store books or updates an order.

## Using it

1. **New Alarm** — choose a condition type and fill in its settings.
2. **Add actions** — a sound, words to say, and/or an agent instruction.
3. Set **Continuous** or **One shot**, an optional **cooldown**, and tick **Enabled**.
4. **Test Sounds** fires the alarm's actions once so you can check they land.

## Notes

- Alarms are checked by the background poller, so they keep running on a [background/headless worker](../background-processing.md) even with no window open — the machine that plays sounds or talks is whichever client is in front of you.
- Alarms complement the actionable **alerts** on the [Overview](overview.md) dashboard: use alarms for conditions you want checked on a timer and surfaced when they first occur.
