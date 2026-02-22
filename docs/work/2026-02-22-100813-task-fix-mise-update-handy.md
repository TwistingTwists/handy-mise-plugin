# Fix mise update for Handy plugin

## Problem
- `mise up handy` says "up to date" because version pinned to `0.7.1`
- Duplicate `github:cjpais/Handy` entry in config (broken — can't extract .deb)
- Install script doesn't symlink .desktop file for rofi
- Handy binary wouldn't launch — missing `libgtk-layer-shell0` system dep

## Bugs Fixed
1. **list-all descending order** — added `sort -V` so mise resolves `latest` correctly
2. **install find exclusion** — `! -path "*/bin/handy"` excluded `usr/bin/handy`; replaced with direct path
3. **Config pinned** — `handy = "0.7.1"` → `handy = "latest"`
4. **Missing desktop entry** — install now copies `.desktop` + icon to `~/.local/share/applications/`
5. **Missing system lib** — installed `libgtk-layer-shell0`

## Tasks
- [x] Diagnose root cause
- [x] Remove broken `github:cjpais/Handy` entry + installed files
- [x] Change `handy = "0.7.1"` → `handy = "latest"`
- [x] Update install script to symlink .desktop to ~/.local/share/applications/
- [x] Kill old handy, test install → v0.7.7
- [x] Commit & push plugin changes (4eb0539)
- [x] Revert plugin source back to github URL
- [x] Install libgtk-layer-shell0 system dep
- [x] Verify handy launches successfully
