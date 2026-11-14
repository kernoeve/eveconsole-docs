# Jabber

EVE Console has a **Jabber** (XMPP) client built in, so you can sit in your corp or alliance rooms and answer direct messages without running a separate chat program. You can add any number of servers.

Jabber is spread over three places:

- **Settings ▸ Jabber** — click the **⚙** gear button in the top-right of the title bar, then open the **Jabber** tab. This is where servers are added, and where your status, contacts' requests, your picture and emote packs are set.
- **Group Chat** — the rooms. Open it from its icon at the top of the window, beside the Eve Mail and Messages icons. See [Group Chat](tools/messages.md#group-chat).
- **Messages** — direct messages with people. Open it from the left sidebar under **Communication**, or from its icon at the top of the window. See [Messages](tools/messages.md).

[IRC](irc.md) and [Mumble](mumble.md) show up in the same two tools, so one list holds all your chat.

## Add a server

1. On **Settings ▸ Jabber**, click **Add Server**.
2. Fill in:
    - **Name** — what the list calls it, such as "Corp Jabber". Blank uses the login.
    - **Login (name@domain)** — your Jabber address, such as `ember@chat.example.com`.
    - **Password**.
    - **Server host (optional)** — leave it blank and the app finds the server from the login's domain. Fill it in only if your group gives you a specific host.
    - **Port** — `5222` to start with.
    - **Encrypted from the start (usually port 5223)** — tick it only if your group says the server wants that; then change the port too.
    - **Nickname in rooms (optional)** — the name rooms show for you. Each room can still be given its own when you join it.
    - **Resource (optional)** — leave it blank unless you know you need it.
    - **Connect when the app starts** — on for a new server. Either way, a server that loses its connection reconnects by itself until you press **Disconnect**.
    - **Alert keywords, separated by commas** — words that raise an alert in a room as your name does, such as `ECE, Ember, ping`.
3. Click **Save**. A new server connects straight away, which is the quickest check that the login is right.

The dot beside each server in the list shows how it stands: green when connected, amber while connecting, red when something needs you, grey when off. The line under it says why, for example **The server refused the login. Check the password.**

Select a server to see its state, **Connect** / **Disconnect**, and **Edit**. **Delete** in the editor removes the server and every message saved for it, after asking.

!!! info "Encryption is required"

    EVE Console only talks to a Jabber server over an encrypted connection. If a server doesn't offer encryption, nothing is sent and the server shows **The server does not offer encryption, so nothing was sent.** The password is never sent in the clear.

### A certificate the app doesn't trust

A private server often uses a certificate it made itself. Instead of connecting, the server then shows **The server's certificate is not trusted.** with the certificate's fingerprint and a **Trust This Certificate** button. Compare the fingerprint with what the server's admin published, and only then trust it. From then on, only that certificate is accepted for this server: if it changes, you're asked again.

### Where the password is kept

- **On SQLite**, it's kept on this computer, in a file of its own, protected the same way as the database password (by Windows for your account, your desktop keyring, or the macOS Keychain).
- **On [PostgreSQL](storage-postgresql.md)**, it's kept in the shared database, encrypted with a key made from the database password. That way whichever computer is doing the [background work](background-processing.md) can sign in, even with nobody at it. If you change the database password, type the chat passwords again.

When editing a server, leave **Password** blank to keep the one saved.

## Your status, contacts and picture

While a server is connected, its page in **Settings ▸ Jabber** has:

- **Status** — **Online**, **Free to chat**, **Away**, **Away for a while** or **Do not disturb**, with a line of text your contacts see (press **Enter** to set it).
- **Add Contact** — type their **Address (name@domain)** and, if you like, a **Name**, then **Add**.
- **Your picture** — **Choose a picture…** (PNG, JPEG, GIF, WebP or BMP, under 20 MB), or pick one of your characters under **Use an EVE portrait**. It's sent as soon as you choose it, made square and small. **Remove picture** takes it off. Nothing changes your picture unless you do it here.

Someone asking to add you shows in the server list with **Wants to add you**. Select them and choose **Accept**, which lets them see when you're online and asks to see their status too, or **Decline**, which keeps your status hidden from them. You can message each other either way.

Your contacts themselves are listed in [Messages](tools/messages.md), which can also add and remove them.

## Rooms

Rooms live in **Group Chat**. Each server is a line there, with its rooms under it.

### Join a room

1. In Group Chat, select the server and click **Add Rooms**.
2. The rooms the server lists appear, with their topic, how many people are in each and flags such as **Password needed**, **Members only**, **Moderated** or **Temporary**. Type in **Filter by name or description** to narrow them down, and change **Sort by** between **Name** and **People in room**. Rooms you're already in say **Joined**.
3. Click a room, or type its name under **Room (pick above, or type a name)** if the server doesn't list it.
4. Set a **Nickname in rooms (optional)** and the room's **Password** if it has one.
5. Choose the room's **Type**:
    - **General** — for talking.
    - **Intel** — also read for intel reports, like an intel channel in EVE's chat logs. Its reports feed the [Intel](tools/intel.md) tool, the map's live marks and the **Intel report** alarm. A report relayed into several rooms, or already read from an EVE chat channel, is counted once.
6. Click **Join**. Join as many as you like, then click **Done**.

Joining a room also saves it in your bookmarks on the server, set to join by itself, so your other Jabber programs get it too. Rooms you've bookmarked elsewhere appear here the first time the server is connected, and those set to join by itself are joined. Leaving a room turns that off again.

### In a room

The top of the room shows its topic, and whether it keeps an archive: a room that does fills in what you missed while you were away when you next connect; one that doesn't shows only what it replays when you join. **Load Earlier Messages** reads further back in what's saved here.

- **Type** changes the room between General and Intel.
- **Alert me** — **When my name or a keyword appears** (the default), **Every message** or **Never**.
- **Leave Room** leaves it. Its unread messages are marked read, so no alert is left behind.

The people in the room are listed on the right, with their pictures; hover a name for their role. If you can't get in, or are put out, the room says why (for example **You were kicked from this room.**, with who did it and their reason) and offers **Join Again**.

### Room menus

Right-click a **person** for **Direct Message**, which opens a conversation in Messages. Below it come only the lines the room's rules allow you: **Give Voice** / **Take Voice**, **Make Moderator** / **Remove Moderator**, **Make Member** / **Remove Membership**, **Make Admin** / **Remove Admin**, **Kick…** and **Ban…**. Kick and ban ask for a reason, which is shown to them.

Right-click a **room** in the list for **Change Topic…**, **Invite Someone…**, **Lift a Ban…** and **Leave Room**, again only as far as the room lets you. In a members-only room, inviting is offered only to an admin or owner. When a room refuses, its own words are shown.

An invitation to a room shows in the list under its server, with who invited you. Select it and choose **Accept** or **Decline**.

## Direct messages

Direct messages are in [Messages](tools/messages.md). Start one there with **New Conversation**, or right-click someone in a room and choose **Direct Message**.

- If the room shows their real address, the conversation is with them directly. If it hides it, the conversation goes through the room, can't carry files, and ends when they leave the room.
- A person who's offline gets your message when they next connect, if their server holds it. Messages says so above the box.
- If the server keeps an archive of direct messages, ones you missed while disconnected are caught up when you connect. The server's page in Settings says whether it does.

## Writing messages

Everything here works the same in rooms and in direct messages, unless it says otherwise.

- **Enter** sends; **Shift+Enter** starts a new line.
- **Replies** — hover a message and click **Reply**. A **Replying to …** bar shows above the box; **×** or **Escape** cancels. The reply shows what it answers above it. Older programs see a quote instead.
- **Edit your own** — hover your latest message and click **Edit**, or press **Up** in an empty box. Only your latest message can be edited, which is all Jabber allows. **Escape** cancels.
- **Delete your own** — hover it and click **Delete for everyone**. It asks first: programs that support it remove the message, but some older ones keep showing it.
- **Styling** — `*bold*`, `_italic_`, `~struck~`, `` `code` ``, a block of code between lines of ` ``` `, and `>` at the start of a line for a quote. The marks stay in the text, shown faintly, so the message reads the same in a program that styles nothing.
- **Reactions** — hover a message and click **React**. The picker offers the common ones first, then the standard emoji by group, searchable by their English names. Each reaction shows under the message once, with how many chose it; hover it to see who. Yours have an outline: click one to take it back, or click someone else's to add yours.
- **Files** — **Attach** puts a file on the server and sends its address. It shows only where the server takes files, and the server sets the largest size. Anyone who has the address can open the file.
- **Paste** — **Ctrl+V** (**Cmd+V** on a Mac) in the message box sends a screenshot, a copied picture or files copied in your file manager, where the conversation takes files. Text still pastes as text.
- **Read markers** — with a person (never in a room), **Seen** shows under your latest message they've read. The tick box **Tell people when I have read their messages** at the bottom of the server list in **Settings ▸ Jabber** decides whether they see the same from you. It's on to start.

When someone else deletes a message, it's replaced by **This message was deleted.**, or **Removed by a moderator.** with the moderator's reason. The words are gone from the screen and from the database too.

### Pictures

People's pictures show beside their messages and in people lists. Someone with none gets their first initial on a colour that's always the same for them.

A link to a picture shows the picture under its message, scaled to fit; click it to open it full size in your browser.

- A picture on the chat server's own file host loads straight away.
- A picture anywhere else waits for you to click **Show picture**, because loading it tells that site your IP address. The button's tip names the site.

### Emote packs

Each server can have its own emote packs: codes such as `:wave:` show as their pictures in that server's rooms and messages, and animated ones move.

On **Settings ▸ Jabber**, select the server and scroll to **Emote packs**:

1. Click **Load a pack…** and pick a smiley theme: its zip, or the file called `theme` in an unpacked folder. Packs are in Pidgin's smiley-theme format.
2. A pack loaded once is kept in the database, so it's there on every computer using it. To give another server a pack you've already loaded, pick it from the list and click **Add**.
3. Use **↑** and **↓** to order the packs: where two packs have the same code, the higher one wins.
4. **Remove** takes a pack off this server. If no other server has it, it's deleted after asking; load it again to get it back.

A pack can hold up to 5,000 pictures and 64 MB.

When writing, click the face button for the picker, which has a search box, or type `:` and two or more letters for a list of matching codes. Codes between colons are found anywhere in a message; faces like `:)` only on their own, and nothing inside a web address. Copying a message gives back the codes, not the pictures.

!!! note
    Reactions use standard emoji only, because that's all the protocol allows, so pack emotes aren't offered there.

## Alerts and sounds

A message that names you, or one of your alert keywords, lights the **Group Chat** icon in warning colours with a count. Any new message in a room you're in counts on the icon too, in plain colour. A new direct message lights the **Messages** icon. Clicking either icon opens what most needs reading. See [Alerts](tools/messages.md#alerts).

## Behind the scenes

### It runs with the background work

On a [PostgreSQL setup](storage-postgresql.md) with several clients, the Jabber connections are kept by whichever client is doing the [background work](background-processing.md#one-worker-many-readers), including a headless worker. That client saves everything that arrives, so messages are captured with every window closed, and every client shows the same rooms, people and unread counts. The other clients show what it saved and send through it.

- A client with nobody doing the background work shows **Waiting for the background process**. If nothing picks up something you sent within 15 seconds, it's dropped and you're told, rather than sent much later.
- The **Jabber** tab of [Background Processes](tools/background-processes.md) shows which client holds the connections, and each account and room with its state, its last message and how many came in the last 24 hours.
- On SQLite there's only one process, so it's always that one.

### A dropped connection

If the connection drops, the app reconnects by itself and, where the server allows, picks up the same session: you stay in your rooms, nobody sees you leave and come back, and messages sent meanwhile arrive. If the server had already let the session go, your direct messages it never confirmed are sent again, and so are room messages, once you're back in the room and only if the room doesn't already have them.

## Limits

- Only your latest message can be edited.
- No end-to-end encryption; the connection to the server is always encrypted.
- Chat times are in EVE time.
- Saved messages are kept for as long as the **Direct Messages** and **Group Chat** rules under **Settings ▸ Data Retention** say: 30 days to start. See [Chat history](tools/messages.md#chat-history).
