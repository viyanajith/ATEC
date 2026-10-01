# ATEC: publishing folder

ATEC (say it A-TE-K) = Advanced Technological Electrical Civilization. Renamed from
"Civilization ATEC" on 2026-09-29 because "Civilization" is Take-Two's video-game trademark:
keep "Civilization" out of the title; the long form as a subtitle is fine.

This folder is the PUBLIC face of ATEC: the download website and the release files.
The game's source code lives separately in `/Users/viyanajith/mc-clone-3d` (a Godot 4.7 project).
Same setup as Boolean Quest's `~/booleanquestGIT`.

## What's in here

- `docs/index.html`: the download website (GitHub Pages from `main` / `docs`).
  The `VERSIONS` list in its script fills the version selection bar; each entry's `tag`
  must be a GitHub release that has `ATEC.dmg` and `ATEC.exe` attached.
- `README.md`: the repo page on GitHub.
- `download_files/`: the built game (`ATEC.dmg`, `ATEC.exe`).
  NOT committed (gitignored, too big); attached to GitHub Releases instead.
- The donate button is Dad's job: its spot is marked `<!-- DONATE BUTTON GOES HERE (Dad) -->`.

## How to rebuild the game files

The build scripts live with the game, in `~/mc-clone-3d/tools/` (same recipe as Boolean Quest's):
```
~/mc-clone-3d/tools/make_fancy_dmg.sh     # Mac installer: drag-to-Applications window, wallpaper, app icon
~/mc-clone-3d/tools/make_windows_exe.sh   # Windows: one .exe with the icon on it
~/mc-clone-3d/tools/make_icons.sh         # only after changing app_icon.html or dmg_background.html
```
Both deliver into `download_files/`. Bump `config/version` in `mc-clone-3d/project.godot` (shown on
the Create World screen) and the versions in `mc-clone-3d/export_presets.cfg` first.

## Releasing a new version

1. Rebuild both files (above).
2. `gh release create <tag> download_files/ATEC.dmg download_files/ATEC.exe --title "ATEC <name>"`
3. Add a line at the top of `VERSIONS` in `docs/index.html`, commit, push.

## Versions (every update has a name)

| Version | Name | Status |
|---|---|---|
| Beta 1.0 | First Debug Release | out, 2026-09-29 (day 3) |
| Beta 1.1 | Performance Fix | out, 2026-09-30: worker-thread meshing, 5 LOD levels, simple shadows, AO, settings menu, death screen, clock |
| Beta 1.2 | Saving & Loading | out, 2026-10-01: 5 worlds, binary saves (blocks diff/whole, items, entities, state), tick order, /tick |
| Beta 1.3 | (not named yet) | next |
| Beta 1.4 | Sounds | planned |

On the website: `title` in each `VERSIONS` entry, and `NEXT` for the version being worked on.
When a version ships, move it from `NEXT` into `VERSIONS` and give the next one a name.
