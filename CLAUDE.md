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

## The browser version (`docs/play/`)

A Godot Web export (preset "Web", threads OFF: GitHub Pages can't send the cross-origin
headers a threaded build needs), behind the "▶ Play in your browser" button. To rebuild (user, 2026-11-11):
1. In `mc-clone-3d/project.godot`, under `[rendering]`, set `renderer/rendering_method` (and `.mobile`)
   to `"gl_compatibility"`.
2. `Godot --headless --path ~/mc-clone-3d --export-release "Web" ~/CivASEC_repo/docs/play/index.html`
3. Put the project BACK to Forward+ (remove those lines again).
In the browser the render distance starts at 5 instead of 10 (`world.gd` WEB_RENDER_DISTANCE), because it lagged.
The browser version is still **Beta 1.6** (user, 2026-11-12): 1.0 was released for Mac and Windows only, so
`docs/play/` was not rebuilt and its button says Beta 1.6.

## The phone version (`docs/mobile/`)

Beta 1.6 with touch controls, behind the "📱 Play on your phone" button (user, 2026-11-12). The 1.6
source was not kept, so it was RECOVERED from `docs/play/index.pck` with Godot RE Tools v2.7.4
(`--recover`; all 90 scripts decompiled, comments are gone) into `~/atec-beta-1.6-mobile`, a
separate project; the real game (`~/mc-clone-3d`) is 1.0 and was not touched.
Added there: `script/ui/touch_controls.gd` (the "TouchControls" autoload: joystick, drag to look,
MINE/USE/JUMP/SNEAK/INV/DROP/SWAP/'/'/pause, < > for the hotbar, Continue/Close in menus), and every
script's `Input.mouse_mode` goes through it (phones can't lock the mouse). Rebuild:
`Godot --headless --path ~/atec-beta-1.6-mobile --export-release "Web Mobile" ~/CivASEC_repo/docs/mobile/index.html`
(its preset has the phone texture formats and the on-screen keyboard on).

## Releasing a new version

1. Rebuild both files (above).
2. `gh release create <tag> download_files/ATEC.dmg download_files/ATEC.exe --title "ATEC <name>"`
3. Add a line at the top of `VERSIONS` in `docs/index.html`, commit, push.
(The site had a single ".pck" download button for a while on 2026-11-12; the user turned it back into the
Mac and Windows buttons the same day, and the ATEC.pck files were deleted from the releases again.)

## Versions (every update has a name)

| Version | Name | Status |
|---|---|---|
| Beta 1.0 | First Debug Release | out, 2026-09-29 (day 3) |
| Beta 1.1 | Performance Fix | out, 2026-09-30: worker-thread meshing, 5 LOD levels, simple shadows, AO, settings menu, death screen, clock |
| Beta 1.2 | Saving & Loading | out, 2026-10-01: 5 worlds, binary saves (blocks diff/whole, items, entities, state), tick order, /tick |
| Beta 1.3 | Sounds | out, 2026-10-03: footsteps + mining sounds (data/sounds/walking.json), mob sounds, volume slider, credits page |
| Beta 1.4 | Terrain | out, 2026-10-04: height limit 70 (was 35), Generation Order, natural structures: Hill, Mountain, River; Large Ocean biome |
| Beta 1.5 | Food Release | out, 2026-10-18: tall grass + seeds, hoe dirt, wheat/carrots, grinder, raw bread, electric oven + fire, harvester, smart porter, steady porters, bucket, breeding, ash, objectives on/off |
| Beta 1.6 | Adventure Release | out, 2026-11-11: the story (tribe, map, bunker, drill flight, Science Dome, Nick and Palios, Pluto), coal generator, battery in/out sides, nuclear reactor, battery compressor + stacks, reinforced iron, launchpad + engine frame, the probe and the gigacoil, caves, thirst, smoother loading |
| 1.0 | First Classic Update | out, 2026-11-12: the main theme (music/main_theme.wav, tools/make_ensemble.py), NS (newer-save copy check), mods (zip install, items/blocks, game code, data edits: newest installed wins), texture packs, bedrock floor (chunk format 3) |
| 2.0 | (not named yet) | next: the login system |

On the website: `title` in each `VERSIONS` entry, and `NEXT` for the version being worked on.
When a version ships, move it from `NEXT` into `VERSIONS` and give the next one a name.
