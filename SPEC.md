# The Polar Sprinter: project spec and Claude handoff

Updated 2026-10-29. This is the current handoff specification. The original brief is preserved in [PROMPT.md](PROMPT.md); its older design choices are superseded below.

## Current status: Workshop delivery is not working

David reports: "nothing you made actually works in the workshop."

Treat the existing deliverable as Blender source and unproven export candidates, not working Workshop items. No successful Dota 2 Item Tools compile, saved import session, in-game preview, or animation validation was demonstrated by the prior agent. No actual Workshop compiler error log has been captured in this handoff. The specific failure cause has not been diagnosed.

Prior reports of passing checks mean Blender FBX re-import, mesh/UV/weights checks, texture decoding and source reopening only. They do not prove Valve's importer accepts the files. Do not repeat those checks as evidence that Workshop works.

## Goal

Produce a Tinker cosmetic set that actually compiles and previews in the installed Dota 2 Workshop Item Tools. Preserve David's approved visual direction while correcting the asset pipeline. Stop before uploading or submitting to Steam unless David explicitly authorizes that separate step.

## Approved design

Tinker as an elite cross-country ski racer, with the pilot, beard, nose, mechanical arms and brass joints recognizable. Plain bib number 1. No athlete face, name, flags, brand lettering or sponsor logos.

- Back: Snowmaker Pack, a static turbine/fan, frost tank and feed hoses. Replaces the original brief's wax belt.
- Head: slim swept wraparound sunglasses with red/burgundy mirrored shading, narrow dark/red frame and slender temples. Not the old bulky glacier-blue goggles. Retain fitted red headband and number 1 clip.
- Weapon: right mechanical arm, slim pink-and-carbon pole, yellow accents/collar, dark grip, compact yellow racing basket and ferrule.
- Weapon Offhand: matching left pole and glove with wrist stopwatch. Preserve the static 00 display.
- Shoulders: red racing torso, sleeves and leg coverage, pale panels, glacier-blue piping, bib number 1 and static ECG detail. Check what each actual item slot hides; the authored body coverage has not been proven compatible with the in-game base hero or other items.
- Boots/skis: predominantly black race boot shells and tall black cuffs, yellow closures and toe/outer-foot accents; slim lime skis, original charcoal graphics, glacier tips and charcoal bindings. This is a separate provisional accessory, not an established community slot.

David approved the latest appearance on 2026-10-28. The current reference is the actual render below, not earlier generated concept art.

![Approved full set](previews/race_gear_lod0_threequarter.png)

See [gear details](docs/RACE-GEAR.md) and repository previews. Private athlete photographs are intentionally excluded from GitHub.

## Files and working environment

Local project root: `C:/Users/dsing/dota-tinker`.

Blender used: 4.2.3 LTS. Local executable: `C:/Program Files/Blender Foundation/Blender 4.2/blender.exe`.

[Download the source ZIP](https://github.com/yuichiromountainshiba/tinker-polar-sprinter/releases/download/race-gear-2026-10-28/polar_sprinter_blender_sources_2026-10-28.zip).

- `polar_sprinter_with_skis.blend`: full six-piece fitted scene, including the provisional Boots accessory.
- `polar_sprinter.blend`: five original-budget slots, without Boots.
- `assets/polar_sprinter_{back,head,weapon,offhand,shoulders,boots}.blend`: six editable item sources, each with LOD0 and LOD1 and packed texture atlases.
- `renders/`: previews; no proof of game rendering.
- `export/`: local five-slot FBX/TGA candidates. `prototypes/boots/`: separate provisional Boots candidates. These folders are in the local project, not the Blender source ZIP.
- `scripts/build_set.py`: five-piece geometry, binding, atlas/export orchestration. `scripts/build_boots.py`: provisional Boots geometry.
- `scripts/surfaces.py`: procedural materials and baked maps. `scripts/update_race_gear.py`: replaces revised items in both masters and renders previews.
- `scripts/verify_exports.py`, `verify_sources.py`, `verify_boots.py`, `verify_boots_source.py`: local checks only. Their use of the word import refers to Blender, not Valve Item Tools.
- `reference/valve/`: downloaded Valve source FBX and textures. `reference/tinker_reference.blend` and `tinker_studio.blend`: local reference scenes.
- `logs/`: local evidence. `archive/`: earlier revisions and pre-change backups. Preserve these before repairs.

The release ZIP contains 8 Blender files, 6 previews, validation records and a manifest. It does not contain the whole local project or build scripts. A Claude session on this PC should work from the local project; a remote session needs the source ZIP and any required local scripts/exports supplied separately.

## Historical numeric targets, not current importer proof

These targets were recorded from Valve documentation in October 2026. Recheck current official documentation and the installed importer before relying on them.

| Slot | Local LOD0 triangles | Local LOD1 triangles | Recorded target LOD0/LOD1 | Texture |
|---|---:|---:|---|---|
| Back | 876 | 463 | 1200 / 500 | 256 x 256 |
| Head | 1564 | 1128 | 3000 / 1200 | 512 x 512 |
| Weapon | 1964 | 1316 | 3500 / 1400 | 512 x 512 |
| Weapon Offhand | 2444 | 1316 | 3500 / 1400 | 512 x 512 |
| Shoulders | 2689 | 2689 | 5000 / 3000 | 512 x 512 |
| Provisional Boots | 1340 | 850 | No established Valve limits | 512 x 512, author choice |

Local exports have 49 skeleton bones. Prior checks claimed reference bone names/positions and normalized weights with at most four influences per vertex. These claims still need confirmation against actual compiler behavior.

## Known gaps and failure investigation

1. Reproduce David's failure in the actual installed Item Tools. Capture the exact slot, selected inputs, importer/tool version, full compiler log, and failure screenshot. No failure cause should be invented from this document.
2. Prove one simple supported slot end to end first, preferably Back: source export, Item Tools input assignment, compile, local preview and saved session. Make the smallest reproducible correction before rebuilding the entire set.
3. Inspect skeleton, bind pose, units/axes, transforms, FBX version/options, vertex weights, material assignments and per-slot attachment fields as possible failure points. These are investigation targets, not confirmed causes.
4. Validate current accepted texture extensions and shader inputs. Existing maps are RGB 24-bit TGA with separate color, normal, specularMask, specularExponent, rimMask, tintByBaseMask, selfIllumMask, metalnessMask, detailMask and diffuseWarpMask files. Suffixes are project conventions, not proven importer requirements. Do not assume every mask is supported for Tinker.
5. Normals are flat RGB 128,128,255, not sculpt-baked detail. Detail and diffuse-warp masks are zero. Blender procedural/mirror appearance does not prove in-game shader appearance.
6. Verify what hero meshes each slot replaces/hides. Check all custom suit coverage against the actual base mesh, both LODs and default animations.
7. Inspect the real Tinker slot list for Boots/Misc. The prior documentation review found no published community Boots budget and historical evidence of a Valve-only Misc slot. Do not promise six-piece Workshop support or force skis into another slot without verifying support and agreeing any design compromise with David.
8. Cold-blue laser, ice shards, animated snow emission/fan and cast-triggered ECG are not implemented. No custom ability effect support was established. Separate these aspirations from the static wearable delivery.
9. Remaining visible polish includes jagged yellow toe-panel texture boundaries, exposed base-hero heel patches and low-detail pole simplification. Correct them where the game preview confirms they matter.

## Completion evidence required

For each supported item: preserve the exact accepted source files, successful Item Tools compiler log, saved local import/session configuration and screenshot of the item on Tinker. Test both LODs; idle, run, attack, cast, portrait/loadout and combined wearables; verify materials, attachments, clipping and top-down readability in the game preview.

A successful Blender render or local FBX round trip cannot satisfy this gate. If a slot or effect is unsupported, identify it plainly and preserve the design source without calling it deliverable. Document any blocker with the exact observed error and next repair, not a generic import checklist.

## Prior notes and primary entry points

The notes below are historical research, not a current verification of the installed tool. Re-fetch relevant official pages during repair.

- [Original project brief](PROMPT.md)
- [Historical Valve rules research](docs/VALVE-RULES.md)
- [Boots slot uncertainty](docs/BOOTS-SLOT.md)
- [Current gear design](docs/RACE-GEAR.md)
- [Tinker requirements](https://www.dota2.com/workshop/requirements/tinker)
- [Modeling guide](https://help.steampowered.com/en/faqs/view/5FB8-4078-8B2A-C52B)
- [Shader masks](https://help.steampowered.com/en/faqs/view/299C-D7F9-09A5-98B6)
- [Item import guide](https://help.steampowered.com/en/faqs/view/3E00-D38F-B793-7384)

## Suggested instruction for Claude

> Read SPEC.md first. David reports that the existing exports do not work in Workshop. Preserve the approved design, reproduce the actual Item Tools failure and repair one supported item through a successful local compile and game preview before propagating changes. Inspect the local project scripts and source files. Do not treat previous Blender checks as Workshop validation, invent a Boots slot, or submit anything to Steam.
