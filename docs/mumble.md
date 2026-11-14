# Mumble

EVE Console has a **Mumble** voice client built in, so you can talk on your corp or alliance comms without running a separate program. You can add any number of servers and be connected to several at once, each talking only on its own keys.

- **Settings ▸ Mumble** — click the **⚙** gear button in the top-right of the title bar, then open the **Mumble** tab. Servers, keys, channel targets and sound settings are set here.
- **The title bar** — each connected server gets a small bar beside the EVE clock, with its channels, mute, deafen and sound settings.
- **Group Chat** — each connected server's text chat. See [Group Chat](tools/messages.md#group-chat).
- **Messages** — private text messages to people on the server. See [Messages](tools/messages.md).

## Add a server

1. On **Settings ▸ Mumble ▸ Servers**, click **Add Server**.
2. On the server's **Connection** tab, fill in:
    - **Name** — what the app calls it. Blank uses the host.
    - **Server host** and **Port** (`64738` to start with).
    - **Username** — the name others see.
    - **Password (if the server has one)**.
    - **Access tokens (optional, separated by commas)** — for channels that ask for one.
    - **Connect when the app starts** — for **this computer only**. Either way, a server that loses its connection reconnects by itself until you press **Disconnect**.
    - **Talk by voice, without holding a key** — see [Voice activation](#voice-activation).
3. Click **Connect** at the top.

Changes save as you make them. Changes to the host, port, username, password and tokens apply the next time the server connects. **Delete** removes the server and its settings after asking. Its certificate goes too, so a name you registered on that server would be lost.

The dot beside each server shows how it stands: green when connected, amber while connecting, red when something needs you.

!!! note "Your identity on a server"

    The app makes a certificate for each server, which is how the server knows it's you, and what a registered name is tied to. On a [PostgreSQL setup](storage-postgresql.md) the server list, the password and the certificate are shared by every computer using the database, so you're the same person from each. That's also why **Connect when the app starts** is per computer: a server takes one connection per person, so two computers connecting as you would keep throwing each other off.

### A certificate the app doesn't trust

Most Mumble servers use a certificate they made themselves. The first time, the server shows **The server's certificate is not trusted.** with its fingerprint and **Trust This Certificate**. Trust it only if you expect this server. From then on, only that certificate is accepted; if it changes, you're asked again.

## Talking

### Keys

Each server has its own keys, set on its **Channel Targets** tab. To set one, click its button, then press the key or mouse button to use; **Esc** cancels and **Clear** removes it. The keys work while that server is connected, even with the app in the background and the game in front.

A new server starts with two **channel targets**, each with a key to hold while you talk:

- **Whisper: the channel I'm in** — only the channel you're in.
- **Shout: my channel and those linked to it** — your channel and any channels linked to it. This is what Mumble calls plain push-to-talk.

The line above the targets says, for the channel you're in, which channels each one reaches.

Below the targets are two switch keys, which work from anywhere:

- **Mute key** and **Deafen key** — each press turns it on or off, as the buttons do.

And a held key:

- **Whisper to selection key** — see [Whisper to whoever is selected](#whisper-to-whoever-is-selected).

!!! info "One key, one job"

    Every key the app listens for from anywhere is in one list: each Mumble server's talk, mute, deafen and selection keys, and the [AI agent's](ai-agent-eden.md#speech-input-optional) push-to-talk key. A key already used somewhere else is refused when you choose it, with a red line that names the other use and where to change it. A clash saved before this check existed shows as an amber warning on both keys, because one press would do both.

On Windows a key still does its normal job as well, so a key you type with will talk as you type. F13 to F20, or a spare mouse button, make good talk keys.

### Channel targets

A channel target is who one key talks to on this server. Change them as you like, or click **Add Channel Target** for more:

- **Name** and **Key**.
- **Channels** — click **Add Channel** for each. A new line starts on **<Current Channel>**, whichever channel you're in at the time. The list then has **Root** and, while connected, the server's channels. A channel you picked stays shown while you're offline, or after it's gone from the server. Tick **Linked channels** and **Subchannels** to reach those too.
- **People, wherever they are (names, separated by commas)**.
- **Only members of this server group, in those channels (optional)**.

A server has room for 29 targets besides plain shout.

### Whisper to whoever is selected

Set a **Whisper to selection key**, then hold it to talk to whatever is selected in the channel tree:

- **Select a person** with a click or a right-click, or **a channel** with a right-click (a plain click on a channel still moves you there). You can't select yourself.
- The selection is highlighted in the tree, and **→** and its name show beside your name while you hold the key.
- Under **When a channel is selected, also reach**, tick **Linked channels** and **Subchannels** to include them.
- With nothing selected, or a person who has left, nothing is sent.

### Voice activation

Tick **Talk by voice, without holding a key** on a server's **Connection** tab to talk without a key. Your microphone then stays open while connected to that server, and whatever is louder than the **Voice activation level** in the sound settings goes out. The keys still work.

### Mute and deafen

The mute and deafen buttons on the server's bar, and the mute and deafen keys, work per server. Deafening also mutes you; undeafening puts back the mute you had before. Unmuting while deafened takes the deafening off too.

## The title bar and the overlay

While you're connected, the title bar shows a bar per server, beside the EVE clock:

- **Channels** — opens the [channel tree](#the-channel-tree).
- The server's name, green while connected, the channel you're in and how many there can hear. Hover it for more.
- **Mute**, **Deafen** and **Sound Settings**, a drop-down with your microphone, speakers and their volumes.

Tick **Show who is talking, always on top** on **Settings ▸ Mumble ▸ Settings** for a small window that stays over the game. It has a column per server, with your name lit as you talk, the same controls, and who's talking under them. Drag it by any part of it.

Names light up as people talk: in one colour for talking in their channel, another for talking through a channel target, and a third for someone talking to you alone.

On a [Client Layouts](tools/client-layouts.md#panel-controls) panel (Windows only), a **Mumble** control shows one server the same way, with a power button to connect or disconnect.

## The channel tree

The tree opens from **Channels** on a server's bar.

- **Click a channel** to move there. The arrows open and close channels with others under them.
- **People are hidden** at first. The button beside **Find someone** shows them in each channel; the choice is remembered. Channels with people in them still open as far as those people.
- **Each channel with people** shows how many are there and how many of them can hear (aren't deafened).
- **Find someone** — shows only the people found, and the channels down to them.
- Channels have a colour of their own, and the one you're in is bold. People have their pictures beside their names.
- **Drag a person onto a channel** to move them, or yourself. Dropping onto a person means their channel. If the server refuses, the tree says so.

### The person menu

Right-click someone for:

- **Send Message** — opens a private conversation in [Messages](tools/messages.md).
- **Mute for Me** — silences them for you only.
- **Ignore Their Messages**.
- **Volume and Details…** — their volume for you only (up to 300%), how long they've been online, their comment, and flags such as **Muted themselves** or **Recording**.
- **Register This Name…** — ties their name to their certificate. Only an admin can undo it.

Then, only where the server gives you the right:

- **Server Mute**, **Server Deafen** and **Priority Speaker**.
- **Move to My Channel** and **Move To…**.
- **Kick…** and **Ban…**, with a reason.

Right-click yourself for **Details…**, where you set **What others see about you** (your comment) and your picture: **Choose a picture…** or **Use an EVE portrait**, and **Remove picture**. A server keeps a picture only for registered users; otherwise it lasts until you disconnect.

### The channel menu

Right-click a channel for:

- **Join Channel**.
- **Listen to This Channel** / **Stop Listening** — hear it without moving there.
- **Link With My Channel** / **Unlink From My Channel**.
- **Details…** — its name and description, which you can change where allowed.
- **Server Information…** (on the root) — the server's version, its bandwidth per person, who's there, and its **Ban List**, where **Remove** lifts a ban.

Then, where the server allows: **New Channel…**, **New Temporary Channel…**, **Remove Channel…** and **Permissions…**.

A line only shows when the server gives you the right for it. If it still refuses, the tree says **The server refused that. You may not have permission.**

### Permissions

**Permissions…** is offered when you have Write on the channel. It has two tabs:

- **Permissions** — the channel's lines, with lines from channels above greyed out (change those there). Each line is for a **Group** or a **Registered person**, says whether it **Applies here** and/or **Applies to subchannels**, and has **Allow** and **Deny** for each permission. Lines further down win over those above them: use **Up** and **Down** to order them. **Take the permissions of the channels above** sets whether the channel inherits.
- **Groups** — make or remove groups, or put one back as it is above; add members by registered name, or take away members that come from above. Server-wide permissions are offered on the root only.

After saving, the editor reads the permissions back from the server and says if the server didn't keep everything, or didn't answer. A server drops messages sent too fast, so wait a moment, then **Read again**.

### Priority speakers

While someone who is a priority speaker talks, everyone else is turned down by 18 dB, so they can be heard. Someone whispering to you directly isn't turned down.

## Text chat

- **Channel chat** is in [Group Chat](tools/messages.md#group-chat), under the server. Tick **Include subchannels** to send one message to the channels under yours too; it's off again after sending. What's said there lasts until the app closes, as a Mumble server keeps none of it.
- **Private messages** are in [Messages](tools/messages.md). Mumble can only deliver to someone who's connected. They're saved, and kept by the **Direct Messages** rule under **Settings ▸ Data Retention**.

## Sound settings

**Settings ▸ Mumble ▸ Settings** applies to every server:

- **Show who is talking, always on top** — the overlay above. Off to start.
- **Microphone** and **Microphone volume** (100% to start, up to 300%).
- **Level my voice automatically** — on to start.
- **Play a tone when I start and stop talking**.
- **Reduce background noise**.
- **Cancel echo from my speakers** — for listening on speakers, so others don't hear themselves through your microphone. A headset has nothing to cancel. While it's on, the microphone stays open so it can learn your room; nothing is sent unless you talk.
- **Voice activation level** — how loud you must be for voice activation (−40 dB to start). **Microphone just now** shows your level to set it against.
- **Speakers** and **Speaker volume** (100% to start, up to 200%).

**System default** follows your system's own choice of device.

### An unplugged headset

If your headset is unplugged, voice moves to whatever device the system now uses, and the microphone keeps working.

- **On Windows**, a device arriving or leaving is noticed straight away, and a headset plugged back in is used again.
- **On Linux and macOS**, the app notices when sound stops flowing for half a second, and opens the devices again; the system's own default usually follows the change by itself.

## Platform limits

- **Global keys on Linux** need an X11 session. Under Wayland they may not work. Mouse buttons can't be used as keys there.
- **Global keys on macOS** need no Accessibility permission. Only keys a Mac keyboard has can be used: no mouse buttons, and no Shift, Ctrl, Alt or similar keys on their own.
- **On Linux and macOS** the system hands a key to EVE Console alone while it's set, so other programs don't see it. Pick a key you don't type with.
- **The microphone on macOS** — macOS asks once, the first time it opens. If you said no, turn it back on under **System Settings ▸ Privacy & Security ▸ Microphone**.
- **Echo cancelling** needs a sound library that may not load on every computer, for example an older Linux. The setting then says **Echo cancelling can't run on this computer, as its sound library would not load. Voice still works.**
- **Mumble runs on each computer itself**, not with the [background work](background-processing.md): voice is one session per person, at the computer you're sitting at. A headless worker doesn't connect to Mumble.
