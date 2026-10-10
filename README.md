# OpenThumb for iPhone

**Your coding agent, operating your real iPhone over USB.** Describe a task in
plain language; the agent opens apps, reads the screen, taps, scrolls, types and
checks the result — on the phone in your hand, not a simulator.

Works with **Claude Code**, **Codex**, and any MCP client. No jailbreak, no
Appium server, no cloud: a local MCP server talks to
[WebDriverAgent](https://github.com/appium/WebDriverAgent) on the phone through
a loopback-only USB forward.

![The agent operating a real iPhone with a live screen preview](assets/iphone-use-demo.png)

Part of the [OpenThumb](https://github.com/neulketing/openthumb) family:
OpenThumb runs an autonomous agent *on* an Android phone; this drives an iPhone
*from* your Mac, because iOS does not let an app operate other apps.

## This is a fork

Nearly all of the code was written by ZHONG XIN in
[zhongerxin/iPhone-use](https://github.com/zhongerxin/iPhone-use) (MIT). This
fork changes three things:

- **Claude Code support** — installs as a Claude Code plugin, alongside the
  original Codex plugin.
- **No telemetry** — upstream sends anonymous usage events to its own PostHog
  project by default. Here the project token is removed, so nothing is sent.
  See [ANALYTICS.md](ANALYTICS.md).
- **English-first docs.** The original Chinese guide is
  [README.zh-CN.md](README.zh-CN.md); the full upstream English guide is
  [README.en.md](README.en.md).

Tool names (`pua_*`), the plugin id (`iphone-use`) and the state directory are
kept as upstream so fixes merge both ways.

## Requirements

- macOS with full Xcode (Command Line Tools alone are not enough)
- An Apple account usable as a signing team in Xcode (a free personal team works; its signature lasts 7 days)
- A real iPhone on USB, trusted, with Developer Mode on
- Python 3.9+, Node.js 20.19+ / 22.12+ / 24+

WebDriverAgent is built and signed **with your own Apple team, on your own
Mac**. That is how iOS automation works; nothing here is installed from the App
Store.

## Install

### Claude Code

```text
/plugin marketplace add neulketing/openthumb-iphone
/plugin install iphone-use@openthumb
```

Then, in a new chat:

> Use iphone-use-setup to configure my USB-connected iPhone, install and start WDA, verify READY, then show the phone screen.

### Codex

```sh
git clone https://github.com/neulketing/openthumb-iphone.git
cd openthumb-iphone
sh scripts/install.sh
```

### Any other MCP client

Register a stdio server: `python3 /path/to/openthumb-iphone/server/iphone_use.py`.

## What it can do

| | |
| --- | --- |
| App navigation | Open an app, reach search, detail, settings or draft screens |
| Reading | Compact accessibility tree, text, positions, real screenshots |
| Gestures | Tap by element or coordinate, swipe, drag, bounded waits |
| Text input | Full Unicode, long text in resumable chunks; typing never submits by itself |
| Lists | Bounded scroll-and-find, de-duplicated collection with coverage report |
| Recovery | Falls back to a screenshot when an element is covered or the tree is incomplete |
| Live screen | Phone preview with visible tap and drag hints (in clients that render MCP app widgets) |

Passwords, verification codes and Face ID stay with you: the agent pauses and
hands over. Full tool list and behaviour: [README.en.md](README.en.md).

## Develop

```sh
sh scripts/check.sh
```

## License

MIT — see [LICENSE](LICENSE) and [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
iPhone is a trademark of Apple Inc. This project is not affiliated with Apple.
