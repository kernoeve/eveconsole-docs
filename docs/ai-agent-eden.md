# AI Agent (Eden)

EVE Console ships with an optional built-in conversational assistant — **Eden** by
default (you can rename it). It has read access to your local database and a set of
**tools**, so it can both answer questions the UI isn't explicitly designed for and
*do* things in the app for you.

> The agent is entirely optional and inactive until you set it up. If you don't
> configure it, you can ignore it completely. Its settings live in
> **Settings** (the **⚙** gear button, top-right), across the **AI Agent**,
> **Personalisation**, **Voice (TTS)** and **Speech Input** tabs.

## What it can do

- **Answer questions about your data.** It discovers your local database's shape and
  runs read-only queries itself, so it can pull together things no single screen
  shows — assets, industry jobs, market prices, character info, and more.
- **Reach ESI when the database doesn't have it.** For live details the app hasn't
  synced, it can make a read-only ESI call.
- **Act in the app for you.** Navigate to an item or entity, open the map with an
  overlay, set a destination, filter the asset or industry views, configure the Item
  Browser, select a character, refresh data, and create or manage [alarms](tools/alarms.md).
- **Show its work in its own tab.** Results can be rendered as a **table** or a
  **document** you can keep, rather than only as chat text.
- **Know who you are.** It follows your name and **standing instructions** (see
  [Personalisation](#personalisation)) so its answers fit how you play.
- **Run on your choice of model** — an **external** provider (Claude or OpenAI) or a
  **local** model (Ollama / LM Studio).
- **Talk and listen** — optional **text-to-speech** and **speech-to-text** with a
  global push-to-talk key, so you can use it hands-free while the game has focus.

Once enabled, a **✦ {name}** button appears in the title bar; click it to toggle
the (resizable) chat panel.

## Setup

Agent settings are split between tabs on purpose:

- The **Personalisation** tab is **about you**, so it's kept in the database and
  **shared by every client** that opens your data.
- The **AI Agent**, **Voice** and **Speech Input** tabs are **this machine's own**
  (provider, API keys, voice, microphone).

Click **Save** at the bottom when done.

### AI Agent tab

1. **Enable** — tick **Enable {name} AI companion**. This just makes the panel
   available; you still need a provider configured below.
2. **Provider** — choose the **LLM Provider**, then fill in the section that appears:
    - **Claude (Anthropic)** — paste an API key (`sk-ant-…`) and optionally a model
      (default `claude-sonnet-4-6`; `claude-opus-4-8` and `claude-haiku-4-5` also
      work). Get a key at
      [console.anthropic.com](https://console.anthropic.com/settings/keys).
    - **OpenAI** — paste an API key (`sk-…`) and optionally a model (default
      `gpt-5`). Get a key at
      [platform.openai.com](https://platform.openai.com/api-keys).
    - **Local LLM (Ollama / LM Studio)** — set the **API Endpoint** (default
      `http://localhost:11434`) and **Model Name** (default `llama3.1`). The runner
      must expose an OpenAI-compatible `/v1/chat/completions` endpoint, which
      Ollama and LM Studio do by default. A local model needs to be capable enough
      to use tools reliably.
3. **Context Management** — optionally persist chat history to disk across restarts
   and set a **summarization threshold** (estimated tokens) at which older messages
   are silently compacted into a summary. Lower values cut cost per message but
   drop older context. For Claude, a **prompt-cache** option trades a slightly
   higher cache-write cost for cheaper reads when your messages are minutes apart —
   the **AI Usage** tool (below) shows the effect.

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
spend goes and whether the prompt-cache setting is paying off. It's most useful with
an external provider; local models are free to run.

<!--
  SCREENSHOT SLOTS (add files to docs/images/, then uncomment):

  ![Agent configuration](images/agent-config.png)
-->

## Voice (optional)

- **Voice (TTS)** — pick a provider to have the agent speak:
    - **OpenAI** — cloud voices (shares the OpenAI API key above); choose voice,
      model, and speed.
    - **ElevenLabs** — cloud voices; needs its own API key and a voice ID.
    - **Kokoro** — high-quality neural TTS that runs fully offline; the model
      (~320 MB of neural-network weights, no executable code) downloads on first use.
    - **Piper** — fast offline neural TTS; the runtime is bundled, and only the
      chosen voice (a data file) downloads on demand.

    Use **Test Voice** to preview. Volume and mute are also available in the agent
    panel itself.
- **Speech Input (Push-to-Talk)** — pick a provider to talk to the agent:
    - **OpenAI Whisper** — cloud transcription (shares the OpenAI key); Windows and
      Linux.
    - **Local Whisper** — runs on this machine, no API key; Windows only, and a model
      file must be downloaded first.

    Then choose a **Microphone Device** (click **↺** to refresh the list) — leave it
    on **System default** to follow whatever Windows/your OS is set to — and a
    **Global Push-to-Talk Key** — hold it to record even when EVE has focus. F13–F20
    are rarely captured by games and make good PTT keys. The mic button in the panel
    works regardless of this setting.

## Related

- [Getting Started](getting-started.md)
- [Browse all tools](index.md)
