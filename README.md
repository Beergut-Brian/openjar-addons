# openjar-addons

Shared Godot 4 addon for every Open Jar Games title. Games pull it in as a git submodule at
`addons/openjar/`, pinned to a tag:

```
git submodule add https://github.com/Beergut-Brian/openjar-addons addons/openjar
cd addons/openjar && git checkout v0.1.0
git submodule add https://github.com/Beergut-Brian/openjar-characters addons/openjar/characters
```

## What belongs here

Only things that are identical across games and that the template would otherwise copy:

| Folder | Holds | Status |
| --- | --- | --- |
| `addons/openjar/theme/` | The big-button UI theme (`openjar_theme.tres`), fonts, P1/P2 colour constants | TODO: first real asset from the launcher |
| `addons/openjar/ui/` | Pause menu, restart prompt, profile picker scenes used as-is by every game | TODO |
| `addons/openjar/launcher/` | `openjar_manifest.gd`: writes `store/openjar.json` at export; `launcher_bridge.gd`: reads `--profile=` and exits cleanly | TODO |
| `addons/openjar/characters/` | Submodule → `openjar-characters` | wire up after first tag |

The autoloads (`Players`, `Game`, `Save`, `Audio`, `Debug`) live in the **template**, not here, so a
game can edit them freely. If one proves identical across three games, move it here then.

## Rules
- Never break a tagged version. Games pin tags; bump the tag when anything changes.
- No game-specific logic. If only one game needs it, it goes in that game.
- Godot 4.7.2, same guardrails as the template `CLAUDE.md`.
