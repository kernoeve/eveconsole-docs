# Messages and Group Chat

Two tools hold all your chat from the servers EVE Console connects to: **Messages** for conversations with one person, and **Group Chat** for rooms, channels and server chat. Both cover [Jabber](../jabber.md), [IRC](../irc.md) and [Mumble](../mumble.md) side by side, so you don't need to know which service someone is on to answer them.

- **Messages** — open it from the left sidebar under **Communication**, or from the speech-bubble icon at the top of the window, beside the Eve Mail envelope.
- **Group Chat** — open it from the people icon at the top of the window, next to the Messages icon. It isn't in the sidebar: its icon carries its counts.

Servers are added in **Settings**, on the **Jabber**, **Mumble** and **IRC** tabs. Until one is set up, both tools say so.

## Messages

### What it shows

- **The conversation list** (left) — **All Conversations**, newest first. Each shows the person's name, the service and server they're on, the last message and its time, a dot for online (green) or away (amber), and a count of unread messages. **Search by name or server** narrows the list. The **Conversations** button at the top hides or shows the list.
- **Tabs** — each open conversation has a tab across the top, with its unread count. **×** closes a tab; the conversation stays saved. The tabs you had open come back next time.
- **The conversation** — the person's name and server, their status (online, away or offline, and their status text), the messages with pictures beside them, and the box to write in. A line above the box says when someone is typing, or why nothing can be sent right now.
- **Play a sound for new direct messages** — at the bottom of the list. On to start.

### Using it

1. Click a conversation to open it in a tab. Opening it marks its messages read.
2. Write in the box at the bottom. **Enter** sends; **Shift+Enter** starts a new line.
3. To write to someone new, click **New Conversation** and type part of their name. The list shows everyone online on the servers connected right now; click someone to start. **Cancel** goes back to the list.

You can also start a conversation from a person's menu: **Direct Message** on someone in a Jabber room or IRC channel, or **Send Message** on someone in the Mumble channel tree.

For a Jabber conversation, **Add Contact** and **Remove Contact** at the top add the person to your contacts on that server, or take them off.

### What each service can do

Hover a message for its buttons. What's offered depends on the service:

| | Jabber | IRC | Mumble |
|---|---|---|---|
| Reply | Yes | — | — |
| Edit your latest message | Yes | — | — |
| Delete or take back your own | Yes | Where the server allows | — |
| Reactions | Yes | Where the server supports them | — |
| Emote packs | Yes | — | — |
| Typing shown | Yes | Where the server supports it | — |
| **Seen** under your message | Yes | — | — |
| **Attach** a file | Where the server takes files | Where the server names a file host | — |
| Message someone offline | Held by their server, if it does | No | No |

Picture links show the picture under the message: straight away from the chat server's own file host, and after you click **Show picture** from anywhere else, because loading it tells that site your IP address. **Ctrl+V** (**Cmd+V** on a Mac) sends a screenshot, a copied picture or copied files where the conversation takes files. The service pages explain each feature: [Jabber](../jabber.md#writing-messages), [IRC](../irc.md#writing-messages).

## Group Chat

### What it shows

- **The list** (left) — each server you've set up, with what's under it: the rooms of a Jabber server, the channels of an IRC server, invitations waiting for an answer, and each connected Mumble server's chat. A dot shows each one's state: green when connected or joined, amber while connecting or for an invitation, red when something went wrong, grey when off. Badges count the unread messages, and, in warning colours, unseen mentions of your name.
- **Add Rooms** — above the list, for joining rooms and channels on the server selected.
- **Play a sound for messages that need attention** — at the bottom of the list. On to start.
- **The conversation** (right) — the room's topic and whether it keeps an archive, its **Type** and **Alert me** settings, **Leave Room**, the messages, and the people in it down the right side.

### Using it

1. Click a room, channel or Mumble server in the list. Opening it marks its messages read.
2. Write in the box at the bottom. **Enter** sends; **Shift+Enter** starts a new line.
3. Right-click a person for their menu (**Direct Message** first), or a room or channel in the list for its menu.
4. To join more, select a server and click **Add Rooms**. See [Join a room](../jabber.md#join-a-room) and [Join a channel](../irc.md#join-a-channel).

Each room or channel has:

- **Type** — **General** for talking, or **Intel**: also read for intel reports, which feed the [Intel](intel.md) tool, the map's live marks and the **Intel report** alarm. A report relayed into several rooms, or already read from an EVE chat channel, is counted once.
- **Alert me** — **When my name or a keyword appears** (the default), **Every message**, or **Never**. Keywords are set per server, in its settings.

A Mumble server's chat is different: it's everything said since connecting, in whichever channel you were in, and it lasts until the app closes, as a Mumble server keeps none of it. Tick **Include subchannels** to send one message to the channels under yours as well.

## Alerts

- **The Messages icon** at the top of the window is dim with nothing new, and lit in warning colours with a count when a direct message is waiting.
- **The Group Chat icon** is dim with nothing new, lit with a count for new messages, and in warning colours, with a second count, when something names you or one of your keywords. Hover it for the counts.
- Clicking either icon opens the tool on what most needs reading: a conversation that called for attention first, then any with unread messages.
- **Sounds** — each tool has its tick box for a sound, which plays the default alarm sound. Nothing plays while alarms are muted, or for the conversation you're looking at.
- **The Overview** shows an alert for unread Jabber and Mumble direct messages, and for Jabber rooms that named you. Clicking it opens the conversation or room. IRC isn't counted there.

On a [Client Layouts](client-layouts.md#panel-controls) panel (Windows only), **Direct messages** and **Group chat** icons drop down what's new, and a **Group chat room** control shows one room.

## Chat history

Messages are saved in EVE Console's database, so the history is there after a restart, and on a [PostgreSQL setup](../storage-postgresql.md) every client sees the same. How long they're kept is set by two rules on **Settings ▸ Data Retention**:

- **Direct Messages** — saved direct messages from Jabber, Mumble and IRC.
- **Group Chat** — saved messages from Jabber rooms and IRC channels. Mumble channel chat is never saved, so there's none to remove.

Each rule is on to start, at **30** days: **Purge direct messages older than** and **Purge group chat older than**. Change the days (1 to 3,650), or untick a rule to keep everything. An enabled rule runs once a day with the rest of the [background work](../background-processing.md); **Purge Now** runs it straight away, and the line beside it says when it last ran.

- **Unread messages are never removed**, however old.
- Reactions go with the messages they were on.
- What an Intel room or channel says is also handed to the intel reader, which keeps its copy with EVE's chat-log messages. That copy follows the **Chat Messages** rule on the same tab, not these two.
- These two rules replace the history setting Jabber had before, and start from whatever it was set to.
- A Jabber room's catch-up after a long absence doesn't fetch further back than the **Group Chat** rule keeps.

## Notes

- All chat dates and times are EVE time (UTC), and every message shows its date.
- Messages and Group Chat each open once; they can't have copies in a [Tool Container](client-layouts.md#tool-containers).
- On PostgreSQL, the Jabber and IRC connections are kept by the client doing the background work, and the others send through it. See [Jabber](../jabber.md#it-runs-with-the-background-work) and [IRC](../irc.md#it-runs-with-the-background-work).
