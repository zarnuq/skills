# Repository Guidelines

## Project Structure & Module Organization

This repository packages a machine-specific Wayland desktop-control skill:

- `ydotool/SKILL.md`: skill metadata, input examples, and operational safeguards.
- `ydotool/scripts/inspect_desktop.py`: Python diagnostics for ydotool connectivity and Reach state (read-only).
- `ydotool/scripts/ui.py`: AT-SPI widget locator and ydotool actor; run with `/usr/bin/python3` (needs system `gi`).
- `ydotool/references/scripting.md`: key codes, focus changes, closing things, holds, typing, timing.
- `ydotool/references/atspi.md`: `ui.py` usage, window origins, LibreOffice and Obsidian locating notes.
- `ydotool/examples/`: runnable real-input tests (`calc-smoke.sh`, `writer-format.sh`) and shared `lib.sh`.
- `ydotool/references/desktop.md`: local configuration sources, shortcuts, and shell IPC guidance.
- `ydotool/references/testing.md`: recording, frame extraction and a worked real-input test session.
- `ydotool/agents/openai.yaml`: agent-facing display name and description.

Keep general usage instructions in the skill file and detailed desktop bindings in the reference document. The example scripts double as the tests: run them against open LibreOffice windows.

## Build, Test, and Development Commands

No build step or dependency installation is required; the diagnostic script uses Python's standard library.

- `python3 ydotool/scripts/inspect_desktop.py --help`: inspect supported arguments without connecting to desktop services.
- `python3 ydotool/scripts/inspect_desktop.py`: report binaries, device visibility, and socket connectivity without emitting input.
- `python3 ydotool/scripts/inspect_desktop.py --state`: read one Reach JSON snapshot.

Diagnostics return status `1` when connectivity fails. Missing services or sandbox access can cause this independently of code correctness.

## Coding Style & Naming Conventions

Follow the existing Python style: four-space indentation, snake_case names, and small functions. Preserve structured JSON diagnostic output, bounded socket reads, connection timeouts, and explicit error handling. No formatter or linter is configured.

Use descriptive Markdown headings, short instructions, and fenced shell examples. Preserve YAML metadata keys and keep agent descriptions consistent with the skill's scope.

## Testing Guidelines

No automated framework or coverage threshold is configured. For script changes, check syntax and run `--help`, then exercise diagnostics where the required desktop services are available. Verify both successful connections and unavailable-service behavior. For documentation changes, cross-check commands and shortcuts against local configuration and installed binaries.

## Commit & Pull Request Guidelines

Git history is unavailable in this workspace, so existing commit conventions cannot be confirmed. Use concise, imperative subjects such as `Document Reach socket diagnostics`.

PRs should explain the behavior changed, list validation performed, and identify environment limitations. Link relevant issues when available; include screenshots only for visible desktop behavior changes.

## Security & Configuration

Treat dated machine observations as temporary facts. Preserve explicit socket overrides and Nix executable paths. Diagnostics must remain read-only; do not add daemon startup, permission changes, or desktop input to inspection routines.
