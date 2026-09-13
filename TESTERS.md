# Testing LocalWhisper (pre-release builds)

Thanks for kicking the tires. What you're testing: **hold Right ⌥ anywhere,
speak, release** — the transcript lands in whatever app has focus. Everything
runs on-device: no network at runtime, audio never touches disk, transcripts
are never logged.

## Requirements

- **Apple Silicon** Mac (M1 or later; built on an M3)
- **macOS 26 recommended.** 14/15 may work but is untested — if the app
  won't launch there, that's a useful bug report in itself.
- ~0.8 GB free RAM while running with the recommended Parakeet engine
  (~1.7 GB if you add Whisper); 669 MB disk for the one-time Parakeet
  download, 1.6 GB more for optional Whisper (needs a network that doesn't
  TLS-inspect huggingface.co — some corporate networks do)

## Install

Grab the DMG from the
[Releases page](https://github.com/BillDX/LocalWhisper/releases/latest) —
it's small; the speech model downloads on first launch.

These builds are signed with a local certificate, **not** an Apple
Developer ID, so Gatekeeper will object. Two ways around it:

**Option A — fetch by terminal (no warnings at all):** quarantine is applied
by the app that downloads a file; `curl` doesn't apply it, so Gatekeeper
never gets involved:

```bash
curl -L -o ~/Downloads/LocalWhisper.dmg https://github.com/BillDX/LocalWhisper/releases/latest/download/LocalWhisper.dmg
```

Open the DMG, drag LocalWhisper to Applications, launch normally.

**Option B — if it arrived via browser / AirDrop / Messages:** after
dragging to Applications, clear the quarantine flag:

```bash
xattr -dr com.apple.quarantine /Applications/LocalWhisper.app
```

(Or: attempt to open it once, then System Settings → Privacy & Security →
"Open Anyway".)

There's nothing to build or sign on your side — the download is already
signed. A `.sha256` file sits next to each DMG if you want to verify it.

## First launch

A setup window walks you through everything:

1. **Speech engine** — click Download (Parakeet, 669 MB, checksum-verified).
   Whisper is an optional second download for non-European languages
2. **Microphone** / **Input Monitoring** / **Accessibility** — three separate
   macOS grants; each row tells you exactly what to click in the Settings
   pane it opens
3. **Start at login** — recommended, one click
4. **Keyboard check** — press your right-hand ⌥ and the diagram lights up
   green (it'll correct you if you hit the left one)

The "Try it" field at the bottom stays disabled until everything above is
green — that's your signal you're ready.

The window updates live as grants land; reopen it anytime from the menu-bar
waveform icon → **Setup Assistant…**. Your grants will survive app updates —
no re-granting on new builds.

**The classic gotcha is Input Monitoring**: if the hotkey only works while
LocalWhisper's own window is focused, that grant is missing.

Day-to-day usage, menu reference, and troubleshooting live in the
[User Guide](USER-GUIDE.md).

## What to try

- Dictate into different apps: browser, terminal, Slack, a code editor
- Long utterances vs. quick phrases; a quick tap (should do nothing); a
  hold with no speech (should say "Didn't catch that")
- **Latch mode**: hold Right ⌥, tap Right ⌘, let go of both, talk for a
  while with pauses, tap Right ⌥ to finish — text should land at the cursor
- Jargon and proper nouns — then add your own under Advanced → Vocabulary →
  Edit Personal List… and see if recognition improves
- Engines (Advanced → Engine): Auto vs Parakeet vs Whisper — note speed and
  accuracy differences on your own voice
- The insertion modes (Advanced → Insert Text By): paste / type / clipboard
- Non-English speech (Advanced → Language)
- Themes (menu → Theme) — do any misbehave or hide the "locked" state?
- Clipboard contents before/after dictating (paste mode should restore
  yours within ~half a second)

## Reporting

Note your Mac model, macOS version, and what app had focus. The app logs
nothing by design, so a description of what you said vs. what appeared is
the whole bug report. File an issue at
[github.com/BillDX/LocalWhisper/issues](https://github.com/BillDX/LocalWhisper/issues),
or send reports to Bill directly.

## Uninstall

```bash
rm -rf /Applications/LocalWhisper.app "$HOME/Library/Application Support/LocalWhisper"
```
