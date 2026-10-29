# VG Brain autosave

A separate marketplace holding one plugin, `vg-brain-capture`: VG Brain autosave
for the few people Liam has set up with it (Alex and Joe). Everyone else uses the
VG Brain connector in claude.ai and installs no plugin at all.

## Why this is its own repo

Automatic capture is opt-in. It lives here rather than beside anything everyone
installs, so it does not show up in the plugin list of people who are not meant to
have it. This repo is public; the separation is about avoiding confusion, not
secrecy. The server only accepts uploads from people on its autosave list.

## Install

1. Connect the **VG Brain connector** in claude.ai (Settings → Connectors) if you
   haven't. That is where the brain tools (search, save, share) come from.
2. **Uninstall the old `vg-brain` plugin** (vg-brain-universal), if you have it.
   Its brain tools would show up twice, and its own hooks would upload twice.
3. In the Claude Code app: **Customize → Plugins → add marketplace**

   ```
   https://github.com/liamsands-arch/vg-brain-capture
   ```

   Then install `vg-brain-capture` (or update it to 0.40.0) and restart the app.
   The first time, it opens a browser to sign in to vg-brain.com with your
   Voyageur Google account.

## What it does

| piece | when | what it does |
| --- | --- | --- |
| `session-start` hook | a session starts | loads your brain context into the session |
| `session-catchup` hook | a session starts | re-sends any earlier transcript whose upload dropped |
| `pre-compact` hook | before a compaction | uploads the transcript so far, so a long chat is not lost |
| `session-end` hook | a session closes | uploads the transcript, to your own notes |
| VG Assistant | always | the plain-English output style |
| `vg-brain-autosave` connection | always | sign-in only; offers no tools |

The connection to `https://vg-brain.com/autosave/mcp` exists only so the hooks
have a signed-in token to upload with. It lists no tools, so Claude sees the brain
tools once, from the connector.

## What gets captured, and who sees it

Everything lands in your own space. Nobody else reads it unless you share it, and
standing access you have granted is named in the first line of every chat.

To keep a single chat out: say "don't save this" in the chat. For anything
genuinely confidential, use a chat without this plugin so it never reaches the
server at all.
