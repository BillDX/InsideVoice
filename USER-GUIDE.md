# Inside Voice User Guide

## Core Function: 

**Hold Right ⌥ (Option), speak, release.**  The transcript appears wherever
your cursor is — any app, any text field. That's the whole product; the rest
of this guide is refinement.

While you hold the key, a small floating panel shows a live level meter
("Listening — release ⌥ to insert"), then a spinner ("Transcribing…"), then
disappears as the text lands. On an M-series Mac the wait after release is
under a second for typical utterances.

**For long dictations, latch it:** while holding Right ⌥, tap **Right ⌘**
(right next to it) — the recording locks and you can let go of everything.
Speak as long as you like; the HUD stays on screen with a lock indicator
the whole time so you always know the mic is live. Tap Right ⌥ once to
finish and insert. The latch chord starts from a held key, so it never
looks like a double-tap to other apps' hotkey gestures.

![The HUD while listening](docs/images/hud-listening.png)
![The HUD while latched](docs/images/hud-locked.png)

Some details you'll discover anyway, made explicit:

- A **quick tap does nothing** — presses shorter than about a third of a
  second are ignored, so using Right ⌥ as a normal modifier key stays safe.
  The key still works as Option for other apps even while Inside Voice
  watches it.
- **Silence is trimmed** from both ends of your recording, and an all-silent
  clip is discarded without transcribing. Long pauses *inside* a dictation
  are fine too — a voice-activity model finds the speech and whisper
  transcribes only that, so you can stop and think mid-thought for minutes
  without derailing the transcript.
- If you held the key but no words came through, a small **"Didn't catch
  that"** notice appears — so you know it heard nothing rather than
  wondering whether it failed silently.
- Punctuation is **inferred from your speech**, not spoken commands — say the
  sentence naturally and whisper punctuates it. (Spoken "new line" /
  "scratch that" commands are on the roadmap, not in the app yet.)

## The menu bar icon

The waveform circle in your menu bar is the whole interface. Its shape
reflects state: hourglass while the model loads (a few seconds after
launch), filled dot while recording, ellipsis while transcribing,
exclamation mark if something's wrong.

The menu keeps the everyday things up top — Copy Last Transcription,
Theme, Setup Assistant, Launch at Login — and tucks everything else under
**Advanced ▸**. You can ignore Advanced entirely; the defaults are tuned
to just work. The sections below cover all of it anyway.

**Copy Last Transcription** — your most recent transcript, kept only in
memory. Use it when you dictated into the wrong window. Quitting the app
forgets it.

**Insert Text By** — three delivery methods:

| Mode | How it works | Choose it when |
|---|---|---|
| **Paste** (default) | Copies to clipboard, sends ⌘V, restores your old clipboard ~½ s later | Almost always — fastest and most reliable |
| **Type it out** | Synthesizes real keystrokes | Apps that block pasting or handle keys specially (some terminals, remote desktops, password-adjacent fields) |
| **Clipboard only** | Just puts the text on the clipboard | You want to review before pasting, or the target is on another machine |

**Language** — Auto-detect works well; pinning your language shaves a little
latency and removes occasional wrong-language guesses. Non-English dictation
is fully supported (whisper covers ~99 languages).

**Engine** — which speech model listens to you:

- **Whisper** — ~99 languages, and the only engine the Vocabulary
  prompt can steer, which makes it the accuracy pick for jargon-heavy
  dictation.
- **Parakeet** — the accuracy pick for *plain* English (it beats whisper on
  standard English benchmarks), several times faster, and immune to
  whisper's invent-text-on-silence quirk. European languages only. A
  separate 669 MB download (Setup Assistant → "Parakeet engine");
  substitution rules still apply, so your forced spellings survive.
- **Auto** (default) — quality-first routing: Whisper whenever your vocabulary is
  active (its jargon edge) or the language needs it (Japanese, Chinese,
  Korean, Hindi); Parakeet for vocabulary-off plain English, where it's
  the stronger model. The menu status line shows which engine Auto is
  currently using and why.

The Setup Assistant reads your Mac's chip and RAM and shows it on the
first line. Parakeet is the recommended first engine everywhere (faster,
more accurate on plain English, a third of the download); Whisper is the
optional add-on for other languages and vocabulary biasing, and on 8 GB
Macs the assistant notes that its ~1.7 GB resident footprint is a squeeze.

**Vocabulary** — how you teach it your world:

- **Personal List** is a plain text file (one term per line). *Edit Personal
  List…* opens it in your editor; changes apply to your very next utterance,
  no restart. Put project names, coworkers, brand spellings, and acronyms
  here — anything it keeps mangling.
- **Coder** is a built-in preset (~80 dev/web/macOS/AI terms), off by
  default — turn it on if you dictate a lot of developer jargon.

The vocabulary *biases* recognition rather than forcing it — it fixes most
spellings and casings ("SwiftPM", "ggml"), but isn't a guarantee. For the
stubborn cases there's **Edit Substitution Rules…**: deterministic
find→replace applied to every transcript. One rule per line
(`questline -> Questline`, `eye oh ess -> iOS`); matching is
case-insensitive and whole-word, multi-word phrases welcome, and the
replacement is inserted exactly as written. Rules apply from your very
next utterance.

**Higher Accuracy (Whisper Beam Search)** — on by default; Whisper only
(Parakeet's greedy decode is already its benchmark mode, and it has no beam
option). On Apple Silicon the speed cost is essentially zero, so leave it
on; the toggle exists for older or busy machines.

**Theme** — how the dictation HUD looks and talks. Purely cosmetic,
switchable anytime, applies to your next utterance. Nine to choose from:

| Theme | |
|---|---|
| **Modern** (default) — native translucent panel, green mic, accent-colored meter | ![](docs/images/themes/modern.png) |
| **Green Phosphor** — glowing CRT terminal, scanlines, blinking cursor | ![](docs/images/themes/phosphor.png) |
| **Red Eye** — a red lens that swells as you speak and addresses you by name; unhurried breathing while it thinks | ![](docs/images/themes/hal.png) |
| **Starship** — bridge-computer panel, ticking readouts, a blinking WORKING | ![](docs/images/themes/lcars.png) |
| **RetroComp '82** — royal blue 8-bit screen, chunky pixel meter, raster-bar loading border | ![](docs/images/themes/c64.png) |
| **Oscilloscope** — graticule screen, glowing trace riding your voice; Lissajous figure while analyzing | ![](docs/images/themes/scope.png) |
| **Punch Card** — your voice punches an 80-column card; the reader sweeps and stamps it READING | ![](docs/images/themes/punchcard.png) |
| **Groovy** — 1968 flower power: doors swing open with flowers springing out, a daisy meter, go-go headlines | ![](docs/images/themes/groovy.png) |
| **Happy Cloud** — 8-bit sprite: a chunky cloud with big eyes and an open mouth on its belly pours a rainbow straight down; it bends through a pixel elbow and runs off as a stepped river — the river is the meter. Blinks, splashes, smiles while digesting | ![](docs/images/themes/cloud.png) |

**Play Sound on Insert** — a soft pop when text lands. Off by default.

**Permissions** — live ✓/✗ for the three macOS grants; click any row to open
the right System Settings pane. Sits at the top level only while something
needs doing; once all three are granted it tucks into Advanced.

**Setup Assistant…** — reopens the first-run window (engine downloads, the
permission grants with step-by-step guidance, start-at-login, a keyboard
check that confirms you're pressing the *right* Option key, and a test
field). Harmless to open anytime.

![The Setup Assistant](docs/images/setup-assistant.png)

**Launch at Login** — what it says.

## Privacy model, in plain language

- Audio is captured to memory, transcribed on this Mac, and gone. It never
  touches disk and never leaves the machine. There is no network use at
  runtime at all — the only network operation the app ever performs is the
  one-time model download you approve in setup.
- Transcripts are never written anywhere by the app. The single exception
  you control: the last transcript is held in memory for the *Copy Last
  Transcription* menu item, and vanishes on quit.
- What *is* stored on disk: the speech model(s) you downloaded, your
  vocabulary and substitution text files, and your settings
  (`~/Library/Application Support/Inside Voice/`, plus standard macOS
  preferences). No audio, no history, no logs.

## Troubleshooting

**Hotkey only works when Inside Voice is frontmost** — the classic. Input
Monitoring isn't granted: menu → Permissions — action needed → Input
Monitoring (or Setup Assistant…). The app picks the grant up within a few
seconds; no relaunch needed.

**HUD appears and transcribes, but no text lands** — Accessibility isn't
granted (needed to deliver the text). Same drill: Permissions or the Setup
Assistant.

**HUD never appears at all** — check Microphone in the Setup Assistant, and
confirm the engine finished loading (the menu's first line reads
"Engine: …" rather than "Loading speech engine…").

**Text lands in the wrong place** — the text goes to whatever owns keyboard
focus at the moment you release. Click into the target field first, then
dictate. If it already happened: *Copy Last Transcription*.

**It typed over my clipboard** — paste mode restores your clipboard about
half a second after inserting. If you copy something new *within* that
window it can be clobbered — rare in practice; use Clipboard-only mode if it
bites you.

**A word keeps coming out wrong** — add it to Advanced → Vocabulary → Edit
Personal List…, dictate again, and it should improve immediately (that
prompt only steers Whisper; with Auto, an active list routes you to Whisper
automatically). If it *still* comes out wrong, make it a substitution rule
(Vocabulary → Edit Substitution Rules…) — those apply to both engines,
unconditionally.

**"No speech engine downloaded" / load errors** — menu → Setup Assistant…
and use the Download button (progress bar, checksum-verified, pausable).

**It took a while after I let go** — a long dictation on Whisper decodes at
roughly 30× realtime; Parakeet is several times faster. Advanced → Engine →
Parakeet (or Auto with vocabulary off) if speed matters more than jargon.

## Updating

For now, updates arrive as a new DMG: open it, drag Inside Voice to
Applications, and click Replace. Everything important survives the swap —

- your three permission grants (they're tied to the app's signing identity,
  not the individual build),
- the downloaded models, your vocabulary and substitution lists, and all
  settings (they live in `~/Library/Application Support/Inside Voice/`,
  outside the app).

Quit the running copy first (menu → Quit Inside Voice), replace, relaunch.
If it was set to launch at login, that carries over too.

**Coming from LocalWhisper (1.2.0 or earlier):** the 1.3.0 rename keeps your
models, lists, and settings — they're moved to the new locations on first
launch — but macOS treats the renamed app as new: re-grant the three
permissions (the Setup Assistant opens to walk you through it), re-enable
Launch at Login, and delete the old LocalWhisper.app.

In-app automatic updates ("a new version is available…") are planned for
the notarized public release.

## Requirements, briefly

Apple Silicon Mac. RAM while running: ~0.8 GB with Parakeet, ~1.7 GB with
Whisper. Disk: 669 MB (Parakeet) and/or 1.6 GB (Whisper). No internet
needed after setup.
