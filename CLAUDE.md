# Civilization ASEC: publishing folder

This folder is the PUBLIC face of Civilization ASEC: the download website and the release files.
The game's source code lives separately in `/Users/viyanajith/mc-clone-3d` (a Godot 4.7 project).
Same setup as Boolean Quest's `~/booleanquestGIT`.

## What's in here

- `docs/index.html`: the download website (GitHub Pages from `main` / `docs`).
  The `VERSIONS` list in its script fills the version selection bar; each entry's `tag`
  must be a GitHub release that has `CivilizationASEC.dmg` and `CivilizationASEC.exe` attached.
- `README.md`: the repo page on GitHub.
- `download_files/`: the built game (`CivilizationASEC.dmg`, `CivilizationASEC.exe`).
  NOT committed (gitignored, too big); attached to GitHub Releases instead.
- The donate button is Dad's job: its spot is marked `<!-- DONATE BUTTON GOES HERE (Dad) -->`.

## How to rebuild the game files

```
G=~/Downloads/Godot.app/Contents/MacOS/Godot
$G --headless --path ~/mc-clone-3d --export-release "macOS" ~/CivASEC_repo/download_files/CivilizationASEC.dmg
$G --headless --path ~/mc-clone-3d --export-release "Windows Desktop" ~/CivASEC_repo/download_files/CivilizationASEC.exe
```
Bump `config/version` in `mc-clone-3d/project.godot` (shown on the Create World screen) and the
versions in `mc-clone-3d/export_presets.cfg` first.

## Releasing a new version

1. Rebuild both files (above).
2. `gh release create <tag> download_files/CivilizationASEC.dmg download_files/CivilizationASEC.exe --title "Civilization ASEC <name>"`
3. Add a line at the top of `VERSIONS` in `docs/index.html`, commit, push.
