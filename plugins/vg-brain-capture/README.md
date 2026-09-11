# vg-brain-capture

Automatic session capture for VG Brain. This is a restricted add-on. Do not install
it unless Liam Sands has given it to you by name.

## What it does

The base `vg-brain` plugin gives you the VG Brain tools: search, read, save on
request, share, groups. It captures nothing on its own. Every save is something you
or Claude did deliberately.

This add-on layers four background hooks on top of that:

| Hook | When it runs | What it does |
|---|---|---|
| `session-start` | a chat opens | announces where the chat will save, and registers the session id |
| `session-catchup` | a chat opens | uploads any earlier session whose upload did not complete |
| `pre-compact` | before a long chat is compacted | uploads the transcript so nothing is lost to compaction |
| `session-end` | a chat closes | uploads the session transcript |

With this installed, every Claude Code session you run is written to your own VG
Brain notes without you asking.

## Where the captured notes go

To your own notes, and nowhere else. Capture and sharing are separate:

- Capture puts the session in your personal space.
- Nobody else can read it until you share it, either by sharing a single note or
  by granting someone standing access to everything you write.

If a chat should not be saved at all, say so in the chat ("don't save this",
"skip this chat") and it is excluded. If something is genuinely confidential, use
an incognito chat instead, which never reaches the Brain in the first place.

## Install

Install it alongside `vg-brain`, never instead of it. This add-on carries no MCP
server, no skills, and no output style, so on its own it captures into nothing.

```
/plugin marketplace add liamsands-arch/vg-brain-universal
/plugin install vg-brain@vg-brain-universal
/plugin install vg-brain-capture@vg-brain-universal
```

To stop automatic capture, remove this plugin. The base `vg-brain` plugin keeps
working, minus the background uploads.

## Why it ships separately

Automatic capture used to be part of the base plugin. It was split out when the
default saving destination moved from a shared team space to each person's own
notes, so that background capture is something a person is handed on purpose
rather than something that arrives with the tools.
