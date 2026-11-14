# IRC

EVE Console has an **IRC** client built in. Its channels sit in **Group Chat** beside your [Jabber](jabber.md) rooms and [Mumble](mumble.md) servers, and conversations with people in **Messages**, so one list holds all your chat. You can add any number of servers.

- **Settings ▸ IRC** — click the **⚙** gear button in the top-right of the title bar, then open the **IRC** tab. Servers are added and changed here, along with your away message, nickname and picture.
- **Group Chat** — the channels. Open it from its icon at the top of the window. See [Group Chat](tools/messages.md#group-chat).
- **Messages** — conversations with people. Open it from the left sidebar under **Communication**. See [Messages](tools/messages.md).

## Add a server

1. On **Settings ▸ IRC**, click **Add IRC server**.
2. Fill in:
    - **Name** — what the list calls it. Blank uses the server's address.
    - **Server address** — such as `irc.example.org`.
    - **Port** and **Encrypted (TLS)** — TLS is on for a new server, on port `6697`. Unticking it switches the port to `6667`, and ticking it back switches it back.
    - **Nickname** — one word, not starting with `#` or `:`. If it's taken, the same with `_` or a number after it is tried.
    - **Log in with** — how the network knows it's you:
        - **No password** — the default.
        - **Account (SASL), as most networks use** — your **Account name** (blank for the nickname) and **Password**.
        - **NickServ, once connected** — the same two, sent to NickServ after connecting.
        - **Server password** — a password for the server itself.
    - **Connect when the app starts** — off for a new server. Either way, a server that loses its connection reconnects by itself until you press **Disconnect**.
    - **Alert keywords, separated by commas** — words that raise an alert in a channel as your nickname does.
3. Under **More settings**, if you need them:
    - **User name** and **Real name**.
    - **Commands once connected** — one per line, as a network asks of its users, such as `/msg`, `/mode` and the like.
4. Click **Save**, then **Connect**.

The dot beside each server shows how it stands: green when connected, amber while connecting, red when something needs you, grey when off. The line under it says why, for example **Not connected: the server does not accept this nickname. Choose another under Edit.**

Select a server to see its state, **Connect** / **Disconnect** and **Edit**. Once connected, its page also says what you're **Connected as**, and whether the server keeps history: one that does sends what was said while you were away, missed direct messages included, when you reconnect. **Delete** in the editor removes the server, with its channels and saved messages, after asking.

### Encryption

- **A password is only ever sent over an encrypted connection**, except to a server on this computer. With TLS off, the editor warns that anyone on the way can read everything, and a server with a login set won't connect: **Not connected: a password is only sent over an encrypted connection. Turn on TLS for this server.**
- **A server that asks to be reached encrypted** gets its wish. Connected without TLS, the server can tell the app to use TLS from then on: the app moves to the encrypted port, keeps that rule until the date the server gave, and the server's page and the editor say so. A rule is only ever taken from an encrypted connection.
- **A self-signed certificate** — instead of connecting, the server shows **The server's certificate is not trusted.** with the certificate's fingerprint and **Trust This Certificate**. Compare the fingerprint with what the server's admin published, and only then trust it. From then on, only that certificate is accepted for this server.

Passwords and channel keys are kept with your other chat logins: on this computer on SQLite, or encrypted in the shared database on PostgreSQL. See [Where the password is kept](jabber.md#where-the-password-is-kept).

## While connected

A connected server's page in **Settings ▸ IRC** has:

- **Away** — type why (optional) and click **Set away**; **Back** clears it.
- **Change nickname now** — type a new one and click **Change**.
- **Your picture** — a web link to a picture (`https://…`, at most 400 characters), or one of your characters under **Use an EVE portrait**, which changes when you change it in the game. **Set picture** sets it; **Remove picture** takes it off. People see it where their IRC program shows pictures. It's set again each time the server connects. A server that doesn't keep pictures says so, and the picture is kept here until a server that does is connected.

## Channels

Channels live in **Group Chat**, under their server.

### Join a channel

1. In Group Chat, select the server and click **Add Rooms**.
2. The channels the server lists appear with their topic and how many people are in each. Filter and sort them as for Jabber rooms, or type a channel's name under **Room (pick above, or type a name)**.
3. Give its **Password** if it has one, and choose its **Type**:
    - **General** — for talking.
    - **Intel** — also read for intel reports, listed as coming from **IRC: #channel**. Its reports feed the [Intel](tools/intel.md) tool, the map's live marks and the **Intel report** alarm. A report relayed into several rooms or channels, or already read from an EVE chat channel, is counted once.
4. Click **Join**, then **Done**.

Channels you've joined are joined again each time the server connects. Typing `/join #channel` in any message box works too. An invitation to a channel shows under its server with who sent it: **Accept** or **Decline**.

### In a channel

- **Type** and **Alert me** (**When my name or a keyword appears**, **Every message** or **Never**) work as for [Jabber rooms](jabber.md#in-a-room). **Leave Room** leaves the channel.
- People are listed on the right with their pictures. Hover a name for their rank (**Founder**, **Admin**, **Operator**, **Half-operator** or **Voice**) and why they're away, if they are.
- Colour and formatting codes are cleaned out of what people send.

### Menus

Right-click a **person** for:

- **Direct Message** — opens the conversation in Messages.
- **Who is this?** — a window with what the server says about them: real name, account, away, how long they've been quiet, when they connected, channels, address, server, and whether they're on an encrypted connection, a network operator or a bot. `/whois nickname` in a message box asks the same; in a conversation with someone, `/whois` alone asks about them.
- Where you're at least a half-operator: ranks to give or take away (those below your own), **Kick…** and **Ban…**. A ban asks for a reason and confirms which address it bans.

Right-click a **channel** in the list for:

- **Change Topic…** — unless only operators may change it and you aren't one.
- **Invite Someone…** — unless the channel is invite only and you aren't an operator.
- **Lift a Ban…** — for a half-operator or above.
- **Channel settings…** — for an operator (below).
- **Leave Room**.

The server can still refuse, and when it does, its answer shows in Group Chat.

### Channel settings

**Channel settings…** opens a window with every mode the channel has, in words, read from what this server supports. Hover a setting for what it does. Examples are **Invite only**, **Only voiced people and operators speak**, **Only operators change the topic**, **Hidden from the channel list**, **Password to join** and **Most people allowed in**. Modes without a name here go in **Other modes, for those who know IRC**, typed as MODE takes them.

Changes to the settings are sent when you press **Save**. The **Bans**, **Ban exceptions** and **Invite exceptions** lists change as soon as you add or remove a line (a mask such as `nick!user@host`, with `*` matching anything). The server refuses what your rank doesn't allow, and says so in Group Chat.

## Writing messages

The same box is used in channels and in Messages.

- **Enter** sends; **Shift+Enter** starts a new line. Where the server supports messages of several lines, they go as one message; otherwise each line is its own. A long line is split between words to fit.
- **Commands** — `/me` for an action, `/nick`, `/join`, `/part` (or `/leave`), `/topic`, `/msg` (or `/query`), `/notice`, `/away`, `/back`, `/whois` and `/quote` (or `/raw`) for a line sent as typed. Start a line with `//` to send it as words starting with a slash.
- **Replies** and **reactions** — hover a message for **Reply** and **React**, where the server supports them. They work as in [Jabber](jabber.md#writing-messages).
- **Take back your own** — hover one of your messages and click **Delete for everyone**, where the server lets messages be taken back. That needs you logged in to an account, or an operator in the channel.
- **Files** — **Attach** shows in channels and direct messages where the server names a file host. The file is uploaded from this computer with your **Account (SASL)** login, and its link is posted as an ordinary message. Nothing is sent to a file host that isn't encrypted, and a host may refuse you if you aren't logged in to an account. The host decides what kinds and sizes of file it takes, and refuses a file that's too big before it's sent.
- **Paste** — **Ctrl+V** (**Cmd+V** on a Mac) sends a screenshot, a copied picture or copied files where the conversation takes files.
- **Pictures** — a picture link shows the picture, as for [Jabber](jabber.md#pictures): straight away from the server's own file host, after **Show picture** from anywhere else.

Requests other IRC programs send for the program's version or a ping are answered.

### Read markers

On a server that keeps read markers, and while you're logged in to an account, where you've read up to in each conversation is kept by the server for your account. A conversation read on your phone, or in any other program on the same account, then shows as read here, and the other way round.

## Direct messages

Conversations with people are in [Messages](tools/messages.md), with online and away, typing, and reactions. Start one with **New Conversation**, from **Direct Message** on a person's menu, or with `/msg nickname text`.

An IRC server delivers only to someone connected now, and keeps nothing for later, so Messages refuses to send to someone who's offline.

## It runs with the background work

Like Jabber, IRC runs under the worker lease. In plain terms: on a [PostgreSQL setup](storage-postgresql.md) shared by several computers, only one of them does the [background work](background-processing.md#one-worker-many-readers) at a time, and that one, a headless worker included, keeps the IRC connections.

- **What's said is saved with every window closed**, as long as some client or worker is doing the background work.
- **Every client shows the same** channels, people and unread counts. The others show what the worker saved, and ask it to send, join or change things for them. Passwords and channel keys aren't passed along that way: they're read from where your logins are kept.
- **One connection per server for the whole database**, which suits IRC: a nickname has one connection, and two computers each connecting would fight over it.
- **Connect when the app starts** is a setting of the server: the client doing the background work connects it when that client starts, or when it takes the work over.
- With nobody doing the background work, a server shows **Waiting for the background process**. Something you sent that nothing picks up within 15 seconds is dropped, and you're told. To keep a computer from ever taking the work, see **Never run the background work on this client** in [Background processing](background-processing.md#one-worker-many-readers).

On SQLite there's only one process, so it's always the one.

## Limits

- No emote packs on IRC.
- You can't edit a message you've sent; you can take it back where the server allows.
- Saved messages are kept for as long as the **Direct Messages** and **Group Chat** rules under **Settings ▸ Data Retention** say: 30 days to start. See [Chat history](tools/messages.md#chat-history).
- Chat times are in EVE time.
