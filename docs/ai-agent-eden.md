# AI Agent (Eden)

EVE Console ships with an optional built-in conversational assistant — **Eden** by
default (you can rename it). It has read access to your local database and a set of
**tools**, so it can both answer questions the UI isn't explicitly designed for and
*do* things in the app for you.

> The agent is entirely optional and inactive until you set it up. If you don't
> configure it, you can ignore it completely. Its settings live in
> **Settings** (the **⚙** gear button, top-right) ▸ **AI Agent**, across the
> **Agent**, **Personalisation**, **Voice (TTS)** and **Speech Input (STT)** tabs.

## What it can do

- **Answer questions about your data.** It discovers your local database's shape and
  runs read-only queries itself, so it can pull together things no single screen
  shows — assets, industry jobs, market prices, character info, and more.
- **Reach ESI when the database doesn't have it.** For live details the app hasn't
  synced, it can make a read-only ESI call.
- **Act in the app for you.** Open any tool, navigate to an item or entity, open the
  map with an overlay, set a destination, filter the asset or industry views,
  configure the Item Browser, select a character, refresh data, and create or manage
  [alarms](tools/alarms.md).
- **Know what you're looking at.** "This", "here" and "this screen" mean the tab you
  have open, so you can ask "what does this show?" without naming it.
- **Show its work in its own tab.** Results can be rendered as a **table** or a
  **document** you can keep, rather than only as chat text.
- **Know who you are.** It follows your name and **standing instructions** (see
  [Personalisation](#personalisation)) so its answers fit how you play.
- **Run on the models you choose** — a free model on a server of your own (Ollama,
  LM Studio) or a paid service (Claude, OpenAI), or several, each doing the job it
  suits (see [Roles](#roles)).
- **Talk and listen** — optional **text-to-speech** and **speech-to-text** with a
  global push-to-talk key, so you can use it hands-free while the game has focus.

Once enabled, a **✦ {name}** button appears in the title bar; click it to toggle
the (resizable) chat panel. The line above each reply shows when it was written,
which model wrote it and which tools it used.

## Setup

Agent settings are split between tabs on purpose:

- The **Personalisation** tab is **about you**, so it's kept in the database and
  **shared by every client** that opens your data.
- The **Agent**, **Voice (TTS)** and **Speech Input (STT)** tabs are **this
  machine's own** (models, API keys, voices, microphone).

Everything on these tabs saves as you change it — text once you pause typing or
leave the box. The line at the bottom confirms each save.

!!! tip "Defaults keep up with the app"
    Texts you can reword — the router's rule and the announcements below — are stored
    only when you change them. Left as they are, they follow any improved wording in
    later versions.

### Agent tab

1. **Enable** — tick **Enable {name} AI companion**. This just makes the panel
   available; you still need at least one model set up below.
2. **Models** — every model the agent can think with. Click **Add** for a new one
   and select it in the list to edit it; **Remove** takes the selected one out (at
   least one model stays). For each model:
    - **Name** — optional; what the roles and announcements call it. Blank shows
      what it is, e.g. *Local — qwen3:8b on gpu-box*.
    - **Service** — **Local server — Ollama, LM Studio… (free)**, **Claude —
      Anthropic (paid)** or **OpenAI (paid)**.
    - The service's key or address:
        - **Claude (Anthropic) API key** (`sk-ant-…`) — one key for every Claude model
          in the list. Get one at
          [console.anthropic.com](https://console.anthropic.com/settings/keys).
        - **OpenAI API key** (`sk-…`) — one key for every OpenAI model, and also used
          for OpenAI's voices and speech input. Get one at
          [platform.openai.com](https://platform.openai.com/api-keys).
        - **Server address** for a local server, e.g. `http://gpu-box:11434` (the
          server's root). It must offer OpenAI's `/v1/chat/completions`, as Ollama,
          LM Studio and most local runners do.
    - **Model** — chosen from the service's own list: the models your Claude or
      OpenAI key can use, newest first (OpenAI's list leaves out models that aren't
      for conversation), or the models on your local server. Click **↺** to ask again.
      A model you chose earlier that is no longer listed stays chosen, marked
      **— not in the list now**. Without a key or an answer from the server, the
      reason is shown and you can type the name instead. There is no default model:
      one with none chosen isn't set up.
    - **Let it think before answering (slower)** — local servers only, on by
      default. For models that think before they answer, such as Qwen3; the thinking
      is never shown or spoken. Untick it for quicker replies at some cost in care.
      Models that don't think ignore it.
    - **Prompt cache lifetime** — Claude only: **5 minutes (default)** or
      **1 hour**. Reading the cache costs a tenth of sending the conversation again;
      the 1-hour option saves money if your messages are usually 5–60 minutes apart,
      but writing it costs more, so it costs more if they are closer together. The
      [AI Usage & Cost](#ai-usage-cost) tool shows cache reads and writes per
      message. Applies to every Claude model in the list.
    - **Test This Model** — asks it for one sentence, as set on the tab. It shows
      how long it took and what it said, or why it failed. Free on a local server; a
      few tokens on a paid service.
3. **Roles** — which model does what (see [Roles](#roles) below).
4. **When a model changes** — what is said when a role falls over to its fallback
   and when its own model comes back (see [Fallbacks](#fallbacks)).
5. **Context Management** — optionally persist chat history to disk across restarts
   (**Persist conversation history across sessions**) and set a **Summarization
   threshold** (estimated tokens) at which older messages are silently compacted
   into a summary. Lower values cut cost per message but drop older context.

!!! note "Older settings"
    Settings from before models and voices became lists are brought across on first
    start: your one model becomes the first in the list and does every job, and your
    one voice becomes the first voice. Nothing changes until you change it.

### Roles

The **Roles** section names a model for each job. The lists show each model with
**(free)** or **(paid)** after it.

- **Conversation** — talks with you and works the app: opens and arranges its
  tools, sets alarms and destinations, remembers your standing instructions.
- **Questions about your data** — anything that needs your database or ESI: what
  you have, own, are doing or have done. This model gets the whole prompt and every
  tool. Leave it on **Same as the conversation** for one model to do everything.
- **Summaries** — compacts older messages when the conversation grows long. A small
  free model does this well. A local summary model gets a short one-line prompt
  rather than the agent's full one, leaving its window for the history being
  summarised, and the history is checked against a local model's window after every
  turn so it can't silently outgrow it.

The sentence under the section sums up what your choices come to.

When **Questions about your data** names a different model from the conversation:

- Before each message, the conversation model is asked in one word whether the
  message needs your data. If it does, the data model answers it instead, with the
  database and ESI. The conversation model gets a prompt about half the size and no
  access to your data.
- **Send a message to this model when…** holds the rule the conversation model
  decides by. Reword it if messages go the wrong way; **Reset to the default** puts
  the app's wording back.
- If a data question slips through, the conversation model hands it over itself.
- Start a message with `/data` or `/chat` to send that one message to the data
  model or the conversation model regardless.

### Fallbacks

The **Conversation** role — and **Questions about your data**, when it has a model
of its own — can name a model to use when its own stops answering (**If it stops
answering, fall over to**). **None — the role simply fails** turns this off.

- A model that stops answering is replaced at once, before a word of the answer.
- Whether a model is there is checked for free (the service's own model list), never
  by paying for an answer.
- Nothing is switched silently at start: if a role's own model isn't there, the
  first message finds out and says so.
- **Say so when it falls over, and when it comes back — in the chat, and aloud when
  speaking** announces each change.

Under **When a model changes**, **Falling over** and **Coming back** are the texts
said. `{user}` is your name from Personalisation, `{purpose}` is "our conversation"
or "data access", and `{primary}` and `{fallback}` are the two models' names. The
two minute settings — **At least … minutes between one change and the next switch
back** and **Up for … minutes without a break before a role's own model returns** —
only govern coming back, so a server that keeps dropping out can't make the agent
flip back and forth. A switch back also waits for your next message.

### Personalisation

On the **Personalisation** tab (shared across your clients):

- **Agent Name** — blank = *Eden*.
- **Response Verbosity** — *Concise* (1–3 sentences), *Balanced*, or *Detailed*.
  This is added to the system prompt on every message.
- **Your Name** — how the agent addresses you.
- **Standing Instructions** — free-form, lasting guidance for the agent: how you
  play, what you care about, conventions to follow. It's included on every message,
  so keep it focused. The agent can also update this itself when you ask it to
  remember something.

## AI Usage & Cost

The **AI Usage & Cost** tool records what each turn cost and did — tokens in and out,
cache reads and writes, and the estimated price per message — so you can see where
spend goes and whether the prompt-cache setting is paying off. Local models are free
to run.

Its **Rates** tab holds the price of each paid model. Every model a paid service
lists for your key gets a row of its own. Where LiteLLM's community price list has
the model, the row is filled from it (the list is fetched again once a day), and the
row's note names the list, the date and the provider's pricing page to check it
against. A rate you set by hand is never overwritten. ElevenLabs voices aren't in
that list, so set their rates yourself.

<!--
  SCREENSHOT SLOTS (add files to docs/images/, then uncomment):

  ![Agent configuration](images/agent-config.png)
-->

## Voice (optional)

On the **Voice (TTS)** tab, tick **Speak the agent's replies** and build a list of
**Voices**, in order of preference. The first voice that can speak is used; if it
fails, the next takes over at once, and the first returns once it's back and has
stayed up. Use **Add**, **Remove**, **▲ Up** and **▼ Down** to arrange the list.

For each voice:

- **Name** — optional. The voice is part of who you're talking to: while a named
  voice speaks, its name is the agent's name, in the panel and in the conversation.
  A voice with no name uses the agent's name from Personalisation.
- **Engine**:
    - **Kokoro (on this PC, free)** — high-quality neural TTS that runs fully
      offline. Pick a voice, then click **Load Model**: one model serves every
      Kokoro voice and is downloaded once (~320 MB of neural-network weights, no
      executable code) into this PC's data folder.
    - **Local server — Chatterbox, Orpheus, Kokoro-FastAPI… (free)** — any server
      that speaks OpenAI's speech API, usually on another machine's GPU. Set the
      **Server address (up to and including /v1)**, e.g. `http://gpu-box:8880/v1`,
      the **Model** and **Voice** as the server names them, the **Speed**, and an
      **API key** only if the server asks for one. A server counts as up only if it
      actually speaks within 30 seconds.
    - **Piper (on this PC, free)** — fast offline neural TTS; the runtime is
      bundled, and only the chosen voice (a data file) downloads, with **Download
      Voice Model**.
    - **OpenAI (paid)** — OpenAI's voices, billed per character. Uses the OpenAI API
      key (the same one as the Agent tab's OpenAI models). Choose the **Model** from
      OpenAI's list (**↺** asks again) and a **Voice** from the ones OpenAI documents
      for that model, and set the **Speed**.
    - **ElevenLabs (paid)** — ElevenLabs' voices, billed per character. Paste your
      **ElevenLabs API key**, then choose a **Voice** by name from your account and
      a **Model** from ElevenLabs' list (**↺** asks again, e.g. after adding a voice
      there).
- **Test This Voice** — speaks with this voice as set, on its own rather than
  through the list. It shows how long it took in green, or the reason it
  couldn't speak (the server's own words) in red.

All voices are brought to the same loudness, so a change of voice doesn't jump in
volume. Speech leaves out emoji and markdown — headings, rules and table lines
aren't read out — and the next sentence is prepared while one plays. Volume and mute
are also available in the agent panel itself.

**When the voice changes** — tick **Announce it, in the new voice** to have the voice
taking over say so. **Taking over** and **Coming back** are the texts, with
`{previous}` and `{current}` for the two names. A change is announced only when the
name changes, so give each voice its own name. Nothing is said when the app starts.
The two minute settings work as they do for models: a failing voice is replaced at
once, and a switch back waits for the end of the current answer.

## Speech Input (optional)

On the **Speech Input (STT)** tab, pick a **Provider** to talk to the agent:

- **OpenAI Whisper** — cloud transcription (shares the OpenAI key); Windows and
  Linux. Choose the **Model** from OpenAI's list of transcription models (**↺** asks
  again). Settings from before this choice existed keep `whisper-1`.
- **Local Whisper** — runs on this machine, no API key; Windows only. Pick a
  **Model** and click **Download Model** before first use, and set the **Language**
  you speak as a two-letter code such as `en` (or `auto` to let the model guess,
  which is often wrong on a short clip).

Then choose a **Microphone Device** (click **↺** to refresh the list) — leave it on
**System default** to follow whatever Windows/your OS is set to — and a **Global
Push-to-Talk Key** — hold it to record even when EVE has focus. F13–F20 are rarely
captured by games and make good PTT keys. The mic button in the panel works
regardless of this setting.

## Related

- [Getting Started](getting-started.md)
- [Browse all tools](index.md)
