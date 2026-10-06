# @alvaroak/pi-omp-ponytail

Lazy senior dev mode with **intensity levels**, one source file (`index.ts`) running on both **omp** ([@oh-my-pi/pi-coding-agent](https://github.com/oh-my-pi/pi)) and **pi** ([@earendil-works/pi-coding-agent](https://github.com/earendil-works/pi)).

The ruleset comes from [@dietrichgebert/ponytail](https://github.com/dietrichgebert/ponytail) (MIT) — a skill the model reads when it notices the task matches. This extension turns that document into an **enforced runtime state**: the ruleset is injected into the system prompt every turn, so it cannot drift away mid-session.

- **Intensity levels** — the original is one static ruleset; this adds `lite`, `full`, and `ultra` tiers.
- **Persistent choice** — an explicit mode choice is recorded in the session (`ponytail-mode` entries, `ponytail:changed` events) and kept for the events feed; every session starts at `full`.
- **Reliable off-switch** — "stop ponytail" / "normal mode" as a standalone message is intercepted directly.
- **Ecosystem surface** — publishes `ponytail:changed` over `pi.events` so status footers can show the current mode.

## Usage

```bash
/ponytail            # picker (off / lite / full / ultra)
/ponytail lite       # gentle nudge
/ponytail full       # the standard ruleset (default)
/ponytail ultra      # aggressively minimal
/ponytail off        # off
```

## Host differences (all in `index.ts`)

| | omp | pi |
|---|---|---|
| Detect | `"logger" in pi` | otherwise |
| `before_agent_start` | `systemPrompt: string[]` | `systemPrompt: string` |
| Picker border | `theme.getThinkingBorderColor(pi.getThinkingLevel() ?? "off")` | `theme.fg("border", s)` |
| TUI helpers | `@oh-my-pi/pi-tui` | `@earendil-works/pi-tui` (dynamic import on open) |

## Install

- omp: symlink into `~/.omp/agent/extensions/pi-omp-ponytail`
- pi: `pi install git:github.com/Alvaroak/pi-omp-ponytail@v0.3.0` (settings.json git package, pinned tag)

## Credits

Ruleset adapted from [@dietrichgebert/ponytail](https://github.com/dietrichgebert/ponytail) (MIT).

## License

MIT
