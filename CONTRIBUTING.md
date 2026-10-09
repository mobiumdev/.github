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
license of the repository it goes into: MIT for mobium, mobium-app and the
documentation site.
