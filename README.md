# VG Brain — automatic capture (add-on)

A separate marketplace holding one plugin: the background hooks that upload
Claude Code sessions to your own VG Brain notes.

## Why this is its own repo

Auto capture used to ship inside the standard `vg-brain` plugin, so everyone who
installed the brain got it whether they wanted it or not. It is now opt-in, and
it lives here rather than beside the base plugin so that it does not show up in
the plugin list of people who are not meant to install it. Keeping it out of
sight is the point: this repo is public, and the separation is about avoiding
confusion, not about secrecy.

## Install

You need the base `vg-brain` plugin first. This one adds to it, and replaces
nothing.

In the Claude Code app: **Customize → Plugins → add marketplace**

```
https://github.com/liamsands-arch/vg-brain-capture
```

Then install `vg-brain-capture` and restart the app.

## What it does

Three hooks, all of which upload and nothing else:

| hook | when | what it sends |
| --- | --- | --- |
| `session-end` | a session closes | the transcript, to your own notes |
| `pre-compact` | before a compaction | the transcript so far, so a long chat is not lost |
| `session-catchup` | a session starts | any earlier transcript whose upload dropped |

The base plugin's `session-start` hook is deliberately NOT duplicated here. That
one injects your notes into a chat and uploads nothing, so it belongs with the
base plugin, and installing it twice would run it twice.

## What gets captured, and who sees it

Everything lands in your own space. Nobody else reads it unless you share it,
and standing access you have granted is named in the first line of every chat.

To keep a single chat out: say "don't save this" in the chat. For anything
genuinely confidential, use a chat with the brain disconnected so it never
reaches the server at all.
