# Time Tracker: how to install it

A Windows app for tracking your day, with a small always-on-top widget and your Notion tasks. Your account, data, Notion database and keys are your own: nobody shares anything with anybody. It takes about 15 minutes.

**You need:** Windows 10 or 11, and an invitation (whoever gave you this page adds your email to the app's accounts, and adds you for Google Calendar if you want it). Everything else below is optional and can wait.

## 1. Install

1. Download **[Time-Tracker-Setup.exe](https://github.com/albertlevicek-crypto/time-tracker-releases/releases/latest/download/Time-Tracker-Setup.exe)**.
2. Run it. Windows will most likely show a blue window, **"Windows protected your PC"**, because the app isn't signed with a paid certificate. Click **More info**, then **Run anyway**.
3. It installs for your Windows user only, with no administrator password, and opens by itself.

The small floating window is the widget. Closing the main window keeps the app running in the tray (the small icons near the clock). To really quit: right-click the tray icon → **Quit**.

## 2. Sign in

1. Open **Settings → Tools → Account & sync**.
2. Type the email you were invited with and click **Send code**.
3. Type the code from the email and click **Sign in**.

**No code arrives?** Check your spam folder. If the app says **"This email can't sign in"**, your email hasn't been added yet, so ask the person who gave you this page. A code can be asked for once a minute.

## 3. Connect Notion

Go to **Settings → Tools → Notion → Set up**. The app guides you and offers two ways to connect:

- **Connection (owner):** if you own the Notion workspace. It's the most private, because the connection only sees the database you share with it.
- **Personal token (member):** if Notion doesn't let you create connections. The token acts as you, but the app only uses the database you pick. It expires after at most a year; then you make a new one. Notion shows the token only once, so paste it straight into the app.

Then:

1. **Pick your task database.**
2. **Map its fields.** Only the title and a **category** are required (a select, multi-select or status). Status, deadline, urgency, leverage, time estimate, actual time and assignee are optional: whatever you don't map simply stays out of the app, and nothing breaks.
3. If your time estimates are labels the app can't read, it asks you what they mean. It never guesses.

**What the app does in your Notion:** it reads the database you pick. It writes only three things: whether a task is done, its actual time (when you map those fields), and new tasks you track that aren't in Notion yet. It never changes or deletes anything else. The token is kept only in Windows Credential Manager.

## 4. Connect Google Calendar (optional)

Click **Settings → Tools → Calendar → Connect Google Calendar** and finish in your browser. The app only ever asks for permission to read.

- Google warns **"Google hasn't verified this app"**. That's expected for a small private app: click **Continue**.
- If Google says you have no access, you haven't been added as a tester yet. Ask the person who gave you this page.
- **About every 7 days** Google asks you to sign in again, because of how this kind of app is registered. The app then shows a **Reconnect Google Calendar** pill and loses nothing: click it and sign in.

## 5. AI suggestions (optional)

Off unless you turn it on. For a Random tasks note, the app can ask Claude which category fits. You use your own Claude API key and pay for it yourself (usually very little), and only the note and your category names are sent. Set it up under **Settings → Tools → AI suggestions**.

## A second computer

Everything follows your account except your secrets, which take one code and one click.

1. Install the app and sign in, as above. Within a minute your blocks, goals, Notion database, field map, chosen calendars and settings appear.
2. **This computer's name:** type e.g. "Laptop" and click **Save**. Your other computer then says "Running on Laptop" while you track here.
3. **Move your Notion token and Claude key.** Your other computer must be on and signed in.
   - **On the other computer:** **Settings → Tools → Another computer → Show a code**. It shows a code like `K7QF-2MXR-9TDP-H4WN`, valid for 10 minutes.
   - **On this computer:** **Settings → Tools → Another computer → Enter a code**. Type the code and click **Get them**.
4. **Google Calendar:** click **Connect Google Calendar** on this computer too. Your chosen calendars are already remembered.

**Why the code is safe:** your computer locks the token and key with the code before they go anywhere, and the code itself is never sent. The locked package waits in your account for at most 10 minutes and works once. Nobody can read it without the code, not even whoever runs the server.

**Good to know:**

- A computer that already has its own token or key keeps it; nothing gets overwritten.
- After a code, both computers use the same token. If you remove it in Notion or it expires, both stop until you connect again. To switch one computer off on its own, give it its own token under **Notion → Set up**.
- Hotkeys, the widget's place and size, the computer's name and start with Windows stay on each computer.
- **Actual time** in Notion is always the total of your blocks from all your computers; it's never added up twice. Mark Done and new tasks are sent once, from the computer where you did them. A computer that's offline catches up when it's back.

## Updates

The app checks by itself and asks before installing. Click **Install** and it closes and opens again in a few seconds; a running timer keeps running and nothing is lost. You can also look under **Settings → About → Check for updates**.

Every update is checked against a signature before it installs. If one ever fails that check, the app refuses it and tells you.

## Exporting your data

**Settings → Tools → Export** saves a CSV file in your Downloads folder, ready for Excel or Google Sheets. Nothing leaves your computer until you share the file yourself.

- Double-click the file and it opens in columns, with Czech characters intact. The file uses the separators your Windows uses (a Czech PC: `;` and `,`; an English one: `,` and `.`).
- To merge files from people with different Windows settings, use Excel's **Data → From Text/CSV** or Google Sheets' **File → Import**, which detect the separator.
- A block belongs to the day it started in, whole. So two exports next to each other never count a block twice.

### Every block: one row each

These columns stay the same in every version and for every person, whatever their Notion looks like. New columns only ever get added at the end. A field you haven't mapped is simply empty.

| Column | What it holds |
|---|---|
| `user email` | Your account's email; empty when not signed in |
| `date` | The day the block started, as `2026-11-09` |
| `start`, `end` | Local time, as `09:00`; `end` is empty while it's still running, and can be on the next day |
| `duration (minutes)` | Work time in whole minutes, with breaks already taken out |
| `entry type` | `work`, `break` or `idle` |
| `task title` | The task, or the title you typed |
| `category` | As written in Notion |
| `leverage`, `urgency`, `time estimate` | As written in Notion |
| `source` | How it was made: `widget` or `manual` (`voice` and `auto_suggested` are reserved for later) |
| `deep work` | `yes` when marked as deep work |
| `break minutes` | Short breaks inside the block |
| `random tasks` | `yes` for a Random tasks block. With ticked tasks it's one row per task, with its equal share of the time, under that task's category |
| `notes` | Your note; empty unless you turn on **Include notes**, since you may share the file |

### By week, month or quarter: the summary

Work time only, one row per period, category and leverage. The totals match the rows above.

| Column | What it holds |
|---|---|
| `user email` | As above |
| `period` | `week`, `month` or `quarter` |
| `period start` | Its first day: a Monday, or the 1st of a month or quarter |
| `category`, `leverage` | As written in Notion |
| `hours` | Work time, with two decimals |
| `deep work hours` | The part of it that's deep work |
| `deep work sessions` | How many deep-work blocks. A Random tasks block with several tasks counts once, on its first task's row |

## Where your data lives

- **On your computer:** an encrypted database. Your keys and tokens are in Windows Credential Manager.
- **In your account:** your blocks, goals and settings, so your computers stay in step. Your data is separated from everyone else's, but **whoever runs the server can technically see it**, as the app tells you at sign-in.
- **Sent elsewhere:** nothing, apart from what you connect yourself (Notion, Google Calendar, and Claude if you turn it on).
- The app never captures keystrokes, screenshots, your clipboard or page content.

## Uninstalling

**Windows Settings → Apps → Installed apps → Time Tracker → Uninstall.** It also stops the app starting with Windows. To remove your data from this computer too, delete the folder shown under **Settings → About → Data folder**. To remove your account and what's in it, ask the person who invited you.
