# PilcrowMD for Mac

A native Markdown reader and editor for the Mac. Open a `.md` file and read it the way
it was meant to look – headings, tables, code, maths, footnotes. Edit it, see the result side
by side, export it to PDF.

**Built for the age of AI agents.** Add a folder, and PilcrowMD keeps it live: when an agent,
a script or another app creates or changes a file, you see it within a second, with a mark
that says *new* or *updated*. And it never overwrites anyone's work without asking you.

This is a **beta**, free to use while the beta lasts. Mac questions and news: [pilcrowmd.com](https://pilcrowmd.com)

**Also on Android** – PilcrowMD for your phone, already in use: [Google Play](https://play.google.com/store/apps/details?id=com.pilcrowmd&referrer=utm_source%3Dgithub%26utm_campaign%3Dmac_readme) · [F-Droid](https://f-droid.org/packages/com.pilcrowmd/)

![PilcrowMD showing a project README, with the folder sidebar on the left and the outline on the right](images/use-coders.png)

---

## Watch an agent work in your folder

![An agent creates a report and edits a runbook; PilcrowMD marks them N and U and updates the open page](images/agent-folder.gif)

An agent writes `benchmark.md` → it appears with **N**. It edits `runbook.md` → **U**.
You open the report; when the agent adds a section, the page updates by itself.
More: [Folders and agents](docs/folders-and-agents.md).

## And when you both edit the same file

![You have an unsaved edit; the agent saves the same file; a banner warns you and saving asks first](images/agent-conflict.gif)

You are editing; the agent saves the same file. PilcrowMD shows a banner, and when you save
it asks: **Save As… / Overwrite / Cancel**. Cancel writes nothing. More:
[Your files are safe](docs/your-files-are-safe.md).

---

## What it does

- **Read, Split, Edit** – three modes, switch with ⌥⌘1 / ⌥⌘2 / ⌥⌘3.
- **Live folders** – add any folder; subfolders, new and updated marks, links between notes.
- **Tabs, Outline, Find, PDF export, text size, Light and Dark themes, three font sets.**
- **Markdown it draws:** tables, task lists, code with colours for 28 languages, maths,
  footnotes, callouts, collapsible sections, front matter, local pictures.
- **Safe saving:** writes only when you edited, all-or-nothing saves, keeps BOM and line endings,
  never silently overwrites another app's changes.
- **Private:** no account, no tracking, no network – except Mermaid diagrams, which are off
  until you turn them on.

Full list, with what it does **not** do: [What it does](docs/what-it-does.md).
Pictures for nine kinds of work: [Use cases](docs/use-cases.md).
Try the same notes yourself: [samples](samples/).

| Light theme | Split view |
|---|---|
| ![A quarterly review in the Light theme](images/use-business-light.png) | ![Markdown on the left, the page on the right](images/split-light.png) |

---

## PilcrowMD on Android

Read your notes on your phone too. The Android app is released, open source (GPL-3.0),
and available on Google Play and F-Droid.

[<img src="https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png" alt="Get it on Google Play" height="80">](https://play.google.com/store/apps/details?id=com.pilcrowmd&referrer=utm_source%3Dgithub%26utm_campaign%3Dmac_readme)
[<img src="https://f-droid.org/badge/get-it-on.png" alt="Get it on F-Droid" height="80">](https://f-droid.org/packages/com.pilcrowmd/)

Source and releases: [github.com/pilcrowmd/pilcrow](https://github.com/pilcrowmd/pilcrow)

---

## Requirements

- macOS 14 (Sonoma) or later.
- Tested on Apple Silicon (M1 and newer). The download also contains an Intel build, which has
  not been tested.

## Install

Download the DMG, open it, drag PilcrowMD into Applications. The first time you open it,
macOS blocks it because the app is not yet signed by Apple; you allow it once under
**System Settings › Privacy & Security › Open Anyway**.

Every step, with a picture: [INSTALL.md](INSTALL.md).

## Known issues in this beta

- **Unsaved edits are lost if the app crashes.** There is no autosave. Save often.
- **Mixed line endings become uniform when you save.** If one file mixes Windows (CRLF) and
  Mac/Linux (LF) line endings, every line gets the same ending. Files that use one style
  throughout are saved exactly as they were.
- **A lone carriage return becomes a line break** when you save.
- **Saving breaks hard links.** Other hard-linked names keep the old text. Aliases and
  symbolic links are not affected.
- **"Changed" means date or size.** A tool that rewrites a file with exactly the same date and
  size is not noticed.
- **Only UTF-8 files open.** Other encodings are refused with a message saying so.
- **Some characters do not draw inside maths:** curly double quotes and `\blacksquare`.
  The formula then shows as its source text; nothing is lost.
- **The window can grow too tall in Split view.** When another app changes the file while you
  have unsaved edits, the window may become taller than the screen while the banner shows.
  Your edits are not affected. Once the banner is gone, the window can be made smaller again.
- **Not signed or notarized by Apple** yet – see Install.
- **Intel Macs are untested.**

## Remove

Drag PilcrowMD from Applications to the Trash. To remove its data too, delete
`~/Library/Preferences/com.pilcrowmd.mac.plist` and the folder
`~/Library/Application Support/PilcrowMac/`.

## Report a problem

[Open an issue on GitHub](https://github.com/pilcrowmd/pilcrow-mac/issues)

## Licence

This beta is free to use, including at work. You may install it on any number of Macs and share the link
to the download page. Please do not put the installer on other sites. You may not sell it, change it, or present it as your own.
Provided as is, without warranty – keep backups of your files.

Full text: [LICENSE.md](LICENSE.md).
