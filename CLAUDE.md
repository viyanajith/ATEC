# Civilization ATEC: publishing folder

This folder is the PUBLIC face of Civilization ATEC: the download website and the release files.
The game's source code lives separately in `/Users/viyanajith/mc-clone-3d` (a Godot 4.7 project).
Same setup as Boolean Quest's `~/booleanquestGIT`.

## What's in here

- `docs/index.html`: the download website (GitHub Pages from `main` / `docs`).
  The `VERSIONS` list in its script fills the version selection bar; each entry's `tag`
  must be a GitHub release that has `CivilizationATEC.dmg` and `CivilizationATEC.exe` attached.
- `README.md`: the repo page on GitHub.
- `download_files/`: the built game (`CivilizationATEC.dmg`, `CivilizationATEC.exe`).
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
2. `gh release create <tag> download_files/CivilizationATEC.dmg download_files/CivilizationATEC.exe --title "Civilization ATEC <name>"`
3. Add a line at the top of `VERSIONS` in `docs/index.html`, commit, push.
