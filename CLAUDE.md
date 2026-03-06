# CLAUDE.md

## Tooling

- Install: `make install PREFIX=~/.local` (no build step)
- No tests, linter, or CI configured

## Non-Obvious Rules

- Scripts have no file extensions: widgets (`logibar-keyboard`, `logibar-mouse`, `logibar-headset`) are Bash, daemons (`logibar-hidpp-monitor`, `logibar-headset-monitor`) and `tools/` are Python
- The three widget scripts are near-identical — only `ICON`, `ICON_CHARGING`, `TOOLTIP`, and `STATE_FILE` differ. Keep them in sync when changing shared logic
- Widget output uses Pango markup inside JSON (`<span>` tags) — Waybar renders it
- Daemons notify Waybar via `pkill -RTMIN+N waybar` — signal numbers are hardcoded per device and must match waybar config
- State files are 3 lines: `battery\nconnected\ncharging` in `$XDG_RUNTIME_DIR/logibar/`
- Python dependency is `hid` (`import hid`), packaged as `python-hid` on Arch
