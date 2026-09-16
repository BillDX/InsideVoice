# Contributing

Bug reports, feature ideas, and accuracy findings ("it keeps hearing X as
Y") are welcome as GitHub issues. The roadmap and open questions live in
[FUTURE-FEATURES.md](FUTURE-FEATURES.md).

## Code contributions

Pull requests are welcome, with one condition explained in the next
section. For anything beyond a small fix, open an issue first so we can
agree on the approach: the codebase is deliberately small (~3,500 lines of
Swift) and auditable in an afternoon, and that is a feature worth
protecting.

Practical notes:

- Build with `scripts/build.sh` (README → Build from source). Before
  opening a PR, run the self-test, which needs no permissions:
  `"build/Inside Voice.app/Contents/MacOS/InsideVoice" --selftest --engine both`
- New theme: add a `Theme` under `Sources/Inside Voice/Themes/`, register
  it in `Themes.all`, render it with `--snapshot-hud`, and add the PNG to
  `docs/images/themes/` plus a row in the User Guide gallery. Optional:
  override `outroDuration` and `beginOutro()` to play a send-off after the
  text lands (`--snapshot-hud … --state outro` renders it).
- Keep the privacy invariants: no audio to disk, no transcript logging,
  no network at runtime.

## Contributor License Agreement

Inside Voice is dual-licensed (`EUPL-1.2 OR GPL-3.0-or-later`), and the
copyright holder also offers commercial licenses and builds commercial
editions on the same code. That only works if the project holds the
rights to relicense everything it ships. So, by submitting a contribution
(a pull request, patch, or any other material you intend to be included),
you agree to the following:

1. **License grant.** You grant Bill McIntyre, and any person or entity to
   whom the project's copyright is later assigned, a perpetual, worldwide,
   non-exclusive, irrevocable, royalty-free license to reproduce, modify,
   distribute, sublicense, and relicense your contribution and works
   derived from it, under any terms, including proprietary and commercial
   ones. You keep your own copyright and may use your contribution however
   you like elsewhere.
2. **Patent grant.** To the extent you hold patent claims that your
   contribution necessarily infringes, you grant the same parties a
   perpetual, worldwide, non-exclusive, royalty-free patent license for
   the contribution alone and in combination with the project.
3. **You have the right to do this.** The contribution is your original
   work, or you have the necessary rights from your employer or other
   rights-holders, and you will say so if any part of it comes from
   elsewhere or is under another license.
4. **Your contribution stays open.** Whatever else it is licensed under,
   every contribution is also released under the project's public
   licenses (`EUPL-1.2 OR GPL-3.0-or-later`) in the open edition, so
   nothing you contribute can be withdrawn from the community.
5. **No warranty.** You provide the contribution as-is.

Indicate agreement by adding a `Signed-off-by: Your Name <email>` trailer
to each commit (`git commit -s`). The sign-off means you have read and
agree to this agreement. If you contribute on behalf of an employer, have
someone authorized to bind the company confirm that in the pull request.

If you can't agree to these terms, an issue describing the change is still
valuable; someone else can implement it.

## AI-assisted contributions

Much of Inside Voice was written with an AI coding assistant under close
human direction, and AI-assisted contributions are fine. You remain
responsible for what you submit: review it, test it, and make sure it
doesn't reproduce third-party code under an incompatible license.
