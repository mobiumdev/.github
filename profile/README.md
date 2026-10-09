## Mobium

**Mobile app automation for AI agents and humans.** One Go binary drives
Android emulators and phones, iOS simulators and iPhones, and Fire TV, through
a CLI, an MCP server and clients for Go, Python, JavaScript, Java and .NET.

An agent reads the screen with `map`, acts on a ref, and maps again to see what
changed: the loop [Vibium](https://github.com/VibiumDev/vibium) uses for
browsers, carried over to devices.

| Repository | What it is |
| --- | --- |
| [mobium](https://github.com/mobiumdev/mobium) | The tool: CLI, MCP server, test runner and five clients |
| [mobium-app](https://github.com/mobiumdev/mobium-app) | MobiumApp, the app Mobium's checks drive; every screen is a control for something that can go wrong |
| [mobiumdev.github.io](https://github.com/mobiumdev/mobiumdev.github.io) | The documentation site, [mobiumdev.github.io](https://mobiumdev.github.io/) |

Mobium is open source under the MIT license and has no tagged release yet;
install it with `go install github.com/mobiumdev/mobium/cmd/mobium@latest`.

[Documentation](https://mobiumdev.github.io/) ·
[Contributing](https://github.com/mobiumdev/.github/blob/main/CONTRIBUTING.md) ·
[Code of conduct](https://github.com/mobiumdev/.github/blob/main/CODE_OF_CONDUCT.md) ·
[Security](https://github.com/mobiumdev/mobium/blob/main/SECURITY.md)
