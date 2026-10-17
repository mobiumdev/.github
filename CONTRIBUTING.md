# Contributing

Thanks for looking. Every mobiumdev repository follows the
[code of conduct](CODE_OF_CONDUCT.md). This file covers the repositories that
have no contributing guide of their own.

## Before you start

- **A bug or a request:** open an issue with the form in that repository.
  For a problem with the tool itself, use
  [mobium's issues](https://github.com/mobiumdev/mobium/issues/new/choose).
- **A vulnerability:** never in an issue; see [SECURITY.md](SECURITY.md).
- **A larger change:** open an issue first, so the approach can be agreed
  before the work.

## What every change needs

- **Verified, not reasoned about.** Say how you checked it: the device and its
  system, and what you ran. A change to how something behaves on a device is
  checked on a device or a simulator, never only in a test fixture.
- **American spelling**, in code, comments, docs and commit messages.
- **No private data.** Screenshots and logs from a real device carry names,
  accounts and locations. Take them out before they go into an issue, a pull
  request or a commit.
- **One change per pull request**, based on `main`. Pull requests are squash
  merged, and the branch is deleted when it merges, so do not base one pull
  request on another's branch.

## mobium

[mobium's own CONTRIBUTING.md](https://github.com/mobiumdev/mobium/blob/main/CONTRIBUTING.md)
has the build, the tests and the project's rules. `make ci` is what its CI
runs.

## mobium-app

MobiumApp is an app under test: each screen is a positive control for
something that can go wrong when a tool drives an app.

- **A new screen names what it is a control for**, and the Mobium check in
  `docs/checks/` that drives it. A screen no check drives proves nothing.
- **Test IDs are an interface.** Mobium's checks find elements by them;
  renaming one breaks a check in the other repository. Add, do not rename.
- **There is no CI.** A change is checked by building it and running the
  checks that drive the screens it touches, on Android and iOS, and saying
  which ran on which device.
- Keep each WebView inspectable (`webviewDebuggingEnabled`). Without it an iOS
  WebView is invisible to any debugger, which is the reason the app exists.

## morpho-market

Morpho Market is an app under test too: a store's checkout, written natively
twice, in SwiftUI and Jetpack Compose, with a switch of deliberate bugs.

- **Both apps change together.** They share ids, text and prices, so one
  test file drives both. A change to one platform's screens is made on the
  other in the same pull request.
- **Prices follow the spec.** `spec/pricing.py` is the reference and
  `spec/pricing-cases.json` the shared cases; both apps' unit tests run them.
- **A new bug needs a test that catches it.** The bug matrix
  (`tests/matrix.sh`, scored by `tests/score.py`) must still catch every bug,
  and with none on, every test must pass.
- **There is no CI.** Say which checks ran on which device.

## mobium-evals and mobium-rag

Two evaluations, one of an agent driving Mobium and one of answers drawn
from its docs. Both follow one rule: a measurement is not a result until it
has been shown it can come back the other way.

- **Every grader and judge passes its controls first.** A new task needs a
  reference driver that passes and null and wrong drivers that fail
  (`mobium-evals controls`); a new metric or judge needs a positive and a
  negative control.
- **A number comes with what it ran on.** Say the Mobium commit, the model
  and its setting, the device, and the seed, as each run's record does.
- **The agent never sees the answer key.** mobium-evals gives the agent
  `mobium mcp` and nothing else; keep Mobium's checks, its defect log and
  MobiumApp's source out of its reach.
- **The golden set is reviewed by a person.** A question goes into
  mobium-rag's `data/golden.jsonl` only through `review/apply.py`, and a new
  corpus pin is reviewed like code.
- `uv run pytest -q` runs each one's tests; mobium-rag's CI also runs the
  retrieval gate (`make ci`). mobium-evals has no CI: runs need an
  emulator and a model, so say which ran.

## mobium-roundtrip

Round-trip verification of Mobium's traces and of tests written from them.
The device decides; no model grades anything.

- **Every mutant is checked against a control.** A suite is scored by the
  cells it loses or adds against a run with no mutant, and with no mutant
  every test must pass, or no other row means anything.
- **A generated test changes only through its generator.** Edit
  `tools/gen.py` or the agent's prompt and generate again, rather than
  editing a generated file. The dialog rules in
  `generated/branch/dialogs-rule.test.json` are the one file written by hand.
- **Keep the agent away from the answer key**: the prompt gives it the
  traces and the format reference, never the original tests.
- **Evidence stays small.** Commit a probe's `RESULTS.md`, JUnit results and
  scores; traces, screenshots and reports are made again by `tools/run.sh`.
- **There is no CI.** Say which device and which Mobium commit a run used.

## mobiumdev.github.io

The documentation site is mostly generated; see its
[README](https://github.com/mobiumdev/mobiumdev.github.io/blob/main/README.md).

- **Never edit the reference by hand.** `docs/reference/` is generated from
  the commands' own help, the MCP schema and the clients' doc comments. Fix the
  source in mobium instead.
- **Guides and the quick start are copied from mobium's `docs/`.** Change them
  there.
- **Every example is checked** against its surface: `npm run check` with a
  checkout of mobium. A new tool needs an example, or the build fails.
- Pushing to `main` deploys the site.

## License

By contributing, you agree that your contribution is licensed under the
license of the repository it goes into: the Apache License 2.0 for mobium,
mobium-app, morpho-market, mobium-evals, mobium-rag and mobium-roundtrip,
and MIT for the documentation site.
