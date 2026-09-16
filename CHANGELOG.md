# Changelog

## 1.4.0 — 2026-09-16

- **First notarized release.** Signed with a Developer ID under the hardened
  runtime, notarized by Apple and stapled: the DMG opens with no Gatekeeper
  warning, and the Homebrew cask no longer needs `--no-quarantine`. The
  signing identity changed with this, so macOS asks for Microphone, Input
  Monitoring, and Accessibility once more after updating; the Setup
  Assistant opens to walk through it, and Launch at Login needs one click.
- New theme: **Glitter Text** — early-2000s glitter graphics. Bubbly
  sticker-edged letters filled with shimmering pink, gold, and lilac and
  twinkling flecks, a holographic shine sweep, a pastel sky of drifting
  sparkles. Headlines rotate (SPARKLE ON, SO SHINY, USE YOUR INSIDE
  VOICE); LOCKED IN gets a glittery padlock; LOADING
  gets three chasing sparkles; the meter is a glitter bar whose flecks
  thicken with your voice. When the text lands, a glitter bomb of hearts,
  stars, and dots bursts from the headline and the panel fades out.
- Themes can now play a send-off after the transcript is inserted
  (`outroDuration` / `beginOutro` on `ThemeHUDView`); the HUD stays up for
  that long, and a new utterance cancels it. `--snapshot-hud … --state
  outro` renders the moment.
- Themes trimmed: **Starship, Punch Card, and Happy Cloud removed** while
  the theme set is revised before the first notarized release. Anyone who
  had one selected falls back to Modern. Six themes remain: Modern, Green
  Phosphor, Red Eye, RetroComp '82, Oscilloscope, Groovy.
- Release pipeline: Developer ID signing with hardened runtime and a secure
  timestamp, notarization and stapling of both the app and the DMG
  (`scripts/notarize.sh`, wired into `publish-release.sh`). The first
  notarized build changes the app's signing identity, so macOS will ask
  for Microphone, Input Monitoring, and Accessibility once more; the Setup
  Assistant walks through it.

## 1.3.0 — 2026-09-13

- **Renamed to Inside Voice** (was LocalWhisper). Models, vocabulary,
  substitution rules, and settings move to the new locations automatically
  on first launch (`~/Library/Application Support/Inside Voice/`,
  defaults domain `com.thinkiac.InsideVoice`). The bundle identifier
  changed, so macOS sees a new app: re-grant Microphone, Input Monitoring,
  and Accessibility once (the Setup Assistant opens to walk you through it)
  and re-enable Launch at Login. Delete the old LocalWhisper.app. The retro
  themes print the new name; developer env overrides are now
  `INSIDEVOICE_MODEL` / `INSIDEVOICE_PARAKEET_MODEL`.
- Homebrew tap: `brew trust BillDX/tap && brew tap BillDX/tap && brew install --cask inside-voice`.
- Public repo moved to github.com/BillDX/InsideVoice; old links redirect.

## 1.2.0 — 2026-09-13

- First public download release: DMG and docs at
  [github.com/BillDX/LocalWhisper](https://github.com/BillDX/LocalWhisper).
  The source repository stays private for now; LICENSING.md states the terms
  it will publish under.
- **Licensing:** LocalWhisper is now dual-licensed `EUPL-1.2 OR
  GPL-3.0-or-later` (was GPL-3.0 only; purely additive — every existing
  right is unchanged). New LICENSING.md (dual grant, commercial licensing,
  trademark policy) and CONTRIBUTING.md (contributor license agreement,
  `Signed-off-by` sign-off). The license texts now ship inside the app
  bundle next to THIRD-PARTY-LICENSES.md.
- New theme: **Happy Cloud** — an 8-bit sprite: chunky 5-pt pixels, thick
  outline, 2×2 eyes, an open mouth on the belly. A rainbow pours straight
  down out of the mouth, bends through a quarter-arc pixel elbow, and runs
  off left as a stepped river that is the level meter.
  Blinks, splash droplets that scale with volume, pixel rainbow arch and a
  smiling "digesting" face while transcribing, two-line 3×5 pixel-font
  headlines ("SHARING / THE MAGIC").
- Think Pink and Rainbow Unicorn themes removed. Anyone who had either
  selected falls back to Modern. Nine themes total.

## 1.1.0 — 2026-09-09

**Accuracy / engines**
- Parakeet TDT 0.6B v3 engine (libparakeet): faster, best plain-English
  accuracy, immune to silence hallucination. Engine menu: Auto (default),
  Parakeet, Whisper. Auto is quality-first: Whisper when vocabulary is
  active or the language needs it (ja/zh/ko/hi), Parakeet otherwise.
- Silero VAD for whisper: long mid-dictation pauses no longer trigger
  repetition loops that swallow later speech; silence hallucination gone at
  the source. Watchdog abort (2× clip length) so a decode can never wedge.
- Substitution rules: deterministic find→replace on every transcript, both
  engines (`substitutions.txt`).
- Parakeet-only installs run without whisper.

**Dictation**
- Chord-latch: hold Right ⌥, tap Right ⌘ to lock recording; tap Right ⌥ to
  finish. Never looks like a double-tap to other apps.
- Insertion waits for physical modifiers to clear (fixes ⌥⌘V misfires).
- "Didn't catch that — try again" notice when a hold produced no words.
- Pressing the key while a previous utterance is transcribing shows the HUD
  instead of being ignored.

**Setup & menu**
- Setup Assistant: step-by-step permission guidance, test field gated until
  everything is green, keyboard diagram with wrong-Option-key detection,
  start-at-login row, Parakeet-first download (669 MB) with Whisper optional,
  hardware line (chip + RAM) with a recommendation.
- Simple/Advanced menu split; Permissions promoted to the top level only
  while action is needed. General-audience defaults: engine Auto, Coder
  preset off, templates with commented examples.

**Themes** (new: Groovy, Think Pink, Rainbow Unicorn — ten total)
- Locked-recording state in every theme. Modern's mic is bright green.

**Housekeeping**
- IP pass: themes renamed to original names (Red Eye, Starship,
  RetroComp '82), no baked-in personal names, THIRD-PARTY-LICENSES.md
  shipped in the bundle, VAD/Parakeet licenses verified and attributed.
- `--selftest --engine whisper|parakeet|both`, `--snapshot-hud --theme
  --state`, `--snapshot-onboarding`.

## 1.0.0 — 2026-08-16

- Push-to-talk dictation: hold Right ⌥, speak, release. Listen-only event
  tap, in-memory audio, whisper.cpp large-v3-turbo on Metal, paste /
  type / clipboard insertion with clipboard restore, non-activating HUD,
  menu-bar app.
- Vocabulary prompt (personal list + Coder preset), silence trim, beam
  search.
- Self-contained bundle: vendored libwhisper/libggml/backends/libomp with
  @rpath rewrites; local signing cert for a stable permission identity.
- Onboarding window with in-app SHA-256-verified model download, app
  icon, DMG script, GPL-3.0, USER-GUIDE / TESTERS / FUTURE-FEATURES docs.
- Theme engine with seven themes.
