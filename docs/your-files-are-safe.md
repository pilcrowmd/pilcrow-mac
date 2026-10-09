# Your files are safe

PilcrowMD opens your files and writes them back. It does not keep its own copy, does not
upload your files (the one exception: if you turn Mermaid on, the text of each diagram is sent
to mermaid.ink to be drawn), and does not change what you wrote unless you edit it. This page lists
every rule the app follows when it saves, in plain words, so you can check them.

---

## The rules

| Rule | What it means for you |
|---|---|
| **Nothing is written unless you edited** | Opening, reading, scrolling and pressing ⌘S on an unchanged file write nothing. The file's date does not change. |
| **A save is all-or-nothing** | The new text is written to a separate file first, flushed to disk, then swapped in. A crash or power cut leaves either the old file or the new one, never half of each. |
| **An interrupted save is finished** | If the app stops in the middle of a save, it completes that save the next time it starts. |
| **Another app's changes are never overwritten silently** | If the file changed on disk since you opened it, saving asks first: Save As… / Overwrite / Cancel. This covers ⌘S, closing, quitting, and leaving a note through a link or Back. |
| **Cancel means nothing is written** | In every save box, Cancel leaves the file on disk exactly as it was. |
| **Your bytes stay yours** | A file that starts with a byte-order mark (BOM) keeps it. A file without one never gets one. Windows (CRLF) and Mac/Linux (LF) line endings are kept. |
| **No autosave** | The app only writes when you save. |
| **No network** | The app makes no network connections, with one opt-in exception (Mermaid diagrams, see Privacy). |

---

## What happens when you save – step by step

1. You press ⌘S (or close, quit, or leave the note and choose Save).
2. If you made no edits, nothing happens.
3. PilcrowMD checks the file on disk. If its date or size changed since the app last read
   or wrote it, you get the box: **Save As… / Overwrite / Cancel**.
4. The text is written to a staging file in the app's own folder and flushed to disk.
5. A copy is placed next to your file and swapped in with one system call.
6. The status line shows *"Saved name.md"*.

![When another app changed the file, saving asks first](../images/overwrite-box.png)

---

## What we tested

Every rule above was checked on the beta build, on a real Mac, by looking at the file on
disk (its bytes and its date) after each step:

| Test | Result |
|---|---|
| Another app saves while you have unsaved edits, then ⌘S → Cancel | File unchanged, same date |
| Same, then close → Save → Cancel | File unchanged, window stays open |
| Same, then Overwrite | Your text written, window closes |
| Same, leaving the note through a link or Back → Save → Cancel | File unchanged |
| ⌘S on an unedited file | Nothing written, same date |
| Edit and save a file with a BOM and Windows line endings | BOM and CRLF kept, only the edited word changed |
| Edit and save a plain file | No BOM added, LF kept |

The app also runs about 700 automated tests before every build, including tests written to
fail if any of these rules break.

---

## Limits you should know

These are not hidden. They are also listed under [Known issues](../README.md#known-issues-in-this-beta).

- **Unsaved edits are lost if the app crashes.** There is no autosave and no draft recovery.
  Save often.
- **Mixed line endings become uniform** when you edit and save a file that mixes CRLF and LF.
- **A lone carriage return (CR) inside a line becomes a line break** when you save.
- **Hard links break on save.** Other hard-linked names keep the old text.
- **Only UTF-8 files open.** Other encodings are refused with a general error message.
- **"Changed" means date or size.** A tool that rewrites a file keeping the exact same date
  and size is not detected.
- **No file locking.** Two apps can still write the same file. PilcrowMD only promises it
  will not overwrite the other app's work without asking you.

---

## Where the app keeps its own data

| What | Where |
|---|---|
| Settings, recent files, added folders | `~/Library/Preferences/com.pilcrowmd.mac.plist` |
| N/U marks for added folders | `~/Library/Application Support/PilcrowMac/NoteMarks/` |
| Staging files for saves in progress | `~/Library/Application Support/PilcrowMac/PendingSaves/` |

Nothing else. To remove the app completely, delete it from Applications and delete these.
