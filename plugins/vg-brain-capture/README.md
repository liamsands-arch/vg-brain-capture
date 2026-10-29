# vg-brain-capture (VG Brain autosave)

VG Brain autosave. Restricted: do not install it unless Liam Sands has given it to
you by name. The server accepts uploads only from people on its autosave list.

## What it does

The brain tools (search, save, share, teams) come from the **VG Brain connector**
in claude.ai. This plugin adds what a connector can't: hooks that run on your
computer.

| Hook | When it runs | What it does |
|---|---|---|
| `session-start` | a chat opens | loads your brain context and registers the session |
| `session-catchup` | a chat opens | uploads any earlier session whose upload did not complete |
| `pre-compact` | before a long chat is compacted | uploads the transcript so nothing is lost to compaction |
| `session-end` | a chat closes | uploads the session transcript |

It also sets the **VG Assistant** output style.

Its connection to vg-brain.com (`/autosave/mcp`) is sign-in only and offers no
tools. The hooks use that sign-in to reach your notes.

## Where the captured notes go

To your own notes, and nowhere else. Capture and sharing are separate: nobody else
can read a captured session until you share it, either one note at a time or by
granting someone standing access to everything you write.

If a chat should not be saved, say so in the chat ("don't save this", "skip this
chat") and it is excluded.

## Install

Uninstall the old `vg-brain` plugin first, and make sure the VG Brain connector is
connected in claude.ai. Then:

```
/plugin marketplace add liamsands-arch/vg-brain-capture
/plugin install vg-brain-capture@vg-brain-capture
```

To stop automatic capture, remove this plugin. The connector keeps working.
