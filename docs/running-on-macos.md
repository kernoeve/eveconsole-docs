# Running on macOS

EVE Console runs natively on macOS, on Apple Silicon and on Intel Macs, and Mac builds ship alongside the Windows and Linux builds with every release. Everything the app needs is bundled, including the .NET runtime and VLC.

!!! warning "Not signed by Apple yet: macOS stops it the first time"

    EVE Console isn't signed by Apple, so macOS refuses to open it until you say otherwise, once for the installer and once more for the app. Open **System Settings ▸ Privacy & Security**, scroll down and click **Open Anyway**. The steps are in [Opening it the first time](#opening-it-the-first-time).

## What you need

**macOS 15 (Sequoia) or later.** That's the oldest version on Microsoft's support list for .NET 10, which EVE Console runs on. Nothing in EVE Console checks the version, and .NET's own lower limit is macOS 12, so an older Mac may get further, but that isn't supported or tested.

## Downloads

All four come from the [Releases page](https://github.com/kernoeve/EveConsole/releases/latest). Pick the ones for your Mac. **Apple menu ▸ About This Mac** says **Chip** and an Apple M-series name on Apple Silicon, or **Processor** and an Intel name on an Intel Mac.

| Your Mac | Installer | Portable |
| --- | --- | --- |
| **Apple Silicon** (M1 and later) | [`EveConsole-osx-arm64-Setup.pkg`](https://github.com/kernoeve/EveConsole/releases/latest/download/EveConsole-osx-arm64-Setup.pkg) | [`EveConsole-osx-arm64-Portable.zip`](https://github.com/kernoeve/EveConsole/releases/latest/download/EveConsole-osx-arm64-Portable.zip) |
| **Intel** | [`EveConsole-osx-x64-Setup.pkg`](https://github.com/kernoeve/EveConsole/releases/latest/download/EveConsole-osx-x64-Setup.pkg) | [`EveConsole-osx-x64-Portable.zip`](https://github.com/kernoeve/EveConsole/releases/latest/download/EveConsole-osx-x64-Portable.zip) |

- **Installer** — puts **EVE Console** in `/Applications`, or `~/Applications` if you install it for yourself only, and opens it when it finishes.
- **Portable** — open the zip and run the app inside. Move **EVE Console.app** out of Downloads first, to Applications or wherever you like, because macOS runs a downloaded app from a temporary read-only copy until it has been moved.

They're the same app. **The installer keeps itself up to date**, as the Windows builds do. Each architecture updates from its own channel, so it stays on the build for your Mac. Updating a Portable copy hasn't been tried yet. See [Staying up to date](getting-started.md#staying-up-to-date).

## Opening it the first time

1. Open the `.pkg`, or for the Portable build, **EVE Console.app**. macOS says it can't check the file and won't open it. Close that message, and don't move the file to the Trash.
2. Open **System Settings ▸ Privacy & Security** and scroll down to **Security**. A line names what was stopped.
3. Click **Open Anyway**, and confirm with your password or Touch ID when macOS asks.
4. With the installer, this happens twice: once for the `.pkg`, then again for the app the first time it launches. Repeat steps 2 and 3.

**Open Anyway** only appears after you've tried to open the file. On current macOS, right-click ▸ **Open** no longer gets past this.

!!! tip "From the Terminal"

    For a Portable copy, this removes the mark macOS puts on downloads, which is what stops it:

    ```bash
    xattr -dr com.apple.quarantine "/Applications/EVE Console.app"
    ```

## Where data lives

Your data and configuration live under your home directory:

- Database (SQLite): `~/Library/Application Support/EveConsole/EveConsole.db`
- Configuration (`config.json`), backups, profiles and downloaded voice models: the same `EveConsole` folder.

Finder hides `Library`: use **Go ▸ Go to Folder…** and paste the path. This is per-user, and it never shares a folder with the app, so replacing or deleting **EVE Console.app** leaves your data alone. To remove everything after deleting the app, delete that folder yourself.

## Saved secrets: the Keychain

The [PostgreSQL password](storage-postgresql.md#where-the-password-is-stored) and the Cloudflare token for [web stores](stores/index.md) are kept in your macOS **Keychain**, as items named **EVE Console**. `config.json` holds only a reference to them, so copying it to another machine doesn't take the secret along, and you type it once there. The app says so beside each.

## EVE's logs

The app looks for this computer's own logs in the first of these it finds, for both `Gamelogs` and `Chatlogs`:

- `~/Documents/EVE/logs/`
- `~/Library/Application Support/EVE Online/p_drive/User/My Documents/EVE/logs/`, where the older Mac client wrote them.

macOS may ask once whether EVE Console can read your Documents folder. Allow it, or the logs can't be read. To read anywhere else, such as a share mounted under `/Volumes`, add it under **Log Folders**. See [Logs & Map Data](logs-and-map-data.md).

## Sound

Alarm sounds need nothing installed. VLC comes inside the app, and each package carries only the copy for its own architecture.

## The AI agent's voice and microphone

**Voices:** Kokoro, a local speech server, OpenAI and ElevenLabs are all available on a Mac. **Piper isn't available on macOS**: its Mac build doesn't start and the project has been archived, so the voice settings say so and ask you to choose another engine. See [Voice](ai-agent-eden.md#voice-optional).

**Speech input:** OpenAI Whisper and Local Whisper are both available. See [Speech Input](ai-agent-eden.md#speech-input-optional).

**Microphone:** macOS asks once, the first time the microphone opens. If you said no, turn it back on under **System Settings ▸ Privacy & Security ▸ Microphone**.

**Push-to-talk key:** this needs no Accessibility permission.

- The choices are **F13** to **F20**, **Insert** (the Help key on keyboards that have one), and **Numpad 0**, **\***, **/** and **-**. **Scroll Lock** and **Pause** aren't offered, because a Mac keyboard doesn't have them.
- A MacBook's built-in keyboard has none of these keys, so a push-to-talk key needs an external keyboard. The mic button in the agent panel works without one.
- While it's set, the key belongs to EVE Console, and other apps don't see it.

## The menu bar icon

Under **Settings ▸ Polling ▸ Notification Area Icon**, tick **Show a menu bar icon, starting when you log in**. It starts straight away too. Its menu has **Background Processes**, **Open EVE Console** and **Exit**. It's a small separate process that shows which client is doing the background work, and it never does that work or sounds alarms itself. See [A tray or menu bar icon](background-processing.md#a-tray-or-menu-bar-icon).

Ticking the box writes a launch agent, `~/Library/LaunchAgents/com.eveconsole.tray.plist`, which macOS starts when you log in. macOS also lists it under **System Settings ▸ General ▸ Login Items**, where you can switch it off.

- **Exit** really exits: nothing restarts it until you next log in.
- Unticking removes the launch agent. An icon already showing stays until you choose **Exit** on it, or log out.
- The launch agent names where the app is. If you move the app, untick the box and tick it again.

## Backups on PostgreSQL: `pg_dump`

Backups of a [PostgreSQL](storage-postgresql.md#backups) database run `pg_dump`, which comes with PostgreSQL's client tools, not with the app. An app opened from the Finder doesn't see the folders your Terminal does, so EVE Console also looks in the usual places itself, and uses the newest it finds:

- **Homebrew:** `/opt/homebrew/bin`, `/opt/homebrew/opt` and `/usr/local/bin`
- **Postgres.app:** `/Applications/Postgres.app/Contents/Versions`
- **The EDB installer:** `/Library/PostgreSQL`

**Check for pg_dump** under **Settings ▸ Database** shows which one it found.

## Command-line switches

Switches such as `--profile` go to the program inside the app:

```bash
"/Applications/EVE Console.app/Contents/MacOS/EveConsole" --profile test
```

A profile lives under `~/Library/Application Support/EveConsole/Profiles/<name>`. See [Can I run a second, separate copy?](faq-and-troubleshooting.md#can-i-run-a-second-separate-copy)

## Running headless

The [background worker](background-processing.md#running-headless) starts on a Mac the same way, with `--headless`, and needs no display:

```bash
"/Applications/EVE Console.app/Contents/MacOS/EveConsole" --headless
```

EVE Console doesn't set it up as a service on a Mac, though. **Settings ▸ Polling** has no service section there, and no `launchd` file ships with it. If you write your own, the rules are the same as for a [Linux service](running-on-linux.md#running-headless-as-a-service): use PostgreSQL, and give it the connection string in `EVECONSOLE_DB_CONNECTION`, because a service outside your login session can't read your Keychain. For a worker that's always on, a Linux machine or [Docker](running-on-linux.md#running-in-docker) is the supported way, with your Mac connecting to it as a desktop client.

## Keys

These pages say **Ctrl**. On a Mac, use **⌘** for copy, paste and picking several rows, as in any Mac app. There are three exceptions, where a grid does its own copying and takes **Ctrl+C**: [Assets](tools/assets.md), [Industry Jobs](tools/industry-jobs.md) and the AI agent's table tabs.

## What has been tried on a real Mac

!!! info "A first release: tell us what you find"

    EVE Console has been run on one Apple Silicon Mac, on macOS 26: starting, EVE sign-in, polling, and the menu bar icon. That Mac had no sound device and nobody at its keyboard, so **sound, voices, the microphone and the push-to-talk key** have passed only automated checks on GitHub's Mac machines: VLC plays a chime, the microphone library finds its inputs, and the hot key registers. The **Intel** packages are built and checked for what they carry, but haven't been run on an Intel Mac. The `.pkg` installer, updating itself and `--headless` haven't been run on a real Mac yet either: that testing used a Portable copy. If something misbehaves, say so on [Discord](https://discord.gg/H6NaAjJMar) or in [GitHub issues](https://github.com/kernoeve/EveConsole/issues).

## Building from source on macOS

The same steps as anywhere — clone, restore, run — using the [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0):

```bash
git clone https://github.com/kernoeve/EveConsole.git
cd EveConsole
dotnet run
```

A `dotnet run` build isn't a packaged app. It doesn't update itself, and it doesn't carry the app's `Info.plist`, which holds the text macOS shows when it asks for the microphone. The steps for a package are in the `macos` job of [`.github/workflows/release-build.yml`](https://github.com/kernoeve/EveConsole/blob/main/.github/workflows/release-build.yml).
