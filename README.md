# kite-mcp-telegram

[![Go Reference](https://pkg.go.dev/badge/github.com/algo2go/kite-mcp-telegram.svg)](https://pkg.go.dev/github.com/algo2go/kite-mcp-telegram)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Telegram bot integration for the algo2go ecosystem. Provides
mobile-friendly trading via inline-keyboard commands (/buy /sell
/quick /setalert) with confirmation flow, morning briefings (9 AM
IST: alerts + token status), daily P&L summary (3:35 PM IST:
holdings + positions, weekend skip + dedup, HTML formatted),
disclaimer/consent flow, and pluggable command extension via
plugin_commands.

Used by [`Sundeepg98/kite-mcp-server`](https://github.com/Sundeepg98/kite-mcp-server)
as the optional Telegram bot endpoint wired in app/app.go,
app/http.go, app/adapters.go.

## Why a separate module?

Telegram is a foundational mobile-first endpoint primitive
applicable to any algo2go consumer running a trading bot — not
just kite-mcp-server. Hosting as its own module:

- Centralizes the Bot + Handler + Commands + Briefings contracts
- Lets command syntax + keyboard layouts version independently
- Decouples Telegram-specific UI flow from any one runtime

## Stability promise

**v0.x — unstable.** Pin `v0.1.0` deliberately.

## Install

```bash
go get github.com/algo2go/kite-mcp-telegram@v0.1.0
```

## Public API

- `Bot` — Telegram client + dispatch
- `Handler` — message handler routing (auth, portfolio, trading,
  plugin commands)
- Trading commands — /buy, /sell, /quick (1-tap presets), /setalert
- Briefings — morning (9 AM IST) + daily P&L (3:35 PM IST)
  scheduler with weekend skip + dedup
- Disclaimer — consent flow before first trading command
- PluginCommands — extension hook for custom commands
- TradingFuzzTest — fuzz test harness for command parsing

## Dependencies (8 algo2go modules)

- `github.com/algo2go/kite-mcp-alerts` v0.1.0
- `github.com/algo2go/kite-mcp-broker` v0.1.0 (incl. /ticker +
  /zerodha subpkgs)
- `github.com/algo2go/kite-mcp-domain` v0.1.0
- `github.com/algo2go/kite-mcp-instruments` v0.1.0
- `github.com/algo2go/kite-mcp-papertrading` v0.1.0
- `github.com/algo2go/kite-mcp-riskguard` v0.1.0
- `github.com/algo2go/kite-mcp-ticker` v0.1.0
- `github.com/algo2go/kite-mcp-watchlist` v0.1.0
- `github.com/go-telegram-bot-api/telegram-bot-api/v5` v5.5.1
- `github.com/stretchr/testify` v1.10.0

All algo2go deps published; no upstream `replace` directives needed.

## Reference consumer

[`Sundeepg98/kite-mcp-server`](https://github.com/Sundeepg98/kite-mcp-server)
— consumed across 3 .go files: app/app.go, app/http.go,
app/adapters.go (Telegram bot wiring + handler registration).

## License

MIT — see [LICENSE](LICENSE).

## Authors

Original design: [Sundeepg98](https://github.com/Sundeepg98) (Zerodha
Tech). Multi-module promotion (2026-05-10): algo2go contributors.
