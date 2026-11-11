# openjar-addons

Shared Godot 4 addon for every Open Jar Games title. Games pull it in as a git submodule at
`addons/openjar/`, pinned to a tag:

```
git submodule add https://github.com/Beergut-Brian/openjar-addons addons/openjar
cd addons/openjar && git checkout v0.1.0
git submodule add https://github.com/Beergut-Brian/openjar-characters addons/openjar/characters
```

## Layout and mount

**The repository root is the addon root.** A game mounts the whole repo at `addons/openjar/`, so
every file here appears in the game at `res://addons/openjar/<path>`:

```
openjar-addons/ (repo)          ->  <game>/addons/openjar/ (submodule)
  plugin.cfg, plugin.gd         ->  res://addons/openjar/plugin.cfg
  tileworld/tile_world.gd       ->  res://addons/openjar/tileworld/tile_world.gd
  split_screen/, cutscene/, picto_bubble/, theme/, ui/, launcher/
  docs/                         ->  markdown only, nothing to import
  tests/                        ->  a separate Godot project (has its own project.godot): the
                                    game's editor skips it, see "Testing the addon"
```

Up to v0.1.0 the files sat under `addons/openjar/` inside this repo, which would have mounted as
`res://addons/openjar/addons/openjar/...`; 0.2.0 moves them to the root (see Decisions).

## What belongs here

Only things that are identical across games and that the template would otherwise copy:

| Folder | Holds | Status |
| --- | --- | --- |
| `theme/` | The big-button UI theme (`openjar_theme.tres`), fonts, P1/P2 colour constants | TODO: first real asset from the launcher |
| `ui/` | Pause menu, restart prompt, profile picker scenes used as-is by every game | TODO |
| `launcher/` | `openjar_manifest.gd`: writes `store/openjar.json` at export; `launcher_bridge.gd`: reads `--profile=` and exits cleanly | TODO |
| `characters/` | Submodule → `openjar-characters` | wire up after first tag |

The autoloads (`Players`, `Game`, `Save`, `Audio`, `Debug`) live in the **template**, not here, so a
game can edit them freely. If one proves identical across three games, move it here then.

## Rules
- Never break a tagged version. Games pin tags; bump the tag when anything changes.
- No game-specific logic. If only one game needs it, it goes in that game.
- Godot 4.7.2, same guardrails as the template `CLAUDE.md`.

## Decisions

- 2026-11-10: the repo root is the addon root (plugin.cfg at the top), because games mount the
  repo itself at `addons/openjar/` and The Hill already references `res://addons/openjar/<module>/`.
