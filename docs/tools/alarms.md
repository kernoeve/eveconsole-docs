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

A few conditions fire in **stages** — an escalating sequence where each stage has its own actions (see *[Undocked too long](#undocked-too-long)*).

!!! note
    Sounds, dialogs and agent notifications play **on this machine only**. The recorded alert is kept either way, so a background/headless client still logs the event even with nothing to play it.

## Condition types

When you press **New Alarm**, you pick the kind of check. Each kind has its own settings, and settings that don't apply to your choices are hidden.

### Date / time

Fires at a specific date and time, and optionally repeats on a fixed interval thereafter. Use it for reminders and anything scheduled. An occurrence that came due **while the app was closed fires at the next start** rather than being skipped.

### Intel report

Fires on intel near what you're watching: hostile pilots reported or seen on a kill, kills, a gate camp or bubbles called in, gate camps worked out from kills, and pilots coming closer. It reads the same intel as the [Intel](intel.md) tool — the intel channels under **Settings ▸ Chat Logs** (see [Logs & Map Data](../logs-and-map-data.md#intel-channels)), Jabber rooms and IRC channels whose **Type** is **Intel**, kills and pasted Local — as it stands now. A pilot seen since somewhere else, a system called clear, or news past its lifetime (see [How long intel lasts](intel.md#how-long-intel-lasts)) no longer fires.

The editor groups its settings under two headings: **Where to watch** and **What fires**. A new intel alarm checks every **15** seconds, and is checked again at once when new intel is written, when a character undocks or changes system, and when the Route Planner sends a route.

#### Where to watch

**Watch around** — what the range is drawn around:

- **Undocked characters** (the default) — wherever your online characters are in space. Docked characters aren't watched.
- **Characters** — your characters wherever they are while online, docked or not.
- **Systems** — a list of systems you name.

With **Undocked characters** or **Characters**, the **Characters** list narrows it to the characters you name; leave it empty for all of them. With **Systems**, add each system to the **Systems** list.

- **Jumps from** / **Thru** — the range in jumps from each character or system, through stargates and through Thera's and Turnur's open wormholes. **Thru** is the farthest: **5** by default, the most 15; **0** watches only the system itself. **Jumps from** is optional, the nearest: systems nearer than it are left out everywhere, priority systems and the route ahead too. Two alarms can split a range this way, **0** thru **2** on one and **3** thru **5** on the other, and never both fire.
- **Light years** — optional. Also watch every system within this many light years, however many gates away — what a jump drive or a cyno puts in reach. The most is 20; empty or 0 is off.
- **Watch the route ahead** — on by default, around characters only. Also watch the systems still ahead on the last route the [Route Planner](route-planner.md) sent to the game for a watched character, however far; what is seen there is said as so many jumps ahead on the route. Only the part not yet flown counts, and the route is dropped on arrival or six hours after it was sent. A route set only in the game can't be known.
- **Priority systems** — optional. Systems always watched, wherever your characters are, but not nearer than **Jumps from**. What is seen there is said first.

A report caught by any of them fires. The Universe Map's **Alert zones** layer outlines the systems your intel alarms watch now (see [Intel layers](universe-map.md#intel-layers)).

#### What fires

- **Min players** — only fire when at least this many hostiles are in the system. The default is 1. Kills and flag-only reports fire whatever the number.
- **Ignore no visual** — skip pilots and counts reported NV, where someone is relaying a contact they can't actually see.
- **Flag-only reports** — on by default. Also fire for a report that counts nobody but says a gate camp, bubbles, a cyno, a hot drop, a spike or combat probes. Each is said once while it lasts. Other things a report can say (a wormhole, someone at the ESS or a skyhook) are said with a sighting, never alone.
- **Gate camps** — on by default. Fire for a gate camp worked out from kills (see [Camps](intel.md#camps)), near a watched character or on a route ahead. It is said once per camp, per character and per route, so a new route through a known camp is said again. One on a route ahead within 5 jumps is urgent.
- **Hostile** — which named pilots count, by the standings of your watched character nearest them, or of the character forced under **Settings ▸ Intel** (see [Standings](intel.md#standings)): **Neutral or worse** (the default), **Negative only** or **Red only**. Your own characters and blues never count; unnamed counts and flag-only reports always do.
- **Use the watch list** — on by default. Follow the Intel tool's [watch list](intel.md#watch-list): anyone or anything on **Always alert** fires within the **Watch list reach**, whatever the range, the **Hostile** choice or **Min players**, and is said first. What is on **Ignore** never fires.
- **Watch list reach** — how many jumps out the watch list's **Always alert** entries fire, when that is farther than **Thru**. The default is **10**; the most is 15.
- **Quieter further out** — on by default. The sound plays at full volume within a jump, and more quietly further out, down to 40% at the edge of the range. Speech keeps your voice volume.

**Kills.** A kill in a watched system with hostile pilots among the attackers always fires, said as a kill: what was lost, and to what ("Kill in *system*: Retriever lost to Sabre and Loki"). Within a jump it is urgent, and said first. NPC attackers don't count, and the kill's attackers aren't said again as a sighting.

**Each thing is news once:**

- a named pilot once while they stay in a system, however many people call them; seen in another system, they are news again;
- a count of unnamed pilots again only when it grows past 1, 4, 9 or 19;
- a flag (a gate camp, bubbles, a cyno, a hot drop, a spike, combat probes) once while it lasts;
- a kill once;
- a gate camp once per camp, per character and per route.

#### Only news fires

Only *news* fires: something seen, or come into range, in the last two minutes (**Only news newer than** under **Settings ▸ Intel**). What was already there is not said. **Every action of the alarm runs for everything it fires on** — the sound, speech, the agent, a dialog and the Alert alike. For something different nearer in, such as a louder sound within two jumps, add a second intel alarm and split the range with **Jumps from** and **Thru**.

**Urgent news** is said before the rest of a firing: a kill within a jump, anything in a priority system, anyone on the watch list's **Always alert**, a pilot coming closer (seen closer than before, or reported heading toward your character), and a gate camp on a route ahead within 5 jumps.

**What it says** names the place and how far: "2 jumps from *character*", "where *character* is", "3 jumps ahead on *character*'s route", or the light years when only that range caught it, with "through Thera or Turnur" when the shortest way goes through one. A pilot coming closer adds "Approaching: heading to *system*" or "Approaching: was 4 jumps out"; one leaving, "Heading away, to *system*". News in a priority system starts "Priority system:", and about someone on the watch list "Watch list:". A camp is said as "Gate camp in *system* on the *gate* gate", with its kills and over how many minutes. Anything else a report said — a gate camp, bubbles, which gate — is said before the hulls.

!!! note "Changed in 0.9.19"
    Intel alarms made before 0.9.19 behave as above from now on, with **Flag-only reports**, **Gate camps**, **Watch the route ahead**, **Use the watch list** and **Quieter further out** on. One left at the editor's general 60-second check now checks every 15 seconds.

### Market / contract price

Fires when an item is listed at or below a price you name — **on the market, in public contracts, or both**. It reads the markets configured under **Settings ▸ Market** and the public contracts the app already sweeps, so it sees what those cover and nothing more.

### Database query

Runs a `SELECT` against the local EVE Console database on an interval and fires on the rows it returns — or on there being none. Use it when no purpose-built check fits. **Only `SELECT` is permitted.**

!!! warning "Write the query so the same situation gives the same rows"
    Because an alarm only re-announces results it hasn't seen before, a query whose output changes every run — for example one that selects the current time — will fire on *every* interval. Return a stable key for a given situation so it fires once, when the situation is new.

### Ship undocks

Fires when one of your characters undocks. Narrow it with filters: only from named **stations, structures, systems or regions**; only in named **hulls or ship classes**; and only in a given **state** — fit or not fit, jump fuel below a number, ammunition below a number. Every filter narrows, so two alarms can be set to cover different undocks rather than the same one twice. The undock is seen by the location poll within about ten seconds; **what was aboard is judged from the last asset snapshot, which ESI refreshes hourly**, and each match says how old that reading was.

### Undocked too long

A **staged** alarm. Fires in up to three stages when one of your characters, in a named hull or ship class, undocks and is **still sitting in the same system after a number of seconds** — a freighter or jump freighter idling on a tether while its pilot dozes off. Optionally it also covers **jump arrivals**: a jump-capable hull that has landed by jump drive or bridge and is still in space (the thirty seconds after a jump). Docking, leaving the system, or logging off ends it. Each stage has its own actions (a spoken line, a dialog, a sound that repeats until acknowledged); repeat and cooldown don't apply.

A window with one button, **Acknowledge**, is up from the first stage to the last, whatever actions the stages have. Pressing it quiets the alarm for the time set under **Quiet after an acknowledgement**. When that lapses and the ship is still there, the stages start over.

**Typing or speaking to the agent counts too.** The first key in the agent box, or the microphone opening, is enough: what you say doesn't matter, it works while the model is busy, and no reply is needed. It resets every Undocked too long alarm at once:

- The alarm's sound and voice stop.
- A stage already due goes quiet for the same time, as if you'd pressed **Acknowledge**.
- Before any stage is due, the clock restarts: the first stage comes its usual number of seconds after your last key, not after the undock.

Other alarm types aren't affected by this.

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

It needs that client's game log folder to be read — see [Game Logs](../logs-and-map-data.md#game-logs). Decloaking, warp scrambles and attacks are recognised in all eight client languages, so the client can run in any of them.

### Planetary Industry

Fires for the colonies of characters that do planetary industry — the same colonies the [Planetary Industry](planetary-industry.md) tool shows:

- **Extractors stopping** — an extractor program has ended or is about to (exact).
- **Storage filling** — storage or a launchpad is full or filling.
- **Inputs running out** — a factory planet's input is running out.

Storage and inputs are estimated from the last time the colony was opened in the game. Under **Watch for**, choose **All three** or one of them. **Lead time** fires that many hours before it happens; **0** fires when it happens.

Each colony's event fires once. Restarting the extractors, or opening the colony again in the game, makes it news again.

### Store order events

Fires on what happens to a [store's](../stores/index.md) orders: a **new order placed** — with the store, buyer, item, price, and whether it's in stock or must be built — an order **newly fillable from stock** or **newly in build**, a **contract issued** for it, the **contract accepted** (the order complete), or the order **canceled**. Tick the kinds you want. Orders you add by hand in the [Order Tracker](order-tracker.md) aren't reported. It runs the moment the store books or updates an order.

An offer to sell to one of the store's [Buy listings](../stores/buy-listings.md) is reported as an offer, in words of its own, never as an order to fill. The same tick boxes cover offers:

| Tick box | For an offer |
| --- | --- |
| **New order placed** | A **new offer** — the alert reads *New offer: (item) from (seller)*, and says the store and the price. |
| **Contract issued** | The seller **sent their contract** — for the whole offer or part of it. When it asks more than you quoted, it says so, so you check it before accepting. |
| **Contract accepted — order complete** | Goods **received** (*N of M received*), and the offer **complete**. |
| **Order canceled** | The offer **canceled**. |

## Using it

1. **New Alarm** — choose a condition type and fill in its settings.
2. **Add Action** — a sound, words to say, and/or an agent instruction.
3. Set **Continuous** or **One shot**, an optional **cooldown**, and tick **Enabled**.
4. Click **Save**.
5. **Test Sounds** plays the alarm's sounds once, so you can check they can be heard.

Ctrl or Shift selects several alarms in the list. The editor edits one alarm, so it gives way to a note until you select one alone.

The list shows each alarm's state — **Armed**, **Disabled** or **Error** — and how many times it has fired. **Recent firings** lists when the selected alarm fired, in EVE time.

## Export and import

**Export** and **Import** sit above the list, and move alarms between machines or profiles as a JSON file.

- **Export** saves the selected alarms and their actions, or every alarm when none is selected. Each alarm's settings are written out as readable objects, and no firing history goes in.
- **Import** only ever adds. Nothing already here is replaced. An alarm identical to one here (same name, check and settings) is skipped, so importing a file twice adds nothing, and so is one whose check this version doesn't have. The status line says how many of each.
- An imported alarm keeps the on or off state it had in the file. It starts from now, as a new alarm does, so it won't fire on what already happened.

## Notes

- Alarms are checked by the background poller, so they keep running on a [background/headless worker](../background-processing.md) even with no window open — the machine that plays sounds or talks is whichever client is in front of you.
- Alarms complement the actionable **alerts** on the [Overview](overview.md) dashboard: use alarms for conditions you want checked on a timer and surfaced when they first occur.
- The [AI agent](../ai-agent-eden.md) can create and change alarms for you too.
